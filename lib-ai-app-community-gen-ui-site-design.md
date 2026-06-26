---
title: lib-ai-app-community-gen-ui-site-design
tags: [ai, design, large-language-model, ui]
created: 2026-06-10T08:52:52.465Z
modified: 2026-06-10T08:53:24.884Z
---

# lib-ai-app-community-gen-ui-site-design

# guide

# benchmark-deisgn
- [Design Arena | Leaderboards ](https://www.designarena.ai/leaderboard)
  - [Human Evaluation of GLM-5.2 : r/LocalLLaMA _202606](https://www.reddit.com/r/LocalLLaMA/comments/1udaq2e/human_evaluation_of_glm52/)
  - this is what OpenRouter bases its benchmarks numbers on.. and it's human voting based
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
  - It works for web, desktop, and mobile prototypes today

- @OpenDesignHQ do you natively support utilizing local LLMs ?
  - Yes! Open Design supports local LLM workflows, including 22 local agent / model paths

- I really want an inspector window too, so rather than typing, I can change properties/styles just by toggling some values, like Figma or framer properties panel 

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
# discuss-ai-ui-toolchain
- ## 

- ## 

- ## 

- ## [gpt 写前端页面很丑怎么办？ - LINUX DO _202606](https://linux.do/t/topic/2480185)
- 训练数据就这样 skill都救不了 换claude 或者新一点的国模都比他好 不过据说快出的5.6前端很强

- 我是纯靠自己的审美来指挥它写页面。主要就是大量留白、极简主义，在复杂中建立秩序。

- 有一说一，感觉claude-design-skill或者claude本身的那个fronted-design也不好用。生成出来一股味儿，全是大块圆角棕色系方形block堆叠。但是抖音那个挺好用的 

- [各位佬们，我想问一下codex怎么使用前端页面才能好看呀 - LINUX DO _202606](https://linux.do/t/topic/2478236)
- 
- 
- 

# discuss-ui-testing
- ## 

- ## 

- ## 

- ## 

- ## [claude如何实现自动化流程测试呢（UI+功能） - LINUX DO _202606](https://linux.do/t/topic/2419475)
- 不管是playwright或者cdp, 都只能做浅一点的UI测试，看下我的  https://github.com/weekitmo/browser-cdp-enhancement  当然，这都是看模型的强度了，我这个指的是web上的，如果其他方面客户端的，还是得借助adb等工具，或者flutter的话现有应该也有对应的mcp或者skill

- 目前playwright mcp做自然描述语言自动化可行，设计测试场景，还是非AI时代的设计模式：setup、testcase、teardown。优点：零代码功底，不用维护脚本；缺点：烧token
# discuss-ai-design-system
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Vibe coding需要知道的设计术语——布局排版 - LINUX DO _202606](https://linux.do/t/topic/2480260)
  - [Vibe coding需要知道的设计术语——文字排版 - LINUX DO _202606](https://linux.do/t/topic/2431084)
  - [Vibe coding需要知道的设计术语——色彩系统 - LINUX DO _202606](https://linux.do/t/topic/2454227)

# discuss-cad/industrial
- ## 

- ## 

- ## 

- ## 

- ## [关于 LLM 理解/设计机械设计模型和图纸的讨论 - LINUX DO _202606](https://linux.do/t/topic/2477644)
  - 当前公司想要将机械设计的模型( *.prt, *.asm, *.drw, *.stp等)及CAD图纸(*.dwg, * .dxf等)全部归档并整理为知识库
  - SW 模型理解/分析 → 输出 Markdown 文件
  - CAD 图纸理解/分析 → 输出 Markdown 文件
  - SW 模型 / CAD 图纸相关知识库(RAG? 或上面两项转换出来的 Markdown 文件知识库?)
  - 机械建模/制图相对来说没有工程制图的要求高, 之前看了一些帖子是讨论工程制图的, 感觉工程安全性是 AI 没法理解和保证的, 所以想看看机械行业能不能引入这块内容

- 目前来说应该做不到吧，从本质上讲，设计模型图纸，cad图纸基本上都是属于公司内部资产，模型厂商基本都拿不到这些数据来做模型的预训练。这种医学图像差不多一个道理的，都是属于垂直领域。目前市面上的都是通用模型吧。
- 我觉得不可能，CAD 不可能被整理为 Markdown 文件，还能被 LLM 识别；先不谈cad to md能不能跑通，起码我见得到的CAD图纸都经不起仔细推敲的，充满逻辑矛盾和冲突的东西，是最不适合给AI调用的

- 我觉得你可以换一个思路，自己整理数据集，然后做模型微调的话，成本非常高。而且是一个黑盒，意味着你的投入不等于你的产出。可以很粗糙的理解为抽卡。
  - 我觉得你可以让现在比较厉害的ai。Coding Agent，例如 codex，Claude code。接满血版的大模型。去分析一下这种设计模型文件和cad图纸，底层都是用什么计算机语言渲染出图像的。
  - 如果现阶段的大模型，懂这门语言。那你可以尝试把你哪些不敏感的cad或者设计模型导出源代码给ai。试试看他能不能理解。
- 看相关讨论有些人说AutoCAD的接口很烂, 会导致 AI 很难去读懂图纸及使用工具, 头疼啊

- 纯机械结构的CAD图纸可能还好点，毕竟有很多行业通用设计标准AI可以参考。更难的是P&ID图纸，这玩意压根就没啥行业通行标准，基本是工艺设计人员个人想怎么画就怎么画。但这和普通AI绘图又不一样，普通绘图能看就行了，这个是真要拿去在三维真实世界里供项目落地的。

- github上看到过freecad的mcp项目，那么LLM就应该是可以理解CAD的。一个想法是先转通用格式，stp/igs等，之后导入freecad（或者其他有LLM接口的开源cad项目例如Vibe CAD ），那么LLM就可以理解，之后再做知识库供查询、修改或生成新设计。
  - 顺着这个思路我去检索了一下，已经有MechVQA（对机械图、工程图进行识别评估） DesignQA（对工程图规则理解）等项目，MechRAG应该是你最终想要的知识库系统，让LLM能统一访问和分析来自不同工程软件的多源异构数据。
- 三维/二维图纸让 LLM 理解现在还是比较难，这块做的最厉害的是国内的自动驾驶，必须要引入世界模型，否则 LLM 无法从本质上理解空间维度。

- AutoCAD 的社区 MCP 看起来也比 SolidWorks 成熟很多, SolidWorks 的社区 MCP 看起来都是刚搭起来的阶段
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
