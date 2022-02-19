---
title: lib-editor-ckeditor5-dev-log
tags: [ckeditor, dev-log]
created: '2021-10-27T03:20:11.947Z'
modified: '2021-10-27T03:20:45.841Z'
---

# lib-editor-ckeditor5-dev-log

# working

- company-unskilled
  - 确认下一步工作计划

- **markdown-editor for vscode**

- 工作开发问题
  - 原因定位
  - 解决方法
  - 其他方案
  - 提出问题之后，有什么更好的方案、行业内更专业的方案

- dev-xp
  - 不要执着于在旧版代码中找实现参考，有时会浪费过多时间，新的api也许自身就提供了实现
  - 一段代码排查很久没找到原因，可能是复制粘贴代码时忘了修改细节，如粘贴后false未修改为true
  - 时间精力有限，对于非核心问题，有时不必执着于实现细节，不一定需要完全搞清楚来龙去脉
    - 分析出核心问题，将精力全部花在重点之上
    - 有时修改bug只需要注释掉部分代码而已，没必要去看这些代码的实现流程
  - 不一定要执着于自己实现组件
    - 自己实现的邮件菜单样式简陋
    - 功能不全，如hover时显示浅色背景
  - 开发环境必须以linux为主，在windows vscode中打开linux下的源码
    - 有些bug只在windows中才会出现，同事也难以分析排查

- dev-summary
  - 使用最多的组件
    - icon
    - button
    - input/TextField
    - list
    - dialog/modal/popover
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
  - 文本以打字动画的形式动态展示 typed.js
    - 书写动画、回退动画
    - to-do
      - 实现多行文本依次展示
  - css模式
    - hover-show-otherwise-hidden
  - react开发模式
    - enum vs switch-case

- almanac体验-pros
- almanac体验-cons
- almanac体验-feat-版本控制
  - 亮点：创建分支 + 合并修改
  - merge分支文档到主文档时，头部图片不会自动迁移，需要手动修改
  - 分支文档被合并到主文档后，分支文档的状态会改变为locked只读，不能再次编辑
    - 已被合并过的分支文档，只有被再次复制创建副本，才能修改
  - 版本控制cons
    - 没有显示分支的时间先后关系，只显示了已合并未合并
      - 类似github insights里面不同fork的顺序

- material-ui缺点
  - ~~没有dropdown，select默认会遮挡触发元素~~

## not-yet

- to-do
  - workspace 文档列表
    - sticky header
    - 删除文档后，只在列表删除了，文档数据库中仍然存在
  - 全局路由守卫的时机错误
    - ~~**应该在路由跳转前重定向，而不是在路由跳转后再次跳转**~~
      - 在跳转前显示loading可以解决此问题
    - 登录后无法访问登录页，需要实现退出登录的逻辑

- 任务看板
  - features
    - 切换 列表视图、看板视图、时间线(甘特图)视图
    - 从看板创建文档
    - checkbox
- 看板 to-do
  - [x] 负责人列表不能多选
  - [ ] 截止日期不能清除
  - 看板、表格的数据考虑全局，暴露出去给其他组件访问

- 刷新页面，登陆会失效的问题
  - 实现退出登录
  - 登录时，不支持未注册用户直接通过验证码登录

- workspace如何设计
  - 本地仓库、云端仓库
  - 我的仓库、公共仓库
  - 是否可参考github仓库？

- affine文档核心功能
  - 双链展示
  - 分支文档
  - 工作空间内搜索

- affine的ux交互设计
  - 落地页/未登录时的宣传页
  - 个人主页/首页
  - 工作空间页
  - 国内环境不适合对接github，可考虑百度网盘

- affine新首页设计与工作计划
  - [x] 首页使用~~类似workspace的设计~~，快捷菜单跳转到workspace
  - [x] 布局改为左侧边栏
  - [x] 文档列表只显示创建的文件，最近操作的文档要跳转到单独页面
  - [ ] 文档列表：pin置顶一个日期

- 编辑器工作计划
  - ~~左侧目录显示参考文献锚点~~
  - ~~编辑器首页顶部显示图片~~

- 折叠列表时，如何添加事件监听器的能减少rerender

- 日期时间的处理
  - 可参考日历组件的实现方案

- 流程图bug
  - ~~复制粘贴后，就变成图片，无法编辑代码了~~

- 检查图片的接入方式
  - toolbar打开文件选择器
  - 拖拽本地图片到编辑器光标位置
  - ctrl+v粘贴图片到编辑器

- 图片上传的问题
  - ~~将 同步执行的createObjectURL 改为 异步执行的` FileReader.readAsArrayBuffer` + `new Blob([arrayBuffer], { type: "mime/type" })`~~
  - 上传已经以前已经上传过的图片时，是否保存了2份数据，存在冗余
  - 首次渲染图片时，由于blobUrl失效了，控制台会报错
    - blob:http://127.0.0.1:4001/223c5400-55e2-4ac7-b936-574b47cd0201 net::ERR_FILE_NOT_FOUND
  - 考虑直接将数据库中docId存储到

- 如何在自定义插件中使用官方image-plugin的功能和UI
  - 类似插入buttonView一样插入imageView
  - 需要继承官方plugin暴露的各个class，然后添加自定义逻辑，再glue一个新的入口类

- 是否需要更新图片标题的显示逻辑
  - 若不存在，则默认不显示；选中图片时，可输入标题
  - 若存在，则始终显示；选中图片时，可输入修改标题
  - 图片下方标题默认居中对齐

- 要不要实现自定义image-plugin
  - 双击图片时，会在蒙版层中放大图片，全屏显示图片
  - 图片裁剪图标
  - 系统操作菜单，如收藏、下载、删除当前图片
  - 替换当前图片
  - 自定义图片标题的显示和更新逻辑
  - 如何插入inline图片，插入图片后，先缩小，再拖放到一行内

- 图片工具条的设计
  - notion 鼠标悬浮时自动显示工具条
    - 图片处于选中状态时，图片和caption上方会出现蓝色蒙版
    - 工具条在图片之内
  - 飞书 鼠标悬浮时图片会显示蓝色边框，图片上方会显示工具条
    - 图片处于选中状态时，蓝色边框会变成深蓝色，此时鼠标悬浮到其他图片上方时不会显示工具条只是边框变蓝
    - 工具条在图片外，且无三角形指示位置关系
  - ckeditor 鼠标悬浮时会显示边框
    - 图片处于选中状态时，会显示工具条
    - 工具条在图片外，且有三角形指示位置关系

- boxEditing, boxUI 的ui部分为什么总是toolbar界面相关的内容
  - 插入元素的位置，通常放在command

- later
  - 就算postcss-loader/style-loader版本与官方文档一致，也可能会出现demo样式异常的问题
  - 测试连续调用自定义hook时useRef的current的值的变化
# 多维表格和看板-pending
- 工作记录在20211220之前

- TODO
  - [x] 点击任务卡片时，应该出现弹窗
  - [x] checklist/子任务
  - [x] 创建文档
  - [x] 添加日程：开始时间、结束时间
  - [x] @负责人成员或用户
  - [x] 看板卡片右上角的删除、更多图标应该悬浮时才出现
  - [x] 鼠标在卡片上方时，形状应该是pointer，而不是拖拽的grab
  - [ ] 卡片弹窗应该自动保存内容，而不是显示保存和放弃修改按钮
  - 卡片上文档列表展开时，底部头像会被快速挤到卡片之外，然后快速还原
  - 卡片上需要动作菜单列表，对话框需要弹出搜索列表、选择列表、日期面板
  - 子任务暂时不能修改，只能先删除再添加，需要一个列表
  - 将卡片拖动到最右边`添加分组`的空列时，应该支持自动新建卡片
  - 标签、子任务添加按钮出现时，旁边应该还有取消按钮
  - 对于看板上的日程，近期日程除了日期数字外，还可以显示类似下周日这样的文本
  - 看板任务与编辑器打通
    - 全局task检索和展示
    - 打通 看板任务、文档侧边栏的任务
    - 在文档中的不能修改checkbox，打开弹窗才能修改
    - 子任务转换成任务卡片
  - 看板设计其他参考
    - 看板必填项
    - 企业倾向于自动发邮件
      - 倾向于低代码完成自动化流程

- 多维表格实现计划
  - [x] 工具条 + 表格
  - [x] 切换普通表格视图、分组表格视图
  - [ ] 分组表格的测试数据修改为trello格式，也会作为看板数据源
  - [x] 切换表格视图、看板视图
    - 如果要做得像notion，不妨做得更像一点，样式改成适合编辑器的卡片和看板样式
  - [x] 实现表格视图下特殊字段的显示，如子任务、参考文档、标签
  - [ ] 全局菜单 字段配置
  - [ ] 表格拖拽改变列宽度
  - 表格顶部的工具条和标题栏都应该支持sticky到页面顶部
  - 表格数据导出
  - 编辑一行、单元格
  - 子任务转换成任务卡片，任务卡片转换成子任务
  - 样式调整
    - 表格整体左边框和上边框缺失
  - 去掉依赖
  - 复制表格自身到下方的动画
- 多维表格计划待定
  - 支持添加任意自定义字段
  - 支持设置字段类型，内置常用数据类型
  - 过滤筛选支持组合条件，如多个条件求交集
  - 更多搜索方式，如日期范围
  - 可设置显示 表格左边和上边的索引列、索引行

