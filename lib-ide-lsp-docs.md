---
title: lib-ide-lsp-docs
tags: [docs, lsp]
created: 2025-01-05T15:00:14.398Z
modified: 2025-01-05T15:00:20.963Z
---

# lib-ide-lsp-docs

# guide

# overview

# docs

## ⚖️ [Language Server Protocol](https://microsoft.github.io/language-server-protocol/)

### [LSP(Language Server Protocol)](https://microsoft.github.io/language-server-protocol/overviews/lsp/overview/)

- The Language Server Protocol (LSP) defines the protocol used between an editor or IDE and a language server that provides language features like auto complete, go to definition, find all references etc. 
- A Language Server is meant to provide the language-specific smarts inside a server that can communicate with development tooling over a protocol that enables inter-process communication.
- The idea behind the Language Server Protocol (LSP) is to standardize the protocol for how such servers and development tools communicate. 
  - This way, a single Language Server can be re-used in multiple development tools, which in turn can support multiple languages with minimal effort.
- The protocol defines the format of the messages sent using JSON-RPC between the development tool and the language server. 
- LSIF defines a graph format to store information about programming artifacts.

- A language server runs as a separate process and development tools communicate with the server using the language protocol over JSON-RPC.
- When a user is working with different languages, a development tool usually starts a language server for each programming language. 
- Not every language server can support all features defined by the protocol. LSP therefore provides ‘capabilities’. A capability groups a set of language features.
  - A development tool and the language server announce their supported features using capabilities. 

- 
- 
- 
- 
- 
- 

### [LSIF(Language Server Index Format)](https://microsoft.github.io/language-server-protocol/overviews/lsif/overview/)

- The goal of the Language Server Index Format (LSIF) is to support rich code navigation in development tools or a Web UI without needing a local copy of the source code.
  - The format is similar in spirit to the Language Server Protocol (LSP), which simplifies the integration of rich code editing capabilities into a development tool.

- 🤔 Why not simply use an existing LSP language server? 
  - The LSP provides rich code authoring features like auto complete, format on type, and rich code navigation. 
  - To provide these features efficiently, a language server requires all source code files be available on a local disk. LSP language servers may also read parts or all of the files into memory and compute abstract syntax trees to power these features. 
  - The goal of the Language Server Index Format is to augment the LSP protocol to support rich code navigation features without these requirements. 
  - The LSIF defines a standard format for language servers or other programming tools to emit their knowledge about a code workspace. This persisted information can later be used to answer LSP requests for the same workspace without running a language server.

- LSIF builds on LSP and it uses the same data types as defined in LSP. 
  - At a high level, LSIF models the data returned from language server requests. 
  - Same as LSP, LSIF doesn’t contain any program symbol information nor does the LSIF define any symbol semantics (for example, what makes the definition of a symbol or whether a method overrides another method). 
  - The LSIF therefore doesn’t define a symbol database, which is consistent with the LSP approach.

- Using the existing LSP data types as the base for LSIF has another advantage as LSIF can easily be integrated into tools or servers which already understand LSP.

- A client tool would retrieve the hover content from a language server by sending a `textDocument/hover` request for document file:///Users/username/sample.ts at position `{line: 0, character: 10}`.
  - LSIF defines a format that language servers or standalone tools emit to describe that the tuple `['textDocument/hover', 'file:///Users/username/sample.ts', {line: 0, character: 10}]` resolves to the above hover. The data can then be taken and persisted into a database.

- 🆚 LSP requests are position based, however results often only vary for ranges and not for single positions.
  - To make the emitted data more compact, the LSIF uses ranges instead of positions. 
- LSIF uses graphs to emit this information. In the graph, an LSP request is represented using an edge. Documents, ranges, or request results (for example, the hover) are represented using vertices.

- The current version of the LSIF specification also supports document symbols, document links, Go to Definition, Go to Declaration, Go to Type Definition, Find All References, and Go to Implementation.

- 
- 
- 

## 🔡 LSP events

- textDocument/didOpen
  - The tool notifies the language server that a document is open 
  - From now on, the truth about the contents of the document is no longer on the file system but kept by the tool in memory. 
  - The contents now has to be synchronized between the tool and the language server.

- textDocument/didChange
  - The tool notifies the server about the document change and the language representation of the document is updated by the language server. 
  - As this happens, the language server analyses this information and notifies the tool with the detected errors and warnings (‘textDocument/publishDiagnostics’).

- textDocument/definition
  - The server responds with the document URI and the position of the symbol’s definition inside the document.

