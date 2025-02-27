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
- https://github.com/microsoft/vscode-livepreview /MIT/202312/ts/inactive
  - http://aka.ms/live-preview
  - Hosts a local server in your workspace for you to preview your webpages.
  - An extension that hosts a local server for you to preview your web projects on
  - The external browser preview also supports debugging via the built-in js-debug extension and attaching to the Edge Devtools Extension. 
  - https://github.com/auchenberg/vscode-browser-preview
    - This extension has been deprecated in favor of the Live Preview extension.

- https://github.com/urin/vscode-web-visual-editor /MIT/202412/ts
  - Visual Editing: Edit HTML elements visually within the WebView.
  - Real-Time Preview: See changes reflected instantly as you edit.
  - Drag elements to rearrange their position.
  - This extension is similar to microsoft/vscode-livepreview 

- https://github.com/bebo-dot-dev/jjs-vscode-toolbar
  - A VSCode toolbar and context menu extension
  - Modifies the VSCode toolbar and context menu to include a few useful commands

- https://github.com/estruyf/vscode-front-matter /MIT/202412/ts
  - https://frontmatter.codes/
  - Front Matter is a CMS running straight in Visual Studio Code. 
  - Can be used with static site generators like Hugo, Jekyll, Hexo, NextJs, Gatsby, and many more
  - Preview your site/content straight in Visual Studio Code
- https://github.com/dedfaf/Code2Ghost /MIT/js
  - VScode extension that can post local markdown to Ghost CMS
# utils
- https://github.com/Priyanshukeshri/extension-uninstaller-plugin /202308/ts
  - extension that allows you to view and uninstall installed extensions from within the editor. 
  - It provides a webview panel that displays a list of installed extensions along with their details.

- https://github.com/a-bentofreire/editortoix /202410/ts
  - EditorToIX are open-source text utilities available for multiple code editors in form of extension or plugins.
  - This is a stable project with utilities being available on brackets code editor since 2016, however, since more editors have been supported, there is still work in progress to support the same extensions and policies across all code editors. 

- https://github.com/KermanX/reactive-vscode /MIT/202406/ts
  - https://kermanx.github.io/reactive-vscode/
  - Develop VSCode extension with Vue Reactivity API
  - This library wraps most of the VSCode APIs into Vue Composables.
  - built on top of `@vue/reactivity`, and ported some code from `@vue/runtime-core` .
  - This library is not designed for using Vue in a webview.

- https://github.com/sekassel-research/vscode-vnc-plugin /202212/ts/archived
  - This extension adds an embedded vnc viewer to the vs code server instance, which is used by fulib.org projects.

- https://github.com/sap/vscode-logging /apache2/202401/ts/inactive
  - A Logging Library for VSCode Extension which supports the following features:
    - Source Location Tracking.
    - Logging to rolling file logs.
    - Logging to a VSCode outputChannel.
    - JSON structure log entries output.
- https://github.com/pustovitDmytro/winston-vscode
    - This package aims to help you use the winston logger in your VSCode application. It utilizes the `OutputChannel` API under the hood.

- https://github.com/microsoft/vscode-l10n /MIT/202411/ts
  - tooling for localizing Visual Studio Code extensions
  - This API, introduced in VS Code 1.73, is used for translating strings in your extension's code. It is a part of the main VS Code extension API 
- https://github.com/lokalise/i18n-ally /MIT/202405/ts/inactive
  - All in one i18n extension for VS Code

- https://github.com/reliverse/vscode-extension-framework /MIT/202502/ts
  - Next-gen framework for developing VSCode extensions.
  - It's like WXT, but for VSCode Extensions.
  - Supports both MV2 and MV3
  - Dev mode with HMR & fast reload
  - Frontend framework agnostic: works with Vue, React, Svelte, etc
  - Module system for reusing code between extensions
  - Download and bundle remote URL imports

- https://github.com/zardoy/vscode-framework /MIT/202111/ts/inactive
  - Framework for fast VSCode extensions prototyping

## utils-webview

