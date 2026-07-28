---
schema_version: "1.0.0"
document_id: "21bac6f66587adb7ab54805746190d101016541cae07af53534673413e83d852"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/exit-handlers-argo-workflows-trigger-notifications-part-2"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:54770dceb8d339b7f198448e55d0a59e7e83136acbe981e7449019a01768f140"
---

# How to Use Exit Handlers with Argo Workflows to Trigger Notifications Part 2

[Argo Workflows is a tool](https://pipekit.io/blog/top-10-argo-workflows-examples) for designing pipelines that run on Kubernetes. These pipelines are composed of multiple tasks and each task runs in a Kubernetes pod. The defined tasks range from downloading data from a storage bucket to running data analytics (Spark or Dask) workloads.


The previous article addressed the basics of Argo workflows and the various ways you can add exit handlers to a workflow. In this article, you’ll learn how to trigger notifications from exit handlers to tools such as email, Slack, PagerDuty, Twilio, and more.


## Triggering Notifications in Argo Workflows with Exit Handlers


Exit handlers are ideal for triggering notifications in Argo Workflows. Before you proceed with this tutorial, you’ll need the following prerequisites:


- A Kubernetes cluster deployed to a cloud environment
- A Slack account
- A PagerDuty account
- A Twilio account
- A Discord account


You’ll be using the same workflow to set up notification handlers for the different tools that will be addressed:


```text


```


### Setting Up Argo Workflows


Argo Workflows is a custom Kubernetes resource, so you need to apply the Argo Workflows Kubernetes manifest. You can set up Argo Workflows in any Kubernetes environment. The easiest setup is a local setup using[minikube](https://minikube.sigs.k8s.io/docs/start/) .


Here are some other ways you can deploy Kubernetes to your local or cloud environment:


- [K3s](http://pipekit.io/blog/how-to-run-argo-workflows-in-k3s)
- [Docker Desktop](http://pipekit.io/blog/argo-workflows-with-docker-desktop)
- [AWS, GCP or Azure](http://pipekit.io/blog/production-install-of-argo-workflows)


You can also automatically provision Argo Workflows using a fully managed service like[Pipekit](https://pipekit.io/) .


#### Installing Argo Workflows


Argo is a Kubernetes resource that can be applied globally or to a specific namespace. Run the command below in a UNIX shell within your Kubernetes environment (in the shell that has access to Kubernetes). The command creates a namespace and applies the Argo Workflows configurations to it:


```text


```


Run the command below in the same shell as above to port forward the Argo Workflows user interface HTTP address to your local environment:


```text


```


This will serve the UI on[http://localhost:2746](http://localhost:2746/) .


#### Install Argo CLI


You can install the Argo CLI on Linux and macOS machines. Visit the[releases page](https://github.com/argoproj/argo-workflows/releases) for the latest CLI release for macOS and Linux. This article makes use of version 3.3.5. You can use the bash snippet below to install version 3.3.5 on a Linux machine:


```text


```


{% cta-1 %}


### Setting Up Notifications Using Exit Handlers


You’re now ready to set up notifications using exit handlers. You’ll be setting up email, webhook, Slack, PagerDuty, Twilio, and Discord notifications.


#### Sending Email Notifications from Exit Handlers


You can send email notifications using providers such as SendGrid, Mailgun, and Amazon SES. First you need to get the cURL configuration and add it to your workflow exit handler. This article uses SendGrid, but any other mail sending tool should also work.


Follow the steps below to configure and send email notifications from exit handlers:


1. Navigate to[app.sendgrid.com](https://app.sendgrid.com/) to log in or create an account.
2. Navigate to the[SendGrid integration guide](https://app.sendgrid.com/guide/integrate) and choose **Web API** .


Integration Guide Page


1. On the Web API integration page, choose **cURL** as the language you want to use.


Language choice page


1. On the cURL integration page, choose a descriptive API key, then copy the environment variable export and the cURL command.


cURL integration options


1. You’ll add the shell code snippet below to your Argo workflow. Replace <SendGrid_API_KEY> with the API that was generated in the previous step. Also, replace <YOUR_VERIFIED_EMAIL> and <YOUR_VERIFIED_SENDER> with your configured verified email and sender.


YOUR_VERIFIED_EMAIL is the email you set that can receive emails you send. YOUR_VERIFIED_SENDER is the email you configured that can send emails through your SendGrid account. This only applies for a free account. You can also modify the subject and content in the following snippet:


```text


```


1. Create a new dummy workflow in your Kubernetes environment where Argo Workflows is running that sends an email when the run completes. You can name this workflow cowsay-email.yml. Add the following YAML snippet to the workflow file:


```text


```


1. Submit the workflow using argo submit -n argo --watch cowsay-email.yml. An email will be sent to your verified email when the workflow run completes. Run argo -n argo logs @latest to see the logs from the cowsay-email.yml workflow. You should get the following logs on success:


```text


```


#### Sending Slack Notifications from Exit Handlers (using a webhook)


Slack provides a webhook endpoint for sending notifications to channels via HTTP POST requests. Here are the steps to send notifications to Slack:


1. Create a channel in a workspace where you have channel creation rights. You can create a new workspace if you don’t have channel creation in any existing workspace.
2. Navigate to the[Slack app API dashboard](https://api.slack.com/apps?new_app=1) to create an app. Choose the **From scratch** option.


Slack app from scratch modal


1. After choosing **From scratch** , pick a name and select the workspace in which you created the channel in the previous step, then click **Create App** . You’ll be navigated to the app settings page.


Name and Workspace Choice Modal


1. Your app needs to be configured to receive incoming webhooks in order to receive notifications. On the basic information page, choose the **Incoming Webhooks** option and turn on incoming webhooks. A section will appear with the button **Add New Webhook to Workspace** . Click on the button. You’ll be redirected to a page to set the channel that will receive the webhook notifications:


1. Choose the channel you created in the first step, then click **Allow** to allow webhook notifications to be sent to the channel. You’ll be navigated to a page that contains the webhook URL of your Slack app. You’ll use this URL in your workflow, so copy it and keep it handy.


Channel chooser


1. Create a new file called cowsay-slack.yml in the cluster and namespacemachine where Argo Workflowsyour Kubernetes cluster is running, and add in the content below. Replace <YOUR_SLACK_WEBHOOK_URL> with the webhook URL you copied in the previous step:


```text


```


1. Run cowsay-slack.yml using argo submit -n argo --watch cowsay-slack.yml. This should send a Slack notification to the channel you created.


#### Sending PagerDuty Notifications from Exit Handlers


PagerDuty is an incident reporting platform that collects signals from different systems (like Argo Workflows), assigns priorities to them, and determines the right people to fix them based on an on-call rotation.


PagerDuty exposes an API that can serve as a webhook endpoint that you can trigger using cURL. Follow the steps below to send notifications from Argo Workflows to PagerDuty:


1. [Create a PagerDuty account](https://stackedit.io/%5Bhttps://pagerduty.com/sign-up%5D(https://pagerduty.com/sign-up)) .
2. Navigate to **Service Directory** under the **Services** tab.


Service directory page link


1. Click on **New Service** to create a new service.


Service Directory Page


1. Give your service a name like “Argo Workflows Alerts” and a description. Then click **Next** .


Service name and description


1. Leave the default options in **Assign** and **Reduce Noise** , by clicking **Next** on each page.
2. Select **Events API V2** from the integrations list on the **Integrations** page, then click **Create Service** . You’ll be redirected to a page with your integration key and a webhook URL.


Select integrations


1. On the integrations details page, make a note of the **Integration Key** and **Integration URL** for **Alert Events** . You’ll use these details in your workflow template.


Integrations page details


1. Create a new file called cowsay-pager-duty.yml in the cluster and namespace where Argo Workflows is running, and add in the content below:


```text


```


Replace <YOUR_INTEGRATION_KEY> with the **Integration Key** shown on your integration details page.


1. Run cowsay-pager-duty.yml using argo submit -n argo --watch cowsay-pager-duty.yml. This should send an incident to PagerDuty.
2. Navigate to your incidents page to see the incident that was created from the workflow run.


Incident page


#### Sending Twilio Notifications from Exit Handlers


Twilio is a service that provides communications APIs for platforms like SMS, phone calls, WhatsApp, and chatbots. It lets you send notifications through these platforms. Follow the steps below to send SMS via exit handlers:


1. [Create a Twilio account](https://www.twilio.com/try-twilio) . You’ll be navigated to an email verification page, and after verifying your email, you’ll land on a phone number verification page.
2. After completing your email and phone number verification, you’ll need to set up a messaging service. Head over to the sidebar, then navigate to **Messaging > Try it out > Get Set Up** to start the setup process. Click on **Start setup** to get started.


set up messaging service


1. First choose a messaging service name, then click **Create Messaging Service** .


Create messaging service


1. Next, select the phone number from your list of phone numbers. Twilio provides you with a default phone number for sending text messages. Click **Add this number** to proceed.


Add phone number


1. Navigate to **Messaging > Try it out > Send an SMS** , to get the cURL command for sending SMS.


send an SMS page


1. Select the messaging service you previously created and enter some body text. Copy the cURL command and keep it handy. The AuthToken in the cURL command can be obtained by navigating to[your Twilio console page](https://console.twilio.com/) .
2. Create a new file called cowsay-sms.yml in the cluster and namespace where Argo Workflows is running and add in the content below. Replace <YOUR_TWILIO_API_URL>, <YOUR_VERIFIED_PHONE_NUMBER>, <YOUR_MESSAGING_SERVICE_ID>, <YOUR_ACCOUNT_SID>, and <YOUR_AUTH_TOKEN> with your credentials:


```text


```


1. Run cowsay-sms.yml using argo submit -n argo --watch cowsay-sms.yml. This should send an SMS to the phone number you provided.


{% related-articles %}


#### Sending Discord Notifications from Exit Handlers


You can send notifications to Discord the same way you can send notifications to Slack. Discord has fewer steps to send notifications:


1. Create a new Discord channel in a Discord server where you have channel-creation permission. You can find the **Create Channel** button when you click on the server name located at the top left corner of the sidebar.


Create channel from server overview


1. Select **Text** as the channel type and input a descriptive channel name.


set up discord channel


1. After the channel has been created, click **Edit Channel** . You’ll be navigated to the channel settings page.


Edit channel


1. In the channel settings page, go to **Integrations** and then click **Create Webhook** .


Create webhook


1. On the **Webhooks** page, choose a descriptive name for your webhook like “Argo Workflow Bot”, click **Copy Webhook URL** to copy the webhook URL, and finally, click **Save Changes** at the bottom. Note that the **Save Changes** button might not appear if you’re on the Discord web app (where saving happens automatically).


Edit Webhook Button


1. Now, create a file called cowsay-discord.yml in your Kubernetes cluster and namespace where Argo Workflows is running, and add in the content below. Replace the <YOUR_DISCORD_WEBHOOK_URL> with the webhook URL you copied in the previous step (step 5).


```text


```


1. Run cowsay-discord.yml using argo submit -n argo --watch cowsay-discord.yml. This should send a Discord message to the channel you created.


## Conclusion


In this article, you learned how to trigger notifications in Argo Workflows. You also learned how to send notifications to Slack, PagerDuty, Discord, Twilio, SMS, and email from exit handlers.


Setting up Argo workflows across different clusters in your infrastructure means you have to manage your infrastructure alongside your workflows. An easier way to set up workflows is through a fully managed service like Pipekit.


Pipekit lets you set up production-ready Argo workflows across multiple Kubernetes clusters. With Pipekit, you can trigger workflows, collect logs, and manage secrets without managing your infrastructure.
