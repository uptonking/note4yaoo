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

- ## 🤔 做 windword 之前，稍微短暂的思考过，用 electron 还是 tauri。
- https://x.com/wwwgoubuli/status/1996028487711556010
  - 在模型下载后几百兆到几个G的情况下，那 100M 有什么关系吗？
  - 尤其是要调用 native api 的时候，在 tauri 里，你真的搞的定吗？
  - 折腾一个月下来，现在看来，选 electron 真是太明智了。

- 我只考虑要不要用 native api ，用了就 electron

- ## I love Tauri but I'd still choose Electron for a production app with thousands of users. 
- https://twitter.com/timfishy/status/1672344034172362754
  - Electron allows you to test and validate on the actual browser your users will be using. 
  - WebView gets updates after you've shipped your app which is a maintenance nightmare.
- what’s different from doing web dev? or any dev for that matter.. they all have frameworks that require update or brake constantly. I think only windows have long lived legacy apps running on it. (although it is nice to have a static version of chromium to work with, for ~200mb)
  - 👉🏻 Users of desktop apps don't expect them to stop working after install! On top of that, updating desktop apps is nowhere near as simple as changing the source of your website.
- It's just extra work as well keeping up with a moving target. We've shipped Electron apps that don't require any maintenance and work for new customers years later.

# discuss-bundler/compiler
- ## 

- ## 🌰🍎 aionui打包 - [三天三夜，三更半夜 踩坑实录 _202602](https://linux.do/t/topic/1573468)
  - 本文记录了我在开源项目 AionUi（一个统一 AI Agent 图形界面）中遭遇的一次 Electron 打包白屏事故。从发现问题到最终定位根因，历时三天三夜。
  - 如果你也在用 Electron + GitHub Actions 做 CI/CD，这篇文章或许能帮你避开一个隐蔽的大坑。
  - 像往常一样推送了一个版本到 dev 分支，GitHub Actions 开始了它忠实的自动构建工作。十几分钟后，CI 亮起了绿灯 —— 所有平台构建成功。我下载了 macOS 的 DMG，拖进 Applications，双击启动, 白屏。没有报错弹窗，没有崩溃提示，就是一片白。
- 第一天：本地没问题，那一定是 CI 的问题。我的第一反应是 —— 先在本地复现。本地打包出来的 DMG 安装后运行完全正常。我打开 Electron 的开发者工具日志，终于看到了这个错误： Not allowed to load local resource: file:///Applications/AionUi.app/Contents/Resources/app/.webpack/renderer/main_window/index.html
  - ERR_FILE_NOT_FOUND——Electron 找不到渲染进程的入口文件。这个 index.html 是 webpack 打包生成的，没有它，整个界面就是一片白。
- 第二天：深入 asar 的内心世界。我从 CI artifacts 下载了 DMG，挂载后检查 asar。CI 打包出来的 asar 里压根没有 index.html！ 这意味着 webpack 的产物在 CI 环境下根本没有生成。但 CI 构建明明显示成功了啊？ 我仔细翻看了 CI 的构建日志。在数百行日志的角落里，我发现了 "FATAL ERROR: Ineffective mark-compacts near heap limit Allocation failed - JavaScript heap out of memory"。 Node.js 内存溢出了，webpack 在打包过程中吃光了内存，进程直接崩溃。
  - 但是 —— 为什么 CI 没有报错？答案就在 GitHub Actions 的 workflow 配置里， `continue_on_error: true` —— 这个设置的本意是：macOS 构建有时会因为 Apple 公证服务超时而失败，为了不阻塞其他平台的构建，设置了继续执行。 但它也悄悄地吞掉了 OOM 错误。webpack 崩溃了，HTML 没生成，但 CI 一脸无事地继续往下走，把一个残缺的产物打包成了 DMG 并上传。
  - Windows 和 Linux 的构建都正常，唯独 macOS 白屏。
  - 原因在于 Node.js V8 引擎的内存管理机制。V8 有一个人为设定的堆内存上限（64 位系统默认约 4GB），这个限制独立于物理内存。
  - GitHub Actions 各平台 Runner 虽然标称内存相同（7GB），但实际可用内存差异很大： macOS 系统开销 (~1.5GB), Xcode / 签名工具 (~0.5GB)， Node.js 可用 (~4.5GB)
  - macOS 系统本身就比 Linux 更 "臃肿"，加上 Xcode 工具链、代码签名服务等额外负担，留给 Node.js 的空间更少。当 webpack 打包一个包含 Monaco Editor、Arco Design、多个 AI SDK 的大型 Electron 项目时，内存消耗刚好卡在了 macOS 的临界点上。
  - 这也解释了为什么这个问题之前没出现 —— 随着项目不断壮大，依赖越来越多，webpack 的内存消耗在某个版本终于突破了 macOS 上的 4GB 天花板。
- 第三天：修复与反思
  - 修复本身只需要一行： NODE_OPTIONS: "--max-old-space-size=8192"
  - 这不是 "给 Node.js 更多物理内存"——Runner 的物理内存还是 7GB，不会凭空变多。 这是解除 V8 引擎的人为限制。告诉 V8：“如果需要，你可以用到 8GB”。实际上 webpack 只会用到它需要的量（约 5GB）。
  - 光修 OOM 不够。真正的问题是 continue_on_error: true 让构建失败变成了 "沉默的杀手"。
  - 我重写了 macOS 构建步骤，将公证失败和构建失败区分开来
