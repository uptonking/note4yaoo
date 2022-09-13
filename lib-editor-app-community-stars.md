---
title: lib-editor-app-community-stars
tags: [community, editor]
created: 2022-06-12T22:14:05.479Z
modified: 2022-08-21T10:12:02.964Z
---

# lib-editor-app-community-stars

# guide
- 编辑器研发方向
  - 实时协作
  - 版本控制
  - 离线存储
  - features
    - 开放api
    - 双向链接

- not-yet
  - 搜索编辑器内容时，如何搜索带格式的文本，如关键词为 解构`props` 时如何搜索
  - 将bibtex插入编辑器的逻辑实现有问题，如何只在光标点击editor内容后才执行插入bibtex的command，否则就会出现现在的问题，鼠标若不再editor中点击一下就不执行该逻辑

- 浏览器的键盘输入事件顺序
  - [Keyboard Event Viewer](https://w3c.github.io/uievents/tools/key-event-viewer.html)
    - 输入英文字母时 keydown > keypress > beforeinput > input > keyup
    - 输入中文时 keyup > keydown > beforeinput > input > keyup
      - 输入中文拼音字母时，触发的是keyup，选完词后时keydown
    - keypress强调输入文本字符，按键ctrl/shift/alt都不会触发此事件
    - 👉🏻 按功能键如ctrl/shift/alt/cap时，只触发keydown/up，不触发beforeinput
    - 按tab只触发keydown，无up
  - [Keyboard Event Viewer for contenteditable](https://w3c.github.io/uievents/tools/key-event-viewer-ce.html)
    - 事件顺序与上面一致

- 鼠标事件顺序
  - mousedown -> mouseup -> click
  - 鼠标先点击input，再点击button，触发的事件顺序
    - mousedown ->  onblur(input) -> mouseup -> click
  - 注意
    - ❓ 在mouseup回调中可以拿到selection取位置，但click回调中selection就变为空了

- events-deprecated
  - keypress  >  keydown/beforeinput

- https://github.com/powcoding/etherpad-core  /仅文档和示意图/无代码
  - etherpad产生diff的2种方式
    - 点击菜单栏上的功能按钮
    - 用户在编辑器内不断的输入文字，那么etherpad通过定时检测来获取内容的变化
  - etherpad内嵌了自己的一个编辑器ace editor，不支持接入第三方富文本编辑器
  - 但etherpad具备了完整的实时协作机制，包括：客户端、服务器端的模型设计，多人冲突的设计，对富文本格式的解析，对输入法的支持等。
  - 如果能利用etherpad的实时协作机制，又能接入第三方编辑器，那就是一个完美的方案
  - etherpad产生diff的2种方式中的第1种方式，完全是etherpad自己的私有机制，没法接入第三方编辑器
  - 但是利用第2种方式，不管第三方编辑器如何改变编辑器内容，只要让etherpad定时去检测到变化，就能生成diff，后续流程完全和原生etherpad一致
  - 将etherpad对内置编辑器的绑定解耦，通过设计api暴露出来，可绑定到第三方编辑器上。这样第三方编辑器就具备了和原生etherpad相同的整套实时协作编辑的能力
# discuss
- ## [国内有做类似于Google Docs级别「富文本编辑器」的团队吗？](https://www.zhihu.com/question/397012334)
- 一个叫“一起写”的产品，创始人是 Google docs 出来的，做的就是类似产品，不过好像已经被快手收购了

- ## [对可多人协同编辑的在线编辑器，如何设计其 undo/redo 的逻辑？](https://www.zhihu.com/question/367915946/answer/985845505)

- ## 

- ## 
