---
title: lib-aikit-langgraph-docs
tags: [docs, langgraph]
created: 2025-08-11T08:47:23.340Z
modified: 2025-08-11T08:47:32.124Z
---

# lib-aikit-langgraph-docs

# guide

# overview
- To create an agent, use `create_react_agent`
- To configure an LLM with specific parameters, such as temperature, use `init_chat_model`

- Static prompt: A string is interpreted as a system message.
- Dynamic prompt: A list of messages generated at runtime, based on input or configuration.

- When you enable the `checkpointer`, it stores agent state at every step in the provided checkpointer database (or in memory, if using `InMemorySaver`).
  - when the agent is invoked the second time with the same `thread_id`, the original message history from the first conversation is automatically included, together with the new user input.

- To produce structured responses conforming to a schema, use the `response_format` parameter. 
  - The schema can be defined with a `Pydantic` model or `TypedDict`.

- 
- 
- 
- 
- 
- 
- 
- 

# docs

# blogs

## [LangGraph 的 内存/记忆 机制总结 - 知乎](https://zhuanlan.zhihu.com/p/1915604388443031303)

- 旨在为 AI 代理提供在不同交互中存储、检索和利用信息的能力
- 短期记忆是针对单个对话线程（或会话）的，可以在该线程内的任何时间被回忆。它类似于人类在一次对话中记住的内容。
  - LangGraph 将短期记忆作为代理状态（State）的一部分进行管理。这个状态会通过检查点（Checkpointer）持久化到数据库中，这意味着即使会话中断，也可以随时恢复。
  - 更新机制： 短期记忆在图被调用或某个步骤完成时更新，并在每个步骤开始时读取。
  - 典型应用： 最常见的短期记忆形式是对话历史（conversation history）。
  - 针对长对话可能导致的上下文窗口限制和性能下降问题，LangGraph 提供了以下策略：
    - 编辑消息列表（Editing message lists）
    - 总结过去对话（Summarizing past conversations）： 通过调用 LLM 对历史对话进行摘要，并将摘要作为新的上下文传入，以减少消息数量同时保留关键信息
  - LangGraph 将短期记忆作为其核心图状态（Graph State）的一部分进行管理，并通过内置的“reducer”函数实现状态的原子性更新。这种基于图的状态机模式使得管理对话历史和相关上下文（如上传文件、检索文档）变得非常自然和强大。检查点机制保证了会话的可恢复性。

- 长期记忆是跨对话线程共享的，可以在任何时间、任何线程中被回忆。它不像短期记忆那样局限于单个会话。
  - LangGraph 将长期记忆存储为 JSON 文档，并使用存储（Store）（如 `InMemoryStore` 或生产环境中的数据库支持的存储）进行管理。
  - 每个记忆都组织在一个自定义的命名空间（namespace）和一个唯一的键（key）下。命名空间通常包含用户 ID、组织 ID 或其他标签，便于分层组织信息，并支持跨命名空间的搜索（通过内容过滤器）。
  - 长期记忆的类型
    - 语义记忆（Semantic Memory）： 存储事实和概念。
    - 情景记忆（Episodic Memory）： 存储过去的事件或行为经验。常
    - 程序记忆（Procedural Memory）： 存储执行任务的规则或指令。
  - 记忆更新时机：
    - 热路径（Hot Path）： 在代理的应用程序逻辑运行时实时创建记忆。优点是实时更新和透明度，但可能增加复杂性、延迟，并影响记忆的数量和质量。
    - 后台（Background）： 作为单独的异步任务创建记忆。优点是避免主应用延迟、分离逻辑，并允许更聚焦的任务完成

- LangGraph 明确区分了短期记忆（会话级）和长期记忆（跨会话），并进一步将长期记忆细化为语义记忆（事实）、情景记忆（经验）和程序记忆（规则）。这种细粒度的区分和管理方式在主流框架中相对不常见。
- LangGraph 提供了一个明确的 Store 抽象，用于存储和检索长期记忆（JSON 文档）。它支持命名空间和内容过滤/向量相似性搜索，并提供了“profile”和“collection”两种不同的语义记忆管理模式。这种抽象使得长期记忆的集成更为直接。

