---
title: lib-aikit-langgraph-community-workflow
tags: [langchain, langgraph, large-language-model, n8n, workflow]
created: 2025-08-11T08:46:25.538Z
modified: 2025-08-11T08:47:03.579Z
---

# lib-aikit-langgraph-community-workflow

# guide

- rpa vs agent
  - agent的操作依赖所提供的api/mcp, 而rpa可以在无api的前提下模拟click等人工操作
# discuss-stars
- ## 

- ## 

- ## 🤼 [Why LangGraph overcomplicates AI agents (and my Go alternative) : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m0hgtt/why_langgraph_overcomplicates_ai_agents_and_my_go/)
- After my LangGraph problem analysis gained significant traction, I kept digging into why AI agent development feels so unnecessarily complex.
  - The fundamental issue: LangGraph treats programming language control flow as a problem to solve, when it's actually the solution.
- What LangGraph does:
  - Vertices = business logic
  - Edges = control flow
  - Runtime graph compilation and validation
- What any programming language already provides:
  - Functions = business logic
  - if/else = control flow
  - Compile-time validation
- My realization: An AI agent is just this pattern. So I built go-agent - no graphs, no abstractions, just native Go:
- https://github.com/vitalii-honchar/go-agent /MIT/202507/go
  - Simplicity: Standard control flow, no graph DSL to learn
  - Clean Architecture - Interface-based design following Go best practices

```go
for {
    response := callLLM(context)
    if response.ToolCalls {
        context = executeTools(response.ToolCalls)
    }
    if response.Finished {
        return
    }
}
```

- Yes, graphs neatly map to function invocation. The point of the graph abstraction is to provide a graphical UI for it that doesn't involve code, which terrifies non technical users.
  - Whenever you see graph based workflow UIs, it's an attempt to cater to a broader user base (n8n, ComfyUI, the zillion non-AI enterprise workflow systems out there, etc). 
  - IMO that type of UI doesn't scale arbitrarily; soon enough you end up with the spaghetti horrors ComfyUI is known for. In this regard code is clearly better as programming languages are built around managing complexity and maintainability, though you can't expect a regular business analyst to deal with Go.

- Every time an industrial use case with a large potential scale comes up, there is a tendency to design graph-based user interfaces (UIs). 
  - This is quite common in manufacturing and production systems, where both design and operations, despite being separate systems, employ such UIs and have been quite successful. 

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

- ## 🆚🤔 [LangChain vs LlamaIndex : r/LangChain _202403](https://www.reddit.com/r/LangChain/comments/1bbog83/langchain_vs_llamaindex/)
- Langchain started as a whole LLM framework and continues to be so. Langchain is much better equipped and all-rounded in terms of utilities that it provides under one roof
  - Llama-index started as a mega-library for data connectors( data connection to your data source ( CSV file, SQL database etc) ). Later on they started expanding to other capabilities after seeing explosive adoption of Langchain. 
  - I would recommend you to start with Langchain. It started out first and has better set of modules.
  - Secondly, do not listen anyone who says Langchain/ Llama-index is crap. They are speaking out their inexperience in this new field.
  - Lastly, best learning / troubleshooting is in source code documentation , first. Documentation in Langchain portal comes second.

- LangChain and LlamaIndex can overlap, but they serve slightly different needs, LangChain shines when you need chaining logic and tool orchestration, while LlamaIndex is more focused on data-connectivity and retrieval.

- My reasons for favoring these frameworks -
  - Excellent suite of data loaders / collectors. 
  - Abstraction is bad when your use case doesn't fit the functionality given by the framework. If it's given though, the task becomes a breeze
  - Langchain has provided it's own language now - LCEL. Adds a layer of customizability.

- As an experienced engineer DO NOT start with either of these two. They're both extremely abstracted and known to frustrate experienced devs. Junior devs will find them helpful though.
  - OP I tend to ignore any comments that start with "as an experienced ..." because they're using a call to authority to convince you, rather than just having a good idea that can stand on its own.
  - There are no experienced devs when it comes to large language models because the latest models' age is measured in months.
  - Start learning by identifying a toy example that's close to your use case, then figure out how the example was built. Work down the abstraction chain until you've got something that works well for you 

