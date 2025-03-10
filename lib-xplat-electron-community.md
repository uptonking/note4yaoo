---
title: lib-xplat-electron-community
tags: [community, electron]
created: 2023-01-02T10:29:39.911Z
modified: 2023-01-02T10:30:19.459Z
---

# lib-xplat-electron-community

# guide

# discuss-electron-vs-tauri/nw
- ## 

- ## 

- ## I love Tauri but I'd still choose Electron for a production app with thousands of users. 
- https://twitter.com/timfishy/status/1672344034172362754
  - Electron allows you to test and validate on the actual browser your users will be using. 
  - WebView gets updates after you've shipped your app which is a maintenance nightmare.
- what’s different from doing web dev? or any dev for that matter.. they all have frameworks that require update or brake constantly. I think only windows have long lived legacy apps running on it. (although it is nice to have a static version of chromium to work with, for ~200mb)
  - 👉🏻 Users of desktop apps don't expect them to stop working after install! On top of that, updating desktop apps is nowhere near as simple as changing the source of your website.
- It's just extra work as well keeping up with a moving target. We've shipped Electron apps that don't require any maintenance and work for new customers years later.

# discuss-bundler/compiler
- ## 

- ## 

- ## 

- ## [Question: what's the relationship between electron-webpack and electron-forge? _202001](https://github.com/electron-userland/electron-webpack/issues/342)
- there is no relationship.... 
  - `electron-webpack` is a module for helping you use electron with webpack and provices a streamlined experience for working with `electron-builder` to package and distribute apps. 
  - Electron forge is a different approach, it adds a boilerplate instead of a module and does a lot of the same things.

# discuss-builder/forge
- ## 

- ## 

- ## 

- ## [Forge vs Builder, as new electron dev : r/electronjs _202412](https://www.reddit.com/r/electronjs/comments/1hd70zu/forge_vs_builder_as_new_electron_dev/)
- I'd suggest to go with electron-builder due to larger community, customisation, easy to adapt and if you need to change autoupdate mechanism in the later part , you can achieve with this.

- I found Forge very easy to start with, but only to get as far as local development. My experience was that for a project which intends to go through with real packaging, signing, and distribution on 2-3 platforms, Forge is insufficiently configurable. You will need to eventually either plan on switching to Builder, or sweep away most of Forge and replace with your own tools.

- Builder because its what the vite template uses: create-electron-vite

- Builder is easier to customize
  - Forge uses the official ASAR packager (so you can use the asar validation flag, but it looks like builder is also enabling this)

- ## [Electron community reinvented electron-builder/etc. as electron-forge. How to package Quasar w/ electron-forge?_202309](https://github.com/quasarframework/quasar/discussions/16380)
- electron-forge uses the electron-packager under the hood. It seems to be a convenience/configuration package.

- ## [Significant Performance Difference Between electron-builder and electron-forge · electron-userland/electron-builder](https://github.com/electron-userland/electron-builder/issues/8000)
- Can you run a test with asar: false?
  - electron-builder only packages the code into an asar format and then copies that into the .app, which should be no different than electron-forge. 
  - The only difference I can think of is that the asar compilation is not as optimized in electron-builder's approach than that of @electron/asar package handles it.

- ## [Question: How easy is it to switch between Builder and Forge? · electron-userland/electron-builder _202003](https://github.com/electron-userland/electron-builder/issues/4733)
- It depends on your needs. Some users needs advanced / regular / portable installer for Windows. In this case only electron-builder provides solution using NSIS.
- it will be easier to switch from electron-forge to electron-builder because electron-builder provides more advanced features than electron-forge. 

- Keep in mind that electron-builder STILL doesn't support Flatpak while electron-forge does. Flatpak is getting big on pretty much "every distro except Ubuntu"

- ## 🆚️ [Question: What's the difference with electron-forge? · electron-userland/electron-builder _201702](https://github.com/electron-userland/electron-builder/issues/1193)
- electron-builder it is a tool to build your Electron application.
  - electron-forge it is a tool to build your Electron application PLUS boilerplate to create electron app.
