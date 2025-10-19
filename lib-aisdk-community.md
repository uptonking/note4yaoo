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

- ## 🤔 [Any concrete drawbacks from using Vercel's AI SDK? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nxmfz7/any_concrete_drawbacks_from_using_vercels_ai_sdk/)
  - I was researching what I would deem to be "good" open source code in this area to try and find some interesting abstractions and noticed that nearly all the projects are using Vercel's AI SDK for connecting to LLMs. 

- Keep your own thin provider interface and treat Vercel’s AI SDK as an optional UI/streaming helper, not the core. 
- Concrete gotchas I’ve hit: 
  - the SDK leans hard on an OpenAI-shaped schema, so Anthropic/Gemini/Ollama quirks (tool_choice, parallel tool calls, reasoning tokens, JSON strict modes, logprobs) need shims and you can lose feature parity. 
  - Streaming can blur tool boundaries and partial deltas, which makes extracting structured state annoying. 
  - Their retry/rate-limit controls are basic, and observability hooks are light; 
  - you’ll likely bolt on your own token accounting, tracing, and redaction. 
  - Version churn is real; small upgrades have broken message types and server components for me. 
  - It’s also very Next.js/Edge flavored-testing outside that stack and running local-first (Ollama) is smoother with your own adapter. 
- What worked well: a ports/adapters layer that normalizes messages/tools, your own SSE parser, and per-provider cost/telemetry, then use the SDK’s `useChat` only for front-end UX. 
  - I’ve paired Cloudflare Workers and Temporal for orchestration, with DreamFactory to expose stable REST tools over legacy DBs. 
  - In short, keep your adapter layer and use the SDK at the edges only.

- Every abstraction seems to have its pros and cons.
  - Vercel AI SDK: easy to use, Next compatible, simple agent concept, adapters for LangChain.js so you can use AI SDK front end primitives (but you could choose AG UI instead too).  Easiest path to supporting both server and client side tools
  - LangChain.js: widest support, lots of agent tools, worst API
  - LlamaIndex. TS: weakest support, nice API and RAG primitives
- In the end you can kind of adapt some parts of these to another.  For example, I have a custom LlamaIndex. TS adapter for Vercel AI SDK language and embedding models.  You can adapt LangChain.js tools to Vercel AI SDK fairly easily.

- ## [Is it worth using LangGraph with NextJS and the AI SDK? : r/LangChain _202506](https://www.reddit.com/r/LangChain/comments/1lnsoud/is_it_worth_using_langgraph_with_nextjs_and_the/)
- Integrating LangGraph with Next.js and Vercel's AI SDK can be tricky due to limited docs, especially for streaming. 

- I found the js langchain to be always behind python, so you often are missing tutorials or things aren't supported. I ended up liking mastra

- ## [OpenAI Agent SDK vs LangGraph : r/LangChain _202503](https://www.reddit.com/r/LangChain/comments/1j95uat/openai_agent_sdk_vs_langgraph/)
- Now with OpenAI stepping into the "LLM framework" territory, I think they will on purpose lock the developers into it, by always providing the best support to OpenAI-exclusive features which Langchain doesn't support well (I'm talking about stuff like real-time generation, audio input, computer use, hell even the basic structured output).

- You're better off writing the flow and architecture of your system in the core programming language you are designing your app in (with classes, threading and all the shit that langgraph hasn't implemented yet), and just directly control the flow in first-class code. It will scale, it gives you more control
  - This is probably true when you have <= 3 ppl working on that system. Once you have a slightly larger team and a bit more complex business logics, you will soon run into problems like: You have to know all the concurrency management really well in the codebase in order to write the most efficient code
  - Graph architecture is exactly used to solve these problems. It modularizes your business logic to only a node and you can add that without knowing the rest of the graph. It does the multi-threading automatically based on node dependencies so you don’t need to think about concurrency at all and your code is already most efficient.

- the use case is key. If all you are doing is creating essentially a static program inside a graph with a couple of decision points which can easily be represented by an if statement (perhaps with a complex condition), I don't see the need. If a graph is allowing for orchestrated flows through the graph... I mean, a directed acyclic graph is essentially what ComfyUI is.
  - The reason people use ComfyUI is because coding in python directly with all of the changing standards of how it works, is a headache. ComfyUI is a DAG for image generation. It's advantages over a non-dag predecessor like Automatic1111 are obvious, because users can generate their own flows without coding.
