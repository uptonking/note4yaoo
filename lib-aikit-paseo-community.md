---
title: lib-aikit-paseo-community
tags: [agent, community, paseo]
created: 2026-09-05T00:27:50.575Z
modified: 2026-09-05T00:28:04.965Z
---

# lib-aikit-paseo-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

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
