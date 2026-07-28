---
schema_version: "1.0.0"
document_id: "0f6b167c48705a7ae5ed9dd8e43fa831abede017b50ea0cf3a848895776bc8e5"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/we-migrated-from-planetscale-to-aws-aurora-v2"
published_at: "2024-02-22T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T21:33:41.699737+00:00"
content_hash: "sha256:a0b0e51607ef21203acae5ca06ea775c4e6e944ee406652c37e2e4951e7c6cbf"
---

# We migrated from PlanetScale to AWS Aurora v2

On January 20, 2024, we moved our production database from PlanetScale to AWS Aurora RDS, a move that I did not personally anticipate to happen for at least two more years, if at all.


The main reasons are:


-


We want a serverless database with autoscaling. PlanetScale was originally marketed as this, but they’ve sunset the serverless offering. Now you have to manually monitor and adjust your CPU and memory.


-


Public databases only, with no private networking option on the Scaler plans, you need a single tenant setup, which is available as part of the PlanetScale enterprise offering


-


No control over the underlying server resources, as it is a multi-tenant shared cluster


-


Pricing generally is not clear and transparent, and you pay a lot of money for something like backup storage


## The History


In late 2021, when we started building Flightcontrol, we chose the following stack:


-


Next.js/Blitz.js for the web application hosted on AWS ECS Fargate


-


Temporal with the TypeScript SDK for our CI pipelines hosted on AWS ECS Fargate


-


Postgres for our database hosted on AWS RDS


During this time, my main concern about that stack was the database. Databases keep me up at night, and we are a small team of two, and I do not want to be managing any servers. I know RDS is a managed service, but still, it is a fixed-size single node that does not scale with any traffic increase.


We wanted a serverless solution, and the options available during this time were mainly Aurora Serverless v1. I had first-hand experience with Aurora Serverless v1, and it was the worst experience I ever had with databases.


The two of us were talking, and I remember Brandon mentioning PlanetScale. Immediately, the product and the idea intrigued me. It is a database service that is serverless, and you are charged for the number of rows read or write. That is a dream come true for me. It supports MySQL only, but the benefits of having a serverless database where I do not need to worry about scaling issues were intriguing.


We have been using PlanetScale since then to host our production database on their Scaler Plan (originally branded Team plan).


## PlanetScale introduces Scaler Pro plans


