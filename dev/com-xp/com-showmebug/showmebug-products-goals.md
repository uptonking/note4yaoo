---
title: showmebug-products-goals
tags: [company, pm, products, showmebug]
created: 2024-05-06T02:51:59.628Z
modified: 2024-05-06T02:52:41.789Z
---

# showmebug-products-goals

# guide

# products

# products-clacky-ai

## goals?

- 目标
  - 以ai为主，减少人的工作
  - 开发者多写ai提示词，而不是代码

- 亮点
  - online版，对协作支持更好
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

- 需要用户导入代码
  - 考虑私有化部署

- 典型的使用场景
  - 自动补全逻辑
  - 自动生成单元测试

- 辅助编码的ai编程产品和侧重拖拽的低代码产品有什么区别
  - 低代码的实现与具体技术栈绑定，而ai编程更多是在语法和语义上帮助开发者提效
  - 低代码的用户可以是非开发者

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

# goals

# more