- electron-builder and electron-forge are tools to build your electron app. electron-compile to create.

- electron-builder 16.2.0 supports electron-forge and electron-compile.

- You can use appimage, snap, nsis and nsis-web electron-builder targets in the electron-forge("win32": ["nsis"]). But it is not recommended, because electron-forge packaging and publishing is a far away in terms of quality/feature set from electron-builder.

- ## 🆚️ [Why Electron Forge - Electron Forge](https://www.electronforge.io/core-concepts/why-electron-forge)
- Electron Forge can be considered an alternative to Electron Builder, which fulfills the same use-case for application building and publishing.
- The key difference in philosophy between the two projects is that Electron Forge focuses on combining existing first-party tools into a single build pipeline, while Builder rewrites its own in-house logic for most build tasks.
- two main advantages to using Forge:
  - Forge receives new features for application building as soon as they are supported in Electron. These features are built with first-party Electron tooling in mind, so Forge receives them as soon as they are released.
  - Forge's multi-package architecture makes it easier to understand and extend. Since Forge is made up of many smaller packages with clear responsibilities, it is easier to follow the flow of the code. 

- ## [Flatpak packaging · gristlabs/grist-desktop](https://github.com/gristlabs/grist-desktop/issues/16)
- 20240615: We use `electron-builder` to build Grist Desktop. 
  - Unfortunately, it currently doesn't support publishing to Flatpak repositories. 
  - We will consider adding a Flatpak build once electron-builder supports it.

# discuss-storage
- ## 

- ## ⚖️ [Question: IndexedDB size limit · Issue · electron/electron](https://github.com/electron/electron/issues/4550)
  - Is there a limit on IndexedDB for electron apps? I know it is somewhat dynamic between browsers link but I would assume it would be hard drive size dependent on electron apps. 
- We have the same size limitation with Chrome browser, which is "1/3 of the of available disk space".

- It so happens that a new api that can help you determine your quota has been exposed. https://developers.google.com/web/updates/2017/08/estimating-available-storage-space
  - What I would do is: know the quota and have a way of informing /warning my user when they are about to hit the quota.

- ## 🛢️ [Store a database locally · Issue · electron/electron _201510](https://github.com/electron/electron/issues/3195)
  - I am developing an app that needs to be run even if there's no internet connection. I am currently getting the data from an online MySQL database. 
  - What I want to do is to find a way to store the database locally, so if I restart the app and there's no internet connection, it will run with the last known data.
  - this was posted 2 years ago. Since then, I have been working on many cordova/electron projects. The best approaches I have found are NeDB, IndexedDB, SQLite and LocalStorage. Use them wisely!

- The simplest way would be writing to a file as JSON. When you query your sql in MySQL write the results to a file then work on that file.

- There's a few other solutions to this problem: 
  - LocalStorage
  - indexeddb(dexie, localForage)
  - level.js and the LevelUP bindings. This is probably heavier than what you're looking for.

- If you are looking for a persistent data storage solution, check out electron-json-storage
  - I have used the jviotti/electron-json-storage and it's not a good solution for production since it doesn't support file locking so if perform several write transaction at the same time, the storage file will break.
  - I'm going to use IndexedDB.

- For anyone reading don't forget about SQLite. You will need to rebuild it for Electron though. 

- this louischatriot/nedb also seems cool and is 100% JavaScript, no binary dependency
# discuss-dev-log
- ## 

- ## 

- ## [Bindings not found error · Issue · vitejs/vite-plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc/issues/74)
- We have fixed the problem with running this command: `npm i -D @swc/cli @swc/core`
# discuss
- ## 

- ## 

- ## 

