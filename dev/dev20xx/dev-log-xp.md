---
title: dev-log-xp
tags: [dev-log, dev-xp]
created: 2022-05-24T17:57:37.897Z
modified: 2022-05-24T17:57:49.545Z
---

# dev-log-xp

# dev-xp

# dev-summary
- company-unskilled
  - 确认下一步工作计划
  - ~~markdown-editor for vscode~~

- 工作开发问题
  - 原因定位
  - 解决方法
  - 其他方案
  - 提出问题之后，有什么更好的方案、行业内更专业的方案

- dev-summary
  - 使用最多的组件
    - icon
    - button
    - input/TextField
    - list
      - 支持不同行类型的list
      - 支持键盘上下导航: react-accessible-menu
    - dnd-kit
    - modal/popover/tooltip/dropdown
    - collapse
  - 日历热力图 react-activity-calendar
    - 中文本地化
    - 始终显示70+N天
    - to-do
      - tooltip传入组件
  - 文件列表 react-table
    - 悬浮工具条
    - to-do
      - sticky header
  - 看板工具 personal-kanban
    - 参考github最新的看板设计和实现，github项目在twitter中预览的卡片
  - 多维表格
  - 多种类型数据的转换和渲染
    - 多种类型的单元格，渲染成不同的组件
    - 多种类型的bibtex，使用对应的转换器，渲染成不同样式的
  - 文本以打字动画的形式动态展示 typed.js
    - 书写动画、回退动画
    - to-do
      - 实现多行文本依次展示
  - css模式
    - hover-show-otherwise-hidden
  - react开发模式
    - enum vs switch-case
    - 折叠列表时，如何添加事件监听器的能减少rerender

- dev-xp
  - 文档数据库的add/update/delete监听只是简单的发布订阅模式，开发了4个月居然没看出来
    - 每次操作数据库后手动调用fetch，不如 `emit('updateDocMetadata')` 事件
  - 不要执着于在旧版代码中找实现参考，有时会浪费过多时间
    - 新的api也许自身就提供了实现
  - 一段代码排查很久没找到原因，可能是复制粘贴代码时忘了重做修改细节
    - 如粘贴后false未修改为true
  - 时间精力有限，对于非核心问题，有时不必执着于实现细节，不一定需要完全搞清楚来龙去脉
    - 分析出核心问题，将精力全部花在重点之上
    - 有时修改bug只需要注释掉部分代码而已，没必要去看这些代码的实现流程
  - 不一定要执着于自己实现组件
    - 自己实现的右键菜单样式简陋、功能不全，如hover时显示浅色背景
  - 开发环境必须以linux为主，在windows vscode中以WSL Remote打开linux下的源码
    - 有些bug只在windows中才会出现，同事也难以分析排查
  - 连续fix问题的时候，一定要fix完一个做一个集成测试，确保未对现有功能产生影响
    - 否则fix完现有问题，却发现新的问题，但问题却很难排查了
  - 将组件中操作blockDB的逻辑分离到service层
    - 降低前端业务开发对后端的依赖
      - 分离dbBlock和editorBlock，两者没有直接关系，但可以转换得到
    - 在service层提供observe这类自动更新的方法，不需要在前端各个组件中连接websocket

- 让b/s架构项目支持纯前端使用的思路
  - 前端使用完整数据库idb，在前端重写所有get/post操作为idb操作，将后端数据模型复制到前端
  - mock get/post 的计算和返回，
  - 考虑成本，对于复杂计算迁移成本太高

- vanillajs框架集成react组件的问题
  - 通过createPortal，可以拿到主应用中的state、theme、event
  - 通过ReactDOM.render，渲染的ui在单独react上下文，不能直接拿到theme

- 🤔 ckeditor编辑器刷新后，图片无法显示的问题；不同时刻触发save方法，如何确保新数据覆盖旧数据
  - 问题排查定位，旧数据覆盖了新数据
    - 不是防抖节流的问题，~~为了性能，将保存数据的函数防抖了，结果新数据被旧数据覆盖掉了~~
    - 不是替换图片blobUrl的问题，一是save异步保存逻辑之后的位置打印出数据库内容就缺失了，二是注释掉保存逻辑取出数据库内容依然缺失
    - 不是数据库保存数据丢失属性的问题，不是数据库同步的问题
    - 编辑器组件保存全量数据的save()方法是async异步的
      - 👉 通过在save方法内部不同位置打t1/t2/t3的log，发现问题处在 
      - 上传图片时，会将图片数据异步保存在本地数据库，此过程是异步，上传时编辑器图片部分数据为 `<figure class="image"><img></figure>` 非完全版，此时可能会触发异步save()方法
      - 若同时有其他异步操作更快地执行完了，也触发了数据保存
      - 那么其他操作触发的save()方法更早执行完，结果等上传图片完触发的save(旧的content)会覆盖掉新数据
  - 解决方案参考1
    - 每次save并不是真正的去保存到数据库的异步方法，将save方法改为简单的将数据保存到数组
    - 通过闭包，保证节流时保存的是最新的数据，而不是旧数据
    - 在useEffect里面异步保存数据时，定义标记变量，if (content && !saving) {，若正在保存数据，则不再执行保存
  - 总结/难以解决问题的原因
    - ⚡ 解决问题核心思路：用闭包确保执行异步方法的数据是有效的，类似setTimeout的延迟打印
      - 搜索资料时，一定要参考关键词 useEffect autosave或其他编辑器的实现
    - 不用数据而用boolean变量来操作ckeditor的model修改图片blob url是错误的实现思路
    - 还包括编辑器editor对象的创建销毁由ckeditor控制，而不由应用层控制
    - 睡一觉，第2天就会发现问题了，在前一天的错误上，多一次focus-blur触发保存，内容就正常了

- almanac体验-feat-版本控制
  - 亮点：创建分支 + 合并修改
  - merge分支文档到主文档时，头部图片不会自动迁移，需要手动修改
  - 分支文档被合并到主文档后，分支文档的状态会改变为locked只读，不能再次编辑
    - 已被合并过的分支文档，只有被再次复制创建副本，才能修改
  - 版本控制cons
    - 没有显示分支的时间先后关系，只显示了已合并未合并
      - 类似github insights里面不同fork的顺序
# ai-coding
- 集成sdk时，数据流和转换逻辑可能很复杂，
  - 一种方案是不让ai直接写业务代码，而是让ai写最普通的文本转换逻辑，然后一步步调试修改为业务代码的结构
# pain-dev
- 块编辑器开始支持跨区选择，后面禁用此功能改为只支持单行选择的原因
  - 跨区选择时，会将各子块的contenteditable改为false，此时选中的内容无法响应键盘事件
