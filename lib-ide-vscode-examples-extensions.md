---
title: lib-ide-vscode-examples-extensions
tags: [examples, extensions, vscode]
created: 2023-01-21T19:02:24.409Z
modified: 2024-08-24T16:17:26.715Z
---

# lib-ide-vscode-examples-extensions

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
- openvsx /1kStar/EPLv2/202312/java/ts/参考前端
  - https://github.com/eclipse/openvsx
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

- https://github.com/estruyf/vscode-front-matter /MIT/202312/ts
  - https://frontmatter.codes/
  - Front Matter is a CMS running straight in Visual Studio Code. 
  - Can be used with static site generators like Hugo, Jekyll, Hexo, NextJs, Gatsby, and many more
  - Preview your site/content straight in Visual Studio Code
# utils
- https://github.com/KermanX/reactive-vscode /MIT/202406/ts
  - https://kermanx.github.io/reactive-vscode/
  - Develop VSCode extension with Vue Reactivity API
  - This library wraps most of the VSCode APIs into Vue Composables.
  - built on top of `@vue/reactivity`, and ported some code from `@vue/runtime-core` .
  - This library is not designed for using Vue in a webview.

- https://github.com/sekassel-research/vscode-vnc-plugin /202212/ts/archived
  - This extension adds an embedded vnc viewer to the vs code server instance, which is used by fulib.org projects.
# vscode-web
- https://github.com/antfu/vscode-browse-lite /ts
  - Embedded browser in VS Code
# extensions

## ext-office/files

- https://github.com/cweijan/vscode-office /MIT/202412/js
  - 让VSCode支持预览PDF, Excel和Word等格式, 并增加markdown所见即所得编辑器
  - 支持预览xlsx, docx, svg, pdf, zip等格式, 后来才增加markdown编辑器
  - 依赖docxjs、sheetjs、vditor(md)、pdfjs
  - [Please support PPT/PPTX files _202211](https://github.com/cweijan/vscode-office/issues/166)
    - I have done research on this, but due to the complexity of ppt/pptx, it is impossible to display it in js.
  - https://github.com/orellabac/vscode-office /202010/js/inactive
    - Word: mammoth
    - Excel: sheetjs + x-spreadsheet
    - md: stackedit
    - PDF: pdf.js
    - PhotoShop: psd.js
    - xmind: xmind-viewer
    - Image: lightGallery

- https://github.com/janisdd/vscode-edit-csv /MIT/202310/ts
  - vs code extension to edit csv files with an excel like table ui
  - If you don't have vs code to hand, you can use the online version at https://edit-csv.net

- https://github.com/mikeebowen/ooxml-validator-vscode /MIT/202412/ts
  - A VS Code extension for validating Office Open XML files
  - The OOXML Validator validates Office Open XML files (.docx, .docm, .dotm, .dotx, .pptx, .pptm, .potm, .potx, .ppam, .ppsm, .ppsx, .xlsx, .xlsm, .xltm, .xltx, or .xlam) and displays the validation errors found in the xml parts in VSCode and creates an optional CSV or JSON log file of the validation errors.

## ext-git

- https://github.com/MichaelCurrin/auto-commit-msg /ts
  - A VS Code extension to generate a smart commit message based on file changes
  - With the explosion of AI tools, you can find alternatives to this extension which use AI - see AI tools

## ext-history

- https://github.com/microsoft/codetour /MIT/202303/ts/inactive
  - VS Code extension that allows you to record and play back guided tours of codebases, directly within the editor
  - A "code tour" is simply a series of interactive steps, each of which are associated with a specific directory, or file/line, and include a description of the respective code. 
  - Tours can either be checked into a repo, to enable sharing with other contributors, or exported to a "tour file", which allows anyone to replay the same tour, without having to clone any code to do it
  - Recording Tours: You can create directory steps, selection steps, or content steps in order to add an introductory or intermediate explanations to a tour.
  - Re-arranging steps
  - Versioning Tours: When you record a tour, you'll be asked which git "ref" to associate it with. 
  - Behind the scenes, the tour will be written as a JSON file to the `.tours` directory of the current workspace. 
    - This file is pretty simple and can be hand-edited if you'd like.
    - you can manually create tour files, by following the tour schema.
  - Maintaining Tours: In order to ensure that your tours stay up-to-date as your codebase evolves, you can install one of the following tasks as part of your CI pipeline, in order to detect "tour drift" in response to PRs/commits/etc.
  - [CodeTour: VS Code extension to record and play guided walkthroughs of codebases | Hacker News _202103](https://news.ycombinator.com/item?id=26488610)

## ext-data

- https://github.com/microsoft/vscode-data-wrangler /未开源
  - [Announcing Data Wrangler: Code-centric viewing and cleaning of tabular data in Visual Studio Code - Python](https://devblogs.microsoft.com/python/announcing-data-wrangler-code-centric-viewing-and-cleaning-of-tabular-data-in-visual-studio-code/)
  - Data Wrangler is a free extension that offers data viewing and cleaning that is directly integrated into VS Code and the Jupyter extension
# sync
- https://github.com/neilmovva/codemirror /202411/ts
  - VSCode extension to continuously sync the open workspace folder to a remote server.
# themes
- https://github.com/vscodethemes/web /202303/ts/inactive
  - https://vscodethemes.com/
  - Search and preview themes from the Visual Studio Marketplace.
  - built with Remix and Cloudflare Workers.
# ai
- https://github.com/unit-mesh/auto-dev-vscode /apache2/202405/ts
  - https://vscode.unitmesh.cc/
  - [AutoDev for VSCode 预览版：精准 AI 编程提示词与编辑器的完美融合 - 知乎](https://zhuanlan.zhihu.com/p/696080970)
  - 将 AutoDev for Intellij IDEA 平台的非凡开发者体验带到了 VSCode 平台。在 IDEA 版本中通过构建非常精准的提示词，以及与编辑器的完美融合， 以帮助开发者更好地编写代码。
  - 设计理念示例：一键精准测试生成
# more
