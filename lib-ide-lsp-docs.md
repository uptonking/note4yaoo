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
- 
- 

# more
