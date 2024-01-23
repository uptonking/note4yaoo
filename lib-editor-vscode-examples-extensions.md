---
title: lib-editor-vscode-examples-extensions
tags: [examples, extensions, vscode]
created: 2023-01-21T19:02:24.409Z
modified: 2023-01-21T19:02:58.833Z
---

# lib-editor-vscode-examples-extensions

# guide

- ext的实现
  - 参考编辑器插件扩展
  - 支持本地/私有/中立仓库，如openvsx

- scripts的实现
  - 参考react-live/mdx-live/script-lab/sandbox-play，每次将数据对象和解析后的代码传进去
  - 类似vscode像codepen的实时预览扩展
# vscode-ext
- [Extension Capabilities Overview](https://code.visualstudio.com/api/extension-capabilities/overview)
  - VSCode offers many ways for extensions to extend its capabilities. It can sometimes be hard to find the right Contribution Points and VS Code API to use. 
  - [Contribution Points](https://code.visualstudio.com/api/references/contribution-points)
  - [VS Code API](https://code.visualstudio.com/api/references/vscode-api)

- [💡 Web Extensions](https://code.visualstudio.com/api/extension-guides/web-extensions)
  - A web extension is structured like a regular extension. 
  - the main entry file is defined by the `browser` property. Extensions that have only a `main` entry point, but no `browser` are not web extensions.
  - Extensions can have both browser and main entry points in order to run in browser and in Node.js runtimes.

- [Custom Editor API](https://code.visualstudio.com/api/extension-guides/custom-editors)
  - There are two parts to a custom editor: the view that users interact with and the document model that your extension uses to interact with the underlying resource.
  - The view side of a custom editor is implemented using a **webview**
  - Webviews cannot access the VS Code API directly but they can talk with extensions by passing messages back and forth.
  - The other part of a custom editor is the **document model**.
  - A CustomTextEditorProvider uses VS Code's standard TextDocument as its document model and all changes to the file are expressed using VS Code's standard text editing APIs.
  - A CustomTextEditorProvider uses VS Code's standard TextDocument as its document model and all changes to the file are expressed using VS Code's standard text editing APIs, for example split-view
  - There are two classes of custom editors: custom text editors and custom editors. 
  - `CustomTextEditor` are considerably easier to implement because VS Code already knows how to work with text files 
  - you can use a `CustomEditor` for binary formats such as images, but it also means that your extension is responsible for a lot more, including implementing save and backing.
- [Your First Extension](https://code.visualstudio.com/api/get-started/your-first-extension)
# open-ext
- https://github.com/eclipse/openvsx /1kStar/EPLv2/202312/java/ts
  - https://open-vsx.org/
  - https://ecdtools.eclipse.org/adopters/
  - Open VSX is a vendor-neutral open-source alternative to the Visual Studio Marketplace.
  - It provides a server application that manages VS Code extensions in a database, a web application similar to the VS Code Marketplace, and a command-line tool for publishing extensions similar to vsce.
  - 前端依赖mui.v5、markdown-it、react-infinite-scroller
  - 后端依赖spring-boot、ehcache
  - 未实现依赖的依赖dependents
  - https://github.com/EclipseFdn/open-vsx.org
    - This repository contains the source of open-vsx.org, the public instance of Eclipse Open VSX. 
    - Most of the code is maintained in eclipse/openvsx, while here you'll find only adaptations specific to the public instance.

- [Using Open VSX in VS Code](https://github.com/eclipse/openvsx/wiki/Using-Open-VSX-in-VS-Code)

- [Help Us Sustain Open-vsx.org!](https://github.com/VSCodium/vscodium/discussions/1433)
  - It's due to the license of the Marketplace which limits its use to only MS product.
  - coder/code-marketplace could become an alternative but I don't see any publisher management...

- https://github.com/coder/code-marketplace /AGPLv3/202312/go
  - an open-source alternative to the VS Code Marketplace for use in editors like code-server or VSCodium.
  - It is maintained by Coder and is used by our enterprise customers 
  - This marketplace reads extensions from file storage and provides an API for editors to consume. It does not have a frontend or any mechanisms for extension authors to add or update extensions in the marketplace.

- https://github.com/nix-community/nix-vscode-extensions /MIT/202401/haskell/nix
  - Nix expressions for VSCode and OpenVSX extensions
  - At the time of writing this, nixpkgs contains 271 VS Code extensions. 
  - This is a small fraction of the more than 40, 000 extensions in the VS Code Marketplace
  - This flake provides Nix expressions for the majority of available extensions from Open VSX and VS Code Marketplace.
# popular
- https://github.com/bebo-dot-dev/jjs-vscode-toolbar
  - A VSCode toolbar and context menu extension
  - Modifies the VSCode toolbar and context menu to include a few useful commands
# utils

# vscode-browser

- https://github.com/antfu/vscode-browse-lite /ts
  - Embedded browser in VS Code
# extensions

## ext-office

- https://github.com/janisdd/vscode-edit-csv /MIT/202310/ts
  - vs code extension to edit csv files with an excel like table ui
  - If you don't have vs code to hand, you can use the online version at https://edit-csv.net

## ext-git

- https://github.com/MichaelCurrin/auto-commit-msg /ts
  - A VS Code extension to generate a smart commit message based on file changes
  - With the explosion of AI tools, you can find alternatives to this extension which use AI - see AI tools
# themes
- https://github.com/vscodethemes/web /202303/ts/inactive
  - https://vscodethemes.com/
  - Search and preview themes from the Visual Studio Marketplace.
  - built with Remix and Cloudflare Workers.
# more
