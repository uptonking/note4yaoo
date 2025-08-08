---
title: lib-ai-app-pm-products
tags: [ai, pm, product-hunt, products]
created: 2024-12-07T09:50:59.442Z
modified: 2025-03-22T16:10:24.856Z
---

# lib-ai-app-pm-products

# guide

# ai-dev-xp
- tips
  - aisdk + docs/excel/image

- agent-ipc

- markdown-stream

- ai-architecture: 与ai的通信和计算是在前端实现，还是在后端实现
  - 前端和大模型直接对接的缺点: 关闭页面会丢失数据
  - 消息持久化时，使用服务端id才方便消息保存与恢复、多人聊天一致性
  - ai在前端或后端的架构都和workflow工作流紧密相关

- 
- 
- 
- 
- 

# pm-mcp
- writing

- image-generation
  - 现在的ai产品很少将图片生成和编辑设计和实现的体验很好

- browser-use
  - computer-use
  - vscode-use, vscode-mcp

- ai-sandbox
  - 不仅用于代码，还可扩展到更多场景，类似manus
  - 在一台vm的前提下，能将ai执行任务的过程更具体的展示给用户，甚至邀请用户协作，甚至执行完将产物以用户熟悉的文件夹或预置软件打开给用户查看操作
# ai-editor
- drawio-use

- 不适合流式的数据
  - markdown-table
  - mermaid-graph
# ai-designing
- cursor for design: logo creator
  - 形态是否要基于vscode，产物是否要直接在vscode打开

- 使用ai实现高仿设计，是否可以绕过版权限制
# ai-lowcode

# ai-workflow

- n8n open alternative

- logicflow + ai
# ai-coding
- [Compare Top AI IDEs & Coding Assistants | 2025 Reviews & Alternatives](https://www.aiidecompare.com/)

```markdown
- apps,       tabs,  chats, pricing
- cursor,     2k,    50,    $20
- windsurf,   any,   100,   $15
- trae,       5k,    1000,  $10
- gh-copilot, 2k,    50,    $10
- gemini-cli, 180k,  240x30,$10/1M-tokens
·- amazon-kiro,any,   50,    $19   

```

- roadmap
  - 1. human-in-the-loop
  - 2. self-correction, auto-debug
  - 3. async-workflow
  - 4. idea-to-launch, 类似manusAi, 基于类似个人云桌面底层实现的助理
  - 5. value as a service

- 可以使用ai协助将代码库从一种语言转换到另一种语言
  - 甚至用ai将GPL协议的代码重写成自己的代码

- ai写与第三方sdk集成的代码时，先写注释example，再写代码
# ai-office
- 产品方向: ask、生成、集成

- google-docs-ai
  - [How to Use AI in Google Docs - Numerous.ai](https://numerous.ai/blog/how-to-use-ai-in-google-docs)

- notion-ai
  - [Everything you can do with Notion AI](https://www.notion.com/help/guides/everything-you-can-do-with-notion-ai)
    - Notion AI helps you find information, create content, understand data, and chat - without ever leaving Notion.
    - Analyze files and images
    - Access information across your integrated apps like Slack & Google Drive
    - Limit your search to trusted knowledge sources
# ai-dev-xp
- 当一个复杂问题让ai折腾了1h还没解决，不要继续纠结，赶紧换更强的模型
  - 让ai动手前自己先拆分任务，不要让ai分析复杂的任务，ai分析不清会乱改增加工作量，自己可以主动mock状态和对象
  - 有时使用搜索引擎默认的ai结果又快又好，可以尝试解决类似stackoverflow类型的问题

- 让ai将从日志平台复制来的残缺字符串补全为合法字符串并格式化缩进，速度很快很好用
# ai/llm-api
- [现在做大模型，还有靠谱且免费的 api 接口吗？ - 知乎](https://www.zhihu.com/question/662092970)
  - 纯粹免费的API也是有的，但是多限于轻量级的大模型，比如智谱AI的flash模型，Google的 Gemini 1.5 Flash。
  - 目前主流的 API 接口都是采用相同的套路，即免费注册送固定的额度，然后再收费的策略。我反正是没有看到纯免费一直可用的 API 接口。
  - DeepSeek和MiniMax是国内模型，包括其他厂商的国内模型也都有免费额度。不过Groq几个月来一直都是免费
  - Groq是一家美国AI芯片公司，专注设计高性能的AI处理器，目前借助自研的AI芯片LPU，每秒能够输出近500个token。和GPT-4，Gemini对标，同一个问题所需的时间，Groq完全碾压了其他两者，输出速度比Gemini快10倍，比GPT4快18倍。
  pm- Groq平台提供个人免费的API-KEY接口，不同的模型限制不同

- [Groq is Fast AI Inference](https://groq.com/)
  - Fast AI inference for openly-available models like Llama 3.1
  - Move seamlessly to Groq from other providers like OpenAI by changing three lines of code.
  - [On-demand Pricing for Tokens-as-a-Service](https://groq.com/pricing/)
  - [Groq公司推出的全球最快的大模型推理服务达到每秒输出500个token，如何看待这一技术？ - 知乎](https://www.zhihu.com/question/645010090)
    - 一句话来说，这个芯片就是玩了个用空间换时间的把戏，把模型权重和中间数据都放在了 SRAM 里面，而不是 HBM 或者 DRAM。
    - 这是我 8 年前在微软亚洲研究院（MSRA）就做过的事情，适用于当时的神经网络，但真的不适合现在的大模型。因为基于 Transformer 的大模型需要很多内存用来存储 KV Cache。
    - Groq 芯片虽然输出速度非常快，但由于内存大小有限，batch size 就没法很大，要是算起 $/token 的性价比来，未必有竞争力。
# ai-products-hunt

# more

# discuss-ai-pm
- ## 

- ## 

- ## "We now want to edit our *tools* as we have previously edited our documents"
- https://x.com/geoffreylitt/status/1646688665479831559
- "As we shape our tools, our tools shape us." 
- This is what makes tools like Notion and Airtable so powerful— they’re lightweight ways to build increasingly customizable interfaces with (albeit small) knowledge databases. As they get more flexible and can handle more data, I feel they’ll become essential parts of UI/UX design