## ⏳ [The Evolution of Graph Processing: From Pregel to LangGraph _202507](https://medium.com/@pur4v/the-evolution-of-graph-processing-from-pregel-to-langgraph-6e8c2063df98)

- The story of large-scale graph processing is fundamentally about solving one of computer science’s most challenging problems: how do you efficiently compute on massive, interconnected datasets that don’t fit on a single machine
  - This journey from makeshift MapReduce solutions to Google’s revolutionary Pregel system, and ultimately to modern applications like LangGraph’s multi-agent AI coordination
- Google’s 2010 Pregel paper didn’t just introduce a new framework — it established an entirely new way of thinking about distributed graph computation that has influenced everything from social network analysis to modern AI agent coordination. 

- Life Before Pregel: The Dark Ages of Graph Processing
  - Single-machine approaches were simpler to program but hit hard physical limits. 
  - The dominant approach for distributed processing was MapReduce, but graph algorithms created a perfect storm of incompatibility. MapReduce required data chunks to be processed independently, while graph algorithms inherently needed information from neighboring vertices. This violated MapReduce’s core assumption of data locality and independence.
  - The performance implications were devastating. A typical PageRank computation on large graphs required hundreds of chained MapReduce jobs, with processing times measured in hours to days. 
  - Each iteration involved moving the complete graph state across the network — a massive waste of resources where disk I/O time dominated computation time by factors of 5–20x.
  - The fundamental problems were clear: excessive data movement violated principles of data locality, synchronization overhead made coordinating distributed graph state expensive, and poor resource utilization meant massive clusters were required for basic graph analytics. 
  - Academic benchmarks from 2009–2010 showed MapReduce implementations were often 10–100x slower than theoretical optimal performance, with up to 90% of execution time spent on data movement rather than computation.

- What is Pregel: Thinking Like a Vertex
  - how Pregel works — it transforms graph problems into a series of coordinated communication rounds called “supersteps.”
  - Pregel builds on Leslie Valiant’s Bulk Synchronous Parallel (BSP) model from the 1980s. 
  - Pregel’s genius lies in its “think like a vertex” programming model. Instead of reasoning about the entire graph, you write code from a single vertex’s perspective
  - Each vertex maintains state that persists across supersteps, can modify its own values and outgoing edges, and communicates through explicit message passing. 
  - This abstraction makes complex distributed graph algorithms surprisingly intuitive to implement.

- After Pregel: The New Graph Processing Era
  - Pregel’s 2010 publication triggered an explosion of innovation in graph processing frameworks. 
  - The core insight — that vertex-centric programming with BSP synchronization could make distributed graph algorithms both intuitive and scalable — inspired dozens of systems that extended, optimized, and adapted the original design.
  - Apache Giraph emerged as the dominant open-source implementation, originally developed at Yahoo and later adopted by Facebook as their primary graph processing platform. Giraph’s technical innovations included memory optimizations (serializing edges into byte arrays rather than Java objects), flexible input models supporting multiple data sources, and enhanced parallelization with multi-threading within workers.
  - Apache Spark’s GraphX took a fundamentally different approach by embedding graph processing within a general-purpose data processing framework. Instead of creating another standalone graph system, GraphX extends Spark RDDs with graph abstractions, enabling the same data to be viewed as both graphs and collections.
  - PowerGraph (Carnegie Mellon) introduced the Gather-Apply-Scatter (GAS) programming model specifically designed for power-law graphs with highly skewed degree distributions. By using vertex-cut partitioning — distributing edges rather than vertices — PowerGraph could handle high-degree vertices more efficiently than traditional approaches.

- These post-Pregel systems demonstrated several key evolution patterns:
  - Architectural Improvements: Memory management moved from object-based to byte-array representations, communication was optimized through message combining and sharded aggregators, and fault tolerance was enhanced with better checkpointing mechanisms.
  - Programming Model Extensions: Multi-phase algorithms gained support through master computation between supersteps, while higher-level abstractions and domain-specific languages made graph programming more accessible.
  - Specialization: Different systems optimized for specific use cases — social networks (Giraph), machine learning (PowerGraph), integrated analytics (GraphX), or research flexibility (GPS).