- https://github.com/microsoft/vscode-webview-ui-toolkit /MIT/202403/ts/archived
  - A component library for building webview-based extensions in Visual Studio Code.
  - [GitHub Next | React Webview UI Toolkit for VS Code](https://githubnext.com/projects/react-webview-ui-toolkit/)
  - [Webview API | Visual Studio Code Extension API](https://code.visualstudio.com/api/extension-guides/webview)
  - 🗑️ [Sunsetting the Webview UI Toolkit _202407](https://github.com/microsoft/vscode-webview-ui-toolkit/issues/561)
    - at the beginning of May the FAST project announced a project re-alignment which includes the deprecation of several core packages. Notably, FAST Foundation (one of the defining pieces of technology we used to build the toolkit) was on this list.
    - the only meaningful path forward is a full top-to-bottom rewrite of the toolkit using FAST Element (a lower-level library from FAST for building web components) and unfortunately the resourcing to complete this work was not allocated.
  - https://github.com/microsoft/vscode-webview-ui-toolkit-samples

- https://github.com/liutaigang/vscode-webview-extension-example /MIT/202501/ts
  - Vscode 的 extension webview 开发示例，提供 Vue 和 React 实现，文档详细，举例丰富
  - https://github.com/liutaigang/vite-plugin-vscode-webview-hmr

- https://github.com/tomjs/vscode-extension-webview /MIT/202410/ts
  - 在 vscode 扩展开发使用 webview.html 时，支持 vue/react 的 HMR
  - You can implement HMR by adding an `<iframe>` tag to the content that returns html and setting the src to http://localhost:5173. The client sends a message to the parent webview through postMessage to implement the API of acquireVsCodeApi.

- https://github.com/vscode-elements/elements /MIT/202501/ts/lit
  - https://vscode-elements.github.io/guides/getting-started/
  - Web component library for developing Visual Studio Code extensions
  - The “webview API” enables extensions to build entirely customizable views within Visual Studio Code. While the VSCode API grants access to different UI elements, none of these UI widgets are functional in the “webview.” VSCode Elements addresses this by re-implementing these UI controls as web components (aka custom elements)
  - You may not need VSCode Elements If you prefer traditional HTML and CSS over JavaScript, or if you’d rather avoid adding a new dependency, consider checking out the VSCode Elements Lite project
  - https://github.com/vscode-elements/elements-lite
    - A partial, pure CSS implementation of VSCode Elements, including only components that don't require JavaScript.

- https://github.com/KermanX/reactive-vscode /MIT/202501/ts
  - https://kermanx.github.io/reactive-vscode/
  - Develop VSCode extension with Vue Reactivity API
  - Source code in the `./packages/reactivity` directory is ported from `@vue/runtime-core`.
  - Source code in the `./packages/mock` directory references the implementation of VSCode
  - Part of the docs website is ported from VueUse

- https://github.com/tomjs/vite-plugin-vscode /MIT/202412/ts
  - 用 vue/react 来开发 vscode extension webview ，支持 esm 和 cjs。
  - Support webview HMR
  - Support Multi-Page App
  - Supports vue and react and other frameworks supported by vite

- https://github.com/estruyf/vscrui /MIT/202410/ts/inactive
  - A React components library for building webview-based extensions with React in Visual Studio Code.
  - The library is based on the VS Code Webview UI Toolkit

- https://github.com/githubnext/vscode-react-webviews /MIT/202110/ts/inactive
  - A sample/starter template for developing VS Code extensions with webviews
  - if your application cannot be implemented using the builtins, then you must implement your UIs using webviews. Webviews in VS Code give you all of the power, but using them effectively can involve a lot of headache, and it's very easy to do things that ruin performance.

- https://github.com/hacker0limbo/vscode-webview-react-boilerplate /202206/ts/inactive
  - Boilerplate for developing VSCode Extension Webview with React
  - https://github.com/estruyf/vscode-react-webview-template
  - https://github.com/cs-magic-open/vscode-extension-template
  - https://github.com/LinLzis/vscode-extension-react-starter
- https://github.com/rebornix/vscode-webview-react /MIT/201902/ts/inactive
  - Create React App starter in VSCode Webview.
  - The webview API allows extensions to create customizable views within VSCode. Single Page Application frameworks are perfect fit for this use case. 
  - to make modern JavaScript frameworks/toolchains appeal to VSCode webview API's security best practices requires some knowledge of both the bundling framework you are using and how VSCode secures webview.

- https://github.com/stack-spot/vscode-async-webview /apache2/202407/ts
  - A utility for making it easier to implement web views within VSCode extensions
  - https://github.com/Tiagoperes/vscode-async-webview-sample

- https://github.com/jasongin/vscode-webview-dialog /202311/ts
  - Sample for using webviews for dialogs or forms in VS Code extensions

- https://github.com/DTeam-Top/vscode-page /apache2/202003/ts/inactive
  - A light-weight page micro framework for vscode webview.
  - abstract the communication between html page and WebviewPanel, developers can focus on business logic.
  - built-in template engine, with handlebars.js.

- https://github.com/jackiotyu/remote-webview-devtools /GPLv3/202407/ts/vue/inactive
  - 使用最新的 chrome devtools 调试移动端 webview

- https://github.com/Lirobi/phoneviewvscode /202412/ts
  - My VSCode extension to get a mobile webview on the side of the editor, with multiple devices avaliable
  - extension that allows you to preview your web application in a phone-sized viewport. 
  - Currently 1.6K downloads on the marketplace

- https://github.com/sandipchitale/vscode-webview-iframe /202304/ts
  - 过于简单

- https://github.com/sandipchitale/vscode-webview-iframe /202007/ts
  - Demonstrates VS Code's webview API 

- https://github.com/sandipchitale/vscode-devtools /202105/ts
  - Chrome Devtools inside VSCode using Webview+iframe

## utils-rpc/messaging

- https://github.com/SAP/vscode-webview-rpc-lib /apache2/202404/ts/inactive
  - Provides a convenient way to communicate between VSCode extension and its webviews. 
  - Use RPC calls to invoke functions on the webview, receive callbacks and vice versa.

- https://github.com/TypeFox/vscode-messenger /MIT/202412/ts
  - RPC messaging library for the VS Code extension platform
  - Makes the communication between your VS Code extension and its webviews much simpler.
  - Support for sync and async request/notification handlers
  - Support for request cancellation

- https://github.com/slightc/web-service-rpc /202311/ts
  - 使用vue/react写vscode插件webview的工具
  - 基于postMessage的RPC通信工具
  - https://github.com/Aaronphy/vscode-webview-rpc
  - https://github.com/huanghaoAlvin/vscode-message-management

- https://github.com/mkloubert/vscode-http-client /LGPL/201903/ts/inactive
  - Simple way to do HTTP requests in Visual Studio Code.
# extensions
- https://github.com/minherz/copyright-inserter /apache2/202501/ts
  - VSCode extension that inserts a copyright header into editing file

## ext-office/files

- https://github.com/cweijan/vscode-office /MIT/202501/js
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

- https://github.com/janisdd/vscode-edit-csv /MIT/202310/ts/inactive
  - vs code extension to edit csv files with an excel like table ui
  - If you don't have vs code to hand, you can use the online version at https://edit-csv.net
  - Note that the data flow is one way (editor to source file). If you make changes to the source file (.csv) while the editor is open, the editor will not be updated!
  - 依赖fork过的handsontable.v6

- https://github.com/sswatson/table-editor-vscode /202410/ts/inactive
  - This extension provides support for editing CSV files in a spreadsheet-like interface.

- https://github.com/RandomFractals/vscode-data-preview /562Star/apache2/202304/ts/inactive
  - Preview .json .arrow .avro .parquet .yml .csv/.tsv & .xlsx/.xlsb data files in a Data Grid w/Sorting & Filtering
  - Grid Data Summary display w/Aggregate Functions, Row & Column Pivots (a.k.a. Group By & Split By)
  - Pluggable Charting libraries for bult-in Charts: d3fc || highcharts
  - Data Preview is already capable of loading a few 10+MB's large data files with 100+K records & extensive list of supported Data Formats you'll be hard pressed to find on VSCode marketplace in one extension.
- https://github.com/RandomFractals/vscode-data-table /apache2/202310/ts/inactive
  - Data Table Renderers for VSCode Notebooks
  - These Data Table Renderers were created to enhance raw data views in Jupyter and custom VSCode Notebooks
  - See Data Preview vscode extension for a generic Grid Data Viewer with many common data formats support, search, sort, filters, grouping, splits, pivot tables, aggregates and basic charts 

- https://github.com/AdamRaichu/vscode-pdf-viewer /MIT/202402/js
  - A web extension which allows you to view PDF files directly in VS Code.

- https://github.com/yzane/vscode-markdown-pdf /202003/js/inactive
  - This extension converts Markdown files to pdf, html, png or jpeg files.

- https://github.com/yuenm18/ooxml-viewer-vscode /MIT/202412/ts
  - An OOXML Viewer for Visual Studio Code
  - When a document opened by the OOXML Viewer is edited from an external program, changed parts are marked with a yellow asterisk, deleted parts are marked with a red asterisk, and new parts are marked with a green asterisk.
- https://github.com/mikeebowen/ooxml-validator-vscode /MIT/202412/ts
  - A VS Code extension for validating Office Open XML files
  - The OOXML Validator validates Office Open XML files (.docx, .docm, .dotm, .dotx, .pptx, .pptm, .potm, .potx, .ppam, .ppsm, .ppsx, .xlsx, .xlsm, .xltm, .xltx, or .xlam) and displays the validation errors found in the xml parts in VSCode and creates an optional CSV or JSON log file of the validation errors.

- https://github.com/skfrost19/Docx-Viewer /MIT/202308/ts/inactive
  - VSCode extension to view docx / ODT files within the editor.

- https://github.com/hediet/vscode-drawio /GPLv3/202401/ts/inactive
  - This unofficial extension integrates Draw.io (also known as diagrams.net) into VS Code.

- https://github.com/DomMinnich/VS-Notes /202501/ts
  - VS-QuickNotes is a simple and intuitive note-taking extension for Visual Studio Code. 
  - It allows users to create, manage, and organize notes directly within the editor.
  - Notes are stored globally, so they can be accessed across all projects in your VS Code environment.
    - Notes are stored in the global storage location of VS Code, meaning they're specific to the VS Code environment and not synced across different machines automatically
  - No Multi-File Support: Currently, each note is created as an individual .txt or .md file.

## ext-editor

- https://github.com/patmood/rich-markdown-editor-vsc /202405/ts/inactive
  - Rich Markdown Editor extension for VSCode
  - This extension replaces the default code editor for markdown files with a rich version, allowing you to "edit" in preview mode.
  - It uses the `rich-markdown-editor` project generously open sourced by Outline

- https://github.com/Milkdown/vscode /MIT/202501/ts
  - vscode-ext: Edit markdown in a WYSIWYG way, powered by milkdown

- https://github.com/zaaack/vscode-markdown-editor /MIT/202501/ts
  - A vscode extension to make your vscode become a full-featured WYSIWYG markdown editor
  - Auto sync changes between the VSCode editor and webview
  - 依赖vditor3、jquery

- https://github.com/kurusugawa-computer/formula-editor-vscode /MIT/202412/ts
  - Formula Editor is a WYSIWYG editor that allows you to edit formulas in Markdown.

- https://github.com/microsoft/vscode-markdown-notebook /MIT/202111/ts/inactive
  - An extension for editing markdown files in VS Code notebooks
  - It shows text paragraphs in markdown cells, and code blocks in code cells.
  - It doesn't support executing code cells (but you could write an extension that adds that functionality!). 

- https://github.com/microsoft/vscode-hexeditor /MIT/202412/ts
  - A custom editor extension for Visual Studio Code which provides a hex editor for viewing and manipulating files in their raw hexadecimal representation.
  - Opening files as hex
  - Editing with undo, redo, copy, and paste support

- https://github.com/dineug/textflow /MIT/202501/ts
  - WYSIWYG Editor VSCode Extension
  - create an empty file with a .txf.json extension and open it in Visual Studio Code.
  - A rich-text editor based on Lexical.

- https://github.com/tomoyukim/vscode-mermaid-editor /MIT/202308/ts/inactive
  - Live editor and image creator for mermaid.js in Visual Studio Code

- https://github.com/henoc/svgeditor /MIT/201812/ts/inactive
  - VSCode extension for svg editor

- https://github.com/SumitNalavade/VS-Code-ReadMe-Editor /202306/ts/inactive
  - A VS Code extension to create, customize and save your Readme without having to leave your project workspace.
  - Built with TypeScript & React using the VS Code Webview API
  - https://github.com/ryanwelcher/vscode-readme-editor

- https://github.com/bpmn-io/vs-code-bpmn-io /MIT/202501/ts
  - View and edit BPMN diagrams in VSCode. Powered by bpmn.io tools.
  - Save changes to your local file
  - Contains parts (bpmn-js) released under the bpmn.io license.

- https://github.com/ChesterXXX/LatexHelper /MIT/202411/ts
  - A VSCode extension to enhance the LaTeX editing experience.
- https://github.com/kurusugawa-computer/formula-editor-vscode /MIT/202412/ts
  - Formula Editor is a WYSIWYG editor that allows you to edit formulas in Markdown.
  - When you're done editing, press the copy icon to copy the LaTeX string of the formula to the clipboard.

- https://github.com/JackieScorpio/convert-json-to-ts /MIT/202404/ts
  - use codemirror and vscode webview to achieve a vscode extension
  - Convert Json to Typescript

## ext-markdown

- https://github.com/Jekwwer/markdown-template /MTI/202501/js
  - A comprehensive template for working with Markdown files, equipped with tools for formatting, linting, spell checking, link validation, and more. 
  - Ideal for documentation projects, blogs, or any Markdown-heavy projects.

- https://github.com/yzhang-gh/vscode-markdown /MIT/202406/ts/inactive
  - Markdown All in One
  - All you need for Markdown (keyboard shortcuts, table of contents, auto preview and more).
  - https://github.com/qjebbs/vscode-markdown-extended
    - an extension extends syntaxes and abilities to VSCode built-in markdown function.
    - Markdown Extended includes lots of editing helpers and a what you see is what you get exporter

- https://github.com/shd101wyy/vscode-markdown-preview-enhanced /NCSA/202403/ts/inactive
  - https://shd101wyy.github.io/markdown-preview-enhanced
  - Markdown Preview Enhanced is an extension that provides you with many useful functionalities such as automatic scroll sync, math typesetting, mermaid, PlantUML, pandoc, PDF export, code chunk, presentation writer, etc. 
  - A lot of its ideas are inspired by Markdown Preview Plus and RStudio Markdown.
  - https://github.com/atom-community/markdown-preview-plus /202205/ts/archived
- https://github.com/domdomegg/markdown-inline-preview-vscode /MIT/202404/ts/inactive
  - extension for improving the display of markdown directly in the editor

- https://github.com/searKing/preview-vscode /MIT/202412/ts
  - A Previewer of Markdown and HTML for Visual Studio Code
- https://github.com/abechanta/vscode-ext-paged-media /MIT/202310/js/inactive
  - vscode extension for writing books using markdown and css paged media.
  - markdown-it: this is a default markdown engine in vscode which renders md file to html.
  - Paged.js: this is a css-based paged-media engine proposed by W3C which renders chunked html pages from one big continuous html.

- https://github.com/takumisoft68/vscode-markdown-table /apache2/202501/ts
  - A vscode extension to add markdown table features.
  - https://github.com/darkriszty/MarkdownTablePrettify-VSCodeExt /202110/ts/inactive
  - https://github.com/fcrespo82/vscode-markdown-table-formatter
  - https://github.com/TomasHubelbauer/vscode-markdown-table-format
  - https://github.com/philipparndt/vscode-markdown-tables
- https://github.com/rpeshkov/vscode-text-tables /MIT/202005/ts/inactive
  - VSCode extension that brings the power of Emacs table editing
  - Support for org and markdown tables
- https://github.com/simonguo/vscode-markdown-table-sort /202402/ts
  - extension to sort markdown tables

- https://github.com/csholmq/vscode-excel-to-markdown-table /MIT/202108/ts/inactive
  - VSCode extension to paste Excel copies to markdown table format

- https://github.com/remarkjs/vscode-remark /MIT/202404/js/inactive
  - Lint and format markdown code with remark

- https://github.com/microsoft/vscode-markdown-languageservice /MIT/202410/ts
  - The language service that powers VS Code's Markdown support, extracted so that it can be reused by other editors and tools
  - This library targets CommonMark. Support for other Markdown dialects and extensions is not within the scope of this project.
  - https://github.com/microsoft/vscode-markdown-languageserver
- https://github.com/so1ve/vscode-language-support-in-markdown /MIT/202402/ts/inactive
  - VSCode extension to provide language support in markdown files.

- https://github.com/DavidAnson/vscode-markdownlint /MIT/202501/js
  - Markdown/CommonMark linting and style checking for Visual Studio Code
  - It is powered by the markdownlint library for Node.js (which was inspired by markdownlint for Ruby). 
  - Linting is performed by the `markdownlint-cli2` engine

- memo /843Star/MIT/202303/ts/vscode/inactive
  - https://github.com/svsool/memo
  - Markdown knowledge base with bidirectional [[link]]s built on top of VSCode
  - Inspired by Obsidian.md and RoamResearch.

- https://github.com/Clikengo/markdown-print-tools /MIT/201904/ts/inactive
  - Tools to nicely print markdown document (vscode extension, markdown it extension, pdf generation)

- foam /15.6kStar/MIT/202411/ts/inactive
  - https://github.com/foambubble/foam
  - https://foambubble.github.io/
  - personal knowledge management and sharing system inspired by Roam Research, built on Visual Studio Code and GitHub.
  - Foam supports link aliasing, so you can have a `[[wikilink]]`, or a `[[wikilink|alias]]`.
  - See how your notes are connected via a graph with the Foam: Show Graph command
  - Foam updates the links to renamed files, so your notes stay consistent.

- dendron /6.8kStar/AGPLv3 > apache2/202404/ts/inactive
  - https://github.com/dendronhq/dendron
  - https://wiki.dendron.so/
  - local-first, markdown-based, note-taking tool built on top of VSCode. 
  - Dendron builds on top of the past five decades of programming languages and developer tooling. We apply the key lessons from software to the management of general knowledge. We make managing general knowledge like managing code and your PKM like an IDE.
  - Dendron finds the usable center between the two extremes by supporting backlinks of any two arbitrary notes while also maintaining a canonical hierarchy for every note. 
  - We do this through our hierarchal first approach to note taking that relies on the combination of hierarchies, schemas, and path based lookups.

- yn /3.6kStar/AGPLv3/202501/ts/vue/网页版+桌面版
  - https://github.com/purocean/yn
  - https://yank-note.vercel.app/
  - 一款面向程序员的Markdown笔记应用
  - 使用 vscode-Monaco 内核，专为 Markdown 优化
  - 支持历史版本回溯；可在文档中嵌入小工具、可运行的代码块、表格、PlantUML图形、Drawio图形、宏替换等；支持接入 OpenAI 自动补全。
  - 兼容性强：数据保存为本地Markdown文件；拓展功能尽量用 Markdown 原有的语法实现。
  - 支持用户编写自己的插件来拓展编辑器的功能。
  - 加密文件的加密解密操作均在前端完成，请务必牢记自己的密码。一旦密码丢失，只能暴力破解了。

- https://github.com/kortina/vscode-markdown-notes /GPLv3/202407/ts/inactive
  - Use [[wiki-links]], backlinks, #tags and @bibtex-citations for fast-navigation of markdown notes.
  - Bring some of the awesome features from apps like Notational Velocity, nvalt, Bear, FSNotes, Obsidian to VS Code, where you also have (1) Vim key bindings and (2) excellent extensibility.
- https://github.com/binyamin/vscode-backlinks-panel /MIT/202012/ts
  - View all markdown documents linking to current document.
  - this extension depends on the wikilink extension by kortina

- https://github.com/imlinhanchao/vsc-markdown-image /MIT/202411/ts
  - An extension for conveniently inserting pictures in Markdown, which supports storing pictures in local or third-party CDN service.
  - Configurable to support Imgur, Qiniu, SM. MS, Cloudflare, Cloudinary, S3, Azure Storage and other CDN service. The default is `local`, you need to open the folder where the Markdown file is located.
  - https://github.com/telesoho/vscode-markdown-paste-image

- https://github.com/3choff/docs-miner /MIT/202501/ts
  - A VSCode extension that generates markdown documentation from web pages and GitHub repositories.
  - Two scraping methods: API Method (Faster but may fail on some sites), Browser Method (Slower but more reliable)
- https://github.com/jsartelle/vscode-web-clipper /MIT/202004/ts/inactive
  - Clip web pages into Markdown in VSCode
  - The extension uses the Mercury parser to extract the main content from a page. The HTML to Markdown conversion is handled by `Turndown`.

- https://github.com/fabiospampinato/vscode-markdown-todo /MIT/202412/ts
  - Manage todo lists inside markdown files with ease.
  - Triggers `Markdown Todo: Toggle Todo/Done`.
  - https://github.com/TomasHubelbauer/vscode-markdown-todo

- https://github.com/houkanshan/vscode-markdown-footnote /MIT/202106/ts/inactive
  - [^1] footnote syntax support to VS Code's Markdown editor and preview.
- https://github.com/mjbvz/vscode-markdown-footnotes /MIT/202211/js/inactive
  - Adds [^1] footnote syntax support to VS Code's built-in Markdown preview

- https://github.com/estruyf/screendown /MIT/202401/ts/inactive
  - Capture stunning screenshots of your Markdown or code directly in Visual Studio Code with ease

- https://github.com/JeepShen/vscode-markdown-code-runner /MIT/202006/js/inactive
  - Run code snippet in markdown language for multiple languages: bash, python, golang, php
  - https://github.com/renathossain/vscode-markdown-runner

- https://github.com/HansKre/markdown-execute /MIT/202408/ts
  - VSCode Extension to execute commands directly from Markdown

- https://github.com/stateful/runmejs
  - A JavaScript module to use Runme in Node.js.

- https://github.com/rlnt/vscode-keepachangelog /LGPL/202306/ts/inactive
  - A VSCode extension that provides snippets for markdown files to create a changelog with the ruleset of Keep a Changelog.

- https://github.com/mjbvz/vscode-markdown-emoji /MIT/202412/ts
  - VS Code extension that adds support for :emoji: syntax to the built-in markdown preview

## ext-git

- https://github.com/lostintangent/gitdoc /MIT/202412/ts
  - VS Code extension that allows you to edit a Git repo, like it's a multi-file, versioned document.
  - GitDoc is a Visual Studio Code extension that allows you to automatically commit/push/pull changes on save
  - Additionally, just because you're auto-commmiting your changes, doesn't mean you lose control over your version history. When needed, you can easily restore, undo, and/or squash versions, without needing to memorize the magic of git

- https://github.com/Silic0nS0ldier/vscode-git-monolithic-extension /MIT/202412/ts
  - Fork of the built-in VSCode Git extension which includes optimisations for monolithic repositories.
  - A fork of VSCode's integrated Git support (from 2021-09-08) designed to work better with large repositories that Git is slow to work with.
  - Timeline view is not supported as the API surface is experimental.

- https://github.com/mhutchie/vscode-git-graph /NonCommercial/202109/ts/inactive
  - https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph
  - View a Git Graph of your repository in Visual Studio Code, and easily perform Git actions from the graph.
  - Compare any two commits by clicking on a commit, and then CTRL/CMD clicking on another commit
  - 可比较任意2个commit(包含当前未提交的最新的)的文件差异，点击一个commitId1作为start，按住ctrl/cmd点击另一个commitId2就是显示diff，注意比较内容包含commitId1而不包含commitId2，想要包含commitId2需要点击commitId2的下/上一个commit
- https://github.com/phil294/GitLG /MIT/202412/js/vue
  - A free, interactive Git UI for VSCode

- https://github.com/gitkraken/vscode-gitlens /MIT+Plus/202501/ts
  - http://gitkraken.com/gitlens
  - Supercharge Git inside VS Code and unlock untapped knowledge within each repository

- https://github.com/MichaelCurrin/auto-commit-msg /ts
  - A VS Code extension to generate a smart commit message based on file changes
  - With the explosion of AI tools, you can find alternatives to this extension which use AI - see AI tools

- https://github.com/caponetto/vscode-diff-viewer /MIT/202311/ts/inactive
  - A simple VS Code extension to easily visualize git diff files.
  - A simple wrapper for `diff2html` library to easily visualize git diff files in the VS Code.
  - Note: The file extension must be `.diff` or `.patch` to be properly loaded by VS Code.

- https://github.com/fabiospampinato/vscode-git-history /MIT/202403/ts
  - View or diff against previous versions of the current file.

- https://github.com/zawys/vscode-as-git-mergetool /AGPL/202111/ts/inactive
  - VS Code extension providing diff editor layouts & more for 3-way merging

- https://github.com/sapegin/vscode-just-blame /MIT/202501/ts
  - VS Code extension to show Git Blame annotations, inspired by JetBrains editors
  - Heatmap like in JetBrains editors.
  - Doesn’t use any resources until you turn on the annotations.

- https://github.com/carlthome/vscode-git-line-blame /AGPL/202407/ts/inactive
  - When you select a line in the text editor, the commit summary, author, and time elapsed since that commit edited that line will appear next to the line number in a discrete and unobtrusive color.

- https://github.com/dzhavat/git-cheatsheet-inside-vs-code /MIT/202501/ts
  - VS Code extension that lets you open a Git cheatsheet directly in the editor.

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

## ext-coding

- https://github.com/lostintangent/codeswing /MIT/202409/ts
  - https://aka.ms/codeswing
  - VS Code extension for building web applications ("swings") using a interactive and editor-integrated coding environment
  - CodeSwing comes with support for all major web languages: js/ts/css/scss/less/html/markdown/pug
  - CodeSwing also allows you to create component-based swings, using either React, React Native, Vue (single-file components) or Svelte
  - If you need to add any external JavaScript libraries (e.g. react) or stylesheets (e.g. font-awesome) to your swing, simply click the Add swing Library command 

- https://github.com/mh-mobile/vscode-inline-repl /MIT/202412/ts
  - Inline REPL extensions for VS Code 
  - Execute Ruby/Rust code and see results directly in your editor using Jupyter kernels.
  - The project is inspired by Zed Editor's REPL functionality, bringing a similar seamless code evaluation experience to VS Code.

- https://github.com/wmanth/vscode-jar-viewer /MIT/202211/ts/inactive
  - JAR Viewer Extension for VS Code
  - Extension for VS Code that gives a quick peek inside a JAR file by listing all classes and files bundled inside the archive.

## ext-js/ts

## ext-data/format

- https://github.com/AdamRaichu/vscode-zip-viewer /MIT/202412/js
  - An extension which allows for the manipulation of zip files in VS Code.
  - If you found this extension useful, you may also want to check out PDF Viewer, Font Preview, or Docx Renderer.

- https://github.com/dineug/erd-editor /MIT/202501/ts
  - https://erd-editor.io/
  - Entity-Relationship Diagram Editor
  - Local-first support (autosaves to the browser).
  - https://github.com/dineug/vuerd-vscode

- https://github.com/microsoft/vscode-data-wrangler /未开源
  - [Announcing Data Wrangler: Code-centric viewing and cleaning of tabular data in Visual Studio Code - Python](https://devblogs.microsoft.com/python/announcing-data-wrangler-code-centric-viewing-and-cleaning-of-tabular-data-in-visual-studio-code/)
  - Data Wrangler is a free extension that offers data viewing and cleaning that is directly integrated into VS Code and the Jupyter extension

- https://github.com/slaugaus/visual-json-editor-vscode /MIT/202412/ts
  - WYSIWYG JSON viewer/editor for VS Code that looks like its settings page
  - Open JSON files in a GUI that looks (kind of) like the VS Code settings page! Includes type changing, item rearrangement, undo/redo, and assistance with colors, dates, and times.
- https://github.com/sunmorgus/vscode-json-editor /201806/ts/inactive
  - A vscode extension to preview and edit JSON documents in a simple tree view

- https://github.com/liriliri/vscode-settings-editor /MIT/202307/ts/inactive
  - VS Code visual editor for settings like prettierrc, tsconfig etc.

- https://github.com/Saber2pr/vsc-ext-todolist /202404/ts
  - TodoList TreeView Editor for Vscode Extension.
  - Create and edit *.todo file

- https://github.com/ai-primitives/vscode-mdxld /MIT/202412/ts
  - VS Code extension for MDX-LD providing integrated support for Structured Data (YAML), Unstructured Content (markdown), Executable Code (JS/TS), and UI Components (JSX/React) with schema.org, gs1.org, and mdx.org.ai enrichment.

## ext-db/sqlite

- https://github.com/qwtel/sqlite-viewer-vscode  /202501/ts
  - https://sqliteviewer.app/
  - easy SQLite viewer for VSCode, inspired by DB Browser for SQLite and Airtable.
  - [Next version of SQLite Viewer, handling 3 million rows, 1 GB sqlite file, in a browser.](https://twitter.com/qwtel/status/1639204056622321664)
    - Memory usage low despite 1GB file, thanks to OPFS and SQLite WASM
  - [Opening large SQLite files is solved in the (unreleased) web version though.](https://twitter.com/qwtel/status/1644319722178248708)
    - The limit is now how much the browser permits to write into the Origin Private File System.
  - I'm surprised the current version of SQLite Viewer keeps getting good reviews in the vsc marketplace. It flat out crashes if you open a large file. I suppose most sqlite files are small.
    - Unfortunately fixing it would be hard. 
    - vsc's own `fs` module doesn't let you read with random offsets, and even if it did, it would require writing a custom VFS and juggling buffers across 2-3 layers of iframes and workers.
  - https://alpha.sqliteviewer.app/
    - https://twitter.com/qwtel/status/1649018168839372803
    - Can handle much larger SQLite files (tested up to 1.5GB), only limited by storage quota of your browser
    - Fixed virutal scrolling and resizing for very large tables

- https://github.com/Gruntfuggly/gerrit-view /202001/js/inactive
  - A vscode extension for viewing Gerrit's dashboard
  - This extension provides a view of your Gerrit server.
  - By default, the view is automatically refreshed every minute.

## ext-image

- https://github.com/hemengke1997/vscode-image-manager /MIT/202501/ts
  - https://hemengke1997.github.io/vscode-image-manager/
  - Powerful yet easy-to-use VSCode image management extension
  - https://github.com/ZhangJian1713/vscode-image-viewer
    - View Images in current project
    - Display all images as thumbnails, support resizing thumbnails and previewing origin image(zoom in/out or rotate freely)
  - https://github.com/1000ch/vscode-svgo
    - Fully featured SVGO extension for Visual Studio Code

- https://github.com/WindMillCode/Paste-Text-From-Image /MIT/202409/ts
  - A VSCode extension that allows you to extract text from images directly from your clipboard and paste it into your editor with a simple right-click.

- https://github.com/Dheovani/SVG-Viewer /MIT/202403/ts
  - Allows you to view SVG images directly within VSCode.
# ext-integrations-note-taking
- https://github.com/sheilaCat/zknotes /202008/ts/inactive
  - zettelkasten zettelkasten .vscode plugin for applying zettelkasten notation.

- https://github.com/inaki-ibarra/vscode-daily-notes /MIT/201910/js/inactive
  - A simple text-based journal extension for Visual Studio Code

- https://github.com/binarynoir/vscode-markdown-tags /202412/ts
  - Enhance your Markdown documents with custom tags. Use predefined or custom labels, customizable colors, and arrow indicators 
# ext-ui
- https://github.com/jkearins/vscode-action-buttons
  - inspired by vscode-action-buttons extension created by Seun Lanlege, maintains compatibility and expands functionality.
  - adds buttons to status bar. The buttons can be used to execute custom commands in Terminal or to activate any VS Code command just like keyboard shortcuts do. The extension has adaptation for esp-idf framework.
  - https://github.com/seunlanlege/vscode-action-buttons /202412/ts
    - Add customizable buttons to the status bar to execute actions or tasks in VS Code.

- https://github.com/DaGhostman/vscode-tree-view /MIT/201907/ts
  - VSCode extension that probvides mail symbol overview of the currently opened file
  - Completely standalone file symbol viewer that does not depend on any other language-specific plugins, making it ideal for cases where the complete language toolset is not available locally.

- https://github.com/subframe7536/vscode-custom-ui-style /MIT/202501/ts
  - VSCode extension that modify CSS and JS code in both editor and webview, unify global font family, setup background image and Electron BrowserWindow options, or add your custom CSS or JS code

- https://github.com/aryanpingle/vscode-webview-variables /202407/ts
  - A collection of all Theme Colors provided by Visual Studio Code's Extension API (and their corresponding CSS names).
  - The primary purpose of this package is to ensure that silly typos in variable names don't cause your code to break. Instead, you can rely on the autocomplete to correctly use (and find!) VSCode's in-built colors.

- https://github.com/GorvGoyl/Shortcut-Menu-Bar-VSCode-Extension /GPLv3/202203/ts/inactive
  - Add handy buttons like beautify, show opened files, save, toggle terminal, etc to the editor menu bar in VSCode
  - Add 35+ handy buttons like beautify, show opened files, save, toggle terminal, activity bar, Find replace etc to the editor menu bar in VSCode

- https://github.com/enyancc/vscode-ext-color-highlight /GPLv3/202403/js/inactive
  - Extension adds colored border around css/web colors in the editor

- https://github.com/BrandonKirbyson/VSCode-Animations /MIT/202501/ts
  - A VSCode extension that adds animations to the editor
  - The theme used in the demo is Solarized Palenight.
  - Apc Customize UI++ is currently not working as of this issue, use Custom CSS and JS Loader or Custom UI Style instead.

- https://github.com/RLabs-Inc/vscode-themes-community /MIT/202410/ts
  - https://vscode-themes-community.vercel.app/generator
  - Create, edit, share and discover new themes for the VS Code editor.
# ext-view
- https://github.com/ctcuff/vscode-font-preview /MIT/202312/ts/inactive
  - A VS Code extension that allows you to view fonts right in your editor

- https://github.com/ericadamski/vscode-carbon_now_sh /202201/ts/inactive
  - A Code package to open the current editor content in carbon.now.sh

- https://github.com/mattbierner/vscode-docs-view /MIT/202401/ts
  - VS Code extension that displays hover documentation in the sidebar or panel
  - Automatically displays documentation for the symbol at the current cursor position.
  - Language independent. Works in any language that supports hovers.
  - Supports syntax highlighting and markdown rendering in the docs view.

- https://github.com/zjffun/vscode-snippets-manager /MIT/202501/ts
  - Create and edit snippets easily.
  - This extension is built over the default VS Code Snippets system, wrapping it into a nice and intuitive UI, improving usability, and making snippets easy to create, edit, delete and search. 
  - It supports user-custom snippets, global snippets and snippets from installed extensions.
  - [Snippets in Visual Studio Code](https://code.visualstudio.com/docs/editor/userdefinedsnippets)

- https://github.com/tahabasri/snippets /MIT/202309/ts/inactive
  - Visual Studio Code already provides robust support for snippets, including their appearance in IntelliSense, tab-completion, and a dedicated snippet picker (Insert Snippet in the Command Palette). 
  - This extension takes snippets to another level by introducing new features that enhance code snippet management.
  - search, sync
- https://github.com/lostintangent/gistpad /MIT/202311/ts
  - VS Code extension for managing and sharing code snippets, notes and interactive samples using GitHub Gists

- https://github.com/usernamehw/vscode-snippets-in-markdown /MIT/202307/ts/inactive
  - Write and keep snippets for VSCode in a markdown file.

- https://github.com/damonsk/vscode-wardley-maps /MIT/202411/ts
  - https://onlinewardleymaps.com/
  - A Wardley Maps for Visual Studio Code extension supporting rendering and editing maps-as-code.
# ext-api
- https://github.com/CodinGame/monaco-vscode-api /MIT/202412/ts
  - https://monaco-vscode-api.netlify.app/
  - VSCode public API plugged on the monaco editor
  - ✨ demo效果类似内存版的vscode，使用纯前端的lsp
  - Most of VSCode functionality implemented as "services"
  - By default, Monaco uses a simplified versions of the VSCode services, called standalone services. 
  - This package allows to 
    - override them with fully-functional alternatives from VSCode
    - add new services that were not included in Monaco
  - This project was mainly created to make the implementation of monaco-languageclient more robust and maintainable.
  - VSCode extensions are bundled as vsix files. This library publishes a rollup plugin (vite-compatible) that allows to load a vsix file.
  - [Getting started guide](https://github.com/CodinGame/monaco-vscode-api/wiki/Getting-started-guide)
  - https://github.com/CodinGame/monaco-editor-react
    - This library uses https://github.com/CodinGame/monaco-editor-wrapper
    - Differences with monaco-react
      - This library outputs some dynamic import and rely on webpack to handle them
# ext-engineering
- https://github.com/redhat-developer/vscode-extension-tester /apache2/202502/ts
  - [ExTester: UI Testing framework for Visual Studio Code Extensions · microsoft/vscode-discussions · Discussion _202404](https://github.com/microsoft/vscode-discussions/discussions/1156)
  - ExTester is designed to enable end-to-end (e2e) testing scenarios using Selenium WebDriver API. 
  - It simulates user interactions with your extension's UI at the VS Code DOM level, providing real UI testing capabilities beyond the VS Code Test CLI.
- https://github.com/webdriverio-community/wdio-vscode-service /MIT/202502/ts
  - A service to test VSCode extensions from end to end using WebdriverIO
# ext-more
- https://github.com/redhat-developer/vscode-didact /apache2/202201/ts/archived
  - Framework and tools for providing interactive tutorials with active links that call VS Code commands
  - 多用于教程
  - The Didact framework is designed to instruct users in a useful way regarding how to complete tasks through a combination of text (Markdown- or AsciiDoc-formatted), images, and active links that show VS Code functionality in action. 
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
# app-toolkit
- https://github.com/SAP/app-studio-toolkit /apache2/202501/ts
  - A VSCode extension that provides a simple way to developer to execute common platform tasks for specific scenarios.
  - This extension allows developers to execute common actions as "Launch Code-Snippet", "Run VS Code command", "Open File", "Execute handler"
# more
- https://github.com/zardoy/vscode-extensions-control /MIT/202304/ts/inactive
  - Extremely powerful extension for VS Code to control (configure) providers of other installed extensions!
  - Currently, it can only disable specific extension providers for now.
