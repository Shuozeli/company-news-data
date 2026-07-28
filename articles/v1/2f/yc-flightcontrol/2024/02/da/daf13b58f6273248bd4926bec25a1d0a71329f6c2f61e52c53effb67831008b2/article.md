---
schema_version: "1.0.0"
document_id: "daf13b58f6273248bd4926bec25a1d0a71329f6c2f61e52c53effb67831008b2"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/a-robust-system-to-handle-and-display-complex-errors"
published_at: "2024-02-15T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T21:33:41.699737+00:00"
content_hash: "sha256:dfbdb585f4afabd92fdc01f1338eee4428a6d4b52b4c2b54620f3a889024ee48"
---

# A robust system to handle and display complex errors

Here at Flightcontrol, it feels like errors are our daily nutrition. We are a layer on top of a user’s AWS account that provides delightful automation so users can focus on building product instead of infrastructure.


Our system is bombarded with expected and unexpected errors from all directions: users’ code failing to build or deploy, improper configuration, lots and lots of AWS edge cases, outages from third-party services, unexpected user actions, and even our own code.


Our users are technical, so it’s often beneficial to surface more information about the error than for a typical consumer app. These errors can originate from vastly different parts of the system. It’s critical to have a robust pattern to handle and display these throughout the app.


In this post, I detail the error system instituted by our senior engineer, Camila Rondinini.


## Goals for the error system


-


Gracefully handle all errors in a consistent way


-


Every error has a unique code for grep-ability


-


Users should immediately understand what happened and how to resolve it by displaying help info or links for resolving the issue


-


Track which part of the system the error originated from


-


Display all expected error information to users


-


Display only minimal details about unexpected errors and silently notify our engineering team


-


Easy for our developers to handle errors


-


Full type safety in our code


-


Centralized error dictionary


-


Store all errors in the database in a normalized format


-


Ability to retroactively change the displayed user content for errors that occurred in the past


## Typescript error system


To satisfy the above requirements, we need to track and store six pieces of information:


-


**Fault** : the high level system from which the error originated. Examples: Flightcontrol, AWS.


-


**Grouping** : the sub-category within that system. For Flightcontrol, that is normally our domain models like Deployment and Project. For AWS, it is specific AWS services like ECS.


-


**Code** : a unique and structured short string about the error.


-


**Original error** : the original error.


-


**Data** : additional data for displaying to the user.


-


**Metadata** : extra information primarily for internal debugging.


We then store that information in the database in an` error` field. Most of our primary models/tables have an` error` field.


### Defining errors


Code samples are available to[view and copy here](https://codesandbox.io/p/devbox/5fw323?file=%2FexampleUsage.test.ts%3A17%2C32) .


I’ll explain the main parts here.


At the top level, we have a` Fault` enum for the major system parts.


```text
// codes/faults.ts
export enum Fault {
AWS = "Aws",
FC = "FC",
Github = "Github",
ThirdParty = "ThirdParty",
}
```


The` ErrorType` type describes the serialized data as stored in the database.


```text
// lib/schema.ts
export type ErrorType<F extends Fault> = {
fault: F
grouping: string
code: string
type: string
data?: Record<string, string | Record<string, string>>
metadata?: Record<string, string | Record<string, string>>
}
```


The` codes/` folder has a file for each fault that describes the groupings and possible errors. This user facing error description info is not stored in the database, so updating it will apply to past errors as well.


```text
// codes/aws.ts


// Groupings
enum Service {
ECS = "ECS",
FARGATE = "Fargate",
IAM = "Iam",
CLOUDFRONT = "CLOUDFRONT",
CODEBUILD = "CODEBUILD",
VPC = "VPC",
}


// Possible errors
const Messages = {
[Service.IAM]: {
ACCESS_DENIED: ({ awsAccountId }: { awsAccountId?: string }) => ({
message: "AWS access denied",
description: `We are receiving Access Denied error from AWS. Please check if you have removed our authentication CloudFormation named "flightcontrol-access-${awsAccountId}" in "us-east-1". If this is unexpected, contact us for help.`,
action: {
label: "Contact support",
url: "https://www.flightcontrol.dev/docs/troubleshooting/contacting-support",
},
}),
},
//...
}
```


### Creating errors


Custom errors are created like this:


```text
import {Errors} from '@/error-library'


try {
// ...
} catch(error) {
throw new Errors.Aws.Iam.ACCESS_DENIED({
data: {
awsAccountId: awsAccount.id
},
metadata: {
timestamp: new Date().toISOString()
},
originalError: error,
})
}
```


And then saved in the database like so:


```text
await prisma.project.update({
where: {
id: projectId,
},
data: {
status: 'ERROR',
error: customError.getData(),
},
})
```


` error.getData()` returns a plain JavaScript object:


```text
{
"fault": "Aws",
"grouping": "IAM",
"code": "ACCESS_DENIED",
"type": "AwsIamError",
"data": {"awsAccountId": "189071383913"},
"metadata": {timestamp: "2024-02-02T17:47:47.604Z"}
"originalError": {/.../},
}
```


### Displaying errors


For displaying errors to the user:


```text
import {formatModelErrorForDisplay} from '@/error-library'


const userFacingErrorData = formatModelErrorForDisplay(project.error)
```


The user facing error data has this structure:


```text
export type UserFacingErrorData = {
message: string
code?: string
description?: string
action?: {url: string; label: string}
}


// Example
const userFacingErrorData = {
"code": "AWS:IAM:Error:ACCESS_DENIED",
"message": "AWS access denied",
"description": "We are receiving Access Denied error from AWS. Please check if you have removed our authentication CloudFormation named "flightcontrol-access-123456789" in "us-east-1". If this is unexpected, contact us for help.",
"action": {
"label": "Contact support",
"url": "https://www.flightcontrol.dev/docs/troubleshooting/contacting-support",
},
}
```


Here’s how we display the error in Flightcontrol:


## Summary


Some[code is available here](https://codesandbox.io/p/devbox/5fw323?file=%2FexampleUsage.test.ts%3A17%2C32) for you to view or copy and paste.


Our implementation in Flightcontrol is not perfect by any means. There are still many errors that need improvement. But this system makes it trivial for us to continue improving errors over time.


Let me know on[Twitter](https://twitter.com/flybayer) or[LinkedIn](https://www.linkedin.com/in/brandonbayer1/) if you’ve found this helpful!