- The real test of Pregel’s impact lies in its production applications at web-scale companies
  - Beyond PageRank, Google employs Pregel-based systems for web spam detection, analyzing link patterns to identify manipulative linking schemes, link farms, and other attempts to game search rankings.
  - Twitter developed GraphJet, a specialized real-time graph processing engine that maintains a bipartite interaction graph between users and tweets entirely in memory. This system achieves 1 million edge ingestions per second while serving 500 recommendations per second with sub-second latency.

- LangGraph and Pregel: Coordinating AI Agents in the Modern Era
  - The emergence of large language models and multi-agent AI systems has created an unexpected new application for Pregel’s BSP model. 
  - LangGraph, developed by LangChain, demonstrates how the same principles that revolutionized web-scale graph processing now enable sophisticated coordination of AI agents in production systems.
- Why Traditional Approaches Fall Short
  - Conversational AI and multi-agent systems expose fundamental limitations in traditional DAG-based workflows. Linear processing pipelines cannot handle the iterative, cyclical reasoning required by intelligent agents. 
  - Traditional frameworks are stateless, processing each interaction independently without maintaining context across conversations or sessions.
  - Traditional approaches cannot maintain shared state across these agents or recover gracefully when individual agents fail.
- The core problems mirror pre-Pregel graph processing challenges: rigid execution paths without dynamic decision-making, poor state management across distributed components, and limited fault tolerance for long-running processes.
  - LangGraph addresses these limitations by implementing Pregel’s BSP model specifically for AI agent coordination. 
  - The system models agent workflows as graphs with shared state, executable nodes, and conditional edges, organizing execution into discrete supersteps where agents that can run in parallel execute simultaneously.
- Agent Communication follows Pregel’s message-passing paradigm:
  - Direct messaging: Agents send specific updates to target agents
  - Broadcast communication: Agents send messages to multiple recipients
  - State-mediated interaction: Communication through shared state channels
  - Conditional routing: Dynamic message routing based on current state
- Each superstep follows the familiar BSP pattern: agents process their current state in parallel, send messages to other agents, and synchronize at a barrier before the next superstep begins.
- Think of LangGraph like coordinating actors in a complex theatrical performance. 
  - Each actor (AI agent) has their role and script, but they must coordinate their actions with other actors on stage. 
  - Supersteps are like synchronized scenes where all actors perform their parts simultaneously, then pause for stage direction (synchronization) before continuing to the next scene.
- Unlike improvisation where actors might interrupt each other or miss cues, the BSP model ensures every actor completes their lines before the scene transitions.

- Production Applications and Success Stories
  - LinkedIn’s SQL Bot demonstrates LangGraph’s production capabilities, using coordinated agents for natural language to SQL conversion. 
  - Uber’s code migration system employs multiple agents for large-scale automated refactoring across repositories. 
  - Replit’s coding assistants use collaborative agent architectures for complex programming tasks.

- Technical Architecture and Fault Tolerance
  - LangGraph implements comprehensive checkpoint systems that save state after each superstep, enabling powerful fault tolerance capabilities. Unlike traditional systems where failures require complete restarts, LangGraph can recover from any checkpoint and even support “time travel” functionality — rolling back and forking execution from previous states.
  - Memory management operates at multiple levels: working memory for current superstep reasoning, conversation memory for multi-turn interactions, long-term memory for cross-session knowledge retention, and shared memory accessible to all agents in the system.
  - The system provides human-in-the-loop integration with interrupt functions that pause execution for human input

- 🤔 Why BSP Works Better Than Event-Driven Models
  - Event-driven architectures create race conditions where unpredictable message ordering leads to inconsistent agent behavior. Agents may operate on stale information, debugging becomes extremely difficult due to non-deterministic execution paths, and the system lacks built-in persistence mechanisms.
  - LangGraph’s BSP approach provides deterministic execution with predictable superstep-based processing, global synchronization ensuring all agents reach consistent states, and built-in checkpoint/recovery mechanisms. The synchronous nature provides consistent timing characteristics and enables reliable resource management across distributed agent networks.
  - Performance characteristics demonstrate BSP’s advantages: predictable latency through synchronous supersteps, resource efficiency via parallel node execution, scalability through framework-managed distribution, and reliability with comprehensive fault tolerance.

