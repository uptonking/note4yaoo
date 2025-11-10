---
title: lib-aikit-langgraph-examples
tags: [examples, langgraph]
created: 2025-08-11T08:47:49.014Z
modified: 2025-08-11T08:47:56.335Z
---

# lib-aikit-langgraph-examples

# guide

- not-yet ❓
  - model routing: 可参考 UniRoute

- resources
  - [langgraph examples | docs](https://langchain-ai.github.io/langgraph/examples/)
# popular
- https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart /apache2/202506/python/ts
  - Get started with building Fullstack Agents using Gemini 2.5 and LangGraph
  - https://x.com/JvShah124/status/1933016336113791159
    - Gemini 2.5 + LangGraph = Build Research Agents That AUTONOMOUSLY Crawl the Web, Cite Sources & Solve Complex Queries.
    - Backend: Python (FastAPI) + LangGraph for orchestrating multi-step workflows
    - Pluggable AI: Gemini 2.5 by default, but swap in Claude/Mistral via API keys
    - Tools: Google Search API + room to add LlamaIndex, custom APIs, etc.
  - https://github.com/zhouruiliangxian/Qwen-Fullstack-LangGraph-Quickstart
    - 原项目基于 Google Gemini 实现，并使用 Google 搜索获取内容。我替换为通义千问（Qwen），并使用 Tavily 作为搜索引擎。

- https://github.com/langchain-ai/agent-chat-ui /1.2kStar/MIT/202505/ts/inactive
  - https://agentchat.vercel.app/
  - Web app for interacting with any LangGraph agent (PY & TS) via a chat interface.
  - a Next.js application which enables chatting with any LangGraph server with a `messages` key through a chat interface.
  - By default, the Agent Chat UI is setup for local development, and connects to your LangGraph server directly from the client. 
  - 基于langchain实现
  - [[Question] LangGraph server deployment example _202504](https://github.com/langchain-ai/agent-chat-ui/issues/89)
    - can you provide a link to a langgraph project which uses best practices that I can deploy locally to test this UI with?
    - here's a repo which contains a few different agents, including generative UI ones: https://github.com/langchain-ai/langgraphjs-gen-ui-examples
  - [Required approach for the backend? _202506](https://github.com/langchain-ai/agent-chat-ui/issues/145)
    - The backend should be Langgraph server API compatible. So either by using the langgraph CLI or their docker containers.
  - https://github.com/langchain-ai/create-agent-chat-app
    - A CLI tool to quickly set up a LangGraph agent chat application.
    - a frontend chat application (Next.js or Vite), along with up to 4 pre-built agents. 
    - You can use this code to get started with a LangGraph application, or to test out the pre-built agents
  - 🍴 forks
  - https://github.com/MyThinkTank-AI/mtt-web-prototype
- https://github.com/langchain-ai/langgraphjs-gen-ui-examples /MIT/202505/ts
  - A collection of generative UI agents written with LangGraph.js
  - This repository contains a series of agents intended to be used with the Agent Chat UI 

- https://github.com/langchain-ai/langgraph-builder /NALic/202504/ts
  - provides a powerful canvas for designing cognitive architectures of LangGraph applications.
  - After designing an architecture with the canvas, LangGraph Builder enables you to generate boilerplate code for the application in Python and Typescript. 
  - Code generation in LangGraph Builder is powered by  https://github.com/langchain-ai/langgraph-gen-py /MIT/python/jinja, a CLI tool that allows you to auto-generate a LangGraph stub from a specification file.

- https://github.com/ahmad2b/canvas-callback /MIT/202503/ts
  - an open-source implementation that demonstrates how to transform AI chat interfaces into interactive visual workspaces using LangGraph's interrupt for human-in-the-loop workflows.
  - Interactive Demo: Practical travel planning agent showcasing the patterns in action
  - Canvas UX Pattern: A dedicated workspace alongside chat for rich, interactive content
  - Human-in-the-Loop: LangGraph interrupts for collecting structured user input
  - Interrupt Handling: Type-based routing system for different interrupt types
  - Modular Architecture: Clean separation between UI, state management, and agent logic
  - Canvas Callback is designed as a focused, accessible implementation to help you understand and integrate the Canvas UX pattern using LangGraph interrupts. Once you've understand these core concepts, you may want to explore LangChain's OpenCanvas for advanced features like memory systems, custom actions, and artifact versioning.

- https://github.com/langchain-ai/open-canvas /4.8kStar/MIT/202505/ts/inactive
  - https://opencanvas.langchain.com/
  - A better UX for chat, writing content, and coding with LLMs.
  - Open Canvas is an open source web application for collaborating with agents to better write documents. 
  - It is inspired by OpenAI's "Canvas"
  - Open Source: All the code, from the frontend, to the content generation agent, to the reflection agent is open source and MIT licensed.
  - Built in memory: Open Canvas ships out of the box with a reflection agent which stores style rules and user insights in a shared memory store. 
  - allowing you to start the session with your existing content, instead of being forced to start with a chat interaction.
  - ⏳ Artifact versioning: All artifacts have a "version" tied to them, allowing you to travel back in time and see previous versions of your artifact.
  - [is this repo still active? _202507](https://github.com/langchain-ai/open-canvas/issues/356)
  - [Support Diff-based edits _202412](https://github.com/langchain-ai/open-canvas/issues/210)
    - Many models support Search + Replace blocks that would make edits faster and make using more powerful and expensive models practical.
    - You can do this with the highlight to edit feature. On the backend, that takes the highlighted text, along with 200 (if I remember correctly, it's somewhere around there) characters before & after and only regenerates that.
    - Why did you choose to have the DOM show where the highlighted content (text or code) on the canvas was rather than using the CodeMirror API?
      - I wasn't aware it existed haha. We use the built in API and not DOM for the markdown renderer

- https://github.com/langchain-ai/open-agent-platform /1.6kStar/MIT/202508/ts/inactive
  - https://oap.langchain.com/
  - open-source, no-code agent building platform.
  - Open Agent Platform provides a modern, web-based interface for creating, managing, and interacting with LangGraph agents.
  - RAG Integration: First-class support for Retrieval Augmented Generation with LangConnect.
  - Agent Supervision: Orchestrate multiple agents working together through an Agent Supervisor.
  - Authentication: Built-in authentication and access control.
  - An agent is a custom configuration on-top of an existing LangGraph graph. This is the same concept as an `assistant`, in the LangGraph API.
  - OAP does not require a standalone backend server to be running in order for the web app to work. However, if you want to use the RAG features, you will need to have the LangConnect server running on its own. 
  - All agents you intend to use with OAP must be LangGraph agents, deployed on LangGraph Platform.

- https://github.com/langchain-ai/open-swe /3kStar/MIT/202508/ts
  - https://swe.langchain.com/
  - open-source cloud-based asynchronous coding agent built with LangGraph. 
  - It autonomously understands codebases, plans solutions, and executes code changes across entire repositories—from initial planning to opening pull requests.
  - 🧊 Open SWE’s sandbox environment is powered by Daytona.io.
  - Planning: Open SWE has a dedicated planning step which allows it to deeply understand complex codebases and nuanced tasks.
  - Human in the loop: you can send it messages while it's running (both during the planning and execution steps). 
  - Parallel Execution: You can run as many Open SWE tasks as you want in parallel. Since it runs in a sandbox environment in the cloud, you're not limited by the number of tasks you can run at once.
  - automatically create GitHub issues for tasks, and create pull requests which will close the issue when implementation is complete
  - [FAQ - Docs by LangChain](https://docs.langchain.com/labs/swe/faq)
    - For most tasks, you can expect to pay between $0.50 -> $3.00 when using Claude Sonnet 4. 
  - [Introducing Open SWE: An Open-Source Asynchronous Coding Agent _202508](https://blog.langchain.com/introducing-open-swe-an-open-source-asynchronous-coding-agent/)
    - The entire project is open source, built on LangGraph, and designed to be extended.
  - https://github.com/PrasanKumar93/demo-open-swe
    - play with langgraph open swe
- https://github.com/botingw/langgraph-dev-navigator /15Star/MIT/202508/python
  - An opinionated development framework for building production-ready AI agents with LangGraph. 
  - It grounds AI coding assistants (Cursor, Windsurf, Cline) and guides them to use local, official documentation, ensuring reliable, secure, and observable agentic workflows.
  - AI coding assistants are powerful, but their general knowledge can be outdated or lead to plausible-but-incorrect code ("hallucinations"). This repository addresses that by providing a framework to ground an AI assistant in the executable truth of a specific, version-controlled codebase.

- https://github.com/esinecan/skynet-agent /107Star/MIT/202506/ts/inactive
  - AI conversation platform implementing dual-layer memory architecture inspired by human cognition.
  - Dual-Layer Memory
    - Automatic Memory (RAG): Non-volitional background memory using ChromaDB vectors and Google text-embedding-004
    - Conscious Memory: Volitional operations via MCP tools - save, search, update, delete with tags and importance scoring
    - Knowledge Graph: Neo4j-powered relationship mapping with automatic synchronization and retry mechanisms
  - LangGraph-Powered Autopilot
  - LangGraph Integration: Complex autonomous workflows
  - Hybrid Search: Solves subset query limitations
  - [Built an Autonomous AI Agent with LangGraph - Features Dual-Layer Memory, Knowledge Graphs, and Self-Healing Autopilot : r/LangChain _202506](https://www.reddit.com/r/LangChain/comments/1lhr4ag/built_an_autonomous_ai_agent_with_langgraph/)
    - I find letting the model decide to write short term memories when it wants to thru tools introduces a lot of latency. Parallel memory tool + responding doesn’t seem to work well for me. Curious if you are experiencing this as well?
      - I do actually. I need you guys' help on ux design side of this.

- https://github.com/BharathxD/ClaimeAI /55Star/MIT/202508/python/ts
  - https://claime.tech/
  - This AI fact-checking system, built with LangGraph, dissects text into verifiable claims, cross-referencing them with real-world evidence via web searches. 
  - It then generates detailed accuracy reports, ideal for combating misinformation in LLM outputs, news, or any text.
  - The system is split into three main parts: Claim Extractor, Claim Verifier, Fact Checker
  - Each component has its own configuration options in their config/ folders. I've spent a lot of time fine-tuning these settings

- https://github.com/AOSSIE-Org/Perspective /MIT/202508/python/ts
  - https://perspective-aossie.vercel.app/
  - Perspective analyzes your news or social feed and presents credible counter-narratives from reliable sources—helping you think critically, reduce bias, and see the full picture. 
  - FastAPI Server: A high-performance API server handling requests, content analysis, and response delivery.
  - Content Analyzer: Processes incoming articles or posts to identify the dominant narrative.
  - Counter-Narrative Engine: Uses advanced AI and NLP techniques to generate alternative perspectives and reasoned analyses.
  - LangChain & Langgraph: Frameworks to manage chains of reasoning and workflow orchestration for coherent narrative generation.
  - VectorDB: A vector database for storing semantic embeddings to efficiently retrieve and compare content.
  - langchain用的很少，仅prompts/schema/langchain_groq

- https://github.com/simonebittidev/Parallax /202505/python/ts
  - https://parallax.chat/
  - an application designed for reflection and dialogue. 
  - Users can submit a thought, opinion, or short text, and Parallax will rewrite it from three distinct perspectives: opposing, neutral, and empathetic.

- https://github.com/usman-faisal/api-flow /202507/python/ts
  - https://api-flow-lyart.vercel.app/
  - An AI-powered tool that translates plain English commands into multi-step API workflows, automating the entire testing process.
  - An AI-powered engine (using Google Gemini & LangGraph) takes your request, creates a multi-step plan, calls the APIs, and even cleverly passes data (like auth tokens) between steps
  - Backend: FastAPI, LangGraph, Python, A Google Gemini API Key
  - Frontend: Next.js, React, TypeScript

- https://github.com/langchain-ai/chat-langchain /6kStar/MIT/202508/python/ts
  - https://chat.langchain.com/
  - an implementation of a chatbot specifically focused on question answering over the LangChain documentation. 
  - Built with LangChain, LangGraph, and Next.js.
  - https://github.com/langchain-ai/chat-langchainjs /MIT/202503/ts/inactive
    - https://chatjs.langchain.com/
    - Built with LangChainjs, and Next.js.

- https://github.com/lalanikarim/langgraph-mcp-pipeline /MIT/202503/python
  - This project demonstrates the use of the Model Context Protocol (MCP) with LangGraph to create workflows that generate prompts and AI-generated images based on a given topic. 
  - These scripts utilize the Comfy MCP Server to generate AI image prompts and AI images.
  - [AI Image Generation with LangGraph and MCP - YouTube _202504](https://www.youtube.com/watch?v=rq69zhxZS-8)
# workflow
- https://github.com/LangGraph-GUI/LangGraph-GUI /196Star/MIT/202506/ts
  - https://langgraph-gui.github.io/
  - Visual node-edge graph GUI editor for LangGraph and run with local LLM or online API
  - an user-friendly graphical interface for interacting with SvelteFlow frontend and fastAPI backend using LLM such ollama or other api key.
  - https://github.com/LangGraph-GUI/LangGraph-GUI-backend /MIT/202605/fastapi
    - The backend supports running LangGraph-GUI workflow json using localLLM such ollama.
  - https://github.com/LangGraph-GUI/LangGraph-GUI-Svelte

- https://github.com/hrhrng/gragraf /202507/python/ts
  - Gragraf is a workflow orchestration application similar to Dify or n8n, built with LangGraph and React. 
  - It provides a visual canvas to build and execute graphs of nodes, including HTTP requests, code execution, conditional branching, and AI agents.
  - React Flow, LangGraph, uv

- https://github.com/clash402/taskflow /MIT/202508/python/ts
  - https://taskflow-one-gules.vercel.app/
  - AI-powered task orchestrator built with LangGraph and FastAPI
  - Taskflow turns natural-language instructions into multi-step backend tasks using AI agents and tool orchestration.
  - Powered by LangGraph, it plans, routes, and executes actions—tracking every step and adapting as needed. Each step is logged, and a built-in reflection node allows it to replan if something goes wrong.
  - Frontend: Next.js, Tailwind CSS, React Query
  - Backend: FastAPI (tool interfaces + execution logic)
  - AI Framework: LangChain (retrieval + prompt chains), LangGraph
  - Storage: ChromaDB, SQLite
  - langchain用的很少

- https://github.com/mrwadams/langgraph-flow-designer /MIT/202507/js
  - https://langgraph-flow-designer.vercel.app/
  - A visual flow designer for creating and managing LangGraph workflows. 
  - This interactive tool allows you to design, edit, and export complex graph-based workflows with an intuitive drag-and-drop interface
  - Interactive Canvas: Pan, zoom, and navigate large workflows with ease
  - React 19: Modern React with hooks for state management
  - SVG-based drawing area with zoom/pan and grid overlay

- https://github.com/nMaroulis/agent-smith /202507/python/ts
  - https://nmaroulis.github.io/agent-smith/
  - AgentSmith is a developer-first, visual framework for building, testing, and exporting LangGraph-based AI agents.
  - describe flows in natural language, define custom state/message schemas, and generate full runnable Python code
  - Drag & Drop Agent Builder: Design nodes, edges, and async flows using a canvas powered by React Flow.
  - Visually define `TypedDict`-based agent state and message schemas.
  - Modify each node’s logic directly in a Monaco (VSCode-style) editor.
  - Built-in support for OpenAI, Anthropic, Hugging Face Transformers, and local LLMs, currently Llama.cpp
  - Frontend	React Flow + TailwindCSS + Monaco Editor
  - Backend	  Python + FastAPI + LangChain + LangGraph
  - Storage	  SQLite / TinyDB / Local JSON

- https://github.com/nyvyn/autonomais /MIT/202504/ts
  - a typeScript library created to streamline the deployment and coordination of multiple AI agents
  - built on LangGraph and LangChain
  - The key addition of this library is to move the configuration of the graph workflows to attributes of the nodes.
  - Conditional nodes use langchain LCEL expression to determine the next node to route too. In practice, this is the function configured as part of a conditional edge for a graph: addConditionalEdges.

- https://github.com/Erickrus/langgraph-editor /MIT/202405/python
  - a visual editor for langgraph workflow. 
  - It is based on litegraph.js as its workflow engine (the same as ComfyUI). You can add, remove, and layout different nodes as you wish, get the workflow as you wish.
# starter
- https://github.com/tyl-paul-lapczynski/learn-langgraph /202506/jupyter
  - learn-langgraph with local lm studio following docs

- https://github.com/langchain-ai/new-langgraph-project /MIT/202508/python
  - This template demonstrates a simple application implemented using LangGraph, designed for showing how to get started with LangGraph Server and using LangGraph Studio, a visual debugging IDE.
  - https://github.com/langchain-ai/new-langgraphjs-project /MIT/202506/ts
    - This template demonstrates a simple chatbot implemented using LangGraph.js, showing how to get started with LangGraph Server and using LangGraph Studio, a visual debugging IDE.

- https://github.com/langchain-ai/agent-inbox-langgraphjs-example /MIT/202501/ts
  - a bare minimum code example to get started with the Agent Inbox with LangGraph.js

- https://github.com/GetsEclectic/langgraph-agent-template /MIT/202508/python/ts
  - starter template for building AI agents with LangGraph, featuring MCP integration, chat UI, and LangSmith observability.

- https://github.com/engagepy/LangGraph-Multi-Tool-Agent /202507/python/ts
  - https://lang-graph-multi-tool-agent.vercel.app/
  - A comprehensive multi-agent system built with LangGraph that provides a wide range of tools and capabilities through a modular, well-organized architecture.
  - https://github.com/tobySolutions/multi-agent-arch-gaia
    - shows how to use LangGraph for a multi-agent system setup

- https://github.com/esurovtsev/langgraph-hitl-fastapi-demo /202507/python/js
  - A minimal working example of a Human-in-the-Loop (HITL) agent using LangGraph and FastAPI. 
  - This demo shows how to pause a LangGraph agent, wait for user input from a frontend, and resume execution — using embedded mode and a simple React UI.
  - https://github.com/kturung/Langgraph-Multi-Agent-HITL-Form /202503/ts/inactive
    - showcasing Langgraph's capabilities for Multi-Agent Collaboration (Swarm-Agents) and Human In The Loop (HITL) interactions.

- https://github.com/KirtiJha/langgraph-interrupt-workflow-template /MIT/202506/python/ts
  - Production-ready LangGraph interrupt template with modern web interface for building human-in-the-loop AI workflows. 
  - FastAPI backend + Next.js frontend
  - langchain用的很少
  - This starter kit provides everything you need to create interactive AI applications that can pause execution, request user input, and resume processing based on user decisions.

- https://github.com/loock-ai/langgraph-chat-app /202508/ts
  - 这是一个使用 Next.js 和 LangGraphJS 构建的智能聊天应用。应用集成了 OpenAI 的语言模型，通过 LangGraph 提供结构化的对话流程。

- https://github.com/blaxel-templates/template-langgraph-ts /MIT/202508/ts
  - A template implementation of a conversational agent using LangGraph TypeScript and GPT-4. 
  - This agent demonstrates the power of LangGraph for building sophisticated workflow-based AI agents with tool integration, state management, and graph-based execution patterns with full TypeScript type safety.
  - Tool integration support with conditional logic
  - Conditional routing and decision-making capabilities

- https://github.com/nngb102/langgraph-nextjs-template /MIT/202505/ts
  - A starter template for building chat applications using LangGraph and Next.js. 
  - This template provides a foundation for creating AI-powered chat experiences with streaming capabilities and modern UI components.
  - State management with LangGraph

- https://github.com/assistant-ui/assistant-ui-starter-langgraph /202508/ts
  - assistant-ui starter project for langgraph.
  - https://github.com/assistant-ui/assistant-ui-langgraph-interrupt

- https://github.com/MrGaoGang/langgraph-mcp-example /202507/ts
  - langgraph use mcp example

- https://github.com/langchain-ai/langgraphjs-studio-starter /MIT/202409/ts/inactive
  - Example LangGraph.js project made to run in LangGraph Studio
# examples
- https://github.com/codemilestones/TinyCodeBase /apache2/202509/python
  - 本项目是一个轻量级的代码智能系统，包含了RAG（检索增强生成）、Agent（智能代理）和评估系统的完整实现。
  - 项目从[TinyRAG](https://github.com/KMnO4-zx/TinyRAG)扩展而来，专注于代码场景的优化和实践。
  - [之前有多嫌弃大模型框架，现在用 LangGraph 就有多香 - 知乎 _202509](https://zhuanlan.zhihu.com/p/1946396924342177830)

- https://github.com/akveo/ai-cookbook /MIT/202507/ts
  - a set of use cases demonstrating how to build AI-featured applications.
  - LangGraph + Next.js: Agent streams LLM tokens to the client application. In the demo app, state is persisted in memory
  - MCP: TypeScript and Python MCP servers implementations. Integration MCP servers with LangGraph servers. STDIO and SSE transport protocols

- https://github.com/meghrp/webresearch-agent /202507/python/ts
  - a langgraph agent that uses gemini to perform web backed research on a topic.
  - use the cli_research.py file to accept a research question as an arg or via stdin.

- https://github.com/notJust-dev/AiAgentRunJS /202503/ts/inactive
  - An AI agent demo that can execute JavaScript code using LangGraph.js
  - [Building your first AI Agent with LangGraph _202504](https://www.notjust.dev/blog/langgraph-ai-agent-genezio)

- https://github.com/iinm/coding-agent-langgraph /202503/ts/inactive
  - An example implementation of a CLI coding agent built with LangGraph.js.
  - Tools: exec_command, write_file, patch_file, tmux, tavily_search
  - https://github.com/iinm/dotfiles/tree/main/agent
    - A more lightweight version without LangGraph

- https://github.com/zedems01/AutoX-app /202507/python/ts/提交多
  - https://achillenguessie.vercel.app/
  - LangGraph AI agent-based system that leverages real-time trends and news to automate wide range content creation and publication, from X posts and threads to full blog articles.
  - LangGraph+FastAPI backend and a Next.js frontend.
  - Image Generation
  - Content can be published directly to X or exported for use.
  - The workflow can run independently or include optional Human-in-the-Loop (HiTL) checkpoints for review and editing
  - Live Progress Dashboard: Provides a real-time overview of the multi-agent workflow, including task status and output previews.

- https://github.com/Shelex/llm-reasoning /202508/ts
  - attempt to enhance llm answers with LangGraph, RAG and dynamic prompting with COT, CCOT, GOT, SOT
  - RAG approach contains hybrid retrieval via vector+bm25 search and reranking.

- https://github.com/max-d3v/geo_toolkit /202507/python/ts
  - GEO Tools is a comprehensive FastAPI-based platform that helps you understand and optimize how your company or brand is positioned in Large Language Model (LLM) responses. 
  - Built with OpenAI's web research capabilities and LangGraph for intelligent workflow orchestration.
  - Uses OpenAI's web search for real-time data
  - Competitive Intelligence: Generates dominance graphs showing competitor positioning

- https://github.com/blaxel-templates/template-similar-company-finder /MIT/202508/ts
  - A LangGraph-powered agent that finds and analyzes similar companies, leveraging Qdrant for data storage, Exa for research, and Gmail for report delivery. 
  - This agent leverages multiple data sources including Exa search, Qdrant vector database for persistent storage
  - Intelligent similar company discovery using Exa search and web data
  - Vector-based data storage and retrieval using Qdrant for persistent analysis
  - Performs comprehensive market analysis across 5 dimensions with 40+ comparison points per company.
  - Multi-dimensional analysis including market positioning, business models, and financials
  - https://github.com/blaxel-templates/template-sales-kpi-reporter
  - https://github.com/blaxel-templates/template-corporate-cortex
    - This repository is a template implementation of a Corporate Knowledge Agent using the Blaxel SDK and LangChain.

- https://github.com/mayooear/ai-company-researcher /202501/ts/inactive
  - An AI agent that automates company research and lead prospecting (powered by langgraph and firecrawl)

- https://github.com/UtkarshTheDev/ai-math-assistant /MIT/202508/ts
  - command-line calculator powered by Google's Gemini AI that understands natural language and provides step-by-step explanations of calculations.

- https://github.com/bracesproul/langgraphjs-examples /202503/ts
  - a series of example TypeScript projects which implement LangGraph.js agents.
  - The following projects all use LangSmith, LangGraph Studio and Cloud, as well as the LangGraph.js and LangChain.js libraries.
  - https://github.com/Dsazz/langgraph-playground /202409/ts/inactive
    - projects built with LangChain and LangGraph

- https://github.com/kenokim/ai-interview /202508/ts
  - A web-based service that allows you to conduct mock interviews with an AI interviewer, powered by LangGraph and LLMs. 
  - It is designed to help users practice their interviewing skills and receive automated feedback.
  - Frontend: A React application built with Vite and TypeScript, styled with Tailwind CSS and Shadcn UI. 
  - Backend: A Node.js server built with Express and TypeScript. It uses LangGraph to implement a stateful, multi-agent AI that can ask technical questions, follow-ups, and evaluate answers.
  - Versatile Interviewer Personas: Choose your desired interview style (e.g., challenging, friendly) to prepare for various environments.

- https://github.com/horizontime/FlowGenius /202508/ts
  - An AI-native note-taking app that leverages LangGraph to automatically research topics, populate note entries, and intelligently organize your ideas.
  - a modern, Electron-based note-taking application designed from the ground up with AI at its core.
  - Rich Text Editing: Full-featured EditorJS-based editor with headers, lists, quotes, and more
  - All data stored locally in SQLite database
  - Data Persistence: SQLite database with proper foreign key relationships
  - LangGraph Integration: Powered by LangGraph workflow with conditional logic and validation

- https://github.com/FreakQnZ/Samvaada /202507/python/ts
  - an Agentic AI Application built using LangGraph to Communicate with Enterprise Database (MySQL) in Natural Language and retrieve data back in a similar Fashion

- https://github.com/tavily-ai/crawl2rag /202507/python/ts
  - https://crawl-to-rag.tavily.com/
  - Turn Any Website into a Searchable Knowledge Base and Chat with it using Tavily and MongoDB. 
  - Use Tavily's crawling endpoint to extract and sitemap content from a webpage URL, then embed it into a MongoDB Atlas vector index for retrieval.
  - Query your crawled data through a conversational agent that provides citation-backed answers while maintaining conversation history and context. The agent intelligently distinguishes between informational questions (requiring vector search) and conversational queries (using general knowledge).
  - Smart Question Routing: Automatic detection of informational vs. conversational queries
  - Persistent Memory: Conversation history and context preservation using LangGraph-MongoDB checkpointing
  - Session Management: Thread-based conversational persistance and vector store management

- https://github.com/kubowania/ai-agent-mongodb /202505/ts/inactive
  - In this tutorial we will build an AI Agent in Express.js using LangGraph with MongoDB to build conversational apps using an agentic approach.

- https://github.com/mongodb-developer/LangGraph.js-MongoDB-Example /apache2/202408/ts/inactive
  - demonstrates how to use LangGraph with MongoDB for building and managing AI agents and conversational applications 
  - Implements a RESTful API using Express.js for chat interactions
  - Integrates with MongoDB Atlas for storing and retrieving conversation data
  - Includes a tool for employee lookup using MongoDB Atlas vector search

- https://github.com/kubowania/ai-agent-mongodb /202505/ts
  - build an AI Agent in Express.js using LangGraph with MongoDB to build conversational apps using an agentic approach.

- https://github.com/harishdeivanayagam/rowfill /283Star/AGPL+EE/202503/ts
  - https://www.rowfill.com/
  - Open-source unstructured data (PDFs, Images, Audiofiles) processing platform built for knowledge workers
  - 似乎没用langgraph
  - Rowfill helps extract, analyze, and process data from complex documents, images, PDFs and more with advanced AI capabilities.
  - Advanced OCR & Processing: Extract text, tables, and handwriting from any document with high precision
  - Custom Actions: Create tailored workflows with automated task processing
  - Supports Local LLMs like Llama, Mistral also supports OpenAI vision models

- https://github.com/flemx/realtime-langgraph-agent /202508/python/ts
  - Multi Agent Realtime Voice with livekit and langgraph, searching linkedin profiles for personalised recommendations

- https://github.com/PR-HARIHARAN/GeoChat-Agent /202507/python/ts
  - Conversational AI agent for geospatial analysis using LangChain, LangGraph, Groq, and Google Earth Engine.

- https://github.com/lalanikarim/comfy-mcp-server /MIT/202503/python/inactive
  - A server using FastMCP framework to generate images based on prompts via a remote Comfy server.
  - https://github.com/lalanikarim/langgraph-mcp-pipeline /MIT/202503/python
    - This project demonstrates the use of the Model Context Protocol (MCP) with LangGraph to create workflows that generate prompts and AI-generated images based on a given topic. 
    - These scripts utilize the Comfy MCP Server to generate AI image prompts and AI images.

- https://github.com/getzep/graphiti/tree/main/examples/langgraph-agent /202504/jupyter/inactive
  - [Using LangGraph and Graphiti | Zep Documentation](https://help.getzep.com/graphiti/integrations/lang-graph-agent)
  - The following example demonstrates building an agent using LangGraph. 
  - Graphiti is used to personalize agent responses based on information learned from prior conversations
  - Graphiti is a framework for building and querying temporally-aware knowledge graphs
  - A knowledge graph is a network of interconnected facts. 
  - Each fact is a "triplet" represented by two entities, or nodes ("Kendra", "Adidas shoes"), and their relationship, or edge ("loves"). 
  - Graphiti powers the core of Zep

- https://github.com/davialabs/davia /MIT/202509/archived
  - The easiest way to build apps from your Python code
  - With Davia, you define your logic in Python, and Davia generates the user interface, handles real-time updates, and manages the backend.
  - Works with any Python application, including LangGraph agents.

## eg-vercel-aisdk

- https://github.com/lokeswaran-aj/next-langgraph-example /MIT/202411/ts/inactive
  - an example Gen AI app built with Langgraph.js, Next.js and Vercel's AI SDK

- https://github.com/ahmad2b/customer-feedback-analysis-ai-agent /202410/python/ts/inactive
  - This project is a Customer Feedback Analysis AI Agent that generates insights and action items based on customer feedback.
  - It is powered by LangGraph, Vercel AI SDK, gpt-4o-mini, FastAPI, and Next.js.

- https://github.com/Ashot72/Multi-Modal-Chat /202503/ts/inactive
  - Multi-Modal Next.js Chat App with Vercel AI SDK & LangGraph.js
  - Users can ask questions, analyze uploaded images, convert content to audio, generate and download charts, display videos, and create AI-generated images.
  - A key feature is the use of custom LangChain.js callback events, enabling seamless streaming. 
  - 使用了langchain message/runnable/tools
  - [Multi-Modal Next.js Chat App with Vercel AI SDK & LangGraph.js - YouTube](https://www.youtube.com/watch?v=6ZWi-TQI-l8)

- https://github.com/StabRise/scaledp-chat /AGPL/202505/python/inactive
  - This is backend project for ScaleDP Chat. Chat over the ScaleDP git repository.
  - It is FastAPI RAG backend based on (LangGraph and LangCain) for the frontend chat based on AI SDK

- https://github.com/Redpandanot/GenUI-SalesAgent /202509/ts/inactive
  - Uses langgraph and ai/sdk to create a generate UI

- https://github.com/auth0-samples/auth0-assistant0 /MIT/202510/python/ts
  - Assistant0: An AI Personal Assistant Secured with Auth0
  - [Build an AI Assistant with LangGraph, Vercel, and Next.js: Use Gmail as a Tool Securely _202504](https://auth0.com/blog/genai-tool-calling-build-agent-that-calls-gmail-securely-with-langgraph-vercelai-nextjs/)
  - [How to build an AI Assistant with LangGraph and Next.js _202508](https://auth0.com/blog/genai-tool-calling-build-agent-that-calls-calender-with-langgraph-nextjs/)
    - We will no longer need Vercel's AI SDK, as we will be using LangGraph's React SDK to stream response tokens to the client

- https://github.com/bracesproul/gen-ui-python /202407/python/ts/inactive
  - Generative UI web application built with LangChain Python, AI SDK & Next.js

- eg
  - https://medium.com/@sirsho29/build-smarter-ai-apps-with-this-langgraph-vercel-ai-sdk-starter-template-8d150e484bf8
# utils/fwk
- https://github.com/pguso/ai-agents-from-scratch /MIT/202511/js
  - [Building LangChain & LangGraph Concepts From Scratch (Next Step in My AI Agents Repo) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1opt2q9/building_langchain_langgraph_concepts_from/)

- https://github.com/ibbybuilds/aegra /265Star/apache2/202510/python
  - https://aegra.dev/
  - Open source LangGraph Platform alternative - Self-hosted AI agent backend with FastAPI and PostgreSQL. 
  - Zero vendor lock-in, full control over your agent infrastructure.
  - Drop-in Replacement: Use existing LangGraph Client SDK, API Compatibile
  - FastAPI + PostgreSQL backend
  - Custom auth: JWT/OAuth/Firebase/NoAuth
  - Self-hosted LangGraph Platform alternative that actually lets you use real auth (Supabase, Firebase, whatever).
  - Agent Protocol Compliant: Aegra implements the Agent Protocol specification, an open-source standard for serving LLM agents in production.
  - Works seamlessly with LangChain's Agent Chat UI
  - [Open-source LangGraph Platform alternative hits 200 stars - now doing Hacktoberfest : r/LangChain](https://www.reddit.com/r/LangChain/comments/1o6acfc/opensource_langgraph_platform_alternative_hits/)
  - How it uses langgraph-sdk if you compose it requests license key how did you use that ?
    - langgraph-sdk is open source under the MIT license, so you can use it freely. what you’re referring to is langgraph-api, which is under the elastic 2.0 license and does require a license key. it’s used locally when you run langgraph dev, providing an in-memory setup, while the langgraph platform uses the same api with postgres, redis, and other components for persistence and scaling.
    - aegra is an open source alternative to the licensed langgraph-api, so we’re not using any restricted or proprietary code.
  - So i can use langgraph-sdk without that api just wrap everything in fastapi?
    - Pretty sure that’s how N8N does it.
  - [Open-source Agent Protocol implementation - LangGraph Platform alternative : r/LangChain _202508](https://www.reddit.com/r/LangChain/comments/1mgoa6o/opensource_agent_protocol_implementation/)
    - a2a is a protocol for agents to talk to each other. 
    - This is a backend to serve LangGraph agents through HTTP (FastAPI).
    - still uses LangGraph and is backward compatible with LangGraph client SDKs.

- https://github.com/keboola/langgraph-chat-transport /MIT/202508/ts
  - https://github.com/fork-archive-hub/langgraph-chat-transport
  - A transport adapter that bridges LangGraph API streaming events to Vercel AI SDK's `useChat` hook format
  - Transforms LangGraph's SSE message format into the chunk protocol that useChat understands, enabling seamless integration between LangGraph agents and React chat interfaces.
  - Message Types: ai, human, system, tool
  - Tool Calls: Full tool invocation and result streaming
  - SSE Parsing: Robust Server-Sent Events parsing

- https://github.com/mlhommet/LangGraphAdapterVercel /202504/ts/inactive
  - LangGraph Adapter for Next.js / Vercel AI SDK 4
  - Shows how to create a next.js Server Route that connects to a LangGraph server and streams the output to a useChat hooked component 
  - The nodes to stream from are passed to the langgraph invocation (as far as I know, this has to be done client-side, there are no mechanism on Langgraph side to specify which nodes are streamable or not).

- https://github.com/atharvagupta2003/Langgraph-streaming /202508/ts
  - Full stack application for streaming responses of langgraph agents

- https://github.com/ITZSHOAIB/agentic-express /MIT/202503/ts
  - A library to accelerate REST agent app development on top of Express
  - By providing prebuilt utilities, middleware, and patterns, it allows developers to focus on building Langgraph agents without worrying about the underlying REST infrastructure.
  - Langgraph Agent Focus: Designed to complement Langgraph agent development by handling REST concerns.

- https://github.com/FluffBaal/ragas-langgraph-vercel /MIT/202507/ts
  - LangGraph Agent Architecture: Specialized agents for different evolution types
  - Documents → Process → Simple Evolution → Multi-Context → Reasoning → Generate Answers → Retrieve Contexts → Results

- https://github.com/langchain-ai/data-enrichment-js /MIT/202506/ts
  - Producing structured results (e.g., to populate a database or spreadsheet) from open-ended research (e.g., web research) is a common use case that LLM-powered agents are well-suited to handle
  - Here, we provide a general template for this kind of "data enrichment agent" agent using LangGraph in LangGraph Studio
  - It contains an example graph exported from `src/enrichment_agent/graph.ts` that implements a research assistant capable of automatically gathering information on various topics from the web and structuring the results into a user-defined JSON format.

- https://github.com/nickwinder/langgraph-client-cli /202508/ts
  - command-line interface for the LangGraph SDK that provides seamless access to LangGraph assistants, threads, and runs from your terminal.
  - Assistants Management - List, get, create, and delete assistants
  - Threads Management - Create, list, get, delete threads, and retrieve state
  - Runs Management - Create, stream, list, get, and cancel runs with real-time updates
  - File-based Configuration - JSON config files

- https://github.com/AmrAnwar/LangGraph-UI-SDK /MIT/202501/ts/inactive
  - SDK for implementing Langgraph in your frontend in few seconds
  - capable of rendering tools and interacting with interrupt tools
  - 基于 @assistant-ui/react-langgraph, zod
  - [Created LangGraph-ui-sdk package to create Chatbot out of the box : r/LangChain _202411](https://www.reddit.com/r/LangChain/comments/1ghkgvf/created_langgraphuisdk_package_to_create_chatbot/)

- https://github.com/jacoblee93/two-factor-support-agent /MIT/202502/ts
  - LangGraph.js agent that requires authorization before invoking tools
  - Cloudflare Workers for development and hosting
  - Cloudflare D1 for checkpointing and state

- https://github.com/cqzyys/lang-agent /apache2/202508/python/ts
  - 以LangGraph为底层技术来实现的一个可有限编程的Agent配置平台
  - 传统的类WorkFlow项目一般只会将上一个节点的输出作为下一个节点的输入，Lang-Agent允许自定义状态变量，可以作用于节点以及条件边的输入和输出，从而实现更精准的控制。
  - LangGraph, FastApi, HeroUI, ReactFlow
  - ✨ Lang-Agent的设计理念更接近于comfyUI，而不是dify和coze，鼓励使用者开发适应自身业务的节点

- https://github.com/enso-labs/orchestra /apache2/202506/python/ts
  - https://demo.enso.sh/
  - AI Agent Orchestrator built on LangGraph powered by MCP & A2A
  - Base API infrastructure for Composable AI Agents built on LangGraph and powered by the MCP & A2A protocols
  - 未实现human-in-the-loop

- https://github.com/levivoelz/checkpoint-redis /MIT/202410/ts/inactive
  - A TypeScript implementation of a Redis-based checkpoint saver for langgraph. 
  - Based on [How to create a custom checkpoint saver (python).](https://langchain-ai.github.io/langgraph/how-tos/memory/add-memory/#use-in-production)

- https://github.com/lablnet/langgraph-checkpoint-mongodb /MIT/202508/ts
  - A lightweight implementation of MongoDB checkpointer for LangGraph
  - A lightweight implementation of BaseCheckpointSaver that persists checkpoints and writes in MongoDB. 
  - Works out‑of‑the‑box with LangGraph’s serde

- https://github.com/Onelevenvy/flock /950Star/apache2/202508/python/ts
  - 一个基于工作流 workflow 的低代码平台：Flock。
  - 基于 LangChain 和 LangGraph 构建，提供灵活的低代码编排协作代理解决方案，可用于快速构建聊天机器人、RAG 应用和协调多代理团队。
  - 支持聊天机器人、RAG 应用、代理和多代理系统，并具备离线运行能力。

- https://github.com/ArtisanCloud/BrainX /apache2/202507/python
  - 一个智能系统，分析各种媒体格式，整合到知识库，并生成定制内容，包括机器人、洞察和媒体

- https://github.com/yokingma/deepresearch /apache2/202507/ts
  - 基于LangGraph构建的DeepResearch Agent，可以搭配任意搜索引擎、OpenAI接口兼容的模型
  - The code logic referenced Google's Gemini LangGraph Project.

- https://github.com/langchain-ai/langgraph-swarm-py /1.1kStar/MIT/202507/python
  - https://langchain-ai.github.io/langgraph/concepts/multi_agent/
  - A Python library for creating swarm-style multi-agent systems using LangGraph. 
  - A swarm is a type of multi-agent architecture where agents dynamically hand off control to one another based on their specializations. 
  - The system remembers which agent was last active, ensuring that on subsequent interactions, the conversation resumes with that agent.
  - Built-in tools for communication between agents
  - This library is built on top of LangGraph, and comes with out-of-box support for streaming, short-term and long-term memory and human-in-the-loop

- https://github.com/langtail/ai-orchestra /202502/ts
  - Simple orchestration for AI Agents built around Vercel's `streamText`. 
  - Lightweight alternative to LangGraph for agent handoffs and state transitions, similar to OpenAI's Swarm but with more developer control and less magic. 
  - Think of it as a simpler alternative to LangGraph, focused on streaming and agent coordination.
  - Built for Streaming - Native support for Vercel's streamText and AI SDK
  - Similar patterns to OpenAI's Swarm, but more flexible

- https://github.com/philmetzger/ChronaGraph /202502/ts/inactive
  - TypeScript-based framework for building graph-based workflows and AI agents. 
  - Inspired by LangGraph, but with a focus on simplicity, speed, and ease of use.
  - Built-in memory and state handling across nodes
  - Save and resume workflow states with FileCheckpointer
  - Rich event callbacks for monitoring workflow execution

- https://github.com/JoshuaC215/agent-service-toolkit /3.5kStar/MIT/202508/python
  - https://agent-service-toolkit.streamlit.app/
  - toolkit for running an AI agent service built with LangGraph, FastAPI and Streamlit.
  - It includes a LangGraph agent, a FastAPI service to serve it, a client to interact with the service, and a Streamlit app that uses the client to provide a chat interface. 
  - Data structures and settings are built with Pydantic.
  - Advanced Streaming: A novel approach to support both token-based and message-based streaming
  - RAG Agent: A basic RAG agent implementation using ChromaDB

## port-lang

- https://github.com/futurxlab/golanggraph /apache2/202509/go/inactive
  - Lightweight AI Agent SDK inspired from LangGraph, written in Golang, so called golanggraph.
# deep-research
- https://github.com/bytedance/deer-flow /16.1kStar/MIT/202508/python/ts
  - https://deerflow.tech/
  - community-driven Deep Research framework, combining language models with tools like web search, crawling, and Python execution
  - DeerFlow implements a modular multi-agent system architecture designed for automated research and code analysis. 
  - The system is built on LangGraph, enabling a flexible state-based workflow where components communicate through a well-defined message passing system.
  - DeerFlow uses LangGraph for its workflow architecture. You can use LangGraph Studio to debug and visualize the workflow in real-time.
  - DeerFlow now includes a Text-to-Speech (TTS) feature that allows you to convert research reports to speech.

- https://github.com/PacoVK/ollama-deep-researcher-ts /202502/ts
  - This repo is a Typescript edition of the Ollama Deep Researcher.
  - Give it a topic and it will generate a web search query, gather web search results (via Tavily), summarize the results of web search, reflect on the summary to examine knowledge gaps, generate a new search query to address the gaps, search, and improve the summary for a user-defined number of cycles. 
  - It will provide the user a final markdown summary with all sources used.
  - Ollama Deep Researcher is inspired by IterDRAG. This approach will decompose a query into sub-queries, retrieve documents for each one, answer the sub-query, and then build on the answer by retrieving docs for the second sub-query.

- https://github.com/mendableai/firesearch /202506/ts
  - AI-powered deep research tool that breaks down complex queries, validates answers, and provides cited comprehensive results using Firecrawl and LangGraph
# rag/docs/kb
- https://github.com/langchain-ai/rag-research-agent-template /MIT/202412/python/inactive
  - a starter project to help you get started with developing a RAG research agent using LangGraph in LangGraph Studio.
  - [Build language agents as graphs](https://github.com/langchain-ai/langgraph/discussions/722)

- https://github.com/safzanpirani/langgraph-agentic-workflow /202505/python/inactive
  - A simple self correcting and hallucination checking RAG workflow in LangGraph.

- https://github.com/junfanz1/Cognito-LangGraph-RAG-Chatbot /202503/python/inactive
  - This project implements an advanced RAG workflow to enhance question-answering accuracy and reduce LLM hallucinations.
  - It leverages LangGraph to create a stateful, multi-step process that includes document retrieval, relevance grading, and web search fallback

- https://github.com/chitralputhran/Advanced-RAG-LangGraph /MIT/202507/python
  - This is a web application that allows you to upload documents and ask questions about them. 
  - a Streamlit-based web application that implements an advanced RAG pipeline using LangGraph, ChromaDB, and Tavily to enable interactive document-based Q&A with enhanced retrieval and error-handling capabilities.

- https://github.com/ranguy9304/LangGraphRAG /14Star/MIT/202407/python/inactive
  - a terminal-based RAG system implemented using LangGraph. 
  - The architecture is designed to handle queries by routing them through a series of processes involving message history caching, query transformation, and document retrieval from a vector database.

- https://github.com/samitugal/KnowledgeGraphQA-Langgraph /202410/python/inactive
  - AI-powered system generating knowledge graphs from text and answering questions
  - LangChain: For building and managing the AI/LLM pipelines.
  - LangGraph: Used for creating the workflow graph.
  - Neo4j: Graph database for storing and querying the knowledge graph.
  - FastAPI: For creating the API endpoints.
  - Streamlit: For building the user interface.
  - Amazon Bedrock: Alternative LLM provider.
  - Tavily Search API: For web search functionality.

- https://github.com/pedarias/langgraph-rag-mcp /202506/jupyter
  - This repo shows how to build a retrieval-augmented generation (RAG) System using LangGraph documentation and then expose it as a tool using the Model Context Protocol (MCP).

- https://github.com/Feed-dev/RAG-agents-Langgraph /202412/jupyter/inactive
  - RAG agent using Langgraph, Ollama, and Llama3.2. The agent can perform document retrieval, web searches, and generate answers based on the retrieved
  - Pinecone (for vector storage and retrieval)

- https://github.com/riolaf05/langgraph-rag-chatbot /202408/jupyter/inactive
  - Agentic RAG chatbot using Langchain and Langgraph

- https://github.com/GreatHayat/langgraph-corrective-rag /202501/python/inactive
  - CRAG is a strategy for RAG that integrates self-reflection and self-grading mechanisms to enhance the accuracy of responses by evaluating the relevance of retrieved documents.

- https://github.com/Grecil/Corrective-RAG /202503/python/inactive
  - https://github.com/Grecil/Corrective-RAG
  - Implementation of Corrective RAG using LangChain and LangGraph.
# rag/memory
- https://github.com/0xPratikPatil/langgraph-db /MIT/202505/ts/inactive
  - A powerful memory backend for LangGraph.js that provides short-term and long-term memory for your agents using flexible storage providers.
  - Multiple Storage Providers: Seamlessly integrate with Redis, MongoDB, Prisma, and more (Redis currently implemented)
  - Checkpoint Support: Built on top of LangGraph's checkpoint system for reliable state management
  - Flexible Architecture: Abstract base classes allow for easy extension with new providers

- https://github.com/moaaz12-web/Offline-RAG /202508/python/ts
  - Offline single click Docker based RAG solution, built with Typescript, FastAPI, Langgraph, and Ollama

- https://github.com/ilni-ai/simple-agentic-rag-langgraph-nodejs /202504/js/inactive
  - a full-stack AI assistant application that demonstrates the use of LangGraph.js, Gemini API, FAISS vector search, and React Vite Bootstrap UI to build a simple yet RAG app
  - Graph-based state orchestration with LangGraph.js
  - Persistent multi-turn memory using SQLite

- https://github.com/MehulG/memX /MIT/202506/python/js
  - https://mem-x.vercel.app/
  - memX is an open-source real-time shared memory layer designed for agent-based systems powered by LLMs. 
  - Real-time CRDT-style state sync(WebSocket)
  - Pub/Sub updates on change
  - Python SDK (memx-sdk) for easy integration
  - Modern multi-agent setups—whether using LangGraph, Autogen, or custom orchestration—lack a reliable way to share evolving context (state, goals, thoughts) between agents. 
  - memX provides a simple and secure memory layer that agents can read/write from in real-time — no message-passing or controller required.
# ai-coding
- https://github.com/langchain-ai/langgraph-codeact /598Star/MIT/202505/python/inactive
  - This library implements the CodeAct architecture in LangGraph. This is the architecture is used by Manus.im.
  - https://x.com/tuturetom/status/1905605150884200871
    - Manus 背后最核心的技术 CodeAct 论文发布
    - 让 Agent 自己编写 Tool 然后完成 Tool 的调用，形成强大的自给自足机制
# langchainjs
- https://github.com/IBJunior/fullstack-langgraph-nextjs-agent /202509/ts
  - Next.js template for building AI agents with LangGraph.js. 
  - Features MCP integration for dynamic tool loading, human-in-the-loop tool approval, persistent conversation memory with PostgreSQL, and real-time streaming responses. 
  - Built with TypeScript, React, Prisma, and Tailwind CSS.
  - LangGraph.js StateGraph with persistent memory via PostgreSQL checkpointer
  - Full MCP Integration - dynamically load tools from MCP servers (stdio & HTTP)
  - Multi-model support - OpenAI and Google AI out of the box
  - Thread-based persistence - conversations resume seamlessly across sessions

- https://github.com/chrisleekr/langchain-playground /202508/ts
  - In this project, I used LangGraph to build a workflow to analyze New Relic logs.
  - A playground for LangChain.js, LangGraph, Slack, Model Context Protocol (MCP) and other LLM-related tools.
  - This project provides both REST API endpoints or Slack bot integration for interacting with different language models and LangChain and LangGraph workflows.
  - langchain.js: Framework for building applications with LLMs.
  - slack/bolt: Integration with Slack for building Slack apps.
  - fastify: serves as a web server in src/api

- https://github.com/mayooear/ai-pdf-chatbot-langchain /15.8kStar/MIT/202502/ts
  - PDF chatbot agent built with LangChain & LangGraph
  - This monorepo is a customizable template example of an AI chatbot agent that "ingests" PDF documents, stores embeddings in a vector database (Supabase), and then answers user queries using OpenAI (or another LLM provider) utilising LangChain and LangGraph as orchestration frameworks.
  - This template is also an accompanying example to the book Learning LangChain (O'Reilly): Building AI and LLM applications with LangChain and LangGraph.

- https://github.com/johnnybui/okos /202503/ts/inactive
  - a Telegram AI Assistant built with TypeScript, LangGraph, and multiple AI model providers. 
  - Multiple Images input support
  - Okos uses BullMQ to implement robust message processing and reminder systems

- https://github.com/sergueigorbounov/Graph-Multi-Agents /202412/ts/inactive
  - This repository implements a multi-agent graph-based system
  - NestJS, Langchain, Langraph

- https://github.com/Clement-Martzloff/minute-md /MIT/202508/ts
  - https://minute-md.vercel.app/
  - an AI-powered Next.js application that automates meeting report generation. 
  - It processes uploaded TXT, PDF, and DOCX files, synthesizes content using LangChain and Google Gemini models, and displays the generated reports in Markdown format. 
  - Built with Clean Architecture and TypeScript, it features real-time progress tracking.
  - File Processing: Allows users to upload and process various file types (e.g., meeting transcripts, documents) as input for report generation.
  - AI-Powered Content Synthesis: Utilizes LLMs (e.g., via LangChain) to synthesize information from processed documents into structured JSON reports.
  - Markdown Output: Converts structured report data into readable Markdown format for display and export.
  - Progress Tracking & Streaming: Provides real-time feedback on the report generation process, including progress steps and streaming text output.
  - Dependency Injection: Uses a robust dependency injection container (ioc/container.ts) for managing services and their implementations, adhering to Clean Architecture principles.
# langchain
- https://github.com/onyx-dot-app/onyx /15.1kStar/MIT+EE/202510/python/ts
  - https://onyx.app/
  - Onyx is a feature-rich, self-hostable Chat UI that works with any LLM.
  - Onyx comes loaded with advanced features like Agents, Web Search, RAG, MCP, Deep Research, Connectors to 40+ knowledge sources, and more.
  - [Introducing Onyx - a fully open source chat UI with RAG, web search, deep research, and MCP : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nw52ad/introducing_onyx_a_fully_open_source_chat_ui_with/)
    - I’ve tried many other open-source chat tools, and I found that none of them had the mix of things I wanted: a beautiful chat UI + great RAG + deep research.

- https://github.com/apocas/restai /431Star/apache2/202508/python
  - https://apocas.github.io/restai/
  - an AIaaS (AI as a Service) open-source platform. 
  - Built on top of LlamaIndex & Langchain. langchain仅用于dalle_image_generator, LlamaIndex用得多
  - Supports any public LLM supported by LlamaIndex and any local LLM supported by Ollama/vLLM/etc
  - Built-in image generation (Dall-E, SD, Flux) and dynamic loading generators.
  - Image Generation: Supports local and remote image generators. 
    - Local image generators are run in a separate process. 
    - New generators are easily added and loaded dynamically.
    - 本地的图片生成基于diffusers实现， 如 `from diffusers import DiffusionPipeline`;
  - Proxy: Allows management of an OpenAI compatible proxy. LiteLLM is supported out of the box.
  - Projects: There are multiple project types, each with its own features. (rag, ragsql, inference, vision, router, agent)
  - The API is a first-class citizen of RestAI. All endpoints are documented using Swagger.
  - There are two vectorstores supported: ChromaDB and RedisVL
  - https://github.com/apocas/restai-frontend /202505/js/inactive
    - 依赖mui.v5、@reduxjs/toolkit、echarts、mui-datatables、react-d3-tree、recharts

- https://github.com/aymen-000/travel_agent /202508/python/ts/FastAPI
  - AI Travel Agent - Intelligent multi-agent system powered by LangGraph that coordinates specialized AI agents (flight search, hotel booking, activity planning) to provide personalized travel recommendations and assistance
  - AI/ML: LangChain + LangGraph (advanced agent orchestration)

- https://github.com/supreme-gg-gg/multiflex /MIT/202507/python/ts
  - https://multiflex-75bba-1cadf.web.app/
  - Multi-agentic platform that gathers and presents knowledge in creative UI generated on the fly (work in progress)
  - Instead of just text, the AI can present answers as cards, tables, galleries, or custom layouts, choosing the best format for each context.

- https://github.com/therealcyberlord/Vea /MIT/202508/python/ts
  - Vea is a local AI copilot that seamlessly integrates with your Ollama installations. 
  - It provides a modern, web-based interface for interacting with local AI models while leveraging additional capabilities such as web search, mathematical operations, weather information, and image analysis. 
  - Backend: FastAPI, Langchain, LangGraph, LangSmith, and Ollama
  - Frontend: React, TypeScript, TailwindCSS, and Vite
  - langchain用的很少
  - https://github.com/keleshteri/langgraph-mcp-ollama-ts /202504/ts/langchain

- https://github.com/ThalesGroup/fred /apache2/202508/python/ts
  - https://fredk8.dev/
  - Fred is not a framework, but a full reference implementation that shows how to build practical multi-agent applications with LangChain and LangGraph. 
  - Agents cooperate to answer technical, context-aware questions.
  - a Python agentic backend (FastAPI + LangGraph)
  - a Python knowledge flow backend (FastAPI) for document ingestion and vector search
  - a React frontend
  - self-contained and do not require any external dependencies such as MinIO, OpenSearch, or Weaviate.
  - Fred is designed with a modular architecture that allows optional integration with these technologies. 
  - By default, a minimal Fred deployment can use just the local filesystem for all storage needs.
  - Fred agents are LangGraph-based conversational experts
  - 使用了InMemoryLangchainVectorStore, langchain-message/tools

- https://github.com/pipeshub-ai/pipeshub-ai /1.2kStar/apache2/202508/python/ts
  - https://pipeshub.com/
  - The OpenSource Alternative to Glean's Workplace AI
  - PipesHub AI helps you quickly find the right information using natural language search—just like Google.
  - The platform not only delivers the most relevant results but also shows where the information came from, with proper citations, using Knowledge Graphs and Page Ranking
  - Beyond search, our platform allows enterprises to create custom apps and AI agents using a No-Code interface.
  - Knowledge Graph Backbone – All data is seamlessly structured into a powerful knowledge graph.
  - Enterprise-Grade Connectors – Scalable, reliable, and built for secure access across your organization.
  - Modular & Scalable Architecture – Every service is loosely coupled to scale independently and adapt to your needs.
  - [Work AI for all - AI platform for agents, assistant, search](https://www.glean.com/)
  - [Best way to extract data from PDFs and HTML : r/Rag _202510](https://www.reddit.com/r/Rag/comments/1oavnx4/best_way_to_extract_data_from_pdfs_and_html/)
    - At PipesHub, we use docling, pymupdf (faster than docling but need to use layout parser on top of it), ocrmupdf/Azure DI (scanned pdfs).
    - If you are looking for Higher Accuracy, Visual Citations, Cleaner UI, Direct integration with Google Drive, OneDrive, SharePoint Online, Dropbox and more. PipesHub is free and fully open source, extensible. 

- https://github.com/StreetLamb/tribe /1kStar/MIT/202501/python/ts/inactive
  - Low code tool to rapidly build and coordinate multi-agent teams 
  - Prefer to write code instead? Check out Rojak — a Python library designed to orchestrate durable, fault-tolerant multi-agent workflows with ease!
  - Tribe leverages on the langgraph framework to let you customize and coordinate teams of agents easily. By splitting up tough tasks among agents that are good at different things

- https://github.com/AIDC-AI/Pixelle-MCP /271Star/MIT/202508/python
  - https://pixelle.ai/
  - Open-Source Multimodal AIGC Solution based on ComfyUI + MCP + LLM
  - An AIGC solution based on the MCP protocol, seamlessly converting ComfyUI workflows into MCP tools
  - Server-side is built on ComfyUI, inheriting all capabilities from the open ComfyUI ecosystem
  - MCP Server provides functionality based on the MCP protocol, supporting integration with any MCP client (including but not limited to Cursor, Claude Desktop, etc.)
  - MCP Client is developed based on the `Chainlit` framework, inheriting Chainlit's UI controls
  - Integrated the LiteLLM framework, adding multi-model support for Gemini, DeepSeek, Claude, Qwen, and more
  - Flexible Deployment: Supports standalone deployment of Server-side only as MCP Server, or standalone deployment of Client-side only as MCP Client, or combined deployment
  - Unified Configuration: Uses YAML configuration scheme, one config file manages all services
  - https://github.com/Chainlit/chainlit /10.5kStar/apache2/202508/python/ts
    - https://docs.chainlit.io/
    - Build python production-ready conversational AI applications in minutes
    - As of May 1st 2025, the original Chainlit team has stepped back from active development.
    - 依赖langchain、LlamaIndex、ChromaDB
# workflow-not-by-langgraph
- https://github.com/callstackincubator/flows-ai /240Star/MIT/202507/ts
  - https://flows-ai.callstack.com/
  - A lightweight, type-safe AI workflow orchestrator inspired by Anthropic's agent patterns. 
  - Built on top of Vercel AI SDK.
  - Last year, we built Fabrice - an AI agent framework designed to break down complex tasks into smaller steps.
  - We realized that AI agent systems today are essentially modern workflows where each node is an LLM call instead of a traditional function. 
  - The key difference lies not in the framework, but in the nature of these nodes: they have flexible input/output contracts.
  - This insight led us to redefine our approach and focus on an orchestration, so you can connect different (often incompatible input/outputs) together.
  - This library provides a simple, more deterministic way to build AI workflows. You can either explicitly define your workflow with loops and conditionals, or use an orchestrator agent to dynamically break down complex tasks.
  - https://github.com/callstackincubator/fabrice-ai /MIT/202412/ts/inactive
    - A lightweight, functional, and composable framework for building AI agents

- https://github.com/blaxel-templates/template-zendesk-ticket-analyzer /MIT/202508/ts
  - Zendesk Ticket Analysis agent built using the Blaxel SDK. 
  - The agent processes Zendesk support tickets and provides automated analysis including ticket categorization, sentiment analysis, and summary generation.
  - Built with Mastra and TypeScript for robust performance and seamless integration with the Blaxel platform.
# more
