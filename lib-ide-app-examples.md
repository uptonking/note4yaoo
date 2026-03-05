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
  - https://github.com/voideditor/void-builder /MIT/202508/sh
    - This is a fork of VSCodium, which has a nice build pipeline that we're using for Void.
    - The purpose of this VSCodium fork is to run Github Actions. These actions build all the Void assets (.dmg, .zip, etc), store these binaries on a release in voideditor/binaries
  - https://github.com/qinglion/yuejuan-builder
    - 基于 void-builder 的思想，为 qinglion_yuejuan（青狮阅卷 Electron 应用）提供本地/CI 一键打包、校验、上传与版本 JSON 更新的脚本集合。

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
# agent-architecture
- https://github.com/langchain-ai/langgraph-codeact /598Star/MIT/202505/python/inactive
  - This library implements the CodeAct architecture in LangGraph. This is the architecture is used by Manus.im.
  - https://x.com/tuturetom/status/1905605150884200871
    - Manus 背后最核心的技术 CodeAct 论文发布
    - 让 Agent 自己编写 Tool 然后完成 Tool 的调用，形成强大的自给自足机制
# coding-saas
- https://github.com/nutlope/llamacoder /6.8kStar/MIT/202512/ts
  - https://www.llamacoder.io/
  - open source Claude Artifacts – generate small apps with one prompt. 
  - Powered by Llama 3 405B & Together.ai.
  - Llama 3.1 405B from Meta for the LLM
  - Together AI for LLM inference
  - Sandpack for the code sandbox
  - Next.js app router with Tailwind
  - Helicone for observability
  - [Generate an entire app from a prompt using Together AI’s LlamaCoder _20240918](https://ai.meta.com/blog/together-ai-llamacoder/)

- https://huggingface.co/spaces/enzostvs/deepsite/tree/main
  - DeepSite is a coding platform powered by DeepSeek AI, designed to make coding smarter and more efficient. 
  - Tailored for developers, data scientists, and AI engineers, it integrates generative AI into your coding projects to enhance creativity and productivity.
  - Multi Pages: Create complex websites with multiple interconnected pages
  - [How to run 🐳 DeepSite locally](https://huggingface.co/spaces/enzostvs/deepsite/discussions/74)
  - [Request for License Information for the DeepSite Project](https://huggingface.co/spaces/enzostvs/deepsite/discussions/119)
    - DeepSite is using the MIT License

- https://github.com/dulapahv/CodeX /apache2/202512/ts
  - https://codex.dulapahv.dev/
  - an online code collaboration platform that enables real-time coding, cursor sharing, live UI preview, and video communication with integrated Git support—no sign-up required.
  - This project is part of the course "COMPSCI4025P Level 4 Individual Project" at the University of Glasgow.
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
# codebase-utils
- https://github.com/yamadashy/repomix /20.4kStar/MIT/202511/ts/vue
  - https://repomix.com/
  - a powerful tool that packs your entire repository into a single, AI-friendly file.
  - AI-Optimized: Formats your codebase in a way that's easy for AI to understand and process.
  - Token Counting: Provides token counts for each file and the entire repository, useful for LLM context limits.
  - Customizable: Easily configure what to include or exclude.
  - Code Compression: The --compress option uses Tree-sitter to extract key code elements, reducing token count while preserving structure.

- https://github.com/yamadashy/repopack /MIT/202411/ts
  - Repopack is a powerful tool that packs your entire repository into a single, AI-friendly file.
  - AI-Optimized: Formats your codebase in a way that's easy for AI to understand and process.
  - Token Counting: Provides token counts for each file and the entire repository, useful for LLM context limits.
  - Git-Aware: Automatically respects your .gitignore files.
  - 可以将你的代码库打包成一个 AI 友好文件（带有文件的目录结构，文件内容以及提示词），然后可以方便的供给大模型进行分析和使用。思路非常有趣。

- https://github.com/403errors/repomind /202511/ts
  - https://repomind-ai.vercel.app/
  - AI-powered coding assistant using Agentic RAG to chat with any public GitHub repository or developer profile, offering deep code analysis, visual architecture maps, and security audits
  - Using an advanced Context-Aware Engine, RepoMind performs deep code analysis without requiring you to clone repositories.
  - Smart Context Loading: Instead of dumping entire files, RepoMind intelligently selects relevant code snippets based on your query.
  - Multi-File Understanding: Traces dependencies and imports to understand how different parts of the codebase interact.
  - RepoMind uses Context Augmented Generation (CAG), not traditional RAG. We don't chop your code into fragmented vectors; we load full, relevant files into the model's long context window for superior understanding.

- https://github.com/argilla-io/argilla /apache2/202408/python
  - https://docs.argilla.io/
  - Argilla is a collaboration tool for AI engineers and domain experts who need to build high-quality datasets for their projects.
  - Argilla can be used for collecting human feedback for a wide variety of AI projects like traditional NLP (text classification, NER, etc.), LLMs (RAG, preference tuning, etc.), or multimodal models (text to image, etc.). Argilla's programmatic approach lets you build workflows for continuous evaluation and model improvement. 
  - Take control of your data and models
# code-search
- https://github.com/RyanNg1403/agentic-search-vs-rag /MIT/202601/python
  - Experimental validation: Agentic Search (context trees) vs traditional RAG for code retrieval. Agentic wins with 99% fewer tokens and 2× better accuracy. Fully reproducible with automated pipelines.
  - A reproducible experiment comparing traditional vector-based RAG with Agentic Search (context trees) for code retrieval tasks.
  - This experiment validates that context trees with agentic search dramatically outperform traditional RAG for code understanding tasks.
    - 2× better retrieval accuracy (IoU score)
    - 99% fewer tokens used per query

- https://github.com/BurntSushi/ripgrep /55.1kStar/MIT/202507/rust
  - ripgrep recursively searches directories for a regex pattern while respecting your gitignore
  - ripgrep is a line-oriented search tool that recursively searches the current directory for a regex pattern. 
  - By default, ripgrep will respect gitignore rules and automatically skip hidden files/directories and binary files.
  - ripgrep has first class support on Windows, macOS and Linux, with binary downloads available 
  - https://github.com/microsoft/ripgrep-prebuilt /MIT
    - Builds ripgrep on Azure Pipelines for multiple platforms, used by VS Code.
  - https://github.com/microsoft/vscode-ripgrep /MIT/js
    - This is an npm module for using ripgrep in a Node project. It's used by VS Code.
    - In this module's `postinstall` task, it determines which platform it is being installed on and downloads the correct binary from `ripgrep-prebuilt` for the platform.
  - [Try ripgrep in Y minutes](https://codapi.org/try/ripgrep/)
  - [Ripgrep playground](https://codapi.org/ripgrep/)
  - https://github.com/phiresky/ripgrep-all /rust
    - rga: ripgrep, but also search in PDFs, E-Books, Office documents, zip, tar.gz, etc.

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

- https://github.com/github/stack-graphs /871Star/MIT/202503/rust/archived
  - https://docs.rs/stack-graphs/*/stack_graphs/
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

- https://gitlab.com/gitlab-org/rust/knowledge-graph /GitLabEE/202601/rust
  - https://gitlab-org.gitlab.io/rust/knowledge-graph/
  - aims to create a structured, queryable graph database from code repositories to power AI features and enhance developer productivity.

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

- https://github.com/facebookexperimental/semcode /MIT/202601/rust
  - a semantic code search tool for C/C++ codebases that indexes your codebase and allows you to search for functions, types, and code patterns using both exact matches and semantic similarity.
  - Rust indexing is now supported. This just uses treesitter, but all the semcode features are there.
  - Fast indexing of C/C++ codebases using Tree-sitter
  - Interactive query interface with comprehensive command set
  - MCP server for integration with AI code tools
# code-rag
- https://github.com/mixedbread-ai/mgrep /3.2kStar/apache2/202601/ts/平台未开源
  - https://demo.mgrep.mixedbread.com/
  - CLI-native way to semantically grep everything, like code, images, pdfs and more.
  - Natural-language search that feels as immediate as grep.
  - Semantic, multilingual & multimodal (audio, video support coming soon!)
    - Today, mgrep works great on: code, text, PDFs, images. 
  - Web search built-in — query the web alongside your local files with --web.
  - Smooth background indexing via mgrep watch, designed to detect and keep up-to-date everything that matters inside any git repository.
  - Under the hood, mgrep is powered by Mixedbread Search, our full-featured search solution.
    - Every file is pushed into a Mixedbread Store using the same SDK your apps get.
  - 🐛 [Why is it online only ?  _202512](https://github.com/mixedbread-ai/mgrep/issues/97)
    - we use our Mixedbread platform under the hood. It exposes a store that enables semantic search over files with nice abstractions. There are no open source solutions currently that expose such capabilities offline with the same speed, availability and throughput.

- https://github.com/Ryandonofrio3/osgrep /1kStar/apache2/202601/ts
  - Natural-language search that works like grep. Fast, local, and works with coding agents.
  - Semantic: Finds concepts ("auth logic"), not just strings.
  - Local & Private: 100% local embeddings via `onnxruntime-node` ~~transformers.js~~.
  - Adaptive: Runs fast on desktops, throttles down on laptops to prevent overheating.
  - Smart Chunking: Uses tree-sitter to split code by function/class boundaries
  - Deduplication: Identical code blocks (boilerplate, license headers) are embedded once and cached, saving space and time.
  - Semantic Split Search: Queries both "Code" and "Docs" separately to ensure documentation doesn't drown out implementation details, then reranks with ColBERT.
  - Global Batching: A producer/consumer pipeline decouples chunking from embedding. Files are chunked concurrently, queued, embedded in fat batches, and written to `LanceDB` in bulk.
  - Auto-Isolated: Each repository gets its own index automatically.
    - Your first search will automatically index the repository. Each repository is automatically isolated with its own index.
    - If the background server is running (osgrep serve), search goes through the hot daemon; otherwise it falls back to on-demand indexing.
  - osgrep serve
    - Watches the repo (via `chokidar`) and incrementally re-indexes on change.
  - Claude Code Plugin, Opencode Plugin

- https://github.com/blazejp83/hygrep /apache2/202512/python/inactive
  - a self-hosted semantic code search system designed for AI coding agents
  - Semantic + Lexical Retrieval: LanceDB vectors plus SQLite FTS5 with per-query weight overrides
  - Self-Hosted Stack: Dockerized FastAPI backend, llama.cpp/Ollama embeddings, optional reranker + llama.cpp LLM, zero cloud dependencies
  - `hygrep-cli index --watch` now asks the backend to start a watchdog observer so subsequent file saves trigger incremental reindexing.

- https://github.com/yetidevworks/ygrep /MIT/202602/rust
  - fast, local, indexed code search tool optimized for AI coding assistants. 
  - Written in Rust using Tantivy for full-text indexing.

- https://github.com/dbinky/Pommel /MIT/202601/go
  - Local-first semantic code search for AI coding agents.
  - Pommel maintains a vector database of your code, enabling fast semantic search without loading files into context.
  - Hybrid search - Combines semantic vector search with keyword search (FTS5) using Reciprocal Rank Fusion for best-of-both-worlds results.
  - Automatic file system monitoring keeps your index synchronized with code changes. No manual reindexing required.
  - Multi-level chunks - Search at file, class/module, or method/function granularity for precise results.
  - Automatically skips minified JavaScript/CSS files that produce low-quality chunks.
  - [Introducing Pommel - an open source tool to help Claude Code find code without burning your context window : r/ClaudeAI _202601](https://www.reddit.com/r/ClaudeAI/comments/1q0gkn8/introducing_pommel_an_open_source_tool_to_help/)

- https://gitlab.com/gitlab-org/rust/knowledge-graph /gitlab-ee/202510/rust
  - https://gitlab-org.gitlab.io/rust/knowledge-graph/
  - aims to create a structured, queryable graph database from code repositories to power AI features and enhance developer productivity.
  - gitlab-code-parser: A language-agnostic parsing engine powered by `tree-sitter` and other native Rust parsers.
  - database: The persistence layer, powered by the `Kuzu` graph database, for storing and querying the knowledge graph.
  - event-bus: A real-time event system for broadcasting progress and status updates.
  - [The GitLab Knowledge Graph, a universal graph database of your code, sees up to 10% improvement on SWE-Bench-lite : r/Rag _202510](https://www.reddit.com/r/Rag/comments/1nu148l/the_gitlab_knowledge_graph_a_universal_graph/)

    - It’s not a vector DB with embedding (yet), but a graph database called Kuzu. It’s taking your code’s AST and translating that into graph format.
# ide-devtools
- https://github.com/zthxxx/react-dev-inspector /MIT/202412/ts
  - https://react-dev-inspector.zthxxx.me/
  - React component on the browser to its source code in your local IDE instantly
  - How to Use and Configure
    - add the `<Inspector/>` component in your page to reads the source info, and sends it to the dev-server when you inspect elements on browser.
    - integrate the middleware in your framework's dev-server: to receives source path info from API, then call your local IDE/Editor to open the source file.
# code-review
- tips
  - nice-to-have, 非必须流程, 需要可跳过

- https://github.com/qodo-ai/pr-agent /10.2kStar/AGPL/202602/python
  - https://qodo-merge-docs.qodo.ai/installation/locally/
  - https://qodo-merge-docs.qodo.ai/
  - PR Agent - The Original Open-Source PR Reviewer, This repo is not the Qodo free tier
  - PR-Agent is an open-source, AI-powered code review agent and a community-maintained legacy project of Qodo.
  - It is distinct from Qodo’s primary AI code review offering, which provides a feature-rich, context-aware experience. Qodo now offers a free tier that integrates seamlessly with GitHub, GitLab, Bitbucket, and Azure DevOps for high-quality automated reviews.
  - ~~似乎必须先存在 pr url 后, 才能使用此工具~~
  - 🏘️ CLI args → PRAgent.handle_request() → GitProvider.get_diff_files() → PR Processing (token handling) → AI Handler → Publish results
    - all git providers implement the same `GitProvider` interface, which abstracts away whether the diff comes from GitHub, GitLab, or a local repository.
    - `LocalGitProvider`: Uses `gitpython` library to interact with local .git directory, Creates a `PullRequestMimic` object to simulate PR structure; Works with /review and /describe commands
  - Fast & Affordable: Each tool (/review, /improve, /ask) uses a single LLM call (~30 seconds, low cost)
  - Handles Any PR Size: Our PR Compression strategy effectively processes both small and large PRs
  - Customizable: JSON-based prompting allows easy customization of review categories and behavior via configuration files
  - Platform Agnostic:
    - AI Models: OpenAI GPT, Claude, Deepseek, and more
    - Deployment: CLI, GitHub Actions, Docker, self-hosted, webhooks
    - Git Providers: GitHub, GitLab, BitBucket, Azure DevOps, Gitea
  - `LocalGitProvider` cannot review uncommitted changes directly.
    - git add -A
    - git commit -m "WIP: changes for review"
    - pr-agent --pr_url=main review
    - git reset HEAD~1
    - error: Getting labels is not implemented for the local git provider
      - LocalGitProvider doesn't support labels (this is a known limitation). harmless.
  - pr必须在单独的branch: LocalGitProvider is designed to compare branches
    - LocalGitProvider compares: Current branch (where you run the command from) **Against** the branch specified in --pr_url
    - git checkout brWithNewCommits
    - pr-agent --pr_url=baseBr review

- https://github.com/techdebtgpt/pr-agent /31Star/apache2/202512/ts/inactive
  - An AI-powered tool that automatically analyzes pull requests and code changes using advanced AI models (Claude, GPT, Gemini). 
  - Available as both a CLI tool for local development and a GitHub Action for CI/CD integration.
  - PR Agent can leverage your project's architecture documentation for context-aware analysis.
  - PR Agent integrates with Semgrep for comprehensive static analysis, detecting security vulnerabilities and code quality issues.
  - pr-agent analyze --staged           # Analyze staged changes
  - pr-agent analyze --full --verbose   # Full analysis with details
  - ? 似乎只能执行命令，不能添加提示词

- https://github.com/diffray/diffray /MIT/202601/ts
  - https://diffray.ai/cli
  - AI-powered code review CLI for git changes
  - A CLI tool that runs multiple AI agents to review your code changes. Each agent specializes in different aspects: bugs, security, performance, code style. 
  - Works with Claude Code, Cursor Agent, OpenCode, or Codex CLI.
  - ? 似乎只能执行命令，不能添加提示词
  - How is it different from diffray.ai? The cloud platform automatically learns from your team's review feedback and generates rules. This CLI version requires manual rule configuration but gives you full control and runs locally.
  - Prerequisites
    - Git - your project must be a git repository
    - diffray uses external AI tools to analyze code. You need to install and authorize one of them: claude-code, codex-cli, opencode, cursor-agent
  - Creating Custom Rules:  Rules connect agents to files. They tell diffray: "Run this agent on these files".
    - By default, diffray runs ALL agents on ALL changed files. 
    - with rules you can add extra instructions for specific file types
  - AI isn't perfect. diffray is tuned for low false positives (fewer wrong alerts) rather than finding every possible issue.
  - Can I use it in CI/CD? Yes! Use --json flag for machine-readable output
  - How much does it cost? The CLI is free, but uses Claude AI which has API costs. With Claude Code CLI, costs are typically $0.01-0.05 per review.
    - Want automated reviews directly in GitHub Pull Requests? Sign up at diffray.ai - connect your repo and get AI review comments on every PR automatically.
  - diffray uses multiple specialized AI "agents" that each focus on one type of problem: bug, security, performance, consistency
  - [Windows: CLI executors fail with command line length errors on large diffs _202601](https://github.com/diffray/diffray/issues/2)
    - Pass prompts via stdin instead of CLI args to avoid command line length limits

- https://github.com/Gentleman-Programming/gentleman-guardian-angel /580Star/MIT/202602/shell/NoDeps
  - Provider-agnostic code review using AI
  - Use whichever AI CLI you have installed
  - Use Claude, Gemini, Codex, OpenCode, Ollama, LM Studio, GitHub Models, or any AI to enforce your coding standards.
  - Zero dependencies. Pure Bash. Works everywhere.
  - Gentleman Guardian Angel runs on every commit, validating your staged files against your project's `AGENTS.md` (or any rules file). 
  - gga run: Runs code review on currently staged files. Uses intelligent caching by default to skip unchanged files.
  - Highly configurable - File patterns, exclusions, custom rules
  - Smart caching - Skip unchanged files for faster reviews
  - PR review mode - Review full PRs, not just last commit
  - 🐛
    - 手动安装存在bug, 用下面的命令修复
    - cp ~/Documents/repos/ai-ml-llm/all-agi-coding/gentleman-guardian-angel/lib/pr_mode.sh   ~/.local/share/gga/lib/pr_mode.sh &&  chmod +x ~/.local/share/gga/lib/pr_mode.sh &&  gga --version

- https://github.com/kodustech/kodus-ai /925Star/AGPL+EE/202602/ts
  - https://kodus.io/
  - Ship better code faster with personalized, context-aware code reviews.
  - open-source AI agent that reviews your code like a real teammate — but one that never gets tired of doing pull requests.
  - Kody (our agent) plugs into your Git workflow, learns how your team writes code, and starts reviewing PRs automatically. You decide what matters — performance, security, readability, or all of the above.
  - 安装复杂, 必须使用docker
  - Custom Review Policies — Create review guidelines in plain language, or any language of your choice, that align with your team's engineering principles and practices.
  - Native Git Integration — Seamlessly integrates with your existing workflow, providing detailed feedback directly in pull requests.
  - open-source vs cloud vs enterprise
    - open-source 不支持 Quality Metrics, Custom Integrations, 10 rules
    - cloud 不支持 Custom Integrations, unlimited rules
  - [Code Review is a pain (so we built this) : r/opensource](https://www.reddit.com/r/opensource/comments/1kawpbm/code_review_is_a_pain_so_we_built_this/)
    - At Kodus, the code review engine (which is the core of the product) is fully open source. You can use it, modify it, and run it without any closed dependencies.
    - The commercial parts, like the UI dashboard or premium integrations, are totally optional and don’t block anyone from running Kodus locally with the core AI working. The goal is to make it easy for any team to use Kody in an open, customizable, and self hosted way if they want.
    - About the .ee. files: yeah, there are still some references to them in the main repo, and we get how that can be confusing. The core engine already works without those parts, but the current setup doesn’t make that obvious. That’s exactly why we’re working on a separate repo with a fully open source version, to make it clearer and easier to use without any closed components.

- https://github.com/mattzcarey/shippie /MIT/202510/ts/inactive
  - https://shippie.dev/
  - extendable code review and QA agent
  - Shippie uses Large Language Models to review code in your CI/CD pipeline. 
  - 支持在 cicd / cli 使用
    - Shippie also works locally to review files staged for commit. Just add some files to the staging area.
    - npx shippie review

- https://github.com/Nikita-Filonov/ai-review /263Star/apache2/202602/python
  - a developer tool that brings AI-powered code review directly into your workflow
  - AI-powered code review tool for GitHub, GitLab, Bitbucket Cloud
  - ❓ 似乎只能在cicd中使用
  - AI Review runs fully client-side — it never proxies or inspects your requests.
    - AI Review does not store, log, or transmit your source code to any external service other than the LLM provider explicitly configured in your .ai-review.yaml.
    - All data is sent directly from your CI/CD environment to the selected LLM API endpoint (e.g. OpenAI, Gemini, Claude, OpenRouter). No intermediary servers or storage layers are involved.
  - Multiple LLM providers — choose between OpenAI, Claude, Gemini, Ollama, ...
  - Customizable prompts — adapt inline, context, and summary reviews
  - Reply modes — AI can now participate in existing review threads, adding follow-up replies in both inline and summary discussions.
  - AI Review runs automatically in your CI/CD pipeline and posts both inline comments, summary reviews, and now AI-generated replies directly inside your merge requests. 

- https://github.com/lava/backloop /AGPL/202510/python/inactive
  - A fully local code review platform with a built-in feedback loop, to make iterating on agentic code output efficient and fun.
  - It works by spinning up an ad-hoc web server that hosts a GitHub-like code review UI that's linked to the current coding session.

- https://github.com/coderabbitai/ai-pr-reviewer /MIT/202311/ts/archived
  - https://coderabbit.ai/
  - AI-based Pull Request Summarizer and Reviewer with Chat Capabilities.

- https://github.com/sourcery-ai/sourcery /NonOpen
  - https://sourcery.ai/
  - automated code reviewer that will review any pull request on any GitHub repository to provide instant feedback on the proposed changes.
  - Every review will include a summary of the changes, high level feedback, and line by line suggestions/comments (where relevant).
  - We use both OpenAI and Anthropic LLMs to provide pieces of our code reviews. Because of this, we need to send them sections of your code (typically the diff of the PR).

- https://github.com/imbue-ai/vet /AGPL/202602/python
  - a standalone verification tool for code changes and coding agent behavior.
  - Vet ships as an agent skill that coding agents like OpenCode and Codex can discover and use automatically.
  - It reviews git diffs, and optionally an agent's conversation history, to find issues that tests and linters often miss. 
  - Vet is optimized for use by humans, CI, and coding agents.
  - run against hosted providers or local/self-hosted OpenAI-compatible endpoints.
  - [We built Vet, an open-source tool that reviews your coding agents work. : r/codex _202602](https://www.reddit.com/r/codex/comments/1rc8ssk/we_built_vet_an_opensource_tool_that_reviews_your/)

- https://github.com/sanyuan0704/code-review-expert /2kStar/202602/skills
  - Expert code review skill: SOLID, security, performance, error handling, boundary conditions
  - SOLID Principles - Detect SRP, OCP, LSP, ISP, DIP violations
  - Security Scan - XSS, injection, SSRF, race conditions, auth gaps, secrets leakage

- https://github.com/awesome-skills/code-review-skill /87Star/MIT/202602/python
  - A modular code review skill for Claude Code, covering React 19, Vue 3, Rust, TypeScript, Java, Python, C/C++, CSS/Less/Sass, architecture design, and performance optimization.

- https://github.com/qdhenry/Claude-Command-Suite /202601
  - development toolkit providing 148+ slash commands, 54 AI agents, Claude Code Skills, and automated workflows for software engineering tasks. 
  - The suite covers code review, testing, deployment, business scenario modeling, and GitHub-Linear synchronization through structured, repeatable workflows.

- https://github.com/FradSer/dotclaude /202602/python
  - collection of plugins and skills for Claude Code, designed to enhance development workflows with specialized agents and automation tools.

- https://github.com/vercel-labs/openreview /MIT/202603/ts
  - https://openreview.labs.vercel.dev/
  - An open-source, self-hosted AI code review bot. 
  - Deploy to Vercel, connect a GitHub App, and get on-demand PR reviews powered by Claude.
  - Mention @openreview in any PR comment to trigger a review
  - Sandboxed execution — Runs in an isolated Vercel Sandbox with full repo access, including the ability to run linters, formatters, and tests
  - https://x.com/haydenbleasel/status/2029646226707362009
    - self-hosted AI code review bot powered by the Vercel AI Cloud.
# code-security
- https://github.com/lintsinghua/DeepAudit /5kStar/AGPL/202602/python/ts
  - DeepAudit：人人拥有的 AI 黑客战队，让漏洞挖掘触手可及。国内首个开源的代码漏洞挖掘多智能体系统。
  - 小白一键部署运行，自主协作审计 + 自动化沙箱 PoC 验证。
  - 支持 Ollama 私有部署 ，一键生成报告。支持中转站。​让安全不再昂贵，让审计不再复杂。
# more