- The Assembly Line Analogy (for BSP)
  - Think of LangGraph’s BSP coordination like a sophisticated assembly line where each station (agent) performs specialized work on shared products (state). 
  - Every station completes its work before the conveyor belt moves to the next position (superstep synchronization). If any station encounters problems, the entire line can pause, fix the issue, and resume from exactly where it left off (checkpointing).
  - This coordination model ensures `quality` control (no agent operates on inconsistent state),  `efficiency` (maximum parallelism within each superstep), and `reliability` (comprehensive error recovery mechanisms).

- Why does BSP’s synchronous model persist despite its apparent inefficiency? 
  - The answer lies in the fundamental tension between performance and predictability. 
  - While asynchronous systems can achieve higher throughput by eliminating global barriers, they sacrifice deterministic execution and introduce complex debugging challenges.
  - The emergence of “chaos engineering” in distributed systems suggests that even modern cloud-native architectures struggle with the complexity introduced by fully asynchronous coordination.

- Pregel and Real-Time Streaming: An Unexplored Frontier
  - Can BSP adapt to real-time streaming scenarios where data arrives continuously rather than in discrete batches? Traditional stream processing frameworks like Apache Storm or Kafka Streams use event-driven models, but recent research suggests hybrid approaches might be possible.
  - The challenge lies in checkpointing and fault tolerance for rapidly changing state. How do you implement recovery mechanisms when the system state changes thousands of times per second? This represents a fundamental research opportunity at the intersection of stream processing and graph algorithms.

- Modern federated learning systems face coordination challenges remarkably similar to early graph processing. 
  - Multiple parties need to collaboratively train machine learning models while maintaining data privacy and handling network partitions or device failures.
  - Could Pregel-style coordination improve federated learning? The BSP model’s deterministic execution and built-in fault tolerance seem well-suited to scenarios where participating devices may join or leave unpredictably. Each device could be modeled as a vertex in a learning graph, with model updates passed as messages between supersteps.

- Privacy-preserving graph algorithms represent another frontier. Techniques like differential privacy or secure multi-party computation could potentially be integrated with BSP coordination to enable privacy-preserving social network analysis or collaborative filtering.

- Will the rise of large language models fundamentally change how we think about graph processing? 
  - LLM-guided graph partitioning could potentially outperform traditional hash-based or even sophisticated algorithms by understanding semantic relationships between vertices. 
  - Conversely, will graph processing techniques enhance LLMs? The success of retrieval-augmented generation (RAG) suggests that combining structured knowledge graphs with language models creates capabilities neither approach achieves alone. Graph neural networks applied to LLM architectures represent an active research area with significant potential.

- How will specialized hardware affect graph processing architectures? 
  - Modern GPUs excel at parallel computation but struggle with the irregular memory access patterns common in graph algorithms. 
  - Graph processing units (GPUs specifically designed for graph workloads) are emerging from research labs, potentially requiring fundamental changes to software architectures.

## [Building LangGraph: Designing an Agent Runtime from first principles _202509](https://blog.langchain.com/building-langgraph/)

- LangGraph builds upon feedback from the super popular LangChain framework, and rethinks how agent frameworks should work for production. 
  - We aimed to find the right abstraction for AI agents, and decided that was little to no abstraction at all. 
  - Instead, we focused on control and durability. 
- This post shares our design principles and approach to designing LangGraph based on what we’ve learned about building reliable agents.

- We started LangGraph as a reboot of LangChain’s super popular chains and agents more than two years ago. 
  - We decided that starting fresh would give us the most leeway to address all the feedback we had received since the launch of the original langchain 
- The main thing we heard was that langchain was easy to get started but hard to customize and scale.
- When we had to make tradeoffs, we prioritized production-readiness over how easy it would be for people to get started.

- “Do we actually need to build LangGraph?” And, “Why can’t we use an existing framework to put agents in production?” 
  - we had to define what makes an agent different (or similar) to previous software. 
  - More latency makes it harder to keep users engaged
  - Retrying long-running tasks when they fail is expensive and time-consuming
  - The non-deterministic nature of AI requires checkpoints, approvals, and testing

