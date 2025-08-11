---
title: lib-aikit-langgraph-community-workflow
tags: [langchain, langgraph, large-language-model, n8n, workflow]
created: 2025-08-11T08:46:25.538Z
modified: 2025-08-11T08:47:03.579Z
---

# lib-aikit-langgraph-community-workflow

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## Most people think of langgraph as agent abstractions, but it’s powered by a low level event driven framework under the hood _202507
- https://x.com/hwchase17/status/1940847199157682383
- LangGraph primitives > abstractions. Expose the core and let us build custom flow control + metrics.

- This was perhaps my biggest realization when I was building @MagickML . Graphs were event driven. Events as inputs and outputs. And easy to shuttle events between graphs, handle side effects, etc. Graphs with events and hooks are the way.

- Exposing the different levels of abstraction will enable developers across the board to use the framework effectively to their use case.

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
# discuss-pm-workflow-ai ⛓️
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Is it really complicated to integrate n8n with langraph? : r/AI_Agents _202506](https://www.reddit.com/r/AI_Agents/comments/1lkxlv9/is_it_really_complicated_to_integrate_n8n_with/)
- Not complicated at all! Just use n8n's webhook node to receive data from LangGraph and HTTP Request node to call LangGraph APIs. 
  - I do this with multiple AI services - n8n handles the simple automations and triggers complex workflows in LangGraph when needed. 
  - Start with n8n for quick wins, then add LangGraph endpoints for the heavy lifting. Way faster than building everything in LangGraph from scratch.

- ## 尝试下 coze studio 开源版本，目前看其整体功能不如 Dify 完备，而且 Coze 做的比 Dify 好的功能基本都阉割了（如实时语音模式），留下的功能没有亮点。
- https://x.com/9hills/status/1949689118784717097
- 有一个很重要的点你没说：License 差异。
  - Coze是完全的 Apache 2.0，Dify 是 Apache 2.0 + 限制（不能多租户 + Logo限制）。
  - 如果只是公司内部自用，无区别。主要是对定制平台的小ToB SaaS公司来说，Coze 会方便做二开。

- 是的，而且模型配置也很麻烦，插件也不多

- ## People have the problem running super long Browser Use tasks (agent forgets stuff after 50+ steps)
- https://x.com/gregpr07/status/1934645184483975566
  - We are fixing this in two ways
  - 1. Workflow Use - we have a branch (heavy wip) which takes a prompt, explores the page with Browser Use agent, and generates the workflow (HARD)
  - 2. Finding new ways to make the agent memory and thinking more robust (VERY HARD, lots of experimenting). This requires really big brain (we hired IMO medal guy to tackle this problem)
  - If you relate with the problem, try using our super early alpha 0.0.0 of Workflow Use auto generation of workflows

- Word of advice, reflect on whether you're not trying to just outrun the scaling hypothesis through mathematics. It gets expensive and the timelines to capture roi are shorter than ever.

- ## 工作流平台大家关注dify 和 coze比较多，还有一个非常不错的框架 langflow
- https://x.com/leeoxiang/status/1884945535507083426
  - 1、Flow as an API，代码优先，workflow可以直接转换为可执行的代码；
  - 2、支持丰富的逻辑判断；

- ## 又一个值得学习的爬虫&RPA开源库 Maxun
- https://x.com/yan5xu/status/1881150511220752884
  - 自带低代码后台，轻松抓取任何网页数据，自动提取整理成表格，还能处理滚动分页和验证码
  - 核心用 Playwright 做浏览器自动化，配合 puppeteer-extra-plugin-stealth/recaptcha 插件处理反爬和验证码，再用 adblocker 清理广告干扰

# discuss-alternatives 🆚
- ## 

- ## 

- ## 

- ## [Can n8n fully replace frameworks like LangChain, LangGraph, AutoGen, etc? : r/n8n _202503](https://www.reddit.com/r/n8n/comments/1j3ub58/can_n8n_fully_replace_frameworks_like_langchain/)
- 🤔 No. Because in frameworks you can use other libs, and in n8n you can use only things that support n8n. But for most of simple tasks n8n can be enough
- call an mcp serv code and you doing whatever you want
  - Or do everything on server faster

- One of the cons I've stumbled upon is scaling. If you're trying to build an agentic system that serves a large number of users you're better off building something with LangGraph since there much more flexibility in configuring it to be scalable.
  - It seems that n8n is best if you're a small business trying to automate things internally, or you're trying to automate aspects of your own job as a solo working individual. (n8n is far better to automate things like that then trying to wrestle with LangGraph)

- whenever you are having some issue implementing something just create a rest api of that and use in n8n

- the issue with n8n is that it is a “no code” solution, which means you can’t build standalone apps to run them run without n8n. 

- ## 🆚 [Langchain vs n8n : r/LangChain _202502](https://www.reddit.com/r/LangChain/comments/1ige7m2/langchain_vs_n8n/)
- I haven't used n8n, but I think the only people who would benefit from paying to build an agent in low code would be non-developers or those who want to quickly validate an idea with a proof of concept.

- n8n got langchain abstractions under the hood. With some limitations. If you want full function low-code langchain editor - it's flowise.
  - [AI Agents Explained: From Theory to Practical Deployment – n8n Blog _202502](https://blog.n8n.io/ai-agents/#why-use-langchain-for-ai-agents)
  - n8n takes it a step further by providing a low-code interface to LangChain. In n8n, you can simply drag and drop LangChain nodes onto the canvas and configure them.
  - Advanced users can even write JS code for some of the LangChain modules. 
  - n8n supports the JavaScript implementation of LangChain. 
  - n8n has integrated most of the core LangChain components as visual nodes.

- If you are a coder then go for Langchain If you are a product manager then go for n8n
  - N8n have lots of nodes for ai but I personally feel like it is easy to write a python code than do a hell lot of configuration in gui. 
  - Even for a simple flow you have to do tons of configuration in n8n You can easily try that with n8n docker and check
- this is how i felt with n8n.. even AI can spit the code out and make quick automation

- I find that most of the agent workflow can be simply done with n8n. The future is moving towards this part of graph based workflow (blender, unreal, comfyui) and n8n can simplifying the process to create AI agent for your business.

- ## [LangChain vs LangGraph vs n8n — Which one are you using and why? : r/n8n _202507](https://www.reddit.com/r/n8n/comments/1m2sc7g/langchain_vs_langgraph_vs_n8n_which_one_are_you/)
- N8N is langchain under the hood when it comes to agents if my memory is not tricking me
  - There are also frameworks like agno, or pydantic ai that provide more robust, customizable and performant agents.
  - Personnaly I build my agents in n8n, and then I ask to the client if he wants it hard coded in pydantic or agno, but often they decline as n8n suffice + traditional dev is more expensive

- n8n agent nodes are literally just langchain nodes(more flexible n8n node), these are not mutually exclusive

- ## 🆚 Which framework should I use for developing AI agents? LangGraph or @pydantic Agent framework? _202505
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

- ## Announcing Flows AI: A light-weight library to build agent workflows, on top of Vercel AI SDK. _202501
- https://x.com/grabbou/status/1882139484994551861
  - Use any LLM and provider of your choice.
  - All patterns from Anthropic article provided out of the box.
  -  we have a branch open and POC of a builder project, where we want to provide a very light-weight flow-based UI for configuring and visualizing this. Standalone and CLI-like, so you can execute those workflows like JavaScript files
- There’s more than on the screenshot, including routers etc. Error handling can be done with a custom agent, overall - very simple, although I am interested to implement the missing blocks!

- No unnecessary abstractions whilst literally abstracting away the AI SDK 

- Is it capable of passing and using structured outputs and objects ?
  - Agent is a function, so simply use generate object inside. The helpers we provide operate on text for now (keeping things slim), but adding that if requested isn’t too much of work

- Does it support streaming?
  - Not yet, keeping scope limited. Theoretically possible
# discuss-roadmap
- ## 

- ## 

- ## 
# discuss-changelog
- ## 

- ## 

- ## 

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
# discuss
- ## 

- ## 

- ## 

- ## 

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

- ## [Thoughts on LangGraph.js & LangChain.js — Great work, but we need more TypeScript-native design : r/LangChain _202505](https://www.reddit.com/r/LangChain/comments/1kelzq6/thoughts_on_langgraphjs_langchainjs_great_work/)
  - much of the design still feels like a direct translation from Python. Patterns like dict-style objects, Pydantic-like schemas, or deep class hierarchies don’t always fit naturally into the JS/TS ecosystem.
  - By contrast, look at Spring AI, also inspired by LangChain, but fully adapted to the Spring ecosystem.
  - I'd love to see more TypeScript-first designs: interfaces, composability, structural typing
  - It’s fine to port initially, but long-term success means embracing the strengths of each language and community.

- On LangChain, while I don’t have anything that I can share publicly, I have been cooking up a new architecture for ChatModel integrations that I think will go a long way toward what you’re talking about here. If I accomplish my goals it should make these integrations much more consistent and predictable, while feeling a lot more TS-native.
  - On LangGraph we’re looking to improve our types substantially, and to provide better devX around things like external detection/handling of interrupt/resume, functional API, state management, tooling, and a host of things that crop up when you go to deploy to some bespoke, self-hosted environment. We’re also investing heavily in prebuilt agents, and reusable components for genetic applications.

- One example from LangGraph.js: using Annotation. Root() to define state feels like a non-idiomatic pattern for TypeScript. It works, but it’s abstract and hard to reason about.
  - In LangChain.js, there’s a similar issue with ChatPromptTemplate.fromMessages(). Passing arrays with magic keys like 'system' is brittle and lacks type safety. TS devs generally expect APIs to guide them with strong types. Those are

- ## [What even is the point of langgraph : r/LangChain _202501](https://www.reddit.com/r/LangChain/comments/1i8rmki/what_even_is_the_point_of_langgraph/)
- It's overkill for a simple workflow. For more complex things where you might need to retry specific steps or orchestrate steps in parallel at scale, a Graph based workflow tool definitely helps.

- LangGraph actually is worse than just straight code. The only reason you would EVER use a graph for anything is if it executed in parallel, which langgraph does not. 
  - ❓ So internally langgraph runs as a sequential series of function calls wrapped in a completely unnecessary and impossible to comprehend graph API. 
  - And its readability is zero.
