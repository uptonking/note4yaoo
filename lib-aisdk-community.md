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

- ## 

- ## 

- ## 

- ## Which framework should I use for developing AI agents? LangGraph or @pydantic Agent framework? _202505
- https://x.com/NielsRogge/status/1928064768109076759
  - avoid fwk, use llm apis to have better control.
  - build workflows instead.
- If you want to make direct requests to the LLM, but you want to still be able to switch provider easily, you can use @pydantic AI's direct API

- Agreed. Many of these frameworks add bloat and unnecessary LLM calls. And in most cases you need an automation, not an agent. I’ve written a guide on it too

- 100% - everything is moving too fast to get locked into a framework.

- I used to think this but @aisdk changed my mind. I wish it was for python too
  - For starters, being able to easily switch between models without any speed loss (*openrouter) is one.
  - Their tool call implementation is really minimal and quick to setup too.

- Use LangGraph but code your own components in it. This way you have visualization, adapt- and extendability and testing while maintaining full control over implementation details.

- Langchain is pain in the ass with every version they change syntax and naming conventions

- agree. These days I just ask the LLM to help me build the tiny part I need from any SDK, then turn it into my own minimal wrapper. No bloat, full control. Most libraries we add, we just use a small part of them.

- ## [OpenAI Agent SDK vs LangGraph : r/LangChain _202503](https://www.reddit.com/r/LangChain/comments/1j95uat/openai_agent_sdk_vs_langgraph/)
- Now with OpenAI stepping into the "LLM framework" territory, I think they will on purpose lock the developers into it, by always providing the best support to OpenAI-exclusive features which Langchain doesn't support well (I'm talking about stuff like real-time generation, audio input, computer use, hell even the basic structured output).

- ## [Confused between AI SDK and LangChain : r/LangChain _202409](https://www.reddit.com/r/LangChain/comments/1fie8ul/confused_between_ai_sdk_and_langchain/)
- AI SDK is very focused on just the chat model abstraction. It also has more focus on building UIs with support for things like the `useChat` React hook.
  - LangChain is broader and has more abstractions around vector stores, indexing, different methods of retrieval, text splitting, etc.
- in vercel ai docs, there's no abstraction for build a RAG, you'll have to do it manually (chunking, text splitter, vector store, etc.). that's where langchain.js comes in.
  - build frontend using vercel ai sdk UI, and build your backend with langchain.js. ai sdk provides adapter to connect the UI with langchain

- Almost all of the other LLM providers have treated openapi's `/v1/chat/completions` as a de facto standard, so you just code against that and call it a day. Try it out with ollama.

- you can use them both: https://ai-sdk.dev/providers/adapters/langchain
# discuss-ai-chrome/browser
- ## 

- ## 

- ## Chrome has an AI summarizer API built in now _20250809
- https://x.com/BHolmesDev/status/1954179936249376962
  - No API keys, no internet. Runs locally
  - Downloads the model on-demand
  - Available as a global in the latest version of Chrome. Works in chrome extensions too
  - [AI with Chrome  |  Chrome for Developers](https://developer.chrome.com/docs/ai)
  - I have so many chrome extension ideas now...

- Its a standard I think there trying to introduce. Vercel ai sdk has support
# discuss-ai-backend/framework
- ## 

- ## 

- ## [Which ai agent framework should I use? : r/LangChain _202412](https://www.reddit.com/r/LangChain/comments/1hhq28r/which_ai_agent_framework_should_i_use/)
- Suggest you start with a problem you'd like to solve and work towards solutions rather than start with a solution and YOLO it.
  - Agents aren't one thing, and we don't agree on what they are.

- ## [Are agent frameworks THAT useful? : r/AI_Agents _202501](https://www.reddit.com/r/AI_Agents/comments/1ianz11/are_agent_frameworks_that_useful/)
- All frameworks that I have seen as of late are almost identical. There are some minor cosmetic differences but at the core they are the same thing.
  - The hard parts are hard and no framework, at least to my knowledge, has solved any of these yet.
  - The right approach is to start from the customer and their problems and then figure out the tools that are present today to solve them, then learn, iterate quickly and repeat the process. After several rounds of this you will most likely build a unique perspective that will drive better decisions and better outcomes. At that point you will know very well what framework is a strategic move and what will be a distraction.

- ## [What is the best AI agent framework in Python : r/AI_Agents _202412](https://www.reddit.com/r/AI_Agents/comments/1hqdo2z/what_is_the_best_ai_agent_framework_in_python/)
- Which one allows you to choose your model freely and don't rely on OpenAI as the default.
  - Which one allows you to monitor the output for governance and QA.
  - Which one allows you to easily integrate session memory and user profile memory
  - Which one allowed you to easily define and use a variety of new tools and reliably call them?
- It comes down to your budget, preferences, use case, and capability to develop agent product in Python.

- I think langgraph is the most complete framework with UI library, development kit.
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

- ## AI SDK 5 is now in Beta! We redesigned the AI SDK to create a next-generation AI framework _202506
- https://x.com/aisdk/status/1937524577854456270
  - Build agents with prepareStep, stopWhen, and provider-executed tools
  - Rely on an updated, robust language model spec

- https://x.com/lgrammel/status/1922274918378459291
  - AI SDK 5 preview: ChatStore & ChatTransport
  - ChatStore synchronizes chat write operations and manages streaming state.
  - ChatTransport makes backend integrations more flexible, allowing for client-only usage.
# discuss
- ## 

- ## 

- ## 
