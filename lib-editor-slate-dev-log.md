---
title: lib-editor-slate-dev-log
tags: [dev-log, slate-editor]
created: 2022-05-15T18:46:55.840Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-dev-log

# guide

- 块级元素前后的光标处理

- table-model
# not-yet

# dev-to
- src
  - createDraft + applyToDraft + finishDraft
  - dirtyPath
# dev-later

# dev-maybe

## model层扁平化

- ❓ 将模型层改为基于扁平key/value + 代表节点关系的map，这样在视图层可以直接getNodeByKey(全表扫面性能比getByPath差)，此时方便实现字段级的crdt，也让持久化层更灵活，无需1:1; 
  - 但旧版slate就是采用key的架构，getByKey底层还是基于getByPath实现
  - key的全量查找没有path快
- v0.50+版本的模型层基于自带节点关系的json，然后在视图层动态添加key，这样op中包含路径关系，方便实现op
- 另一种方案是op.apply时保存会受影响的path+value，这样也可以方便实现字段级crdt
# answers

## noseditor中点击bullet和checkbox list的空白行无法显示光标，数字列表可正常显示光标

- 原因未知，坑能和flex布局相关，zero-width字符的span、div宽度都为0，但数字列表是能正常显示

- 解决方法有2种
- 方法1 通用解法
  - 在零宽字符元素的外层div min-width:1px; 
- 方法2 只针对bullet list
  - 在列表符号后添加空字符''，然后才是列表项内容
# done
- src
  - toSlateRange
  - toDOMRange
# dev-log-2023
- dev-to-collab
  - 🐛 每次刷新页面，空白行会多一行
    - 每次刷新，observeDeep会执行
  - 🐛 yOffset out of bounds
    - 位置：getSlatePath > yOffsetToSlateOffsets
    - 复现方法，在一个浏览器输入，在另一个浏览器全选+删除

- dev-to 提炼核心`需求+产出`工作流，不能在产品中检验的技术不玩
  - headless-comp: sidebar
  - replace forceUpdate with useSyncExternalStore
  - slate-docs-examples
  - dnd-kit preset-tree
    - 参考react-sortable-tree
  - noseditor-docs
  - unit-tests
    - test in firefox
  - drag
    - rewrite dndkit by use-gesture
    - dnd-kit tree performance
      - 自定义冲突解决
      - 拖拽指示线
    - 拖拽到页面顶部或底部时，自动滚动
    - 拖拽时原布局不变，只显示预期位置的指示线
    - [x] 支持向左拖动更新层级
    - [x] 支持方向键向左更新层级
  - toolbar
    - [ ] dropdown 组件样式、active值
    - [x] 工具条按钮处理跨选区的情况
    - [x] 当前 block type 指示与转换
    - [x] 点击按钮时保存选区，逻辑+视觉
    - [x] 高亮当前光标对应的格式按钮
    - [x] 字体大小、颜色
    - [x] 按钮按功能分组
  - image
    - 上传图片时，默认图片原大小
    - upload by drag-drop
    - paste
    - [x] upload by filePicker
  - table to tanstack
    - 删除表格
    - 删除行时，若只有一行，则应该删除表格
    - [x] 隐藏浏览器selection
    - 优化model
    - copy from word
  - list
    - [x] rename todoList to checkboxList
  - scss to linaria
    - list-item
  - callout 高亮块
  - keyboard-shortcuts
  - copy-paste
    - images
  - 去掉依赖
    - plate-serializer
    - zustand
  - emoji
  - embeds
    - video
    - iframe
    - notion
    - apitable
  - formats
    - 清除格式
  - link
    - 粘贴图片url时提示显示为图片
  - 高亮块
  - 格式刷
  - 斜杠菜单
  - resume with noseditor
  - editor-features-playground
    - rewrite lexical for slate
    - with devtools

- dev-later
  - realworld - test
  - 悬浮工具条
  - merge-cells 逻辑优化
  - cell-floating-menu 右上角
  - list
    - 第一个列表项无法向左拖实现提升到父级
      - 列表项A的兄弟项B无法拖到A的位置，即无法替换A，B会自动变成A的子级
    - 列表折叠图标在item内容多行时，会竖直居中
    - 将无序列表项拖进数字列表项时，数字列表项会增加？数字编号或自动变动
    - 数字列表跟在符号列表后时，数字不会从0开始，需要在前面插入一个空行
    - 列表组件设置面板，设置折叠、可拖动
    - 拖拽时，不相关的列表项也会抖动
    - checkboxList完成后可选变灰
    - bulletList支持emoji
  - initialDataLong示例，无法删除首行列表项
  - drag
    - paragraph的drag handle有时无法选中
  - collab
    - ✨ 2个编辑器同一页面协同的示例未完成
    - cursor光标位置经常对不上
  - [x] streaming infinite-list/tree
