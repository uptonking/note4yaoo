---
title: lib-aikit-ollama-community-gateway-router
tags: [gateway, large-language-model, litellm, new-api]
created: 2026-01-21T04:21:57.290Z
modified: 2026-01-21T04:22:29.956Z
---

# lib-aikit-ollama-community-gateway-router

# guide

# draft
- 渠道列表
  - 优先按优先级排序，其次按权重排序

- 支持调整用户分组的展示顺序

- 刷新页面会使系统崩溃429，待排查是前端问题还是后端问题
  - 复现步骤: 快速连续多次刷新任意页面如 http://localhost:4090 

- admin配置模型名映射后, 使用token的用户的日志名应该显示别名，而不是原始名称

- ai-provier-issues
  - mistral api转换为 claude api 时, 出现异常 Expected last role User or Tool (or Assistant with prefix True) for serving but got assistant
  - 字节火山: [Transformer maxtoken field ineffective for Volcengine API with DeepSeek-v3 model ](https://github.com/musistudio/claude-code-router/issues/213)
    - The maxtoken transformer field in the configuration does not work properly when using the Volcengine API with the DeepSeek-v3 model, resulting in API call failures. However, the same configuration works correctly with the DeepSeek-R1 model.
    - 👀 仅deepseek-v3.2存在此问题, glm-4.7正常
# donehub/one-api
- codex-cli的渠道接入很简单, 类型选custom， 添加模型名即可, 不需要开启 v1/responses 

- there is no configuration option to enforce max context length
  - While there is a `ContextLength` field in the ModelInfo struct (model/model_info.go:12), it is only used for informational/display purposes in the web UI - it does not enforce any validation.

- 
- 
- 
- 
- 

# new-api

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 建议 AI 大厂的模型接口加个签名字段吧，输出的内容可以快速验证来自官方。这个不仅是防中转站作弊，还可以有更多用途。
- https://x.com/jolestar/status/2029949873869705608
  - 再进一步，让用户也生成 keypair，给 prompt 带个签名，这样 api key 也可以干掉了，还更安全。
- 效率问题。apikey的效率比非对称签名验证要高非常多。不管哪种，走中转，实际上中转就已经能够解开了。
- 让 AI 大厂新增 GPU 服务器处理非对称密钥的解码， 估计人家不太愿意哦

- 即便如此也挡不住官方降智

- 只要是前端，基本上都可以逆向出来，只是难与不难而已

- https://x.com/geniusvczh/status/2030083754509959545
  - 不太行，因为AI说话是streaming，现在的签名算法不可能做到一边stream一边签，因为这是一种安全上的缺陷
- 最后加个 chunk 带上签名也也行呀

- streaming 输出是按 chunks 来，每个 chunk 签个名似乎也可以。

- chacha20不就行了。能解密出来的一定是用密钥签出来的
  - prefix不变第二天就被攻破了
- 有ecdh算法保证

- 可以签，   rsa 非对称加密 典型问题。但是都是中间站了， 那中间人攻击 ，官方说你咋不直接买我订阅 或者 买token

- 可以在模型生成token的那个层做标记，有对应的论文
# discuss-donehub/one-api-news
- ## 

- ## 

- ## 

- ## 
# discuss-donehub/one-api-roadmap
- ## 

- ## 

- ## 

- ## 
# discuss-donehub/one-api-issues
- ## 

- ## 

- ## 

- ## 

- ## [请求增加文心一言的联网参数web_search透传 · Issue · MartialBE/one-hub _202504](https://github.com/MartialBE/one-hub/issues/671)
  - 文心一言的联网功能都没有效果，在lobechat上面打开联网功能无效，在客户端直接使用文心一言的key有效

- [请问智谱怎么开启联网？ · Issue · MartialBE/one-hub _202401](https://github.com/MartialBE/one-hub/issues/82)
- 现在可以直接在渠道中配置插件信息了， 目前支持智谱 和 qwen的插件配置
  - 不过 智谱的API设置web_search好像有点问题，开启和关闭没区别，并没有进行联网。 它的知识库 是可以使用的。

- [接口更新 · Issue  · MartialBE/one-hub _202408](https://github.com/MartialBE/one-hub/issues/321)
  - 希望添加是否开启web_search联网，质谱的glm-4-alltools模型目前无法调用工具
- 这个鬼模型这么贵的吗，调试几下，我20大洋没了， 对接不起

- ## [codex app接入 glm-4.7 · Issue · deanxv/done-hub](https://github.com/deanxv/done-hub/issues/43)
  - 提示这个：stream disconnected before completion: failed to parse ResponseCompleted: missing field id

- ## [[Feature Request] Response API · Issue · MartialBE/one-hub _202511](https://github.com/MartialBE/one-hub/issues/868)
  - 提供对外的 Response API 接口。现在只能将上游的转为 ChatCompletions 接口。
- 现在 Codex 中使用，报错如下： stream disconnected before completion: failed to parse ResponseCompleted: missing field `cached_tokens` 

- 最新版渠道设置最下面有相关设置

- ## [有些渠道报错不会切换到低优先级渠道，比如429、504 · Issue · MartialBE/one-hub _202411](https://github.com/MartialBE/one-hub/issues/410)
  - 有时候高优先级的渠道返回错误，比如429、504等，会直接返回错误而不会切换到低优先级渠道

- 429 错误是可以重试的， one hub的重试机制是，将高优先级渠道 全部重试完毕，没有可用的情况下，才会流向低优先级，
  - 比如你重试设置3， 2优先级有4个渠道 1优先级有1个渠道， 那么除非 2优先级全部失败或者被冻结，不然永远不会重试到1优先级。
- 400错误，除了渠道类型是Claude以外都不会重试， 因为 400错误一般都是用户请求参数有问题，没有重试的必要。 而Claude重试，是因为 Claude 余额不足返回的也是 400错误，所以需要重试。

- ## [功能：需要支持内容审计，将外发及AI响应的内容记录下来 · Issue · songquanpeng/one-api _202405](https://github.com/songquanpeng/one-api/issues/1440)
- debug模式有日志，可以发es分析。不过debug会影响性能
  - 环境变量DEBUG=true开启，DEBUG=false关闭

- 我感觉内容审计放在应用端做比较好，让one-api更加纯粹一点

- 这个有隐私问题，建议放到网关层

- 自写渠道，加上百度文本审核
  - 我可能是需要的，我自己写了渠道，支持了语音生成，bert-vits2等，或者其他get post都可以兼容，但是这语音生成有好有坏，怕被拿去干坏事，了解一下5s的音频gpt-sovits就可以克隆音色了
  - 因为我要接入自己的tts api（vits-simple-api），然后看了one api的项目代码，发现有基本的支持，我寻思着得知道发过来的请求是啥，才能针对的截取要的进行返回
  - 就是我通过oneapi的tts调用路径，调用到我的渠道，然后那个渠道再调用一次token计费渠道，再返回音频，上面的截图是token计费渠道的代码
# discuss-donehub/one-api-internals
- ## 

- ## 

- ## 

- ## 

- ##  `$.parameter.cbm.max_tokens` value must be less or equal than 16384

- option 1: `{"remove_params": ["max_tokens"]}`
  - This deletes the `max_tokens` parameter from the request body before sending it to your custom OpenAI-compatible API.
  - If the provider API has a default `max_tokens` value when not specified, this would use that default instead of whatever Claude Code sends.
  - Some APIs might reject requests without max_tokens specified

- option 2: `{"overwrite": true, "max_tokens": 16384}`

- `max_tokens` is the maximum number of output tokens (completion tokens), NOT the total context length.

- [AI_APICallError: `max_tokens` must be less than or equal to `16384` · Issue · anomalyco/opencode](https://github.com/anomalyco/opencode/issues/1000)
  - It looks like groq currently only supports a max of 16384 output tokens. I can't seem to go higher in their playground. 
# discuss-new-api-issues
- ## 

- ## 

- ## 

- ## 
# discuss-new-api
- ## 

- ## 

- ## 

- ## 
# discuss-model-api-gateway/router/proxy
- ## 

- ## 

- ## 

- ## [中转管理系统！！中转商价格对比器 ](https://linux.do/t/topic/1673364)
  - 写了这个对比工具，并且可以链接自己的实例（new api）进行数据更新过去，管理自己的中转

- ## 🤔 [关于中转站的选择，除了富可敌国之外，还有别的选择 ](https://linux.do/t/topic/1616153)
  - 在见识充分价格竞争的市场后，我不得不怀疑 l 站的部分富可敌国商家仗着利益联盟，把持着最大流量渠道，在站内搞价格垄断，一起涨价了。
  - 后面去了闲鱼看，好家伙，各种琳琅满目的套餐，性价比不说吊打站内富可敌国，至少也是性价比非常高了。为了避免打广告，我就不说是什么套餐，具体价格多少，是哪家店了。也请各位佬不要私信我，我不会答复是哪家店的。
  - 事实上，你只需要在闲鱼简单搜索 “claude code” “codex” 这几个关键词，你就绝对能找到性价比极高的套餐，这充分证明闲鱼的中转站生意，是一个充分自由竞争的市场。对了，补充一句，购买之前一定要向老板要一个免费的试用卡，如果不愿意给你试用卡的就 pass 掉这家。如果实在要买，务必先买天卡或者最低额度的。另外，我觉得闲鱼还有一个最大优势就是平台担保 + 收货打款时长。退一万步来说，就算商家真的要跑路，他也是一个星期或者两个星期之后才能跑路，请务必不要立即点击确认收货，催你发货的你务必申请退款或者部分退款，这种百分百骗子。
  - 兼听则明，希望大家多多货比三家，不要拘泥于信息茧房当中。底下如果有人说买了个什么的套餐很划算，一律视为引流打广告的，不要信，各位也不要私信我。

- 差不多，商业模式没有任何秘密，就跟技术没有秘密一样，cc退款流, codex试用白嫖流不就是目前大部分中转的盈利模式么, 这种模式只是踩在了风口上，过了风口，体验都得大打折扣，用户充值了就是真正赚钱。
  - 一旦形势危急了，掺点假，反正用户余额减少就是赚到，即使发生退款，少数可以接受（还能顺便树立点口碑），大量挤兑就可以找各种理由淡化，毕竟在商家眼里真正欠用户钱的是Claude和gpt，不关他事，不服可以报警，不过不一定有用

- 确实，淘宝有一家纯血 claude，我看就 0.75 倍率，我测了几天都是纯血。原来离开 l 站，外面一片海阔天空
  - 有没有可能你看分组倍率而没有看实际的模型定价，我是遇到过很多家分组倍率低，但是他把模型原本计费价格定高了。拿 opus 为例，1 倍率的情况下是模型计费是 5 和 25，那么 0.75 的倍率下，模型倍率应该就是 5 *0.75=3.75 和 25* 0.75=18.75，但是咸鱼或者淘宝有些是倍率 0.7 或者 0.8 的情况下，模型定价超过了 5 和 25。

- 刚才去闲鱼逛了逛，排名靠前的几个便宜的吓人，如果他们说的一刀和站内的一刀是一样的计量的话，那大概也就是 0.1-0.15 一刀的水平，写着纯血 max 但是我打开评价就看到了有人说是反重力 + kiro，就算如此那也比站内的 kiro 便宜许多…

- 我的心态也给你一样的，直到这几天反重力反代被封杀之后，才去闲鱼扫货看看，一看吓一跳，一堆价格是 l 站二分之一的套餐，有月卡有次数卡啥的，各种套餐都任你选。

- 那我岂不是可以在闲鱼买过来倒卖？不用怎么折腾

- 本质就是要多次少冲，几十几十的冲就能避免损失大的

- 佬友的监督一文不值，我 88 还没退款呢，三周了。都一样，毫无约束力的情况下或者官方 max，或者找便宜的

- 富可敌国最大的优势其实是爆雷了有佬友能帮你说两句话……

- 你把咸鱼坑踩个遍跟你把富可敌国踩个遍，有什么本质区别吗？

- 区别就是闲鱼的坑我不知道, 富可敌国的坑我知道啊
  - 闲鱼谁来帮你排除？谁帮你测？

- 好多佬友动不动几千上百的往中转站里充，在论坛上还能拉个维权群什么的，在闲鱼索赔都不好索赔。
- 至少就上次 p 站爆雷的情况来看，如果人真想跑，维权群的意义好像也有点尴尬, 不过说到底还是看人。就像淘宝有好商家，l 站也有出生一样，反正这几个月这么多事综合来看我现在对富可敌国的印象就只剩下骗子和二道贩子了

- 闲鱼和淘宝可以退款，有平台这一层资金不会立即到账。 而 L 站内的你买了还会被泄露 IP + 开盒，或者是被老赖和 13 岁的小赖合伙跑路，反过来还得说你网暴人家。

- 闲鱼，是很便宜, 但是渠道掺水的概率也大得多
- 咸鱼买的自己测不来, 站内的佬友们会帮忙测测
- 闲鱼也是鱼龙混杂啊，自己一家一家试真没那精力。

- 我倒是跟佬友不一样，我是从咸鱼转到 l 站的。闲鱼上的试了蛮多家都是积分制，而且网站很简陋，给人一种说不出的感觉。
  - 后来在站里才发现中转站原来有这么多花活。一开始也确实是奔着社区氛围好 → 相信站里的中转站。刚开始还是用的很舒服的。后面随着 a 社那边收紧，也是闹出来很多花活。也是很心累。
- 我是从淘宝买，后来又来 L 站的，我的最大感受说淘宝和闲鱼大部分商家收费极其不透明，不是积分制就是乱七八糟看不懂的算法，前前后后体验过很多家站，L 站里富可敌国商家相对来说是最靠谱的，尽管有一些抽象行为，但起码有监督和及时曝光，淘宝闲鱼很多店都是新开的，说跑就跑，完全不敢下单

- 我在淘宝图优惠力度冲了个季卡，第二个月就出问题了，然后过了一个月了也不能退款，亏麻了。

- 就中转站而言, 我觉得至少在专业论坛, 基础的技术能力还是有的, 闲鱼 淘宝 小红书的那些, 嗯 我宁可国内模型都不想去买
  - 不过月抛类的号可以去闲鱼

- 急需一个支持完整 gemini 原生借口所有功能的中转站 有知道的佬友踢一下我
  - 薄荷

- ## 🔧 [机场公益站有没有现成的轮子 ](https://linux.do/t/topic/1592629)
- 多是golang实现

- ## [claude code anyrouter和88code能不能混着用 _202602](https://linux.do/t/topic/1568829)
- cc switch 这类工具就是应你这种需求来的，有个开关可以统一 api 入口，后端 api 服务自动负载。
  - 不过工具都有一定的学习成本，有问题得去了解工具，看工具的日志

- 可以一起用，不过如果两边切换的话，会重建缓存

- ## [多个公益站切换使用 _202601](https://linux.do/t/topic/1541285)
  - 看到新的公益站都会注册一个 ，这样就涉及到管理的问题了。
  - 用到的客户端可能有 Kilo Code, Claude Code, codex, Cherry Studio。这么多客户端我就得每个都添加一遍配置，而且存在某个公益站有时不可用的问题。
  - 为了偷懒不必配置那么多，是时候要上 API proxy 了，只要在 API proxy 上配一遍所有公益站，其他软件配置一次 proxy，后续就不需要动其他软件的配置了。
  - 搜索一遍，主要看到有两个开源项目，第一是公益站基本都在用的 New-API，第二是 github 上 3w star 的 LiteLLM。
  - new-api 分为渠道和模型配置，一开始类型不太清楚应该配置什么，两个概念也不太好理解。不过 new-api 可以方便的禁用某些渠道。
  - LiteLLM 配置模型只有一个概念，就是模型，这样容易理解一些。但是管理上就不太方便了，特别是都是 gpt-5.2，我都不知道是哪个渠道的，好像也没办法备注。LiteLLM 也没有禁用模型，只有删除，很不方便。
  - 另外 new-api 有个特色，可以针对某些渠道配置 socks 代理访问。
  - 各位佬们还有其他好的方案吗？总感觉为了这个需求要部署一个 new-api 太重了。不过有 docker 的话，部署起来也不慢。

- 我就在用 new-api，满足大部分需求，最近新出一个 AxonHub，感觉更好，但用不起来。

- 部署在 hugginface，不需要服务器

- 聚合公益站的话，要确认一下公益站允许，记得有些站点不允许聚合的
  - 黑与白会人工复核是自用还是分发的

- ## [如果有多个公益站，应该怎么管理方便一点呢 _202601](https://linux.do/t/topic/1475126)
  - 看到好多人用cch的，还有ccw，ccr什么的，太多工具一下子没研究明白
- 看具体要的管理是什么了，有各种管理工具
  - API使用上的，API格式转换，负载均衡之类的，然后还分本地和服务器的
  - 账号管理上的，账号情况检测，余额查询之类的

- 如果是 api 聚合在一起的话，octopus 和 axonhub 都可以。

- 如果是claude code/codex使用，就用cc switch。如果是api使用，就自建newapi

- 现在直接用cliproxyapi的地址，公益站在cliproxy管理，挺多坑的

- [请问有多个公益站统一接入的方案有吗? - LINUX DO _202603](https://linux.do/t/topic/1761186)
  - 部署个New API
  - 你都用ALL API Hub了不如直接一步到位上NewAPI，再转CPA有的折腾
  - 主要是可以all api hub内的账号一键导入

- ## [使用axonhub对自己已有的公益&2api进行整合+负载均衡 _202601](https://linux.do/t/topic/1397062)
  - 之前使用的是new-api+GPT Load的方式实现多个渠道模型的整合。不过最近在用站内 @looplj  佬的axonhub，感觉用起来差不多可以替代前者两个项目加起来的办法了。
  - 添加渠道（即你的API来源）: 大部分的公益站使用的都是new-api，所以我们一般选择openai的格式即可。渠道是数字越大权重越高
  - 添加模型（对外暴露的，也就是你实际调用的）: 配置我们实际要使用的模型了，也就是我们在各种cli工具/AI对话客户端中需要使用到的模型。举个例子，假设现在薄荷佬、Fovt佬、以及我自己的openrouter都有gpt-4.1-mini这个模型。那么就可以点击批量添加，然后选择好提供商，从模型ID里面选择自己需要的模型。现在已知我有三个来源，都是同一个模型。那么我们可以进行模型的关联。点击对应模型上的:link: 符号，即可进行关联。
- 如果觉得只是自用而且只是需要一个均衡负载功能的话，可以看看这个佬的项目，API转换用的是一套的。
  - https://github.com/bestruirui/octopus /AGPL/go/ts
  - 项目里面api转换就是直接抄的axonhub, 这个佬的功能太多了，我的更偏个人，功能更简单

- ## [New API 内导入的模型渠道无法使用联网功能吗？ _202512](https://linux.do/t/topic/1250898/6)
- 支持啊，但是要用gemini的格式请求，供应商类型选择gemini，newapi里也要选择是gemini、vertex

- newapi将模型请求方式改为gemini，客户端也用gemini格式，gemini模型就可以正确使用联网工具，newapi的转换功能实属有点问题，grok已经变成工具代理了

- ## [【开源】Metapi：中转站的中转站，一个 Key 聚合 New API / One API / OneHub 等多个站点，定时自动签到，适用于个人管理公益站等  _202602](https://linux.do/t/topic/1671489)
  - https://github.com/cita-777/metapi /777Star/MIT/202603/ts
  - 能不能搞一个东西，把这些中转站全聚合起来，只给下游暴露一个 Key？
  - 当然了，也有ALL-API-Hub和New-API这样优秀的项目，Metapi和这些优秀项目的定位差距在哪里呢？
  - ALL-API-Hub为浏览器插件，而Metapi可以使用Docker一键部署运行在云服务器或自家主机上，实现完全自动化的定时签到，并且有完整的SMTP通知等功能，出现错误在手机上就可以收到通知，且支持自动路由，聚合API的功能。
  - New-API更加适合团队使用或用户管理、开中转站使用，而Metapi的定位是个人使用，不用于给他人分发使用，因此 删除了用户管理功能，只有一个管理员令牌防止资源被盗用。V1.2 起还支持项目级多 Key 管理 ，每个 Key 可独立配置过期时间、费用上限、请求上限、模型白名单等，适合多项目拆分使用。有自动签到、各中转站令牌管理等功能。
  - Metapi和上面两者适用于不同用户群体，因此Metapi也兼容从ALL-API-Hub导入备份数据，方便站点较多的佬友们快速迁移体验，大家选择适合自己情况的就好~
  - MIT License，完全自托管，所有数据存储在本地 SQLite，不会向任何第三方发送数据，大家可以放心

- 问一下有模型映射吧，比如很多个站点可能模型命名都有一些出入，能用正则之类的方式批量映射成同一个模型吗
  - 这个目前还没有做，但批量自动映射感觉可能有点困难，如果说是不同上游的同一个模型怎么处理好呢 ，因为同一个站点也有提供多个一样的但是来源不同上游的模型
- octopus 有这个批量映射可以参考下
- 因为我目前在用的一个聚合项目有这个功能，感觉挺方便的，比之前用newapi聚合一个个配置好很多。主要是可以让我自己设置一个正则，来匹配模型名称，都映射到同一个模型上，比如上面的minimax-m2.1、minimaxai/minimax-m2.1，我可以设置正则(?:^|.*/)(minimax-m2.1)$来处理不管是什么前缀，都合并到模型minimax-m2.1上。

- 主要是all-api-hub因为受限于用户的浏览器进程，你如果好几天没看浏览器应该就没法自动签到了，因为浏览器不在24小时运行，all-api-hub不能提供自动路由和聚合api还有通知之类的功能 可以简单理解为我更类似于是New-API和all-api-hub的杂交结合体。

- 有签到不？
  - 有的有的，大部分比如Wong之类的正常公益站都能签到，详细功能可以看看项目的README，有一些比较严的比如随时跑路公益站加了严格人机验证的没办法，anyrouter这种简单过盾的可以签到 
  - 有些站点不希望被自动签到，加了人机验证就签不了了，而且是比较好加的，不过目前大部分站点还是没有加的，也没有禁止自动签到的说法

- 这个和cch这个好像啊

- ## [想对公益站做一下简单的渠道管理，用new api就可以吗？ _202601](https://linux.do/t/topic/1398557)
  - 公益站真的好多哦， 确实需要做一些简单的渠道管理，以及是不是要固定ip防止乱飘？
  - 目前是想要把公益站顶前面，有自动重试和自动更换，最后放一点官方key兜底
  - 这些需求，在国内小鸡上放一个new api就可以了吗？

- newapi 可以的， 纯自用中转，几个二开大差不差

- 个人使用 在可支援docker的状态下, 可以参考new api, axonhub

- New-api 比较像独立的站点项目 如果你有渠道想要分发的话 他会是个非常好的选项

- 今天刚写了，如果考虑负载均衡和自动重试的话，axonhub会更好。

- ## 🤔 [请问大家有没有主流Ai综合平台推荐 ](https://linux.do/t/topic/1358867)
  - Gemini学生会员，但是生图只有2k，而且感觉网页版性能受限，还是得付费。
  - 目前主要在用lovart中的Nano Banana pro 4k的生图功能，每日白嫖一点点GPT5.2做提示词反推和一些设计策划分析。偶尔会需要写一些Python脚本快速批量处理文件。
  - lovart生图没问题，但是提示词反推和生成，以及对话功能很差，而且每月220元也挺贵。
  - GPT5.2目前每天白嫖用起来确实挺好用，很想开会员
  - 买过302的token，但是功能都要手搓，playground能直接用，但是不保留记录， 关掉就没了，有点难用。
  - 求助各位大佬，有没有合适的实惠的，能调用多种不同模型的平台推荐？需要有聊天对话界面，最好能包月的。万分感谢。

- 直接买openrouter的credits也不失为一种选择
  - 最全的模型个个满血保真。除了要花钱没有缺点。

- 产品设计那些前端工具都可以，lovable什么的。生图的话lovart编辑能力无敌，提示词可以让chatgpt/claude/gemini生成好复制过去，毕竟术业有专攻
- Lovart还是不适合一般对话的

- ## [[公益] BetterClaude：更流畅的 Claude 使用体验，代理Anyrouter等公益站 ](https://linux.do/t/topic/1358893)
  - 已经有很多优秀的公益站点，比如 anyrouter、薄荷等。但由于网络环境、线路等各种客观原因，国内访问的稳定性始终不太理想。
  - BetterClaude 的初衷，就是“走完公益的最后一公里”。
  - 我们做的事情很简单： 为 所有公益站提供统一代理, 针对国内与亚太地区，适配 Cloudflare 优选线路 + 亚太 CDN
  - BetterClaude 完全基于 Cloudflare Workers 构建，并部署在全球的 **Cloudflare PPO ** 进行回源策略优化，从而尽可能 降低 BetterClaude 到任意上游服务的延迟。
  - 对所有个人用户永久免费
  - 永久支持公益站点的代理
  - ⚠️ 同时，你也可以将 BetterClaude 用于部分商业站点的代理, 需要说明的是部分商业站点明确禁止转发或代理, 因违反上游站点规则导致的账号封禁，我们概不负责
  - 在技术层面，我们会： 完整、透明地转发所有请求, 包括 客户端 IP、Headers 等信息, 确保请求格式 严格符合 Claude API 的要求

- ## [Too many LLM API keys to manage!!?! : r/LLMDevs _202502](https://www.reddit.com/r/LLMDevs/comments/1irpjjk/too_many_llm_api_keys_to_manage/)
- Check openrouter.ai
  - It’s expensive but has some really nice features like providing costs in each response. (Why actual providers don’t do that mystifies me.)

- LiteLLM does require API key from the providers

- Check out stashbase.dev, it will help you manage all your API Keys as well as other secrets.

- ## 🤔 [Why You Need an LLM Request Gateway in Production : r/LLMDevs _202504](https://www.reddit.com/r/LLMDevs/comments/1jp6ot7/why_you_need_an_llm_request_gateway_in_production/)
- I only adopt abstractions when they prove genuinely useful. Among all the possible abstractions in the LLM ecosystem, a proxy server is likely one of the first you should consider when building production applications.
- This is where a proxy server comes in. It provides one unified interface that all your applications can use, typically mimicking the OpenAI chat completion endpoint since it's become something of a standard.
  - Your applications connect to this single API with one consistent API key. All requests flow through the proxy, which then routes them to the appropriate LLM provider behind the scenes. 
  - The proxy handles all the provider-specific details: authentication, retries, formatting, and other logic.
- Four Reasons You Need an LLM Proxy Server in Production
  - Using the best available models with minimal code changes
  - Building resilient applications with fallback routing
  - Optimizing costs through token optimization and semantic caching
  - Simplifying authentication and key management

- ## 🤼 [why are llm gateways becoming important : r/LLMDevs](https://www.reddit.com/r/LLMDevs/comments/1notvwd/why_are_llm_gateways_becoming_important/)
  - 网管层 vs 应用层
- the idea (from what i understand) is that prompts + agent requests are becoming as critical as normal http traffic, so they need similar infra:
  - routing / load balancing → spread traffic across providers + fallback when one breaks
  - semantic caching → cache responses by meaning, not just exact string match, to cut latency + cost
  - observability → track token usage, latency, drift, and errors with proper traces
  - guardrails / governance → prevent jailbreaks, manage budgets, set org-level access policies
  - unified api → talk to openai, anthropic, mistral, meta, hf etc. through one interface
  - protocol support → things like claude’s multi-context protocol (mcp) for more complex agent workflows
  - what are people here using for this gateway layer these days are you rolling your own or plugging into projects like litellm / bifrost / others curious what setups have worked best

- llm gateways are critical once you need reliability and observability across multiple providers. bifrost handles routing, semantic caching, and governance in one openai-compatible api. you get health-based failover, embedding-keyed cache, and org-level policies with zero-config startup. for production teams, this means consistent uptime, traceable requests, and budget control.
  - For a brief comparison with LiteLLM: Bifrost delivers 100 percent success at 500 rps; litellm drops below 90 percent. bifrost median latency is 804 ms, litellm is 38 seconds at scale. bifrost throughput is 424 rps, litellm is 44 rps. bifrost uses 120 mb memory, litellm uses 372 mb

- honestly I’m on the other side of the equation so i have adapters that enforce defensive strategies to deal with llm responses and tools and things. But you can see right in your diagram why the other half finds value to add in the gateway. It’s written in your diagram

- We looked at using a router but it was a single point of failure.
  - We are a node shop and we went with the Vercel AI SDK. Built some custom fallbacks, simple retries, and it's built in telemetry. I haven't been yearning for an LLM router since.

- ## [What’s the Fastest and Most Reliable LLM Gateway Right Now? : r/LLMDevs _202508](https://www.reddit.com/r/LLMDevs/comments/1mh962r/whats_the_fastest_and_most_reliable_llm_gateway/)
- I’ve been testing out different LLM gateways for agent infra and wanted to share some notes. Most of the hosted ones are fine for basic key management or retries, but they fall short once you care about latency, throughput, or chaining providers together cleanly.
  - Bifrost (Go, self-hosted): Surprisingly fast even under high load. Saw around 11µs overhead at 5K RPS and significantly lower memory usage compared to LiteLLM. Has native support for many providers and includes fallback, logging, Prometheus monitoring, and a visual web UI. You can integrate it without touching any SDKs, just change the base URL.
  - Portkey: Decent for user-facing apps. It focuses more on retries and usage limits. Not very flexible when you need complex workflows or full visibility. Latency becomes inconsistent after a few hundred RPS.
  - Kong and Gloo: These are general-purpose API gateways. You can bend them to work for LLM routing, but it takes a lot of setup and doesn’t feel natural. Not LLM-aware.
  - Cloudflare’s AI Gateway: Pretty good for lightweight routing if you're already using Cloudflare. But it’s a black box, not much visibility or customization.
  - Aisera’s Gateway: Geared toward enterprise support use cases. More of a vertical solution. Didn’t feel suitable for general-purpose LLM infra.
  - LiteLLM: Super easy to get started and works well at small scale. But once we pushed load, it had around 50ms overhead and high memory usage. No built-in monitoring. It became hard to manage during bursts or when chaining calls.

- i think if you're self-hosting on kubernetes, the kgateway + agentgateway combo crushes the rest of the competition, by a pretty large margin. (it's not just a LLM gateway, they're pioneers of the kubernetes gateway api, which is the agreed upon standard for kubernetes)
  - I think the only thing they lose to other AI gateway implementations at, is the variety of use cases that are currently supported. For example, a gateway like LiteLLM will have a broad range of supported endpoints (that aren't built well, but exist).

- [Best LLM gateway? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1mh9r0z/best_llm_gateway/)
- Litellm is easy to setup but difficult to scale when you are building for production. I have seen litellm fail around 250-300 RPS. It is also quite resource hungry leading to unnecessary infra complexity.
# discuss-model-api-paid
- ## 

- ## 

- ## 

- ## 

- ## [team号有了之后，怎么给龙虾使用啊，能像公益站一样提供api和token吗 - LINUX DO _202603](https://linux.do/t/topic/1719944/21)
- cliproxyapi 走auth登录

- 加入cpa反带生成apikey。但是不建议不如直接使用free账号的5.2。龙虾太吃token了free量大管饱

- ## [站内有什么好用的codex中转站？ - LINUX DO _202603](https://linux.do/t/topic/1537844)
- 跳蚤市场频道，一直有，高强度的话，搞3~4个team够了，低强度的话，感觉一个都够了。

- 直接海鲜市场呗，15一个team，轻度用不完

- 目前我用过体验比较好的就是rightcodes和xyai两家，站内都可以搜到

- ## [L站赚钱指南：如何开中转站 - LINUX DO _202603](https://linux.do/t/topic/1723638)

- ## [有没有靠谱的Codex的team商家或者geminiUtral商家  - LINUX DO _202603](https://linux.do/t/topic/1768672)

- ## [6位数充值？用过的Claude Code中转商报价分享和成本分析 - LINUX DO _202603](https://linux.do/t/topic/1753106)
  - 最近由于 Claude Code 大量使用，在我自己已经订阅了 Claude 官方会员的情况下，难以忍受5小时的限制。又大量深度使用了多个Claude Code中转商。
  - 我看重的两点就是要稳定+独立号池。
  - 所谓稳定，就是当我想用的时候随时能用。
  - 而独立号池可以确保当一个服务商倒闭的时候，其他的服务商却还都在。
  - 最怕那种表面上好几个服务商看似独立，实际上用的都是一套上游共同号池，倒了一个就全倒了。
  - 中转成本更新 (3月)：3月中旬测试发现，在支持 opus [1m] 之后，有概率$200/月的Claude Max会员可以稳定榨出 $3500 的额度。（如果不担心封号，可以继续往上触及$5200）

- “CC MAX居然能榨出$3500的额度” 这属于是信息差了。
  - 最关键的就是：claude官方会员的缓存读取是免费的。 也就是说逆向服务商收的缓存读取费是纯赚。

- ## [中转管理系统！！中转商价格对比器 - LINUX DO _202603](https://linux.do/t/topic/1673364)
- https://github.com/Goingu/New-API-Price-Sync-Tool

# discuss-model-api-free
- resources
  - https://github.com/cheahjs/free-llm-api-resources
    - free access or credits towards API-based LLM usage.

- ## 

- ## 

- ## 

- ## 

- ## [Free Model List (API Keys) : r/LLMDevs _202603](https://www.reddit.com/r/LLMDevs/comments/1s020se/free_model_list_api_keys/)
  - Here is a list with free models (API Keys) that you can use without paying. Only providers with permanent free tiers, no trial/temporal promo or credits. 
  - Rate limits are detailed per provider (RPM: Requests Per Minute, RPD: Requets Oer Day).
- Provider APIs

Google Gemini 🇺🇸 Gemini 2.5 Pro, Flash, Flash-Lite +4 more. 10 RPM, 20 RPD

Cohere 🇺🇸 Command A, Command R+, Aya Expanse 32B +9 more. 20 RPM, 1K req/mo

Mistral AI 🇪🇺 Mistral Large 3, Small 3.1, Ministral 8B +3 more. 1 req/s, 1B tok/mo

Zhipu AI 🇨🇳 GLM-4.7-Flash, GLM-4.5-Flash, GLM-4.6V-Flash. Limits undocumented

- Inference Providers

GitHub Models 🇺🇸 GPT-4o, Llama 3.3 70B, DeepSeek-R1 +more. 10–15 RPM, 50–150 RPD

NVIDIA NIM 🇺🇸 Llama 3.3 70B, Mistral Large, Qwen3 235B +more. 40 RPM

Groq 🇺🇸 Llama 3.3 70B, Llama 4 Scout, Kimi K2 +17 more. 30 RPM, 14, 400 RPD

Cerebras 🇺🇸 Llama 3.3 70B, Qwen3 235B, GPT-OSS-120B +3 more. 30 RPM, 14, 400 RPD

Cloudflare Workers AI 🇺🇸 Llama 3.3 70B, Qwen QwQ 32B +47 more. 10K neurons/day

LLM7.io 🇬🇧 DeepSeek R1, Flash-Lite, Qwen2.5 Coder +27 more. 30 RPM (120 with token)

Kluster AI 🇺🇸 DeepSeek-R1, Llama 4 Maverick, Qwen3-235B +2 more. Limits undocumented

OpenRouter 🇺🇸 DeepSeek R1, Llama 3.3 70B, GPT-OSS-120B +29 more. 20 RPM, 50 RPD

Hugging Face 🇺🇸 Llama 3.3 70B, Qwen2.5 72B, Mistral 7B +many more. $0.10/mo in free credits

- The list is on GitHub https://github.com/mnfst/awesome-free-llm-apis

- ## [Claude Code Max，Opus-4.6的所有渠道研究  _202603](https://linux.do/t/topic/1740014)
  - Claude Code + Max反代拼车方案
  - Claude Code + Max中转站方案
  - Antigravity Ultra家庭组拼车方案
  - Antigravity学生Pro方案
  - VSCode + Copilot会员方案

- ## [Mistral API quota and rate limits pools analysis for Free Tier plan (20.02.2026) : r/MistralAI](https://www.reddit.com/r/MistralAI/comments/1rc8rwf/mistral_api_quota_and_rate_limits_pools_analysis/)
  - The goal of research is to map which models share quota pools and rate limits on the Mistral Free Tier, and document the actual limits returned via response headers.
  - Important note: On the Mistral Free Tier, there is a global rate limit of 1 request per second per API key, applicable to all models regardless of per-minute quotas.
  - Quota limits are not per-model — they are shared across groups of models. All aliases consume from the same pool as their canonical model.
  - Pool 1: Standard Limits: 50, 000 tokens/min | 4, 000, 000 tokens/month
  - Pool 2: mistral-large-2411 (special) Limits: 600, 000 tokens/5-min | 60 req/min | 200, 000, 000, 000 tokens/month
  - Pool 3: mistral-medium-2508 Limits: 375, 000 tokens/min | 25 req/min | no monthly limit
  - Pool 7: devstral-2512 Limits: 1, 000, 000 tokens/min | 50 req/min | 10, 000, 000 tokens/month

- ## [minimax m2.5的风到底怎么刮起来的？ ](https://linux.do/t/topic/1671843)
  - 使用体感甚至不如 k2.5 评分难道是对基准测试问题的特殊优化（拟合）来的？
- 官方会营销, 大v带着冲, 量就上去了, 还可以, 但是也有很多不足

- 不是每个人都会买gpt的api，所以就在推国产模型，方便购买。

- 看openrouter是因为kilo里面免费可用，和之前grok code fast一样，提供免费的模型刷用量，实际能力远远比不上跑分，还是不如sonnet 4.5

- 感觉除了价格真的便宜以外都是不足

- 我估计是他们公司绩效压力太大了，已经开始纯纯刷分了，当时m2.1比起m2.0还是能感受到不少提升的。但是m2.5我试了下几乎感受不到什么提升, 我估计他们就是为了快节奏发布专门针对几个benchmark特调了下然后就放出来给大家用，结果一用就感觉失望.

- ## kilo提供 [Kimi K2.5 MiniMax M2.5免费API渠道](https://linux.do/t/topic/1683518)
  - Kilo Code扩展里扣出来的

- 但是我使用的感觉是，kilo的free模型很降智，甚至不如opencode的public。 
  - 无限free的api用得多的是英伟达，魔搭社区，grok2api的

- ## [iFlow账号被封了，高强度刷论坛，找到一个解封链接，佬友们可以提交看看 _202602](https://linux.do/t/topic/1658255)
- 我该怎么和它说我一个手机号要解封10个号？
  - 因为google账号不用绑手机，也不用绑实名
  - google登录: 你把全局翻墙打开，然后进去就有了：https://iflow.cn/ 

- ## [openrouter出免费模型路由了 _202602](https://linux.do/t/topic/1559289)
  - 稍微测了下，不是 50rpd，挺好

- ## [哪里有免费或者便宜的stt语音模型 可以接api用的 ](https://linux.do/t/topic/1211369)
- 硅基流动的 SenseVoiceSmall
  - Groq 的 Whisper-large

- 火山引擎有一个免费的，一个应用免费两个小时，嗯，挺够用的。

- ## [免费的AI服务额度 _202601](https://linux.do/t/topic/1516842)
- 日常我除了付费购买了 AI 编程，其它都使用一些免费的 AI 服务，这些服务额度有限
1、ChatGPT https://chat.openai.com
- 通用消息数：一个对话窗口大约 10–80 条 / 5 小时
- 图片：约 2～10 张 / 每天

2、Gemini https://gemini.google.com/
- 通用消息数：普通对话 约 100-500 次 / 每天，高级推理 约 5-10 次 / 每天
- 图片： 普通质量 约 100 张 / 每天 高清质量 2-3 张 / 每天
- Deep Research：5 份 / 每月
- NotebookLM：建立最多 100 本笔记本、每本最多 50 个资料来源与每日 50 次对话

3、Claude https://claude.ai/
- 通用消息数：约 20-40 条 / 5 小时

4、Perplexity https://www.perplexity.ai/
- 基础搜索：几乎无限
​- 专业搜索：3 次 / 每天
- 附加文件：3 次 / 每天

5、Grok https://grok.com/
- 通用消息数：标准查询 约 10-20 次 / 每 2 小时，高级模式 约 2-5 次 / 每 24 小时
- 图像：生成 约 10 次 / 每 2 小时，分析 约 3 次 / 每天

6、豆包 https://www.doubao.com/chat/
- 通用消息数：无次数上限
- 图像： 普通质量 无明确次数限制，高清质量 5 次 / 每天
- OCR 单次文字识别 ≤500 字 / 每天
- 手机端全量 AI 生成操作 5-60 次 / 每天

- ## [aistudio的模型 和 gemini上的能力上有什么区别？ ](https://linux.do/t/topic/1429519)
- gemini.google.com有提示词来降低推理强度。
- 我不会主观下判断这个提示词是否是官方故意降智，但客观测试结果显示，该提示词确实导致了在处理复杂问题时推理强度的下降。虽说推理强度的下降也并不是会使所有类型的回答质量下降。

- 我看到的内置提示词是增加推理强度的，请问你这个降智是哪一版的gemini？

- Gemini官网是产品, 之前被扒出来提示词故意降智, AI studio会好用一点

- 一个是卖钱的正式版，一个是对话用于训练的免费公测版。测试版不一定弱，但 Ta 是测试版。

- ## 💡 [【长期更新-授人以鱼不如授人以渔】公益站渠道公示（人人都可搭公益？） _202601](https://linux.do/t/topic/1477161)
  1. q2api(claude)
  2. 英伟达ai平台（大部分开源模型）
  3. hf抱脸（大部分开源模型）
  4. groq平台
  5. 硅基流动平台
  6. 富可敌国平台（duck已许可分发付费站anti, 正在申请分发max）
  7. 杂七杂八的短效羊毛平台（国外）

- [还有可以白嫖opus的平台嘛  ](https://linux.do/t/topic/1510785)

- ## [求免费/低成本的embedings（bge m3）渠道 ](https://linux.do/t/topic/1487194)
  - 手上有百万级别的记录需要embbeding。试用过本地部署，可惜太慢了；之前是用大善人siliconflow的，但是现在他们家即限制IP，（未实名情况下）又降rpm了，根本没法用。 
- 我也这么折腾了一圈。最后压着40rpm永英伟达
  - 多搞俩号撒

- [类似魔塔社区的免费模型网站，modelscope、openrouter 还有其他的吗？ ](https://linux.do/t/topic/1480347)
- 目前用 modelscope 模型，主要是 embeding 模型，导几篇文章就超限了，
- 以前用过 openrouter，但这个受限更严重了
- 可以自己跑一个，这个并发不高的话不怎么占用资源，可以先试试bge系列的(2.5 cpu 就能跑，也有现成的onnx格式的，java，python跑起来都很方便)，如果效果不好可以试试千问的(这个用gpu好一些)
- https://ai.gitee.com 这个估计有可能最符合你要求 大部分向量模型都是免费, 其他模型每天免费100次

- [哪里有高并发的嵌入模型？ - LINUX DO _202603](https://linux.do/t/topic/1805477)
  - 硅基流动的速率限制RPM和TPM有点不太够用，然后在论坛里找发现了魔力方舟，结果这个更黑，说是不限速率，但是运行了程序，还没轨迹流动的时间跑得长就给报错了, 关键是它提醒我要买资源包我想着用的量有点大，还是老老实实买了吧

- ## [OpenCode 反代断流问题解决方案 - 解决Antigravity\2api\反代\断流\回复一半不回\莫名奇妙中断  ](https://linux.do/t/topic/1487267)
  - 使用 OpenCode + Antigravity Tools API 反代时，经常出现以下问题：
  - 回复到一半就不回了
  - 莫名其妙中断
  - 长时间 streaming 时连接被意外关闭
  - 根本原因
  - @ai-sdk/openai-compatible 的 SSE（Server-Sent Events）处理与 Bun 的 HTTP 客户端存在兼容性问题，导致长时间 streaming 时连接被意外关闭。
  - 最终解决方案
  - 使用 @ai-sdk/anthropic 协议替代 @ai-sdk/openai-compatible
  - 之前断流是用 @ai-sdk/openai-compatible + OpenAI 格式
  - 现在不断流是用 @ai-sdk/anthropic + Anthropic 原生格式 + 模型映射

- ## [One API还是用New api 还是有更好的 _202512](https://linux.do/t/topic/1378708)
- 我有一个旧的one api，渠道管理功能没法自动获取和添加渠道的所有模型，添加了新渠道要手动填写模型。
  - 但是one api可以自定义api的key，比如自定义成使用者的拼音全拼, 而newapi必须要自动生成sk-XXXX
  - 所以公司用one api的人很多，都用自己的名字作为key，想为整个公司更换成new api都不行。一换就要全部人都通知一遍，而且我们的one api添加了好多渠道, 想不影响现网使用0影响转移到newapi根本没有头绪。
  - 所以你还是直接用newapi吧
- newapi先在后台创建key，然后去数据库改成自定义的，数据库存的key没有sk-前缀，api调用的时候也可以不加sk-前缀，之前测试过，sk认证的时候会截取第一个“-”之前的部分丢掉，只使用第一个“-”后面的部分作为key认证，不晓得现在这个逻辑改了没，自定义的时候注意一下横线的问题就可以了

- Done-hub项目更好，大佬在站里
  - 支持，我就是从new API换到done hub了，功能更多，如果是第一次个人用其实我推荐done hub。

- One 最干净简洁，但很多基本功能都已经跟不上了例如参数覆盖啥的。只是以前用的 One 不想换就一直用着。

- 
- 
- 
- 
- 

- ## [天塌了, 今日Oaifree正式宣布跑路 _202411](https://linux.do/t/topic/272321)
  - 不论是打开new.oaifree.com，shared.oaifree.com还是Cloudflare Workers反代都会跳转到there is no wall

- OAIPRO是始皇对官方API的中转，绝对保真，其他的估计都会或多或少的掺假

- ## [cliproxyapi反代出来的接入到cherrystudio还能调用bananapro 出4k图吗？ _202601](https://linux.do/t/topic/1426093)
- 可以出图的，CLIProxyAPI里面配置就不需要配置cherry studio了，图是4K的

- 自定义参数设置成这样试试imageConfig json {“aspectRatio”: “比例: 比例”, “imageSize”: “4K”}

- gemini返回不止一个，cherry只选取第一个，就是最低分辨率那个，所以你无论怎么设置都不行。你需要用Antigravity-Manager那个带后缀名的就可以直接出4k

- https://github.com/bohesocool/gemini-chat

- ## [claude-relay-service 和 new-api 哪个更适合个人用户聚合中转站？ ](https://linux.do/t/topic/1415646)
  - 个人购买了几家中转站的服务，也使用了社区的一些大佬的公益站，之前一直使用CRS做聚合，但是好像很多佬友推荐用 new-api 做聚合，有佬友做过对比么，这两者哪个更适合呢？

- 个人聚合使用比较推荐octopus，axonhub, llmio这些项目嘞
  - 这些在负载均衡，模型映射上做了更好的优化吧，并且是自用的话，不会太考虑多用户使用，所以也更轻便吧。我个人在用octopus，也是站内佬的，优点就是模型映射和负载均衡挺方便的，不同渠道的同一个模型可能名字都不太一样，但是可以批量定义同一个出口模型名称，然后你调用的时候用你自己定义的名称就行，你还可以自己设定负载均衡模式，轮询还是随机还是故障转移还是加权之类的。还有一个优点就是挺美观的，看着很舒服

- 这些可以先用CLIProxyAPI等项目将其逆向成api，然后再接到聚合项目里。实测挺好用的，我就是用CPA逆向反重力，接到octopus，然后用cc switch管理
  - 我现在也是这样干的，所以想着有没有可以跳过 cliproxyapi 这个的网关系统
- 其实CPA也能导入聚合其他渠道吧，把中转站公益站的放进去就行，不过负载均衡和模型映射不知道怎么样

- 我用的one-hub就是多渠道映射什么的不太行，很久以前搭建的，现在的工具都支持多渠道映射了好用很多

- 在用站内佬做的veloera(基于newapi二开), 因为有渠道前缀的功能挺好的用来区分不同渠道的模型, 不过可惜已经不更新了

- ## [开一个公益站前期大概要准备几个号啊？ _202601](https://linux.do/t/topic/1415483)
- 七八个肯定不够用，claude两下都蹬完了。但是Gemini3flash应该够100人吧，建议先开放100个名额试试水。站内大佬应该不少用的kiro，Geminicli加antigravity双逆向，再说还有捐赠。（即使这样，也很容易被撑爆）

- 七八个不够，七八个pro再全都拉家庭组 然后设置速率限制注册不知道够不够蹬

- ## [[公益 + 开源] BetterClaude 0.2：引入 Axisnow GTM 智能调度，亚洲链路智能调度+ 公益站直达  ](https://linux.do/t/topic/1407246)
  - 更新重点：结合 Axisnow GTM 做“智能路由再优化”
  - 这次升级的核心，是把入口域名做成全局调度 + 边缘执行的架构
  - 列出了公益站的请求成功率
  - https://betterclau.de/claude/wzw.pp.ua
  - https://betterclau.de/claude/runanytime.hxi.me

- ## [对于公益站多个渠道提供相同模型怎么聚合（newapi） ](https://linux.do/t/topic/1398050)
- 在newapi前聚合呢w

- gpt-load？不过我平常直接用 uni-api 了，自用的话抱抱脸部署的都还很稳

- https://github.com/atopos31/llmio /MIT/go/ts
  - LLM API 负载均衡网关
  - 基于 Go 的 LLM 负载均衡网关，为你的 LLM 客户端 ( claude code / codex / gemini cli / cherry studio / open webui ) 提供统一的 REST API、权重调度、日志记录与现代化管理界面，帮助你在一个服务中整合 OpenAI、Anthropic、Gemini 等不同模型能力。

- ## [NVIDIA NIM - Free DeepSeek R1(0528) and more : r/SillyTavernAI _202507](https://www.reddit.com/r/SillyTavernAI/comments/1lxivmv/nvidia_nim_free_deepseek_r10528_and_more/)
- Nvidia is much slower than the chutes

- [My experience coding with open models (Qwen3, GLM 4.6, Kimi K2) inside VS Code : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nzal91/my_experience_coding_with_open_models_qwen3_glm/)
- K2 0905 and Qwen 3 Coder 485B are entirely free, for unlimited use up 40 RPM from nvidia api. This is exactly two times more requests than GLM 4.6 MAX plan if we devide their 5 hourly quota into minutes.
  - The quota comparison is also wrong: the “40 RPM” and from what I could find with Qwen for their free CLI 2000 requests per day numbers are counting every single low‑level API call an agent makes, and a single non‑trivial agent run can easily fan out into dozens of those. GLM’s agent quota is per agent run, which can include a lot of internal sub‑calls, so you’re not even talking about the same unit of work. Like let me give you a close number of the value you get with GLM 4.6 Max, 2400 * 20-100 = 48000 - 240000 actual requests.

- [Roo Code, Cline, Opencode, Codex, Qwen CLI, Claude Code, Aider etc. : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o54lfc/roo_code_cline_opencode_codex_qwen_cli_claude/)
- Nvidia nim has free kimi k2 0905, unlimited use, 40 rpm, I highly recommend it.

- https://www.threads.com/@bsunter/post/DP6atv7EdIL _202510
  - Crazy that you can sign up for nvidia and get almost unlimited free access to their models and use them in OpenCode
  - Once you exhaust free credits (1000-3000 credits), you basically have to purchase credits. Or use models locally if you have nvidia gpu
  - droid is actually better in my use case lol. sometimes opencode just cant solve the problem but droid pass the case

- ## [“Request More” (+4, 000 credits) option on build.nvidia.com - NVIDIA NIM / Access/Accounts - NVIDIA Developer Forums _202509](https://forums.developer.nvidia.com/t/request-more-4-000-credits-option-on-build-nvidia-com/344567)
- 👷 We no longer use a credit-based system for build.nvidia.com. As you noted, this has been replaced by rate limits for trial usage. The rate limits vary for each model, and we do not publish those. However, you can see your maximum rate limit in the top right of build.nvidia.com
- what do you mean by the trial usage? When I created an account and get API keys, does that count as “trial“ or should I do something else first? And about the trial “period“, is it limited by week, month, or else? 
  - When you create the account and get the API key you are using the NIM as a trial. You don’t need to do anything else first. The trial period is not limited by a time period.
  - We use ‘trial’ to mean any use for prototyping, research, development, testing, learning, etc.
  - If you are looking to move an application from development or testing to production, you are no longer using it as a trial, so will need to get an NVIDIA AI Enterprise license in this case.

- [Cannot find the amount of credits left on NIM API _202506](https://forums.developer.nvidia.com/t/cannot-find-the-amount-of-credits-left-on-nim-api/337051/2)
  - we removed the credits system earlier this year. The NVIDIA API catalog is a trial experience of NVIDIA NIM, so the number of calls allowed during a certain period of time is designed to serve evaluation and prototyping needs only. The rate of requests will vary per model queried and may vary based on the number of concurrent users. To verify rate limits of the models being used, please check your account at the top right of the navigation bar of build.nvidia.com

- [Getting 429 Too many request for NIM cloud api _202506](https://forums.developer.nvidia.com/t/getting-429-too-many-request-for-nim-cloud-api/335755)
  - We are currently experiencing 429 (Too Many Requests) response codes when using the NVIDIA NIM cloud API. Previously, the same integration was working smoothly in our project. However, we are now encountering this issue even with as few as 10 requests in a loop.
  - API Endpoint: https://integrate.api.nvidia.com/v1/chat/completions
  - Please note that the API Endpoints are only to be used for experimentation, development, testing and research

- [Model Limits - NVIDIA NIM / Models _202504](https://forums.developer.nvidia.com/t/model-limits/331075?utm_source=chatgpt.com)
  - We do not plan to publish specific model limits, since the limits only apply to the APIs which are for trial experiences.
  - For unlimited usage of NVIDIA NIM, check out NVIDIA AI Enterprise, the Hosted NIM endpoint providers (Together.ai, Baseten, Fireworks) or DGX Cloud Serverless Inference.

- [Clarification on NVIDIA embedding/reranker API access and costs - Intelligent Video Analytics / Visual AI Agent - NVIDIA Developer Forums _202512](https://forums.developer.nvidia.com/t/clarification-on-nvidia-embedding-reranker-api-access-and-costs/354320)
  - Are you running your embedding/reranker model locally? If so, it’s free; it only consumes the computing power of your local GPU.

- ## [Deepseek V3.2 is now available on Nvidia NIM. : r/SillyTavernAI _202512](https://www.reddit.com/r/SillyTavernAI/comments/1poinrj/deepseek_v32_is_now_available_on_nvidia_nim/)
- Does anybody know if there are any rate limits for Deepseek models on NVIDIA NIM?
  - There's no daily limit, just a limit per minute; if I remember correctly, it's 40 requests per minute for everyone.

- NIM has extra content moderation guardrails that the official API doesn't have - the official API is dirt cheap and works great so I don't see myself bothering with this
  - Me neither, I actually prefer using the official API. But the Nvidia NIM models aren't censored, they're on par with the originals, so I don't think they have the protections you're probably looking for.
- Ok now that I'm looking more closely it looks like the content moderation micro service is an optional component - but looking at their terms of service, NSFW is not allowed and they supposedly scan for it https://ngc.nvidia.com/legal/terms

- ## [佬们，像这种缝合怪的AI应用聚合站，是不是有统一的源码啊，我已经看到好几个了 _202405](https://linux.do/t/topic/98476)
- GoAmzAI, SparkAI, 奈斯猫 AI 你试试看这几个，以前见过的就这几个

- GoAmzAI 授权 2400 定制5000+

- 这都是各种闭源二开，有的卖源码，有的只卖授权，开源很少

- ## [【首发】全新高颜值的VoAPI正式发布，免授权，基于NewAPI开发，完全兼容支持 _202409](https://linux.do/t/topic/218357)
  - 断断续续花了几天时间开发的， 基于 one-api 与 new-api 开发的更好看和轻便的 AI 模型接口管理与分发系统，免授权使用。
  - 增加登录 / 对话 / 绘画 IP 记录
  - 注：本系统为闭源程序，免授权，若有介意请勿使用。

- ## [各位佬，你认为最好看的newapi二开版本是哪个？ _202508](https://linux.do/t/topic/889486)
- Veleora

- 除了特别偏的 api 源，大部分都支持 OPenAI 格式，所以对我而言，与其要求它有一堆我用不到的功能，不如要求它好看一点

- onehub 我个人觉得最简单好看

- ## [【T佬】公益站被非法倒卖，我有风险吗 _202511](https://linux.do/t/topic/1150763)
  - 我公益站资源被咸鱼上倒卖 1w，本身公益站提供 openai 服务就不合规，我有风险吗？
  - 无论事件真实性如何，受伤的都是我啊。关站已经成定局。不管真假，先关站规避风险。

- 个人觉得没事，因为你个人没有盈利。

- 先出公告，撇清责任，让买了的去退款。 还要标明你马上关服了，钱不是你收的。 先免责再说，谁收的钱找谁去。 不然交了钱的误会你是参与方就惨了, 1W 数额说大不大 说小不小, 够得上那啥了

- 自己买几个，然后去后台看是哪个渠道？顺藤摸瓜，摸到了就举报他，摸不到就封自己号，要求退款！

- 百度开发的一款 AI 法律工具 ，依据恐怕是有的 [法行宝-您的免费AI律师](https://ailegal.baidu.com/)

- ## 💰 [有没有大佬搞一个靠广告盈利的免费大模型api站 _202510](https://linux.do/t/topic/1045546)
- 广告费远不够覆盖 ai 成本的。既砸了公益口碑，还要自己往里面垫钱，何苦来哉

- 参考腾讯元宝现状

- API 站不是用户界面啊。 文本里自动插入广告会导致大量场景无法使用。
- 可以是每天隔几个小时去站点页面上看广告获取额度，但不能是在客户端输出广告。

- 把签到改成看广告了是吧。

- 我们做过这种站点，目前已经关停了，我个人认为这个模式不健康， 或者广告人需要摸索出一个新的良好模式。
  - fmvp 大佬建议的这种模式和 x 果短剧等流媒体平台类似，大家一定知道，这种注意力剥夺式的广告，并不适合 ai-api 调用，因为开发者需要保持很强的专注度，如果一个开发者在一个 case 中，刷了 3 个广告之后，思想一定无法腾空。
  - ai-api 站点如果间接瞄准用户怎么样？ 也就是开发者需要按照 api 站点给出的接口示例，将自己的产品打造成多次请求中，固定向用户展示一次广告的方式。 这样开发者成本降低、用户为 api 供应商直接献力。—— 这个玩法就太新颖了，首先很多供应商不懂广告，广告的模式也很粗暴，开发者不仅需要向供应商妥协，还破坏了用户的使用体验，这样的产品就难生存了。这一点我们以后可能会看到有人破局。
  - ai-api 广告的植入方式，有个新玩意，那就是根据 prompt-keywords 的关联度，触发一些预设语，让本次输出结果除了 “顺利交差”，还 “夹带私货”。 AI 搜索引擎产品，在结果中根据广告主投放，修改权重，就是很典型的例子。这个相对优雅，但是也差强人意 —— 这样的产品竞争力不行，用户信任度低（为什么纳米搜索狗都不用）
  - 以上是几个简单的分析，有很强的主观色彩，但有很多现货的案例可以佐证，后期可以细聊。我们运营改旗更张，现阶段也在调研公益站点的生存之道 —— 调研 —— 你需要什么样的公益站

- 结尾插广告不影响使用，广告就没效果，自然不会有广告商投钱；影响使用可能就转向别的了

- 我作为程序员，不太能接受广告的形式，在上班中弹个广告出来
  - 宁愿付费，公司还能申请报销

- ## [各位佬的公益站点是不是都不支持上传文件 _202509](https://linux.do/t/topic/971390)
  - 我摸索了几天 添加了好几个佬的公益站 发现都不支持上传文件
- 我知道的只有官方 Gemini 和 OpenAI 的 Responses API 支持传文件呀, 而且大部分公益站用的还是 2api

- 模型原生支持文件的不多，换个支持文件处理的软件解决更快

- 很多 2api 都没处理图片 

- ## [目前哪个公益站claude code体验比较好呢？ - 开发调优 - LINUX DO _202511](https://linux.do/t/topic/1114843)
- 付费站体验都没几个好的

- 收费的都崩，公益现在也难，别勉强了。 搞个 GLM 4-6 勉强蹬一蹬吧。 我用魔搭的 KEY，小蹬也算够用。

- gemini pro 只能用 5 次。 超额就变成了 gemini flash 。

- ## 🤔 [如何最大化利用社区key（自动故障转移切换） - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1098166)
  - 现在各家 ClaudeCode 中转都难保障 24 小时稳定性，自动切换显得灰常重要

- Claude Code Hub 虽然目前还不支持 auth token, 但是负载均衡和故障重试这一块儿绝对是杠杠的

- claude-relay-service: CRS暂不支持自动切换重试

- 感觉无论key还是token都可以全塞http请求头里，让中转商服务端自行忽略处理
  - 那样就不符合请求透传的原则了, CCH 的原则是除必要头部外不对请求做任何处理

- [怎么看每个公益站的RPM呢  _202510](https://linux.do/t/topic/1108753)
  - 公益别逮着一个薅，开轮询负载均衡一下
  - 我也想问一下关于轮询的问题，很多公益站的模型命名都不同，应该如何导航到同一个id，我尝试在veloera里手动把渠道模型id改为同样的id，但是当我调用的时候，当一个渠道的模型无法使用，也不会给我自动轮询到下一个渠道

- ## [CC封号太严重了，上车就翻车，平替用CC+GLM还是CodeX ？友友们有经验吗 - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1092260/10)
- glm用着用着，会有问题解决不了的。还是需要一个能力更强的AI

- 有几个渠道
  - 1. 最省钱的 直接咸鱼买 尼日利亚 app store充值卡, 差不多89 RMB = 15000 货币, 刚好14990 可以订阅claude
  - 2. Google play 绑定国内visa 卡 , 应该也可以直接订阅claude
  - 3. 虚拟卡, bybit之类的就可以随便订阅了吧
  - 我现在是方案1 , 什么时候这个不好使了我就用虚拟卡订阅, 梯子是要的, 但是这个网站里面不是到出都分享免费的梯子吗

- GLM4.6现在都敢和GPT-5并肩了？这几乎没什么可选的吧，CODEX CLI，除了慢点起码在做事, GLM4.6超卖严重，你愿意和其他人一起抢卡和抽奖可以试试。

- ## [目前有哪些公益站支持codex？ - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1095599)
  - 国庆节之后用了一段时间codex，感觉不错，期间也用了一些公益站的。不过自从openai减量之后好像都用不了了。使用team也会报账号关联的问题。
- No available OpenAI accounts support实际上是由CRS导致的BUG，原先只需管理员在后台手动重置状态即可，同时她适配的也有问题，我是使用OAI-KEY的形式接入，居然也会被限流拦截，然后不走企业微信推送

- 大多数公益站的gpt-5只能聊天，不能工具调用。偶尔有公益站用的是官逆的gpt-5，属于站长用爱发电了。 

- [公益站codex要怎么配置呀 - 开发调优 / 开发调优, Lv1 - LINUX DO](https://linux.do/t/topic/1017195)
  - 公益站里有一些余额，想使用codex。但是不知道怎么使用。下面的办法都不行，是不是有些压根就不支持？这个配了也用不了，大佬知道怎么弄吗？比如23公益和 xmdbd
- 有些公益站不支持Codex的，支持的在文档或者公告里都会说明

- [第一種： 用上env_key，需export api key as environment variable]
  - [第二種：用http_headers，需在 auth.json加上api key，但不用export env var]
- 我用的佬的23公益站，方法二调用成功了，感谢佬提供的方法

- 不知道你是怎么调用的，如果是调用作为mcp的话，那就偶尔才能成功。因为这个只有基本的chat功能，你可以找一些支持fc功能的站点

- ## [一个 Claude Code 公益站，支持 GLM, DS 3.1, Qwen 3, K2 等 - 资源荟萃 - LINUX DO](https://linux.do/t/topic/895380/1)
- 虽然我创建了 Veloera。但用 new api 而不是 veloera 原因很简单，veloera 还没有 cc 支持  

- ## [B4U公益站的Claude是只能对话吗 - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1066446)
- 算是b4u的技术问题，没有部署用原生工具调用的版本，所以效果不太稳定

- 也不支持图片呢
- 接 roocode 用挺好的。 cc 是不行。

- ## [【B4U公益站】是克劳德，我们有救了！（每周六限时开放注册） ](https://linux.do/t/topic/801848)
  - 渠道技术： Claude-SessionKey号池→claude2api→FC使能
  - 模型特点：支持工具调用、上下文 128K+、支持 RooCode，不推荐接入 ClaudeCode

- 大转盘是彩蛋，在投喂站里，投喂站从主贴进去就好了

- [B4U公益站接入Claude Code尝试(CCR接入) - 开发调优 / 开发调优, Lv1 - LINUX DO _202509](https://linux.do/t/topic/921779)
  - 在站内查看相关的帖子，站长也开了接cc的研究贴，效果不太满意
  - 当前缺点上下文太小，导致经常触发上下文压缩，损失项目信息，回应也更慢。上下文小可能是其他原因，还得研究研究。更新：最新尝试64K上下文也行，mcp调用没啥问题，但文件编辑错误次数有点多

- 上下文好像是最近A社限制了免费对话上下文的原因，以前如果开启网络搜索是可以128k，现在都是20k了似乎

- b4u之前就提供了实验性claude code，用这个不需要用ccr

- 直接配置用CC的话，前几次试过，体验不好，错误率太高了。各种报错

- 之前用这个公益 ＋ cc 的时候经常不能调用工具，体感不是很好

- B4U用的应该是Toolify，原先对Claude Code的tools支持确实有限。这几天Toolify做了几次比较重要的更新，包括工具调用的格式强调、tool_call消息的处理等等，现在工具调用的体验应该会好很多

- 1，上下文绝大部分时间仍是128K+（每天有半个小时会降至10K）
  - 2，newapi:v08660之后，就已经支持直接cc以及其他代理工具，基础功能、文件读写编辑都可以通过测试，稳定性、速度、智商我都不满意，所以不推荐接入cc
  - 3，一直用的是杯佬的toolify旧版本，新版0827经测试b4u的适配性、稳定性不如旧版

- kilo使用b4u，发现大概120k附近就会开始报错了。

- ## [请问公益站就是有老板免费提供API意思吗？  _202510](https://linux.do/t/topic/1036007)
- 有一部分是
  - 用限时免费的渠道，转到公益站
  - 批量注册薅的免费新人福利羊毛，转到公益站
  - 批量 2api 转的
  - 低成本薅注册羊毛，转到公益站，比如批量虚拟卡开号，或者用接码平台批量注册硅基获取邀请余额之类的

- 公益站稳定性非常一般。经常回答问题一半就挂掉了。做项目的话老老实实买吧。
  - 我只知道我后台的 GLM-4.6 和 Gemini-2.5-Pro 的报错率不到 2%，绝大部分报错都是传了敏感内容

- ## [有点好奇公益站的API都是从哪搞来这么多的 ](https://linux.do/t/topic/1606515)
- 批量注册（国外 AI 不像国内大部分只需要邮箱注册、麻烦找网站和写批量脚本）、爬虫密钥（比如 github 总有马虎开发上传 key）

- 我买的 pro 号只拿来用 sora，codex 额度不蹬浪费了，遂开了个公益站

- 爬虫密钥都是什么时候的老黄历了，现在基本上扫不到了
  - 这些 api 站点的主要来源是各种各样的逆向。

- ## [公益站的api来源是什么 ](https://linux.do/t/topic/1099545)
  - 2API和投喂为主
- Gemini-2.5Pro和绘图系列为GeminiCli逆向，可以自行部署使用较为稳定的，不做项目推荐，因为在用系统系Claude魔改版本
  - Gemini-2.5-flash有个轮询分组，来源于其名称一模一样
  - GLM系类为官转，转接与官方渠道
  - GPT系类为官转，其中5-Codex来源于逆向Codex，5来源于微软AZ
  - KAT来源于快手官方平台转接
- OpenRouter、OaiPro 这种是正价官转（不过这俩不是公益），是纯官方 API
  - 其他公益站就是明确告诉你主要渠道就是 2api，公益站一般是免费站 2api，付费站则主要是 Pro/Max 2api，当然还有 GLM ￥0.01 亿万 Tokens 这种不是 2api 的随机羊毛。偶尔也有大善人 Azure、AWS 等赠金快过期了捐给公益站这种也是纯官转 API。

- [观23公益 翰林文苑有感 麻烦佬友们进来指点一二 ](https://linux.do/t/topic/1115602)
- 大部分都是平台薅羊毛或者 2api，但是都不稳定，很麻烦，没点信息渠道或者手段很难维持的，我的已经停摆了。2api 就不说了，站内一大堆，平台薅羊毛一般都是批量注册号来白嫖免费 api，再放到中转站轮询调用，我知道的有 iflow, 硅基，七牛云之类的，不过薅多了平台风控就严重了，后两个已经限制的很严重了。然后有手段的话海外的某些平台应该也能薅。你要搞的话可以试试薅快手国际版的，站内好像没见人薅，国际版的注册一个号给两千万 tokens，单邮箱就能注册，写个程序批量注册应该不难，不过只有 90 天有效期。
  - 总之我觉得搞这玩意信息差很重要呢，有些东西发站里会被蝗虫般薅秃，或者门槛高，违 f，所以比较少人分享

1. 首先你要有渠道，没有别往下看了
2. 你要有闲置资金，时间。至少要有自己的服务器吧，没有就得各种薅，折腾。
3. 有渠道，有时间，有资金。那就开始造。
4. 可以接入，newapi/one-hub/done-hub。记得在 Linuxdo connect 中申请应用接入，配置好 L 站登入。差不多就完事了。
5. 奔着公益去开公益，不是很推荐。我们都是奔着折腾，玩弄的。就比如我的，智谱年包 lite 230 / 年，netcup 服务器 55 / 月，各种七七八八还得 100 / 月。就这都还有人贴脸说各种不行。不过我很少回应。不行别用

- ## 🤔 [深入浅出，解密 L 站内中转站的秘密 - 搞七捻三 / 搞七捻三, Lv1 - LINUX DO _202509](https://linux.do/t/topic/981851)
- 目前据我所知的中转站分为两类：
  - 1 是通过类似 new api 进行转发的
  - 2 是直接提供官方账号的 sk 的

- 通过类似 new api 进行转发的，本质上连接到 claude 或者 openai，都是同一出口，中间过了中转站站长的号池，这里会出现一个差别 ** 缓存命中 ** ，也就是说如果同一个人，短期内都用一个模型，模型会更加容易记住自己要做什么，效率更高，费用更低
  - 改成多队列，按人分列, 提高了缓存的命中率，从而降低成本
- claude的plus和max套餐，区别在于使用的tokens，那站长们除了提高缓存命中，减少tokens消耗之外，当然就要给你的账户限制额度啦，假设一个claude max一天可以瞪1000美刀，那么一般的站长就会超发，会拆成每个人100美刀，卖15个人左右，因此你会看到中转站大多数都是按月套餐，每日限额
- 优势：轻度使用时，费用低，使用简单【不需要管节点和号池】
- 劣势：重度使用时，费用高，非同key比同key效果差【本人用中转站codex和gpt-team codex对比结果】

- 接提供官方账号的 sk 的
  - 除了缓存优势外，就是不限额，这个key只有自己在用
  - 优势：重度使用时，费用低，缓存命中高，效率高，效果好，稳定性高
  - 劣势：需要自备干净节点，具备一定的基础

- 少了一种：二开插件或者包装插件的，这种就是黑盒了。

- 公益站就多了，还是得分类
  - 如果只对编程来说，几乎比较少公益站能稳定运行，因为编程的封号概率极低，他们这些号主要来源于，别人想要激发退款流，而抛出来的账号，例如max用户，订阅是1个月，大概使用20天之后，就会抛出他们的账号，让大家刷，便于退款，公益站多数收集这些账号，途径包含L站或者隔壁站点之类的，甚至飞机上会有相对于的群聊
  - codex的途径相对简单，目前都是来自1刀team的比较多
  - 其余就是富可敌国的中转站们放出来的公益，比较没人用就是沉没成本，还不如趁机推广
  - 有以前一些AI中转站推广的时候送的余额+注册机堆积起来的，像火山，openrouter，硅基之类的，也有gpc300剩余的余额用于公益站的，渠道较多，稳定性也较高，打野的除外

- 目前的codex来源大多数是用野卡1美金开了一个月team，相当于成本很低，所以大家都拿来做公益
- 其实都是辛苦费，因为你不知道什么时候，号就掉了，掉了又要担心会不会黑卡，会不会风控，如果是境外卡，风控被冻结了，人是要去国外解冻的

- 野卡连卡都是野的，没有人在乎这个的，而且1刀team的途径很多，还有通过google pay去开通，另外openai没有claude监管严格了，应该知道自己热度不行了，封号的越来越少
- 国外一堆野鸡银行的信用卡，野卡目前也只能用来开1刀team，卡未必就真的是你的实名，月末你不还款，卡就被冻结了，但是野鸡银行申请卡非常简单，一般一次能申请20-30张

- 2API只能被拿去镜像站和酒馆，因为2API的没有function call，调用不了工具
- 不能调 function call的 还有一种，就是逆向的，说白了中转的背后和你在网页版聊天一样，这样就没有按tokens计费，这种在一些特定情况下就会不太好用

- 可以看看亚马逊对这个缓存的介绍，不是简单的问题，他默认的周期是5分钟， 系统会自动检测重复的代码模式、上下文和请求，同人同key命中率能达到90%。

- ## 看到一个同行退了，所以还是 A 厂“胜利”了
- https://x.com/tuzi_ai/status/1982641845575589987
- 这行当是时间窗口期生意, 无限开卡白嫖撬信息差杠杆, 1美金开个codex团队账号, 上百人民币往国内卖, 持续补号, 直到对手开始补漏, 生意就会进入消退期
  - 但这种信息差用不了多久就会出现一次, 跑通了渠道后就可以一直换品了
  - 最不济最后就是转成正规军呗

- ## [感觉大厂 2api 才是长期公益站的最好方案  _202508](https://linux.do/t/topic/919087)
  - 2api御三家 grok，qwen，z.ai
  - 都有共同点：注册简单，token 刷新简单/长期有效，高并发，稳定，0成本…
  - 反观其它大部分api羊毛的共同点：很难长期，渠道一公开就活不久，上某三字脚本大概率封号…
  - 不过2api缺点也明显，只能聊天，很难用于科研/代码领域

- 只是占有率还不高的吧, 占有率高了可能就去反2api了
  - 2api本来就不是很稳定的 而且还不支持很多功能

- 最好的方案当然是aws, 官转啦

- 2大厂的也有可能被封号，而且随便改点参数上点验证2就失效了

- grok4和qwen一堆新模型上线，都没改过已有模型的参数 老项目直接用
  - 有验证的只有grok一家，貌似只有亚洲ip才会触发

- 我跟佬友们保持长期良好关系，是我最好的方案

- ## 🤔 [各位运营公益站的佬，想请教公益站的key一般怎么来及封号策略 - 开发调优 - LINUX DO](https://linux.do/t/topic/838799)
- 免费轮询较多，或者2api（哪来的这么多富哥）

- 站内的稳定公益站都做的很有原则，没遇到随意封号，现在慢慢的只用稳定站了。本来是想均匀用，各站都用一点，不逮着一家薅羊毛 

- ## [关于站内各种公益站的一点困惑 - 资源荟萃 - LINUX DO](https://linux.do/t/topic/846699)
  - 首先感谢各位佬的大义，提供各种key，但是站内各种漫天飞的公益帖子 ，试过不少配置好了之后发现过几天就失效了，都让我产生一种是不是来骗赞的感觉。

- 3 级的就比较稳

- 公益站这种东西很多是朝生夕灭，毕竟免费的东西也没法要求，如果真的有持久的需求还是用正式的东西，公益的适合用在一时兴起的玩具上

- 看公益站渠道来源、大方程度（随便发个一千刀的大概就是来玩票的），其他的也区分不了，不排除部分公益是集合 L 站公益或者找个某个 2api 渠道后练手部署的，见仁见智
  - 再加上可能有号商打击，所以公益死得快是情理之中的事

- 不要对免费的东西有太多执念
- 既然公益，放出来免费用一段时间就可以，这时间可能长或短

- 可以用这样的逻辑理解：支付一个赞用以换取一个短时间的服务。这就好比淘宝上一毛钱一个的wps账号，便宜吗？确实便宜。长久吗？肯定不长久。我觉得编辑帖子花费的时间精力以及信息差本身自带的价值还是值一个赞的。

- 一个人从各种渠道获得了自己用不完的资源，打算贡献出来无偿分享给大家。这是一种美德。 对于这类人，我们应该赞扬他，而不是妄加揣测。 至于你想要找寻的稳定的公益站， @tbphp 的公益站做的非常出色，推荐。
- 放下对公益站的执念就好了，心态放稳，用的时候做好下一秒就消失的准备。当然，也有稳定的，所以T佬公益站的口碑就出来了不是。

- ## [公益站好多！已经对额度麻木了 - 搞七捻三 / 搞七捻三, Lv1 - LINUX DO](https://linux.do/t/topic/1091221/25)
- 我之前也注册了很多，后来慢慢的只剩几个主力了。因为稳定性是个大问题，工作中被打断这件事比较头疼

- 感觉kyx里面claude code不好用，上下文太短，根本写不了代码

- 没几个能用cc 的，没几个额度超过 10 刀的，没几个不是高负载、号池没号的
- 真能干活的没几个，现在用这ang。。。其他几个要么没额度，要么不能直接调用，要么截断。

- [Augment没了，接下来用啥呢  - LINUX DO](https://linux.do/t/topic/1090749)
- 能用claude code最好，不然droid凑合也行，
  - 现在cc中转站因为封号要么涨价要么降智掺水，体验可能还不如droid这个cc下位了，
  - codex我今天试了下，太慢了而且我ubuntu和他那个沙盒模式有兼容问题，这也运行不了那也没权限
- codex我因为这个沙盒问题体验很糟糕，但我看很多人也认为codex和cc是一个级别的，droid我是用了几天，我感觉比cc是能感觉出差距的，但droid免费用claude4.5+gpt5，而且速度很快，codex抛开那个在我电脑上的沙盒兼容问题外，速度也是太慢了，因为我没买那种特别贵的cc中转站，现在用的我感觉是降智很明显，所以我觉得目前我最舒服的是droid

- ## [求推荐稳定的聚合AI大模型平台 - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1084727/1)
- 满足你的要求的只有openrouter

- 公益站好像都不稳定吧？

- 站内公益站很多都很稳定啊，薄荷佬的，翰林文苑的，都稳定呀
  - 收费的那就看看富可敌国吧

- 我看现在富可敌国都是做codex和cc，没几个开放api呢

- 如果要稳定又要便宜，低价的是没怎么，原价的倒是有挺多

- www.hubagi.ai, 这个有国内的模型，比官网价格便宜，可以用api调用，也很稳定

- ## [如何聚合各家公益站的api - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1005534)
  - 站内有非常多佬提供的公益站，同时各家公益站又会有很多一样的模型，我的想法是本地搭建一个new，然后配置对接各家的公益站，通过让各家的api轮询，这样子用ai的时候就能雨露均沾了，各家api通过同一个模型名称调用，实现负载均衡
- 怎么实现的？我现在是用newapi重定向功能，的确是集合了，但是不能自动切换，还需要手动切换模型

- 之前有这个讨论，不过要注意，有些公益站是不能用new api聚合，怕二次分发，所以佬友记得要看一下公益站说明

- 很简单的, 模型名一样就可以配置负载均衡了, 自己配置一下模型名到id 的映射就行了

- 目前的方案是gpt-load+newapi, 等gpt-load更新聚合分组和重定向，自用就不用再搞个newapi了

- GitHub - atopos31/llmio: llm接口负载均衡工具 我自己写过一个

- ## [求推荐免费模型api，公益站付费的太慢了，只是用于ai中文翻译成英文，速度有要求 ](https://linux.do/t/topic/1061766)
- 免费的还要快准的 那就薅平台羊毛吧，或者本地搭建一个小模型，肯定嘎嘎快

- 4396佬的cerebras，嘎嘎快

- cerebras的快, ollama cloud的速度也很快 就是上下文砍了

- ## [佬，有哪些好用的公益站llm（个人对话，用量小）  _202509](https://linux.do/t/topic/930055)
- 很多佬的公益站是不让公开的，多水水或许就遇到了呢

- 都是站内的，只要到了等级就能看到了, 你如果的等级不够才看不到，多水就行了

- 所有公益站默认均不支持和对外分享。 除非站长本人同意了。 所有公益站发布原帖子有级别限制的， 默认不转发给级别不够的佬友。 还请新加入的佬友用心升级。

- [[KYX API 公益站] 红绿榜也来了 kunkun 背景也加上了 是ikun就来抽 ](https://linux.do/t/topic/1093602)

- ## [好奇这些公益站的商业模式是怎样的，如何赚钱维持运营 _202508](https://linux.do/t/topic/833661)
  - 论坛里一堆各种api网站，b4u inst anyrouter之类，频繁提供免费api，我一天就能嫖1k左右的货币（不知道是cny还是usd），很好奇这些网站是如何保持生存的，这种行为的目的是什么。

- 一般可能是有别的业务来回血 比如区分等级 免费付费用户之类的

- 都是玩流量的，“公益”往往都是自己用不上的资源，你白嫖他，他白嫖别人。简单几个字：倒买倒卖
  - 所以，早些时候就看到有些人吐槽“零度解说”毁资源，其实这只是愤怒的一种说辞，其实很多资源分享的人，从一开始就知道这资源分享出来不会长久，也不会刻意去想着保护资源，他有自己的目的，可能是商业性的，也可能是兴趣之余回报别人。想保护资源的往往是白嫖了，又不愿意继续分享下去的中间人，这就是人性，面对利益，都想据为己有的心态。
  - 真“公益”也有的，但往往这种极少，本身作者已经是处于社会的佼佼者了，真正能做一点自己理想中的事情了，比如linuxdo，我们看一个人怎么样，往往是这个人做了什么，从论坛创建初期，到现在为止，linuxdo始终在用金钱和责任感为大家提供着一个好的交流氛围环境，这种公益目的就不那么商业化了，主要在于作者的心态，比较随心

- b4u是逆向的，就算通过ccr用在cc也不稳定吧
- b4u是普号池啊，时boom时好的 塞进去都不知道啥时候断

- 靠爱发电啊, 我公益站流量超了都是自己掏钱的, 但实在顶不住了，一天20G流量，只好关停撤啦

- ## [Resource List to build with LLMs for 100% FREE no credit card : r/learnmachinelearning](https://www.reddit.com/r/learnmachinelearning/comments/1ihvm0c/resource_list_to_build_with_llms_for_100_free_no/)

LLM

free LLM from galadriel.com (free 4M tokens/day. This is by far THE best option and i use it myself)

free cerebras and groq -- extremely fast LLM responses but cerebras needs u to sign up on a waitlist

Gemini flash: super generous free tier (1500+ requests/day)

Monitoring

posthog and sentry for monitoring (both with generous free tiers)

Cron Jobs

Free cron jobs via ubicloud.com / github actions

Modal.com gives 30$/month for GPU usage credits

AI Training

Lightning.ai gives u GPU workspace for free

Deployment

free hosting via heroku (24 months for free from github student perks)

Digital Ocean 200$ free credits (needs cc tho)

render has some decent deployment options

Database

cockroachDB (10 GB free)

supabase for DB (500MB free)

free 5GB postgres via aiven.io

- ## [Mistral "free" LLM API is a game changer for so many developers : r/SaaS _202409](https://www.reddit.com/r/SaaS/comments/1fmxg9k/mistral_free_llm_api_is_a_game_changer_for_so/)
- free tier: It's one request per second, 500, 000 tokens per minute, and 1 billion tokens per month. Except Mistral Embed, which is two hundred billion tokens per month.
