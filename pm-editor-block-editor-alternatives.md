---
title: pm-editor-block-editor-alternatives
tags: [alternatives, block-editor, features]
created: '2022-06-08T11:06:00.338Z'
modified: '2022-06-08T11:12:21.488Z'
---

# pm-editor-block-editor-alternatives

# guide

# 飞书块编辑器
- 飞书发布了block-editor v20220608
  - (炫酷的功能，但可能不实用；飞书推广概念降低我们的运营成本)
- 亮点是拖动实现水平并排布局，并排后可调节每栏宽度
  - 分栏默认最多5个，之后不可再次添加分栏
  - 日程可以拖到分栏里面，但多维表格不能拖到

- 【二期提醒】: 使用 html 初始化时，请用newEditor反序列化后传入到 oldEditor
  - aceRegisterBlockElements 不再支持，请业务重写Editor.isBlockElement

> 与ace editor应该无关，因为虽然每行也是 ace_line，但data-*属性用的少
