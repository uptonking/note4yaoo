---
title: lib-editor-codemirror-community-pm-ide-ai
tags: [codemirror, community, ide]
created: 2024-08-11T03:30:50.811Z
modified: 2024-08-11T07:19:29.817Z
---

# lib-editor-codemirror-community-pm-ide-ai

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-coding-ai
- ## 

- ## 

- ## Aider keeps shipping with 70% of its code now written by AI. But I think its growth is constrained by being terminal only. 
- https://x.com/imrat/status/1845158205552226742
  - Replit Agents has massive potential especially as early alpha. Improvements made are great. But I think they may struggle to be adopted in enterprise.
  - Cursor  adoption in enterprise is huge (70%-80% of users are on Windows) and I think they will focus more and more on code for complex services / apps. Those that can’t be deployed at the press of a button and have UIs too complex for AI. 
  - V0 owns the front end space right now. I think they will deliver big improvements on Tuesday launch. I hope better support for backend and deployment is coming. 

- google idx looks pretty interesting. So does bolt(dot) new. FOSS version of v0 is called "Llamacoder" (also fairly nice).

- ## Parallel cmd-k’s are becoming unexpectedly popular
- https://x.com/cursor_ai/status/1765512112200151391
- didn't see programmers liking parallel processing and async multitasking capabilities? or didn't realize that you built the thing that is actively building the thing... AI-Powered Devs.  of course that'd be popular, once it found some hype-men

# discuss
- ## 

- ## 

- ## 

- ## Everyone's building AI Agents. Here are the most popular libraries:
- https://x.com/deedydas/status/1845297659760058668
  Langchain [93.4k]
  Microsoft Autogen [31.8k]
  Microsoft Semantic Kernel [21.6k]
  Crew AI [20k]
  OpenAI Swarm [4.7k]
  Langroid [2.4k]

- I would add couple to this list:
  mem0 (22.3k stars and it includes super useful embedchain)
  streamlit (35.1k stars)
  crawl4ai (13.3k stars)
  OpenAI API (a lot of open source LLMs can be used via same API)
  Gemini Developer API
  Anthropic API
  3rd party providers like: Monster API, Replicate and AI/ML

- Most popular, sure. But the only ones they should use is swarm and lang graph. Theres a good series on YT breaking down why that is, but long story short, the other frameworks are so costly (up to 15x more) and nowhere near production ready.

- ## Introducing @Taskade 's AI Teams with Multi-Agent Collaboration, now in beta
- https://x.com/Taskade/status/1822908447597396176
  - They plan, execute, and manage tasks—all together!

- ## 我发现cursor，有好多不方便的地方，
- https://x.com/simon_he1995/status/1824282160741924955
  - 比如它在调试的时候没办法知道你当前选中的长度，没办法拖拽自定义窗口到任意侧边栏，没办法配置 settings， vscode 插件搜索经常失败，
  - 但唯一让人觉得很优秀的是它的代码提示，可以影响到上下文，就是你在当前行提示晚，可以继续tab，它能跨行接着tab
- 我都是开两个，python插件根本用不了，写代码我就在cursor，调试其他的我就在vscode

- ## I am open sourcing Cursor Analytics, a dashboard for @cursor_ai to log all API requests, see tokens used, and let you choose any LLM model. _20240816
- https://x.com/thehamedmp/status/1824216074579218678
  - All the logs are saved to a postgres db, enabling you to do cool analytics and projects on top
  - Started with Python, doing UI was messy, switched to Node for some performance improvements, but ended up with @nextjs 

- ## 🐛 LLMs are bad at returning code in JSON. They write worse code in structured JSON responses. Even gpt-4o-2024-08-06's strict JSON mode.
- https://x.com/paulgauthier/status/1824442504290374061
- This is literally why we wrote a self healing json parser
  - The problem isn’t the json. That’s fine. The code inside is worse and has syntax errors.
- I've had better success (currently) using my old method of using a prompt to say, "return response exactly like this, nothing extra: "X:x, Y:y, Z:z, " then using regex to extract. Helps me pull info out of PDFs for financial management purposes
- This is also the case with other reasoning tasks. better results by having the llm output "flat" text w/ simple delimiters

- There are several issues here
  - Complexity Overload: When LLMs are tasked with generating code within a JSON structure, they face the dual challenge of producing syntactically correct code and ensuring the JSON format is also correct. This dual task can overwhelm the model, leading to more syntax errors in the code itself. The model might focus on JSON formatting at the expense of code accuracy or vice versa.
  - Token Overhead: JSON requires specific syntax (brackets, commas, quotes) which adds to the token count. This overhead can lead to models making compromises in code generation due to limitations in context window or token generation strategies, which might prioritize JSON structure over code functionality.
  - Misinterpretation of Task: The requirement to output in JSON might cause the model to misinterpret the task's primary goal, focusing more on producing a JSON structure rather than ensuring the code within is logically sound or complete.
  - Structured JSON capabilities introduced recently are created for the goal of integration with the millions of API’s in Open API format not for code generation for which we can use Tools.

- The best practice is to separate reasoning and structuring, by doing a two-stage completion
- My advice is to separate reasoning and formatting into their own distinct prompts.
- This is probably one of the reasons why allowing agents to write code blobs works better than forcing JSON tool calls