- 多维表格实现问题
  - 🤔️ 多个视图来回切换时，如何保存每个视图的状态
    - 表格的每个ui状态都可以由tableOptions确定
  - 要不要区分普通表格和分组表格
    - 分组表格不适合 合并单元格
- 多维表格实现说明
  - 分组
    - 暂时只支持离散变量，不支持连续型数值
    - 破坏了useExpandAll的sticky header
  - 竞品参考
    - 飞书和notion的多为表格都是现在在编辑器页面中，未考虑分页的情况

- 🤔️ 看板组件和表格组件切换视图的状态设计问题
  - 除非要明确使用缓存，否则每个视图的数据都应该动态计算出来，这样能减少内存消耗和及时同步更新
    - 在顶层定义更新一行数据的方法，传下去
    - 每个视图层可以进一步封装顶层数据更新方法，然后更新自己的ui时更新顶层数据和配置
  - 工具栏的状态应该放在每个视图层，工具栏的dom可以放在顶层
    - 每个视图可显示不同的过滤条件
  - ✅️ 都存在自己的内部状态，将顶层存储数据和更新方法都传到2个组件
    - 数据更新方法被调用后，所有视图被刷新
  - ❌️ 以表格内部状态作为基础，将表格组件的数据和更新方法传到看板组件
    - 表格更新时，数据源更新，看板会更新；看板更新时，表格也会更新
    - 如果只创建看板视图，那没必要定义表格数据的更新方法
  - 如果增加其他视图，比如甘特图呢？
    - 定义一份配置数据，传下去作为初始state

- 表格 not-yet
  - 表格末尾为什么会渲染一个英文分号
# 2022
- 下一步工作内容
  - 开发规范
    - 总结 react patterns
    - 总结 typescript patterns
  - readonly-list-grid
    - plain
      - no sort/filter/group
      - no reorder
      - no column width resize
      - custom cell renderer
    - searchable
    - virtualizable
  - crud-list-grid
    - checkbox
    - draggable/reorder list
    - fields menu - filter/groupable
    - inline editing
    - orm integration
  - sortable-filterable-groupable table
  - 重构文章页题头部分组件

- to-be-discussed
  - 初步实现的菜单项都是英文，产品化时应该用中文
    - [ ] 文章页可拖拽改变侧边栏宽度

- 重构题头部分
  - [x] 更换emoji picker
  - 字段列表分类型重构

- bugs真的多，修的我很烦躁
  - 编辑器
    - blockquote插件中的换行，每次刷新页面后，中间的空行会加一个
      - 空文档无此问题，复制示范文档会出现此问题
    - 图片按回车不能换行
    - 编辑器工具条第一个查找替换图标是烂图标，左上部分都是黑色
  - 文章页
    - [x] 去掉水平滚动条
    - [x] 应该使用CustomScrollbar，最好去掉浏览器默认的竖直滚动条
  - 文章左侧标题目录toc
    - [x] 点击无法跳转
    - [x] 收起折叠按钮会被文章中的图片挡住
  - 侧边栏部分
    - 已注册的用户是不可删除的，是否应该不显示删除按钮
    - 参考文献
      - 连续按两次插入bibtex后，会出现2个编辑器
      - [x] 有时点击插入bibtex的图标会无反应
        - 首次添加bibtex时，新添加的bibtex entry会带有onClick点击事件
  - hard
    - 粘贴第三方文章如知乎专栏复制的文章时，侧边栏和导航栏字体会缩小到无法辨认
      - 光标移动到待创建双链的文字的位置时，文字会突然缩小

- 测试文献部分
  - 刷新页面后，侧边面板的bibtex未显示，原因是用了全局store中的doc对象

## 0219

- 高亮块功能设计

- 高亮块api设计

- 高亮块ui交互设计

## 0217

- 列表项上显示悬浮卡片是不是一种优雅的交互体验？
  - 可采用类似wolai的单独的侧边悬浮卡片

- 为什么编辑器中插入的bibtex文献，点击后跳转的url显示的id变了
  - 原因是默认创建的文档类型是 binary，而不是 article
  - (await editor.db.get('d65338ed-8651-4dc8-91e2-60649e5711db')).type
  - 等待以后修复双链的链接文档

## 0216

- 样式picker almanac侧边栏
  - 主文字 #2E4155，灰色文字 #757C8A
  - font-family: "Microsoft YaHei"

- magic-css-heading-title
  - 为什么文末参考文献 h1-References 的高度为71
    - margin-block-start/end 的效果就是 margin-top/bottom

- 登录后，没有从 /docs 跳转到 /docs/docId 的原因是
  - 后端获取workspace的请求失败了
  - url前面多了一个空格，见npm run dev后webpack-dev-server的异常信息

```bibtex
@misc{piece, author={J Strother Moore}, title={``{M}y'' Best Ideas.\\ \url{https://www.cs.utexas.edu/users/moore/best-ideas/structure-sharing/text-editing.html}}}

@article{myers1986ano,
    title={An {O(ND)} difference algorithm and its variations},
    author={Myers, Eugene W},
    journal={Algorithmica},
    volume={1},
    number={1-4},
    pages={251--266},
    year={1986},
    publisher={Springer}
}

```

- 文字省略号的一种实现方式

```CSS
.text-ellipsis {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  max-width: 60%;
}
```

## 0215

- 编辑器设置选项分类
  - 编辑器样式
    - 字体、大小、宽度
    - toc目录样式
    - 折叠图片、列表
  - 编辑器功能特性
    - fork/创建副本、分支
    - 历史版本
    - 拼写检查
    - 离线
    - 图片编辑器
    - 查找替换
    - 文档信息统计
  - 导入、导出
    - 导出/下载
  - 分享、权限
    - 只读、可编辑
    - 分享链接、二维码、微信
    - 分享管理
  - 产品功能特性
    - 收藏
    - 分享
    - 删除
    - 保存为模板
    - 回收站
    - 集成到slack
    - 文档更新提醒
    - 关闭评论
    - 翻译
    - 举报

## 0213

- 让dom中id为`#id001`的元素滚动到页面顶端的方法 (如toc点击跳转)
  - `$('#fixed-tabs').scrollIntoView({ block: 'start', behavior: 'smooth' })`

## 0211

- bug修复
  - [ ] 修改store中的doc对象为docId
    - 等到闫东先实现请求文章id再实现此工作
  - 修改编辑器中代码字体 monospace  ->  'Courier New', monospace
  - 讨论
    - 要不要做退出登录
    - 要不要暂停修复编辑器bugs，开始实现分享功能

- react-router
  - 应该将PublicRoutes和PrivateRoutes分开，这样在public路由页面就不会发出用户数据请求

```JS
(await (await editor.db.getNamedDocument('global')).getDecodedContent()).getMap('recent-docs').get('lastDocument')
await (await editor.db.getNamedDocument('global')).getDecodedContent()
temp1.getMap('recent-docs').get('lastDocument')
temp1.getMap('recent-docs')
temp1.getMap('recent-docs').get('d')
temp1.getMap('recent-docs').set('d', 'idddd')
temp3.set('d', 'idddd')
temp3.get('d')
```

## 0210