- textDocument/didClose
  - notification is sent from the tool informing the language server that the document is now no longer in memory. 
  - The current contents are now up to date on the file system.

- textDocument/codeAction
  - These commands are typically code fixes to either fix problems or to beautify/refactor code
  - To ensure that a server is useful in many clients, the commands specified in a code actions should be handled by the server and not by the client 

- This example illustrates how the protocol communicates with the language server at the level of document references (URIs) and document positions. 
  - The fact that the data types are simple and programming language neutral simplifies the protocol significantly. 
  - It is much simpler to standardize a text document URI or a cursor position compared with standardizing an abstract syntax tree and compiler symbols across different programming languages.

- When a user is working with different languages, a development tool usually starts a language server for each programming language. 

- 
- 
- 

## ⚖️ Language Server Protocol Spec

- The language server protocol defines a set of JSON-RPC request, response and notification messages which are exchanged using the above base protocol. 
  - Please also note that a response return value of null indicates no result. It doesn’t tell the client to resend the request.

- In general, the language server protocol supports JSON-RPC messages, however the base protocol defined here uses a convention such that the parameters passed to request/notification messages should be of `object` type (if passed at all). However, this does not disallow using `Array` parameter types in custom messages.

- 🔀 The protocol currently assumes that one server serves one tool. 
  - There is currently no support in the protocol to share one server between different tools. 
  - Such sharing would require additional protocol e.g. to lock a document to support concurrent editing.

- The set of capabilities is exchanged between the client and server during the `initialize` request.

- the server may decide to use a parallel execution strategy and may wish to return responses in a different order than the requests were received. The server may do so as long as this reordering doesn’t affect the correctness of the responses 
  - the server most likely should not reorder textDocument/definition and textDocument/rename requests, since executing the latter may affect the result of the former.

- Care should be taken to handle encoding in URIs. but clients and servers should be consistent with the form they use themselves to ensure the other party doesn’t interpret them as distinct URIs. 
  - Clients and servers should not assume that each other are encoding the same way (for example a client encoding colons in drive letters cannot assume server responses will have encoded colons). 

- The current protocol is tailored for textual documents whose content can be represented as a string. 
  - There is currently no support for binary documents. 
  - A position inside a document (see Position definition below) is expressed as a zero-based line and character offset.

- Prior to 3.17 the offsets were always based on a UTF-16 string representation. 
  - Since 3.17 clients and servers can agree on a different string encoding representation (e.g. UTF-8). 
  - The client announces it’s supported encoding via the client capability general.positionEncodings. 
  - To stay backwards compatible the only mandatory encoding is UTF-16 represented via the string utf-16
  - The server can pick one of the encodings offered by the client and signals that encoding back to the client via the initialize result’s property
  - If the string value utf-16 is missing from the client’s capability general.positionEncodings servers can safely assume that the client supports UTF-16.

- To ensure that both client and server split the string into the same line representation the protocol specifies the following end-of-line sequences: ‘\n’, ‘\r\n’ and ‘\r’.
  - Positions are line end character agnostic.

- Position in a text document expressed as zero-based line and zero-based character offset.
- A range in a text document expressed as (zero-based) start and end positions. 
  - A range is comparable to a selection in an editor. Therefore, the end position is exclusive

- A document filter denotes a document through properties like language, scheme or pattern. 
  - An example is a filter that applies to TypeScript files on disk. Another example is a filter that applies to JSON files with name package.json:

- New in version 3.16: Support for `AnnotatedTextEdit`.
  - range: Range; // The range of the text document to be manipulated
  - newText: string; // The range of the text document to be manipulated
- annotated text edit supports to add an annotation to a text edit. 

- Complex text manipulations are described with an array of TextEdit’s or AnnotatedTextEdit’s, representing a single change to the document.
  - Text edits ranges must never overlap, that means no part of the original document must be manipulated by more than one edit. 
  - However, it is possible that multiple edits have the same start position: multiple inserts
- AnnotatedTextEdit： The support is guarded by the client capability `workspace.workspaceEdit.changeAnnotationSupport`. 
  - If a client doesn’t signal the capability, servers shouldn’t send AnnotatedTextEdit literals back to the client.

## considerations

- Servers usually support different communication channels (e.g. stdio, pipes, …). To ease the usage of servers in different clients it is highly recommended that a server implementation supports the following command line arguments to pick the communication channel:
  - stdio: uses stdio as the communication channel.
  - pipe: use pipes (Windows) or socket files (Linux, Mac) as the communication channel. The pipe / socket file name is passed as the next arg or with --pipe=.
  - socket: uses a socket as the communication channel. The port is passed as next arg or with --port=.
  - node-ipc: use node IPC communication between the client and the server. This is only supported if both client and server run under node.

