---
title: lib-editor-ckeditor5-dev
tags: [ckeditor, editor]
created: '2021-10-25T09:33:19.901Z'
modified: '2021-10-25T09:33:39.528Z'
---

# lib-editor-ckeditor5-dev

# 2022

# 0510
- 迁移到包含service层的架构后，顶部导航条获取page标题的时机难以确定
  - 原因1: 导航条NavigationBar是未被route_private包裹的，渲染时机非常早
  - 原因2: 顶导航条通过router的useParams只能获取到workspace_id，不能获取到page_id
  - 就算用魔法强制在page初始化后注册title更新的事件监听器，navbar更新title还是失败
# guide
- features

- who is using ckeditor 5
  - drupal
    - CKEditor 5 is a new experimental module

- who is using ckeditor 4
  - Liferay alloy-editor
  - Salesforce Lightning Knowledge
# block-editor-codebase
- db层的设计
  - getContent 用来获取block内容
  - getChildren 用来构建block间的关系

- 全局共享的editor对象，只在db初始化时创建一次，并未对外暴露修改自身的方法，所以可以直接在editor对象上添加新属性

- BlockEditorEntry
  - editor.loadBlock(rootId)
  - editor.setRootBlock( editor.getBlockById(rootId) )
  - 提供editor默认插件和配置

- EditorRoot
  - 将全局共享的editor对象通过 EditorContext. Provider 传递下去
  - 触发编辑器的渲染 editor.pluginManager.runHook('render'); 

- RenderBlock
  - `return <RenderBlockContent {...props} />;` 直接把props传过去渲染Content
  - 注册 content 和 children 的监听器，触发block的重渲染

- RenderBlockContent
  - 渲染 `<View {...context}></View>` ，所有View都传入editor和RenderChildren/Map方法
