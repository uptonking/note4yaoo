---
title: lib-ai-app-community-gen-ui-site-design
tags: [ai, design, large-language-model, ui]
created: 2026-06-10T08:52:52.465Z
modified: 2026-06-10T08:53:24.884Z
---

# lib-ai-app-community-gen-ui-site-design

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-ui-examples/showcase 🌰
- ## 

- ## 

- ## 

- ## Open Design: Point. Comment. Mark. Edit. Capture and remix.
- https://x.com/OpenDesignHQ/status/2067192475853180997
  - Let AI design everything for you. Take control anytime.
  - Use Open Design inside Cursor. Or use it directly.

- @OpenDesignHQ do you natively support utilizing local LLMs ?

- ## [我的前端管理平台 shadcn UI开发最佳实践，写了很多个项目总结出来的最快，最没有AI味的管理UI设计方案 - LINUX DO _202606](https://linux.do/t/topic/2219562)
  - 如果大家不排斥这个shadcn的UI风格的话，所有的管理后台都可以采用shadcn来写
  - 先进入到这个shadcn的官网，然后找到这个能够安装一键初始化前端项目命令的地方：这个配置页面了就给了大家这个菜单、颜色，还有这个弹窗的一些配置，你可以在这里边去调整你想要的方案。下面有一个按钮 Get Code
  - 请使用此命令初始化一个shadcn ui的前端项目 pnpm dlx shadcn@latest init --preset b0 --template next
  - codex 插件里自带一个web 插件，叫Build Web Apps，里边有 shadcn/ui 的 Skill , 也可以直接安装它不需要安装shadcn的官方skill也可以。
  - codex会在调整UI的时候自动使用shadcn/uiSkill
  - 注意别让他在之前前端上重构，重构不太行，都是垃圾代码，最好就是新创建前端项目，然后让他迁移逻辑

- 我是用的semi design ，也提供接入mcp和skills 感觉差不多
# discuss-ui-gen 💄
- ## 

- ## 

- ## 

- ## 

- ## I'm completely convinced at this point that the "Command Palette" is a fundamental UI concept, and should be in all applications. 
- https://x.com/devongovett/status/2041378392570999200
  - It should also be a built in browser concept, there should be an API for websites to push items to the command palette ("new post", "muted words" etc)
- Another case of programmers making all UIs into a terminal. Command palettes are a huge UI cop-out. I hate apps that have commands that are only available in these things. Most people will never discover them. That’s why we invented menus and buttons. Design actual UI!

- macOS has had this for years, and it's scriptable via AppleScript. AppleScript's use is underrated, but (no doubt) it'll become a big part of Apple's soon-to-be announced AI integration into macOS.

- ## Claude交互式UI的原理分析和开源实现
- https://x.com/Gorden_Sun/status/2032829589253447985
  - 本质是工具调用，交互式UI的部分直接注入DOM渲染，没有使用iframe的方式，所以能实现流式渲染。为了保证渲染效果，严格限定了UI规范，例如禁止渐变和阴影等。
  - https://github.com/CopilotKit/OpenGenerativeUI 开源的这个方案就比较简单粗暴，直接使用了iframe，缺点是不能实时渲染且笨重，优点是兼容各家LLM。

- ## 逆向 Claude 的生成式 UI 架构，移植到 Coding Agent CLI ~ Pi
- https://x.com/shao__meng/status/2032649105852473365
  - Anthropic 为 Claude 推出了 generative UI 功能，对话中内嵌可交互的 HTML 组件（滑块、图表、动画），而非静态图片或代码块。 
  - @micLivs 对它的实现机制进行了逆向分析，并基于 Pi 和 Glimpse 将同一套能力移植到了终端环境。
- Claude Generative UI 的实际实现 -- 实现机制：不是 Markdown 渲染，是一个名为 show_widget 的 tool call，参数中携带 HTML 片段，由前端做 DOM 注入。证据——CSS 变量能跨组件解析、内容随 token 实时渲染、背景透明无 iframe 痕迹。安全边界靠 CSP 白名单限定可加载的 CDN。
  - 与 Artifacts 的本质区别：Artifacts 是侧边面板中可下载的交付物，用预打包库；
  - generative UI 是对话流内联的临时组件，可从 CDN 实时加载任意库。
  - read_me 模式：模型调用 show_widget 前必须先调用 read_me，按需加载对应模块的设计规范（diagram/chart/interactive/mockup/art）。这是渐进式上下文注入——基础 prompt 保持精简，专业知识按需加载，节省 token。
  - 设计规范提取：通过导出对话 JSON，从 tool_result 中提取了 Anthropic 完整的 72KB 设计体系原文。核心要求包括：流式优先（style → HTML → script）、禁用渐变/阴影/模糊、深色模式强制、9 条色阶体系、Chart.js/SVG 专用规范等。
