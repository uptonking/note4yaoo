---
title: dev-log-faq-engineering
tags: [dev, engineering, faq]
created: 2021-01-21T13:16:03.667Z
modified: 2021-03-29T19:17:06.810Z
---

# dev-log-faq-engineering

> 开发、测试  >  维护、重构  >  更新、升级

- tips
  - 参考主流api设计，如dom api
# not-yet
- 海量小文件如何存储、更新
- 海量图片如何存储、更新

- 如何遍历文件夹下上亿文件而不栈溢出
  - 考虑层序遍历   
  - https://www.cnblogs.com/intsmaze/p/6031894.html

# 

# infinite-scroll的实现要点

> 也是常见业务组合的场景

- 是否实现virtualized render: 
  - 参考tanstack-virtual
- ally: 键盘导航
  - 参考ariakit、radix-ui
- 拖拽改变顺序: 
  - 参考dnd-kit
- async-data、网络请求
  - 参考tanstack-table
# 类似slate，将各种change函数放在全局map的设计
- pros
  - 存取方便

- cons
  - 不支持动态更新，或者动态更新后触发通知实现不方便
  - 不方便实现多实例
# 前端组件的渲染架构设计 - props
- 大多数组件都是 dom-container + data/source + view/templates/vdom + options，包括react
  - where/what/how to render
# [程序员们有什么好的编程习惯？](https://www.zhihu.com/question/440136872)
- 习惯去看源代码，网上的攻略再好，也是二手资源
- 不要重复造轮子，要相信前人的智慧和尊重大家的鉴别能力

- 注释里尽量写为什么，而不是做了什么。
  - 做了什么，看代码就好，代码不会骗人
  - 但为什么要写成这样，有时候就非常让人困惑。
  - 有可能是处理某个 corner case，有可能是绕过某个系统限制，也可能是什么奇葩需求，这种代码，没有当时的 context，过几个月看，不知道是想干什么
  - 再有年轻力壮的，看不顺眼来优化一下，以后就不知道哪个地方会崩了
  - 注释也需要维护，代码更新了，注释也要更新

- tips
  1. 代码重构得趁早
  2. 不要注释掉无用代码，直接删掉
  3. 切勿用拼音来命名变量
  4. 代码写好同时也要规范注释
  5. 函数里的代码保持同样的抽象层级，可以提取公共函数或工具函数
