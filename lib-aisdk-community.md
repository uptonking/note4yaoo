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

- ## [Is it worth using LangGraph with NextJS and the AI SDK? : r/LangChain _202506](https://www.reddit.com/r/LangChain/comments/1lnsoud/is_it_worth_using_langgraph_with_nextjs_and_the/)
- Integrating LangGraph with Next.js and Vercel's AI SDK can be tricky due to limited docs, especially for streaming. 

- I found the js langchain to be always behind python, so you often are missing tutorials or things aren't supported. I ended up liking mastra

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

- ## 

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

- 
- 
- 
- 
- 

- ## [How would you build an LLM agent application without using LangChain? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1i2n0il/how_would_you_build_an_llm_agent_application/)
- llamaindex is just as bad

- what's bad about LangChain?
- everything is overcomplicated and it's painful to do even very default stuff, for example: How I can do rag + function calling + text streaming with local model? It will be very difficult to get this right with docs.

- LangGraph is quite good imo. You can either use prebuilt components or add completely customised ones.

- The good so far: unified interface for different LLMs, retry/fallback mechanisms, langfuse/smith tracing and profiling (especially for out-of-the-box RAG setups), some RAG building blocks, structured outputs.
- The bad: the actual chains (a kitten dies every time some dumbnut tries clever things with operator overloading in Python and breaks code introspection), LCEL, documentation. I steered away from almost everything due to the latter.

- This is the same discussion about frameworks in web dev: a framework can make you massively more productive but it comes at the cost of complexity to your codebase

