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

- https://github.com/TypeFox/monaco-languageclient /MIT/202504/ts
  - monaco-languageclient to connect Monaco editor with language servers.
  - monaco-editor-wrapper for building monaco editor application driven by configuration.
  - monaco-languageclient-examples provides the examples which allows to use them externally.
  - monaco-editor-wrapper依赖monaco-languageclient
  - [Teaching the Language Server Protocol to Microsoft's Monaco Editor | TypeFox _201704](https://www.typefox.io/blog/teaching-the-language-server-protocol-to-microsofts-monaco-editor/)
  - [如何创建集成 LSP 支持多语言的 Web 代码编辑器 - 米开朗基杨 - 博客园 _202309](https://www.cnblogs.com/ryanyangcs/p/17693108.html)

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

- https://github.com/lspserver/proxy /apache2/202204/ts/inactive
  - the proxy of lspserver written in JavaScript
  - https://github.com/lspserver/proxy-go /go
    - the proxy of lspserver written in Go

- https://github.com/emacs-lsp/lsp-docker /GPL/202503/emacs
  - lsp-mode uses lsp-docker to run language servers using in containers
  - pylsp
  - lsp-mode starts the image passed as :docker-image-id and mounts :path-mappings in the container. 

## ts-server

- https://github.com/typescript-language-server/typescript-language-server /apache2/202409/ts
  - TypeScript & JavaScript Language Server
  - typescript-language-server --stdio
  - Language Server Protocol implementation for TypeScript wrapping `tsserver`.
  - The core logic for interacting with tsserver is nowadays mostly based on the code of the TypeScript Language Features VSCode bundled extension maintained in vscode.
  - 📡 NOT_PLANNED: [Support .eslintrc config _202303](https://github.com/typescript-language-server/typescript-language-server/issues/708)
    - This server has nothing to do with eslint. It doesn't integrate with it
    - There might exist typescript plugins that run eslint but it's out of scope of this server if Zed is using those. I would anyway recommend running a separate LSP server for eslint.
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

## python-server

- https://github.com/DetachHead/basedpyright /MIT/202504/python/ts
  - https://docs.basedpyright.com/
  - a fork of pyright with various type checking improvements, pylance features and more.
  - basedpyright-langserver --stdio
  - unlike pyright, the basedpyright CLI and language server are available as a pypi package.
  - once installed, the `basedpyright` and `basedpyright-langserver` scripts will be available in your python environment.

- https://github.com/replit/pyright-extended /MIT/202503/python/ts
  - pyright with yapf and ruff
  - a new Python meta-LSP that includes tools such as pyright, ruff, and yapf.

## go-server

## rust-server

## java-server

- https://github.com/chaitanya71998/monaco-language-testing-with-java /MIT/202308/ts/inactive
  - integrating monaco language client with java language server from eclipse
  - referenced from TypeFox/monaco-languageclient

- https://github.com/eclipse-jdtls/eclipse.jdt.ls /EPL/202504/java
  - The Eclipse JDT Language Server is a Java language specific implementation of the Language Server Protocol and can be used with any editor that supports the protocol
  - Eclipse JDT, which provides Java support (code completion, references, diagnostics...)
  - Supports compiling projects from Java 1.8 through 24
  - Maven pom.xml project support
  - Gradle project support (with experimental Android project import support)
  - Code actions (quick fixes, source actions & refactorings)
  - Code lens (references/implementations)
  - Annotation processing support (automatic for Maven projects)
  - Choose a value for `-data`: An absolute path to your data directory. eclipse.jdt.ls stores workspace specific information in it. This should be unique per workspace/project.
  - [Question, How to "GoToDefination" for JDK package? _202111](https://github.com/eclipse-jdtls/eclipse.jdt.ls/issues/1931)
    - Jumping to the definition of JDK libraries or other third-party libraries requires the `classFileContentsSupport extendedClientCapabilities` on the client. This is not part of the core protocol, but a custom extension of eclipse.jdt.ls
  - [Issue when trying to connect using Monaco Editor _202111](https://github.com/eclipse-jdtls/eclipse.jdt.ls/issues/1933)
  - ⛓️ [Unable to Start Eclipse JDT Language Server _202310](https://github.com/eclipse-jdtls/eclipse.jdt.ls/issues/2890)
    - java -Declipse.application=org.eclipse.jdt.ls.core.id1 -Dosgi.bundles.defaultStartLevel=4 -Declipse.product=org.eclipse.jdt.ls.core.product -Dlog.level=ALL -Dosgi.dev -Dsocket.stream.debug=true -DCLIENT_PORT=5036 -DCLIENT_HOST=127.0.0.1 -Xmx1G --add-modules=ALL-SYSTEM --add-opens java.base/java.util=ALL-UNNAMED -jar ./plugins/org.eclipse.equinox.launcher_1.6.500.v20230717-2134.jar -configuration ./config_linux -data /tmp/foospace/
  - [Support for ARM/aarch64 _202308](https://github.com/eclipse-jdtls/eclipse.jdt.ls/issues/2784)
  - [snippet and inmemory uri support _202501](https://github.com/eclipse-jdtls/eclipse.jdt.ls/discussions/3359)
    - Only `file://` URIs are supported. Looking through the JDT-LS codebase, I see places where we make assumptions regarding whether the file scheme is file (ie. file:/some/path/on/local/system). There's only a handful of these in the code base, but it would be good to examine them.
  - [Cannot run server on apple M2 silicon ](https://github.com/eclipse-jdtls/eclipse.jdt.ls/issues/2680)
    - Perhaps Eclipse is able to match against the cocoa.macosx.x86_64 platform-specific bundles. We definitely don't ship the aarch64 one. I did read that with Rosetta, it should be possible to run the x86_64 binaries so perhaps this is supported.
  - [Neovim LSP can't run LSP client: `Unrecognized option: --add-modules=ALL-SYSTEM` ](https://github.com/eclipse-jdtls/eclipse.jdt.ls/issues/2175)
    - java -Declipse.application=org.eclipse.jdt.ls.core.id1 -Dosgi.bundles.defaultStartLevel=4 -Declipse.product=org.eclipse.jdt.ls.core.product --add-modules=ALL-SYSTEM --add-
  - [Lombok with jdtls.py script _202206](https://github.com/eclipse-jdtls/eclipse.jdt.ls/issues/2113)
    - jdtls --jvm-arg=-javaagent:/path/to/lombok.jar --jvm-arg=-Xbootclasspath/a:/path/to/lombok.jar -data "$HOME/dev/eclipse/workspace"
  - [Getting - {"jsonrpc":"2.0", "method":"window/logMessage", "params":{"type":3, "message":"12-Jan-2024, 12:00:51 am Main thread is waiting"}} on insallation ](https://github.com/eclipse-jdtls/eclipse.jdt.ls/issues/3021)
  - [Put this bash script into the appropriate location ](https://github.com/eclipse-jdtls/eclipse.jdt.ls/issues/1823)
  - https://github.com/eruizc-dev/jdtls-launcher /deprecated
    - It included awesome features like updates, and backups, and Lombok configuration.
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
