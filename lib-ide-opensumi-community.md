---
title: lib-ide-opensumi-community
tags: [community, opensumi, vscode]
created: 2024-07-29T03:05:10.429Z
modified: 2024-08-24T16:17:55.032Z
---

# lib-ide-opensumi-community

# guide

- pros
  - 开箱即用，使用方便
  - 功能丰富

- cons
  - lite纯前端模式下，内容全部存储在内存，需要手动持久化到localStorage
  - 纯前端模式不支持diff视图
# demos
- online
  - https://preview.opensumi.com/
  - https://opensumi.github.io/ide-startup-lite/

- web和lite示例都不使用http通信

- web示例使用socket通信传递文件内容，数据都存在localStorage
  - 每次切换文件，都会发送socket消息，切换之前打开过的文件也会发

- lite纯前端，无socket和http通信，数据都存在localStorage

-
-
-
-

# dev-xp

-
-
-
-
-
-
-

# docs

-
-
-
-
-

# discuss-stars
- ## 

- ## 

- ## 
# discuss-collab 🔀
- ## 

- ## 

- ## 
# discuss-storage 💾
- ## 

- ## 

- ## 
# discuss-codeblitz
- ## 

- ## 

- ## 

- ## codeblitz内置的BrowserFS，是否有自带的事件系统，监听文件变化？还是只能依赖VS code API的渠道自己手搓？
- `<AppRender runtimeConfig={{workspace: {onDidChangeFiles, onDidDeleteFiles} }} />` 可以获取到

- ## 要实现类似codereview的功能, 有可以参考的demo吗 _20250320
- 没有哎，这块集成代码我们没有开源
  - 可以实现的，就是加的代码有点多，我们内部就是基于codeblitz开源版做的

# discuss
- ## 

- ## 

- ## 
