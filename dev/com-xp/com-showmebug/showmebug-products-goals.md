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
  - 修改文件行号的左侧高亮
  - ai助手的交互可参考灵动岛，可缩放大小变换形状的小窗
  - 前端提出并触发生成需求的命令后，前端关闭ide页面，稍后打开页面能看到ai生成的pr, 即支持后端静默执行
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
  - devvi, swe
- clacky工具的产出是代码pr? 还是编译通过的部署预览?
  - 暂时不实现部署预览

- 自动化软件工程的生产力工具
  - p1: 生产力工具，兼容日常的开发流程
    - 提升开发效率，集成主流语言的主流开源框架，上云下云前后开发习惯不便
    - 生态集成，为了提高效率
  - p2: 平台化
  - p3: 自动化

- 需要用户导入代码
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
  - ai能力不断提升
  - ui交互创新
  - 在vscode实现基础功能的插件，引流到paas平台

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
  - 制定计划、执行计划 可采用分别的ai-agent

- 暂停时
  - 询问是否撤销当前action，会取消当前编辑或在shell输入撤销命令
  - 支持重新生成选择的代码块
  - 若暂停时修改了文件，可按原计划执行剩下的action

- 回放时
  - 文件的只读的，不能编辑

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
  - 针对需求，现在本地生成新分支，push到github新分支

- 
- 
- 
- 
- 
- 
- 

## com-meeting240506-showMeBug

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

# pm
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
# pm-cursorai
- cmd + k : edit and write code with the AI
- Terminal Command K
  - write terminal commands in plain english
  - You can use it to write sql commands, fill in argparse arguments, and parse jsons with jq.
- Copilot++ is Cursor's native autocomplete feature
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
# pm-code-ai
- [2024 Roadmap · opensumi/core Wiki](https://github.com/opensumi/core/wiki/2024-Roadmap)
  - AI Native 模块发布：提供 AI 原生的 IDE 交互体验
  - 通信层改造：去除 jsonrpc 协议，使用 fury 压缩后的二进制方式协议提高 IDE 通信性能
  - 插件市场迁移：插件市场由阿里云迁移至支付宝小程序云，提供更稳定的服务
# more
