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
# more
