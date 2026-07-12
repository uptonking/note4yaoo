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
  - 首先按优先级排序，其次按权重排序(目前是按添加顺序排序)

- 模型列表界面，支持调整用户分组的展示顺序

- 刷新页面会使系统崩溃429，待排查是前端问题还是后端问题
  - 复现步骤: 快速连续多次刷新任意页面如 http://localhost:4090 

- admin配置模型名映射后, 使用token的用户的日志名应该显示别名，而不是原始名称

- 日志记录
  - 搜索支持模型名模糊匹配
  - 支持按session id搜索， 可参考各种chat viewer的设计

- load-balancing
  - 优先级和权重分开设计显得繁琐
  - 可支持小数如50.8， 整数部分是优先级，小数部分的权重用来负载均衡

- ai-provier-issues
  - mistral api转换为 claude api 时, 出现异常 Expected last role User or Tool (or Assistant with prefix True) for serving but got assistant
  - 字节火山: [Transformer maxtoken field ineffective for Volcengine API with DeepSeek-v3 model ](https://github.com/musistudio/claude-code-router/issues/213)
    - The maxtoken transformer field in the configuration does not work properly when using the Volcengine API with the DeepSeek-v3 model, resulting in API call failures. However, the same configuration works correctly with the DeepSeek-R1 model.
    - 👀 仅deepseek-v3.2存在此问题, glm-4.7正常
# ai-providers-devops
- 当2api失效时，先不要怀疑是软件没更新或平台故障了， 先去主流论坛/交流群看看是否有同样问题，可能就是风控严格了
# donehub/one-api
- codex-cli的渠道接入很简单, 类型选custom， 添加模型名即可, 不需要开启 v1/responses 

- there is no configuration option to enforce max context length
  - While there is a `ContextLength` field in the ModelInfo struct (model/model_info.go:12), it is only used for informational/display purposes in the web UI - it does not enforce any validation.

- exceeded retry limit, last status: 429 Too Many Requests 频繁出现问题，但无法确定哪个channel/provider
  - 因为频繁出现，说明优先级和权重高, 缩小范围
  - 然后可以观察api的使用记录，观察哪个权重高的api没有出现在使用记录中，说明这个渠道出现了问题
  - 最后可以让agent排查日志，锁定channel id

- 
- 
- 
- 

## 🔠 prompts

- project `done-hub` in current folder implements a openrouter-like llm gateway that supports to input different llm providers/channels and expose one unified llm api for users. 
- it is running locally by `./dist/one-api --config config.yaml` on my mac. the log is at folder `~/Documents/runlog/donehublocal` .

- done-hub also supports to transform llm response format between openai/claude/gemini compatible api.
- several minutes agon, i configured a channel 74(named cline_gateway__yaoo) that itself is openai-compatible api. and i use it in claude-code cli by `http://localhost:4090/claude`. but claude-code does not work. i backuped the log at `~/Documents/runlog/donehublocal/channel74`.

- 
- 
- 
- 

- several minutes ago, when when i use llm api, the error is

- please analyze related logs and code, explain to me the reason and how should i configure the api channel

- 
- 
- 
- 

# new-api

# cliproxyapi

- codex oauth 在firefox浏览器登陆第2个账号时，无法触发回callback, 但在chrome浏览器可以
# discuss-stars
- ## 

- ## 

- ## [CC Switch 在Claude Code里用gpt，如何使用xhigh的思考 - LINUX DO _202604](https://linux.do/t/topic/2054991)
- 

- [CPA使用gpt-5.4(xhigh)问题 - LINUX DO _202603](https://linux.do/t/topic/1783205)
- cpa里面的写法是gpt-5.4(xhigh)，cherry studio里面的写法又是另一种

- ## [聊一聊信息渠道，我觉得我自己很信息茧房 - LINUX DO _202604](https://linux.do/t/topic/2054193)
- 常用的信息获取渠道
  - telegram + 极搜：我觉得很难用，搜片都搜不到契合的，要翻几页来筛选，总是搜出搜一些无关紧要的聊天记录。还有TG上要么是骗子、要么是二道贩子，想找点儿一手的信息很难
  - Twitter：Twitter上的搜索功能更是:poop:，和我用过的所有产品搜索功能完全不一样，就感觉像是它不想让你搜索一样，给出的信息总是很少、无关、全是颜色广告
  - Linux.do：我自己最爱的信息获取渠道了，获取一手的教程很方便
  - NodeSeek：第二喜欢的信息渠道，交易和教程
  - V2EX：学生时代爱上，做产品经理了就远离了，现在偶尔看看大家关于技术的一些思考
  - 酷安：找玩机教程，偶尔用用
  - yandex：搜破解资源（软件、影视）
  - 常见信息渠道就不说了（Google、Reddit、国内社媒…）
  - 再补一个：ChatGPT、Claude直接搜不同国家的Linux.do、V2EX类似网站，打开网页翻译，看其他国家的人在聊什么
  - 我自我感觉检索信息的能力还行，但最近多次想找一手信息源、一手渠道买东西，屡屡碰壁，真是给我心态搞崩了，才发现自己的信息检索能力大概是存在问题的。
  - 例1：闲鱼上有 “cursor 500次” 的卖家，上个月只有一家，最近很多都出来卖了，我猜想是有渠道扩散了，并且价格比上月翻倍，我自己每天都在用，因此想找找源头看能否稳定、价格合理的购买自用，但无论如何搜，都找不到。
  - 例2：前几天传的沸沸扬扬的GPT 2大源头渠道，我都是消息流传到V站后，我才知道，并且发现很多人都悄悄的用（二手转卖），这说明：一手信息是不会在站内流通的，站内的人知道也不会出来讲，但他们是如何知道的呢？
  - 我感觉绝大多数信息都是开源的，但就是检索不到。我的问题就是：如果提高自己的信息检索能力，从而找到一手信息源？

- 你举例都是灰产信息呀，流出越快，死得越快；主导世界的可能是黑暗丛林法则，那么意味着，我们始终都在茧房里，在一个自己觉得自洽的叙事里。对我而言，有限的信息就够了，我可以不停地挖深呀。挖久了，对其他人来说就是茧房了。

- 你的身份是一个pm, 关注的领域应该是流量和产品。互联网每天都有爆炸量的信息，就像美国抓马杜罗，这些信息你也想获得一手吗？信息差一直都会有，但是能拿到你关注领域的信息不就够了吗

- 很直白的讲，你陷入思维的误区了。信息不是开源的，信息被隔离在每座孤岛。与其找信息，不如找孤岛

- 去telegram各种群聊去找一手信息，成本就是时间，从大量闲聊的垃圾信息中找有价值的即时信息

- telegram 上的搜索 bot 我一个都不用，用google site:t.me 都比那些 bot 好用

- 佬可以使用下 grok 搜索渠道能力拉满，薅的 grok heavy ，一共 12个 agent 给我搜信息，爽的很

- 极搜的检索我感觉是最急眼的，感觉除了片基本上搜不到啥，也没找到过真正好用的电报搜索引擎

- 在目前的社会格局下 信息差和钱直接挂钩 你要别人的信息渠道 等于直接问别人要他的底裤

- 我来起个头，我在百度、阿里都做过搜索。 今年因为用 Grok 然后开始了解 ai 世代的搜索工具，tavily、 exa.ai、parallel、you，每个都测试了噪声、准确度。发现 Grok 搜索能力无与伦比。 我能搜到美国人的家人、门牌号、住址；可以搜索初中群里大家联系不上的同学读书、工作的轨迹。
  - 我就决定疯狂地研究 Grok，哈哈，GPT、Claude 再智能，只要 web_search 没有 Grok 好，也无法准确感知当下的问题，现在我们在 期货 的交易中使用，结合 polymarket 可以更快地感知到价格的变动。
  - 我做了监控的网关，从春节开始一直迭代～昨天又测试了历史数据清洗，绑了银行卡，测试了开销，发现 三个小时烧了 400 刀，现在问题是准确搜索的效用很大，但是代价很高～
  - 要么增加投产比，要么降低搜索的成本。

- 如果要深挖，我目前的方法是用grok+解限词这种搭配，目前grok的检索能力还是很不错的，很容易出现自己想要的东西，就是得研究解限词。平时资源获取啥的就只能自己慢慢找了，没有特别好的方法，要么就是用AI代替你的手动时间

- 当大家发现 Grok 好用，grok2api 很多人部署了，马斯克就下手了。先是图片不能生成了，前几天大范围 429，今天只有 fast 可以用了。 信息差曝光越快，死得越快，一有注册机，基本就活不久了。

- 挖信息很浪费时间，我自己的感触：最近在家没上班每天都会蹲各类羊毛，但是薅到了其实也没多大价值，掉的也快，和上班差不多，精力换渠道罢了

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
# discuss-new-api-spec/format
- ## 

- ## 

- ## 

- ## 🧩 [深度解析 AI API 里的 `/v1/messages` 、 `/v1/chat/completions` 、 `/v1/responses` ：这些后缀到底是什么，为什么要这样设计？ - LINUX DO _202606](https://linux.do/t/topic/2306861)
  - 打算从协议的设计、GPT 规范的演进，以及工程和主流厂商的不同角度，基于我的理解，解释 API 这个路径到底是什么，以及为什么我们这么写这个东西。
  - /v1/chat/completions 的核心是 messages 数组和 choices 返回值。
  - /v1/messages 的核心是 Anthropic 风格的 message 对象、content block、stop_reason。
  - /v1/responses 的核心是更通用的 input、output、items、tools、stateful response。
  - Gemini 的 models/{model}:generateContent 则是 Google API 风格：对某个模型资源执行 generateContent 方法。

- /v1/completions
  - 早期的大语言模型是文本补全类型，用户传入一段 prompt，然后让模型继续补全。
  - 这里有一个弊端，就是模型需要通过输入的文本来猜测哪一部分是系统发出的，哪一部分是用户的输入，这时就给了破限更多的机会。
  - 还有一个问题就是，你对话的历史不能结构化的输出。所有的上下文都在这整个输入中。当遇见了工具的调用，或者说多模态（比如视频、图片、声音的输入）时，就很难优雅地进行沟通。

- /v1/chat/completions 是过去几年最重要、最广泛兼容的 LLM API 协议。
  - 从一个整体的 prompt 输入变成了一个可以结构化进行处理的消息数组。

- OpenAI-compatible 的兼容程度有层级
兼容 OpenAI API，通常至少意味着它支持：
POST /v1/chat/completions
model
messages
temperature
max_tokens 或 max_completion_tokens
stream
choices[0].message.content

但不一定完整支持：

tools
tool_choice
parallel_tool_calls
response_format
JSON schema strict mode
vision input
audio input/output
logprobs
reasoning tokens
cached tokens
streaming tool-call delta
structured outputs

所以兼容可以分层理解：

Level 1：普通文本聊天兼容
Level 2：支持流式输出
Level 3：支持函数调用 / 工具调用
Level 4：支持结构化输出
Level 5：支持多模态输入
Level 6：支持复杂 agent 事件流和状态管理

- /v1/messages，Claude 的消息协议
  - Claude 的 system 通常是顶层字段， 而 OpenAI 则是将其设为了普通消息数组中的一个 role。
  - Claude Messages API 的内容可以是字符串，也可以是 content blocks。例如文本、图片、工具调用结果等都可以作为不同 block 表达。

- /v1/responses 则给出了更现代化的统一接口。
  - Responses API 中设计了一套更通用的数据结构，用于包含各种文本工具调用、工具返回的结果以及一些状态信息等，让这个内容更加抽象和宽广。
读取图片
处理音频
查询文件
搜索网页
调用函数
使用代码解释器
调用 MCP 工具
维护服务端上下文
输出结构化 JSON
返回推理摘要
产生多个中间事件

- Gemini models/{model}:generateContent
  - 反映的是对某个模型的资源执行内容的生成方法，而不是访问某一个服务。
  - Gemini 通常使用 contents、parts 这类结构，而不是 OpenAI 风格的 messages。

- /v1/embeddings 向量接口
  - 作用是把文本变成向量。它常用于：

语义搜索
RAG 检索
相似度匹配
聚类
推荐
去重
分类

- /v1/models 通常用于列出可用模型或查询模型详情。

- 流式输出也不是统一格式
# discuss-ai-api-gateway-devops
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [一个不做中转就没必要了解的焚绝 - LINUX DO _202607](https://linux.do/t/topic/2548075)
- 目前oai和a/对中转的ip都有进行检阅
a/没办法只能上家宽
oai目前是比较宽松的
但是当量达到一定级别以后
- 你的ip会被封禁，只要你这里的号池补号了，就会立马401被下线
目前解决方案是，ovh等独服，都有提供ipv6
只需要把号池出口的代理绑定到ipv6即可
v6封不完

- 直接按照v6前缀封那不就寄了吗？
  - 目前来看，还没有这么做，主要是加代理以后，多了一层网络，延迟又更大了

- 到多少量会被封禁啊 累计的还是短时间内并发？
  - 我是差不多到30B左右，总的

- ipv6虽然一个/48段很多IP, 你能想到, 对方也很清楚, 不封你ip, 直接封你的asn, 嘿嘿

- ## [If you pay for OpenCode Go, 12 of 15 models break on follow-ups. Here's why superior LLMs were having errors. : r/opencodeCLI _202606](https://www.reddit.com/r/opencodeCLI/comments/1uco67e/if_you_pay_for_opencode_go_12_of_15_models_break/)
  - If you're on the OpenCode Go subscription and use anything besides Qwen, you've probably hit this: Turn 1: You ask something. It answers. Turn 2: You follow up. HTTP 400. "The reasoning_content in the thinking mode must be passed back to the API" The Go model list has 15 models. 12 of them - DeepSeek V4 Pro/Flash, Kimi K2.7/K2.6, GLM 5.2/5.1, MiMo V2.5/V2.5 Pro, MiniMax M3/M2.7/M2.5, all produce reasoning traces. Every one of them needs that field present on every assistant message in history. OpenCode strips it. Qwen 3.7 Max/Plus/Plus is the only one that doesn't hit this because it doesn't expose reasoning in the API at all.
  - So if you're paying for Go and using anything other than Qwen, multi-turn conversations are basically broken.
  - DeepSeek's docs say it straight: "Between two user messages, if the model performed reasoning, the intermediate assistant's reasoning_content must be passed back to the API in all subsequent turns."
  - Three PRs tried to fix it in OpenCode. None went through. The field is non-standar, OpenAI's spec doesn't include reasoning_content, so every tool in the chain just drops it.
-  The reason you haven't hit it is almost certainly session length and tool usage pattern. The requirement only triggers when the model performs a tool call between two user messages. Casual back-and-forth without heavy tool orchestration won't reproduce it. The moment you run 5+ parallel subagents delegating tools across turns , which is not how most people use OpenCode, it starts failing constantly.

- ## [codex风控升级！CPA作者连更3版 - LINUX DO _202606](https://linux.do/t/topic/2283110)
  - 昨天L站已经有佬发现了OAI的风控逻辑。我总结下就是 封了的会话会污染下一个账号。 昨天在 填充优先 + 会话粘性 的情况下一瞬间风控了3个号。
  - 具体操作是： 3个号刷新了有额度，打开原来 G的会话要求继续。 前几次请求是正常的，30秒后眼睁睁看着3个号 G了。
  - 这种风控策略 意味着 即使我正价开pro，踩到G的会话依旧账号就没了。
  - 因此目前的应对： 填充优先 + 会话粘性+ 前端会话G了直接新开会话
  - 而昨天也在考虑要不要把CPA换了，sub2api有额度管理。但是在github上冲浪时发现了CPA已经有大佬提了pr，是为了解决这个问题的，就一直在跟踪。
- 为啥不直接轮询+会话粘性，一直没有过问题。
  - 就这样配挂了一半的号

- ## [深度好文——一篇文章说明白OPENAI的风控黑盒机制 - LINUX DO _202606](https://linux.do/t/topic/2279952)
- 本人使用GPT两年以上，订阅过plus，business，Pro 5x，Pro 20x。试过至少6个不同的IP，折腾过无数次，被风控的经验丰富。希望本文可以为大家提供一些关于OPENAI风控的思考，减少重复与杂乱的数据使得大家眼花缭乱
- 风控解析————什么可能决定你是否被风控？
其实很简单，无非分为两类。一种是行为特征，一种是背景特征。前者指的是用户在使用中的行为特征，后者指的是用户在使用服务的非行为背景信息。我们来举例：

行为特征：
如短时间大量并发，咨询有关敏感信息与违规信息，多端同时大量使用，单次对话复杂度过高(常发生在Pro Extend Thinking的复杂对话中，指的是5.4超过2小时，5.5超过1小时的高负载任务)，新注册帐号，支付方式，支付地区等等

背景特征：
如IP纯净度较低，机器和浏览器曾被标记过，地区与时区泄露，DNS泄露，空白浏览器指纹等等

- 风控解析————我怎么知道我被风控了？
对大众来说，绝大部分情况下的风控表现为降智。模型被路由到了低级模型。包括但不限于thinking模型不思考，Pro模型未显示Pro thinking或直接不思考，emoji的明显增多，询问模型给出的低级模型回答。但在近期风控的表现有了明显改变。一方面表现在heavy thinking的思考时长缩短，但juice值不变。因LLM本身缺乏鲁棒性所以难以量化智力，不做评价。默认认为thinking模型并没有向以往一样直接不思考，而是表现在Pro模型不思考。但也有可能是近期本人并没有遭遇严重风控所导致的。

还有一种风控表现为明显的提示或拒绝服务，这种主要是由于用户多次问答了高危问题导致的。

- 风控解析————被风控了怎么办？
我们需要具体情况具体分析。首先对于行为特征，一般静置能够有效解决问题。时间大概在12h~14天不等。对于背景特征，在解决背景特征本身的情况下，有的情况下可以即时恢复，有的也会在静置后恢复。

那有没有更快的办法呢？当然是有的。请注意，风控系统是综合的评估而不是孤立的评分。
举例：DMIT机房IP|指纹浏览器做时区和webrtc优化|因单次对话复杂度过高与并发导致pro模型路由到mini模型。
实验：
静置5h依然表现出Pro模型不思考。于是切换夏威夷家宽[qq.pw]。此时注意，本人使用的是NAT家宽，刷新出现了人机认证(此处可以体现出IP已被标记，背景特征较差)，但立刻正常。

结论：
在行为特征导致的风控情况下，除了静置[静置本身也是在行为特征上下功夫]，提升背景信息的质量也是在综合风控系统提升分数的核心。但背景信息特征并不完全取决于综合的风控值，与其本身的家宽属性也有关[可见家宽真的有用]。
[反之亦然，笔者曾经也用过这家的NAT家宽，但当时IP已经较差，被风控，加上笔者没有足够好的独立家宽VPS，静置了14天才恢复正常]。

- 关于风控的经典担心————CODEX会降智吗？
据笔者的使用体验来看，不会，但是会限速。如果您的CODEX被降智，那更多可能是普遍的bug问题而不是您的账户风险。就像Android端，桌面端，CODEX都是分开的风控体系，但也有一定的关联性。CODEX的限速表现在首字token和整体速度下降，但很难完全跟本地网络质量和服务器高载的影响因素脱离，本身这种情况也并不多见。

- 逐点剖析————行为特征
01.        单次复杂度过高：
Pro Extend Thinking的复杂对话中，具体是5.4超过2小时，5.5超过1小时的高负载任务。其实具体分为两个部分：一个是思考时长[反映的是思考token耗费]，一个是输入输出内容。为什么5.5是1小时，5.4是2小时呢？其实business的限制可以放更长一些。因为Pro订阅的模型token速度更快，business速度要慢，以及5.5的算力平台较新，token速度脱离套餐本身就更快。
01.        新注册账号：
新注册账号是典型的高风险场景。新注册帐号建议至少7天后再开付费套餐或您的背景特征较优秀，也是完全没问题，但对背景特征(如IP)的要求就较高。

01.        支付方式与地区：
低价区也是风控的高峰，但这里，OPENAI对于支付地区的权重远比支付方式要高得多。Anthropic对于支付方式和支付地区抓的都严[如果想要听后续可以出Anthropic版本]。OPENAI对于低价区的风控水平明显高于其他地区，比如土区、菲区，误杀也会显著增加。

- 逐点剖析————背景特征
01. IP质量：
这或许是全网争论最激烈的一个特征。到底要不要家宽？笔者的答案是取决于需求。如果你能接受偶尔的静置，同时并不是Pro套餐，使用率也不高或是主用codex。笔者认为一个不要太离谱的机房IP就足够，但即使网络有多个IP数据库来源也并不一定就是决定性因素。机房IP质量很好不意味着就不降智[比如邻居闹腾，被OPENAI标记等等]，机房IP差[如digital ocean，臭名昭著的IP质量]也有正常使用的情况。尽可能选择好一点的原生机房IP足矣，但不值得太多的溢价。

但，如果您是重度使用者，有pro订阅，同时对业务稳定性要求极高[毕竟您也不想着急的时候没有AI用]。我推荐您购买家宽而不是双ISP机房。一方面家宽本身的网络性质权重就较高，所以如果您的需求没有那么高，足够好的质量的NAT是可以考虑的[前提是质量一定要足够好，但实际上比较难保证，包括笔者的qq.pw，邻居闹腾，而且很多人不会保护IP]，但独立的家宽VPS或许是最终解。把其他背景特征完善，您会使用的非常愉快且稳定，全身心投入到价值产出中。

02. 机器与浏览器被标记：
这种情况其实也并不多，因为很少人使用gpt的客户端，主要还是codex居多，但codex本身并不会引起风控。解决办法是不使用gpt客户端，换用指纹浏览器。当然，如果有极致需求，也可以像笔者一样，Hyper-V虚拟机运行。出问题重新换环境。

03. 空白浏览器指纹：
该风控点不会单独作为一个拉分项，但尤其是背景特征较差情况下，新账户会显著增加风险。空白的浏览器指纹意味着高度可能的自动化脚本环境。建议如果无法改变背景特征的情况下，新的指纹先浏览一些网站，不建议一直用无痕模式的浏览器长期使用账号，否则也会累计风险。

基本上就是这些内容，笔者想到哪里写到哪里。基本也覆盖全了。如果有想看Anthropic的，笔者有空会写一篇。主要基于笔者本人的各种案例，因为两年来笔者被降智麻了。

总结OPENAI的风控系统，综合是最大的特色。无论是风控系统本身还是风控中的每个参数特征，无不是互相影响，综合决策的。没有绝对的风险，也没有绝对的安全。谢谢各位看到这里。

- dmit的ip很差吗 我扔在上面的好几个plus全都跳二验了
  - 我是64段的，可能是有差别的，但DMIT整体IP质量不高

- 毕竟大家都是各取所需，一个要token，一个要好看的ipo招股书 

- ## [开源了一个OpenAI/Codex的邮箱重新登录工具 - LINUX DO _202605](https://linux.do/t/topic/2262563)
  - https://github.com/haeyupi/relogin-mail-manager
  - 最近gpt/codex登录及其不稳定，因此需要工具进行大规模批量重登，所以relogin mail manager这个工具就孕育而生了。
  - 它从你的邮箱资料中导出Outlook/Hotmail邮箱、邮箱refresh token、OpenAI密码和手机号，然后在本项目内完成邮箱验证码读取、重新登录、token保存和可选的远端上传。
  - 项目不依赖外部邮箱池服务。所有账号资料都保存在本地 SQLite 数据库中。
  - 目前我关于cpa的已经试过，sub2api还没测试过

- ## [【HelloKimi】免费无限的KimAPI+0成本+工具调用 - LINUX DO _202605](https://linux.do/t/topic/2244578)
  - 在之前，我们已经向DeepSeek，GLM清言，甚至Steam说出了"Hello"
  - 使用了HelloTools2.0工具调用方案，Trae, CY可以正常使用。
  - 支持的模型：kimi-k2-instruct-0905 、kimi-k2-instruct 好像没有2.6

- ## 🔒 [询问关于 cpa 内自动刷新账号相关内容 - LINUX DO _202605](https://linux.do/t/topic/2111797)
  - 假期五六天没开电脑，电脑处于没关机但是也没联网的状态，cpa 内的 gpt free 账号会不会回去都失效了呢？这个自动刷新的逻辑是什么
- at没失效就没事，我在其它贴里面有说过, at（access_token）或者rt（refresh_token）失效过期这个json就不行了
  - at由rt获得，能保证登录（json能用的就是通过at调用的）
  - rt不是让json失效的原因，但是它能刷新at
- at一般14天左右（不封号情况下）
  - 主要就是不知道你没联网前是放了多久at, 没联网啥也刷新不了
  - rt在at换的时候也会换一遍，理论无过期时间

- 一个auth的rt有10天的有效期，cpa会在第5天刷新。如果你的at没过期确实能用，但是rt过期了，下个周期你就得重新授权。
  - 如果你有一批号刚好是rt刷新了之后第4天23小时59分，你在第0天关机，然后过了5天01分再开机，是有可能失效的

- cpa定时检查auth，哪个到了过期前5天之内，就用rt刷新at。你不关机cpa就会不停按周期刷。

- ## [开源一个工具-CPA-SUB2_CONV（CPA/sub2 json文件转换工具——支持压缩包） - LINUX DO _202605](https://linux.do/t/topic/2190918)
  - 一个轻量的 JSON 转换工具，用来在 CPA (codex) 和 Sub2API 两种账号数据格式之间快速互转。它支持直接粘贴 JSON、上传单个 .json 文件，或者批量上传 .zip 压缩包进行转换，并可按多种规则自定义下载文件名，适合日常账号数据整理、迁移和批量处理。
  - 支持在线使用:http://conv.wangmin.xyz

- ## [我临时修复了HelloGLM（GLM2API）的工具调用问题，现在可以小范围调用工具了 - LINUX DO _202605](https://linux.do/t/topic/2149016)
- 请问和这个 glm2api 有什么区别吗？
  - 同一个项目的不同分支，这个主要是讲究轻快灵活的临时使用，上下文短，但是有工具调用。另外那个是需要你自己获取Token，上下文长，工具用不很齐全

- ## [一键将 OpenAI账户导入到sub2api - LINUX DO _202605](https://linux.do/t/topic/1665581)

- https://github.com/WTFGEDelphia/chatgpt2cpa
  - 把 ChatGPT / Codex session JSON 转成可下载的 CPA auth.json 或 sub2api sub2api-data 的本地工具。

- ## [sub2api, newapi, 9router三个如何选 - LINUX DO _202606](https://linux.do/t/topic/2303966)
- cpa、newapi、sub2api我都用过，cpa适合个人用，分发管理麻烦，newapi是什么功能都有，但是用户体验太差了，菜单做的很复杂（上手后还好），sub2api，用户体验做的最好，菜单是最方便的，模型映射那些都可以，至于大家说的封号，我4个20x的账号都没问题，分发给朋友拼车用，妥妥滴

- axonhub有个比较好用自定义路由

- ## [newapi、sub2api、cpa 有啥区别 - LINUX DO _202605](https://linux.do/t/topic/2153855)
- cpa 能做号池管理，但没有 key 分发机制和统计功能，只适合自用。
  - new api 没法管理号池，但是分发做的好，和 cpa 互补，因此通常配合使用。但是我觉得它 UI 丑丑的，用的不多。
  - sub2api 号池管理和分发 key 都挺不错，UI 也看得顺眼，不过配置起来稍微复杂一点。听说兼容性好像没有 new api 好（常用的 codex 和 cc 这种没啥问题）。

- newapi纯中转，sub2api和cpa支持反代，而sub2api也能中转用，属于即能反代又能中转

- ## [佬友们，0成本开站的方法找到了 -- huggingface spaces - LINUX DO _202605](https://linux.do/t/topic/2139475)
  - duplicate 已有的new api
- 没真人访问就关机。然后很多限制关于使用用途上

- 确实部署在上面一会就封号了，我之前部署过cpa在这里，还没部署就报错

- ## [CPA号多应该轮询还是？ - LINUX DO _202605](https://linux.do/t/topic/2132423)
- 我有很多个free，一直是填充模式，封不封感觉和路由模式没有关系，而且我一直是同一个IP，放心大胆的用吧

- 和这个没关系，和邮箱有关系，该封就封。我一直是轮询，有的号根本没轮询到也会封

- ## [有没有大佬科普下cpa和sub2api的原理和差别 - LINUX DO _202605](https://linux.do/t/topic/2108651)
- 两个我都部署过，CPA才是更轻量那个吧，纯反代，前端都要额外配，没任何权限管理。
  - sub2api更偏企业级，前端页面和权限控制更完善，要用docker compose起PostgreSQL啥的好几个服务

- Cpa性能差劲啊，低配机配置CPA经常内存爆炸

- 佬友可以去https://zread.ai/看看，智谱搞得，对开源项目的分析质量很不错

- ## [[拙见]分享一下高速中转站架构 - LINUX DO _202605](https://linux.do/t/topic/2106032)
  - cloudflare和dnsPod都可以实现类似于cdn的效果 来源于支持一个前缀多个解析 如果用到这个功能的话我建议使用dnspad因为便宜还有短信通知
  - 如果是通过cloudflare和dnsPod实现类似于CDN效果我推荐使用dmit机器CN2GIA+9929+CMIN2…叠加 每个节点最少1-2 最好是2-2
  - 这里给大家提供一种思路, 不建议任何已经在正式运营的佬这样改(对运维能力要求还是有的!!!).
  - 上面方案使用dmit自建类cdn方案 通常也在60s左右
  - 单纯使用独立服务器+号池分离+cloudflare方案在90-300s

# discuss-ai-api-gateway/router-tips
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [中转站真的用得起吗？ - LINUX DO _202607](https://linux.do/t/topic/2518728)
  - 我试过几个中转站，充进去 100 块钱，用 Claude 的模型，基本撑不到两个小时，而且还是比较谨慎地在用。
  - 按这个花销算，如果正常高强度使用，一个月没有三四千块钱估计都下不来。
  - GPT 的中转就更让我想不通了。有这个钱充中转，难道还充不起正版的 GPT Plus 或者 Pro 吗？而且 GPT 基本也不会封号，大多数情况下就是验证一下手机号，正规充值的门槛其实已经很低了。

- 你要是选择中转站，其实可以找找gpt的低价中转，不一定非要磕死在claude

- 我周围有好几个用GPT都被封了，而且申诉还不退款，直接破大防。它是日常用，用量不大，而且没有反代那些。 

- 我知道订阅最合适，但是我①没有稳定的IP，②没有外币卡，③现在各种认证接码等太麻烦，也不太想花费精力去折腾，所以，中转就变得适合我了

- 花钱买中转和自己官网开账号的是不同的人群，需求都不一样. 比如要发票报销，不想折腾网络工具，有的人用AI能给自己创造有形的价值，这时候价格会显的没那么重要。

- gpt的话，4000刀正常按量计费走中转大概在320-640（当然都是有点卡bug的，但是目前都是这些渠道），如果这k12蹬的够快，4000刀走中转站差不多就160块钱

对于超大量的话推荐自己开，8000刀以下我都推荐中转站

claude的max我接触过的对外底价就是0.6:1，站里面富可敌国基本上都是1:1，cc有手法的推荐自己开

- 你有没有发现？越是倍率低，也就是说越是便宜的，贴近官方原价的模型就说明门槛越低，越容易直接从官方获得。常见例子来说，GPT 的倍率就远低于 claude。就是因为它的封号概率也是远低于 claude。所以中转商赚的就是这个过程的钱。只要这里有难度差的存在，就会有利润产生，也自然就会有中转商的存在

- ## [【开源推广】解决在 infinite-canvas 无法直接调用薄荷站的veo3.1做视频生成 - LINUX DO _202606](https://linux.do/t/topic/2324796)
  - 使用薄荷站本身的url请求，在infinite-canvas v0.2.4中

- ## [公司最近和AWS合作，打听了一下Claude的封号政策和降智问题，想要稳定适用的佬友可以参考 - LINUX DO _202605](https://linux.do/t/topic/2269632)
- AWS目前应该是Anthropic最大的股东了，我们合作的部门也属于是2B业务的，我感觉说法还是还是比较可信：
01.        根据AWS同事方面给的信息，Anthropic在2026年4月份坏账超过1.5亿美元，其中约70%来自中文用户或东南亚IP（主要是大量羊毛号）； 1.5亿美元，确实是这么多，我还特意确认了不是人民币，就是美元
02.        根据全球用户使用特征检测到的违规账号中，约90%来自于中文用户或东南亚IP；
03.        Anthropic的老板除了广为流传的入职过百度之外，其实也入职过阿里巴巴美国总部，但是与中方上司闹掰了，还好几次被当着众人阴阳怪气；
04.        作为美国商业公司，必须严格遵守美国政策；
05.        在AI为每个账号建立的模型中，根据用户的会话内容、记忆历史推断明显不是一个正常用户，一般中转站封号都是因为这个；
06.        Anthropic每个月会使用不同的常规智能体进行不同维度的AI自检，以不同的侧重点推理违规账号，对于MAX账号会重点监控，一旦任何账号用量或使用行为异常，会转向更高级的智能体进行分析。
07.        降智原因注意有几个：1、算力使用高峰期降智；2、中文分词器问题；3、判断用户未使用官方账号或几个大渠道的API通道；4、新模型使用了某些国产模型训练并进行灰度测试。

- 给出的稳定使用建议，就5点：
01. IP、电脑时区、操作系统语言尽量使用美区；
02. 不要使用高风险IP，不要多人共用一个IP（短时间内不同ID的会话内容推断不是同一个用户，比如语言习惯，使用环境等等）；
03. 尽量不要使用中文沟通，中文账号重点监控，但是生产的中文产物不算；
04. 开启TUN模式，并且开启全局代理，直接关掉IPv6（疑似中国用户，会使用随机的国内可直连的测试服务器作为探针，加规则也没用，很多普通用户就是这点被封了）；
05. 使用苹果和Google商店付款时，请使用相同IP，并且关闭移动网络，付完款就把APP卸载；
06. 不用使用任何反代工具，除非几个人不在同一时间使用；
07. 推荐使用Kiro，Kiro直接使用AWS组织授权，只要IP稳定就不会封号，某一个号被封了，剩余用量可转移到新号（即将支持），并且支持1M上下文，然后马上就可以支持GPT和Claude所有模型。
08. 使用AWS Bedrock服务登录Claude相关服务。

- 以上检测手段都是今年确认使用过的，并且只是其中一部分容易触发的，实际检测手段在不同时段侧重点都不同。AWS那边给我们的反馈，每个月实际都会在不同时间，使用不同方式巡检，没有太大规律。
  - 实际上只要IP稳定，不要让AI分析出你在中国，也不要用不正常的开号及充值方式（怕黑产连带封号）也是能稳定使用的。

- 下面是我自己的经历：纯中文max，梯子到处飞，和朋友一起用（朋友人在美国），没改区。两月了没封。用中文但严格固定ip，自用pro，封了。感觉看个乐吧，总结的感觉和之前大伙猜测得大差不差但是封号还是到处跑，玄学因素挺大的

- ## ✨ [【开源】做了个中转站模型批量测试工具，解决「不知道哪些模型能用以及支不支持工具调用」的问题 - LINUX DO _202605](https://linux.do/t/topic/2188147)
  - 用了好几个中转站之后，发现一个共同的痛点：就是站里有哪些模型可以用、哪些支持工具调用，完全看不出来，只能一个个试。
- https://github.com/yuanzhi-yw/model-tester
  - https://yuanzhi-yw.github.io/model-tester/

- ## [反代用 CLIProxyAPI 还是 Sub2API ? - LINUX DO _202604](https://linux.do/t/topic/1972760)
- 我记得 sub2api 有粘性会话，cliproxyapi 没有？

- ## [API中转如何让模型联网？ - LINUX DO _202605](https://linux.do/t/topic/2251944)
  - 就是自己在做一些小项目的时候，发现接入的API无法联网，无法搜索网页知识，不知道该如何解决，同样的配置放到codex里能够正常联网使用。不知道有没有佬知道该如何解决？

- 你大概说的是某些模型原生没有 web_search 能力？比如 sub2api 是可以配置给他们增加 Tavily 或者 Brave 搜索来兜底。
- 这个api搜索能力需要看官方支不支持tool调用，tool调用中有没有网络搜索

- 如果模型支持websearch 可以用reponses 透传websearch，不能的话使用自部署的searchxng，或者是api，tavily，exa，grok，brave这些。送的额度也很难用完

- 直接安装groksearch mcp就行，然后grok就使用grok2api自己组号池或者站内公益站

- ## [toolcall-gateway ：让不支持function call的模型支持function call - LINUX DO _202604](https://linux.do/t/topic/1915096)
  - 分享一个从我的web2api项目抽离出来的python库(已发布pypi)：toolcall-gateway 作用：让不支持function call的模型支持function call

- [一个普通的虚拟 tool calling - LINUX DO _202605](https://linux.do/t/topic/2256408)
  - 前几天做了一个qwen2api 的tool bridge(也叫tool bridge), 效果很不理想, 几轮对话, 就卡的没边了, 遂放弃了，今天借鉴一下佬友看看

- [「开源自荐」[AnyToolCall] 去tmd原生工具调用 | 基于提示词注入的工具调用中间件  - LINUX DO _202601](https://linux.do/t/topic/1400154)

- [Toolify——为任意LLM API添加完善的Function Calling支持 - LINUX DO _202507](https://linux.do/t/topic/797373)
# discuss-llm-api-vendor-tricks
- ## 

- ## 

- ## 

- ## 💡 [AI 中转站大起底：什么是中转站，倍率是什么（科普贴） - LINUX DO _202607](https://linux.do/t/topic/2504277)
- 便宜渠道的风险
01. 缓存额外价格
因为你可能现在发了一堆消息给 A 号，然后在下一次对话的时候是 B 号承接。

如果 A 号被封了，就会导致缓存无法继续命中，实际成本提高。

02. 被二次利用
因为他们接入的上游并不是中转自己，可能是别人的号。

别人发现被盗用后，可能会开启截留数据。

甚至这个上游本来就是为了数据做的蜜罐，而你就是被坑骗的用户。

03. 降智
逆向会附带 IDE，也就是程序本身自带的上下文。

这会导致上下文被重复覆盖，最终表现变差。

04. 被替换模型、掺水
因为低价，所以很多人不会认真核验。

掺 Mimo 都算好的。

不过豆包模型很多时候比 OAI 这类渠道还贵，所以一般不会有人掺豆包，会亏钱。

- 
- 

- ## [Sub2API 正在毁了你的 GPT（和中转站）——Codex 降智调查之番外篇 - LINUX DO _202606](https://linux.do/t/topic/2501944)
  - 所有使用 sub2api 且未开启透传（默认不开启）时。也包括大部分中转站。
  - 暂时解决方式：如果你在意这个性能损失，且如果你是自己有账号，建议首选使用 CPA（他在各种情况包括此问题的处理都干净的多）

- 使用cpa也差不多，Hermes如果config里面不设置api_mode: codex_responses也会傻傻的。

- ## [High session usage on GLM Coding Plan with Pi - solution found : r/PiCodingAgent _202606](https://www.reddit.com/r/PiCodingAgent/comments/1uflco3/high_session_usage_on_glm_coding_plan_with_pi/)
  - z.ai coding plan endpoint supports thinking.clear_thinking parameter (ref), which defines how model processes reasoning_content blocks
  - I've double-checked relevant OpenCode code, and it turned out they set explicitlythinking.clear_thinking parameter to false for z.ai provider
  - I've tried applying similar changes to Pi locally and tested it for quite some time - anomalously high session burn rate was gone, so I suppose it was a correct fix
- the similar thing has been happening when i use cursor models in pi. (may be not the exact case)
  - In my case, the token usage metrics (x%/400k) comes back to 0 after every response to my request. And can see in cursor dashboard that for every request, the token usage is way too which means cursor-sdk is not liking the caching extension i have in pi.

- Pi and some of it's extensions have issues with changing the chat history and invalidating the cache (meaning every token has to be recalculated) if you are not careful with your settings.
# discuss-llm-api-gateway/router/proxy
- ## 

- ## 

- ## 

- ## GPT 账号跳手机验证问题整理
- https://x.com/cccchuizi/status/2061705367977906566

OpenAI 最近加强管控，ChatGPT、Codex 等全系账号频繁要求手机号验证，尤其是多账号切换、新设备登录或使用新功能的时候都会跳验证或者二次验证。

老账号用接码平台注册的，容易陷入死循环（收不到原验证码，也换不了绑定）。

用接码平台只能短期用，第二次验证很容易封号，属于饮鸩止渴。

解决方法：

01. 减少验证触发（不用额外手机号）
在网页版登录 ChatGPT → 设置 → 安全 
先绑定 谷歌验证器（Google Authenticator 或类似 App），开启二步验证。
实测一部分账号绑定以后，Codex 登录直接跳过手机号验证。  
进一步：进入高级账户安全，注册通行密钥（Passkey）。
用谷歌密码管理器或 Chrome 浏览器创建。
完成后，邮件和短信验证基本被禁用，适合长期使用。

注意：用干净的浏览器和网络环境操作，先在网页端设置好，再切换到 App 或 Codex。

02. 长期方案
自己准备一张能长期接收短信的真实运营商卡：  
giffgaff（英国号码） ：最受欢迎，月租低，甚至可以 0 月租保号，信任度高。
适合需要长期使用的账号，一个号码一般最多绑定 2-3 个账号。  
其他选择：美国 T-Mobile 实体卡、eSIM 等真实运营商号码。

03. 其他补充
接码平台：仅限测试小号或一次性使用。  
多账号：用不同浏览器容器 + 稳定网络，降低弹二次验证概率。

- ## [10个plus，每周大概能跑多少 - LINUX DO _202604](https://linux.do/t/topic/1980754)
- 5H限额15刀, 周限95刀, 自己计算倍, 反正现在plus纯垃圾了, 没什么额度

- [三天蹬爆了10个gpt plus号，分享一下实际的额度和小问题求助 - LINUX DO _202604](https://linux.do/t/topic/1994112)
  - 自组一个 plus 号池来维持，结果就是三天居然蹬完了 10 个 plus 号
  - 一个号周限 94.4$ = 216.1887M tokens
  - 按照 9 块钱一个号的均价来算的话: ~9.53￥/ 100$ ；~4.16￥/ 100M tokens
- 看好多人说 team 和 plus 额度差不多，但是 team 现在市场价更便宜，为什么不使用 team 呢
  - team 一般需要自带账号，我嫌麻烦所以包括这里也是直接去收的成品号 还有就是，我这样薅基本上就是奔着蹬完周限等封号去的，放 team 有点算炸车了吧
- plus 还是高贵一点呀，team 的周限才 60 出头。一个 plus 是 team 的 1.5 倍了
  - 但是一个team母号能拖5个子号吧。

- gpt工作时间短的问题应该只出现在gpt-5.4, 换到5.3codex就好了

- ## [Does ChatGPT Team Plan Offers Better quota compared to Plus? : r/codex _202603](https://www.reddit.com/r/codex/comments/1rzskhx/does_chatgpt_team_plan_offers_better_quota/)
- Plus and business have the same quotas. Business just gives you free pro uses per month and consolidated billing. 

- [gpt付费选择plus还是team？ - LINUX DO _202604](https://linux.do/t/topic/1939900/21)
- 建议整一个team来用，自从砍了plus额度之后team额度跟plus额度好像是一样的了，一个team母号还能拉多个子号
- 主要是team 0刀绑卡都是死得极快，plus有英区谷歌使用，现在还算稳的
- OpenAI经常搞一些给用户重置额度的活动，最近两次都没team的份儿

- ## [你们都用什么管理模型，想找cc-switch替代品 - LINUX DO _202604](https://linux.do/t/topic/1970428)
- 现在各种渠道我都用metapi整合一下，感觉蛮好用的 
- 有服务器的可以套一个 newapi 或者 sub2api，这样管理也方便，也不用频繁去改配置

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

- [还有其他类似metapi聚合公益站的项目吗 - LINUX DO _202604](https://linux.do/t/topic/1888908)
  - metapi 我只用来签到的，cli用cch，cherry这种chat 用octopus
- 我现在喜欢用 ccload。因为他有个好处，API 调用实时刷新，我一眼就能判断我的龙虾有没有在工作

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
# discuss-llm-api-embedding
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🤔 [求推荐embedding模型资源 - LINUX DO _202606](https://linux.do/t/topic/2326834)
- embedding 和 reranker 都是按量付费的，自己跑两个就好了，有 GPU 最好，没有 GPU，用 CPU 跑也能跑起来，就是慢点

- 自己部署的话, 穷则bge m3 embedding reranker。 富则qwen3 embedding reranker

- 这个最好自建，因为不同版本的向量模型生成的数据空间维度大小是不一致的会导致后续查询数据处理啥的有问题！要保证前后生成的向量数据一致性最好固定用一个模型版本自己部署即可。

- 硅基流动，我现在就在用qwen3系列的embedding和reranker，个人按量非常便宜，vl的不知道有没有上。
  - 另外，embedding不能随便换，每个模型的向量空间不一样，换了就会出现召回问题，reranker可以换

- 硅基的超便宜吧，现在充钱还送10%充值额度

- 这玩意就是把切片初始化到向量数据库的时候消耗最大，后期查询消耗一般。所以按量计费应该也还好。我都是本地跑embedding
- cpu跑embedding模型，那速度简直就是灾难
  - 慢是慢点，倒也到不了灾难的程度，看模型大小, 用 tei 在 cpu 下跑个 “BAAI/bge-m3” 也不是不能忍受

- 公益站的问题就是限并发很厉害，很容易就超限，宁可花点钱走商业站，反正跟对话比花不了几个钱
# discuss-llm-api-paid-cn
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 💰 [为什么中转都喜欢1¥ = 1$ - LINUX DO _202607](https://linux.do/t/topic/2519401)
- 计算方便, 不然充值倍率加模型倍率
- 只需要看倍率就知道1元钱有多少Mtoken，方便对比和计算使用量

- 方便计算呀。又不是真实的钱，鬼管你真多多少呢。只要倍率设置好。那没区别的。

- ## [盘点目前可用的GLM-5.2渠道 - LINUX DO _202606](https://linux.do/t/topic/2458733)
  - 省流：付费订阅 OpenCode Go 综合最佳；免费尝鲜可以选官方 ZCode 或 阿里云百炼。

- devin(原来的windsurf)pro订阅可以免费用到7月5号，缺点是上下文只有200k

- 火山拉完了、lite用量少、工作台想看个额度还老掉线、然后也没有详细的用量统计、当然9.9体验一下还是可以的
- 而且还巨卡，除了他家的弱智豆包其他的模型几乎不可用，简直拉完了。 买过一次之后再也不碰，成功避雷
- 实则并非，用他自家豆包也会被路由到神秘模型

- ## [GLM lite套餐和OpenCode go套餐的用量区别 - 搞七捻三 - LINUX DO _202606](https://linux.do/t/topic/2444138)
- GLM Pro、Lite套餐额度( 有佬友说Lite月限非高峰期90M，高峰30M，Pro官网标注5x Lite(但是貌似没有5倍) )
  - 根据信息简单估算：3个Go基本平替GLM Pro，价格每月 [35+5(google账号)] * 3 = 120 元 < GLM Pro(149元/月)
  - 缺点是每月需要折腾新号5刀，优点是没有高峰期倍数

- opencodego多开的话一个支付宝账号可以吗
  - 我付了3个，应该可以
- 用支付宝付呀，得用外币卡。我之前试了支付宝显示40，外币卡33，一个号的go就差7元呢
- 没有吧，我用支付宝是 35r，跟外币卡没啥区别

- ## [GLM coding plan pro用量 - LINUX DO _202606](https://linux.do/t/topic/2404260/13)
- 5小时高峰期大概2000Wtoken，平峰期大概6000Wtoken。一直高峰期使用，一周大概1亿，一直平峰期一周大概3亿。
- 一天100M pro肯定不够用，pro周限量大概是150M左右

- 5小时上午用绝对超10m的，下午不行。

- [GLM coding plan的pro版本够用吗 - LINUX DO _202606](https://linux.do/t/topic/2397814/6)
- 一个人基本够用，用满周限大概是2亿token。非高峰

- 你如果一直避开高峰期使用 基本是够的，月pro套餐大概是15亿左右把, 尽量上max, 可以不用心疼猛蹬，不过大概率抢不到

- ## [有一说一，智谱的官方套餐完全没有性价比了吧 - LINUX DO _202606](https://linux.do/t/topic/2405897)
  - 以我订阅的MAX举例，我大概非高峰期用了2亿左右的token，就用掉了周限的百分之19。估算一下一周非高峰期也就10亿token。这是469块钱。
  - 然后这么贵的价格下，在今天工作日10点开始，就处于不太可用的状态了
  - 我没想到能快到这种地步。缓存命中好像完全没用。用多少就消耗多少。搞得我都不敢在2点之后用了
  - 对比一下1200一个月的GPTPRO20x。智谱这个套餐完全不划算了吧。而且这套餐还不是想买就买的，要抢购的。甚至还要加钱上闲鱼的

- 订阅怎么都比直接用API划算，至于各家厂商的订阅互相比较，这个变量太多，也控制不好，只能自己亲自用，体感上感受，然后看划不划算了。
# discuss-中转站
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [别只看0.01倍率，中转站计费的几个常见猫腻 - LINUX DO](https://linux.do/t/topic/2572618)
- 常见的几个地方：

充值比例
有些站是7元人民币兑换1美元额度，有些是充值1元送10个额度。站内余额只是商家定义的数字，充值后显示得多，不代表真的便宜。

输入、输出单价
以GPT-5.5、GPT-5.6 Sol为例，标准短上下文价格大致是：

输入：5美元/百万Token
缓存：0.5美元/百万Token
输出：30美元/百万Token
有些站充值送得很多，却把模型单价调高。看起来倍率很低，实际上Token一点都不耐烧。

缓存命中率
Codex这类长会话场景，缓存通常会占输入的大头，正常使用一段时间达到90%左右并不奇怪。

如果相同模型、相同客户端、相同任务，在某个站的缓存率明显低很多，就需要注意。不过不能只看一两次请求，要跑一段时间再判断。

缓存价格
正常情况下，缓存价格只有普通输入的10%左右。

但有些站把缓存也按照普通输入价格计费，相当于把缓存价格提高了10倍。即使页面显示 0.01 倍率，实际效果也可能接近 0.05，甚至更高。

分组倍率
也就是最容易看到的 ×0.01、×0.02、×0.1。但它必须结合充值比例、模型单价和缓存计费一起看，单看这个数字没有意义。

- 按Token计算更适合快速对比；按请求次数误差会更大，因为每次请求的长度不同。
  - 总之，不要只问这个站显示多少倍，而要看：实际支付1元人民币，到底能跑多少Token。
  - 这个结果，才是把充值比例、模型价格、缓存计价和分组倍率全部算进去之后的真实综合成本。

- ## [【帅API】公布帅API目前全部收益，以及运营方式 - LINUX DO _202607](https://linux.do/t/topic/2563086)
- 我们的号池组成主要由
  bug team（目前全网拉闸）
  首月免费plus（目前基本拉闸）
  黑冲号（基本拉闸）
  pro正价号（没限制破限一直死）
  kiro号（kiro池里面）
  ccmax号（纯小黑开号，封了就当地银行介入退款）
  一些我们确认过技术手段，并且验证过号池的上游

- 目前营业实际收入
几乎为0而且倒贴

主要原因是5.6没出之前，我们依仗着自己开的bugteam，几乎0成本的为所有用户提供token，但是因为现在的bugteam是正价开通母号，所以美元还是花了点，成本倍率约为0.016

我们日常卖0.07，但是实际上在群内提供0.01-0.00001的价格

在后面bugteam的成本提高，倍率约为0.03，但是实际上在群内依旧是0.01-0.00001的价格，短暂的提高到了0.03

在5.6模型出来的当天，我们就上线了，但是没上线动态收费，我们最贵的pro分组0.17，实际价格跟0.1倍率差不多，因为没分档，这天亏损非常的严重，bugteam因为缩水，5.6模型只能跑大概100+刀
同时一整天都保持0.03的低价价格，但是不太敢发在站内，因为这几天遭到的攻击也很多

成本上，除了账号成本还有
富可敌国月充值4200元
服务器是OVH的独服 一个月2100元左右
网络是cf的网络（买了240刀年费会员），以及cnm的cdn亚太加速，部分支付接口是edgeone防护

- 在上线后遭遇了邮件接口攻击，注册充值批量扫5.4mini攻击，支付接口ddos攻击，自建邮箱接口攻击等

- 点进来的时候我预想你的实际盈亏是保底亏 3000. 甚至服务器费用占亏本大头.
  - 实际上账号成本是大头，后面两天日均3000+账号获取了，我们自己搓不出来，全网买，价格从4一路到15了
  - 两个人，三班倒，我已经好几天没睡超过5小时了 

- claude号池因为前段时间不是主要运营目标，我们容灾做的不足，最近会加强 

- 之前有想过搞中转，后来发现其实没想象的好赚，太卷了，主要最烦的还是没有稳定的货源渠道，得每天去烦怎么搞新的低价渠道，封号得一直补号，感觉累死了。

- 一直想用，就是发票门槛高了点，怕用不到1k没法开票得自费了。申请降低一些，有手续费也行呀
# discuss-llm-api-paid
- accounts
  - 带at/rt的帐号价格不同，在不同的封控政策下，可使用时间差异很大，最好选择 RT(可长期) + 可刷新AT(手动刷新来解决401问题)
  - 不用纠结，就用量大管饱的gpt, $20刀的套餐，opencode-go提供 ¥60 x2(2个套餐), 但gpt-plus 提供 $120 x4(4个周限)

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [佬有谁知道 super grok 的额度是多少，super grok heavy 的额度又是多少呀 - LINUX DO](https://linux.do/t/topic/2565065)
  - 搞了一个 super grok 的七天试用，api 请求才 25 刀、三千万 token 这样就到了周限了

- ## [我宣布grok 4.5王朝了 - LINUX DO _202607](https://linux.do/t/topic/2554427)
  - 现在7天试用号也就两块一个，用完即抛，额度也体感上挺多的

- ## [LDC悬赏Kiro反代处理缓存 - LINUX DO _202607](https://linux.do/t/topic/2517656/12)
  - 求助大佬能够帮我二开kiro-go或者kiro-rs反代 处理缓存的问题

- 确实现在反代可能都对cache支持不太好，所以反代出来，quota消耗的比直接在kiro里快很多很多

- kiro的反代缓存问题基本无解，现有的很多站点都是拿kiro打窝，看起来便宜，实际上因为缓存每次重建，价格反而很高

- 这个缓存不是LLM返回的缓存数据，是中转自己算的，本质上还是降低价格，不如字面上直接降价格好了。服务器还少算一点。kiro ide都没有缓存回来，这种假缓存，有啥意思

- claude的kiro渠道反代的成本目前也比gpt高，现在k12、bugteam都还活着，如果没到彻底没token，我想我应该不会做kiro

- ## opencode: GLM 5.2 is ranking the highest on cost per session and everyone is raving(狂热赞扬, 极力夸奖) about this model
- https://x.com/opencode/status/2071830563317584346
  - which means if cost/session is high it might actually be a sign that the model is useful

- cost per session is really measuring verbosity × price. GLM 5.2 at $2.31/session might just pad its reasoning. a terse model that's right in 500 tokens doesn't score here — not because it's worse.
- Careful, high cost per session isn't a usefulness signal, it's a token count. GLM-5.2 sits at 4.9M tokens a session. That could mean people trust it with the hardest jobs, or that it's just chattier and less efficient. Same number, opposite conclusions. Cost measures usage, not value.

- ## [GLM5.2又有便宜的渠道了 - LINUX DO _202606](https://linux.do/t/topic/2499029)
  - 之前我们都知道可以在opencode go和commandcode订阅5美元和1美元去使用glm5.2，现在cline的也来了

- glm官方不能用，再聪明也不行，他的可用性甚至没有any能用的时间多
- 不存在封号，除非是几个人蹬一个套餐，不然不可能封号的，但429和慢这个问题，一时半会不可能解决了

- glm官方api的是fp8的, 很多第三方都是一致的
- 智谱自己部署的都是FP8，第三方大部分也是FP8，这个精度相比全量其实性能损失极小。

- 这个到底有多少额度也没说清楚，opencode go是明确说了月限额60刀的
- 这个20块包50刀, go是35块包60刀, 不过模型价格和go一样, 这个套餐也是用ds最划算

- opencode和官方的区别有的，特别是高峰期，我怀疑opencode在高峰期时会路由到一个更加量化的模型，昨天测了一下，同样的提示词，用opencode的api做出来是错的，清掉代码换官方的api一遍过，现在是三持渠道了，公司的自部署一到高峰期首字几十分钟都有 只能换着蹬了

- 直接接到cc里面缓存命中咋样，和opencode一样吗
  - 感觉差不多吧，opencode每次请求花费$0.7左右，cline也大概这个数
- api接入到cc switch里面显示的缓存也太低了吧。。。

- 银联信用卡就能买。刚在cc-switch里配置好了，跟opencode go一样需要开路由转换才能在claude code里用。

- ## [半夜和plati的opencode商家聊了聊 - LINUX DO _202606](https://linux.do/t/topic/2491652)
  - ladykiller这个商家之前看佬友说存在一号多卖的情况，当时我刚买了一个（不过是stripe代付），还在纳闷怎么能做到这一点的，恰好最近glm5.2用量很大又急需大量opencode订阅，最终还是没忍住又买了几个。
  - 卖家没法在L站上回复，在这顺手当个传话筒, 一号多卖可以联系卖家换号。不过还是希望大家保持独立思考，这里只做一个消息转达。如果一定贪便宜的话那就最好还是走代付，自己准备邮箱吧。

- 我找的另一个mike什么的，我直接让他交付的邮箱，目前没发现有人公用情况，也做个参考

- ## [Cursor Pro (20 刀) composer+auto 额度参考 - LINUX DO _202606](https://linux.do/t/topic/2480590)
  - 看这样子纯composer2.5 的话大概在 7 亿的token 额度左右, 其实还是蛮够用的
  - composer2.5的 fast 感觉没必要开, 普通模式感觉就挺快的了, 贵了好几倍, 感觉不值当

- cursor 就是一个月总额度, 没有小时和周限额之说
  - gpt plus是走 5 小时限额和周限额
- cursor的全部都是月用量

- composer 2.5 不带 faster是怎么搞出来的？ 我一直faster的， 只能蹬个3亿左右
  - 入口是有点隐蔽, 不过配置都在 edit 这, 包括其他模型的 think 程度也是同样的入口

- 基于 kimi 后训练的, 基础任务开发体感是很不错的
  - 不过在做 agent 任务, 比如调 agent 的 skill 时, 我是遇到了它很爱枚举式解决问题, 改起 skill 不能符合我的预期
  - 其他任务感觉还是挺给力的, 我现在都是 gpt5.5 策划, 然后用 composer2.5 做实施这样就是

- ## [3X usage for Gemini models for all AI Plus, Pro, and Ultra users. Forever. : r/google_antigravity _202605](https://www.reddit.com/r/google_antigravity/comments/1tjbd1e/3x_usage_for_gemini_models_for_all_ai_plus_pro/)
- I hope they've fixed the high token usage too! because there's no point in resetting if one prompt would eat up %40 of the daily limit!

- When there's no fixed base, doubling is just a mathematical game.

- ## [兄弟们晚上这种红账单的cursor pro怎么卡的呢？ - LINUX DO _202604](https://linux.do/t/topic/2021819)
  - pro没到期 还有25天 主要我想知道这种红单的号怎么卡的 我感觉这种号是白嫖出来的

- 看起来是0云购漏洞，账单都是打开状态，没有支付，该不会是美国银行支付吧。

- ## [有大佬知道怎么速刷cursor pro吗 - LINUX DO _202605](https://linux.do/t/topic/2188946)
- 公开了号商不得饿死 

- 我觉得有可能是信用卡盗刷， 或者卡不为人知的支付bug
  - 就比如之前公开的刷ultra那样，但很快被封了，刷pro我看已经活了很久了

- [佬们cursor pro一天卡，25值得买吗 - LINUX DO _202606](https://linux.do/t/topic/2389291)
- 其实cursor pro速刷号性价比还算不错的，因为cursor pro速刷，也不会说续费之类的了
  - 一个号，高级模型的API等价额度是40刀左右（20刀内置+20刀的超额，偶尔超额可以到30-40刀，不过我没遇到过）
  - 也就是假设40rmb，能用40usd的API，而且至少保真，这比某些不保真的中转还要划算一点
  - 当然，你要确保卖家给你的是账号登录，不是什么插件之类的，那个有掺假可能

- 海鲜市场到处都是，速刷号，你搜一下呢
- 卖家说红账单是啥意思啊
  - 开账单没支付 一般3-5天挂速刷号
- 确认独享一般速刷没问题 但是红账单开不了超刷只能用45刀内正常用 取决于号之前有没有开超刷开了多刷20刀左右

- 那还不如Kiro月末倒数第二天0元买Kiro power呢，10000积分几乎就是Opus 4.8无限用

- 现在贵了，而且好多人都不卖了，也不知道为啥，用claude模型也就一上午吧

- ## [cursor auto夯爆了 - LINUX DO _202606](https://linux.do/t/topic/2475401)
  - 纯auto, 没有高级模型，海鲜市场一个月16.8。无限auto.
  - 1.5一天，无限auto, 其实就是free不停的换号，直连官方不降智。

- 我也买过这个，但是体验很差劲呐，问一个问题就要换一个号，有点折腾

- 感觉改一些简单东西还好，复杂bug改几轮都没改对地方
- 有明确的目标，方案还是很好用的。当纯牛马效果杠杠的。一天2块，香爆了。

- 海鲜市场的吗？咱们搞不能注册free的号吗？
  - free号额度很少的，你有注册机的话另说。主要是不贵没必要折腾。

- 还有老的教育优惠无限auto, 今天感觉确实香

- 我也用了一天了，估计咱俩用的同一个工具，我也是海鲜市场淘的16.8r一个月，比gpt5.5快，而且智商还行，干一些小活真的很棒
- 我个人用下来的感受就是，简单的 curd 这些工作完全可以交给它来完成了。另外你如果足够多的技能和 rules调教的可以，我感觉是比 人纯手写快，因为重复性简单的工作 是占据多数的，极少数疑难杂症可以 人介入 结合也能解决了。高级模型我基本不咋用了 除非快过期了。主要是要切换网络。很麻烦。绝大数时间 auto 是足够用的。

- [我想知道那种2元的cursor auto额度的pro号是在哪里买的，小黄鱼上也没有哇 - LINUX DO _202606](https://linux.do/t/topic/2365558)
- 站里面就有啊，哈雷佬就做出来一个这样的插件

- ## [如今性价比最高的模型或许是composer-2.5-fast？ - LINUX DO _202606](https://linux.do/t/topic/2395679/43)
  - 首先已知super grok 印度区价格为50人民币三个月，其次composer2.5-fast价格为 input $0.5
  - super grok每月额度为150刀，换算下来

- composer2.5-fast的道德感如何，能不能用来破限啊
  - 不能破限，完完全全就是cursor的模型
- 别说破限了日常对话都困难，没有系统提示词的情况下发个你好会显示
- 我用来逆向本地的vscode插件，做作业写考试都是没问题的，道德比gpt和claude低很多

- composer2.5好模型，日常用确实很舒服，其实cursor这边也还行，几块钱买个号能用好多
- 什么叫几块钱买个号能用好多，Cursor Free 的 Composer 2.5 额度很多吗 
  - 指的是 pro 刷完剩 auto 的号吧, free 额度很少
- 现在没了，之前有那种用完高级模型额度的pro号，几块钱composer能用一两百刀，不知道为啥现在买不到了
- 现在闲鱼还能找到，不过比起以前涨价到十块多了

- 感觉一个supergrok根本不够用，老马咋不开放composer 2.5非fast的

- 用的curosr 60刀跑非fast，速度也没差多少，跑了10亿token了，还剩好多额度。grok也能用非fast绝对爽翻

- ## [cursor高级模型已用完，auto和composer，可用额度还不少 - LINUX DO _202606](https://linux.do/t/topic/2413248)
- 是的，auto和composer是能用，使用起来auto偶尔会很聪明
- 聊胜于无吧，简单点的任务还是可以的

- 只有去年9月分前开的才有这个优惠， 等到期了也就没了 auto 也开始算量了， 我是在他们改收费政策前充值的

- [如何高性价比使用 cursor3 - 开发调优 - LINUX DO _202605](https://linux.do/t/topic/2258778/9)
- cursor官网说是auto和composer是单独的用量池
  - 但是我实测一直用composer2.5用到45刀左右就和其他模型一样用不了只能用auto啊？感觉和它说的逻辑不太一样呢 只有auto有额外的用量池
- 是的，我体验下来，发现api是单独有20$的额度，和auto+composer分开。我有一天不知道怎么开启了composer的fast模式，累计计费刀五六十刀了，但还能用composer2.5

- ## [大善人马斯克给 Grok build 上了 Composer 2.5 - LINUX DO _202606](https://linux.do/t/topic/2289594/13)
- Grok 是月限额，Groq heavy 订阅月额度可能比 GPT 5x pro 的周额度还低
  - heavy现在不少，原本是600刀，现在改成了1600刀，cpa里能看到
- 不要忘记heavy是一个月三百刀的逆天价格

- 30刀的 SuperGrok 月限额是 150 刀

- x premium的grok build额度是$40。都是套餐费用的5倍

- ## [想问下是购买cursor教育版一年呢，还是购买cursor按月半价付的pro呢？ - LINUX DO _202606](https://linux.do/t/topic/2451597)
- 半价会员至少是官方渠道，封号的概率应该会低很多。教育版的话就不太清楚了。

- 教育版会二次验证, 如果要买, 至少要商家质保一段时间, 比如一个月之类的, 要不然很亏的.

- 个人建议先按月半价付pro，理由有几个：一是官方渠道稳，不用担心二次验证翻车；二是看你用量不算特别大，月付灵活，随时可以停；三是教育版200多一年虽然便宜，但闲鱼买的被回收风险确实存在，万一用一个月封了反而不划算。半价pro算下来一个月也就$10，先体验再说。

- 买半价的成品号，这样可以超额使用。月抛半月抛也没负担，教育版的也不敢超额用，而且感觉随时会封号，提心吊胆的，用着也不爽。

- 以前买过两个教育版一年的，基本都是三个月掉线，店铺关门。

- ## [Deepseek V4 Pro 目前最便宜的渠道 1刀3亿token - LINUX DO _202606](https://linux.do/t/topic/2461029)
  - Commandcode Go Plan(1刀), 订阅需要缴纳0.36刀的手续费
  - 获得完整官网价格10刀的API额度、约66%的OPCodeGo的月限，限制使用提供的CLI，可通过反代用于别处。不限制邮箱，可多账号购买多个，1个3亿tokens，买5个就是15亿tokens了。
- 还有，这个是需要信用卡买，不是很方便，要是支持pp或者支付宝就方便点

- 用了0.2刀，然后号直接就被扬了
  - 不过好在退款了
  - 没反代，就正常在他的官网cli用的
- 我1周前开始反代，用到现在10刀用7.5了还活着，没想到是侥幸吗
  - 我接到openclaw里用的哈哈，没做什么复杂的事情，不过体感蛮聪明的。 反代再接newapi，5天用了 144M token，缓存命中率91.3 %，平均响应速率 3675ms， 官网看用了166m token（一开始没接到newapi里用），7.1刀额度，我感觉还不错

- 需要反代，而且他们的接口很奇怪，还要传一个什么taste的参数，感觉会降低智商
- 1刀 go plan只能反代，15刀起的套餐可以用openai/anthropic api

- 所以是opencode go是v4flash最便宜，command go是v4 pro最便宜？不过这个command go要额外交零点几美元的手续费

- ocg感觉现在的免费额度被砍了，挺少的
  - 换个ip就行

- ## 📌 [Opencode Go 套餐额度分析(GLM、Deepseek对比官网) - LINUX DO _202606](https://linux.do/t/topic/2424234)
  - 按95%的缓存率估算可用Tokens
  - glm 5.2 - 167M
  - kimi 2.7 - 226M
  - mimo 2.5 - 4863M
  - minimax m3 - 721M
  - qwen-3.7 - 818M
  - ds-falsh - 4863M
  - ds-pro   - 446M
  - 由于Deepseek的缓存太便宜，随着缓存率提高，可用Token就会成倍的翻。相对而言，GLM的缓存价格是正常的，因此没有DS的巨额增长
- 最特殊的就是ds4pro了，因为官网降价而go没跟进。也就是说其它都是5刀买60刀，而v4pro是5刀买15刀，虽然没那么值，但总归还是值的。
- 确实是，尤其是考虑，GO还有DS4 Flash/Mimo V2.5几乎无限的额度

- GLM Pro、Lite套餐额度(有佬友说Lite月限非高峰期90M，高峰30M，Pro官网标注5x Lite)
  - 根据信息简单估算：3个Go基本平替GLM Pro，价格每月 [35+5(google账号)] * 3 = 120 元 < GLM Pro(149元/月)
  - 缺点是每月需要折腾新号5刀，优点是没有高峰期倍数

- pro 的話, 就是5刀價格(首月) / 10刀價格 買60刀的額度, 外加一些免費模型, 
  - 其實單看額度, 其實比起其他coding 套餐, go 是完全沒有性價比的, gpt plus 20刀但月限起碼有500-600刀
  - 好處是有免費的模型用, 加上可以多模型組合用

- 我看我自己的D老师官网用量，真要用一用一天就是两三个亿，按目前的缓存水平，也得0.1元/1M，一天也跑二三十块，有点难绷。

- 我们订购的智谱codingplan团队版，目前用了几天，算下来，一周520M左右，一个月算下来，1200块钱/2080，约0.58/M
  - ocg纯算glm5.2的话，70块钱150M，约0.47/M
  - 但是智谱团队版现在是2个席位起购，而且经常429，普通的也抢不到。
- 其实谷歌账号没多难搞，5元一个，算上去就是33+5=38，开三个(114元)就是GLM Pro(5xLite 149元)了
  - 普通的抢不到，可以试着多开一点5刀的opencode go就行了，邀请还多送5刀

- 性价比最高的是应该是DeepSeek v4pro吧，flash这种小模型到处都有免费，不需要花钱，minimax m3给的额度多，但能力属实也不大行，不过我没用qwen3.7，不知道这个能力如何，它额度比d4p还多一点

- 我一周用了112M的Flash，和177M的Pro，才把周限用完，月限50%，怎么可能单用200M的Flash就23%

- ## [有关 Ollama Cloud Pro 的情况分享 - LINUX DO _202606](https://linux.do/t/topic/2442235)
  - 目前 Ollama Cloud 上的 GLM-5.2 是很快的，再经过我自己的一层中转（美西服务器，回程优化）+一层本地代理后，今天下午的TTFT为5.86s，平均TPS达到了103.4
  - 类型	总Token	未缓存输入+输出	预估金额
  - 5h限额	14M	0.5M	$4.5
  - 周限	78M	2.5M~3M	$25~$30
  - Ollama的优势在于无需抢购、无使用场景限制、可选用多种模型、速度快，如果只是为了在编程场景中使用GLM-5.2，其实并不推荐（因为量太少了，不如官方国内站和OCG）。想要够用的话，必须搭配别的模型（比如消耗同样的限额，DSv4Pro能产出两倍以上的Token）或者购买100刀的Max订阅。

- Ollama Pro 20刀/Max 100刀（Max=5倍Pro限额）
- ollama这俩月削了很多额度了 以前量很大的 现在不行了
- 可能你近期没用过Ollama，现在Ollama的5h额度不到半小时就能用尽

- OCG每月限额60刀，少于Ollama，但是其首月订阅价格只需要5刀，算一下比例的话，是比Ollama更具性价比的
  - 相比起OCG，Ollama胜在高速。此外OCG的供应商是不确定的，而且传闻是FP4量化的模型（指DeepInfra；z.ai这种官方供应的目前是fp8）；而Ollama可以确定至少是FP8的

- opencode不够用，只用 glm5.2，opencode 的月额度仅能支持 1 天 10 小时或 2 天的使用

- ## [GLM 5.2 Cost: Opencode Go vs Neuralwatt : r/opencode _202606](https://www.reddit.com/r/opencode/comments/1ub1nvy/glm_52_cost_opencode_go_vs_neuralwatt/)
  - The $20/mo plan gives you 6kWh/mo, which is a 33% discount from PAYG. They offer a trial with $1 free credit, and an additional $4 if you add a payment method, giving you $5 to test out the service.
  - I've been testing GLM 5.2 usage at Neuralwatt with their energy based pricing.
  - Input Cache MISS = 1.9M Input Cache HIT = 17.9M (90%) Output = 0.16M Total Energy Consumed was 0.51 kWh, at a cost of $2.53
  - So how does this compare to OC-go? 1.9M input x $1.4 = $2.66 17.9 cache x $0.26 = $4.65 0.16M output x $4.4 = $0.70 Total Cost = $8.01
  - On the surface this looks like NW is far cheaper, but GO gives you $60 of usage for $10. So $8.01 / 6 = $1.34 in actual money spent.
  - If we use NW sub pricing, with the 33% discount the $2.53 would have cost $1.68. The higher subs offer better discounts, but even the pro $100/mo plan would have meant $1.55 for the 0.51kWh used.
  - Conclusion: NW's energy based pricing is novel, and is a very good deal, but GO is still the better deal. I may continue to use NW as a backup provider though.

- Yes, OC Go is a slightly better deal but the difference is you only have a $60 limit per month, once you hit that limit you can't do anything else. Meanwhile with NW you can just keep going forever since it's just API costs
  - Just create a 2nd workspace in your account and add a 2nd sub. Boom, another $60 to use.

- Huh, for me I got a lot better pricing with nueral watt. I generally get 10-15x of API price while go is 6x. 100 million tokens mostly of GLM for $3. I wonder if the cache made the big difference for you?

- NW is also known to use quantized models. So dumber
  - No, they don’t. The quants are on the model cards and they are accurate. They are very transparent on discord as well. They are running Zai’s fp8 just like most providers — including Zai.
  - Hell, not long ago they shutdown an openly discussed nvfp4 test on old 5.1 because they detected a subtle degradation edge case that didn’t meet their standards for it. And opened a bug issue with the upstream library to address it.

- ## [Neuralwatt - What is the most cost-effective API model that matches DeepSeek V4 Pro or MiniMax M3 in terms of strength and pricing. : r/opencodeCLI _202606](https://www.reddit.com/r/opencodeCLI/comments/1ubt6it/neuralwatt_what_is_the_most_costeffective_api/)
- Use GLM 5.2 short, it has 200k context, Enoght for 99 percent work, and is 3x inexpensive than GLM 5.2 with 1 M context, don't use GLM 5.2 short fast as it is a non reasoning model. Short gives 5-7 times token usd value, so kinda in opencode go category. But speed wise Neuralwatt is better, but it has fp8 (99 percent accuracy to fp16/native). Btw 10 Usd new plan at Neuralwatt will give 25 USD after 3 days. So, Neuralwatt with new account is technically ~ 2.5 x 6 = 15 times api value and Opencode go with new account is 2 x 6 = 12 times. Speed is better at Neuralwatt, accuracy maybe at Opencode go (not sure).
- The main variants to consider are “fast”, which have thinking disabled but are cheaper and faster, and “short” on GLM which has a 200k context window instead of the full 1M and is also cheaper. There is a short-fast as well I believe.

- 5.2 is expensive the 397b might be the best cheap bet short term
  - It apears 397B is weaker than deepseek v4 flash, on top of that v4 flash is free in opencode zen.

- ## [I burned through 19M tokens of GLM-5.2 for under $3 today : r/opencodeCLI _202606](https://www.reddit.com/r/opencodeCLI/comments/1u8l3qb/i_burned_through_19m_tokens_of_glm52_for_under_3/)
  - Based on OpenRouter pricing, this would've cost me ~$8.
  - Neuralwatt runs GLM-5.2 at FP8 precision 

- for GLM 5.1, in 30 days (with a bit of trying kimi and qwen) really, neuralwatt is amazingly cheap

- i just bought their $20/month subscription today and i can say yes the speeds are usually pretty good, although at times there were some latency issues for me at least

- If this is the good price, then I'm screwed when my zai legacy plan runs out. I'm using 340M tokens a week on the lite plan.

- for glm-5.2, Neuralwatt is still about 7 times cheaper vs standard inference provider zai.

- OpenCode Go + Neuralwatt is exactly the "stack" I use for my models, and I'm really happy with it! Can recommend!

- Codex 20x offers like 15B tokens per month of 5.5... that would be $2K+ for neuralwatt's glm. 

- Still not worth it. I spent 4.2B tokens with me Claude code 5x for 100 usd within the last month. This would cost me 595 dollars with glm. So… what is the point of paying for glm? I can’t get it anymore since they’ve risen their prices
  - The point is that you can spend way less than $100 and get a model that's good enough for your needs.

- [neuralwatt is suprisingly good. : r/opencodeCLI _202606](https://www.reddit.com/r/opencodeCLI/comments/1uaq80m/neuralwatt_is_suprisingly_good/)
- Either I'm doing something wrong, or this is a bit overhyped. 3m tokens with GLM 5.2 cost me $1.61 with 0.32 kWh energy consumed. Have it on the energy based billing.
  - Same, I saw someone used 19M tokens for GLM 5.2 and was charged $2.74 yet I tried it on my own and got charged for $1.15 for 627.9K tokens.

- ## [Neuralwatt has been a surprisingly good cheap pair with Opencode Go for agentic workflows : r/opencodeCLI _202605](https://www.reddit.com/r/opencodeCLI/comments/1tcq264/neuralwatt_has_been_a_surprisingly_good_cheap/)
  - some the models are FP8 quantized, but honestly FP8 has been pretty decent from my experience. I barely notice much quality difference for most coding/agent tasks compared to full precision stuff.
  - Token usage equivalent: around $23.21 ; What I actually paid: $2.56
  - I’ve already used around 33 million tokens on GLM 5.1 and it only consumed about 0.3897 kWh, which honestly surprised me.

- I just signed up and I’m getting very good rates (but weekends are typically good for every provider) and price. Over 100 TPS and $0.045 per Mtok on GLM-5.1-FP8. Way better than anyone else I can find right now.
  - Wafer and Crof both abandoned their request based subscription plans this week so a lot of their former users are now looking for better rates. I’m in search of a replacement for GLM-5.1 personally. Some Kimi 2.6 as well.

- Neuralwatt paygo is quite nice I've used 90mil tokens so far with GLM-5.1 and it costing me only $4.78. But I reckon if you are going to use it really intense the subscription for $20 you get 6 kWh is very reasonable too. Even me with 1200 GLM 5.1 request only costed me 0.9 kWh, but the Kimi-2.6 might be kinda expensive 129 request and its 0.12 kWh.

- ## [感觉opencode的go套餐很便宜 - LINUX DO _202606](https://linux.do/t/topic/2321251)
  - 5刀变60的12倍，对比kimi199才能拥有13倍，这个起售价对于小用量的国产模型很舒服了

- 35块钱的kimi2.6我记得大概3亿左右。kimi199的那个套餐我记得一周就是3亿多。而且还送个云端龙虾啥的，说实话go用GLM5.1和kimi2.6都很亏。最爽的还是用mimo和DeepSeek

- 很划算，正常是12X也就是5美元当60美元用、Deepseek之前有佬算过因为不是按优惠价算的最终是2-3X差不多5美元当15美元用，当国模备用很香
- v4pro新的价格2.5折大概是原价的4倍额度，5刀当20刀用。 go的计费是12倍额度，60刀， 如果go用的是pro原价计费的话go大概是v4pro官方额度的3倍量

- opencode go的套餐说明页是有说明隐私保护的。 其次官方说过前期是靠贴钱换用户量，再用用户量去和供应商谈折扣的。 企业大使用量的供应价格和我们看到公开的小额计费也是不一样的。
  - opencode go智力高的模型的性价比没有那么高：像dsv4 pro按计费首月5刀能用官方api计费大概15刀的量，只有3倍。
  - opencode go的优惠期肯定是有限的，到一定规模后取消优惠肯定得按10刀正价去看。

- 肯定是会卖数据的，仔细看zen套餐下面写着保护隐私xxxxx，但是go没有写，表明了go的套餐是要吃数据回扣的，卖给大公司之类的，基本不会亏

- Kimi 的有 Kimi 的专用金融数据库

- ## [求一个能爽用deepseek v4 pro的渠道 - LINUX DO _202606](https://linux.do/t/topic/2347970)
- commandcode，1.34刀可以买10刀的额度，多注册几个账号，ds基本可以爽用

- ## [佬们有没有量大管饱还好抢的 token/coding plan 可以推荐一下啊 - LINUX DO _202606](https://linux.do/t/topic/2428139)
- 35块差不多可以蹬100 v4 pro, flash 可以蹬400左右

- 5刀只有首月吧，后续得10刀了，
  - 取消订阅 然后 再次订阅我这 一直显示5刀 用三个月了
- 已经无了, 我之前就是这样, 这周一重新订阅显示10刀了, 直接换了个号

- ## [My Honest Command Code Review After Few Days of Daily Use : r/opencodeCLI _202606](https://www.reddit.com/r/opencodeCLI/comments/1u0vi9b/my_honest_command_code_review_after_few_days_of/)
- Opencode go 10$ plan gives 60$ usage but doesn't give deepseek v4 discount. So, except other models, if we use only deepseek, opencode is giving 60/4 meaning 15 dollar worth deepseek tokens. So 1$ spent on opencode go goves 1.5$ deepseek worth. Commandcode gives 1$ spend 2$ worth deepseek. Only opencode go 5$ first month plan is cheaper than commandcode 15$ plan.
- its just being advertised on command code that you'll get 2$ worth but actual models are very shit you are not getting the actual models you are paying for

- ## [Best subscription to buy when opencode go limits are no longer sufficient? : r/opencodeCLI _202606](https://www.reddit.com/r/opencodeCLI/comments/1ubwbl6/best_subscription_to_buy_when_opencode_go_limits/)
- Create new workspace. Create go subscription for that workspace.
- You could just make a new workspace and buy 2 opencode go subscriptions, I have found that nueralwatt is quite good but the models it offers are limited. For GLM 5.2 and kimi 2.7 it is significantly better value than opencode though, i got over 100 million tokens of GLM for less than $4 of payas you go or $3 of the subscription ($20 a month). But it has way less models than opencode go does.
  - Otherwise codex $20 is a decent amount of usage as long as you remember that gpt 5.4 high performs the same as gpt 5.5 medium while costing half, so dont ever use 5.5 medium. Claude $20 is also alright but I find their budget model sonnet is quite poor for how expensive it is. If you use a lot of deepseek and mimo commandcode is also alright, $1 for $10 of credits at official api rates, a nice one to subsidize other subscriptions since its so cheap.

- So it depends, as long as you think you’ll use 67% of your second OpenCode go subscription, it’s worth it to simply purchase a second one.
  - But it really depends on what models you use. If you mainly use DeepSeek and you’re not sure if you’ll use the full second subscription, you can just use DeepSeek directly through their API (it’s cheaper to use direct API if you don’t use at least 67% of your monthly limit).

- Commandcode 1 dollar is no brainer final backup.
  - Minimax m3 20 dollar 1.7Billion token plan.
  - Then openadapter and Neuralwatt.
  - I have switched from opencode go to Neuralwatt, but even in Nuralwatt 20$ << 2 opencode go memberships. Only benefit I am seeing in Neuralwatt is relatively cheaper GLM and kimi models. But, tbh kimi 2.6 ~ deepseek v4 pro and I miss deepseek v4 pro of opencode.

- ## [对于commandcode的coding plan计费有点疑惑 - 搞七捻三 - LINUX DO _202606](https://linux.do/t/topic/2408464)
- 网站上不是写着15美金的套餐包括30美金的代币么? 30美金等于~203元，没有问题的

- [求佬友推荐下token plan？ - LINUX DO _202606](https://linux.do/t/topic/2306514)
  - 还有一个commandcode go，一刀订阅，但是只能用他们的command code，不过性价比非常高

- ## 给各位提个醒，GLM Coding Plan 的 API Key，你用在各种客户端或者框架下，都能跑通。但是只有官方认可的那些，才不另外计费。
- https://x.com/wshuyi/status/2066071474813927458
  - 我们跑仿真，客户端出了白名单范围，于是 6 月份的账单一下子来到了 1700 多，比全球顶级模型的 Max 20x 套餐都贵
- 用错 URL 了吧，我接到手机里也没单独计费
- token plan 的 url 不是不一样的吗

- ## SuperGrok 近期有优惠，30刀/3个月，两天后截止, 可以买来蹭 composer2.5
- https://x.com/Stv_Lynn/status/2066208560703541626
- Premium+包含SuperGrok

- SuperGrok印区700卢比，折合人民币50一个月，只要Stripe能刷通就可以
  - 十几张卡都难刷通，最后走 iOS 礼品卡通的

- [supergrok 3个月只需要 51.82人民币(Grok Build可用composer 2.5 模型)  - LINUX DO _202606](https://linux.do/t/topic/2404134)
  - 亚马逊印区 购买礼品卡，使用招行万事达支付付款。不是招行万事达直接在 苹果印度区 App Store付款
- composer 2.5 模型用量怎么样，额度机制是什么？窗口还是积分？
  - 150刀每月，cpa可以看。缺点是只有fast，fast比非fast的composer2.5贵6倍。

- ## [我愿称 opencode go $5 为最佳deepseek token-plan - LINUX DO _202606](https://linux.do/t/topic/2398823/17)
- 蹬flash可以 能用30亿 pro不行 才3亿
- 但是切记，仅限蹬flash，别的模型是按照美金计价的，之后v4flash是人民币计价花美金

- 可是 opencode 的 DeepSeek v4 flash 不是免费吗？为什么要花钱？
  - 免费对于每个ip来说有额度限制以及上下文是200K，而付费是1m上下文

- 几个站佬的公益站里ds系列基本蹬不完，跑路佬每天25元，ds费用又那么低

- 用DeepSeek-Reasonix，命中基本都在90以上，也花不了几个钱，思考规划还是要用pro

- ## [Coding Plan 哪家强 - LINUX DO _202606](https://linux.do/t/topic/2361011)
- 刚买的火山，47个ds v4 pro的请求打满5小时，7%的月限额，还是opencodego吧

- 火山的模型倍率很高用不了多少，现在优惠10块钱也只能算一般，和你api价格区别不大（按只用deepseek的情况算）

- ## [GLM的coding plan套餐还行啊 - LINUX DO _202606](https://linux.do/t/topic/2396609)
  - 5h限额: lite-80, pro-400, max-1600

- 下午高峰期3倍，lite绝对是不够用的，我同时实测pro稍微上点强度的情况下下午也是不够用的
  - 调用时将按照“高峰期 3 倍，非高峰期 2 倍”系数消耗额度 
  - 限时福利：非高峰期当前仅按 1 倍额度消耗，持续至 6 月底。 注：“高峰期”为每日的 14:00～18:00 （UTC+8）

- 买了以后它的用量表会显示具体的 token 用量，但是不显示缓存。个人用的比较多的话，比如经常多开几个窗口同时执行大量任务，建议直接上 pro。极高频繁的话只能 max，虽然贵但用量是比国外御三家要大大得多的

- 理想很美好，现实抢不到，什么额度都抢不到

- 怎么没人写协议抢，我记得这个提前点亮教程出好久了
  - 有佬友分享的，从点亮按钮到抓接口更新了好几版了，以前点亮按钮就有机会抢到，现在抓接口都抢不到了

- ## [anthropic和codex各订阅套餐额度大公开 - LINUX DO _202606](https://linux.do/t/topic/2381961/2)
  - 最近，semianalysis针对anthropic和codex各个价格的订阅套餐的额度进行了测试，发现最贵的200刀订阅套餐claude-max-20x和chatgpt-pro-20x都是性价比很高的套餐，几乎可以用到1W刀，有没有佬实际测试过是不是和他的结论一致的，我用过codex的plus和pro-5x套餐可，感觉pro-5x的实际额度基本上是对的上的，但是plus似乎没有700刀额度

- 应该是按照官方API的原价进行计价，我一般是直接用cc-switch这种在后台监控用量，pro-5x还是挺准的，差不多就是3500刀

- 算是有参考价值的，但是不同账号貌似会有额度差异，例如codex的plus周限不同号可能有几十刀差异，这个额度测试可能是最佳情况下能使用到的额度吧

- ## [opencode Go套餐试水-速度测试和用量反馈 - LINUX DO _202606](https://linux.do/t/topic/2362288)
  - 最近codex用不上，想着试试opencode go套餐，看看是不是真的那么划算，额度有那么多，所有就开通了下5美元的GO套餐体验下。【支付支持支付宝，这一点比另一家CommandCodeAI友好多了】
  - 我的结论：果然，如果只是用deepseek-v4-flash，那确实是很多，但是在我的coding场景中，很多时候deepseek-v4-flash不行，就得切换到 deepseek-v4-pro / mimo-v2.5-pro / kimi-k2.6，这个时候额度就完全不够看了。
- 简单来说，就是 $5换$60，额度和价格人家都写清楚了，按自己平时的用量算一下就知道划不划算了, 注意v4 pro是折前价，所以用flash是最划算的

- kimi 就是有点贵, 效果是真好，特别是前端这块儿，感觉比GLM5.1强

- go还是很不错的 至少glm5.1能流畅使用

- 有空也测试下commandcode GO套餐（1$）:https://commandcode.ai

- 不确定是不是我环境的问题，ocgo订阅在claude code中缓存命中只有~50%，在pi/opencode都有~98%

- 免费模型好像是限制一天两百次调用
  - 我一直在使用免费的deepseek-v4-flash，绝对不止200次调用

- [bugteam陨落之后，天才程序员选择了opencode go，佬们你们是如何继续的 - LINUX DO _202606](https://linux.do/t/topic/2364217/2)
- 这个貌似无限不了了，现在限制支付宝了，一个支付宝只能支付一个账号。之前的工作空间bug也没了，不过如果纯用flash，10刀也不是不能接受，比官方还是便宜的

- 看你用哪个模型，头部的几个，额度不多。dsV4pro跟小米的那个量可以，挺多的
  - 我觉得它里面的GLM 5.1不错，就是GLM 5.1的额度太少了

- ## [火山引擎coding plan 怎么突然 9.9一个月拉新了 - LINUX DO _202606](https://linux.do/t/topic/2362049)
- 只是前2个月9.9，后面都是40.
- 这个套餐就是豆包coding plan, 因为其它模型都慢死了
- 之前开过, 实在是太慢了, 晚上根本用不成. 直接放弃

- 他这个coding plan的模型倍率巨夸张，不经用
- 昨晚试了一下，用deepseekv4pro一个任务都没执行完，就五小时限制了，倍率太高了

- 强制实名啊，要不用实名可以整个流口水的豆包玩玩

- 这种说多少额度就多少，说怎么限就怎么限。你甚至搞不清额度单位，哈哈。可以偶尔用用，别形成习惯和依赖就好。

- ## [想问下那些薅kiro企业10000积分的是怎么薅的啊？有大佬分享吗？ - LINUX DO _202606](https://linux.do/t/topic/2346176/9)
- 需要有一个企业（最好是美国企业，据说国内的企业也行），有一定的业务展示（官网等，至少表面你们在开发一些东西），然后申请 kiro startup (Kiro for startups - Kiro)，等审核，他们会根据你们的实际情况给不同的额度（比如我申请到了 4800 刀）。
  - 总之并不是没有成本，而且如果卖的多估计会被查，更多的是 aws 给初创企业的一种扶持，另外 aws 也可以申请一定的 startup 额度，本意是帮企业起步。

- ## [我的付费中转使用经验：一“必须”，四“不碰”，一“绝对” - LINUX DO _202606](https://linux.do/t/topic/2306954)
- 必须：
必须用多少冲多少，绝对不充计划之外的额度
- 不碰：
倍率超低的我不碰，绝对卖数据赚两份钱
频繁调倍率的我不碰，无论是活动原因还是啥，绝对不碰
有订阅的我不碰，卖订阅=跑路
充值限制多的我不碰，比如最低充值数额高于1块钱的，直接润
- 绝对：
绝对没有稳定的中转站
- 以上观点不适用一些官方背书的中转。以及一句忠告：不用任何中转，使用官方渠道。

- 我现在还有800+余额烂在某P站了，想想就来气

- ## [opencode go里的deepseek价格和官方deepseek api价格哪个更便宜？ - LINUX DO _202606](https://linux.do/t/topic/2292942)
- 我记得之前有个帖子算过，你每个月使用 token 超过七亿的话，那就开；不超过七亿的话，那就还是用 API 比较合适。不过，好像指的是 DeepSeek v4 Flash。

- opencode go是按token用量折算美元计费，套餐包含每月60美元的用量。具体来说，5小时限制15美元，周限30美元，月限60美元。而订阅的价格是每月10美元，首月优惠只要5美元（不会有人真的花10美元开第二个月吧？）
  - 模型的价格基本上是对标官方的，比如deepseek v4 flash和官方价格是一致的。但是有例外，deepseek v4 pro和mimo 2.5 pro的定价是官方的4倍。
  - 所以总结来说，v4 flash的价格是官方的十二分之一，v4 pro的价格是官方的三分之一。当然你得用完才划算。
  - 另外，opencode go的模型是支持直接外部接口+api key调用的，我的很多服务都用着它提供的巨便宜的v4 flash。

- ## [国模Coding Plan 在包含glm5.1并且随时可买的套餐分析 - LINUX DO _202605](https://linux.do/t/topic/2267936)
  - OpenCode Go > 讯飞星辰 > 百度千帆（新号有折扣券时）
  - OpenCode Go 整体体验最好，速度和稳定性都还行，热门模型覆盖也全。
  - 讯飞星辰 主要是量大，整体还能用，适合作为备用。
  - 百度千帆 如果新号真有折扣券，Lite 20 一个月的话，我觉得也能接受，但白天 429 严重这个问题还是挺影响体验。
  - 只算最划算肯定是v4f和小米2.5, 能用一百多亿.v4p5刀买怎么都比官方实惠的. 建议每次注册新号买, 10刀买两个号邀请还能多10刀一共130刀

- 国模或多或少都有短板。。说点个人看法。
能用的：
deepseek物美价优，就是首字和整体速度不太行。这个能力这个价格没啥挑的了。最重要的codex不能干的活他能干。
GLM不好买，下午体验差。。（有一阵没用过了）
kimi套餐量不大，能力还过得去，综合体验就是贵了点。这价格不如上A/或这大善人家的。
不值得付费的：
minimax纯量大。丢给一个openclaw实例狠狠地烧token不心疼。。能力捉急。。几个额外的额度如TTS 口播等额度还凑合。纯大冤种订阅了俩月，m3模型没大提升就不续订了。
mimo不评价，申请的额度用了半天丢给同事体验去了。

- 体验上的话, OpenCode Go 是属于那种, 之前偶尔会路由到 FP8 的超级快5.1之外, 大部分时间都很舒服的, 它的K2.6和5.1基本上不会出现429之类的情况, 就是60刀不是很够烧. 大部分时间可能还是得用 Deepseek Pro或者 Flash, 不然60刀很快就能花完, 只能偶尔用K2.6或者5.1爽一下
  - 联通云的话, 就相当的难受了. 白天的速度非常的离谱. K2.6的速度能到10~20 token每秒, 甚至比同一时间的5.1速度还要低. 5.1速度的话, 也是类似的15~30左右.

- OpenCode Go确实行，给的真够多。千帆经常性的限流 对我几乎不可用。 方舟的先开了个最低档，问了几个问题，看了下用量直接去退款了。

- go还有个大优势，就是目前可能最便宜的qwen3.7
- go只是个额度套餐, 我没看到有包mcp, 应该是自己配联网搜索

- 讯飞我用过高效版。glm5.1 没有思考。其他智谱的glm5、glm5.1、百炼的glm5 都有思考。此外讯飞的经常429和400，烦的很。
  - 讯飞默认关闭思考, 这个确实可以自己开的, 而且最近讯飞扩宽了, 429不多了, 还算稳定, 比较多的问题反而是有时降智

- ## [修了一晚上注册机，发现还是手搓算了 - LINUX DO _202605](https://linux.do/t/topic/2202258)
  - 下午手搓了三四个plus，实在是累了，于是想着晚上改改之前的注册机，但是改着改着实在是恼火了，不是这有问题就是那有问题，弄了一晚上实在没辙了，还是手搓吧，手搓大概3分钟一个吧，有改注册机的功夫都注册不知道多少个了

- 日区注册获取试用
邮箱使用outlook的邮箱，差不多4分一个，谷歌搜索就能找到相关的渠道

买完邮箱后接码可以用站内佬的开源项目进行接码 【开源自荐】OutlookMail Plus：专为注册而生

注册完成后获取美区的长链，这里可以使用以下油猴脚本
- 支付
打开长链后记得切换纯净的美国节点，下午我用垃圾节点没过，然后去LD士多花了199LDC买了一个月美国家宽嘎嘎过

这里直接使用支付的油猴脚本即可 GPTPLUS PayPal无卡激活 油猴自动化脚本

但是这个脚本有个问题就是长链的时候如果刷新太慢了会不勾选PayPal支付，还有就是使用的卡比较固定，这里我是让gpt改了一下，自动生成visa卡来达到一卡一号，虽然都是假卡 

- 接码
至于接码的话我相信大家都有渠道，同时告诉大家一个找渠道的方法，不涉及引流

闲鱼买过虚拟卡的都知道，stripe支付的时候有时候需要接验证码，商家给的提卡地址里面往往会带有一个接码的api，一般api和平台都是同一个域名，一张卡2块多还送短信验证，所以你觉得接码成本能高到哪去
反正成本不到一毛钱一个

- ## 🤔 [佬友们如何看待号商？ - LINUX DO _202605](https://linux.do/t/topic/2152488)
  - 没想到自己做公益，只是表达一下自己对现象的观察和思考，对事不对人，已经被称为伪君子了。公益佬友不能哪怕是有点羡慕商业中转赚钱，不然就是伪君子，中转商业放点福利，就是大善人么
- 每个人的想法都不一样。我的想法是: 赚钱嘛不寒碜
- 做号池中转的好多。确实是赚钱。感觉l站很多公益最后也是卖token了。

- 个人的感觉，来源如果是别人提供的公益，用公益赚钱，这是可耻的。但是如果是你也投入了资源、资金、时间等成本，用来赚钱，那是你该赚的。我的原则是，别把别人的好心当成自己赚钱的工具

- 这个世界就是在用信息差赚钱，海鲜市场的也都是。只能说一个愿打一个愿挨~至于这种现象，我表示能理解。但如果不提前告知风险跑路等等举措，那就是人心坏，这个没法理解

- ## [gpt plus日抛号注册原理 - LINUX DO _202605](https://linux.do/t/topic/2159178)
- 印度尼西亚gopay渠道订阅试用plus，协议批量注册，因为gopay开的试用plus就算是正常开的也只能活3天左右，大部分只能活6小时，所以叫做日抛号
  - 还有一个渠道就是 paypal 渠道，这个渠道相对来说活的久一点，这种商品常见号商卖的一键开通plus，价格在10元左右。这种一般质保3天。目前来说只有这两个渠道多一些，至于你说的google pay我了解的，现在就极少了。

- ## 运营中转站这段时间是真没赚到钱，只能说勉强cover了我自己用ai的消费。
- https://x.com/sukie234/status/2052067924257493416

首先整个系统由3个部分组成：
• 第CN2 回国专线服务器：放在海外但回国速度极快的 VPS，作为运行核心。
• sub2api：核心程序，负责把网页账号转成 API 接口。
• Cloudflare：把流量再绕一道，提升国内访问速度，同时隐藏真实服务器 IP。

你需要准备：
• 一台 CN2 GIA 或 CN2 GT 线路的海外 VPS（推荐配置：2 核 CPU、2GB 内存、20GB 硬盘以上）。

普通海外 VPS 在国内晚高峰几乎不可用，而 CN2 GIA 通过专线绕开了拥堵的公网节点，国内访问延迟一般在 150ms 以内。如果你买了不是 CN2 的服务器，国内用户体验会非常糟糕。

• 一个域名（建议在 Cloudflare 或 Namecheap 上购买，便宜的 .top 或 .xyz 也行，几块钱一年）。
• 一个 Cloudflare 账号（免费）。
• 号池：初期可以用 claude code pro 账户+ 注册大量gpt账户，货比三家去找到别的号商卡商，等后期你就可以搞claude code max kiro 反代 aws bedrock（去跟sales聊，基本能搞到7.2折），但是初期只需要保障claude code pro账号稳定即可，因为你需要养号，后期转max。

完整请求路径如下：
国内用户的客户端 → 解析到 Cloudflare 的 IP → Cloudflare 边缘节点 → CN2 专线回源到你的服务器 → 宝塔面板的 Nginx 反向代理 → sub2api 程序 → 你的号池 → ChatGPT 或 Claude 网页 → 数据原路返回。

购买并初始化CN2服务商
CN2 GIA 线路的常见服务商有 BandwagonHost（搬瓦工）、RackNerd、CloudCone、Lisahost。新手推荐搬瓦工的 CN2 GIA-E 套餐，稳定但价格略贵。预算紧的可以看 Lisahost 的香港 CN2 套餐。
如果你懂命令行搭建Nginx，手动部署SSL证书，那你就自己搞，如果你不懂可以使用中国程序员流行的宝塔面板，一键搭建Nginx、一键部署SSL证书、可视化配置反向代理，全程鼠标点击操作，新手也能轻松上手。
安装完Linux + Nginx + MySQL + PHP，就可以开始设置防火墙，够买域名，添加DNS解析。
最后去命令行输入ping.api. 你购买的域名，返回服务器ip就行了。

搭建sub2api:

sub2api 是一个开源项目，可以把 ChatGPT 网页版、Claude 网页版的 cookie 或者 session 转换成 OpenAI 兼容的 API 接口。

打开sub2api的官方教程，安装流程安装docker，拉取并启动sub2api的容器。

你需要把号池数据放到 /www/sub2api/data 目录下，sub2api 容器会读取这个目录。具体格式参考 sub2api 项目文档。

设置Nginx反向代理

添加完之后目标url是127.0.0.1:8080因为 sub2api 容器监听的就是这个地址。Nginx 收到外部请求后，转给本机的 8080 端口，sub2api 处理完返回给 Nginx，Nginx 再发回给用户。

后面你去问claude code 如何优化Nginx的配置，AI API 调用是流式响应（SSE），需要长连接 + 不缓存才能正常工作。默认 Nginx 配置在这种场景下会出问题，按照claude的提示优化，proxy_buffering 必须关闭，如果不关闭这个，AI 的回答会"卡一阵 → 一次性吐出"，而不是逐字流式输出。客户端会感觉非常慢甚至超时。

申请HTTPS证书：
OpenAI 兼容客户端基本只信任 HTTPS。HTTP 明文会暴露 API Key 给中间网络。
申请好Let's Encrypt证书之后，回到 SSL 主界面，把"强制 HTTPS"开关打开。

优化Cloudflare配置
测试HTTPS-开启cloudflare代理-Cloudflare SSL 模式必须设为 Full (strict)
AI API 是动态接口，Cloudflare 的某些"优化"会破坏流式响应。
Cloudflare → 你的域名 → 速度 → 优化。
全部关掉以下选项：
• Auto Minify（自动压缩 HTML/CSS/JS）：关闭。
• Rocket Loader：关闭。
• Mirage：关闭。
• Polish：关闭。

设置缓存规则：
Cloudflare → 缓存 → 配置。
Caching Level 选 Bypass，或者保持 Standard 但是后面用页面规则覆盖。
更彻底的做法：Cloudflare → 规则 → 页面规则 → 创建页面规则。
URL 模式：http://api.example.com*
设置：Cache Level = Bypass

设置防火墙规
Cloudflare → 安全性 → WAF → 自定义规则 → 创建规则。
规则一：限制单个 IP 频率
字段：IP source address，操作：Rate limiting，每 10 秒最多 30 次请求，超出后挑战或屏蔽 1 小时。
规则二：屏蔽明显恶意爬虫
字段：User Agent，运算符：包含，值：python-requests
启用 Cloudflare Argo Smart Routing，每月 5 美元，能在 Cloudflare 内部用最优路径路由你的流量。对国内用户访问海外服务器有 30% 到 50% 的速度提升。预算够推荐开。

测试上线
用 curl 测试 API，或者打开 CherryStudio 或 ChatBox，填写你的api地址和key做测试
使用Prometheus/Grafana，或者直接用宝塔面板做监控，可以看到 CPU、内存、流量实时数据。如果 sub2api 容器经常吃满 CPU，考虑升级服务器配置。

- 写完技术部分来写一下如何推广营销：营销这部分算是我的专长，首先我们需要一句话写清楚我们这个产品的优势：
  - 国内直连、高稳定、多模型 AI API 中转，支持 GPT-4o/Claude Opus 满血，企业级技术支持。
- 另外确定目标用户：

01.                                                                                                                                                           个人开发者：
特别厉害的个人开发者其实自己也可以解决我刚刚写的那些东西，所以我就不跟这些人卷了，我去闲鱼上找了很多代写项目，毕业设计，软件开发的开发者，这部分人一般懒得折腾，不懂如何配置号池。

01.                                                                                                                                                           ai套壳创业者：
他们需要稳定的api，高并发，子账号，针对这部分用户定制了一些企业级的面板和技术支持，然后去三四线城市的boss直聘/转转找各种ai创作视频，装修，ai做本地服务的小团队小企业，跟他们聊合作。

01.                                                                                                                                                            中小企业/传统行业/实验室
他们需要合规，开发票，私有路由，所以我在国内开了个公司，给他们走合规公司签单。

其次就是做seo，小红书，抖音，比如我这篇文章就是一篇seo，seo的核心就是why what how 通过教别人如何搞中转站，如何使用claude code获取流量，当然你也可以发布在知乎掘金csdn个人博客V2EX、NodeSeek、SegmentFault、Linuxo
标题：

《国内直连 GPT-4o/Claude API，稳定 99.9%》

《破产后我在家开中转站日入过万》

回帖：在“求 API”“不稳定”问题下推荐自己

然后就是社群裂变：

在各大开发者群里面发自己的产品，并招募代理，通过免费试用 + 裂变实现冷启动。

注册送10刀额度，邀请好友双方各得5刀。

长期返佣：邀请用户消费的 10%–20% 返给邀请人。

针对学生用户，我们还有学生邮箱打折的优惠。

然后就是建qq群，把以上用户全部引流在群里，定期更新项目动态。

这样一条龙下来，你的生意就启动了。

- ### 我也总结下自己运营快一个月的中转站经验
- https://x.com/wangray/status/2052271405081997734
  - 结论跟 sukie 老师差不多，即使现在我有上千注册用户，日流水破千，但实际算下来并没有网传的那么暴利，用来当个副业，或者说像我一样是作为主业的增值服务那是划算的，不然现在埋头进来就是淹没在一片红海里
- 
我的初始准备：
• 一台 VPS，DMIT 家的 EB. WEE 年付款，本来用来搭梯子的，使用率不高，就直接拿来当服务器了
• 一个域名，我已有
• Cloudflare 账号，给域名开通 Argo 路由，月付5美元
• Stripe 收款：美国主体开通，单次手续费在3%左右，确实高，但是考虑到合规性必须用 Stripe
• 号池：我维护的都是 Claude Max 20x和 GPT Pro 200u正价账号，这也是为什么实际我赚的并不多的主因，成本确实高，包括提供的 Anthropic API 也是官 Key，基本是赔本赚吆喝，也正因为如此，前阵子 GPT 封号潮，对我们的稳定性影响不大
启动成本：$600-$1000

如何开始：
Step 1:
初始化 VPS，然后本地指挥 Claude Code 去服务器配置好所有环境，然后安装 sub2api 开源项目，跟随指引很快就能部署好一套服务

Step 2:
配置外网访问，在 Cloudflare 完成 DNS 解析，同时可以用 CF 提供的10年期 SSL 证书配置 HTTPS 请求，完成之后你就可以用域名访问你的中转站了

Step 3:
CF 优化可以参考 sukie 老师原帖，我就不再赘述，建议开的是 Argo Smart Routing，毕竟 CF 在国内部分区域可能存在不可访问的情况，这在一定程度上会有些改善

Step 4:
完成自测，考虑好定价模型，即可小范围内测，如果没问题就可以大范围公开上线

自此，你就拥有了一个自己的中转站

如何获客：
这应该是你考虑做中转站之前就应该想好的问题，如果你只是想搭一个中转站跟朋友一起分享平摊 AI 订阅费，这完全OK，但如果你想以赚钱为目的，你就要想好你的客源在哪里

中转现在已经是红海，你通过闲鱼/小红书/抖音去截流获客，转化低，而且竞争者的价格可能比你还低，反正就我的情况来说卷价格肯定是卷不动的

c端客户的流动性很高，哪家便宜就去用哪家，最稳的方式还是你有客源，或者参考 sukie 老师的推广营销方案，去找 AI 套壳创业者/中小企业/传统行业，这些客群只要求你稳定提供服务，现金流就是持续的，28原则放在哪里都是真相

- ## 老实人是赚不了钱的，最近也是听同行说一个前段时间刚开始干的中转站，严重掺水利润做到九成
- https://x.com/Pluvio9yte/status/2050436054591877593
  - 他们现在一个月就至少赚200万，基本是我们的50倍。
  - 保持初心很困难，听了他们这个我也动摇过。不过还是忍住了。这卷钱速度真的堪比没有风险的抢银行

- 掺水做不了太远的，用一阵子都知道，只能骗骗新入门玩龙虾的人

- 能用顶级模型的大家又不傻，一次骗就不会再信任，我们就不会要低价造假的，这行业最后就是拼口碑

- ## @justinsuntron孙哥也加入中转站创业了，有种刘强东搞外卖大战美团和饿了么的感觉。前期大撒币最是简单抢占市场的手段。
- https://x.com/eastweb3eth/status/2050156414954525009
  - 另外连孙哥都加入这门生意，说明这生意是真赚钱。对于消费者来说也是好事，希望更多竞争给消费者带来更多实惠。
下面我将列出自己收藏的全部中转站，排名不分先后，大家挑便宜和服务好的用即可：
01.       https://tokennav.cc TokenNav 中转站导航
02.       https://aibijia.org
03.       https://aigocode.com
04.       https://manage-xai.ainaibahub.com
05.       https://openrouter.ai
06.       https://subrouter.ai
07.       https://helpaio.com/transit
08.       https://packyapi.com
09.       https://openclaudecode.cn
10. https://api.ikuncode.cc
11. https://dapicloud.com
12. https://b.ai 

- 孙哥的投资眼光还是不错的

- ## [复盘：两周代理生意，从入局到出清 - LINUX DO _202605](https://linux.do/t/topic/2093866)
- 为什么入局
  - KYC 焦虑：Anthropic 即将对订阅账号做 KYC 验证，我们担心自己过不了——既然自己要去找代过 KYC 的渠道，那这条渠道反过来也能做生意。
  - 业务转型的判断：自营的 API 中转站对 to C 客户越来越难做，只有 to B 与稳定渠道能在官方封号的"猫鼠游戏"里活下去。
  - 代理模式的吸引力：在推特上观察到一类 Web3 风格的上游玩家，他们抓推流、提供渠道，下游负责销售与售后。"代理"这个概念第一次进入视角——本质上是把售后风险从供应商身上分摊出去。
- 投入成本
项目	金额	复盘
上游推流玩家的代理权	1500 元	价值在于进入代理群、认识同行，由此知道了 GPT 低价代充渠道的存在
上游一级代理（V2）资格	1200+ 元	过度投入。V1（约 600 元）就够用
- 失败原因
  - 入行太晚: 这条低价代充渠道从去年 12 月就稳定运行，我们整整晚了四个多月才入场。原因很直接：我们自己不用 ChatGPT，也没在跟踪这个圈子的信息。如果 4 月初就开局，结局会完全不同。
  - 没识别出倒计时信号: 4 月中旬，圈内已经有人公开向 OpenAI 举报上游的两家头部号商。我当时知道这件事，但判断 OpenAI 不会那么快修复——结果半个月内就修完了。推特上"凭证被回收"的提示同样被我忽略。事后看，这些都是窗口关闭前的明确信号。
  - 销售平台全部不合适: 
    - 闲鱼	对 AI 服务的关键词屏蔽极严，上架几次就被处罚，走不通
    - 小红书	收货周期 15 天，几乎没人提前确认收货；订阅两三天内就开始掉，售后压力极大
    - 链动小铺	一天后不直接退款，但客户投诉到平台仍会被强制退款；一旦投诉到上游或支付方，可能清空全部收益
    - 灰色品类，没有任何一个平台能真正甩掉售后责任。
- 最本质的失败原因是入行节点不对，其余都是次要：投入时间有限、代理层级买得太高、绑定上游过深。
  - 但两周不算白折腾。号商、卡商、代理、二级代理、分销平台、散客、中转站之间的链路，第一次完整摸了一遍。 下次再遇到类似的窗口，至少能在前两周内判断出渠道还能活多久。

- 你付费进群了难道没有了解出他们的卖的渠道都是tg吗
  - 我是想尽可能弄那种稳定的卖，做代理就是面对下游代理和散客，我也不想天天处理售后。

- 更多是没有自己的技术，GPT 低价代充现在还有各种门路，并没有像你说的死掉，当上代理不自己发展技术那就只能GG 了
  - 现在还有各种 IOS，优惠码开出来的 PLUS/Team 甚至 Pro 售卖

- 弄公益站吧，边培养人脉，边学技术，转收费站

- ## 美国公司含金量还在涨。这部分token的价值目前在30万人民币左右。除去公司成本外，这部分token的总成本仅为1400刀。
- https://x.com/xkajon/status/2047982771378040937
  - 小中转站很快会彻底失去竞争力。前提是这个渠道被大规模公开，不过离那天还有一阵。
  - 目前这笔账我算出来是这样的：成本 200 到 250 刀，最低换 2000 刀的 token 额度，最高可以换到9000刀的token额度，成本比反代还低几个数量级，并且在稳定性直接碾压。
  - 最吃稳定性的就是企业客户，而企业客户恰好是整个链条上付费意愿最强的一群人。

- 能用完都不一定吧，这个东西早被中转站玩烂了吧，特别是谷歌的，封控不是一般的严重，真上生产级别的项目，503 429一堆吧

- 一样美国公司银行卡 付完款claude就封号.. 当然是新号
  - 其中的变量有很多，包括网络环境、机器识别码等等，支付只是其中一个，能做的就是将可控的环节都做掉。

- 然后因为税务问题被罚几万 后面入境不了美国

- https://x.com/xkajon/status/2048255475305808156
  - 美国批量申请空壳公司去撸云厂商启动补贴，这路子根本走不通。为什么？我亲手跑完的，我最清楚：
  - 第一，新注册的公司拿不到 startup funding，零。公司没满三四个月，系统里连资格的影子都看不见。
  - 第二，想拿一千刀以上的补贴，加速器背书或者投资人背书，必须得有。

- ## [【GPT Team 疑问】一个账号能加入多个 Team 车队吗 - LINUX DO _202604](https://linux.do/t/topic/1762419)
  - 想问一下一个账号能否加入多个 Team，每次用完了就切换一下
- 可以加多个，是按周重置

- 会自动切换吗还是要重新oauth一下？
  - 要重新oauth

- [一个号加入好几个gpt team，封一个会被全封吗？ - LINUX DO _202604](https://linux.do/t/topic/1979774)
- 以前用的时候不会，team空间掉了只会掉那一个。
- 个人使用经验：只加team并不会封。我开的就为了加team的小号，目前陆续加了19个（前面18个被封，因为是纯小号，甚至懒得退出），目前还在使用。不同的team之间也不会互相影响，经常同时开车一个掉的快一个慢。

- ## [低价chatgpt plus渠道交流 - LINUX DO _202604](https://linux.do/t/topic/2050162)
  - 近日，由于OpenAI将谷歌0刀bug修复，凭证较难开出，但仍有其他源头能够开出凭证，且价格水涨船高，从以往7元涨到了现在的35元，相当于以往开5个plus，这中间的利润可想而知。
  - 目前，发现的最便宜的渠道为One. IDKey，只需20元即可开出plus (pro较贵)，为了避免被说引流，请自行搜索。
  - 还有更便宜的就是第一个月试用 (plus和team)，但是不稳定，站内也有教程。希望佬友积极交流，放出价格，可以不给渠道，以此给大家心里面一个价格线，方便了解目前鱼龙混杂的市场。

- 自用根本不需要那么高的成本，凭证复用才是高成本的来源

- team可以，有的卡需要垫刀才能开出来，有的卡可以直接开出来

- 佬友的渠道还是太闭塞了 目前日抛的价格在3~5块/个 plus成品号 三日team子号的价格在6~10元/成品
  - 最近好像还有一批jason渠道的，不知道走的哪个渠道，是9元号源，听说稳一周
- jason渠道有点意思好像都是批发几万出

- ## [分享下最近低价 GPT Codex 的来源(源头) - V2EX _202604](https://www.v2ex.com/t/1206503)
https://shop.86gamestore.com/ 最近泛滥就是因为这个源头下场卖货然后一堆倒卖的 plus7 元
https://ferrigpt.asia/ plus 6 元 5x 95 元 20x 160 元（这家 Plus 掉订阅比较多）
https://shop.nitro.xin/ xin 渠道散客买不到太低价格 代理 Plus 8 元左右
https://makerich.club/ chong 这个渠道不是源头，也是流传最久的渠道 价格散卖 5x 110 元 20x160 左右
@gptnocard_bot tg 机器人 20x 大概 60 元左右 plus 零成本（机器人队列比较慢）被大家论坛熟知就是这个 bot 下场送 20x.

申明：上面链接与我无任何利益相关。

现在外面任何 Gpt 代充都是这个原理，别相信官方代充 ios 代充。这个方法已经从去年 12 月份流传至今了。可以说从去年 12 月份开始你们在外面找的代充都是这个渠道，都是狠狠赚了你们一笔，别不信。
我也倒卖了一段时间，闲鱼卖不了之后，还开卡网卖了一段时间。闲鱼卖了几百单，小铺卖了几千单。总结异常的稳定，plus 掉订率 0.5%左右，pro 掉订率 1%左右. 至于封号基本都是你自己号的问题。

- 楼下有个卖货的货源 https://auto-subscribe.com/cat/2 这个应该是套壳的 chong 的大家别上当。这个论坛所有的卖 GPT 的都是从我发的货源来的充值界面不一样都是套壳的。原理很多人都懂但是能批量拿出卖的人还是没有几个的。

- OpenAI 怎么还没下场, pro 用的我好爽
  - 说不定早就知道了，要用户量，或者根本不想管。

- 源头都是零成本。一天几十万利润。
  - 谷歌 play 英国虚拟卡试用，然后抓包改账号 大概是这个
- apple 和谷歌充值特定账号后给个收据， 第二步这个收据绑定到一个账号, 即激活 plus/pro. 这个收据可以复用, 没有上限, 付款一次拿到的收据可以激活无限个账号

- 看到一个帖子，大概是说正常账号付款后在某个页面的接口中，会返回一个付款凭据的 json ，然后这个 json 可以拿着去给别的账号用，不知道是不是真的
  - 就是这个原理。

- 为什么第一个源头站，年卡比月卡还贵？
  - 年卡源头他们是有成本的，月卡可能用的 0 元购的链接没有成本。

- https://x.com/xkajon/status/2044979326630891642
  - 帖子被删，账号被关小黑屋。 就因为我把0成本GPT Plus 漏洞的技术细节写出来了。
  - 因为我他妈实在看不下去 Web3 那帮博主天天在那儿制造 FOMO。手里攥着个破技术跟攥着传国玉玺似的，藏着掖着，然后转头收你二百 U 教你怎么搞代理站。二百 U 学什么？学怎么帮他拉人头。
  - 我就一个态度：开源。扔出来，大家一块儿看，一块儿研究，一块儿学。
  - 外面那些收费几千教人“GPT 代充技术”的，教的就是这几步，GPT Plus 土耳其漏洞全公开技术贴(本文仅供技术交流。任何实际操作产生的账号封禁、法律风险，自行承担)
  - 原理：OpenAI 不查 Apple ID 对应关系，拿张收据就能给任意号开会员
  - 你 iPhone 上点付款 → App Store 扣钱 → Apple 把收据扔到你手机本地 → ChatGPT App 捡起收据 → App 把收据和你当前登录的账号 token 一起打包发给 OpenAI → OpenAI 验一下收据真假 → 给你账号开 Plus。
  - 漏洞就藏在 OpenAI 验票那一步。

- 其实你完全不用说的这么冠冕堂皇，说难听点，不就是你看不惯人家赚钱嘛，为什么非闲着没事儿干断人家财路呢？有需求就有市场，你有堵不完的路，何必把自己搞的这么累？赚自己能赚的钱，谁有谁的道和术，仅此而已。

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

- ## 对于中国市场而言，中转站的意义是帮用户：
- https://x.com/interjc/status/2050839205010661758
  - 搞定了网络；且不说有没有以次充好搞灰色的问题，是不是一定程度上扮演了机场的角色？
  - 搞定了支付；
  - 搞定了KYC；
- 中转站上游是原罪，需要用各种薅羊毛、仅退款等形式来获取 token 价差，把正常中国用户都给牵连。这是一个恶性循环，你越使用中转站，官方就封中国账号越厉害，然后反过来又越依赖中转站。这其中获利的只有中转站老板，但是也迟早会面临法律风险，就跟当初在墙内卖 VPN 的那些人一样，赚钱的都会被清算
  - 早期是这样，客户稳定以后他们就会以次充好了，上游风险会降下来

- AI中转站利润比机场高，法律风险远比机场低，的确是一个赚钱的好机会
# discuss-llm-api-free
- resources
  - https://github.com/cheahjs/free-llm-api-resources
    - free access or credits towards API-based LLM usage.

- ## 

- ## 

- ## 

- ## 

- ## 

- ## We just launched free Kimi K2.7 Code in our free coding agent: npm i -g freebuff
- https://x.com/jahooma/status/2075775678633648503
  - Check it out! We have a web agent as well as the CLI.
  - Note that not all regions have access to all the models.
  - [Freebuff — the free coding agent (free Claude Code, Codex, Cursor & Lovable alternative) ](https://freebuff.com/)
  - https://github.com/CodebuffAI/codebuff /7.3kStar/apache2/202607/ts
- is there a reason users cant use kimi if they're using a vpn?
  - Sorry, it's only available in certain regions and vpns make that hard to discern!

- don't call it *free* when you have like 5 mins using and it's done. scam alert!
  - You get at least 5 hours per day! Not sure what you saw

- 
- 

- ## [免费魔搭实现token自由 - LINUX DO _202607](https://linux.do/t/topic/2531571)
  - 10账号轮询。500次glm-5.2、500次DeepSeek-V4-Pro、500次DeepSeek-V4-Flash，用完就切或者自动切，一天1500次请求实在不行就切到qwen又不是不能用，还要什么自行车，这个体验比nvidia好多了。
  - 图上几个模型都是限50
- 但是魔搭注册得要绑定手机号吧？没那么多手机号啊
  - 用朋友家人的就行，收两条验证码，一个身份证可以绑定6个阿里云
  - 一个身份证可以绑定6个阿里云，支付宝扫码一下就能绑，试过了很简单。

- 1m上下文，我今天用了50Mtoken，按次请求，平均每次100k token

- 哪来这么多实名…我也不太想用自己的，万一封了得不偿失了

- 魔搭的免费版限流特别严重。之前是调用量特别少，像ds-v3.2只能调用20次。ds-v4出来以后，我发现调用量给了500次，阿里突然这么好心了？一用才发现嗷嗷限流，体验感和满大街发的mimo差不多，跑两步就限流，再跑两步又限流。

- ## [最近总结的免费用 GLM 5.2 / DeepSeekV4 的几个方法 - LINUX DO _202606](https://linux.do/t/topic/2441446)

- ## [怪不得copilot 积分用的这么快 _202606](https://www.nodeseek.com/post-786737-1)
  - 我把copilot接入了中转。之后使用了一段时间，结果发现缓存命中率只有60左右（CODEX应该是要到90%）

- ## [华为出code cli了，无限用GLM5.1 - LINUX DO _202606](https://linux.do/t/topic/2405921)
  - https://gitcode.com/openharmony-sig/deveco-code /MIT
  - 面向 HarmonyOS 开发场景的 AI Agent 工具，支持代码编写、编译构建、设备运行、文档查阅、运行时调试及 ArkTS 问题修复等能力。
  - 基于开源项目 OpenCode 扩展开发，保留了 OpenCode 的终端交互、配置体系、 Provider / MCP / Skill / Plugin 等能力，并针对 HarmonyOS 工程增加了 DevEco Studio、Hvigor、HDC、Skill、HarmonyOS 知识库、ArkTS 检查和设备调试相关集成。
  - 暂不支持 Linux。HarmonyOS 编译构建、模拟器与真机调试依赖 DevEco Studio，且目前仅提供 Windows 与 macOS 版本。
  - 当前免费提供 GLM-5.1 模型，单账号默认每分钟 50 次请求。也可以通过 Ctrl+A 进入 Provider 选择界面，配置支持的第三方模型。

- 替大家试了，吐字非常慢，不如公益站

- deveco看起来非常像opencode原版，比mimocode的定制化程度小，不知道有什么额外的功能

- ## [不同服务器上调用Nvidia免费api成功率区别挺大的 - LINUX DO _202606](https://linux.do/t/topic/2357012)
  - 我在两台服务器上部署了newapi，调用nvidia的免费api。 主要测试调用deepseek v4 pro，ds比较热门。
  - 一台是美东的dedirock，1H2G小弱鸡，cogent->4837线路，延迟250ms～300ms，大部分时间调用ds v4 pro是失败的；其他模型整体测试成功率也不如下面这台skyline的。
  - 下面这一台是小鬼子家的skyline，1H1G小弱鸡，软银->4837，延迟70ms～100ms，大部分时间可成功调用。
  - 按说即便所属地区不同，调用的也是nvidia同一个算力池。但明显小鬼子家延迟低这台小鸡实际调用成功率更高。
  - 我连着三天不同时段测试了，最开始我以为是dedirock上newapi版本旧的问题，更新后再测试依然是这个结果。整体上skyline这台服务器调用成功率就比较高，尤其是ds v4 pro模型。

- 可能是恰好时间点的问题，nvidia的api就有时候只会卡顿3分钟左右就又变流畅了

- ## [闲鱼上卖的反重力从哪里来的 - LINUX DO _202605](https://linux.do/t/topic/2215828)
- 我是建议不要买，买了给自己找罪受, Antigravity对号的各种风控评价，你如果号白的话用起来很不错，如果号黑就是一直429

- ## 📌 [L站，GPT羊毛史官 编年史 - LINUX DO _202605](https://linux.do/t/topic/2196712)

- ## [有没有用Kiro反代的佬 - LINUX DO _202605](https://linux.do/t/topic/2141352)
- 用kiro-go，都不用安装kiro客户端，直接添加cookie就行，我玩了一天没被封

- 是的，打开app.kiro.dev/home网站，右键审查元素找到cookie，然后填入 凭证 JSON
  - 填最后那个，像这种格式就行[{“refreshToken”:“xxx”, “provider”:“Google”}]
  - 拿到的是浏览器cookie有效期应该很长吧，我用了四五天都没失效

- kiro官方的提示词始终都在的，上游注入进去没办法去掉，只能加点提示词减少干扰了（不然直接在claude code之类的地方用会胡言乱语）

- [kiro额度超到1w+了还能用啊 - LINUX DO _202605](https://linux.do/t/topic/2178790/17)
  - 同一个账号，kiro ide可以正常看到使用opus模型，kiro cli就只能用DeepSeek 3.2等，有佬知道怎么解决吗
  - 因为cli默认不走代理，问一下ai加个环境变量就行
- 头两天一直用的4.7，很快很流畅，差不多从前天开始估计薅的人多了，现在4.7动不动就无响应，现在白天用4.6, 晚上人少的时候用4.7, 总体下来还是4.7用的多
  - 体感上还是4.7强一点，4.6遇到问题撞墙撞多了的时候切个4.7往往能很快解决，不过也没有压倒性的强，大部分活4.6干也没啥问题
- kiro go 超额也是不能用了，但是客户端好像还能用

- [Kiro反代情况 - LINUX DO _202605](https://linux.do/t/topic/2148687)
  - 跑了1天了 KiroGo 目前状态正常 一个号没有阵亡爽飞了

- ## [【开源推广】免费 Token Agent？用 yaCA 与 yaCA-Web 让你的 2api 模型也能调用本地工具！  - LINUX DO _202605](https://linux.do/t/topic/2169087)
  - 自己搓了一个仿 Claude/Codex cli 的终端 Agent，取名 yaCA（yet another Coding Agent）。基本仿照 Claude/Codex cli 制作，但特别加了工具兼容模式，通过提示词让大模型输出 XML 风格的工具调用，从而让一些无法调用本地工具的 2api 模型也能用上本地工具调用。
  - yaCA Web 作为 yaCA 的拓展包，主推的是默认 HTML 模型输出的功能，通过几个内置类名让模型轻松输出信息密度和组织程度更高的消息。运行时动态依赖 yaCA Cli，需要先全局安装并配置好 yaCA Cli。
  - 整体来说是人工 + vibe 搓出来的玩意，开始的时候还愿意自己手搓核心代码组织项目结构只 vibe 写迁移等繁杂任务并逐行审查，到后期项目大了一点就放开自我了……大部分 AI 写出来有效果就过也不看了

- ## [用Hub的一定要慎重，怎么制裁他？？？ - LINUX DO _202605](https://linux.do/t/topic/2132553/30)
- 我早在15天前就说过这个问题，发布渠道的人可以随时改价，可以让一个渠道本来免费，看有人调用的多了，马上改成高价来背刺用渠道的人
- 这个站理想是好的, 人人拿闲置的token互相交换, 但是完全不透明, 甚至还有暗箱操作的情况, 模型你都不好分辨是不是真的, 很花精力, 只能说有很长的路要走
- 看调用记录，是缓存读命中的时候，扣费非常离谱, 所以那个上游是钻了空子，假设佬友们试着调用一次，那无所谓缓存，费用很低，但是佬友们开始多次调用，缓存命中高了，费用就逆天了

- 还有人用haiku伪装opus4.6的。

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

- ## ✨ [cline免费调用m3, mimo-v2.5, 和dsv4f, 支持创建key直接调用 - LINUX DO _202606](https://linux.do/t/topic/2321520)
  - https://api.cline.bot/api/v1

- [关于Cline免费模型在OpenCode的一些坑 - LINUX DO _202606](https://linux.do/t/topic/2322384)
  - 三个免费模型（v4/2.5/3）端点都不支持 Anthropic 和 OpenAI Responses 格式，只支持 OpenAI Compatible 格式（@ai-sdk/openai-compatible），否则返回
    - {"error":"Unauthorized: Please make sure you're using the latest version of Cline and re-authenticate your Cline account."}
  - 三个免费模型只支持最高 xhigh 推理强度（"reasoning_effort": "xhigh"），否则返回 Failed to create stream

- 注册还要手机号
  - 谷歌登录无需手机号, 直接送0.5
- 注册好了，Google SSO，也得手机号，好在支持 +86.

- 在手机客户端看起来没有获取到模型，不知道是不是平台不支持的缘故，我试试手动添加
  - 👷 实测需要手动添加模型名， 可在vscode-cline获取到模型名
- 免费模型还经常换，需要手动填写， 感觉有点麻烦呀

- 实测会对并发作限制，得和 opencode 一样搭配动态 IP 池才行

- 好像有日限额。已经429了哈哈哈哈，不过是一个模型算一个的好像
- 总调用次数：124 次
  Prompt Tokens：13.64 M
  Completion Tokens：0.09 M
  Total Tokens：13.73 M
  Cached Tokens：13.14 M
  账号单模型
  用的是deepseek-v4-flash
  24小时之后重置
- 也不算少就是了一个号每天, 还算可以

- ## ✨ kilo提供 [Kimi K2.5 MiniMax M2.5免费API渠道](https://linux.do/t/topic/1683518)
  - Kilo Code扩展里扣出来的
  - https://api.kilo.ai/api/openrouter/chat/completions
  - https://api.kilo.ai/api/gateway

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
  01.                                           q2api(claude)
  02.                                           英伟达ai平台（大部分开源模型）
  03.                                           hf抱脸（大部分开源模型）
  04.                                           groq平台
  05.                                           硅基流动平台
  06.                                           富可敌国平台（duck已许可分发付费站anti, 正在申请分发max）
  07.                                           杂七杂八的短效羊毛平台（国外）

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

01. 首先你要有渠道，没有别往下看了
02. 你要有闲置资金，时间。至少要有自己的服务器吧，没有就得各种薅，折腾。
03. 有渠道，有时间，有资金。那就开始造。
04. 可以接入，newapi/one-hub/done-hub。记得在 Linuxdo connect 中申请应用接入，配置好 L 站登入。差不多就完事了。
05. 奔着公益去开公益，不是很推荐。我们都是奔着折腾，玩弄的。就比如我的，智谱年包 lite 230 / 年，netcup 服务器 55 / 月，各种七七八八还得 100 / 月。就这都还有人贴脸说各种不行。不过我很少回应。不行别用

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
