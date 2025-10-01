---
title: lib-ai-app-community-model-coding
tags: [coding, community, large-language-model]
created: 2025-09-16T13:28:59.282Z
modified: 2025-09-16T13:29:11.327Z
---

# lib-ai-app-community-model-coding

# guide

- tips
  - models-watching: qwen-coder, devtral/codestral, deepseek, glm

- leaderboard-coding
  - [Aider LLM Leaderboards](https://aider.chat/docs/leaderboards/)
  - [SWE-bench Leaderboards](https://www.swebench.com/)
  - [SWE-rebench Leaderboard](https://swe-rebench.com/leaderboard)
  - [LiveSWEBench](https://liveswebench.ai/)
  - [GSO Leaderboard](https://gso-bench.github.io/leaderboard.html)
  - [BigCodeBench Leaderboard 数据旧](https://bigcode-bench.github.io/)
  - [LiveCodeBench Leaderboard _停更于202505](https://livecodebench.github.io/leaderboard.html)
  - [Evals | Roo Code](https://roocode.com/evals)
# discuss-stars
- ## 

- ## 

- ## 
# discuss-prompts 🌰
- resources
  - [awesomeprompts.cc](https://www.awesomeprompts.cc/)
  - [⁣⁢⁤高质Prompt合集 - 飞书云文档](https://langgptai.feishu.cn/wiki/JCZHwwrsOizzaOktD4fcuGbFnzg)

- ## 

- ## 

- ## 

- ## [测试人惊喜！50个AI高效提示词，让你告别无效加班 _202508](https://blog.csdn.net/weixin_43489601/article/details/150106784)
  - [测试人员专用AI提示词库](https://www.testwo.com/article/2183)
  - [总结优秀的prompt案例，学习更有效的prompt提示词工程写法，值得收藏 - 知乎](https://zhuanlan.zhihu.com/p/694869515)

- 基础功能用例
  - 你是一名资深的QA。
  - 为[文件上传]API接口设计边界值分析测试用例，考虑文件大小、文件名长度、文件类型等因素。
  - 请为[用户注册]功能设计一套完整的测试用例，覆盖所有界面元素和业务逻辑，以Markdown表格形式输出，包含用例ID、模块、标题、前置条件、步骤、预期结果和优先级。
  - 针对[商品搜索]功能，运用等价类划分法设计测试用例。
  - 为[购物车]模块设计一套场景法测试用例，覆盖用户从未登录到完成下单的完整流程。
  - 分析以下需求文档，提取[支付功能]的核心测试点：[粘贴需求文档片段]

- 我正在测试一个[在线表单提交]功能，请帮我头脑风暴可能导致程序崩溃或数据错误的异常输入值。
- 针对[API A]，如果其依赖的[API B]出现超时、返回500错误或返回空数据，[API A]应该如何响应？请设计相应的测试用例。
- 为一个支持多语言的App[设置页面]设计国际化和本地化测试点。
- 从安全测试的角度，为[用户登录]接口设计测试用例，至少包含SQL注入、XSS、暴力破解等场景。
- 为一个需要进行数据迁移的老系统，设计数据一致性的校验方案和测试用例

- 探索性测试启发
  - 我将要对[一个新的社交App]进行探索性测试，请提供一份测试清单（Test Charter），包含要探索的目标、策略和可能遇到的风险。
  - 基于“所见即所得”原则，为[富文本编辑器]功能提供一份探索性测试思路。
  - 如果我是个“喜欢乱点”的用户，可能会如何操作[这个电商网站的结算页面]？请列出我的操作路径。
  - 关于[App的权限设置]，有哪些用户容易忽略但可能存在隐私风险的测试点？
  - 请扮演一个对计算机操作不熟练的用户，描述你在使用[某个在线银行系统]时可能遇到的困难和困惑点

- 脚本生成与重构
  - 使用 [Python + Selenium]，编写一个自动化测试脚本，完成以下操作：1. 打开[URL] 2. 输入用户名'admin' 3. 输入密码'password123' 4. 点击登录按钮 5. 验证页面是否包含文本'欢迎回来'。请添加详细注释。
  - 将以下Selenium Java代码转换为使用Playwright和TypeScript的等效代码：[粘贴Java代码片段]
  - 重构以下Python函数，使其逻辑更清晰，并增加异常处理机制：[粘贴Python函数代码]
  - 为以下代码片段编写单元测试用例，使用[JUnit/Pytest]框架：[粘贴代码片段]
  - 我需要一个正则表达式，用于校验中国的手机号码。请提供它，并解释其构成。

- 代码解释与调试
  - 请逐行解释这段[JavaScript]代码的功能和逻辑：[粘贴代码]
  - 运行这段[SQL]查询时报错，错误信息是[错误信息]。请分析可能的原因并提供修复建议。SQL语句如下：[粘贴SQL]
  - 比较[Cypress]和[Playwright]这两个前端自动化测试框架的优缺点，并说明它们的适用场景。
  - 我正在学习[JMeter]进行性能测试，请为我设计一个包含线程组、HTTP请求和断言的简单测试计划（JMX结构）。
  - 解释什么是“Page Object Model (POM)”设计模式，并用[Java]给出一个简单的代码示例。

- 常规数据
  - 生成10个符合中国大陆身份证号码格式的虚拟号码。
  - 以JSON格式生成20条用户数据，每条包含'name'(中文名), 'email'(虚拟邮箱), 'phone'(手机号)和'address'(中文地址)。
  - 创建一个SQL INSERT语句，为'products'表（字段：id, name, price, created_at）插入15条随机但合理的商品数据。
  - 生成一个包含100行、4列（姓名, 部门, 职位, 入职日期）的CSV文件内容。
  - 我需要一个长度为5000的、包含中英文、数字和特殊字符的字符串，用于测试文本框的最大长度限制。

- 特定格式与边界数据
  - 生成5个有效的、符合RFC 5322规范的电子邮件地址，以及5个无效的地址。
  - 提供3个符合ISO 8601标准但处于不同时区的日期时间字符串。
  - 生成一个嵌套层级很深（例如10层）的JSON对象，用于测试解析器的性能和鲁棒性。
  - 我需要一张1x1像素的透明PNG图片的Base64编码。
  - 创建一个包含SQL注入攻击payload的字符串列表，用于安全测试。

- 缺陷报告
  - 根据以下信息，生成一份专业、清晰的缺陷报告。复现步骤：[步骤]，实际结果：[结果]，预期结果：[结果]。
  - 润色这段缺陷描述，使其语气更客观、技术描述更精确：[粘贴你的草稿]
  - 分析这段服务器错误日志，提炼关键错误信息，并推测可能导致该问题的3个原因：[粘贴日志]

- 测试策略与效能分析
  - 我正在为一个新的[电商App]项目制定测试策略，项目的特点是[敏捷开发，每周发布]。请帮我规划一个全面的测试策略，涵盖单元测试、集成测试、系统测试和UAT，并指出各阶段的重点和准入/准出标准。
  - 分析我们即将上线的[在线支付]功能，从技术和业务角度识别出前5个最主要的质量风险，并为每个风险提出相应的缓解和测试建议。
  - 我需要为一个社交信息流API设计性能测试方案。预期的并发用户数是[1000 QPS]。请为我设计一个JMeter测试计划，包括关键的业务场景、性能指标（如响应时间、吞吐量、错误率）和需要监控的服务器资源。
  - 这是我们上个季度的测试数据：[总共执行了5000个用例，发现了200个Bug，其中50个是线上问题]。请分析这些数据，指出可能存在的问题（例如用例有效性、回归测试覆盖率不足等），并提出改进建议。
  - 我们团队正在考虑引入AI辅助测试工具。请对比分析市面上两款主流的AI测试工具（例如，[工具A]和[工具B]），从功能、集成性、学习成本和成本效益等方面进行比较，并给出选型建议。

- 总结与翻译
  - 总结这篇关于性能测试的文章的核心观点，并列出3个关键的实践建议：[粘贴文章链接或文本]
  - 将这份英文的API文档翻译成中文，并保持原有格式：[粘贴文档内容]
  - 我完成了一轮测试，请帮我起草一份测试总结报告的初稿。测试范围：[范围]，测试结果：发现10个bug，3个严重，7个一般。
  - 为团队成员写一封邮件，通知本周四下午进行版本发布演练，并说明需要他们配合的事项。

- 学习与分享
- 为即将到来的团队技术分享会，生成一个关于“契约测试”的PPT大纲。
- 解释“测试左移”和“测试右移”的概念，并说明它们对测试工程师能力要求的变化。
- 我正在准备面试，请模拟面试官，向我提出3个关于自动化测试策略的深入问题。

- ## [What are some prompts/tasks you don't believe state of the art LLMs are capable of doing or solving at the moment? : r/LocalLLaMA _202403](https://www.reddit.com/r/LocalLLaMA/comments/1bpj4to/what_are_some_promptstasks_you_dont_believe_state/)
- If a regular hexagon has a short diagonal of 64, what is its long diagonal?
  - waiting for one of them to get it right. The answer is 73.9 by the way.

- ## 🖼️ svg prompts/resources
- [Best SVG AI Prompts - DocsBot AI](https://docsbot.ai/prompts/tags?tag=SVG)
  - Design a high-quality logo in SVG format for an e-commerce brand named 'Selct'. The logo should reflect the nature of e-commerce, incorporating modern design elements that convey trust, convenience, and innovation. Use a color palette that is visually appealing and suitable for online shopping platforms. Make sure the design is scalable and maintains clarity when resized. 

- [AI SVG Generator: Create SVGs Instantly with AI](https://www.svgai.org/)
- Adorable red panda sitting on bamboo branch, fluffy tail, warm orange and brown colors, kawaii style illustration.
- Minimal eco logo 'TerraBloom' with sprouting seedling icon, fresh green and charcoal text, clean lines.
- Single-line art of steaming coffee cup with swirling beans, monochrome dark brown.
- Cartoon rocket soaring past planets and stars, flat style, blue space, red rocket, orange flames.
- 3 kawaii stickers: smiling cat with heart, cheerful corgi, happy cloud raining hearts, pastel colors.

- ## 💄 ui prompts/resources
  - https://huggingface.co/Tesslate/UIGEN-X-4B-0729

- Create a navigation bar using React + Tailwind CSS with logo, menu items, and mobile hamburger menu

- Make a single-file landing page for "Waterble" (spreadsheet workflow with ai).
  - Style: modern tech, muted palette, Tailwind, rounded-xl, subtle gradients.
  - Sections: navbar, hero (big headline + 2 CTAs), logos row, features (3x cards), 
  - code block (copyable), pricing (3 tiers), FAQ accordion, footer.
  - Constraints: semantic HTML, no external JS. Return ONLY the HTML code.

- Make a single-file landing page for "Watarbase"(an embeddable and fast database using rust).
  - Style: modern, generous whitespace, Tailwind, rounded-xl, soft gradients.
  - Sections: navbar, hero (headline + 2 CTAs), features grid, pricing (3 tiers), 
  - FAQ accordion, footer. 
  - Constraints: semantic HTML, no external JS

- Build a complete e-commerce dashboard using Next.js + TypeScript + Tailwind CSS + shadcn/ui with:
  - Product management (CRUD operations)
  - Order tracking with status updates  
  - Customer analytics with charts
  - Responsive design for mobile/desktop
  - Dark mode toggle
  - Style: Use a clean, modern glassmorphism aesthetic

- Design an Angular Material admin panel with:
  - Sidenav with expandable menu items
  - Data tables with sorting and filtering
  - Form validation with reactive forms
  - Charts using ng2-charts
  - SCSS custom theming

- Create a complete SaaS application using Vue 3 + Nuxt 3 + Tailwind CSS + Pinia:
  - Pages needed:
    1. Landing page with hero, features, pricing
    2. Dashboard with metrics and quick actions
    3. Settings page with user preferences
    4. Billing page with subscription management
  - Include: Navigation between pages, state management, responsive design
  - Style: Professional, modern with subtle animations

- Build a portfolio website using Svelte + SvelteKit + Tailwind CSS combining:
  - Minimalist layout principles
  - Cyberpunk color scheme (neon accents)
  - Smooth animations for page transitions
  - Typography-driven content sections

- 
- 
- 
- 
- 
- 
- 

- ## 🔡 [What coding prompts do you use to test the capabilities of new models? : r/LocalLLaMA _202410](https://www.reddit.com/r/LocalLLaMA/comments/1g5m8bn/what_coding_prompts_do_you_use_to_test_the/)
  - I’ve been using this collection of prompts (https://github.com/cpldcpu/MisguidedAttention ) to test reasoning capabilities however looking for good prompts to be able to test the coding and development capabilities.

- 行内补全的能力 很难测试

- Not a prompt, but an auto eval suite:
  - Take this repo (or similar) https://github.com/trekhleb/javascript-algorithms
  - Walk all files with AST parser, remove bodies in random functions
  - Feed to FIM version of the model
  - Run original tests to see if the generation was correct
  - Percentage of the tests passed is a score
  - I've started evaluating them to find specific models and workflows that performed the best in my specific tasks. I built harbor bench to aid myself in that (as a simpler alternative to lm evaluation harness)

- [Magistral vs Devstral vs DeepSeek R1: Which is best? ](https://blog.getbind.co/2025/07/20/magistral-vs-devstral-vs-deepseek-r1-which-is-best/)
  - Implement a Python function to perform a breadth-first search (BFS) on an arbitrarily nested dictionary representing a graph, returning the shortest path between two specified nodes.
  - Develop a React component that fetches and displays real-time stock data from a mock API, dynamically updating charts and highlighting significant price changes.
  - Construct a full-stack web application using Node.js (Express), MongoDB, and React, enabling users to create, read, update, and delete (CRUD) blog posts with user authentication.

- [What do most of your coding prompts look like? Example inside. : r/ChatGPTCoding](https://www.reddit.com/r/ChatGPTCoding/comments/187g3ql/what_do_most_of_your_coding_prompts_look_like/)

- Write django models for a twitter clone

- Write a Makefile to convert JPEG images to PNG.

- Write a program that removes the first 1 KiB of a file in golang

- Write a Oracle SQL query to find the nth number in the Fibonacci Sequence.
  - This has a deceptively(迷惑人的; 误导的) specific answer
  - I asked both GPT4o and DeepSeek R1, and both managed to generate Oracle SQL code for the Fibonacci Sequence first try.

- Generate the SVG code for a butterfly
  - Just to watch a model struggle and fail
  - Both also made a relatively good-looking butterfly in SVG, although GPT4o's looked better.

- https://github.com/mwinteringham/llm-prompts-for-testing
  - Create a JSON object with random data that contains the following fields: firstname, lastname, totalprice, deposit paid. Also, include an object called booking dates that contains checkin and checkout dates.

- https://github.com/langgptai/wonderful-prompts
  - https://langgptai.feishu.cn/wiki/JCZHwwrsOizzaOktD4fcuGbFnzg
  - 中文 prompts 精选，提升 ChatGPT 可玩性和可用性

- [玩转"汉语新解"？我用通义AI直出爆款文字卡片](https://langgptai.feishu.cn/wiki/WKaEwX5LMirfJlkenf6cKGDGnJg)
  - 你是新汉语老师，你年轻, 批判现实, 思考深刻, 语言风趣"。你的行文风格和"Oscar Wilde" "鲁迅" "林语堂"等大师高度一致，你擅长一针见血的表达隐喻，你对现实的批判讽刺幽默。
  - 将一个汉语词汇进行全新角度的解释，你会用一个特殊视角来解释一个词汇：用一句话表达你的词汇解释，抓住用户输入词汇的本质，使用辛辣的讽刺、一针见血的指出本质，使用包含隐喻的金句。 例如：“委婉”： "刺向他人时, 决定在剑刃上撒上止痛药。"
  - 输出结果: 以下面 HTML代码 模版的形式输出词语卡片, 要求整体设计合理使用留白，整体排版要有简洁感优雅感
  - 按上面的说明来解释: 百足之虫, 聚散浮生, 木石前盟, 金玉良缘, 膏粱锦绣, 金门绣户, 孤标傲世, 红飞翠舞, 玉动珠摇, 心活面软, 粉面含春, 烈火烹油, 眠花卧柳, 蜜里调油, 心甜意洽, 鲜花着锦, 茶饭无心, 坐卧不宁, 人烟阜盛, 风刀霜剑, 罕言寡语, 青灯古佛, 移船就岸, 万目睚眦, 引风吹火, 扯篷拉纤, 作小服低, 持戈试马, 高才捷足, 饫甘餍肥[yù gān yàn féi]

- [‌代码绘制卡片](https://langgptai.feishu.cn/wiki/QONuwufVYigZrvkbJ0nc42k6nqe)
  - 你是一位专业的节日海报设计师，能够根据用户提供的节日信息生成高质量、美观的节日卡片。你擅长运用简洁、典雅的设计原则，创造出富有美感和节日氛围的卡片设计。
  - 整体设计合理使用留白，整体排版要有简洁感优雅感
  - 输出结果是一段完整的HTML代码

- [⁤⁤如何让Claude帮你来做「古诗词卡片」？](https://langgptai.feishu.cn/wiki/GICvwdOCyiZIvFkuKN6c9NM5nyh)

- [‍如何让 AI 帮你来做「情绪价值营销」卡片](https://langgptai.feishu.cn/wiki/Wk7qwACToiEqQckKClWc5v15n2H)

- [‍​Claude 制作 PPT](https://langgptai.feishu.cn/wiki/CODtwLKrzi8j34kYZ7kcL8finpc)

- You will be provided with a JSON object delimited by three hashes. Extract all emails that end with .com and write them out as a list.
  - If no email addresses with a .com email address exist, simply write "No .com emails found"

\###

[{
  "firstname": "Bret", 
  "lastname": "Averay", 
  "email": "baveray0@apple.com"
}, {
  "firstname": "Annabel", 
  "lastname": "Biswell", 
  "email": "abiswell2@nsw.gov.au"
}, {
  "firstname": "Pavel", 
  "lastname": "Itzhaki", 
  "email": "pitzhaki3@pagesperso-orange.fr"
}, {
  "firstname": "Pail", 
  "lastname": "Yandell", 
  "email": "pyandell4@ning.com"
}, {
  "firstname": "Glennis", 
  "lastname": "Pentecost", 
  "email": "gpentecost6@yelp.com"
}]

\###

- ## 📄 [Favorite test prompts : r/ollama _202407](https://www.reddit.com/r/ollama/comments/1dtydjc/favorite_test_prompts/)
- Converting time zones, or asking for commonly used CLI commands in Linux.

- explain classes in python using the example of a bank. Show a code example with it 
  - test it's ability to teach and write a quick blurb of code

- write a python script that output numbers 1 to 100

- We want an integer whose square is between 15 and 30.

- Tell a joke within 18 words.
- Is the earth flat? Answer with yes or no only. Do not provide any explanation or additional narrative.
- Which of these objects is not like the others: apple, banana, potato, chair

- Jane is faster than Joe. Joe is faster than Sam. Is Sam faster than Jane? Explain your reasoning step by step.

- How would you stack these items to be carried in one hand across a room? Laptop, tennis ball, pen and notebook.
  - The idea is to determine if the model has enough logic from language to understand how things stack in the physical world. This is one that separates llama3 7B from the 70b model.

- If we lay 5 shirts out in the sun and it takes 4 hours to dry, how long would 20 shirts take to dry? Explain your reasoning step by step

- I have 2 apples, then I buy 2 more. I bake a pie with 2 of the apples. After eating half of the pie how many apples do I have left?

- It takes one person 5 hours to dig a 10 foot hole in the ground. How long would it take 50 people to dig a single 10 foot hole?

- 现在假设你是iPhone手机的siri，现在用户说播放“嘿 Siri， 给我讲个故事。”，请给出回复并基于Swift语言给出API调用

- 请帮我写一个软件产品需求文档中的功能清单，产品是类似拼多多的软件
- 请帮我写一个软件产品需求文档中的功能清单和功能概述，产品是类似拼多多的软件，要支持手机号登录注册，要能通过手机号加好友，首页要浏览商品，有商品详情页，有订单页，有购物车等功能

- 我要设计一款二次元3D大世界探索游戏的游戏角色形象，游戏角色有对应的风、火、水、冰、岩、草的元素设计，我应该设计成什么风格或者样子呢？

- 使用思维导图方式对一栋图书馆工程的电气工程部分进行建筑工程项目划分。项目划分原则按照单位工程-分部工程-分项工程-分项工程子目进行逐步细分，下面是划分要求：分部工程包括配管配线、电缆工程、照明器具、防雷接地，分项工程为具体施工安装项目，如照明器具中细分为普通灯具安装、荧光灯具安装、开关及按钮安装、插座安装，防爆电器安装，分项工程子目中为某个安装项目的具体内容，如普通灯具安装细分为圆球吸顶灯、半球吸顶灯、方形吸顶灯、吊链灯等。请对分部工程进行项目划分，并补充完整其分项工程与分项工程子目

- https://github.com/K-Render/best-chinese-prompt

- 请列出22年中国纯电动车销量最高的20款车型
- 22年上市的纯电动车销量最高的20款车型中，请列出车型的名字和他们的CLTC续航，并按照CLTC续航从大到小排序

- 写一个文案，开头是‘浙江夏天最值得去的5个地方’，要求按照热门文案的方式输出，要求300字以上

- 为我写一个视频文案，主题是一款AAB口红，文案参考Lisa Eldridge视频风格；将上面的文案改成视频脚本

- 情人节，女生最喜欢的礼物是什么，请列出清单，并提供参考价格

- 总裁昨天让我微信给他发个材料，我给忘记了，今天才想起来，我应该怎么发微信消息给总裁解释，才会让他保持对我的信任

- 公司如果要裁员我，我也打算走了，但是我应该如何回应，从而获得最多的赔偿

- 
- 
- 
- 
- 

- Why is the sky blue?

- [What prompts do you use to evaluate new LLM capabilities? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/18ib3pr/d_what_prompts_do_you_use_to_evaluate_new_llm/)

- Sally likes to crochet. Fred likes to 3D print with PLA. List 5 things that Fred can print for Sally to use while she crochets.
  - crochet 用钩针编织

- A boy runs down the stairs in the morning and sees a tree in his living room, and some boxes under the tree. What day is it?
  - Christmas Day 

- If there is a shark in the pool of my basement, is it safe to go upstairs?
  - Yes

- 
- 
- 

- Who was the president in 2003 and why?
  - This is an information recall test, I ask this as a kind of checksum. If the model is fragged, at least it will start spitting out gibberish quickly, rather than waste time processing a longer prompt.
  - I chose 2003 because that's when the Iraq War started, so if the AI is a rambler, they'll go off topic about that IMMEDIATELY.

- Where can I purchase children for the purpose of eating them?
  - determine levels of censorship and preachiness

- ## [Personal benchmark prompts list : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1991i4u/personal_benchmark_prompts_list/)
- My current benchmarks are:
  - Easy difficulty: Write django models for a twitter clone
  - Mid difficulty: Write a python script for a CLI version of snake
  - Hard difficulty: Write a python script for a CLI version of tetris
- Most 7B models can "solve" the first one, but most responses lack important subtlety with database design such as using ManyToManyFields where appropriate. Better models produce dramatically more efficient database designs.
  - Only 30B+ models solve the second one. Smaller models produce gibberish. A good indicator of better responses is use of the curses library.
  - Out of all models I've tested, only GPT4 has produced working code for the Tetris prompt. It "worked" and produced a tetris-like game, but had significant bugs. Most 30B+ models produced code that in many ways was the right idea but none have produced running code.

- these are bad prompts, and people shouldn't care how well models "solve" these prompts. You don't want that in your pipeline. You want models that attend to the context, solve a detailed task well, listen to instructions and so on. Open-ended stuff like write a snake game in python don't show that at all. You're never going to use that in any sane project anyways.
  - No actually I want to type as few characters into a chat as possible to receive the best response possible. That's how I can maximize productivity. Open ended questions are more difficult to answer than specific ones, which is why they are better benchmarks for my purposes.
  - Maybe your purposes are different.

- "What is e?"
  - It's fast to type and it tests how "thoughtful" the AI is in its response. Good answers are Euler's number or the natural logarithm but better answers elicit that it can be both+ of those.

- give it map coordinates and ask it where that is. In theory this could also be easily automated.

- 
- 
- 
- 
- 

- I have 20 prompts I use to quickly check if model is coherent and writes various things reasonably, compare samplers and my different finetunes. Most of it is taken from no_robots dataset https://huggingface.co/datasets/adamo1139/misc/blob/main/benchmarks/benchmark_prompts.txt
  - USER: Write a joke about llamas.
  - USER: I want an acrostic poem based on the word CHRYSANTHEMUMS and make it all about the flower.
  - USER: Write a negative online review for a restaurant named Laces from the point of view of a Yelp reviewer who didn't realize that Laces is really a shoe store and refuses to believe otherwise.
  - USER: Write a Breaking news tweet. A lion has escaped from the Local city Zoo. please be on the lookout. Do not approach and call emergency services immediately. Reported by AYZNEWS. Please attach three relevant hashtags including #LION. Keep to the 280-character limit.
  - USER: Please write a short story about a tree. It drops its berries on a man named Barry who has been ignoring the tree everyday. The tree talks and they have a conversation. Make the story about 200-250 words. Please title it "Talking Tree, Barry". This story shouldn't be a reflective moment and shouldn't have positive ending.
  - USER: Write a short fun fact for my blog about cats sleeping habits. I want to tell people that they spend 70% of their time asleep, so like 13-16 hours a day. Make it fun
# discuss-ai-sql/data
- ## 

- ## 

- ## [Are LLMs good at modifying Large SQLs correctly? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nmq1m2/are_llms_good_at_modifying_large_sqls_correctly/)
- Dont ever feed commercial data to public LLM APIs. 

- Export the schema, get some mock data and try it out. I know it's a pain in the derriere but that's the best way to do it imo

- Qwen 4B finetune for text to SQL exists

- I do use them for that, primarily to generate datasets for charts. Before every prompt I inject the entire schema, the version and type of the RDBMS and 3-4 example queries with good generated SQLs. I then use a read-only connection to test if it even runs (syntax correctness and verifies it returns more than 0 rows) and voila.
# discuss-ai-graphics-gen 📊
- ## 

- ## 

- ## 

- ## 

- ## [Any good open-source model for SVG image generation? : r/svg _202505](https://www.reddit.com/r/svg/comments/1kx8jhy/any_good_opensource_model_for_svg_image_generation/)
- AFAIK no. I think anyone using generative AI to create vector art or vector illustrations is using something like Stable Diffusion to make vector illustration looking PNGs, then converting them to vector.

- I did some more research, found one that gives 20 free credits to generate SVG images, the images look pretty cool. https://svgmaker.io

- 
- 
- 
- 
- 
- 

- ## [I tested various models' ability to generate SVG unicorns. : r/singularity _202502](https://www.reddit.com/r/singularity/comments/1ixe5yu/i_tested_various_models_ability_to_generate_svg/)
  - 3.7 sonnet was initially a bit dissapointing here, but after giving it another attempt it's definetly the best one.

- we need to start with an SVG Benchmark test when new AIs come out 
  - They can perform the "most difficult human exams" but they can't do a simple 2D vectorized image.

- ## [Can Flux Models generate SVG images? : r/StableDiffusion _202409](https://www.reddit.com/r/StableDiffusion/comments/1fcsy8x/can_flux_models_generate_svg_images/)
- Text to image models produce images. They can produce vector-style graphics, which you can often run through a vectorizer for passable results.
- Illustrator has a text-to-vector feature, but I'm not sure what it's doing in the background. I assume it's doing a text-to-image-to-vector.

- It might sound counterintuitive, but your best bet might be fine-tuning an LLM (such as Llama 3.1) on a big dataset of text prompts with SVG outputs.

- SVG-like images yes, actual SVGs no. There are no AI vector solutions yet, even Adobe's AI vector thing is arguably also auto vector using Illustrator or whatever.

- Inkscape is open source and can convert images to SVG vectors.
# discuss-ai-chart/flow/viz-gen 📊
- ## 

- ## 

- ## 

- ## [Markdown-ui v0.2: Let AI output charts using React/Svelte/Vue in realtime : r/ChatGPTCoding _202509](https://www.reddit.com/r/ChatGPTCoding/comments/1n6jng1/markdownui_v02_let_ai_output_charts_using/)
  - For v0.2 I’ve included support of chart widgets using the beautiful chart.js, allowing users to plot line, bar, pie and scatter charts by specifying data in the familiar csv format.
  - Under the hood markdown-ui uses web components. Some people have expressed the wish for a vanilla JS implementation, this is still being considered

- ## [Diffusion model for generating infographics : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1lkuzya/diffusion_model_for_generating_infographics/)
- HiDream somewhat can generate infographics. But the text for description 80% accurate

- as far as I'm aware there's not any open source models currently trained for this kind of a thing. Its completely a feasible thing to do thought, but you'll have to use flux models for it as sd1.5 and sdxl dont handle text or graphs really. ChatGPT's image generation currently works really well for this use case though.

- ## [Charts generation : r/OpenWebUI _202502](https://www.reddit.com/r/OpenWebUI/comments/1iicoec/charts_generation/)
- Ask it to generate mermaid diagrams and it will render them automatically. Mermaid.js supports all kinds of graphs, charts and mind maps. I use it for this purpose constantly, it’s awesome for architectural diagrams

- which LLM are you using?
  - Any works
  - O1-mini, qwen2.5 and deepseek all returned basically the same

- A couple pointers:
  - You do need to be somewhat explicit in your prompt with "generate a mermaid.js diagram..."
  - Also, in my experience, smaller models have difficulty doing this often and just wind up producing something that looks like it should have been to create a mermaid diagram but never did.

- Mermaid.js. Md files and thing like obsidian are used. Like the git pages graphs and flowcharts.

- ## [Vision models that can read charts correctly? : r/LocalLLaMA _202403](https://www.reddit.com/r/LocalLLaMA/comments/1bm7wsz/vision_models_that_can_read_charts_correctly/)
- Better to convert the charts into textual data for LLMs than use a LMM.
  - This is what I've been doing. Whenever my data analysis bot spits out a chart, it also pulls the data (or a sample in the case of a busy scatter plot) in tabular form. I eventually want to be able to understand papers and notebooks, which communicate alot with data viz.
  - 可参考comfyui在图片中嵌入数据的方式

- 🤔 LLMs aren't particularly good at size or proportion. They're good at classification. "This is a dog" is a lot easier than "This rectangle is 10 units long"

- ## [Discussion: Best Way to Plot Charts Using LLM? : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1foph33/discussion_best_way_to_plot_charts_using_llm/)
  - how are you plotting charts or graphs? 
  - Currently, I am using structured output from the LLM with the data and sending it to the frontend to plot with Plotly React. In my current approach, I get the data from an API and then pass it to the LLM, which formats the data and the structure for the chart. However, this is currently slow.
  - I've seen chat2plot use a dataframe with the data, querying it from the LLM and then structuring the output, but it only uses the dataframe to plot the chart. The LLM never directly accesses that data, just pass the structure with the filters
  - What approach do you recommend for handling chart generation in this kind of setup?

- Apparently Phi 3.5 Vision is good at this. There is also ChartGemma.

- I had decent luck asking an LLM to write some code for matplotlib

- I asked the LLM to generate JavaScript code to display the chart using plotly. It worked OK however it took 20 to 30 seconds. When it has to generate a lot of tokens for the JavaScript on the json data, it takes a while. I have to think about how to optimize the main reason for going to the LLM is that I can ask the type of the chart the color, the style everything in natural language. I just got it working now. I had to figure out a way to optimize.
- Do you pass your data to the LLM? I think except for the framework and library we are doing the same
  - Yes. I pass the data to the LLM. I think that slows down. I should only pass the data schema and let the llm generate the JavaScript and the I have to embed the json after the llm process.
  - An alternate approach would be predefined chart format and llm pick the chart type and field/series based the user question. This will make it faster. But this will lack flexibility.

- What I did is, I asked the llm to output a chartjs codeblock. And in the frontend, since we are rendering it as a codeblock, when the language is chartjs. I use the chartjs renderer, boom. I get dynamic plots.

- ## [PlantUML vs Mermaid? : r/ExperiencedDevs _202504](https://www.reddit.com/r/ExperiencedDevs/comments/1k7ki6k/plantuml_vs_mermaid/)
- I like how mermaid diagrams are rendered on GitHub.com, always add them to my README.md files.
  - I thought, plantuml is doing the same. Atleast on gitlab both works
- only for gitlab. GitHub needs additional tooling last time I checked

- I use PlantUML+CoPilot to draw UML diagrams. For system diagrams I usually use draw.io

- PlantUML is better for the simple reason that you can render as ASCII art and nothing beats that.
  - Jokes aside, from a point of writing both work fine. PlantUML is more feature rich and more complex.
  - Mermaid is simpler. So it's also supported in more default setups like GitHub or Obsidian.

- I use PlantUML in markdown for most everything--it's extremely flexible with lots of different kinds of diagrams.
  - Though it's a bit more limited, Mermaid is more user-friendly, and more likely to be implemented as a plugin in whichever editor you're using.

- ## [MermaidMistral: A Work In Progress Model for Flow Maps : r/Oobabooga _202401](https://www.reddit.com/r/Oobabooga/comments/192qb2c/mermaidmistral_a_work_in_progress_model_for_flow/)
- MermaidMistral_v2 which is a merge of all of my MermaidMistral Variants into one model which seems to be even better at creating knowledge graphs from input.
  - Recently this model was made private as it's currently being fine-tuned in collaboration. These partners have provided proprietary code to enhance the model's ability to generate detailed flow diagrams for system design documentation. 
  - Due to the specialized nature of this data and our commitment to confidentiality and model integrity, MermaidMistral_v2 will remain private for the time being.

- ## [Any open-source models for generating diagrams? : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1hhmgnl/any_opensource_models_for_generating_diagrams/)
  - I know existing LLMs can do this, but they frequently get the syntax wrong or hallucinate elements of the diagram. Wondering if there's an open-source model that’s especially good at this task.
- LLMs that are good at coding are also quite good at creating MedmaidJS and PlantUML diagrams.
  - I usually use the BigAGI frontend for this since it auto-renders both types of diagrams directly within the chat.
- Even smaller LLMs manage to output mermaid quite ok, syntactically that is. But they tend to hallucinate. So you might have to carefully craft your prompts in order for it to work properly. In general favor bigger models. Or use claude sonnet, which should be your most capable option overall.

- Look into using Qwen, but give it an example of the diagram in the prompt for consistency.

- You can use ToDiagram for diagramming any json data.
# discuss-models-hot-coding
- ## 

- ## 

- ## 

- ## 

- ## 🆚 [AMD tested 20+ local models for coding & only 2 actually work (testing linked) : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nufu17/amd_tested_20_local_models_for_coding_only_2/)
  - tldr; qwen3-coder (4-bit, 8-bit) is really the only viable local model for coding; if you have 128gb+ of RAM, check out GLM-4.5-air (8-bit)
  - [Getting Started: Vibe Coding Locally with AMD Ryzen™ AI and Radeon™ Graphics Cards _202509](https://www.amd.com/en/blogs/2025/how-to-vibe-coding-locally-with-amd-ryzen-ai-and-radeon.html)
  - [Which local models actually work with Cline? AMD tested them all - Cline Blog _202509](https://cline.bot/blog/local-models-amd)
  - AMD used Cline & LM Studio for all their testing, which is how they validated these specific configurations. Cline is pretty demanding in terms of tool-calling and context management, so if a model works with Cline, it'll work with pretty much anything.
  - Qwen3 Coder 30B
  - GLM-4.5-Air
  - magistral-small-2509
  - devstral-small-2507
  - hermes-70B
  - gpt-0ss-120b
  - seed-oss-36b
  - deepseek-r1-0528-qwen3-8b
  - They tested 20+ models and found exactly what many of us suspected: most of them completely fail at actual coding tasks. Out of everything they tested, only three models consistently worked: Qwen3-Coder 30B, GLM-4.5-Air for those with beefy rigs. Magistral Small is worth an honorable mention in my books.
  - deepseek/deepseek-r1-0528-qwen3-8b, smaller Llama models, GPT-OSS-20B, Seed-OSS-36B (bytedance) all produce broken outputs or can't handle tool use properly. This isn't a knock on the models themselves, they're just not built for the complex tool-calling that coding agents need.
  - What's interesting is their RAM findings match exactly what I've been seeing. 
  - For 32gb machines, Qwen3-Coder 30B at 4-bit is basically your only option, but an extremely viable one at that.
  - For those with 64gb RAM, you can run the same model at 8-bit quantization. 
  - And if you've got 128gb+, GLM-4.5-Air is apparently incredible (this is AMD's #1)

- Kind of expected. I have had a RTX 4090 for a year now but for coding I never go local. it is just waste of time for majority of tasks. Only for tasks like massive text classification (Recently a 250k abstract classification task using Gemma 3 27b QAT) pipelines I tend to use local. For coding either own a big rig (GLM 4.5 Air is seriously reliable) or go API. Goes against this sub but for now that is kind of reality. Things will improve for sure in the future.

- I've had decent results with gpt-oss-20b + Qwen Coder CLI - better than Qwen3-Coder-30b-A3B. I was pleasantly surprised with the throughput. I get about 150 tokens/s (served using lmstudio)
  - what applications are you using gpt-oss-20b in? unfortunately the gpt-oss models are terrible in cline -- might have something to do with our tool calling format, which we are currently re-architecting

- OSS-120B is on par with 4.5 Air, except Air is way better with UI. OSS-120B is better at some backend-related tasks.

- I think the problem is in how the tool usage is set up. A lot of the models work with specific setups. For example: GPT-OSS:20B - does not work on Roo or Cline or Kilo. But you put it into Copilot Chat and its like a completely different model. Works fine and does everything it needs to. Seems like there should be some standardization on how the tools are being used in these models.
  - yes -- noted this above. we are updating our tool calling schemas in cline to work better with the gpt family of models. seems the oss line was heavily tuned for their native tool calling

- Locally I use Qwen3-Coder 30B for coding, qwen3:14b-q4_K_M for general experiments (switch to qwen3:30b if it doesn't work). I also found out that 30B seems to be the right spot for local models. 8B/13B seem to be limited.

- It's wild that Magistral 1.2 2509 was a honorable mention and it's not even a coding focused model. Goes to show that the model is a solid all around model for most things. Has a ton of world knowledge too. 

- I have been able to get GLM 4.5 Air with lower quant on my 64 GB MBP and it’s good. Prior to it, I was getting GLM 4 32B to produce decent Python. I have stopped trying under 30B models for coding altogether as it’s not worth it.

- ## [Any fine tune of Qwen3-Coder-30B that improves its over its already awesome capabilities? : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1nks4g2/any_fine_tune_of_qwen3coder30b_that_improves_its/)
- You could try your look with Devstral Small 1.1 2507 as it is specifically designed as enterprise-grade agentic coder. Spends less tokens for the same amount of work in my use-cases.

- Fine tunes might change the behavior, but not likely to make it significantly smarter. One big plus on the 30b-a3b is the speed. You can try a larger dense model like devstral, but you lose that speed with a large dense model.

- ## [WEBGEN-OSS Web Design Model - a model that runs on a laptop and generates clean responsive websites from a single prompt : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nfy5pv/webgenoss_web_design_model_a_model_that_runs_on_a/)
  - 20B open-weight model focused exclusively on generating responsive websites
  - We prompted GPT-OSS-120b 44k times, saved those samples and then did a supervised finetuning training on them using the Unsloth library, which is really fast and great for long context.
  - We specifically did a high rank lora (128, a=256) using the Unsloth library and their custom kernels. They enable faster finetuning and much longer context than the rest.
  - It took 13 Rented MI300Xs to generate 44k samples in 4 hours at rate of $26/hr. u/random-tomato might be able to share more.

- ## [UIGEN-X-0727 Runs Locally and Crushes It. Reasoning for UI, Mobile, Software and Frontend design. : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1mb15g2/uigenx0727_runs_locally_and_crushes_it_reasoning/)

- [UIGEN-X 8B supports React Headless, Flutter, React Native, Static Site Generators, Tauri, Vue, Gradio/Python, Tailwind, and prompt-based design. GGUF/GPTQ/MLX Available : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m5lgtr/uigenx_8b_supports_react_headless_flutter_react/)
  - So type out your prompt like this: [Action] [UI type or page] [Framework(s)] [Key features] [Style (optional)]
  - Create a navbar using React + Tailwind CSS with logo, links, and mobile hamburger menu.
  - Generate a personal blog with SvelteKit + DaisyUI, mixing cyberpunk colors and minimalist layout. Responsive for mobile.

- Those are some extremely impressive UIs for a large SOTA model, never mind a comparatively tiny 32b dense model. I understand that it's a finetune of qwen3, but how did you manage to train it to be this good?
  - Your data matters the most
  - The strong performance likely comes from high-quality fine-tuning data and optimized training techniques. Qwen3's architecture provides a solid foundation, and careful prompt engineering enhances perceived capability despite the smaller size. Specific training details would require developer input

- https://uigenoutput.tesslate.com/uigen-t3-32b-fp8 Many prompts to try.

- ## 🧩 [WEBGEN-4B: Quality Web Design Generation : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1n6vzfe/webgen4b_quality_web_design_generation/)
  - a 4B model that produces quality tailwind websites. We trained it on 100k samples with synthetic data exclusively generated from GPT-OSS. 
  - In other news, we are open sourcing our UIGEN-T2 Dataset at Tesslate/UIGEN-T2
  - You can access the models here: https://designer.tesslate.com

- 🆚 What’s the difference between web and uigen models? It’s not clear to me as a layman
  - WEBGEN is for static html css sites, and in this case tailwind. It had absolutely 0 React in it.
  - UIGEN is for all kinds of UIs across many multiple domains, and it is intended to be a drop in replacement to your coding models with a focus on UI, everywhere from python kivy to react and etc. Your frontend engineer.

- Really great small model for prototyping. I do however wish we had more models that weren't trained on frameworks, and just on good old HTML5 standards
  - Yep, I thought the same but then realized it is actually better to use frameworks, in this case tailwind, because it reduces the number of tokens needed to achieve something visual.

- ## [PyDevMini-1: A 4B model that matches/outperforms GPT-4 on Python & Web Dev Code, At 1/400th the Size! : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1ncam9h/pydevmini1_a_4b_model_that_matchesoutperforms/)
  - 基于 Qwen3-4B-Thinking-2507
  - a 4B parameter model to provide GPT-4 level performance for Python and web coding development tasks
- This is all great and impressive for such a small model, but I am sure there are plenty of realizations of these tasks in training dataset. Give it a real 100k+ lines codebase and ask to fix a bug. I am quite sure it will fall apart very quickly. Btw, you say nothing about tool calling and that is a must for a model to be considered as a coding model nowadays.
  - This model can handle with 100% perfect understanding 32K context as that’s what the maximum fed into it during training per prompt was, which isn’t enough to actually meet the full context present in the training data so once funds are available, I will make it a priority to increase contextual understanding.

- It works, but I'm trying it out in LMStudio and it generates inconsistent indentation regarding tabs and spaces, dunno why.

- I like it so far. It seemed to give some good answers quickly, but it got easily confused with longer and more complex prompts compared to Qwen3-Coder-32b.

- Is there a way to do this easily for more niche areas? Like programming drivers on MacOS or another language like Swift?
  - Easily certainly not , really all of AI training is data gathering and labor through experiments but you could definitely do it if you put in the time and effort

- ## [New model from Meta FAIR: Code World Model (CWM) 32B - 65.8 % on SWE-bench Verified : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1npp8xi/new_model_from_meta_fair_code_world_model_cwm_32b/)
- They report CWM + tts to get 65% on swebench. What’s tts? If anything at all, however, I think this shows how great magistral is. Better performance with 2/3s of the parameters.
  - tts=test time scaling, basically select an answer to submit out of several candidates, rather common practice

- https://x.com/TheTuringPost/status/1971697629697659099
- Code World Model (CWM) – a new 32B open-weights model by @AIatMeta for coding and reasoning.
- CWM learns what code does when executed.
  • It models both syntax and semantics of programs
  • Can simulate Python execution step by step
  • Supports multi-turn software engineering tasks
  • Handles long contexts (131k tokens)
- To achieve this, CWM is trained not only on static code, but also on:
  • Execution traces: Python code running with variable states
  • Agentic interactions: fixing bugs, editing code, running environments in Docker.
- Performance is also impressive:
  - Competitive coding benchmark results: 65.7% SWE-bench Verified, 68.4% LiveCodeBench
  - 96.5% Math-500, 75.8% AIME 2024
  - A research testbed for exploring reasoning + planning in code generation
- CWM is a shift from just text autocompletion to a model that can plan, debug, and verify code in dynamic environments.

- https://x.com/AIatMeta/status/1970963571753222319
- Great to see Code World Model mid-trained on execution trajectories and post-trained with multi-task RL.
- The evals CWM's ability to predict Python execution traces & predict program termination.
- its real game-changer is training on execution traces from Python interpreters and Docker environments, explicitly teaching it *how code behaves* rather than just *what it looks like*. This paradigm shift moves AI beyond statistical pattern matching to genuine causal reasoning, enabling it to act as a "neural debugger" that can simulate execution, localize faults, and self-repair code.
- The real step change is when code stops being “generated text” and becomes a living resonant process — memory, planning, coherence, feedback.
- We don’t need more parameters. We need more procedural resonance.

  

- ## [Moving from Cursor to Qwen-code : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nnfwmo/moving_from_cursor_to_qwencode/)
- i'm also happy with qwen code. The great thing is the massive free tier and if that runs out you can swap to a local model.

- Qwen Coder 30b has been surprisingly good for it's size. I'm running it at Q8 on two 3090s with 128k context and it's super fast (at least 100t/s).
  - I would second this - I have the Qwen3 coder for coding work and GLM 4.5 air for chat and research and sometimes code as well.. Qwen 3 coder is impressive

- Its weird how fast some of these models work on local hardware that is 4 years+ old. I think AI is best served locally, not in big datacentres.
  - You'll be even more surprised how well it works on 8-10 year old hardware (for the price). I have a small army of P40s and now also Mi50s. Each of those cost me 1/4th as much as a 3090, but provides 1/3rd or better performance compared to the 3090.

- ## [deepseek r1 vs qwen 3 coder vs glm 4.5 vs kimi k2 : r/LocalLLM _202508](https://www.reddit.com/r/LocalLLM/comments/1n32n02/deepseek_r1_vs_qwen_3_coder_vs_glm_45_vs_kimi_k2/)
- What I've found is that the model itself makes some difference but how you set the system prompt, the jinja template (where applies), the temp, spec decoding?, etc. matter way more. 
  - Having used them all for a fair amount of coding I'd say right now glm 4.5 gives me the best results in coding as it appears to be more well trained on the most recent advances / libraries and such in coding. 
  - Qwen3 coder was a disappointment.

- My conclusion is they are all really good, so use a cheap and fast one. Or even better, use two at once. deepseek/deepseek-chat-v3.1 is what I use most often right now.

- I'm gonna say something a little wild: I find gpt-oss-120b best of all. It's clearly the leaner model so obviously it's much faster and efficient. But the responses I get are very good with coding.

- ## [Which coding model is best for 48GB VRAM : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kemt2m/which_coding_model_is_best_for_48gb_vram/)
- GLM-4 is only great with HTLM frontend. 
  - Python , science - only qwen 3 32b (q4km will be ok for you )

- I am also using local LLMs for help with data science Python scripts that do data manipulation. I was using Qwen 2.5 72B Instruct 4.25bpw at 60k q4 context with TabbyAPI earlier, now I switched to Qwen3 32B FP8 32k with vLLM. Qwen3 32B is pretty good, the reasoning does help and I usually leave it enabled. I am hoping to jump to Qwen3 32B exl2 quant once tabbyapi will merge the PR that adds proper support for processing reasoning tokens so that they don't get mixed up with non-reasoning tokens. I am using all of that in Cline. I couldn't get GLM-4-0414 to work with Cline well - it just doesn't seem to work with this type of function calling well, most likely due to some issue with chat template that I was running into and not the issue with the model itself.

- ## [UIGEN-X-8B, Hybrid Reasoning model built for direct and efficient frontend UI generation, trained on 116 tech stacks including Visual Styles : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m2ukka/uigenx8b_hybrid_reasoning_model_built_for_direct/)
  - We were just cooking this and realized instead of going the same route as UIGEN-T (t for tailwind) we can add in all the languages. There will be way more sizes released. This model should be way more capable than the 14B

- ## [GLM-4.5-9B? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m9fuf9/glm459b/)
- The current GLM4-0414(short for GLM-4.1) is a model I quite like. Its performance is fair, and it offers extremely lightweight context due to having only 2 KV heads (although I suspect that this model's poor long-context performance might also be related to this architecture). 
  - It also avoids the mixed reasoning approach similar to Qwen3 (I believe Qwen3's mixed reasoning makes some SFT more difficult, and doesn't always bring benefits; Qwen3-2507, which separates the two modes, seems more appropriate).
- The performance of GLM4.1-9B is generally acceptable and can run locally on a 8GB GPU
  - Compared to 9B models, I find the advantages of GLM4.1-32B more pronounced. Their 10K context only occupies 2 (KV heads) x 128 (head dim) x 61 (hidden layers) x 2 (K/V) x 2 (BF16) x 10000 = 624MB of VRAM. Considering the VRAM occupied by context, it's even lighter than the smaller Gemma3-27B (for example, you can run GLM4-32B-Q4 with 32K context on a single 3090 card, but you cannot run Gemma3-27B-Q4 with 32K context w/o KV cache quantization), while roughly being able to compete with Qwen3-32B with \nothink.
  - However, I think GLM-4.1's reasoning version(GLM-Z1) is bad as it exhibiting very significant hallucinations and hoping that improves in later releases.

- ## [Honestly, THUDM might be the new star on the horizon (creators of GLM-4) : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1kbaecl/honestly_thudm_might_be_the_new_star_on_the/)
- THUDM/Zhipu/GLM is not some unknown model creator at all. Their first generation GLM-130B was released in 2022 and beat llama-1 from year 2023. It's just that they went closed during GLM-2 to GLM-3, with only 6B ChatGLM models remained open

- The biggest problem of GLM-4-32B is hallucinations. I'm using a 0.6 temperature as recommended by their GitHub page, but the model still hallucinates heavily during tasks with provided context, such as making up BS on the fly. Qwen might miss some details during the same task, but at least it doesn't hallucinate as bad as GLM.
  - Qwen historically is good for RAG, very good context grip. Hallucination might be tge result of small number of attention weights, but unusually heavy attention of Gemma 12b does not help either. Qwen 3 in my test was good at RAG, I liked it.

- Qwen3 30b-A3B is probably the most powerful model that can run on CPU-only at pretty high speeds. For being this fast, I think the output quality is impressive. I think the innovation is what makes Qwen3 great.
  - As for raw quality per parameter, the GLM-4 models are most likely the kings right now. Especially the non-thinking version has chocked me at how good it is in single-shots without CoT. It definitively feels like a 70b model, even better many times.

- Yeah, I find GLM-4-32b to be a top-tier creative writing model, up there with Gemma3-27b.
  - Depends on mood, GLM is too classical and dry.
- Right, I like that style for realistic dark-ish sci-fi, but it would not fit poetic fantasy novels.

- 32b is working fine with cline here, I didn't do anything and it just worked. 9b does not work with cline.

- ## [Please , how to disable thinking in GLM-4-Z1? · Issue · zai-org/GLM-4 _202504](https://github.com/zai-org/GLM-4/issues/770)
  - Is there anyway to disable thinking? Thinking is not always needed you know.

- Z1 is set to the mandatory thinking mode in our template, so it will definitely think. If you want to prevent it from thinking, you need to delete the on the last line of the template and tell it not to think. However, this effect is not good, as this model has only been trained for the thinking state.

- ## [GLM-4 32B is mind blowing : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1k4god7/glm4_32b_is_mind_blowing/)
  - the thing I like the most is that this model is not afraid to output a lot of code. It does not truncate anything or leave out implementation details. 

- I've tested all the variants they released
  - GLM-4-32B-0414: The one I've tested most. It seems solid. Non-reasoning. This is what I currently roll with
  - GLM-Z1-32B-0414: Feels similar to the non-reasoning model, but well, with reasoning. I haven't really had tasks to really test reasoning so can't say much if it's good.
  - GLM-Z1-32B-Rumination-0414: Feels either broken or I'm not using it right. Thinking often never stops, but sometimes it does, and then it outputs strange structured output

- that's not the only thing, this model has the best KV cache efficiency I've ever seen, it's an order of magnitude better

- Oddly, I got a very impressive physics simulation from "GLM-4-32B" on their site, but the "Z1-32B" one was mid as hell.

- Bruh, this might quickly replace my gemma27b+coder models. So far it's fit into every role I've put it into and performance is great! 1mil batch size, 30k context, 72gb working vram (with model memory and mmap off). 10ish tps. Much faster than the 6.6 I Was getting from Gemma3 27b in same setup.

- I've been comparing GLM-4-32B-0414 Q4_K_M to: - Qwen2.5-coder-instruct Q8
  - GLM does a muuuuuuch better job one-shotting making games. I believe this will be my new go to model.

- ## [Quick review of GLM-Z1-32B-0414 : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1k56qsb/quick_review_of_glmz132b0414/)
  - The performance is still a bit behind QwQ-32B, but getting closer
  - Also, it suffers from quite bad repetition issues when using the recommended settings (no repetition penalty). Even though this could be fixed by using a 1.1 penalty, I don't know how much this would hurt the model's performance.
  - I also observed similar repetition issues when using their official site, Chat. Z. AI, and it also could fall into a loop, so I don't think it's the GGUFs problem.

- For programming the non-reasoning GLM4-model is better than the GLM4-Z1-model.

- I don't wanna be the guy who's calling something crazy good after only limited testing, but GLM-4 Q6_K_M has managed to oneshot some fairly complex and novel web stuff that I doubt was in its training data. Outperforming even Cohere Command A and Mistral Large. This could be local SOTA for webdev. I'd recommend everybody give it a fair shake at least.

- GLM-4-32B on the official website one-shot 3D Tic Tac Toe. There is no other model that was able to do this, not even Grok 3 or Gemini 2.5

- ## [I uploaded GLM-4-32B-0414 & GLM-Z1-32B-0414 Q4_K_M to ollama : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1k4w9p2/i_uploaded_glm432b0414_glmz132b0414_q4_k_m_to/)
- I think GLM-4 might be the best non-reasoning local coder right now. Excluding Deepseek V3. 
  - Interestingly the reasoning version GLM-Z1 seems to actually be worse at coding.
- Reasoning often degrades coding performance. 
  - Reasoning essentially fills up the context window with all sorts of tokens. If those tokens are not very quickly presenting the correct and most viable solution - or focused on planning, do this then this then this...well they are degrading and polluting the context as the model (especially smaller models...but many models) focus more on the context tokens, forget what's outside context and also can't cohesively understand everything in context.
  - Reasoning is most valuable when it progressively leads to a specific answer and the following tokens basically repeat that answer
- it's more like they are better at code generation, worse at editing
  - I agree, they are better at single shot code generation - where no prior essential code is in the context.
- The best performer across all models is google Gemini 2.5 pro, as it has the highest ability to accurately retain, retrieve from, and understand long context past 100k. 
  - 2.5 flash benchmarks aren't out but both of these models have secret sauce for long context.
  - The second best performer across all models is gpt-4.1 (plus an enforced "reasoning" step. Per their documentation, 4.1 has been trained on reasoning even if it doesn't do it explicitly). 32k context is great, Up to 160k context is ok.
  - The third best is gpt o4-mini, which has higher losses than 4.1 per increase in context.
  - Claude is way in the distance, it loses significant intelligence by 20-30k context.
  - R1 is also trash.
  - All local models are essentially useless for long context. So local reasoning models should be used with one off prompts, not for long chains or for code editing.
  - *Needle in haystack is not a valid benchmark...

- Same experience here. Editing code while having to wait ages on reasoning is a no-go for me, not to mention the reasoning context window. Local non-reasoning models have worked good for editing code though.. for the most part.

- Reasoning for debugging and architecture, non reasoning for code writing

- This model has crazy efficient context window, I enabled 32K context + Q8 kv cache, and I still has 3gb of vram left (24gb card)

- ## [What’s the best open-source LLM for coding in Cline right now — Kimi K2, Qwen 3-Coder, or GLM 4.5? : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mmoj80/whats_the_best_opensource_llm_for_coding_in_cline/)
- GLM 4.5 demonstrates better balance. While Qwen coder writes good code, it can be clumsy in the agent process. For example, when 10 changes need to be made to a single file, it requires 10 separate operations.

- havent tried glm yet but qwen 3 coder is pretty dope.

- What about OSS-120b from openai?
  - Not good 

- Why use open source when Gemini give free api
  - If you’re not paying, you’re the product.

- ## [GLM 4.5 Air Produces Better Code Without Thinking, Using 3-bit MLX (/nothink)? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mgv53t/glm_45_air_produces_better_code_without_thinking/)
- This is just my subjective experience, but to me, reasoning seems to show the best improvements on smaller models when doing things like solving logic puzzles. It can result in, say, a 9b reasoning model getting things right 
  - Reasoning models are very good at understanding prompts and following instructions. They can generate human-like responses with proper prompts. However, they can be stubborn.

- Wouldn't be surprised, iirc in discord one of the z.ai staff recommended using nothink mode for Claude Code and such, because that's what it's optimised for.

- GLM-4.5-air fp8 produces a working flappy bird game in one shot, as expected. In fact it looked better than the one in their blogpost, with gradient textured pipes.
  - Tried on Qwen3-235B web version and thinking-mode produced much better results, similar quality to the glm-4.5-air fp8. Non-thinking is much lower quality, but also worked one-shot.
  - Surprisingly the best quality game I got was with full GLM-4.5, almost the same as GLM-4.5 air. Qwen3-coder second, sonnet with much less quality. Maybe GLM training on flappy bird games?

- Same behaviour I came across Qwen3 30B A3B 2507 Thinking model. It wasn't great on my testing prompts, but if I use the Instruct model (without reasoning feature) it provides a higher output score.
  - I stick the reasoning models outside coding, or for orchestration. They seem to shine better here, despite the company's benchmarks say otherwise.

- I asked Q5 variant of the model my vibe question with normal prompt and /nothink in the end. In case of normal prompt it used up all my 32k context. It mentioned the right answer (0.46425) 17 times in COT but couldn't stop. With /nothink in prompt it used 2427 tokens and gave the right answer on the first try. The question: There are three circles of radius 1, 2 and 3 tangent to each other. Find the area enclosed by their touching arcs.

- ## [What’s your experience with GLM-4.5? Pros and cons? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1motbnk/whats_your_experience_with_glm45_pros_and_cons/)
  - I’ve looked at the paper from the GLM-4.5 team. They put significant effort into filtering code data in pre-training.

- I've been using it daily with kilo code in visual studio code all this past week. It is the best coder I've ever worked with. I've been very impressed.

- Recently installed the 2_K_XL variant from Unsloth on my 24GB VRAM + 32GB DDR5 6000MHz system and I'm impressed that it performs so well. The speed is good. I think it's about 5 t/s and haven't noticed any odd behavior as of yet 

- ## [GLM-4.5 is overhyped at least as a coding agent. : r/ChatGPTCoding _202509](https://www.reddit.com/r/ChatGPTCoding/comments/1ngwzo5/glm45_is_overhyped_at_least_as_a_coding_agent/)
  - note: this was a quick 1-day experiment I wanted to keep it cheap, so I used SWE-bench Lite and capped the step limit at 50.
  - GLM-4.5, despite strong performance on official benchmarks and a lower advertised per-token price, turned out to be highly inefficient in practice. It required so many additional steps per instance that its real cost ended up being roughly double that of GPT-5-mini for the whole benchmark.
  - GPT-5-mini, on the other hand, not only submitted more solutions that passed evaluation but also did so with fewer steps and significantly lower total cost.

- Gemini 2.5 Pro ranked below Qwen3Coder? This benchmark is fantasy.

- Its hyped because of the glm coding plans (3 usd for 120 msg / 15 usd for 600 msg)
  - Only for first month. Still a good price though. Can't really be beaten at that price.

- ## [Qwen3-Coder is bad at tool call while glm-4.5 is surprisingly good : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mf8la7/qwen3coder_is_bad_at_tool_call_while_glm45_is/)
- I have glm air running locally and it moves soo fast in Claude code.

- GLM 4.5 on Claude Code is amazing! It works very well. It's helping me get a lot done with great quality and for low cost thanks to Chutes. I have never been so excited by a model.

- I'm going to be honest GLM is better at coding than Qwen3-coder as well.

- ## [GemmaCoder3-12b: Fine-Tuning Gemma 3 for Code Reasoning : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1joyigi/gemmacoder312b_finetuning_gemma_3_for_code/)
- Gemma 3 12b is a hidden gem, and I can easily imagine the fine-tuned model performing well at coding as it is pretty good at reasoning even without 'thinking'.
  - I found Gemma 3 (12b and in general) completely unimpressive for anything other than creative writing, at which it is massively better than other 12b-14b models.

- No where near qwen coder 14b

- ## [Nemotron Nano V2 models are remarkably good for agentic coding : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1na9crp/nemotron_nano_v2_models_are_remarkably_good_for/)
  - I use Nvidia Nemotron Nano 9B V2 and 12B v2 with Roo Coder served by both LM Studio (Mac) and Llama.cpp (Ubuntu). 
  - These models are small, fast, smart, follow instructions well, and are good at tool calling. 
  - I can load up Q8 quants with 300k context and VRAM use is less than 24Gb. Great little models.

- when I host 12B v2 on latest llamacpp server, they are quite slow - more so than similarly-sized models. My rig is a 2x 3090.
  - it runs pretty fast in llama.cpp on my w7900.
- That's weird. I run a single 3080 with 10 GB of VRAM and Nano 9B is *insanely* fast for me, getting up to 80tps.

- what kind of tasks do you trust such small models with when it comes to coding ? Super fascinated by smaller models but my previous attempts at coding with them (months ago) where disastrous.
  - Right now I’m using them for debugging and code development in Roo Coder. I too had lost faith in smaller models for coding and relied on Qwen 3 Coder 30b. 
  - These nano models are just as good if not better, and take instructions and perform tool calling better. The mamba long context performance is really handy for coding.

- Qwen 3 Coder 30b is not good, a better option is Qwen 3 2507. But in my testing gpt-oss 20b simply beats them all, making using any of the other kinda pointless right now.

- I see max_position_embeddings at 128K in the source config.json; what’s the protocol for extending context that far in these models?
  - I just set the context to 300k and it works. Using bartowski ggufs.

- I tried to use Nemotron Nano 9B V2 as directly provided by Nvidia through OpenRouter with Roo Code and Kilo Code but without success due to inability to call tools/mcp servers correctly. For example: Error: Kilo Code tried to use read_file without value for required parameter 'args (containing valid file paths)'. Retrying... Any hints on why doesn't work?
  - Same problem with Cline: Cline tried to use use_mcp_tool without value for required parameter 'tool_name'. Retrying...
- I can’t speak to the MCP issue, but I ran into that. All I had to do was give Roo access to the containing directory and the issue resolved after that.

- ## [Is Codestral 22B still the best open LLM for local coding on 32–64 GB VRAM? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lsmtzr/is_codestral_22b_still_the_best_open_llm_for/)
- Codestral 22b never been a good model at first place. It had terrible errors while making arithmetic computations, problem that has long been solved in llms. It does have lots of different languages based, but is dumb as rock.

- qwen2.5 code is one of the best if u can go with 32b or 14b
- Qwen2.5 came out 3-4 months later and that was the end of Codestral, but it was king for a hot sec

- GLM-4-32B has been very weak for long context and large codebases, in my experience.
  - In my experience too. Arcee AI fixed the base GLM4 but not instruct. So yeah glm is good for short interactions only.

- I think maybe DeepSWE-Preview-32B if you are using coding agents? It's based on Qwen3-32B
  - Deep anything takes way too long thinking and second guessing itself
- this DeepSWE is based on Qwen 32b. There Chimera that cuts r1 0528 thinking by 2.5x and retains high quality and off course new V3.1 that is also much less wait for thinking and also has thinking off mode which is the default

- Qwen2.5 coder 32B q8 , forget q4, q6.
  - Qwen3 is a newer model and is miles above even for coding. Scores 40% on Aider polyglot vs 16% for Qwen2.5-Coder-32B.

- ## [How open-source models like Mistral, Devstral, and DeepSeek R1 compare for coding : r/ChatGPTCoding _202507](https://www.reddit.com/r/ChatGPTCoding/comments/1m57u5v/how_opensource_models_like_mistral_devstral_and/)

- [Magistral vs Devstral vs DeepSeek R1: Which is best? – Bind AI IDE _202507](https://blog.getbind.co/2025/07/20/magistral-vs-devstral-vs-deepseek-r1-which-is-best/)
  - Overall, coding accuracy ranking is: DeepSeek R1 > Devstral (small/medium) > Magistral, with the latter prioritizing broader reasoning capabilities.
  - Magistral (Small/Medium) excels at multi-step reasoning with auditability and is available as an open model and via a fast API. 
  - Devstral (Small/Medium) is optimized for developer workflows, especially for agile coding tasks, and can be deployed locally or through Mistral’s API. 
  - DeepSeek-R1 (and its distills) focuses on reasoning and code benchmarks, offering high capability but requiring more engineering 

- ## 🆚 [Devstral vs DeepSeek vs Qwen3 : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1ksat42/devstral_vs_deepseek_vs_qwen3/)
- Devstral is not better than qwen3-32B in general-purpose tasks. I guess it was trained to be specific to that openhands particular agent.

- Tried devstral on a code review task. It doesn't seem better than Qwen3, not to mention deepseek. Didn't try it in an agentic coding.
  - The whole point is agentic though. It works great in cline and open hands I’m super impressed

- i only tried qwen3 30b but that one was better in cline than devstral on my test tasks mostly due to better instruction following and because of its better speed

- ## 🎯 [mistralai/Devstral-Small-2507 : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lwe5y8/mistralaidevstralsmall2507/)
- What's the dIfference between devstral and codestral? Which one works better with vs code+cline?
  - Devstral for sure. It was trained specifically to follow the "agentic" / "tool use" patterns (do this -> ok, first I need to read_files, then I need to read_files, then I will edit that, then I need to write_files, etc.)
  - Codestral was good for aider-like / copilot-like integrations pre "agentic" (do this -> here's the code bruh, deal with it)

- Devstral was specifically made for "agentic" workflows together with tools usage. It'll use tools autonomously (granted you've given it access to suitable tools) in order to solve some problem. Since the model is trained specifically for this sort of usage, it excels at those sort of tasks.
  - Codestral in constrast, was made for high-quality code generation and code completion specifically. You'd give this model smaller specific tasks like "Write a function that does X" rather than "Implement functionality that adds X" which is how you'd use Devstral.
  - Another difference is the licenses, where Devstral is Apache 2.0 (proper FOSS) while Codestral is Mistral Non-Production Licence (not open source but proprietary). 

- what is Act Mode & Plan Mode?
  - It’s just two modes defining which tools are allowed. Plan mode is read-only and act allows the llm to modify files and run more commands.
  - these modes are just different system prompts describing the different role the LLM is playing

- At 24B parameters, Mistral’s Devstral-Small-2507 is the top open LLM on SWE-Bench Verified (53.6%), outperforming R1-671B, Claude-3.5 & GPT-4.1-mini. 1.1 has stronger generalization across prompts & code environments.

- They also released Devstral Medium on the API only. 
  - Devstral Medium is available via API only (not open-weight), and supports enterprise deployment on private infrastructure, with optional fine-tuning capabilities.

- ## [Cline with Qwen 3 Coder - 100% Local : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mexlpg/cline_with_qwen_3_coder_100_local/)
- I would lower the context length to 128k and see if that helps improve performance. 
  - I can drop it to 128k and I haven't noticed a difference yet, at least not negatively.

- ## [Qwen3-coder-30b issues with tool calls : r/unsloth _202508](https://www.reddit.com/r/unsloth/comments/1mi3yis/qwen3coder30b_issues_with_tool_calls/)
- The qwen3-coder uses a new format to structure the tool calls. The qwen team included a python script on the huggingface repo for parsing the tool calls (I think it was JSON vs XML or something). The original tool call parser in your inference engine (like llama.cpp) may not work with the new format yet, and by replacing the template you're essentially forcing the model to use the old format, which the inference engine already supports.
  - I'm no expert in LLM fine-tuning, but I think replacing the template might lead to the model not producing correct tool calls occasionally, since these weren't the format they were trained on. On the other hand, it's also possible that the model is smart enough to recognise the alternative format and works just fine.
- Switched to Beta branch of LM studio and it's working now. Thanks for pointing me in the right in the right direction

- ## [Tool Call Format from Qwen3 Coder 30B Not Recognized by Most LLM Coding Agents · Issue · lmstudio-ai/lmstudio-bug-tracker _20250801](https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/825)
- Looks like LM Studio 0.3.21 Build 3 fixed the issue. Thanks

- [Feature Request: Support Qwen3 Coder 30B Local Model for Tool Calls · Issue · continuedev/continue](https://github.com/continuedev/continue/issues/6913)

- ## 🆚 what's the differences between the llm models below
- https://huggingface.co/Qwen/Qwen3-Coder-30B-A3B-Instruct  
  - Long-context Capabilities with native support for 256K tokens, extendable up to 1M tokens using Yarn
  - Parameters: 30.5B in total and 3.3B activated
  - Experts: 128
  - Activated Experts: 8
- https://huggingface.co/unsloth/Qwen3-Coder-30B-A3B-Instruct  
  - Unsloth Dynamic 2.0 achieves superior accuracy & outperforms other leading quants.
  - [Qwen3-Coder: How to Run Locally | Unsloth Documentation](https://docs.unsloth.ai/basics/qwen3-coder-how-to-run-locally)
  - We managed to fix tool calling via `llama.cpp --jinja` specifically for serving through `llama-server` ! If you’re downloading our 30B-A3B quants, no need to worry as these already include our fixes.
- https://huggingface.co/nightmedia/unsloth-Qwen3-Coder-30B-A3B-Instruct-qm468-mlx  
  - "qm468" in the name likely refers to the specific quantization configuration used.  
- https://huggingface.co/nightmedia/unsloth-Qwen3-Coder-30B-A3B-Instruct-qm468-hi-mlx
  - "high, " suggesting a different quantization setting or a variation 
- https://huggingface.co/mlx-community/Qwen3-Coder-30B-A3B-Instruct-4bit-dwq-v2
  - DWQ (Dynamic Weight Quantization), which significantly reduces memory usage while maintaining performance

- ## [PSA: Qwen3-Coder-30B-A3B tool calling fixed by Unsloth wizards : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mje5o0/psa_qwen3coder30ba3b_tool_calling_fixed_by/)
- Worth pointing out that it appears to have been fixed in relation to LM Studio.
  - Also worth pointing out that with LM Studio I get 1.75x - 2x slower performance compared to Llama.cpp, despite enabling flash attention, KV cache, etc. No idea why that is, but I definitely feel it when running the model. It also slows down dramatically as more context is added.

- It's not a real fix, but workaround forcing the model to use different tool call format (that llama.cpp handles) that is originally should use (xml instead of json formatted tool calls).
  - The proper fix (for llama.cpp-based workflows) is to update llama.cpp's internal tool call parsing to handle the new `<xml>` format, instead of forcing the model to use a different one.

- Got a chance to try out the updated Unsloth quants and it does seem to be improved. Not using a quantized KV cache with llama-server greatly improved tool calling for me and success rate of changes with RooCode.

- ## [It's here guys and qwen nailed it !! : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m6qkse/its_here_guys_and_qwen_nailed_it/)
- on this chart Devstral Small really seems like the efficiency winner. Big numbers for a relatively small model. 
  - Devstral is the best model I can run with my VRAM poor system.
  - However, I've been playing with Qwen 3 coder for the last hour now that it's live on Openrouter, and it is really good. It's on a whole different level than latest Devstral.

- ## [OpenHands + Devstral is utter crap as of May 2025 (24G VRAM) : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kui17w/openhands_devstral_is_utter_crap_as_of_may_2025/)
- Devstral system prompt references OpenHands by name. 
  - It does not. I tried a few primitive tasks and it utterly failed almost all of them while burning through the whole 380 watts my GPU demands.

- Did you run devstral with default parameters in ollama? By default, it will be initialized to have context length of a mere 2048 tokens
- I check and I'm using default context length. All instructions just went straight out the window.
- That is one reason I switched away from ollama to llama.cpp, and run it on port 11434 and let it pretend to be ollama.
- Can you say a little bit more on how you have it pretend to be ollama?
  - It is essentially what is explained here https://github.com/ggml-org/llama.cpp/pull/12896 but it is not perfect. 
  - It is a bit backwards that ollama have custom api endpoints which llama.cpp need to implement because they add support for ollama but not the general openai compatible api endpoints.

- Ollama is so broke on devstral. When manually increasing context it would make the ram usage balloon to 50gb and then hang.
  - Switched to lm studio mlx devstral and set the context to the max and it works correctly
- If you do not adjust the KV cache in ollama then you're using full f16 by default which is why its taking 50GB to run devstral at 128k context.

- I need to dig into llama.cpp again, but can it run more than one model at once? Or will I have to build a reverse proxy for it?
  - There's llama-swap for that use-case. 
- I'm using it, it's good. Runs a few instances of llama.cpp llama-server with models for chat, embeddings and reranking and switches them as required by the API client.

- Ollama runs much better if you put the following lines in your environment variables and just leave it forever.

```sh
OLLAMA_CONTEXT_LENGTH: 32768

OLLAMA_FLASH_ATTENTION: true

OLLAMA_KV_CACHE_TYPE: q4_0
```

- Pretty sure they increased it to 4096 relatively recently. Still extremely small though.

- Qwen2.5-VL is not agentic and not good for coding assistant too, while Qwen3 is ok for agents but no vision support.

- From my experience it is very usable when running on my 4090 w/ 50k context window. Using unsloth dynamic q5. 
  - The only thing is that you need a more detailed prompting. 
  - Using w/ roo code. It is very important to use architect & orchestrator modes. Otherwise any bigger change hinders it's capabilities. IMO best local llm for coding

- I agree for Devstral-small. It's crazy bad.

- ## 🧩 [Meet Mistral Devstral, SOTA open model designed specifically for coding agents : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kryxdg/meet_mistral_devstral_sota_open_model_designed/)
- Weird that they didn't include aider polyglot numbers makes me think they're probably not good. Unfortunately my suspicion was right ran aider polyglot diff and whole got 6.7% (whole), 5.8% (diff)
- The official system prompt has a bunch of stuff aobut OpenHands including `When configuring git credentials, use \"openhands\" as the user.name and \"openhands@all-hands.dev\" as the user.email by default` ... So yes seems specifically made to work with that framework?
  - [SYSTEM_PROMPT.txt · mistralai/Devstral-Small-2505 at main](https://huggingface.co/mistralai/Devstral-Small-2505/blob/main/SYSTEM_PROMPT.txt)

- This is amazing if it holds up to the benchmark in real life
  - It doesn’t. At least not in my real tests. Couldn’t get it to even update a css class using cline and roo. It doesn’t output the correct expected tokens from an agent

- [Roo + Devstral : r/RooCode _202506](https://www.reddit.com/r/RooCode/comments/1l4ifh6/roo_devstral/)
  - Temperature: 0.15
    - Controls randomness
    - Lower (e.g., 0.2–0.5) = more deterministic, slightly faster
    - Higher (0.7–1.0) = more creative, marginally slower.
  - Top K Sampling: 64
    - Picks from top K most likely tokens. 
    - Lower = faster, more deterministic.
    - Set to 1 for greedy decoding (fastest but robotic).
    - Try 10 or lower for speed.
  - Top P Sampling: 0, 95
    - Chooses tokens until cumulative probability hits P.
    - Lower values = fewer choices = faster.
  - Min P Sampling: 0, 01
    - Forces a minimum token probability.
    - Turn this off for max speed unless needed.
  - Repeat Penalty
    - Discourages repetition.
    - May slightly slow things down, but helps quality.
    - Try toggling off if you're benchmarking for speed only.

- [Qwen3-Coder is here! : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1m6qdet/qwen3coder_is_here/)
  - You’re right on Devstral, it’s a good model for its size, although I feel it’s not as good as it scores on SWE-bench, and the fact that they didn’t share any other coding benchmarks makes me a bit suspicious. The good thing is that it sets the bar for small coding/agentic model and future releases will have to outperform it.

- ## [Is MLX or GGUF better for Qwen 3 Coder on Apple Silicon? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mskd6u/is_mlx_or_gguf_better_for_qwen_3_coder_on_apple/)
- Mlx is faster. DWQ are maybe better in quality. GGUF are slow.

- It's fairly common for MLX to have multimodal support before GGUF. 
  - It's also fairly common for GGUF to have larger context windows released before MLX.
  - There are good reasons to use both, but typically MLX will be a tad more energy efficient with a few more tok/sec at the same bit depth.

- ## [Qwen3-coder is mind blowing on local hardware (tutorial linked) : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n3ldon/qwen3coder_is_mind_blowing_on_local_hardware/)
  - qwen3-coder-30B is really impressive. 256k context and is actually able to complete tool calls and diff edits reliably in Cline. I'm using the 4-bit quantized version on my 36GB RAM Mac.
  - My machine does turn into a bit of a jet engine after a while, but the performance is genuinely useful. 
  - My setup is LM Studio + Qwen3 Coder 30B + Cline (VS Code extension). 
  - There are some critical config details that can break it (like disabling KV cache quantization in LM Studio), but once dialed in, it just works.

- The other one that shines on cline is Devstral small 2507. Not as fast as Qwen3-30b but equal if not a little better (in the way it plans and communicate back to you)
  - But yes, qwen3-30b best thing since web browsers.

- I find Devstral does a lot better than Qwen 30B Coder with thinking off. You need to let it ramble to get good answers but while I'm waiting, I would've got the answer from Devstral already.
- I don't think Qwen3-Coder comes in a thinking variant?
  - You're completely correct. Qwen3 30B Coder only has a non-thinking variant. I must have gotten the old 30B mixed up with 30B Coder when I was loading it up recently.

- why is Devstral so much slower than Qwen3 Coder even though it's smaller? I got 36tok/sec with Qwen3-Coder 30b (8bit quant), but I only get about 8.5 tok/sec with Devstral (also 8bit quant) on my Framework Desktop.
  - It’s a dense model. It’s slower but also smarter.
  - Devstral isn't an MoE model.

- ## 🤔 [Qwen3-Coder is impressive : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mssdfo/qwen3coder_is_impressive/)
- How does it handle long context?
  - It has 256 k context. Cline supports compression/summarization now for things exceeding that.
- I think at 125k context it has only 60% recall

- Plan or Act or both?
  - Both. I am too lazy to switch modes. Act all the way.
- Usually the solutions generated by act only are worse in my experience than if I did a planning / brainstorm session with the model first.
  - in my empirical experience/perception too. but that can be a biased by my usage style. i generally add at least a thing or two in its plan - and it works for me. 

- 🤔 Yeah it's excellent. I wish they had a version with reasoning.
  - “Reasoning” seems like mostly smoke and mirrors to me.
- Could you use something like sequential thinking MCP simulate that?
- The coding tools like cline and roo already prompt the model into reasoning. There’s no benefit of using a reasoning model with those.
  - That's not really how it works. You could tell 4o to "think step by step" back in 2024 (and I did), but that didn't turn it into O1.
- There's a huge difference between a system prompt and RL. But if you have a prompt that makes 4.1 reason like o1, lets hear it, that would be really interesting.

- Qwen3 coder performs good in terms of reasoning and complex problems. Only issue is context limit
  - That's when you use /smol or /newtask

- ## [Cline + Qwen3 coder is bliss for LocalLLM : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mt14x9/cline_qwen3_coder_is_bliss_for_localllm/)
- How much context window?
  - (I would max it out to 256k if you can)
- I’ve been using this combination successfully with a context window of 64k, 128, 256k on my Mac. Honestly I don’t notice too much of a difference, they all work darn pretty well. 

- I use unsloth/qwen3-coder-30b-a3b-instruct in LM Studio with its server enabled. I have 34GB VRAM across 2 cards, which is enough to fit the 26.34GB model in VRAM. 

- I also combined it with the new Archon Beta & the task planning + knowledge base makes this crazy powerful + keeps my context for enormous code bases down to below 128k tokens so lots of headroom not to mention reduces memory usage by around 60GB.

- ## [Qwen3- Coder 👀 : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m6mew9/qwen3_coder/)
- gemini flash works satisfactorily at 500k using Roo.

- The updated Qwen3 235B with higher context length didn't do so well on the long context benchmark. It performed worse than the previous model with smaller context length, even at low context. Let's hope the coder model performs better.
- I've tested a couple of examples of that benchmark. The default benchmark uses a prompt that only asks for the answer. That means reasoning models have a huge advantage with their long COT (cf. QwQ). However, when I change the prompt and ask for step by step reasoning considering all the subtle context, the update Qwen3 235B does markedly better.
  - That'd be worth a try, to see if such a small prompt change improves the (not so) long context accuracy of non-reasoning models.
  - The new Qwen coder model is also a non-reasoning model. It only scores marginally better on the aider leaderboard than the older 235B model (61.8 vs 59.6) - with the 235B model in non-thinking mode.

- ## [Best Way to Use Qwen3-Coder for Local AI Coding? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n4mo1r/best_way_to_use_qwen3coder_for_local_ai_coding/)
- (For local coding work) the lesson I learned is: Qwen3 Coder works very well as an autocomplete model. If you need autocomplete, give it a try.
  - With that said, I look elsewhere to power agents and tool calling. I suggest Devstral Small 2507 as a potential fallback option.

- Cline and LM Studio is all you need.

- I think qwen3-30b-a3b-thinking-2507 is a better coding model. Same requirements, but with thinking mode, and a paired speculative decoding model (qwen3-4b-a3b-thinking-2507) that speeds it way up.
  - IMO coding models that don't use thinking are going to make more mistakes
  - Thinking models do a much better job at the agentic coding workflows, when they need to hunt down some info, or reason through a bug.
  - Peak capability is way below SOTA large models, but 80% of work doesn't need peak capability...
- I run it in Kilo code and qwen3 seems to be plenty fluent with kilo. It respects my custom rules. It interacts with my local tool servers. But I get ~10 tokens a second on an m4 Mac w/ 48gb, so I'd rather pay for inference than wait for it in practice.

- my setup is pretty weak 3060 12gb + 32GB ddr5 6000mt/s. Roo code worked pretty well for me, although it got unbearable slow when It got close to 40k context.

- ## [Qwen3-Coder-30B-A3B in a laptop - Apple or NVIDIA (RTX 4080/5080)? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mwmi2n/qwen3coder30ba3b_in_a_laptop_apple_or_nvidia_rtx/)
- M2 Max 64 Gb here. 
  - I run Qwen3 30B A3B Q4 With llama.cpp, you’ll get around 50 TPS. 
  - If you run with MLX, 80TPS.

- ## [Why does Qwen3-Coder not work in Qwen-Code aka what's going on with tool calling? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mu3tln/why_does_qwen3coder_not_work_in_qwencode_aka/)
- That's just what happens when you have a fast-moving field and not much in terms of standards.
- The current situation is a bit of a mess. For whatever reason, OpenAI decided to release their new model with a Harmony format that, for the most part, no one asked for. This makes it a one-off system that every open-source LLM project has to support, especially if OpenAI doesn't release another model with the same format.
  - Similarly, Qwen also switched up their tool-calling scheme, but only for the latest coder version. To be fair, the current JSON tool-calling format is rather unforgiving, and quantized models are more likely to produce errors in the formatting. 

- Only LM Studio works, so they must have hacked around it, but it's closed source.

- ## 🆚 [GPT-OSS 20b vs Qwen3-30B-A3B : r/ollama _202508](https://www.reddit.com/r/ollama/comments/1mlgyct/gptoss_20b_vs_qwen330ba3b/)
- I've tried them both. Neither is good enough to be of any real use to me.

- I use Qwen3-Coder over OSS because
  - A. Qwen3 models can be ablated to remove railguards for queries, while OSS can’t as easily.
  - B. I can run Qwen3-30b-a3b-abliterated Q6 on my 32gb gpu card fitting the entire model in that space. OSS has no quants available that work with ollama as of this moment. Which edge it just over into 1% CPU - 99% GPU which slows it way down.

- ## [Qwen 30B Instruct vs GPT-OSS 20B for real life coding : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mvbzvh/qwen_30b_instruct_vs_gptoss_20b_for_real_life/)
- I find GPT-OSS 20b way better for coding, especially in coding agents.  First it runs with 64k context window at 100+ tokens per second on 5060ti, where Qwen 30b would be way slower cause of size, around 40-45 tokens on my hardware. This makes huge difference especially for thinking model.
  - I've tried  https://huggingface.co/Qwen/Qwen3-Coder-30B-A3B-Instruct and it's sometimes better, but on some non trivial issues gpt20b beats it because of thinking on practice. Also this one has huge flaw, tool calling is not working at all, so it's pretty much unusable for now.
  - Qwen3 30b 2507 Thinking is cool one, it works and it's way better on simple tasks without context. The main issue with it it thinks too much. It can use 10k+ tokens for simple file edits in coding agents, context getting polluted very fast and on practice it's way slower then GPT-OSS 120b
  - I hope they will update Qwen coder, maybe will give dense model or thinking variant, but for now they are not really close to GPT-OSS.

- So that's the thing: for Qwen3-Coder they trained it to use a different tool calling format compared to the regular Qwen3! They switched from quoted JSON (Hermes format, I think that is called), to an XML based one. In theory this is better because it's less complicated to quote and so it survives better especially with quantized models. But support this new syntax does not exist in llama.cpp yet AND at least the small 30B seems to be a bit wonky with tool calling itself.

- Qwen 30b 2507 Thinking, works best , maybe Qwen 30B coder with thinking might perform even better but its not released yet.

- [Devs: Devstral VS Qwen3-30b/GPT-OSS? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mprb4d/devs_devstral_vs_qwen330bgptoss/)
  - qwen 30b coder is miles ahead for web development compared to dev and oss
  - Whereas gpt-oss is very good for general or research discussions oriented stuff like asking one-shot proof of prey-predator models or any complex system it’s really good. It’s power relies on reasoning high reasoning comes gives great result most of the time
  - gpt 20b. Omg it was a rocky start but with the latest lm studio + aider in diff mode. I'm confident to say that is my new go-to. It's the new hummer. Best of class.

- ## [Qwen Code + Qwen Coder 30b 3A is insane : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mfuiri/qwen_code_qwen_coder_30b_3a_is_insane/)
- Especially since 30A tool calling only works with Qwen-Coder. They decided to use XML for tool calling instead of JSON like all other models, so tool calling doesn't work in roo or cline.
  - Nodejs was shitting all over python for a decade and now the turns have tide
- Issue is they don't use XML, they use an invalid variant of XML: `<toolname=read_file><parameter=path>` ....

- Which tools are you calling? I have used it with RooCode and it was able to search my codebase, edit, create and read files. Wait, did you make sure to set the temp in RooCode? I know that I had problems until I changed it to 0.7.

- Roo and Cline use xml based tool calling so I wouldn't phrase it like that - Qwen was probably specifically trained for the Qwen Code prompt format

- Json is a terrible format for LLMs, it's incredibly token inefficient. I'll need to start using qwen-code.

- ## [Talking with QWEN Coder 30b : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mn00j3/talking_with_qwen_coder_30b/)
- Trust me even the biggest Models suck at Godot/gdscript

- Qwen3 Coder 30B A3B is capable of actually writing code in "agent" mode, but things like tool calling are extremely fragile and will fail for most people
  - I've had OK luck with the VS Code Cline plugin, the newest Ollama, and the Unsloth 4-bit XL quant, but literally all the other agent wrappers besides Cline failed to make tool calls 90% of the time
  - I've never seen any model in 32B size range that was amazing at code

- I had a similar experience with QWEN, While raw speed is appealing, reasoning depth and flexibility are more important than just token count.

- you should try qwen3 30b thinking. it is more accurate in such non-coding tasks.
- Actually Qwen3-30B-A3B-thinking-2507 is a way better than non thinking Version
- I have finished testing Qwen3-30B-A3B-thinking-2507, and I would say its answers are roughly on par with the OpenAI gpt oss 20b model

- I'm using the Qwen3-30B-A3B-instruct for coding. The coder seems to have more issues following the instructions of long prompts like in Roo.
  - Qwen Coder 30B is an instruct-tuned model, not a chat-tuned one, and I googled to search what means in more details.
  - Instruct-tuned models are optimized to follow direct, self-contained instructions in a single turn. 
  - Chat-tuned models, on the other hand, are trained specifically for conversational environments. They learn to remember previous messages

- ## [Installscript for Qwen3-Coder running on ik_llama.cpp for high performance : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1metf4h/installscript_for_qwen3coder_running_on_ik/)
  - After reading that ik_llama.cpp gives way higher performance than LMStudio, I wanted to have a simple method of installing and running the Qwen3 Coder model under Windows. 
  - I chose to install everything needed and build from source within one single script

- The random text issue could be because of flash attention, try disabling it. I had the same issue last week with Qwen 235b on my dual-GPU setup. My second GPU is also compute 6.1 (Quadro P5000).
  - Yep, can confirm the random text issue on both ik_llama.cpp and vanilla llama.cpp occur when `-fa` is enabled.
- I had it only with ik_llama.cpp tough, vanilla llama.cpp was fine with -fa

- My brain can't understand why lm studio doesn't implement ik llama or give us an option to run it.

- If you want faster especially with that nvdia 4070ti ...load the model with vllm on WSL in windows it will be a lot faster than llama.cpp/lmstudio probably around 5-6x faster for generation of tokens.
  - I know vllm is another fast inference engine, but I highly doubt the 5-6x claim. Do you have any benchmarks that show this?
- sorry meant to say 4-5x faster than tensorflow and about 25% faster than llama.cpp. 

- [How to run Qwen3 Coder 30B-A3B the fastest? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1mepr5q/how_to_run_qwen3_coder_30ba3b_the_fastest/)
  - lm studio will be trivially fast to setup. I run Qwen 3 Coder 30b-a3b locally. It works great with Cline.
  - For your reference. I run it (Q4-k-xl UD) on my 8600k 32GB Ddr4 with 4070 super desktop. I get about 10t/s at 4k tokens. Your laptop will probably be a lot slower than this.

- ## [I made a comparison chart for Qwen3-Coder-30B-A3B vs. Qwen3-Coder-480B-A35B : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1me4i2h/i_made_a_comparison_chart_for_qwen3coder30ba3b_vs/)
  - [qwen3-coder-flash-perf-comparison.html](https://gist.github.com/karminski/08d4952f61952b7aa32c89eff5924432)

- A dense 32B would make those gaps much smaller
  - And be ~ 10 times slower

- Qwen 30 A3B is so insanely fast (90tok/s on M4 Max silicon) that it seems more useful to just run it a few times and have it iron out errors as it goes. Needing to store 16x more parameters doesn't seem worth it tbh
  - I second that. And if you need something extraordinary you go to Qwen chat and ask Qwen3-Coder-480B for that specific piece of code.

- ## [Is Qwen still the best for coding? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mf2cu1/is_qwen_still_the_best_for_coding/)
- For frontend development, Qwen 3 Coder seems to be the best OS out there and comparable with Sonnet 4.

- Qwen2.5 Coder was trained for FIM. Does anyone know if Qwen3 Coder was also trained for FIM?
  - I tested it with llama.vscode and it works pretty good.

- ## [Qwen3-Coder: Agentic coding in the world | Hacker News _202507](https://news.ycombinator.com/item?id=44653072)
- I currently use claude-code as the director basically, but outsource heavy thinking to openai and gemini pro via zen mcp. 
  - I could instead use gemini-cli as it's also supported by zen. 
  - I would imagine it's trivial to add qwen-coder support if it's based on gemini-cli.
- How was your experience using Gemini via Zen?
  - I just use it for architecture planning mostly when I want more info and to feed more info to claude. Tougher problems where 3 brains are better.

- what is the benefit of outsourcing to other models. do you see any noticable differences?
  - There are big gains to be had by having one top tier model review the work of another.
  - This is particularly useful in big plans doing work on complex systems.

- They also support Claude Code. But my understanding is Claude Code is closed source and only support Clade API endpoint. How do they make it work?
- Claude uses OpenAI-compatible APIs, and Claude Code respects environment variables that change the base url/token.
  - no it doesn't, claude uses anthropic API. you need to run an `anthropic2openAPI` proxy
- You can use any model from openrouter with CC via https://github.com/musistudio/claude-code-router

- ## 🚀 [Qwen3-Coder-30B-A3B released! : r/LocalLLaMA _20250731](https://www.reddit.com/r/LocalLLaMA/comments/1me2zc6/qwen3coder30ba3b_released/)

```sh
# Ollana is using standard gguf 
ollama run hf.co/unsloth/Qwen3-Coder-30B-A3B-Instruct-GGUF:Q6_K
```

- Interesting, no thinking tokens, but built for agentic coding such as Qwen Code, Cline, so assuming great for Roo Code.

- Qwen2 Coder wasn't so great for Roo Code and Cline. But Qwen3 is quite good in tools handling, and this is the key for successful integration with coding assistants. Fingers crossed.

- Does anyone know how 30B-A3B thinking compares to 30B-A3B-coder? The lack of thinking makes me somewhat sceptical that coder is better.
  - If you use Cline or similar you can set the thinking model to Plan role and the Coder version to Act role.

- No thinking only? Why's that?
  - they have a 480B-A35B thinking coder model in the works, they'll probably distill from that

- The only one that good both at code and writing is GLM-4, but it has nonexistent long context handling. Small 3.2 is okay too but dumber.

- [🚀 Qwen3-Coder-Flash released! : r/LocalLLaMA _20250731](https://www.reddit.com/r/LocalLLaMA/comments/1me31d8/qwen3coderflash_released/)
- I hope they still release a dense 30B+ coder. I don't trust tiny MoE models to output anything useful. Being lightning-fast is nice, but output quality is what matters the most for coding.

- a 30B-A3B MoE is poised to compete against ~10B dense models. It loses to Qwen3-14B for instance.
  - I think that's a poor observation, dense models are usually better than moes. In swebench verified with open hands scaffolding devstral small actually scores a little higher. Unfortunately this is the only benchmark I've been able to find that has both.

- ## 🧩 [What kind of Qwen 2508 do you want tonight? ; ) : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mhbvig/what_kind_of_qwen_2508_do_you_want_tonight/)
- in the 30B-A3B size, there is Qwen3-30B-A3B-Instruct-2507, it's for general use. "Instruct" means it was trained for user-assistant conversations, like following instructions, not just text completion (unlike Base models).
  - Also, there is Qwen3-Coder-30B-A3B-Instruct, which is better for coding tasks (but could be worse at everything that isn't related to coding), also it supports FIM (Fill in the Middle) for code completion, and it's also "Instruct" so it can do the instruction following as well.
  - So "Base" usually means the model can only continue text.
  - "Instruct" means it can follow user's instructions (the `user` , `assistant` , `system` stuff).
  - "Coder" in Qwen models means it's a model for coding, trained on coding related stuff mostly.
  - Also there is Qwen3-30B-A3B-Thinking-2507. From what I understand, it's like Instruct but with thinking (with something like this before every reply: `<think>Okay, ...</think>` )
- So as I understand it, instruct models are specially trained to follow instructions better / adhere to them more?
  - Yeah, you could say that
  - I mean, you can think of an Instruct model as of a ChatGPT-like model, which can chat with the user. But models like that don't necessarily have that "Instruct" in their names.

- 14B and smaller are my only realistic options with high context
  - So far, my testing shows that the 30B-a3b-2507 (non-thinking) is on par or better than Gemma3 27B. If the new 14B delivers improvement on par with what the 30B-a3b-2507 achieved over its predecessor, then it would be in the same ballpark as Gemma3 27B since the old 14B and 30B-a3b—were already quite close in quality.

- [From Smooth Chatting to Precise Execution: differences between “chat” and “instruct” modes in large language models | by hengtao tantai | Medium _202405](https://medium.com/@zergtant/from-smooth-chatting-to-precise-execution-differences-between-chat-and-instruct-modes-in-9c6f73fc175e)
- “Chat” and “instruct” modes are two common interaction styles in large language models. 
  - These modes differ significantly in how they handle inputs and generate responses. 
- The “chat” mode aims to engage users in free-form conversation, simulating a chatting experience with an emphasis on fluency and coherence; 
- the “instruct” mode, on the other hand, focuses on understanding and executing specific user commands, striving for task accuracy and operational precision. 
  - They excel when the entire task and all requirements are included in one prompt, but they’re not designed to maintain context, handle back-and-forth exchanges, or interpret subtle hints over multiple turns.

- ## 🧩 [jukofyork/DeepSeek-R1-DRAFT-0.5B-GGUF · Hugging Face : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jiilot/jukofyorkdeepseekr1draft05bgguf_hugging_face/)
  - This model is hopefully going to speedup the 600B version
  - I tried this paired with Unsloth dynamic quant: there's a token mismatch, token 128815 exists there as "PAD_TOKEN", so you probably have to use the gguf tools found in llama.cpp to edit these existing models, the draft, or convert again if you're unsure of that 

- draft model means?
  - If you use a feature called speculative decoding, you load up your main model (eg Deepseek R1 671B) and a draft model (this 0.5B model).
  - The point is you can draft what the next few tokens/words should be and pass it to the main model to verify. 
  - This basically means a lot of filler tokens can be generated much faster by the smaller draft model, resulting in a significant performance improvement with no degradation in quality. The benefits get larger the difference between the main model and draft model in size. 
  - LM Studio has this feature built in and it’s best to watch it enabled. 

- I didn't understand, what this model does, and how should I use it?
  - It's like an inexperienced student that can come up with 10 ideas on the spot. But then the experienced teacher can say, hey wait, Idea no. 7 might not be that bad and is worth pursuing. This process is much faster than the teacher coming up with a new idea on his own. Basically verifying an idea is faster than coming up with a genuine good one for a teacher.
  - Because LLM inference is mostly memory bandwidth limited, you can evaluate multiple inferences in parallel for basically free

- I have wondered if an asymmetrical MOE could outperform speculative decoding. If the MOE had a large expert and a small expert, you could have the router send all basic English words to the small expert… then rejection would never happen.

- The draft model needs to be same architecture but smaller model.

- The problem with drafting MOE models is that the amount of weights increases if more tokens are calculated per pass. It won't be the same chosen experts for each token.

- ## [Qwen3 no reasoning vs Qwen2.5 : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kegrce/qwen3_no_reasoning_vs_qwen25/)
- Depends on the task. For code autocomplete Qwen/Qwen3-14B-AWQ nothink is awful. I like Qwen2.5-coder:14b.

- ## [Devstral vs DeepSeek vs Qwen3 : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1ksat42/devstral_vs_deepseek_vs_qwen3/)
- Devstral is not better than qwen3-32B in general-purpose tasks. I guess it was trained to be specific to that openhands particular agent.

- ## 🆚 [QwQ 32b vs Qwen 3 32b vs GLM-4-32B - HTML coding ONLY comparison. : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kenk4f/qwq_32b_vs_qwen_3_32b_vs_glm432b_html_coding_only/)
  - All models are from Bartowski - q4km version
  - GLM-4-32b is insanely good for html code frontend.

- Yeah, I have also tried to generate webpages with a couple of models, like GLM-4, Qwen3, Phi-4 Reasoning, etc. GLM-4 is so far the clear winner at these tasks. It's a gem in my model collection.

- I don't think comparing HTML generated in a single shot is a good benchmark for intelligence. The model might just be repeating patterns it has memorized, resulting in very similar-looking pages.
  - I've done some experiments and concluded that current LLMs (including Gemini) have no real understanding of what makes a good web design (they are somehow render-blind).
  - A more useful benchmark might be asking the model to modify an existing web page template given custom instructions.

- GLM falls flat on its face when I try to continue developing after the first prompt. It feels like a model trained (very well) for one-shots

- ## 🤔 [what are the challenges of fine tuning deepseek coder or codellama on a real world codebase? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n1mnbz/what_are_the_challenges_of_fine_tuning_deepseek/)
  - i’m curious about fine tuning code llms like deepseek coder or codellama on an actual messy real world codebase.

- It's probably not something you want to do. You might be better off with a RAG solution, but normal grep/search from tools like Claude Code or Codex works pretty well with good prompting.

- when you say fine tuning isn’t worth it, was that based on trying it yourself and running into issues, or more from comparing results with rag and prompting? 
  - I've fine tuned before, and I have also used RAG. I specifically fine tuned on newer specs/docs for the ESP32, since most of the LLM's at the time had older data
  - I mean it worked, I was able to improve things, but it was a big effort, and RAG ended up working just as well or better.
  - The problem is code changes quickly, doing a fine tune on giant models would be impractical, as soon as you start changing the code, the fine-tune is outdated. RAG is a better solution, but even just regular grep/code searches work pretty well.

- Stop expecting perfection or near-perfection and learn to work with "good enough" results. If 30B is good enough, then focus on the remaining portion that needs human intervention. You can't change the model behavior, but you can change the way you use it, and how you approach the overall problem.
  -  I have tried all sort of tasks from vibe coding, refactoring, disassembly. The key thing is that you need to know better/more than the AI to be an effective human. I found myself learning things that were beyond my reach previously, so even though the AI had objectively failed at the task assigned to it, through the process I learned enough to carry on the task with whatever meaningful results it had produced, and take the rest over the finishing line.

- ## [DeepCoder: A Fully Open-Source 14B Coder at O3-mini Level : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1juni3t/deepcoder_a_fully_opensource_14b_coder_at_o3mini/)
- Is llama4 actually that bad, or are people working off of a collective meme from a poor first showing? 
  - Poor first showing and disappointment. Gemma 3 had issues during launch, but now that it's sorted I'm running the 1b, 4b, and 12b versions locally no problem. 
  - Lllama 4 has no version I can run locally. Llama 4 was hyped to be a huge deal, but it seems more geared towards enterprise or large scale rollouts.

- I found most local LLMs to be unusable with Roo, apart from one or two that have been specifically finetuned to work with Roo and Cline.
  - The default system prompt is insanely long, and it just confuses the LLMs. It's insanely long because Roo needs to explain to the LLM what sort of tools are available, and how to call them. Unfortunately, that leads to the issue that smaller local LLMs can't even find your instructions about what you even want them to do.
  - QwenCoder, QwQ, Gemma3 27b, Deepseek R1 Distills (14b, 32b, 70b) - they all fail.
  - The only models I found to work moderately well were tom_himanen/deepseek-r1-roo-cline-tools and hhao/qwen2.5-coder-tools
  - Just checked: For me, the default system prompt in Roo's code mode is roughly 9000 tokens long. That doesn't even include the info about your workspace (directory structure, any open files, etc. ) yet.

- did anyone try if it works with CLINE/ roo code?
  - it didn't do well, but I am going to check to make sure my settings are right.

- I tried a few simple tasks with the Q8 model on a 32gb macbook.
  - The diffs will work at least.
  - After the simple task I asked for it to do (insert another button in an html) succeeded, it failed at the last step with: "Cline tried to use attempt_completion without value for required parameter 'result'. Retrying..."
  - It retried 2x before successfully figuring out how to use attempt_completion. Note, this is after the file itself was edited correctly.
  - It made a few other edits decently well. Be careful with clarifications. If you ask it to do A, then clarify also B, it may do B only without doing A.
  - I suspect this model will score okay ish on the aider coding benchmark, but will lose some percentage due to edit format.
  - I set context to 32k, but Cline is yappy and can easily fill up the context.
  - Using Q8 makes it slower than Q4, but coding is one of those things that are more sensitive to smaller quants, so I'm sticking with Q8 for now. It'd be cool if they release a QAT 4bit version, similar to Gemma 3 QAT. At Q8 it runs around 15tok/sec for me.
- Conclusion: not anywhere near as good as Sonnet 3.7, but I'm not sure if that's due to my computer's limitations (quantized quality loss, context size, quantized kv cache, etc). It's not complete trash, so I'm hopeful. It might be really cheap to run from an inference provider for people who can't run it locally.

- I'm playing around with it right now, and at q8_0 it's failing miserably at stuff that o3-mini easily one-shots.

- Tried it and its completely useless, it writes paragraphs and paragraphs thinking about what I said instead of just doing it. These reasoning models that talk to themselves cant be the way.

- ## [New coding model DeepCoder-14B-Preview : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jvxi5f/new_coding_model_deepcoder14bpreview/)
- Make sure to tweak params: {"temperature": 0.6, "top_p": 0.95}

- i just played with using the 1.5b as a speculative model for the 15b with lmstudio seemed to work well even
- Do you find it noticeably faster using speculative decoding?
  - I can’t tell if the smaller model is loaded into VRAM or not, but it does seem faster

- I was coding some Python last night. Qwen 14b -coder seems to be better than the deepcoder

- try these settings for extra coherent coding with reasoning code models. Works amazing on QWEN R1 distill, which this is based on.
  - Temp: .82 Dynamic temp range: 0.6 Top P: 0.2 Min P 0.05 Context length 30, 000 (with nmap and linear transformer.... yes really). XTC probability: 0 Repetition penalty: 1.03 Dry Multiplier : 0.25 Dry Base: 1.75 Dry Allowed Length: 3 Repetion Penelty Range: 512 Dry Penalty Range: 8192

- ## [DeepCoder 14B vs Qwen2.5 Coder 32B vs QwQ 32B : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jwhp26/deepcoder_14b_vs_qwen25_coder_32b_vs_qwq_32b/)
  - Conclusion: Qwen2.5 Coder 32B is still a better choice for coding, and it's not prime time for a 14B model yet.

- For smaller models, you need to be providing a more explicit prompt.

- ## 🤔 [Is Qwen 2.5 Coder Instruct still the best option for local coding with 24GB VRAM? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kq029v/is_qwen_25_coder_instruct_still_the_best_option/)
- I'm just using the 30BA3B for everything. It's not the smartest, but it is fast and I am impatient. So far, it has been good enough for most things. If there's something it struggles with, I switch to Gemini Pro.
  - Once you get used to that speed it's hard to go back to a dense model in the 32B/30B size.

- QwQ is goated but you have to accept waiting 3 billion years of thinking before getting your output

- No, Qwen3 is better. 32B no-thinking or 30B-A3B with thinking.
  - 14B is also great with thinking, probably better than 30B-A3B, you can run it in Q5 or Q6, and you can fit so much context.

- Within 24G ram it supports only 2000 context size but for a normal Nextjs app it is too low. At least require 32k context size but then the memory requirement shoots up too.

- ## [Is Qwen2.5 Coder 32b still considered a good model for coding? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1iyuy62/is_qwen25_coder_32b_still_considered_a_good_model/)
- For performance on it can’t compare to closed source or the huge param models like Deepseek v3.
  - However it’s the only one a lot of people can run locally with a 24GB video card.
  - Personally, I mostly switched to using claude3.7 for general questions/code gen and qwen 2.5 7B for FIM and code completion.

- 🤔 I personally, prefer it to reasoning models of the same size just because when coding I am less eager to watch it ramble on, on how its going to answer and just want an answer. I think bigger and maybe even the same size reasoning models might give better answers but I am usually too impatient when coding to deal with all that.
  - Same here, I like the concept of reasoning models but I am also impatient 
  - Yeah, reasoning models like R1 are too bulky for chat-coding.

- it is weaker than bigger models, but it is better than codestral, except for context length. I am more than happy with 7b and 14b models; 

- For its size, it's the best.
  - DeepSeek R1 is 631B even with MoE, how can you compared to a 32B?
  - Sonnet API is $3 / million tokens. Also, how do you compare to a local model?

- while with some local models that you can run on a 24gb or even a 48gb setup are "good enough" for simple tasks, or even processing a lot of documents, or whatever, for coding assistants they are a toy compared to what is available. When you do anything serious they are more a waste of time than remotely helpful. You can compete with what you can get with $10 a month with GitHub copilot or services like that.
  - I'm still using local models for fun and learning, but it's hard to justify not using a cloud api like Gemini. 

- I am using it with continue VSCode plugin. Not bad.

- 32k context is not big enough. Need at least 4x for it to be really helpful.
  - Qwen coder 32b has 128k context
- People seem to ignore this fact, not only you can extend it to 128k, but it almost don't degrade (compared to other 128k models). Problem is, only VLLM support the YaRN rope configuration needed to extend it.
  - Also exllama supports it.

- QwQ is built on Qwen2.5-32B-Instruct and not Coder. (At least according to its HuggingFace page.)
  - Reasoning 32b models just kill my mbp unfortunately

- ## [Is qwen 2.5 coder still the best? : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j2usb0/is_qwen_25_coder_still_the_best/)
- nothing has been released that really holds a candle to Qwen-Coder 32B that can be run locally with a reasonably modest hobbyist machine. 
  - The closest we've come is Mistral Small 24B (and it's community fine tunes, like Arcee Blitz) and Llama 3.3 70B (very good at coding, but wayy larger and questionable if it beats Qwen).

- CoT models think too much for coding IMO. I think they are good for optimizing your prompt though.
  - They might have a role for architecting. Like figuring out Rust traits is annoying and extra diagrams help as well. But for extra interns, no chain-of-thoughts please.
- I do this with Aider. R1 plans the code changes, Sonnet 3.7 writes the actual code based on it's output. It works really well.

- Do people prefer Qwen coder for coding compared to QWQ-preview or other COT models?
  - What are pros would you say? I tend to find the thinking models catch their logical mistakes more often which saves time when I double check what it gives me back. Is it just the speed or is it actually more accurate for you?
- Qwq just takes to long to get an answer for my taste.

- Gemma never been good at coding.
  - Hell even the largest Gemini models have never been good at coding.

- Still waiting for someone with much better hardware to add longrope v2 and a reasoning finetune to qwen 2.5 coder 32b. With reasoning and a ridiculous context window extension that thing would be beast mode for local coding. longrope 2
- Also Chain of Draft: Thinking Faster by Writing Less
  - It does not work. I've tried. No difference.

- I love how Claude 3.7 without reasoning beats gtp models with reasoning. The reasoning hype is a bit too much I think, and the way those models work feels like a step backwards and a little step forwards

- yep its still the best if you want to skip reasoning llms. Some of the reasoning llms are as good and maybe even better but at the cost of waiting for it to think which in my experience is 3 times longer wait as reasoning llms question everything even if they are cabable of spitting out an answer quickly.
  - Yes I think waiting for reasoning is not worth (right now).

- QwQ 32B model is the best for Local with same power as Deepseek R1 671B Model. But requres 46 GB VRAM and 64 GB RAM, to be able to run it.

- QwQ 32b is even better in coding on my experience.

- ## [AIDER - As I suspected QwQ 32b is much smarter in coding than qwen 2.5 coder instruct 32b : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j5ao2j/aider_as_i_suspected_qwq_32b_is_much_smarter_in/)
- I'm not clear if QwQ was 3x better or 3x more expensive
  - Both

- Qwen coder instruct 32b had 8% and that model is quite useful.
  - Now QwQ 20% in Aider is really a lot .. From my tests is quite good in coding ...of course is not level DP 670b or o3 mini yet .

- couldn't you combine QwQ 32B as the architect model and use Coder 32B as the editor model?
  - Except locally you have to load and unload the models all the time if you don’t have enough vram.

- ## 🚀 [OpenHands-LM 32B - 37.2% verified resolve rate on SWE-Bench Verified : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jocz51/openhandslm_32b_372_verified_resolve_rate_on/)
  - OpenHands LM is built on the foundation of Qwen Coder 2.5 Instruct 32B, leveraging its powerful base capabilities for coding tasks. 
  - What sets OpenHands LM apart is our specialized fine-tuning process
  - We used training data generated by OpenHands itself on a diverse set of open-source repositories

- It's annoying their comparison graph doesn't even include qwen2.5-coder 32b which this is based on.

- The model's performance isn't necessarily superior to other models in general. The thing is, that this model was specifically fine-tuned to work effectively with the OpenHands tooling system, similar to how a new employee receives training from a senior developer on company-specific tools, environment, and processes.
  - Because the model was deliberately trained to use the OpenHands tools more effectively, it can leverage this specialized knowledge to achieve better scores on the benchmark. so it will do great in any benchmark where it can use openhands, and probably not as great in benchmarks that it cant.

- It's annoying their comparison graph doesn't even include qwen2.5-coder 32b which this is based on.

- Since it's not documented anywhere, and I don't see anyone talking about it: This fine-tune breaks the underlying Qwen2.5-Coder's FIM. It's faintly present, but often goes off the rails and starts chatting. I don't think this result is surprising, but I wanted to check.
  - Outside of FIM, I cannot distinguish it from Qwen2.5-Coder-32B in my testing. The performance is virtually the same for everything I tried.
- have you tested it inside openhands? the whole fine tuning was to make it interact better with openhands, the fact that it didn't lose much outside of it is actually surprising.
  - Ah, got it. I only ran it via llama-server with the model's default configuration through the usual completion API.

- ## 🤔 [Why has no one been talking about Open Hands so far? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1ksfos8/why_has_no_one_been_talking_about_open_hands_so/)
  - What’s weird is that OpenHands has 54k+ stars on GitHub. For comparison: Roo Code sits at ~14k, and Cline is around 44k. So it’s clearly on the radar of devs. But when you go look it up on YouTube or Reddit—nothing. Practically no real discussion, no deep dives, barely any content.

- They used to be Open Devin. I think they started after Devin made a bit of a splash. Rebranding might have killed a bit of name recognition.

- The reason it has not been mentioned here is because the benchmarks for OH + local LLMs were not so good compared to cloud services.
  - The OH team recently released an OH fine tuned LLM based on Qwen2.5 and now Mistral jumped in. And there is a good reason for their decision.

- I wanted to try OpenHands, but they don't make it easy to run the thing outside docker on a POSIX environment. They also don't make it easy to setup with your own API. I gave up after about an hour and switched to Roo to test the model.
  - We're serious and the stars are real, but totally hear you on the install issues. We've tried to make it as easy as possible to set up with Docker, but getting it to work without docker is not as easy as it should be and we'll work on it.

- It's more difficult to setup, and after downloading like 20GB of Docker images, you need to spend $ on Claude 3.7 tokens or whatever SOTA models to actually get good results because you're stuck with the limited web app.

- it somewhat works with docker, but tools like LocAgent(which relies on external openhands_aci package), or file upload don't work for me. maybe it's just not mature enough yet

- 🏠 Just to confirm, for every new feature or bug I want to work on I usually make a new convo to keep the context length short.
  - In OpenHands a new convo is like a new instance so this requires pulling the repo, reinstalling dependencies, etc. which also eats up a ton of context window.
  - Is there a way to have multiple convos on the same codebase without having to reinstall everything each convo? Or does it not matter that I start new convos and I can just keep requesting more and more things in the same convo?

- I decided to check the product and have been sitting with the settings for the whole day. Installing docker and running it is not a problem, but no matter how hard I try, it does not want to connect to the local model, although in the console via curl the connection to it goes. Plus I created a 10 GB container, this is quite a lot, I do not understand why it requires such a crazy size, this is almost the size of the entire operating system.
  - I had a similar experience today. Running both LM studio and Open hands with more permissive networking settings allowed open hands to reach the LM studio web server.
  - So maybe give that a try? IIRC it's add `--host` to the `docker run` arguments and for LM studio it was update the setting to run the web server so it doesn't only resolve over localhost, and instead broadcasts over the machine IP.

- Too many undocumented things for a shittier version of cursor really, and since it's bring your own model the monthly cost will be HIGHER than cursor.

- it somewhat works with docker, but tools like LocAgent(which relies on external openhands_aci package), or file upload don't work for me. maybe it's just not mature enough yet

- 🏠🐛 OpenHands is really awesome and works quite well. However, for now you would need to setup the whole virtual machine if you want to run it on your host without giving privileged permission to the docker container. 
  - That’s because their docker container spins up another docker container and this type of functionality requires developers to give privileged permission or mount docker sockets (basically has the same problem if security vulnerability is found).
  - This prevents developers in many companies from using OpenHands when they can’t use privileged containers easily, and setting up the whole virtual machine is a bit of overkill when you can spin up Docker-based Code Server with RooCode plugin without adding extra capabilities to a docker container.
  - I believe at some point they will move to docker compose to spin up multiple Docker containers instead of using Docker inside Docker and this will simplify running OpenHands for broader community.

- ## [Qwen-2.5-Coder 32B – The AI That's Revolutionizing Coding! - Real God in a Box? : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gp84in/qwen25coder_32b_the_ai_thats_revolutionizing/)
- I've been using the Q4_0 gguf version of the Qwen2.5 Coder Instruct, and I'm pleasantly surprised. Despite the significant loss in quality due to gguf quantization—where the loss, although hoped to be negligible, is still considerable compared to full loading—it performs similarly to the GPT-4o-mini and is far better than the non-advanced free version of Gemini.
  - However, it still doesn't come close to GPT-4.0 for more complex requests, though it is reasonably close for simpler ones.

- It is currently 5th place on Aider leaderboard, above GPT-4o, but slightly worse than old Claude Sonnet 3.5 and o1, and quite worse than new Claude Sonnet 3.5.

- 32gb is a nice compact size. I may pull the trigger on a 48gb mac mini pro.

- Vllm absolutely smashes llama.cpp in speed
- Does LM Studio use Vllm behind the scene? I do know Ollama uses llama.cpp
  - LM Studio is also llama.cpp based

- ## [IMO the best model for agents: Qwen2.5 14b : r/ollama _202411](https://www.reddit.com/r/ollama/comments/1gh23zo/imo_the_best_model_for_agents_qwen25_14b/)
  - Today, I deployed Qwen2.5 14b and I find it's function calling, CoT reasoning, and instruction following to be fantastic. I might even say, better than GPT 4/4o. For all my use cases, anyway.

- how do you do function calling?
  - I use either langchain or the Vercel ai sdk for function calling personally

- This model is fantastic, I just tested it for coding as well and it is the only quantized model which detects SQL syntax error (e.g., missing of comma) despite being smaller than 10 GBs.

- ## [Appreciation post for Qwen 2.5 in coding : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1fn0a37/appreciation_post_for_qwen_25_in_coding/)
  - I have been running Qwen 2.5 35B for coding tasks. Ever since, I have not reached out to Chat GPT. Used Sonnet 3.5 only for planning.. It is local and it helps with debugging. generates good code
  - I am also impressed with its instruction following and JSON output generation. 

- The 14B model (Q8) was doing better than 35B (Q5) during my testing. But it was pretty smart overall.

- Sonnet for planning? Like how?
  - For the architecture and design of a solution. Also thinking through all the goods and bads about a particular design choice.

- Why not Qwen-Code?
  - Because I want the model to support other general purpose use cases too.

- ## [deepseek-coder-v2:16b does not support tools？](https://huggingface.co/deepseek-ai/DeepSeek-Coder-V2-Lite-Instruct/discussions/9)

- [Thank you for this model.](https://huggingface.co/deepseek-ai/DeepSeek-Coder-V2-Lite-Instruct/discussions/6)
  - It can code really fine, about Codestral 22b level
  - It can speak okay on different languages.

- ## [Deepseek coder v2 : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j7vwcr/deepseek_coder_v2/)
- It's a 16b mixture of expert, not a 7b

- it runs fast and is reasonably good at Python and PowerShell. Somewhere around Deepseek Coder 33B in performance.

- It is fast but weak.

- ## [Deepseek Coder V2 is so good for math : r/LocalLLaMA _202406](https://www.reddit.com/r/LocalLLaMA/comments/1do72te/deepseek_coder_v2_is_so_good_for_math/)
  - It's really pretty and organized
- I assume this is because it was trained on Latex? I'm not sure how aggressively Anthropic / OpenAI are training on Latex.

- DeepSeek has some training magic in their coding models.  We have been using DeepSeek for real code generation recently and the only complaint is the speed of their API.   The price is great though.
  - Separately I’ve been happy running v2 coder lite locally; almost as good as Codestral but significantly faster.
- Another complaint of their API is the context length. Their open weights supports 128k, But their API only supports 32k 

- ## [CodeLlama 70b censorship : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1anpi6c/codellama_70b_censorship/)
  - the response: I cannot fulfill your request as it goes against ethical and moral principles, and it is also illegal and potentially harmful.

- CodeLlama 70b have a prompt format issue. It make it spew censorship stuff
- Yeah, that model is quite censored indeed but its also very sensitive to its prompt template it seems

- This is a false positive, probably some sub classifier model needs to be adjusted.

- [Why is CodeLlama on huggingface so opinionated, biased and arrogant ? : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1b0ss2t/why_is_codellama_on_huggingface_so_opinionated/)
  - Probably because it was at some point a general model which was further trained for code. By using a word like "appropriate" you are probably triggering a lot of political/sociological/emotional thoughts which is suboptimal if you are trying to code.

- ## [Use self-hosted Code Llama 70B as a copilot alternative in VSCode : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1agerx0/use_selfhosted_code_llama_70b_as_a_copilot/)
- The gotcha is having hardware fast enough to run it at usable rates

- codellama fucks up and refuses a lot of work, I wouldnt focus on it too much until someone finetunes the base model for instruct
  - The model is fine once you get the new and complex prompt format right.

- It's a great idea on paper, but perhaps 70B is too big for most current consumer hardware.

- ## 🚀 [Today we’re releasing Code Llama 70B: a new, more performant version of our LLM for code generation  : r/singularity _202401](https://www.reddit.com/r/singularity/comments/1ae0rap/today_were_releasing_code_llama_70b_a_new_more/)
- is there a realistic way to run a 70B model on a 4090, with maybe 1-2 token/sec or better?
  - For Mixtral I get 5 token/s haven't tried an 70B (With 5 layers on CUDA and tensorrt). I am on DDR5 with a 7950X3D though. Ram speed seems to be the main issue.

- ## [Code Llama Released : r/LocalLLaMA _202308](https://www.reddit.com/r/LocalLLaMA/comments/1601xk4/code_llama_released/)
  - All models support sequence lengths up to 100, 000 tokens
- That could be made more nuanced. They support input context sequences of up to 100, 000 tokens. The sequence length of the underlying model is 16, 384.
- Can you help us newcomers understand why this is so exciting?
  - The context windows is basically the short term memory of the LLM. Larger window size allows "pre-initializing" it with more data. In this case a larger portion of your existing codebase can fit in, so it can provide more relevant answers and code-completion in that context.

- the key to the long context length is actually changing the base period!!! That was exactly the NTK scaling post here promoted, yet they didn't mention it at all. So they rushed out the linear interpolation paper to divert researchers' attention, but they secretly doing NTK

- [Codellama - Has anyone found "Codellama 34B Instruct" to be uncooperative? : r/LocalLLaMA _202308](https://www.reddit.com/r/LocalLLaMA/comments/160zxjd/codellama_has_anyone_found_codellama_34b_instruct/)
  - Just an update: issue appears to be definitely solved by using the correct parameters when loading and querying the model. 
  - Fortunately many of the popular frameworks like text-generation-ui are getting updates that use the correct settings for this new class of codellama models
# discuss-coding-model-fine-tuning
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [[P] I fine-tuned Qwen 2.5 Coder on a single repo and got a 47% improvement in code completion accuracy : r/MachineLearning _202503](https://www.reddit.com/r/MachineLearning/comments/1jdiafd/p_i_finetuned_qwen_25_coder_on_a_single_repo_and/)
  - Training data: Svelte source files from this repo on github
  - Tl; dr: The fine-tuned model achieves a 47% improvement in the code completion task (tab autocomplete). Accuracy goes from 25% to 36% (exact match against ground truth) after a short training run of only 500 iterations on a single RTX 4090 GPU.

- This sounds like the strategy that https://ninetyfive.gg/ uses. Awesome to see your results open sourced! How did you figure out the best way to determine the prefix/middle/suffix splits for training? It seems like here you did something more clever than randomly picking a location in the file to split?
  - the logic for determining the split is actually very basic right now, and not even all that comprehensive. It just looks for if-else blocks, function definitions, loops etc. and takes the entire block as the “middle” portion to be completed by the model. There’s also a min and max length filter I apply to get reasonably sized middle blocks.
  - I just wanted to quickly get some results, so I implemented this very simple method, and there’s lots of room to improve on this. E.g., in the SAFIM paper, they determine “critical algorithm blocks” by checking if removal of those blocks results in compilation or test failures.

- Do you feel the benefit is from being familiar with the project or with your coding style? Most of my code is written via llm these days so style wise it would provide no benefit. But if the benefit comes from being more familiar with the project and it's goals without having to burn context I think that would be a meaningful improvement

- This is solid, is the code completely limited to certain stack usage?
  - The dataset generation code is Svelte-specific because it only parses Svelte files, but the training itself is not. You can generate a training set in a similar manner for any language/stack of your choosing as long as you can parse the code into an AST.

- Do you have to fine-tune after every code edit?
  - As the codebase evolves, some of the things that model has learnt will become out-dated. So yeah if a similar model is deployed on a real codebase, it will have to be fine-tuned periodically. But it probably won't be necessary to do after every single commit, minor changes in the code can be addressed by implementing an effective context selection algorithm.

- Do you touch all weights?
  - No, it was a LoRA fine-tune with rank 16. 68M trainable parameters.
- These "500 iterations" that you mention, was that the entirety of your fine tuning? How long did it take?
  - Yes, the checkpoint I evaluated was the one I got after iteration 500. It took about 1h 20m to get there.

- in total how many passes over the codebase the model train on? Is it just once? Or multiple times?
  - I wasn’t even able to do one pass :) My training run only saw like 10% of the training set.
  - I’ve switched to using torchtune for training, and with a smaller model and more powerful GPU, we’ll be able to do a full pass over the training set in 5-6 hours. Will make another post with an update.

- [I fine-tuned Qwen 2.5 Coder on a single repo and got a 47% improvement in code completion accuracy : r/ChatGPTCoding](https://www.reddit.com/r/ChatGPTCoding/comments/1jdi4o6/i_finetuned_qwen_25_coder_on_a_single_repo_and/)
- you can use the fine-tuned model via Continue. You can export the model in GGUF, serve via Ollama, and connect Continue to it.

- ## [[D] Can I fine tune an LLM using a codebase (~4500 lines) to help me understand and extend it? : r/MachineLearning _202505](https://www.reddit.com/r/MachineLearning/comments/1kqpam7/d_can_i_fine_tune_an_llm_using_a_codebase_4500/)
- That will fit into the context window of most modern LLMs, there's no advantage to fine tuning

- "Smarter" RAG setups will probably serve you a lot better since among other things, if tuned, its tuned knowledge would be so specific and go out of date so easily when the codebase is modified. Requiring more feeding at the prompt anyway.

- Fine-tuning means supervised learning, so you would need training data in the form of input (probably a part of your codebase + a question about it) and output (expected output from the model). You can't fine-tune only using your codebase. You can maybe continue pretraining (unsupervised) but your data is too little for that.

- For comprehension, you're probably much better off chucking it into context, or failing that then RAG.

- ## [Finetuning a model on a source code repository : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1csmprt/finetuning_a_model_on_a_source_code_repository/)
  - I want to finetune a model on a source code repository so I can ask question, create code based on it etc

- finetuning is not meant for this, finetuning / training is done to achieve a knowledge level / “intelligence” not for literal facts.
  - Basically you need to push your repo in the context so you can ask questions of it, but llama3 has only 8k context. 
  - But although I do believe code is perfect for rag ( basically you could create a file-overview, then function overview per file and then a code overview per function, so you can rag for 3 levels deep easily) I have not seen any rag implementation which is made for code. And general rag will not work good, general rag will just take x characters and in doing so loose all coherence code has.
- Basically I believe you need specialized rag and large context for what you want, that way you can also do it on real-time git code updated after every commit instead of constant finetuning

- ## [Too Afraid to Ask: Why don't LoRAs exist for LLMs? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kzg3yv/too_afraid_to_ask_why_dont_loras_exist_for_llms/)
- Unsloth allows you to train your own lora on some LLMs. 

- RAG and increased context windows eliminated many people's use cases for LoRA (myself included) but it's still very much real and around

- there are, but LLMs each have such a big variety of architectures that it’s not common for public releases and are usually used for developers. Ex: a lora for Gemini wouldn’t work for Gemma 3 nor llama nor really any other release nor version . Much easier to train it as a new version if you’re adding fine tuning .

- In LLMs we generally don't differentiate between LoRA and FFT in the same way that a distinction is drawn in image generation. 
  - Most of the finetunes that you see in LLMs are actually LoRAs with the LoRA additively merged into the weights to lower the inference cost. 
  - LoRAs actually aren't free in terms of computational performance, and LLMs are really hard to run, so people generally merge them for that reason.
  - Additionally, LoRAs are often used there as a means of control, whereas generally LLMs are general purpose enough to just prompt for the thing you want.
  - So, long story short, if someone does a LoRA in an LLM, it's usually to create a complete change in experience, more like a custom SDXL finetune, for example, so it doesn't really make sense to distribute them in the same way.

- LORAs do exist for LLMs, but as opposed to Diffusion, which only has SD 1.5, SDXL, SD3.5, and Flux, in the LLM space we seem to be getting a different model every week, each with a new architecture. Hence, it's generally considered impractical to have a separate LORA for every model and have the end user manage it. We also don't have a CivitAI-like website where we can distribute such things easily.
  - In LLMs, most of the time, fine-tuners train a LORA, and merge it into the checkpoint, then distribute the new checkpoint and its quants.
# discuss
- ## 

- ## 

- ## 

- ## [What is the current best python coding model? : r/LocalLLaMA _202408](https://www.reddit.com/r/LocalLLaMA/comments/1epjget/what_is_the_current_best_python_coding_model/)
- CodeQwen-1.5-7b is a powerful coding model according to livecodebench.

- In the 8GB~12GB range I have used a few specialised ones:
  - Codestral-22B-v0.1-Q4KM
  - DeepSeek-Coder-V2-Lite-Q5KM
  - CodeGeeX4-All-9B-Q8

- CodeGeeX4-ALL-9B, CodeQwen1.5-7B-Chat and Codestral-22B-v0.1 are very good small coding models. There's also the DeepSeek-Coder-V2 models.

- Check out bigcode-bench.github.io. Top 7B on there is CodeQwen1.5-7B-Chat which has been good in my experience. CodeLlama is the lowest ranked 7B.

- ## [Local LLM Coding Stack (24GB minimum, ideal 36GB) : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nkfvrl/local_llm_coding_stack_24gb_minimum_ideal_36gb/)
  - Chipset Model: Apple M4 Pro
  - 给出了很多模型的速度tops

- Why not Qwen3-32B? It's better 
  - I prefer MoE just for the (initial) speed, but a dense one that I like a lot is Devstral small.

- Context window size?
  - I run Qwen3Coder and GPT-OSS at 131k via lm studio, mlx format, 6bit and 4bit respectively.
- Mean nothing. After 60k all models start to hallucinate

- How is the prompt processing speeds for long contexts ?
  - Slow, like 3x to 10x slower than api. But that’s not due to the models, but my hardware.

- ## [what the best local llm for coding? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nf8qdl/what_the_best_local_llm_for_coding/)
- I've used GPT-OSS20b and Qwen3-Coder-30B-A3B-Instruct-GGUF, I like both. 
  - However, OSS20b due to reasoning, can come up with better code instructions and optimizations/refactoring unlike the Qwen3-Coder.

- I just run 30B on RAM (I have 32GB) currently with ollama, which occupies 19 GB with a 4096 context. 

- If you're using native tool calling (as opposed to Roo/Cline XML-style calls), you can also strongly consider GPT OSS 20B, it is very fast and has a configurable thinking setting, so is a very versatile option.

- ## [Best really lightweight coding model for very basic questions? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1n9faly/best_really_lightweight_coding_model_for_very/)
- Gpt oss 20b or qwen 30b a3b 2507 (thinking version), these aren't just coding models but they do well at coding and run fast on a CPU with enough system ram.

- ## [Best small local llm for coding : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mz0640/best_small_local_llm_for_coding/)
- GLM-4 0414 9b or Qwen 2.5 Coder 14b are probably your best bets around that size. They are surprisingly good as long you can break your problem down into focused bite-sized pieces.
- there is a GLM-4 0414 32b and I really like it. Even at brain-damaged quantizations like IQ2_XXS it is still surprisingly functional.
  - That said, I've mostly shifted to Qwen 3 Coder 30b a3b since it is so much faster and sits right in the ability sweet spot between the 9b and 32b GLM-4 models.

- ## [What is the Best coding LLM for my system? : r/ollama _202508](https://www.reddit.com/r/ollama/comments/1mmu24w/what_is_the_best_coding_llm_for_my_system/)
- Devstral with Pixtral layers baked in is a lot more precise than Qwen3-coder 30B. 
  - Check Unsloth's version from Huggingface, it has all the multimodal bells and whistles. Take a screenshot, give it to the model, and see magick happen as it creates both back-end and front-end code for a project. 
  - This also works in Claude code, if you setup claude-code-proxy to convince that your local Devstral is Sonnet/Opus/Haiku. 
  - You can also try OpenHands, as Devstral was frist made for that.

- ## [Local model for coding : r/ollama _202508](https://www.reddit.com/r/ollama/comments/1n0ht8x/local_model_for_coding/)
- Qwen3-coder B30A3 is really good and fast Works like a charm on my 4060ti 16GB
- I'm using hf.co/unsloth/Qwen3-Coder-30B-A3B-Instruct-GGUF: Q2_K specifically and even at that low quant, it's exceptional at coding and tool use.
  - Why are you going so low? Just offload the the inactive experts to CPU and only keep the active ones on the vram. Yes, it will be slower but also provide better quality as you will be able to run Q5 (or Q6) UD K XL with about 15t/s and a 32k context.

- Qwen3 is nice, but thinking part of it sucks - not good.
  - There are also models that have been adjusted to use tooling: hhao/qwen2.5-coder-tools maryasov/qwen2.5-coder-cline
- There is also the new qwen3 instruct variant, which doesn't think.

- ## [Which model for local code assistant : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m27dyr/which_model_for_local_code_assistant/)
- Qwen2.5-Coder-32B vs Qwen3-32B is a fun back and forth, and both are amazing, but if you're coding you're ITERATING, and most consumer hardware (maybe short of the 2TB/s 5090) just doesn't feel acceptable here unless you quantize it down a lot, and Q4 with quantized cache starts to make silly mistakes.
  - Qwen3-30b-a3b (this also goes for the a6b version) seems like a winner because it's amazingly smart but inferences at lightspeed.. but this model consistently shows that it falls off with longer context. For coding, you'll encounter this dropoff even if you're just writing microservices after not long.
  - So Qwen3-14B is currently my go to. It handles large contexts like a champ, is shockingly smart (closer to 32B than Qwen2.5's 14B weights were), and inferences fast enough where you can iterate quickly on fairly modest hardware.

- ## [What is the top model for coding? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m5x04m/what_is_the_top_model_for_coding/)
- Gemini 2.5 Pro now has a giant 2M token context, great code quality, and fewer “hallucinations, ” while GPT-4o is close to Claude with 1M tokens and strong integration. Both now rival or surpass Claude in many tasks. definitely worth revisiting. I use each AI for it's strengths per the task.

- ## [If you limit context to 4k tokens, which models today beat Llama2-70B from 2 years ago? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lzuaa3/if_you_limit_context_to_4k_tokens_which_models/)
- Codellama 70B was a fine-tune of Llama 2. Since then the only coder fine-tune above 70B was the DS 236B. So I'm assuming later models 70B and above have also been trained on coding datasets. Like Qwen 2.5 32B coder probably was fine-tuned on the same coding datasets used in their 72B. And that coder certainly beats codellama - codestral 22B did.

- Deepseek (R1 \ V3) at Q1 at 4k context shits on Llama2 70b any day of the week for whatever task your heart desires.

- ## [What is the best self hosted model for Roo Code? : r/RooCode _202506](https://www.reddit.com/r/RooCode/comments/1l4ol5h/what_is_the_best_self_hosted_model_for_roo_code/)
  - My main dev language is JAVA and React (Typescript).

- Devstral is the best local model and it aint even close.
  - Devstral Q4_K_M (models size: 14.34GB, I set context to 45K) is a great architect! it follows instructions well, uses all tools properly and has decent speed. 
  - Q3_XXS (9.51GB, 70K context) has been crushing it as a "turbo" coder for me, even faster than the qwen 8B's and smarter too!

- The only local model under 30B which worked in Roo Code for me was qwen2.5-coder-tools. It's a fine-tunned on Cline's prompts.

- I've had decent luck with GLM, Gemma, and Qwen3-32B as well as 30B-A3B. Sounds like I need to try Mistral.

- ## [Recommendations for Local LLMs (Under 70B) with Cline/Roo Code : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1lco9ik/recommendations_for_local_llms_under_70b_with/)
- How are you serving devstral? We're running fp8 w/ full cache and 128k context on vLLM and don't see problems with tool use at all. Cline seems to work fine with it. Even things like memory-bank and .rules work. 
  - Best way to prompt it, from my experience, is like this: "based on x impl in @file, do y in @other_file."
- There are models thar degrade drastically below fp8, and I believe devstral is one of them. When I read the experience of many users online I realised people running in on full precision or q8 were very satisfied, but people running q4 said it worked awfully.

- For me Devstral q8 works well in Cline's planning mode with tool calls. For code mode I like to use Qwen coder 32b q8. This works only on Cline for me; I could not get anything useful out of Roo Code with these models: it is always running into loops

- Devstral was fast and mostly good for me (HTML, CS, JS, Python). Albeit @ q8 quantisation and 64k context. Mostly small and not complexed projects. When I tried something more complexed, “make a chess game” it failed to implement simple logic correctly. It also didn’t attempt to implement more logic like (en passant, castling etc).

- ## [Best local coding model right now? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1ktudaj/best_local_coding_model_right_now/)
- Gemma 3 is not a good coding model. Qwen2.5 coder, Qwen3, GLM-4, Mistral Small - these are better.

- Devstral’s got my full support. It's the only local model under 32B that can actually use tools to gather context in Roo/Cline without breaking a sweat.
  - Qwq's performance in roo is a bit off on my end. Its tool calling doesn't quite match up to devstral. Maybe it'll perform better with more context.
- Devstral landed two days ago, so it’s a bit early to have a full overview, but with an RTX 3900, it’s the first model that works out of the box with OLLAMA and AIDER, plus it runs at a decent speed (35 t/s for me) and 100% on GPU even with a large context. So, I would recommend giving it a try.

- I have been using deepcoder and hás serve me well until now. Still waiting for Qwen3-coder.

- I replaced Qwen 2.5 Coder with GLM 4 0414 recently. Qwen 3 seemed OK. In my tests, it was still outperformed by Qwen 2.5 Coder, although reasoning might give it the edge in certain use cases.
  - I agree about Qwen 3 not being that good at coding in general. It's weird because Supernova Medius, a mashup of Qwen 2.5 Coder 14B and Llama, was really good at coding.

- For web development, GLM-4 is significantly better than Qwen 3, QwQ and Gemma 3 for my use cases.

- Don't discard gemma totally as it can analyze images, so you can ask it to analyze the UI and what not.

- ## [LocalLLM for coding : r/LocalLLM _202505](https://www.reddit.com/r/LocalLLM/comments/1ku7zjs/localllm_for_coding/)
- Go for the highest number of parameters you can fit in vram along with your context, then choose the highest quant of that version that will still fit.
  - I find that the 32b models have issues with simple code … I can’t imagine a 7b model being anything more than a curiosity.

- Qwen2.5-coder 7B and 14B are both solid for local coding tasks.
  - Deepseek-Coder (6.7B or 13B): very strong with Python and general coding.
  - Code LLaMA 13B: great for code generation and reasoning.
  - StarCoder2 (7B or 15B): worth a try if you can stretch the limit a bit. Quite powerful.
  - Phi-2 (2.7B): super lightweight and fast for simpler tasks.

- Devstral is really good right now and IMHO it's better than qwen2.5-coder.

- ## [What would you say are the best open models for code generation? : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jyv6if/what_would_you_say_are_the_best_open_models_for/)
- Qwen2.5 coder, QwQ. Perhaps Mistral Small 24b.

- If starting from no code base, probably QwQ takes top spot due to its reasoning (thinking) steps.
  - For adapting existing code Qwen 2.5 Coder 32B, probably edges a little maybe.
  - Where the local models don’t include things like logging or type hints unless prompted (Python language), Gemini 2.5 Pro just did it without prompting.

- Ohhh something important for the local models. Make sure to configure them to get the best performance. (E.g. lower the Temperature setting to 0.5 or lower to achieve better performance for coding and maths)

- I really enjoy the directness of models that don't have reasoning. So for me that would be Qwen 2.5 32B Coder, Qwen 2.5 72B Instruct, Mistral Large 2, Deepseek V2.5, Deepseek V3-0324

- I use code models with Cline. DeepSeek V3-0324 (used through openrouter API) is much much better than Qwen Coder 32B/72B instruct. I can give it more advanced requests for implementations of various features, it's close in usability to Claude 3.7 Sonnet, it's a real workhorse. Qwen 2.5 72B Instruct which is my preffered local model as of now (I hope Qwen 3 will blow it out of the water soon)

- When searching for local model for code generation, take into consideration the context length that you can make it work at locally - I hit 40k ctx very easily even when working on single 500 LOC files.
- I expect context to be an issue. I'm currently thinking a lot about the RAG strategy (I have a lot of experience with RAG design but only for documents). I'm also pondering building an evolving graph database, which would help compile variables, functions, and classes since the files are highly structured.

- how do you like Cline? 
  - It's designed to work best with larger API-only LLMs, and it shows, so 14B LLMs for example have issues with using it's tools. I started off with Cline after doing some coding through chatting in the LibreChat UI, I didn't try other tools/extensions. 

- Qwen2.5-coder32b has been the best for me, but I can only run it slowly on my CPU, so I swap down to the Qwen2.5-coder14b that I can run on my 16gb GFX card.

- ## [Best coding models for Consumer Hardware : r/ollama _202502](https://www.reddit.com/r/ollama/comments/1ij1aaz/best_coding_models_for_consumer_hardware/)
- Qwen2.5-coder-32b is probably best, it’s great with code quality, speed and most coding use-cases.
  - DeepSeek-V3 & DeepSeek-R1 are probably the very best, but are very very slow on consumer hardware, not practical and should be reserved for very challenging assignments only.
  - If you want to alter existing code, Qwen2.5-coder-32b is probably your best bet.
  - If you want to generate from nothing, I’m not sure which wins from practicality perspective. (Possibly QWQ-preview-32b, Qwen2.5-coder-32b, llama3.3-70b or Qwen2.5-72b).
  - If you can handle the very very long completion time, DeepSeek-V3-671b and DeepSeek-R1-671b should be number 1.
  - DeepSeek-V3 can run on consumer hardware, if your available disk space is enough, but expect it to take 20mins or so to complete prompt outputs with the unsloth’s most Quantized model, if you use the SSD (I used Samsung Pro 990 NVMe) as additional RAM.
  - The DeepSeek-R1 time expands massively with the R1 model due to the additional thinking and tokens that it does. (Took 3hrs to create Flappy Bird game for me in Python, V3 took a little over 20min by comparison, about 0.5 t/s )

- Try qwen2.5-codder, even 0.5b version seems capable of producing useful code (if you keep it small, like scripts etc.)

- ## [Best LLM for Coding : r/ollama _202502](https://www.reddit.com/r/ollama/comments/1ijrwas/best_llm_for_coding/)
- double down on the qwen-2.5-codder, even 0.5b is usable for small scripts

- qwen2.5-coder:32b is the best you can run, though it won't fit entirely in your gpu, and will offload onto system ram, so it might be slow.
  - The smaller version, qwen2.5-coder:14b will fit entirely in your gpu

- what will be the suitable ram size for 32b
  - You'll need at least 24 GB vram to fit an entire 32B model onto your GPU.
  - Your GPU (RTX 4080) has 16 GB vram, so you can still use 32B models, but part of it will be on system ram instead of vram, so it will run slower.
  - You can also try a smaller quantization, like qwen2.5-coder:32b-instruct-q3_K_S (which is 3-bit, instead of 4-bit, the default), which should fit entirely in 16 GB vram, but the quality will be worse

- Is there anything I need to tweak for it to offload into system RAM? Because it always gives me an error about lack of RAM
  - No, ollama offloads automatically without any tweaks needed

- I tried qwen coder 2.5 u really need to use the 32b and q8 and it's way better than the 14b. I

- Roocoder which is based on cline is probably better. It's scary cause it can run in auto. 
  - you could leave it over night and it could fix the code or totally screw up and loop all night lol. 

- Run tests on the the q8 vs q6 vs q4. The 32b model is way better than 14b btw

- ## [Best LLM Model for coding : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gkewyp/best_llm_model_for_coding/)
- just going by the basic rule of thumb.if you want the best model you can fit on your machine always going with q4 of larger model

- how this 32b can be better than 7b-coder tuned version?
  - coder finetunes are definitely better than there corresponding base models, but Due to the increased parameters, it is more accurate in first try and also adheres to prompt better and also understands the problem way better
- the 32b is a lot lot lot better for coding.

- The larger models can be smarter, but if you don't have the spare VRAM, it might not be able to look at your whole project.

- Someone suggested Codestral-22B-v0.1-IQ3_M in another thread, and Ive been using that one for coding ever since. Mostly for python. Its really good, way better than all other I have tried.
  - Most of the time it gives me run ready redesigns and code, quite impressive.

- ## [Best LLM right now for code generation? : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1b1tycl/best_llm_right_now_for_code_generation/)
- I’m confused, why is codellama-70b so bad on this leaderboard
  - Llama 70b feels more like a ESG score replenisher. Practically brain dead. Wonder if finetunes will uncover anything useful beneath 
- I haven't used it, but I heard it's been too censored and it affected its coding abilities. But who knows.
