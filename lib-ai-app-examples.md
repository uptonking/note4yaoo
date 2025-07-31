---
title: lib-ai-app-examples
tags: [ai, examples]
created: 2023-02-08T07:20:33.048Z
modified: 2023-02-08T07:20:48.475Z
---

# lib-ai-app-examples

# guide

# popular
- https://github.com/mudler/LocalAI /MIT/202403/cpp
  - https://localai.io/
  - free, Open Source OpenAI alternative. 
  - Self-hosted, community-driven and local-first. 
  - LocalAI act as a drop-in replacement REST API that’s compatible with OpenAI API specifications for local inferencing. 
  - It allows you to run LLMs, generate images, audio (and not only) locally or on-prem with consumer grade hardware, supporting multiple model families. 
  - Does not require GPU.

- https://github.com/janhq/jan /AGPLv3/202403/ts
  - https://jan.ai/
  - an open source alternative to ChatGPT that runs 100% offline on your computer
  - Nitro is a high-efficiency C++ inference engine for edge computing. It is lightweight and embeddable

- https://github.com/vercel/ai /apache2/202406/ts
  - https://sdk.vercel.ai/docs
  - Build AI-powered applications with React, Svelte, Vue, and Solid
  - Vercel AI SDK abstracts away the differences between model providers, eliminates boilerplate code for building chatbots
  - https://x.com/nicoalbanese10/status/1806680358093541401
    - this is all you need to use chrome's built in ai model with the vercel ai sdk
    - no api keys, no configuration, running locally in the browser
- https://github.com/langtail/ai-orchestra
  - a lightweight TypeScript library for orchestrating AI agents
  - No magic, just simple patterns built around @aisdk 's streamText for managing agent handoffs and state transitions.
  - A lightweight alternative to LangGraph without the complexity.
  - State lives outside the library - you control everything.
- https://github.com/nickscamara/open-deep-research
  - An open source deep research clone. 
  - AI Agent that reasons large amounts of web data extracted with Firecrawl
  - Powered by the @aisdk
  - https://x.com/nickscamara_/status/1886459999905521912
    - This is an experimental clone of Open AI's Deep Research. Instead of using a fine-tuned version of o3, this method uses Firecrawl's extract + search with a reasoning model to deep research the web.
- https://github.com/moeru-ai/xsai /MIT/202502/ts
  - https://xsai.js.org/
  - extra-small AI SDK for Browser, Node.js, Deno, Bun or Edge Runtime
  - xsAI is a series of utils to help you use OpenAI or OpenAI-compatible API.
  - xsAI doesn't depend on Node.js Built-in Modules, it works well in Browsers, Deno, Bun and even the Edge Runtime.

- https://github.com/nicolasmontone/ai-sdk-agents /202502/ts
  - https://ai-sdk-agents.vercel.app/
  - Tools for Vercel AI SDK

- https://github.com/Doriandarko/maestro /202406/python
  - ⛓️ A framework for Claude Opus to intelligently orchestrate subagents.
  - This Python script demonstrates an AI-assisted task breakdown and execution workflow using the Anthropic API. 
  - It utilizes two AI models, Opus and Haiku, to break down an objective into sub-tasks, execute each sub-task, and refine the results into a cohesive final output.
  - Run locally with LMStudio or Ollama
  - Breaks down an objective into manageable sub-tasks using the Opus model
  - Executes each sub-task using the Haiku model
  - Refines the sub-task results into a final output using the Opus model
  - Generates a detailed exchange log capturing the entire task breakdown and execution process
  - Required Python packages: anthropic and rich
  - https://x.com/tuturetom/status/1805823266671775875
    - 基于 Claude 3.5 Sonnet 实现的「多 Agent 调度」框架
    - 同时提供了 Python flask 应用支持 UI Demo 完成多 Agent 演示
    - orchestrator 拆解任务，全局视野调度 sub_agent 