- Pi 终端重建 -- 问题：终端无法渲染交互式 HTML。
  - 方案：用 Glimpse（macOS 原生 WKWebView，<50ms 启动，双向 JSON 通信）作为渲染容器。

- ## Anthropic shipped generative UI for Claude. I reverse-engineered how it works and rebuilt it for PI. _202603
- https://x.com/micLivs/status/2032244251464188184
  - Extracted the full design system from a conversation export. Live streaming HTML into native macOS windows via morphdom DOM diffing.
  - Built on @badlogicgames 's pi and @DanielGri 's Glimpse.
  - [Reverse-engineering Claude's generative UI - then building it for the terminal _202603](https://michaellivs.com/blog/reverse-engineering-claude-generative-ui)
- https://github.com/Michaelliv/pi-generative-ui /255Star/MIT/202603/ts
  - Claude.ai's generative UI - reverse-engineered, rebuilt for pi.
  - this cannot work on other harnesses because it requires access to the harness’s streaming layer (which pi natively provides, but other harnesses don’t).

- Isn’t it just MCP-UI?
  - no, the agent generates the ui ad-hoc. in mcp-ui, the mcp server injects an iframe into the agent ui.
  - because as per the spec, the UI is defined by the MCP server. the agent doesn't define it. it can only spawn it via a tool call.
- Can MCP UI render arbitrary html+js?
  - Json rpc can not a big deal

- morphdom for live DOM diffing is a great choice here. The fact that you can extract a full design system from a conversation export and rebuild it independently says a lot about how well-structured Anthropic's approach is. Open-sourcing the repo is a W.

- DOM diffing for live HTML streaming is a smart call — fast rendering without full re-renders. but the bigger shift is generative UI as a first-class interface paradigm rather than a party trick. curious how far the design system extraction can generalize across different apps.

- ## ⚖️ json-render now supports YAML as a wire format
- https://x.com/ctatedev/status/2032557225030664272
  - JSONL needs a full element before rendering
  - YAML is valid at every prefix, going from element-level to property-level
  - YAML looks like source code to LLMs
  - And we use 3 standards they know: JSON Patch, Merge Patch, Unified diff

- YAML being valid at every prefix is a bigger advantage than most people realize. Streaming interfaces get easier when partial state is already valid instead of waiting for a full object boundary. Curious how you handle patch ordering once multiple incremental updates arrive close together.

- Can this be done for SSR streaming? Or just client?
  - It's possible but haven't put together an example (yet)
  - It's just JSON + renderer

- Is this how Claude generates charts directly in the chat window now?
  - Claude writes raw html and hosts it in an iframe. Super flexible but slow and token heavy.

- https://github.com/lucianfialho/visual-yaml /apache2/202603/ts
  - The visual YAML editor. Schema-aware, embeddable, extensible.
  - Inspired by https://github.com/vercel-labs/visual-json /apache2

- https://x.com/dan_note/status/2032768253311721701
  - LiveRender now supports it too!
  - https://github.com/dannote/live_render/releases/tag/v0.5.0  /elixir-Phoenix
  - LiveRender. Format. YAML — YAML wire format with progressive streaming. The LLM outputs YAML inside a ```spec or ```yaml fence, and the streaming parser incrementally re-parses on each newline.

- https://x.com/0xblacklight/status/2032939792263164003
  - underrated aspect of YAML is that while JSON is ridiculously hard to parse and stream partial objects based on deltas for, YAML is easy. You just split on newlines.
- All json is valid yaml.
  - An incomplete multiline json object is not

- Isn't that the point of using json over yaml, where you don't want to accidentally partially parse anything?  The streaming capabilities come from yaml being weakly formatted

- What if the browser had a native yaml parser

- Python: bad because it depends on whitespace 
  - Yaml: good because it depends on whitespace 

- ts really not that hard to write a streaming JSON parser, the spec is simple compared to YAML. But yeah if you are trying to do it the naive way (run a full parse on every delta update) it doesn't work.
  - So just don't do that, write the streaming parser, and enjoy the simplicity of a much  smaller spec.

- i was just battling NDJSON
# discuss-site
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-ui-components
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-ui-testing
- ## 

- ## 

- ## 

- ## 

- ## [claude如何实现自动化流程测试呢（UI+功能） - LINUX DO _202606](https://linux.do/t/topic/2419475)
- 不管是playwright或者cdp, 都只能做浅一点的UI测试，看下我的  https://github.com/weekitmo/browser-cdp-enhancement  当然，这都是看模型的强度了，我这个指的是web上的，如果其他方面客户端的，还是得借助adb等工具，或者flutter的话现有应该也有对应的mcp或者skill

- 目前playwright mcp做自然描述语言自动化可行，设计测试场景，还是非AI时代的设计模式：setup、testcase、teardown。优点：零代码功底，不用维护脚本；缺点：烧token
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
