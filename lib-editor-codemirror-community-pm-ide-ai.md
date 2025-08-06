---
title: lib-editor-codemirror-community-pm-ide-ai
tags: [codemirror, community, ide]
created: 2024-08-11T03:30:50.811Z
modified: 2024-08-11T07:19:29.817Z
---

# lib-editor-codemirror-community-pm-ide-ai

# guide
- pm-ai-coding
  - ai编程类热门产品可以在各大ide的插件市场搜索排序
# discuss-stars
- ## 

- ## 

- ## 最近 AI Coding 越来越🔥。此类产品依赖的一项核心能力，是对 AI 生成的代码实时预览。 _202503
- https://x.com/idoubicc/status/1896136572564902124 
  - 不同的项目代码，用到的预览方案不太一样。
  - 如果生成的代码是单个文件，直接放到 iframe.srcdoc 就能预览，这个方案实现起来很容易。
  - 如果生成的代码是多个文件，涉及到框架 / 组件 / 依赖，预览方案要复杂很多。
  - 考虑到想切入 AI Coding 赛道的产品很多，每个人都去实现一个预览服务，成本很高。
  - 可以做一个通用的 code-preview 服务，提供 API 供第三方接入，支持预览任意类型的项目代码，包括单文件 / 多文件。
- 这个 code-preview 服务，可以用 go 实现，基于 docker + 预置镜像支持各类项目的预览需求。
  - 先制作几套常用的代码模板，打包成 docker 镜像，包括 vite + react/nextjs
  - 用 go 实现一个服务管理模块, 接收上游传递的代码包, 根据预览的项目类型，选用特定的 docker image 启动 docker 容器，挂载要预览的代码文件到容器
  - 需要评估预览服务的启动耗时（文件传输耗时，容器启动耗时），需要支持并发请求
- code-preview 服务跟 AI Coding 业务完全解耦，业务方请求 AI 生成完代码，请求 code-preview 服务的 API 拿到预览地址，通过 iframe.src 预览
  - code-preview 服务需要保证稳定性和启动预览的速度，如果因为代码问题导致预览报错，需要把错误信息返回给业务方，以便业务方带上错误请求 AI 修正代码后重新启动预览
  - code-preview 服务按照业务方的 API 调用次数计费
- 跟 bolt 公司用到的 WebContainer 技术有点类似，只不过 WebContainer 是跑在浏览器端，code-preview 服务是跑在云端，code-preview 的接入会更方便，灵活性也会更高。预览速度方面需要调试后才能对比。

- 有套现成的方案是 sandpack ，LobeChat 的 Artifacts 现在用的就是这个。但这货的加载速度有点慢，不能秒开的体验还是差很多的
  - npm install 是可以通过预置镜像提前缓存的
- 就怕用了预置镜像里没用到的组件或者依赖？这个咋解决哇
- 除非不用现代化的工具链，一个 npm install 就注定不可能秒开了

- 从接收文件到启动docker，到挂载页面，整个时长 会不会超过 aicode预览者们的忍耐限度 ？
  - 所以说 预览速度是关键

- 跑在云端的问题是成本不低，浏览器端成本就低多了
  - 云端实现感觉要容易一些 浏览器端看了 WebContainer 的方案 也需要成本 最主要还是速度有点慢
- 跑在客户端，简单的可以用 esm 来实现（React 加一些常用库完全可以应付），亦或是用 CodeSandBox 私有化部署。WebContainer 是闭源的

- 去年我搞了个在浏览器 wasm + web-worker 跑构建的实现了，而且支持React/Vue/TS等，但是因为老板突然要搞中台内部计费，雪藏了
  - 不知道你咋实现的，但大概率用到了 esbuild 的 wasm 和 esm 来实现？像 CodeSandBox 是在浏览器端实现了一个简易版的 webpack。http://esm.sh 这个项目支持很多 package 的打包策略

- 这玩意的关键是上下文长度，否则ai还没浏览完代码，已经把前面的忘光了。目前ai编程跑不了大项目，不是因为ai不够聪明，上下文长度是一个决定性的因素。因为学新忘旧，所以会出现不限于：重复创建文件/调用错误的函数名/遗忘关键代码/遗忘数据库表名……等等问题，而所有这些都是因为上下文长度不够。
  - 这问题也能解决 把架构规划和代码生成拆分成不同的子任务。生成单个代码文件的子任务，不需要感知整体的上下文

- 现在正是刚需，速度是关键，抢先跑通能快速拉用户。各家 IDE 半年内可能跟进集成预览，但先发优势能锁住客户。做成 code-preview API，按需计费，商业化也有戏。

- 这个我们已经搞2年了，最初是仿照 Replit，后面商业模式国内一直没跑通。
# discuss-coding-ai
- ## 

- ## 我最近有个奇怪的发现，ai写go的质量特别高。如果Python代码oneshot可用50%的话，go能到80%。
- https://x.com/virushuo/status/1904915286010081529
- 个人感觉 Go/TS >> Python >>>>> Rust/C++/Swift

- 语法简单，版本兼容性好，开源质量高。从某种角度来说，更接近自然语言。 Python 本来是语法简明的脚本，但是经过几十年的迭代，越来越臃肿了。

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
