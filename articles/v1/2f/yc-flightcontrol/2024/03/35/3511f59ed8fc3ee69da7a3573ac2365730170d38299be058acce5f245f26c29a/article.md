---
schema_version: "1.0.0"
document_id: "3511f59ed8fc3ee69da7a3573ac2365730170d38299be058acce5f245f26c29a"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/introducing-flightcontrol-long-running-cron-jobs-and-ad-hoc-commands"
published_at: "2024-03-20T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T22:26:07.231499+00:00"
content_hash: "sha256:881182f4a1798d7e75cb277a8b7d1a9db1a643879b89584d1bda1e1193173ce6"
---

# Introducing Flightcontrol long-running cron jobs and ad-hoc commands

**We’re Flightcontrol, the PaaS for deploying production apps that is uniquely best at the combo of reliability, flexibility, and performance. We achieve that with a simple, powerful interface that automates deployments to your own AWS account. Today we’re announcing that our Fargate scheduler job runner is generally available.**


Scheduled and one-off tasks can be somewhat annoying things that almost every app eventually needs. Yes, you can deploy a traditional worker server with something like BullJS or[Inngest](https://www.inngest.com/) , but sometimes that’s more overhead than you want, or maybe you need a dedicated container for a long-running, resource intensive task.


## Each job runs in a dedicated container that starts and stops on-demand


When it’s time for your job to run, we automatically spin up a dedicated server via AWS Fargate that runs your job. Once completed, the server shuts down, so you only pay for execution time.


You can also trigger a new run on-demand, whether the job is scheduled or not.


## Jobs can be long running


The default timeout is 8 hours, but it can be configured from 1 minute to 24 hours. 24 hours is a soft limit, reach out to us if you need longer.


## When you might want to use our job runner


### You have a long-running, resource intensive task that is best run in a temporary container


Even if you already have a worker system like Inngest, our job runner is well suited to resource intensive tasks. For example, a periodic job could require more CPU and memory than you normally need for the worker, causing it to be over-provisioned. By offloading that job to our scheduler service, it can have as much CPU and memory as needed, and your workers can be smaller and more efficient.


### You need scheduled jobs but don’t already have a worker server


Our scheduler service is the easiest way to run scheduled jobs because it doesn’t require any custom code or libraries.


It’s also likely cheaper than running a dedicated worker if you don’t have many jobs or they don’t run often.


### You want an easy way to trigger scripts on-demand


When adding a job, you can define a recurring schedule or require it to be manually triggered. This is a great way to run ad-hoc scripts in production as needed.


## Features to make your life easier


As you’ll see below, we obsess over user experience. It wasn’t good enough to just ship a basic text box for the cron schedule. Creating a cron string can be frustrating, and we can make it better, so we did. It wasn’t good enough to just have schedules in UTC. Because you shouldn’t have to update your schedule twice a year to keep the same local time when DST kicks in.


### Intuitive cron schedule input


It is a regular text box, but it’s supercharged with validation hints when a segment is focused. You also have 1-click presets for hourly, daily, weekly, and monthly.


### Custom timezone


If you want to run a job at a certain local time year round, we have you covered with the ability to define the timezone for the job. You won’t have to worry about updating the schedule each time daylight savings time comes around.


### See important information at a glance


We show all the important information, like the execution history, the defined schedule, and when the job will next run.


### Complete logging


Our dashboard makes it easy to see all the logs, including build logs and logs for each job execution.


### Pause jobs


Sometimes you need to pause a job, and we make it easy to do.


### Parallel executions


Rest assured, you can have multiple jobs running in parallel since each job is executed in it’s own isolated container.


### Customize CPU and memory per job


Each job can have a different resource configuration based on its own requirements.


### Multiple build source types


All our services support the following four build types, so you can use exactly the workflow that you want.


-


[Nixpacks](https://nixpacks.com/) is like modern Heroku build packs. Point it to your code, and it mostly just works.


-


**Custom Dockerfile** allows you to fully customize the build


-


**Image registry** allows you to manage the build instead of Flightcontrol, and we’ll deploy what you built.


-


**From service** , currently only available in flightcontrol.json, allows you to re-use a build from another service.


### Notifications


Get notified by email and/or Slack when any of your jobs execution fails. It contains a link to our dashboard, where you can view all the logs and see why it failed.


### Sidecars for monitoring


For more advanced monitoring, you can add a sidecar container to send metrics to something like Datadog.


## Try it out!


Give it a try, and[let us know](https://www.flightcontrol.dev/docs/troubleshooting/contacting-support) if you have any issues or feedback! See[the docs](https://www.flightcontrol.dev/docs/guides/flightcontrol/using-code/fargate-scheduler) for more information.
