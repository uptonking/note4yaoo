---
title: lib-aikit-aionui-community
tags: [aionui, claude-code, community, electron, large-language-model]
created: 2025-12-13T18:38:47.137Z
modified: 2025-12-13T18:38:59.837Z
---

# lib-aikit-aionui-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## [看到claude cowork，心态崩了一下午... AionUi还有必要发新包吗 _20260113](https://linux.do/t/topic/1443101/39)
  - 熟悉我的佬都知道我基于Gemini CLI改了个AionUi，做的过程中我感受到了这类Terminal Agent的可塑性，所以一直着想在此之上魔改出更适合通用场景的Agent，比如文档修改、excel数据分析、PPT创作 都能开箱即用，那是多么美好的画面啊
  - 所以我最近其实一直在倒腾Terminal agent的自定义，让用户魔改system prompt，Rule，MCP，Skills打包一个更开箱即用的场景，为此UI界面也在尽可能往这个形态靠拢，埋头苦干大半月，内置了一些办公类的Agent
  - 不能说一样，但是想做的功能极其相似，它还比AionUi好看，那…就太崩溃了
  - 其实这不是第一次了，我公司也有AI商业化产品，吭哧吭哧做了挺长时间，结果Claude一个更新顺手cover了，也是非常噩梦的回忆
- 早就不想搞ACP了… 只是有流量感觉挺好的就一直留着，最近一直在改第一版做的基于Gemini CLI的Core包和CLI包

- ubuntu安装windows无法预览，因为工作空间默认选择的是从服务端选择，所以确实没办法从windows上传，可以给webui加一个上传到服务器功能；
  - html/md这类文件是支持编辑的；

- 你这个还是免费呢 不止Gemini CLI, 还有Claude Code, Codex, Qwen Code, Goose Cli, Auggie
  - 其实不是，除了Gemini CLI是真的完全接管和复刻，其他几个全是ACP接入的，含金量不太高。 我好好打磨gemini cli的版本，学习成长也挺好

- 你这个真的可以的，针对现有非编程场景，把它搞个Skills的打包，那一以后可以在任何cli里面开箱即用，那就牛逼了，继续发力啊，大佬

- claude真的各种扩场景，连excel侧边栏、浏览器侧边栏都进去了，gemini也算是在模型和IDE上有了新场景突破

- 当然要做啦， 如今天下三分，Claude gemini ChatGPT， 你再好，我免费， 你大而强，我就小而美。 总有你的一席之地， 加油！大佬！
- 加油啊佬 opencode 也是在 cc 下杀出了一条血路
# discuss-roadmap
- ## 

- ## 

- ## 

- ## [Two functional requirements _202508](https://github.com/iOfficeAI/AionUi/issues/89)
  - Can you add a place to configure the GMEINI.md file, similar to the configuration rules in augment?
  - Can you develop a code index similar to the RAG feature in augment?

- better yet just follow agents.md . instead of multi gemini claude md

- 👷 202511: 
  - Request 1: Already on our roadmap! We'll support custom configurations, but tailored for office workflows rather than pure coding scenarios.
  - Request 2: We're taking a different approach. AionUI focuses on terminal agents with ReAct patterns, not IDE-style code indexing. We may revisit RAG if needed for office productivity use cases in the future.
# discuss-issues
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

## dev-log-aionui

- ## webpack > rspack
- npm run webui 会启动express server后端服务器 http://localhost:25808

- 前端使用不同端口时, chat history不会显示，因为存储在 localStorage ?
- 
- 

- ## params must have required property 'file_path'
  - 部分本地模型经常执行tool call失败，就出现此问题

- ## 使用claude-code-router全局激活的claude，~~会提示 Authentication required~~
- 无法复现, 几乎都能正常运行claude
