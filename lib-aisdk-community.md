---
title: lib-aisdk-community
tags: [aisdk, community]
created: 2025-08-08T07:36:19.120Z
modified: 2025-08-08T07:36:31.265Z
---

# lib-aisdk-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚🤔 [Framework vs. SDK for AI Agents – What's the Right Move? : r/AI_Agents _202502](https://www.reddit.com/r/AI_Agents/comments/1iqg6w1/framework_vs_sdk_for_ai_agents_whats_the_right/)
  - Should we use full frameworks (LangChain, AutoGen, CrewAI) or go raw with SDKs (Vercel AI, OpenAI Assistants, plain API calls)?
  - Frameworks give structure but can feel bloated. SDKs are leaner but require more custom work. What’s the sweet spot?

- Frameworks can sometimes feel bloated, but raw SDKs often feel too bare-bones. When working directly with SDKs, anything beyond simple use cases can feel like reinventing the wheel or building a micro-framework from scratch.
  - I don’t mind a bit of extra overhead if it leads to better long-term maintainability
  - I’ve also seen a lot of discussions about no-code and low-code platforms, but for serious use cases, they come with a major drawback... vendor lock-in. 
  - Another advantage of frameworks is their flexibility at the LLM level. Many make it easy to switch between different LLM providers

- Ultimately, choosing between PaaS or SaaS comes down to balancing risk and reward.

- There are also some lightweight frameworks like PydanticAI worth checking out, especially since Pydantic itself is so powerful.

- lightweight framework is the best of both worlds. like mastra for js

- I’ve been down this exact rabbit hole, frameworks often feel bloated, SDKs feel like you’re rebuilding everything from scratch. So we ended up building something in-between.
  - https://github.com/voltagent/voltagent

- check out smol agents for a middleground option.

- If you want the benefits of a framework with the leanness of an SDK (and being able to have defined REST APIs), you should check out Letta (runs an agents service that manages state/context on top of LLM providers). We support both Node and Python SDKs.
# discuss-ai-sdk/platform
- ## 

- ## [OpenAI Agent SDK vs LangGraph : r/LangChain _202503](https://www.reddit.com/r/LangChain/comments/1j95uat/openai_agent_sdk_vs_langgraph/)
- Now with OpenAI stepping into the "LLM framework" territory, I think they will on purpose lock the developers into it, by always providing the best support to OpenAI-exclusive features which Langchain doesn't support well (I'm talking about stuff like real-time generation, audio input, computer use, hell even the basic structured output).

- 
- 

- ## [Confused between AI SDK and LangChain : r/LangChain _202409](https://www.reddit.com/r/LangChain/comments/1fie8ul/confused_between_ai_sdk_and_langchain/)
- AI SDK is very focused on just the chat model abstraction. It also has more focus on building UIs with support for things like the `useChat` React hook.
  - LangChain is broader and has more abstractions around vector stores, indexing, different methods of retrieval, text splitting, etc.
- in vercel ai docs, there's no abstraction for build a RAG, you'll have to do it manually (chunking, text splitter, vector store, etc.). that's where langchain.js comes in.
  - build frontend using vercel ai sdk UI, and build your backend with langchain.js. ai sdk provides adapter to connect the UI with langchain

- Almost all of the other LLM providers have treated openapi's `/v1/chat/completions` as a de facto standard, so you just code against that and call it a day. Try it out with ollama.

- you can use them both: https://ai-sdk.dev/providers/adapters/langchain
# discuss-ai-providers
- ## 

- ## 

- ## 
# discuss-ollama
- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 
# discuss-changlog
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 
