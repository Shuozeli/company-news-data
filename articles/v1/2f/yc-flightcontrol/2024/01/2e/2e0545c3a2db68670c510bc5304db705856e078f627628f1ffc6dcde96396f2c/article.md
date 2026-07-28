---
schema_version: "1.0.0"
document_id: "2e0545c3a2db68670c510bc5304db705856e078f627628f1ffc6dcde96396f2c"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/fix-nextjs-routing-to-have-full-type-safety"
published_at: "2024-01-16T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T21:33:41.699737+00:00"
content_hash: "sha256:2a823b08dd0b6bb05481726ff9b7b5c0745cb57d9ffcca4c5f3ea8092dd41bb1"
---

# Fix Next.js routing to have full type-safety

Broken links, incorrectly formatted query strings, and missing route parameters are all easily solvable with a type system like Typescript.


Sadly, most modern routing solutions, including Next.js, don’t include this, leaving us sad and alone on a cold, dark night.


## Next.js has limited built-in type safety


Next.js has an opt-in experimental feature for[statically typed links](https://nextjs.org/docs/app/building-your-application/configuring/typescript#statically-typed-links) . To enable this, turn on` experimental.typedRoutes` in your` next.config.js` like so:


```text
/** @type {import('next').NextConfig} */
const nextConfig = {
experimental: {
typedRoutes: true,
},
}


module.exports = nextConfig
```


Now Next.js will generate link definitions in` .next/types` that will override the default type of the` href` prop on the` <Link />` component.


```text
import Link from 'next/link'


// No TypeScript errors if href is a valid route
<Link href="/about" />


// TypeScript error
<Link href="/aboot" />
```


This is a good start, but it has many limitations:


-


no type validation of route or query string parameters


-


no runtime validation of route or query string parameters


-


no autocomplete for dynamic routes — very cumbersome in a large application with many dynamic routes


-


no type validation at all when passing href as an object like` <Link href={{href: '/about', query: {ref: 'hello'}}} />` (but I don’t think this even works anymore in app router)


-


no type or runtime validation for` useParams()` and` useSearchParams`


-


it couples the page reference to the route string — if you restructure your routes, you must also change all the links


## Ideal type-safe routing for Next.js


A fully featured type-safe routing system should support the following:


-


static type validation of routes


-


static type validation of route parameters


-


static type validation of query string parameters


-


runtime validation of route parameters


-


runtime validation of query string parameters


-


decouple route names from the route urls (this makes it easy to restructure urls without having to update links everywhere)


-


type safe` useParams()` and` useSearchParams()`


-


easily re-use route parameter types for Page props


To achieve both type and runtime validation, we’ll use the excellent[Zod](https://github.com/colinhacks/zod) library.


### Dynamic routes


We want a route definition interface that looks like this:


```text
//routes.ts
import {z} from 'zod'


export const OrgParams = z.object({orgId: z.string()})


export const Routes = {
home: makeRoute(({orgId}) => `/org/${orgId}`, OrgParams)
}
```


And that can be used like this:


```text
import Link from 'next/link'
import {Routes} from '../../routes.ts'


<Link href={Routes.home({orgId: 'g4eion3e3'})} />
```


### Static routes


That same interface will work for static routes:


```text
//routes.ts
import {z} from 'zod'


export const Routes = {
about: makeRoute(() => `/about`, z.object({}) /* no params */)
}
```


That can be used like this:


```text
import Link from 'next/link'
import {Routes} from '../../routes.ts'


<Link href={Routes.about()} />
```


### Query parameters


And that can be extended for query parameters like so:


```text
//routes.ts
import {z} from 'zod'


export const SignupSearchParams = z.object({
invitationId: z.string().optional().nullable(),
})


export const Routes = {
signup: makeRoute(() => "/signup", z.object({}), SignupSearchParams),
}
```


And that can be used like this:


```text
import Link from 'next/link'
import {Routes} from '../../routes.ts'


<Link href={Routes.signup({}, {search: {invitationId: '8haf3dx'}})} />
```


### useParams()


You can read the route parameters from the` Routes` object too. Fully type-safe and runtime-validated.


```text
import {Routes} from '../../routes.ts'


// type = {orgId: string}
const params = Routes.home.useParams()
```


### useSearchParams()


You can even read the query parameters from` Routes` . Fully type-safe and runtime-validated.


```text
import {Routes} from '../../routes.ts'


// type = {invitationId: string}
const searchParams = Routes.signup.useSearchParams()
```


### Page prop types


` Routes` also provides the page prop types:


```text
import {Routes} from '../../routes.ts'


type HomePageProps = {
params: typeof Routes.home.params
}


export default async function HomePage({
params: {organizationId},
}: HomePageProps) {
// render stuff
}
```


### Page prop runtime validation


And` Routes` let's you validate the page props


```text
import {Routes} from '../../routes.ts'


type HomePageProps = {
params: typeof Routes.home.params
}


export default async function HomePage({params}: HomePageProps) {
const safeParams = Routes.home.parse(params)


// render stuff
}
```


## The makeRoute() utility


Here’s the only utility code you need to accomplish the above.


```text
npm install zod query-string
```


```text
import {z} from 'zod'
import {useParams as useNextParams, useSearchParams as useNextSearchParams} from "next/navigation"
import queryString from "query-string"


export const OrgParams = z.object({orgId: z.string()})


export const Routes = {
home: makeRoute(({orgId}) => `/org/${orgId}`, OrgParams)
}


type RouteBuilder<Params extends z.ZodSchema, Search extends z.ZodSchema> = {
(p?: z.input<Params>, options?: {search?: z.input<Search>}): string
parse: (input: z.input<Params>) => z.output<Params>
useParams: () => z.output<Params>
useSearchParams: () => z.output<Search>
params: z.output<Params>
}


const empty: z.ZodSchema = z.object({})


function makeRoute<Params extends z.ZodSchema, Search extends z.ZodSchema>(
fn: (p: z.input<Params>) => string,
paramsSchema: Params = empty as Params,
search: Search = empty as Search,
): RouteBuilder<Params, Search> {
const routeBuilder: RouteBuilder<Params, Search> = (params, options) => {
const baseUrl = fn(params)
const searchString = options?.search && queryString.stringify(options.search)
return [baseUrl, searchString ? `?${searchString}` : ""].join("")
}


routeBuilder.parse = function parse(args: z.input<Params>): z.output<Params> {
const res = paramsSchema.safeParse(args)
if (!res.success) {
const routeName =
Object.entries(Routes).find(([, route]) => (route as unknown) === routeBuilder)?.[0] ||
"(unknown route)"
throw new Error(`Invalid route params for route ${routeName}: ${res.error.message}`)
}
return res.data
}


routeBuilder.useParams = function useParams(): z.output<Params> {
const res = paramsSchema.safeParse(useNextParams())
if (!res.success) {
const routeName =
"(unknown route)"
}
return res.data
}


routeBuilder.useSearchParams = function useSearchParams(): z.output<Search> {
const res = search.safeParse(convertURLSearchParamsToObject(useNextSearchParams()))
if (!res.success) {
const routeName =
"(unknown route)"
throw new Error(`Invalid search params for route ${routeName}: ${res.error.message}`)
}
return res.data
}


// set the type
routeBuilder.params = undefined as z.output<Params>
// set the runtime getter
Object.defineProperty(routeBuilder, "params", {
get() {
throw new Error(
"Routes.[route].params is only for type usage, not runtime. Use it like `typeof Routes.[routes].params`",
)
},
})


return routeBuilder
}


export function convertURLSearchParamsToObject(
params: ReadonlyURLSearchParams | null,
): Record<string, string | string[]> {
if (!params) {
return {}
}


const obj: Record<string, string | string[]> = {}
for (const [key, value] of params.entries()) {
if (params.getAll(key).length > 1) {
obj[key] = params.getAll(key)
} else {
obj[key] = value
}
}
return obj
}
```


### Bonus for number and boolean query strings


Search query parameters are always typed as strings in the browser, so for numbers and booleans you’ll need to use zod's` coerce` feature like this:


```text
export const LogsSearchParams = z.object({
logsId: z.coerce.number()
fullscreen: z.coerce.boolean().default(false),
})
```
