---
schema_version: "1.0.0"
document_id: "4d300552107cb66c775bbd15cd8794deb7f741355251a0cf933d4ad9189fded7"
company_key: "yc-sift"
company: "Sift"
source_id: "yc-sift-news-import-56a09e055dd6"
canonical_url: "https://engineering.sift.com/testing-and-deploying-sifts-javascript-sdk/"
published_at: "2018-04-25T20:27:39+00:00"
first_seen_at: "2026-07-24T13:26:21.656972+00:00"
fetched_at: "2026-07-28T21:33:49.818370+00:00"
content_hash: "sha256:5af374b73e4a50eacdfbdaf9fb1a287fd26e69929393c9287532f0a877a33bc9"
---

# Testing and Deploying Sift’s JavaScript SDK

Post category:


[Articles](https://engineering.sift.com/articles/)


# [Testing and Deploying Sift’s JavaScript SDK](https://engineering.sift.com/testing-and-deploying-sifts-javascript-sdk/)


Brian Higgins


• April 25, 2018


### ***By Janice Lan and Brian Higgins***


# What is Sift’s JavaScript SDK?


As part of


integrating Sift


, customers


embed


a snippet of JavaScript code onto their websites. The snippet sends us data about users’ behavior and devices for


our machine learning models and to generate a device identifier that tracks fraudsters across our global network.


The rapidly evolving device and browser landscape allows us to collect increasingly rich data via our snippet. Because we host the snippet and our customers fetch it from us dynamically, expanding its functionality requires a strict eye on compatibility for all of our customers’ end users. Our primary concerns are safety and iteration speed, and we’ve invested heavily in robust testing and deployment infrastructure to allow us to confidently roll changes out without spending weeks in manual testing. This blog post dives into how we built these tools and issues we encountered along the way. Specifically, we focus on:


- Our priorities for test coverage


- Challenges we tackled while writing tests


- How to gradually roll out a


CDN hosted


resource


#


# Redesigning our JavaScript Testing Infrastructure


###


### **Testing Coverage & Priorities**


We use unit and integration tests to


check


functionality of the


JavaScript snippet


. These tests make sure we collect valid data and our downstream services process it correctly.


Beyond checking functionality, we also evaluate the snippet on customer websites to identify and prevent changes to customers’ sites. We look


for


the following issues:


- Changing the visual layout of the page


- Creating pop


–


ups or security notifications


- Creating or modifying


variables in the global scope


- A


ffecting


page load performance


With these checks, we verify that our snippet will not change the user experience of our customers’ website


s


.


####


### **Challenges Tack**


**l**


**ed While Creating Tests**


I


n our tests, we compare a website to itself before and after our JavaScript executes. Dynamic content and changing views


make this challenging because the website’s state will be different before and after our snippet runs. For consistent and reproducible tests, we need to know that changes to the page only come from our code, and there won’t be differences because of a social media scroller or image slideshow.


To address this issue, we remov


e


everything in the page that could change


DOM


elements after the page renders. We followed these steps:


1. Load the page and let it render completely.


2. Take the rendered page source from the DOM and store it.


3. Remove all JavaScript and prevent CSS animations and transitions.


4. Replace the HTML of the page with the


“


cleaned” version.


5. Run initial tests to create a baseline snapshot of the page.


6. Inject the JavaScript Snippet into the page.


7. Re-run tests and compare results to initial results — there should be no changes.


This process isolate


s


our code and makes tests robust across


websites with dynamic content.


But, by removing the site


’


s normal


JavaScript, we don’t measure the full scope of possible interactions between our snippet and the website


’


s own JavaScript. We mitigate that risk by scoping all of our variables and


running tests to check for global variable mutation


.


Automated test


ing


is


a great tool, but to complete our testing it


i


s important that we simulate


a


customer


’


s website exactly as it would run with a new version of the snippet. This matters because our customers


’


integrations vary, which changes how and when our JavaScript code is invoked.


During


automated testing


,


we inject the snippet into websites


after page load and everything has rendered.


For a full rollout


,


we need to confirm that the snippet does not create issues in live customer integrations with the website’s JavaScript and CSS intact.


In our manual testing process, we evaluate the new snippet


by replacing the CDN


–


hosted version with a local


ly


hosted development version.


Switching the snippet in place enables us to view our customers’ sites exactly as an end user would after we deploy. This strategy allows us to spot check


various


customer integrations, major web framework


s


, popular devices and operating systems prior to deployment.


#


# Staged Deployment of a CDN Resource


Once the


JavaScript


snippet


is released, we


have


no visibility into errors or issues outside of customer feedback because it runs client


–


side from our customers’ websites.


To mitigate


risk


, we roll out to end users incrementally


to


give customers time to raise concerns if they see anything. We can also roll back very quickly if we find an error. We divert a small portion of traffic to a secondary CDN for the new version of the snippet using DNS load balancing rules. This approach gives us control over how much traffic the new snippet receives without affecting the original CDN. Over the course of a week, we


gradually


increase traffic, giving us opportunity to verify new data and changes on customers’ sites. Finally, after several days handling non-trivial amounts of traffic, we are confident that the new version will not disrupt service and we replace the original CDN’s content with the latest tested version.


By combining our testing framework and gradual deployment system, we’re able to minimize time spent manually testing when we release new versions of our JavaScript snippet. This will enable us to more quickly and confidently deploy changes and improve our client side data collection.


*If these topics interest you, or you want to help build trust on the internet,[check out our careers page](https://siftscience.com/careers) !*


## Author


-


[Brian Higgins](https://engineering.sift.com/author/bhiggins/)
