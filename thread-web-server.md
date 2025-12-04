---
title: thread-web-server
tags: [server, thread, web]
created: 2023-04-24T15:43:37.001Z
modified: 2023-04-24T15:43:49.485Z
---

# thread-web-server

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-architecture
- ## 

- ## 

- ## 

- ## 

- ## 看起来现在都倾向于Node做前后端的全栈，如果项目涉及到重计算 / 调模型的部分，再单独起一个python/Go的worker项目，通过 HTTP / gRPC / 队列互相调用
- https://x.com/Jiaxi_Cui/status/1996564238551363676
- 没错，而且目前来看趋势更加极端，vibe coding出来的大部分初始项目舍弃server端，从纯edge functions开始构建
  - 是的，趋势是全都不自己做server，把这部分交给了saas，所以也不会用到GPU，甚至都不会用到服务器

- 借楼问一下，node一般怎么做负载扩容，是横向给k8s加pod还是用pm2垂直起多worker
  - 一般来说就是 k8s 的 ingress 到 pod，pod 里面启单进程
  - 或者是用 openresty 也行，直接到 pod
  - 如果是直接 ecs，那可以 pm2 启多个进程

- 结合bun被收购来看, ai coding时代, 技术栈会迅速大一统
# discuss
- ## 

- ## 

- ## 

- ## Flask 作者 用 Rust 写了个新的Python 包管理工具 
- https://twitter.com/chaojie_cn/status/1650322809930027008
- 我理解 conda 太偏向于数据科学、AI 等研究人员用，pip 只是个包安装工具，在项目管理上（比如打包、安装、依赖同步等等）太不方便了。
- 多年前学 python web 开发，用的是 Aaron Swartz 的 http://web.py 框架，那个时候整个框架只有一个文件，今天还可以下载到，不知道还能不能用
