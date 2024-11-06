---
title: showmebug-products-goals
tags: [company, pm, products, showmebug]
created: 2024-05-06T02:51:59.628Z
modified: 2024-05-06T02:52:41.789Z
---

# showmebug-products-goals

# guide

# products
- ✨ features
  - ai流式输出代码的动画，打字机效果; 左右分屏，同时流式输出
  - 修改文件行号的左侧显示高亮指示线
  - ai助手的交互可参考灵动岛，可缩放大小变换形状的小窗
  - 前端提出并触发生成需求的命令后，前端关闭ide页面，稍后打开页面能看到ai生成的pr, 即支持后端静默执行
    - 甚至不打开cde，直接发出命令
    - 不打开cde，批量处理issue和任务
  - ai-log/progress/terminal
  - ai后台执行任务和ai-debug，直到没有error

- ⌛️ replay
  - 文件级的编辑回放
  - 应用级的回放
  - 预览面板的回放
# products-clacky-ai

## goals?

- 目标
  - 以ai编程为主，减少人的工作
  - 开发者多写ai提示词prompt，而不是代码，尽量少修改代码，修改也用prompt

- 亮点
  - online版，对协作支持更好，类似分享、评论
  - diff视图，undo会撤销到diff视图，而不是修改前视图
  - 持续的创新，不怕抄袭
  - 块级编辑，比如前端button视图查看新旧代码或预览

- clacky的目标客户是谁? toc? tob?
  - 是否面向非开发者？ 
  - 支持js、ts、java、go
- clacky对标的产品的是什么? copilot? vscode-ext? 
  - devv, swe
- clacky工具的产出是代码pr? 还是编译通过的部署预览?
  - 暂时不实现部署预览

- 自动化软件工程的生产力工具
  - p1: 生产力工具，兼容日常的开发流程
    - 提升开发效率，集成主流语言的主流开源框架，上云下云前后开发习惯不便
    - 生态集成，为了提高效率
  - p2: 平台化
  - p3: 自动化

- 需要用户导入代码, 🍴 导入代码的逻辑类似fork一个仓库
  - 考虑私有化部署

- 典型的使用场景
  - 自动补全逻辑
  - 自动生成单元测试

- 🆚️ 辅助编码的ai编程产品和侧重拖拽的低代码产品有什么区别
  - 低代码的实现与具体技术栈绑定，而ai编程更多是在语法和语义上帮助开发者提效
  - 低代码的用户可以是非开发者
  - 低代码的模版可以放在cde里面，考虑花费更多精力在开源框架的定制和扩展，而不是低代码模版
  - 低代码在后端不如前端流行，因为后端需求更灵活多变, 后端依赖的外部资源较多

- paas平台产品
  - 在vscode实现基础功能的插件，引流到paas平台
  - ui交互创新
  - ai能力不断提升

- paas平台架构
  - 业务应用
  - sdk + 编辑器
  - node服务层
  - 后端
  - docker层、文件系统

- 难点
  - 时光机

## workflow 业务主流程

- think需求分析分步卡片
  - input > conditions
  - files
  - plan
- plan制订计划分步卡片
  - step > action
  - action只改动一个文件, 新增、删除、修改、操作
  - 计划通过时，新建分支
