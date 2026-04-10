---
title: thread-pm-app-kickstarter-coding-devops
tags: [coding, devops, kickstarter, thread]
created: 2024-06-08T10:26:37.496Z
modified: 2024-06-08T10:27:08.423Z
---

# thread-pm-app-kickstarter-coding-devops

# guide

# discuss-stars
- ## 

- ## 🤼🤔 Cloning any random piece of SaaS is something that could already be done before agentic coding, and the economics of it haven't changed meaningfully. 
- https://x.com/fchollet/status/2025283590972756284
  - Before, writing the clone would cost 0.5-1% of the valuation of the legacy SaaS company. Now it might be 0.1%. 
  - It doesn't make a difference -- if you can pull it off profitably today you could also have done it profitably in the past.
  - The code is a very small part of the process of making such a clone successful, and the reason legacy software has often bad UX is not because code was expensive to write.
- I genuinely think "code is now much easier to write and features are much easier to ship" strictly benefits legacy SaaS because it addresses their main weakness
  - The main threat to legacy SaaS is other legacy SaaS trying to move horizontally into their space because it is now easier to do so
- Circa 2012 you had a lot of devs "cloning Twitter" as a weekend project. Reproducing the UI and features of any app was never difficult and was never particularly valuable.

- I agree with this, and it explains why Meta would spend billions of dollars acquiring competitors rather than just building it themselves, which they could have done so easily.
  - However, I think there are examples of software which are just genuinely very difficult to build, even now with Vibe coding. It would still take many years to vibe code Adobe Photoshop, DaVinci Resolve/Fusion, or Unreal Engine again from scratch, even if you knew exactly "what" to build, and mimicking anything means you don't understand it in the same structural/phylogenetic way -- so you won't be able to creatively evolve it. 

- the workday example is perfect. google could clone it in a week. they don't because the value isn't in the code, it's in the compliance templates, the audit trails, the integration with 500 payroll providers, the decade of edge cases baked into business logic. vibecoders cloning saas UIs are solving the easy 5% and calling it disruption.

- Exactly. Code has never been the moat. Distribution, data network effects, switching costs, and trust are. Agentic coding lowers build cost, but it doesn’t magically give you customers, integrations, or brand credibility.

- The moat was never the code. It was distribution and switching costs. That math still holds.

- Problem of SaaS is not cloning. Their problem is that now I do not need many SaaS at all. I can just build things for myself or as internal tools for the company way cheaper than it was before
  - The reason people pay for SaaS is not just because of the effort of development

- ## we’ve found a clear way to make a project stand out and gain traction.
- https://x.com/GithubProjects/status/1905901281165648204
1️⃣ A Killer README is Non-Negotiable
2️⃣ A Strong Visual Identity Helps
3️⃣ A Live Preview Builds Trust
4️⃣ Localization Expands Your Reach
5️⃣ Easy Deployment = More Users
6️⃣ A Roadmap & Contribution Guide Keep It Alive
Bottom Line: Success isn’t just about good code. It’s about presentation, accessibility, and ease of contribution. Nail these, and your open-source project might just be the next big thing.

- ## 💰 I think more open source projects should have a commercial clause. 
- https://x.com/threepointone/status/1799424997946986899
  - If you can’t figure out how to extract value from your own labour, then you should rethink why you’re doing it. 

- I suppose an alternative is "open core"

- I recently found out that ag-grid, the fancy spreadsheet component, makes $20 million in revenue per year and charges $999+ per developer. I was like “wtf am I doing giving stuff away for free?”. Wild!
  - Yeah that things used all over institutional financial apps. High performance grid for trading desk apps etc, those things could be updating a table of 200 items with an update every row a few times a second. People will pay for that

- We’re working on a new brand called Fair Source that is basically this. http://fair.io 
# discuss-pm/shwocase-coding-based 🌰
- ## 

- ## 

- ## 

- ## Anthropic 在 AI 模型 2B 这个领域，1000 家年化消费超百万美元的大客户 _202604
- https://x.com/shao__meng/status/2042152822691782661
- Claude找对了发展方向，企业才是能真正给钱的大户

- ## [Cursor Revenue Leak: $2 Billion Annual Sales Rate : r/cursor _202603](https://www.reddit.com/r/cursor/comments/1rjqupl/cursor_revenue_leak_2_billion_annual_sales_rate/)
  - Cursor, the AI coding assistant startup led by CEO Michael Truell, has reached a $2 billion annualized revenue run rate as of February 2026, doubling its revenue in just three months. 
  - Roughly 60 percent of revenue comes from corporate customers, including new enterprise clients and expanded seat purchases from existing ones.
  - Founded less than five years ago, Cursor is now one of the fastest-growing startups ever and was valued at $29.3 billion in a November funding round led by Accel and Coatue. 
  - The company recently released an update allowing its AI to autonomously implement code, test it, and record its workflow. 
  - Its product has helped popularize “vibe coding, ” where developers use simple prompts to generate complex software with AI handling most of the execution.