- https://github.com/run-llama/llama-agents /MIT/202407/python
  - llama-agents is an async-first framework for building, iterating, and productionizing multi-agent systems, including multi-agent communication, distributed tool execution, human-in-the-loop, and more!
  - each agent is seen as a service, endlessly processing incoming tasks. Each agent pulls and publishes messages from a message queue.
  - At the top of a llama-agents system is the control plane. The control plane keeps track of ongoing tasks, which services are in the network, and also decides which service should handle the next step of a task using an orchestrator.
  - https://x.com/tuturetom/status/1809445355832111312
    - 多 Agent 框架，使用 Docker/K8S 部署

- https://github.com/dstackai/dstack /MPL/202407/python
  - https://dstack.ai/
  - open-source container orchestration engine designed for running AI workloads across any cloud or data center. 
  - It simplifies dev environments, running tasks on clusters, and deployment.

- https://github.com/DataformerAI/dataformer /apache2/202410/python
  - https://dataformer.ai/
  - Dataformer empowers engineers with a robust framework for creating high-quality synthetic datasets for AI, offering speed, reliability, and scalability
  - We integrate with multiple LLM providers using one unified API and allow you to make parallel async API calls while respecting rate-limits.
# LLM
- https://github.com/songquanpeng/one-api /MIT/202404/go/js
  - https://openai.justsong.cn/
  - OpenAI 接口管理 & 分发系统，支持 Azure、Anthropic Claude、Google PaLM 2 & Gemini、智谱 ChatGLM、百度文心一言、讯飞星火认知、阿里通义千问
  - 可用于二次分发管理 key，仅单可执行文件，已打包好 Docker 镜像，一键部署，开箱即用