- [First item from a Map on JavaScript ES2015](https://stackoverflow.com/questions/32373301)
  - console.log(m.entries().next().value); 

- 早期在 useUser(){} hook声明中放useEffect请求数据的缺陷
  - react创建虚拟dom树时，所有执行了useUser() 的组件都会触发http请求
  - 解决方案1: 拆分成2个hook
    - 抽象出一个单独的 useInitUser(){} hook，只执行请求初始化操作；
      - 在顶层组件(通常是Router组件)中获取到user对象后才渲染其他组件
      - 其他组件直接从useUser()中取user对象，而useUser中没有请求操作

- 测试添加bibtex的示例

```js
await editor.db.setReference({
  entry: 'article',
  author: 'Grishchenko, Victor',
  year: '2010',
  title: 'Deep hypertext with embedded revision control',
  journal: 'proceedings of the 6th International Symposium on Open Collaboration',
});

await editor.db.search({ tag: 'type:reference' });
```

- bug修复
  - [x] 移除文章页水平滚动条
  - [x] 去掉container 100vw 100vh
  - [x] 修复添加bibtex后刷新页面却显示为空的问题

- [Microsoft 提供的等宽 TrueType 字体](https://support.microsoft.com/zh-cn/topic/microsoft-%E6%8F%90%E4%BE%9B%E7%9A%84%E7%AD%89%E5%AE%BD-truetype-%E5%AD%97%E4%BD%93-93aa7a47-2149-be09-31a9-c22df598c952)
  - Microsoft 隨附的唯一 monospaced TrueType 字型是「宋體」（隨附于 Windows 3.1）和黑體（包含在 TrueType 字型套件中）。 Windows 3.1 隨附的所有其他 TrueType 字型，以及 TrueType 字型套件都是成比例字型。
  - Microsoft 附带的唯一等宽 TrueType 字体是 Microsoft 3.1 附带的 "宋体" 和 "宋体"，它包含在 TrueType 字体包中。 Windows 3.1 和 TrueType 字体包中包含的所有其他 TrueType 字体都是成比例字体。
  - The only monospaced TrueType fonts shipped by Microsoft are Courier New, which shipped with Windows 3.1, and Lucida Sans Typewriter, which was included in the TrueType Font Pack. All other TrueType fonts included with Windows 3.1 and the TrueType Font Pack are proportional fonts.

## 0209

- 设置调试逻辑
  - localstorage.debug = 'DocumentDB:*'

- [React.js with Factory Pattern ? Building Complex UI With Ease](https://dev.to/shadid12/react-js-with-factory-pattern-building-complex-ui-with-ease-1ojf)
  - 示例用的switch-case获取指定类型的组件，这些组件被memo过

- [React Hooks Factories](https://dev.to/pietmichal/react-hooks-factories-48bi)

```JS
// Alternatively, without classes

function getUser(name: string): User {
  return { name }
}

const user = getUser("Bob") // { name: "Bob" }

// Factory function that returns a new function that uses Hooks API.
function createHook(initialValue: string) {
  return function useHook() {
    return React.useState(initialValue)
  }
}
```

- [Conditionally render react components in cleaner way](https://dev.to/ms_yogii/conditionally-render-react-components-in-cleaner-way-1ik5)
  - 提出了enum 和 switch-case 2种方法并争论
  - enum-pros
    - 简单直观，直接从预定义对象中取组件
    - {roleSettings(username)[userRole]} 所有子组件都有username参数
    - {createElement(RoleSettings[userRole], { username })}
  - enum-cons
    - 对每个组件不方便传入定制参数
    - A downside of enum solution is all the component will be compiled even it doesn't need to rendered，但可解决
  - switch-case-pros
    - 选择组件自身也是一个组件，all in react
    - memo后方便优化性能
    - 扩展case方便
  - switch-case-cons
    - The long term cost of the switch/case in this scenario is higher. 
      - When you're wrapping different components inside a single component (which is the case for this component), is better to share props across them because they will be used in the same places, so ideally they should receive the same props
  - 不要直接写组件，可以先定义一个组件变量

## 0208

- react实现conditional rendering的3种模式
  - [Which is the react way of complex conditional rendering?](https://stackoverflow.com/questions/50901604)
  - 👍 `{ this.state.err ? <Err /> : <Main /> }` 数据驱动视图
  - 👎 `<div className="App"> {this.state.comp} </div>` state中不要存comp
    - `<div className="App"> {comp} </div>` 将comp提取成变量更好

## 0207

- 编辑器刷新时非常卡
  - 需要清理storage
  - 不能稳定复现

## 0126

- 下一步的工作计划
  - 重构文章页题头列表组件
  - 重构文章页的复杂组件

## 0125

- 🤔 通过双链创建新文档时，为什么在代码中可以打印出 `newDoc.getMetadata('metadata')` 的属性键值对，但在控制台打印出来却为空
  - 确定了问题出在文档数据库层
  - 原因是在执行 dbClient.set(newDoc) 后，其他地方触发执行了 dbClient.set(oldDoc)，很难排查

- 文档页工作需求
  - [x] 从本地数据库中读取文章参考文献列表
  - [x] fix types
  - [ ] 实现更多的参考文献样式 bibtex styles

- 检查parser是否具有isValid的方法

- 补充ts类型

## 0124

- latex的参考文献处理要考虑文中引用和文末条目
  - 文末条目默认是所有作者全部列出，且不使用作者缩写

- bibtex style的难点
  - 多个作者的分隔符可能是逗号，也可能不是逗号，and是人名还是分隔符

## 0121

- [ ] 封装bibtex的转换方法，默认转换方风格为plain

## 0120

- https://github.com/enric1994/bibtexonline
  - Convert your BibTeX bibliographies into text on the fly
  - 但字体用的是无衬线体，十分圆润

- https://github.com/bertobox/CSS-for-APA-Style-references

- [Citation Style Language vs. biblatex (vs. possibly other "citing-systems"?)](https://tex.stackexchange.com/questions/434946)
  - biblatex basically is a reimplementation and reinvention of the BibTeX way of creating bibliographies that had been with the TeX world since the late 1980ies
    - With BibTeX the `.bst` files written in their own reverse Polish notation language determine the output of the bibliography. 
    - BibTeX compiles all the information from the `.bib` file and outputs it to the `.bbl` in the expected format, LaTeX then simply imports the `.bbl` and typesets its contents. 
  - With biblatex on the other hand the formatting is done on the LaTeX side. 
  - CSL is an XML-based language for citation and bibliography styles. 
    - It aims to be a universal language that can be used by all kinds of reference managers and word processors. 
  - biblatex is basically LaTeX-only and CSL is supposed to be a universal standard.

- [Overleaf Bibtex bibliography styles](https://www.overleaf.com/learn/latex/Bibtex_bibliography_styles)

- 当title字段中间存在"\url"时会提示错误，原因是\会被理解为转义字符
  - 变通方法是将\url改为\\url
  - [\u in JavaScript String.raw`template literal`](https://stackoverflow.com/questions/39310685)
    - replacing the line with `\u005Cusepackage{indentfirst}`, or even just `\x5Cusepackage{indentfirst}`.
      - `5C` corresponds with `\`.
    - Another option might be using the dollar sign and curly braces notation for expressions. `${'\\'}usepackage{indentfirst}`

- [overleaf中关于引用website的处理](https://www.overleaf.com/learn/latex/Bibliography_management_with_bibtex)
  - `@misc` is for whatever doesn’t quite fit any other entry type. 
  - not all bibliography styles support the `url` field: plain doesn’t, but IEEEtran does. All styles support `note`. 
  - It can be especially useful for web pages—by writing `note = \url{http://...}` or `url = {http://...}`

- A simple way of doing it in BibTeX is with a `@misc` entry
  - If you are using BibLaTeX there is an `@online` entry type
- [Generate BibTeX entry from URL](https://www.reddit.com/r/LaTeX/comments/q85jo1/generate_bibtex_entry_from_url/)
  - https://karlosos.github.io/url_to_bibtex/

```latex
@misc{WinNT,
  title = {{MS Windows NT} Kernel Description},
  howpublished = {\url{http://web.archive.org/web/20080207010024/http://www.808multimedia.com/winnt/kernel.htm}},
  note = {Accessed: 2010-09-30}
}

@online{WinNT,
  author = {MultiMedia LLC},
  title = {{MS Windows NT} Kernel Description},
  year = 1999,
  url = {http://web.archive.org/web/20080207010024/http://www.808multimedia.com/winnt/kernel.htm},
  urldate = {2010-09-30}
}

@MISC{Anu:2013,
author = {Aggarwal, Anupama},
title = {This is how you cite a website in latex},
month = may,
year = {2013},
howpublished={\url{http://precog.iiitd.edu.in/people/anupama}}
}
\usepackage{url}
```

## 0119

- BibTexBook的类型需要添加title，editions改为edition
- BibTexMisc类型需要添加url
- 每个参考文献的元数据类型是否都要添加 `doi` 字段
  - 还有url字段
- 暂未实现，当一篇文章有多个作者时需要缩写，是在从数据库读取bibTex时实现，还是在渲染时实现
- 暂未实现，bibTex的tag值中可能含有`{}`包裹的变量，需要在读取元数据字段时解析，还是就设计为不支持

```latex
@article{grishchenko_2010, title={Deep hypertext with embedded revision control implemented in regular expressions}, DOI={10.1145/1832772.1832777}, journal={Proceedings of the 6th International Symposium on Wikis and Open Collaboration - WikiSym 10}, author={Grishchenko, Victor}, year={2010}}

```

- [TS 3.1 - 高级类型总结](https://www.cnblogs.com/qq3279338858/p/14206569.html)

## 0118

- 参考文献的显示流程
  - 解析获取文章元数据的各个字段
  - 判断文章类型，选择最合适的文献显示组件
  - 参考文献组件根据文章元数据，渲染到dom

- [APA style Reference List: Basic Rules](https://owl.purdue.edu/owl/research_and_citation/apa_style/apa_formatting_and_style_guide/reference_list_basic_rules.html)
  - [Reference List: Articles in Periodicals](https://owl.purdue.edu/owl/research_and_citation/apa_style/apa_formatting_and_style_guide/reference_list_articles_in_periodicals.html)
  - [Reference List: Books](https://owl.purdue.edu/owl/research_and_citation/apa_style/apa_formatting_and_style_guide/reference_list_books.html)

- [How to Cite in APA Format (7th edition) | Guide & Generator](https://www.scribbr.com/category/apa-style/)
  - components of a reference entry
  - 1. author
    - 一作，多个作者，合作者，通讯作者，联合@
  - 2. date
    - 年、年月日、未发布、未知日期
  - 3. title
    - 文章网页用普通文字、书籍用斜体、未知来源用方括号
  - 4. source
    - 期刊、出版社、网站、地址
  - prefix
    - doi
    - Use the prefix field in situations like see also or i.e..

- [How to Create an APA Style Appendix | Format & Examples](https://www.scribbr.com/apa-style/appendices/)
  - 附录可以放图片、表格、伪代码、名词解释

## 0117

- 参考文献暂不支持手动输入

- latex入门
  - [LaTeX入门指南|新手速进](https://www.zhihu.com/zvideo/1421078748670566400)

- [在arXiv下载论文的LaTeX源码](https://www.jianshu.com/p/b8baca4bfc20)
  - 找到一篇arXiv论文的版面，点击Download中的Other formats；
  - 点击Source目录下的：Download source；
  - 改名为：.zip， .tar.gz等的尾缀，然后解压缩此文件；
  - 打开tex主文件，编译成PDF；

- 闫东沟通
  - workspace的操作接口写了哪些
  - 向workspace中添加手机号或邮箱时，该用户登录后会自动拥有workspace的权限

- 搜索ui的设计
  - cmd+k调出位置固定的弹窗，类似docusaurus、notion
    - 弹窗空间较多，可显示详细条目及信息
  - 下拉菜单，类似github
    - 可切换全局搜索、仓库内搜索、org内搜索

- [flexsearch](https://github.com/nextapps-de/flexsearch)
  - Next-Generation full text search library for Browser and Node.js
  - fastest and most memory-flexible full-text search library with zero dependencies.
  - `Document` is multi-field index which can store complex JSON documents (could also exist of worker indexes).

- https://github.com/timc1/kbar
  - https://kbar.vercel.app/
  - Command+k interfaces are used to create a web experience where any type of action users would be able to do via clicking can be done through a command menu.
  - With macOS's Spotlight and Linear's command+k experience in mind, kbar aims to be a simple abstraction to add a fast and extensible command+k menu to your site.

## 0112

- 完善/docs
  - [x] 图片保存到本地数据库 迁移到 toe-frontend
  - [ ] 文档内搜索
- 实现/user
  - 最近文档列表
  - 搜索用户数据
- 实现/workspace
  - 输入关键字搜索出匹配文档名或内容的文档
  - [ ] 选中一篇文档后，所有行的复选框都应该显示
  - 全局header

## 0111

- 实现所有文档列表组件时，要考虑在以后实现回收站文档列表时方便复用
  - 不支持文件夹的设计，大大简化了文件列表的实现难度

- 实现列表一行的悬浮菜单花费了大量时间
  - 原因是查看mui的Popover文档示例时，看漏了一行触发条件
    - const open = Boolean(anchorEl);
    - const id = open ? 'simple-popover' : undefined;

## 0109

- 登录后无法访问登录页，需要实现退出登录的逻辑

- react custom hook函数不需要有返回值
  - useEffect可以有返回值，也可以没有

- [useFetch: Building custom hooks in React to fetch Data](https://dev.to/shaedrizwan/building-custom-hooks-in-react-to-fetch-data-4ig6)

- [How to extract React component logic into a custom Hook](https://www.benmvp.com/blog/how-to-extract-react-component-logic-custom-hook/)
  - Most of the time I write the “messy” logic in the component first and then extract it into a custom Hook. 
  - But sometimes I am able to “see in the future” and build the custom Hook first and “magically” have the data ready in the component.

- [what is the difference between using useEffect inside a custom hook and a component](https://stackoverflow.com/questions/62329615)
  - The `useEffect` function inside custom hook will only run when you use it inside a functional component and invoke it. 
  - Also note that the behavior of `useEffect` will remain exactly the same as if it were written inside the functional component itself

## 0108

- 路由未解决的问题
  - 刷新页面能保持原页面状态的问题，路由是不变的
  - 示例MentorLabs给出的解决方案是，在 if (!isAuthenticated) 前有一个前置判断  if ( status === 'pending'){ show loading } 
    - 首次请求用户数据pending时，会显示加载组件；
    - 注意当用户数据请求完成后，isUserAuthenticated会变成true，下一个if也不会执行了

- 注意更新user状态的顺序，前面会先执行，错误顺序会匹配执行错误的if分支
  - 先 setUserInfo(userInfo); 
  - 后 setUserStatus('resolved'); 

- [React batch updates for multiple setState() calls inside useEffect hook](https://stackoverflow.com/questions/56885037)
  - on next major release (probably v17) React will batch everywhere by default.

## 0107

- routing难点
  - 登录用户刷新页面时，会闪过明显的登录窗口
    - 可以使用useNavigate()在合适的时机命令式执行跳转，而不是使用`<Navigate>`声明式每次都会跳转

- 刷新页面保持用户登录状态的方法
  - https://github.com/adarshaacharya/MentorLabs/blob/main/client/src/App.tsx

## 0106

- 区分3种路由
  - RoutePrivate 未登录不可访问，登录后才可访问
  - RouteUnauthorizedOnly 未登录可访问，登录后不可访问，会自动跳转到指定路由
  - 默认public 未登录可访问，登录后可访问

## 0104

- 图片保存本地数据库仍然存在的问题
  - 不显示dataReference属性的原因，在上传图片addRef后，不能  await dbClient.set(articleDbDoc); 
  - Failed to execute 'createObjectURL' on 'URL': Overload resolution failed
    - 不能稳定复现

- 🤔 复现调试图片刷新时，突然编辑器不见了
  - 🔈 变通的方案是在wsl的linux下复现bug，竟然能顺利执行，没有bug
  - 注意wsl的4001端口会被windows的4001端口屏蔽掉，要检查端口是否相同
    - ⚠ 开发环境必须以linux为主，在windows vscode中打开linux下的源码
  - TypeError: Cannot read properties of null (reading 'getAttribute')
  - at IconView._updateXMLContent (iconview.js:100)
  - https://github.com/ckeditor/ckeditor5/issues/10927
    - Most probably, the file-loader handles CKEditor 5 icons. You need to exclude CKEditor 5 assets from this loader. But it's hard to say more as we don't see the full webpack config.
  - Cannot read property 'getAttribute' of null in react
    - it seems there's something wrong with your webpack configuration
# 2021

## 1231

- 图片保存到本地数据库的改进点
  - 在应用层实现src属性替换，所以首次渲染图片时控制台会报错，但之后会正常显示图片
  - 拖拽移动图片到inline位置后，imageInline的dataRef属性仍存在，还原成imageBlock时dataRef仍能正常显示
    - 但图片处于inline状态时，刷新页面后，dataRef属性会丢失，图片会无法显示
    - 已解决

- 解决图片刷新的问题
  - 在react应用层更新图片src是最简单的
  - 也可以考虑afterInit钩子函数

- 图片刷新的预期
  - model可以不变
  - 上传新图片后，旧图片不会重新刷新，刷新页面时，所有图片会刷新

## 1230

- 编辑器依赖外部数据的解决办法

- ??? 在downcast中执行 viewWriter.setAttribute('src', imgToBlobUrl, img); 后，ckeditor的view视图属性值更新了，但dom却没有更新
  - ~~变通思路是在upcast里面做属性值替换~~
  - 测试发现，不能在downcast和upcast里面有异步的过程

- db?.get(doc?.id as DocumentEnum.article)
  - 当id是自定义字符串时，返回的doc.id是原字符串吗  

## 1229

- 图片上传流程
  - 理想流程
    - 图片上传得到图片数据对象 -> src/blobUrl -> 显示 -> src/dbId -> 更新显示
  - 暂时流程
    - 图片数据对象 -> src/dbId -> src/blobUrl -> 显示

- 要处理 `Ctrl + V` 粘贴的图片

- 上传图片的保存
  - 保存到本地数据库
  - 图片model里面保存的是图片在数据库中的id
- 上传图片的读取
  - 思路1: 编辑器加载后，修改model，替换所有图片url
    - 可在在react层做，也可实现为一个插件
  - 思路2: 扩展官方Image插件，在downcast的过程中，替换图片url，model不变

## 1228

- 流程图的饼状图示例可以缩放，但流程图示例不能缩放
  - ~~问题在于 figure 下的 div.ck-widget__type-around 标签宽度auto为全宽，而不是图片宽度~~
    - 将figure display改为table后，type-around的宽度为正常的预期值了
  - 缩放时，图片的高度为什么没有变化

- 其他图片如何使用ImageToolbar插件
  - 本质上是WidgetToolbar

- 流程图图片实现的问题、使用官方图片插件实现图片的问题
  - 选中图片时，会出现内外2个高亮框，内层图片高亮框是蓝色，外层mermaid高亮框是黄色
    - 变通的方式是鼠标悬浮时取消显示mermaid高亮框，但此时需要选中图片外的空白才能选中mermaid，按回车才能换行
    - 图片左右对齐时，mermaid高亮框变成一条线，回车不能换行
  - 选中内层图片时，按回车不能换行，必须选中外层mermaid框
  - 选中内层图片时，拖拽移动后就变成了纯图片，不能再编辑代码
    - 只有选中外层mermaid框，拖拽移动后，才能再次编辑代码

## 1227

- 图片缩放问题稳定复现的场景
  - 在空编辑器的情况下，上传一张图片，此时img标签下面有3个resizer div

- 转正答辩工作

## 1226

- 在toe-editor里面缩放图片的体验不如ckeditor官方编辑器图片插件示例
  - 在沿水平或竖直方向缩放图片时，官方示例有时也会感到卡顿

- 二分法排查问题
  - 注释掉 InsertBlankLine 插件后，上传图片就不会生成3个resizer div了
    - 注释掉其他插件时，缩放图片仍然可能出现突然变大或突然卡住，然后无法缩放的问题
    - 卡住的时候，可以看到view里面又生成了3个resizer div
    - 原因可能是，每次插入空行后，model数据发生变化，此时img resize相关插件读到的width就变为空了，然后style属性就变成空了，此时图片会显示成宽度最大且无法拖拽缩放

- 图片插件问题确认
  - 在编辑器中创建图片插件imageBlock时，ImageResizeHandles Plugin 的init()中创建了3次resizer对象，所以dom中出现3个resizer div
    - 正确的方式应该只创建一次，后面缩放图片时不用创建，直接resizer.redraw();
  - 在缩放图片的过程中，view的figure元素style属性设置width失败了
    - 但ImageResizeEditing的downcast的data参数是有宽度数据的，并且也执行了 viewWriter.setStyle( 'width', data.attributeNewValue, figure );

## 1225

- ImageResize插件的结构
  - ImageResizeEditing
    - 在imageBlock/Inline的schema上添加了`width`属性
    - 在downcast中，将width映射到style属性的width值
    - 注册resizeImage命令
  - ImageResizeHandles
    - 此插件依赖 WidgetResize
  - ImageResizeButtons
    - 根据`image.resizeOptions`配置，创建button并注册缩放方法

## 1224

- 图片插件无法缩放问题分析
  - 替换全新的InsertImage插件后，只产生了一个`<div class="ck ck-reset_all ck-widget__resizer"`，但是仍然无法缩放
  - 定位问题在widget，而不是ImageResize
  - 每次拖拽缩放图片后，正常情况下，
    - figure元素会更新 `style="width:16.6%;"` 宽度值
    - 内部resizer会更新 `<div class="ck ck-reset_all ck-widget__resizer" style="height:159px;left:0px;top:0px;width:334px;"` 宽度值

## 1223

- 图片插件重构
  - 无法稳定复现
    - 在dev tools的application页面可以清除旧数据，然后插入图片就没有2个高亮框和无法缩放的问题了
  - 两个高亮框
  - 无法resize
    - 原因是figure标签内层结构错误，用来缩放的div有3个
      - `<div class="ck ck-reset_all ck-widget__resizer" style="height: 200px; left: 0px; top: 0px; width: 200px;">` 此div内包含用于缩放的4个点，会显示在图片4角
      - 第1个ck-widget__resizer宽度特别宽，后2个resizer宽度正常
    - 原因需要进一步分析，UploadImage后有3个resizer div，InsertImage后有1个resizer div，此时InsertImage得到的图片仍然无法缩放大小

- 多维表格新建视图的设计
  - 分组表格不是单独的视图，就是在表格视图下调整得到
  - 在分组表格下新建得到的表格视图，默认是不含分组的普通表格视图，也就是配置丢失了

## 1222

- table work
  - [x] icon cell
  - [ ] 切换同一数据的视图

## 1220

- 看板或表格内容涉及到全局任务、全局文档时，难以本地化

- 样式是实现表格复杂度最低的一部分，是靠后的一部分
  - 重点是过滤排序分组

- 看板数据结构的层次
  - 数据存储结构
  - 看板视图结构
  - 表格视图结构
    - 任务id存在对应的任务名称

- 多维表格数据结构的层次
  - 存储结构
    - 对象数组
  - 看板视图结构
    - 预定义对象
  - 表格视图结构
    - 任务id存在对应的任务名称
    - 分组视图使用 useGirdLayout
    - 普通视图使用 useFlexLayout

## 1219

- 子任务如何显示
  - 显示在嵌套的行？
  - 显示在单独的任务列，并且显示进度？

## 1217

- 多维表格数据源设置
  - { data : [] }
  - 对表格 data, columns
    - if( field === 'subTasksList' )
    - 特殊处理文档字段、子任务字段
  - 对看板 data -> kanbanData

- notion卡片边框的样式

```css
.card {
  position: static;
  display: block;
  margin-bottom: 5px;
  box-shadow: rgba(15, 15, 15, 0.1) 0px 0px 0px 1px, rgba(15, 15, 15, 0.1) 0px 2px 4px;
  border-radius: 3px;
  color: inherit;
  background: white;
  text-decoration: none;
  overflow: hidden;
  transition: background 100ms ease-out 0s;
}
```

## 1216

- 工作计划
  - 看板的目标：看板作为多维表格的一个模板
  - 加强看板样式和功能与文档编辑器的联系
    - 看板界面使用编辑器的题头，但不是编辑器
    - 甚至重用文档侧边栏的功能，比如显示最近引用过的文档
  - 看板的数据结构重构到 trello导出的json
  - 切换看板视图和表格视图
  - 实现crud
    - 看板和看板表格暂时都只支持弹窗编辑
  - 接入文档数据库，测试之后文档数据库api应该更稳定了

## 1215

- react-table示例中Grouping和GroupingColumn的区别
  - Grouping的每个分组列都在最左边显示成单独列，当有多个分组字段时会显示成多个列
  - GroupingColumn的所有分组列都在最左边显示在一个列之中，这一列是树形结构

## 1214

- react-table的expanding和subComponent的区别
  - expanding的行展开后，tableInstance的rows总行数会增加，折叠后rows数量会减少
  - subComponent展开后，tableInstance的rows不变

## 1213

- 如何更新看板的数据和ui
  - ✔ 看板的数据源作为props从外部传入
  - ✔ 看板更新的方法也作为props传入

- 🤔 看板适不适合做成离线可用、本地数据库的形式?  独立看板、文档中的看板
  - 增加了看板任务/用户全局任务crud的复杂度；看板一定属于workspace
    - 文档侧边栏的任务从哪里读取
    - 文档侧边栏添加的任务数据保存到哪里
    - 如何从其他组件 添加、修改、删除 子任务
  - 动态看板增加了编辑器本地存储的复杂度
    - 在编辑器中显示任务卡片增加了文档的外部依赖和请求数据量，就算只存储一个卡片id，也会有单个卡片甚至整个看板数据的请求
    - 在离线状态下，任务卡片在编辑器中的显示形式和交互形式
  - 动态看板是在增加了协作的复杂度，应该避免这种设计
    - 离线协作时，应该将涉及在线资源和第3方资源的block元素禁用掉
    - 看板的协作，不适合用本地数据库的方式来实现，当然用本地数据库来实现是可行的
  - 我的想法
    - 区分独立看板和文档中的看板，独立看板不可离线但可全局统计，文档中的看板可离线但不可全局统计
    - 编辑器内只能查看和读取任务项，不能修改，但可跳转到看板进行修改
    - 离线状态下，文档侧边栏的任务应该提示只读信息，不能访问全局看板

- 卡片的存储结构
  - 最好是扁平的结构，每个卡片存储所属的分组列id和看板id

## 1210

- 看板预定义的字段名称不能太随意
  - 可参考成熟的产品，如trello，这样就直接支持导入trello数据

## 1209

- ✔ 待讨论：表格的实现形式
  - 多个表格的视觉形式通过分组实现
  - 视觉上 单个表格
    - https://v89sa2wwaq.feishu.cn/base/bascnDfGDUAC9uZmG8WAIm68pDf?table=tblLEEoU9EpeZpaF&view=vewG1l8FO1
    - https://fupi20211128172727640.worktile.com/mission/projects/61a3bc018c35ea4484cf9468
  - 视觉上 多个表格
    - https://v89sa2wwaq.feishu.cn/base/bascnkYxZcXLhaTfIDpw6MIpvkd?table=tblAmjmotNVInT2p&view=vewxycGIAm
    - https://tower.im/projects/fc0d13409e357c612254c3707d9150e3/list/todos/

## 1207

- 工作任务确定
  - 先做具体场景的看板和表格，再逐渐迁移到通用的多维表格

## 1205

- CRUDList的设计
  - 针对较短、易编辑的列表
  - 可crud列表项
- CRUDList的使用场景
  - 待办事项、清单
  - 文档列表

- SearchList的设计
  - 针对列表数据的搜索
- SearchList的使用场景
  - 选择用户
  - 搜索标签、添加标签

## 1203

- @material-ui/pickers日历的局限
  - 已废弃
  - 日历文本必须先显示，日历卡片才能弹出在正确位置；
  - 若日历文本未提前渲染到dom，文本和卡片同时渲染出来时，由于卡片的位置依赖于文本位置，所以会出现分离和漂移
  - 临时解决方案：提前将日历文本渲染到dom，但`visibility：hidden`，会占据空间，不触发事件

- onClick事件触发多个任务的实现思路
  - 要考虑如何在其他地方触发相同的操作，将计算逻辑抽离出去方便其他地方复用

- input设置`border: none; `后，仍然显示边框的问题
  - 排查失败
  - MuiPickersUtilsProvider   DatePicker
  - . MuiInputBase-input{ border: 0; }
  - https://codesandbox.io/s/material-demo-forked-fg5xk?file=/demo.js

## 1202

- **react子组件获取不到父组件传递的props，始终是undefined**
  - 原因排查
    - 从react devtools工具中分析问题组件接收的props的具体值，发现Board组件的直接子组件是KanbanColumn，而不是Column
    - 从Board到Column，中间还有KanbanColumn、Draggable、ContextProvider等组件
    - 连源码都没有看清楚就想当然测试了，浪费了很多时间
  - 错误思路
    - 因为对react的forceUpdate理解不够深入
    - const [ignored, forceUpdate] = useReducer(x => x + 1, 0); 
    - function handleClick() { forceUpdate(); }
    - `<button onClick={forceUpdate}>Force update</button>`

- 更新对象数组中一个对象的方法
  - setState(prevState => ( { data: prevState.data.map(el => (el.id === id ? { ...el, text } : el)) }) )

## 1201

- https://github.com/nishantpainter/personal-kanban
  - wipLimit可以限制一个面板内的任务卡片数量，当达到指定数量时，不能再添加新卡片

## 1129

- 之前的editoe组件为什么会报那个chunk错误？

- codebase-https://github.com/nishantpainter/personal-kanban
  - Column 看板的一列，是一个面板，上面可以放置小卡片

## 1127

- affine
  - /e'fain/
  - adjective mathematics
  - Allowing for or preserving parallel relationships
  - The Notion-like docs solution for enterprises.

- affine首页的打字效果
  - https://www.theorange.digital/
  - "typed.js":"^2.0.12"

## 1126

- 文章页 上下结构
  - 右侧资源面板可切换隐藏

## 1125

- 创建workspaceId以数字开头
  - 但rxdb的数据库不能以数字开头
  - 变通方案：保存前统一加前缀

## 1124

- affine产品操作流程
  1. 用户登录  >  landing未登录页、注册页、登录页
     - /usernameId

  2. 请求workspace列表  >  用户个人主页
     - /usernameId 

  3. 打开单个workspace  >  workspace页面
     - /usernameId/workspaceId 

  4. 打开单个文档  >  编辑器页面
     - /usernameId/docId

- nextjs router.push()要放到useEffect或onClick里面

- 权限状态码
  - 401 Unauthorized（未经授权），需要登陆
  - 403 Forbidden（被禁止），需要对应权限
  - 404 Not Found（找不到），可能的原因是服务器端没有这个页面

- 处理复制粘贴url的流程
  - 先访问/user/me检查登录
  - 在获取workspace列表等基本信息
  - 然后检查目标url是否符合权限要求
  - 最后显示目标url的页面

- 路由权限和http取数权限的验证返回值结构
  - 路由权限要检查返回的用户对象是否包含`role/canAccess`属性，通过后才跳转路由；
    - 需要新的查询接口，或者直接在前端配置规则
    - {errorCode: 401, canAccessRes: false}
  - http请求权限要在请求头中带上 authorization，检查返回值是否包含成功标志，返回值包含成功标志才直接使用，否则鉴权失败
    - {errorCode: 401, canAccessRes: false}

- nextjs用户登录的实现
  - rbac路由
  - [Role-Based Routing](https://github.com/vercel/next.js/discussions/23041)
    - 思路是基于 import { useRouter } from "next/router" 实现
    - 不要将router.push()写到render方法里面，要写到onClick方法或useEffect里面
  - [Role-Based Routing with Next.js](https://spin.atomicobject.com/2019/12/11/role-based-routing-with-next-js/)
    - 每次跳转page时检查 router.pathname.startsWith("/employee") && role !== "employee"
  - [Next.js - Redirect to Login Page if Unauthenticated](https://jasonwatmore.com/post/2021/08/30/next-js-redirect-to-login-page-if-unauthenticated)
  - [[RFC] - Route guards](https://github.com/vercel/next.js/discussions/11822)
  - [Implement Protected Routes in NextJS： verify & no-verify token](https://dev.to/shubhamverma/implement-protected-routes-in-nextjs-37ml)

- 解决用户权限的2个维度
  - 路由级权限控制，定义路由配置对象时，声明访问该路由需要的role
  - http请求级权限控制，访问敏感数据或执行敏感操作时需要检查role
  - 其他参考
    - 动态添加路由
    - 菜单与路由分离，菜单由后端返回菜单
    - 或者 菜单与路由完全由后端返回

- useEffect的返回值函数未执行的原因
  - 可能组件已经卸载，就不会执行了

## 1123

- material-ui 暂时没有dropdown组件
  - select组件样式太简陋

- nextjs动态路由
  - 将匹配路由的过程在构建时或请求时自动计算匹配
  - 与react-router的手动计算类似

- 不登录的时候，能够查看哪些内容
  - 本地缓存
  - 公共模版
  - 用户分享

- workspace的路由url设计
  - 类似github的url： username/workspace
  - 用户名必须6位及以上，小于6位由系统保留使用

- nextjs的全局状态管理
  - pages/_app.js 中可以定义全局使用的context，这样子组件就能通过useContext获取到
  - 可考虑将经常变动的state值放在单独的context，然后将不变的dispatch方法放在另一个单独的context

## 1122

- 只在鼠标悬浮时才显示元素的方法
  - [Using only CSS, show div on hover over another element](https://stackoverflow.com/questions/5210033)

```CSS
.showme {
  display: none;
}

.showhim:hover .showme {
  display: block;
}
```

```html 
<div class="showhim">
  HOVER ME
  <div class="showme">hai</div>
</div>

```

- 表格的最大宽度无法占满右边
  - 问题在于表格是inline-block，列宽默认150，总宽是多少就显示多少
  - 可以手动修改列宽

- 表格一列的宽度无法设置
  - 考虑使用 `useBlockLayout` 布局
  - [Width is not working Material-UI Enhanced Table](https://github.com/tannerlinsley/react-table/discussions/2332)

- workspace的文档列表功能实现顺序
  - [x] 替换mock数据
  - [x] 图标
  - [x] 折叠
  - [x] 排序
  - [ ] 工具条
  - [ ] sticky header

- react-table选用哪种布局
  - 参考相关示例和成熟的产品，可选择table或绝对定位

## 1119

- material-ui v4 组件
  - `Modal` component provides a solid foundation for creating dialogs, popovers, lightboxes, or whatever else.
  - `Popper` can be used to display some content on top of another. 
    - It's an alternative to react-popper.
  - `Popover` can be used to display some content on top of another.
    - The component is built on top of the `Modal` component.
    - The scroll and click away are blocked unlike with the `Popper` component.
  - `Dialog` informs users about a task and can contain critical information, require decisions, or involve multiple tasks.

## 1118

- 日历热力图样式
  - github方块 10x10
  - gitee方块 13x15
  - affine方块 14x14
  - 方块样式参考github

- 点击添加文档按钮，在日历热力图上会反映出操作记录

## 1117

- useStyles()的地方会触发warning
  - Each child in a list should have a unique "key" prop.
  - 原因定位，返回react fragment时，如果使用`<>`则无法添加key，必须使用完整的react元素 `<React. Fragment key='yourKey' >`

- 利用mui的breakpoints，实现不同宽度时，同一位置显示不同元素
  - 只在宽屏时显示
    - hiddenSmDown:{ [theme.breakpoints.down('xs')]: { display: 'none' } }
  - 只在小屏时显示
    - hiddenSmUp:{ [theme.breakpoints.up('sm')]: { display: 'none' } }
  - [Using Breakpoints in MaterialUI](https://dev.to/christensenjoe/using-breakpoints-in-materialui-5gj0)

- css单位
  - `ch` Represents the width, or more precisely the advance measure, of the glyph "0" (zero, the Unicode character U+0030) in the element's font.

## 1116

- 排查水平滚动条出现的原因
  - [Finding/Fixing Unintended Body Overflow](https://css-tricks.com/findingfixing-unintended-body-overflow/)
    - 打印出过宽元素的dom

## 1115

- 首次执行editor.setData时，解决本地上传图片blobUrl失效的问题
  - 借助正则表达式
  - URL.createObjectURL返回的url一直是63位

- 图片本地化后，刷新页面仍然会导致图片无法显示的问题
  - 因为modelWriter.setAttribute后，ckeditor的model变化不会自动触发react的setContent更新
  - 解决方法是手动触发更新content数据，接着自动保存更新内容

- 保存图片数据后，如何恢复
  - 通过从rxdb中读取图片数据，再对blob对象创建url

- 编辑器初始测试数据

```html
<h1>title</h1>
<figure class="image image-style-align-right">
  <img src="blob:http://127.0.0.1:4001/f24939fd-49c8-4fb2-b90c-86917bec4b88">
  <figcaption>&nbsp;</figcaption>
</figure>
<figure class="image"><img src="blob:http://127.0.0.1:4001/f4fe8af7-300e-4c89-b713-94abd837f8d4">
</figure>
<pre class="mermaid" style="width:80vw;"><figure class="image"><img src="https://api.editoe.com/api/mermaid/generate?data=graph%20TD%0A%20%20%20%20A%20--%3E%20B%0A%20%20%20%20A%20--%3E%20C%0A%20%20%20%20B%20--%3E%20D%0A%20%20%20%20C%20--%3E%20D%0A"></figure>graph TD
    A --&gt; B
    A --&gt; C
    B --&gt; D
    C --&gt; D
</pre>
<p>&nbsp;</p>
```

## 1114

- 对上传后保存图片和取出图片数据的api理解不清晰
  - 上传图片时，img-file  ->  blobUrl  ->  rxdb-doc-id
  - 刷新页面时，model不变，如何根据blobUrl查找图片数据

- DocumentImpl.addVersion(blob, type)的目的是为了什么
  - 操作 DocumentImpl.#versions，保存新数据的版本
  - this.#versions.add(blob, type)

- DocumentClient.set(document)的目的是为了什么
  - 通过DocumentClient操作rxdb数据库
  - this.#documents.atomicUpsert({ ...value, id })
  - this.#blobs.insert({ id, type: v.type, created: v.created })
  - 问题：为什么返回document.id，这个id本来就可以从参数中取到，中间有被更新吗
    - 虽然再次调用了setArticleId，但因为状态没变，react也不会rerender

## 1112

- 在imageBlock插件里面实现src url转换，还是在react层
  - 在react层，每次重载文档都会创建一次blobUrl

- 每次刷新页面，图片无法显示的问题
  - URL.createObjectURL是临时的，每次刷新都会重新创建
  - model层存ref，而不是blobUrl

- 如何处理同一张图片的问题
  - 上传已经以前已经上传过的图片时
    - 每次在保存图片数据前，能拿到ArrayBuffer
  - 复制粘贴src为blobUrl形式的图片时
    - 每次图片的src会自动变化

- not-yet
  - URL.createObjectURL(file)每次返回的url都不相同，即使对于同一个文件
    - 每次粘贴普通图片后，粘贴得到的新图片url也不相同
  - 文档rxdb保存图片的ArrayBuffer时，去重是如何实现的？很难

- 不同方式读取图片文件的ArrayBuffer得到的数据是否相等
  - 难以比较2个ArrayBuffer对象是否相等，因为是js对象
  - imgFileReaderRetArrayBuffer === fileArrayBuffer 
  - 通过下面的工具方法，可以比较得出上面两种方式读出的文件数据相等

## 1111

- 图片上传问题
  - 图片保存时，id如何设计；由服务端实现
    - 取 uuid、文件名+随机值 、 md5-hash值 、 文件url
  - 图片更新如何实现
    - 目前只能先删除，再上传
  - 图片blob对象只保存到了rxdb，暂时没有读取和使用，可以用来实现图片编号
    - 图片数据单独存储的目的
  - uploadedImg这个新api的设计
  - 只实现了图片存储，暂未实现editor.getData()获取文件的无关数据移出

- 体验
  - 本地文档不方便调试图片

- 实现图片本地化的思路
  - 1. 上传图片时，图片保存到本地数据库
  - 2. 图片保存的格式为blob格式的url

- File是Blob的子类
  - new File([], 'foo.txt') instanceof File // true
  - new File([], 'foo.txt') instanceof Blob // true

- [FileReader vs. URL.createObjectURL](https://stackoverflow.com/questions/31742072)
- createObjectURL 同步执行
- FileReader.readAsDataURL 异步
- createObjectURL
  - returns url with hash, and store object in memory until document triggers unload event (e.g. document close) or execute revokeObjectURL
  - 需要手动释放内存
  - ？ 注意每次上传相同的图片会返回不同的url，是否存在过多的冗余数据
- FileReader.readAsDataURL 
  - returns base64 that contains many characters, and use more memory than blob url, but removes from memory when you don't use it (by garbage collector)
  - 占用更多内存，但会自动gc回收内存
  - 方便读取和保存额外的元数据

## 1110

- 图片本地化
  - 图片保存为doc的结构设计？图片存储 id/url, displayName编号或显示名, data
    - data保存在哪里，如何向doc里面添加图片base64数据
    - 最后图片img的src应该显示的是什么
  - 流程图的图片src本身就是符合要求的url，只需要替换通过工具栏上传的图片
    - 但注意流程图要去掉无必要的元素标签

- 审阅balloonToolbar悬浮工具条的方法
  - editor.plugins.get('BalloonToolbar').show()

```CSS
.ck.ck-balloon-panel.ck-balloon-panel_visible {
  & .ck.ck-dropdown {
    & .ck.ck-splitbutton {
      display: inline-flex;
      flex-flow: row nowrap;
    }
  }
}

.ck.ck-balloon-panel.ck-balloon-panel_visible .ck.ck-dropdown .ck.ck-splitbutton {
  display: inline-flex;
  flex-flow: row nowrap;
}
```

- [x] 编辑器editor.getData()再editor.setData()时，mermaid的model会多出一个空的imageBlock的问题
  - 原因定位
    - pre元素的upcast过程中，imageBlock只有在不存在时才需要创建，没必要每次都创建
    - ~~观察model的变化，model变化了，说明command的执行过程中执行了额外的操作, 应该在command中排查，而不是在upcast或downcast的地方排查~~
      - editor.setData(editor.getData())的过程，实测不会触发command
  - 比较理想的方式，是getData时只输出mermaidCode，不输出image，但没有找到具体实现方法，因为dataDowncast无法完全控制getData的输出过程
  - 变通的方式，是getData时输出mermaid和imageBlock，setData时修改upcast过程，避免创建新的imageBlock

- 测试编辑器内容的保存
  - editor.setData(editor.getData())

- editor.getData()的实现原理
  - 会调用DataApiMixin.getData( options ) { return this.data.get( options ); }
  - core/editor中, this.data = new DataController( this.model, stylesProcessor ); 
  - DataController.constructor中，会创建 this.viewDocument
  - DataController.get(options)方法，return this.stringify( root, options )
  - 会执行 DataController.stringify( modelElementOrFragment, options)，只做2件事
    - model -> view: const viewDocumentFragment = this.toView( modelElementOrFragment, options );
    - view -> data: return this.processor.toData( viewDocumentFragment );

- editor.setData(data)的实现原理
  - DataController.set( data, options = {} ) 会把将新数据设置到editor的任务添加到队列
  - 会执行 DataController.parse(data, context)，只做2件事
    - data -> view: const viewDocumentFragment = this.processor.toView( data );
    - view -> model: return this.toModel( viewDocumentFragment, context );

- mermaid dataDowncast的输出是正常的
  - mermaidView = writer.createContainerElement

- 检查editor.getData的过程和dataDowncast的关系

## 1109

- [ ] 流程图获取焦点时是否要移除外部蓝色边框
- [ ] 流程图双击时出现编辑文本代码弹窗，但修改过的文本代码无法保存

- CKEditorError: model-position-before-root
  - Cannot read properties of undefined (reading 'length')
  - 检查修改model时插入元素的位置

- 媒体查询@media技巧
  - 如果判断最小值，即使用(min-width)，应该从小到大写；也是推荐的写法，因为一些前端框架（如：bootstrap）就是判断最小值，从小往大写的；
  - 如果判断最大值，即使用(max-width)，应该从大到小写

- 给文档添加margin的设计
  - 飞书文档网页版未适配手机浏览器
  - 文档内容的宽度需要设置 min-width， max-width
  - 当宽度缩小到最小宽度以下，文档宽度就不会继续变小了，此时也没有水平滚动条，水平选择和浏览不方便

- 飞书文档容器宽度样式css
  - 文档在宽屏上，最大宽度为790

- mui的默认断点
  - xs 0
  - sm 600
  - md 960
  - lg 1280
  - xl 1920
  - [@media 查询条件判断的顺序](https://www.jianshu.com/p/c9901d17a5d6)

```CSS
.etherpad-container {
  min-width: 470px;
  max-width: 790px;
  min-height: 100%;
  margin: 0 auto;
  justify-content: center;
  transition: margin .4s ease-out;
}

/* @media screen and (max-width: 900px) */
.etherpad-container {
  width: calc(100% - 40px);
  margin-left: 32px;
  min-width: 344px;
}

/* @media screen and (max-width: 1279px) */
.etherpad-container {
  width: 70%;
  margin-left: 15%;
}

/* @media screen and (max-width: 1400px) */
.etherpad-container {
  width: 80%;
  margin-left: 20%;
}
```

## 1108

- 修复了插入流程图时复用官方图片插件的问题，但引入了新的问题
  - 粘贴mermaid流程图文本代码时，无法正常显示
  - 双击流程图图片时，无法出现编辑mermaid代码的弹窗
  - ~~流程图的缩放仍未实现~~

- [x] 图片标题切换显示要改成中文提示

- 修改图片悬浮工具条的文字提示为中文
  - 思路0：利用官方提供的构建多语言的方法，add/t(), webpack配置
    - add需要手动在创建editor实例前，修改`window.CKEDITOR_TRANSLATIONS`属性对象，添加键值对
    - webpack能提取出.po文件中配置的多语言翻译，但这些多语言翻译文件资源必须作为第3方包引入
  - 思路1：通过私有api获取到图标工具条的toolbar菜单项，直接修改js对象的属性
    - editor.plugins.get('WidgetToolbarRepository')._toolbarDefinitions
  - 思路2：修改缺失多语言翻译所在插件的源码，添加对应的文字翻译；但需要持续修改更新
    - \ckeditor5-image\src\imagecaption\imagecaptionui.js

## 1107

- 双击图片时，是如何出现编辑弹窗的，弹窗中提供了流程图模版
  - MermaidUI.init()方法中，通过_enableUserBalloonInteractions()注册双击事件，每次双击mermaid图片节点，都会执行showUI()，触发执行 `ReactDOM.render(<MermaidPanel />, this.element)`，会显示包含流程图模版的弹窗
  - `<MermaidPanel />`会传入初始文本代码，以及更新文本代码的方法
  - 在MaterialUI中监听`'change:code'`事件，每次文本代码code更新，都会执行insertMermaid命令(该命令会创建或更新当前的model对象)，然后触发view更新

- [x] 插入mermaid时，如何和image联系起来
  - 获取到mermaid或第三方的图片url地址后，不要手动创建img，而是修改image-plugin对应的的model数据

- [x] 自定义图片更新时，修改model还是修改view
  - 比较理想的方式是model只定义最外层结构，不定义imageBlock的实现细节
  - 可考虑在downcast过程中动态创建imageBlock的model
  - 次优的方案是修改schema，将实现细节也定义出来
  - 因为modelWriter不检查schema，所以可以在不修改schema定义的前提下，动态插入内容

- image-plugins
  - ImageToolbar
    - Instances of toolbar components (e.g. buttons) are created using the editor's component factory based on the image.toolbar configuration option.
  - ImageCaption
  - ImageStyle
    - glue for ImageStyleEditing, ImageStyleUI
    - It provides a default configuration, which can be extended or overwritten.
  - ImageResize
    - It adds a possibility to resize each image using handles.
  - ImageUpload
    - glue for ImageUploadEditing,ImageUploadUI,ImageUploadProgress
  - ImageInsert
    - Insert images via source URL
    - glue for ImageUploadImageInsertUI
  - AutoImage
    - It recognizes image links in the pasted content and embeds them shortly after they are injected into the document.
  - ImageTextAlternative
  - LinkImage

- editor.config中的配置变化时，如何rerender editor
  - 思路1: 先destroy editor实例，再创建新的editor实例
  - 思路2: 修改CKEditor的id属性，交给ckeditor5-react更新

## 1106

- 更新plugin config的方法
  - 提前设计成可开启关闭的配置项，然后添加到配置对象

- All changes in the document structure, of the document’s selection and even the creation of elements, can only be done by using the model writer.

- Currently, there is no straightforward way to override the schema preconfigured by features. 
  - If you want to override the default settings when initializing the editor, the best solution is to replace `editor.model.schema` with a new instance of it. 
  - This, however, requires rebuilding the editor.

- The role of the model layer is to create an abstraction over the data. 
  - Its format was designed to allow storing and modifying the data in the most convenient way
  - Most features operate on the model (read from it and change it).

- The view may need to be changed manually if the cause of such change is not represented in the model. 

- Technically, the data pipeline does not have a document and a view controller. 

- there is no editing upcasting 
  - because all user actions are handled by editor features by listening to view events, analyzing what happened and applying necessary changes to the model.

## 1105

- 图片目标
  - 导出data view时，去掉image部分
  - 编辑显示时，添加imageBlock的部分
  - 打开带数据的文档初始化时，添加imageBlock的部分

- 如果要用官方的image插件的功能，model包含imageBlock是最简单的方式
  - 否则，要在downcast之中手动创建元素

- 插入图片和标题的参考
  - [How to insert an image with a caption into a custom element in CKEditor 5?](https://stackoverflow.com/questions/53208435)
  - [Refreshing a CKEditor5 widget upon model changes](https://stackoverflow.com/questions/51319311)

- 流程图插入标题的自定义实现

```JS
const mermaidView = writer.createEmptyElement('img', {
  src: `https://api.editoe.com/api/mermaid/generate?data=${encodeURI(mermaidCode)}`,
});

const figcaptionElem = writer.createEditableElement('figcaption', {
  class: 'ck-editor__editable ck-editor__nested-editable ck-placeholder image__caption_highlighted',
});

writer.insert(writer.createPositionAt(container, 0), mermaidView);
writer.insert(writer.createPositionAt(container, 1), figcaptionElem);
writer.insert(writer.createPositionAt(figcaptionElem, 0), writer.createText('请输入标题或描述'));

return toWidget(container, writer, 'figure');
```

## 1104

- 如何允许新的schema
  - 作为parent，包含已有schema，allowContent
  - 作为子元素，包含在已有父元素schema中，allowedIn

- 修改model的writer参数对象 和 conversionaApi的writer属性(DowncastWriter) 不同
  - `editor.model.change((writer) => {` 在源码 @ckeditor/ckeditor5-engine/src/model/writer
    - The model can only be modified by using the writer. 
    - It should be used whenever you want to create a node, modify child nodes, attributes or text, set the selection's position and its attributes.
    - The instance of the writer is only available in the change() or enqueueChange().
    - Note that the writer should never be stored and used outside of the change() and enqueueChange() blocks.
    - Note that writer's methods do not check the Schema. It is possible to create incorrect model structures by using the writer.
  - `conversion.for( 'One-way converter' ) → DowncastHelpers` | UpcastHelpers
    - elementToElement( config = { config.model, config.view, [config.triggerBy], config.triggerBy.attributes, config.triggerBy.children } )
    - This conversion results in creating a view element.

- **UI elements are ignored by the editor selection system**.
  - the selection cannot be placed in it, it is skipped (invisible) when the user modifies the selection by using arrow keys 
  - and the editor does not listen to any mutations which happen inside your UI elements.
  - The limitation is that you cannot convert a model element to a UI element. 
  - UI elements need to be created for markers or as additional elements inside normal container elements.

- The **raw elements** work as data containers ("wrappers", "sandboxes") but their **children are not managed or even recognized by the editor**. 
  - This encapsulation allows integrations to maintain custom DOM structures in the editor content without, for instance, worrying about compatibility with other editor features. 
  - Raw elements are a perfect tool for integration with external frameworks and data sources.
  - they are considered by the editor selection and they can work as widgets.

## 1103

- 读image部分的源码
  - 分析描述性标题的实现
  - 分析多语言的实现

- 图片形式的内容如流程图是否要做个小重构
  - 是否要显示左右居中对齐、添加字幕

## 1102

- [x] 要添加全局样式去掉所有图片的左上右下操作按钮

- [x] nightly网站上最新commit未生效，右键菜单未去除插入相关菜单项，但本地运行时右键菜单已精简过了
  - 原因是pr合并到了错误的canary分支，应该合并到nightly分支
  - package-lock.json需要每次更新toe-editor的版本

- 插入图片时，图片标题添加的代码位置 captionElementCreator()
  - editoe\plugins\ckeditor5-image\src\imagecaption\utils.js 

## 1101

- 新编辑器缺少的props
  - autoSave, updateTitle

- npm发版流程
  - npm run patch 修改版本号
  - npm run release
  - npm run pub 自动创建新分支，自动push，需要手动提添加新分支的pr
  - npm自动会自动发包

## 1029

- 上传图片的问题
  - 使用的是源码定制的编辑器ckeditor5-editor-classic，而不是预定义编辑器ckeditor5-build-classic
    - 对预定义编辑器，添加自定义插件要使用extraPlugins属性
    - 对于源码定制的编辑器，直接添加在依赖项之后
  - 插入图片的command选择错误
    - insertImage -> uploadImage
  - 未实现将图片上传并保存到服务器

- data view 和 editing view的区别

- semantic views for rendering and data retrieval purposes and non-semantic views for data input.
- The view may need to be changed manually if the cause of such change is not represented in the model.
- Because the UI is organized according to the view-per-tree rule, it is clear which view is responsible for which part of the UI 

## 图片上传问题

- 上传图片到阿里云oss的逻辑不清晰

- 临时变通的思路：
  - 上传时将图片转换成base64，保存到localStorage
  - 显示时使用 data: url 前缀的形式

- 限制说明
  - 单个域名下，localStorage/sessionStorage的总大小不能超过5mb，若超出则丢弃而不会覆盖

## 1028

- 图片插件features
  - 支持拖拽上传、粘贴上传、从toolbar的图片按钮打开文件选择器上传选定图片
  - 实现本地预览预览图片，可选上传
  - 支持插入外部图片url
- 实现说明
  - 一次只能上传一张图片，暂不支持上传多张

- 实现图片上传的基本步骤
  - The images are intercepted by the image upload plugin
  - For every image, the image upload plugin creates an instance of a file loader.
  - While the images are being uploaded, the image upload plugin 展示占位符或进度
  - Once uploaded, the upload adapter notifies the editor
  - ref
    - [How To Use React Ckeditor Upload File Image With Demo and Example Codes](https://www.techgalery.com/2021/05/how-to-use-react-ckeditor-upload-file.html)
    - [CKEditor5 With Custom Image Uploader in React](https://www.alvinrapada.com/stories/ckeditor5-with-custom-image-uploader-in-react)
    - [CKEditor Image upload with Firebase and React](https://dev.to/suraj975/ckeditor-image-upload-with-firebase-and-react-1pe8)
    - [How to enable image upload support in CKEditor 5?](https://newbedev.com/how-to-enable-image-upload-support-in-ckeditor-5)

- 图片插件的问题
  - 要不要上传到后端? yes
  - 要不要支持用户输入任意图片url? no

- 流程图

```markdown

graph TD
    A-->B;
    A-->C;
    B-->D;
    C-->D;

graph TD
    A[Christmas] -->|Get money| B(Go shopping)
    B --> C{Let me think}
    C -->|One| D[Laptop]
    C -->|Two| E[iPhone]
    C -->|Three| F[fa:fa-car Car]

- User Journey Diagram

journey
    title My working day
    section Go to work
      Make tea: 5: Me
      Go upstairs: 3: Me
      Do work: 1: Me, Cat
    section Go home
      Go downstairs: 5: Me
      Sit down: 5: Me
```

## 1027

- conversion提供的3种转换方式的时机确认
  - upcast
  - dataDowncast
  - editingDowncast

- 创建block widget的基本流程
  - 设计插件和widget的层次结构：entry、editing、ui、cmd
  - 在editing中定义schema
  - 在editing中定义converter
  - 将converter细粒度定义，editingDowncast的view方法的返回值使用toWidget/toWidgetEditable
  - 继承Command，实现execute/refresh
  - 在editing中注册commands
  - 在ui中创建图标，并添加到toolbar

- 创建inline widget的基本流程
  - 设计插件和widget的层次结构
  - _defineSchema
  - _defineConverters
  - 继承Command，实现execute/refresh
  - 在editing中注册commands
  - fix position mapping 解决点击inline文字中间会抛出异常的问题
  - 创建dropdown ui，并添加到toolbar
  - 将placeholder的预定义类型在editing中定义，而不是硬编码

## 1026

- 创建简单plugin的基本流程
  - 确定插件功能目标、依赖关系、数据流或架构
  - 继承Plugin class
  - 在init方法中创建ui
  - 在ui组件中注册execute事件处理函数
  - 通过editor.model.insertContent插入内容到目标位置

- 状态放在plugin，还是放在command
  - 放在plugin，可方便获取
  - 放在command，可方便修改 refresh() --> this.value
  - answer
    - 一般放在command，方便从外部触发修改
    - ui相关状态一般用react管理，而不是ckeditor
    - 编辑器内容相关状态，还可以考虑放在attributes

- EmitterMixin、ObservableMixin 的区别
  - 用的很少

- 怎么知道要将view放在plugin的位置
  - editor.model.insertContent的第2个参数指定插入位置

- 如何使用自定义react组件定制ui
  - 参考文档示例，思路是实现ui插件时ui渲染部分使用react组件