- 
- 
- 
- 
- 

# docs-acp(Agent Client Protocol) ⚖️
- resources
  - [Overview - Agent Client Protocol](https://agentclientprotocol.com/protocol/overview)

- The Agent Client Protocol standardizes communication between code editors/IDEs, and coding agents (programs that use generative AI to autonomously modify code).
- AI coding agents and editors are tightly coupled but interoperability isn’t the default. 
  - Integration overhead: Every new agent-editor combination requires custom work
  - Limited compatibility: Agents work with only a subset of available editors
  - Developer lock-in: Choosing an agent often means accepting their available interfaces

- ACP solves this by providing a standardized protocol for agent-editor communication, similar to how the Language Server Protocol (LSP) standardized language server integration.

- ACP assumes that the user is primarily in their editor, and wants to reach out and use agents to assist them with specific tasks.
  - Agents run as sub-processes of the code editor, and communicate using JSON-RPC over stdio. 
  - The protocol re-uses the JSON representations used in MCP where possible, but includes custom types for useful agentic coding UX elements, like displaying diffs.
  - The default format for user-readable text is Markdown, which allows enough flexibility to represent rich formatting without requiring that the code editor is capable of rendering HTML.

- When the user tries to connect to an agent, the editor boots the agent sub-process on demand, and all communication happens over stdin/stdout.
  - Each connection can support several concurrent sessions
  - one editor can connect to multiple agents
- ACP makes heavy use of JSON-RPC notifications to allow the agent to stream updates to the UI in real-time. 
  - It also uses JSON-RPC’s bidirectional requests to allow the agent to make requests of the code editor: for example to request permissions for a tool call.
- Commonly the code editor will have user-configured MCP servers. When forwarding the prompt from the user, it passes configuration for these to the agent. This allows the agent to connect directly to the MCP server.
- The code editor may itself also wish to export MCP based tools. Instead of trying to run MCP and ACP on the same socket, the code editor can provide its own MCP server as configuration. As agents may only support MCP over stdio, the code editor can provide a small proxy that tunnels requests back to itself

- The Agent Client Protocol allows Agents and Clients to communicate by exposing methods that each side can call and sending notifications to inform each other of events.

- The protocol follows the JSON-RPC 2.0 specification with two types of messages:
  - Methods: Request-response pairs that expect a result or error
  - Notifications: One-way messages that don’t expect a response

- A typical flow follows this pattern:
- Initialization Phase
  - Client → Agent: `initialize` to establish connection
  - Client → Agent: `authenticate` if required by the Agent
- Session Setup - either:
  - Client → Agent: `session/new` to create a new session
  - Client → Agent: `session/load` to resume an existing session if supported
- Prompt Turn
  - Client → Agent: `session/prompt` to send user message
  - Agent → Client: `session/update` notifications for progress updates
  - Agent → Client: File operations or permission requests as needed
  - Client → Agent: `session/cancel` to interrupt processing if needed
  - Turn ends and the Agent sends the `session/prompt` response with a stop reason

- Agents are programs that use generative AI to autonomously modify code. They typically run as subprocesses of the Client.
- Clients provide the interface between users and agents. 
  - They are typically code editors (IDEs, text editors) but can also be other UIs for interacting with agents. 
  - Clients manage the environment, handle user interactions, and control access to resources.

- The Agent Client Protocol provides built-in extension mechanisms that allow implementations to add custom functionality while maintaining compatibility with the core protocol. 
- All types in the protocol include a `_meta` field that implementations can use to attach custom information. 
  - This includes requests, responses, notifications, and even nested types like content blocks, tool calls, plan entries, and capability objects.

- Custom Requests
  - The protocol reserves any method name starting with an underscore (_) for custom extensions. 
  - In addition to the requests specified by the protocol, implementations MAY expose and call custom JSON-RPC requests as long as their name starts with an underscore (`_`).
- Custom Notifications
  - Custom notifications are regular JSON-RPC notifications that start with an underscore (_). Like all notifications, they omit the id field

- ACP uses JSON-RPC to encode messages. JSON-RPC messages MUST be UTF-8 encoded.

- The protocol currently defines the following transport mechanisms for agent-client communication:
  - stdio, communication over standard in and standard out
  - Streamable HTTP (draft proposal in progress)

- Agents and clients MAY implement additional custom transport mechanisms to suit their specific needs. The protocol is transport-agnostic and can be implemented over any communication channel that supports bidirectional message exchange.

- 
- 
- 
- 

# more
