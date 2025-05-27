---
title: lib-ide-cursorai-community
tags: [community, cursorai]
created: 2024-05-14T03:19:08.192Z
modified: 2024-09-02T02:28:27.398Z
---

# lib-ide-cursorai-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [为什么我觉得 AI 写代码纯属添乱? - 知乎](https://www.zhihu.com/question/590636216)
- 首先我是Copilot重度用户, 有Copilot的白嫖使用资格, 在仅支持VSCode时使用的比较少, 在Visual Studio 2022有copilot插件后, 基本是每次代码必用, 我日常基本使用C语言，总结一下copilot写C代码的一些特点:
  - 第一、如果说Copilot的代码能用，当且仅当Copilot写的代码刚好是你想写，想这么写，你写出来和Copilot的生成的代码基本一样的情况，你必须审计并清楚的知道生成代码每一行的所有细节及意义，这个代码才能够使用。如果靠给注释直接生成稍微长一点点的功能代码，翻车几率极高。
  - 第二、Copilot非常擅长生成类比代码，比如你写了一个NodeRotateLeft（树节点左旋），那么之后你写一个一样的函数NodeRotateRight（树节点右旋），那么Copilot帮你补全的概率极高
  - 第三、如果你自己写的代码有逻辑漏洞或bug，那么Copilot生成出来的代码极大可能也带有同样的逻辑漏洞与bug
  - 第四、那种非常常见的代码和逻辑功能代码，copilot的补全成功率很高，但一些高度定制化的功能代码，一般需要前面已经写过类似代码提供给copilot“联想”，否者生成的基本不太靠谱。
  - 第五、用的久了你几乎猜得到哪些代码Copilot是能够补全的，哪些代码是可以比较放心让Copilot帮你补全的，这个时候Ctrl+alt+\这个快捷键就很好用了。

- AI写代码最大的问题还是事实检测的问题，它不考虑当前的代码对不对，尤其是变量名，函数名补全，它可以非常肆意妄为。
  - 而这个是传统IDE补全代码的强项，因为它们只会检索你声明过的东西。

- 
- 
- 

