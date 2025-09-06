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
# draft

# dev-xp

# more
