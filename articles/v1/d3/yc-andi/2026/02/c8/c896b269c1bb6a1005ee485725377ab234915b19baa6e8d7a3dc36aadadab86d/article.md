---
schema_version: "1.0.0"
document_id: "c896b269c1bb6a1005ee485725377ab234915b19baa6e8d7a3dc36aadadab86d"
company_key: "yc-andi"
company: "Andi"
source_id: "yc-andi-news-import-887dceecc721"
canonical_url: "https://andiai.com/blogs/airun-prompts-as-programs"
published_at: "2026-02-12T00:00:00+00:00"
first_seen_at: "2026-07-24T06:55:59.564380+00:00"
fetched_at: "2026-07-28T22:20:36.551441+00:00"
content_hash: "sha256:b58ef92e40e6fff9b3569e3c868317b3034d463d7c113778ad1d4614dc0b4268"
---

# Prompts should be programs

## Your prompts should be programs


In November, Pete Koomen[posted on X](https://x.com/koomen/status/2007894999506235409) about making markdown files executable — like shell scripts, but for AI. We implemented it that day.


It works well. So we kept coding, and it is now AIRun, a free open-source CLI that lets you run AI prompts like programs, locally or with any cloud model.


You write a markdown file with a prompt. You add a shebang line. You make it executable and run it.


```text
#!/usr/bin/env ai
Analyze this codebase and summarize the architecture.
```


```text
chmod   +x   task.md
./task.md
```


This is a program that lives on disk, rather than in a chat session.


You may not be a fan of AI. You may worry about non-deterministic outputs, safety, privacy, and security. Those are real problems to fix. But I remember when people scoffed at BASIC over Assembly, and Python over C. Sometimes you need C++. Sometimes you need TypeScript.


With agentic tools, English is becoming a viable programming language. Claude Code is a compiler. You write in English; it produces Python, JavaScript, shell scripts — whatever the task needs. You should be able to use it like any other programming language: save your prompts to files, make them executable, pipe them together, and schedule them with cron.


Claude Code already has persistence. CLAUDE.md files give every session your project context, and skills store reusable procedures. System prompts shape how the model behaves. These are all ways of teaching the interpreter. They make the REPL smarter — it remembers your project, your conventions, your preferences. But you’re still sitting at the REPL, typing commands.


An executable markdown file doesn’t need an interactive session.` ./task.md` works the same way` python script.py` works — the interpreter runs the file and exits. You can schedule it with cron or trigger it from CI. It runs while you sleep.


This is the same transition that happens when you learn a traditional programming language. You start in the REPL, exploring. Then you save your work to a file, and the file becomes a program.


Once a prompt is a file, it inherits everything Unix knows about files:


```text
cat   data.json   |   ./analyze.md   >   results.txt
git   log   -10   |   ./summarize.md
./generate.md   |   ./review.md   >   final.txt
```


Pipes, redirection, git, make, CI: fifty years of tooling, built for files, now works with AI prompts. No new infrastructure needed.


That last pipeline pipes the output of one AI script into another. The first generates; the second reviews. Small tools composed through pipes, the way Unix has worked since 1973.


This gives text-in, text-out scripts agentic powers. Claude Code has full tool use: it can edit files, run shell commands, and navigate your codebase. A markdown file can orchestrate a multi-step workflow:


```text
#!/usr/bin/env -S ai --sonnet --skip --live
Analyze this codebase. Run the tests. Print your findings as you go.
Summarize how many passed and failed.
Document any issues and recommend next steps.
```


` --skip` lets Claude run commands and write files without prompting.` --live` streams progress in real-time so you see results as they happen. Claude reads the codebase, runs the tests, parses the output, and writes a report. The prompt orchestrates the tools.


Pete Koomen’s[“Horseless Carriages”](https://koomen.dev/essays/horseless-carriages/) essay framed system prompts as functions: the system prompt defines behavior (like a function definition), the user prompt provides input (like arguments), and the response is the output. Take that to its logical end and you get an interpreter for prose: a runtime that executes natural language with real tools. Make the prompt a file with a shebang, and the file system becomes your development environment.


The startup community sees the problem. There are now dozens of prompt management platforms (Langfuse, PromptLayer, Braintrust, Humanloop) building versioning, evaluation, and deployment infrastructure for prompts. They’re solving a real problem: prompts in production need to be versioned, tested, shared, and deployed. But the file system already does all of that. Git versions them, CI runs them, and pipes compose them. The simpler answer was there all along.


We also added provider switching, so the same script runs on any backend: your Claude subscription, AWS Bedrock, Ollama or LM Studio locally, or OpenAI’s codex models through Vercel. Write a prompt once, test it against different models, compare the results. The prompt is portable because it’s a file.


For many scripting tasks, you don’t need expensive models. Smaller, faster models work. Local models are free and private, so we use them. Because prompts are files, you can benchmark the same script against different models, or use different models for different steps in a pipeline.


---


```text
git   clone   https://github.com/andisearch/airun.git   &&   cd   airun   &&   ./setup.sh
```


I’m building[Andi AI](https://andiai.com/) . AIRun is open source and free.


[airun.me](https://airun.me/) |[GitHub](https://github.com/andisearch/airun)
