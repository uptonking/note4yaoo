---
title: lib-aisdk-docs
tags: [aisdk, docs]
created: 2025-08-08T07:36:08.968Z
modified: 2025-08-08T07:36:16.802Z
---

# lib-aisdk-docs

# guide

# overview

# docs
- AGI refers to models that predict and generate various types of outputs (such as text, images, or audio) based on what’s statistically likely, pulling from patterns they’ve learned from their training data. 

- A LLM is a subset of generative models focused primarily on text.
  - An LLM takes a sequence of words as input and aims to predict the most likely sequence to follow. 
  - The model continues to generate sequences until it meets a specified stopping criterion.

- An embedding model is used to convert complex data (like words or images) into a dense vector (a list of numbers) representation, known as an embedding. 
  - Unlike generative models, embedding models do not generate new text or data. 
  - Instead, they provide representations of semantic and syntactic relationships between entities that can be used as input for other models or other natural language processing tasks.

- Each provider typically has its own unique method for interfacing with their models, complicating the process of switching providers and increasing the risk of vendor lock-in.
- AI SDK Core offers a standardized approach to interacting with LLMs through a language model specification that abstracts differences between providers.

- Prompts are instructions that you give a large language model (LLM) to tell it what to do.
  - Many LLM providers offer complex interfaces for specifying prompts. They involve different roles and message types. 

- Text prompts are strings. They are ideal for simple generation use cases, e.g. repeatedly generating content for variants of the same prompt text.
- System prompts are the initial set of instructions given to models that help guide and constrain the models' behaviors and responses.
  - System messages are messages that are sent to the model before the user messages to guide the assistant's behavior. 
- A message prompt is an array of user, assistant, and tool messages. They are great for chat interfaces and more complex, multi-modal prompts. 
  - Each message has a `role` and a `content` property. The content can either be text (for user and assistant messages), or an array of relevant parts (data) for that message type.

- Assistant messages are messages that have a role of assistant. They are typically previous responses from the assistant and can contain text, reasoning, and tool call parts.

- While LLMs have incredible generation capabilities, they struggle with discrete tasks (e.g. mathematics) and interacting with the outside world (e.g. getting the weather).
- Tools are actions that an LLM can invoke. The results of these actions can be reported back to the LLM to be considered in the next response.

- Tools (also known as function calling) are programs that you can provide an LLM to extend its built-in functionality. 
  - This can be anything from calling an external API to calling functions within your UI

- A tool is an object that can be called by the model to perform a specific task. You can use tools with generateText and streamText by passing one or more tools to the `tools` parameter.

- You can automatically pass tool results back to the LLM using multi-step calls with streamText and generateText.

- Schemas are used to define the parameters for tools and to validate the tool calls.

- Streaming UIs can help mitigate this issue by displaying parts of the response as they become available.
  - This is because the blocking UI has to wait for the entire response to be generated before it can display anything, while the streaming UI can display parts of the response as they become available.

- While streaming interfaces can greatly enhance user experiences, especially with larger language models, they aren't always necessary or beneficial. 
  - If you can achieve your desired functionality using a smaller, faster model without resorting to streaming, this route can often lead to simpler and more manageable development processes.

- When building AI applications, you often need systems that can understand context and take meaningful actions.
- When building these systems, the key consideration is finding the right balance between flexibility and control. 

- Patterns 💡

- Single-Step LLM Generation
  - one call to an LLM to get a response.

- Multi-Agent Systems
  - Multiple LLMs working together, each specialized for different aspects of a complex task.

- Tool Usage
  - Enhanced capabilities through tools (like calculators, APIs, or databases) that the LLM can use to accomplish tasks.
  - The AI SDK makes this multi-step tool usage straightforward through the `stopWhen` parameter.

- Start with the simplest approach that meets your needs. Add complexity only when required by:
  - Breaking down tasks into clear steps
  - Adding tools for specific capabilities
  - Implementing feedback loops for quality control
  - Introducing multiple agents for complex workflows

- 📌 Sequential Processing - Steps executed in order
- The simplest workflow pattern executes steps in a predefined order. 
  - Each step's output becomes input for the next step, creating a clear chain of operations. 
- This pattern is ideal for tasks with well-defined sequences, like content generation pipelines or data transformation processes.

- 📌 Parallel Processing - Independent tasks run simultaneously
- This pattern takes advantage of parallel execution to improve efficiency while maintaining the benefits of structured workflows.

- 📌 Evaluation/Feedback Loops - Results checked and improved iteratively
- This pattern introduces quality control into workflows by having dedicated evaluation steps that assess intermediate results. 
  - Based on the evaluation, the workflow can either proceed, retry with adjusted parameters, or take corrective action. 
  - This creates more robust workflows capable of self-improvement and error recovery.

- 📌 Orchestration - Coordinating multiple components
- In this pattern, a primary model (orchestrator) coordinates the execution of specialized workers. 
  - Each worker is optimized for a specific subtask, while the orchestrator maintains overall context and ensures coherent results. 
