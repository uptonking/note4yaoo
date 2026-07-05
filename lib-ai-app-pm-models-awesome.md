---
title: lib-ai-app-pm-models-awesome
tags: [ai, awesome, large-language-model]
favorited: true
created: 2026-06-20T15:49:20.652Z
modified: 2026-06-20T15:49:57.019Z
---

# lib-ai-app-pm-models-awesome

# guide

# awesome-models
- core-features
  - 可采用基于backlink的架构来实现，而不是普通crud后端, 还能基于文档的架构统一writing和chat
  - latest-free-models today: free, paid(各种coding plan额度测算, 这就是信息差)
  - model-wiki+comparison: 最重要的部分是双链
  - model-bench with history
  - news-report/submit
  - alternatives: 和 股票分析类saas/huggingface/gitea 相似

- non-goals
  - comments: 类似editor的行内评论足够了，类似github-issues/discussion的评论太重了，不是当前重点

- features

## models-bases

- tips
  - 可参考crm的bases来实现本项目, people--project--meeting/deal ~ model--project--bench/news

- model-wiki
  - id
  - name + totalB
  - total parameters
  - active parameters
  - multimodal: image, audio, video
  - reasoning: no, always, togglable
  - Context length
  - ~~tool-use~~ 
  - MoE
  - embedding
  - branding
  - release-collection
  - Authors
  - release-date
  - license
  - is-open-model
  - model-weight-repo
  - content: description, usage, docs
- model-media
  - branding-logo
  - creator-logo
  - provider-logo

- model-news
  - news-date
  - provider
  - model
  - pricing
  - url
  - content

- model-bench-vendor
  - bench-name
  - bench-date
  - model-name
  - parameter1-2-3...

- model-quants
  - hosted-url: huggingface, modelscope
  - quant-size

- model-pricing
  - date-pricing...
  - type: offcial-release, latest, stable

- model-tips
  - unsloth-guide-docs
  - links-submit

## models-directory/catalog/registry

- https://github.com/anomalyco/models.dev /MIT/202511/ts
   - https://github.com/sst/models.dev
  - https://models.dev/
  - open-source database of AI model specifications, pricing, and capabilities
  - We also use it internally in opencode.

- https://github.com/janhq/model-catalog /202607/python
  - A curated catalog of Large Language Models (LLMs) sourced from the Hugging Face Hub, specifically designed for integration with the Jan application's model hub. 