- you dont see the need because you never had to deal with a ETL or moving big amounts of data around while doing transformations and crap. Having a tool for easy visibility of the flows, maintainability of the workflows, easy retry of only failed nodes/dags is invaluable, even if your workflow is simple.

- ## [Confused between AI SDK and LangChain : r/LangChain _202409](https://www.reddit.com/r/LangChain/comments/1fie8ul/confused_between_ai_sdk_and_langchain/)
- AI SDK is very focused on just the chat model abstraction. It also has more focus on building UIs with support for things like the `useChat` React hook.
  - LangChain is broader and has more abstractions around vector stores, indexing, different methods of retrieval, text splitting, etc.
- in vercel ai docs, there's no abstraction for build a RAG, you'll have to do it manually (chunking, text splitter, vector store, etc.). that's where langchain.js comes in.
  - build frontend using vercel ai sdk UI, and build your backend with langchain.js. ai sdk provides adapter to connect the UI with langchain

- Almost all of the other LLM providers have treated openapi's `/v1/chat/completions` as a de facto standard, so you just code against that and call it a day. Try it out with ollama.

- you can use them both: https://ai-sdk.dev/providers/adapters/langchain
# discuss-ai-chrome/browser
- ## 

- ## [免费 + 本地 + Chrome 内置] Prompt API : 基于 Gemini Nano 模型的 Chrome 内置 AI 功能，让开发者通过自然语言、图像和音频输入创建智能化的网页应用。
- https://x.com/shao__meng/status/1955152721205662037
  - Prompt API 是 Chrome 浏览器提供的一项实验性功能（目前在 Chrome 138 及以上版本的 Origin Trial 中），让开发者可以通过 API 调用 Gemini Nano 模型，直接在浏览器中处理自然语言、图像和音频输入，生成文本输出
  - 操作系统：Windows 10/11、macOS 13+ 或 Linux（暂不支持 Android、iOS 或 ChromeOS）。
  - 存储空间：至少 22GB 空闲存储（模型大小可能随更新变化，可在 chrome://on-device-internals 查看，如果存储空间不足 10GB，模型会自动删除，需重新下载）。
  - GPU：显存大于 4GB。

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

- ## 

- ## 

- ## 🆚 [LangChain: JavaScript or Python? : r/LangChain](https://www.reddit.com/r/LangChain/comments/1mtq9e4/langchain_javascript_or_python/)
- I am biased; I find Python is the simplest and most intuitive for me. There are more examples out there. The data libraries available work well.

- When i tried the js version last time (few months ago), few features i was looking for not there. It was only available in the python one, so i had to switch. Not sure if it is the case right now.
  - The redischeckpointer for one. I did the same thing.

- We did it fully in JS/TS, contrary to any advice from partners, "experts", friends. And we are very happy. Simply because it integrates better in our ecosystem of apps, tools, frameworks. The rule of thumb: The best programming language is the one you know best.

- In python you can write jupyter notebooks. Very useful for ML stuff and when you are new to something. In js you would need to rerun/recompile all your code. This can take long depending on your preprocessing, volume of data, etc. Also python has a very large ML ecosystem.

- I have struggled with the same questions. From what ive seen LangChain and Lang* have more support for python. For example, chunking for RAG? LangChain has more text splitters in python (Semantic for example). Also LangMem isnt in TS. Which is odd since its never been more easier to port over code from python to TS with the advent of LLMs. Go figure.

- ## [Which AI agent framework do you find most practical for real projects ? : r/AI_Agents _202509](https://www.reddit.com/r/AI_Agents/comments/1nfz717/which_ai_agent_framework_do_you_find_most/)
  - I have been testing out different AI agent frameworks recently like LangGraph, CrewAI, and AutoGen.
  - Each of them seems strong in certain areas but weak in others. For example, one feels easier to set up while another handles memory better.

- I have bounced between crew ai and langgraph but honestly what mattered most for me was how painful debugging got in production. I ended up using mastra for TS projects because it gave me structure without all the overhead

- Google ADK is great so far Just worried if they totally shove us towards only using gcp stuff. Example the only other memory service is Vertex AI Memory Bank. No local or third party db support for this like how Autogen does. Open it up Google pls!

- I prefer Agno for its simplicity, clean documentation, speed over langraph in execution, and lastly stable APIs.

