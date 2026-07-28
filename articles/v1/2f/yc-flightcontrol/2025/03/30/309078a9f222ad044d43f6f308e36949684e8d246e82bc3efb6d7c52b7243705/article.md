---
schema_version: "1.0.0"
document_id: "309078a9f222ad044d43f6f308e36949684e8d246e82bc3efb6d7c52b7243705"
company_key: "yc-flightcontrol"
company: "Flightcontrol"
source_id: "yc-flightcontrol-news-import-3b34406332e0"
canonical_url: "https://www.flightcontrol.dev/blog/announcing-s3-buckets-and-cost-budgets-alerts"
published_at: "2025-03-10T00:00:00+00:00"
first_seen_at: "2026-07-21T20:27:41.783025+00:00"
fetched_at: "2026-07-28T21:30:42.971376+00:00"
content_hash: "sha256:1daca253bafbf7636462059726c57c2f0361abde506a5088e6ab2d7e63bdd742"
---

# Announcing S3 buckets and cost budgets & alerts

We're thrilled to share several new features and updates we've rolled out at Flightcontrol this month. These enhancements are designed to improve your experience and provide even more value in your projects.


### Introducing S3 Bucket Management!


We've made it easier than ever to create and manage S3 buckets directly through Flightcontrol. This new feature allows you to:


-


**Easily create S3 buckets** with configurations for blocking public access and setting custom policies.


-


**Use S3 in your preview environments** for seamless operation with bucket-per-pull request and automatic cleanup after merging.


The best part? **S3 buckets are now included in Flightcontrol at no additional charge.** They do not count as a billable service, though standard AWS costs will apply.


[Read the documentation and try it out today!](https://www.flightcontrol.dev/docs/guides/flightcontrol/using-code/s3)


### New Cost Budgets & Alerts


Take control of your spending with our new cost management features. You can now set cost budgets and receive alerts for:


-


**Project level**


-


**Environment level**


-


**Service level**


Notifications can be received via email and Slack, depending on your configuration.


[Set up your budgets now in the Budget tab in your project settings.](https://app.flightcontrol.dev/)


### Automatic Tagging for AWS Resources


We've implemented automatic tagging for all AWS resources managed by Flightcontrol. Tags include:


-


` fc:id`


-


` fc:serviceId`


-


` fc:environmentServiceId`


-


` fc:environmentId`


-


` fc:previewEnvironmentId`


-


` fc:projectId`


-


` fc:awsAccountId`


-


` fc:organizationId`


These tags help streamline management and improve visibility across your resources.


[Learn more about our tagging strategy in the documentation.](https://www.flightcontrol.dev/docs/guides/flightcontrol/resource-tags)


### Expanded RDS Configurations


Our RDS service offerings have expanded to include more options to serve you better:


-


Encryption at rest


-


Deployment across multiple availability zones


-


Adjustable backup retention durations


-


Customize storage type and provisioned IOPS


[Explore these new RDS features now.](https://app.flightcontrol.dev/)


### Documentation Additions


All the Flightcontrol config documentation pages have been overhauled and improved.


We've added a few key pages:


-


[Docs for optimizing build & deploy speed](https://www.flightcontrol.dev/docs/tips/optimizing-build-deploy-speed)


-


[Docs for understanding ECS-EC2](https://www.flightcontrol.dev/docs/guides/advanced/ecs-ec2)


-


[Docs for using CUE lang to simplify large flightcontrol.json's](https://www.flightcontrol.dev/docs/guides/flightcontrol/using-code/using-cue)


### Stay Informed with Our Changelog


Don't miss any updates or improvements; check out our weekly[changelog](https://roadmap.flightcontrol.dev/changelog) for all the details.
