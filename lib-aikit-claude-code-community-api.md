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

- [《 Claude Code 终极版 FAQ 指南 》 - 文档共建 - LINUX DO](https://linux.do/t/topic/803265)
  - 官网 / 中转站 / CCR 类自定义重定向 API 接入，在设定上有何区别
  - 官网：设定 HTTP_PROXY / HTTPS_PROXY 环境变量正常登录即可
  - 中转站：如无魔改 使用其提供的 api 端点地址和 key 设定即可
  - ANTHROPIC_BASE_URL (需是 Anthropic 形式接口)
  - ANTHROPIC_API_KEY (只有标准 Anthropic 填写此项)
  - ANTHROPIC_AUTH_TOKEN (有极高概率是此项)
    - 二选一而非可以共存
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