- ## 🌰 [The Most Powerful Way to Build AI Agents: LangGraph + Pydantic AI (Detailed Example) : r/AI_Agents _202504](https://www.reddit.com/r/AI_Agents/comments/1jorllf/the_most_powerful_way_to_build_ai_agents/)
  - we built an AI Listing Manager Agent capable of web scraping (crawl4ai), categorization, human feedback integration, and database management.
  - [How We Built an AI Listing Manager Using LangGraph, PydanticAI & Crawl4AI - YouTube](https://www.youtube.com/watch?v=KPw6IPTOUPQ&t=3150s)
  - I also show how we orchestrate agents using LangGraph, and how we built an interactive front end with Streamlit to manage everything seamlessly
- The system is made of 7 specialized Pydantic AI agents connected with Langgraph.
  - Search agent: Searches the internet for potential new listings
  - Filtering agent: Ensures listings meet our quality standards.
  - Summarizer agent: Extract the information we want in the format we want
  - Classifier agent: Assigns categories and tags following our internal classification guidelines
  - Feedback agent: Collects human feedback before final approval.
  - Rectifier agent: Modifies listings according to our feedback
  - Publisher agent: Publishes agents to the directory
- In LangGraph, you create a separate node for each agent. Inside each node, you run the agent, then save whatever the agent outputs into the flow's state.
  - The trick is making sure the output type from your Pydantic AI agent exactly matches the data type you're storing in LangGraph state. 
  - This way, when the next agent runs, it simply grabs the previous agent’s results from the LangGraph state, does its thing, and updates another part of the state. By doing this, each agent stays independent, but they can still easily pass information to each other.
- Human-in-the-loop. Listings are only published after explicit human approval. 

- Judging by your workflow, I’m wondering if it can even be called agentic? it seems like a sequence of tasks are being performed one after the other without any loop of multi-agent collaboration or complex decision making. Correct me if I’m wrong?

- how would this be different from pydantic graph ?
  - I used Langgraph because it's battle-tested

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

- ## [Thoughts on LangGraph.js & LangChain.js — Great work, but we need more TypeScript-native design : r/LangChain _202505](https://www.reddit.com/r/LangChain/comments/1kelzq6/thoughts_on_langgraphjs_langchainjs_great_work/)
  - much of the design still feels like a direct translation from Python. Patterns like dict-style objects, Pydantic-like schemas, or deep class hierarchies don’t always fit naturally into the JS/TS ecosystem.
  - By contrast, look at Spring AI, also inspired by LangChain, but fully adapted to the Spring ecosystem.
  - I'd love to see more TypeScript-first designs: interfaces, composability, structural typing
  - It’s fine to port initially, but long-term success means embracing the strengths of each language and community.

- On LangChain, while I don’t have anything that I can share publicly, I have been cooking up a new architecture for ChatModel integrations that I think will go a long way toward what you’re talking about here. If I accomplish my goals it should make these integrations much more consistent and predictable, while feeling a lot more TS-native.
  - On LangGraph we’re looking to improve our types substantially, and to provide better devX around things like external detection/handling of interrupt/resume, functional API, state management, tooling, and a host of things that crop up when you go to deploy to some bespoke, self-hosted environment. We’re also investing heavily in prebuilt agents, and reusable components for genetic applications.

- One example from LangGraph.js: using Annotation. Root() to define state feels like a non-idiomatic pattern for TypeScript. It works, but it’s abstract and hard to reason about.
  - In LangChain.js, there’s a similar issue with ChatPromptTemplate.fromMessages(). Passing arrays with magic keys like 'system' is brittle and lacks type safety. TS devs generally expect APIs to guide them with strong types. Those are

- ## [Why are people choosing LangGraph + PydanticAI for production AI agents? : r/LangChain _202505](https://www.reddit.com/r/LangChain/comments/1kpkybb/why_are_people_choosing_langgraph_pydanticai_for/)
- I'm using the Typescript version (Langgraph + Zod) but the big answer is task decomposition plus reliability. Agents perform more reliably when you decompose the problem and give each subtask the right tools to get the job done. Zod (or pydantic) helps you reinforce a reliable schema. This makes it much easier to build in proper guardrails for bigger LLM tasks.

- With LangGraph, we defined a clear sequence: summarize → extract headings → draft content → run SEO check.
  - PydanticAI ensured each output matched strict formats (e.g. JSON with predefined fields for title, meta description, etc.).
  - We even added a conditional branch where, if the SEO score is below 80, it loops back to rewrite with a different prompt.

- I have personally used LangGraph, Crew AI, LangChain and gotten briefly introduced to AutoGen and others. I feel LangGraph gives complete control over the agents you are building. 
  - The ease of coding and visualizing the agentic system end-to-end makes it the go-to choice.

- ## [Langgraph vs Pydantic AI : r/LangChain _202503](https://www.reddit.com/r/LangChain/comments/1ji4d2k/langgraph_vs_pydantic_ai/)
- theoretically you can mix Pydantic AI with Langraph which is what I recommend you do. 
  - But my recommendation would be to stay away from langchain as much as you can while using langgraph.
  - Even within langgraph, be careful about using their built-in components too much e.g. use a third party memory library mem0 instead of built in checkpointer.

- Pydantic is a kind of open environment for mainly software developers. Creating agents are like 2 lines of code and managing the workflow is also like building a state machine, rather than chain or acyclic graphs. It has its pros and cons. Pros are probably, it's easy and fast to bootstrap anything. Cons is that the developer needs to keep a conscious eye on the code architecture as the flow is free.
  - Langchain or graph is bloated, but that enforces some standard of development which has its own value proposition in scalable architecture.

- I was in the middle of refactoring a module from using LangChain to PydanticAI when I made the shocking discovery that the latter doesn't appear to have proper retry logic or connection management for concurrent requests. For retries it instead relies on a clunky FallbackModel paradigm. You instead need to wrap it with your own retry and async logic for real world usage at scale. This alone has convinced me to stick with my current LangChain implementation for the moment.

- ## [LangChain vs LangGraph? : r/LangChain _202505](https://www.reddit.com/r/LangChain/comments/1kynej0/langchain_vs_langgraph/)
- Langchain helps you make LLM calls with structured data, tools, etc…
  - Langgraph helps you build a whole complex workflow defined of a series of steps called nodes, each of which could be an LLM call, running some code, doing whatever. These nodes are connected by edges, which are basically the rules of once you finish one node which you go to next.

- LG, by itself doesn't have infrastructure to communicate with LLMs by itself, is designed to be used in conjunction with, something like LC.
  - LG is _just_ a flow design tool for program execution. Agents are just one particular type of flow i.e. with a feedback step.
  - If you want to build something like deep research you need to add `langgraph-supervisor` on top of vanilla LG as it doesn't do it out of the box

- I use LangChain just for LLM calls with structured output. Then, I try to write everything from scratch, as you don't want to get pulled into the LangChain ecosystem.
  - LangGraph, on the other hand, is perfect for orchestrating complex workflows/agents.
  - So I suggest going with LangGraph to orchestrate your logic + custom code for LLM calls/RAG stuff.

- my experience with langgraph has been very positive, cursor can build langgraph very well

- What I like about LangGraph is you can customize and configure your agent/chatbot apps really flexibly, but they also offer some prebuilt things like a ReAct agent that is more plug-n-play.

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

- ## tell me why your agent framework is better than langgraph _202504
- https://x.com/hwchase17/status/1913662736963412365
- There seems to be a common pattern for the agent syntax that everyone is regressing to. (Not to mention everybody thinks everybody else is copying from them.)
  - At some point, they all pretty much look and act the same, with very little differentiation.
  - The “real” differentiation starts to be in the tools layer for memory, retrieval, etc.

- Frankly we wrote ours when there weren't other great options in the space and at this point it's super tailored to our work so I wouldn't replace it.
  - But being honest we actually don't rely heavily on the graph element of it anymore and if I was rewriting it I would drop the graph executor in favor of a stack based approach leveraging tool calls to queue and pop or something like that because we naturally kind of moved there anyway.
  - https://github.com/BismuthCloud/asimov /apache2/202506/python
    - A Python framework for building AI agent systems with robust task management in the form of a graph execution engine, inference capabilities, and caching.
    - We support advanced features like State Snapshotting, Middleware, Agent Directed Graph Execution, Open Telemetry Integrations and more.
- in practice we could probably just model the whole thing as a queue or stack of tool calls so yeah the graph stuff just feels heavier than it needs to be is what I was trying to say
- so main agent is basically using a tool call to route to another agent (diff system prompt, tools)?
  - yeah basically, and then we’re only relying on our actual graph executor rn for things like writing a commit message and posting to GitHub but I can see how I would fold that in

- short term memory, long term memory, human in the loop, human on the loop, observability
  - you can write all those yourself, but a good framework will handle those for you

- While we use Langgraph, fragmentation seems concerning (ex. langgraph-supervisor, langgraph-swarm).. IMHO, they should be part of the same ecosystem, otherwise they feel like they would be left on their own to die similar to langserve.

- People are choosing their abstractions based on ergonomics and other factors. Graphs are explicit but hard to intuitively reason about in aggregate.

- Langgraph seems to be an orchestration tool at it's core. This operates on a much lower level that a framework like PydanticAI which is a higher abstraction.
  - A better comparison would be with the likes of PydanticGraph or even Temporal. Here's one - it's hard to inject dependencies like database driver objects in Langgraph nodes. You have to keep it global or do some weird hack. Its possible but not as clean as DI in PydanticGraphs.

- LangGraph’s visual nodes rock for prototyping LLM flows, but OpenAI Agent Framework brings native func calling with type safety, built in RAG memory, multi model orchestration GPT, Whisper, Vision telemetry & secure sandboxes

- Langgraph lacks batch inference support. Pretty important functionality imo

- https://x.com/fungiblexbt/status/1940579019113816341
  - this is why the langgraph framework beats autogen and crewai in terms of state management and persistent memory
  - i would recommend crewai for beginners looking to get into agentic systems but langgraph for complex tasks that require context (which is most tasks)

- ## Most people think of langgraph as agent abstractions, but it’s powered by a low level event driven framework under the hood _202507
- https://x.com/hwchase17/status/1940847199157682383
- LangGraph primitives > abstractions. Expose the core and let us build custom flow control + metrics.

- This was perhaps my biggest realization when I was building @MagickML . Graphs were event driven. Events as inputs and outputs. And easy to shuttle events between graphs, handle side effects, etc. Graphs with events and hooks are the way.

- Exposing the different levels of abstraction will enable developers across the board to use the framework effectively to their use case.

- ## langgraph: we've spent a lot of time on the langgraph persistence/state layer _202501
- https://x.com/hwchase17/status/1874486239723712939
  - enables production ready short term & long term memory, checkpointing, human-in-the-loop, time travel, etc
  - if we made this work with ANY agent framework (including DIY) would that be interesting to folks?

- Yeah I think people would use it!  You can roll your own memory thing but lots of people don’t want to do that esp when getting started

- would be very cool if i can bring my own database (and embedding/inference). 
  - i’ve been looking for something like this but mem0 and zep are too opinionated 

- One thing missing for me on the persistence layer is the ability to export the long term memory from a LangGraph Cloud Deployment, it would be really useful (seeding, migration of long term memory from one deployment to another, backup...)

- Related: clearer edge traversal visibility (e.g., from_node → to_node) and pre-execution indicators (e.g., next_node) would make debugging and steaming a lot cleaner in LangGraph.

- Does langchain have something to interact with browsers? The idea is agent perform certain task on the browser, for example, search for a name(s) or something or fill in the text fields, etc.

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
