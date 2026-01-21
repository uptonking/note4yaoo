---
title: lib-aikit-claude-code-community-api
tags: [api, claude-code, community]
created: 2025-12-18T12:26:14.630Z
modified: 2025-12-18T12:26:35.487Z
---

# lib-aikit-claude-code-community-api

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-reseller
- ## 

- ## 

- ## 🔡 [WONG公益站CC使用报错500 ](https://linux.do/t/topic/1332470)
- 我用的是 CC SWITCH，不指定模型可以使用了，但不知道为啥
- 我是’*-thinking’模型报错，不加 thinking 没有什么问题。

```JSON
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "sk-xxxxxxx",
    "ANTHROPIC_BASE_URL": "https://wzw.de5.net",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "claude-haiku-4-5-20251001",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "claude-opus-4-5-20251101-thinking",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "claude-sonnet-4-5-20250929-thinking",
    "HTTPS_PROXY": "http://127.0.0.1:7897",
    "HTTP_PROXY": "http://127.0.0.1:7897"
  }
}
```

- [【WONG公益站】关于claude code专用分组403的问题 _20251207](https://linux.do/t/topic/1282396)
  - 403 其实是 crs 的判断客户端不是 claude-cli 不可用，暂时先放开客户端限制，这是由于 new-api 不转发 user-agent 导致的。

- [【WONG公益站】终于折腾完了，签到已上线，已恢复2级注册限制（域名已更换，） _20251207](https://linux.do/t/topic/1282804)
  - 现在 claude code 专用分组仅限用于 droid cli, gemini cli, claude code 和 codex，优惠倍率 0.5。
  - 如果报错请去自己的日志看一下报错原因，403 就是客户端限制。
  - 纯萌新，我用的是 CCR ，claude code 倍率下会出现 403 是正常的吗 默认倍率是能使用的 
    - cc 有自己的格式，不需要 ccr

- [有使用Claude code的大佬吗，一直报403 - 开发调优 - LINUX DO](https://linux.do/t/topic/702742/76)

- ## [理一下 New-API 的协议转换：如何完美兼顾 Claude Code 和 Gemini 生图？ _202512](https://linux.do/t/topic/1354989)
  - 目前我在 VPS 上使用 New-API 来管理我的 AI 资源，上游主要是通过 cilproxy 转出来的 2api 以及站内的一些公益站（基本都是 OpenAI 格式）。
  - 上游： cilproxy (2api) / 公益站接口（OpenAI 格式）。
  - 中转管理： New-API。电脑端还用了 cc switch。
  - 下游终端：
  - Claude Code： 对协议要求极严，必须是标准的 Anthropic 响应格式。
  - Kelivo (或其他类似前端)： 主要用来聊天和 OpenAI 格式的 Gemini 生图。
  - 我发现 New-API 的“渠道类型”设置直接决定了最后的输出逻辑：
  - 渠道设为 Anthropic： Claude Code 配合完美，输出正常；但 Kelivo 的 OpenAI 生图请求会报错（因为协议路径或 Header 不对）。
  - 渠道设为 OpenAI： Kelivo 生图和普通对话正常；但 Claude Code 无法正常解析输出（或者是流式输出断掉）。
  - 这种情况是不是说明 New-API 在单一渠道下无法同时做到“向下兼容两种协议”？我现在只能同一个用 new-api 来使用 OpenAI 格式，然后单独用 2api 的接入 claude code

- 建两渠道最快，其他佬友分享了不少的工具，但是去找出来还是费点心思测试使用。
- 在newapi里建两个渠道就好了啊

- 两个渠道是一个 openai 一个 Anthropic  嘛？

- newapi直接用Anthropic 渠道就行了，cc就可以用了，之所以要两个渠道是因为我需要用openai接口来进行生图，所以才需要两个渠道，cc的话你只要在newapi里设置好渠道就行了，前提是你的上游要能支持这个格式，如果不支持的话还是得用ccr
  - 总结：如果你的上游不支持Anthropic 渠道的话，cc的话还是得用ccr，这是我目前试出来的

- 类似我这种情况，上游是国产模型商，例如deepseek是 openai格式的，哪怕new-api里设置了Anthropic 也是不行的咯。那么这个类型就只是个标记了，不具有转换能力。
  - 是的，因为你的上游没有转换能力，你可以试一下，大概率是不行的
- 我目前设置的渠道如图，可以看见CLI Proxy API我同时设置了两个渠道，但是Anthropic类型的渠道时gemini和Claude，下面那个openai的只有生图模型，这是因为生图模型只能用openai渠道才能正常生图，我的CLI Proxy API也有转换能力，就是不管是Anthropic的v1/message还是openai的v1/chat都可以发出请求，newapi也是同理，我用openai格式请求时，请求Gemini，在cherry studio等软件也是可以正常回复的，同时用claude code发出Anthropic的请求，也能有结果

- 我看了下目前的国产厂商都是支持A家格式的, 感觉是可以直接用啊。

- 
- 
- 
- 
- 
- 
- 

- ## 🧑‍🏫 [CLIProxy反代Antigravity + 接入claude code教程 _202512](https://linux.do/t/topic/1362485)
  - 认证成功后即可进入下一步，开始配置cc。建议使用cc-switch来管理配置
  - 需要注意Antigravity提供的opus模型的ID比较特别

- [[图文]手把手教你Antigravity反代，全程不用敲代码，小白也能看懂的保姆教程  ](https://linux.do/t/topic/1485942)
- [AntiGravity 2api claude code实战教程 ](https://linux.do/t/topic/1361784)
- [【使用CliProxyApi对Antigravity进行反代】实现多个ide之间共用模型  ](https://linux.do/t/topic/1373335)

- [根据佬们的经验, 自己写的反代Gemini CLI和Antigravity教程，感觉很好懂很详细 ](https://linux.do/t/topic/1371625?page=2)

- [即使模型自带联网功能，claude code也无法调用web_search吗？ ](https://linux.do/t/topic/1348078)

- [CLIProxyAPI获取免费api+cline配置代码生成 ](https://linux.do/t/topic/1348585)
  - zeabur 会有$5/月免费使用

- ## 🧑‍🏫 [《 Claude Code 终极版 FAQ 指南 》 - 文档共建 - LINUX DO](https://linux.do/t/topic/803265)
- 官网 / 中转站 / CCR 类自定义重定向 API 接入，在设定上有何区别
- 官网：设定 HTTP_PROXY / HTTPS_PROXY 环境变量正常登录即可
- 中转站：如无魔改 使用其提供的 api 端点地址和 key 设定即可
- ANTHROPIC_BASE_URL (需是 Anthropic 形式接口)
  - 直接接驳的 ANTHROPIC_BASE_URL 提供的服务必须是 Anthropic格式
- ANTHROPIC_API_KEY (只有标准 Anthropic 填写此项)
- ANTHROPIC_AUTH_TOKEN (有极高概率是此项)
  - 二选一而非可以共存

- [Claude Code小白指引贴（给完全不懂cc的小白佬友写的） ](https://linux.do/t/topic/1048674)
  - cc作为一个客户端，它只会发A社兼容的API请求，包括API规范/模型名称
  - 那么思路就是把格式兼容的问题解决，比如搭建一个中转站转换格式，然后去配置CC文件，比如很多公益站就是兼容oai和a社的格式的，为了兼容cc。
  - CCR是一个转换格式的路由器程序，安装完然后运行ccr code就会启动服务，然后CC 被设置为把 CCR 当作它的唯一对话目标，这个程序会一直运行一直转你发给cc的请求，并且接受模型发来的响应转给cc
# discuss-vendors
- ## 

- ## 

- ## 
# discuss-toolchain
- ## 

- ## 

- ## 

- ## [OpenPackage - A better, universal, open source version of Claude Code Plugins : r/opencodeCLI](https://www.reddit.com/r/opencodeCLI/comments/1qbqn96/openpackage_a_better_universal_open_source/)
  - We’re all familiar with Claude Code Plugins, which allows devs to package, share, and install sets of rules/, commands/, agents/, skills/, and MCP configs.
  - I wrote OpenPackage, an open source, universal, and arguably better version of Claude Code Plugins.
  - You can even install Claude Code Plugins to OpenCode, file conversions handled and everything
  - OpenPackage defines how plugins should be
  - P. S. I see a lot of people migrating from CC to OpenCode, you can use OpenPackage to migrate your configs easily (I’ll drop a guide for this soon)

- I’m working on a universal agent client and have been thinking about how I could support Claude Code plugins, but for all agents. This seems like what I would want to support in my project eventually
  - It took a lot of tweaking and so many iterations haha, need to thank my early users for the great feedback as well.
# discuss
- ## 

- ## 

- ## 

- ## 
