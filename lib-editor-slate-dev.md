---
title: lib-editor-slate-dev
tags: [lib, slate-editor, text-editor]
created: 2022-05-15T18:41:00.527Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-dev

> A completely customizable framework for building rich text editors.

# guide
- features
  - First-class plugins
  - Schema-less core
  - Nested document model
  - Parallel to the DOM
  - Intuitive commands
  - Collaboration-ready data model
  - Clear "core" boundaries

- pros
  - easy to start

- cons
  - 未提供comment示例

- who is using #slate
  - worktile slate-angular
  - wangEditor

- slate-resources
  - https://docs.slatejs.org/
  - https://www.slatejs.org/examples/richtext
# dev-slate-not-yet
- 业务事件的处理时机选择 onKeyDown、onDOMBeforeInput、onChange
  - 文本格式快捷键
  - 软换行
  - 选区快捷键
  - 复制粘贴
  - markdown解析与转换
  - 根据外部数据源更新编辑器内容数据
  - 恢复focus
# dev-slate
- event-order
  - 改变点击光标的位置 onChange
  - 键盘在编辑器内输入文字 onKeyDown > beforeinput > onChange
  - 通过快捷键改变编辑器内文字样式 onKeyDown x2  > onChange

- 浏览器的键盘输入事件顺序
  - [Keyboard Event Viewer](https://w3c.github.io/uievents/tools/key-event-viewer.html)
    - 输入英文字母时 keydown > keypress > beforeinput > input > keyup
    - 输入中文时 keyup > keydown > beforeinput > input > keyup
      - 输入中文拼音字母时，触发的是keyup，选完词后时keydown