On July 6, 2023,[PlanetScale announced the new Scaler Pro](https://planetscale.com/blog/announcing-scaler-pro) plans, and with this introduction, PlanetScale’s positioning started to change. Here is the quote from the announcement post:


> As we've onboarded thousands of customers, large and small, one of the most common pieces of feedback people have given is that they're unsure how to map our pricing model onto their business. Reads and writes are easy to understand conceptually, but they don't map back to capacity planning that businesses are accustomed to. Many customers want more control than the traditional serverless model provides and clarity on how it compares to products like Amazon RDS and Google Cloud SQL.
>
>
> PlanetScale announcement


This is a shift in the product and the main selling point for us, where they are no longer marketing the product as serverless, and their focus now is to offer high-performance databases.


## Serverless database that is not actually serverless


Shortly after this new product announcement, as we checked our query insights, it appeared that some queries started to take longer than others. We had our indexes created, and it was not clear what we could do to enhance the performance. Then, a new CPU and memory chart appeared on our dashboard, showing our fully utilized cluster. That was when it was apparent that the product was moving away from the serverless positioning.


Also, the pricing page started using terms like “low-traffic” for their Scaler product.


That did not make sense because we are being charged on one dimension, which in this case is the row read and written. It did not make sense to show CPU & Memory, a completely different dimension that we cannot control.


We had a conversation with the team on Twitter, and it was clear that PlanetScale is moving away from the serverless positioning.


**Update:** During the writing of this article, PlanetScale ultimately[retired the Scaler Plan](https://planetscale.com/blog/deprecating-the-scaler-plan) , keeping only the Scaler Pro plans, and removed all mentions of serverless from their marketing website.


## Upgrading to Scaler Pro


After this conversation with the team, it felt to us that PlanetScale was not necessarily the right product to use, but we went ahead and upgraded to Scaler Pro; we immediately upgraded to` PS-20` as we were basically on` PS-10` previously. To my surprise, our CPU usage dropped to 40% immediately after this upgrade, which is great, but memory usage stayed at the high 80%. This surprised us, as we just doubled the memory available to our cluster, which did not have any effect. This could be due to page caching on Vitesse; the CPU kept spiking to high usage, which felt unclear.


Cluster utilization after upgrading from PS-10 to PS-20


Shortly after the upgrade, we got our cost estimate, and our cost immediately increased from ~$100 to ~$250; the pricing breakdown did not make sense; for example, read-replicas had varying prices, with no information on the pricing per region.


## Other PlanetScale limitations


Other PlanetScale limitations helped with the decision to move out of it:


-


Public databases only; if you want to protect your database behind a private network, you need to move to the enterprise plan. This is probably the biggest limitation of PlanetScale.


-


No foreign key support (foreign key support was just introduced in beta after our move). We were depending on Prisma’s relation mode.


-


No control over the server: for instance, we have hit a MySQL bug related to sorting buffer. There is no way to change the underlying server version, and you cannot set any of its parameters (to increase the sorting buffer for example). For any query that we know will be sorting large datasets, we have to open a transaction, and inside this connection, we increase the sorting buffer; once the connection is closed, we lose this config.


-


No alerts about CPU and Memory utilization, you have to manually monitor the charts.


-


If you need to protect your main branch from accidental deployments, you must use deploy requests for migrations, which is a lengthy process and challenging to streamline. Also, we spent a lot of time automating this process, which never worked as expected.


-


PlanetScale pricing on the outside might feel cheap, but the compute part of the total bill is probably the least amount; the more significant part of the bill is add-ons like storage for any custom backup and additional branches.


-


There are some undocumented limitations related to Vitesse; for example, if we need to dump the database, we can’t use the standard MySQL dump tool as some tables hit a size limit, so we had to use PlanetScale CLI.


-


PlanetScale performance is top-notch, but it falls short in special operations; for example, I ran the same query that retrieves the last updated row for each table in our database in PlanetScale and RDS. RDS finished the query in less than half the time.


## Great things about PlanetScale


-


Resource Utilization: Vitesse resource utilization is superior to native MySQL or other engines like Aurora; you are probably getting higher performance per unit of compute and memory.


-


Load Balancer: PlanetScale load balancer is their secret sauce and allows them to scale to many connections; this is very similar to the RDS proxy.


## RDS Aurora v2 Benefits


-


Serverless: I believe Aurora v2 Serverless is a great product and a solid offering from AWS. It really responds very quickly to your traffic, whether scaling up or down.


-


Private networking, the database is inside the same VPC as your application, you get speed and security.


-


RDS Proxy: RDS proxy can be considered an add-on on top of AWS RDS, and it basically consolidates all the connections from all apps and clients into a more reliable connection pool with the database server. The process of opening a new connection between the application and the database is very expensive and offloading that to a proxy, frees up your DB precious resources to handle the actual queries.


-


Runs in your cloud, you own the infrastructure, and you can customize it in a way that makes sense for your use case.


## RDS Aurora v2 Drawbacks


-


Price: Probably Aurora v2 will end up being more expensive compared to something like PlanetScale, because you have to pay for replicas and proxy. We were paying around $250 on PlanetScale after moving to Scaler Pro, and now paying around $400 monthly.


-


You have to do some heavy-lifting; there are many optimizations that the PlanetScale team did for their product, and it took us some time to reach the same stability with Aurora.


## Migrating to RDS


The move to RDS was not that easy and needs its own blog post, but there are a few points worth mentioning in the context of this post.


-


You have to do lots of planning, and you will still hit one or two issues: database migration is not something to take lightly.


-


Prices with RDS are higher, but that could be caused by the fact that now we have an auto-scalable database, Aurora Serverless v2. In other words, the database adds more compute to serve the queries needed from it.


-


If you are moving to a private RDS, external applications will stop working; make sure you have a plan for those.


-


AWS Aurora multi-AZ failover is probably one of its most outstanding features.


## Word of gratitude to PlanetScale


Any software, including Flightcontrol, has its limitations and various tradeoffs. You have to make an informed decision about what works for you. PlanetScale worked for us in the first two years, but we did not feel it was the right product as we are scaling and growing. We’re thankful for the product and team that served us well this far.
