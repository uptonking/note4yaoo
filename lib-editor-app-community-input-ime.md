---
title: lib-editor-app-community-input-ime
tags: [community, editor, ime, input-method]
created: 2023-03-05T02:26:47.590Z
modified: 2023-03-05T02:27:52.126Z
---

# lib-editor-app-community-input-ime

# guide

- [Keyboard Event Viewer for contenteditable](https://w3c.github.io/uievents/tools/key-event-viewer-ce.html)

- 浏览器的键盘输入事件顺序
  - [Keyboard Event Viewer](https://w3c.github.io/uievents/tools/key-event-viewer.html)
    - 输入英文字母时 keydown > keypress > beforeinput > input > keyup
    - 输入中文时
      - 👉🏻 keydown > compositionstart > beforeinput > compositionupdate > input > keyup
    - keypress强调输入文本字符，按键ctrl/shift/alt都不会触发此事件
    - 👉🏻 按功能键如ctrl/shift/alt/cap时，只触发keydown/up，不触发beforeinput
  - [Javascript Key Event Tester](https://unixpapa.com/js/testkey.html)
  - [Keyboard Events](https://dvcs.w3.org/hg/d4e/raw-file/tip/key-event-test.html)
  - [JavaScript Key Code Event Tool | Toptal®](https://www.toptal.com/developers/keycode)

- 中文输入法输入单个普通字符事件顺序
  - keydown
  - compositionstart
  - beforeinput
  - compositionupdate
  - input
  - compositionend
  - keyup

- 鼠标事件顺序
  - mousedown -> mouseup -> click
  - 鼠标先点击input，再点击button，触发的事件顺序
    - mousedown ->  onblur(input) -> mouseup -> click
  - 注意
    - ❓ 在mouseup回调中可以拿到selection取位置，但click回调中selection就变为空了

- editor操作相关事件
  - 光标在editor时鼠标点击editor外的元素，会触发编辑器的 blur > focusout
  - 仅chrome实现的EditContext也能拦截keyboard input character

- events-deprecated
  - keypress  >  keydown/beforeinput

- [规范定义的`inputType`类型 Input Events Level 2](https://www.w3.org/TR/input-events-2/)
  - insertText
  - insertReplacementText
  - insertFromPaste
  - 只在v2中: historyUndo, historyRedo
  - [Input Events Level 1](https://rawgit.com/w3c/input-events/v1/index.html#interface-InputEvent-Attributes)

- 虚拟键盘测试难点
  - 移动端输入法种类多
  - 桌面端虚键盘分为系统层面, 浏览器软件层面
    - 操作系统on-screen keyboard依赖系统环境，如wayland、浏览器不支持虚键盘但terminal支持
    - 浏览器扩展里面的虚键盘行为无标准
    - 浏览器的输入法扩展可以覆盖操作系统的输入法，如系统是英文输入法，但浏览器Google Input Tools扩展可以使用中文输入法

- 目前prosemirror对beforeinput使用很少
# discuss
- ##

- ##

- ##

- ##

- ## [Eliminate insertFromComposition, deleteByComposition, and deleteCompositionText by BoCupp-Microsoft_202109](https://github.com/w3c/input-events/pull/122)
  - 还在讨论中，需要关注进度

- This PR eliminates three inputTypes from beforeinput/input events: insertFromComposition, deleteByComposition, and deleteCompositionText.
- The proposed behavior is that beforeinput and input events for `insertCompositionText` occur only after `compositionupdate` events.
- Additionally, a note stating that multiple compositionend events may occur for one compositionstart event was removed.

- 💡 The result is that the composition sequence is:
- A `compositionstart` event
- Multiple occurrences of this sequence:
  - A `compositionupdate` event
  - A beforeinput event with inputType = insertCompositionText
  - An input event with inputType = insertCompositionText
- A `compositionend` event