- 🐛 The first defining quality and challenge of LLM-based agents is latency. We used to measure the latency of our backend endpoints in milliseconds. Now, we need to measure agent run times in seconds, minutes, or soon hours.
  - This is because LLMs themselves are slow and are becoming slower with test-time compute. It’s also because we often need multiple LLM calls to achieve our desired results, with looping agents, and chaining
  - So, we identified two features that would come in handy when building agents: Parallelization, Streaming 💡

- 🐛 Long-running agents fail more often because, the longer they run, the more opportunity there is for something to go wrong.
  - When traditional software bugs out, you usually want to retry. With AI agents? That may not be the best approach. 
  - going back to the beginning is pretty time consuming and also expensive.
  - So we knew we had to add two more features to the list: Checkpointing, Task queue 💡

- 🐛 the non-deterministic nature of LLMs creates two more challenges.
  - With LLMs, both input and their output is open-ended. 
  - two more features then become very useful when going to production: Human-in-the-loop, Tracing 💡

- If the agent you’re building doesn’t need most of these features (eg. because it’s a very short agent without tools and a single prompt), then you might not need LangGraph, or any other framework.

- Why was a new framework needed?
- Existing frameworks were mostly split between two categories:
  - DAG frameworks (made popular by Apache Airflow and many others): These we had to exclude just based on the name, as LLM agents really benefit from looping, ie. the computation graph for an LLM agent is cyclical, and thus cannot be handled by DAG algorithms.
  - Durable execution engines (made popular by Temporal and others): they were lacking some of those specific features — namely streaming. In addition, these engines introduced latency between steps which would have been noticeable to chatbot developers. Lastly, due to their design, the performance degrades the more steps there are in the history

- We designed LangGraph with two leading principles.
  - We don’t know what the future holds for AI. The only assumptions we wanted to bake into it were the realizations we talked about above, i.e. that LLMs are slow, flaky, and open-ended.
  - It should feel like writing code. The public API for the framework should be as close as possible to writing regular framework-less code
- These principles impacted a few key design decisions that have stayed with us ever since.
  - First, the runtime of the library is independent from the developer SDKs. The runtime (which we call PregelLoop) implements each of the features listed earlier, plans the computation graph for each agent invocation, and executes it. This design enables us to evolve the developer APIs and the runtime independently. 
  - Second, we wanted to provide each of the 6 features as building blocks, with the developer free to pick which to use in their agent at any point in time.

- ✨ let’s look at how LangGraph implements each of the 6 features we wanted to have (as a reminder, these are parallelization, streaming, checkpointing, human-in-the-loop, tracing and a task queue).
- If there is one idea that informs every other architectural decision we’ve made, it is the idea of structured agents. 
- Once you make the choice to structure agents into multiple discrete steps, you need to choose some algorithm to organize its execution. 
  - Even if it’s a naive one that feels like “no algorithm, ” which is where LangGraph started before launch. 
  - The problem with using “no algorithm” is, while it may seem simpler, you’re making it up as you go along, and end up with unexpected results. (For instance, an early version of a precursor to LangGraph suffered from non-deterministic behavior with concurrent nodes). 
  - The usual DAG algorithms (topological sort and friends) are out of the picture, given we need loops. We ended up building on top of the BSP/ Pregel algorithm, because it provides deterministic concurrency, with full support for loops (cycles).

- Our execution algorithm works like this:
  - Channels contain data (any Python/JS data type), and have a name and current version (a monotonically increasing string)
  - Nodes are functions to run, which subscribe to one or more channels, and run whenever they change
  - One or more channels are mapped to input, ie. the starting input to the agent is written to those channels, and therefore triggers any nodes subscribed to them
  - One or more channels are mapped to output, ie. the return value of the agent is the value of those channels when execution halts
  - The execution proceeds in a loop
  - The execution loop stops when there are no more nodes to run (ie. after comparing channels with their subscriptions we find all nodes have seen the most recent version of their subscribed channels), or when we run out of iteration steps (a constant the developer can set).
# more