- I used OpenAI Agents SDK. It's super simple and flexible. I prefer it over more opinionated frameworks such as Crewai and LangGraph. Those tend to to be difficult to work with if what you're trying to do doesn't fit their template.

- The core pattern is simple but production reality hits different.
  - Built agents for months and the real killer wasn't picking frameworks - it was debugging when things went sideways. Tracing through multi-step workflows is always a pain point.
  - Most frameworks optimize for demos, not for "why did this break at 2am" moments.
  - We ran into the same wall at Adopt, so we built our own tooling layer. Instead of black box agent reasoning, you define workflows declaratively. When stuff breaks, you can see exactly which step failed.

- In many cases you are trading simple problems for complex ones using those SDKs. It may be easier to start with AI sdk, but as you go, the overhead of dealing with them may outweigh the benefits, e.g. Langgraph python SDK has a bizarre approach to working with postgresql checkpointers or to how they store messages in the DB. Also most AI SDKs force you into python or typescript, both of which come with huge maintenance pain and a baggage of inefficiency.

- What you actually want is to just use a traditional for loop with an LLM with tool calls.

- I think the “best” framework really depends on the project’s goals. For quick prototyping, something like LangGraph feels lighter to set up, while frameworks like AutoGen seem better when you need strong memory and more complex coordination. CrewAI looks promising for team-based workflows, but it can feel heavier at the start. 
  - For me, ease of integration and community support make the biggest difference. 
  - Curious to hear what trade-offs others have noticed.

- LangGraph. they have great free academy courses. this framework lets to squeeze everything from agents

- tbh if you're building for a production use case, the frameworks add an unnecessary layer of abstraction in exchange for awful debugging, observability, and so-so performance. I'd recommend just using OpenAI Agents SDK. We spent about a month debugging Mastra and then just decided to code the thing ourselves and it's been a huge unlock.

- ## [Why are people hating LangChain so much, organisations are also not preferring projects built on top of LangChain : r/LangChain _202411](https://www.reddit.com/r/LangChain/comments/1gmfyi2/why_are_people_hating_langchain_so_much/)
- The original versions of LangChain were released at an early stage of LLMs when the APIs were new. They got some of the abstractions wrong and it was unnecessarily complex.
  - LangGraph is much, much better and they are building out tools to support it. Plus the documentation has taken a step up.

- Doing (sane) dependency injection with LangGraph is still a terrible experience. Other decisions as keeping RunnableConfig a TypedDict instead of a pydantic BaseModel makes you wonder about their SwEng experience (at least in python terms).
  - we intentionally chose not to use pydantic (after using it as the backbone in many other places). heard on the dependency injection though, we'll improve that

- Pydantic adds a nonneglible impact to perf though? serializing/deserializing big objects in pydantic is pretty slow

- You should use LangChain to get out of the box LLM observability. Only people with real production problems can understand this. So what ever you choose to replace LangChain make sure you are covered on all of the software life cycle problems LC is solving.

- The LangChainGo implementation is a little cleaner, imo.

- I use langchain for 2 reasons: Rich ecosystem of tools and loaders, ingle LLM interface which allows me to use these tools with different LLMs.
  - However, I stay away from the over-engineered an unnecessary parts such as chains using |, output parsers and others...

- if you use langchain your code is slower than mine, less understandable, and less extensible than mine. that’s all.

- ## [How would you build an LLM agent application without using LangChain? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1i2n0il/how_would_you_build_an_llm_agent_application/)
- llamaindex is just as bad

- what's bad about LangChain?
- everything is overcomplicated and it's painful to do even very default stuff, for example: How I can do rag + function calling + text streaming with local model? It will be very difficult to get this right with docs.

- LangGraph is quite good imo. You can either use prebuilt components or add completely customised ones.

- The good so far: unified interface for different LLMs, retry/fallback mechanisms, langfuse/smith tracing and profiling (especially for out-of-the-box RAG setups), some RAG building blocks, structured outputs.
- The bad: the actual chains (a kitten dies every time some dumbnut tries clever things with operator overloading in Python and breaks code introspection), LCEL, documentation. I steered away from almost everything due to the latter.

- This is the same discussion about frameworks in web dev: a framework can make you massively more productive but it comes at the cost of complexity to your codebase

