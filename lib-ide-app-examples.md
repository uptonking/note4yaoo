---
title: lib-ide-app-examples
tags: [coding, examples, ide, vscode]
created: 2024-08-24T16:30:01.289Z
modified: 2024-08-24T16:30:20.218Z
---

# lib-ide-app-examples

# guide

- pm-ai-coding
  - ai编程类热门产品可以在各大ide的插件市场搜索排序
# popular
- https://github.com/microsoft/vscode /MIT/202501/ts
  - https://code.visualstudio.com/
  - This repository ("Code - OSS") is where we (Microsoft) develop the Visual Studio Code product together with the community.

- https://github.com/trypear/pearai-app /apache2/202409/ts
  - https://trypear.ai/
  - Open Source AI-Powered Code Editor. 
  - A fork of VSCode and Continue
  - Pear has context on your codebase so you can ask questions directly (code is stored locally on your computer).
  - PearAI is in TypeScript/Electron.js
  - PearAI backend is a Python Flask server with Supabase database
  - Logging/Telemetry is done with Axiom

- https://github.com/voideditor/void /MIT/202409/ts
  - https://voideditor.com/
  - the open-source Cursor alternative，主打隐私安全
  - Void is a fork of the of vscode
  - Write code with the best AI tools, retain full control over your data, and access powerful AI features
  - https://x.com/shao__meng/status/1835850141527601330
    - 可基于 @ollama 加载运行本地模型，让自己的代码不会被提交到服务器，实现本地隐私安全；也预留了在线模型 API 模式，在不涉及到隐私时选择，可直接使用任意 LLM。
    - Code Editor: VSCode 
    - Local LLM: Ollama 
    - Codebase chat: Greptile 
    - Doc Search: DocSearch 
    - 如果是在本地运行，模型参数量级确实不能选太大，性能和速度很难兼得。不过如果是企业内部服务器，还是有机会兼顾性能和安全。
    - cursor的代码补全/提示太迅速及时了 这个能做到吗 除了ai的修改代码功能 我最喜欢就是cursor这个功能了 已经依赖了
    - 用cursor的时候我就找过其他开源的竞品（例如http://continue.dev），大部分步骤（例如embedding、apply、llm）在本地跑都不得劲。或许是我机器太差了？而这些还是相当重要的，例如apply这个在chat完成后自动填入代码这个直接使用普通的llm完成度都太差了。

- https://github.com/we0-dev/we0 /202402/ts
  - https://we0.ai/wedev
  - we0 is an AI code editor for development programmers and product managers. same v0, bolt.new, lovable
  - Supports browser-based debugging: Built-in WebContainer environment allows you to run a terminal in the browser, install and run npm and tool libraries.
  - 类似于一个 bolt 的升级版，除了支持生成主流编程语言代码以外，还支持 d2c 模式，上传你的设计稿将1:1为你还原。

- https://github.com/CodeEditorLand/Editor /MIT/202410/ts
  - https://npmjs.org/code-oss-dev
  - We're rewriting VSCode @code with Tauri

- https://github.com/reconsumeralization/CodeCurse /MIT/202404/ts/inactive
  - CodeCurse is not a mere fork but a pioneering set of scripts which automatically merge cursor functionalities into Microsoft's VS Code, resulting in freely-licensed binaries

- https://github.com/stackblitz/bolt.new /MIT/202410/ts
  - https://bolt.new/
  - Bolt.new is an AI-powered web development agent that allows you to prompt, run, edit, and deploy full-stack applications directly from your browser—no local setup required
  - Claude, v0, etc are incredible- but you can't install packages, run backends or edit code. That’s where Bolt.new stands out
  - Full-Stack in the Browser: Bolt.new integrates cutting-edge AI models with an in-browser development environment powered by StackBlitz’s WebContainers.
  - AI with Environment Control: Bolt.new gives AI models complete control over the entire environment including the filesystem, node server, package manager, terminal, and browser console. 
  - Once your free daily token limit is reached, AI interactions are paused until the next day or until you upgrade your plan.
  - https://x.com/oran_ge/status/1842497547010728358
    - Bolt，可以提供写代码、preview、部署网站一条龙服务
- https://github.com/stackblitz-labs/bolt.diy /MIT/202503/ts
  - https://stackblitz-labs.github.io/bolt.diy/
  - the official open source version of Bolt.new, which allows you to choose the LLM that you use for each prompt
  - use any other model supported by the Vercel AI SDK
  - AI-powered full-stack web development for NodeJS based applications directly in your browser.
  - Revert code to earlier versions for easier debugging and quicker changes.
  - Integration-ready Docker support for a hassle-free setup.
  - 💰 bolt.diy source code is distributed as MIT, but it uses WebContainers API that requires licensing for production usage in a commercial, for-profit setting.

