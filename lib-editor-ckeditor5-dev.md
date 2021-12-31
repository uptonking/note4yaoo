---
title: lib-editor-ckeditor5-dev
tags: [ckeditor, editor]
created: '2021-10-25T09:33:19.901Z'
modified: '2021-10-25T09:33:39.528Z'
---

# lib-editor-ckeditor5-dev

# 2021

- 工作内容
  - 完善docs 编辑文档页
    - 图片保存到本地数据库 迁移到 toe-frontend
  - 实现user
    - 最近文档列表
  - 实现workspace
    - 文档搜索

- 图片保存到本地数据库的改进点
  - 在应用层实现src属性替换，所以首次渲染图片时控制台会报错，但之后会正常显示图片
  - 拖拽移动图片到inline位置后，imageInline的dataRef属性仍存在，还原成imageBlock时dataRef仍能正常显示
  - 但图片处于inline状态时，刷新页面后，dataRef属性会丢失，图片会无法显示
# guide
- features

- who is using ckeditor 5
  - drupal
    - CKEditor 5 is a new experimental module

- who is using ckeditor 4
  - Liferay alloy-editor
  - Salesforce Lightning Knowledge
