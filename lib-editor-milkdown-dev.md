---
title: lib-editor-milkdown-dev
tags: [editor, lib, markdown, milkdown, prosemirror]
created: 2021-07-11T12:20:13.844Z
modified: 2021-07-11T15:08:26.481Z
---

# lib-editor-milkdown-dev

# guide
- pros
  - prosemirror和remark的生态都很丰富
  - 支持自定义markdown语法并给出了示例，可以自定义解析过程

- cons
  - 没有实现较复杂的组件，如直接缩放的图片，全部基于html标签toDOM/parseDOM实现
  - 过于强调remark的配置会破坏编辑器插件的设计，remark不应该作为和编辑器插件平级的一级配置，一级配置应该是编辑器的主要features如slash菜单、markdown；remark应该作为markdown的二级配置

- features
  - WYSIWYG
  - themeable
  - hackable with plugins，支持创建remark和prosemirror两类plugins
  - reliable on top of prosemirror and remark
  - plugins
    - slash & tooltip，不像其他项目内置slash，这里可选择
    - latex math equations support
    - table support

- tips
  - 不要将关注点放在markdown，渲染和编辑的实现几乎全部依赖于prosemirror，只有少数场景如初始化和导出才会用到parser和serializer
  - 自定义syntax的要点
# faq
- 通过atom来控制执行流程的设计更清晰，还是更繁琐？
  - 优点：
  - 很多其他项目也会使用这种类似ioc依赖注入的风格，传入实例属性不使用constructor，而是通过在init/inject方法中赋值
  - 本项目只注入了全局单例的this.context对象，没有注入其他对象，实现很简单；
  - 其他很多其他对象都保存到了this.context的二级属性或三级属性
# examples

## extensions

- https://github.com/omarmir/milkdown-plugin-file /AGPL/202506/ts
  - Milkdown plugin that adds remark directive support and prosemirror component to handle file uploads
# codebase
- dataflow
  - md str > mdast > prosemirror node > dom

## prosemirror-editor

- nodeViews作为pm-EditorProps传入，支持使用react组件作为NodeView

- 通过在editorView.dispatchTransaction()中执行options中传入的监听器函数，来实现各种交互
  - 控制粒度不如NodeView，NodeView只在指定类型Node出现时才会触发执行；并且NodeView和plugin.view对dom ui的控制力很强

- Editor编辑器所有操作的顶级入口类，但pm-EditorView的创建不在这里
  - this.#ctx保存了核心的编辑器数据，通过#injectCtx()注入到所有atoms对象，有点依赖注入ioc的风格；几乎所有atom子类都没有构造函数，公共父类的构造函数只是简单赋值，main()方法只有一个，不像声明周期函数
  - 编辑器的初始化流程是依次执行状态分别为idle/loadSchema/schemaReady/loadPlugin/complele的所有atoms的main方法
  - 流程中最重要的步骤是createSchema, loadPlugin

- schema.nodes
  - 内置doc、text、p、blockquote、ol、ul、li、codeblock、heading、hardbreak、image、hr
  - 全部基于html元素标签实现，包括image、ul
- schema.marks
  - 内置strong, em, code-inline, link

- code-fence/codeblock的实现
  - parseDOM中getAttrs只获取了language，没有获取代码文本内容
  - toDOM实现较复杂，完全基于dom操作，交互通过select.addEventListener注册监听器实现

- milkdown统一了插件的注册方式都是milkdown.use(pluginAtom)
  - 但remarkPlugin在idle状态执行，因为每注册一个新的remarkPlugin，remark的值都被更新
  - prosemirrorPlugin在loadPlugin状态执行

## markdown

- mdToPMNode-parser
  - 使用场景很少：转换defaultValue，解析pasteValue

- PMNodeToMd-serializer
  - 使用场景很少：export-file, copy, drag, listener

- 组件与markdown转换的parser、serializer
  - 将递归要执行的部分暴露出去了，非常灵活，但实现复杂，方法的第一个参数用来传递this
# changelog

## [v7.0.0_20230222](https://saul-mirone.github.io/a-brief-introduction-to-milkdown-v7/)

- The editor becomes a first-class headless component.
- Factory plugins are fully replaced by composable plugins.
- Runtime plugin toggling is supported.
- Universal widget plugins.
- Better Vue and React support.
- API documentation is provided.
