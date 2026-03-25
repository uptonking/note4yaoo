---
title: lib-xplat-electron-dev
tags: [cross-platform, dev, electron]
created: 2020-05-18T09:49:23.005Z
modified: 2021-05-13T03:08:52.583Z
---

# lib-xplat-electron-dev

# guide

- pros
  - ✨ 使用最新的chrome特性: split-view, WebMCP, chrome-built-in-AI
  - 内置了chromium/nodejs, 使用方碰到兼容性问题的概率小很多
  - 相对于qt/zed等原生框架实现ui，electron基于html/dom实现，可以方便集成类似rrweb进行操作回放
  - 基于electron可将数据保存在本地文件系统，比web浏览器支持更大的缓存
  - 成熟工具如vscode提供了多平台如 web/win/linux/mac 的架构参考
  - 支持extension及扩展市场，很多第三方ide如theia/opensumi都支持vsc扩展

- cons
  - 基于ipc的通信增加了web端开发的复杂度，但能支持client-server/local/idb多种架构

- features
  - Build cross-platform apps with web tech(js/html/css/chromium)
  - Compatible with macOS, Windows, and Linux

- who is using #electron 🌰
  - popular: vscode/theia/opensumi, jupyter, postman-like(web+pc)
  - known: obsidian, qq, slack, mattermost, zulip, figma-desktop
  - db: mongodb-compass, dbgate, beekeeper, sqlectron
  - notes(web/pc): obsidian, joplin(AGPL), marktext(MIT), siyuan(AGPL), trilium(AGPL), notable(MIT), notesnook(GPL), Zettlr(GPL), yn(AGPL), tinywrite
  - open: drawio(apache2), tagspaces, medis
  - ai: comfyui, transformerlab-training-chat
  - ai-known: codex-app, claude-cowork
  - trending: aionui
  - 经典示例: file-manager, note-taking, reader-epub

- web+pc: vscode, jupyter, (rstudio)
  - git clients
  - postman, hoppscotch
  - notes: colanode
  - bitwarden-passwords-clients
  - otel
  - ocr
  - package-manager, downloader
  - services: nginx, redis, pg/mysql/sqlite, sync, monitoring
  - cases: wallpaper

- cli-wrapper
  - claude-code-ui
  - git-ui
  - ai: ollama

- tips
  - 🏘️ 可参考各大 coding-agent-cli 的实现, 有第三方开发者在cli上实现web/electron/tauri
  - 要在侧重web(no-server)和侧重本地(c/s或b/s)的架构上做取舍，主要考虑数据源、数据量、性能
    - 还要在csr/ssr上做选择，没有大而全的架构
  - 不要执着于web与桌面版mac/win/linux采用相同的架构, web版可针对速度优化, 桌面版可针对本地计算优化, 需求不同
    - vscode的桌面版性能很好, web版就感觉很慢
  - 不建议基于electron实现自定义浏览器，要考虑支持各浏览器自带的扩展商店，可在自己的应用层实现
  - ? electron-for-android/ios vs apps

- 🤔 what can chromium and nodejs do, but tauri webview cannot do?
  - compatibility: safari-webkit cons
  - agentic browser-use
  - headless browser
  - Execute Dynamic Code (The "Interpreter" Pattern): using vm or eval
    - 是否可用于sandbox场景
  - Media Codecs
  - os/hardware
    - audio/video recording
    - WebHID, Web Serial, WebUSB
    - Bluetooth API
    - Desktop Capturer
  - 使用nodejs/npm生态
  - the main things Chromium+Node give you in an Electron renderer that a Tauri system WebView doesn't are direct access to the Node runtime (fs, child_process, native addons, npm-only modules) and a consistent, full Chromium feature set (Chromium flags / newer web APIs available because Electron ships Chromium).
  - Electron bundles a specific Chromium release so you get the same web APIs everywhere (WebRTC, modern codecs, WebCodecs, WebAudio, WebCrypto changes, web platform flags). 
  - Tauri uses the system WebView (WebView2/WKWebView/etc.), so available browser APIs depend on the OS and webview version and may lag or vary by platform.
  - Chrome-only flags or embedder features & extensions: opfs
  - Chrome Extensions: react-devtools
  - Electron's `<webview>` tag allows you to embed external websites directly within your app's DOM with full isolation and control. Tauri cannot do this 
    - webview 比 iframe 更强大, 突破 X-Frame-Options 的限制