- ## [Basic Electron Framework Exploitation | Hacker News _201908](https://news.ycombinator.com/item?id=20636805)
- > The problem lies in the fact that Electron ASAR files themselves are not encrypted or signed
  - ASAR files are signed as part of the application bundle. The issue is that folks don't understand how gatekeeper works so let me try explain it here.
  - When you download an application from the internet, macOS initially considers it "quarantined". When a quarantined application is first opened gatekeeper scans it _completely_ and if it's happy removes the quarantine tag and let's it launch.

- ASAR code-signing is not fool-proof, as we can still do in-memory patching, etc. Game hackers have been patching (signed) OpenGL and DirectX drivers for decades. It's a very common technique.

- If you ship your app as a setup bundle (say, an AppSetup.exe, an App.dmg, or rpm/deb files), you should code-sign the whole thing, which completely sidesteps this issue. The same is true if you use the Mac App Store, Windows Store, or Snapcraft Store.

- 

- ## [java 也是跨平台, 为何没有 gui 框架像electron 那么火? - 知乎](https://www.zhihu.com/question/601426954/answers/updated)
- Java最初诞生之后，它的GUI也是比较火的，许多Java应用程序都是具有GUI的桌面应用程序。 但现在GUI界面已经普遍地被网页界面取代，Java也不例外，Java Web应用成为主流的应用。所以Java的GUI API就逐渐使用得少了。

- ## [为什么用 electron 开发的桌面应用那么多？ - 知乎](https://www.zhihu.com/question/509656170/answer/3176126664)
- 飞书和钉钉肯定不是，他俩用的CEF。Electron和CEF底下其实都是chromium内核。
  - 确实大家都喜欢用前端开发桌面端软件，只能说前端开发圈的强大吧。最近二十几岁的QQ也发布了electron版本，足见electron的厉害了

- ## I learned that you can load multiple "BrowserViews" inside one "BrowserWindow" in @electronjs
- https://twitter.com/hhg2288/status/1769708139182449041
  - This is interesting to have multiple UI's load on the same window but in separate "threads"

- ## Am I right in thinking that Electron apps can't have "type": "module" in their package.json? Getting errors when I try.
- https://twitter.com/mattpocockuk/status/1719028975945531724
  - its landing in v28 - use @28 .0.0-alpha.6 to get it now

- ## Would anyone like to partner on creating an Electron alternative that builds on top of React Server Components?
- https://twitter.com/tomus_sherman/status/1684522055696351234
  - It would take the good parts of Electron, Tauri, and React Native. The IPC would be replaced with the server components (React Flight)

- Try building the React parts on top of Electron first, and then replace Electron once you’ve got the abstractions in the right spot — and you’re sure Electron is the problem
- This is a good place for a POC, but really I wanna avoid shipping chromium. This just seems silly to me
- Building an app framework that can do the native things Electron can across multiple platforms sounds like not much challenge, but a lot of work.
- 👉🏻 I think the issue with Electron apps is primarily the Javascript in the render process and multi-process architecture **without shared memory**, not the webview engine. Getting bytes from native-land into any webview involves annoyingly expensive copying.
- What use cases are blocked or hindered because of that copying across processes?
- The example I hit recently building a screenshot editing app:
  1. Trigger screenshot using global shortcut in main process
  2. Capture screenshot using native API in main process
  3. Copy screenshot from main process to render process
  - All the unavoidable encode/copy/decode take time. Even optimized using a Worker to receive and decode the image bytes, my app feels laggy compared to native screenshot apps
- Tbh I struggle to believe this is an absolute blocker, otherwise how would we have performant apps like VS Code?
  - Well the big difference between my app and VS Code is the amount of bytes we need to copy from the main process to the WebView process. VS Code needs *at minimum* a screen of text, <10kb. I need *at minimum* ~600kb of JPG image (noticeably bad) or ~15mb of PNG image.
- but this is not over the network. How can this even be noticeable? Think about how fast ram is compared to the network and still loading of images on the web feels fast (enough).

- What about implement the new RN architecture for desktop, Fabric, instead of the bridge concept
  - I want to specifically avoid JS<->native foreign function calls (eg. Tauri, RN) because it requires complicated codegen among other nastiness. Instead I want to use the React Flight spec for all IPC