- https://github.com/langchain-ai/open-canvas /MIT/202412/ts
  - https://opencanvas.langchain.com/
  - Open Canvas is an open source web application for collaborating with agents to better write documents. 
  - It is inspired by OpenAI's "Canvas", but with a few key differences.
  - Built in memory: Open Canvas ships out of the box with a reflection agent which stores style rules and user insights in a shared memory store. This allows Open Canvas to remember facts about you across sessions.

- https://github.com/TeamCodeStream/codestream-archive /NALic/202408/ts/archived
  - https://github.com/TeamCodeStream/codestream-server
  - they seem to be using the "webview" approach extensively and able to re-use code across IDEs. 
  - 似乎fork了vscode
# code-playgrounds

# coding-engineer
- https://github.com/paul-gauthier/aider /17kStar/apache2/202408/python
  - https://aider.chat/
  - aider is AI pair programming in your terminal
  - Aider works best with GPT-4o & Claude 3.5 Sonnet and can connect to almost any LLM.
  - Aider uses a map of your entire git repo, which helps it work well in larger codebases.
  - Aider has one of the top scores on SWE Bench

- https://github.com/All-Hands-AI/OpenHands /30.8kStar/MIT/202408/python
  - https://docs.all-hands.dev/
  - Welcome to OpenHands, a platform for autonomous software engineers, powered by AI and LLMs (previously called "OpenDevin").
  - OpenHands agents collaborate with human developers to write code, fix bugs, and ship features.
  - OpenHands works best with Docker version 26.0.0+ (Docker Desktop 4.31.0+). You must be using Linux, Mac OS, or WSL on Windows.

- https://github.com/stitionai/devika /18.2kStar/MIT/202408/python/svelte
  - Devika is an advanced AI software engineer that can understand high-level human instructions, break them down into steps, research relevant information, and write code to achieve the given objective.
  - Devika is modeled after Devin, aims to be an open-source alternative to Devin
  - Supports Claude 3, GPT-4, Gemini, Mistral , Groq and Local LLMs via Ollama. For optimal performance: Use the Claude 3 family of models.

- https://github.com/Doriandarko/claude-engineer /202408/python
  - Claude Engineer is an interactive command-line interface (CLI) that leverages the power of Anthropic's Claude-3.5-Sonnet model to assist with software development tasks
  - Comprehensive file system operations (create folders, files, read/write files)

- https://github.com/gpt-engineer-org/gpt-engineer /MIT/202408/python/非开源?
  - https://gptengineer.app/
  - Specify what you want it to build, the AI asks for clarification, and then builds it.
  - gptengineer.app is a commercial project for the automatic generation of web apps. It features a UI for non-technical users connected to a git-controlled codebase. The gptengineer.app team is actively supporting the open source community.

- https://github.com/saoudrizwan/claude-dev /MIT/202409/ts
  - Autonomous coding agent right in your IDE, capable of creating/editing files, executing commands, and more with your permission every step of the way
  - Claude Dev uses an autonomous task execution loop with chain-of-thought prompting and access to powerful tools that give him the ability to accomplish nearly any task

- products
  - https://x.com/0xrandomlabs
    - https://www.ycombinator.com/launches/Lnp-random-labs-an-open-source-agent-that-deeply-understands-you
# ai-manus
- https://github.com/langchain-ai/langgraph-codeact /MIT/202503/python
  - This library implements the CodeAct architecture in LangGraph. This is the architecture is used by Manus.im.
  - https://x.com/tuturetom/status/1905605150884200871
    - Manus 背后最核心的技术 CodeAct 论文发布
    - 让 Agent 自己编写 Tool 然后完成 Tool 的调用，形成强大的自给自足机制
# coding-ai
- https://github.com/vizhub-core/editcodewithai /MIT/202503/ts
  - The premise of this project is to build and iterate an open source AI code editing system. 
  - The core idea is that you can feed this system a set of source code files and high level instructions, and it will return the edited code after some time. 
  - 依赖langchain、llm-code-format
  - It aims to be compatible with many LLMs, and flexible enough to adapt to future models as they come out.

