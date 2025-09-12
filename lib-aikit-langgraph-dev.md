---
title: lib-aikit-langgraph-dev
tags: [langgraph, workflow]
created: 2025-08-11T08:45:52.661Z
modified: 2025-08-11T08:46:16.962Z
---

# lib-aikit-langgraph-dev

# guide

- pros-langgraph
  - license: MIT
  - low-level primitives provide the flexibility needed to create fully customizable agents: single, multi-agent, hierarchical
  - 官方提供了多种语言实现: python/js
  - 文档丰富、示例多
  - Human-in-the-loop: Seamlessly incorporate human oversight by inspecting and modifying agent state at any point during execution
  - memories: stateful agents with both short-term working memory for ongoing reasoning and long-term persistent memory across sessions.

- cons-langgraph 🐛
  - no http api
  - no cron scheduling

- features-langgraph
  - ✨ parallelization, streaming, checkpoint, task queue, human-in-the-loop, tracing
  - LangGraph provides low-level supporting infrastructure for any long-running, stateful workflow or agent. LangGraph does not abstract prompts or architecture
  - First-class streaming for better UX design
  - Durable execution: Build agents that persist through failures and can run for extended periods
  - Debugging with LangSmith: Gain deep visibility into complex agent behavior with visualization tools that trace execution paths

- who is using #langgraph 🌰
  - Replit, Elastic

- pros-langchain
  - license: MIT
  - 官方提供了多种语言实现: python/js

- cons-langchain 🐛
  - LCEL ？

- features-langchain
  - Ship powerful agents: handle sophisticated tasks with control
  - Accelerate agent development: Build faster with templates & a visual agent IDE
  - Gain visibility & improve quality

- who is using #langchain 🌰
  - n8n
  - flowise
  - langflow
  - librechat
# not-yet

# draft
- langgraph进度监控: 当前执行到了哪个Node，已执行哪些Node，还剩几个Node

- langgraph本身只是库，是sdk的一部份，服务端需要自己实现
# dev-xp
- 🤔 rag的对话结果质量不好
  - 有时是 qwen3-embedding-0.6b 的embedding出问题了，embedding时LM Studio的控制台日志一直有异常, 异常时搜索结果一直都只返回一个片段，导致结果不好

- Node是每次都会参与计算的部分，而tool可由ai决定是否调用

- v1的 api 十分混乱，暂时不要花费过多时间
  - langgraph-python 逐渐使用 create_react-agent
  - langgraphjs/langchain 逐渐使用 createAgent

- 使用 `while True: graph.stream` 相关的逻辑测试时，注意死循环
# more
