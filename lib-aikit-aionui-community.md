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

- aionui用claude code的时候，能不能自动把小任务分给haiku模型呀, 感觉好像现在开源的ui都不咋支持这个功能
  - aionui除了gemini cli是完全重构自主接管了（等于fork了一个从头到尾自己搭），其他的比如CC，Qwencode都是通过ACP协议接进来的，Aionui能自主控制的空间不大（就是个真UI壳子），所以如果CC不支持，aionui也支持不了

- 我其实研究过一段时间word的问题，不过我后面意识到，当AI更擅长写markdown的时候，会不会有一天，word这种xml格式会被世界遗弃，因为它复杂且AI不友好。基于这个思考，我不是特别想碰word，当然我也不确定自己的想法对不对
  - pandoc试过了，总的来说体验上不是特别丝滑，复杂格式保留还是差点意思，我之前尝试过用pandoc把word拆解成json配置，修改完后再还原，效果也不是特别好
- 我觉得是的，而且Latex数学公式的渲染在markdown下更加友好。但是现在被大多数人接受的还是word格式，所以还得做

- 我最近是魔改了Gemini cli，发现gcli的问题不少，和Claude code有本质上的差别
  - 是的，当初包gemini cli的主要原因是它是第一个开源的agent
  - 不过也完全够我学习了，我真是大开眼界。现在有更多资料对比，其实发现他们几家之间实现方式差别很多，连skills的实现方式都不一样。
- Gemini cli对任务安排以及工具并发上的处理不如Claude code。我当时拉取了一个cc的逆向产物kode和Gemini cli让codex作比较，codex就指出了类似的问题（当然具体是什么我有点忘了，但是记得很清楚的就是Gemini cli是串行架构，效率低，而Claude code好像串并行结合，效率更高）

- 

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
  - Request 2: We're taking a different approach. AionUI focuses on terminal agents with ReAct patterns, not IDE-style code indexing. 
  - We may revisit `RAG` if needed for office productivity use cases in the future.
# discuss-issues
- ## 

- ## 

- ## 

- ## 
# discuss-paseo
- ## 

- ## 

- ## [远程AI用Paseo还是mindfs  - LINUX DO _202607](https://linux.do/t/topic/2526142?tl=en)
- paseo 我一直在用 还行 自己内网穿透一下就可以 不用走他的中转。 我现在就在手机上控制

- 只用过 paseo，目前除了不能在对话框里使用 hermes 的所有命令，其他都挺好用的，现在都是挂在服务器上，全部远程访问了，也支持远程上传文件到对话框

- ## [佬友们有无好用的codex远程控制工具？ - LINUX DO _202606](https://linux.do/t/topic/2383965)
  - paseo 不太好用，官方 app 又因为没有国外手机号没办法做验证来绑定 codex 的 pc 端。paseo 是无法同步已有 codex 的会话，codex desktop 能用的一些模式在 paseo 也不可用。paseo app 在多会话同时运行的时候也会掉帧比较严重。 没有完美的远程控制貌似，尝试绕过 chatgpt 的手机号验证也会直接在会话和连接时失败

- 可以试下 happy coder，配置很简单，用着还可以。但是确实没有 gpt 移动端远控好用（如何能用的话）

- 我用 Hermes 成功控制了 codex cli，可以通过手机上的 TG 和 飞书来调用。不过回复很慢

- uu 远程？清奇的思路，但数据隐私问题？外加我是打算用安卓手机或 chromebook 远程控制，用这类软件控制不算好用

- ## [推荐一个软件 orca  - LINUX DO _202606](https://linux.do/t/topic/2495723)
- paseo 也很不错，但 paseo 的实现似乎是自己去实现各种 Agent provider 的调用，效果是界面效果比较统一。orca 是利用各种 agent 自己的 cli/tui+hook。
  - 在 pc 上我举得 orca 细节更美观一点，但我觉得 orca 多个项目一起用的时候，比较卡。

- paseo 三方 api 没法设置思考强度

- orca 好像走的是终端集成展示 cli 界面的路子。还有 aionui, codeg，这 2 个走的是 web 对接 cli，web 页面展示对话的路子。