- resources
  - [Cross platform software frameworks](https://blog.tomayac.com/2023/02/23/cross-platform-software-frameworks/)
  - [electron alternatives](https://dev.to/urielsouza29/comment/1lb73)
  - [QQ技术团队分享：新QQ NT桌面版/electron内存优化探索之路_202308](https://mp.weixin.qq.com/s/uk_KKk3YuMyY2Auk68SwgA)
# draft
- nativefier(archived): webpage wrapper for electron
  - 可以复用pake的打包逻辑但产物为electron
- electron + chrome-mcp/WebMCP

- 编辑器/笔记/llm-api的客户端都需要便捷的ui

- clients for popular apps like notion-database
  - Stirling-PDF
  - joplin or extension
  - drawio
  - devtools: lint/format-cli
  - cli: ImageMagick, ocr, pandoc(GPL/haskell), ffmpeg, curl/wget
  - saas: filebrowser
  - more: electron wrapper for chromium
- llm-ui/client
  - 可参考 ollama/lmstudio/janai 封装 llama.cpp 的逻辑
  - 封装db操作工具, 针对sqlite/turso
  - huggingface-cli

- compatibility
  - vscode-extension
  - obsidian-plugins

- integrations
  - vercel-aisdk
  - chat/slack

- maybe
  - copy zed xp to vscode

## ai-electron 👾

- [Chrome Web AI Demos](https://chrome.dev/web-ai-demos/)
  - [Proofreader API](https://chrome.dev/web-ai-demos/proofreader-api-playground/)
  - [Translator and Language Detector API Playground](https://chrome.dev/web-ai-demos/translation-language-detection-api-playground/)
  - [Join the early preview program  |  AI on Chrome](https://developer.chrome.com/docs/ai/join-epp)
# dev-xp
- 对本地文件的rag采用client/server更合适, 而不是在每个文件夹都创建index.sqlite数据库
  - 方便支持多个terminal/agent/app同时操作文件，能减少冲突
  - 减少重复索引
# dev
- Electron运行package.json中的main脚本中的进程被称为主进程，该进程在应用整个生命周期只会存在唯一一个，负责面窗口的创建、控制、销毁等管理行为，同时也能控制整个应用的生命周期。
  - 主进程本质上是一个 Node.js 进程，该进程充分利用了 Node.js 的跨平台特性，在其 API 的底层，抹掉了不同操作系统中的差异
  - 主进程同时提供一套跨平台的接口，能控制各个操作系统中的原生资源，如：对话框、菜单、文件拖拽等，使得 Electron 的用户体验极大的接近了原生应用。
  - Electron应用的入口是一个js文件（NW.js入口是html文件），运行这个入口文件（通常会是package.json里的main脚本）的进程称作主进程，在主进程使用BrowserWindow模块可以创建并管理web页面，也就是应用的GUI
- 当主进程每创建一个独立 BrowserWindow 实例，Electron都会初始化一个独立的渲染进程，隔离了不同窗口之间的环境
  - 在主进程创建的一个个web页面也都运行着自己的进程，即渲染进程，渲染进程各自独立，各自管理自己的页面，类似浏览器一个的tab
  - 可隐藏窗口，然后让其在背后运行代码
- webview
  - Display external web content in an isolated frame and process.
- preload
  - preload属性能够在webview内所有脚本执行之前，先执行指定的脚本
  - preload环境是一个既能用Node API，又能访问DOM、BOM的特殊环境，我们熟悉的另一个类似环境是renderer
  - preload属性的特点是只在第一次加载页面时执行，后续加载新页不会再执行preload脚本
- Setting `nodeIntegration` to `false` will disable node.js in the renderer process - i.e. your app can only do what a web browser will do.
  - BrowserWindow提供的preload的配置是为了在页面第一次加载文档之前预先加载js脚本文件, preload配置的脚本文件路径，只能为本地文件，其协议必须是file:、asar: 二者之一
  - preload脚本仍然有能力去访问所有的 Node APIs, 即使配置 `nodeIntegration: false` 。但是当这个脚本执行执行完成之后，通过Node 注入的全局对象（global objects）将会被删除
# nw.js
- [nw.js: 0.12 to 0.13](https://nwjs.readthedocs.io/en/latest/For%20Users/Migration/From%200.12%20to%200.13/)
  - NW.js application is running as a Chrome App internally. 
  - All chrome.* platform APIs and features can be used in NW application now. 
  - The default protocol is changed from file:// to chrome-extension://
# changelog
- ECMAScript modules (i.e. using `import` to load a module) are supported in Electron as of Electron 28(_20231205).

- From Electron 20 onwards, preload scripts are sandboxed by default and no longer have access to a full Node.js environment. 
# more
