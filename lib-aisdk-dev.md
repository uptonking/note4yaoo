---
title: lib-aisdk-dev
tags: [aisdk, large-language-model]
created: 2025-08-08T07:35:28.042Z
modified: 2025-08-08T07:35:49.535Z
---

# lib-aisdk-dev

# guide

- pros
  - 方便前端接入ai，ui体验好
  - 提供了常用的ai开发pattern

- cons
  - 后端功能很弱, 如 RAG/持久化/工作流

- features
  - Unified Provider API
  - UI Framework-agnostic
  - Streaming AI Responses
  - Generative UI: allow a LLM to go beyond text and "generate UI"
    - Generative UI is the process of connecting the results of a tool call to a React component.

- who is using #vercelAiSdk
  - voltagent
  - opencode

- ai-framework-comparison
  - observability/debugging: supports langfuse?
  - vendor-agnostic
  - integrations
  - memory: locked?
  - workflow conceptions/architecture
  - lowcode ux
  - use-cases/courses/tutorials

- tips
  - 🤔 ai-sdk或许是错误的架构, ai输出放在后端实现是更可靠的方案，后端python工具链更完善
  - 不要在ai fwk选型上浪费太多时间，直接分析具体业务场景的需求和现有案例，然后尝试理解方案并改进
  - 🆚 ai sdk vs framework --> lightweight fwk 轻量/可扩展定制/模块化
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
  - [Model Deprecation - GroqDocs](https://console.groq.com/docs/deprecations)
    - deprecation of gemma2-9b-it in favor of llama-3.1-8b-instant

- openrouter
  - aisdk对free-model由社区提供支持
  - [API Rate Limits | OpenRouter | Documentation](https://openrouter.ai/docs/api-reference/limits)
    - If you’re using a free model variant (with an ID ending in `:free`), you can make up to 20 requests per minute.
    - If you have purchased less than 10 credits, you’re limited to 50 `:free` model requests per day.
    - If you purchase at least 10 credits, your daily limit is increased to 1000 `:free` model requests per day.
  - [What are the fees for using OpenRouter? | Documentation](https://openrouter.ai/docs/faq#what-are-the-fees-for-using-openrouter)
    - OpenRouter charges a 5.5% ($0.80 minimum) fee when you purchase credits.
    - Is there a fee for using my own provider keys (BYOK)?
    - Yes, if you choose to use your own provider API keys, there is a fee of 5% of what the same model and provider would normally cost on OpenRouter.
    - This fee is deducted from your OpenRouter credits. This allows you to manage your rate limits and costs directly with the provider while still leveraging OpenRouter’s unified interface.

- cloudflare workers ai 提供了免费额度
  - [Pricing · Cloudflare Workers AI docs](https://developers.cloudflare.com/workers-ai/platform/pricing/)
# draft

# dev-xp

# changelog

- 
- 
- 

- ## [AI SDK 6 Beta _202510](https://v6.ai-sdk.dev/docs/announcing-ai-sdk-6-beta)
- AI SDK 6 is a major version due to the introduction of the v3 Language Model Specification that powers new capabilities like agents and tool approval.
  - However, unlike AI SDK 5, this release is not expected to have major breaking changes for most users.
  - AI SDK 6 is expected to have minimal breaking changes. The version bump is due to the v3 Language Model Specification, but most AI SDK 5 code will work with little or no modification.
  - ⚖️ https://github.com/vercel/ai/tree/main/packages/provider/src/language-model

- 🧩 Agent Abstraction: A new unified interface for building agents with full control over execution flow, tool loops, and state management.

- Tool Execution Approval: Request user confirmation before executing tools, enabling native human-in-the-loop patterns.
- Structured Output (Stable): Generate structured data alongside tool calling with generateText and streamText - now stable and production-ready.
- Reranking Support: Improve search relevance by reordering documents based on their relationship to a query using specialized reranking models
- Native support for image editing (coming soon).

- ## [AI SDK 5 release blog _20250731](https://vercel.com/blog/ai-sdk-5)
- [Migrate AI SDK 4.0 to 5.0](https://ai-sdk.dev/docs/migration-guides/migration-guide-5-0)
  - `maxTokens` parameter has been renamed to `maxOutputTokens` for clarity.
  - Core Type Renames: CoreMessage → ModelMessage, Message → UIMessage
  - For UIMessages (previously called Message), the `.content` property has been replaced with a parts array structure.
  - AI SDK 5.0 introduces dynamic tools for handling tools with unknown types at development time, such as MCP tools without schemas or user-defined functions at runtime.

- v5/rename `toDataStreamResponse` to `toUIMessageStreamResponse`

- ## [Migrate AI SDK 3.4 to 4.0](https://ai-sdk.dev/docs/migration-guides/migration-guide-4-0)
  - `baseUrl` option has been removed from all providers. Please use the `baseURL` option instead.
  - `streamText` returns immediately: Instead of returning a Promise, the streamText function now returns immediately. 
# more