- ## 🆚 [RPA vs AI agents vs Agentic Process Automation : r/rpa _202502](https://www.reddit.com/r/rpa/comments/1iftre3/rpa_vs_ai_agents_vs_agentic_process_automation/)
- Not everything needs an LLM to perform rules based decisions. In fact it's expensive (energy, cost, infra) or wasteful to do so.
  - Most rpa platforms are rebranding as AI platforms with rpa backbones so I suspect we'll see a blending of the two into the future.

- APA: The AI is just the ‘R’ part of RPA, imo
- You’re right that many are moving toward “Agentic Process Automation, ” where rulebased automation (RPA-style) blends with LLM powered reasoning. Hybrid setups are becoming more popular because they balance reliability with flexibility.

- My two cents on this is that for most enterprises, the bottleneck will be tooling. 
  - How will you interact with all your applications and data, transparently and be assured the outcomes are precise. Hence why RPA will still be popular. It’s much faster to build out and maintain an automation with an RPA solution than with a non low code platform.
  - Orchestrating agents and tools is not trivial, but it’s also not technically difficult. LangGraph is the great example of that and most RPA vendors are building this in or have some means of doing it already.

- I've worked as Upath rpa dev, and now i build chatbots. 
  - I feel like they need to co-exist because the AI agents are able to interact with apps only using API. 
  - For things where you don't have API and you want the bot to actually interact with an app and perform repetitive steps, you still need RPA. 
  - You can trigger this RPA process using the chatbot but i feel like this works only for smaller processes. 
  - In my previous company we had hundreds of different bot with a very big volume, it's impossible to orchestrate this using AI agents

- I’ve worked at a company that was one of the largest banking institutions in its state. They deployed software from a company who had few APIs and no integrations with the systems they wanted. 
  - The banking dev team had an overflowing backlog so they couldn’t get to making something custom and the company said there would be a wait and potential cost to build those APIs. 
  - We used RPA to build a UI automation to get the job done.
  - A LOT of people just assume there will be APIs for everything, but it takes devs to make them to start with and that assumes you’re not dealing with the above hurdles. 
  - RPA will be a thing in larger slower moving companies, but smaller companies probably won’t have much use for it if they have a dev team and APIs are available.

- It seems that RPA is not going to die but will cover less use cases. In my opinion the trend right now will gear towards workflow automation tools (make.com, n8n, etc.) where you can connect and call whatever tools are best for the use case (RPA, AI Agent, API, etc) or even for certain steps in the process
  - At my role currently we only use RPA strictly for UI click automations where there are no APIs available. AI Agents are slowly starting to be used but at this point the hype outweighs the actually utility. However that will definitely flip in the next 3-6 months. AI capabilities have an exponential growth not linear.

- You have use cases that need automation and you have tools to automate. 
  - Line up the most suitable tool for each use case based on your value prop: Speed, Accuracy, Cost, Scale etc etc.
  - Ignore the puns and spin, its all gimmicks.
  - With that being said, RPA is crap and there is no real place for it in the modern tech stack.

- I’d say AI agents (intelligence layer - planning, decision making, reasoning) and automation/rpa (automation layer, whether its api or ui based) are complementary to each other - they thrive together.
  - RPA thrives in rules based end to end process so its more reliable for structured tasks, while agents thrive on processes having lots of nuances - its can get more flexible by leveraging its ability to plan, reason, execute and iterate bots/automations.

- The purpose of RPA is not just to provide cost savings on manual tasks, but to do so while at the same time providing a completely transparent and signed off set of business rules for the automated process, as set by operational stakeholders. The automation will not deviate from that (assuming reasonable RPA design).

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
# discuss-internals
- ## 

- ## 

- ## 

- ## [Can you explain why it is called a graph? · langchain-ai/langgraph _202403](https://github.com/langchain-ai/langgraph/discussions/171)
  - I'm coming from a graph database perspective and I don't understand why this is called a graph.
  - Wouldn't it be better to call it langflow? I have watched a few videos on langgraph and it is described as a flow, not a graph

