---
title: editoe-engineering-guide
tags: [editoe, engineering]
created: '2021-10-23T18:07:53.915Z'
modified: '2021-10-23T18:08:23.141Z'
---

# editoe-engineering-guide

# guide

# principles 设计原则
- Think Universal
  - 支持纯键盘唤起
  - 支持纯按钮唤起
  - 支持 i18n
- Keep It Simple
  - 简洁易用、最小化
- Shareable & Collaborative & Iterative
  - 可分享、可协作、可迭代(版本控制)
- Illustrative, Designed For Web
  - 可交互的好于动态的
  - 动态的好于静态的
  - 静态的好于纯文字
- Focus on content, not formatting
  - 处于创作模式时，不应该加入复杂的排版配置功能
  - 让用户专注创作，输出结果时进行排版
# compatibility 兼容性要求
- PC浏览器平台
  - 支持Firefox，Safari，Chrome，Edge浏览器

- 移动端
  - 除去编辑功能外，其他展示性组建均能正常显示
  - 需要验证的设备：iPhone, Android
# development 研发流程
- 每个版本的预计工作量大概在一个月左右
  - 在新版本release前，我们会持续将增量更新推送至 canary 频道
  - canary的数据、账号，与Editoe相互隔离

- Done的定义
  - 满足 设计原则
  - 满足 兼容性要求
