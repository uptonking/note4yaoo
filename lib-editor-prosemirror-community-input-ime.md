---
title: lib-editor-prosemirror-community-input-ime
tags: [community, ime, input-method, prosemirror]
created: 2022-09-17T09:30:19.022Z
modified: 2022-09-17T09:31:16.310Z
---

# lib-editor-prosemirror-community-input-ime

# guide

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

- ## I noticed that the native undo / redo input events historyUndo / historyRedo events do not work as expected in ProseMirror._201903
- https://discuss.prosemirror.net/t/native-undo-history/1823
- the problem is that browser makers have a very different view of how undo/redo work than how the web works. 
- In the browsers’ view, there should just be one undo/redo stack for everything on the same webpage. So say you have two different textareas on the same page, or some form elements and an editor, the browsers believe that they should all share the same undo stack. 
- In the case of Safari, they go a step further in that for them it’s a “platform behavior” that has to be preserved so that web apps work the same as native apps.
  - There is a little bit of hope right now though in that Safari has been experimenting with an API that will allow JavaScript to add items to the global undo stack programmatically 
