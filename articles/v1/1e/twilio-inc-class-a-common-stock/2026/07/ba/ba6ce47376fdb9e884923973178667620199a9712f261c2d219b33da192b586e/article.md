---
schema_version: "1.0.0"
document_id: "ba6ce47376fdb9e884923973178667620199a9712f261c2d219b33da192b586e"
company_key: "twilio-inc-class-a-common-stock"
company: "Twilio Inc. Class A Common Stock"
source_id: "twilio-inc-class-a-common-stock-news-import-801d48e1d714"
canonical_url: "https://www.twilio.com/en-us/blog/developers/tutorials/product/integrate-openai-twilio-voice-using-conversationrelay"
published_at: null
first_seen_at: "2026-07-22T17:37:59.927743+00:00"
fetched_at: "2026-07-28T21:40:00.658555+00:00"
content_hash: "sha256:0035d82994cd45bd01e9953af7f94d6ecb25fc6795faa0dc3aaef46adb560a08"
---

# Integrate OpenAI with Twilio Voice Using Conversation Relay

## Integrate OpenAI with Twilio Voice Using Conversation Relay


[Conversation Relay](https://www.twilio.com/docs/voice/twiml/connect/conversationrelay) is a product from Twilio that allows you to build real-time, human-like voice applications for conversations with any AI *Large Language Model* , or *LLM* . It opens a WebSocket so you can integrate with any AI API, allowing for a fluid, event-based interaction and fast two-way connection.


This tutorial will serve as a quick overview of a basic integration of OpenAI’s models with[Twilio Voice](https://www.twilio.com/en-us/voice) using Conversation Relay. When you are finished with this quickstart, you will be able to deploy a Node.js server that allows you to call a Twilio phone number and get into a conversation with an LLM. When you’re done with the tutorial, you’ll have a solid base to add more advanced features.


Let's get started!


## Prerequisites


To deploy this tutorial you will need:


1. [Node.js](https://nodejs.org/en) installed on your machine
2. A Twilio phone number ([Sign up for Twilio here](https://console.twilio.com/) )
3. Your IDE of choice (such as Visual Studio Code)
4. The[ngrok](https://ngrok.com/) tunneling service (or other tunneling service)
5. An[OpenAI Account](https://platform.openai.com/api-keys) to generate an API Key
6. A phone to place your outgoing call to Twilio


## Write the code


Start by creating a new folder for your project.


Copy code


```text
mkdir conversationRelayNode
cd conversationRelayNode
```


Next, initiate a new node.js project, and install the prerequisites.


Copy code


```text
npm init -y
npm pkg set type="module";
npm install fastify @fastify/websocket openai dotenv
```


For this tutorial, you’ll use[Fastify](https://fastify.dev/) as your framework. It will let you quickly spin up a server for both the WebSocket you'll need, as well as the route for the instructions you're going to need to provide to Twilio.


To view all of the code for this quickstart, please visit the[repo on GitHub](https://github.com/robinske/cr-demo) .


Start by creating the files you will need to run your connection.


To store your API key for OpenAI, you will need an *.env* file. Create this file in your project folder, then open it in your favorite editor.


Use the following line of code, replacing the placeholder shown with your actual key from the[OpenAI](https://platform.openai.com/settings/organization/api-keys)[API keys](https://platform.openai.com/settings/organization/api-keys)[page](https://platform.openai.com/settings/organization/api-keys) .


Copy code


```text
OPENAI_API_KEY="YOUR_OPEN_API_KEY"
```


If you're going to save your project on GitHub, be sure not to expose any API keys to the internet. Do this by adding your *.env* file to a *.gitignore* file, or making sure to blank any API keys out before committing your build as in the provided GitHub example.


Next, create a new file called *server.js* . This is where the primary code for your project server is going to be stored. Create this file in the same directory as your *.env* file.


Nice work – next, you will work on your imports and define the constants you'll need to change the behavior of the LLM.


### Add the imports and constants


First, add the necessary constants to your file by putting in this code.


Copy code


```text
import Fastify from "fastify";
import fastifyWs from "@fastify/websocket";
import fastifyFormBody from "@fastify/formbody";
import OpenAI from "openai";
import dotenv from "dotenv";
dotenv.config();


const PORT = process.env.PORT || 8080;
const DOMAIN = process.env.NGROK_URL;
const WS_URL = `wss://${DOMAIN}/ws`;
const WELCOME_GREETING =
"Hi! I am a voice assistant powered by Twilio and Open A I . Ask me anything!";
const SYSTEM_PROMPT =
"You are a helpful assistant. This conversation is being translated to voice, so answer carefully. When you respond, please spell out all numbers, for example twenty not 20. Do not include emojis in your responses. Do not include bullet points, asterisks, or special symbols.";
const sessions = new Map();
```


Here, notice that you are adding the system prompt that will sculpt out the personality for our AI. This prompt keeps it simple – and lets your AI know this conversation will be spoken aloud. Therefore, you want the AI to avoid using special characters that will sound awkward to spell out.


Crafting the prompt is an art in itself. You’ll want to bookmark our[Prompt Engineering best practices](https://www.twilio.com/docs/voice/twiml/connect/conversationrelay#prompt-engineering-for-voice-responses-in-conversationrelay) to read through when you are done with the tutorial and continuing the build.


You also add the greeting that our AI can say when a caller rings in using the variable` WELCOME_GREETING` . As you can see, the greeting spaces out letters so the AI speaks them aloud correctly.


### Write the Fastify server code


Great stuff. Now, you'll move on to the heart of the code: the server.


Next, add the following lines of code to *server.js* below where you let off before:


Copy code


```text
const openai = new OpenAI({ apiKey: process.env.OPENAI_API_KEY });
async function aiResponse(conversation) {
const response = await openai.responses.create({
model: "gpt-5.4-mini",
instructions: SYSTEM_PROMPT,
input: conversation,
});
return response.output_text;
}
```


This code block is adding the connection to OpenAI. And the` process.env.OPENAI_API_KEY` line will get your API Key from the` /env` file.


Finally, beneath that, add the code to get your server started and complete the webhook connection.


Copy code


```text
const fastify = Fastify();
fastify.register(fastifyWs);
fastify.register(fastifyFormBody);
fastify.all("/twiml", async (request, reply) => {
reply.type("text/xml").send(
`<?xml version="1.0" encoding="UTF-8"?>
<Response>
<Connect>
<ConversationRelay url="${WS_URL}" welcomeGreeting="${WELCOME_GREETING}" />
</Connect>
</Response>`
);
});


fastify.register(async function (fastify) {
fastify.get("/ws", { websocket: true }, (ws, req) => {
ws.on("message", async (data) => {
const message = JSON.parse(data);


switch (message.type) {
case "setup":
const callSid = message.callSid;
console.log("Setup for call:", callSid);
ws.callSid = callSid;
sessions.set(callSid, []);
break;
case "prompt":
console.log("Processing prompt:", message.voicePrompt);
const conversation = sessions.get(ws.callSid);
conversation.push({ role: "user", content: message.voicePrompt });


const response = await aiResponse(conversation);
conversation.push({ role: "assistant", content: response });


ws.send(
JSON.stringify({
type: "text",
token: response,
last: true,
})
);
console.log("Sent response:", response);
break;
case "interrupt":
console.log("Handling interruption.");
break;
default:
console.warn("Unknown message type received:", message.type);
break;
}
});


ws.on("close", () => {
console.log("WebSocket connection closed");
sessions.delete(ws.callSid);
});
});
});


try {
fastify.listen({ port: PORT });
console.log(
`Server running at http://localhost:${PORT} and wss://${DOMAIN}/ws`
);
} catch (err) {
fastify.log.error(err);
process.exit(1);
}
```


This block of code is doing most of the heavy lifting. The first thing it does is establish a connection from your phone call to Twilio, at the route` /twiml` . That route returns a special dialect called TwiML, which gives Twilio instructions about how to connect to your WebSocket.


Then, it sets up a` /ws` route for Twilio to open a WebSocket app to you. This WebSocket is where you will communicate with ConversationRelay; you will receive messages from Twilio, but you will also need to pass messages from your LLM to Twilio to run the Text-to-Speech step.


We won’t go into all of the messages that will go in either direction. Here, you're handling the` setup` ,` prompt` , and` interrupt` message` type` from ConversationRelay. You can[find more detail on these message types here](https://www.twilio.com/docs/voice/twiml/connect/conversationrelay#messages-from-conversationrelay-to-your-application) .


You can see the message` type` s you can send back to ConversationRelay here. You’ll note that this tutorial is only demonstrating` text` messages (in the line` ws.send()` ) here, but know that you can ask Twilio to play media, send DTMF digits, or even handoff the call!


## Run and test


To finish setting up the ConversationRelay, there are a few more critical steps to connect your code to Twilio.


The first step is to return to your terminal and open up a connection using ngrok:


Copy code


```text
ngrok http 8080
```


You need to open up the connection socket first, because you will need to keep the ngrok url for use in two places: in the Twilio console, and in your environment files.


Get the URL for your file and add it to the *.env* file using this line:


Copy code


```text
NGROK_URL="1234abcd.ngrok.app"
```


Replace the beginning of this placeholder with the correct information from your ngrok url. Note that you do not include the scheme (the “https://” or “http://”) in the environment variable.


Now you are ready to run your server.


Copy code


```text
node server
```


Go into your Twilio console, and[look for the phone number](https://console.twilio.com/us1/develop/phone-numbers/manage/incoming) that you registered.


Set the configuration under **A call comes in** with the **Webhook** option as shown below.


In the URL space, add your ngrok URL (this time including the “https://”), and follow that up with` /twiml` for the correct routing.


Finally, set the **HTTP** option on the right to **GET** .


When a call is connected, Twilio will first get the greeting message that you provided. Then it will use the provided ngrok URL to connect directly to the websocket. That websocket connection will open up the line for you to have a conversation with OpenAI.


Save your configurations in the console. Now dial up the number on your phone.


If everything is hooked up correctly, you should hear your customized greeting. Say hello and ask the AI anything you like!


## What's Next for Conversation Relay?


This simple demonstration works well, but it has limits.


For example, though you may be able to interrupt the conversation *verbally* , you may notice that the conversation text is generated before it's spoken aloud. With this code, the server does not have knowledge of exactly when in the conversation you interrupted it, which might lead to a misunderstanding down the line. You’ll also notice that this version of the code introduces quite a bit of latency when your prompt generates a lot of text from the LLM (try asking it to count to 100!).


[In our next post](https://www.twilio.com/en-us/blog/developers/tutorials/product/token-streaming-interruption-handling-twilio-voice-openai) , we’ll show you how to improve latency by streaming tokens to the LLM. We’ll also show you one way to maintain local conversation state with OpenAI with Conversation Relay’s interruption handling. Finally, we’ll show you how to[add external tools your LLM can call](https://www.twilio.com/en-us/blog/add-function-tool-calling-twilio-voice-openai-integration) using[OpenAI function calling](https://platform.openai.com/docs/guides/function-calling?api-mode=chat) , and integrate everything into this same app.


We hope you had fun building with Conversation Relay! Let's build - *and talk to* - something amazing!


### Appendix


Our colleagues have built some awesome sample applications and demos on top of Conversation Relay. Here’s a selection of use cases:


- [Conversation Relay Architecture for Voice AI Applications Built on AWS](https://www.twilio.com/en-us/blog/conversation-relay-aws-reference-architecture)
- [VoiceAI: Building Voice Bots with Twilio's Conversation Relay](https://www.twilio.com/en-us/blog/voice-ai-build-voice-bots-conversation-relay)
- [Integrate Twilio Conversation Relay with Twilio Flex for Contextual Escalations](https://www.twilio.com/en-us/blog/conversationrelay-flex-contextual-escalations)
- [Twilio Agentic Voice Assistant built on Conversation Relay](https://github.com/pBread/twilio-agentic-voice-assistant-ts)


*Amanda Lange is a .NET Engineer of Technical Content. She is here to teach how to create great things using C# and .NET programming. She can be reached at amlange \[ at\] twilio.com.*