- 这个 bug 之所以能藏这么深的根本原因 ——AionUi 的打包流程本身就不走寻常路。
  - 大多数 Electron 开源项目的打包流程是这样的： builder 或 forge
- AionUi 的打包流程长这样
  - 单独用 Forge 做不了完善的公证；单独用 electron-builder 又没有 Forge 的 webpack 集成好用。
  - 所以 AionUi 用了一个混血方案 ——Forge 负责编译，electron-builder 负责打包。
  - 问题就出在这里：Forge 和 electron-builder 之间没有原生的握手机制。Forge 编译完就完了，至于 .webpack/ 目录里到底有没有该有的文件，它不管。electron-builder 拿到 .webpack/ 就打包，至于里面是不是空的，它也不管。
  - 当 webpack 因为 OOM 中途崩溃时，.webpack/ 目录可能是 "半成品"——main 进程的代码可能已经编译好了（因为它先编译），但 renderer 的 index.html 还没来得及生成。electron-builder 照样把这个半成品打进了 asar，产出了一个 "看起来正常但其实没有界面" 的 DMG。
  - 这就是混血架构的代价：两个工具之间的信任边界，恰好是 bug 的藏身之处。
- 需要 Electron Forge 的原因： 
  - 它的 WebpackPlugin 对 Electron 多进程架构（main + renderer + preload）有开箱即用的支持
  - 开发时的 HMR 热更新、DevServer、日志端口管理都做得很好
  - FusesPlugin 可以在打包时控制 Electron 安全特性（禁用 RunAsNode、启用 Cookie 加密等）
- 需要 electron-builder 的原因：
  - macOS 代码签名 + Apple 公证（Forge 的 maker 支持有限）
  - 跨架构编译（在 arm64 机器上构建 x64 包，反之亦然）
  - 精细的 asar 控制（哪些模块打包、哪些解压、哪些排除）
  - 多格式输出（DMG + ZIP 同时生成）
  - 更成熟的 CI/CD 集成
- 原生模块：另一个深坑
  - AionUi 不是一个纯 JS 应用。它依赖了多个原生 C++ 模块：
  - better-sqlite3 — 本地数据库，存储对话历史和设置
  - node-pty — 终端模拟，用于运行 CLI AI 工具
  - tree-sitter — 代码解析，用于语法高亮
  - 这些模块必须针对目标平台和架构编译成 .node 二进制文件。在 afterPack.js 中，AionUi 实现了一套完整的跨架构重建逻辑
  - 这意味着一次 macOS arm64 构建实际上要经历：webpack 编译 → Forge 打包 → electron-builder 打包 → 原生模块重建 → 代码签名 → Apple 公证，六个步骤。任何一步失败都可能导致最终产物有问题。
- 为什么不简化？
  - Forge 的 maker 不支持 Apple notarytool — 这是硬伤，没法绕过
  - electron-builder 的 webpack 集成不如 Forge — 特别是多入口（main + renderer + preload + worker）场景
  - 原生模块的跨架构编译 — 需要精细控制，两个工具各自的方案都不够灵活
  - 安全特性 — Electron Fuses 只有 Forge 的 FusesPlugin 支持得好
  - 所以这个 "混血" 方案虽然复杂，但在当前的 Electron 生态下，它是 AionUi 这种重量级桌面应用的实际最优解。
- 经验总结
  - 1. continue_on_error 是一把双刃剑
  - 2. CI 绿灯 ≠ 构建成功
  - 3. OOM 是一个平台相关的 "薛定谔 Bug": 同样的代码，同样的 webpack 配置，在 Windows 不 OOM、在 macOS 就 OOM。它可能今天不出现，明天加了一个依赖就出现了。对于大型 Electron 项目，主动设置 --max-old-space-size 是一个好习惯，不要等到 OOM 了才想起来。
  - 4. 永远验证最终产物: 不要相信过程，要验证结果。在 CI 流水线里加一步检查最终产物是否存在且完整，能省去无数个排查白屏的深夜。
  - 修复只用了一行配置。但找到这一行的过程，让我深刻理解了一个道理： 最难调试的 bug，不是会报错的 bug，而是假装没有 bug 的 bug。

- ## [rspack support · Issue · electron/forge](https://github.com/electron/forge/issues/3450)
- there's a community rspack electron forge template
  - https://github.com/noshower/electron-forge-rspack-template

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

- ## 🆚 Made the hard decision to migrate a native (React Native Windows) app to Electron myself.
- https://x.com/birch_js/status/1988433012321853736
  - We could deliver more frequent updates
  - bugs went down dramatically
  - support calls went down
  - the customer got a far better product
  - easier to sell
  - 🤔 Disk and RAM bloat is a small price to pay in the face of that.

- Why not use something like Tauri which DOESN'T ship chromium?
  - Because Electron gives us production-ready clock-synchronised loopback audio + microphone recording on macOS, Windows, and Linux for free, all in under 100 lines of JavaScript code. System WebView wrappers like Tauri don't give that.

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