- [LM Studio - Model Catalog](https://lmstudio.ai/models)
  - https://github.com/lmstudio-ai/model-catalog /inactive
- [Unsloth Model Catalog | Unsloth Documentation ](https://unsloth.ai/docs/get-started/unsloth-model-catalog)

- [Catalog of Large Language Models ](https://systems-analysis.ru/eng/Large_language_models:_Catalog)

- [AI Models Directory — Compare 280+ LLM Models | LLM Gateway ](https://llmgateway.io/models)
  - https://github.com/theopenco/llmgateway /AGPL+EE/202607/ts
  - https://github.com/theopenco/llmgateway/blob/main/apps/ui/src/app/models/page.tsx
  - open-source API gateway for Large Language Models (LLMs)
- [AI Model Directory — 300+ LLMs by price, region, ZDR | Opper AI ](https://opper.ai/models)
- 🆚 [DeepSeek V4 Pro vs Kimi K2.7 Code - AI Model Comparison | OpenRouter ](https://openrouter.ai/compare/deepseek/deepseek-v4-pro/z-ai/glm-5.2)

- [LLM Directory: All Local LLMs List ](https://apxml.com/models)
- [LLM Large Language Model Directory - DocsBot ](https://docsbot.ai/models)
- [LLM Model Card Directory ](https://www.prompthub.us/resources/llm-model-card-directory)

- [有没有一个网站收集顶级科技公司的大模型名单 - LINUX DO _202606](https://linux.do/t/topic/2488815)
  - [AI大模型列表 - 评测结果、参数与价格汇总 | DataLearnerAI ](https://www.datalearner.com/ai-models/pretrained-models)
- [Models Table (10, 000+ LLM data points) – Dr Alan D. Thompson – LifeArchitect.ai ](https://lifearchitect.ai/models-table/)
- [All Large Language Models Directory - All LLMs ](https://llmmodels.org/)
- [Design Arena ](https://www.designarena.ai/)

- [llm-stats AI Leaderboard 2026: Compare & Rank 300+ Top AI Models by Intelligence, Speed & Price ](https://llm-stats.com/)
  - Your idle credits are losing value every day. Connect them to LLM Stats and earn 50% on every inference request we route through your keys.

- [codingplans.cc — AI Coding Plans ](https://codingplans.cc/)
# model-api-resources
- [Model Pricing for Kilo Code – Compare LLM Model Pricing & Capabilities ](https://kilocodepricing.com/?freeOnly=1)
  - [I built a free Kilo AI model pricing browser - feedback welcome : r/kilocode _202606](https://www.reddit.com/r/kilocode/comments/1tvb84z/i_built_a_free_kilo_ai_model_pricing_browser/)
  - I pulled the live model list from `api.kilo.ai/api/gateway/models` and wrapped it in a quick browser.

- https://github.com/tashfeenahmed/freellmapi /12.3kStar/MIT/202606/ts
  - https://freellmapi.co/
  - OpenAI-compatible proxy that stacks the free tiers of 16 LLM providers (~1.7B tokens/month) behind one /v1 endpoint — plus any custom OpenAI-compatible endpoint. 
  - Smart routing, automatic failover, encrypted keys. Personal experimentation only.
  - Aggregate the free tiers from Google, Groq, Cerebras, NVIDIA, Mistral, OpenRouter, GitHub Models, Cohere, Cloudflare
  - Every serious AI lab now offers a free tier — a few million tokens a month, a few thousand requests a day. On its own each tier is a toy. Stacked together, they add up to roughly 1.7 billion tokens per month of working inference capacity, across 100+ models from small-and-fast to reasonably capable.
  - /v1/chat/completions and GET /v1/models work with the official OpenAI SDKs and any OpenAI-compatible client 
  - /v1/responses (the wire format current Codex CLI versions require) is implemented as a translating shim over the same router, with full streaming events and tool calls.
  - /v1/messages (plus /v1/messages/count_tokens) speaks Anthropic's wire format over the same router
  - /v1/images/generations and POST /v1/audio/speech route across the providers that serve media models. 
  - /v1/embeddings with family-based routing: failover only ever happens between providers serving the same model
  - Automatic fallover — If the chosen provider returns a 429, 5xx, or times out, the router skips it, puts the key on a short cooldown, and retries on the next model in your fallback chain (up to 20 attempts).
  - Admin dashboard — React + Vite UI to manage keys, reorder the fallback chain, inspect analytics, and run prompts in a playground
  - Not yet supported
    - n > 1 (multiple completions per request)
    - Per-user billing / multi-tenant auth — single-user by design
  - https://x.com/geekbb/status/2069978295320690888
    - 这玩意有融合模式，可以让一组模型并行作答，再由评审模型综合出更优的答案。
    - 只是 API key 要一个个添加有点麻烦，作者可能也没想到有些人有几百上千个 key

- https://github.com/12britz/awesome-free-models /202606
  - A curated list of free AI models, APIs, and tools you can use without paying a cent.

- https://github.com/cheahjs/free-llm-api-resources
  - services that provide free access or credits towards API-based LLM usage.
  - https://github.com/ShaikhWarsi/free-ai-tools

- https://github.com/vava-nessa/free-coding-models /202606/js
  - https://freecodingmodels.vercel.app/
  - Find, benchmark and install in CLI 170+ FREE coding LLM models across 15+ providers in real time
# awesome/leaderboard/benchmark
- https://github.com/wenbochang888/github-trending-spider /20.8kStar/MIT/202606/ts
  - https://newsnow.busiyi.world/
  - 优雅地阅读实时热门新闻
  - 当前版本为 DEMO，仅支持中文。正式版将提供更好的定制化功能和英文内容支持。
  - 支持 GitHub 登录及数据同步
  - 根据内容源更新频率动态调整抓取间隔（最快每 2 分钟），避免频繁抓取导致 IP 被封禁
  - 本项目主推 Cloudflare Pages 以及 Docker 部署， Vercel 需要你自行搞定数据库，其他支持的数据库可以查看 https://db0.unjs.io/connectors 。
  - roadmap
    - 多语言支持（英语、中文，更多语言即将推出）
    - 个性化选项（基于分类的新闻、保存的偏好设置）
    - 扩展 数据源 以涵盖多种语言的全球新闻

- https://github.com/wenbochang888/github-trending-spider /MIT/202606/python/vue
  - https://www.gdufe888.top/ai/
  - 每日AI前沿信息。开源趋势、社区热议、AI 动态
  -  每日自动爬取 GitHub Trending、Hacker News、TLDR AI、OpenAI、Anthropic、InfoQ AI Development 等信息源，通过 GitHub Models API (GPT-4o) 生成中文摘要，提供 FastAPI 只读接口和 Vue 前端资讯流页面。
  -  历史归档 最近 7 天，不包含今天。选择日期后读取当天历史资讯。
  -  [【开源自荐】AI信息，自动爬取 GitHub Trending、Hacker News、OpenAI、Anthropic、InfoQ AI 等AI信息 - LINUX DO _202606](https://linux.do/t/topic/2300464)

- https://github.com/SWE-bench/SWE-bench /MIT/202603/python
  - https://www.swebench.com/
  - SWE-bench: Can Language Models Resolve Real-world Github Issues?

- https://github.com/sierra-research/tau2-bench /MIT/202606/python
  - https://taubench.com/#leaderboard?benchmark=text
  - A Benchmark for Tool-Agent-User Interaction in Real-World Domains
  - https://github.com/sierra-research/tau2-bench/tree/main/web/leaderboard
    - The leaderboard accepts model evaluation results through pull requests for both text (standard) and voice (audio-native) modalities.

- https://github.com/harbor-framework/terminal-bench /apache2/202601/python
  - https://www.tbench.ai/
  - A benchmark for LLMs on complicated tasks in the terminal

- https://github.com/run-llama/ParseBench /apache2/202606/python
  - https://parsebench.ai
  - a benchmark for evaluating how well document parsing tools convert PDFs into structured output that AI agents can reliably act on.

- https://github.com/getomni-ai/benchmark /MIT/202510/python/ts
  - https://github.com/getomni-ai/benchmark/tree/main/dashboard  /streamlit
  - https://getomni.ai/ocr-benchmark
  - A benchmarking tool that compares OCR and data extraction capabilities of different large multimodal models such as gpt-4o, evaluating both text and json extraction accuracy. 
  - The goal of this benchmark is to publish a comprehensive benchmark of OCRaccuracy across traditional OCR providers and multimodal Language Models. 

- https://github.com/NanoNets/idp-leaderboard-benchmarks /apache2/202603/python
  - https://idp-leaderboard.org  /排行榜白色ui友好
  - An on-premises, OCR-free unstructured data extraction, markdown conversion and benchmarking toolkit.
  - 排行榜的ui和数据似乎未开源
  - Running Benchmarks via LiteLLM (GPT, Gemini, Claude, etc.)

- https://github.com/jeinlee1991/chinese-llm-benchmark /NonOpen
  - https://nonelinear.com/
  - 非线智能 NoneLinear - ReLE评测：中文AI大模型能力评测（持续更新）

- https://github.com/alvinreal/awesome-opensource-ai /CC0/202606/python/简单列表
  - https://awesomeosai.com/
  - Curated open-source artificial intelligence models, libraries, infrastructure, and developer tools.

- https://github.com/benchmark-action/github-action-benchmark /MIT/202605/ts
  - https://benchmark-action.github.io/github-action-benchmark/dev/bench/
  - This repository provides a GitHub Action for continuous benchmarking. If your project has some benchmark suites, this action collects data from the benchmark outputs and monitor the results on GitHub Actions workflow.
  - This action can store collected benchmark results in GitHub pages branch and provide a chart view. Benchmark results are visualized on the GitHub pages of your project.
  - This action currently supports the following tools:
    - cargo bench for Rust projects
    - go test -bench for Go projects
    - benchmark.js for JavaScript/TypeScript projects
    - pytest-benchmark for Python projects with pytest
    - JMH for Java projects

- https://github.com/pingcap/ossinsight /apache2/202402/ts
  - https://ossinsight.io/
  - OSS Insight is a powerful tool that provides comprehensive, valuable, and trending insights into the open source world by analyzing 5+ billion rows of GitHub events data.
  - OSS Insight's Data Explorer provides a new way to explore GitHub data. Simply ask your question in natural language and **Data Explorer will generate SQL** , query the data, and present the results visually.
  - Simply ask your question in natural language and Data Explorer will generate SQL, query the data, and present the results visually. 
    - It's built with Chat2Query, a GPT-powered SQL generator in TiDB Cloud.

- https://github.com/iloveitaly/openbook /MIT/202310/ts/inactive
  - https://www.dolthub.com/repositories/iloveitaly/venture_capital_firms
  - Like pitchbook, but open. An open source investor/venture capital database
  - Open source databases have always been interesting to me. There's lots of open source code, but not much open source data. 
  - Scraping with GPT: This repo has some interesting code which uses langchain + openai to return JSON results from a webpage by converting the raw HTML to simplified markdown. 
  - 仓库代码是爬取公司数据并清洗
# ai/llm-api 👾
- api-choices
  - 支持热门模型、vlm
  - api稳定: production用的api稳定性必须要高，否则产品体验差
  - 速率限制
  - 工具集成支持: cline, roo, librechat
  - 另一种思路， 新开的商业站一般会限免最新的模型和热门模型，也可以用来测试
- 不要在公益站浪费过多时间, 工作状态需要稳定和高效, 折腾公益站经常打断核心任务
  - 可尝试直接购买付费中转站， 注意跑路
  - 可采用类似 opus+sonnet+haiku 的 顶级+主流+轻量 组合架构
    - 一种轻量token方案: 使用gpt/中转站作为类似sonnet的高级模型, 类似haiku的普通模型可用nvidia/openrouter/ollama/opencode/longcat
  - 跳蚤市场经常有临期或拼车的惊喜
  - 少数公益站支持投喂 plus 来换取无限额度1天的套餐， 在token需求大时可考虑付费支持以小换大
  - 部分公益站和token-hub支持用LDC换低倍率的模型，可在ldstore用商品换LDC，再用LDC来换低倍率套餐
  - 注意不同来源的号池不要混用， 否则会出现问题 Encrypted content could not be decrypted or parsed
  - 公益站多帐号的兑换码一般未与用户绑定，可以兑换到其他用户，甚至延迟兑换，这样可以将兑换码的额度接力使用而不触发限流
  - 在ldstore卖兑换码的公益站就是活着的，按销量排序就能去试用了

- [最新跳蚤市场话题 - LINUX DO ](https://linux.do/c/trade/10)
  - [最新积分乐园话题 - LINUX DO ](https://linux.do/c/credit/106)
  - [LD士多 - LinuxDo站点积分兑换中心](https://ldcstore.com/)
    - [LD士多 - LDC积分商城](https://ldst0re.qzz.io/)

- token-news
  - [商汤送免费的glm5.2了 - LINUX DO _202607](https://linux.do/t/topic/2504080)
  - [每月50刀免费额度 支持glm5.2 邮箱注册即可 - LINUX DO _202606](https://linux.do/t/topic/2489020)

- claude-news
  - [Ollama v0.14.0 and later are now compatible with the Anthropic Messages API _202601](https://ollama.com/blog/claude)
  - [魔搭免费api接口支持Anthropic API可直接用于claude code附教程 _202508](https://linux.do/t/topic/876488)
    - 模型库里面有的模型可能不支持，k2好像也不行，试了glm4.5和qwen3都可以

- [Token HUB](https://hub.linux.do/), 封号严重
  - 部分公益站和token-hub支持用LDC换低倍率的模型，可在ldstore用商品换LDC，再用LDC来换低倍率套餐
  - hub.linux.do深夜福利的cc倍率也能达到0.02, 而付费的cc普遍在0.3, 所以可以适当留好余额在hub用cc
  - [讨论token银行的可行性 - LINUX DO _202604](https://linux.do/t/topic/2007302)
  - [L站的活跃佬友永远也不缺token花了，token自由已实现 _202605](https://linux.do/t/topic/2111825)
  - 置换的总体思想就是将你闲置的订阅套餐、朋友赠送的 Key、公司发的额度——闲着也是浪费。把它们上架成公开渠道，换成可以继续消费的 credits
  - 其实这样会有一个弊端，肯定会出现拿次要模型换取好的模型，感觉会出现最后一堆好模型的供不应求，hub中又会存在大量无法消费的次要模型
  - https://github.com/lhish/hub_pro
    - 一个用于 Linux.do Hub Marketplace 的用户脚本，主要增强 Channel Hub 的筛选和浏览体验
    - [【hub_pro：一个强大的hub.linux.do站的增强工具,解决大部分hub站痛点】<channel一页全部显示，根据热门度排序，根据接口筛选，根据支持模型筛选，只查看free channel，显示channel所有可用模型>  - LINUX DO _202604](https://linux.do/t/topic/2060896)

- [RawChat公益站点](https://chatgptplus.cn/)
- 免费的共享ChatGPT账号
  - [RawChat公益站点 ](https://sharedchat.cc/)
  - [RawChat公益站点](https://sharedchat.fun/)
  - https://new.sharedchat.cc
    - [codex公益站已开 继续每人免费100刀   _202605](https://linux.do/t/topic/2260900)
    - 关t子或者用非us节点访问，ccswtich的不要获取模型，手填模型可以直接用

- 中转站
  - 不需要用自己的gpt/claude账号
  - 不需要网络代理
  - 个人帐号在内地使用顶级模型时，经常触发风控/KYC， 使用中转站的api很少碰到此问题

- tips: 公益站不稳定(3个月就倒闭一批), 来源不明可能导致效果差, 需要经常确认和维护, 不要浪费过多时间
  - 🤔 一种思路: tool-call时使用擅长tool-call的模型，分析时使用公益站的聊天优质但无法tool-call的模型
  - 🤔 与其花时间签到游戏，不如研究2api和反代; 比较 公益站的配置折腾 / 反代的配置及更新
  - coding方案还可使用 ccr 转换 qwen-code-cli
  - 是否需要统一管理公益站，不同站点的安全盾绕过方式不同，模型名不同，api分组名不同，key的有效期不同
  - 有的api不能显示thinking内容
  - 模型不断更新，落后的公益站会逐渐淘汰
  - 公益站主页模型广场展示的可用模型不准确，可以在控制台的playground直接测试，异常会直接抛出
  - 公益站api稳定性较差，顶级模型难获取或很慢，集中工作阶段稳定性最重要
- 免费api的技巧: 在知乎/小红书直接搜索 免费 claude (公益站), 就会有最新的api推广信息, 可以用小号邀请自己
  - 公益站 [Search results for '公益站' - LINUX DO](https://linux.do/search?q=%E5%85%AC%E7%9B%8A%E7%AB%99%20order%3Alatest)
  - [L站免费AI汇总 ](https://linux.do/t/topic/638821)
    - [LD OPEN HUB — 公益站导航](https://ldoh.105117.xyz/)
    - [站内公益站汇总 ](https://linux.do/t/topic/1398351)
      - 👀 不要花费过多时间，有站点会不定期清理不活跃账号，如 windhub/Fovt
    - [模型中转状态检测](https://check.linux.do/)
    - [L站的佬友们应该早已经 token 自由了吧 ](https://linux.do/t/topic/1397594)
    - [最新福利羊毛话题](https://linux.do/c/welfare/36)
    - [All-API-Hub：开源AI中转站集中管理和自己的New API增强管理，基于 one-api-hub 大幅重构增强 _202511](https://linux.do/t/topic/1001042)
    - [关于部分公益站支持CC的测试，欢迎更多反馈 ](https://linux.do/t/topic/1162888)
  - 📌 [duckcoding 公益站](https://free.duckcoding.ai/console/personal), 签到
    - [DuckCoding](https://www.duckcoding.ai/console/personal)
    - [DuckCoding Az-CC，单独开启公益站，只允许L站注册 ](https://linux.do/t/topic/1308120)
    - [status](https://status.duckcoding.com/status/duckcoding)
  - [Compute Token](https://computetoken.ai/console/personal)
    - [【正式上线】Compute Token —— 是大家推着我们走到这里 _202603](https://linux.do/t/topic/1772654)
    - 正式上线付费版，但公益的精神不丢。每天签到送额度
  - 📌 [君の的公益](https://muyuan.do/console/personal), 签到额度少
    - [『高级推广』『君の公益』Claude渠道恢复  ](https://linux.do/t/topic/1853293)
    - 仅支持Claude Code
    - [「慕鸢の公益站」](https://newapi.linuxdo.edu.rs/console/personal)
    - [星辰·AI ](https://ai.centos.hk/pricing), 无签到， 支持对公转账和发票
  - 📌 [Any Router](https://anyrouter.top/), 每日签到获取$25
    - 仅支持coding工具，不支持使用api聊天
    - 本站直接接入官方 Claude Code 转发，无法转发非 Claude Code 的 API 流量
    - 无充值，邀请注册来获得更多额度
    - tg群讨论的内容看，作者似乎精力不在anyrouter而在开发商用产品
    - 用户较多，有提供vscode插件无法使用的解决方案
  - [Agent Router](https://agentrouter.org/console), 每日签到
    - 转向商业了
    - 模型支持 Claude Code、Codex、RooCode、Qwen Code、Gemini Cli 等多款工具， 仅支持coding工具，不支持使用api聊天
    - > 签到功能在哪里呀？ 退出登录重新登陆就好了. 
    - [AgentRouter 问题汇总 · Issue · millylee/anyrouter-check-in](https://github.com/millylee/anyrouter-check-in/issues/48)
      - agent 是在登录的时候签到的，并没有额外的 sign_in 接口，是在登录的那个接口是返回了一个check_in 的字段判断的，所以才把cookie 时间给调短了，就是让重新登录签到才有效
  - [Kiro-Go Contribute _202604](https://sub.timefiles.online/contribute)
    - [[Kiro Free Contribute] 一个不常规的公益站开放 · 每小时免费kiro 试用号反代 · kiro账号无偿托管服务  ](https://linux.do/t/topic/1971059)
    - 每小时更新一个新apikey,前40分钟会使用AI自动生成的字谜加密，后20分钟密文会解开，可以直接查看
  - [Code Router](https://api.code-relay.com) , 无法签到和更多额度
    - [Code Router](https://api.codemirror.codes/)
    - 支持 Claude Code & CodeX
  - [SWT-API](https://api.lhyb.dpdns.org/), 无限额度, 无需签到
    - [备用站](https://new-api.koyeb.app/)
    - [免费众多模型公益api站  ](https://linux.do/t/topic/1106811)
    - 公益站干一两年了，都是白嫖的api
    - 现在Gemini的模型都用不了了，我也进不去主站了，副站也进不了，备用站无法登陆
    - [200刀用完关停](http://152.136.137.130/pricing)
  - [123nhh](https://new.123nhh.xyz/pricing), 余额多
    - 模型来源谷歌反重力，rpm限制10/3min，不可用于NSFW，酒馆等
    - 模型不稳定，经常异常再恢复再异常
    - [【nhh公益站】介绍贴及主贴  ](https://linux.do/t/topic/1370326)
    - [模型中转状态检测](https://status.123nhh.xyz/)
  - 📌 [Wind Hub](https://windhub.cc/console/personal), 农场
    - https://api.224442.xyz/panel  /legacy
    - [福利站](https://wcdk.224442.xyz/)
    - 提供了free分组，包含deepseek-v3.2, gpt-4.1-mini
    - cc分组倍率0.6
    - 活跃任务检测：窗口=600s，活跃任务槽位=8（阈值>5），疑似异常并发/自动化（辅助指标）
    - [[Wind Hub]新的公益API 主帖 ](https://linux.do/t/topic/1344450)
  - 📌 [薄荷 API](http://x666.me/console), 每日签到
    - 改了下速率限制。现在变成5分钟25次，对自动化和roocode这些用户变好了很多
    - [薄荷公益站签到](https://up.x666.me/), 模型一次调用 0.002
    - 模型丰富: claude, gpt, gemini
    - [薄荷公益站主贴 ](https://linux.do/t/topic/1170760)
    - 支持cline/roo/cc
    - Gemini 的模型是支持三种格式的： Gemini 格式（带原生和搜索）, OpenAI 格式, Claude 格式（能 CC？）
    - 反重力和veterx逆向的锅，claude对open ai格式调用问题，用cline系的产品吧，比如roo或者kilo
    - [请问薄荷怎么才能用Claude Code ](https://linux.do/t/topic/1304580)
  - 📌 [WONG公益站](https://wzw.pp.ua/console/topup), 每日签到
    - [WONG公益站](https://wzw.de5.net/console)
    - [WONG公益站](https://newapi.netlib.re/)
    - rpm为30
    - 高效连接 Claude Code CLI
    - [【WONG公益站】弄个主贴 ](https://linux.do/t/topic/1179964)
    - 不要对模型进行测试，测试失败不是因为服务不可用，是我禁掉了测试
  - 📌 [随时跑路公益](https://runanytime.hxi.me/console/personal), 每天签到
    - [随时跑路福利站](https://fuli.hxi.me/wheel)
    - RPM 暂时定为 5，之后看情况调整
  - 📌 [Elysiver](https://elysiver.h-e.top/console/personal), 站内签到
    - 支持embedding model
    - [模型健康度监控](https://elysiver.h-e.top/model-health)
    - [Elysiver 添加 Nanobanana Pro 啦 _202601](https://linux.do/t/topic/1506018/16)
      - 是 business 2api
    - [『Elysiver公益站主贴』 ](https://linux.do/t/topic/1175087)
    - 2cx 指接入 Codex 使用
    - docs 指的是这是 claude 的文档 ai，不破限只会回答文档相关的内容
  - 📌 [ Alpha _202605](https://gw2.oops.asia/dashboard)
    - [『Alpha』公益站开站 _202605](https://linux.do/t/topic/2242621)
    - [兑换码商店 · Alpha Codex](https://shop.oops.asia/)
    - 不限量套餐: 限时、限并发
  - [123nhh API ](https://api.123nhh.com/profile), 只能签到得额度
    - [[nhh站]随时跑路和关闭注册 _202606](https://linux.do/t/topic/2468396)
  - [Dk _202606](https://apideepseek.com/console/personal)
    - [DeepSeek公益站！支持缓存，完整原生支持 - LINUX DO _202606](https://linux.do/t/topic/2302675)
    - 10 LDC : 1 元用量 【DeepSeek 0.5倍率】（相当于 5 LDC = 1 元用量）
    - 渠道：第三方平台 + DeepSeek 官方API 兜底
    - 无签到，仅LDC兑换，用多少换多少
  - [九幺 7r.fit ](https://api.7r.fit/console/personal)
    - 价格贵
    - [【九幺】我们也有claude了 ](https://linux.do/t/topic/2439721)
  - [SunRouter _202605](https://sun.meowai.net/console/personal)
    - [SunRouter 公益站，来源bai号池，无限 gemini ](https://linux.do/t/topic/2114421)ƒ
    - 限制每用户rpm为30，enjoy
  - [GPT Pool _202605](https://gpt-pool.com/)
    - [[GPT Pool]临时开放 LinuxDO Connect 注册 _202605](https://linux.do/t/topic/2150883)
  - [aini8 API _202605](https://api.aini8.com/console/personal)
    - [【干草铺】公益站开放注册啦 - LINUX DO _202605](https://linux.do/t/topic/2159952)
  - [果咪咪 aiinterface API](https://aiinterface.site/)
    - [【公益推广】GPT公益满血官转支持图片 - LINUX DO _202605](https://linux.do/t/topic/2160297)
  - [HelloAI(CN+) _202605](https://hellofriend.eu.cc/console/personal)
    - [【HelloAI CN+】公益继续，规则调整 ](https://linux.do/t/topic/2275490)
    - 大部分模型渠道（GLM,Mimo,Qwen）都可以正常访问，只是MimiMax有点不稳定，DeepSeek没时间修复。
    - 将放弃每日自动补充额度。之后将不会在以签到，套餐等任何方式向用户固定的增加额度。
  - 🗑️ [NihaoAPI _202603](https://nih.cc/console/personal)
    - cc
  - 🗑️ [Pond Hub 反重力号池 _202603](https://code.claudex.us.ci/panel/profile), 签到
    - [【公益站】Code公益站-反重力号池 重回更名为Pond Hub ](https://linux.do/t/topic/1785656)
  - [ThatAPI](https://gyapi.zxiaoruan.cn/console/personal), 签到
    - 有多个cc分组，IP限制严格(无需gfw)
    - 免费提供 glm flash
  - 🗑️ [太子公益 API](https://api.codeme.me/console/personal), 签到
    - cc支持
  - [Old API](https://sakuradori.dpdns.org/console/personal), 签到
    - [Old API](https://oldai.zeabur.app/console/personal)
    - [【old API公益站】公益站上线（已恢复？） ](https://linux.do/t/topic/1541085)
    - rpm 为 25，还是老样子小容器部署，服务稳定性未知，随时可能因为账号短缺、高并发而死掉
  - 📌 [小呆API](https://api.daiju.live/console/personal), 签到，api不稳定
    - https://china.184772.xyz
    - [小呆API](https://new.184772.xyz/)
    - cc支持
    - [农场](https://game.daiju.live/)
    - [小呆公益站 要不要claude模型这件事 ](https://linux.do/t/topic/1424755)
  - [Hotaru API](https://hotaruapi.com/console/personal)，签到
    - https://api.hotaruapi.top/console/personal
    - codex
    - [〔Hotaru公益站〕新的公益站启动 ](https://linux.do/t/topic/1398297)
    - https://codex.mqc.me/
  - [KFC API](https://kfc-api.sxxe.net/console/personal), 签到
    - https://kfc-api.kyx03.de/
    - Claude和gpt 暂时不支持工具调用, gemini模型没有pro
    - API 调用频率限制为 12RPM，公益站永久免费，采用公平限流策略以保障服务稳定
    - 别玩至尊场，1000积分一次警告扣16x，风险太高; 高级场的高积分也可以获得高收益
  - [Huan API](https://ai.huan666.de/console/personal), 签到, 生图模型
    - cc支持
  - [黑与白chatAPI](https://ai.hybgzs.com/), 每日转盘
    - 模型丰富: claude/gemini/codex
    - 很多openrouter渠道的模型
    - cc不支持tool, **cc渠道经常上架下架** 
    - [黑与白chatAPI福利站](https://cdk.hybgzs.com/)
  - 🗑️ [OAI-FREE](https://newapi.zhx47.xyz/console/personal), 每天100, 需手动
    - [LinuxDo 社区福利活动](https://campaign.zhx47.xyz/)
    - [OAI-FREE 签到发送订阅 ](https://linux.do/t/topic/1632349)
    - 都是临时渠道，不开签到了，直接每天送 100 刀余额
  - [Enjoy _202604](https://free.glen.cc.cd/dashboard), 无签到, 每天限额1000刀
    - [enjoycodex公益站1000个账号邀请码 ](https://linux.do/t/topic/1944332)
  - [ruilab ](https://newapi.ruilab.top/console/personal)
    - [ruilab _202604](http://sub2api.ruilab.top/dashboard)
    - [公益站更换域名 ](https://linux.do/t/topic/1947960)
  - [FreeAI _202604](https://free.closeai.hk/home), 无需签到, 
    - $5/d, $35/w, 非L站, 可付费
    - rpm为2, 全为Plus号池
  - [Super Codex _202603](https://supercodex.lol/dashboard), 每天100, 自动发放
    - [Codex公益站，三网优化，每天100刀 - LINUX DO _202603](https://linux.do/t/topic/1833285)
    - 并发限制35
    - 注册看见余额是0不需要管，注册就有每日100u的套餐
  - [冰のCodex _202603](https://icoe.pp.ua/dashboard), 签到
    - 当余额低于 20 刀时可申请重置到 200 刀。
    - [【开放】【冰の公益站】纯GPT站点 支持5.3 5.4 ](https://linux.do/t/topic/1795246)
    - 清理首批不活跃用户信息（默认条件：注册超过 48 小时，且无 usage、无签到、无重置、API Key 从未使用）
  - [Joverna _202603](https://jiuuij.de5.net/console/personal)
    - 余额超过100时无法签到
  - [CM-API-公益站 _202603](https://api.chengmo.cc.cd/console/personal), 无签到
    - [【CM公益站】佬们，该蹬车了！GPT-5.4强势回归！0倍率+无限制 ](https://linux.do/t/topic/1777029)
  - 📌 [52公益站 _202603](https://free.9e.nz/dashboard), 无需签到
    - [[52公益站]既然天才程序员回归了，那各位爽蹬吧（支持5.4） ](https://linux.do/t/topic/1774352)
    - 倍率设置为0，为保证可用性并发默认5
    - 随时失效，不作保障性承诺
  - [QuicklyAPI _202603](https://sub.jlypx.de/dashboard)
    - 直接注册就可以无限用，默认10并发
    - [gpt-5.4无限蹬，今日依旧正常，24小时各位佬友们蹬了500亿token ](https://linux.do/t/topic/1781875)
  - [DGB 公益站](https://freeapi.dgbmc.top/console/personal)
    - [【DGB 公益站】降低了Codex的倍率，趁现在能蹬赶紧蹬吧 _202603](https://linux.do/t/topic/1801858)
    - 下调了Codedx的倍率，现在倍率只有0.1了
  - [I'm snake _202603](https://imsnake.dart.us.ci/pricing), 无需签到无限用
    - [【I'm Snake公益站】GPT（包括5.4/5.3）系列恢复 _202603](https://linux.do/t/topic/1774170)
    - 无限用无需余额
  - [hotaru Codex Distributor _202603](https://codex.mqc.me/)
    - hotaru作者
  - [APIKey - Subscription Automation](https://gpt.apikey.uk/subscribe), 注册机
    - [【APIKey公益站】速蹬！全新协议注册+绑卡自动化注册机  _202603](https://linux.do/t/topic/1802338)
    - 内置了大概100条号吧，还有七八张卡吧，内置四条ip，美英韩日
  - 🗑️ [CRWorld API _202604](https://api.crworld.site/console/personal), 签到-需手动
    - [CRWorld公益站  ](https://linux.do/t/topic/1906259)
    - 提供GPT Grok Gemini Claude
    - 自用，但不保证可用性
  - 📌 [Ciallo  _202604](https://ioll.pp.ua/console/personal), 手动签到10
    - https://sin.ioll.pp.ua
    - [【Ciallo~公益站】公益站新增域名喵 ](https://linux.do/t/topic/1945895)
  - [New00000 _202604](https://api.00000.mom/console/personal)
    - [[限速了]Codex公益站支持GPT5.5 ](https://linux.do/t/topic/2051012)
    - 号池组成是Pro(2)+Plus(3)都是快要过期的. 服务器是香港cn2gia一模就GG
  - [Huainova _202604](https://ai.huaibao.top/console/personal)
    - [【Huainova公益站】二次开放注册啦 ](https://linux.do/t/topic/1939664)
    - 定时清理注册未使用的
  - [CnGPT公益站 _202604](https://cngpt.net/console/personal)
    - [CnGPT 公益站：给佬友们搭的免费 AI API 中转站 - LINUX DO _202604](https://linux.do/t/topic/2053819)
    - 支持 每日签到，每天可以领取少量额度，适合轻量使用
  - [CHY API公益站 _202604](https://api.xn--chy-js0fk50c.top/console/personal)
    - [CHY API公益站主域名已恢复访问 ](https://linux.do/t/topic/1947845)
  - [【深夜 100】【章鱼小站】给站内的公益站分担点压力 _202604](https://linux.do/t/topic/1897365), 无签到
    - 不定期兑换码
  - [vvcode _202603](https://vvcode.cc/dashboard), 无额度
    - [Codex 公益站  _202603](https://linux.do/t/topic/1859392)
  - [Rosmontis](https://ai.rosmontis.de/console/personal)
    - [[迷迭香公益站]  ](https://linux.do/t/topic/1694922)
    - 公益站有无限codex(目前限制500并发)，无限grok(程序默认限制50并发)。glm系列目前不保证可用性。还有一些杂七杂八的模型。
  - 🗑️ [YAO API _202603](https://yybbwan.xyz/console/personal)
    - [YAO](http://154.37.220.66:3000/console/personal) , legacy
    - [[Yao公益站]codex注册200刀，可能随时倒闭  ](https://linux.do/t/topic/1683788)
  - [荷塘AI _202604](https://hetang.lyvideo.top/console/personal)
    - [【荷塘公益站】仅支持GPT5.4  ](https://linux.do/t/topic/1875698)
  - 📌 [Hello AI _202603](https://hello.xhyun.eu.cc/console/personal)
    - [「XH AI Center/Hello AI 」重新出发 _202603](https://linux.do/t/topic/1759449)
    - [Hello AI/XH AI Center 国产模型狂欢节 ](https://linux.do/t/topic/1948668)
  - [dudu公益站 _202603](https://wududu.edu.kg/console/personal)
    - [【dudu公益站】gpt价格0.01，gpt号池持续补号，grok3000+账号，还有十几个国产模型。（不限制nsfw） - LINUX DO _202603](https://linux.do/t/topic/1808197)
    - gpt和grok的速率限制是60。国产模型速率限制40rpm
    - grok和gpt价格都是0.001/ 1M Tokens，基本无限，gpt号池还在不断补充
  - [XuYa公益站 _202603](https://openai.xuya.dev/dashboard), 无签到
    - 余额9999
  - [晚霞公益站 API _202603](https://newapi.431128hys.site/console/personal)
    - [【晚霞公益站】开放注册 _202603](https://linux.do/t/topic/1706993)
  - 📌 [Infinite API](https://infiniteai.cc/checkin)
    - dark-mode 水平方向逐渐变化的动画效果很好
    - [【Infinite API】全新公益站上线试运营 ](https://linux.do/t/topic/1622685)
    - 50 RPM， 25 个同时进行的请求
    - arrow-preview, QuiverAI API flagship SVG gen
  - 🗑️ [真好记公益站](https://api.zhenhaoji.qzz.io/console/personal)
    - 随便刷吧，可能刷崩了，我就关站了
    - [真好记公益站 ](https://linux.do/t/topic/1795254)
  - [api-test](https://new-api.abrdns.com/console/personal)
    - https://openai.api-test.us.ci  /legacy
    - https://new-api.publicvm.com /legacy
    - [LDC Virtual Goods Shop](https://shop.api-test.us.ci/)
    - https://cdk.api-test.us.ci/
    - 包括 deepseek，硅基流动全模型，阿里云千问全模型，glm，gemini，codex
    - 有claude, 无opus
    - 默认 RPM30，1 级可注册，不允许批量测活
    - [开个小公益站测试一下 ](https://linux.do/t/topic/1414593)
  - 📌 [小辣椒 公益站 ](https://yyds.215.im/console/topup), 签到类似wong
    - cc
  - [蒸蚌公益站 _202603](https://laoxi.ethan010203.online/console/personal), 签到50
    - gpt-5.2
  - [Dooong AI ](https://ai.dooo.ng/console/personal), 签到需过盾
    - 后台有加权风控分系统，T+1和不定时封禁违规账号
  - [Mu. API 2026](https://demo.awa1.fun/console/personal)
    - cc支持, 国产模型
    - 不定期兑换码, [兑换码领取系统 ](https://cdk.awa1.fun/app/redeem)
    - [「公益站」最终还是换成了 New-API _202509](https://linux.do/t/topic/927953)
  - [六万 购曼公益 _202603](https://ai.dogaltman.us.ci/console/personal)， 签到
    - [六万公益站复活，改名【购曼公益】 ](https://linux.do/t/topic/1855060)
  - [无邪公益站 _202603](https://wuxiexiexie.us.ci/console/personal)
    - [【公益站】仅限Linuxdo注册 回馈佬友 随时跑路 _202603](https://linux.do/t/topic/1853752)
  - 📌 [marybrown API _202603](https://marybrown.dpdns.org/console/personal)
    - [服务器小升级,grok-4.2无限用和gpt-5.4试用 _202603](https://linux.do/t/topic/1795512)
    - 23公益站作者后续维护
  - [xiaoxin _202604](https://api.xiaoxin.cfd/dashboard), 无签到
    - [自建了一个中转站，佬们可以体验一下 ](https://linux.do/t/topic/2055010)
  - [955code _202603](https://955code.top/console/personal), 无签到
    - [【955code】codex公益站，上线试运营 _202603](https://linux.do/t/topic/1840889)
  - 🗑️ [意念公益站 _202604](https://yinian.564779.xyz/dashboard), 无签到
    - [［意念公益站］正式运营啦 ](https://linux.do/t/topic/1886962)
  - 🗑️ [鱼汤公益站 _202603](https://ai.zhansi.top/console/personal)
  - [API分享站](https://new-api-bxhm.onrender.com/console/personal)
    - [【API分享站】公益站主帖 ](https://linux.do/t/topic/1355814)
    - 反代 kiro
  - [SakuraCode _202603](https://codex.sakurapy.de/dashboard), 计算pow
    - https://codesign.sakurapy.de/
    - 5.4
  - [GGBOOM公益站](https://ai.qaq.al/dashboard)
    - [签到控制台](https://sign.qaq.al/app)
    - [【GGBOOM公益站】签到站上线啦 ](https://linux.do/t/topic/1517772)
    - 本站点为codex中转站，不包含其他模型
    - sub2api的openai api仅支持 openai-responses API协议。不要选老版本的哦
    - [【GGBOOM公益站】 全面支持gpt-5.3-codex ](https://linux.do/t/topic/1581803)
  - [97公益站 _202603](https://free.9977.me/purchase), 每天20
    - [【97公益站】上线签到功能，下调倍率至0.1 - LINUX DO _202603](https://linux.do/t/topic/1814962)
  - 🗑️ [Einzieg API](https://api.einzieg.site/console/personal), 签到
    - 仅提供codex模型
  - [不可明说 API _202603](https://1.cnmz.de/console/personal)
    - 5.4
  - [LogosAPI _202603](https://api.777114.xyz/console/personal), 签到10
    - 5.4
  - [Acmio _202604](https://ai.acmi.run/dashboard)，无签到
    - [【AcMio 公益站】上线试运营 codex公益站 ](https://linux.do/t/topic/1870102)
    - 注册送200刀。暂未扩展签到功能
  - [AnAnAPI _202603](https://www.ananapi.com/dashboard), 无签到
    - [【AnAnAPI】codex公益站，免費gpt-5.4  _202603](https://linux.do/t/topic/1828940)
  - [zenscaleai](https://lc.zenscaleai.com/console/personal), 签到少
    - 5.4
  - [520 API](https://520.wcgio.com/console/personal), 签到10
    - gpt-5.3-codex 
  - [NPC API](https://codex.hyw.me/console/personal)
    - [NPC API](https://npcodex.kiroxubei.tech/console/personal), legacy
    - [[NPC-API]codex公益站开业 ](https://linux.do/t/topic/1564054)
  - [Codex - New API](https://codex.makeup/console/personal), 无签到
    - [又一个codex公益站，人手一个蹬  ](https://linux.do/t/topic/1645651)
    - gpt-5.4, gpt-5.3-codex
    - [上线claude-sonnet-4.6模型（不稳定版），爱来自cursor  _202603](https://linux.do/t/topic/1739712)
  - [小天公益站 _202603](https://new-api.xt-url.com/pricing)
    - https://checkin.new-api.xt-url.com/
    - 医疗健康大模型 2api, 对话模型，不支持工具调用
  - 🗑️ [纳米哈基米](https://free.nanohajimi.mom/console/personal), 签到
    - Gemini Imagen
    - [【纳米哈基米 · 公益站】 支持香蕉Pro画图，Veo视频，Gemini全系模型 ](https://linux.do/t/topic/1512770)
  - [玩票 API](https://api.361888.xyz/console/personal)
    - opus4.6 和 codex 虽迟但到
  - [sorai API](https://newapi.sorai.me/console/personal)
    - [codex公益站启动 _202601](https://linux.do/t/topic/1524003)
    - 只有 codex 模型
  - [lucky API _202603](https://lucky-sub2api.zeabur.app/dashboard), 签到iframe
    - 10的并发
    - [[lucky codex公益站]清理一批账号了，开放注册 ](https://linux.do/t/topic/1851203)
    - [lucky codex](https://codex-lucky.zeabur.app/console/personal),gone
    - [【lucky公益站】codex公益站  ](https://linux.do/t/topic/1616313)
    - 目前只有 10 个 team 号，所以可能随时跑路
  - 📌 [云端API](https://cloudapi.wdyu.eu.cc/console/personal), 签到, 生图
    - grok-imagine-1.0
  - [Neb 公益站](https://ai.zzhdsgsss.xyz/console/personal), 签到
    - 采用按量计费，每次0.01，注册送2000次，因为该阶段的初衷就是最大化利用这些将要过期的key。
    - 当前额度用完或2026.1.31之后进入第二阶段，采用按量计费，倍率会很低
    - 会不会有签到站不会，因为我太懒了
    - 之前想过接入CC，但是对于我这种新手来说调教整个流程还是太难了
    - [【Neb 公益站】这是主贴 ](https://linux.do/t/topic/1354122)
  - [北极AI大模型](https://bapi.outaucer.me/console/personal)， 签到
  - [Ciprohtna](https://anthorpic.us.ci/console/personal), 签到
    - [【Ciprohtna 公益站】上新 10 LDC = $100 一天订阅畅享包 ](https://linux.do/t/topic/1606615)
    - 注意！没有 opus，opus 在后台都会被重定向到 sonnet
  - [Jarvis API](https://ai.ctacy.cc/console/personal), 签到
    - 备用, [Jarvis API](https://jarvis.ccwu.cc/)
  - [八岁公益站](https://ai.xoooox.xyz/console/personal)
    - cc
  - [摸鱼公益](https://clove.cc.cd/console/personal), 可签到, 额度少
    - [【摸鱼公益】 自己的反重力和codex有一些不怎么用，开个摸鱼站给需要的用用 ](https://linux.do/t/topic/1513131)
    - 后续只能使用积分充值。随用随冲。
  - [WOW公益站](https://linuxdoapi.223384.xyz/console/personal)
    - [【已接入LinuxDO OAuth】老破小公益站复活 ](https://linux.do/t/topic/1516043/1)
    - 因站内目前不支持 Claude-Sonnet，所以接入 Claude Code 时需指定模型 ID 为站内可用的模型
  - [SNOW AI CLI](https://snowcli.com/dashboard/overview), 签到但余额仅当天有效
    - Kiro政策似乎有变化，Opus不稳定，但不是不能用，Sonnet和Haiku正常
    - 特别注意，Kiro逆向因为Token返回数据不精确，所以Snow CLI 无法准确判断自动压缩，根据经验，上下文到达25k~30K左右差不多就满了（这不是真的只有这么短）而是Kiro逆向没有返回缓存信息实际上下文可能非常接近200k了
    - [【Snow CLI】Console 开放部分注册人数，以及近期更新汇总 ](https://linux.do/t/topic/1568653/1)
    - 依旧免费提供稳定的 Kiro 逆向、Codex、KIMI 以及适用于 Codebase 的嵌入模型
  - [GLM 仪表板](https://pureai.shop/dashboard.html)
    - glm + qwen
  - 🗑️ [FovtAPI](https://api.voct.top/console)
    - 模型旧，模型少
    - [NewAPI签到系统](https://gift.voct.top/dashboard/checkin), ~~已失效~~ 
  - [FKAI](https://orchids.fuckai.me/dashboard), 无需签到
    - [【FKAI公益站】 ](https://linux.do/t/topic/1476184)
    - 额度每天刷新 
    - 根据论坛等级确定额度 等级 1 20000, 等级 2 50000, 等级 3 100000
    - 可用模型：claude, gpt
    - 在CC中效果不佳，更推荐作为日常对话
    - 这个网站最开始是给kiro写的，但生不逢时
  - 🗑️ [轻 API](https://lightllm.online/console/personal), 签到
    - cc支持
  - [DEV88公益](https://api.dev88.tech/console/personal), 签到-0.01
    - cc支持
  - 🗑️ [曼波API](https://ai.dik3.cn/console/personal), 签到
  - [ICAT公益站](https://icat.pp.ua/console/personal), 签到
    - [【公益站】ICAT公益站上线了 _202601](https://linux.do/t/topic/1461073)
    - 目前仅支持Claude Code相关模型，其他模型视情况再接入
    - 目前服务器是甲骨文的免费服务器，所以性能上有点一言难尽
    - [ICAT公益站可用状态](https://status.icat.pp.ua/status/icat-server-status)
  - [扣腚API](https://api.jonwinters.pw/console/personal), 
    - 每天15刀，0点重置
    - cluade 配置, 有多余的反重力小号 可以捐到号池里面
    - [CLI Proxy API Management Center](https://cpamc2.jonwinters.pw/management.html#/quota-public)
  - [Luckin 公益API](https://api.oaiapi.online/console/personal)
    - 所有模型均支持 沉浸式翻译
  - [香草API](https://ai.xiangcao.de/pricing), 文生图
  - [六哥公益站](https://api.crisxie.top/), 文生图
  - [佬友API](https://lyclaude.site/console/personal)
  - [APIKEY_公益站](https://welfare.apikey.cc/console)
  - [XiaoYo](https://www.xiaoyo.cn/personal), 签到, deepseek多
  - [唔系唔系](https://claude.chiddns.com/console)
  - [foxhank - Claude Relay Service](https://cc.foxhank.cn ), 无法注册
    - [【CC公益站】尝试维护一个智谱的CC公益站  ](https://linux.do/t/topic/1108974)
  - [Fengye API](https://fengyeai.chat/console)
    - cc
  - [一个小站的 API 商店](https://one-api.ygxz.in/app/dashboard), 每日签到1刀内随机
    - 提供半公益的高质量 API 中转服务，始于202406
    - 无调用频率限制
    - 支持gpt5,claude,gemini
    - 部分模型倍率很高，可选按次计算版本, 如claude
  - [mmkg API](https://api.mmkg.cloud/)
    - 仅在每周五下午 18:00 至 21:00 开放，每周限量 100 人
    - 支持claude,gemini, 不支持gpt
  - [莹のAPI](https://api.wpgzs.top/pricing)，模型贵
    - rpm15
    - [莹のapi 加油站](https://quota.wpgzs.top/), 鸡你太美，每天可转100刀到公益站
    - [公益站支持claude ](https://linux.do/t/topic/1351151)
  - [莹のapi & 随时升天](https://supersb.me/console)，模型贵
    - [随时升天的公益站](https://any.97819781.xyz/)
  - [KFC API](https://kfc-api.sxxe.net/console/personal)
    - [KFC API公益站 - 正式上线  ](https://linux.do/t/topic/1233747)
    - [逆水寒](https://api.sxxe.net/), 即将关闭
    - [逆水寒公益API——扬帆起航 ](https://linux.do/t/topic/1173036)
  - [包子铺](https://api.5202030.xyz/)
    - [包子公益](https://api.codeqaq.com/)
    - 只开放linuxdo lv2以上注册
    - 支持gpt,claude,gemini, 但没有gpt5(有mini)
    - [包子公益 - Baozi DoneHub](https://lucky.5202030.xyz/)
    - 每日普通用户可自行划转 200$ 到 newapi 站点
    - [【包子公益站】更新一个总的汇总贴。现在上线了newapi的分站 ](https://linux.do/t/topic/1124776)
  - [我爱996公益](https://529961.com/console)
    - [我爱996公益附属站 - 每日签到领取奖励](https://hub.529961.com/)
    - [【公益站我爱996一次】测试上线已接入LinuxDo ](https://linux.do/t/topic/1147448)
  - [GoGoGo公益站](https://api.chengtx.vip/console/personal), 签到可得20~50刀，0.2刀/次
    - [GoGoGo公益站启航：目标是刷爆gemini小破号池 ](https://linux.do/t/topic/1494070)
    - rpm-15, 不限用途，可酒馆
    - 模型: gemini-2.5/3-flash/pro
    - 渠道是自部署gemini business2api，自己域名邮箱注册的，放了100多个号
  - 🗑️ [ibsgss公益站](https://codex.ibsgss.uk/console/personal), 签到
    - [【ibsgss公益站】支持codex cli / cherry  ](https://linux.do/t/topic/1434464)
    - 维护期限：到 codex-team 渠道耗尽为止
  - 🗑️ [随缘API](https://newapi.tanmw.top/console/personal)
    - [【随缘API公益站】开放注册！余额已调整 ](https://linux.do/t/topic/1634879)
    - 目前只有 GPT 和 Grok 
    - 不保证稳定性！随时跑路
  - 🗑️ [b4u API](https://b4u.qzz.io/console), 每日转盘, 关站20260222
    - 会不会增加其他模型: 不会，本站专注于Claude
    - 不支持opus
    - 支持工具调用、上下文 128K+、支持 RooCode，不推荐接入 ClaudeCode
    - 普通用户：每次 1 刀、RPM=10
    - 渠道技术： Claude-SessionKey号池→claude2api→FC使能
    - [转盘抽奖](https://tw.b4u.qzz.io/)
    - 仅每周六晚21:00至21:30限时开放注册
    - [【B4U公益站】是克劳德，我们有救了！（每周六限时开放注册） ](https://linux.do/t/topic/801848)
    - [[B4U]如何 配置 claude code ](https://linux.do/t/topic/1068671)
    - 需要ccr，而且工具调用不稳定。  反正我b4u聊天经常被断，所以只能简单的写个代码修改个东西
    - [B4U2CC：让B4U支持Claude Code＋思考 ](https://linux.do/t/topic/1285981)
    - B4U2CC 是一个Anthorpic Message 格式到 Openai Chat 的桥接器，无需上游支持FC, 就能实现接入Claude code并支持启用thinking
    - 不止支持b4u，任意支持openai chat格式的模型都可通过b4u2cc接入claude code，如果模型是claude的话还能启用思考
  - 🗑️ [Privnode](https://privnode.com/)
    - free分组支持claude-code，也支持gpt-5-nano
    - https://pro.privnode.com/
    - [【Cone 公益站】找个佬共同维护  ](https://linux.do/t/topic/1035525)
    - [Cone 公益站更新 ](https://linux.do/t/topic/1002152)
  - 🗑️ [无言AI](https://aiai.li/panel), 每日签到, 已关闭
    - 支持cc
  - 🗑️ [23公益站](https://sdwfger.edu.kg/console), 已关闭
    - 平台将于每周五、周六统一发放额度兑换码 
  - 🗑️ [tbai API](https://tbai.xin/), 已关闭
    - 模型支持gemini/gpt, 不支持claude
    - API调用频率限制为 10 RPM
    - gpt-load 作者
    - [【T佬公益】TBAI公益站主贴-爽用Gemini|OpenAI|DeepSeek模型 ](https://linux.do/t/topic/683726)
  - [VoAPI公益站](https://demo.voapi.top/), 每日签到, 
    - [【首发更新】全新API分发和管理系统-VoAPI ](https://linux.do/t/topic/218662)
    - 曾经的帐号已注销，需要重新注册
  - [ ~~Cats API~~ ](https://catsapi.com/), 已关闭
    - API调用频率限制为 15 RPM
    - [【猫猫公益】API使用说明 ](https://linux.do/t/topic/851028)
  - [RawChat公益站点](https://chatgptplus.cn/)
    - 免费的共享ChatGPT账号
    - [RawChat公益站点](https://sharedchat.fun/)
    - [HammerAI公益站](https://hammerai.vip/)
  - [Claude免费镜像号池](https://share.claude.best/)
    - 若无法对话了，说明对话额度被其他朋友用完了（需要你更换其他账号或者等待额度刷新）
    - [RawChat公益站点 kelaode](https://kelaode.ai/)
  - [cupsfunny API](https://free-llm.cupsfunny.com/)
    - 支持cluade, gpt5, 其中gpt5全免费(但经常429响应异常)
    - 每位用户RPM为2
    - 借助Toolify项目实现了函数调用，可以用于Claude Code
    - 如果增加额度和申请Claude的留言我没有及时回复，可能只是我不在而已，可以再等等 
    - Sonnet模型每次调用消耗两次使用次数，Opus每次调用消耗四次使用次数
    - [公益大模型API接口 - 小欢博客 - Fly your dreams](https://www.cups.moe/archives/free-llm-api.html)
  - [yx](https://api.dx001.ggff.net/pricing)
  - [方舟API](https://www.yxaiapp.com/)
  - [YesCode](https://co.yes.vg/)
    - [YesCode test](https://cotest.yes.vg/)
    - [【YesCode公益测试站】Claude Code/Codex 长期免费测试 ](https://linux.do/t/topic/964164)
  - [银河AI](https://mmaqq.top/console)
    - 需支付宝付费
  - [cone Veloera Zone](https://zone.veloera.org/)
    - 此服务完全免费提供，并仅在 LINUX DO 社区宣传
    - 不定期删除 0 额度，0 消耗，且注册超过一周的用户。
  - [SLA API](https://www.sla-api.zone.id/)
  - [ZenscaleAi](https://gy.zenscaleai.com/)
    - 仅提供gemini模型
  - [小丑Ai公益站](https://gy.jiubanai.com/)
    - 仅提供gemini模型
  - [小松公益站 New API](http://api.lanapi.top/pricing)
    - 仅提供gemini模型， 满血版
    - 默认分组只有5分钟3次的请求速率，至尊分组无上限分组
  - [素墨API —— AI公益站](https://apifree.rensumo.top/)
  - 🗑️ [翰林文苑公益API站点](https://aiapi.hlwy2025.me/)
    - 价格太高了 我决定攒到1000再用
  - [SillyDream 公益站](http://ff.sillydream.top/pricing)
  - [linjinpeng Veloera](https://linjinpeng-veloera.hf.space/)
    - 现在rpm是6，模型全部免费，1级即可注册
    - 一次一美元的调用，但是这个1美元是无限刷新的，你用了就知道了
    - 聊天记录均留样检测，违规直接封禁，请不要对话任何隐私信息
    - [能否成为全站用量最大的claude 4.1 opus公益站 _202509](https://linux.do/t/topic/956435)
  - [learn-ai 公益站点](http://free.learn-ai.top/), 需要签到且额度很少
    - 支持的模型质量较低: 很少一部份claude模型, gpt-mini/nano
    - 可以加入付费站点：https://learn-ai.top/
  - [LLM API 公益站](https://llm.indrin.cn/)
    - 本站永久运营，服务免费提供个人使用,禁止高并发,禁止高输入, 高并发会封号
    - 额度不限量,注册送$30，邀请送$5,正常用户额度快用完时会给后台增加
    - 不支持claude，支持openai, xai
  - [归一](https://ai.luuu71.dpdns.org/pricing)
    - gpt5
  - [TudouAPI](https://www.tudou.chat/), 签到复杂
    - 如果账户连续3天以上都是只有5-10条， 会判定为屯额度账号签到失败
    - 支持claude, gpt
  - [Becode 公益站](https://becode.be-a.dev/)
  - [88code - 企业级Claude Code/Codex中转](https://www.88code.org/)
    - 添加客服领取 10 美元免费额度, 每个用户仅限领取一次
  - [AICodeMirror官方共享平台 - 中国用户专属AI编程助手](https://www.aicodemirror.com/)
    - 每月 2000积分
    - 因成本大幅上升，免费用户暂不开放体验。后续开放时间另行通知
  - [一叶知秋API](https://88996.cloud/)
    - 本站已勉强运行 1020 天
  - [cto.new ](https://cto.new/)
  - [Claude 4.5 国内免费使用指南 | 最全访问方式汇总 2025 - 知乎](https://zhuanlan.zhihu.com/p/1956204058139431066)
    - 镜像、中转、合租、代充
  - [2025年10月 Claude 国内使用指南（支持 Claude Sonnet 4.5） - 知乎](https://zhuanlan.zhihu.com/p/1940070586635223559)
  - [白嫖最强AI编程模型Claude 4.5，暨一哥Claude Code的免费下位替代（10月22亲测可用） - 知乎](https://zhuanlan.zhihu.com/p/81947374736)
  - [求推荐免费模型api，公益站付费的太慢了，只是用于ai中文翻译成英文，速度有要求 ](https://linux.do/t/topic/1061766)
  - [长期收录靠谱稳定长期免费AI （API）Claudecode等 实现 AI 自由](https://www.nodeseek.com/post-450243-1)
    - https://github.com/CyYxl2024/freeai
    - 只收录商业平台。
  - [【项目自荐】一个免费使用Claude AI纯公益号池镜像站 ](https://github.com/ruanyf/weekly/issues/8047)
  - https://x.com/search?q=claude%20%E5%85%AC%E7%9B%8A%E7%AB%99&src=typed_query&f=live     /搜索最新公益站
  - https://github.com/chatanywhere/GPT_API_free
    - 免费ChatGPT&DeepSeek API
    - 免费API Key限制200请求/天/IP
  - [【Check-CX】监控站正式上线啦！现已加入LinuxDo元宇宙豪华套餐 ](https://linux.do/t/topic/1286480)
    - https://check.linux.do/
    - 之前 @Dean 佬做了一个富可敌国商家评价平台，我心血来潮：能不能做一个富可敌国商家模型渠道监控站呢？
    - 前后端代码全部开放，检测逻辑一目了然
    - https://github.com/BingZi-233/check-cx /MIT/ts

- api-bookmarks
  - [agentify API](https://api.agentify.top/pricing)
    - [H800 公益站回归！200tps 的 gpt-oss-120b 继续不限量免费用 ](https://linux.do/t/topic/1356689)
      - 模型部署在两张 H800 上面，人少的时候可以 200tps
      - 还加了一些 openrouter 的免费模型也几乎不限量
  - [做点长期公益，nvidia nim 大部分开源模型 + OpenAI免费模型的gptload ](https://linux.do/t/topic/1427060)
    - 搭建了一个gpt-load负载站：
    - NVIDIA NIM
    - OAI-Free: gpt-5-nano, GPT-4.1-mini
    - https://independent-adrea-mtg-154afb72.koyeb.app/proxy/nvidia
    - https://independent-adrea-mtg-154afb72.koyeb.app/proxy/openai
    - GALAXYPUBLICAI1984282

- embedding
  - [embedding New API](https://router.tumuer.me/)
    - [[Embedding 公益站] 专门提供 Embedding API 的迷你站 ](https://linux.do/t/topic/1385442)
    - 服务器在国外，所以需要使用魔法
    - [Embedding API 使用指南](https://embedding-docs.tumuer.me/)
    - 来自 gemini, vertex 渠道的后来几天陆续添加。
  - [【求助】寻找一个嵌入模型的公益站 ](https://linux.do/t/topic/1637724)

- llm-ui/apps
  - [SmallAI](https://free.smallai.asia/chat)
    - 基于lobechat实现
    - [【网站自荐】SmallAI公益站——免费使用GPT4o mini，支持多模态 ](https://github.com/ruanyf/weekly/issues/4969)
  - [AI对话 - db的AIGC站](https://ai.feles.town/chat)
  - 💰 [GoAmzAI - 个人、团队、企业私有化、运营的AIGC平台解决方案](https://d.goamzai.com/)
    - https://github.com/Licoy/GoAmzAI /非开源
    - https://github.com/VoAPI/VoAPI /仅提供docker-compose.yml
    - [AI对话 - GoAmzAI Plus](https://demo6.goamzai.com/chat)
    - [对话 - GoAmzAI Pro](https://prodemo6.goamzai.com/chat)
    - [goamzai已集成LinuxDO Connect，演示站开放给L佬们使用 _202406](https://linux.do/t/topic/122462)
    - [【公益AIGC】最适合日常使用的公益站，高级AI工具一网打尽 ](https://linux.do/t/topic/1175890/37)
      - volo api 吧，基于 new api 改的，但是 v1 开始好像就完全重写了
      - VoAPI 一直是闭源的，甚至好像只放出 Docker 的部署方式，连编译后的可执行文件都不发布的，截止到我最后一次看时是这样的，不知道后续有没有改变和有没有收费计划
  - [WorldOF](https://worldof.onrender.com/)
    - [GPT5、gemini2.5 Flash 的不限量无需登录的 API 来了，应该刷不死 ](https://linux.do/t/topic/1443674)

## image-gen 🖼️

- modelscope对部分模型提供了免费生图的额度, 如z-image-turbo

- [Cogview-3-Flash - 智谱AI开放文档](https://docs.bigmodel.cn/cn/guide/models/free/cogview-3-flash)
  - 智谱推出的免费图像生成模型，能够根据用户指令生成符合要求且美学评分更高的图像
  - 支持多种分辨率，包括 1024x1024、768x1344、864x1152、1344x768、1152x864、1440x720、720x1440 等

- csdn 的 gitee 的 ai模型服务，每天免费 1000 次好像是(有些开源生图模型)

- image-api
  - [云端API](https://cloudapi.wdyu.eu.cc/pricing), 签到
  - [Huan API](https://ai.huan666.de/pricing)
  - [香草API](https://ai.xiangcao.de/pricing)
  - [六哥API站](https://api.crisxie.top/pricing)
  - [pollinations.ai](https://enter.pollinations.ai/)
    - [基于Pollinations的图像生成接口的工作台  _202601](https://linux.do/t/topic/1423187)
    - 1 额度可生成张数: z-image--5k, sdxl--3k, seedream--25
    - 已经被阉割了，现在免费的生图质量极差
  - [啾啾小铺](https://api.usegemini.xyz/pricing)
    - [NanoBananaPro 4K生图公益 ](https://linux.do/t/topic/1486971)
    - 注册送100额度，用完重新注册即可; 不要走 linux.do 渠道注册就好了
    - 逆向的flow接口
    - 模型名如下：gemini-3.0-pro-image-landscape,gemini-3.0-pro-image-portrait,gemini-3.0-pro-image-square
    - 由于目前flow官方流量大，官网都生不了图，佬友们等会再蹬
  - [图片生成](https://pam-carrier-korean-chemicals.trycloudflare.com/)
    - [nanobanana公益站 ](https://linux.do/t/topic/1616133)
  - [TS-AI | 灵感创作工坊](https://linux.tsart.lat/workspace)
    - [【绘画公益站】TS-AI  ](https://linux.do/t/topic/1641029)
    - 每天签到可获得 3000 积分（三天内有效）
  - [IMG Hub ](https://aiddup.com/)
    - [公益生图站点 - LINUX DO _202604](https://linux.do/t/topic/2004335)
    - 三级	200积分/天

- image-saas
  - [小白生图 - AI Image Generator](https://catsapi.com/)
  - [AI 生图平台](https://ztu.ai/)
    - 每天5张免费
    - [【公益站】ztu.ai 视频生成上线 _202601](https://linux.do/t/topic/1507837)
  - [RyanVan Z-Image | AI 图像生成](https://ryanai.org/)
    - 每天5张免费
    - 排队时间可能较长
  - [RyanVan Z-Image | AI 图像生成](https://txt2img.1771177.xyz/)
    - [[Z-Image公益] 跟随R佬脚步，闲置显卡分享zimage ](https://linux.do/t/topic/1643183)
    - 按照教程通过 gpu-worker 的方式接入了 R 佬的节点。目前本地跑的是 fp8 量化版的 z-image-turbo 模型，实测生成一张 1K 图片 15 秒左右。
  - [Z-Image 控制台](http://image.dx001.ggff.net:8080/dashboard)
  - [香蕉皮 AI](https://nanobanana.xiao.mom/)
    - [NanoBananaPro支持4K、免费无限制，轻蹬 ](https://linux.do/t/topic/1401748)
    - 在家逆向了一个NanoBananaPro香蕉皮AI，支持4K，不用登录，不限次数
  - [Nano Banana Pro - Free AI Image Editor & Generator ](https://www.nanaai.app/)
  - [最新公益绘画API ](https://linux.do/t/topic/599258)
    - 百度绘画
    - 豆包绘画
  - [Dreamifly - 免费AI绘画在线生成工具 | 一键生成动漫、插画、艺术图](https://dreamifly.com/zh)
    - 由全国30台家用电脑的闲置4090显卡，免费无限制提供分布式算力支持
  - [FluxEz - 免费的文生图网站](https://flux.comnergy.com/zh)
    - 提供完全免费的生图服务, 无需注册
  - [Seedream AI - 免费在线AI图像生成器](https://seedream.pro/zh)
  - [Cloudflare Workers AI Models](https://developers.cloudflare.com/workers-ai/models/)
    - 提供免费的文生图模型: sdxl, sdv1-5
  - [Free AI Image Generator - AI Free Forever](https://aifreeforever.com/image-generators)
  - [Free Gemini Pro](https://freebanana.pro/)
    - 速度慢
  - [FreeGen 白嫖图片生成器](https://hachimiai.dpdns.org/freegen/)
  - [SoraApi](https://api.67.si/)
    - 不可用
    - 继续上新 即梦4.6 和 5.0 
  - [呜哩AI，一站式AIGC创意平台](https://wuli.art/generate)

- image2api
  - [Antigravity的反代的Nano Banana用不了了 ](https://linux.do/t/topic/1419858/2)
    - 下午都很慢。晚上1点后一般都快些
  - [Libre Assistant](https://libreassistant.vercel.app/)
    - [又一款免费无限用的生图及对话LLM站 ](https://linux.do/t/topic/1418376)
  - [youmind2api，可以使用大香蕉 ](https://linux.do/t/topic/1363986)
  - https://github.com/iptag/jimeng-api /GPL/202511/ts
    - Free AI Image and Video Generation API Service - Based on reverse engineering of Jimeng AI (China site) and Dreamina (international site).
    - [【即梦jimeng/dreamina官网2api】10/20更新：双站均支持文生图和图生图  _202509](https://linux.do/t/topic/995691)
    - 即梦 jimeng 和 dreamina 文生图和图生图的官网 api，借鉴了几位大佬的项目，但他们的参数都有些小问题，稍加改进下，稳定性强了不少，目前只测试了文生图和图生图功能
  - [[Flow2api] 无限次数的banana pro！逆向账号池 ](https://linux.do/t/topic/1214169)

- tutorials-image
  - https://github.com/rere43/image-generator-hybrid
    - CliProxyApi 反重力生图 skill, 支持4K, 有两种方法整合, http 和google genai SDK
    - [CliProxyApi 反重力生图 skill, 支持4K, claude code , codex可用 _202512](https://linux.do/t/topic/1378927)
  - [借助 Antigravity-Manager, 终于用上反重力了！可4k banana pro _202512](https://linux.do/t/topic/1374557)

- [Lorem Picsum - Images - The Lorem Ipsum for photos](https://picsum.photos/images)

## logo-gen

- [Accio — Ask anything about B2B, find suppliers & inspiration](https://www.accio.com/)

## video-gen

- [l0veyou](https://l0veyou.com/)
  - [可能是全网第一个ai图生视频公益站，让佬友们实现做ai漫剧自由（l0veyou） - 福利羊毛 - LINUX DO _202606](https://linux.do/t/topic/2287218)

- [Video Studio](https://doubao.happieapi.top/)
  - rpd: 30
  - 两款模型分别是 doubao-seedance-1-0-pro-fast-251015 和 doubao-seedance-1-5-pro-251215：前者主打高速视频生成，适合大多数文本或单图生成视频的场景，视频时长为 4–12 秒，最多支持 1 张图片输入，支持全部比例，不支持音频，默认无水印（API 可配置水印）；后者主打高质量视频生成，支持多图输入，画面一致性更强，视频时长同样为 4–12 秒，最多支持 2 张图片输入，支持全部比例，支持音频（默认带音频），默认无水印（API 可配置水印）。

## translation

- 「慕鸢の公益站」 [这是谁的公益站呢？好难猜阿](https://newapi.linuxdo.edu.rs/pricing), 签到获取0.01
  - 专门有一个翻译分组，需要创建对应分组的key，超低倍率，不限制并发
  - [上新沉浸式翻译和codex ](https://linux.do/t/topic/1501277)
- [cerebras fanyi API](https://fanyi.963312.xyz/pricing)
  - cerebras 的，目前有200个号
  - 智普官网的 glm-4.5-flash, glm-z1-flash
- [老魔公益站](https://api.2020111.xyz/pricing)
  - [【老魔公益站】沉浸式翻译站开放注册 ](https://linux.do/t/topic/1514451)
  - translate：沉浸式翻译分组，限速 300次/5min
  - cc-glm4.7和cc-m2.1：支持cc的分组，上游分别路由到glm-4.7和minimax-m2.1，限速 35次/5min
- [6655 API](https://translate-api-cf.6655.pp.ua/)
  - [【2月兑换码】6655公益 沉浸式翻译api ](https://linux.do/t/topic/1564148)

- [Chiban api](https://api.chibanban.de/pricing)
  - [［赤坂公益站］维护通知 ](https://linux.do/t/topic/1630985)

- [New API](https://new-api-latest-1-eu26.onrender.com/pricing)
  - 无法签到, [公益API站~ 可用于翻译  ](https://linux.do/t/topic/1552193)

## audio

- [MimoTTS ](https://mimotts.jlen.top/billing/)
  - [小米mimotts公益站 - LINUX DO _202606](https://linux.do/t/topic/2437265)

## llm-2api

- embedding
  - [Embedding](https://router.tumuer.me/pricing)
    - [[Embedding 公益站] 问题+更新+预告 _202601](https://linux.do/t/topic/1421074)
      - 用 gemini 的 embedding-001 和 text-embedding-004 时容易出现，因为上游接的是 tier1 层的号，所以有限额，可以等段时间或者使用其他模型
    - [[Embedding 公益站] 囤囤鼠集合啦  ](https://linux.do/t/topic/1507741)
      - 上架了模型 gemini-embedding-001(不是 embedding-001)
      - openrouter 的 key 了，专门用于 text-embedding-3-large 

- tutorials
  - [手把手带你用上AI神器 - CLIProxyAPI（零：配置详细解说） _202510](https://linux.do/t/topic/1011966)
  - [手把手带你用上AI神器 - CLIProxyAPI（壹：项目介绍+Qwen实战） _202510](https://linux.do/t/topic/1011983)
  - [在 opencode 中使用CLIProxyAPI 的配置教程，享受模型自由 _202601](https://linux.do/t/topic/1407247)
  - [CLIProxyAPI 的反重力BananaPro 稳定输出 4k 图片 教程 _202601](https://linux.do/t/topic/1396957)
  - [zeabur免费搭建CLIProxyAPI，CLI和Antigravity都能用 _202601](https://linux.do/t/topic/1381902)

- [OpenCode - Zen](https://opencode.ai/docs/zen/)
  - Zen works like any other provider in OpenCode. You login to OpenCode Zen and get your API key.
  - if you are using a model through something like OpenRouter, you can never be sure if you are getting the best version of the model you want.
  - We tested a select group of models and talked to their teams about how to best run them.
  - OpenCode Zen is an AI gateway that gives you access to these models.
  - [opencode其实提供了三种模型的免费api可以直接使用 ](https://linux.do/t/topic/1436094)
    - api url: https://opencode.ai/zen
    - api key: public
    - 原以为好歹有个session 鉴权什么的，没想到是这么做的  
    - ip 限流，有 rate limit，最近感觉限制变得更严重了，或许是用 opencode 的人变多了。
    - 实测其实只有 grok-code 比较稳定，glm 经常 429

- [Zeabur](https://zeabur.com/)
  - $5/月免费使用

- [XiamenLabs - Unity AI](https://xiamenlabs.com/)
  - [【开源】 厦门实验室的UNITY2api，全网最简单的2api项目 ](https://linux.do/t/topic/1417828)
  - [神秘厦门lab模型Unity实测报告  ](https://linux.do/t/topic/1418561/1)
    - 先说结论：很大可能是一个小/中等大小模型，高度蒸馏Gemini的产物。
    - 这个模型在蒸馏Gemini的时候竟然只蒸馏到了知识库，其他的全抛了，也算科技创新了
    - 我的结论是，用来骗投资刚刚好

- [ExaFree](https://exa.chengtx.vip/ )
  - [ExaFree公益站来袭：全民无限Exa搜索API时代 _202603](https://linux.do/t/topic/1724047)
# llm-api-official/router/gateway/aggregator
- 北龙超级计算云平台 [AI 智算云](https://ai.blsc.cn/#/lms/model)
  - 免费提供: PaddleOCR-VL-0.9B, GLM-4.5-Flash, GLM-4V-Flash, GLM-4-Flash, GLM-CogView3-Flash, GLM-Z1-Flash

- 📌 [OpenRouter API Rate Limits ](https://openrouter.ai/docs/api-reference/limits)
  - tldr: rpd-1000 
  - Free usage limits: If you’re using a free model variant (with an ID ending in `:free`), you can make up to 20 requests per minute. 
  - If you have purchased less than 10 credits, you’re limited to 50 :free model requests per day.
  - If you purchase at least 10 credits, your daily limit is increased to 1000 :free model requests per day.
  - If your account has a negative credit balance, you may see `402` errors, including for free models.
  - https://github.com/jomonylw/openrouter-free-model /202509/ts/inactive
    - https://openrouter-free-model.vercel.app/
    - a web application designed to browse, filter, sort, and manage free models available on OpenRouter.
    - 可参考 https://github.com/MauroDruwel/NIMStats 添加状态
  - [Free Models Router ](https://openrouter.ai/openrouter/free)
    - openrouter/free
  - [openrouter出免费模型路由了 _202602](https://linux.do/t/topic/1559289)
    - 稍微测了下，不是 50rpd，挺好
  - [Introducing Web Search via the API  _202501](https://openrouter.ai/announcements/introducing-web-search-via-the-api)
    - The OpenRouter API now supports a web search feature, available for all models. 
  - [OpenRouter Charges for FREE models, why? : r/openrouter _202605](https://www.reddit.com/r/openrouter/comments/1t0kr36/openrouter_charges_for_free_models_why/)
    - Web search always has been charged, disable that and enjoy the freebies

- [OpenCode Go ](https://opencode.ai/docs/go)
  - If you reach the usage limit, you can continue using the free models.
  - Model	requests per 5 hour	requests per week	requests per month
  - GLM-5.2	880	2, 150	4, 300
  - Kimi K2.7 Code	1, 350	4, 630	9, 250
  - MiniMax M3	3, 200	8, 000	16, 000
  - Qwen3.7 Plus	4, 300	10, 800	21, 600
  - DeepSeek V4 Pro	3, 450	8, 550	17, 150
  - DeepSeek V4 Flash	31, 650	79, 050	158, 150

- [Neuralwatt Pricing - Energy-Based Inference API ](https://portal.neuralwatt.com/pricing)
  - $5.00 /kWh
  - $20 /month: 6 kWh, 

- 📌 [Ollama Cloud models](https://ollama.com/search?c=cloud)
  - Hourly + Weekly limits
  - Unlimited public models
  - [Announcing Cloud models · Ollama Blog _202509](https://ollama.com/blog/cloud-models)

- 📌 [Cerebras Inference Rate Limits](https://inference-docs.cerebras.ai/support/rate-limits)
  - tldr: tpd-1m, rpd-14.4K
  - 注意免费模型的context长度最大为64k
  - Model	TPM	TPH	TPD	
  - gpt-oss-120b	60K	1M	1M
  - llama-3.3-70b	60K	1M	1M
  - qwen-3-32b	60K	1M	1M
  - qwen-3-235b-a22b-instruct-2507	60K	1M	1M
  - qwen-3-235b-a22b-thinking-2507	60K	1M	1M
  - qwen-3-coder-480b	150K	1M	1M, rpd-100

- 📌 [NVIDIA NIM APIs](https://build.nvidia.com/explore/discover)
  - free: Up to 40 rpm
  - models: deepseek-r1, qwen3-coder-480b
  - [NVIDIA NIM FAQ - AI & Data Science / NVIDIA NIM - NVIDIA Developer Forums _202409](https://forums.developer.nvidia.com/t/nvidia-nim-faq/300317)
    - NIM access through the NVIDIA Developer Program is for prototyping, research, development and testing purposes only and does not include enterprise features or support.
  - [API Reference — NVIDIA NIM](https://docs.nvidia.com/nim/large-language-models/latest/reference/api-reference.html)
    - api文档表明支持 /v1/responses api, 但放在donehub中存在异常
    - unexpected status 404 Not Found: Provider API error: bad response status code 404 (request id: 20260505034505506297000MT8jCw5U), url: http://localhost:4090/v1/responses
  - https://github.com/MauroDruwel/NIMStats /python
    - https://nimstats.maurodruwel.be/
    - Automated hourly benchmarks for 20+ NVIDIA NIM models — interactive dashboard, zero infra, self-hostable.
    - [NVIDIA NIM is inconsistent, so I benchmarked 20+ models every hour : r/SillyTavernAI _202605](https://www.reddit.com/r/SillyTavernAI/comments/1t1zlcj/nvidia_nim_is_inconsistent_so_i_benchmarked_20/)
  - https://github.com/sherman-yang/nvidia-model-info /202604/js
    - Local dashboard for exploring the free models exposed through build.nvidia.com.

- [Groq Rate Limits - Docs](https://console.groq.com/docs/rate-limits)
  - tldr: tpd-100k~500k
  - MODEL ID	RPM	RPD	TPM	TPD
  - groq/compound	30	250	70K	No limit
  - qwen/qwen3-32b	60	1K	6K	500K
  - openai/gpt-oss-120b	30	1K	8K	200K
  - llama-3.3-70b-versatile	30	1K	12K	100K
  - moonshotai/kimi-k2-instruct-0905	60	1K	10K	300K
  - meta-llama/llama-4-scout-17b-16e-instruct	30	1K	30K	500K

- [Gemini Developer API Pricing  ](https://ai.google.dev/gemini-api/docs/pricing)
  - tldr: 国内不可用, rpd-100~250
  - gemini-2.5-pro: Grounding with Google Search	Not available
  - gemini-2.5-flash: Grounding with Google Search, up to 500 RPD (limit shared with Flash-Lite RPD)
  - [Rate limits  |  Gemini API  ](https://ai.google.dev/gemini-api/docs/rate-limits)
    - model,          RPM,   TPM,      RPD
    - Gemini 2.5 Pro	  5	   125,000	  100
    - Gemini 2.5 Flash	10	 250,000	  250
    - Gemini 2.0 Flash	15	 1,000,000	200

- [Mistral Rate Limits & Usage tiers ](https://docs.mistral.ai/deployment/ai-studio/tier)
  - tldr: tpmon-1b(tpd-33m)
  - Maximum requests per second: 1
  - Tokens per Minute: 500, 000
  - Tokens per Month: 1 billion
  - models: codestral-2501, mistral-large-2411
  - [Codestral - AI Studio - Mistral AI](https://console.mistral.ai/codestral)
    - Limits: 30 requests/minute, 2,000 requests/day
    - Use Codestral via your favorite Code completion tool for free.
    - Codestral is available in select code-completion plugins but can also be queried directly. 

- 📌 [魔搭推理API-Inference API推理介绍 · 文档中心](https://modelscope.cn/docs/model-service/API-Inference/intro)
  - tldr: rpd-200~500
  - 免费推理API由阿里云提供算力支持，要求您的ModelScope账号必须绑定阿里云账号后才能正常使用。
  - 每位魔搭注册用户，当前每天允许进行总数为2000次的API-Inference调用，其中每单个模型不超过500次，具体每个模型的限制可能随时动态调整。
  - 在每个模型每天不超过 500 次调用的基础上，平台可能对于部分模型再进行单独的限制，例如，deepseek-ai/DeepSeek-R1-0528，deepseek-ai/DeepSeek-V3.1等规格较大模型，当前限制单模型每天200次调用额度。
  - 在上述调用次数限制的基础上，不同模型允许的调用并发，会根据平台的压力进行动态的速率限制调整，原则上以保障开发者单并发正常使用为目标。
  - 实际单模型可用次数以及允许的并发，以平台实时调整为准。
  - 🖼️ 当前API-Inference为魔搭平台上的部分开源大语言模型（LLM），多模态模型（MLLM），以及AIGC专区文生图模型等，提供了可直接使用的API。

- [硅基流动 SiliconFlow - 大模型 API 价格方案](https://www.siliconflow.cn/pricing)
  - tldr: tpm-50k
  - llm: Qwen/Qwen3-8B, deepseek-ai/DeepSeek-R1-0528-Qwen3-8B, THUDM/GLM-Z1-9B-0414, THUDM/GLM-4-9B-0414, Qwen/Qwen2.5-Coder-7B-Instruct
  - vlm: THUDM/GLM-4.1V-9B-Thinking
  - image: Kwai-Kolors/Kolors
  - asr: TeleAI/TeleSpeechASR
  - [Rate Limits - SiliconFlow](https://docs.siliconflow.cn/cn/userguide/rate-limits/rate-limit-and-upgradation)
    - 语言模型(Chat)	 RPM=1000-10000 TPM=50000-5000000
    - 🖼️ 图像生成模型(Image)	 IPM:2 IPD:400

- 🗑️ [iflow 心流开放平台 - 限流](https://platform.iflow.cn/docs/limitSpeed)
  - 当前服务免费使用，但请合理使用资源，避免不必要的高并发请求。
  - 每个用户最多只能同时发起一个请求，超出限制的请求会返回429错误码。
  - 流式请求: 主动取消后立即释放令牌，推荐使用流式请求以提高效率。
  - 非流式请求: 主动取消后，模型实际仍在运行，需等待运行完毕后才释放令牌。
  - 最大输出 64K:  qwen3-coder-plus, glm-4.6, deepseek-v3.2, deepseek-v3.1, qwen3-235b-a22b-thinking-2507, qwen3-235b-a22b-instruct, kimi-k2, kimi-k2-0905, 
  - 最大输出 32K:  qwen3-vl-plus, qwen3-max, deepseek-r1

- [302. AI - API超市 cn](https://dash.302ai.cn/product/list?cate=api&tag=LLM)
  - [302. AI - API超市 ww](https://302.ai/product/list?cate=api&tag=%E8%AF%AD%E8%A8%80%E5%A4%A7%E6%A8%A1%E5%9E%8B)
  - 很多免费api, 国内版和国外版免费的api相同
  - 很多api是直接转发的其他平台，如硅基流动/快手万擎平台本身就提供的小模型， 质量不高
  - 有时会有限时免费的大模型

- [无问芯穹 LLM API 计费规则 ](https://docs.infini-ai.com/gen-studio/api/billing.html)
  - 基础服务：RPM=12、RPD=300、TPM=12000；默认情况下，租户均享受基础服务。基础服务不计费。支持在线自助升级为高级服务
  - 高级服务：RPM=120、RPD 不限、TPM=120000；租户可选择升级服务，享受更高限频。高级服务根据实际 Token 用量进行后付费结算。
  - 每个并发槽位代表 1 个正在执行的 LLM API 请求。LLM 包并发服务包并发槽位服务同样受 API 频率限制指标约束

- [火山方舟大模型服务平台-免费推理额度](https://www.volcengine.com/docs/82379/1399514?lang=zh)
  - ⚠️ 规则复杂, 注意每日超额使用token需付费, 部分模型名需要使用自动生成的id别名才能被采集和限免而不能使用预置的名称
  - rpm/tpm各模型不同，一般rpm为1w， tpm为500w
  - 单模型默认免费50w, 协作计划可奖励单模型200w
  - 免费额度仅适用于抵扣模型推理消耗的 token（50w 免费 token），不能抵扣使用各类插件、知识库等产生的费用
  - 免费推理额度，基础模型和精调后模型共享。
  - 模型支持deepseek/kimi/doubao/seedream
  - 协作奖励计划规则（第二期）和数据授权协议
    - 将在每日额度内自动按顺序采集授权模型推理接入点对应的调用数据，次日根据每个模型的前一日采集量返还等量的每日奖励包
    - 奖励包将在发放到您账号后的 30 个自然日内有效，到期后清零

- [DeepSeek API Docs - 模型 & 价格](https://api-docs.deepseek.com/zh-cn/quick_start/pricing/)
  - 扣减费用 = token 消耗量 × 模型单价，对应的费用将直接从充值余额或赠送余额中进行扣减。
  - 百万tokens输入（缓存命中）	0.2元
  - 百万tokens输入（缓存未命中）	2元
  - 百万tokens输出	3元

- 📌 [Z. AI DEVELOPER DOCUMENT](https://docs.z.ai/guides/overview/pricing)
  - tldr: 请求并发数量（在途请求任务数量）flash-2
  - GLM-4.5-Flash Free ✅
  - free: glm-4-flash-250414(20), glm-4-flash(200), glm-4.1v-thinking-flash(5), glm-4v-flash(10), cogview-3-flash, cogvideox-flash, glm-experimental-preview(5)
  - 没找到 用量统计/token统计 的界面
  - 非glm-coding-plan的api，仅提供openai格式，不提供 anthropic格式
  - [免费模型 - 智谱AI开放文档](https://docs.bigmodel.cn/cn/guide/models/free/glm-4.7-flash)
  - [智谱AI - pricing](https://bigmodel.cn/pricing)
  - [模型实时调用专属权益 及 标准单价 (很多免费)](https://bigmodel.cn/usercenter/equity-mgmt/user-rights)
  - 免费模型: [福利专区](https://bigmodel.cn/dev/activities/free/glm-4-flash)
  - [智谱AI开放平台 - 速率限制 - 用户等级限制](https://bigmodel.cn/usercenter/proj-mgmt/rate-limits)
  - [智谱AI开放平台 - 速率限制 - 通用默认限制](https://www.bigmodel.cn/dev/howuse/rate-limits)
    - 当前我们限制的维度是请求并发数量（在途请求任务数量）
  - [Z.ai - Rate Limits](https://z.ai/manage-apikey/rate-limits)
    - GLM-4.5-Flash	2

- [KAT-Coder开发工具接入指南-快手万擎-StreamLake](https://www.streamlake.com/document/WANQING/me6ymdjrqv8lp4iq0o9)
  - tldr: rphour-20~30
  - 免费已取消
  - ✅ [KAT-Coder-Air V1 模型免费使用规则 ](https://www.streamlake.com/document/WANQING/mh1g9y6knewv5sft54k)
  - 非高峰时段: 02:00-08:00 每6小时内您将可以发起200次对话请求，超过此请求数后，您可能会经历更长的排队等待时间或更严格的速率限制
  - 高峰时段: 08:00-02:00（次日） 每6小时内您将可以发起120次对话请求。在此时段，KAT-Coder-Air V1 的请求优先级可能会降低。您可能会经历更长的排队等待时间或更严格的速率限制。
  - https://wanqing.streamlakeapi.com/api/gateway/v1/endpoints/kat-coder-air-v1/claude-code-proxy
  - https://wanqing.streamlakeapi.com/api/gateway/v1/endpoints

- [LongCat API开放平台快速开始 | API 文档](https://longcat.chat/platform/docs/zh/)
  - tldr: tpd-500K
  - 每个账号每天自动获得 500, 000 Tokens 免费额度
  - 免费额度将于每日凌晨（北京时间）自动刷新
  - 输入和输出Tokens均计入消耗, 流式接口和段式接口消耗相同
  - 单次请求限制 输出文本：最大8K Tokens
  - LongCat-Flash-Lite 模型(non-thinking 68.5B-A3B MoE)，每个账号每天自动获得 50, 000, 000 Tokens 免费额度
  - https://api.longcat.chat/openai
  - https://api.longcat.chat/anthropic

- [腾讯混元大模型 混元生文计费概述 ](https://cloud.tencent.com/document/product/1729/97731)
  - Hunyuan-lite 免费使用
  - 经常拒绝用户的直接请求，而回答其他内容
  - [腾讯混元大模型 混元 OpenAI 兼容接口相关调用示例](https://cloud.tencent.com/document/product/1729/111007)
  - [腾讯混元大模型全面降价！混元-lite 即日起免费 _202405](https://cloud.tencent.com/developer/article/2419914)

- [百度千帆 - 百度智能云控制台](https://console.bce.baidu.com/qianfan/modelcenter/model/buildIn/list)
  - ERNIE-Lite 免费使用， 非开源， 上下文长度: 6K tokens + 2K tokens
  - [百度千帆 - 百度智能云控制台](https://console.bce.baidu.com/qianfan/modelcenter/model/buildIn/detail/am-ju3hi4ts39u9?tab=version)

- [讯飞星火大模型API](https://xinghuo.xfyun.cn/sparkapi)
  - 免费1个模型: Spark Lite 
  - QPS: 2
  - [星火大模型，燃情双十一-讯飞开放平台](https://www.xfyun.cn/activities/discount)
  - [讯飞星辰MaaS平台](https://maas.xfyun.cn/modelSquare)
    - 限免活动
    - 限免 z-image-turbo、Qwen3-Embedding-8B
  - 🐛
    - 少部分模型存在无法调用mcp的问题，如kimi-k2.5, 而glm-4.7支持调用mcp-tools; 调用失败的表现是， claude对话突然停止，且history里面没有相关对话日志
      - 排查过程: 中转claude模型能用mcp， 但讯飞的kimi用不了， 进一步测试讯飞的glm-4.7能用
  - 🛝

- [七牛 AI 大模型推理服务 - 七牛云](https://www.qiniu.com/ai/chat)
  - 采用按量计费的模式，根据实际使用的 token 数量收费，每月初出账。新用户享有免费额度
  - [AI 大模型广场](https://www.qiniu.com/ai/models)
    - 部分免费模型为其他厂商的免费模型

- [模力方舟（Gitee AI）](https://ai.gitee.com/serverless-api)
  - 提供了很多免费小模型，如 8b/4b, glm-4.6v-flash, 
  - AI图片检测: 并发数不限制，根据负载动态调整

- gitcode - [AtomGit AI社区 - 模型: 开源大模型 ](https://ai.gitcode.com/models)
  - https://ai.atomgit.com/serverless-api
  - [AtomGit AI社区 - 模型广场](https://ai.gitcode.com/serverless-api)
  - 注册即可领取 2M 免费 Token
  - 免费容器 1000 核时/月

- [DMXAPI官网：中国多模态大模型API聚合平台](https://www.dmxapi.cn/rmb)

- [Moonshot AI 开放平台 - 充值与限速](https://platform.moonshot.cn/docs/pricing/limits)
  - 赠送用完后需要充值

- [Xiaomi MiMo 开放平台](https://platform.xiaomimimo.com/#/docs/pricing)
  - 平台公测期间，模型推理服务免费

- [Cloudflare Workers AI Pricing](https://developers.cloudflare.com/workers-ai/platform/pricing/)
  - Our free allocation allows anyone to use a total of 10, 000 Neurons per day at no charge. 
  - Workers AI is included in both the Free and Paid Workers plans and is priced at $0.011 per 1, 000 Neurons.
  - gpt-oss-120b, 31818 neurons per M input tokens
  - gpt-oss-20b, 18182 neurons per M input tokens

- [GitHub: Prototyping with AI models ](https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models#rate-limits)
  - 限制很严格
  - Requests per day	50~150
  - Tokens per request	8000 in, 4000 out

- [huggingface Pricing and Billing](https://huggingface.co/docs/inference-providers/pricing)
  - limited to models smaller than 10GB. Some popular models are supported even if they exceed 10GB.
  - [Inference Providers](https://huggingface.co/docs/inference-providers/index)
  - Hugging Face provides a Serverless Inference API as a way for users to quickly test and evaluate thousands of publicly accessible (or your own privately permissioned) machine learning models with simple API calls for free
  - Every Hugging Face user receives monthly credits to experiment with Inference Providers
  - Account Type	Monthly Credits	Extra usage (pay-as-you-go)
  - Free Users	$0.10, subject to change	no
  - [HuggingFace changes to PRO subscription Inference limits, should I switch providers now? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ii4nst/huggingface_changes_to_pro_subscription_inference/)
    - The $2 credit limit is pretty weak for a $9 subscription. RunPod gives you way more bang for your buck - just pay for what you use and test as many models as you want.

- [Cohere API Keys and Rate Limits](https://docs.cohere.com/docs/rate-limits)
  - all endpoints are limited to 1000 calls per month with a trial key
  - 仅支持自研模型 Command A, Command R

- [AIHubMix - Models](https://aihubmix.com/models)
  - 免费模型不多，大多coding相关
  - free-per-model: 5rpm, 500rpd, 1Mtpd
  - mimo-v2-flash-free
  - coding-glm-4.7-free, coding-glm-4.6-free, coding-minimax-m2-free, kimi-for-coding-free

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

- [江城模境 模型广场](https://www.whaihub.cn/modelplaza/modelsquare/)
  - free: 百度 ernie-tiny/lite/speed
- [鲸智 模型广场](https://aihub.caict.ac.cn/modelplaza/modelsquare/)
  - free: free: 百度 ernie-tiny/lite/speed

- [超算互联网](https://www.scnet.cn/ycjh/index.html)
  - https://www.scnet.cn/

- [ZenMux](https://zenmux.ai/models?sort=pricingLowToHigh)

- [令牌查询](https://apikey.cifang.xyz/)

- [AI-中台 ](https://maas.gd.chinamobile.com:38559/maas/uifm/#/model-quota)
  - [广东移动发售token plan - LINUX DO _202604](https://linux.do/t/topic/1980940)
  - 定价为体验版-40/月，标准版-100/月；两个首月都是免费
  - 体验版-30000次/月，20000次/周，2000次/5h
  - 标准版-45000次/月，30000次/周，3000次/5h
  - 刚刚发现暂时只可用oai协议
  - 可用模型：minimax-2.5（其他模型陆续上线）
# paid-api 💰
- ai-plan2606
  - codex - gateway -- ¥50
  - claude - opencode + antigravity  -- ¥40
  - cursor - composer/auto  -- ¥30
  - kiro - claude  -- ¥50

- tips
  - 有时api请求慢, 可能不是卖家/服务器的问题, 换个ip看看
  - 重度开发时间，优先买天卡(10元/天)， 按量太贵
    - 不要花过多时间比价, 一般1亿token在2-4元就已经是业内非常划算的了, 节省时间去做研发
  - 直接在电报搜索倍率如 0.08 , 能快速找到候选商家, 优先选提供交流群和通知频道的, 在频道可以查看历史倍率是否正常
  - 站内直接充值时三思， 冲进去可能就跑路了退不了， 平台有保障
  - 当购买一个商品有很多渠道时，优先选择可靠的平台，售后/质保/退款更方便
    - 提供多天 model health status 的平台更可靠
    - 大站的售后可能被封控，如短信/邮箱的接码可能被限流
    - 特别在金额较大时，售后防止损失
    - 优先买提供售后交流群的, 能及时发现和反馈问题, 有交流群的也会跑路, 优先qq而不是tg
  - 付费站和公益站都会有rpm的限制，甚至限制都很大
  - 注意中转站的缓存命中率, 正常需要在90%以上， 部分低倍率的渠道缓存命中很低
    - 0.01的倍率差距不重要, 缓存命中率在93%以上时, 费用更低
  - 轮询的渠道不要太多，感觉会降低缓存命中率? 或者是new-api的缓存命中比sub2api默认就低? (实测sub2api高达94%)
    - 无人值守时才多号轮询, 人工干预时不需要多号
  - 廉价的套餐如lite-plan也可能慢/卡/不可用, 抢不到不必执着
    - 优先买容易退款的
  - 比较 主流coding-plan 和 中转/非正规套餐如cursor/devin 的价格/token额度, 灵活选择，没必要执着
    - 1亿token大概花费多少, 算起来比较通用
  - 利用bug的包月套餐不要买, 突然修复后可能直接高倍率刷光余额
  - 小众模型的中转站也可以考虑，比如grok
  - 中转商的价格每天都在变化, 套餐也在改变, 不要在一家花费过多
    - 很可能注册的第一天会显示低价，后面就恢复正常价格了，注意误导
    - 在5月13号，几乎所有成品号渠道都失效了，所有店铺(无论贵的还是便宜的)的源头渠道几乎相同，，，以后买便宜的就行了
  - 月初是openai集中清理风险型用户和欺诈性用户的敏感时间, 很多便宜的渠道会挂掉
    - 封号的时机注意周初和月末， 周初前几天可能会清理，月末很可能集中清理，最好在北美周二买号
  - 带at/rt的帐号价格不同，在不同的封控政策下，可使用时间差异很大，最好选择 RT(可长期) + 可刷新AT(手动刷新来解决401问题)
    - 廉价的AT号几乎都不提供刷新，在每天掉号的状况下经常用不完周限，很浪费
    - 如果有rt和邮箱取码，可以手动接码来刷新AT，也是一种折中的方案(介于2个AT号 和 一个接码成品号)

- sources
  - [货源广场 - 链动小铺](https://pay.ldxp.cn/merchant/my_parent/source_square)
  - [阿华的AI比价聚合站 ](https://ahua-ai-price-aggregator.onrender.com/)
  - [AI 商品库存聚合搜索工具 ](https://goods.moo.kim/)
    - [售票处的小店 - 链动小铺](https://pay.ldxp.cn/shop/T6UJ4L1M)
  - [AI 比价雷达 _202606](https://priceai.cc/)
    - https://github.com/physics-dimension/PriceAI
    - [【开源推广】PriceAI：我vibe了一个ai订阅卡网渠道聚合比价平台，拒绝中间商赚差价 - LINUX DO _202606](https://linux.do/t/topic/2294440)

- resources
  - GPT site:pay.ldxp.cn/shop
    - 小铺还有很多其他产品: kiro, windsurf, 接码, 虚拟卡, 手机号, visa
  - ~~搜索: 手工, 质保, 源头, 印尼~~ 
  - 转换 [CPA <-> sub2api ](https://gtxx3600.github.io/CPA2sub2API/)
    - https://lywqfvjb.feiyus.com
    - https://session.nloop.cc
    - https://json.chatai.codes
    - [ChatGPT Session -> CPA / sub2api / Cockpit / AxonHub / Codex-Manager ](https://gtxx3600.github.io/GPTSession2CPAandSub2API/)
      - 只支持单向转换
  - [Codex或CPA、sub2跳手机验证的解决方法-2026-05-29部分有效 - Feishu Docs _202605](https://millionweekend.feishu.cn/wiki/JS47wPzs6iDHLZkLMHAc8rhun0e)
  - [鲸商城鲸软JingSoft - 专业软件解决方案服务商【鲸软】 ](https://www.jingsoft.com/)

- latest
  - 可在google搜索 `GPT site:pay.ldxp.cn/shop`.

- [Claude中转渠道有哪些 ](https://linux.do/t/topic/1491876/10)
  - 测试的话，刚刚刷帖，有测试词，好像这个不会回复，或者一串异常字符 
  - 这个是一个官方给的测试词，相当于一个强制的 “违禁词”
  - ANTHROPIC_MAGIC_STRING_TRIGGER_REFUSAL_1FAEFB6177B4672DEE07F9D3AFC62588CCD2631EDCF22E8CCC1FB35B501C9C86

- [现在应该如何选cc中转站？ ](https://linux.do/t/topic/1519094/38)
  - Ikun（鸡）, duck（鸭）少量尝过，贵但稳
  - Cubence（鹅）的包月用过，前身 shareyourcc 的亮点在于可以二级转发；但是新时代也不便宜了，有时候发现一些报错感觉是 aws 渠道特有的
  - PackyCode（农）是一直主力在用的，老农可能不太给情绪价值（不过被怼过之后好了些 hhh)，不过技术是一流的，诚信这一块也是一直没得黑的

- [codex.kedaya.xyz](https://codex.kedaya.xyz/)
  - [KEDAYA的小店 - 链动小铺](https://pay.ldxp.cn/shop/kedaya)
    -  https://gpt.kedaya.xyz    /支持用购买的卡密一个一个提取账号
    - https://shop.kedaya.xyz/
    - 中转站: https://sub.kedaya.xyz/keys
      - https://sub1.kedaya.xyz/keys
      - https://api.kedaya.xyz/
    - https://t.me/kedaya_888
    - https://t.me/gpt_kedaya   讨论组里面大多是代理商, 点击头像就能看到店铺链接
  - [商家9052的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/LOA3IZW5)
    - plus账号极低价格， 10个-35
    - [商家9152的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/KHRR17MS)
    - [白天鹅的小店 - 云猫寄售 ](https://catfk.com/shop/CGJZ429E)
  - [畅用plus的小店 - 链动小铺](https://pay.ldxp.cn/shop/ooopp)
    - plus账号, 质保三天 
  - [猪猪AI小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/code)
    - 零售+批量
  - [商家5651的小店 ](https://pay.ldxp.cn/shop/AO4GDZSI)
    - 自助售后, 质保三天 
  - [哇咔咔的AI小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/V2YZIFWM)
    - 开发了ldxp扩展
  - [喜乐GPT plus xileyyds的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/KK5XQNYK)
    - https://api.xileyyds.xyz
    - 低价代理商
    - 低价0.02 小并发(10)中转站， 鸭总0.03
  - [山姆奥特曼商店的小店 - 链动小铺](https://pay.ldxp.cn/shop/1E5DST9P)
    - plus账号-6, 质保三天 
  - [超低价GPT会员的小店 - 链动小铺](https://pay.ldxp.cn/shop/dijiagpt)
    - 【手工】【30天】GPT-Team / Business 高质量激活码（质保3天）
  - [普露米AI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/plumire)
    - 低价号多
  - [OAI DO的小店 - 链动小铺](https://pay.ldxp.cn/shop/oai)
  - [GPTPLUS的小店 - 云猫寄售 ](https://catfk.com/shop/LFQJHO5C)

- [NexusVault 中转号池交易台(类似交易所) ](https://trade.livetools.top/workspace)
  - [协议登录测试台 ](https://token.livetools.top/)
  - 面向中转站主和供应商，统一处理账号入库、质量检测、余额提号、自动补池、质保售后和结算核账
  - 买号补池: 余额提号与自动推送
  - 供应入池: 批量导入与质保上架
  - 售后结算: 退款核账与付款申请
  - https://inbox.ignore.md  /ngcoffee
    - 注意第二次接码无解 Gopay渠道 + Outlook邮箱 + 可接邮件
  - https://email.xrfcloud.xyz /kaopu
    - 支持邮箱验证、手机验证

- [麦当当plus的小店 - 链动小铺](https://pay.ldxp.cn/shop/EOTZ17J2)
  - 交流: https://t.me/maidangdangplus
  - 兑换及售后：https://plus.geekzone.cloud
  - 在兑换后48小时内账号有问题，可以到网站提供兑换码或者邮箱兑换新的

- [NFXW的小店 - 链动小铺](https://pay.ldxp.cn/shop/MYIAKTYT)
  - 交流 https://t.me/aivip6688
  - 账号检测 https://ban.nloop.cc/
  - https://json.nloop.cc/
  - 邮件取件助手：https://email.nloop.cc/
  - CPA ↔️ Sub2API：https://conversion.nloop.cc/
  - plus-8.5

- https://nissanserena.my.id/otp    /印尼
  - https://zovlyx.fun/
  - [哈哈的ai杂货铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/22DHYNNV)
    - plus账号, 质保
    - 现在起降价至4r，发货的格式是账密，后面还带上了at，是可以直接导入到sub2，也可以登录web端。 我这的号不是无卡pp流!
- [叮当猫稳定AI渠道的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/dingdangmao)
  - 品类特别多， 里面可以找到质保2天的
  - 只做群里面的三级代理
  - [xiamai gpt_plus_批发的小店 - 链动小铺](https://pay.ldxp.cn/shop/xiamai)
    - 低价渠道多
  - [青蛙AI·低价源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/qingwaAA)
  - [464的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/7HVUEC3Y)
    - 品类多
  - [MLYF的AI工厂的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/TAFHH1PS)
    - 质保、非质保 分开
  - [GPT成品plus的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/FEO0CLZ6)
  - [ParHom的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/parhom)
    - Cursor Auto｜超账单｜库存号
    - Cursor Pro Plan 20$官方套餐【已用完高级模型额度】
    - 可Auto、Composer模型｜可对接Api
  - [奥仔小铺的小店 - 链动小铺  ](https://pay.ldxp.cn/shop/aozai)
    - windsurf低价
- [AI源头-oak的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/oak)
  - tg频道：https://t.me/dabaizu 
  - 接码多, paypal

- aidark [邮件与账号工具台](https://mails.aidark.icu/)
  - [xiaoxiao的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/YD93JLNG)

- https://plus.keria.cc.cd/ 
  - [PLUS直营店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/FNAOIGBK)
  - 卡密下单起1小时内自动失效, 还请快速兑换，icloud邮箱
  - 提卡 https://plus.keria.cc.cd/
  - 昨天到今天有六万多次取码, 使用的人太多了，限流了， 号卖不出去，服务器还在吸血
  - rt还能产吗，能产的话给什么价
    - 不能产了, 除非接码
  - 刚复活了 30个账号， 连一周前的账号 都没掉PLUS, 接码 就能活, 一周前从群主这里拿的 401 接码都还在
    - 就是要手动, 有点麻烦
  - 现在都需要 验证才能直登 codex, 还是得接码后才能登录
  - 有rt他也给你掉
    - 别折腾了 有那个时间不如多便宜卖几个
  - 也不知道哪里听的rt不掉的, 我600个怎么掉了
  - 有些显示401的，去登录网页端没死的，然后去获取https://chatgpt.com/api/auth/session数据，最后用Claude转换一下sub2的json格式就行了
  - 一个码是不是能接很多号? 5
  - [icloud 邮箱 GPT PLUS直营店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/A87R3DZP)
  - [商家8190的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/AY1FXLQX)
  - [AI会员小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/XLF7RCJG)
  - [青熵的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/P9HPIPWA)

- [小猫GPT源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/1D0LD6BR)
  - 频道通知链接：https://t.me/+UkH0O6HZLBM5MTJh

- [吱吱鼠卡网](https://zzshu.com/)
  - https://t.me/gptteamzz
  - https://t.me/ttshushu
  - 宽松期会发布低价渠道

- [GPTPLUS.icu team 的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/YQJERQW3)
  - 自助激活页面：https://gptplus.icu
  - 纯净激活页面：https://icustore.icu
  - 防迷路请进客户⑥群 1091880491
  - 【手工】【30天】GPT-Team / Business 高质量激活码（质保3天）
  - [极速的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/jishu)
    - 【手工】【30天】GPT-Team / Business , 源头 GPTPLUS. ICU 
    - icloud邮箱

- [Chat-gpt（源头）的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/OGBZJ5SY)
  - team

- http://155.229.50.232/email-assistant 
  - [plus源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/IY16OXB7)
    - GPT-PLUS-JSON 中转站版
    - 售后群QQ群1085440916，客户交流群1097585298
    - 支持登录网页版，支持批量兑换批量生成sub2api和CPA两种格式，支持登录codex
    - 登录codex会出现手机验证，需自行解决
  - [xybbz_api的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/BZKYFZG4)
    - 邮箱查询地址：   http://82.156.59.169:8848/ 
    - 7元

- [Apex AI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/apexcode)
  - 卡密取货地址为  https://apexcode.eu.cc 或 https://register.lovelymira.com/
  - 取号内容为邮箱+验证码+无rt格式的JSON成品，单个卡密可以重复查询多次，不会用可以多看看介绍
  - 卡密有效期3天，3天后销毁，不要囤货
  - 也可以使用批量上号功能生成成品授权文件，支持sub2api和CPA两种格式
  - 还提供高价的gmail版plus
  - 可sub2api  <==>  CPA互转，转换格式地址 https://register.lovelymira.com/format-converter

- [AI杂货铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/PBY2YIR3), /周全
  - 低价渠道多
  - [爱喝奶茶的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/V3MBPGC5)
    - 号多
    - [爱喝奶茶的小店 - QXVX Pay](https://pay.qxvx.cn/shop/EUTV8STA)
  - [AAA plus批发的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/F6077NPC)
    - free + plus
  - [商家9237的小店 - 链动小铺](https://pay.ldxp.cn/shop/RXKT7LFX)
    - https://otp.forestpolarpilot365.shop/
  - [发呆的小店 - 链动小铺](https://pay.ldxp.cn/shop/PL4EBAMI)
    - https://otp.the22222.org/
    - https://t.me/GPTattackz
  - [商家3593的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/BQMWH5MY)

- [AI杂货铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/ai-shop)
  - 管理员小店 [faka.gsyun.cloud ](https://faka.gsyun.cloud/)
  - AI科研交流群：560520490
  - [ChatGPT源头的小店](https://pay.ldxp.cn/shop/B8TNSEBM) , 还有开单独中转站
    - 提供2类账号: hotmail邮箱+密码登陆，邮箱+验证码登录
  - [视界AI的小店 - 链动小铺](https://pay.ldxp.cn/shop/shijieAI)
    - 印尼， 提供批量折扣
  - [shop.aitonse.com](https://shop.aitonse.com/products)
    - 印尼

- [极速AI源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/1CMPMUXM)
  - 低价 https://redeem.buycodekey.com/
  - PLUS (icloud邮箱1卡1绑) 带At(不带rt)不带账密质保首登
  - PLUS (精品雅虎邮箱1卡1绑) 带rt，不带账密质保首登
  - cpa格式自己转换:  https://cvt.okcode.cc.cd/ 
  - [☀️的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/J0Q89LSE)
    - 只是个代理
  - [商家4955的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/V38JA2MD)
  - [gpt低价货源的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/5XX41BQK)
  - [babu的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/9T40GAS6)
    - 前往  https://downs.yossq.com/ 进行兑换获取邮箱和cpa
    - plus账密一个月  质保首登 带cpa/sub2文件(AT)  
  - [foxfishs的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/foxfishs)
    - icloud邮箱，一号一绑, CPA和Sub2api格式，只适合中转站
    - 兑换网址： https://diamon666.xyz/ 
- [鼎尚AI 商家5812的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/8QYLBYPO)
  - 提卡 https://ai.cdns.ccwu.cc/  , 提卡网站已经更新上线了自助刷新AT功能 
  - 卡密现在发卡之后有效期只有6小时。超过6小时卡自动销毁后无法使用不售后
  - [玛玛哈哈的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/GRFAVRBF)
- [ngcoffee codex小铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/BGPNHEF6)
  - 20份起售, 散户别碰
  - 需要登录网页的可去 https://inbox.ignore.md 贴入JSON收邮件验证码和登录密码
  - 只要账号没封 AT过期可自行登录网页再取AT
  - 401后自己登录手动转sub2, 重新登录刷新 session 再转换 sub
- [ChongAPI-源头商家的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/TSCE0SEH)
  - 只做批发，不零售
- [ 9527code ](https://fk.9527code.com/)
  - ¥5
  - [大熊AI小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/G09AC5SS)
  - [企业级AI交易平台的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/ULOOBF79)
- [Ai Plus shop](https://shop.558669.xyz/)
  - 兑换网址：https://gpt.558669.xyz
  - At成品号（无Rt）, 一号两绑，目前存活率很高，已有3天；
  - 只出中转格式，CPA和Sub2api格式，不会用的不要买
  - https://faka.skiii21hc11.cc/
- [GPT365商店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/gpt365)
  - [shop GPT365商店 ](https://new-shop.gpt365.wiki/)
  - 账号发货格式 卡密|激活地址，卡密激活成功后，将自动获取账号信息， 支持下载 CPA / Sub2 JSON
  - 卡密必须在48小时内兑换，若在规定期限内未兑换，将直接封禁卡密，不予退款

- [黑鹅小铺的小店 - 云猫寄售 ](https://catfk.com/shop/ithte)
  - plus-¥2
  - 不包codex接码， 实测需要绑定手机号
  - https://plus3.yhmoai.online/?key=
  - 夏蜉蝣 [gpt plus的小店 - 云猫寄售 ](https://catfk.com/shop/2JXXIUKT)
    - 成品号提货网站： http://gpt.airelay.cn.mt
    - 只支持json导入，不会用的不要拍
  - [sanguine的小店 - 云猫寄售 ](https://catfk.com/shop/sanguine)
    - at号4r，rt号5r
  - [风里的ai小铺的小店 - 云猫寄售 ](https://catfk.com/shop/I7DPO2IK)
    - 很多接码
  - https://team.longxiadev.store/
  - [Antipro 的小店 - 云猫寄售 ](https://catfk.com/shop/W5YJ6A0E)
  - [商家696的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/Kegan04)
- [旋律plus的小店 - 造梦企发Pro，造梦寄售平台 ](https://fh10.zmfaka.cn/shop/XGLVB89E)
  - 低价plus

- [Tora-雪诺AI源头分销小铺的小店 - 链动小铺](https://pay.ldxp.cn/shop/Tora)
  - 通知 https://t.me/Tora_AiShop
  - 提供正规充值 gpt/claude 的方式
  - 品类很多
  - plus成品号-质保1天， 15
  - plus成品号-质保30天， 75
  - GPT TEAM 手工直拉 无质保， 35
  - GPT Cyber认证【Persona认证】， 100

- [AI小铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/echo_dream)
  - https://gpt.aveve.xyz/ 
  - 手机接码推荐：https://hero-sms.com/cn  找安哥拉+244地区，接码成功率高
  - 低价team子号
  - [ai主理人的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/AV8G25IF)
    - 低价team
  - [API聚合转发源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/QN3MH16E)
    - team子号 有rt CPA json 无账密目前测试活三天
  - [青蛙AI·低价源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/qingwaAA)
  - [远程技术服务站的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/yunduo)

- [源头GPT的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/1DM0L7CR)
  - 100个 free账号 Token（实时验活）CPA + sub2api格式
- [XC的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/K9NFLN0C)
  - 账号----密码----邮箱----自行解决需要登入验证码的问题
  - 如果需要跳过手机号认证，只能使用本地中转方案
- [plus专卖店的小店 - 链动小铺](https://pay.ldxp.cn/shop/RNJDBGD4)
  - PP渠道｜无质保，当日抛使用
- [464的小店 - 链动小铺](https://pay.ldxp.cn/shop/7HVUEC3Y)
  - 通知频道：https://t.me/hdunzx
  - 质保两天
    - 一天就上几个，引流的
- [yimoAi-US的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/CQRJKJ0N)
  - 频道：https://t.me/songbai0420
- [波哥小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/boge)
  - 提取  https://yuyu.chiyiyi.cloud/ 
- [天选AI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/txai)
  - https://plus.oai.do/ 
  - [seven85777的小店 - 链动小铺  ](https://pay.ldxp.cn/shop/SEVEN857)
    - 切换日本节点注册新号，具有免费试用资料
    - 5个起购直冲渠道cdk-质保6小时（必须用日本节点注册新号）
  - [桃俊泽的AI小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/DJOBBG3H)
    - GPT plus日抛成品号x1
  - [GPT小杂货铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/YPFLK17T)
    - GPT plus账号(印尼），一般日抛，没有rt ，就at ，日抛要什么rt？ at能用10天
    - 发货格式是：  txt 文件 一行就是一个json
  - [小NO plus的小店 - 链动小铺](https://pay.ldxp.cn/shop/BWGFCYG1)
  - [秋刀鱼精品小铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/qiudaoyu777)
    - 购买后需要手动联系来索取json
  - [faka.jnmtk PLUS 账号 ](http://faka.jnmtk.com/)
  - [随欲小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/MO2JGWG9)
    - 高价plus
  - [一只狗子的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/2IG615LQ)
  - [Xun AI - 海外效率工具订阅的小店 - 链动小铺 5](https://pay.ldxp.cn/shop/XunAI)
  - [AI小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/HGQW9XKA)
  - [AICA的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/aica)
- [卓建AI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/THJ70HZO)
  - sub2格式json不带账密质保首登
  - 格式转换网站 https://lywqfvjb.feiyus.com
- [sekirocloud的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/L9P7JDGN)
  - sub2api josn格式
- [BMCCA小铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/BMCCA)
  - 频道：https://t.me/lucky_fores
  - 1r 带rt的plus，json发货，带rt可以自行刷新at，支持cpa sub2，直接私我

- [青蛙AI·低价源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/qingwaAA)
  - plus成品team的，，只能反代codex。实测平均每个15刀
  - [GanAI小铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/ganai)
    - Team稳定版 7日卡
    - 有效期至 05-28 + 7 版本，稳定版车位有效期过了后一般可以继续用再 7 天，但是如果用不到要自行承担风险。
  - [壹码工坊的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/1aicode)
  - [GPT TEAM 日抛号的小店 - QXVX Pay ](https://pay.qxvx.cn/shop/3V3CBG6P)

- [度偶Ai专卖店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/G3EUVLR7)
  - gpt plus月订阅CPA json(质保3天)
  - 无密码，无codex登录。质保3天，出现401封禁可换1次账号。
  - 购买后获得兑换卡密，卡密到 https://chat.duou.ai/download/ 网站兑换gpt plus cpa json

- [花无缺的小店 - 9. PLUS ](https://9.plus/shop/bingbong)
  - https://t.me/bingbongAI

- [AI HOME的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/MEDDEX4V) , 保证金1000元
  - 群：https://t.me/aihome123
  - 无低价号
  - plus-32
  - pro5x-140
  - pro10x-210
  - Gpt认证Kyc-100

- [咕咕Ai源头号商（招代理）的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/gugu)
  - 价格较贵, 只做批发

- [TangSeng AI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/tangsengai)
  - 提供不限量token的日卡(¥19)/周卡(¥99)/月卡(¥299)
  - 按量: ¥5-800w, ¥11-2000w, ¥30-6000w, ¥50-0.125b
  - [这个api中转站的定价如何？ _202603](https://www.nodeseek.com/post-649864-1)
  - 12/分钟的请求量单个任务都跑不下去，经常是跑一会就断了，然后一分钟到了又继续，昨天买个19一天不限量的的根本无法流畅使用
    - 主要是并发太低了，单线程都跑不了，不然我还是愿意买的
  - 月卡是12，天卡设置的6, 因为买天卡狠狠蹬的太多了, 单线程没有问题，多线程是顶不住的。
  - 大家有多线程需求的可以单独找我
  - 不支持代中代, 就是再放到sub2api里面使用

- [松松的小店，招代理的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/gpt_songsong)
  - [松松 AI ](https://songsongcard.shop/)
  - 交流群: https://t.me/+5UfugtLTLq40ZGQ0
  - 无低价号
  - plus-35
  - pro5x-160, 质保400
  - pro10x-250, 质保650

- [YCYAPI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/ycyapi), 已被封禁
  - YCY供应商订阅: https://t.me/+n5uswJrZIAg2NTk1
  - plus成品号-10, 质保3天, 反代质保首登---不是日抛
  - plus-30
  - pro5x-175
  - pro10x-270

- [LToken的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/12P8XO9Z)
  - 公益Plus/Team机器人
  - 品类非常多
  - 低价号很多， 很多10个起购
  - plus-8
  - team-3
  - pro5x-175
  - [咕咕嘎嘎 GPT Plus的小店 - 链动小铺](https://pay.ldxp.cn/shop/E7AEE7TS)
    - 和上面的plus很像

- [AI源头小铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/lwq)
  - QQ群：1080624221 , 进群需提供订单号
  - plus-6, Plus新号慢充需要排队（无质保）

- [FantasticAiCccx的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/1C57XPY2)
  - 主站链接：https://testvideo.site
  - 加速节点：https://hk.testvideo.site
  - gpt中转, 3元-$100, 1.5倍率-换算下来是0.045一刀, 
  - Plus号池是2.5除了不能生图都一样, 1.5倍率是Free, 没生图而已

- [GPT PRO的小店 - 链动小铺](https://pay.ldxp.cn/shop/progpt)
  - pro5x-236, 质保1月

- [懒虫AI](https://buy.aieasy.plus/)
  - [懒虫AI充值的小店  ](https://pay.ldxp.cn/shop/LanChongAI)
  - TG客服: https://t.me/LanChongAI
  - pro5x-140
  - pro10x-250

- [见AI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/JIANAI)
  - TG频道：https://t.me/JIANAI996
  - 兑换网址：aichong.plus

- [52AI店铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/52ai)
  - 品类非常多
  - TG客服：https://t.me/x87110  , 仅通知，无聊天

- [AI源头小陈的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/AItools)
  - 客服微信BIGLanjiao00
  - 品类多
  - pro5x-350

- [ai源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/dagou.vip)
  - plus成品账号-15，特价商品极不稳定，随时会封，3件起购
  - pro5x-214
  - pro10x-310

- [九渊Ai源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/jiuyuan)
  - 售后TG：https://t.me/jiuyuanai
  - plus-150
  - plus土区-120

- [codex-for.me ](https://codex-for.me/)
  - [vibe coding 专营的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/GUBERQA2)
  - 日卡-5
  - 月卡-59

- [Ai2You智友社，让更多的人用上更好的AI的小店 - 链动小铺](https://pay.ldxp.cn/shop/282D9KDL)

- [逍遥AI批发小铺的小店 ](https://pay.ldxp.cn/shop/1490777)
  - plus-质保15
  -  https://ai.dcfkj.com/xin/chatgpt 
  - [出GPT Plus直充卡密8元 _202604](https://www.nodeseek.com/post-687488-1)

- [AI 源头旗舰店的小店 - 链动小铺](https://pay.ldxp.cn/shop/CodexBro)
  - 中转站: https://www.inroi.shop
  - 低价号多，但及其不稳定
  - Plus土区iOS官方直充月卡（无质保，987渠道）， 100

- [AI源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/shiwanfute)
  - TG：https://t.me/mikaksa2
  - 仅gemini

- [玩偶小铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/WOXP888)
  - https://t.me/WOXP66
  - 无pro

- [5jupe1的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/5jupe1_5)
  - 可以加QQ：3673905468或添加公众号：5jupe1, 或者电报客服机器人：https://t.me/jupe1_5_bot

- [逸轩ai店铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/xuanplus/)
  - team-5

- [沐风的小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/mfshop)
  - pro5x-185, chong

- [炒鸡变黑的AI店的小店 ](https://pay.ldxp.cn/shop/chaoji)
  - plus-无质保6

## ide/vendors

- tips
  - ? 大厂的优惠活动更多, 优先cursor/kiro/antigravity
  - 二手号: 速刷号掉号快, 不会多人用, 质保掉号还是几天, 优先账密而不是token登录

- cursor内置的都是非常高级的模型claude/haiku/gpt/gpt-mini/composer/gemini/grok/glm/kimi, 所以用auto模型完成普通开发也可考虑
  - 咸鱼上的cursor-pro废号可考虑，保证登录官网且是Pro号，可以自己修改账号密码，有效期15以上
    - 优先考虑账密登录， 不考虑 发货格式：SessionToken/AccessToken 
    - 👀 部分号来自速刷cursor pro, 刷完了再转卖
    - 速刷号速刷号！非月号非月号，在1天内使用完毕
    - 部分号是拼车收过来的号 不可能保证一定一个人用 部分账号两人共享使用。
  - 高级模型额度已用完，只剩Auto+Composer模型额度，大概在100刀额度。 
  - 可在账户余量界面看到剩余composer/auto的用量，来估算余量
  - ✨ 有商家甚至推出了自动换号的月卡， 价格合适也可考虑
    - 不考虑 不是直接给账号密码，不是Pro号，按激活时间，24小时50个号，不会一小时内50个号一下放开
    - 不是pro，不是插件，不是直接给cursor账号，需要软件来换号
  - [cursor订阅原来不支持本地provider吗 - LINUX DO _202606](https://linux.do/t/topic/2476713/1)
    - 要对公网开放。我的方案是服务器部署Sub2API
    - 其实也不算特别奇怪() 毕竟允许自定义 provider 就相当于允许查看完整的 agent harness 和提示词工程了，可以分析出很多东西来

```
你好, 我想买个划算的用完了高级模型的 cursor pro。
1. 请问你这个是不是用漏洞的速刷号，据说速刷号掉号快, 发给我的是正常账密，还是token？
2. 买好后是我一个人用吗，还是多人用, 我不想买共享的
3. 下个月几号到期, auto模型用了多少了， 用的不多我能接受
4. 我不会反代，就正常用auto模型， 如果掉号会质保换号对吗
提前问清楚了，免得售后麻烦，大家都方便 🌹
```

- supergrok支持 grok-composer-2.5-fast, fast的价格是2.5的6倍，
  - 所以 ¥25的supergrok 提供的composer模型 不如 ¥20的cursor pro提供的100刀auto池
  - supergrok不能包能用到一个月, 也不稳定

- [Cursor 专卖的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/cursor-pro)
  - cursor--¥80
    - 质保十五天！支付宝支付，正价充值
    - 邮箱----密码----Token
    - 当前商品是提前预制，非现场激活，有效时限 25 - 30 天左右
- [黑客AI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/Loong)
  - [词元神 - 全球AI聚合平台 ](https://ciyuanshen.top/)
  - cursor--¥50
    - 日抛速刷号无质保，默认一天内掉Pro订阅，token登录
- [小小工头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/IFMZTI8P)
  - 品类多
- [Lyla-精灵小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/lyla)
  - cursor 天卡/周卡/月卡 - 5/19/50
    - Cursor月卡=【激活后30天内有效+75个账号（共计15000积分，每次换号消耗200积分）Auto模型+无感秒换号+两台设备+支持win、mac、linux系统】
  - kiro 天卡/周卡/月卡 - 6/19/50
    - 插件只支持win10以上电脑，支持mac,而且支持ssh
- [Gemini Pixel 设备认证 ](https://autopixel.qzz.io/blackcat)
  - 品类多

- [AI小铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/XWTVY86A)
  - kiro
- [AI服务站的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/ikun666)
  - 发货账号为谷歌邮箱: 账号----密码----辅助邮箱----2fa密钥
  - kiro官网选择谷歌邮箱登录，输入账号密码登录，选择身份验证器验证，去2fa.fun网站输入2fa密钥获取6位数验证码
- [蒲美丽のAI副食店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/YXCTJAH4)
  - 只发凭证，不发账号，自行导入使用，质保首登
  - 反代可用 claude opus
  - 低价kiro
- [KiroSwitch官方直营店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/Z3VSKEGC)
  - pro

- [Gemini源头供货商的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/pixelshop)
  - gemini年卡--¥18
- [gemini专家的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/gemini123)
  - 反重力--¥18
- [AKMOZ-魔卡AI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/AKMOZ)
  - gemini年卡--¥65
- [Gemini丨Telegram的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/Pro)
  - gemini产品多
- [Antipro（请看店铺公告）的小店 - 云猫寄售 ](https://catfk.com/shop/Antipro)
  - Gemini PRO一年会员成品 （随机地区，不包gcp）, ¥13
    - 仅质保首登，2fa验证码可以去  https://2fa.fun/ 获取验证码
    - 如果你说奔着反重力来的，想便宜些去买美区pro，想省事就买反重力pro
- [金幺の小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/911)
  - 反重力--¥22
- [奥特曼丨ChatGPT的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/atmgpt)
  - 品类多
  - 反重力--¥46

- [Windsurf专卖4988的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/3FR7Y3PY)
  - 谷歌母号, 不质保，只保拍下立马登录满配额。有效期10天左右。
- [Pine12345的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/PY91LPJ0)
  - devin70美刀账号
- [AI账号百货通的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/windsurf-test)
  - Windsurf 全新 纯谷歌邮箱账号 （wf 账号、密码发货）无质保（下单请思考）
- [YOUC的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/INJXURRY)
  - 临期windsurf很低价
- [claude 供应商的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/73QTX1TH)
  - 过期日期临期，剩余时间就3-7天随机
- [AI账号百货通 962395845的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/windsurf-test)
  - Windsurf 谷歌别名（子号） 自行研究 无质保
- [A8 小店 购买账号 - 链动小铺 ](https://pay.ldxp.cn/shop/16888)
  - 顶部售后群有切号软，可导入账号一键切号查看额度等 
- [Windsurf专卖4988的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/3FR7Y3PY)
  - 送免魔法登录插件

- [AI万能工具箱的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/grok)
  - grok品类多
  - SuperGrok 独享账号 一月会员, ¥55
  - SuperGrok 独享账号 三个月会员, ¥100
  - SuperGrok 独享账号 一年会员 官方渠道, ¥240
- [ai源头批发的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/ATURU7MU)
  - SuperGrok 30天, ¥35, 质保1天，质保5天45
    - 账号模式是3天试用然后自动续费
    - 不能包能用到一个月，小白建议拍120直充款，稳定不掉订阅
- [云边小铺（招代理）的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/one)
  - x premium + 赠送3/6/12个月的grok
- [Ai2You智友社，让更多的人用上更好的AI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/282D9KDL)
  - Super Grok 稳定特殊渠道季卡独享成品号, ¥88
- [金金Ai源头批发（招实力代理）的小店 - 云猫寄售 ](https://catfk.com/shop/jinjin)
  - Grok Super直充月卡（30刀，质保不掉订阅版）, ¥65
- [聊聊AI ](https://talkai.cyou/)
  - gork

- [GGgrok ](https://ggrokheavy.xyz/pricing)
  - 旧版 [New API ](https://newapi.neokoaigc.com/pricing)

## 发卡网

- [Plati. Market : digital goods marketplace ](https://plati.market/)
  - 很多俄罗斯大佬卖ai

- [KnauHip-Ai — 高级 AI 工具发卡站 ](https://www.payline.pics/)
  - 很多低价帐号如kiro/cursor都是10个起购

- [聊聊AI ](https://talkai.cyou/)
  - gork

- [月亮AI ](https://aimoonai.com/)

- [发卡网 - 在线购买虚拟商品 ](https://sd.ncet.top/)

- [鹰鹰发卡](https://fk.apiway.cc/)
  - 下单前请检测自己的号有没有试用资格，如果拿没有试用资格的普号导致无法升级

## 中转站

- tips
  - 很多中转站带有峰值倍率和闲时倍率, 夜间多用闲时倍率, 白天可用半公益站
  - hub.linux.do深夜福利的cc倍率也能达到0.02, 而付费的cc普遍在0.3, 所以可以适当留好余额在hub用cc
  - 少数中转站会用非常短暂的低倍率吸引充值, 充完后取消低倍率只剩高倍率, 所以不要充多了

- resources
  - [LinuxDo商家评价平台](https://rate.linux.do/)
  - [模型中转状态检测](https://check.linux.do/)
  - [模型状态检测 御三家](https://jiankong.qianxing-ai.cc.cd/)
  - [AI中转站推荐 | Claude/Gemini/Codex中转站评测对比](https://www.helpaio.com/transit)
    - 评分结果与L站评分基本一致
    - 提供了很多折扣码

- [zzshu /NewAPI ](https://zzshu.cc/pricing)  , 长期运营
  - [吱吱鼠AI的小店 - 云猫寄售 ](https://catfk.com/shop/SXS913NA)
  - 中转站仅支持gmail
  - kiro--0.2
  - plus--0.031

- [刀刀刀-天才程序员 - /NewAPI ](https://codexapis.com/pricing)
  - [刀刀刀-天才程序员的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/6YQL25Q0/b6scwi)
  - QQ群：740937090
  - kiro--0.12/0.3
  - plus--0.035
  - 找找看 cc-0.06
- [cc-api  /New API](https://cc-api.chat/pricing)
  - 专注于kiro中转
  - kiro--0.12, 低缓和高缓都是0.12
- [wangwang - /Sub2API ](https://wangwang.sbs/dashboard)
  - kiro-0.18/0.2
  - kiro分组多，还有cc
  - plus--0.04

- [超超 mouubox  - /Sub2API ](https://sub2api.mouubox.com/dashboard) , 已充值, 副站
  - [/Sub2API ](https://api.mouubox.com/home), 主站
    - 一个主站一副站, 副站sub2api.mouubox.com,
    - 现在好像sub2api这个要绿一点
  - 主站更新倍率更及时, 副站有时不会降到活动倍率
  - [秒速 5 厘米的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/UJ3XQ6VC)
  - 新发卡网 [WogHub ](https://fk.woghub.com/)
  - plus--0.02

- [mdkj  - /Sub2API ](https://mdkj.lol/dashboard), 已充值, 廉价但很不稳定
  - plus--0.025
  - 注意倍率调整 

- [Xybbz /Sub2API](https://sub2api.xybbz.xyz/dashboard)
  - plus--0.045, 算是低价，有点中等价格

- [钧澈API /NewAPI ](https://vip.lcodex.cn/pricing), 已充值, 深夜低价
  - plus--0.03
  - team--0.01
  - plus/pro号池多, 0.04-0.07

- [NikoAPI /NewAPI](https://nikoapi.xyz/pricing), 已充值
  - 充值地址 https://nikoapi.xyz/shop
  - 加群可领取1刀体验

- [莫比乌斯 2Chat /Sub2API](https://2chat.cc/keys)
  - 低倍率渠道， 夜晚可用性低

- [Code-Plan  /NewAPI](https://code-plan.site/pricing), 已充值
  - [GPT-源头供货-招代理的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/IY16OXB7)
  - AMD 顶级服务器 + 10Gbps 带宽

- [DataCodex ](https://api.datacodex.net/keys), 已充值

- [数智AI ](https://api.xpluse.plus/pricing)
- [AI来了 ](https://api.ailaile.site/)
  - [littleKK的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/BVGUTB12)
  - 注册需要花1元买邀请码
  - 日卡 10元--$100
- [小蓝AI ](https://www.inroi.shop/)
  - 禁止大陆ip
  - 日卡倍率 4x-6x
- [HCAI ](https://ai.hctopup.com/)
  - 日卡，仅限周末
  - 倍率0.25

- [土豆 /Sub2API](https://zz.211b.site/keys)
  - 注意倍率变动

- [YCY API /NewAPI](https://ycyapi.cn/pricing) , 长期运营, 较贵
  - [YCYAPI的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/ycyapi)

- 🗑️ [naonao - /Sub2API ](https://gpt.qinnaonao.com/dashboard), 已充值, 已跑路
  - codex分组--0.03
  - 不可用

- [松松 AI ](https://ai.songsongcard.shop/keys), 已充值
  - [松松 AI ](https://songsongcard.shop/)
  - plus--0.02

- [suncode API ](https://ai.suncode.space/keys), 已充值
  - [Sun-ai的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/SunAPi)
  - 交流群 469032841
  - plus/pro

- [梦幻API /sub2api](https://api.mhapi.cn/keys) 
  - [顶级 AI 铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/5O4RQJM1)

- 🗑️ [yypyyj- Sub2API ](https://sub2api.yypyyj.com/keys), 已充值, 高价, 缓存低
  - [max9527的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/2KFETVZG)
  - ip限制严格，不支持jms/ikuuu
- 🗑️ [白山中转站 ](https://baishanai.club/dashboard), 已跑路
  - 注意倍率
- 🗑️ [青熵 ](https://api.qs89hub.com/keys), 中转已关
  - [青熵的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/P9HPIPWA)
  - 渠道多
  - plus--0.02

- [180txt.cn ](https://ccb.180txt.cn/dashboard)
  - [中转站的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/L466CII9/5szz1p)
  - qq群 1102515021 , 仅3人 
  - plus--0.03
- [132q /new-api](https://132q.dpdns.org/pricing)
  - [中转站的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/L466CII9/6s6fmo)
  - 人少
  - plus-0.035

- [777358 /New API ](https://newapi.777358.xyz/)
  - plus-0.04

- [ApexCode API ](https://codeapx.com/models/pricing), 已充值
  - 注意套餐价格变化, 还提供了包月 ¥188--$55/day
  - 特价分组gpt--0.03
  - 常规分组gpt--0.18

- [Qmy2AI /sub2api](https://sub2api.qmytai.com/dashboard)
  - 个人0.04x，中转站0.03x

- [Global Model API Transfer Station ](https://api.mosshubs.com/pricing)
  - cc低价

- [C-API. CC /sub2api](https://c-api.cc/dashboard)
  - plus--0.05

- [豆子Ai /sub2api ](https://top.douziai.xyz/dashboard)
  - plus--0.05
  - kiro--0.5

- [Codex不限量 /sub2api](https://codex.0u0o.com/dashboard)
  - plus-0.06

- [xem API ](https://ai.xem8k5.top/pricing)
  - plus--0.2
  - claude--0.3
  - 赞助和额度充值入口：https://afdian.com/a/cong0707

- [AI-Relay ](https://www.ai-relay.org/dashboard)
  - plus--0.1
  - claude--0.7

- [cp中转站 /Sub2API](https://huozz.cn/dashboard)
  - kiro--0.2
  - plus--0.1

- [稳问AI /Sub2API](https://api.wenwenai.org)
  - 0.01是1块钱100刀
  - 并发才给5, 不然给人刷吗
  - gpt, kiro

- [PackyAPI](https://www.packyapi.com/pricing)
  - [Packy - 模型健康面板](https://check.linux.do/group/Packy)
  - [PackyAPI 使用文档](https://docs.packyapi.com/)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/4)
    - 价格经常变动
    - 消费500才给开发票
    - aws-q 渠道 0.15 的倍率应该是全 L 站最低的了
    - 国内的这种中转站都不用梯子
  - [packycode 全新服务指南 _202511](https://linux.do/t/topic/1133615)
  - [packycode：全部服务指南，包含 claude code codex 公益、付费全部站点 _202509](https://linux.do/t/topic/933715)
  - [话题 - 活动 - Zeus - LINUX DO](https://linux.do/u/zeus/activity/topics)
  - cc官方 1.5x
  - cc逆向 0.3x, 提供opus, 美元计算, in-$1.5-6, out-$7.5-30
    - 支持stripe/支付宝支付
    - 最低50元起充, 支付页面输入优惠码 "cc-switch" 可以再减10%
    - 好友充值可返利10%
  - codex - [PackyCode](https://codex.packycode.com/pricing)
    - ¥6.3/mon: 30-d, 90-week
    - ¥10.9/mon: 60-d, 180-week
    - ¥12.9/mon: 120-d, 360-week

- [Right Code - 企业级 AI Agent 中转平台](https://www.right.codes/models)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/49)
    - 这codex缓存怎么做的这么厉害的，和官方一模一样
    - 稳定好用，群里每周四还有抽奖
  - [【Right. Codes】佬友福利！每人共450$ Codex  ](https://linux.do/t/topic/1145045)
  - [话题 - 活动 - Lyndonw - LINUX DO](https://linux.do/u/lyndonw/activity/topics)
  - cc官方 5x
  - cc逆向-awsq 1x, 提供opus, in-￥1.00/M, out-￥5.00/M
    - Kiro逆向，200K上下文、有缓存，与官渠相差不大
    - cc-token大约是官方0.2x
    - 支持支付宝
    - 好友支付完成后，双方同时获得实付金额对应额度的 5%
  - codex套餐量大管饱
    - ¥45/mon: 30-d, 900-mon
    - ¥60/mon: 60-d, 1800-mon
    - ¥75/mon: 90-d, 2700-mon
  - L站用户注册就送小小股东, $5/mon
    - right code 也是站内的一家主要做codex的中转站
  - o2a基本没有缓存?

- 🗑️ [帕帝AI](https://padi-shop.closeai.hk/), 已倒闭
  - [FreeAI - AI API Gateway](https://free.closeai.hk/)
  - [Home - 帕帝AI _202604](https://padi.closeai.hk/home)

- [IKunCode](https://api.ikuncode.cc/pricing)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/15)
    - 太喜欢有求必应的客服了，回复速度快，解决问题快，稳定性也很不错
  - [【IKunCode】全民编码人们大家好，我们是练习时长两周半的cc中转站 ](https://linux.do/t/topic/965944)
  - [话题 - 活动 - zyoung - LINUX DO](https://linux.do/u/zyoung/activity/topics)
  - cc官方 1.5x
  - cc逆向 0.4/0.8, 提供opus, in-¥2-4/M, out-¥10-20/M
    - 200K上下文 + 5min缓存，支持非CC客户端
    - 支持 支付宝/微信

- [CUBENCE - Claude Code & Codex Gateway](https://cubence.com/dashboard/model-plaza)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/17)
    - 目前用过最稳的，别家一天一崩，这家一周一崩
  - [【Cubence】SHAREYOUR正式改名Cubence ](https://linux.do/t/topic/1069292)
  - [话题 - 活动 - Fetters - LINUX DO](https://linux.do/u/fetters/activity/topics)
  - cc官方 1.5x
  - cc逆向 0.3x, 提供opus, in-¥1.5/m, out-¥7.5
    - 支持缓存

- [DuckCoding](https://duckcoding.com/)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/12)
    - 最贵的一家
    - 太贵了，消耗token太快了，即使买官方的包月也没有这么夸张啊
    - L站最贵的倍率了
  - [【富可敌国】InstCopilot API 更名 DuckCoding ](https://linux.do/t/topic/937521)
  - [话题 - 活动 - WCyrus - LINUX DO](https://linux.do/u/wcyrus/activity/topics)
  - cc官方 1.5x , 提供opus, in-¥5-15/M, out-¥25-75

- [米醋API](https://www.openclaudecode.cn/)
  - 提供opus, in-￥1.00/M, out-￥5.00/M
  - [openclaudecode好像是也被卖了，但还是好评 _202601](https://linux.do/t/topic/1520754)
    - 比较负责的，人家全退款了。 花了 2 个月的时间，办理完所有退款，才交割出售。 这点非常好评。

- [AICodeMirror官方共享平台](https://www.aicodemirror.com/dashboard/pricing)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/59)
    - 这家中奖必须给五星好评？那我直接给你0.5星
  - cc官方 0.4x
  - cc逆向 0.2x, 提供opus, in-¥1.4/M, out-¥7/M
    - 缓存创建也要付费

- [foxcode](https://foxcode.rjj.cc/)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/6)
    - aws渠道有点蠢，其余渠道经常卡。。。体验差
  - [【FoxCode稳定超耐用】一款为你量身定制的ClaudeCode镜像+API双合一 O](https://linux.do/t/topic/859649)
  - 消耗量惊人，店铺写的次数严重虚标
  - 暗改了计费的 一个问题能跑10$
  - 开发票要收5%的开票费，88code和鸭子都不用
  - [FoxCode 中转站 Claude 2API 上下文压缩时6倍天价计费 ](https://linux.do/t/topic/1373802)
  - [FoxCode发卡](https://fk.hshwk.org/)
    - ¥35/0.1b, ¥135/0.5b, ¥468/2b
  - [扛过这波了，FoxCode 稳定不涨价通知 + 优惠券发放 + 新增超高质量cc-Super渠道 _202601](https://linux.do/t/topic/1505358)
  - [【富可敌国】小于1毛钱/$的claude-opus-4-6已全面适配, 上线gpt-5.3-codex _202602](https://linux.do/t/topic/1571488)
  - [一文搞清楚foxcode的计费 ](https://linux.do/t/topic/1486166)
    - 在这里以我的实际上付费为例，我充了 135 人民币，在账号上有 500 刀的可用余额。在实际上进行调用后可以发现，这三个渠道有以下的比率。aws 是原价的 0.25 倍，ultra 是 2 倍，max 是 18 倍。
  - 🐛 [foxcode 和 tiger 用一台服务器? _202601](https://linux.do/t/topic/1468155)
    - IP 和 证书都一样，买 MAX 还送服务器啊，还是主站服务器啊
  - [foxcode+opencode计费是否出问题了？ ](https://linux.do/t/topic/1473221)
    - 买东西不能光盯着几分钱的价格，没缓存 / 缓存不生效，相同的场景会贵很多的，命中缓存只有 1/10 价格
  - [Foxcode最近的utral和super是啥渠道？ ](https://linux.do/t/topic/1506436)
    - utral 是反重力
    - 只有几种渠道 1、官转 2、aws 3、kiro/cursor/antigravity

- [Tiger API](https://tiger.bookapi.cc/pricing)
  - opus, in-¥1/M, out-¥5/M
  - [【低倍率&耐用王Tiger】春节炸场福利！Claude 4.6 Opus ，Codex 5.3首发 ](https://linux.do/t/topic/1572928)
    - 充值 6000 以上的佬友请私信群主转账并可开具发票
    - 纯血 CC Max，假一赔十

- [Jiekou AI](https://jiekou.ai/resource-pack)
  - ¥15/20M/mon, ¥75/0.1b/mon, ¥225/0.3b/mon

- [YesCode](https://co.yes.vg/)
  - [LinuxDo商家评价平台](https://rate.linux.do/merchant/13)
  - [YesCode, Claude Code中转站测试完毕已正式上线 ](https://linux.do/t/topic/801547)
  - 按月付费, 美元计费, $10-20-45-66

- 88code [LinuxDo商家评价平台](https://rate.linux.do/merchant/5)
  - 最近不要再买了，建议观望，极其不稳定，经常没法用

- [DMXAPI官网：中国多模态大模型API聚合平台](https://www.dmxapi.cn/)
  - 提供免费小模型: glm-flash, qwen3-8b
  - 很多国内模型
  - 提供opus， in-¥12/M, out-¥62/M

- [Ai Go Code - AI编程助手 | 接入Claude等先进AI模型](https://www.aigocode.com/)
  - ¥400/4weeks

- [整数云 model router](https://model.zhengshuyun.net/pricing)
  - 月卡49
  - 套餐倍率0.17(计算后就是right.code的价格)，按量倍率0.3

- [BeeCode AI](https://beecode.cc/dashboard)
  - [pay](https://pay.beecode.cc/)

- [GAPI ](https://api.easyabcard.ltd/dashboard)

- [兔小店](https://store.tu-zi.com/)
  - 特别贵, 199+
  - 充值基本是官方价格

- [UUcode - API 中转管理平台](https://www.uucode.org/)
  - [【致敬开源】与其打硬广，不如给佬友们的代码“供电”，寻找L站开源作者，UUcode送商业级API额度 ](https://linux.do/t/topic/1370667)

- [AI Ping](https://aiping.cn/modelList)

- [New API  /newapi](https://cc-api.chat/pricing)

- [Duo API - /newapi](https://api.duou.ai/)

- [subgo /sub2api](https://code.subgo.qzz.io/)

## sms/code

- [superman的小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/superman)
  - codex接码 一个号码可以接三次，小概率号码无效，不一定能接到，无质保，如果连续三个有问题，找我退款问题账号

- [La shop的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/aisell)
  - 加拿大接码

- [Rick的AI小铺 的小店 - 云猫寄售 ](https://catfk.com/shop/rick)
  - 美国paypal接码 有效期15-30天
  - 普遍接码10次以上，部分20-30次
  - [某的号铺的小店 - 云猫寄售 ](https://catfk.com/shop/mou)
    - 各国接码

- [AI源头-oak的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/oak)
  - tg频道：https://t.me/dabaizu QQ群：996266572

- [SMS-AIShop的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/66666SMS)
  - 包售后，接不到不收费。稳定售后
  - 3块接3次
  - [gpt的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/IMNUA240)
- [天天开心的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/ED9POSCY)
- [舒心的小铺的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/AIZ3PXUW)
  - ¥1.5

- [API聚合转发源头的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/QN3MH16E)
  - Openai接码 经过测试最大3次
  - 发货信息: 手机号----接码链接
  - 里面可能会存在部分号有问题，介意勿买

- [我要掀桌子的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/T1UUZFW4)
  - gpt美区接码(速度超快-一号一次)

- [ccc的小店 - 670K发卡网 ](https://shop.670k.com/shop/PIVBQN6T)
  - 一码一接，不懂别来，小白请勿下单，只有接不到码售后

- [ZhuSMS — 接码平台 ](https://zhusms.com/)
  - https://caowo.store/
- [商家9272的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/cooree)
  - 此商品为单次Codex接码额度卡 适用于Free/Plus/Pro接码
  - 兑换地址:https://zhusms.com
  - 超时无售后，接码失败直接点击换号

- [Smz - 数字商品自动发卡平台 ](https://shop.smz6.com/)
  - pp-¥1.6

## email

- [T佬的gmail批发渠道 ](https://ai666.dnxb.cc/)
  - 全tg最便宜gmail邮箱批发
  - Gemini专区：美区/随机2022--2024谷歌邮箱/指定地区gmail邮箱

- [91的小店 ](https://gmail91.shop/)
  - gmail-5/6: 美区, 混合地区

- [AI账号乐园的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/SB9T68JP)
  - gmail-3.5/5: 美区, 随机

- [极速的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/jishu)
  - Gmail母号 邮箱，正规账号，单账号独立注册。 可用opus4.6  4.7

## accounts

- [海外社媒批发的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/GVF3KJWI)
  - fb
  - ins

- [豀南小店的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/N33RKBWR)
  - tg
  - appleid
  - twitter/x

- [阿北AI会员的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/abei)
  - ai
  - twitter

## ip

- [静态IP的小店 - 链动小铺 ](https://pay.ldxp.cn/shop/HLT0XHF9)
  - 共享ip 或 单人
# vpn/networking
- [风萧萧公益机场](https://chanel.weyolo.com)
  - [萧草 · 臻选](https://shop.sxxe.net/)

- [SecOne](https://secone.telecom.moe/#/dashboard)
  - [[SecOne公益机场] 开放注册 - LINUX DO _202604](https://linux.do/t/topic/2004418)
  - 300GB/月 - 100LDC
# video/movie
- [OmniBox - 在线观影](https://omnibox.wangchao.uno/)
  - [MoonTVPlus](https://moontv.wangchao.uno/)
  - [MoonTVPlus](https://moontv.662778.xyz/)
  - [𝔔𝔦𝔫𝔤 𝔖𝔥𝔢𝔫𝔤 -公益MoonTVPlus - LINUX DO _202605](https://linux.do/t/topic/2126755)
  - [𝓙𝓲𝓪1 𝓣𝓿 ](https://moontv.jia1.de/)
  - [【影视库】自建MoonTV PLUS - LINUX DO _202606](https://linux.do/t/topic/2415308)
    - https://tv.094264.xyz
# devops
- [Hello Code ](https://code.hellofriend.eu.cc/explore)
  - [【HelloCode】加入内测，与我们一起共建代码平台。 - LINUX DO _202606](https://linux.do/t/topic/2317331)

- [CHY公益域名 _202606](https://ym.chybenzun.top/)
  - [【CHY公益域名】开站 - LINUX DO _202606](https://linux.do/t/topic/2437664)
  - 开发自 https://git.houlang.cloud/houlangcloud/hl6
  - 可注册xxx.chybenzun.top和xxx.enener.com域名
  - chy本尊.top域名因为备过案了就先不开放注册了
  - enener.com域名明年三月过期，过期后不会续，佬友们需要注意下

- [Canopy Wave](https://cloud.canopywave.io/)
  - 提供模型API
  - 也提供部署环境
# saas
- [Huggingface和Cloudflare羊毛自建代理的方法 ](https://linux.do/t/topic/1411544)
  - 利用cf大善人的网络代理加速，利用hug大善人的免费域名和证书，达到我们的目的
  - huggingface.co免费的容器： Free版本就是2vCPU和16GB RAM，就已经非常强了
    - 新建一个Space，然后点 Embed this Space
    - huggingface 跑了个前置的Nginx或Caddy或traefik代理，自动申请了证书，代理后端容器的7860端口，为什么是7860端口呢？
    - 因为最常见的用途是托管基于 Gradio 构建的机器学习模型演示。Gradio 是一个非常流行的 Python 库，用于快速创建交互式 Web 界面来展示 ML 模型。它的默认启动端口就是7860。
  - 接着我们去薅大善人cloudflare，首先弄好一个域名并托管到CF上面
    - 点开左边的菜单：Build –> Compute & AI –> Workers & Pages > create app
    - 返回这个worker的空间，点击Settings，下面的Domains & Routes ，右边点击 +Add

- [gdgame - 免费单机游戏下载 | 游戏库 - 免登录直接下载单机游戏](https://gdgame.org/)
  - [公益免费单机游戏站 ](https://linux.do/t/topic/1561998)
  - 免登录享受 4000 款单机游戏
  - 支持国内全主流网盘：百度，夸克，迅雷，123，天翼。天翼盘是可以做到免费不限速，真正不花一分钱。
