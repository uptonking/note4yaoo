---
title: lib-xplat-tauri-community
tags: [community, tauri]
created: 2023-01-14T17:21:39.551Z
modified: 2023-01-14T17:22:00.810Z
---

# lib-xplat-tauri-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## zed gpui 和 electron 就没啥可比性，gpui 里的 webview 依然是 system webview（套用的 tauri wry） _202511
- https://x.com/lencx_/status/1984833232664424704
  - [WebView | GPUI Component](https://longbridge.github.io/gpui-component/docs/components/webview)
  - 支持替换的 verso，真就比 chromium 强吗？
- [Experimental Tauri Verso Integration | Tauri](https://tauri.app/blog/tauri-verso-integration/)
  - Verso is a browser based on Servo, a web browser rendering engine written in Rust
  - https://github.com/versotile-org/verso /202510/rust/archived

    - Several major contributions from this project have been integrated into Servo
# discuss-alternatives-wails/like
- ## 

- ## 

- ## 

- ## [Wails? Why or Why Not? : r/golang _202503](https://www.reddit.com/r/golang/comments/1jkvym6/wails_why_or_why_not/)
- wails might be best in windows because native WebView is perfect there .. but in linux ? linux WebView is terrible. I don't have any others complaining about Wails yet

- I don't think you can use go as backend language in tauri right?
  - Nope. Tauri is all Rust.

- Wails is great in my case. I have a RESTApi server with web interface. And i dont need to create desktop app from scratch, just wrap frontend to Wails.

- Why = It is web based, easier to build complex gui application 
  - Why not = It is using system browser, almost all time it is good but sometimes occurs bug that never happen in your end.

- ## [We decided to use Golang with Wails instead of Rust with Tauri for building Krater desktop app. : r/golang _202311](https://www.reddit.com/r/golang/comments/17koicc/we_decided_to_use_golang_with_wails_instead_of/)
  - We were building Krater, a desktop app for debugging Laravel apps, with Rust using Tauri. However, this is no longer the case because a few months ago we made the decision to migrate the entire project to Wails
  - Better developer experience! Way easier to understand.

- whether you choose Fyne, Wails, or Tauri you'll still be way more lightweight than Electron

- We are using golang in production. It is simple and code looks fresh. In production its important that code must need to be understandable by other developers for long term maintainability. Though I appreciate rust for bringing new concepts

- I developed two project one on Tauri one on Wails, Wails is just enough for a desktop app based web. Tauri is intersted but in real life project it sometime take too much time to resolve a traditional issue (I faced with the CORS) To me, for now I will choose Wails for desktop app development.

- Rust's ability to interop fairly easily with C (and to some extent, C++ apis) can make tauri a good choice for adding a GUI layer to existing library projects

- Go's GC stops have minimal impact on those kind of standalone apps, because the UI is rendered in a webview, with its own JS process.  The STW only happens in the backend side, which won't be noticible given Go has optimised GC stops to sub millisecond

- ## [Comparison with wails · tauri-apps/tauri _202202](https://github.com/tauri-apps/tauri/discussions/3521)
- here is my take on WAILS/Tauri and Neutralino/NWjs as well.
- Uptil now NW.js has done this quite well - custom builds of the distributed binary can be done by developers if they wish (not necessarily easy) but otherwise apps can be developed using just HTML/JS/CSS/Node technologies. 
  - Core features such as windowing/notifications/events/etc are implicit within the binary but made available via the nw API to the JS/Node world so no need to get to grips with lower level languages such as C++/Rust/Go/etc. 
  - The downside of NW.js is the size of the shipped binary because a browser is always being bundled (Chrome).
- This led me to look at Neutralino/WAILS/Tauri which all offer the advantage of a vastly smaller shipped binary package by using the OS'es inbuilt webview interface.

- Neutralino (uses C++ for backend)
- Pros:
  - Easy to use with distributed compiled binaries. Server binary using C++ code and Client library using JS.
  - The server binary controls the Native API and core features and every HTML file in the app code need to reference the Client library to work with the Server binary via the Native API.
  - It has a CLI that will package app assets/resources into a file called resources.neu that can be used with the server binaries. App assets/resources can also be used as plain source along with the binaries and this is how I usually package my mac apps which can be done manually without toolchains.
  - This is an advantage for Neutralino because both WAILS and Tauri package the app resources within the shipped binary so compilation is required.
  - Mac app - resources can be available in Resources folder or as bundled package.
- Cons:
  - Native menus not available.
  - Newly introduced websocket not robust.
  - Lot of dependence on upstream libraries that don't get enough attention.
  - Multi-window management not implicit needs to be done by dev however can be done in JS using the API.
  - Node not supported directly - only via extensions somehow.
  - Raw binaries are produced (compilation is easy) but no packaging/bundling code is included.

- WAILS (uses Go for backend)
- Pros:
  - App bundling done with builds.
  - Go is meant to be easier than Rust from what I have heard (can't see until the dust settles on that one).
  - Main dev is very responsive to queries/etc.
- Cons:
  - Multi-window still on roadmap
  - Notifications still on roadmap
  - Native menus not available to JS context.
  - App bundling appears to only support modules for JS
  - Mac app - resources always compiled into binary rather than available in Resources folder.

- Tauri (uses Rust for backend - other languages on roadmap)
- Pros:
  - App bundling done with builds.
  - Native Menus supported
  - Multi-windows supported
  - Notifications supported
- Cons:
  - Native Menus require Rust coding
  - Multi-windows require Rust coding
  - Notifications require Rust coding
  - No DMG customisation
  - Mac app - resources always compiled into binary rather than available in Resources folder.
# discuss-issues
- ## 

- ## 

- ## 

- ## 🛢️ [FEAT: Use Tauri or Pake instead of Electron. · Issue · dbgate/dbgate _202409](https://github.com/dbgate/dbgate/issues/905)
  - Frameworks like Tauri/Pake give us the same product as Electron but better product.

- Probably this is not possible, because native DB driver packages have only support for electron, eg. SQLite here

- It's a pity, hopefully DB Drivers will provide more support in the future. Looks like we have to use pure Rust libraries. launchbadge/sqlx docs.rs/gluesql/latest/gluesql
# discuss-tauri-chromium
- ## 

- ## 

- ## [Is it possible to have Chromium bundled/used for a Linux build ? _202212](https://github.com/tauri-apps/tauri/discussions/5796)
- No. sidecars also don't help at all here. It would basically allow us to bundle a "normal" browser, but we can't use browsers as a tauri backend because we don't have any control over them. For what it's worth, we are somewhat actively researching our own webview which could be based on chromium too.

- ## [Bundle chromium renderer · Issue · tauri-apps/wry _202311](https://github.com/tauri-apps/wry/issues/1064)
  - The performances of WebkitGTK are really bad and the implementation often breaks. It is also hard to test for app maintainers since nobody really uses it outside of some obscure default browser. It is also not on the MDN compatibility list for API.
  - For better or worst, shipping a chromium renderer like electron does is the way all big companies ship their app today and the reason is simple: it works great. The experience is consistent for the user and it's not a pain to QA.
  - I think wry should support bundling a renderer.

- if Microsoft had any vision of would be awesome to have a webview2 standard across OS and it could be even a user setting (like use Firefox to provide webviews in my apps). Sadly we are not there yet.
- CEF work I think is the way to go. Even better if the user can patch the chromium version without us. I know that for security oriented OS (like Parrot OS) the maintenance of electron apps is annoying because they cant easily patch the browser in case there is a critical CVE.

- As a MacOS first shop I'd like to add that this isn't just a Linux issue - MacOS webviews are also wildly inconsistent.
  - Making the bundle just a bit smaller for a desktop app is outweighed by the simplicity and consistency of having Chromium bundled for many users imho.

- I guess iOS also suffers from the same webview issue. Though on the apple side, you may use html, js, css features that are available on the lowest macos version of safari.

- The solution is to to go with chromium until servo/verso gets stable enough, which will very likely happen earlier than webkitgtk becoming usable.

- How is electron faster at WebGL than CEF? (Sorry OT)
  - Other way around. Electron is faster than Tauri as it stands currently for doing any kind of 3D render through webgl. Tauri using CEF would fix that.
  - Dioxus is also showing some promise with the new WGPU Overlays.
# discuss-news
- ## 

- ## Tauri v2 正在大力开发移动端，我还没尝试不知效果如何
- https://twitter.com/lencx_/status/1778353417607676104
  - 桌面端是基于系统 webview（v2 比 v1 API 强了许多），移动端也是调用内置 webview 嘛？对系统 API 的控制权又有多少？
- 必定是 webview，和 capacitor 差不多
- 国内Rom碎片化太严重了，WebView也不能像原生Rom一样随时更新。

# discuss
- ## 

- ## Tauri 2 的权限系统太苛刻了。窗口默认不能拖动，sidecar (vendor binaries) 默认不接受参数，诸如此类
- https://x.com/_limboy/status/1894673659903852920

- ## 用 Tauri 在小型企业内部做工具会比较合适，大家的系统会比较一致，比如大多是Windows或者macOS之一。
- https://twitter.com/lencx_/status/1752973276018844061
  - 排查问题也更方便，直接怼到工位上。
  - tauri其实是个胶水层，由上游的 WRY 和 TAO 实现

- ## Tauri 看起来很不错啊！提前问一下，这个框架有什么坑么？
- https://twitter.com/beihuo/status/1724300870068953428
- 主要的坑在于各个系统上不同的 webview 的差异带来的一些问题。如果这方面能忍，这是一个不错的跨平台框架

- ## 如果你恨一个人，你就劝他把自己开发的跨平台软件从 Electron 切换成 Tauri 吧
- https://twitter.com/yetone/status/1643660861805043714
  - tauri renderer 层不同操作系统版本不兼容我理解，
  - 你 main 层的 Rust 跨平台库各个平台表现不一致就罢了，好的，我不跨平台了，找各个平台自己的库，结果压根儿编译不通过，我去提了个issue，结果告诉我这个库从2020年后就编译不通过了建议我换别的库，合着是得了个新冠呗，这种Rust库不止一个，都给我碰上了
  - 一直以来我都是花 80% 的时间来解决 Tauri 留给我的烂摊子，当然你也可以说你用 Tauri 很爽毫无问题，这也是我基于我当初使用 Electron 很爽的基础上得出的结论

- 感觉 aot 编译的语音都是这样，没有虚拟机抹平不同操作系统的差异

- 全部自己写 了解三大系统ffi 其实这个问题rn flutter都有只是那些大公司帮忙写完了 
  - electron毕竟有十年历史了 时间都花在plugin兼容了

- Tauri 在 Linux 下用的是 webkitgtk 引擎，这玩意性能很差，兼容性也不好。事实上 Rust 里面有很多东西是吹得过于神化了。比如 Alacritty(没有tmux它就是残废)， wezterm 性能比Gnome Terminal 还差，白瞎了用Rust

- 这就是历史轮回啊，Electron被发明出来，收获几万star，各大app不管用户骂都要切过去肯定是有原因的。以前基于webview的跨版本跨平台兼容性问题，基本上不是大公司玩不转的。用了electron等于chrome和node team一起帮你解决一大堆屎坑问题。Tauri这种历史倒车方案大概只能让最modern的平台体验好一点吧
- Tauri就是个玩具而已，这种开历史倒车的项目不知道怎么这么多人关注。用系统自带的浏览器，有无数的兼容性问题，根本解决不了。要不然当年electron也不会自带浏览器内核

- 一个连输入法都没解决的东西好意思发布？

- 被前端生态保护太好了是不知道其他静态编译语言的生态是有多限额，静态编译型语言生态尤其还要跨平台的，有一个算一个的坑，相比之下 rust 生态已经是最好的了。

- 你都用Tauri了，大多数功能都是WebView实现了，剩下的一些边角的东西就不要指望用Rust库解决了，直接用C/C++的库用FFI调用。Rust的FFI很容易并且没有开销。
