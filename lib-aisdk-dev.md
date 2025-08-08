---
title: lib-aisdk-dev
tags: [aisdk, large-language-model]
created: 2025-08-08T07:35:28.042Z
modified: 2025-08-08T07:35:49.535Z
---

# lib-aisdk-dev

# guide

- features
  - Unified Provider API
  - UI Framework-agnostic
  - Streaming AI Responses
  - Generative UI: allow a LLM to go beyond text and "generate UI"
    - Generative UI is the process of connecting the results of a tool call to a React component.
# ai-providers
- free-api
  - google-gemini

- groq
  - llama/gemma/deepseek/qwen/gptoss: 30rpm, 1Krpd, 6ktpm, 500Ktpd
  - compound-beta/compound-beta-mini: 15rpm, 200rpd, 7000tpm, UNtpd
  - tpm较大的是 gemma2-9b-it, meta-llama/llama-4-scout-17b-16e-instruct, openai/gpt-oss-120b
  - aisdk对groq-llama提供官方支持，支持image input
  - groq-names: deepseek-r1-distill-llama-70b, qwen/qwen3-32b, moonshotai/kimi-k2-instruct
  - aisdk/groq-names: llama-3.3-70b-versatile, meta-llama/llama-4-scout-17b-16e-instruct

- openrouter
  - aisdk对free-model由社区提供支持
# draft

# dev-xp

# changelog

- 
- 

- [Migrate AI SDK 4.0 to 5.0](https://ai-sdk.dev/docs/migration-guides/migration-guide-5-0)
  - `maxTokens` parameter has been renamed to `maxOutputTokens` for clarity.
  - Core Type Renames: CoreMessage → ModelMessage, Message → UIMessage
  - For UIMessages (previously called Message), the `.content` property has been replaced with a parts array structure.
  - AI SDK 5.0 introduces dynamic tools for handling tools with unknown types at development time, such as MCP tools without schemas or user-defined functions at runtime.

- [Migrate AI SDK 3.4 to 4.0](https://ai-sdk.dev/docs/migration-guides/migration-guide-4-0)
  - `baseUrl` option has been removed from all providers. Please use the `baseURL` option instead.
  - `streamText` returns immediately: Instead of returning a Promise, the streamText function now returns immediately. 
# more