- ## [Python vs Javascript for langchain : r/LangChain _202407](https://www.reddit.com/r/LangChain/comments/1dtjqwi/python_vs_javascript_for_langchain/)
- The main advantage of python is that in case you need advanced customization of the ML architecture then there are already lot of support for that in python since the critical frameworks like pytorch are in python.
  - if you are much familiar with js then in order to get faster results, I would go with js.
  - Note that js community is catching with python ml advantages, see transformer.js

- I'm currently using langchain js in prod. No issues so far. I'm skilled in python but I'd like to maintain a full stack TS app so I'm sticking with it. I've been told by very senior TS Devs that I won't need python.

- LangchainJS does seem to be behind the python version in support. I have noticed quite a few of the python utilities are not available in the JS version.

- [LangChain JS vs Python : r/LangChain](https://www.reddit.com/r/LangChain/comments/14jweso/langchain_js_vs_python/)

- ## [Why use LangChain over OpenAI directly? : r/OpenAI _202308](https://www.reddit.com/r/OpenAI/comments/15vn9jz/why_use_langchain_over_openai_directly/)
- I use langchainjs and do not recommend it. Basic stuff like getting token counts back from OpenAI chat completions results in hard-to-grok code. OpenAI’s api is very clean and the abstract complicates things unnecessarily.
  - If OpenAI adds params their API, you’re stuck until you or someone else writes a PR for langchainjs.
- couldnt agree more. we built https://www.fables.gg with langchain but recently ripped it all out because it was too much abstraction that made things harder than if we just wrote things ourselves
- I realized their JS lib doesn't support o1, while their python lib already does

- Langchain helped save me a ton of time in parsing json for a text extraction prompt. 

- ## Wondering what's the current best way to build AI agent
- https://x.com/MattM_lj/status/1933087756596678963
- Based on my experience, I would start with AI SDK, for sure. It's a low-level primitive that gives you the important stuff in a simple API, and you can go nuts on top building custom loops etc.

- mastra is built on top of AI SDK but gives you more structured primitives like Workflows, Agents, Evals, etc.

- Any reason against going langchain/crewai?
  - Nothing specific, but as mainly a typescript dev, I feel like AI SDK is more of of a fit

- ## @LangChainAI just released a new Python package called deepagents _202507
- https://x.com/hwchase17/status/1950617211267354685

- It’s built around a simple idea: the best research and coding agents (Claude Code, Manus, etc.) all have a few things in common—
  - a detailed system prompt
  - a planning tool (even if it's a no-op)
  - sub-agents for task decomposition
  - Access to a file system for shared memory
  - deepagents packages those ideas into a framework you can tweak for your own use case.

- `deepagents` is different than other agent frameworks, comes more with "batteries built in"
  - its also built on top of langgraph - so if you want to modify those batteries and go to a lower level - its pretty easy!
- batteries included" is exactly what production needs
  - mario's workflows broke constantly before we added proper error recovery and state management
  - langgraph foundation + deepagents orchestration? this could save teams months of debugging agent loops

- ## 🆚🌰 I am coding the same agents in all LLM frameworks to compare them side-by-side: _202504
- https://x.com/_rchaves_/status/1914083928647885122
  - https://github.com/langwatch/create-agent-app /MIT/202508/python/ts
  - I'm still expanding on create-agent-app, so far I built the same customer service agent in 6 different agent frameworks
- conclusion
  - Agno for high-level agents
  - DSPy for optimizable workflows
  - LangGraph Functional API for low level state handling
  - Inspect AI for agent research and evaluations

- One option should definitely be no framework. Just a for loop.
  - Quite seriously, a loop, a few Pydantic models, and LiteLLM is probably the right baseline to compare other things to.
- I love this, the barebones one, but then using what for calling the llm, just openai completion? litellm perhaps to fit all models

- 📌 LangGraph: that was my first implementation, focusing on the functional api, took me ~30 min 
  - documentation is all spread up, there are many too ways of doing the same thing, but there isn’t an official recommended best way, each doc follows a different pattern
  - sync/async/stream/async stream all work seamless by just using it at the end with the invoke
  - I really like both the functional api and the more high level constructs and think it’s a very solid and mature framework.

- 📌 Pydantic AI: took me ~30 min, mostly dealing with async issues
  - no native memory support
  - recommended way to connect tools to the agent with decorator @agent .tool_plain is a bit akward
  - having to manually agent_run.next is a tad weird too
  - parts is their primary constructor on the results, similar to vercel ai, which is interesting thinking about agents where you have many tools calls before the final output

- 📌 Google ADK: took me ~1 hour, I expected this to be the best but was actually the worst
  - Agent vs LlmAgent? Session with a runner or without? A little bit of multiple ways to do the same thing even though its so early and just launched
- it looks to me that ADK is meant to be used with Google's Vertex, and as such, things start to make sense (session management etc) and is much more efficient that way.

- 📌 DSPy: took me ~10 min, 
  - it’s actually hiding and converting my prompts, but somehow also giving better results 
  - behind the scenes is not really doing tool call, which can cause smaller models to fail generating valid outputs
  - DSPy is a very interesting case because you really need to bring a different mindset to it, and it bends the rules on how we should call LLMs.
  - I could not simply print the tool calls that happen in a standard openai format like the others, they are hidden inside ReAct 👀
- Can you expand a nit on "DSPy doesn't use native tool calling by default". What is DSPys take on tool calling?
  - Native tool is when the LM can decide at runtime to emit a JSON “function call” that your code then executes. 
  - DSPy treats the LM as a text-in/text-out component. There is no function call at runtime, if you want tool use in DSPy you add it yourself.

- 📌 Smolagents: took me ~45 min
  - agents have memory by default, an agent instance is a memory instance, which is interesting, but then I had to save the whole agent in the memory to keep the history for a certain thread id separate from each other
  - not easy to convert their tasks format back to openai, I’m not actually sure they would even be compatible

- 📌 Agno: took me ~30 min, mostly trying to figure out the tools string output issue
  - Agno is the only framework I couldn’t return regular python types in my tool calls, it had to be a string
  - It has a few interesting concepts I haven’t seen around: instructions is actually an array of smaller instructions, the ReasoningTool is an interesting idea too
  - Pretty robust different ways of handling memory, having a session was a no-brainer, and all very well explained on the docs, nice recomendations around it, built-in agentic memory and so on

- 📌 No Framework: took me ~30 min, mostly litellm’s fault for lack of a great type system
  - I have done this dozens of times, but this time I wanted to avoid at least doing json schemas by hand to be more of a close match to the frameworks, I tried instructor, but turns out that's just for structured outputs not tool calling really
  - So I just asked Claude 3.7 to generate me a function parsing schema utility, it works great, it's not too many lines long really, and it's all you need for calling tools
  - As a result I have this utility + a while True loop + litellm calls, that's all it takes to build agents
  - Going the no framework route is actually a very solid choice too, I actually recommend it, specially if you are getting started as it makes much easier to understand how it all works once you go to a framework

- on pydantic, I actually faced a few issues with pydantic ai that I didn't expect, I expected them to be super solid indeed and lower level, like a better instructor for function calling
  - but actually they are a high level agent framework like all the others, and I found Agno to be way more solid in that arena

- 
- 
- 
- 
- 
- 
- 
- 

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
# discuss-roadmap
- ## 

- ## 

- ## 
# discuss-changlog
- ## 

- ## 

- ## HITL(Human in the loop) in AI SDK v5, using custom data parts
- https://x.com/mattpocockuk/status/1952322985068802369
- Does this have to be stateful ? 
  - No, my implementation is not stateful

- ## 🎯 AI SDK 5: Introducing type-safe chat, agentic loop controls, data parts, speech generation and transcription, Zod 4 support, global provider, and raw request access. _202508
- https://x.com/aisdk/status/1950952373616337280
  - The chat abstraction has been redesigned to support type-safety, customizable transports, flexible state management, and more.
  - Data parts provide a first-class way to stream custom, type-safe data from the server to the client, ensuring your code remains maintainable as your application grows.
  - For information about a message, such as a timestamp, model ID, or token count, you can attach type-safe metadata.
  - AI SDK 5 brings all new agentic controls. stopWhen/prepareStep
  - AI SDK 5 extends our unified provider abstraction to speech. Just as we've done for text and image generation, we're bringing the same consistent, type-safe interface to both speech generation and transcription.
  - AI SDK 5 works with Zod 4 and Zod Mini giving you faster validation, better TypeScript performance, and reduced bundle size.
  - [AI SDK 5 - Vercel](https://vercel.com/blog/ai-sdk-5)

- ## The @vercel Chat SDK now features stream resumption _202505
- https://x.com/cramforce/status/1921211838110593310
  - This is based on https://github.com/vercel/resumable-stream /MIT
  - A core feature is that while it uses Redis, the actual Redis usage is minimal unless you actually need to resume a stream (which should be rare in practice).
  - It would be dramatically more efficient and lower-cost, because it only does O(1) database writes in the common case.
- It supports:
  - Clients resuming streams on network interruption
  - Multiple browser tabs following the same underlying stream
  - Multiple users following the same stream

- But this "only" applies to when you have own business logic workflow and you need to "attach" back to ongoing process; it's not resuming an LLM engine streaming in "the middle" of the process, correct?

- https://x.com/rauchg/status/1921168985900372081
  - No proprietary APIs, no sticky load balancing, just Redis pubsub.
- I was also a little worried about latency of pushing into redis. I know redis is fast, but for this application the ms count. A design with a sticky session seems to make sense since the number of users in a chat is going to be very, very small.
  - It makes O(1) Redis writes per stream in the common case. If you use Upstash it would cost $4 per million streams which seems very fine
- Why doesn't every token have to be  written to the stream?
  - Because it only writes if there are any listeners. By default (no client network error, no second tab opened, etc.) there is no listeners
- Redis pub-sub scales very well, so you’d probably only need a single node to handle many nodes of your chat service.

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

- ## Things I don't like about the AI SDK #1
- https://x.com/mattpocockuk/status/1915840893917032521
  - You can specify 'maxSteps' on streamText & generateText to toggle from a single LLM call to an agentic loop.
  - what happens when you run out of steps? Well, your app stops. If you've built a coding agent, your agent will just stop half-way through.
  - maxSteps overall hands _so_ much control over to the AI SDK, I almost find it hard to recommend.

- You can use prepareStep and implement this idea now

- ## [Groq API always returns 404 - Forum - Groq Community _202507](https://community.groq.com/t/groq-api-always-returns-404/426)
  - For quite some reason, when I do requests to the API, I always get this: `{ error: { message: 'Not Found' } }`

- 👷: 实测groq api请求有时失败，有时成功

- one thing to check, if you’re behind a firewall and/or a VPN, the API calls might be blocked. Could you do a simple cUrl call from the same machine to see if you get a response? Could you try using a serverless system like Cloudflare workers to see if you get different results?

```sh
curl -X POST https://api.groq.com/openai/v1/chat/completions \
-H "Authorization: Bearer gsk_xxxx" \
-H "Content-Type: application/json" \
-d '{
"model": "meta-llama/llama-4-scout-17b-16e-instruct",
"messages": [{
    "role": "user",
    "content": "tell a joke"
}]
}'

```

- Same issue here. The API worked a few days ago, but now it consistently returns { error: { message: ‘Not Found’ } } .

- Appears that its all because of my location…. I have to use a vpn, i guess… theres nothing else i can do Oh well, unless someone finds a solution vpn-less, i will have to use one.
  - yes we block certain IP ranges and countries like Iran and North Korea from accessing Groq for legal reasons, sorry

- ## 👀 [PR 974 introduces unspecified Redis dependency · Issue · vercel/ai-chatbot _202505](https://github.com/vercel/ai-chatbot/issues/977)
- The issue is that I was using `redis://` as provided by Upstash.
  - However when you connect Upstash to Vercel directly through their integration, the connection string uses `rediss://` which works with this PR.

- ## [Error when chat · Issue · vercel/ai-chatbot _202506](https://github.com/vercel/ai-chatbot/issues/1053)
- Here are three steps that I found the doc was lacking.
  - pnpm tsx lib/db/migrate.ts && pnpm run build
  - AUTH_SECRET
  - LLM keys

- ## [Failed to create guest user (createGuestUser database query) · Issue · vercel/ai-chatbot _202505](https://github.com/vercel/ai-chatbot/issues/1035)
- I had the same problem. Three things that helped me:
  - Creating and connecting the app in Vercel dashboard - vercel link
  - Running vercel env pull
  - Running pnpm tsx lib/db/migrate.ts manually

- [Installation Guide is Incomplete, Create Neon, then no instructions on setting up tables, users, user logging. · Issue · vercel/ai-chatbot _202502](https://github.com/vercel/ai-chatbot/issues/749)
- Pull the environment variables: vercel env pull
  - pnpm tsx lib/db/migrate.ts 
  - pnpm run build
