---
title: lib-aikit-langgraph-docs-langchain
tags: [docs, langchain]
created: 2025-09-05T07:18:24.640Z
modified: 2025-09-05T07:18:34.805Z
---

# lib-aikit-langgraph-docs-langchain

# guide

# overview
- Architecture
  - `langchain-core`: Base abstractions for chat models and other components like chat models, vector stores, tools 
  - `langchain`: Chains, agents, and retrieval strategies that make up an application's cognitive architecture.
  - langchain-community: Third-party integrations 
  - `langgraph`: Orchestration framework for combining LangChain components with persistence, streaming
  - `langserve`: A package to deploy LangChain chains as REST APIs
# docs-v1.0

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
- 
- 
- 

# blogs

# more
