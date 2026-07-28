---
schema_version: "1.0.0"
document_id: "844a662df1998a65a24388fd020143f47bd822746f90a17dacd9c2f18b5a2059"
company_key: "yc-capy"
company: "Capy"
source_id: "yc-capy-news-import-ccb8c20193bf"
canonical_url: "https://scrapybara.com/blog/cua"
published_at: null
first_seen_at: "2026-07-23T04:45:19.830543+00:00"
fetched_at: "2026-07-28T21:20:09.527818+00:00"
content_hash: "sha256:5570f81cd7cf4ff656bbb36a96e6ca053849a8f261674608533192c68109d9fd"
---

# OpenAI CUA Starter Kit

## TL;DR try CUA for free[here](https://scrapybara.com/playground)


OpenAI's[Computer-Using Agent](https://openai.com/index/computer-using-agent/) was just launched in the API. This is the same model that powers their popular[Operator](https://openai.com/index/introducing-operator/) . The model is a new variant of GPT-4o that leverages the powerful underlying multimodal capabilities to interact with GUIs similarly to humans - by moving the mouse, clicking buttons, typing in text, etc.


This paradigm allows for a truly generalist and flexible digital interface for LLMs, bypassing the often prohibitive requirement for APIs and truly leveraging the powerful reasoning abilities of new models.


## What is Scrapybara?


Scrapybara provides virtual desktop instances in the cloud for computer use agents. Our goal is to make it easy for developers and enterprises to put models like CUA into production.


Over the past few weeks, we have been working closely with OpenAI to provide first-party support for CUA through our Playground and Act SDK and benchmark its performance.


## A New State of the Art


To evaluate CUA and other computer use LLMs, we developed a new private benchmark called CapyBench to guage the capabilities of such GUI models beyond simple demo tasks.


CapyBench consists of 50 carefully curated medium to long horizon tasks. Instead of relying on an LLM judge or automated evals, we asses success on these tasks by manually scoring each attempt. As such, we have found this to be the most reliable way to measure the true "usefulness" of a GUI model in real-world scenarios encountered by our users and ourselves.


Here are some sample tasks from CapyBench:


1.


Configure DNS Records on Vercel


2.


Find @sama's latest tweet and share it on my WeChat family group with a Chinese translation


3.


Create a new account on a specific website (needs to verify email)


We have found only a handful of GUI models to even be suitable for testing with CapyBench. In the interest of fairness, they are all given exactly the same state space (screenshot only) and[action space](https://scrapybara.com/blog/unified-action-space) . Stay tuned to hear more about CapyBench.


In our testing so far, we have observed CUA to be the state of the art GUI model.


Rank Model Score (out of 50)


1 OpenAI CUA 21


2 Claude 3.7 Sonnet 19


3 UI-TARS-72B-DPO 10


4 Claude 3.5 Sonnet 8


CapyBench results across different computer use models


## Using CUA with Scrapybara


Scrapybara now supports three types of integrations with CUA:


1.


Try CUA for free in the[playground](https://scrapybara.com/playground)


2.


Use our[Act SDK](https://docs.scrapybara.com/openai) to build your own computer use agents


3.


Integrate directly with OpenAI's new[Responses API](https://platform.openai.com/docs/guides/tools-computer-use)


## Building CUA agents with Scrapybara Act SDK


To start building with the Act SDK, simply install either the Python or the TypeScript SDK, initialize the client, start your instance, and call act.


PYTHON - pip install scrapybara


```text
1  from   scrapybara  .  openai   import   OpenAI  ,   UBUNTU_SYSTEM_PROMPT
2   from   scrapybara   import   Scrapybara
3   from   scrapybara  .  tools   import   ComputerTool
4
5  client   =   Scrapybara  (  )
6  instance   =   client  .  start_ubuntu  (  )
7
8  response   =   client  .  act  (
9      model  =  OpenAI  (  )  ,
10      tools  =  [
11          ComputerTool  (  instance  )
12        ]  ,
13      system  =  UBUNTU_SYSTEM_PROMPT  ,
14      prompt  =  "Go to the top link on Hacker News"  ,
15      on_step  =  lambda   step  :     print  (  step  .  text  )  ,
16   )
17  messages   =   response  .  messages
18  steps   =   response  .  steps
19  text   =   response  .  text
20  usage   =   response  .  usage
```


TYPESCRIPT - npm install scrapybara


```text
1  import     {   openai  ,     UBUNTU_SYSTEM_PROMPT     }     from     "scrapybara/openai"  ;
2   import     {     ScrapybaraClient     }     from     "scrapybara"  ;
3   import     {   computerTool   }     from     "scrapybara/tools"  ;
4
5   const     {   messages  ,   steps  ,   text  ,   usage   }     =     await   client  .  act  (  {
6    model  :     openai  (  )  ,
7    tools  :     [
8        computerTool  (  instance  )
9      ]  ,
10    system  :     UBUNTU_SYSTEM_PROMPT  ,
11    prompt  :     "Go to the top link on Hacker News"  ,
12      onStep  :     (  step  )     =>     console  .  log  (  step  .  text  )  ,
13   }  )  ;
```


You can also find basic templates for both Python and TypeScript:


[PYTHON scrapybara-python-template](https://github.com/scrapybara/scrapybara-python-template)[TYPESCRIPT scrapybara-ts-template](https://github.com/scrapybara/scrapybara-ts-template)


For more examples, check out our new cookbook:


[COOKBOOK Examples and guides for Scrapybara](https://docs.scrapybara.com/cookbook)[GITHUB scrapybara-cookbook](https://github.com/scrapybara/scrapybara-cookbook)


## Integrating with the Responses API


To see how to integrate Scrapybara with the Responses API natively, check out OpenAI's CUA sample app featuring us!


[OFFICIAL SAMPLE openai-cua-sample-app](https://github.com/openai/openai-cua-sample-app)


## GET STARTED TODAY


Visit our docs and join our Discord community to see how our developers are building with Scrapybara and CUA.
