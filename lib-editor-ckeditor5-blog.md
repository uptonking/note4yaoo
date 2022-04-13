---
title: lib-editor-ckeditor5-blog
tags: [blog, ckeditor]
created: '2021-10-31T15:56:15.028Z'
modified: '2021-10-31T15:56:24.071Z'
---

# lib-editor-ckeditor5-blog

# 2022

- 工作小结
  - 因为在线api服务无法跨域访问，就在本地跑通了登录、获取workspace列表的逻辑
  - 对接blockdb相关
    - 去掉找不到workspace的404页面，默认workspace为space前缀_userId
    - 用户登录后，默认打开上次访问的文件，逻辑没跑通
    - 刷新页面恢复用户和页面相关数据，需要继续完善
  - PageTree获取blockdb数据源失败了，因为api改变了
    - PageTree的更新方式有2种，会采用哪一种
  - 登录相关细节优化
    - 登录后显示google头像、退出登录
    - 顶部导航条切换白板视图和页面视图已经work
# guide

# ckeditor-faq-repeat
- ckeditor通知更新react组件
  - react组件将自身setState方法注册到eventEmitter，在editingDowncast中更新view时触发执行更新react组件的方法，并传入最新编辑器状态作为参数

- react组件通知更新ckeditor状态
  - 自定义command
# 富文本编辑器ckeditor5源码分析
- ckeditor5/engine封装了model tree的几个概念。
- 主要数据类型，其中Node、NodeList、Element、RootElement、Text、TextProxy和DocumentFragment具有类似的结构

- ckeditor5定义了8个主要的操作（operation）
  - insert, move, rename, attribute, split, merge, no, marker
- 通过model.applyOperation(opt)的方式应用operation，在model和model.documention中通过observablemixin和emittermixin使得其可以将applyOperation转换成事件名，当model调用applyOperation方法时，触发applyOperation事件的回调

- CommandCollection用于管理command，包括新增、查找、迭代（iterator）、执行和销毁。

- 绑定到可观察对象的模板使得用户界面具有动态和交互式特质。一些基本类如Editor、Command可也是可观察对象。
- 如何设置类为observable
- set
- delegate
- bind
  - editor.commands.isEnabled必须使用set方法定义，才能保证bind方法的有效性
- decorate
  - 通过decorate方法，可以将object methods转换为事件驱动性质的方法。
  - 当某个方法被decorate后，那么当方法被执行时，一个同名的事件将会被创建和触发

- EmitterMixin 主要负责事件绑定、触发和代理用。
  - 主要方法有listenTo/stopListening、fire和delegate/stopDelegating。

- extend( ObservableMixin, EmitterMixin )
  - extend的作用就是将EmitterMixin关于事件触发、监听和代理等方法引入有到ObservableMixin中

- ckeditor5的locale方案会往全局变量`window. CKEDITOR_TRANSLATIONS`上挂载映射用的字典信息
