---
schema_version: "1.0.0"
document_id: "8db823187a24403871cab1424af507a41fc5e173357f9ed5a65db7348bae9c3b"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/add-type-safety-to-formiks-field-component"
published_at: "2024-06-20T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T22:01:08.511319+00:00"
content_hash: "sha256:f7ceef1f041c5c3ca5a980ad3ad7ae164b4b568a7f44aa3f80f587ef5016748e"
---

# Add Type Safety to Formik’s Field Component

[Formik](https://formik.org/) is one of the oldest and most used React form libraries. We use it for all our forms.


Unfortunately, it has only limited type safety by default.


This Typescript example is taken from their docs. In this example, **only** **` initialValues`** **and** **` onSubmit`** **is type safe** . The` Field` ’s` name` prop, for example, is not. The` name` prop is type` string` so you could add a name that is not in` MyFormValues` and your app will compile but totally fail at runtime.


```text
import * as React from 'react';
import {
Formik,
FormikHelpers,
FormikProps,
Form,
Field,
FieldProps,
} from 'formik';


interface MyFormValues {
firstName: string;
}


export const MyApp: React.FC<{}> = () => {
const initialValues: MyFormValues = { firstName: '' };
return (
<div>
<h1>My Example</h1>
<Formik
initialValues={initialValues}
onSubmit={(values, actions) => {
console.log({ values, actions });
alert(JSON.stringify(values, null, 2));
actions.setSubmitting(false);
}}
>
<Form>
<label htmlFor="firstName">First Name</label>
<Field id="firstName" name="firstName" placeholder="First Name" />
<button type="submit">Submit</button>
</Form>
</Formik>
</div>
);
};
```


## Type safety for <Field>


We implemented a user-land solution that adds full type safety to the` Field` component.


The new` makeForm()` utility takes a[Zod schema](https://zod.dev/) and returns the` Form` and` Field` components.


` Form` validation is automatically set to use that zod schema and to have` initialValues` and` onSubmit` typed based on that zod schema.


` Field` component is also now fully typed based on the zod schema.


It’s used like this:


```text
import {makeForm} from "@/form/Form"
import {z} from "zod"
import {FormField, FormInput, Button} from "@/component-library"


const ResetPasswordFormSchema = z.object({
password: z.string(),
token: z.string(),
})


const {Formik, Field} = makeForm({schema: ResetPasswordFormSchema})


export default function Page() {
// stuff
return (
<Formik
initialValues={{
password: "",
token: useSearchParams()?.get("token"),
}}
onSubmit={async (values, form) => {
try {
await resetPasswordMutation(values)
toast({
icon: "success",
description: "Saved new password",
})
} catch (error) {
handleFormErrors({error, setFieldError: form.setFieldError, values})
}
}}
children={(form) => (
<form onSubmit={form.handleSubmit} className="flex flex-col">
<Field
// 🔥 Fully type safe now!
name="password"
children={({field, meta}) => (
<FormField label="Your new password" error={meta.touched && meta.error}>
<FormInput {...field} type="password" />
</FormField>
)}
/>


<Button type="submit" disabled={form.isSubmitting} spin={form.isSubmitting}>
Set password
</Button>
</form>
)}
/>
)
}
```


## Preserve types with nested form components


For large forms, it’s often beneficial to abstract some of the fields into another component, but you still want type safety.


Here’s how to do that.


The` <AbstractedFields>` component should take` form` and` Field` as components.


```text
import {makeForm, FormikProps, FieldComponent} from "@/form/Form"
import {FormField, FormInput, Button} from "@/component-library"


// Same makeForm usage at the top level
const {Formik, Field} = makeForm({schema: MyFormSchema})


export function Form() {
// stuff
return (
<Formik
initialValues={initialValues}
onSubmit={onSubmit}
children={(form) => (
<form onSubmit={form.handleSubmit}>
{/* 🔥 pass in form and Field  */}
<AbstractedFields form={form} Field={Field} />
</form>
)}
/>
)
}


export type AbstractedFieldsProps = {
form: FormikProps<typeof MyFormSchema>
Field: FieldComponent<typeof MyFormSchema>
}


const AbstractedFields = ({form, Field}: AbstractedFieldsProps) => {
// 🔥 form can be used in here with type safety
return (
<Field
// 🔥 Still has type safety
name="myFieldName"
children={({field, meta}) => (
<FormField label="My Field Name" error={meta.touched && meta.error}>
<FormInput placeholder="Web server" {...field} disabled={disabled} />
</FormField>
)}
/>
)
}
```


## All the code you need


Here’s all the code for the` makeForm` utility above. It's not for the faint of heart 😅


[This code is also available in this Typescript Playground](https://www.typescriptlang.org/play/?#code/PTAEGcCcGNgMwPaQLbAGJOQOgC7gB4BQARAK7gCmo0ANgJYUB2OxhdyADkjqAN6GhQaBjQAmAYQSM4dAOYAaAUJGiACpAQdwiwRhR0A1pOlydQzIfWbtSvckMA1AIY1SFG4IDiTCpDrRhCjEACQAVAFkAGQBBHBw-ACNSHHczQLFQJ3BQAHk-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-QB-ywHNigcUA2q6t17pHEBqmFhqGCQpEgHAAYVBHLGBSHyOjzkCNyO1lDdcVVYaGwRqbTGTrHWcswFhqQOG8ZHtsCoH9JkjNKsU+eplXdUMzvYccbUdg+UCpVcK0V4reC2xFjUUkvnJWgB2BG-TzrmCojdaqz1mqdPoKZjwCY4BSA0B4FCU1jlSQcoMAunAPL80i17FajDohsvzu5ZAXl7q1Uau9Z+4rNNK43szsl1LOAmVAA) .


```text
// src/form/Form.tsx
"use client"
import {
FieldConfig,
FieldProps,
FormikConfig,
FormikProps,
FormikValues,
GenericFieldHTMLAttributes,
Field as OrigField,
Formik as OrigFormik,
} from "formik"
import React from 'react'
import {ZodError, ZodSchema, z} from "zod"


export type DeepKeys<T> = unknown extends T
? string
: // eslint-disable-next-line
T extends readonly any[]
? DeepKeysPrefix<T, keyof T>
: T extends object
? Exclude<keyof T, ObjectKeys<T>> | DeepKeysPrefix<T, keyof T>
: never


type DeepKeysPrefix<T, TPrefix> = TPrefix extends keyof T & (number | string)
? `${TPrefix}.${DeepKeys<T[TPrefix]> & string}`
: never


type ObjectKeys<T> = {
[K in keyof T]: T[K] extends object ? K : never
}[keyof T]


export type DeepValue<T, TProp> = T extends Record<string | number, any>
? TProp extends `${infer TBranch}.${infer TDeepProp}`
? DeepValue<T[TBranch], TDeepProp>
: T[TProp & string]
: never


export type FieldAttributes<
FormValues extends FormikValues,
Name extends DeepKeys<FormValues> = DeepKeys<FormValues>,
> = Omit<GenericFieldHTMLAttributes, "children"> &
Omit<FieldConfig, "name" | "component" | "as" | "render" | "children"> & {
children: (props: FieldProps<DeepValue<FormValues, Name>, FormValues>) => React.JSX.Element
name: Name
}


type FormikFormComponent<FormValues extends Record<string, unknown>> = React.FC<
FormikConfig<FormValues> & {
initialValues?: FormValues
}
>


export const validateZodSchema =
(schema: ZodSchema | undefined) => async (values: Record<string, unknown>) => {
if (!schema) {
return {}
}
try {
await schema.parseAsync(values)
return {}
} catch (error: any) {
return formatZodError(error)
}
}


export function formatZodError(error: ZodError) {
if (!error || typeof error.format !== "function") {
throw new Error("The argument to formatZodError must be a zod error with error.format()")
}


const errors = error.format()
return recursiveFormatZodErrors(errors)
}


export function recursiveFormatZodErrors(errors: any) {
let formattedErrors: Record<string, any> = {}


for (const key in errors) {
if (key === "_errors") {
continue
}


if (errors[key]?._errors?.[0]) {
if (!isNaN(key as any) && !Array.isArray(formattedErrors)) {
formattedErrors = []
}
// @ts-expect-error this looks like a mistake from `formattedErrors = []` above
formattedErrors[key] = errors[key]._errors[0]
} else {
if (!isNaN(key as any) && !Array.isArray(formattedErrors)) {
formattedErrors = []
}
// @ts-expect-error this looks like a mistake from `formattedErrors = []` above
formattedErrors[key] = recursiveFormatZodErrors(errors[key])
}
}


return formattedErrors
}


function formikFactory<S extends z.ZodTypeAny>(schema: S): FormikFormComponent<z.input<S>> {
return function CustomFormik({
children,
...props
}: FormikConfig<z.input<S>> & {initialValues?: number}) {
return (
<OrigFormik
validate={validateZodSchema(schema)}
{...props}
children={(form) => children && typeof children === "function" && children(form)}
/>
)
}
}
function fieldFactory<
FormValues extends FormikValues,
Name extends DeepKeys<FormValues> = DeepKeys<FormValues>,
>() {
return function CustomField<N extends Name>(props: FieldAttributes<FormValues, N>) {
return <OrigField {...props} />
}
}


export type FieldComponent<FormValues extends Record<string, unknown>> = <
N extends DeepKeys<FormValues>,
>(
props: FieldAttributes<FormValues, N>,
) => JSX.Element


export interface FormikContext<FormValues extends Record<string, unknown>> {
Formik: FormikFormComponent<FormValues>
Field: FieldComponent<FormValues>
}


export function makeForm<S extends z.ZodTypeAny>({schema}: {schema: S}): FormikContext<z.input<S>> {
const result = {
Formik: formikFactory(schema),
Field: fieldFactory<z.input<S>>(),
}
return result
}
```
