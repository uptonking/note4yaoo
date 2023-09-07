---
title: lib-editor-quill-dev
tags: [quill, text-editor]
created: 2023-02-09T18:17:22.759Z
modified: 2023-02-09T18:23:23.288Z
---

# lib-editor-quill-dev

# guide
- features
  - 定义了delta结构表达编辑器的内容和changes

- cons
  - 扁平的结构查询一个节点的子节点不太方便，但也可通过attributes自定义属性来实现

- who is using #Quill
  - vaadin rich-text-editor is built with Quill
    - https://vaadin.com/docs/latest/components/rich-text-editor
# roadmap
- quill很久未更新了，v1.3.7和v2都最后更新在202004

- [The State of Quill and 2.0_201709](https://medium.com/@jhchen/the-state-of-quill-and-2-0-fb38db7a59b9)
  - Historically, major software releases have focused on technical developments and new features. Quill’s 2.0 release, however, will also prioritize supporting activities.
  - With early adopters proving out several uses cases and providing more confidence in Parchment’s API, we can move from making sure our aim is possible towards making them easy for the wider audience.
  - Tables are coming.
  - Quill has been designed with a modular architecture. Themes has also been underdeveloped
  - Adopting New Web Features. One example is using `event.key` to more easily add keyboard shortcuts
# dev