- “leak”, they are just trying to raise new funding.

- I’m curious was their current losses are.
  - Everyone is, but of course AI companies only “leak” their ARR

- Antigravity is far less polished, and that's a fact. Also, the way Google quantize the models they serve via the app is kinda shameful. No wonder Cursor is better.
  - Gemini CLI is also half baked. A lot of their stuff is, honestly.

- I ended up cancelling recently. The CEO latest x post about moving away from tab complete towards cloud agents gave me a bad taste. I'm going to try the $10 copilot tier for a month.

- They likely pay tons of $$ to their AI providers (Claude, OAI, Google) so is that gross revenue or net revenue? And that's a high valuation when Anthropic could just ship an IDE fairly easily and crush them.
# discuss-toolchain
- ## 

- ## 

- ## 

- ## 🤔 [为什么还要让AI写高级代码 _202602](https://linux.do/t/topic/1620666/5)
  - 虽然 AI 对于高级代码喂的内容比较多了，但是为什么不直接让 AI 写汇编等更底层的，然后去运行，之前有人用 AI 写了个新的编程语言虽然很差。但是如果让 AI 写很高级的很长的 java 代码，还要理解 java 的 spring 什么的架构不是很麻烦嘛，况且他还要知道 sdk 或者各库的最新版本情况什么的。

- 因为高级代码足够多？没试过语料只给 asm，但我猜训练效果会惨不忍睹
- 简单来说就是因为训练数据的问题，那些汇编语言数据量太少而且太陈旧，并且很多都是严格保密的代码。 而且按照现在模型 6 个月一更新的节奏来看，其实你 SDK 的更新速度比不上模型的迭代速度，正常来说一个项目都是按年来规划的，所以不担心这个问题。 还有一点就是利用高级语言可以更快产出并且迭代产品，没有商业价值的东西没有谈论的必要

- 以 transformer 为代表的 LLM 真正闪耀的的地方就是对抽象概念的理解，而高级语言处于抽象层级的较顶端。

- 因为搓汇编 AI 依然需要理解 PE/ELF 的结构，依然需要知道最新版本的 libc 和 kernel32 库和 sdk
  - 现在高级语言都能跑飞，直接搓二进制这种要较长时间记忆跳转相对偏移和寄存器状态的，我都不敢想会出来一坨什么东西
  - 哦单凡哪里错了几个字节，gdb 调试的时候更是能直接放在地狱做某一层刑罚

- ## Vue & Vite+ 作者 尤雨溪 @yuxiyou 创建 VoidZero 拿下 1250 万美元 A 轮融资
- https://x.com/AppSaildotDEV/status/1984616482152857668
  - 尤雨溪 应该是目前融资金额最高的个人开源作者之一，也可能是全球第一。
  - 下一步计划：🦀 用 Rust 重写前端工具链。

- 融资由 Accel 领投，还有一大票优秀公司的创始人都投了：
  Tom Preston-Werner（GitHub 创始人）
  Eric Simons（StackBlitz 创始人）
  Paul Copplestone（Supabase 联合创始人）
  David Cramer（Sentry 联合创始人）
  Matt Biilmann & Christian Bach（Netlify 联合创始人）
  Sébastien Chopin（NuxtLabs 创始人）
  Johannes Schickling（Prisma 创始人）
  Zeno Rocha（Resend 创始人）

- laravel 融资了 5700 万，也是从 Accel 拿的钱，创始人最喜欢的就是兰博基尼
# discuss
- ## 

- ## 

- ## 

- ## Astral has entered into an agreement to join OpenAI as part of the Codex team. _202603
- https://x.com/OpenAINewsroom/status/2034616934671724639 
  - https://x.com/astral_sh/status/2034622016049860869

- ## 来自中国的硬件团队的这个 PicoClaw ，把 OpenClaw（前Clawdbot）用 Go 彻底重构了
- https://x.com/chuhaiqu/status/2023244280903663878
  - 直接把 AI Agent 的硬件门槛打到了地板，内存占用不到 10MB，启动仅需 1 秒。以前得用 Mac Mini 跑的服务，现在 9.9 美元的开发板或者树莓派就能跑。
  - 不仅保留了核心功能（写代码、联网搜索、Discord/Telegram 聊天），还加入了安全沙箱。
  - 最骚的是 官方宣称这套架构迁移 95% 的代码都是 AI 自己写的
  - https://github.com/sipeed/picoclaw

