---
title: lib-aikit-langgraph-examples
tags: [examples, langgraph]
created: 2025-08-11T08:47:49.014Z
modified: 2025-08-11T08:47:56.335Z
---

# lib-aikit-langgraph-examples

# guide

# popular
- https://github.com/langchain-ai/agent-chat-ui /1.2kStar/MIT/202505/ts/inactive
  - https://agentchat.vercel.app/
  - Web app for interacting with any LangGraph agent (PY & TS) via a chat interface.
  - a Next.js application which enables chatting with any LangGraph server with a `messages` key through a chat interface.
  - By default, the Agent Chat UI is setup for local development, and connects to your LangGraph server directly from the client. 
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

- https://github.com/LangGraph-GUI/LangGraph-GUI /196Star/MIT/202506/ts
  - https://langgraph-gui.github.io/
  - Visual node-edge graph GUI editor for LangGraph and run with local LLM or online API
  - an user-friendly graphical interface for interacting with SvelteFlow frontend and fastAPI backend using LLM such ollama or other api key.
  - https://github.com/LangGraph-GUI/LangGraph-GUI-backend /MIT/202605/fastapi
    - The backend supports running LangGraph-GUI workflow json using localLLM such ollama.
  - https://github.com/LangGraph-GUI/LangGraph-GUI-Svelte

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

- https://github.com/usman-faisal/api-flow /202507/python/ts
  - https://api-flow-lyart.vercel.app/
  - An AI-powered tool that translates plain English commands into multi-step API workflows, automating the entire testing process.
  - An AI-powered engine (using Google Gemini & LangGraph) takes your request, creates a multi-step plan, calls the APIs, and even cleverly passes data (like auth tokens) between steps
  - Backend: FastAPI, LangGraph, Python, A Google Gemini API Key
  - Frontend: Next.js, React, TypeScript
# workflow
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
# starter
- https://github.com/langchain-ai/agent-inbox-langgraphjs-example /MIT/202501/ts
  - a bare minimum code example to get started with the Agent Inbox with LangGraph.js

- https://github.com/GetsEclectic/langgraph-agent-template /MIT/202508/python/ts
  - starter template for building AI agents with LangGraph, featuring MCP integration, chat UI, and LangSmith observability.

- https://github.com/engagepy/LangGraph-Multi-Tool-Agent /202507/python/ts
  - https://lang-graph-multi-tool-agent.vercel.app/
  - A comprehensive multi-agent system built with LangGraph that provides a wide range of tools and capabilities through a modular, well-organized architecture.

- https://github.com/esurovtsev/langgraph-hitl-fastapi-demo /202507/python/js
  - A minimal working example of a Human-in-the-Loop (HITL) agent using LangGraph and FastAPI. 
  - This demo shows how to pause a LangGraph agent, wait for user input from a frontend, and resume execution — using embedded mode and a simple React UI.

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

- https://github.com/assistant-ui/assistant-ui-starter-langgraph /202508/ts
  - assistant-ui starter project for langgraph.
  - https://github.com/assistant-ui/assistant-ui-langgraph-interrupt
# examples
- https://github.com/akveo/ai-cookbook /MIT/202507/ts
  - a set of use cases demonstrating how to build AI-featured applications.
  - LangGraph + Next.js: Agent streams LLM tokens to the client application. In the demo app, state is persisted in memory
  - MCP: TypeScript and Python MCP servers implementations. Integration MCP servers with LangGraph servers. STDIO and SSE transport protocols

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

- https://github.com/ahmad2b/customer-feedback-analysis-ai-agent /202410/python/ts/inactive
  - This project is a Customer Feedback Analysis AI Agent that generates insights and action items based on customer feedback.
  - It is powered by LangGraph, Vercel AI SDK, gpt-4o-mini, FastAPI, and Next.js.

- https://github.com/mayooear/ai-company-researcher /202501/ts/inactive
  - An AI agent that automates company research and lead prospecting (powered by langgraph and firecrawl)

