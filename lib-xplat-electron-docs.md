---
title: lib-xplat-electron-docs
tags: [docs, electron]
created: 2024-01-31T19:33:53.245Z
modified: 2024-01-31T19:34:04.442Z
---

# lib-xplat-electron-docs

# guide

- resources
  - [Why Electron](https://www.electronjs.org/docs/latest/why-electron)
# faq

## 🆚️ electron vs cef

- The CEF is a project that turns Chromium into a library, and provides stable APIs based on Chromium's codebase. 
  - Very early versions of Atom editor and NW.js used CEF.
- To maintain a stable API, **CEF hides all the details of Chromium and wraps Chromium's APIs with its own interface**. 
- So when we needed to access underlying Chromium APIs, like integrating Node.js into web pages, the advantages of CEF became blockers.
- So in the end **both Electron and NW.js switched to using Chromium's APIs directly**.
- ref
  - https://www.electronjs.org/blog/electron-internals-building-chromium-as-a-library

### [CEF和Electron的区别是什么？ - 知乎](https://www.zhihu.com/question/510368054)

- Electron面向的开发者是纯前端开发者，会用JavaScript，HTML，CSS，但不会用C++。
- CEF面向的开发者是会用C++也会用JavaScript，HTML，CSS的开发者。

- V8只负责解析并执行JavaScript，它是没有访问操作系统的能力的，比如读写文件，访问网络（这里主要指通过Socket访问网络），访问进程信息等，这些能力V8没有，集成了Node.js后，开发者就拥有这些能力了，
  - 但光集成Node.js还不够，Electron自己还封装了一些操作系统的能力供JavaScript调用，比如访问剪切板，发送系统通知，访问托盘图标等，
  - 这些能力是V8和Node.js都没有的，但却是开发一个桌面应用所必备的。

- CEF则比较单纯，只对Chromium做了精简和封装，允许开发者通过C++代码控制Chromium核心，允许JavaScript和C++互操作，允许开发者在Chromium的多个进程间通信，
  - 像访问托盘图标、访问剪切板、Socket通信、读写文件这类事情，它都没做，要完成这些工作，开发者得自己写代码。
  - 这也无可厚非，因为C++开发者可以很容易的完成这些任务。
  - 但JavaScript开发者就很难完成这些任务，所以Electron为他们做了这些事情，而且做的很好。

## 🆚️ electron vs nw.js

- [Technical Differences Between Electron and NW.js | Electron](https://www.electronjs.org/docs/latest/development/electron-vs-nwjs)
  - Electron works more like the Node.js runtime
  - In NW.js, the Node integration in web pages requires patching Chromium to work, while in Electron we chose a different way to integrate the libuv loop with each platform's message loop to avoid hacking Chromium. 
  - By using the multi-context feature of Node, Electron doesn't introduce a new JavaScript context in web pages. NW.js has optionally supported multi-context since 0.13.
  - Electron has a bigger community, more production apps 

- 两个原理应该不一样，electron应一个窗口会对应一个渲染进程，而nw.js本身是可选一个窗口一个渲染进程，且默认应该不是，你可以比较下当nw.js开启一个窗口一个渲染进程后两者的速度。

### [NW.js 和 Electron 各有什么优缺点 - 知乎](https://www.zhihu.com/question/38854224)

- 比较NW.js和Electron之前，先要明白虽然是用javascript+html写的app，但是都会跑两部分的js runtime，分别是node-runtime和chromium-runtime

- 功能上看，2者差不多，主要的区别是入口方式。
- Electron是基于node的，入口是类似node module的index.js，这是因为Electron是基于node的event-loop将chromium的功能和event全部整合app，Electron的开发跟其他的node应用没区别。
- NW.js像一个跑在node-platform上的浏览器，所以他的入口是index.html，NW.js将自己的功能都整合进了chromium-runtime，因此更接近一个前端的应用开发方式。NW.js也可以用到node的api，这是通过binding到chromium-runtime来调用的。
- 👉🏻 NW把2套js-runtime环境整合到了一起，Electron则是保持2套js-runtime彼此独立。
  - NW的app中的js代码可以使用所有的API（这不见得是好事）。electron的app中的js是可以分前后端的。

- NW提供了二进制JS加密方案，electron没有并且以后也不打算搞
  - 常规画界面那种低价值代码，minified就差不多够用了。核心代码（如果有）可以转webassembly，既解决代码保密问题又解决性能问题

- nw和electron 出自同一个人之手，而且他也玩知乎。 electron 比 nw 后出世，你说该用哪个？

### [Electron 和 NW.js 在技术上的差异 - 知乎](https://zhuanlan.zhihu.com/p/34250289)

- 程序入口。
  - 在NW.js中，应用的主入口是网页或者js脚本；
  - 在Electron中，入口是一个js脚本
- 构建系统。
  - Electron通过libchromiumcontent来访问Chromium的Content API，避免了构建整个Chromium带来的复杂度
- 与Node集成。
  - 在NW.js，网页中的Node集成需要通过给Chromium打补丁来实现，Electron通过各个平台的消息循环与libuv的循环集成，避免了直接在Chromium上做改动
- 多上下文语境。
  - NW.js包括Node上下文和web上下文，自从0.13以来NW.js选择性支持多上下文。通过使用Node的multi-context特性，Electron不需要在网页中引入新的js上下文

### [为什么用 electron 开发的桌面应用那么多？ - 知乎](https://www.zhihu.com/question/509656170/answers/updated)

- 飞书和钉钉肯定不是，他俩用的CEF。
  - Electron和CEF底下其实都是chromium内核。

- 因为软件开发太卷了，及其追求速度，所以怎么快怎么来呗，至于性能啥的，后面再说，又不是不能用

## electron中可以使用web worker吗？

- 可以用，但不推荐
- It is possible to use Node.js features in Electron's Web Workers, to do so the nodeIntegrationInWorker option should be set to true in webPreferences
- All built-in modules of Node.js are supported in Web Workers
- However none of Electron's built-in modules can be used in a multi-threaded environment.
- Any native Node.js module can be loaded directly in Web Workers, but it is strongly recommended not to do so. 
  - **Most existing native modules have been written assuming single-threaded environment, using them in Web Workers will lead to crashes and memory corruptions**.
  - Note that even if a native Node.js module is thread-safe it's still not safe to load it in a Web Worker because the `process.dlopen` function is not thread safe.
  - The only way to load a native module safely for now, is to make sure the app loads no native modules after the Web Workers get started.

- ref
  - https://www.electronjs.org/docs/tutorial/multithreading
# [Why Electron](https://www.electronjs.org/docs/latest/why-electron)
- Why choose web technologies
  - Web technologies include HTML, CSS, JavaScript, and WebAssembly. They’re the storefront of the modern Internet. 
  - Versatility: all industries
  - Reliability: Web technologies are the most-used foundation for user interfaces on the planet
  - ⚖️ Interoperability: Whatever provider or customer data you need to interact with, they will have probably thought of an integration path with the web. 
  - Ubiquity: ample access to resources and materials

- Why choose Electron
  - Enterprise-grade: reliable, secure, stable
  - Mature: an impact project with the OpenJS foundation
  - performance: for security reasons, apps have to run in their own sandboxes, isolated from each other.
  - Developer experience: ecosystem, built-in capabilities, Native code when you need it
    - Thanks to Node.js’ mature native addon system, you can always write native code. 
# docs
- Although you need Node.js installed locally to scaffold an Electron project, Electron does not use your system's Node.js installation to run its code. 
  - Instead, it comes bundled with its own Node.js runtime. This means that your end users do not need to install Node.js themselves as a prerequisite to running your app.

- Many of Electron's core modules are Node.js event emitters that adhere to Node's asynchronous event-driven architecture. The `app` module is one of these emitters.
- In Electron, BrowserWindows can only be created after the app module's `ready` event is fired.

- Each web page your app displays in a window will run in a separate process called a renderer process (or simply renderer for short). 
  - Renderer processes have access to the same JavaScript APIs and tooling you use for typical front-end web development

- Preload scripts are injected before a web page loads in the renderer, similar to a Chrome extension's content scripts. 
  - A preload script contains code that runs before your web page is loaded into the browser window. 
  - It has access to both DOM APIs and Node.js environment, and is often used to expose privileged APIs to the renderer via the `contextBridge` API.
- A BrowserWindow's preload script runs in a context that has access to both the HTML DOM and a limited subset of Node.js and Electron APIs.
  - From Electron 20 onwards, preload scripts are sandboxed by default and no longer have access to a full Node.js environment. Practically, this means that you have a polyfilled `require` function that only has access to a limited set of APIs.

- All built-in modules of Node.js are supported in Web Workers, and asar archives can still be read with Node.js APIs. 
  - However none of Electron's built-in modules can be used in a multi-threaded environment.
- Any native Node.js module can be loaded directly in Web Workers, but it is strongly recommended not to do so. 
  - Most existing native modules have been written assuming single-threaded environment, using them in Web Workers will lead to crashes and memory corruptions.
- Note that even if a native Node.js module is thread-safe it's still not safe to load it in a Web Worker because the `process.dlopen` function is not thread safe.
  - The only way to load a native module safely for now, is to make sure the app loads no native modules after the Web Workers get started.

- Navigation history is stored per WebContents instance. 

- If you want to embed (third-party) web content in an Electron BrowserWindow, there are three options available to you: `<iframe>` tags,  `<webview>` tags, and `WebContentsView`
- Iframes in Electron behave like iframes in regular browsers.
  - To limit the number of capabilities of a site in an `<iframe>` tag, it is recommended to use the `sandbox` attribute 
- `WebContentsView`s are not a part of the DOM—instead, they are created, controlled, positioned, and sized by your Main process.
  - WebContentsViews offer the greatest control over their contents, since they implement the webContents similarly to how BrowserWindow does it. 
  - However, as WebContentsViews are not elements inside the DOM, positioning them accurately with respect to DOM content requires coordination between the Main and Renderer processes.
- WebViews are based on Chromium's WebViews and are not explicitly supported by Electron. 
  - we do not recommend you to use WebViews, as this tag undergoes dramatic architectural changes that may affect stability of your application. 
  - WebView is a custom element (`<webview>`) that will only work inside Electron. They are implemented as an "out-of-process iframe". This means that all communication with the `<webview>` is done asynchronously using IPC. 
  - Compared to an `<iframe>`,  `<webview>` tends to be slightly slower but offers much greater control in loading and communicating with the third-party content and handling various events.

- Chromium and Node.js have their own implementations of the ESM specification, and Electron chooses which module loader to use depending on the context.
- Electron's main process runs in a Node.js context and uses its ESM loader. Usage should follow Node's ESM documentation
  - ES Modules are loaded asynchronously. This means that only side effects from the main process entry point's imports will execute before the `ready` event.
  - This is important because certain Electron APIs (e.g. app.setPath) need to be called before the app's `ready` event is emitted.
  - With top-level await available in Node.js ESM, make sure to `await` every Promise that you need to execute before the `ready` event. Otherwise, your app may be ready before your code executes.
  - These CommonJS `require` calls load module code synchronously. If you are migrating transpiled CJS code to native ESM, be careful about the timing differences between CJS and ESM.
- Electron's renderer processes run in a Chromium context and will use Chromium's ESM loader. 
  - If you wish to load JavaScript packages via npm directly into the renderer process, we recommend using a bundler such as webpack or Vite to compile your code for client-side consumption.
- A renderer's preload script will use the Node.js ESM loader when available. 
  - Preload scripts will ignore `"type": "module"` fields, so you must use the `.mjs` file extension in your ESM preload scripts.
- Sandboxed preload scripts can't use ESM imports
  - Sandboxed preload scripts are run as plain JavaScript without an ESM context. 
  - If you need to use external modules, we recommend using a bundler for your preload code. 
  - Loading the electron API is still done via require('electron').

## process

- Electron inherits its multi-process architecture from Chromium, which makes the framework architecturally very similar to a modern web browser.

- the Chrome team decided that each tab would render in its own process, limiting the harm that buggy or malicious code on a web page could cause to the app as a whole. 
  - A single browser process then controls these processes, as well as the application lifecycle as a whole. 
  - Electron applications are structured very similarly. As an app developer, you control two types of processes: main and renderer. These are analogous to Chrome's own browser and renderer processes outlined above.

- Each Electron app has a single main process, which acts as the application's entry point. 
  - The main process' primary purpose is to create and manage application windows with the `BrowserWindow` module.
  - Each instance of the BrowserWindow class creates an application window that loads a web page in a separate renderer process. 
  - A renderer process is also created for web embeds such as the `BrowserView` module. The `webContents` object is also accessible for embedded web content.
  - When a BrowserWindow instance is destroyed, its corresponding renderer process gets terminated as well.

- the main process also adds custom APIs to interact with the user's operating system. 
  - Electron exposes various modules that control native desktop functionality, such as menus, dialogs, and tray icons.
- Each Electron app spawns a separate renderer process for each open BrowserWindow (and each web embed). 
  - code ran in renderer processes should behave according to web standards (insofar as Chromium does, at least).
  - An HTML file is your entry point for the renderer process.
- Renderer processes can be spawned with a full Node.js environment for ease of development. Historically, this used to be the default, but this feature was disabled for security reasons.

- Preload scripts contain code that executes in a renderer process before its web content begins loading. These scripts run within the renderer context, but are granted more privileges by having access to Node.js APIs.
  - Because the preload script shares a global `Window` interface with the renderers and can access Node.js APIs, it serves to enhance your renderer by exposing arbitrary APIs in the window global that your web contents can then consume.

- Each Electron app can spawn multiple child processes from the main process using the UtilityProcess API.
  - The utility process can be used to host for example: untrusted services, CPU intensive tasks or crash prone components which would have previously been hosted in the main process or process spawned with Node.js child_process.fork API. 
  - The primary difference between the utility process and process spawned by Node.js child_process module is that the utility process can establish a communication channel with a renderer process using MessagePorts.
  - An Electron app can always prefer the `UtilityProcess` API over Node.js `child_process.fork` API when there is need to fork a child process from the main process.

- Context Isolation is a feature that ensures that both your preload scripts and Electron's internal logic run in a separate context to the website you load in a webContents
  - This means that the window object that your preload script has access to is actually a different object than the website would have access to
  - Context isolation has been enabled by default since Electron 12, and it is a recommended security setting for all applications.

- 
- 
- 
- 
- 
- 
- 
- 
- 

- Starting from Electron 20, the sandbox is enabled for renderer processes without any further configuration.
- One key security feature in Chromium is that processes can be executed within a sandbox. 
  - The sandbox limits the harm that malicious code can cause by limiting access to most system resources — sandboxed processes can only freely use CPU cycles and memory. 
  - In order to perform operations requiring additional privilege, sandboxed processes use dedicated communication channels to delegate tasks to more privileged processes.
- In Chromium, sandboxing is applied to most processes other than the main process. 
  - This includes renderer processes, as well as utility processes such as the audio service, the GPU service and the network service.
- Sandboxed processes in Electron behave mostly in the same way as Chromium's do, but Electron has a few additional concepts to consider because it interfaces with Node.js.
  - A sandboxed renderer won't have a Node.js environment initialized.
  - In order to allow renderer processes to communicate with the main process, preload scripts attached to sandboxed renderers will still have a polyfilled subset of Node.js APIs available. 
  - Because the `require` function is a polyfill with limited functionality, you will not be able to use CommonJS modules to separate your preload script into multiple files. If you need to split your preload code, use a bundler such as webpack or Parcel.

- For most apps, sandboxing is the best choice. In certain use cases that are incompatible with the sandbox (for instance, when using native node modules in the renderer), it is possible to disable the sandbox for specific processes.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

# more
