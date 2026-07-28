---
schema_version: "1.0.0"
document_id: "8dae288f707483711f478e79acf5c4e6d85e8aadfcd77877c0fc0c72a7af0686"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/secret-knowledge-to-self-host-nextjs"
published_at: "2024-07-10T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T22:01:08.511319+00:00"
content_hash: "sha256:f41a2cbfb4a52848e815a9fb7fc67d822addc6bd6fa648bd7d36693f3182013d"
---

# Secret knowledge to self-host Next.js

“Self-hosting” Next.js is commonly used to describe hosting it anywhere besides Vercel. In reality, it’s all just hosting, but whatever.


Vercel does a lot of magic for Next.js hosting, but they don’t share what they do or how you can replicate it.


Thankfully, Vercel has made some efforts to make sure all core functionality works with` next start` . But it’s not production ready out of the box unless you don’t have a CDN, only have 1 server instance, and don’t use image optimization.


This guide attempts to cover everything you need for deploying production Next.js outside Vercel to both servers and serverless.


-


Each of these arrow bullet points indicate an action you need to take


## Deploy Next.js to servers or serverless functions?


There’s no right answer here, only tradeoffs.


There are some exceptions, but these are the general rules.


Servers sound intimidating to people who have grown up on Vercel, because you hear about how much easier serverless is. But this rhetoric is misleading. The old fashioned way of manually managing virtual private servers (VPS), where you have to apply operating system patches, etc, is absolutely harder than serverless, but that is no longer the modern way to use servers. Today, those low level concerns are abstracted away by containerization, and this eliminates most of the infrastructure complexity of servers.


Most people using servers today are using “serverless containers,” where you just connect your code, set your CPU and memory, and git push. So from this perspective, servers are just as easy to deploy as serverless.