- I feel Electron/Tauri and React Native are in very different spaces. The former display web content, the latter uses a javascript / react runtime, but displays *native* platform widgets via a bridge. Many conflate them, but I think the difference is really significant

- ## [【CEP 扩展开发一】简介 - 知乎](https://zhuanlan.zhihu.com/p/506927682)
- Adobe 插件，大致可以分成以下几类：
  - ExtendScript 脚本
  - 面板插件：Flash 面板插件，CEP 面板插件，UXP 面板插件
  - 独立客户端
  - C++ 插件
- ExtendScript 是 ECMAScript3 的一种方言，和 JavaScript 基本上语法一样，不过集成了一些例如指令，模块化，反射系统，三引号字符串，操作符重载等语法特性。文件后缀名是 .jsx（不是 react 用的那个 JS 的 DSL），所以 ExtendScript 又被称为 jsx。由宿主（例如 PS, AE, PR 等设计软件自身都叫宿主）实现的 ExtendScript 引擎解释执行，不同宿主都能解释执行 jsx，但是底层实现以及注入的宿主特有的 API 不一样。
- ExtendScript 可以调用宿主的各种 API，例如在 AE 中可以访问图层信息，调用渲染队列输出媒体资源，也有原生能力例如读写文件，还可以使用内置的各种窗口和控件接口去创建图形界面。因此它完全可以作为一种插件形式去实现独立的功能。
- 其实 adobe 软件支持的脚本语言并不只有 ExtendScript，例如在 PS 其实是支持：Apple Script, VBScript 和 ExtendScript
- CEP(Common Extensibility Platform) 扩展的界面是使用 Chromium 渲染的，采用的是 CEF（Chromium Embedded Framework） 架构。
  - CEF简单理解就是将浏览器嵌入到其它应用中让我们可以直接使用前端技术去开发界面，electron, nwjs，tauri 是 CEF 架构的代表框架了。
  - 这类框架除了是使用前端技术开发界面，runtime 往往都还搞成混合型的，例如开启了 node 集成的 electron 和 nwjs 的浏览器窗口的运行时都是 web runtime 和 nodejs runtime 的复合 runtime。
- 其实 CEP 的架构和从 HTML 页面启动的 nwjs 最像，每一个 CEP 扩展本质就是本地的一个文件夹，打开一个 CEP 扩展其实就是就是去渲染 manifest.xml 指定的一个 HTML 文件。

- ✨ UXP (Unified Extensibility Platform)是下一代的面板插件架构，未来 CEP 扩展的结局会和 Flash 插件一样被废弃，并被 UXP 架构取代。
- CEP 的劣势：
  - CEP 使用完整的 Chromium 渲染 web，非常的吃资源，开多个 CEP 插件的时候更甚
  - CEP 并不能直接访问宿主，需要写 jsx 代码访问宿主。实际开发时你要写两端代码，一份是 jsx，一份是浏览器环境代码，分别被两个不同的 js 引擎执行，互相调用很不方便
  - CEP 插件不能使用原生控件，你需要编写很多 CSS 样式才能与原生面板和对话框的样式风格匹配
  - jsx 的 ECMAScript 规范版本很低，你需要在浏览器的高版本 ECMAScript 和 jsx 的 ECMAScript3 来回切换
- UXP 的优势：
  - UXP 可以直接沟通宿主，不需要编写 jsx
  - UXP 官方有提供一个插件启动器和自定义的 Chrome Dev Tools 用于 debugger，比起 CEP 开发更简单
  - UXP 可以使用 Spectrum CSS 组件库来，这个组件库支持自动切换主题而且是跨平台的，能够让你开发的面板看起来和应用本身风格一致
- UXP 目前只支持 PS 平台，如果你是给 PS 以外的 adobe 软件开发面板插件，那你只能选 CEP，CEP 扩展支持的平台很多