- ## [请问cursor-IDE与copilotX两个工具使用体验如何？相比较而言哪个对程序员帮助更大一些呢？ - 知乎](https://www.zhihu.com/question/593171282/answers/updated)
- [AI编程工具Copilot、Tabnine、Codeium和CodeWhisperer之间的竞争 - 知乎](https://zhuanlan.zhihu.com/p/630213524)

- 更喜欢cursor聊天式帮忙生成代码。

- 做工程不会拿着ai一路问到底的，cursor 就项目初开的时候用得多，路走顺了，就一个copilot帮补一下。
# discuss-internals-cursorai
- ## 

- ## 

- ## cursor代码库索引技术细节展示了代码的RAG 实现方法大概（虽然很粗，也值得学习）：
- https://x.com/LinearUncle/status/1856597751930474873
  1. 利用 Turbopuffer 生成分块代码向量嵌入做代码RAG。
  2. 通过 Merkle 树 每 10 分钟检测代码变动，更新嵌入。
  3. 若代码改动，仅为新 chunk 索引，旧 chunk 走缓存，节省成本
- cursor是写在安全页面用来自证cursor没有上传用户代码
  - Cursor 没有，Anthropic 干了

# discuss-examples-cursorai-like
- ## 

- ## Replit Agent just dropped, and it's about to completely change the app development game...  from idea to deploy, even from your mobile
- https://x.com/minchoi/status/1832759069733482680

- ## 🌰 You probably missed these new Cursor projects? 10 wild examples:
- https://x.com/imrat/status/1832805131626180747

- ## 🌰 someone just adapted cursor-party and added (among other features) teeny eyes to the cursors that point to where you're going
- https://x.com/genmon/status/1833973123894346219
  - [elle's homepage](https://ellesho.me/page/)
  - [Cozyroom](https://cozyroom.xyz/)

# discuss-issues
- ## 

- ## 

- ## As an early adopter and heavy user of cursor (at least 1, 000 hours so far), here are 3 major issues I've noticed over the past couple of months:
- https://x.com/mayowaoshin/status/1833557628401627245
  1. The first generated output(s) often contains subtle bugs that could cost you a ton of time and money. 1. The first generated output(s) often contains subtle bugs that could cost you a ton of time and money
  2. Inconsistent quality of outputs. In addition, if you ask the AI any questions that contain suggestions or alternative solutions, it will apologize and refactor the entire code again.
  3. It can significantly increase technical debt
  - TLDR: Cursor AI (or AI coding in general) is a useful autocompletion tool that can boost your development productivity in the short run, but in the long run, it can waste significant time and energy IF you don't thoroughly review generated outputs.

# discuss
- ## 

- ## Cursor started with the CodeMirror editor, not with VSCode
- https://x.com/carloslfu/status/1835713381090599247
  - There is a simple case for extension of VSCode vs forking it. Being an extension would be too limiting. The CMD+K magic, which was one of the main things that initially got Cursor so much attention, wasn't possible as a VSCode extension, afaik. VSCodium is much more flexible.

- ## 又用了 1 周 Cursor，目前感觉它优于 Codeium + VSCode 有以下几方面：
- https://x.com/chenenpei/status/1833421862233379139
  1. 能建议多行代码的修改
  2. 能更方便地使用 Claude3.5
  3. Chat 结果提供了 accept 按钮，减少复制粘贴的动作

- ## [集成 GPT-4 的代码生成器 Cursor 使用体验如何？怎么用更高效？ - 知乎](https://www.zhihu.com/question/590152131)
- Cursor 之所以能火起来，就是因为它主打一个亮点：通过 GPT-4 来辅助你编程，完成 AI 智能生成代码、修改 Bug、生成测试等操作。
- cursor 让我感觉爽的点主要是：
  - 能够准确理解需求：如 “先构建 return 矩阵，然后一次性计算相关性” 这样的 instruction，人都不一定能第一时间 get 到我在说什么。
  - 自动纠错：贴报错堆栈就能自动修复问题。
  - 生成速度快：这一点在高频使用时还是比较重要的。
  - 另外 cursor 能够自动生成单元测试和文档，这对于广大不爱写测试和文档的程序员简直是福音！

- 交互体验一般般，就是一个demo级的工具应用。可以用它来生成模版代码，但没法用它来写工程代码

- cursor就两个mit毕业生开发的，上周提交的hello world是真的有点hello的意思了。
  - cursor好像在1月拿到了openai的风投，想乘着市场热度尽快上线，代码质量别想了，和vscode不知道相差多少个层次，现在只是用electron套了个codemirror来实现，一行测试用例都没有。
  - 它目前最大优势是理解项目工程和免费（这个优势已经没了），相比之下可能还是copilot x靠谱点

- 期待看到完整架构都自动实现的那一天, 目前的单个文件还不够

- 体验很好，让Cursor自动生成过C、C++、python、Arduino、latex公式、简单的markdown文稿，至于怎么样使用最高效，我觉得应该是和自己的知识体系有关

- 
- 
- 

- ## [如何评价Cursor？ - 知乎](https://www.zhihu.com/question/590754839/answers/updated)
- Cursor 编辑器在 GitHub 上是开源的，可以自由访问。
  语法高亮
  自动完成
  智能缩进
  括号匹配
  多光标编辑
  远程文件编辑
  可拓展性

# discuss-pm-cursorai
- ## 

- ## 

- ## [Is Cursor Tab available only for Pro subscribers? - Discussion - Cursor - Community Forum _202409](https://forum.cursor.com/t/is-cursor-tab-available-only-for-pro-subscribers/14333)
- you get 2000 completions only once. After that, you need to upgrade to the PRO plan to continue using it and access other great features of Cursor.
  - Cursor Tab works only with a PRO subscription, once your free trial has expired, and you have used up your one-off allowance of 2000 completions the free plan allows for.

- All model usage is counted and billed in requests. 
  - Free requests automatically activate when you run out of normal requests. They’re processed at a lower priority, so you may wait a bit longer compared to fast requests—but they still cost nothing.
# discuss-cursor-like
- ## 

- ## 

- ## 

- ## pearai: i put up a proxy on their app and guess what 270k coinbase engineers are calculating user's usage on client side. i blocked their log_tokens api and now i can access their all models without any usage restriction lol???
- https://x.com/that_anokha_boy/status/1840476530536780072

- ## Cursor 对于公共领域的代码理解能力是很不错的，比如每个语言的基本库，常用的开源库。
- https://x.com/waylybaye/status/1834944111817978345
  - 但是自己写的代码，它的幻觉很大。比如你在其它模块中写了一个类，它在写代码时并不会将其带入 context 中。
  - 从这一点来看我觉得 JetBrains 潜力很大，JB 有强大的静态分析能力，可以有效的低成本消除此类幻觉。
- cursor在ai辅助交互上已经算是登峰造极了，现在最大的瓶颈还是模型不够聪明(即便是claude)：
  1. 让它实现一个比较完美的raf节流它老实现成防抖
  2. 还是经常会修改一些和需求无关的代码
  3. 对于不知名的第三方库老是编一些不存在的 api
  4. 剪切一段代码，新建一个函数，提示的居然不是剪切的代码而是编的

- jb 必须得加速跟上才行，现在他们的 ai 需要一个产品经理对着 cursor 抄
  - jb动作慢的像是那种过日子的国企

- 我现在特别希望这些代码工具可以把在Linux下能够编译完成的项目，进行一个跨平台的改变，变成Windows可编译和执行的。

- ## Introducing AI Codex: the self-improving system for @cursor_ai .
- https://x.com/zbeyens/status/1832079140083687671
  - codex.md: Error and learning repository.
  - learn.md: Auto-save new insights.
  - split-codex.md: Smart categorization.
  - Free. Open Source. Ready-to-use template.
  - All my AI prompts are now at https://github.com/udecode/dotai, feel free to use and contribute!

- Codex idea is cool, I think all Ai could use that.
  - Yes that’s why I didn’t call it Cursor Codex.

- I had a similar idea with `knowledge.md` files: 
  - I like how you've refined the learning into clear algorithms.
  - [Manicode YC application](https://manifoldmarkets.notion.site/Manicode-YC-application-d748f8e890f24a3ba4b5308821a34351)

- Does this really work or is it just a waste of tokens?

- what's your workflow after using split-codex? Do you alter learn.md to account for there being multiple codex files?
  - You can add all the codex files in the composer Project, or tag the codex folder

- ## Introducing Dotai: a template to supercharge all @cursor_ai projects.
- https://x.com/zbeyens/status/1832345581617926231
  - codex: Error and learning repository
  - session: Project memory management
  - blueprints: Tech stack setup guides
  - plugins: Tool integrations like http://v0.dev

- Have you seen: https://cursor.directory
  - Pretty cool, but I think these prompts hardly fit real-world projects. I’ll think about a solution.
- Yeah, it’s not complete. But it’s nice to system prompt your tech stack and coding style.

- Oh nice, so you have a running context file for a project as you use cursor and it answers questions and edits code, and you have a second file that tells the first file how to update itself as you code. Am I getting the gist of this approach correct?

- ## 💰🆚️ [Cursor Has Raised $60M | Hacker News _202408](https://news.ycombinator.com/item?id=41325543)

- > Why Not an Extension?
  - As a standalone application, Cursor has more control over the UI of the editor, enabling greater AI integration. Some of our features, like Cursor Tab and CMD-K, are not possible as plugins to existing coding environments.

- 🪧 For reference, here is a list of the current main code assistants:
  - GitHub Copilot
  - Cursor.sh
  - Cody
  - Codeium
  - Amazon Q (formerly CodeWhisperer)
  - Pieces (This team is from Cincinnati, deserving a special mention from a fellow Cincinnatian)
  - Tabnine
  - Supermaven
  - Zencoder (waitlist)
  - Replit's Ghostwriter (not sure if it can be used outside of Replit)
- There are also tools that provide a UI for LLM models. While there are many, here are the main ones:
  - Continue.dev
  - Tabby
  - Aider
  - Double.bot
- Additionally, there is "Project IDX" from Google, though I am unsure how to classify it.

- 🤔 I've been using Cursor for many months now. The biggest feature it had that I wanted when I first used it was searching your own repository. It indexes all of your code in a vector DB so that it can then use RAG to make suggestions against your own codebase. That was the "killer feature" for me - I don't get a ton of value from inline code completions, but I get LOTS of value if I can ask "Is there a utility function in this repo that does XYZ?" when working in a large codebase with lots of developers.

- Not that many people use Copilot Chat, anecdotally. We've focused on codebase chat when building Cody (https://cody.dev), since we can use a lot of the code search stuff we've built before. It's hard to build, esp. cross-repo where you can't just rely on what's accessible to your editor. 
  - Ollama models show up in the chat model dropdown in Cody, if Ollama is running on your machine.
  - Cody can use Ollama for both chat and autocomplete

- I know that Copilot can see open tabs as context.

- I’m sure this is great for some people. (Really, I’m sure it is.)
  - But whenever I’ve tried Copilot I can’t stand it for more than a minute. Because sometimes it’s magical. And when it is, it is!
  - But then way more often it’s like having someone looking over my shoulder, telling me what they think I want to do, disrupting my thoughts.

- Genuine question: how do the economics work to raise $60M, for a product that costs at most $40/month?
  - Assuming $60M for 20%, that's a $300M valuation ($60M/20%).  估值大约是五倍融资
  - Assuming a 10x multiple on revenue, that requires $30M in ARR ($300M/10). 估值大约是十倍ARR
  - Cursor only needs 83k paying users to hit that ARR.
  - Github has over 100M users. Copilot has 1M users.
  - It's a new, growing market.
- My napkin math is your valuation is usually 5 x raise amount and 10x annual revenue.
  - So valuation is 5*60m = 300m And expected annual revenue is 30m.
  - At 40/month they are expecting roughly 1M monthly actives. So I am guessing their pitch is with the vc money they will get to this number and beyond before the next funding round.
  - Reality is more like the founders got to cash "something" for their troubles and ability to sell the dream to others. Who knows may be they will hit it out of the park before the next round.
- interesting...and if you have this type of revenue who do you approach
  - If you have this kind of revenue, you don't approach anyone, they approach you.
- So the funding is usually for a "future" revenue. Ie to hit this goal. Imo if they had this revenue they'd be aiming for 10x that with a much higher valuation. VC funding is all about a growth story. If you can keep selling vision you never have to worry about revenues or hitting them. There's even a name for such schemes!
- what happens to the founders if they dont hit it
  - They either run out funding (so be forced to do layoffs, liquidations etc) or they have to find someone who can bail them out at unfavorable terms (read dilutions) or be really really good at story telling

- Considering Zed introduced AI and it's so much faster than Cursor or VSCode, I think the competition will be much harder than they sold to the investors.
  - Zed's approach of building the context manually with files and text and then asking for stuff is way more direct and less "magic". It works consistently.

- i think cursor is the only player that forked vscode. i've been using cursor for a week and i really like it. it's able to auto complete/correct code in multiple places at the same time. other copilot extensions in vscode were not able to do this. but i assume microsoft will quickly add this feature in vscode and others will catch up soon. 

- [Cursor: We Raised $60M | Hacker News _202408](https://news.ycombinator.com/item?id=41321996)
  - It's its own editor (albeit[虽然；尽管] forked from VS Code), it's not a VS Code extension.
  - This is the problem with this industry and this appears to be a acquisition vehicle rather than an actual sustainable business.
  - They probably know they don't have a moat(壕沟；护城河), but once again; all for the better to take advantage of the AI bubble and exit out quickly once it collapses.

- ## 🤔 很高兴看到 Cursor 越来越火， 因为这是必然的趋势： AI 的代码能力，推理能力，数学能力，是可预期的稳定提升
- https://x.com/oran_ge/status/1828547354812916130
  - 这件事的影响深远，不仅是程序员写的代码，还有产品经理做的原型，最终是用户需求直接构建产品
- 产品经理直接通过代码生成原型吗？
  - 不是原型是mvp
- 一年前同样很多人在OpenAI, 疯狂程度选比如今的Cursor
  - 但是现在公开说OpenAI看起来不行了已经不会被鄙视了。很有可能只要1年后，新宠一样的结局
  - 创新很难，能提前整个行业几年看到正确的方向，说出来都没人信

- AI在生产力和创造力上的价值是帮助人们高效地使用工具，在Cursor的场景下coding、API、运行环境就是工具，可以让那些有想法的人快速实践。

- ## Free and open source Alternative to Cursor's composer feature directly in Replit
- https://x.com/itsPaulAi/status/1828472273260683627
  - Cursor's composer is getting a lot of buzz because it lets anyone create apps using just English.
- There is also ClaudeEngineer

- Can we do SQL?  
  - Yes you can.aider .chat/docs/languages.html

- Set up the free open-source alternative to Cursor Composer in less than 3 minutes in Replit _202408
- https://x.com/itsPaulAi/status/1828834199597633724
  - Steps to use Aider chat:
  - Create a new Python Repl
  - Generate your Anthropic API key
  - Paste it into the “Integrations” section
  - Install and run the aider-chat package
  - I also recommend that you take a look at Aider's extensive documentation if you need to.

- so this only works for python repls?
  - Yes but you can make it write any language and run with Flask. 

- 
- 
- 

- ## 拆解如何实现一个 Cursor _202408
- https://x.com/tuturetom/status/1827007055137571032
  - 如何设计一个能够生成「全栈 App」的 AI Editor 架构 - Townie
  - 使用 CodeMirror 作为编辑器，AI 生成代码、处理 Diff、人类 Review，生成预览，处理多模型与成本控制，甚至包括评测
  - [How we built Townie – an app that generates fullstack apps _202408](https://blog.val.town/blog/codegen/)

- ## 🔡 Just for the record, I recently found out that most of Cursor's core is based on this open-source project
- https://x.com/arpagon/status/1827315413950046225
  - And now, http://trypear.ai by @not_nang and @CodeFryingPan is trying to achieve parity of functionality with Cursor, but in a more transparent and, of course, open-source way.
- Yes, Cursor is based on Continue.