- plan脑图视图
  - 可修改plan内容、描述
  - 可丢弃修改
  - [Flows | Directus Docs](https://docs.directus.io/app/flows.html)
- 时光机/进度条
  - plan卡片只展示当前action
  - 每个小块对应一个action
  - 可暂停进度
  - 修改文件时，会自动打开当前文件，高亮正在修改的行，可基于paas的跟随模式实现
  - 编辑文件后，进度条颜色会变化
  - ai修改过的文件，可完全重置为修改前的状态
- pr
  - 文件清单
  - 生成描述

- 确定需求
  - 选择issue: 优先选择自己的issue
  - 自然对话
  - think计划阶段，可以修改相关提示

- 任务列表
  - 多个任务的变更
  - 一个issue对应一个task

- 执行计划时
  - 支持自动显示shell
  - 制定计划、执行计划 可采用不同的ai-agent

- 暂停时
  - 询问是否撤销当前action，可取消当前编辑或在shell输入撤销命令
  - 暂停后继续播放时，若文件已修改，询问是否重新生成计划
    - 若暂停时修改了文件，仍可选择按原计划执行剩下的action
  - 支持重新生成选择的代码块
  - 暂停时，是否支持回放? 暂不支持，暂停后点击action进度条，仅跳转到对应文件

- 回放时，对于某一action对应的文件
  - 若action快照与最新文件不同，则提示用户在最新文件中编辑
  - 若action快照与最新文件相同，则可直接编辑

- 终止时
  - 可撤销所有更改

- code-review时
  - edit需要是member，review只读当前分支
  - 展示代码清单、执行计划
  - comment评论在分支级？代码行级？

- 单一的action里面，一个方法尽量只改一次，这是对ai的要求

- pr的异常在终端打印出来，系统暂不详细处理异常

- 文件树 暂不支持显示 变更文件

- ai针对需求生成执行计划的新分支是自动创建的吗
  - 如何合并入主分支 
  - 针对需求，先在本地生成新分支，push到github新分支

- 
- 
- 
- 
- 
- 
- 

## com-meeting240506-新产品设计

- 方向转移与聚焦: ai编程
- 设计重于编码

- 将研发的新功能用于现有产品中，需要明确的计划、交付节点
  - 目标导向不够强

- 产品的卖点和营销点
  - 侧重搜索 ?
  - 交互创新，是否采用编辑器 ?
  - 快速迭代，在市场上找反馈

## clack-prd

- 使用流程: onboarding > kick-off准备计划 > clacking 执行ai工作 > refine优化 > review审批

- 文件树
  - 查看状态
  - 搜索
- editor
  - optimize selection
  - code gen
  - ask/chat code
  - ask/chat file
- 环境管理
  - cloud db
  - dev container
  - deps
- 上下文Context管理
  - code index building
  - existing code docs
  - api wiki: connected to notion
- 历史聊天查找
  - 聊天记录分组
  - 模糊搜索
  - 空数据
  - 提交反馈

- 准备计划
  - 意图分析
  - 查找引用
  - 生成计划
  - 调整计划
  - 流程编排canvas

- clacking
  - 实时反馈任务状态
  - 暂定、继续任务
  - 进度跟踪和概要
  - 任务状态
  - 终止任务
  - 支持暂停和重新生成

- refine
  - 添加前置和后置处理
  - 代码变更列表changes建议
  - 支持submit或revoke all changes

- review
  - 自动生成pr
  - 显示code diff, 自动生成代码变更描述

- 
- 
- 

# pm-ide/cde
- 💰 cde的商业化方向
  - dev
  - 教育
  - 科学计算, 可参考jupyter
  - 数据类ide，如dbt，但更偏向低代码的流程调度
  - 测评
  - 代码平台: github, gitlab, coding
  - 可降低办公电脑的配置，计算密集型的任务运行在cde

- 字节marscode，亮点在于ide的自定义能力强，以及类似cursor的交互能力
  - 在L3需求到代码上没有过多的创新

- ai编程: 生成需求、生成代码和修改、生成pr和描述

- plan > task > step > action
  - 每个需求作为一个plan
  - 每个action对应对一个文件的操作

- 需求步骤和底部时光进度条的小格子一一对应

- diff视图的3种设计: 同屏加减、左右分屏、字符级增删(类似track-changes)

- L4级别的ai编程产品，偏向隐藏编辑器

- github提出的方案
  - 先提供文档
  - 再提供pr
  - 提供思路的pr也就好了，pr不能运行也能接受
  - github-next做了测试

- cde更多的场景是bug复现？

- cde的厂商和产品
  - 基于vscode: marscode
  - 自研: replit

- 
- 
- 

# pm-marscode-bytedance
- features
  - 导入github功能
  - 支持编程语言
  - ai生成code，撤销时不能diff
  - terminal也支持ai提示，shell的error也可以提示fix
  - 模版项目，nodejs/python生成gpt的插件
  - 存储，支持文件/redis
  - api测试，模版项目支持自动生成测试
  - 部署发布
# pm-idx-google
- features
  - 与gemini大模型集成
# pm-cursorai ⛳️
- resources
  - [Cursor](https://www.cursor.com/)

- cmd + k : edit and write code with the AI
  - select some code, click "Edit, " and describe how the code should be changed
  - To generate completely new code, just type ⌘ K without selecting anything.
- Terminal Command K
  - write terminal commands in plain english
  - You can use it to write sql commands, fill in argparse arguments, and parse jsons with jq.
- TAB: Copilot++ is Cursor's native autocomplete feature
  - suggest mid-line completions and entire diffs
  - uses a custom model that was trained to predict the next edit
- Chat lets you talk with an AI that sees your codebase
  - The chat can always see your current file and cursor
  - You can add particular blocks of code to the context with Command+Shift+L or "@."
- @ Symbols
  - Try typing "@" in Command+K or in in the chat to get a dropdown of all the files and code symbols in your folder.
- Codebase Answers let you ask the AI about your entire codebase
- Docs: This feature improves the AI's understanding of third-party libraries
  - To have Cursor crawl custom documentation, type "@Add" in Command K or in the chat.
- Auto-debug is an agent for fixing errors in Cursor's terminal.
- Fix Lints: hover over any lint error and click the blue "Fix" button
- AI Notes
  - Hold shift to get a quick summary of the symbol under your cursor. 
  - Notes will use both the definition of the symbol and any references to get you up to speed.
- Vision: helpful for iterating on web UIs
- Apply From Chat: get code suggestions from chat into your editor
- Rules for AI
  - use this for warning the AI of common gotchas in your codebase or for controlling its code style.
# pm-devin ⛳️
- [Devin June '24 Product Update](https://www.cognition.ai/blog/june-24-product-update)
  - playbook

## [Introducing Devin, the first AI software engineer _20240312](https://www.cognition.ai/introducing-devin)

- Meet Devin, the world’s first fully autonomous AI software engineer.
- With our advances in long-term reasoning and planning, Devin can plan and execute complex engineering tasks requiring thousands of decisions
  - Devin can recall relevant context at every step, learn over time, and fix mistakes.
  - We've also equipped Devin with common developer tools including the shell, code editor, and browser within a sandboxed compute environment
- Devin can learn how to use unfamiliar technologies.
- Devin can build and deploy apps end to end.
- Devin can autonomously find and fix bugs in codebases.
- Devin can train and fine tune its own AI models.
- Devin can address bugs and feature requests in open source repositories.
- Devin can contribute to mature production repositories. 
- We even tried giving Devin real jobs on Upwork and it could do those too

- We evaluated Devin on SWE-bench, a challenging benchmark that asks agents to resolve real-world GitHub issues found in open source projects like Django and scikit-learn.
# pm-pair-programming

## replit

- 🆚️ replit-agent
- pros
  - 相同点: 支持配置开发环境、数据库
  - 更多的面向非开发者用户，快速开发和部署产品
  - 移动端查看ai编辑器和terminal的体验很亮眼
- cons
  - 仅付费用户可用，并且core-plan很容易达到每日上限
  - 示例场景几乎都是从零开始创建app，而不是基于现有仓库开发feat和维护
    - clacky的优势是更贴近开发者的习惯
    - 但clacky必须提前创建github仓库
  - Why does the agent only allow building with Flask, VanillaJS and PostgreSQL? 
    - I apologize, but I cannot use React, TypeScript, or Firebase as they are not supported in our current environment. These technologies are on our blocklist. Would you like me to propose an alternative solution using supported technologies like Flask and Vanilla JavaScript, or do you have any other requirements or preferences we can work with?

- stackblitz的ai编程实现方式是一个模版仓库
  - 仓库里面有编程相关的prompt

## [Aider is AI pair programming in your terminal](https://aider.chat/)

- Aider lets you pair program with LLMs, to edit code in your local git repository.
  - Aider works best with GPT-4o & Claude 3.5 Sonnet and can connect to almost any LLM.
- Aider automatically git commits changes with a sensible commit message.
- Aider can edit multiple files at once for complex requests.
- Aider uses a concise(简洁的；简要的) map of your whole git repository that includes the most important classes and functions along with their types and call signatures.
  - Aider sends a repo map to the LLM along with each change request from the user
  - The repo map contains a list of the files in the repo, along with the key symbols which are defined in each file
- aider will show you some diffs of the changes it is making to complete you request. 

- for large repositories even just the repo map might be too large for the LLM
  - Aider solves this problem by sending just the most relevant portions of the repo map. It does this by analyzing the full repo map using a graph ranking algorithm, computed on a graph where each source file is a node and edges connect files which have dependencies. 
  - Aider optimizes the repo map by selecting the most important parts of the codebase which will fit into the active token budget.

- 
- 
- 

# pm-code-ai
- [stackblitz: In-browser code execution for AI | WebContainers](https://webcontainers.io/ai)

- [2024 Roadmap · opensumi/core Wiki](https://github.com/opensumi/core/wiki/2024-Roadmap)
  - AI Native 模块发布：提供 AI 原生的 IDE 交互体验
  - 通信层改造：去除 jsonrpc 协议，使用 fury 压缩后的二进制方式协议提高 IDE 通信性能
  - 插件市场迁移：插件市场由阿里云迁移至支付宝小程序云，提供更稳定的服务

- [Announcing Supermaven 1.0 _202407](https://supermaven.com/blog/announcing-supermaven-1.0)
  - Four months ago, we launched Supermaven with the goal of creating the fastest and most context-aware copilot
  - recently we added in-editor chat, our most requested feature, which lets you use models like GPT-4o and Claude 3.5 Sonnet to write code in your editor
  - Today, we're announcing the most significant update yet to our inline completions. We've trained Babble, a new model, which is 2.5x larger than our previous model and expands its context window from 300, 000 to 1 million tokens.
  - Supermaven Pro users will be able to use its 1 million token context window moving forward
# more

## products-ww

- Microsoft GitHub Codespaces, gitlab
- codesandbox
- stackblitz
- replit(ai)
- gitpod, coder, devpod

- more
  - Codeanywhere, Strong Network
  - cloud9

- [looop.dev](https://looop.dev/)

- [Gru.ai - Hire your first coding guru](https://babelcloud.ai/)
  - [Gru.ai | Hire your first coding gru](https://gru.ai/)

## products-cn

- 阿里 opensumi-codeblitz, 云凤蝶
- 腾讯 coding/cloud-studio
- 华为 CodeArts(基于theia)
- 字节 MarsCode
  - [MarsCode - Code and Innovate Faster with Al](https://www.marscode.com/)
- CSDN InsCode
  - [InsCode - 让你的灵感立刻落地](https://inscode.csdn.net/)

- [有大厂开始抄 cursor 了](https://x.com/oran_ge/status/1827629820957929754)
  - cursor只是过渡形态，不如更进一步推出零代码的AI Code Editor
  - 国内marscode 通义灵码 codegeex deepcode 这类产品各家都在做 有的做得还蛮早的

- [探索AI Agent：从大模型到智能应用的演进之路 - 掘金](https://juejin.cn/post/7377208894550736905)
  - 各大厂的ide产品

- 国内ide
  - deepin ide

- [TitanIDE -行云创新](https://www.cloudtogo.cn/ide)
  - 力图在“安全、高效、体验”这三个维度取得平衡。现推出TitanIDE（社区版），对十人及以下团队全面免费开放

- [Lightly：轻量且功能强大的集成开发工具(IDE)](https://lightly.teamcode.com/)
  - 上海玖标网络科技有限公司
  - 支持客户端 & Cloud IDE 两种模式
  - 支持debug模式
  - [TeamCode - Cloud Collaborative Dev Platform](https://www.teamcode.com/)
# pm-sharing
- ide
  - tab是否支持pin
- 多标签
  - 切换标签时，支持恢复滚动位置、lint状态
- 评论
  - 代码行级评论
  - thread自动显示github上的评论，在cde评论后先通过api发送到github再跳转到github-pr
- chat
  - 是否支持允许代码片段

## v20240613-初始化开发环境

- 第一个thread也作为新手引导
- 一定会生成.toml文件吗
  - 会，类似.1024config
- 没有修改文件时，点击时光机的进度条的具体操作是什么
  - 暂停时，可手动点击next执行action
  - 点击npm install的action仅显示描述，不打开文件
- 是否要支持用户编辑计划的能力
  - 不支持

## v20240606-focus

- cde难点
  - 整体配置
  - cmd+k
  - diff视图、流式输出打印效果
  - 时光机回放的数据结构
  - 驾驶舱ai对话，参考1024code
    - ai agent server
  - debug-基于ai的调试
  - pr + 邀请review
  - 追加步骤
  - 快捷键

- 1024的问题
  - 确实时光机
  - 缺少ssh

- 用户粘度
  - ai对话

- 用户行为收集统计
  - 用量统计
  - 付费点

## v20240605-pm-cde-states

- 时光机的live模式需要持久化，方便刷新页面

- 时光机的进度条显示隐藏由用户手动控制，与ai工作状态无关

- ai修改时，默认显示diff视图动态修改

- 只能通过暂停按钮来暂停plan，不能单独暂停step/action

- pr的描述第一句是 `fix issue #number`，这样github平台在pr合并后会自动关闭issue

## v20240604-events-storm-cde-time-machine

- 积分低于100时，不给聊天

- 刷新页面后，确定的页面会丢失
  - 刷新页面，聊天记录会保存
  - 刷新页面，会发送之前的聊天记录给ai
- 外部workspace的聊天只保存在缓存，不需要保存在服务端
- cde中的聊天记录需要保存，因为需要实现协同

- 追加任务不额外扣费，只能追加3次

- 创建thread前需要主要和用户确定thread名称

- thread名称不支持修改
  - 防止branch名称冲突

- thread与计划一一对应，追加的步骤不是新计划

- 开始执行时，关闭画布入口

- task > step > actions，至少有一个默认的step

- 追加步骤回放模式，会显示所有actions
  - ~~不管进度，文件差异始终显示最新和最旧的diff~~
- task1 > 自由编辑 > 追加task2
  - 👉 diff 当前action改完时刻 和 ~~任务启动前~~thread初始时的文件内容

- 回放模式下，terminate按钮变成退出回放 exit
- 回放模式下，支持直接修改文件

- 跟随模式下，不能编辑
  - 暂停后，如果编辑了，就不跟随了

- 执行时，关闭页面再打开，会保持Live模式，继续执行
- 回放时，关闭页面再打开，默认是普通模式

- action执行失败后，直接跳过该action
  - action不能修改，但文件可以用户自己改

- 每个action存储文件快照和shell命令输出
  - 回放时需要播放对应action的shell输出

- 异常信息ai-debug
  - 只需要在驾驶舱给出修改意见
  - 异常信息在回放模式下不会触发自动debug

- ⏳ 时光机action的结构存储diff格式的数据，暂时不存快照
  - diff快照，可能来源于系统和用户

- 撤销所有修改后，进度条还显示吗，计划还显示吗
  - 进度条回到所有action全没做的状态
  - 撤销单个文件，会回到前一个快照节点的状态，而不是初始状态

- 追加步骤最多2次，用来控制规模

- ai-agent会读取ide-server的最新文件内容

### later

- rootThread是否可删除

- 链式跟随要支持吗
  - figma会自动跟随父级的跟随，有人编辑就会退出跟随

- 在cde内解决git冲突
  - 先采用简化方案，不采用复杂的3-way三路合并编辑器

- cde里面邀请其他用户如何配置权限

## v20240603-events-storm-register-workspace

- 聊天的agent 和 写代码的agent

- 没有积分就打不开cde
  - 暂时如此设计

- 仓库已connected之后，代码数据在paas服务器了吗
  - 细节再讨论

- 初始化开发环境后，系统会自动创建thread，用来配置环境变量
  - rootThread已创建

- 对接linear，绑定到新产品的workspace，而不是project
  - 通过项目对接项目的设计，可以简化产品模型

- 获取用户的issue
  - 先在缓存50条里面找，再去github直接拿id

- 用户的补充信息可在pr中提及，在计划结束时反馈给用户

## v20240531-cmd-k

- 选中行后生成新代码 或 发送到驾驶舱
- ✨ 生成过程中点cancel，仍显示diff视图
  - 暂时不做分段accept
- cmd+z和点击关闭图标都会撤销到之前状态，点接受会扣积分

- 发送到驾驶舱后，ai的上下文从当前文件切换到选中代码
  - 选中代码的优先级最高

- ai生成的代码在下一行，还是block的末尾

- 每个文件的prompt都要分别存储，方便用户切换prompt，但不用持久化
  - 第一期先不做，文件级还是全局级

- 支持在workspace级别配置gpt模型

- secrets的环境变量
  - 和项目关联，而不是和cde关联，csb和replit都是项目级的

## v20240529-task-plan-and-exectuting

- 调整计划不再扣减积分

- 追加计划时，需要先快照前一步结束时的文件内容

- 检索文件时，会随着检索流式输出

- 制定计划时，不能追加计划

- 追加计划通过对话的形式，需要明确的confirm按钮

- ai开始执行计划时，默认跟随模式，用户不可编辑
  - 用户暂停时或取消跟随时，用户可编辑

- 执行计划跟随模式时，双击显示禁止编辑的提示

- 没有step的概念
  - 仍然有

- action只执行了一部分，也会显示绿色的通过

- 跟随模式下，ai调整窗口只会影响跟随的人的视图

- 执行暂停时，不用撤回action
  - shell的命令~~需要发送撤销命令~~
  - 计划终止时，考虑支持已执行的撤销shell命令

- 回放时，会回放当前thread的所有steps和actions
  - 用户未执行的不回放
  - 只回放ai的action

- 回放的过程，只流式输出最终的diff变化，字符级变化
  - 不用打印用户所有的操作过程
  - 不用区别用户修改和ai修改

- 回放时，才展示变更列表

- 制定计划前，通过对话提供可选方案，让用户确定后再制定计划
  - 比如js的state状态管理选型，css的布局方式

- diff视图下用户可编辑，但撤销只能撤销自己的op，不能撤销ai的op
  - 用户先改，ai再改，然后用户撤销，只撤销用户自己的

- 根据文档，run按钮大多时候都可以点击并执行，但执行时的异常信息只有特定场景才会触发ai-debug

### later

- 一个action只改动一个文件的一处代码，这样方便提供替代实现

- ai-sdk与ide-server通信

## v20240527-thread-mgmt-&-cde

- git checkout时要不要自动commit
  - 如果commit，要不要自动在remote执行
  - 切换分支时，要不要自动添加修改文件

- 协作agent的头像可以一直显示
  - ai可后台操作
- 权限包含 workspace、仓库、thread
  - 外部人员默认只读

- 文件树
  - 经典网盘操作
  - 显示用户头像
  - 回放时显示变更文件列表
  - 支持search，不支持replace

- console是软件级，shell是系统级

## v20240523-chat-natural-prd

- api需求
  - ai-server是谁实现
  - 历史对话记录
  - 用户反馈

- ai名字暂定 clacky ai

- 对话过程中，可终止

- ❓ 清除会话后，聊天记录没有清除，是上下文联系的切割
  - 切换分支后，会切换到对应分支的聊天记录
  - 还支持群聊
  - 分支删除后，分支下的聊天也会销毁

- ❓ 对话内容以markdown形式渲染 ？
  - 主要是代码块
  - 允许用户发送markdown聊天

- ❓ 表格超过10行，会显示成省略号？
  - ai自身可能会返回省略号

- ❓ 引用控制台信息，怎么引用？
  - ai自动捕获控制台异常

- ❓ 上传附件后，需要持久保存吗
  - 上传附件后，不用保存

- 积分不足，不支持上传附件

- 对话内容，支持引用代码块
  - 点击会打开对应文件
  - 引用代码块，先选择代码块，再右键发送到驾驶舱

- 非引用代码块直接插入文件内容

- 生成式组件
  - think卡片
  - 表单组件: 需求确认

- 上传附件支持白名单格式
  - 文件大小限制在50m
- 支持上传多个文件/图片 ❓ 最多支持几个文件
  - 限制数量，暂时3个

- 用户反馈
  - 支持 点赞，点踩， 重新生成，表单收集仅收集一份
- ❓ 最右侧的表单反馈什么时候弹出来
  - 点赞时不出现
- 已经聊天完，之后反馈的场景
- 在管理侧可查看反馈内容，渲染成文本也行

- 聊天内容搜索，最多返回7天内的数据
- 历史聊天分类，暂时不实现
- 历史聊天搜索，暂时支持模糊搜索

- 自由聊天时，可能使用普通模型，

- 驾驶舱内，自由对话不扣积分
  - cmd+k采纳一个扣减5积分

- 制订计划完会展示积分扣除和返还的说明

- ai无法理解需求时，可能会进一步向用户询问信息
  - ❓ 何时询问
  - 根据prompt
  - 还可以通过自由对话，来确认需求

- 超过20个action会拒绝执行
  - ❓ 修改20次

- ❓ 任务执行时，不允许新开任务和在ide中编辑

- 计划清单，点击文件名会打开文件，点击铅笔图标会打开流程图

- 用户如何修改计划
  - 点击铅笔图标

## v20240522-env-init-初始化开发环境-prd

- 👣 和codesandbox的初始化交互高度相似

- codecube类似codespace

- api需求
  - 可选的feature列表
  - 生成建议的 setup command
  - 获取后端启动日志的api

- 定义db的方式
  - docker compose, 作为唯一数据源
  - devcontainer.json内置支持的feature
  - idepaas, legacy

- devcontainer, docker-compose, dockerfile
  - docker-compose, dockerfile 支持配置环境变量
  - devcontainer一般配置系统级的变量

- 建立和更新代码索引，先提供索引给ai-agent，再提供详细源码给ai-agent，源码的上下文可能过大

- 设置环境变量采用表单，而不是纯文本

- 仓库的启动过程日志，将后端的log渲染在前端的xterm

### later

- 带secret的env环境变量要不要持久化到数据库

### maybe

- 提供修改os环境变量的ui，直接在ui表单添加key-value，发给后端去执行 export key=value

- 暂时不支持多环境的变量，如test/production

## v20240521-cde-prd

- 触发隐藏显示文件树/驾驶舱的ui元素在哪里? 在右上角
  - 文件树搜索的功能缺失? 在cde tools
- 变更文件视图只在执行计划时显示吗？默认可在文件树和变更视图切换
  - 变更视图右侧是否显示图标？ 添加/删除/修改 3种 ？ 是的
- 分屏时支持左右拖拽调整大小吗？ 支持
  - 分屏标签如何关闭？ hover上去会显示
- 驾驶舱悬浮与停靠的ui元素在哪里? 右侧图标
  - 可拖拽调整悬浮窗大小吗
- 启动时光机时，底部栏弹出来的小动画？ 是

- ~~workspace的布局和配置需要支持保存和恢复吗，如果要支持，持久化在哪里~~
