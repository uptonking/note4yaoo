---
title: lib-ai-app-community-chat-conversation
tags: [ai, chatgpt, community, conversation]
created: 2023-04-16T10:02:33.647Z
modified: 2023-04-16T10:02:58.738Z
---

# lib-ai-app-community-chat-conversation

# guide

- pm-ai-chat
  - 与ai或bot的对话可参考类似产品的设计和api，如chatgpt、copilot

- HuggingFace
  - [魔搭社区](https://modelscope.cn/home)
    - 汇聚各领域最先进的机器学习模型，提供模型探索体验、推理、训练、部署和应用的一站式服务
# pm-chat
- table内容也能按行打印，如gemini/chatgpt

- 
- 

## not-yet-chat

- ai返回的内容通常不直接包含可点击的链接或引用

- 
- 

# discuss-stars
- ## 

- ## [nextchat已经四个月没更新了，是凉了吗？ ](https://linux.do/t/topic/1506232)
- 有太多选择了，桌面端好几个，不过个人更重视安卓端。

安卓端可以选：

RikkaHub / Kelivo
LastChat Plus（RikkaHub 的 fork，增加额外功能，比如 Agent Skills）
BotHub（新晋客户端，走类 ChatGPT 的清爽风格，支持多模型同时回复、文生图等，提示词注入正在开发，Agent Skills 也有望加入；iOS 端正在开发中；后续会开源……）
Operit AI
AetherLink
NoteGen（以笔记为主要形态）
TChat（开发者原本是 fork 的 RikkaHub，名为 RikkaHubX，后又决定重新开发，但外观上还是与 RikkaHub 相仿）
BotGem
Chatbox（老资历，但目前没什么新的发展）
AIaW
OMate（角色扮演）
ChatterUI / PocketPal（本地推理）
还有一些不是那么广为人知的……
iOS 端至少有 Kelivo……（没接触过苹果，更多的就不清楚了）

网页端 LobeChat 十分活跃，LibreChat 也偶尔更新。

- ## We separate ui message and model message in LobeChat 1.0 last year. And it turns out to be the most flexible way
- https://x.com/arvin17x/status/1920106270415360251 
  - Glad to see ai sdk go toward this path
  - What you display to the user (ui messages) is different from what you want to send to the LLM (model messages).
  - Actually we storage the llm messages in db and then construct the ui message from llm message. 
  - For example, in the tool calling, we save both assistant and tool llm message as serperate item. And then combine them into one ui message.
  - I think it's the key. Don't make ui message as SoT. Because display demand is flexible, ui message should be constructed by all db items

- ## 🏘️ 分享下我们在做 SaaS 产品 LobeChat Cloud 上用的技术平台选型吧： _202410
- https://x.com/arvin17x/status/1847627132891254803
  - https://x.com/arvin17x/status/1803761433714507850 /202406
  Serverless 部署：Vercel
  Server 部署：Railway、Zeabur
  数据库： Postgres Neon
  用户管理： Clerk
  文件/对象存储：Cloudflare R2
  数据统计： Google Analysis / Plausible
  邮件支持： Zoho
  SEO： GSC / SimilarWeb
  支付： Stripe
  这一套下来会有一些费用开支（几十刀/月），但能大大降低运维成本，体验非常棒

- Google Analytics 和 Plausible是一起用吗，还是选一个
  - 是一起用的。实际上看其实 GA 的数据更准， Plausible 的数据接近 GA 的两倍，但 Plausible 基本和 SimilarWeb 差不多

- vercel，clerk，neon 都是超出用量之后开销上升非常快的
  - 算过了能接受， ROI 划得来

- Clerk 和 authjs 对比有什么优势吗？一直在用 authjs 还没尝试过 Clerk
  - Clerk 是 Auth 的服务，给了一套解决方案，你接入了以后就能直接有一套完整的用户后台管理系统，可以直接看到各种用户活跃数据信息、设置白名单/黑名单、用户禁用等等操作，但相应的也需要付费才能启用所有功能。
  - 而 Authjs 只是一个 npm 包，它解决了 auth 集成的问题，但配套的管理的功能都得自己搞。
  - 我们在 LobeChat 中其实两种方案都集成了，如果是要体验最佳的话推荐接入 Clerk，如果要完全自主可控的私有化部署我们会推荐配置 next-auth（authjs 的 next 版）。

- supabase 包含的clerk和neon，且免费方案中给的活跃用户额度更高，为什么没选用呢？是有什么弊端吗？
  - 这个在我们一开始选型的时候专门对比过，以后有空可以展开讲讲，简单来说的话：虽然 Supabase db 和 auth 都有，但 db 不如 neon , auth 不如 clerk。

- ## 根据过去半年的观察，我认为 2024 年 Chat 领域的第一个交互范式应该初步成型了 —— 我暂且称之为 Chat Portal（对话模态窗）。
- https://x.com/arvin17x/status/1809847312187027628
  - 无论是最近大火的 Claude Artifacts， 还是上半年 ChatGPT 上线的 Excel 表格编辑、 Dall·E 图片改写，亦或是社区中去年就有的 ChatPDF 等，所有让人一眼亮的地方都在于超脱对话框的富模态交互方式。
  - 比起 chat， GUI 可以大大提升用户交互的便利性。但 Chat Portal 与纯 GUI 不用，用户又可以灵活地在对话与 GUI 中自由切换，灵活性极佳。
  - 因此我们在 LobeChat Cloud 中做了一个初步尝试 —— Cloud 专享搜索插件。用户可以采用对话的方式快速获取搜索结果，当需要进行深度检索时，又可以打开 Portal ，用搜索 GUI 重新搜索结果并总结。同时又可以将搜索到的内容发送回对话窗口中继续进行下一步的讨论。
  - 这个高级搜索插件会是 Cloud 独有的。不过这种富对话的交互模态已经在开源版中集成了，后续把 DallE 插件也支持上这种交互方式。

- Datou 老哥说的没错，叫成「富对话」更好
- 这就是富对话 对应原来的简单对话，直接有 ui。 同时有了对话的灵活和 GUI 的直观

- NotebookLM 也属于这个方向。

- ## GPT3.5没开源，但可以免费用了，无需注册
- https://twitter.com/nash_su/status/1774930531165315286
- 数据截止到22年，感觉贼落后
- 一开始就能免费用吧？不过现在是免登陆用了，更进一步了。

- ## 用 Excel 实现了一个简易的 GPT2，可以下载：不过特别大，有 1.25 个G
- https://twitter.com/vikingmute/status/1768452277600387161
  - [Spreadsheets are all you need.ai – A low-code way to learn AI](https://spreadsheets-are-all-you-need.ai/)
  - 用一个Excel 表格来学习 ChatGPT 的工作原理，不用写任何代码，配有三个Youtube 视频，非常形象。

- ## 👣 GPT 回答标准模板：
- https://twitter.com/kk_shinkai/status/1767841511516082470
  1、把问题用自己更啰嗦的语言复述一遍；
  2、大篇幅地介绍提问里那些你显然非常熟悉而且完全没问的背景概念；
  3、像当代大学生写有字数要求的毕业论文那样回答你的问题 (如果运气好的话偶尔可以从这部分里抠出来明明一句话就能说明白的答案)；
  4、一段仿佛是在凑字数的综述；

- ## Chat interfaces won't supersede GUIs for most purposes.
- https://twitter.com/msimoni/status/1732439305530851679
  - Clicking buttons/menus requires much less effort than entering text into a chat, esp. mobile.
  - Voice input won't fly because people use computers in public/social situations, and don't want others to hear what they're doing.

- ## 💡 Embeddings: What they are and why they matter
- https://twitter.com/simonw/status/1716449601505657224
  - [Embeddings: What they are and why they matter](https://simonwillison.net/2023/Oct/23/embeddings/)

- I've done some cool project with embeddings in computer vision a few weeks back
  - 三维示例
  - [Leverage Embeddings and Clustering in Computer Vision](https://blog.roboflow.com/embeddings-clustering-computer-vision-clip-umap/)

- ## AutoGPT现在超火，它是一个由开发者 Significant Gravitas 推出的项目，​可以根据用户设置的目标，​使用 GPT-4 自动帮助完成任务。
- https://twitter.com/duanzi/status/1647284362541662213
  - ​用户只需提供 OpenAI 的 API Key，​AutoGPT 就可以根据用户设定的目标，​采用Google搜索、​浏览网站、​执行脚本等方式帮助用户完成目标
  - utoGPT 最大的特点是突破了现有的 GPT 只能做文本方面的任务的限制，​可以利用各种工具来完成目标。​AutoGPT 背后接入的语言模型可以是 GPT-4 或 GPT-3.5 的 text-davinci-003。​作者的聪明之处在于将各种操作变成命令，​让 GPT-4 模型选择，​然后根据返回的结果进行操作
  - AutoGPT 使用了一些技巧确保任务完成地更加有效，​如使用列表保存历史发送的信息，​并在每一次请求token 允许的条件下发送最多的历史消息给 GPT-4。​AutoGPT 有很多用例，​早期用户已经能够使用它来做各种各样的事情，​包括通过手机生成软件代码和为网站生成 SEO 审计。​它还可以用作互联网搜索和规划
  - AutoGPT 可以完成的任务或者决策比 HuggingGPT 更强。​要运行AutoGPT，​用户需要 Python 3.8 或更高版本、​一个 OpenAI API 密钥和一个 PINECONE API 密钥。

- AutoGPT 的 GitHub 星标超过了 Bitcoin，只用了16天。 最简单的理解它的方式就是把AI当人了。 人最厉害的是什么？使用各种工具。 怎么使用工具？让LLM来当总指挥调用其他的API工具。 在哪儿找到工具？HuggingFace 不是有一堆模型吗。

- ## One of the biggest weaknesses of ChatGPT/LLMs is that it just tells you stuff but doesn't actually *do* anything.
- https://twitter.com/DavidKPiano/status/1636020080826896389
  - So the only jobs it will be able to replace are the majority of management jobs.

- ## 多轮问答跑了一天，目前效果很稳定，可以来解释一下是如何实现的了。
- https://twitter.com/xicilion/status/1647408696312602624
  - 问答通常的实现，embedding -> search -> llm，连续语义在第一步就丢失了。
  - 我的方案是在前面，**先让 ChatGPT 解释问题，返回关键词**，流程变为：explain -> embedding -> search -> llm。
- 两次 llm 会不会慢了点
  - 第一次几乎不推理，很快。
- 类似langchain conversational chain里面的CONDENSE_QUESTION_PROMPT，让llm先对用户的提问结合历史进行重新的阐述，从而提高搜索命中率
  - 去看了一下，确实很
- 感觉还是用llm转述问题会更好些，关键词任然会丢失语义，比如用户问一个没有关键词的问题。
  - 我对比了一下，效果一样。没有关键词也不会迷失，ChatGPT 会按照要求根据上下文补齐。
- 很好的思路，本质上就是通过对每句话进行句子表述上的补全，让每句话都是独立且完整的表述，保证了能进行可靠的向量搜索
- plugins 的思路也类似这样

# discuss-chat-format
- ## 

- ## 

- ## 

- ## 

- ## 目前 render AI chat history 有什么现成的三方库吗？就是我有一个 jsonl 文件或者 array of message 的数据，然后要根据不同的 role 把对话重新呈现出来。
- https://x.com/tison1096/status/2026837754882175150
  - 目前看最暴力的就是硬写一个 component 上不同的颜色，然后 message content 里用 Markdown render 出来。可能再加一个折叠。

- 加个 load more button，再加个搜索。vibe 也就十分钟的事

- pi-mono里都有, 看下share功能的实现，风格就是完全terminal，应该vibe下也没什么问题
  - 不过如果是分享的话，有个很重要的脱敏功能没有
# discuss-db-chat
- ## 

- ## 

- ## 一个轻量级的数据库管理工具：WhoDB，支持自然语言交互，不写代码也能查数据
- https://x.com/aigclink/status/1854436720957407697
  - 支持多种数据库，PostgreSQL、MySQL、SQLite、MongoDB、Redis、MariaDB、Elastic Search等
  - https://github.com/clidey/whodb

- 和chat2db相比哪个好用？
# discuss-ui-chat
- ## 

- ## 

- ## 

- ## 🆚 [研究了半天，觉得目前最好的AI客户端方案 _202512](https://linux.do/t/topic/1380309)
  - 前前后后装了Cherry Studio、Kelivo、DeepChat、各种CLI封装的GUI等app，也折腾了半天自建了LobeChat、Open WebUI、LibreChat、HiveChat、NextChat等云端web服务。
  - 最终对比下来，感觉综合最好的还得是LobeChat（虽然现在性能确实还是需要再提升点）
  - 首先像CS、Kelivo、DeepChat这类app，虽然做得都不错，各有优点，但是无奈要么不支持iOS、要么数据同步要靠webDAV（需要养成使用前先恢复的习惯，太麻烦了），在多端同步这块目前确实还是很难满足我的需求，只能pass了。
  - NextChat没有数据存储，只是一个网页代理，有点过于简单，而且好像也好几个月没更新了。
  - LibreChat配置麻烦，而且UI也没有看起来那么精致，体验了一会就卸载了。
  - HiveChat功能比较简单，一些联网搜索等细节功能做得不太行，也好像好几个月没更新了。
- 最终就剩Open WebUI和LobeChat里面选了，两个项目在PC网页，iOS的pwa应用体验上都有各自做得不错的地方，但是最终LobeChat还是在一些小细节上做得更好，让我忽略了它在页面响应方面稍稍的劣势。
  - 深度思考时会自动展开思考内容在一个固定的高度，能同时看到思考内容，并且也不会对主要恢复造成太大的干扰。owu要么就是折叠，要么就是展开所有的思考内容。
  - 模型配置类似cherry studio那种方式，交互更直接方便。owu需要在管理员面板里添加连接，然后再在模型里去配置，比较麻烦
  - 图片文件都是存在MinIO里面的，自己管理、备份什么的都比较方便，而且性能也更好。
  - 支持artifact，一些回复如果包含代码、md、mermaid、网页之类的可以通过产物快速的展示或者下载，比较方便，交互也很不错。
  - macOS上的客户端，可以直接连接自托管实例，体验又比网页提升了一截，只不过现在内存还是占用有点高，需要优化一下，哈哈。
- 最后希望LobeChat iOS app也能支持连接自托管实例

- 曾经有这想法， 但后来发现只是浪费时间，到后面都在处理 bug， 而且我会用一大堆工具，更不好搞， 现在以结果导向滚动式纪录还比较省心省力
  - 工具用得多的话，确实麻烦，这些开源项目迭代太快，bug 很多，不过如果就是常规的当做知识问答和搜索，还是不错的

- openwebui满足日常使用。可以用hf抱脸部署。
- 抱脸部署的稳定吗，是不是需要保活
  - 用uptime每天请求一下就行

- 我还是习惯用各家的网页版，然后如果真的有需要保留的东西我会手动备份一份到我的文档
  - 目前web端配合singlefile备份就是我的生产力场景

- 这一年半里用来用去，我觉得最稳定适合作为生产力工具的的还是claue网页端（除了贵还有额度少硬挑不出其他毛病），站里佬的公益api我一般配合视频总结工具平时杂耍用也蛮好的

- lobehub 2.0 next 分支已经很流畅了，除了几个特别的页面

- cherry studio功能基本上是天花板了，不过最大的两个问题就是：
  - 1. 功能越来越多，内存占用越来越大，对于小内存的Mac用户来说不太友好。
  - 2. 移动端迟迟不正式发布，多端也无法实时同步。

- ## 💄🤔 A2UI ---「AI 自动生成 UI」, 这个项目初看神奇，实际上是个死胡同。
- https://x.com/brucexu_eth/status/2001784942486081774
  - 本质上就是做一套动态 UI 渲染引擎，将网页和交互使用 JSON 等其他结构化的语言描述，配合 React 组件库实现无代码生成应用，甚至可以动态调整 UI。只不过当年需要拖拽或者人工编写 JSON，现在 Google 用了 AI 生成。
  - 为什么说是死胡同呢？如果你做简单的页面和交互，这个肯定没问题，但是多少复杂一点的业务和定制化需求，就完蛋了。因为 JSON 不管你怎么设计数据结构，能表示的交互和功能永远无法达到 HTML + CSS + JS 代码组合所能实现的。也就是说针对真实自定义的需求，要么你生成一个无比复杂的 JSON 和渲染引擎去解析；要么降级需求只能用你限定的框架和功能；要么直接生成代码，现在生成代码并不复杂了。
  - 所以当年那些低代码尝试在我看来比较鸡肋，要么你就是生成纯 UI 加简单 form 交互，例如：wix；要么你就是高度定制化的组件，针对特定业务场景例如问卷生成来自动生成，例如各种 form app。

- 如果是类似http://v0.dev的方案呢，感觉他们生成的UI挺流畅的

- 还有人记得 imgcook 吗

- 现在应用场景变了，UI的目的和呈现逻辑也变了，你担心的问题应该不存在了

- https://x.com/dotey/status/2002080595665371575
  - AI 动态生成 UI 这个方向是没问题的，技术上不是当年低代码那套思路和技术方案了，也不需要 JSON，直接动态生成 HTML/CSS/JS 就可以了。
  - 动态 UI 不需要满足所有场景，适合那种即用即走的场景。
  - 另外现在动态 UI 其实有两个主要方向：
  - 一个是 Google 的完全动态生成的 UI，这种灵活度高，稳定性差一些。
  - 另一个方案是 OpenAI 正在做的 ChatGPT App，它其实是一个个做好的小程序，按需调用，比如你要订酒店，不需要跳出 ChatGPT，在聊天窗口会有个订酒店的小程序跳出来，根据你提供的信息填充好信息，你自己修改确认一下就可以完成酒店预订的操作。

- 一种模式是GUI完全由通用agent自己按需动态生成，其中A2UI这样的只能生成「DSL」组装预制好的组件，GenTabs这样的能生成真实代码得到相对任意的GUI，但共同点都是第三方应用（Tool或垂直Agent）无法掌控GUI、无法实现那些依赖GUI的用户价值
- 另一种模式是MCP-UI：
  - GUI由通用 agent 基于第三方应用（MCP App）声明的GUI素材（HTML模版、URL、或组装原生组件的DSL描述）来按需生成，且生成的时候必须遵循Web标准等规范，第三方应用（Tool）能包含GUI，能对面向end user的GUI有一定掌控、能实现更多用户价值。ChatGPT最新的App商店里就都是这种

- ChatGPT App的UI不是自动生成。现实现方式，是引入mcp方来提供的预制ui模版（可包成js包放npm），以一个iframe来展示。 chatgpt从mcp里取出数据后填充到（这里的填充也不是智能填充，就是实现定义好的字段）这个iframe里。 至少现在这个阶段，整个ui是没有任何组合性。外加有各种权限限制，比tg小程序自由度还低。

- 我都没把这个当作是技术问题，就是头部生态布局抢占用户心智，做标准定义

- 每一代人都有自己的低代码

- 生成JSON有好处，因为JSON相当于定义描述界面要生成的东西，可以给大语言模型一个schema约束，这样子成功率更高。如果直接从NLP到UI界面的话，成功率会比走JSON，再转UI稳定性低

- ## 🆚 [Librechat vs openwebui : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mmh6k8/librechat_vs_openwebui/)
- Personally I prefer to use inference engines like vLLM because the speed is incredible and I find their openai compatibility is often the best on the market (especially around tool calling), and there is no built in UI in vLLM.

- My biggest complaint with Open WebUI is that it is very bloated. A full deployment is like 3.5 GB without any user data. It installs a million Python dependencies that are completely unnecessary for most use cases. That being said, it works well.

- ## 🆚 [OpenWebUI vs LibreChat? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1l0bc5j/openwebui_vs_librechat/)
- I've used both quite extensively and found OpenWebUI to be a lot easier to setup, update and maintain. Adding new endpoints and models is also quite a bit easier as well since you can just do that through the web ui.

- I still use Oobabooga, but I tend to plug its API into Void and OpenHands for agentic stuff.

- ## [Ollama's new app | Hacker News _202508](https://news.ycombinator.com/item?id=44739632)
- OpenWebUI refuses to support MCP and uses an MCP to OpenAPI proxy which often doesn't work. If you don't like or need MCP, then it is a good choice. The dev is very opinionated

- ## a quick prototype sprint on an LLM chat interface
- https://x.com/argyleink/status/1949966641233531030
  - https://codepen.io/editor/argyleink/pen/wBKWNwQ
  - view transitions
  - readablestreams
  - flow control

- ## [What LLM frontend you are using ? : r/LocalLLaMA _202404](https://www.reddit.com/r/LocalLLaMA/comments/1cdk5nr/what_llm_frontend_you_are_using/)
- LM Studio - When I just want to start chatting right away without any technical hassle.
  - Text Generation Web UI - When I want more "advanced" features.
  - I have also coded my own very personal chat front end for very specific use cases, for example when I want to chat with an local LLM on my phone by connecting it to my PC that runs the heavy model.

- I wanted to use RAG features, and models that were set up for specific tasks, so I plugged into Anything LLM, and that is also very user-friendly, and has fast vector searches

- I use discord as a GUI. Also, the bot supports multiple simultaneous users with permanent memory and RAG. No goldfish syndrome. Remembers info from outside the context window, while keeping context below 32k. https://github.com/DataBassGit/AssistAF
# discuss-chat-dev/server
- ## 

- ## 

- ## 

- ## 🆚 [OpenWebUI vs LibreChat : r/selfhosted _202503](https://www.reddit.com/r/selfhosted/comments/1jltdjq/openwebui_vs_librechat/)
- I will give you two somewhat conflicting answers; 
  - Hands-down Open-WebUI is far easier to deploy and support and lowest cost.
  - Open-WebUI is client heavy, bogs down and has extremely high network utilisation (annoys mobile phone uses). Entire conversation is held in the browser, lots of back and forth and images are stored in the single json payload. Although easier to setup there is no real database design, limited indexing, and real no database design. As such both the main application and vector databases grow and will get bloated. Moving to Postgres helps, but doesn't address the fundamental lack of database design\indexing.
  - b) Hands-down LibreChat provides a closer ChatGPT Plus style experience and is FAR easier to use.  Open-Webui development stick closely to their own guardrails and principles, as such far slower to adapt new features. eg: LibreChat users can use MCP servers\features. Where as Open-WebUI devs have stuck with the OpenAPI approach (great idea, but only 1% of the real-world use case), when all the popular agents are MCP. LibreChat seems to support image generation and editing within chat, without add-ons Open-WebUI can only create images. Much better code-interpreter experience however you need to PAY\SUBSCRIBE but absolutely worth it.
- LibreChat supports all the common providers out of the box, Open-WebUI just supports OpenAI compatible providers, everything else you need middleware or pipelines.
- 🐛 Common downsides with both these are
  - No native iOS\Android applications (Open-WebUI works as a PWA app)
  - No advanced voice
  - Both lag with new features (eg: Advanced Imaging), yes that is expected but of note.
  - Tool usage is clumsy at best on both

- For some reason chat apps like using stupid database choices. At least OpenWebUI on Postgres won’t lose your data.
  - LibreChat uses… MongoDB. In 2025. Yep.

- OpenAI-compatible APIs clearly won out as the standard. Even Google provides an OpenAI compatible endpoint for Gemini.

- In LibreChat, if you want to add an OpenAI API key, where would you add it? The file .env of course! And if you want to add an OpenRouter API key, where would you add it? The file librechat.yaml of course... wait what? ... Yes, the configuration system is that badly incoherent.

- ## [Best way to start Open-WebUI server from software? : r/OpenWebUI _202504](https://www.reddit.com/r/OpenWebUI/comments/1k1er0s/best_way_to_start_openwebui_server_from_software/)
- Docker is the way. You're nailing it with the env var idea.
- if you're using python why not pip install it and then just run it?

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [完胜3款同类AI聊天工具！群晖部署OpenWebUI小白教程 - 知乎 _202503](https://zhuanlan.zhihu.com/p/32145475986)
- OpenWebUI 更多是用来结合本地部署的大模型来使用，不过它也支持 OpenAI 格式的API。
  - 多用户管理功能，且可以自定义用户访问到的模型范围
- NextChat
  - 项目目前已接近停更状态。虽然 NextChat 的部署过程非常简便，却存在不少问题：功能添加新模型的步骤复杂，用户分享机制过于基础，整体来看并无明显竞争优势。

- ## 对于大语言模型来说，它是没有记忆功能的，也就是每一次你必须发送给它所有的历史会话内容，也就是每次发新消息都会把历史消息一起发送过去。
- https://x.com/dotey/status/1856437700225532234
  - 但是这样一直累加就会超出最大上下文窗口长度，并且会让会话的成本急剧上升，毕竟内容越多，需要消耗的算力越大。
  - 所以对于  AI 聊天应用来说，在几轮会话后会自动对历史会话进行摘要，只保留最近的几次会话。这也是为什么你和 AI 聊的多了，它可能会忘记前面聊过的内容。
  - 复杂一点还会对消息历史做 RAG，根据新的聊天问题去检索历史消息

- 如果要有记忆功能，需要应用自己用类似MemGPT这样子的工具实现。

- ## chrome is bringing ai directly to your browser with `window.ai` ! it runs locally, works offline, & it's fast
- https://x.com/nicoalbanese10/status/1806377270518391177
  - it's compatible with @vercel AI SDK, so you can start building with it today
  - try it out with our open-source @nextjs chatbot
- Just use Page assistant from Ollama repository on chrome white Powerfull features

- ## gpt 4估计小调了一些agent场景，最近一些本来就需要交互的问题上，它开始表现的更像一个agent。
- https://x.com/SuJinYan123/status/1801839116189110590
  - 比如我让它写一个python读取csv然后用lru跑命中率，它没有直接给我代码，先问我数据文件路径，然后缓存大小。
  - 还有数据处理，能自动执行，然后根据报错，自己分析一下，然后改代码，然后继续执行，细看代码还写得蛮不错，理解了我的意思。体验很好啊。

- ## https://kimi.moonshot.cn 推荐一个号称国内最强 ai， 超大上下文，还免费。谁了解这家公司的
- https://twitter.com/huangjinbo/status/1768443353417560520
- 公司： 月之暗面科技有限公司（Moonshot AI）
  - 杨植麟 - 法人代表、主要创始人。杨植麟曾在清华大学计算机系学习，并在卡内基梅隆大学攻读博士学位，师从苹果公司AI负责人Ruslan Salakhutdinov和Google AI首席科学家William W. Cohen。他在自然语言处理（NLP）领域有着显著的贡献，包括发表有影响力的论文如Transformer-XL与XLNet，并在Facebook AI Research和Google Brain有过工作经历
  - KimiChat ，联网搜索和文件总结能力在中文场景确实很好用。 

- 这家公司前不久融了1b
- 好像里面很多人来自谷歌，创始人是90后，昨天输入三份PDF测试，实测kimi产品上下文能力，超过gpt和Claude了，gpt长了会截断，claude 直接提示超长，kimi正常解答还是对的

- ## RAG 路线确实是最可行的了，相当于把审核工作和成本 delegate 给了别的厂商，自己坐享其成。
- https://twitter.com/laike9m/status/1768537063392231714
  - 不过未来说不准会吃版权官司。
- 目前kimi差不多是想bing那样用得最多的是知乎的数据。另外公众号数据最值钱了，要是大家都反应过来走RAG线路，腾讯最后是赢家。

- https://twitter.com/laike9m/status/1768456246154379647
  - kimi目前效果很好了，走的是perplexity路线，先检索过滤过的互联网内容，然后补充AI生成，就是RAG路线。一是减少幻觉，二是直接用网络资料增加中文理解，吊打文心。这个路线真实天才。

- ## [Vanna.ai: Chat with your SQL database | Hacker News_202401](https://news.ycombinator.com/item?id=38992601)
- All these products that pitch about using AI to find insights from your data always end up looking pretty in demos and fall short in reality. 
  - This is not because the product is bad, but because there is enormous amount of nuance in DB/Tables that becomes difficult to manage. 
- I couldn’t agree more. I’ve hooked up things to my DB with AI in an attempt to “talk” to it but the results have been lackluster. Sure it’s impressive when it does get things right but I found myself spending a bunch of time adding to the prompt to explain how the data is organized.

- We did something similar for our reporting service which is based duckdb. Overall it works great, though we've ran into a few things:
  * Even with low temperature, GPT-4 sometimes deviates from examples or schema. For example, sometimes it forgets to check one or another field...
  * Our service hosts generic data, but customers ask to generate reports using their domain language (give me top 10 colors... what's a color?). So we need to teach customers to nudge the report generator a bit towards generic terms
  * Debugging LLM prompts is just tricky... Customers can confuse the model pretty easily. We ended up exposing the "explained" generated query back to give some visibility of what's been used for the report
- Our primary issue is that our DB is a dynamic Entity-Attribute-Value schema, even quite a bit denormalized at that. The model has to remember to do subqueries to retrieve "attributes" based on what's needed for the query and then combine them correctly.
  - NLQ is a somewhat new feature for us, so we don't have a great library to pull from for RAG. Experimenting, I found that having a few-shot examples with some CoT (showing examples of chaining attributes retrieval) sprinkled around did help a lot.

- ## ChatGPT-Next-Web 这个项目太好用了，
- https://twitter.com/_Xheldon/status/1731897455145263340
  - 部署在软路由上，Docker+内网穿透+腾讯云 Nginx 转发（不是必须），给不会翻墙的亲友每人一个访问密码，太赞了！
  - 我二开增加了腾讯云 log，简化了界面复杂配置，比我之前搞的微信小程序好用多了，早知道有这个就不折腾小程序了
- 想问下你內网穿透用的什么方案，我用的 taikscale，给其他人用还得给他们装客户端
  - tplink 路由器自带的，免费用

- ## Anyone figured out the most useful format to feed documentation into a GPT Assistant yet?
- https://twitter.com/simonw/status/1721714675182899509
  - I've tried PDFs but I'm interested in the optimal format, ideally supporting returning citation links if possible

- currently i'm preprocessing PDFs into markdown in chunks, I am putting the filename as a header within each file's chunk. I have had the best luck so far with GPT & markdown, will let you know when i've had a chance to play more

- ## Many startups just died today. Because OpenAI added PDF chat. You can also chat with data files and other document types.
- https://twitter.com/thealexker/status/1718445317559902371

- ## 目前市面上“用户提供 PDF 文件，得到一个专向 AI 聊天工具” 的产品，哪个效果最好？
- https://twitter.com/taresky/status/1693112350075965841
  - ChatGPT Code Interpreter 无法顺利阅读 PDF，有第三方插件好用吗？
  - Chatpdf 回答质量很低。
  - Chatbase 还不错，有没有更好的？

- copilothub 好像针对 ocr 做了一些公式/图理解优化，可以试试？
- gptbase.ai 不支持理解图片内容，其他大概满足需求

- ## 借鉴 `json/yaml/toml/markdown` 设计，搞了个 pdl 格式（Prompt Description Language），并相比于其他格式，可以最大化节省 Token 数量。
- https://twitter.com/blackanger/status/1659826017341702146

- ## 今天跟一位朋友讨论为什么国产的AI产品已经沦落到到免费都没人去用了，原因总结下来是两点：
- https://twitter.com/oran_ge/status/1653753194206601216
  - 我的覆盖群体基本人手 ChatGPT/Claude
  - 玩 AI 太多有种疲惫感，阈值拉高了，很难兴奋起来
- 我拿我的专业最基本的知识问文心，十次里有五次是胡言乱语，都不能算是幻觉了，就是那种你哪怕去百度搜索引擎查都能一秒找到答案的概念，他会瞎说
- 国产的 AI 对提升生产力帮助并不大

- ## is anyone else getting sick of chatbots?
- https://twitter.com/Wattenberger/status/1653045107266924545
  - I wrote down a few thoughts on why chatbots are not the future of interfaces and how we can be more thoughtful
  - [Why Chatbots Are Not the Future](https://wattenberger.com/thoughts/boo-chatbots)
- Great post. I think the point about “hard to read edits without a diff” can be generalized too: plaintext is a suboptimal data viz for so many LLM outputs.
  - We need diff views, weather widgets, mini maps, 2x2 charts
- Two cons of using chat bot in async user feedback/bug report:
  - (1) users expect real time response. If you don’t have enough CS resource, it will damage the expectation of users
  - (2) scripted + automatic responses make things worse. Users just want to hit that “talk to human” btn

- Agree! I think chat corresponds to stage we are in. Many folks feel alone/remote in their daily work & chat feels connective.
  - I like the concept of a toolbar of Code Brushes - but it lives very unnaturally in the UI right now
  - totally agree ❤️ Brushes was a really rough initial exploration, but someday I'll fix up the ui and it should work its way into other GH experiments!

- I _hate_ when chatbots are used as customer support, and there is no option available to just talk to a human

- Code Hike `<Chat/>` prototype (it's the UI, not the AI)  

- Yep. Chat is not the right interface for AI. It has the same discoverability problem as voice assistants and the terminal — it’s hard to learn the capabilities of the system without trial and error or reading a manual. Eventually the tech just will be integrated into real UIs.

- ## 这几个月一直都没找到 Infra 里面有什么可以真正利用 LLM/ChatGPT 的场景
- https://twitter.com/xxm459259/status/1650713723235885056
- 给彩笔工程师每人发个账号…目前看起来这个比任何其他的都好使。
- 写邮件给老板们吹自己 impacts
- LLM-based FAQ
- 在 postmortem 中甩锅，在 newsletter 中邀功

- ## 并不那么Open的AI生态挑战者可能已经来了：@huggingface开源了自己30B参数的chatbot（不仅仅是模型），
- https://twitter.com/cryptonerdcn/status/1650952444745240577
  - @NVIDIAAI的研究者盛赞如果chatgpt是苹果，那么HuggingChat之后的生态环境可能就是安卓。（注意这不是之前公布的HuggingGPT，那是用来协调各种模型的）

- ## 帮助我最多的 5 个技术相关 ChatGPT Prompts：
- https://twitter.com/Tim_Qian/status/1650733864510459905
  1. 生成正则表达式
  2. 生成 Cron 表达式
  3. Tailwindcss 专家
  4. 英语老师
  5. 帮我写 SQL

- ## 其实之前不仅仅关注LLaMA生态的一些开源大模型，国内的一些开源大模型也在关注，这里分享几个最近挺火的LLM。
- https://twitter.com/xinqiu_bot/status/1645616019103428609
- https://github.com/THUDM/ChatGLM-6B
  - 开源的、支持中英双语的对话语言模型，基于 General Language Model (GLM) 架构，具有 62 亿参数。
  - 结合模型量化技术，用户可以在消费级的显卡上进行本地部署（INT4 量化级别下最低只需 6GB 显存）
- 除了基于GLM的ChatGLM，另一种基于RNN的ChatRWKV

- ## Is it fair to think of LLMs as a database with a natural language query interface? Where does the database metaphor break?
- https://twitter.com/dvassallo/status/1644914034905579526
- The most interesting counter-argument is that LLMs seem to be practically **👀 read only**. There’s only short-term memory (so far), and no insert/update equivalent.
  - The rest still seems to stand. There’s data, a query, and a result derived from the data and the query algorithm.
- LLMs create data in response to queries, unlike traditional databases which simply retrieve data.

- ## AskBend 所有训练数据都是英文的文档，但是它可以非常自然的使用中文来回答。有没有朋友科普一下为什么🥵，不同的语言输入对于 embedding 的计算没有影响吗？
- https://twitter.com/redsun_diamond/status/1643904510883135490
- 没影响，因为是基于语意的不是基于语言的。【virtual thread】和【虚拟线程】 这个两个词的embedding差不多，余弦90%的样子。
- 没影响，中英文embedding后在同一个vector space
- 多语言的embedding模型是相互关联的。比如中文的我有一个苹果和i have an apple的embedding的相似度数值是很高的
- 因为第一层和最后一层都走的 openai, embed 走的是 open ai 的 text-embedding-ada-002 返回数据库查找是根据你的语言返回 vector 而这个 vector 的拿回的 text 也是用来问 openai 的。所以语言在这里相当于走的 openai 的 embed 猜测不同语言在 vector 里算 distance 是有差异但不是那么大的。
- 要分开来看，普通句子的差别不大的。但是一些复杂场景下的中文预料就不一样了。比如，你见到一个仇人，你问她，你吃了吧？跟你见到一个你喜欢的人，你问她，你吃了吧？所以还是要用针对性的语料进行训练吧。然后大模型神经网络本身也很容易一通百变的，到输出的时候只是组合单词

- ## 文本模型爆发比图像晚了大约半年，所以那边发生的事情这边貌似在重新发生一次…从那边可以知道的经验至少是：prompt不会成为壁垒
- https://twitter.com/virushuo/status/1632405930015899648
- 开源模型会大力度搅局。 一部分人疯狂 hack 只是为了好玩，另一部分疯狂想着快速收割韭菜。 
  - 闭源有点自研的AI商业应用的生命周期可能只有几个月。API套壳的更可能是以周计算的。更别说 prompt 了。
- 对于我来说，壁垒是算力，毕竟图像要本地计算足够才好玩
- 那什么是壁垒？还是数据？

- ## 搜索引擎的范式转移 PageRank -> ModelRank
- https://twitter.com/Tisoga/status/1623916651996680193
- 对话式 AI 目前最显著的一个问题就是没有信息引用来源，这有很大的安全隐患！大规模语言模型并没有像人类大脑这样创造知识结构，而是训练数据源的神经网络权重，虽然提升参数规模可以神奇的产生语言逻辑的抽象概括能力，但这毕竟不是通用智能
