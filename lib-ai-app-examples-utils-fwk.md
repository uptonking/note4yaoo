---
title: lib-ai-app-examples-utils-fwk
tags: [ai, examples, utils]
created: 2025-02-21T18:20:28.621Z
modified: 2025-02-21T18:20:42.624Z
---

# lib-ai-app-examples-utils-fwk

# guide

# popular
- https://github.com/langgenius/dify /82.5kStar/apache2/202503/python
  - https://dify.ai/
  - Dify is an open-source LLM app development platform
  - combines AI workflow, RAG pipeline, agent capabilities, model management, observability features and more
  - 依赖flask-sqlalchemy、beautifulsoup4、celery、gunicorn、langfuse、numpy、pandas、pydantic、starlette、unstructured
  - license 💰
    - Unless explicitly authorized by Dify in writing, you may not use the Dify source code to operate a multi-tenant environment.
    - In the process of using Dify's frontend, you may not remove or modify the LOGO or copyright information in the Dify console or applications. 

- https://github.com/cloudflare/agents /MIT/202502/ts
  - https://developers.cloudflare.com/agents/
  - Build and deploy AI Agents on Cloudflare
  - https://x.com/threepointone/status/1895097050439593993
    - an event bus for ai agents
# agent-framework
- https://github.com/mastra-ai/mastra /Elastic/202502/ts
  - https://mastra.ai/
  - Mastra is an opinionated Typescript framework that helps you build AI applications
  - It gives you the set of primitives you need: workflows, agents, RAG, integrations and evals.
  - You can run Mastra on your local machine, or deploy to a serverless cloud.
  - Mastra uses the Vercel AI SDK for model routing, providing a unified interface to interact with any LLM provider including OpenAI, Anthropic, and Google Gemini. 
  - Agents are systems where the language model chooses a sequence of actions. 
  - Tools are typed functions that can be executed by agents or workflows, with built-in integration access and parameter validation. 
  - Workflows are durable graph-based state machines. They have loops, branching, wait for human input, embed other workflows
  - RAG lets you construct a knowledge base for agents
  - Evals are automated tests that evaluate LLM outputs using model-graded, rule-based, and statistical methods.
  - https://x.com/dingyi/status/1893329741060489438
    - 以前非常喜欢且深度使用的 Gatsby，他们团队原班人马做的新产品，The TypeScript Agent Framework
# ai-sdk
- [AI SDK Cookbook](https://sdk.vercel.ai/cookbook)
  - An open-source collection of recipes and guides for building with the AI SDK.
# browser-use

# computer-use
- https://github.com/Aident-AI/open-cuak /apache2/202503/ts
  - https://aident.ai/
  - Open CUA Kit (Computer Use Agent), is THE platform for teaching, hiring and managing automation agents at scale — starting with browsers.
  - Open-CUAK is designed to run and manage thousands of automation agents, ensuring each one is reliable.
  - Run Operator-like automation workflows locally, ensuring full privacy
# crawler-ai
- https://github.com/mendableai/firecrawl /AGPLv3/202502/python/rust/ts
  - https://firecrawl.dev/
  - Turn entire websites into LLM-ready markdown or structured data. 
  - Scrape, crawl and extract with a single API.
  - The hard stuff: proxies, anti-bot mechanisms, dynamic content (js-rendered), output parsing, orchestration
  - Batching (New): scrape thousands of URLs at the same time with a new async endpoint.
  - open-version: scrape, extract, map, formats, sdk
  - cloud-version: anti-bot, dashboard, actions, browserless, enterprise
  - This project is primarily licensed under AGPLv3
    - However, certain components of this project are licensed under the MIT 
    - The SDKs and some UI components are licensed under the MIT License. 

- https://github.com/getmaxun/maxun /AGPL/202503/ts
  - https://www.maxun.dev/
  - Open-source no-code web data extraction platform. 
  - Maxun lets you create custom robots which emulate user actions and extract data. A robot can perform any of the actions: Capture List, Capture Text or Capture Screenshot. Once a robot is created, it will keep extracting data for you without manual intervention
# perf/large
- https://github.com/MoonshotAI/MoBA /MIT/202502/python
  - Mixture of Block Attention for Long-Context LLMs
  - https://x.com/tuturetom/status/1892753818028216717
    - 可以实现近乎无限的上下文窗口，将一整本书或一整个代码库扔进去提问
# proxy
- https://github.com/lymanzhao/Ollama-serve /202503/python
  - 一个 Ollama转发代理，用于为原生 Ollama 服务添加 API 密钥认证功能。
  - 该项目解决了 Ollama 官方不提供 API 密钥验证的问题，使您可以更安全地部署 Ollama 服务并防止未授权访问
# more
