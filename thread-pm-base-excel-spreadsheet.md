---
title: thread-pm-base-excel-spreadsheet
tags: [excel, pm, spreadsheet, thread]
created: 2022-04-23T18:47:38.924Z
modified: 2022-04-23T18:48:32.550Z
---

# thread-pm-base-excel-spreadsheet

# guide

- ideas
  - excel + whiteboard: [Subset - A remarkably simple way to create a spreadsheet](https://subset.so/)
  - 自然语言查询、中文查询优化
# discuss-stars
- ## 

- ## 

- ## how about version control for spreadsheets? Here's Patchwork added to a @handsontable data grid.
- https://twitter.com/_adamwiggins_/status/1775523348430069853
  - Here an edit is selected in the history, highlighting the diff on the document.

# discuss-excel-ai 👾
- ## 

- ## 

- ## [How to analyze data from Excel with NotebookLM? : r/notebooklm](https://www.reddit.com/r/notebooklm/comments/1p6mu92/how_to_analyze_data_from_excel_with_notebooklm/)
- You can't. You can load XLSX files but it will only read the text chunks. NotebookLM = RAG, and it is not made for data analysis. You can use a Python kernel in ChatGPT, Mistral etc...

- You can add Google sheets as a source, but support pages say they are limited to 100k tokens currently (however much that is!)
- In theory, you should just be able to import the Excel into Google Sheets and then use it as a source in NotebookLM

- Convert the excel document into a markdown file using google scripts. Chatgpt can help with the script

- ## we made Claude for Excel is now live for all Max, Team, and Enterprise users. Opus 4.5 makes it meaningfully better at complex spreadsheet tasks. _202511
- https://x.com/alexalbert__/status/1993349203935084861
- This is the underrated moat: domain-specific LLM wrappers that understand context. Excel has 1.2B+ users, most doing repetitive, rule-based tasks. Claude understanding "make me a summary" in spreadsheet terms = removing friction from 80% of spreadsheet workflows. The real profit pool for AI tools is domain expertise, not generalization.

- This is awesome. The real test for these tools is always cross-sheet dependencies. Is it able to trace a formula back through 3 different tabs to find the source data, or does it mostly operate on the active sheet?
  - It does, worked on 20 tab excel workbook and it finds all the cross dependency
- The limitation isn’t cross-sheet, rather cross-file.

- ## [LlamaSheets | AI Parsing and Extraction for Spreadsheets _202511](https://www.llamaindex.ai/blog/announcing-llamasheets-turn-messy-spreadsheets-into-ai-ready-data-beta)
- https://x.com/jerryjliu0/status/1993366579632115752
  - https://x.com/jerryjliu0/status/1993419298900263243
  - We launched a new API today to let you parse any Excel sheet in a structured table.
  - This lets you directly run text-to-pandas/SQL over this data if you’re building an AI agent, or do ETL yourself over it.

- Data prep is the invisible 80% of ML pipelines. The magic isn't "run ML on raw Excel"—it's "automatically infer schemas from chaos". 
  - LLMs bridging natural language intent → structured outputs is how we scale data ingestion from enterprises stuck in manual ETL hell. This unlocks self-service analytics at scale.
  - Semi-structured data is the Achilles heel of AI workflows. LlamaSheets solves the parsing problem that kills automation at scale. Standardized data feeds > complex agent logic. This unlocks enterprise automation for every business stuck with Excel. Game changer.

- Love this direction. Excel is basically “ad‑hoc schema as UI”, and most agents still treat it as plain text. Curious if LlamaSheets is (1) learning layout → schema → records, then (2) validating against a domain ontology, or more like few-shot layout cloning?

- Nice. The hierarchical column layout is a tough one. How does it handle the other classic spreadsheet nightmare: merged cells? Curious if it un-merges and fills down or preserves the span info.

- can you talk at all about approaches to benchmarking or evals for complex formulas and interdependencies?

- ## 有人搞了个Excel的AI插件，可以直接在单元格与AI聊天让它帮你写公式或者宏。
- https://x.com/karminski3/status/1955103864400777414
  - 我看了下源代码，也是宏实现的，估计用的时候可能杀软会报。感兴趣的朋友可以看看。
  - 我觉得这个实现得还是太程序员思维了。理想的情况应该是出现一个类似 Browser Use 的 Excel Use 界面，输入任务后让AI直接完成整个Excel。而不是硬着头皮弄到一半开始折腾单元格。
  - 但是实现方式还是可以参考下的，可以给想做 Excel+AI 的同学提供思路。
  - https://github.com/deepanshu88/ollama-excel
  - [Run Open Source Local AI Models in Excel with Ollama](https://www.listendata.com/2025/08/ollama-in-excel.html)

- excel 实在是太复杂了，而且很多时候表述也很麻烦，我现在很多都是输出 csv 完成即可。

- ## 🚀 Endex is the first AI agent to live inside Excel. _202508
- https://x.com/TarunAmasa/status/1953130965355905140
- It's a tool on Excel or you guys building your own excel? Looks like tool on Excel, would be a lot limited.
  - Quadratic AI: For anyone ready to skip legacy file formats, Quadratic puts the AI agent inside a modern, browser-based spreadsheet with Python, SQL, and state-of-the-art LLMs baked right in. Spreadsheet power without the Excel baggage.
  - That's why we built a modern spreadsheet with native AI functionality, Python & SQL support, and smoother interactions. The sky is the limit
  - we recently improved performance to handle more data than Excel
- Can it also update data? For e.g., I give a list of Million skills and ask it to update the definition of those? Or only for data analysis and insights
  - Yes, essentially Quadratic's AI would read the first handful of rows of data to understand the structure, then write Python in the grid next to your data to generate the table with whatever changes you request.
- But I don't need Python, I need it to work according to prompt and use intelligence to add definition. Please confirm
  - There is no LLM today that can handle millions of rows of data as context - there are limits to input tokens. Therefore we use AI understand the data, then write Python that solves your problem.
- Yeah, without API, none can do it.
  - our support for Python allows you to connect to any public API so you can get financial data and other info right into your sheet without additional tools :) AI makes it easy to write the code you need.

- Can I ask it to organize data from a .csv file into a properly formatted table?
  - No, don’t be silly. But it can automate vlookup

- Excel is where financial data lives. Smart move targeting where the work actually happens instead of creating yet another dashboard.

- http:excalai.com might be better 
- http://Docupulse.org is doing it for a while already

- ## Been building the 'Cursor for Spreadsheets'
- https://x.com/jc__gr/status/1892705094463844688
  - With SheetLang, you just type what you need—AI takes care of the rest. Watch how it instantly analyzes the data and generates Python-powered visualizations.
  - using @e2b_dev sandboxes

# discuss-table-ux
- ## 

- ## Design for Table of Product 
- https://x.com/barlydesign/status/1892020212075012402
  - 表格按行自上而下出现的动画效果

- ## Here are 6 simple tips to help you design beautiful & usable tables
- https://x.com/MichaelFilipiuk/status/1888890604392001834

# discuss
- ## 

- ## 

- ## 

- ## Notion: Type /database to try it with ai
- https://x.com/NotionHQ/status/1890106240425918827

- ## What if a spreadsheet cell could hold multiple values at the same time?
- https://x.com/alexwarth/status/1886915048309973164
  - That's the idea behind Ambsheets, a project I've been working on w/ @geoffreylitt at @inkandswitch . It's a new spreadsheet that makes it easier for you to explore many possibilities simultaneously.
  - [Ambsheets: Spreadsheets for exploring scenarios](https://www.inkandswitch.com/ambsheets/)
- Microsoft Excel array constants?

- ## 👾 who’s working on the spreadsheet for generative ai?
- https://twitter.com/JungleSilicon/status/1771196431115710496
  - i’m not talking llm’s helping you with formulas. i mean feature detection, style transfer, addition of concepts, etc.
  - should work across modalities (text, images, video, audio)
- simplest case you could get it to do math on the embeddings and do reverse embedding look ups. more complex would be using ai to interpret the values

- ## 用 Excel 实现了一个简易的 GPT2，可以下载：不过特别大，有 1.25 个G
- https://twitter.com/vikingmute/status/1768452277600387161
  - [Spreadsheets are all you need.ai – A low-code way to learn AI](https://spreadsheets-are-all-you-need.ai/)
  - 用一个Excel 表格来学习 ChatGPT 的工作原理，不用写任何代码，配有三个Youtube 视频，非常形象。

- ## You are exporting the data and processing it in excel, are you not?
- https://twitter.com/haro_ca_/status/1761440042965168526
- Shameless plug incoming - I built http://pushbyte.io to sync data from SQL to Google Sheets

- ## Ask Copilot in Excel
- https://twitter.com/msexcel/status/1750594443076407740
  - Reveal correlations
  - Identify outliers
  - Suggest new formulas
  - 提供了效果动画
  - [Introducing Microsoft 365 Copilot | Microsoft 365 Blog](https://www.microsoft.com/en-us/microsoft-365/blog/2023/03/16/introducing-microsoft-365-copilot-a-whole-new-way-to-work/)

- ## 第一次用Google表格的Apps Script，用来做自动化任务很方便。
- https://twitter.com/wong2_x/status/1742388411481342134
  - 比如我用下面这段代码每小时自动把一个Youtube视频的观看量等数据收集到一个表格里。
  - 而且ChatGPT很适合写这种代码，基本一次就对了。

- ## How do computers execute math expressions?
- https://twitter.com/Franc0Fernand0/status/1741387317263122677
  - But prefix and postfix notations are better because they don't need brackets or rules about which comes first.

- ## 尝试用 Gemini Pro Vision 来解决目前 RAG 的核心问题之一：OCR 转 Markdown（带表格）。
- https://twitter.com/9hills/status/1736362451728494852
  - 表格效果一般。
- 我现在用的一个方法，Nougat或者marker先把markdown格式的表格抽取出来，再配合pdf2image把表格的图片喂给LLava然后让LLava 作为一个orc去修复Nougat当中的markdown的错误，但是还是很多时候会表格位置错误
- 可能是中文的缘故？

- ## 我现在完全并深刻理解很多日本传统企业DX转型为什么会失败了。​因为日企那一套管理和做事方法，根本就不适用于互联网软件行业。
- https://twitter.com/lcayu/status/1731903269793116649
  - ​有问题要调查？日式做法：先用PPT或excel把问题的前因后果写出来，然后找人开会。
  - ​这还没太大问题。问题在于开会或汇报的对象：人家不懂怎么办？
  - 很可能是非科班出身，或非本岗位懂行人员。你得费尽心力去解释，这到底是个什么情况，为什么要这么做。
  - 你没有权限！有权限也不能随便改！即使不是生产环境，也得汇报，走流程。
  - 必须让不懂行且能拍板的人也听懂并理解你这么做是有道理的。先证明你是对的，再去行动。然而很多问题细节，你不先尝试一下，怎么知道一定能解决？就好像开发人员改bug，结果你得向产品说明每一行代码是干嘛的，并且脑内编译运行一下。我这么改应该能解决。
  - 产品完全理解并同意后，你才能把它发到测试环境验证一下。如果验证不通过，那再来一遍。（类似这么个玩法）这么一套流程下来，本来半个小时能搞定的事情。到了日企，半个月算快了。可能得半年。
  - 大家都不敢担责任，干活的有想法的人也没地方能施展。要么暗骂傻逼走人，要么接受这一切，最后大家一起摆烂。反正工资照样领，干好干坏都一样。能成功就有鬼了。
- 申请一个打印机，写分析报告，走审批流程走了1个星期
  - 一个星期？这应该称之为神速
- 👉🏻 虽然听说过日本人把Excel玩得很溜，但好奇excel怎么做报告？ 把问题用浅白的语言让外行人都听得明白是很值钱的技能，直接拉开距离。
  - 做正经的报告还是得PPT，但是不妨碍他们用excel写操作手册，写事情的说明，还是图文并茂的那种。
  - 用大家都能听懂的语言给外行人讲明白，这确实是很值钱的技能，一般这种人也不会只当个工程师了。不如去当讲师、搞培训、写书。
  - 我反正无法面对一个连基本的术语都不懂的人，还能耐着心去讲明白专业的问题
- ChatGPT最擅长把专业的事情讲的让外行听懂
- 我原来有两个日本同事确实就是这样的。有个bug，会写很详细的doc记录问题是啥，怎么debug，怎么解决，以后怎么弄。内容其实非常好。但是我当时就在想要是对每个bug都这么搞的话，效率有点太低了
- 日本IT就是混日子拿钱  即便是外国人占比高的会社也好不到哪去 技术靠外包 外包一半靠派遣 能负责的人也就懂一点点技术
- 很多职员也喜欢这样，出了事就谁谁谁批准的。私企大到一定程度就会像国企，有没有创新有没有成绩不重要，重要的是别搞出事。
- 敬语文化是日本最让人恶心的糟粕，比租房还让人反胃，简单点要死吗，发个邮件都得反复检查几次有没有不对的地方，就这还搞创新驱动

- ## 经过很长一段时间以后，我发现 excel/sheets 比脑图啥的都好用...
- https://twitter.com/lyricwai/status/1729375911844487218
- 我也是这个习惯，脑图和笔记我都是用excel。
- 我用excel手动做甘特图，简单、高效。

- ## Here are some handy CHAR functions that you can use to add context to your #GoogleSheets
- https://twitter.com/benlcollins/status/1724774908972921219
  - ▪️ CHAR(8594) produces the right arrow ➡️
  - ▪️ CHAR(10) produces a carriage return (new line)
  - ▪️ CHAR(8595) produces a down arrow ⬇️
- My tracker with char()

- ## 第一个 GPTs：合并 Excel 文件。 实现了一个 WPS 的付费功能，上传多个 Excel 文档，合并为一个文件后下载。
- https://twitter.com/yeshu_in_future/status/1723331524161122366

- ## 📈👾 Introducing Rows AI, the ultimate AI tool that makes Excel look like a toy
- https://twitter.com/heyshrutimishra/status/1718165718816968712
  - Import your data from files ( like: csv, xlsx ) or from over 50+ integrations
  - With its GPT integration, Rows is like a data analyst with superpowers.

- ## Introducing Python in Excel
- https://twitter.com/Sumanth_077/status/1716468495129661552
  - To get started all you need to use is the new PY function which allows you to input the Python code directly into Excel cells.

- ## 谷歌刚刚在谷歌表格中添加了一项令人惊叹的人工智能功能。“智能填充”会自动检测两列之间的关系并预测您要输入的值。
- https://twitter.com/FinanceYF5/status/1716292981886775690
- 以下是一些使用示例：
  - 按主题对反馈进行分类
  - 按主题组织新闻文章
  - 将地址数据转换为一致的格式
  - 从文本字段中提取电话号码

- ## 🎙 Recording → ✍️ Text → 💭 Analysis with AI now available in Glide! 
- https://twitter.com/glideapps/status/1646603234096848896
  - The “Speech to Text” action uses Whisper and our @OpenAI integration to dictate and analyze text. 
  - Our CEO and Co-Founder @dvdsgl demos an applicant tracker that records voice notes and sorts by sentiment
- Instantly generate transcriptions so you can search through recorded notes.

- ## 智能聊天表格应用「ChatExcel」，思路挺有趣的，直接在网页上输入文字告诉它希望怎么处理表格，就会在线自动处理，这样就不用记函数了
- https://twitter.com/HiTw93/status/1636155567872901120
  - [酷表ChatExcel](https://chatexcel.com/)
- 稍微复杂一点儿的表格就识别不了。花拳绣腿的东西，和OPENAI完全不是一个量级的东西

- ## Preparing a tutorial on how you can easily share data with your customers without exposing your database via @GRID_hq
- https://twitter.com/thomas_yang1/status/1630370358309306368

- ## [GRID 2.0: Next-gen spreadsheet with presentation layer & AI assistant](https://www.producthunt.com/posts/grid-2-0)
- Now with a GPT-3 powered formula copilot.
* GRID Sheets, our fully featured spreadsheet editor
* GRID AI Formula Assistant powered by GPT-3: write formulas with plain language prompts
* Integrations: Notion, Airtable, Slack & more to come!
* Automatic refresh for Notion and Airtable databases

- ## [Google Sheets Advent Calendar](https://www.benlcollins.com/spreadsheets/google-sheets-advent-calendar/)

- ## Introducing:  Observable for Excel Users! 
 - https://observablehq.com/@observablehq/excel-introduction?collection=%40observablehq%2Fobservable-blog

- ## Really powerful UI for working with relational databases! Nesting tables to represent joins is really clever.
- https://twitter.com/ccorcos/status/1520273524161581057
  - [Ultorg at the 2022 HYTRADBOI Database](https://vimeo.com/695905306)

- ## The biggest reason Excel is the most popular layfolk programming language is that its UX and IDE is miles miles miles better than any other language
- https://twitter.com/hillelogram/status/1525217533518831621
- This is probably true but we should emphasize that the UX is mostly driven by the spreadsheet concept, rather than particular details about Excel.
- It also makes program state extremely visible, something that I think PLs generally don’t think about much. Not saying the idea wasn’t there, eg, with smalltalk, but excel goes way beyond.
- Arguably the UX comes down to just having a visible location for a value, rather than the idea of a constant or variable held in a named location off screen.

- ## Need a versatile function that can make static spreadsheets fun & interactive? It’s gotta be the IF function
- https://twitter.com/GRID_hq/status/1524796293004107776

- ## The QUERY function: the most powerful and versatile spreadsheet function in existence.
- https://twitter.com/benlcollins/status/1521528069105893378

- ## EXCEL 是你最被忽视的设计工具
- https://twitter.com/nishuang/status/1519558823622680581
  - 这些美观、易用的数据可视化图表和控制台面板，都是用 EXCEL 设计的
  - 作者是数据可视化专家，介绍了利用形状、图片、图标、文本和色彩、特殊的图表样式，在 EXCEL 里进行设计。他还顺便卖模板

- ## I feel like so many tools for "building interactive apps in a spreadsheet" end up struggling w/ the same problem: how to fit side effects and async computations into the simple spreadsheet model of reactivity.
- https://twitter.com/geoffreylitt/status/1516904903184060416
  - The spreadsheet model is awesome: data updates, pure formulas re-evaluate, the whole sheet is consistent, nice.
  - But what happens when a cell can "do something" when it updates?
  - You can try to fit it more closely into the existing spreadsheet model, or you can bolt on an events/triggers system... these days I tend to think a separate event system is more straightforward. Jotted some notes on different approaches
- Asynchrony is also tricky. Even if your computation is pure, if it's slow and async then you have two options:
  - a) refreshing the spreadsheet is slow
  - b) you can partially refresh the spreadsheet, now the sheet is no longer guaranteed consistent at any given time
- Feels like many of the challenges in UI and state management frameworks boil down to answering these kinds of questions. 

- @observablehq seems to handle it well!