- This pattern excels at complex tasks requiring different types of expertise or processing.

- 📌 Routing - Directing work based on context
- This pattern allows the model to make decisions about which path to take through a workflow based on context and intermediate results. 
  - The model acts as an intelligent router, directing the flow of execution between different branches of your workflow. 
- This is particularly useful when handling varied inputs that require different processing approaches.

- 📌 Multi-Step Tool
  - If your use case involves solving problems where the solution path is poorly defined or too complex to map out as a workflow in advance, you may want to provide the LLM with a set of lower-level tools and allow it to break down the task into small pieces that it can solve on its own iteratively, without discrete instructions. 
  - To implement this kind of agentic pattern, you need to call an LLM in a loop until a task is complete. 
  - The AI SDK makes this simple with the `stopWhen` parameter.
  -  The SDK automatically triggers an additional request to the model after every tool result (each request is considered a "step"), continuing until the model does not generate a tool call or other stopping conditions (e.g. `stepCountIs`) you define are satisfied.

- Structured Answers
  - You can use an answer tool and the `toolChoice: 'required'` setting to force the LLM to answer with a structured output that matches the schema of the answer tool. 

- [AI SDK Core: Image Generation](https://ai-sdk.dev/docs/ai-sdk-core/image-generation)
  - The AI SDK provides the `generateImage` function to generate images based on a given prompt using an image model.
  - You can access the image data using the `base64` or `uint8Array` properties

- AI SDK UI provides robust abstractions that simplify the complex tasks of managing chat streams and UI updates on the frontend
- `useChat` offers real-time streaming of chat messages, abstracting state management for inputs, messages, loading, and errors, allowing for seamless integration into any UI design.
- `useCompletion` enables you to handle text completions in your applications, managing the prompt input and automatically updating the UI as new completions are streamed.
- `useObject` is a hook that allows you to consume streamed JSON objects, providing a simple way to handle and display structured data in your application.

- The `useChat` message format is different from the `ModelMessage` format. 
  - The `useChat` message format is designed for frontend display, and contains additional fields such as `id` and `createdAt`. 
  - We recommend storing the messages in the `useChat` message format.

- In addition to a chat ID, each message has an ID. 
- By default, message IDs are generated client-side:
  - User message IDs are generated by the `useChat` hook on the client
  - AI response message IDs are generated by `streamText` on the server

- For applications without persistence, client-side ID generation works perfectly. 
  - However, for persistence, you need server-side generated IDs to ensure consistency across sessions and prevent ID conflicts when messages are stored and retrieved.

- 💡 [AI SDK UI: Transport](https://ai-sdk.dev/docs/ai-sdk-ui/transport)
  - The useChat transport system provides fine-grained control over how messages are sent to your API endpoints and how responses are processed. 
  - This is particularly useful for alternative communication protocols like WebSockets, custom authentication patterns, or specialized backend integrations.
  - By default,  `useChat` uses HTTP `POST` requests to send messages to `/api/chat`; 

- ⚖️ The stream protocol defines how the data is streamed to the frontend on top of the HTTP protocol.
  - You can use this information to develop custom backends and frontends for your use case, e.g., to provide compatible API endpoints that are implemented in a different language such as Python.

- A text stream contains chunks in plain text, that are streamed to the frontend. 
  - Each chunk is then appended together to form a full text response.
- Text streams only support basic text data. If you need to stream other types of data such as tool calls, use data streams.

- A data stream follows a special protocol that the AI SDK provides to send information to the frontend.
  - The data stream protocol uses Server-Sent Events (SSE) format for improved standardization, keep-alive through ping, reconnect capabilities, and better cache handling.

- Message Start Part: Indicates the beginning of a new message with metadata.
- Text content is streamed using a start/delta/end pattern with unique IDs for each text block.
  - Text Delta Part: Contains incremental text content for the text block.
- Reasoning content is streamed using a start/delta/end pattern with unique IDs for each reasoning block.
- Source parts provide references to external content sources.
- Tool Input Delta Part: Incremental chunks of tool input as it's being generated.

- Prompts are the starting points for LLMs. They are the inputs that trigger the model to generate text. 
  - The scope of prompt engineering involves not just crafting these prompts but also understanding related concepts such as hidden prompts, tokens, token limits, and the potential for prompt hacking, which includes phenomena like jailbreaks and leaks.
- Prompt engineering includes the use of techniques like semantic search, command grammars, and the ReActive model architecture.
- To assist with comparing and tweaking LLMs, we've built an AI playground that allows you to compare the performance of different models side-by-side online.

- The different parts of the AI SDK support cancelling streams in different ways.

- With the lazy approach, this is taken care of for you. Because the stream will only request new data from AIBot when the consumer requests it, navigating away from the page naturally frees all resources. 

- 
- 
- 
- 
- 
- 

# more