- 我现在在 Mac Mini 上跑 OpenClaw，光 Node.js 就吃不少内存。Go 重构后 10MB 内存 + 1秒启动，这意味着树莓派集群跑多 Agent 完全可行了。

- 好多朋友问为啥不用 Rust，官方给出了答案，简单来说还是因为 AI 更擅长 Go。

- rust入门门槛更高，训练ai的样本略逊少一点

- 不是AI擅长Go，是Go适合claws这种网络应用类型

- ## [【6k star 开源】屎山代码检测器 fuck-u-code，看看你的项目能拿多少分 ](https://linux.do/t/topic/1619511)
  - https://github.com/Done-0/fuck-u-code

- ## [Ask HN: what are examples of successful "open-source alternatives"? | Hacker News _202407](https://news.ycombinator.com/item?id=40848998)
  - It seems like every day there's a Show HN post for another "open source alternative" to a popular SaaS app.
  - this search shows 34 pages of results, with clones of everything from Notion to Jira to Hex to Figma to Carta. https://hn.algolia.com/?q=open+source+alternative
  - succeeded as in "has a large user base" or as in "makes a lot of money"

- no one mentioned LibreOffice yet? 200 million active users (!) seems like it's successful enough. 

- I think the market share of ublock Origin helped limit the success of so-called "acceptable ads" schemes, where adblock makers took money for excluding certain ad providers.

- OBS Studio - I found this to be a very valuable and successful application for video and audio editing, with some amazing companies sponsoring them.

- GitLab is definitely the most obvious success at $600M+ in revenue, but a couple new ones are Cal.com and PostHog.

- GitLab, Mattermost, RocketChat would be a few good examples of products that began as OSS alternatives to well-established players.

- Blender didn't start as open source.

- Reports from large bodies of users is they are very happy with https://OnlyOffice.com which some clients are on to avoid GSuite

- It looks like baserow (open source alternative to AirTable) is making a fair amount of income.

- ## WeChat、WeTerm，IDE叫WeCode好了
- https://x.com/stephenzhang233/status/1906025084445454836

- ## http://Bolt.new 让我意识到了降维打击教育行业的巨大潜力。本意是让开发更容易，随着 base model 和产品力的提高，过不了多久就会把教育行业的图像绘制能力顺带给打崩了
- https://x.com/lyson_ober/status/1852448467945210061
  - 之前 Claude Artifacts 让咱看到这种力量，而 @stackblitz 这种项目级别的输出无疑让我们提前窥见了未来
  - 更好的模型和十倍的推理速度是我们所需要的。人不仅没办法一目十行，也没办一下写十行。

- 教育行业的图像绘制能力是啥意思？
  - 我的意思是利用代码绘图 = 现有所有的库都能加以利用。教育行业的图像绘制是说上课的时候手动绘图讲解某些知识点的能力，或者提前做好放在 Slides 里的图像，以及下课后追问、因材施教时绘图解惑的场景。反过来说，教学者也能用好这种能力进行教育，而现有的教学和素材准备模式将被更好的方法替代。

- 期待Framer AI了

- ## 作为开发者，你可能只需要@devv_ai一个工具就够了
- https://x.com/forrestzh_/status/1798891748753908058
  1. 支持自定义模型，登录用户可以每天免费使用一定次数的 GPT-4o
  2. 使用 Web Mode（联网模式）获取最新、最准确的答案（基于 Devv 构建的垂直领域的 search index）
  3. 使用 GitHub Mode 深入理解一个代码仓库的功能、原理、设计
  4. 使用 Chat Mode 进行技术方案的撰写、长代码的重构（解决了很多用户需要重复订阅 ChatGPT & Devv 的问题）
  - Devv的竞争优势在于：第一，产品能力比模型能力更重要，用户实际使用的是产品而不是模型。Devv区别于Perplexity的地方在于Devv刻意模糊了底层使用的模型  
- 客户端其实就是用 Pake 打包了一下，会随着网页自动更新的，Google 登录的问题我们来看一下（也有可能是您这这边的网络问题，可以切换一下其他网络）。

- 每次一发布session就失效，session数据放在服务端内存了😝
- 出桌面端和 IDE 插件吧
  - next step
- 有个建议，每次搜索，等待结果的时候，那个回答下面的灰色部分界面感觉不是很美观。
- 聊天模式，跟直接使用 gpt4 有什么区别吗？
