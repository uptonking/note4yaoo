---
title: lib-ide-lsp-examples
tags: [examples, ide, lsp]
created: 2025-04-12T19:18:04.799Z
modified: 2025-04-12T19:18:28.788Z
---

# lib-ide-lsp-examples

# guide

# popular

# lsp-servers
- https://github.com/qualified/lsp-ws-proxy /MIT/202205/rust/inactive
  - WebSocket proxy for Language Servers.

- https://github.com/wylieconlon/jsonrpc-ws-proxy /201906/ts/inactive
  - Create a web socket interface for any number of language servers running in subprocesses
  - Each server is run as a subprocess which is connected to by sending the client to the URL / based on a configuration file defined locally. 
  - 依赖vscode-ws-jsonrpc、ws
  - 🍴 forks
  - https://github.com/Ferix9288/jsonrpc-ws-proxy /202105
    - add passable `host`. usecase is for dockerized container to use `0.0.0.0`.
  - https://github.com/mihirs16/jsonrpc-ws-proxy /202208
    - add Dockerfile, 逻辑未调整
  - https://github.com/devopzacademy/jsonrpc-ws-proxy /202310/js
    - DEFAULT_PORT = 3000

## ts-server

- https://github.com/typescript-language-server/typescript-language-server /apache2/202409/ts
  - TypeScript & JavaScript Language Server
  - Language Server Protocol implementation for TypeScript wrapping `tsserver`.
  - The core logic for interacting with tsserver is nowadays mostly based on the code of the TypeScript Language Features VSCode bundled extension maintained in vscode.
  - [How do I spin up a language server and then invoke it using a Code editor like codemirror?? _202309](https://github.com/typescript-language-server/typescript-language-server/discussions/760)
    - You can use `vscode-jsonrpc` to communicate with the language server in nodejs

- https://github.com/mkslanc/websockets-ls /MIT/202503/js
  - This script provides a WebSocket bridge to interface multiple Language Servers (e.g. `svelte-language-server, pylsp, gopls, clangd`, etc.) with clients via a single WebSocket connection. 
  - 🔀 It supports various language servers concurrently and handles language-specific file extensions and initialization parameters.
  - Utilizes `vscode-jsonrpc` for LSP message handling.
  - Support for IPC and stdio communication with language servers.
  - Automatic file URI translation between server and client paths.
  - Temporary file creation for `textDocument/didOpen` events.

- https://github.com/lukehaas/ws-ts-language-server /202503/js
  - cli, 依赖 vscode-ws-jsonrpc

- https://github.com/dlvhdr/typescript-lsp-poc /202210/ts/inactive
  - What’s bad with monaco’s TS webworker?
  - The webworker monaco uses is a limited Typescript language client. The language client can understand only the current file, and cannot analyze the entire project. 
    - For example, this means it cannot know where an implementation of a function is, if it’s in a different file.

- https://github.com/Aaaaash/multi-language-server /201805/ts
  - language-server for php, javascript, go and more...
  - 依赖vscode-ws-jsonrpc

- https://github.com/marc2332/lsp-codemirror /202008/ts
  - LSP integration for CodeMirror5
  - 依赖node-jsonrpc-lsp, (based on https://github.com/wylieconlon/jsonrpc-ws-proxy，而不是直接依赖vscode-jsonrpc)

- https://github.com/ImperiumMaximus/ts-lsp-client /MIT/202404/ts/inactive
  - This npm module allows to communicate to a Language Server via LSP 
  - The aim is to provide a standalone library with minimal dependencies in contrast to the official one implemented by MS which depends on VSCode node libraries.
  - The interface is heavily inspired by a Python library counterpart called `pylspclient`.

- https://github.com/savetheclocktower/pulsar-ide-typescript-alpha /MIT/202502/js
  - This package used to use Pulsar’s built-in version of Node to run typescript-language-server

- https://github.com/brettimus/ts-static-analysis-test /202409/ts
  - Work on this project has moved to https://github.com/fiberplane/fpx

- https://github.com/sgtest/sourcegraph-typescript /202003/ts/inactive
  - This is a backend for the Sourcegraph TypeScript extension, speaking the Language Server Protocol over WebSockets.
  - It supports editor features such as go-to-definition, hover, and find-references for TypeScript and JavaScript projects, including support for dependencies and cross-repository code intelligence.
  - Cross-repository Go-to-Definition
  - Cross-repository Find-References
- https://github.com/elastic/typescript-langserver /201906/ts/inactive
  - typescript-langserver

- https://github.com/SFX123456/AlpineLspServer /202405/ts/inactive
  - Alpine Lsp Server

## markdown-server

- https://github.com/remarkjs/remark-language-server /MIT/202407/js/inactive
  - A language server to lint and format markdown files with remark.
  - Use `vscode-remark` to use the remark language server with Visual Studio Code.
# lsp-apps
- https://github.com/kcaswick/language-server-diagram-tool /MIT/202411/ts/inactive
  - A tool to export diagrams of programs, read via language servers or LSIF (language server index format)

- https://github.com/labring/laf /apache2/202501/ts
  - laf 是开源的云开发平台，提供云函数、云数据库、云存储等开箱即用的应用资源。让开发者专注于业务开发，无需折腾服务器，快速释放创意。
# lsp-utils
- https://github.com/Artawower/smells-code-analyzer /MIT/202312/ts/inactive
  - CLI tool powered by LSP and `tree-sitter` for finding dead and smells code from your project
  - This package allows you to find code that is not used in the project. The search is performed by finding references with the help of LSP. The project is based on tree-sitter, LSP and ripgrep.escription

- https://github.com/TechHara/lsp_sniffer /202403/rust/inactive
  - This tool allows one to intercept communications from a language server protocol (LSP) client and server.
  - This simply creates a thin wrapper that relays all the stdio communications between the client and the server, while logging them to files.
  - Let's say we want to sniff LSP communications between VSCode and rust-analyzer extension.
  - Currently, this works only if the LSP server binary is a natively compiled executable, such as `rust-analyzer`. However, some language servers are distributed as non-native executable, such as `jar`. 
  - it only supports communications via stdio, but again, it should be trivial to extend and support other channels as well, such as TCP or WebSocket.
  - [Sniffing LSP traffic. _202403](https://medium.com/@techhara/sniffing-lsp-communications-54f27b539685)
# mcp-lsp
- https://github.com/oakenai/headless-editor-mcp /MIT/202412/ts
  - A robust, language-agnostic headless code editor that leverages the Language Server Protocol (LSP) for code intelligence and the Model Context Protocol (MCP) for AI-assisted code manipulation.
  - Session-based editing with state management
  - React component detection and manipulation

- https://github.com/Tritlo/lsp-mcp /MIT/202503/ts
  - An MCP server that lets you interact with LSP servers
  - This server acts as a bridge that allows LLMs to query LSP Hover and Completion providers.
  - This enables LLMs to utilize LSPs for more accurate code suggestions.
  - The LSP-MCP server supports language-specific extensions that enhance its capabilities for different programming languages. 
  - `get_info_on_location`: Get hover information at a specific location in a file
  - `lsp-hover://` resources for retrieving hover information at specific file locations
  - `lsp-completions://` resources for getting code completion suggestions at specific positions
  - For the demo server: GHC (8.10 or later), Cabal (3.0 or later)

- https://github.com/alexwohletz/language-server-mcp /202412/js
  - This is a TypeScript-based MCP server designed to enhance code editing experiences by providing features such as hover information, code completion, and diagnostics. 
  - Only tested with typescript, theoretically should support Python. Would love to add additional language servers or be more agnostic if possible.

- https://github.com/sammcj/mcp-package-docs /MIT/202504/ts
  - https://smcleod.net/
  - An MCP server that provides LLMs with efficient access to package documentation across multiple programming languages and language server protocol (LSP) capabilities.
  - Multi-Language Support
  - Language Server Protocol (LSP) Support
  - Advanced Search Features
# more
