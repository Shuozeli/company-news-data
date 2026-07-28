---
schema_version: "1.0.0"
document_id: "0c59368b4a57c0a97934a493e932860919b5f2143d281eaf81f71ece2fa5b70d"
company_key: "yc-sift"
company: "Sift"
source_id: "yc-sift-news-import-56a09e055dd6"
canonical_url: "https://engineering.sift.com/security-bulletin-aws-reported-ami-issue/"
published_at: "2018-09-21T23:40:52+00:00"
first_seen_at: "2026-07-24T13:26:21.656972+00:00"
fetched_at: "2026-07-28T21:33:49.818370+00:00"
content_hash: "sha256:7780b250411cb42b768b09e8bfbe67239d1fa4f0ac7e0d650af218894c8ebe0f"
---

# Security Bulletin – AWS Reported AMI Issue

Post category:


[Articles](https://engineering.sift.com/articles/)


# [Security Bulletin – AWS Reported AMI Issue](https://engineering.sift.com/security-bulletin-aws-reported-ami-issue/)


Philip Allchin


• September 21, 2018


AWS notified Sift on September 18th, 2018, of an issue where AWS incorrectly labeled Amazon Machine Images associated with Sift’s account. AWS incorrectly labeled AMIs as encrypted when the images were unencrypted. Sift engineers investigated and confirmed that the mislabeled AMIs did not place customer data at risk, and that affected systems will receive corrected AMIs with encryption in place. Because Sift and some of Sift’s customers received a similar notice from AWS, Sift is providing this notification to assure our customers there was no impact to the security of their data as a result of this issue.


## Author


-


[Philip Allchin](https://engineering.sift.com/author/phil-legacy/)