- https://github.com/notJust-dev/AiAgentRunJS /202503/ts/inactive
  - An AI agent demo that can execute JavaScript code using LangGraph.js
  - [Building your first AI Agent with LangGraph _202504](https://www.notjust.dev/blog/langgraph-ai-agent-genezio)

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
# utils/fwk
- https://github.com/keboola/langgraph-chat-transport /MIT/202508/ts
  - A transport adapter that bridges LangGraph API streaming events to Vercel AI SDK's `useChat` hook format
  - Transforms LangGraph's SSE message format into the chunk protocol that useChat understands, enabling seamless integration between LangGraph agents and React chat interfaces.
  - Message Types: ai, human, system, tool
  - Tool Calls: Full tool invocation and result streaming
  - SSE Parsing: Robust Server-Sent Events parsing

- https://github.com/mlhommet/LangGraphAdapterVercel /202504/ts
  - LangGraph Adapter for Next.js / Vercel AI SDK 4
  - Shows how to create a next.js Server Route that connects to a LangGraph server and streams the output to a useChat hooked component 
  - The nodes to stream from are passed to the langgraph invocation (as far as I know, this has to be done client-side, there are no mechanism on Langgraph side to specify which nodes are streamable or not).

- https://github.com/atharvagupta2003/Langgraph-streaming /202508/ts
  - Full stack application for streaming responses of langgraph agents

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

- https://github.com/jacoblee93/two-factor-support-agent /MIT/202502/ts
  - LangGraph.js agent that requires authorization before invoking tools
  - Cloudflare Workers for development and hosting
  - Cloudflare D1 for checkpointing and state

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

- https://github.com/MehulG/memX /MIT/202506/python/js
  - https://mem-x.vercel.app/
  - memX is an open-source real-time shared memory layer designed for agent-based systems powered by LLMs. 
  - Real-time CRDT-style state sync(WebSocket)
  - Pub/Sub updates on change
  - Python SDK (memx-sdk) for easy integration
  - Modern multi-agent setups—whether using LangGraph, Autogen, or custom orchestration—lack a reliable way to share evolving context (state, goals, thoughts) between agents. 
  - memX provides a simple and secure memory layer that agents can read/write from in real-time — no message-passing or controller required.

- https://github.com/Onelevenvy/flock /950Star/apache2/202508/python/ts
  - 一个基于工作流 workflow 的低代码平台：Flock。
  - 基于 LangChain 和 LangGraph 构建，提供灵活的低代码编排协作代理解决方案，可用于快速构建聊天机器人、RAG 应用和协调多代理团队。
  - 支持聊天机器人、RAG 应用、代理和多代理系统，并具备离线运行能力。

- https://github.com/ArtisanCloud/BrainX /apache2/202507/python
  - 一个智能系统，分析各种媒体格式，整合到知识库，并生成定制内容，包括机器人、洞察和媒体

- https://github.com/yokingma/deepresearch /apache2/202507/ts
  - 基于LangGraph构建的DeepResearch Agent，可以搭配任意搜索引擎、OpenAI接口兼容的模型
  - The code logic referenced Google's Gemini LangGraph Project.

- https://github.com/cqzyys/lang-agent /apache2/202508/python/ts
  - 以LangGraph为底层技术来实现的一个可有限编程的Agent配置平台。 
  - 传统的类WorkFlow项目一般只会将上一个节点的输出作为下一个节点的输入，Lang-Agent允许自定义状态变量，可以作用于节点以及条件边的输入和输出，从而实现更精准的控制。
  - LangGraph, FastApi, HeroUI, ReactFlow

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
# rag
- https://github.com/moaaz12-web/Offline-RAG /202508/python/ts
  - Offline single click Docker based RAG solution, built with Typescript, FastAPI, Langgraph, and Ollama
# langchainjs
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
- https://github.com/Ashot72/Multi-Modal-Chat /202503/ts/inactive
  - Multi-Modal Next.js Chat App with Vercel AI SDK & LangGraph.js
  - Users can ask questions, analyze uploaded images, convert content to audio, generate and download charts, display videos, and create AI-generated images.
  - A key feature is the use of custom LangChain.js callback events, enabling seamless streaming. 
  - 使用了langchain message/runnable/tools

- https://github.com/aymen-000/travel_agent /202508/python/ts/FastAPI
  - AI Travel Agent - Intelligent multi-agent system powered by LangGraph that coordinates specialized AI agents (flight search, hotel booking, activity planning) to provide personalized travel recommendations and assistance
  - AI/ML: LangChain + LangGraph (advanced agent orchestration)

- https://github.com/therealcyberlord/Vea /MIT/202508/python/ts
  - Vea is a local AI copilot that seamlessly integrates with your Ollama installations. 
  - It provides a modern, web-based interface for interacting with local AI models while leveraging additional capabilities such as web search, mathematical operations, weather information, and image analysis. 
  - Backend: FastAPI, Langchain, LangGraph, LangSmith, and Ollama
  - Frontend: React, TypeScript, TailwindCSS, and Vite
  - langchain用的很少

- https://github.com/nyvyn/autonomais /MIT/202504/ts
  - a typeScript library created to streamline the deployment and coordination of multiple AI agents
  - built on LangGraph and LangChain
  - The key addition of this library is to move the configuration of the graph workflows to attributes of the nodes.
  - Conditional nodes use langchain LCEL expression to determine the next node to route too. In practice, this is the function configured as part of a conditional edge for a graph: addConditionalEdges.

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

- https://github.com/pipeshub-ai/pipeshub-ai /apache2/202508/python/ts
  - https://pipeshub.com/
  - The OpenSource Alternative to Glean's Workplace AI
  - Knowledge Graph Backbone – All data is seamlessly structured into a powerful knowledge graph.
  - Enterprise-Grade Connectors – Scalable, reliable, and built for secure access across your organization.
  - Modular & Scalable Architecture – Every service is loosely coupled to scale independently and adapt to your needs.
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
