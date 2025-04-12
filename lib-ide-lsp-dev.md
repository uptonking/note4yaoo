---
title: lib-ide-lsp-dev
tags: [ide, lsp]
created: 2025-01-05T14:59:47.574Z
modified: 2025-01-05T15:00:07.466Z
---

# lib-ide-lsp-dev

# guide
- pros
  - 标准化的方式，支持多种ide如vscode/jetbrains, 启发技术发展如MCP/backlink

- cons
  - jsonrpc

- features
  - autocomplete
  - go to definition
  - Go to Implementation
  - find all references
  - format on type
  - rich code navigation

- language-servers list
  - [Language Servers](https://microsoft.github.io/language-server-protocol/implementors/servers/)
  - [Langserver.org by sourcegraph](https://langserver.org/)
# draft

# dev-xp
- 基于web worker实现LSP的缺点，对于更新types不友好
  - a language server requires all source code files be available on a local disk
  - The goal of the Language Server Index Format is to augment the LSP protocol to support rich code navigation features without these requirements. 
# examples-lsp

## lang-server

- https://github.com/remarkjs/remark-language-server /MIT/202407/js/inactive
  - A language server to lint and format markdown files with remark.
  - Use `vscode-remark` to use the remark language server with Visual Studio Code.

## utils-lsp

- https://github.com/TechHara/lsp_sniffer /202403/rust/inactive
  - This tool allows one to intercept communications from a language server protocol (LSP) client and server.
  - This simply creates a thin wrapper that relays all the stdio communications between the client and the server, while logging them to files.
  - Let's say we want to sniff LSP communications between VSCode and rust-analyzer extension.
  - Currently, this works only if the LSP server binary is a natively compiled executable, such as `rust-analyzer`. However, some language servers are distributed as non-native executable, such as `jar`. 
  - it only supports communications via stdio, but again, it should be trivial to extend and support other channels as well, such as TCP or WebSocket.
  - [Sniffing LSP traffic. _202403](https://medium.com/@techhara/sniffing-lsp-communications-54f27b539685)
# more