- 优先 orca 吧，这个基本就是可远程连接的 tmux，实际手机连到电脑操作终端。因为封装比较轻，bug 应该会少一点。 其他都是 web 页面封装对话消息、管理 agent 进程，封装比较重。

- 这么多回复，就没有一个同行跟我一样用 warp 吗？这个也可以多开 agent，我用几个月了，opencode、kilo 等等同时撸代码

- ## [paseo工具挺好用的，更新频率也挺快 - LINUX DO _202606](https://linux.do/t/topic/2399702?page=2&tl=en)
- 最近用了 paseo，真的非常好用，已经是主力了。
我最满意的一点就是，它只是一个壳，不会自己整一些 Agent。在里面能用原汁原味的 Codex 和 Claude Code 这些。
然后 WSL 环境和 PowerShell 环境也能方便的分开。
官网的 Relay 服务器也挺快的，现在有事没事就用手机远程写命令，每日 Token 量一下子上去了。

- 这个确实是我用过最好用的。之前 happy 老连不上，hapi 能连上但是经常死会话，不知道为什么（而且很卡）。paseo 就是本地引用打不开看不到图

- relay 其实不太稳定，还慢，佬可以试试把他当最终的兜底，优先可以先用局域网内直连。其次使用 tailscale 的连接。我现在魔改 paseo 后，按照这个优先级自动切换，有局域网就优先局域网其次到 tailscale，最后才回退到 relay

- 我用的服务器 frp 出去，用起来挺稳的

- 别吹 paseo, 用它打开代码，连多行选定复制都不行，多少个版本过去了，连这么 low 的 bug 都没解决。
其次，复制网址去认证还要科学上网，一个开源软件有意思吗？
其三，我环境是 termux debian root 用户。创建一个 agent, 又有 root 问题解决，这破软件谁爱用谁用，反正我用 hapi。

- 这家内存占用比 happy 高一个数量级，小鸡根本受不了，还有一个将近 1g 的语音包，对磁盘又是爆杀，大盘鸡当我没说

- 不算吹 paseo 多牛多牛，只是说这个工具我用起来还可以，而且我常用环境是 windows，目前没遇到你说的这些问题

- paseo 让我感觉最不适应的一点就是他的侧边栏是和分支绑定的，而主流工具都是用会话显示在侧边栏里面的。

- 是可以自建 relay 的，官方提供的确实不稳定

- 内网穿透自己架啊，用 easytier。

- ## [I built a fully self-hosted and open-source Claude Code UI for desktop and mobile : r/ClaudeCode _202602](https://www.reddit.com/r/ClaudeCode/comments/1r8rqnv/i_built_a_fully_selfhosted_and_opensource_claude/)
- Really cool project. The relay for remote connectivity is probably the trickiest part of something like this -- how does it handle reconnections if the WebSocket drops mid-session? Like if you are on your phone and switch between wifi and cellular.
  - Mosh + tmux running on a sleepless server is the only way I've found to solve websocket drops.  
- Mosh is solid but there's nothing that Mosh does around connection stability that you can't replicate on top of WebSocket
  - Sure but doesn’t that require another brittle customization instead of using a tried and true pattern?
- the app will keep trying to reconnect until it finds a connection. you'll still be able to access your chats. it's resilient against connection drops

- how these claude code uis are working? does claude code have server mode, or using the agent sdk or some other black magic?
  - it's using agent sdk

- [I built an open-source app for Claude Code : r/ClaudeAI _202603](https://www.reddit.com/r/ClaudeAI/comments/1s4x9mb/i_built_an_opensource_app_for_claude_code/)
- it just launches the Claude Code program using the official Claude Agent SDK, it's as if you ran it yourself from the terminal
# discuss
- ## 

- ## 

- ## 

- ## 
# dev-log-aionui
- ## webpack > rspack
- npm run webui 会启动express server后端服务器 http://localhost:25808

- 前端使用不同端口时, chat history不会显示，因为存储在 localStorage ?
- 
- 

- ## params must have required property 'file_path'
  - 部分本地模型经常执行tool call失败，就出现此问题

- ## 使用claude-code-router全局激活的claude， ~~会提示 Authentication required~~ 
- 无法复现, 几乎都能正常运行claude
