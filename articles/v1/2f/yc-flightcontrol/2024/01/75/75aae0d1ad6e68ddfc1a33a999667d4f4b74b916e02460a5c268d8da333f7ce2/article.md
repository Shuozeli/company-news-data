---
schema_version: "1.0.0"
document_id: "75aae0d1ad6e68ddfc1a33a999667d4f4b74b916e02460a5c268d8da333f7ce2"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/nextjs-app-router-migration-the-good-bad-and-ugly"
published_at: "2024-01-29T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T21:33:41.699737+00:00"
content_hash: "sha256:6f64215b9e5b1a1051a089c987590b8311491317570af03b0f5e2ac7c1ff409a"
---

# Next.js App Router migration: the good, bad, and ugly

Last year, we rebuilt the Flightcontrol dashboard from scratch with[Next.js](https://nextjs.org/) App Router. The old dashboard was built with Next.js Pages Router. The old dashboard did the job, but the UI was designed by me, an engineer, and felt too much like a prototype. It was time to grow up and bring in some real design talent.


We partnered with Overnice to redesign the entire UI. They designed[an incredible work of art](https://www.overnice.com/case/product-for-flightcontrol) . While we loved it, it required some major changes because it wasn’t possible to build with Next.js Pages Router. We needed nested routing and shared layouts.


A full rewrite was required, so we considered all the React options at the time (April 2023): Next.js App Router, Remix, and TanStack Router for true Single Page App (SPA) architecture. App Router and React Server Components (RSC) seemed like the future because it’s part of React, and Next.js is the most popular framework. Although it was still bleeding edge, it seemed like the safest long term option.


The traditional SPA approach was attractive because RSC are complex and blends server and client. Having a pure client and clear separation from the backend has obvious benefits. We care tremendously about type safety, so[TanStack Router](https://tanstack.com/router/v1) was the only option. It seemed very promising, but it was still alpha at the time and unclear if or when it would reach production.


Unfortunately, we barely gave[Remix](https://remix.run/) any consideration. Partly because we already used[Blitz.js](https://blitzjs.com/) auth and RPC. So moving to Remix would also require changing these two parts of the stack that could otherwise remain with Next.js.


With Next.js App Router chosen, we got to work.


## The migration to Next.js App Router


The following points are directly about our experience using this for a web app dashboard. Undoubtedly, there are more good and bad things for other use cases.


### Good: layouts


We needed nested layouts for our right side panel UI and navigation.` /environments/\[envId\]` shows the environment details, and` /environments/\[envId\]/deployment/\[deployId\]` opens a side panel next to the environment details.


This was impossible to build with Pages Router, but doable with App Router. Each layout persists, so navigation between sibling pages does not unmount and remount the parent layout.


Although you can’t nest pages, so it was awkward to build this UI. The environment UI has to be inside the environment` layout.tsx` , with the environment` page.tsx` only containing` return null` .


### Good: flexibility of loading states


When navigating to a new page with React Suspense, you can show a loading spinner on the old UI or the new UI depending on the desired user experience. This is a React feature and is now usable in Next.js because App Router supports it.


The traditional spinner on the new route is easily achieved with a` <Suspense>` boundary around it.


The new possibility is using` React.useTransition()` on links to show a spinner in the old UI. Once the new UI is loaded, the UI switches instantly. The benefit is that the user can continue looking at useful information while the new page loads in the background.


The resulting UX is nice, but the developer experience is clumsy.


```text
import {useTransition} from "react"
import Link from "next/link"
import {useRouter} from "next/navigation"


function NavLink() {
const [isPending, startTransition] = useTransition()
const router = useRouter()


return <Link
href="/about"
onClick={() => startTransition(() => router.push("/about"))}
>
About
{isPending && <Spinner />}
</Link>
}
```


Keep in mind that you still need` <Suspense>` around the page for showing the spinner on that page if the user navigates directly to it, for example from a browser bookmark.


### Good: DX of initial data loading on the server


React Server Components have proved useful mainly for the DX of initial data loading. We’re using the following pattern, where basically every page is a Server Component that loads data and passes that to a client component.


```text
// page.tsx
import {ProjectPage} from './ProjectPage'
import {getProjectData} from '@/domain/project'


export default async function Page() {
const projectData = await getProjectData(/*args*/)
return <ProjectPage initialData={projectData} />
}
```


And then in the client component, we use TanStack Query for live data updates with polling. The initial data is passed to the` useQuery()` hook via the` initialData` option.


I expected to get better initial load performance since that was so highly marketed. But in reality, I can’t tell a difference between this and client side data loading.


At the end of the day, this DX may be slightly worse than just having` useQuery()` do the initial data fetch on the client. Because then you wouldn’t have to explicitly handle` initialData`


### Bad: have to add client side fetching for live UI updates


It seems like Server Components should be able to support the same stale-while-revalidate semantics as TanStack Query and also polling. But it doesn’t with Next.js.


You have to add client side data fetching for this. And we want this for almost everything in our UI. This results in a lot of duplication, as mentioned in the previous section about server-side data loading.


### Bad: server side errors easily swallowed or hidden


If something errors on the server and you haven’t added an` <ErrorBoundary />` in the proper spot, it will render the Suspense fallback instead and try to re-render that page on the client.


This results in errors being thrown and logged, but the UI appears to work fine. Overall, it’s very confusing and hard to trace.


### Bad: can’t implement route exit animations


We are using[Framer Motion](https://www.framer.com/motion/) for animations. It works great for route entry animations, but Next.js[is completely broken](https://github.com/vercel/next.js/issues/49279) when it comes to exit animations.


Framer Motion is doing its job, but Next.js does not persist the old layout id and kills the children too early.


### Bad: lack of routing type safety


Next.js has experimental built-in type safety but it has many limitations.


Fortunately, it’s not too hard to implement this in user land. In another post, I share[our full copy paste-able implementation for full routing type-safety](https://www.flightcontrol.dev/blog/fix-nextjs-routing-to-have-full-type-safety) .


### Ugly: abysmal dev server performance


It’s a lot better now than it was nine months ago, but it’s still unacceptably slow.


As one of our engineers put it, “the dev server performance is so bad, I would give up all the good features in a heartbeat to avoid it. I would even switch to an alternative framework just to avoid the Next.js dev server. I’d even switch to a different language. That’s how much I hate using Next.js’ App Router.”


### Ugly: dev server memory leak


Every 20 minutes or so, you have to restart the dev server because it crashes. And before it crashes, it progressively gets slower and slower as you make more changes.


### Ugly: hard to trace errors


Many errors you encounter are super vague, with no traceable call stack. Leaving you to trial and error like binary search by deleting half your app at a time.


### Ugly: it was marketed as production-ready way too early


It took almost a year after it was called production-ready for it to really be usable in production. There were so, so many bugs and issues early on. It was absolutely miserable. Thankfully, many of those are now fixed, but the bitter taste remains.


### Ugly: overcomplicated and opaque


All of the above leads us to the conclusion that Next.js is overly complex and complicated. When something goes wrong, there’s no way to work out why or how to fix it.


We have certainly wasted a lot of company money wrestling with it.


### Update: we upgraded to Next.js 14.1.1 with minimal improvement


We finally managed to upgrade to Next.js 14. The dev server still crashes, but less often. And the dev server is still painfully slow.


## We’d go back and choose Remix if we could


Aside from much better dev performance I think Remix has a better architecture and abstraction. For example, with Remix the user owns the client and server entry points. But Next.js owns everything, preventing you from doing anything they don’t explicitly allow, unless you use npm patches, which we’ve had to consistently do.


Of course Remix has its own warts, but I consistently see Remix users incredulous at things we Next.js users have to deal with. Hopefully the Next.js ship can get turned around.


Long live React!
