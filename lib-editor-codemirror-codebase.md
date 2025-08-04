---
title: lib-editor-codemirror-codebase
tags: [code-editor, codebase, codemirror]
created: 2024-05-02T06:41:04.049Z
modified: 2024-05-02T06:41:19.983Z
---

# lib-editor-codemirror-codebase

# guide
- codemirror的架构主要分3方面: model/state, view, extension
  - extension的扩展方式也是这3方面，state-field, deco, view-dom/event

- editor业务的数据更新
  - 修改编辑器内容
  - 修改其他状态
# dev-debug
- 编辑器最外层contenteditable的dom在调试时可以store as global variable，在属性上可拿到 cmView, 可以进一步拿到 cmView.view/ cmView.view.state

## dev-codemod-update

- 更新fork代码的基本步骤
  1. 备份fork处旧代码，备份在平行目录更方便
  2. 全量复制最新代码到fork仓库, replace部分文件(可替换或减少第三方依赖/数据)
  3. lint + format, 格式化方便后面看修改的diff。 eslint里一些特殊的规则需要在更新/patch代码后设为error，但lint大部分完后设为warn, 如prefer-const有时会修改源码结构，所以保留一部分lint error不处理
  4. codemod，基于jscodeshift; 一般是添加或移除class field modifier，如declare/private, 设置初始值; 可利用流程先移除所有再添加部分来实现移除部分
  5. tests

- 需要更新的主要文件·
  - state SectionIter.len/offset/ins 去掉declare
  - state Facet.tag, FacetProvider.extension, PrecExtension.extension CompartmentInstance.extension 去掉declare
  - state RangeValue.startSide/endSide/mapMode/point LayerCursor/HeapCursor.from/to 去掉declare
  - state Text/RawTextCursor/PartialTextCursor.[Symbol.iterator]   去掉declare
  - state Annotation._isAnnotation 去掉declare
  - view ContentView.breakAfter 去掉declare
  - view Decoration.point 去掉declare  MarkDecoration 添加 point = false; LineDecoration 添加 point = true; mapMode = MapMode. TrackBefore; PointDecoration 添加 point = true
  - view DocView.children/split 去掉declare
  - view EditorView.inputState/styleModules 去掉declare
  - view GutterMarker.elementClass 去掉declare
  - view HeightMap.size 将declare改为size=1, HeightMapBranch.size 前面加上declare
  - view WidgetView/WidgetBufferView.children 将declare改为= noChildren
  - view ViewState.viewportLines/viewport/viewports 去掉declare
  - view placeholder.update 去掉declare
  - view tooltipPlugin.container 去掉declare
  - diff Frontier.len/start/end 去掉declare
# not-yet

# dev-xp

- document是否总以换行符结尾
  - 并不是，文档内容可为空字符串
# overview

# architecture

- codemirror的整体架构和extension的架构都是从model/view/update三方面考虑的
  - 在mvu架构的基础上通过provide暴露api
# extensions/plugins

# state

# view

## widget

- 通过eq和updateDOM多层拦截判断来减少重绘
- `toDOM`
  - 具体实现可以调用this.updateDOM()，也可以不调用
- `updateDOM`
  - if return true, the original dom is kept and updated
  - if return false, the original dom is destroyed and recreated
- `eq` is used in merge widgets/decorations
# styling
- 编辑器获取到焦点时 .cm-editor 的dom元素会增加样式类 .cm-focused

- 语法高亮通过 defaultHighlightStyle 定义了默认值, 可通过自定义theme覆盖任意值
# more
