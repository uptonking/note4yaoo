---
title: lib-editor-ckeditor5-dev
tags: [ckeditor, editor]
created: '2021-10-25T09:33:19.901Z'
modified: '2021-10-25T09:33:39.528Z'
---

# lib-editor-ckeditor5-dev

# 2022

# guide
- features

- who is using ckeditor 5
  - drupal
    - CKEditor 5 is a new experimental module

- who is using ckeditor 4
  - Liferay alloy-editor
  - Salesforce Lightning Knowledge
# block-editor-codebase
- AffineEditor
  - 准备编辑器相关配置和插件，初始化 BlockEditor 实例
  - RenderRoot 传入BlockEditor实例
  - RenderBlock 传入root_block_id
  - mock未传入root_id时，手动先创建page再渲染editor

- RenderRoot
  - 获取editor最外层的div元素ref，挂到editor对象的属性下
    - editor的内容block会作为children渲染
  - 触发editor渲染 editor.getHooks().render(); 🤔 
  - 传入全局鼠标事件到editor
    - onMouseUp/Down/Move/Out

- RenderBlock
  - 异步获取block对象
  - 每个block都是div，div ref会挂到block.dom属性下
  - 通过 block_util?.createView({ block, editor }) 渲染block视图
  - 注册当前block的 onMouseMove 事件到editor全局
  - 提供了block层级的选区事件 useOnSelect/useOnSelectionChange

- useBlock
  - 返回AsyncBlock对象
  - 返回的block对象会自动触发block重渲染，实现通过 node.on('change', () => { requestReRender(); }); 

- BlockEditor
  - BlockManager
  - PluginManager
  - SelectionManager
  - CacheManager
  - StorageManager
  - hooks
  - block_utils
  - workspace_id
  - root_block_id
  - readonly
  - ui_container
  - 提供了编辑器的对外操作方法

- page-block
  - createPageView
# block-editor-codebase-legacy
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
