---
schema_version: "1.0.0"
document_id: "2bb79513c80a53ab0619c384c63495ddd06313e5f82afc031febcc17777da84a"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/temporal-error-handling-in-practice"
published_at: "2024-03-11T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T22:26:08.375343+00:00"
content_hash: "sha256:7ead1140a28c954631d89752ccb28d2655c1b2c299ae9cae1022dec6893abf87"
---

# Temporal Error Handling In Practice

[Temporal](https://temporal.io/) is an extremely powerful workflow orchestrator. It’s an open-source version of the system created at Uber. At Flightcontrol, we use it to manage all our backend workflows, like provisioning infrastructure and managing deployment pipelines.


Temporal’s error handling is also powerful, but it’s complex and takes some time to wrap your mind around. I recently wrote about[our custom error handling system](https://www.flightcontrol.dev/blog/a-robust-system-to-handle-and-display-complex-errors) for managing and displaying complex errors. In the post, I show how we integrate our custom errors into Temporal.


If you’re unfamiliar with Temporal, the two core concepts are Workflows and Activities. A Workflow is a durable execution function that can execute Activities or other Workflows. Workflows are a special environment to orchestrate non-async logic. All async logic lives in Activities.


## Basics of Temporal’s errors


Errors thrown in workflows and activities are:


-


Serialized because Temporal is a distributed event-driven system and every execution in the workflow is actually a gRPC call. Any custom errors you add must account for this.


-


Retried by default according to your retry policy unless you throw a` nonRetryableApplicationFailure` .


-


Wrapped at every level. For example, if you have a workflow that calls a child workflow that calls an activity and that activity fails, you read the original error in the top level workflow with` error.cause.cause` . The chain is essentially` ChildWorkflowFailure.ActivityFailure.\[orignalError as ApplicationFailure\]`


Errors thrown in activities are:


-


Converted to an` ApplicationFailure` and then wrapped in an` ActivityFailure` . To read the original error from a workflow, you need to read` error.cause` .


For more information, see[the Temporal documentation](https://docs.temporal.io/references/failures) .


## 4 main Temporal error cases


You need to account for each of the four primary error cases:


-


Error is thrown inside a workflow


-


Error is thrown inside an activity


-


Error is thrown inside a child workflow


-


Error is thrown inside an activity in a child workflow


## Requirements for handling our custom errors


-


We want our custom error data to be serialized and transmitted over the network.


-


So we must convert` CustomError` to` ApplicationFailure` and set our custom data in the` .details` field.


-


There is the option of using a custom converter (` FailureConverter` ), but there is not enough documentation or examples for us to figure it out.


-


We don’t want expected terminal errors to be retried. Because for example, broken code is not going to resolve itself by trying to compile it again.


-


So we must convert our` CustomError` to` ApplicationFailure.nonRetryable` (in the future, we can expand` CustomError` to support retries for specific ones).


-


We don’t want error wrapping (the` error.cause.cause.cause` mentioned above).


-


So we must unwrap at each level


## Use Temporal Interceptors to customize error handling


Temporal[Interceptors](https://docs.temporal.io/dev-guide/typescript/features#interceptors) are middleware you can add to run custom code before or after workflows and activities. They work perfectly for customizing the error handling.


### Activity Interceptor


This activity interceptor meets requirements 1 and 2 from above for when a custom error is thrown from an activity. It converts` CustomError` to` ApplicationFailure.nonRetryable` and passes along the` CustomError` type string and the custom data.


```text
import {ApplicationFailure, Context} from "@temporalio/activity"
import {ActivityExecuteInput, ActivityInboundCallsInterceptor, Next} from "@temporalio/worker"
import {CustomError} from "../../../shared/domain/errorLibrary/codes/customErrorClass"


/** Get the current Activity context with an attached logger */
export function getContext(): Context {
return Context.current()
}


export class ActivityInboundInterceptor implements ActivityInboundCallsInterceptor {
constructor(_ctx: Context) {}


async execute(
input: ActivityExecuteInput,
next: Next<ActivityInboundCallsInterceptor, "execute">,
): Promise<unknown> {
try {
const res = await next(input)
return res
} catch (error) {
if (error instanceof CustomError) {
throw ApplicationFailure.nonRetryable(error.message, error.getData().type, error.getData())
}


throw error
}
}
}
```


### Workflow Interceptor


This workflow interceptor meets requirements 1 and 2 for when a custom error is thrown from a workflow or a child workflow. Now requirements 1 and 2 are solved for all four cases.


Lastly, this meets requirement #3 to unwrap errors and pass along the original` ApplicationFailure` instead of a nested one.


```text
import {
ApplicationFailure,
CancelledFailure,
ContinueAsNew,
Next,
TemporalFailure,
TerminatedFailure,
TimeoutFailure,
WorkflowExecuteInput,
WorkflowInboundCallsInterceptor,
} from "@temporalio/workflow"
import {ErrorData} from "../../../shared/domain/errorLibrary/codes/ErrorData"
import {isCustomErrorData} from "../../../shared/domain/errorLibrary/helpers/isCustomErrorData"
import {getRootCauseMessage} from "../errors/userReadableError"


export class WorkflowErrorInterceptor implements WorkflowInboundCallsInterceptor {
async execute(
input: WorkflowExecuteInput,
next: Next<WorkflowInboundCallsInterceptor, "execute">,
): Promise<unknown> {
try {
return await next(input)
} catch (error) {


// Pass along native errors
if (
isTemporalNativeError(error) ||
error instanceof TemporalFailure && isTemporalNativeError(error.cause)
) {
throw error
}


// When CustomError is thrown in this workflow
if (error instanceof CustomError) {
throw ApplicationFailure.nonRetryable(
error.message,
error.getData().type,
error.getData(),
)
}


// When CustomError is thrown in an activity at this level
// Throw the ApplicationFailure so it doesn't get converted to an ActivityFailure
if (error instanceof ApplicationFailure) {
const customErrorData = extractCustomErrorDataFromApplicationFailure(error)
if (customErrorData) {
throw error
}
}


// When CustomError is thrown in a child workflow
// Unwrap the custom error and convert to ApplicationFailure
if (error instanceof TemporalFailure && error.cause instanceof CustomError) {
throw ApplicationFailure.nonRetryable(
error.cause.message,
error.cause.getData().type,
error.cause.getData(),
)
}


// When CustomError is thrown in an activity inside a child workflow
/     // Unwrap the ApplicationFailure
if (
error instanceof TemporalFailure &&
error.cause instanceof ApplicationFailure
) {
const customErrorData = extractCustomErrorDataFromApplicationFailure(error.cause)
if (customErrorData) {
throw error.cause
}
}


const errorMessage = getRootCauseMessage(error) || "Unknown error"


throw ApplicationFailure.nonRetryable(errorMessage, "Unknown Workflow Error")
}
}
}


export const isTemporalNativeError = (error: unknown): boolean => {
if (error instanceof ContinueAsNew) {
return true
}


if (error instanceof CancelledFailure) {
return true
}


if (error instanceof TerminatedFailure) {
return true
}


if (error instanceof TimeoutFailure) {
return true
}


return false
}


export function extractCustomErrorDataFromApplicationFailure(
error: ApplicationFailure,
): ErrorData | undefined {
if (!("details" in error)) {
return
}


const details = error.details
if (!details || details.length !== 1) {
return
}


const errorDetails = details[0]
if (!isCustomErrorData(errorDetails)) {
return
}


return errorDetails
}
```


## Saving the custom error data


Those two interceptors allow us to throw a custom error anywhere and then capture and save it in one place, the top level workflow.


Here’s an example in our` environmentDeploymentWorkflow.ts`


```text
} catch (error) {
await signalEvent(DeploymentEventType.DeploymentFailure)


const customErrorData = extractCustomErrorData(error)
if (customErrorData) {
// an activity that saves the error in the database
await saveDeploymentError({
deploymentId,
error: [],
errorData: customErrorData,
})
}
throw err
}
```


Here’s the code for the` extractCustomErrorData()` utility:


```text
import {CustomError} from "@fc/shared/domain/errorLibrary/codes/customErrorClass"
import {ApplicationFailure, TemporalFailure} from "@temporalio/common"
import {ErrorData} from "../../../shared/domain/errorLibrary/codes/ErrorData"


export function extractCustomErrorData(error: unknown): ErrorData | undefined {
if (error instanceof CustomError) {
return error.getData()
}


if (error instanceof TemporalFailure) {
if (isApplicationFailure(error)) {
return extractCustomErrorDataFromApplicationFailure(error)
}


if (hasApplicationFailureCause(error)) {
return extractCustomErrorDataFromApplicationFailure(error.cause)
}
}
}


function isApplicationFailure(error: unknown): error is ApplicationFailure {
return error instanceof ApplicationFailure
}


function hasApplicationFailureCause(
error: TemporalFailure,
): error is TemporalFailure & {cause: ApplicationFailure} {
if (!error.cause) {
return false
}


return isApplicationFailure(error.cause)
}


export function extractCustomErrorApplicationFailureFromTemporalFailure(
error: unknown,
): ApplicationFailure | undefined {
if (error instanceof TemporalFailure && error.cause instanceof ApplicationFailure) {
if (!customErrorData) {
return
}


return error.cause
}
}


export function extractCustomErrorDataFromApplicationFailure(
error: ApplicationFailure,
): ErrorData | undefined {
if (!("details" in error)) {
return
}


const details = error.details
if (!details || details.length !== 1) {
return
}


const errorDetails = details[0]
if (!isCustomErrorData(errorDetails)) {
return
}


return errorDetails
}
```


## Closing


Hopefully, this was helpful! Let me know on[Twitter](https://twitter.com/flybayer) or[LinkedIn](https://www.linkedin.com/in/brandonbayer1/) if you have any questions or feedback.