- https://github.com/xenova/transformers.js
  - Run Transformers in your browser! We currently support BERT, ALBERT, DistilBERT, MobileBERT, SqueezeBERT, T5, T5v1.1, FLAN-T5, mT5, BART
  - [宝玉 on Twitter: "这有必要吗？"](https://twitter.com/dotey/status/1643801825580122115)
    - 毕竟浏览器有沙盒，相对在本地运行一个没审计过的程序放心一点，但现在浏览器对gpu硬件支持还是拉胯。
    - 这是分布式算力啊，这不就是挖矿嘛

- https://github.com/outlines-dev/outlines /apache2/202408/python
  - https://outlines-dev.github.io/outlines/
  - Robust (structured) text generation.
  - The first step towards reliability of systems that include large language models is to ensure that there is a well-defined interface between their output and user-defined code. Outlines provides ways to control the generation of language models to make their output more predictable.
  - Multiple model integrations: OpenAI, transformers, llama.cpp, exllama2, mamba
  - Simple and powerful prompting primitives based on the Jinja templating engine
  - Fast JSON generation following a JSON schema or a Pydantic model
  - Interleave completions with loops, conditionals, and custom Python functions

## benchmarks-llm

- https://github.com/bigcode-project/bigcodebench /apache2/202408/python
  - https://bigcode-bench.github.io/
  - BigCodeBench is an easy-to-use benchmark for code generation with practical and challenging programming tasks
  - It aims to evaluate the true programming capabilities of large language models (LLMs) in a more realistic setting.
  - The package is built on top of the EvalPlus framework, which is a flexible and extensible evaluation framework for code generation tasks.
  - [2024-06-18] We release BigCodeBench, a new benchmark for code generation with 1140 software-engineering-oriented programming tasks. Preprint is available here
# chatgpt
- app-site
  - https://github.com/LiLittleCat/awesome-free-chatgpt
  - [免费 chatgpt](https://twitter.com/search?q=%E5%85%8D%E8%B4%B9%20chatgpt&src=typed_query&f=live)

- api-free
  - [一口气送了350个免费的key](http://freeopenai.xyz/)

- https://freechatgpt.chat/
  - 类似官网，需要key
  - 可选内置不稳定key

- [ChatGPT API Demo](https://ai.ls/)
  - https://ai.ls/
  - Powered by gpt-3.5-turbo

- [free ChatGPT](https://freegpt.one/)
  - using gpt-3.5-turbo

- [OpenGPT](https://open-gpt.app/)
  - 立即使用海量的 ChatGPT 应用，或在几秒钟内创建属于自己的应用

- https://github.com/lencx/ChatGPT /rust
  - ChatGPT Desktop Application (Mac, Windows and Linux)
  - 国内ip无法访问

## gpt-apps

- https://github.com/n4ze3m/dialoqbase /MIT/202401/ts
  - https://dialoqbase.n4ze3m.com/
  - open-source application designed to facilitate the creation of custom chatbots using a personalized knowledge base
  - open-source application designed to facilitate the creation of custom chatbots using a personalized knowledge base

- https://github.com/binary-husky/gpt_academic /GPLv3/202405/python/js
  - https://github.com/binary-husky/gpt_academic/wiki/online
  - 为GPT/GLM等LLM大语言模型提供实用化交互接口，特别优化论文阅读/润色/写作体验，模块化设计，支持自定义快捷按钮&函数插件，支持Python和C++等项目剖析&自译解功能，PDF/LaTex论文翻译&总结功能，支持并行问询多种LLM模型，支持chatglm3等本地模型。
  - 接入通义千问, deepseekcoder, 讯飞星火, 文心一言, llama2, rwkv, claude2, moss等。

- 写了个基于 ChatGPT 的 AI 维权律师，根据事实和诉求帮当事人生成起诉书。
  - https://twitter.com/imyuanx/status/1641715695762436098
  - https://github.com/imyuanx/ai-lawyer

- https://github.com/nicepkg/gpt-runner
  - Conversations with your files! Manage and run your AI presets!

- https://github.com/Mintplex-Labs/anything-llm /MIT/js/python
  - https://useanything.com/
  - An efficient, customizable, and open-source enterprise-ready document chatbot solution.

- https://github.com/AprilNEA/ChatGPT-Admin-Web /MIT/202312/ts/inactive
  - CAW 是一个自托管网络应用程序，提供开箱即用的用户管理，包括后台界面以及可配置的支付计划和相关支付界面
  - Nest.js + Next.js
  - 开箱即用的用户管理
  - 付费方案配置，一键对接支付接口
  - 关键词过滤、替换保证文本安全

## api

- [https://www.steamship.com](https://www.steamship.com/)
  - SteamShip 开放了 GPT-4 的模型接口，只需要注册SteamShip 账号，无需付费，几行代码直接就能调用 GPT-4

## prompts

- [Open Prompt](https://openprompt.co/)

- https://github.com/verazuo/jailbreak_llms
  - A dataset consists of 15, 140 ChatGPT prompts from Reddit, Discord, websites, and open-source datasets (including 1, 405 jailbreak prompts).
  - 开源了论文中使用的 15, 140 个 ChatGPT 提示，其中包括 1, 405 个越狱提示，收集于 Reddit、Discord、网站和开源数据集。

## gpt-impl

- https://github.com/newhouseb/potatogpt
  - Pure Typescript, dependency free, ridiculously slow implementation of GPT2 for educational purposes

- https://github.com/openai/gpt-2 /MIT/201908/python
  - https://openai.com/blog/better-language-models/
  - Code for the paper "Language Models are Unsupervised Multitask Learners"
- https://github.com/openai/gpt-3 /202009/仅数据
  - GPT-3: Language Models are Few-Shot Learners
# coding-copilot
- products
  - https://copilot.microsoft.com/

- https://github.com/Codium-ai/pr-agent /apache2/202407/python
  - CodiumAI PR-Agent: An AI-Powered Tool for Automated Pull Request Analysis, Feedback, Suggestions
  - aims to help efficiently review and handle pull requests, by providing AI feedbacks and suggestions
  - Our JSON prompting strategy enables to have modular, customizable tools. 
  - We support multiple git providers (GitHub, Gitlab, Bitbucket), multiple ways to use the tool (CLI, GitHub Action, GitHub App, Docker, ...), and multiple models (GPT-4, GPT-3.5, Anthropic, Cohere, Llama2).
  - PR-Agent Pro is a hosted version of PR-Agent, provided by CodiumAI
    - Extra features - emphasize more customization, and the usage of static code analysis, in addition to LLM logic, to improve results. See here for a list of features available in PR-Agent Pro.
  - https://x.com/tuturetom/status/1809053337825989009
    - 自动基于你提交的代码进行分析，给于评论反馈与意见，生成 PR 描述
    - 支持私有化部署和开源模型
    - 针对大的 PR 设计了 PR Compression 策略，可以极大的处理几百个文件的场景

- https://github.com/TabbyML/tabby /apache2/202408/rust
  - https://tabbyml.github.io/tabby
  - Self-hosted AI coding assistant. 
  - An opensource / on-prem alternative to GitHub Copilot.
  - Self-contained, with no need for a DBMS or cloud service
  - OpenAPI interface, easy to integrate with existing infrastructure (e.g Cloud IDE).
  - Tabby 是一个自我托管的 #GitHub #Copliot 开源替代品，自带可视化界面与 #OpenAPI 接口，还支持消费者级别的 #GPU，具有 FP-16 重量加载和各种优化功能，提供了 #Docker 镜像

- https://github.com/rjmacarthy/twinny /995Star/MIT/202403/ts
  - The most no-nonsense locally hosted (or API hosted) AI code completion plugin for Visual Studio Code, like GitHub Copilot but 100% free and 100% private.
  - designed to work seamlessly with: Ollama
# agents-multi
- https://github.com/microsoft/autogen /31.4kStar/MIT/202410/python/jupyter
  - https://microsoft.github.io/autogen/
  - AutoGen is an open-source programming framework for building AI agents and facilitating cooperation among multiple agents to solve tasks.
  - It offers features such as agents capable of interacting with each other, facilitates the use of various large language models (LLMs) and tool use support, autonomous and human-in-the-loop workflows, and multi-agent conversation patterns.

- https://github.com/om-ai-lab/OmAgent /apache2/202407/python
  - OmAgent是一个多模态智能体系统，专注于利用多模态大语言模型能力以及其他多模态算法来做一些有趣的事
  - 包含一个专为解决多模态任务而设计的轻量级智能体框架omagent_core。我们利用这个框架搭建了超长复杂视频理解系统——OmAgent，当然你可以利用它实现你的任何想法。
  - DnCLoop: 受到经典算法思想Divide and Conquer启发，我们设计了一个递归的通用任务处理逻辑，它将复杂的问题不断细化形成任务树，并最终使复杂任务变成一组可解得简单任务。
# open-agent
- https://github.com/modelcontextprotocol/servers /MIT/202411/python
  - https://modelcontextprotocol.io/
  - A collection of reference implementations and community-contributed servers for the Model Context Protocol (MCP). This repository showcases the versatility and extensibility of MCP, demonstrating how it can be used to give Large Language Models (LLMs) secure, controlled access to tools and data sources.
  - Each MCP server is implemented with either the Typescript MCP SDK or Python MCP SDK.
  - https://x.com/alexalbert__/status/1861464485011300839
    - The future of MCP is truly going to be community-led and not controlled by any single entity.
    - Here are some of the highlights I'm seeing from across the industry:
    - Replit is looking into adding MCP support to Agents
    - Sourcegraph has already added MCP to Cody and you can go try it out right now!
    - Zed has added MCP support in their editor, also available to try out!
    - Github Copilot is working with MCP
    - Codeium is using MCP to improve Windsurf's capabilities
  - https://x.com/alexalbert__/status/1861453744216453309
    - we do have a few clients beside Claude desktop that have already integrated MCP in production (Zed, Sourcegraph, etc).

- https://github.com/QwenLM/Qwen-Agent /tongyi/202411/python
  - https://pypi.org/project/qwen-agent/
  - Agent framework and applications built upon Qwen>=2.0, featuring Function Calling, Code Interpreter, RAG, and Chrome extension
  - 基于Qwen2.0的agent框架：Qwen-Agent，它有指令遵循、工具使用、做规划和记忆能力
  - 基于Qwen-Agent的一个Chrome浏览器扩展，一个智能浏览器助手：BrowserQwen, 它可以基于当前页面或文档跟你对话、能记住你浏览过的内容进行总结、可以解决数学问题、数据图表可视化
# llama
- https://github.com/pamelafox/ollama-python-playground /jupyter
  - A dev container with ollama and ollama examples with the Python OpenAI SDK
  - This project is designed to be opened in GitHub Codespaces as an easy way for anyone to try out SLMs (small language models) entirely in the browser.
  - https://x.com/pamelafox/status/1801678164969853034
    - To make it super easy for anyone to try out Ollama (esp teachers/students)
    - I've included an example notebook that walks through completions, prompt eng, few-shots, and RAG

## llama-rewrite

- https://github.com/naklecha/llama3-from-scratch /MIT/202405/jupyter/inactive
  - llama3 implementation one matrix multiplication at a time
# text2image
- https://github.com/Stability-AI/stablediffusion
  - https://github.com/CompVis/stable-diffusion
  - A latent text-to-image diffusion model

- https://github.com/camenduru/stable-diffusion-webui-portable
  - This Project Aims for 100% Offline Stable Diffusion (People without internet or with slow internet can get it via USB or HD-DVD)

- https://github.com/AUTOMATIC1111/stable-diffusion-webui
  - A browser interface based on Gradio library for Stable Diffusion.

- https://github.com/cmdr2/stable-diffusion-ui
  - The easiest way to install and use Stable Diffusion on your computer.

- https://github.com/Nutlope/blinkshot /202410/ts
  - https://www.blinkshot.io/
  - An open source real-time AI image generator. 
  - Powered by Flux through Together.ai.
  - Flux Schnell from BFL for the image model
  - Together AI for inference
# ml-neural-network
- https://github.com/AlloyTeam/netural
  - JavaScript的前向神经网络和反向传播的实现。

- https://github.com/TrevorBlythe/MentisJS
  - A javascript neural network library. 
  - It can train with backpropagation or neural evolution! 
  - [A better alternative to convnetjs](https://github.com/karpathy/convnetjs/issues/122)
    - This library has Deconv layers and other new features that not even convnetjs has.
    - It also doesn't require you to put your data in a custom data type.

- https://github.com/mlc-ai/web-llm
  - Introducing WebLLM, an open-source chatbot that brings language models (LLMs) directly onto web browsers. 
  - We can now run instruction fine-tuned LLaMA (Vicuna) models natively on your browser tab via @WebGPU with no server support.

- https://github.com/photopea/UNN.js
  - Deep Learning in Javascript. Alternative to ConvNetJS, that is 4x faster.
  - [A 4x faster alternative to ConvNetJS](https://github.com/karpathy/convnetjs/issues/115)
    - It has capabilities similar to ConvNetJS, but both training and testing are 4x faster (while still running in a single JS thread on the CPU).

- https://github.com/mil-tokyo/webdnn
  - The Fastest DNN Running Framework on Web Browser

- https://github.com/karpathy/convnetjs
  - Deep Learning in Javascript. Train Convolutional Neural Networks (or ordinary ones) in your browser.
  - [[Question] Why use javascript ?](https://github.com/karpathy/convnetjs/issues/72)
    - Performance-wise there is no reason to believe that JavaScript would perform significantly slower than Python. The reason why Python is used over C++ is not performance, it is the ecosystem.
    - For fast execution Python or C++ might not even be the best for neural networks as GPGPU computing could be the ultimate solution for fast parallel computing of lots of artificial neurons. In that case JavaScript would yield roughly the same performances as Python of C++.

- https://github.com/BrainJS/brain.js
  - robot GPU accelerated Neural networks in JavaScript for Browsers and Node.js
# ml-dl
- https://github.com/visheratin/web-ai /MIT/ts
  - run modern deep learning models directly in the web browser or in Node.js
  - Powered by ONNX runtime. Web AI runs the models using ONNX Runtime, which has rich support for of all kinds of operators.
  - Web worker support. All heavy operations - model creation and inference - are offloaded to a separate thread so the UI does not freeze.

- https://github.com/xenova/transformers.js /js
  - https://huggingface.co/docs/transformers.js
  - State-of-the-art Machine Learning for the web. 
  - Run Transformers directly in your browser, with no need for a server!
  - Transformers.js is designed to be functionally equivalent to Hugging Face's transformers python library
  - Transformers.js uses ONNX Runtime to run models in the browser. The best part about it, is that you can easily convert your pretrained PyTorch, TensorFlow, or JAX models to ONNX using Optimum.

- https://github.com/ml5js/ml5-library /js
  - provides access to machine learning algorithms and models in the browser, building on top of TensorFlow.js

- https://github.com/alibaba/pipcook /ts
  - https://alibaba.github.io/pipcook/
  - provides subprojects including machine learning pipeline framework, management tools, a JavaScript runtime for machine learning, and these can be also used as building blocks in conjunction with other projects.
  - provides access to Python packages by bridging the interface of `CPython` using N-API. so pytorch/tensorflow/scikit is available

- https://github.com/mljs/ml /js
  - Machine learning tools in JavaScript
# audio
- https://github.com/myshell-ai/OpenVoice /MIT/202407/python
  - https://research.myshell.ai/open-voice
  - Instant voice cloning by MyShell
  - Free Commercial Use. Starting from April 2024, both V2 and V1 are released under MIT License. 
  - OpenVoice has been powering the instant voice cloning capability of myshell.ai since May 2023. 
  - 即时语音克隆工具，只需从参考资料中截取一段简短的音频即可实现克隆。可详细控制语音风格，包括情感、口音、节奏、停顿和语调。生成多种语言的语音。
# rag-utils
- https://github.com/rag-web-ui/rag-web-ui /apache2/202502/python/ts
  - RAG Web UI is an intelligent dialogue system based on RAG
# rag-knowledge-base
- https://github.com/pingcap/autoflow /apache2/202411/python
  - https://tidb.ai/
  - pingcap/autoflow is a Graph RAG based and conversational knowledge base tool built with TiDB Serverless Vector Storage.
  - An open source GraphRAG (Knowledge Graph) built on top of TiDB Vector and LlamaIndex and DSPy.
  - UI交互类似chatgpt
  - https://x.com/9hills/status/1862522244527972625
    - RAG Demo 到 RAG Application 难度的完美表现，其实功能不算丰富（增加了 Graph RAG和 Agent RAG 的思想），
    - 代码却不得不做的非常复杂，大部分其实是应用逻辑。 P. S. 代码已经成熟到可以直接抄了，直接复刻就完了

- https://github.com/dontizi/rlama /202503/go
  - RLAMA is a powerful AI-driven question-answering tool for your documents, seamlessly integrating with your local Ollama models. 
  - It enables you to create, manage, and interact with Retrieval-Augmented Generation (RAG) systems tailored to your documentation needs.
# rag-search
- https://github.com/Cinnamon/kotaemon /apache2/202409/python
  - https://cinnamon.github.io/kotaemon/
  - https://huggingface.co/spaces/cin-model/kotaemon-demo
  - open-source clean & customizable RAG UI for chatting with your documents. Built with both end users and developers in mind.
  - This project serves as a functional RAG UI for both end users who want to do QA on their documents and developers who want to build their own RAG pipeline.

- https://github.com/memfreeme/memfree /MIT/202409/ts
  - https://www.memfree.me/
  - MemFree is a Hybrid AI Search Engine.
  - Search and ask questions with text, images, files, and web pages.
  - Multi AI Models: ChatGPT, Claude, Gemini
  - 支持多模态（图片、文字、文件），多来源（Twitter、学术、本地知识库），多种表现形式（思维导图、图片音视频）等混合搜索形态

- https://github.com/KruxAI/ragbuilder /apache2/202410/python
  - https://docs.ragbuilder.io/
  - A toolkit to create optimal Production-readyRetrieval Augmented Generation(RAG) setup for your data
  - By performing hyperparameter tuning on various RAG parameters (Eg: chunking strategy: semantic, character etc., chunk size: 1000, 2000 etc.), RagBuilder evaluates these configurations against a test dataset to identify the best-performing setup for your data.

- https://github.com/infiniflow/ragflow /apache2/202502/python/ts
  - https://ragflow.io/
  - open-source RAG (Retrieval-Augmented Generation) engine based on deep document understanding
# ai-examples
- https://github.com/Zeyi-Lin/HivisionIDPhotos /apache2/202409/python
  - https://swanhub.co/ZeYiLin/HivisionIDPhotos/demo
  - 一个轻量级的AI证件照制作算法
  - 旨在开发一种实用、系统性的证件照智能制作算法, 利用一套完善的AI模型工作流程，实现对多种用户拍照场景的识别、抠图与证件照生成
  - SwanLab：训练人像抠图模型全程用它来分析和监控，以及和实验室同学协作交流，大幅提升了训练效率。
  - 支持 纯离线 或 端云 推理
# assistant-ai
- https://github.com/mem0ai/mem0 /apache2/202409/python
  - https://mem0.ai/
  - Mem0 (pronounced as "mem-zero") enhances AI assistants and agents with an intelligent memory layer, enabling personalized AI interactions. 
  - Mem0 remembers user preferences, adapts to individual needs, and continuously improves over time, making it ideal for customer support chatbots, AI assistants, and autonomous systems.
  - Multi-Level Memory: User, Session, and AI Agent memory retention
  - Mem0 leverages a hybrid database approach to manage and retrieve long-term memories for AI agents and assistants. 
    - Each memory is associated with a unique identifier, such as a user ID or agent ID, allowing Mem0 to organize and access memories specific to an individual or context.
    - 🛢️ When a message is added to the Mem0 using add() method, the system extracts relevant facts and preferences and stores it across data stores: a vector database, a key-value database, and a graph database. 
    - This hybrid approach ensures that different types of information are stored in the most efficient manner, making subsequent searches quick and effective.
    - Mem0 performs search across these data stores, retrieving relevant information from each source

- https://github.com/getzep/zep /apache2/202409/go
  - https://docs.getzep.com/
  - a long-term memory service for AI Assistant apps. 
  - With Zep, you can provide AI assistants with the ability to recall past conversations, no matter how distant, while also reducing hallucinations, latency, and cost.
  - Zep persists and recalls chat histories, and automatically generates summaries and other artifacts from these chat histories. 
  - Zep also provides a simple, easy to use abstraction for document vector search called Document Collections. This is designed to complement Zep's core memory features, but is not designed to be a general purpose vector database.
# ui-ai 💄
- https://github.com/open-webui/open-webui /MIT/202405/svelte/python
  - https://openwebui.com/
  - User-friendly WebUI for LLMs (Formerly Ollama WebUI)
  - extensible, feature-rich, and user-friendly self-hosted WebUI designed to operate entirely offline. 
  - It supports various LLM runners, including Ollama and OpenAI-compatible APIs

- https://github.com/richardgill/llm-ui /MIT/202502/ts
  - https://llm-ui.com/
  - The React library for LLMs
  - Removes broken markdown syntax
  - Throttling smooths out pauses in the LLM’s streamed output
  - Renders output at native frame rate
  - Code blocks for every language with Shiki
  - Headless: Bring your own styles

- https://github.com/fmaclen/hollama /MIT/202407/ts/svelte
  - https://hollama.fernando.is/
  - A minimal web-UI for talking to Ollama servers
  - Markdown parsing w/syntax highlighting

- https://github.com/kangfenmao/cherry-studio /NonCommercial/202409/ts
  - https://cherry-ai.com/
  - a desktop client that supports for multiple LLM providers, available on Windows, Mac and Linux
# protocols/MCP

## use-computer

## use-browser

- https://github.com/browserbase/stagehand /MIT/202502/ts
  - https://stagehand.dev/
  - An AI web browsing framework focused on simplicity and extensibility.
  - Stagehand is the easiest way to build browser automations. It is fully compatible with Playwright, offering three simple AI APIs on top of the base Playwright `Page` class
  - It works best when your code is a sequence of atomic actions.
  - Stagehand allows you to write durable, self-healing, and repeatable web automation workflows that actually work.
  - https://github.com/browserbase/mcp-server-browserbase
  - https://github.com/browserbase/sdk-node
# ai-devops/tooling
- https://github.com/Tencent/AI-Infra-Guard /MIT/202503/go
  - 腾讯开源了一个AI基础设施安全评估工具：AI-Infra-Guard，一键检测AI系统的潜在安全风险
  - 支持包括langchain、ollama、gradio、open-webui以及ComfyUI等在内的30种AI组件
  - 可以帮助识别，比如像Ollama在其docker中默认以root权限运行且开放到公网上，由于缺乏鉴权，可能会导致模型被删除/窃取/投毒或算力被窃取的风险
  - 这个工具的特点是轻量级，二进制文件8MB，内存占用低，支持跨平台运行，开箱即用
# more