- https://github.com/cline/cline /24.5kStar/apache2/202501/ts
  - Meet Cline, an AI assistant that can use your CLI aNd Editor.
  - Autonomous coding agent right in your IDE, capable of creating/editing files, executing commands, using the browser, and more with your permission every step of the way.

- https://github.com/kodu-ai/claude-coder /AGPL/202503/ts
  - https://www.kodu.ai/
  - Kodu is an autonomous coding agent that lives in your IDE
  - It's a VS Code extension that adapts to your skill level, helping you bring ideas to life faster than ever before. 

- https://github.com/nutlope/llamacoder /202409/ts
  - https://www.llamacoder.io/
  - open source Claude Artifacts – generate small apps with one prompt. 
  - Powered by Llama 3 405B & Together.ai.
  - Llama 3.1 405B from Meta for the LLM
  - Together AI for LLM inference
  - Sandpack for the code sandbox
  - Next.js app router with Tailwind
  - Helicone for observability
  - [Generate an entire app from a prompt using Together AI’s LlamaCoder _20240918](https://ai.meta.com/blog/together-ai-llamacoder/)

- https://github.com/artmoskvin/hide /MIT/202408/go
  - https://hide.sh/
  - Headless IDE for Coding Agents
  - Hide provides containerized development environments for codebases and exposes APIs for agents to interact with them. When given a code repo, Hide spins up a devcontainer, installs the dependencies and provides APIs for codebase interaction. Developers can craft custom toolkits using Hide APIs or use Hide's pre-built toolkits for popular frameworks like Langchain.

- https://github.com/argilla-io/argilla /apache2/202408/python
  - https://docs.argilla.io/
  - Argilla is a collaboration tool for AI engineers and domain experts who need to build high-quality datasets for their projects.
  - Argilla can be used for collecting human feedback for a wide variety of AI projects like traditional NLP (text classification, NER, etc.), LLMs (RAG, preference tuning, etc.), or multimodal models (text to image, etc.). Argilla's programmatic approach lets you build workflows for continuous evaluation and model improvement. 
  - Take control of your data and models

- https://github.com/TabbyML/tabby /apache2/202408/rust
  - https://tabbyml.github.io/tabby
  - Self-hosted AI coding assistant. 
  - An opensource / on-prem alternative to GitHub Copilot.
  - Self-contained, with no need for a DBMS or cloud service
  - OpenAPI interface, easy to integrate with existing infrastructure (e.g Cloud IDE).
  - Tabby 是一个自我托管的 #GitHub #Copliot 开源替代品，自带可视化界面与 #OpenAPI 接口，还支持消费者级别的 #GPU，具有 FP-16 重量加载和各种优化功能，提供了 #Docker 镜像

- https://github.com/meltylabs/melty /MIT/202409/ts
  - https://docs.google.com/forms/d/e/1FAIpQLSc6uBe0ea26q7Iq0Co_q5fjW2nypUl8G_Is5M_6t8n7wZHuPA/viewform
  - Melty, an open source AI code editor for 10x engineers
  - Melty is the first AI code editor that's aware of what you're doing from the terminal to GitHub, and collaborates with you to write production-ready code
  - 两位来自 Replicate 和 Netflix 的工程师开发了 Melty，第一个能够在多个文件中进行大规模修改并与整个工作流程集成的 AI 代码编辑器。

- https://github.com/SilasMarvin/lsp-ai /MIT/202408/rust
  - LSP-AI is an open-source language server that serves as a backend for AI-powered functionality, designed to assist and empower software engineers, not replace them.
  - It offers features like in-editor chatting with LLMs and code completions. Because it is a language server, it works with any editor that has LSP support.
  - In-Editor Chatting
  - Note that speed for completions is entirely dependent on the backend being used. For the fastest completions we recommend using either a small local model or Groq

- https://github.com/morph-labs/rift /apache2/202310/python/inactive
  - https://morph.so/
  - Rift: an AI-native language server for your personal AI software engineer
  - The Rift Code Engine implements an AI-native extension of the language server protocol. The Rift VSCode extension implements a client and end-user interface which is the first step into that future.

- https://github.com/block/goose /apache2/202503/rust/ts
  - https://block.github.io/goose/
  - a local, extensible, open source AI agent that automates engineering tasks
  - an open source, extensible AI agent that goes beyond code suggestions - install, execute, edit, and test with any LLM
  - goose is your on-machine AI agent, capable of automating complex development tasks from start to finish. More than just code suggestions, goose can build entire projects from scratch, write and execute code, debug failures, orchestrate workflows, and interact with external APIs - autonomously.
  - Designed for maximum flexibility, goose works with any LLM and seamlessly integrates with MCP-enabled APIs, making it the ultimate AI-powered assistant

## terminal-ai

- https://github.com/google-gemini/gemini-cli /15.2kStar/apache2/202506/ts
  - a command-line AI workflow tool that connects to your tools, understands your code and accelerates your workflows.
  - Query and edit large codebases in and beyond Gemini's 1M token context window.
  - Generate new apps from PDFs or sketches, using Gemini's multimodal capabilities.
  - Automate operational tasks, like querying pull requests or handling complex rebases.
  - Use tools and MCP servers to connect new capabilities, including media generation with Imagen, Veo or Lyria
  - Ground your queries with the Google Search tool, built in to Gemini.
  - [Google announces Gemini CLI: your open-source AI agent _202506](https://blog.google/technology/developers/introducing-gemini-cli-open-source-ai-agent/)
  - [Gemini CLI: your open-source AI agent | Hacker News _202506](https://news.ycombinator.com/item?id=44373754)

- https://github.com/openai/codex /29.7kStar/apache2/202506/rust/ts
  - Lightweight coding agent that runs in your terminal
  - [Introducing Codex | OpenAI _202505](https://openai.com/index/introducing-codex/)
  - [Support for local / other LLMs _202504](https://github.com/openai/codex/issues/26)
    - The current logic supports the openai sdk, but we are excited to review contributions that would decouple this if done without introducing significant complexity to the project.
    - This project is currently using the /responses endpoint from OpenAI's API. Ollama has compatibility with some OpenAI API endpoints, but the /responses endpoint is not included yet.
  - [Codex CLI is Going Native · openai/codex · Discussion _202505](https://github.com/openai/codex/discussions/1174)
    - We're planning to continue merging bugfixes in the TypeScript implementation, while we get the Rust implementation to experience and feature parity in the coming weeks.

- https://github.com/anthropics/claude-code /202506/NonOpen
  - https://docs.anthropic.com/s/claude-code
  - an agentic coding tool that lives in your terminal, understands your codebase, and helps you code faster
  - [open source? · Issue #59 · anthropics/claude-code _202502](https://github.com/anthropics/claude-code/issues/59)
    - We currently don't have plans to open source it.

## vscode-ext-ai

- https://github.com/continuedev/continue /21.3kStar/apache2/202508/ts
  - https://docs.continue.dev/
  - Continue is the leading open-source AI code assistant. You can connect any models and any context to build custom autocomplete and chat experiences inside VS Code and JetBrains
  - Tab to autocomplete code suggestions
  - [Continue 实现原理 · Pines-Cheng/blog _202505](https://github.com/Pines-Cheng/blog/issues/108)

- https://github.com/twinnydotdev/twinny /MIT/202408/ts
  - https://twinny.dev/
  - The most no-nonsense, locally or API-hosted AI code completion plugin for Visual Studio Code - like GitHub Copilot but completely free and 100% private
  - Operates online or offline
  - Conforms to the OpenAI API standard
  - Chat conversations are preserved
  - Compatible with Ollama, llama.cpp, oobabooga, and LM Studio APIs

- https://github.com/julesmons/recline /MPLv2/202501/ts
  - The AI assistant that seamlessly integrates with VSCode to autonomously create, edit, and run terminal commands; redefining how you code.

## ide-repo-ai

- https://github.com/yamadashy/repopack /MIT/202411/ts
  - Repopack is a powerful tool that packs your entire repository into a single, AI-friendly file.
  - AI-Optimized: Formats your codebase in a way that's easy for AI to understand and process.
  - Token Counting: Provides token counts for each file and the entire repository, useful for LLM context limits.
  - Git-Aware: Automatically respects your .gitignore files.
  - 可以将你的代码库打包成一个 AI 友好文件（带有文件的目录结构，文件内容以及提示词），然后可以方便的供给大模型进行分析和使用。思路非常有趣。
# ide/cde
- https://github.com/pulsar-edit/pulsar /MIT/202501/js
  - https://pulsar-edit.dev/
  - A Community-led Hyper-Hackable Text Editor, Forked from Atom, built on Electron.
  - Designed to be deeply customizable, but still approachable using the default configuration.
  - https://github.com/atom-community/atom /202304/js/fork/inactive
    - Community build of the hackable text editor
  - https://github.com/atom/atom /MIT/202211/js/archived
    - a hackable text editor, built on Electron
    - [Sunsetting Atom - The GitHub Blog _202206](https://github.blog/news-insights/product-news/sunsetting-atom/)

- https://github.com/phcode-dev/phoenix /1.3kStar/AGPLv3/202405/js
  - https://phcode.dev/
  - Phoenix is a modern open-source Code Editor for the web, built for the browser
  - Extension support maintaining full compatibility with Brackets extensions (except brackets-node extensions).
  - Adobe 公司开发过一个代码编辑器 Bracket，现在将其做成了 Web 版，重新命名为 Phoenix，可以当作线上 IDE 使用。
  - 依赖codemirror5、@floating-ui/dom、file-saver、marked、mustache
  - Support for pluggable remote back-ends.
  - Phoenix core will work from a static web server.
- https://github.com/adobe/brackets /MIT/202003/js/archived
  - http://brackets.io/
  - a modern open-source code editor for HTML, CSS and JavaScript that's built in HTML, CSS and JavaScript.
# code-search
- https://github.com/sourcebot-dev/sourcebot /1.9kStar/MIT+EE/202505/ts
  - https://sourcebot.dev/
  - a fast code indexing and search tool for your codebases. 
  - It is built on top of the zoekt indexer, originally authored by Han-Wen Nienhuys and now maintained by Sourcegraph.
  - Multi-repo search: Index and search through multiple public and private repositories and branches on GitHub, GitLab, Bitbucket, Gitea, or Gerrit.
  - Full file visualization: Instantly view the entire file when selecting any search result.
  - [Show HN: Sourcebot, an open-source Sourcegraph alternative | Hacker News _202410](https://news.ycombinator.com/item?id=41711032)

 - https://github.com/sourcegraph/zoekt /apache2/202411/go
    - This is a fast text search engine, intended for use with source code.
    - Zoekt supports fast substring and regexp matching on source code, with a rich query language that includes boolean operators (and, or, not).
    - It can search individual repositories, and search across many repositories in a large codebase.
    - Because of its general design based on trigram indexing and syntactic parsing, it works well for a variety of programming languages.
    - Zoekt also contains an index server and web server to support larger-scale indexing and searching of remote repositories. 
    - This is a Sourcegraph fork of github.com/google/zoekt. It is now the main maintained source of Zoekt.
    - The JSON API supports advanced features including:
      - Streaming search results 
      - Alternative BM25 scoring
      - Context lines around matches
      - the web server exposes a gRPC API that supports structured query objects and advanced search options.
- https://github.com/isker/neogrok /MIT/202502/ts/svelte
  - https://neogrok-demo-web.fly.dev/
  - a frontend for zoekt
  - Neogrok exposes zoekt's search APIs in the form of a modern, snappy UI. Neogrok is a SvelteKit application
- https://github.com/TreeTide/zoekt-underhood /apache2/202203/go/inactive
  - An Underhood UI gateway for Zoekt indices.
  - https://github.com/TreeTide/underhood
    - UnderHood is a code browsing interface backed by Kythe indices.

- https://github.com/google/codesearch /BSD/202406/go
  - Fast, indexed regexp search over large file trees
  - Code Search is a tool for indexing and then performing regular expression searches over large bodies of source code. It is a set of command-line programs written in Go.

- https://github.com/sourcegraph/sourcegraph-public-snapshot /apache2 > private/202306/go/ts/archived
  - https://sourcegraph.com/
  - Sourcegraph makes it easy to read, write, and fix code—even in big, complex codebases.
  - Sourcegraph transitioned to a private monorepo. This repository is a publicly available copy of the sourcegraph/sourcegraph repository as it was just before the migration.
  - Sourcegraph stores most data in a PostgreSQL database. Git repositories, uploaded user content (e.g., image attachments in issues) are stored on the filesystem.
  - [Sourcegraph architecture overview](https://github.com/sourcegraph/sourcegraph-public-snapshot/blob/main/doc/dev/background-information/architecture/index.md)
    - At its core, Sourcegraph maintains a persistent cache of all repositories that are connected to it. It is persistent, because this data is critical for Sourcegraph to function, but it is ultimately a cache because the code host is the source of truth and our cache is eventually consistent.
    - By default, Sourcegraph uses zoekt to create a trigram index of the default branch of every repository so that searches are fast. This trigram index is the reason why Sourcegraph search is more powerful and faster than what is usually provided by code hosts.
    - Sourcegraph also has a fast search path for code that isn't indexed yet, or for code that will never be indexed (for example: code that is not on a default branch).searcher implements the non-indexed search.
    - Syntax highlighting for any code view, including search results, is provided by Syntect server.
    - Code navigation surfaces data (for example: doc comments for a symbol) and actions (for example: go to definition, find references) based on our semantic understanding of code (unlike search, which is completely text based). By default, Sourcegraph provides imprecise search-based code navigation.
  - [GitHub code search vs. Sourcegraph - Sourcegraph docs](https://docs-legacy.sourcegraph.com/@v4.4.2/getting-started/github-vs-sourcegraph)
    - Sourcegraph is a code intelligence platform that makes codebases intelligible by semantically indexing and analyzing all of an organization’s code, providing developers and engineering leaders with a complete understanding of their codebase. 
    - In addition to universal code search across every code host, Sourcegraph has features to help developers find code, understand and answer questions about code, and fix code faster.
    - GitHub allows you to search indexed code, but not all code is indexed.Files over 350 KiB and empty files are excluded.With GitHub, only the default branch is searchable 
    - Sourcegraph offers structural search, and GitHub code search does not offer this search method. 
    - GitHub code search does not offer commit diff search or commit message search.
  - 🍴 forks
  - https://github.com/SINTEF/sourcegraph /apache2/202302/go/ts/inactive
    - a fork of SourceGraph with a few modifications
    - It only contains the opensource code. The proprietary code is removed to make sure it's not used during compilation.
    - It has a Oauth2 Proxy Mode allowing to fetch the user information from the HTTP headers.
  - https://github.com/efritz/sourcegraph /202311/go/inactive
    - [Sourcegraph went dark | Eric Fritz _202408](https://www.eric-fritz.com/articles/sourcegraph-went-dark/)
    - Over my tenure at Sourcegraph I’ve done a fair bit of writing for the engineering blog
    - [Sourcegraph went dark | Lobsters _202408](https://lobste.rs/s/tg5vwi/sourcegraph_went_dark)

- https://github.com/livegrep/livegrep /BSD/202412/cpp/go
  - http://livegrep.com/
  - Livegrep is a tool, partially inspired by Google Code Search, for interactive regex search of ~gigabyte-scale source repositories
  - livegrep builds an index file of your source code, and then works entirely out of that index, with no further access to the original git repositories.
    - The index file will vary somewhat in size, but will usually be 3-5x the size of the indexed text.
    - livegrep memory-maps the index file into RAM, so it can work out of index files larger than (available) RAM, but will perform better if the file can be loaded entirely into memory. 
  - Livegrep uses Google's re2 regular expression engine, and inherits its supported syntax.

- https://github.com/oracle/opengrok /CDDL/202412/java
  - http://oracle.github.io/opengrok/
  - OpenGrok is a fast and usable source code search and cross reference engine, written in Java

- https://github.com/Rajeev-K/eureka /GPLv3/202302/java/inactive
  - Lucene-based search engine for your source code
  - eureka is a web application that harnesses the power of Lucene to index and search your source code.
  - https://github.com/wisercoder/eureka

- https://github.com/salsa-rs/salsa /MIT/202412/rust
  - https://salsa-rs.netlify.app/
  - A generic framework for on-demand, incrementalized computation. 
  - Inspired by adapton, glimmer, and rustc's query system.
  - [Salsa In More Depth (2019.01) - YouTube](https://www.youtube.com/watch?v=i_IhACacPRY&t=1348s)
  - The key idea of salsa is that you define your program as a set of queries. 
    - Every query is used like function K -> V that maps from some key of type K to a value of type V. 
    - Queries come in two basic varieties: inputs/functions

- https://github.com/kythe/kythe /apache2/202412/cpp/google
  - https://kythe.io/
  - Kythe is a pluggable, (mostly) language-agnostic ecosystem for building tools that work with code.
  - Indexer implementations for C++, Go, and Java
  - Compilation extractors for javac, Maven, cmake, Go, and Bazel
  - Sample cross-reference service
  - The Kythe project was founded to provide and support tools and standards that encourage interoperability among programs that manipulate source code
  - 👉🏻 Kythe grew out of our experience creating a large-scale semantic index of cross-references for the enormous, multi-lingual internal codebase at Google
  - What Kythe Provides
    - Language-agnostic graph storage format. Kythe defines a simple, flexible, and portable graph representation that is easy to emit from an instrumented compiler, and for clients to consume.
    - extensible graph schema for a variety of interesting semantic cross-reference data in various languages, including C++, Java, and (soon) Go
    - Analyzers, tools and examples. a self-contained server that can use Kythe data to answer cross-reference queries;
  - https://github.com/TreeTide/underhood /202203/inactive
    - UnderHood is a code browsing interface backed by Kythe indices.
    - With https://github.com/TreeTide/underhood, my goal is to provide a read-only view of code, geared for understanding and debugging. Having to maintain the ability to edit comes with constraints.

- https://github.com/facebookincubator/glean /BSD/202412/haskell/cpp/facebook
  - https://glean.software/
  - System for collecting, deriving and working with facts about source code.
  - Glean is designed around an efficient storage model that enables storing information about code at scale.
  - There is currently full support for: C++, C, Hack, Haskell, JavaScript/Flow
  - We also support the SCIP or LSIF code indexing formats, for: rust, ts, go, java, python, .net
  - [SCIP - a better code indexing format than LSIF | Sourcegraph Blog](https://sourcegraph.com/blog/announcing-scip)
    - Fri-yayy so hacked up native @sourcegraph SCIP support for TypeScript repos in Glean. The SCIP data is protobuf-encoded and typed, so compared to LSIF its about 8x smaller, and can be processed 3x faster.

- https://github.com/rizsotto/Bear /GPL/202411/cpp
  - Bear is a tool that generates a compilation database for clang tooling.
  - The JSON compilation database is used in the clang project to provide information on how a single compilation unit is processed. With this, it is easy to re-run the compilation with alternate programs.
  - Some build system natively supports the generation of JSON compilation database. For projects which does not use such build tool, Bear generates the JSON file during the build process.

- https://gitee.com/koode/kooder /apache2/202306/java/inactive
  - Kooder 是 Gitee 团队开发的一个代码搜索系统，为 Gitee/GitLab/Gitea 提供代码搜索服务
  - Kooder 服务包含两个模块，分别是 gateway 和 indexer（默认配置下 indexer 被集成到 gateway 中）。 
    - 其中 gateway 用来接受来自 HTTP 的索引任务， 对任务进行检查后存放到队列中； 同时 gateway 还接受搜索的请求，并返回搜索结果给客户端。
    - 而 indexer 进程负责监控队列中的索引任务， 并将这些要新增、删除和修改索引的任务更新到索引库中。

- https://github.com/kantord/SeaGOAT /MIT/202503/python
  - https://kantord.github.io/SeaGOAT/
  - local-first semantic code search engine
  - 依赖ripgrep、ChromaDB
  - SeaGOAT is a local search tool that leverages vector embeddings to enable you to search your codebase semantically.
  - SeaGOAT does not rely on 3rd party APIs or any remote APIs and executes all functionality locally using the SeaGOAT server
  - it uses the vector database called `ChromaDB`, with a local vector embedding engine and telemetry disabled by default.
  - SeaGOAT also uses `ripgrep`, a regular-expression based code search engine in order to provider regular expression/keyword based matches in addition to the "AI-based" matches.
  - The preferred character encoding is `UTF-8`. Most other character encodings should also work. 
    - Only text files are supported, SeaGOAT ignores binary files.
  - SeaGOAT needs a server in order to provide a speedy response. It's worth noting that you are able to run SeaGOAT server entirely locally
  - Why is SeaGOAT processing files so slowly while barely using my CPU?
    - SeaGOAT is designed to allow you to use your computer while processing files. 
    - It is an intentional design choice to avoid blocking/slowing down your computer. This design decision does not affect the performance of queries.

- https://github.com/github/stack-graphs /MIT/202503/rust
  - Rust implementation of stack graphs
  - Incremental, zero-config Code Navigation using stack graphs.
  - allow you to define the name resolution rules for an arbitrary programming language in a way that is efficient, incremental, and does not need to tap into existing build or program analysis tools.
  - stack graphs use a graphical notation to define the name binding rules for a programming language. They work equally well for dynamic languages like Python and JavaScript, and for static languages like Go and Java.
  - Our solution is fast — processing most commits within seconds of us receiving your push. It does not require setting up a CI job, or tapping into a project-specific build process.
  - 优点: 生产检验过的方案，但github code search不支持按时间排序
  - 缺点: 方案过于创新，未提供LSIF的转换器过度，SCIP提供了
  - 🚀 [Introducing stack graphs - The GitHub Blog _202112](https://github.blog/open-source/introducing-stack-graphs/)
  - [Allowing folks to optionally specify repo-specific configuration _202112](https://github.com/github/stack-graphs/discussions/46)
    - With something like sourcegraph, end users can upload their own LSIF indices to this end. It would be really great if this were eventually possible with GitHub's code navigation.
  - [Explore whether 'smart code search' (AST, stack graphs, scope graphs) would improve performance beyond the current find/grep based approach. · Issue #38 · SWE-agent/SWE-agent](https://github.com/SWE-agent/SWE-agent/issues/38)
    - GitHub has developed two code navigation approaches based on the open source tree-sitter and stack-graphs library
    - Search-based - searches all definitions and references across a repository to find entities with a given name
    - Precise - resolves definitions and references based on the set of classes, functions, and imported definitions at a given point in your code

- https://github.com/sourcegraph/scip /apache2/202504/go
  - SCIP (pronunciation: "skip") is a language-agnostic protocol for indexing source code, which can be used to power code navigation functionality such as Go to definition, Find references, and Find implementations.
  - If you're interested in writing a new indexer that emits SCIP, check out our documentation on how to write an indexer.
  - [SCIP - a better code indexing format than LSIF | Sourcegraph Blog _202206](https://sourcegraph.com/blog/announcing-scip)
    - Sourcegraph code navigation such as “Go to definition” comes in two flavors: search-based and precise. 
      - Search-based code navigation is available out-of-the-box. It is fast and always available, but it can occasionally return false-positive and false-negative results. 
      - Precise code navigation, on the other hand, requires custom configuration to set up, but the results are compiler-accurate and work across repositories. 
      - While search-based is less powerful, it is a quick and convenient solution. Precise is more powerful, but it also requires more upfront investment to configure.
      - 🔧 Search-based code navigation is powered by tools like ctags and tree-sitter and precise code navigation at Sourcegraph has been powered by LSIF.
      - Precise language indexers first write LSIF to disk, and then users upload the LSIF to our Sourcegraph backend, which processes the LSIF index before storing it in our database. The final result of this pipeline is that users benefit from compiler-accurate code navigation on Sourcegraph that works across multiple repositories.
    - As our usage of LSIF has grown, we have encountered several limitations of the protocol:
      - Slow development velocity caused by the lack of static types. LSIF doesn’t come with a machine-readable schema, and the dynamic graph structure makes it difficult to encode LSIF payloads as a simple set of structs or classes in most programming languages.
      - Slow performance caused the need to hold large in-memory data structures when writing or reading the graph encoding of LSIF payloads.
      - Difficulty of manually debugging raw LSIF payloads caused by the heavy usage of opaque ID numbers to encode the graph structure.
      - Complexity of implementing incremental indexing, which becomes necessary for large codebases. Globally incrementing IDs make it difficult, as well, to update an existing index with new information for only a subset of the documents.
    - Most of these issues boil down to the graph encoding of LSIF, which heavily relies on opaque ID numbers to connect edges and vertices. 
    - To address these problems, we created SCIP as a Protobuf schema that is centered around human-readable string IDs for symbols replacing the concept of ‘monikers’ and ‘resultSet’.
    - The design of SCIP is heavily inspired by SemanticDB 🛢️, another code indexing format that was pioneered in the Scala ecosystem.
    - we anticipate SCIP additionally unblocks the following use-cases that we previously struggled to support with LSIF:
      - Incremental indexing: once implemented, SCIP users will experience shorter waiting time for precise code navigation to become available on Sourcegraph after a git push because our backend only needs to index the files that have changed instead of the entire repository on every commit.
      - Cross-language navigation: once implemented, SCIP users will, for example, be able to navigate between Protobuf and generated Java/Go Protobuf bindings, helping them find relevant code examples that were previously unavailable with both search-based and precise code navigation.

- https://github.com/hound-search/hound /MIT/202307/go/js/inactive
  - Hound is an extremely fast source code search engine. The core is based on this article (and code) from Russ Cox: Regular Expression Matching with a Trigram Index.
  - Hound itself is a static React frontend that talks to a Go backend. 
  - Currently Hound is only tested on MacOS and CentOS, but it should work on any *nix system. Hound on Windows is not supported
  - By default Hound polls the URL in the config for updates every 30 seconds. You can override this value
# ide-devtools
- https://github.com/zthxxx/react-dev-inspector /MIT/202412/ts
  - https://react-dev-inspector.zthxxx.me/
  - React component on the browser to its source code in your local IDE instantly
  - How to Use and Configure
    - add the `<Inspector/>` component in your page to reads the source info, and sends it to the dev-server when you inspect elements on browser.
    - integrate the middleware in your framework's dev-server: to receives source path info from API, then call your local IDE/Editor to open the source file.
# more
