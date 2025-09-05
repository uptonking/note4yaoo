---
title: lib-aikit-langgraph-community-langchain
tags: [community, langchain, langgraph]
created: 2025-09-05T07:18:02.221Z
modified: 2025-09-05T07:18:16.308Z
---

# lib-aikit-langgraph-community-langchain

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## [如何评价LangChain LCEL? - 知乎](https://www.zhihu.com/question/634584770)

- LangChain的表达式语言（LCEL）通过重载__or__运算符的思路，构建了类似Unix管道运算符的设计，实现更简洁的LLM调用形式。
  - 另外，Chain也可以分叉、合并，组合出更复杂的DAG计算图结构。
  - 基于LCEL确实能描述比较复杂的LangChain计算图结构，但依然有DAG天然的设计限制，即不能支持“循环”。
  - 于是LangChain社区推出了一个新的项目——LangGraph，期望基于LangChain构建支持循环和跨多链的计算图结构，以描述更复杂的，甚至具备自动化属性的AI工程应用逻辑，比如智能体应用。

- 又来一个tensorflow，满眼既视感？为啥谁都想在语言上再做一个语言，你说你做了计算图调度做了极致优化你上actor都行，最后还是做了个皮但是增加了debug难度，你说你加不就是因为调试以及观测性更差了吗，顺便要狂吹自家。不知道会不会像tf debugger一样出来个lang debugger
# discuss
- ## 

- ## 

- ## 

- ## 

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

- ## [学习AI，是不是要学习LangChain这个框架？ - 知乎](https://www.zhihu.com/question/1899527932420002416)
- 如果学习应用落地，那LangChain，SGLang，vLLM是很值得看的框架。
  - 如果学习模型算法训练，那Deepspeed，Megatron，Torch是很好的框架。

- 学习这些框架的意义，并不是说你一定要在实际工作中用某一个框架，而是遇到了类似的问题，可以去参考现有的解法。
  - 像 Langchain 其实封装了很多东西，调试也非常复杂，但他整体设计的思路还是值得借鉴和学习。简单来说，就是它过度封装了，但你一点都不了解的话，连设计思路都没有。

- 只是学炼丹，那是完全没必要学Langchain的。如果要做LLM开发，我觉得先照着OpenAI API Document依葫芦画瓢，同时做过工业项目了，有软件工程的经验，再去学习Langchain也不迟。
  - 学完以后可能会发现绝大多数场景不会用Langchain，但也会发现Langchain提供的思想在工程里还是值得借鉴的。

- langchain是个包装严严实实的框架，东西太多太重了，会让你陷入学习它的api中去，从而错误的以为lamgchain就是入口似的

- 虽然链式思维（CoT）提示已经表明LLMs可以为算术和常识推理等任务生成推理痕迹，但其缺乏对外部世界的访问可能会导致事实虚构等问题。
  - ReAct通过让LLMs为任务生成口头推理痕迹和动作来解决这个问题。语言模型可以根据输入生成响应，但ReAct通过允许模型与其环境互动来增强这一点。这种互动是通过模型可以用来提问或执行任务以获取更多信息和更好地理解情况的文本动作实现的。