- LangGraph's `StateGraph` abstraction extends our implementation of `Pregel`, the graph processing framework.
  - [Pregel: a system for large-scale graph processing _201006](https://dl.acm.org/doi/abs/10.1145/1807167.1807184)
  - The orchestration is organized into nodes (vertices) and edges. Each node performs computation, and the edges determine the control flow. Edges then denote relationships.
- Thank you. That helps differentiate between graph databases and graph process frameworks.
# discuss-langchain
- ## 

- ## 

- ## 

- ## 

- ## 



- ## [LangGraph, Google ADK, or LlamaIndex. How would you compare them? : r/LangChain _202504](https://www.reddit.com/r/LangChain/comments/1jw87c0/langgraph_google_adk_or_llamaindex_how_would_you/)
- langgraph: very low level, will give you a lot of control over your agents. also very good focus on persistence (enabling memory, human in the loop, etc)
  - llamaindex: more focused on rag but has some agent things, but just less built out around that area
  - google adk: higher level than langgraph, more similar to crewai/autogen/etc

- For google ADK, and agent frameworks, the questions I keep in mind:
  - Code: Is the tool restricted to a particular programming language, no-code, tweak-able?
  - Structure: Does it stay within a single process, launch many processes, work on multiple machines, use a single or many LLMs (locally or via API)?
  - Memory: Does it share memory between agents, over the network? can it pause and restart? does it run regularly and remember prior results?
  - Debugging: Does it have a UI, good ways to inspect progress, ways to allow human checks, tools to debug when not working well?

- I have used llama_index to build a RAG application. One thing that was useful is observability. You can add a few lines of code and see what LLM / embedding calls are being made. Langfuse provides good free limits.

- llamaindex has pivoted a lot into building Agents rather than RAG pipelines. Thats why you saw a demo of agentic AI with llamaindex.

- ## 💄 [LangGraph Studio Alternatives? Has Anyone Built Their Own Visual Agent Debugging System? : r/LangChain _202501](https://www.reddit.com/r/LangChain/comments/1i92evk/langgraph_studio_alternatives_has_anyone_built/)
  - I’ve been experimenting with LangGraph Studio for building and debugging LangGraph agents. 
  - While it’s powerful for visualizing stateful workflows and adding breakpoints, the dependency on LangSmith and limited customization options are holding me back.
  - Are there open-source alternatives to LangGraph Studio for designing/debugging agent workflows visually?
  - Context: LangGraph Studio is great, but I’m looking for something more flexible for production use. Projects like `LangFlow` or `AutoGen Studio` are close but lack granular control over state transitions.

- Flowise is similar to LangFlow. I've only skimmed its starter templates, but it seems to offer more control over state management. A major drawback from my experience though is its debugging capabilities. It's very difficult to trace errors back to specific nodes or understand their root cause.
  - Another visual workflow tool you might like is Dify. I use it myself currently, but its agent implementation differs from LangGraph.

- Mastra is open source and has workflows (and a visual dev server) built in. It's a little earlier than LangGraph but moving really fast.
  - CrewAI has flows, but there is no visual studio as far as I know and I haven't gone further than the getting started experience.

- ## 🤔 [Can I use LangGraph without LangChain? : r/LangChain _202411](https://www.reddit.com/r/LangChain/comments/1gu3yya/can_i_use_langgraph_without_langchain/)
- yes - you can definitely use LangGraph without any LangChain components! In LangGraph the graph nodes are just python functions that can contain arbitrary logic, so you can call OpenAI client or query a vectorstore directly in the node. good luck with your multi-agent RAG app!

- I'm pretty sure you can use langGraph without using langchain. Most of langGraph does not use langchain anyway, and it's mostly the prebuilt components that do, so you could substitute them with your own code, which shouldn't be that complex. You could also check out langflow, which offers a similar way to create your own agents.

- ## [Disadvantages of Langchain/Langgraph in 2025 : r/LangChain _202507](https://www.reddit.com/r/LangChain/comments/1m2skwu/disadvantages_of_langchainlanggraph_in_2025/)
- As it has always been, the best thing you can do is learn to understand what the tool solves and how that tool particularly solves it. If you know why you would need to use it and how it solves that problem, then pivoting to different system will become just understanding how they specifically do it, as concepts often transfer between tools.

- Langchain has a lot of features, but honestly, most of them don’t do much for me. The only parts I really like are the abstractions for:
  - Messages (AIMessage, HumanMessage, etc)
  - Chat models (ChatOpenAI, ChatGoogleGenerativeAI, etc)
  - Tools (creating custom tools)
  - What I find useful is how you can swap out models and the rest just works, since everything’s pretty standardized (though there are some edge cases).
  - Outside of that, though, it gets pretty painful.
  - I think the underlying ideas behind Langgraph are solid, but the steep learning curve and the sense of vendor lock-in kept me from fully committing to it.

- [A story of using langchain/langgraph : r/LangChain _202507](https://www.reddit.com/r/LangChain/comments/1m3kn6x/a_story_of_using_langchainlanggraph/)
  - I hope you enjoy my story of working with langchain and langgraph these past 2, almost 3 years. Also, this short story is about sticking with langchain and langgraph. Not doing things your own or choosing to integrate other libraries. But we'll talk about that towards the end.
- Langchain before LCEL
  - So I started using langchain in its beginnings, I think most of you will remember all the StuffDocumentsChain and MapReduceChain, so this was way before the current LCEL way of doing. 
  - We started using langchain just because it was one of the first "popular" libraries in the space.
  - Our uses cases at the time were simple, The most common one, and that we also had was to have a generic RAG platform where users would deposit their documents and we'd handle all the infrastructure (auth, database, frontend, endpoints etc.), embeddings, vector store etc. At the time RAG was "painful"
- Langchain and LCEL
  - Then langchain introduced LCEL. It's a declarative way to chain together "chains". It's nice in theory, but in practice, for complex use cases, it adds another layer of complexity. 
  - And that layer of complexity is solved with langgraph. And this is a recurrent theme with langchain. New layers of complexity that get solved by introducing new tools. 
  - To put it simply, LCEL = pipelining runnables. And Runnables would be this general interface that's somewhat synonym to "processing". It's something you can run.
  - The big advantage of LCEL is that it solves these rigid ways of creating chains through the langchain built-ins, and offers an easy way to compose chains, and even reuse them in some scenarios. You can think that it is syntactic sugar
  - The main drawback of LCEL is debuggability. For a moderately complex chain, if you don't filter the logs, you'd get tons of details that just make it hard to read them.
  - The other major drawback is how to inject data at runtime in the chain.
  - The other major drawbacks of LCEL is that the composability and reusability of chains that it claimed was also one of its weaknesses. The easily composable chains are the ones that come from some langchain built-ins like their parsers (say StrOutputParser) or the base chat models (say ChatOpenAI) etc. But that is very limited. 
- Langgraph
  - I think langgraph came to be by transposing what we saw in the real world, developers making LLMs do different things and then make them interact with each other.
  - Langgraph solves many of the issues above because it forces you to define your state or data schema beforehand, so when you want to use the graph (or the chain written as a graph), you're more likely to adapt the code around it to that state, rather than write the chain in a way that adapts to the code around it. Also, you have more granular control on how its mutated and when.
  - But langgraph still suffers from a lot of the burden of the 1000 abstractions that langchain introduces, and also from how complex langgraph itself is. 
  - Another drawback of working with constantly evolving things is, you are somewhat dependent on how good the library developers handle their updates.
- The advice I'd give for using langgraph in production is the same I'd give to any other code in production. Use Pydantic, or at least dataclasses with validation. Think clearly of your state and what you need to be passed through the graph and for what reason. Type hinting obviously, though it's a pain with langchain sometimes. 
  - One another advice I'd give is, as you are writing your graph's code, think of its evaluation and write its evaluation code.
- I think, one good practice (and obviously this will depend a lot on your use cases) is to separate data access from the nodes of the graph as much as possible. Make the agents or LLMs or whatever have access to the data through tools. Whether those tools are defined as nodes in the graph or are bound to the LLM is not important, the important part is not to have a non-tool node that fetches data.
  - You can restrict parts of the graph from access some data, but data injected dynamically in the state through nodes is harder to reason about and it's just better handled with a tool in that case. 
  - And obviously, any compute heavy processing should not be a node in your langgraph graphs.

- I know there are a bunch of other libraries such as autogen, crewai, pydantic-ai. I have not tested them in their current form, but I have tested them in their beginnings and they fell short of features compared to langgraph. langgraph allowed to do much more complex workflows.

- You made a good point — LLMs are just functions, and it's about learning how to use them effectively.

- ## [LangChain bad, I get it. What about LangGraph? : r/LocalLLaMA _202407](https://www.reddit.com/r/LocalLLaMA/comments/1dxj1mo/langchain_bad_i_get_it_what_about_langgraph/)
- My main grudge against langchain was the fact that behind the initial impression of good abstractions you immediately met with discrepancies in behaviors of internal implementations - how messages are passed around, how system prompt is defined, how parameters can be proxied to a model, how external APIs are called - you named it. And every little integration is written in a slightly different way.
  - In general, seeing this low consistency level makes me want to avoid using the project, as it's an indication of the overall level of quality there.

- Hmm as a LISP and Haskell enthusiast, it seems like lang-graph is trying to implement a DSL but doing it in a weird way because in Python there is no easy way to represent Python code as a code graph or abstract syntax tree.

- For entirely offline solution, I have a project LangGraph-GUI, this use ollama.

- I think the main thing LangGraph adds is, a state machine framework for human in the loop with time travel.
  - you get a flowchart graph way of doing things, and you get a nice chart. But it won't do anything you couldn't do writing your control flow in Python. 
  - In the future I could see people building low-code GUI tools to create a workflow interactively on top of LangGraph without typing a bunch of boilerplate.
  - If you didn't like LangChain by itself, you're not going to like using it within some LangGraph nodes. It seems more about adding a control flow framework to LangChain.

- LangGraph adds very little to itself. `langchain-core` is a huge dependency. If we think of it, a chain is just a linear graph. 
  - LangGraph library only implements "a way" to declare a workflow, checkpointer and manage state. These could be theoretically just 3 files but LangGraph took care of edge cases, is organised and and tested. 
  - Majority of the actual functionality after compiling your graph comes form `Runnable` and its variants defined in `langchain-core`. Even graph visualisation method is defined there and not in LangGraph.
  - So, if you code your rag using requests or openai or re modules, LangGraph will eventually wrap it with Runnable primitive. If you are okay with that, which I am, then great!
- OK, I think if all you want is a runnable you can subclass or decorate a python function with `@chain`, but the reason to use langgraph instead would be, you like the whole state graph framework

- LangChain’s original strength was its ability to connect LLMs with actual information sources—databases, APIs, PDFs, tools like Gmail or Slack. That’s what made it practical.
  - As we move toward more agentic workflows, the biggest bottleneck isn’t flow control or state management—it’s connectors.
  - There’s a serious tooling gap here—and not for lack of ideas. It’s that the most powerful tools are not open.
  - Big tech players (Google, Microsoft, OpenAI) are prioritizing integrations within their own ecosystems—Gemini, Copilot, GPTs—rather than enabling external developers to build agentic SaaS on top of their platforms.
- perhaps using anthropic's mcp is one solution?wrap the mcp server with your own llm and it does do a pretty god job

- ## [Should I learn LangGraph instead of LangChain? : r/LangChain _202408](https://www.reddit.com/r/LangChain/comments/1env9og/should_i_learn_langgraph_instead_of_langchain/)
  - while I reading the documents of LangChain about Agents I saw warning note. I think LangChain won't support building Agents with Langchain anymore. They will use LangGraph to create Agents anymore. 

- Knowing Langchain will make your Langgraph learning journey quite easy since they both use LCEL. That said, Langgraph is the most capable framework for building Agents currently. I wouldn't even look at Autogen or CrewAI. They have a quickstart on their page, just search Langgraph tutorial and see how you feel about it. It's not that hard but like anything, requires practice

- 👷 Erick from LangChain here. Would highly recommend starting with LangGraph for your entry point if you're working with agents. 
  - you can also follow the migration guides if you're used to working with the legacy AgentExecutor (still supported, but much less controllable than langgraph)!
  - You can use them completely separately, or together. 
  - LangGraph is much lighter-weight in the sense it's just orchestrating python functions (nodes and conditional edges), and you can choose to use LangChain integrations/other abstractions within your nodes.

- ## [langchain到底该怎么使用，大家在项目中实践有成功的案例吗? - 知乎](https://www.zhihu.com/question/609483833)
- 如果目的快速搭出可用demo, 是可以考虑用框架的, langchain这里就帮了我很多
  - 第一个优点, 方便模型切换
  - 长期记忆ConversationSummaryBufferMemory会自动帮我总结对话历史, 并在每次对话中带着这段总结. 好处是确实总结了, 但好像又没总结. 因为带的细节太多了, 实际上并没有省多少token.
  - 短期记忆, 也就是Redis History Message实质上就是把list存储到Redis里了, 没有太大技术含量.
  - 最大的问题是什么呢, 是Langchain里面有两类模型llm和chatmodel.
  - 因为历史原因, langchain大部分代码和文档都是基于llm的, 比如我发送一段对话, 让llm回复, 我发送的是一段文本. 而OpenAI官网例子中, 是发送的一串message list
  - 为了更好地符合OpenAI的使用方法, 我就从基于llm的代码, 改为了基于chatmodel.

# discuss
- ## 

- ## 

- ## 

- ## [What is the other best alternative to LangGraph? : r/LangChain _202411](https://www.reddit.com/r/LangChain/comments/1ggrqis/what_is_the_other_best_alternative_to_langgraph/)
- No surprise there, every senior dev, techlead and CTO despises most current frameworks like langgraph, langchain, crewai, ... Due to being overly complex...
- The whole Lang* ecosystem is a repackaging of existing ideas under the banner of generative AI. LangChain is an elaborate library for string formatting and web requests; 
  - LangGraph reinvents state machines but worse because it thinks a request to an LLM warrants an entire framework.
  - To engineers who have been around for a while: there’s nothing new here. It’s just JSON, strings, web requests, and maybe some database persistence. Use libraries which already exist for these things.

- Here is a building block for any agent library
  - memory ( basically past alternate messages) + ability to track current messages , ability to take multi modal messages)
  - tools - function calling or plain prompt
  - an executor (kind of react ) or state based like langraph
  - parser ( structured output- can be json parser plus LLM call on fallback )
  - ability to retry
  - multi language - ii8n
  - ability to use multiple llms.
  - agent agent interaction
  - ability to pass context between agents . ( database in production vs in memory)
  - prompt optimizer
  - ui to visualize and test
  - evaluator
- When you have the whole package and start combining things every other new framework will be bulky .
  - So there is nothing wrong with the frameworks out there . These will adapt as “LLM as a service “ brings newer capability (probably some functionality will shift left like memory) .

- Can you give a concrete example and explain exactly what would be more difficult about it without langgraph?
  - As soon as you start having multiple agents with complex routing logics among them, and complex interaction and information exchange, using langgraph becomes a lot more convenient
  - Mind you, you can do everything without it, it will just require more time and effort, as you would have to reimplement many functionalities that langgraph gives you out of the box, like a shared state, persistency, routing functionalities, and even an easier interface for tool usage and task delegations

- Nice part about LangGraph is the use of Pregel, which you can roll yourself, but it’s there and the state management isn’t half terrible. If you skim the paper you have a reasonable understanding of LangGraph.

- Right now LangGraph is the best thing in my opinion....where are you struggling....if I have to guess you might have missed some concepts or you are yolo-ing your DAG on the fly.

- I actually prefer the Graph part over the Chain part. If you want to get more control you could just build on the Pregel implementation that Graph ships with and ignore the rest, maybe even ditch Chain if your model of choice comes with a decent SDK (OpenAI assistants for example)

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

- ## 🆚 [LangChain vs LangGraph? : r/LangChain _202505](https://www.reddit.com/r/LangChain/comments/1kynej0/langchain_vs_langgraph/)
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

- One way to think about it - langchain is a linear version of langgraph
  - Langchain will allow you to create a linear chain of AI workflow: prompt generation - LLM call - structured output.
  - Langgraph will allow you to create a more complex state machine, with flow branching, going back, etc, depending on runtime state.

- LangChain is great for sequencing simple LLM tasks, but when your workflow needs loops, states, or embedded agents, LangGraph’s graph-based orchestration is a game changer.

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
