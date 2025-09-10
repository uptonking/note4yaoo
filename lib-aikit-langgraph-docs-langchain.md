---
title: lib-aikit-langgraph-docs-langchain
tags: [docs, langchain]
created: 2025-09-05T07:18:24.640Z
modified: 2025-09-05T07:18:34.805Z
---

# lib-aikit-langgraph-docs-langchain

# guide

# overview
- langchain exists to be the easiest place to get started building with LLMs.
- There are two core focuses
  - We want to make it possible for developers to build with whatever the best model is at the time. 
  - we want to make it easy to use these models to orchestrate more complex flows that interact with other data and computation, tools

- Architecture
  - `langchain-core`: Base abstractions for chat models and other components like chat models, vector stores, tools 
  - `langchain`: Chains, agents, and retrieval strategies that make up an application's cognitive architecture.
  - langchain-community: Third-party integrations 
  - `langgraph`: Orchestration framework for combining LangChain components with persistence, streaming
  - `langserve`: A package to deploy LangChain chains as REST APIs

- 
- 
- 
- 

# docs-v1.0

- 
- 
- 
- 
- 
- 
- 

# docs-v0.x-langchanjs
- The model on its own does not have any concept of state.
  - We can see that it doesn’t take the previous conversation turn into context, and cannot answer the related question
  - To get around this, we need to pass the entire conversation history into the model

- 
- 
- 
- 
- 
- 
- 

- LLMs aren’t perfect at generating structured output, especially as schemas become complex. 
  - You can avoid raising exceptions and handle the raw output yourself by passing `includeRaw: true`. 

- You can also create a custom prompt and parser with LangChain Expression Language (LCEL), using a plain function to parse the output from the model

- 
- 
- 
- 

# docs-v0.x
- Why LangChain?
  - Standardized component interfaces: a standard interface for key components, making it easy to switch between providers.
  - Orchestration: Complex control flow, Human-in-the-loop
  - Observability and evaluation

- Multimodality: The ability to work with data that comes in different forms, such as text, audio, images, and video.
- Runnable interface: The base abstraction that many LangChain components and the LangChain Expression Language are built on.
- LangChain Expression Language (LCEL): A syntax for orchestrating LangChain components. Most useful for simpler applications.
- Retrieval: Information retrieval systems can retrieve structured or unstructured data from a datasource in response to a query.
- Retrieval Augmented Generation (RAG): A technique that enhances language models by combining them with external knowledge bases.
- Text splitters: Split long text into smaller chunks that can be individually indexed to enable granular retrieval.
- Embedding models: Models that represent data such as text or images in a vector space.
- Few-shot prompting: A technique for improving model performance by providing a few examples of the task to perform in the prompt.

- For models that support more than one means of structuring outputs (i.e., they support both tool calling and JSON mode), you can specify which method to use with the `method=` argument.
  - When the underlying method for structuring outputs is tool calling, we can pass in our examples as explicit tool calls. 

- Tool calling allows a chat model to respond to a given prompt by "calling a tool".
  - this is actually not the case! The model only generates the arguments to a tool, and actually running the tool (or not) is up to the user.
  - Tool calling is a general technique that generates structured output from a model, and you can use it even when you don't intend to invoke any tools. An example use-case of that is extraction from unstructured text.

- we need to pass in tool schemas that describe what the tool does and what its arguments are.
  - Chat models that support tool calling features implement a `.bind_tools()` method for passing tool schemas to the model. 
  - Tool schemas can be passed in as Python functions (with typehints and docstrings), Pydantic models, TypedDict classes, or LangChain Tool objects.
- Note that chat models can call multiple tools at once.

- 
- 
- 
- 
- 

# rag
- Corrective-RAG (CRAG) is a recent paper that introduces an interesting approach for self-reflective RAG.
  - The framework grades retrieved documents relative to the question
  - If at least one document exceeds the threshold for relevance, then it proceeds to generation
  - It will use web search to supplement retrieval

- Self-RAG is a recent paper that introduces an interesting approach for self-reflective RAG.
  - The framework trains an LLM (e.g., LLaMA2-7b or 13b) to generate tokens that govern the RAG process in a few ways
  - Input: x (question) OR x (question), y (generation)
    - Decides when to retrieve D chunks with R
    - Output: yes, no, continue

- 
- 
- 
- 

- `WebBaseLoader` uses `urllib` to load HTML from web URLs and `BeautifulSoup` to parse it to text. 
  - We can customize the HTML -> text parsing by passing in parameters into the BeautifulSoup parser via `bs_kwargs`. 

- we use a `RecursiveCharacterTextSplitter`, which will recursively split the document using common separators like new lines until each chunk is the appropriate size. This is the recommended text splitter for generic text use cases.

- Conversational experiences can be naturally represented using a sequence of messages. 
  - In addition to messages from the user and assistant, retrieved documents and other artifacts can be incorporated into a message sequence via tool messages.
  - This motivates us to represent the state of our RAG application using a sequence of messages.

- 
- 
- 
- 
- 
- 
- 
- 
- 

# blogs

# ⏳ changelog-langchain

- 202210: A month before ChatGPT, LangChain was launched as a Python package
  - It consisted of two main components: LLM abstractions, and high level “chains” for common use cases.
  - “Chains” were predetermined steps of computation to run. 
- 202212: The first general purpose agents were added to LangChain. They were based on the ReAct paper (ReAct standing for Reasoning and Acting). 
  - They used LLMs to generate JSON that represented tool calls, and then parsed that JSON to determine what tools to call.
- 202301: OpenAI releases a “Chat Completion” API. Previously, models took in strings and returned a string.
  - LangChain releases a JavaScript version.
- 202302: LangChain Inc was formed as a company around the open source LangChain project.
- 202303: ✨ OpenAI releases “function calling” in their API. 
- 202307: 🚀 LangSmith is released as closed source platform
- 202401: langchain releases 0.1, its first non-0.0.x. 
- 202402: 🚀 LangGraph is released as an open source library
  - a low-level orchestration layer allowing developers to control the exact flow of their agent.
- 202407: LangChain splits integrations out of the core package, and either into their own standalone packages (for the core integrations) or langchain-community (for the long tail).
- 202503: langchain-core updates their message format accordingly to allow developers to specify these multimodal inputs in a standard way.
- 202509: 🎯 LangChain releases 1.0 with two major changes:
  - Standard content blocks: Model APIs evolved from returning messages with a simple content string to more complex output types - reasoning blocks, citations, server-side tool calls, etc. LangChain evolved it’s message formats to standardize these across providers.
  - Complete revamp of all chains and agents in langchain. All chains and agents are now replaced with only one high level abstraction: an agent abstraction built on top of LangGraph. 
# more