The infrastructure complexity for deploying Next.js serverlessly is much higher than that of a server with a CDN because the framework is very complex. See the[OpenNext architecture diagram](https://opennext.js.org/aws/inner_workings/architecture) .


The operational complexity of serverless is much higher, because serverless deployments are fine-grained, distributed, asynchronous applications. This article on the[Serverless Illusion](https://architectelevator.com/cloud/serverless-illusion/) explains more of the tradeoffs.


## Deploy to serverless functions


Next.js does not yet officially support deploying to serverless functions. Vercel does a lot of proprietary magic for their serverless deployments. But as of April, 2025 they have posted a[Deployment Adapters RFC](https://x.com/nextjs/status/1907491571152589124) that should be a huge help when shipped.


[OpenNext](https://open-next.js.org/) is a community adapter for converting Next.js builds into assets that can be deployed to serverless functions. It has a good number of production users. Because it’s not officially supported, keeping it working with each new Next.js version is a constant game of whack-a-mole, and breaking changes can occur with Next.js patch or minor releases. The Deployment Adapters RFC mentioned above will fix this too.


See the OpenNext documentation for all the information on serverless deployments with it.


[AWS Amplify](https://aws.amazon.com/amplify/) is another option for serverless deployments that works for some people. But some functionality is different than Vercel, may lag behind Next.js versions, and the deployed infrastructure is a black-box and not customizable.


## Deploy to servers


Deploying Next.js to servers is the only officially supported way to deploy Next.js outside of Vercel. But it’s not production-ready out of the box.


### Image optimization


Image optimization fully works, but **prior to Next.js v15** you need to install an extra dependency. The Next.js server will process images on-demand.


-


Install the` sharp` dependency to your app’s production dependencies (if not using v15+)


Without this, image optimization will work but will be slow and memory hungry because it uses code designed only for local development.


Alternatively, you can use a third-party service for image optimization by[configuring a custom loader in Next.js](https://nextjs.org/docs/app/api-reference/next-config-js/images#example-loader-configuration) .


### Caching Next.js data & ISR


By default, Next.js uses local filesystem cache. This is problematic for production when you have more than one instance running because each instance will have its own data and ISR cache. This can cause lots of weird behavior.


-


Configure a custom` cacheHandler` in` next.config.js` to use a durable cache like Redis. (see[Next.js docs](https://nextjs.org/docs/app/api-reference/next-config-js/incrementalCacheHandlerPath) )


-


Here’s the[official Redis cache handler example](https://github.com/vercel/next.js/tree/canary/examples/cache-handler-redis)


### CDN


You almost certainly want a CDN in front of your Next.js app to ensure blazing fast loading of static content and to reduce load on your servers.


CDNs might seem magical, but they are very simple. Any http request can include a` Cache-Control` header with any number of commands on where and when to cache responses. For example` Cache-Control: s-maxage=3600` tells the CDN to cache the response for 60 minutes.


Next.js automatically sets` Cache-control` headers for most things, but a few of them are actually set incorrectly :(


You need a CDN to take advantage of this, like[AWS CloudFront](https://aws.amazon.com/cloudfront/) ,[Cloudflare](https://www.cloudflare.com/) , or[Fastly](https://www.fastly.com/) .


**Important caveat if you are using ISR/stale-while-revalidate features** : you need a CDN that supports the` stale-while-revalidate` cache-control header, and as of this writing, only AWS CloudFront and Fastly support this. Cloudflare does not support it.


-


Add a CDN if your deployment platform doesn’t give you one automatically, and make sure it supports the` stale-while-revalidate` header if you are using ISR/stale-while-revalidate.


#### ISR & Stale-while-revalidate


Prior to v15, Next.js did not conform to the` stale-while-revalidate` specification defined in[RFC 5861](https://httpwg.org/specs/rfc5861.html#n-the-stale-while-revalidate-cache-control-extension) . By default Next.js returned headers like` s-maxage=60, stale-while-revalidate` which does not work anywhere except on Vercel. The latter part must have a time defined like` stale-while-revalidate=31536000` to work correctly.


-


If not using v15+, configure` experimental.swrDelta: 31536000` in` next.config.js` . This will fix SWR to include` stale-while-revalidate=31536000` .


-


If using v15+, you can customize the default expire time. See[Next.js docs](https://nextjs.org/docs/app/api-reference/config/next-config-js/expireTime) .


If you do manual revalidation with the Next.js` revalidate()` API, you’ll also need to invalidate that path on your CDN.


-


When using` revalidate()` , make sure to also invalidate that path on the CDN.


### Draft or Preview mode


Next.js draft and preview mode is a feature for bypassing the CDN and Next.js cache to force dynamic rendering and see changes before they are published. It’s often used in conjunction with content management systems.


It works by setting the` __prerender_bypass=SECRETVALUE` cookie in the user’s browser.


If you use this feature, you need to:


-


Configure your CDN to forward requests to the server when the` __prerender_bypass=SECRETVALUE` cookie is set. The value of the cookie changes with each build. While you can allow any value in that cookie to bypass the CDN, it gives attackers a way to force requests to your server. (see[Next.js docs](https://nextjs.org/docs/app/building-your-application/configuring/draft-mode) )


### Middleware


Next.js middleware fully works out of the box with servers. The middleware just runs on the server instead of the CDN when using Vercel.


### Redirects & rewrites


Next.js redirects and rewrites fully work out of the box. These are handled by the Next.js server instead of the CDN when using Vercel.


### Core web vitals


If you want to continue getting the core web vital metrics that Vercel provides, you can configure Next.js to send those metrics anywhere.


-


Add` useReportWebVitals()` to your code to report metrics to a third party analytics provider (see[Next.js docs](https://nextjs.org/docs/app/api-reference/functions/use-report-web-vitals) )


### Version skew protection


Next.js has built-in skew mitigation. It will automatically trigger a reload of assets on page navigation when detected.


Digression: server components are frustrating because they make users experience version skew with every single deployment you make because it’s constantly making version-specific requests to the server. This does not happen nearly as often with Pages Router because most of the static assets are loaded once and don’t need to be refetched.


### Other production tips


#### Minimum 2 instances


For production servers, you want a minimum of 2 instances running behind a load balancer so that if one crashes, there will still be a server serving traffic while the crashed one is automatically rebooted.


It’s better to have 2 smaller instances than 1 large one.


#### CPU & Memory consumption


For production, you likely want 1-2 CPU and 2-4 GB of memory. This range is a good starting point, and then you can adjust based on your specific compute usage.


#### Reduce deployment size


Next.js has a[standalone output mode](https://nextjs.org/docs/app/api-reference/next-config-js/output) that will trace dependencies and generate a standalone output folder that contains only required files instead of all of` node_modules` .


I don’t have experience with it, and I haven’t seen many others talking about it. So I don’t know how well it works. If you’ve used it, let me know!


## Join the conversation


Was this useful? Have a suggestion? Join the conversation on[Twitter](https://x.com/flybayer/status/1811400967956414648)[LinkedIn](https://www.linkedin.com/feed/update/urn:li:activity:7217167949457969152/) , or[Reddit](https://www.reddit.com/r/nextjs/comments/1e0qse4/secret_knowledge_to_selfhost_nextjs/) .
