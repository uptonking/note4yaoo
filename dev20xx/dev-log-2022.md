---
title: dev-log-2022
tags: ['2022', dev-log, dev-xp]
created: '2022-05-24T17:56:50.063Z'
modified: '2022-05-24T17:57:03.592Z'
---

# dev-log-2022

# dev-xp

# dev-04

## 0429

- todo
  - subPage悬停菜单消失了
  - 基于slate编辑器实现添加和清除富文本格式

- 废弃 getWorkspaceConfig，自定义数据的读写统一用 get/setDecoration

- 搜索的初步实现
  - 搜索根据索引实现，而不是直接搜索源数据
  - 元数据更新时，搜索结果是即时反馈的
  - page内容更新时，搜索结果要等待一段时间

- 在代码实现时，有疑问的、做决策花了很多时间的，要文档记录、然后讨论

- pageEditorBlock.getChildren 获取所有直接block
- workspaceDBBlock.getChildren ?

- redo/undo分2类
  - 文字加减
  - 异步：上传文件、删除文件

- ctrl+a 全选是否要选上标题
  - notion选上
  - 飞书第二次ctrl+a才会选上标题

- 检查所有block的backspace、enter按键后的光标位置
  - 特别是todo list

- 从block查找其他block都通过搜索来实现

- 富文本相关文字创作完全依赖slate实现

- divider在回删时，保留分割线且删除到上个block，参考notion

## 0428

- 在架构上分离 dbBlock、businessBlock、editorBlock
  - dbBlock是block在存储层的存储结构和实现
  - businessBlock是block在业务层的较为通用的数据结构，通过dbBlock计算或转换得到
  - editorBlock是block在具体编辑器业务层的数据结构，是编辑器直接存取的业务数据

- 将数据转换和计算放到组件层，还是放在service层？
  - 一个判断方法是，其他地方需不需要用原始数据？转换后的数据？
  - 切换到react-native后，service需不需要改动？改动大不大？

## 0427

- block-editor插件重构
  - 修改 defaultValue
  - 修改 get properties/fields
  - 新增 PageModel PluginModel
  - 💡 将db操作重构为传统CRUD应用的service层

## 0426

- dev-to-daily-notes
  - 点击每个日期时，显示当天的自动生成的统计page。只读？
  - 显示什么内容？
    - todo list 列表
    - 文档创建修改记录

- debug在特定版本浏览器才会出现的问题
  - 首先在同一台电脑上多试几个浏览器，如果只在一个浏览器出现问题，在其余浏览器是正常的，则说明是浏览器的问题，而不是代码的问题
  - 在问题浏览器上debug时，发现问题是y-websocket的监听4个事件只处理了2个漏了2个导致的，但单步debug调试能锁定问题的位置和异常值

## 0425

- dev-to-calendar-heatmap
  - 🤔 用户昨天只新建了一篇文章A，日历上显示最浅的颜色，今天把文章A删除了，要不要更新日历颜色
    - 每次登录系统根据db数据动态计算，所以删除page后，颜色就变浅或消失了

- databse需求讨论及数据结构
  - notion中2个database跨表格拖动行时，对非文本列，根据列定义名称匹配
    - 若将tableA的tags列拖到tableB的tags列，若OptionA在tableB中也存在，则显示，若不存在，则OptionA对应的列显示为空
  - 要考虑支持列名的国际化
    - 列名不能是字符串，要考虑方便用户添加翻译配置，使用对象
    - 交互实现可以用2个输入框
  - 省略的效果就是折叠展开，不支持部分折叠展开

- 🤔 列定义、tags的动态修改放在page级别，还是workspace级别？
  - 参考现有产品的设计
  - 一个page的tags/column变动了，其他page也要变？
  - tags跟随page?
  - 💡 讨论阶段性结论
    - 在跨group层级拖动block时，会先合并列字段，始终都是增量合并的方式，若存在同名列，则新建列col(1)
    - 根据col名称合并

- 目前db搜索所有content
  - 要优化对元数据的搜索

- 对无序列表，一行是block
  - 切换成看板视图，子任务显示进度
  - 切换成列表视图，子任务在单元格？缩进子列表？

- 用户选中任意元素的组成 block-group
  - 隐式创建group的规则取舍太多
  - 可以先实现显式手动创建group，在体验中继续优化逻辑

- 默认一个page所有内容都在一个group

- local-first要考虑用户断网的场景

- 有对手比没有对手好。接下来我们的每一步都有honourable的对手：
  - block transform ——》干死notion和monday，asana
  - page transform ——》 干死miro和mural
  - 版本控制 ——》干死almanac
  - blockdb加密协作，selfhost ——》干死skiff和anytype
  - 网页发布时编辑器套壳editor ——》干死super和simple.ink
  - automation，流程自动化 ——》干死google docs和uipath

## 0422

- daily-note初步实现
  - 查询某一天的所有pages，基于search api实现
  - 搜索基于tag实现
  - 前端blockdb的搜索实现，直接用sql，还是自定义dsl
    - 倾向于类似mongodb的查询dsl，完善类型，查询简单

- daily-notes的数据源包括本地数据库和服务端数据2部分
  - 本地直接读取
  - 🤔 服务端数据可以直接请求数据、可以先从数据库请求然后前端从本地数据库

- 登录时需要fetch recent workspaces，因为有多设备同步的问题
  - 若用户先在设备A使用了spaceA，然后在设备B使用了spaceB，当再次登录设备A时应该进入spaceA

- PageTree小结
  - 标题支持点击和拖拽事件
  - 支持保存和恢复折叠展开状态

- dnd-kit-onClick 失效的问题
  - https://github.com/clauderic/dnd-kit/issues/296
  - useSensor(PointerSensor, { activationConstraint: { distance: 10, }, }); 

- pm-features
  - block transform: notion/monday/asana
  - page transform: miro/mural
  - version control: almanac
  - self-host with encryption: anytype/skiff
  - publish editor: super/simple.ink
  - automation: uipath/google docs

### oneOnOne-terry-google-docs-产品矩阵

- 2005年收购 wirtely(doc)、xl2web(sheet)、DocVerse(collab)、QuickOffice(mobile)
- 2015年google工程师回国，本地化、替换docker，发布一起写
- 2017年快手收购一起写
- google-docs控制台调试，save?id
- 快手，?sid=
- doc核心 
  - 排版gui
  - 数据交换协作协议
- google办公套件
  - drive
  - document
  - sheet
  - ppt
  - form
  - cloud file
- 产品一体化的研发趋势
  - 黑盒卡片，集成im、figma
  - 编辑器能力插件组合，学术版、设计版，类似vscode扩展包、ckeditor打包了四五种

- 壁垒
  - gui架构
  - 排版器
  - sheet比doc更复杂

## 0421

- 登录时，PageTree显示untitled

- PageTree 数据结构和更新分析
  - 更新标题名称时，异步通知再重新读取标题
  - 更新标题顺序层级时，先更新缓存，再异步保存

## 0420

- PageTree现有组件的问题
  - 所有内层叶节点默认展开，而不是记住折叠状态

## 0419

- dev-to
  - [x] 修改获取初始workspace的流程，优先使用本地找不到，可以不从api获取

- 大日历暂停

- 先实现文章数据保存和恢复

- 重构编辑器的load-save
  - .get()
  - .set()
  - 去掉 .getContent()

## 0418

- discussion
  - 小日历接入实际创作数据时，日历颜色根据什么指标确定？创建、修改文件数量？
    - 日历颜色分3级，分级指标如何确定？ 3/6/9？
  - daily-notes数据具体包含哪些数据？ pin+todo-task+activities/comments
    - 每天的daily-notes文档是动态计算生成的？还是把前一天的算好了存起来？若预先存储长期会占用空间？
  - 顶部导航条什么时候显示7天日期？因为默认显示2个视图切换按钮
  - 左侧日历热力图切换弹窗大日历？全页的大日历还存在吗？

- dev-to
  - 重写PageTree正在进行中

- google-calendar的格式已成为协同类产品的基建
  - 功能参考
  - 导入导出日程

- 编辑器的数据与无状态react组件分离
  - `<ReactComp blockId={dbBlockId} />` 抽离出react组件
  - 让看板组件、日历组件能够在editor里面用，也能单独使用

- 白板和editor集成的额外信息
  - 白板shape的位置信息
  - shape所属group

## 0415

- dev-to
  - 前端项目请求api通过proxy代理到线上服务端
  - PageTree组件重写
  - 后端登录流程熟悉

- @nrwl/web:dev-server 的配置项不包含proxy, packages\web\src\executors\dev-server\schema.json
  - 但其他文档有个单独的页面介绍了配置方法，proxyConfig
  - 对照webpack-dev-server的文档，发现沿用了其配置
  - nx的代理配置不在options页面，而在单独的配置教程页面，要先搜索，再提问讨论

- 多个useEffect尽量不要依赖执行顺序
  - 有时候，deps依赖项过多，effects就会比预期的先执行，结果常是显示旧数据

## 0414

- dev-to
  - 本地配置代理，直接使用后端在线服务
  - 🤔 本地是否要实现免登录

- daily-notes/calendar-view
  - 作为文档的入口，比文档更高一级

- workspace、page 的content可以用来放metadata
  - 普通block的content用来放内容

## 0413

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

- dev-to
  - workspace flavor类型的block用来干嘛的
    - workspace与page是如何关联的
  - page flavor类型的block应该是类似以前的doc
    - 如何设置title、author、lastUpdate、create
  - 迁移到新db后更新目录树的数据源

- 若没有workspace，则新创建默认workspace

- block flavor  
  - workspace, page, text, title, comments, tag, reference, video, audio, image

- blockdb结构
  - workspace、page、block
  - page.insertChildren(block1); 

- 实现数据存储和操作时，要考虑 编辑器多实例的问题

- [wsl安装mongodb教程](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database)

- caddy类似 nginx

## 0412

- 浏览器滚动条宽度
  - The default scrollbar width can range anywhere from 12px to 17px. 
  - Webkit browsers also have the ability for the user to configure scrollbar widths. 
  - Webkit browsers, such as Chrome can have custom scrollbars that can have any size scrollbar.

## 0411

- 数据请求的问题
  - api函数放在哪里
  - 有没有比拆分更好的方式

- 💡 发现将 useUser 和 useSpaces 合并为一个hook后能够减少请求次数，同时降低复杂度，流程更清晰

- dev-to
  - 推进产品上aws

- 白板的激光笔设计，笔迹3S后自动消失

## 0408

- dev-to 完善本地数据库操作和文档树操作的逻辑
  - 文档树的拖拽按钮被挡住了，重构为拖拽标题改变顺序
  - 实现左侧面板滚动条

- linear
  - 最常用的单位是issue
  - 看板常用于浏览数据，而不是修改数据
- height
  - 完全任务的动效，提升体验
- cron
  - 专注于日历，日/周/月

## 0407

- 研发方案讨论
  - 全局共享dbClient的方式，共享editor对象的方式
  - documentdb vs blockdb，该用哪一个
  - 全局状态管理

- 协作的粒度是block
  - block层级 workspace-page, page, sub-page
  - PageTree优先级很高

- 文档树旧bug
  - 拖到最下面时，会弹到最上面

- 产品
  - workspace 数据
  - login
  - daily notes

- 左侧面板需求讨论
  - 面板内容如PageTree页面树太高时、太宽时如何显示和交互？
    - 太高时，是否显示滚动条
      - notion一直会显示定制滚动条
    - 太宽时，总是显示一行？
  - 页面树每行
    - 在鼠标悬浮时，应该显示哪些内容
    - 拖拽的部分是标题文字，还是尾部手柄

- PageTree 组件需求分析
  - 每行内容为👉🏻️ 折叠按钮 + 文档图标 + 标题 + 悬浮操作菜单
  - 折叠展开
  - 拖拽移动实现改编顺序和层级
  - 拖拽时显示位置提示条
  - 每行末尾为悬浮操作菜单

- doc-db执行db.set时异常 insert a new version before save
  - 不能用 doc.addVersion('')
  - 应该用 doc.addVersion(' ')

- react-router
  - useNavigate() may be used only in the context of a `<Router>` component. 
  - I think duplicated react-router-dom is the problem. Removing react-router-dom can be the solution

## 0406

- 日历问题
  - 选择年份后，星期那一行会被挡住，经排查是flex-column的弹性项目height不生效的问题

- 还原设计稿时，注意卡片div2的margin是32px的代码实现方式， div1 > div2 > div3
  - div2的margin为16，div2的内容div3如span的margin也为16

## 0404

- dev-to
  - calendar-heatmap细节调整到完全还原设计稿
  - 迁移旧项目文档树组件到新产品，并mock数据
  - 完全理解dnd-kit的原理，设计实现多维表格的拖拽列宽度
    - drag和layer的工作以前都做过，但没系统地总结
  - 重新实现calendar-heatmap组件

## 0402

- 当div定义宽度和实际宽度不同时，排查方向应该是作为flex容器内项目的grow或shrink比例生效了
  - 若要去掉自动放大缩小，flex可取值 auto (1 1 auto) 和 none (0 0 auto)

- 注意图标按钮写法
  - `<IconButton><SvgIcon /></IconButton>` 如果只把svg设为visibility： hidden，那么外层IconButton的hover仍然会存在，不符合预期交互

## 0401

- 顶部导航条的元素依次是
- HeaderStart
  - logo图片
  - 侧边菜单图标
  - 版本记录图标 + 版本文字
  - 文章标题，可选emoji
- HeaderMiddle
  - 文章页
    - 视图切换按钮：文章视图、白板视图
- HeaderEnd
  - 用户下拉菜单
  - 打开文章面板

- `升级到pro版`的元素的定位是fixed ？
# dev-03

## 0331

- 日历热力图沟通
  - 不显示当天
  - 颜色分3级

- style9的样式keys只支持 at-rules or pseudo selectors
- material v5正在将部分组件迁移到付费plan
  - 已迁移 data-grid、tree-view、date-picker
  - 迁移中 charts、sparkline、gauge

## 0330

- 为什么要自定义calendar组件 / mui-组件DatePicker的问题
  - [x] 需要参考现有组件实现i18n
  - [x] 自定义样式更灵活，如日期背景色、日期背景形状、日期小红点
    - mui v5的日期选择器内层组件会丢失className，变通方案是使用普通css selector
    - 自定义切换年月图标、星期与月份文字
    - 定制日期选择的方块大小、方便与头部星期几对齐，同时控制高度增加时不会显示竖直滚动条
  - 定制功能更方便，如鼠标悬浮提示
    - 定制选择年份的面板的内容，定制打开年份选择器时显示的初始年份(StaticDatePicker)
  - eg: Customized day rendering 👉 StaticDatePicker 没有弹出层
    - renderDay属性类型是function
  - eg: Dynamic data 👉 DatePicker
    - renderLoading属性显示日期空白占位符
    - 切换月份时更新highlightedDays
    - renderDay属性值函数返回的是封装过PickersDay的组件
  - eg: Sub-components 👉 CalendarPicker, MonthPicker, YearPicker
    - rendered without a wrapper or outer logic (masked input, date values parsing and validation, etc.).
    - 没有renderDay属性

- StaticDatePicker 源码结构
  - Picker
    - CalendarPicker
      - YearPicker
      - MonthPicker
      - PickersCalendar 选择日期

- PickersCalendar 源码结构
  - PickersCalendarWeek
    - PickersDay
      - children

## 0329

- 两个daily notes
  - 左侧calendar，日历热力图
  - 上侧全屏calendar，交互细节还要设计和修改

- cloverapp的daily notes文档是自动创建的
  - subscription events
  - overdue tasks

- dev-xp
  - 用户可编辑/不可编辑，作为系统内置的filter实现
  - 本地数据库是否都要支持pin、第三方导入的？
    - 实现时讨论，本地pin预缓存然后合并云端数据源

- [TS2322: Type 'Timeout' is not assignable to type 'number'](https://stackoverflow.com/questions/55550096)
  - You could try with using `window.setTimeout` instead of just `setTimeout`, this way the typescript one will be explicitly used
  - `let timeoutId: null | ReturnType<typeof setTimeout> = null` 显式声明
    - timeoutId = setTimeout(fn, 1000)

- 遇事不决，先按 F12 > Application/应用程序 > 存储/Storage > 清除站点数据 Clear site data

## 0328

- fix类型后，出现编辑器持续重复渲染，且无法正常工作的问题
  - 排查原因，先稳定复现bug

- 新编辑器抽象层次
- app 
  - useDatabase => `<BlockEditor db={database} />` 传递数据库操作实例
- block-editor
  - 定义block-editor的vdom结构，以及初始化editor对象
  - EditorRoot, div, RenderBlock
  - createDefaultEditor -- createStandaloneEditor

## 0327

- 浏览器中人工合成（synthetic）的事件派发（dispatch）是同步执行的，包括执行click()和dispatchEvent()这两种方式。
  - Unlike "native"(dom) events, which are fired by the browser and invoke event handlers asynchronously via the event loop, dispatchEvent() invokes event handlers synchronously

```JS
console.log('本轮任务');

new Promise((resolve, reject) => {
  resolve(3)
}).then(() => {
  console.log('本轮微任务');
});

// 💡️ 通过click方式触发的事件是同步执行的，只有浏览器自己触发的事件才是放在一个 macrotask 里执行的。
document.getElementById('div').addEventListener('click', () => { console.log('click'); })
document.getElementById('div').click()
```

## 0326

- block-editor新编辑器类型补充
  - 难以补充类型的use case，主要是深层路径属性的取值
    -  const element = editor?.children?.[path[0]]?.children?.[path[1]];

## 0325

- ts noImplicitAny的解决方法
  - // @ts-ignore

- Property 'current' does not exist on type 'ForwardedRef
  - [React fordwardRef with typescript](https://stackoverflow.com/questions/69503174)
  - `type ForwardedRef<T> = ((instance: T | null) => void) | MutableRefObject<T | null> | null;` 类型定义
  - Therefore attempting to just access .current, without doing some type checking, won't work because functions do not have such a property.

```jsx
// This should work:

const ProfileMenu = forwardRef<HTMLInputElement, PropsDummy>((props, forwardedRef) => {
  if (forwardedRef != null && typeof forwardedRef !== 'function') {
    console.log(forwardedRef.current);
  }
  
  return (
    <div className="App" ref={forwardedRef}>
      <h1>Hello there</h1>
    </div>
  );
});
```

## 0324

- nx
  - nx build myapp --skip-nx-cache

- 使用nx编译修改源码后，nx在cli编译仍然报错
  - src/lib/Text/Text.tsx(459, 25): semantic error TS7030: Not all code paths return a value.
  - 原因是，nx在命令行报错针对的是转译后的代码；
  - 要修改源码错误，应该以ide提示的problems/error的行数位置为准

- typescript playground可以打印出类型变量定义的结果，使用 `// ^?` 然后鼠标停在问号后就可以显示类型定义的结果
  - 如果不能显示，可以刷新页面，之后就能显示
  - [打印类型的示例](https://www.typescriptlang.org/play?pretty=true#code/C4TwDgpgBAqgdgSwPZwPIDMAqBXMAbCAZygF4BYAKCmqgB8oBtAIgAUE4BrJgGilYEM4wABYQATkwC6lGnUZMASkn4ATHnwXY4ccVJk16zNh37qmAYWHY9FSqEhRUAIwBWEAMbAAYmKQBbHHwiAB5AgmIIAA9gCDgVYgZCYDF2AHNeJJS4VMkAPlIoAG99agYw6HYocuJ+YnKGAAZJSQAuKtwCBgBGaQoAXygAMiK+yjtwaAUibDxgAuc3Tx9-auD4ZDQsDqJcygB6PdkAPQB+MYp7aEwJroKpwhm5+gByTLTngG59w5pToA)

## 0323

- pnpm: fast, disk space efficient package manager
- features
  - fast
  - efficient
  - support monorepos
  - strict access to pkg with non-flat node_modules

- nx: build system with first class monorepo support and powerful integrations.
- features
  - Best-in-Class Support for Monorepos
  - Integrated Development Experience
  - Rich Plugin Ecosystem

- ckeditor顶部工具条的dropdown被页面顶部导航栏挡住的原因
  - 编辑器的父容器使用了自定义滚动条，外层div-overflow：hidden，内层div-overflow：scroll
  - 临时的解决办法：外层 overflow：auto，内层div-overflow：auto，但此时编辑器无法滚动了
  - 💡排查元素被部分挡住的问题，思路是查找position-absolute的元素、overflow-hidden的元素

- 替换ckeditor图标的2种方法
  - 1. 编译器替换：new webpack. NormalModuleReplacementPlugin
  - 2. 运行期替换：自定义插件 localizedBoldPlugin 
    - boldButton.icon = getIcon( 'bold', locale.language );
    - 适合做国际化图标合文字
    - https://github.com/ckeditor/ckeditor5/issues/1613
  - NormalModuleReplacementPlugin site:github.com/ckeditor/ckeditor5
  - 在com-editor项目替换ckeditor图标完成后，在前端项目却仍显示ckeditor图标的解决办法
    - 在com-frontend项目重复替换图标的逻辑

```SCSS
// 修改cke工具条文字
& .ck.ck-toolbar__items .ck-heading-dropdown {
    & .ck-button_with-text .ck-button__label{
      color: #133b75;
    }
}
```

## 0322

- milestone 交付jnu-editor编辑器
  - not-yet
    - 将bibtex插入编辑器的逻辑实现有问题，如何只在光标点击editor内容后才执行插入bibtex的command，否则就会出现现在的问题，鼠标若不再editor中点击一下就不执行该逻辑

### 多维表格和看板-pending

- 工作记录在20211220之前
- my-agenda
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

### products-old-dev-log

- 重构题头部分
  - [x] 更换emoji picker
  - ~~字段列表分类型重构~~
- 编辑器
  - blockquote插件中的换行，每次刷新页面后，中间的空行会加一个
    - 空文档无此问题，复制示范文档会出现此问题
  - 图片按回车不能换行
  - [x] 编辑器工具条第一个查找替换图标是烂图标，左上部分都是黑色
- 文章页
  - [x] 去掉水平滚动条
  - [x] 使用CustomScrollbar后，最好去掉浏览器默认的竖直滚动条
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

### products-old-not-yet

- my-agenda
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
- workspace如何设计
  - 本地仓库、云端仓库
  - 我的仓库、公共仓库
  - 是否可参考github仓库？
- 文档核心功能
  - 双链展示
  - 分支文档
  - 工作空间内搜索
- ux交互设计
  - 落地页/未登录时的宣传页
  - 个人主页/首页
  - 工作空间页
  - 国内环境不适合对接github，可考虑百度网盘
- 新首页设计与工作计划
  - [x] 首页使用~~类似workspace的设计~~，快捷菜单跳转到workspace
  - [x] 布局改为左侧边栏
  - [x] 文档列表只显示创建的文件，最近操作的文档要跳转到单独页面
  - [ ] 文档列表：pin置顶一个日期
- 编辑器工作计划
  - ~~左侧目录显示参考文献锚点~~
  - ~~编辑器首页顶部显示图片~~
  - 日期时间的处理
    - 可参考日历组件的实现方案
  - 流程图bug
    - ~~复制粘贴后，就变成图片，无法编辑代码了~~
- 检查图片的接入方式
  - toolbar打开文件选择器
  - 拖拽本地图片到编辑器光标位置
  - ctrl+v粘贴图片到编辑器
- 图片上传的问题
  - ~~将 同步执行的createObjectURL 改为 异步执行的 `FileReader.readAsArrayBuffer` + `new Blob([arrayBuffer], { type: "mime/type" })`~~
  - 上传已经以前已经上传过的图片时，是否保存了2份数据，存在冗余
  - 首次渲染图片时，由于blobUrl失效了，控制台会报错
    - blob:http://127.0.0.1:4001/223c5400-55e2-4ac7-b936-574b47cd0201 net::ERR_FILE_NOT_FOUND
  - 考虑直接将数据库中docId存储到编辑器图片model
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

## 0321

- editor自动保存失败
  - 复现方法
    - 在toe-editor仓库不能复现，说明问题出在前端应用层
    - 当光标闪烁时，如光标在标题处刚修改完闪烁时，立刻刷新页面，就能复现
  - 原因排查
    - yjs的set不是原子操作，先删除，再添加；当删除后，文档数据库gc发生，文档内容就变为空了的，之后执行的添加操作就成了添加undefined，内容变成空

```
  Uncaught (in promise) TypeError: Cannot read properties of null (reading 'forEach')
    at Bs (index.js:9:66961)
    at Fs (index.js:9:67618)
    at index.js:9:83227
    at ps (index.js:9:57845)
    at yn.insert (index.js:9:83194)
    at yn._integrate (index.js:9:82305)
    at Bn.integrate (index.js:9:91244)
    at Fn.integrate (index.js:9:94802)
    at qs (index.js:9:68815)
    at index.js:9:71751
```

- react-table virtualized之后要检查功能
  - scroll to index
  - search/filter
  - row selection
  - 示例参考
    - https://codesandbox.io/s/cubs-react-virtualized-resizable-sortable-filterable-table-x77iw
      - 支持 virtualized、global filter、row selection

## 0320

- js处理私有属性的方法
  - ❌️ 名称以 _ 开头
    - python、dart也有此习惯
    - ide提示时很清晰
    - microsoft/google都不推荐这种方式
  - ✅️ 将私有属性或方法的声明全放在最前面或最后面
  - ✅️ es6新提案支持class的属性名或方法名以#开头代表私有
  - ❓️ 使用Symbol类型的值作为私有属性名
    - 使用反射api可以获取到Symbol值

- prosemirror offline / local-first

## 0318

- 新品ui交互设计
  - block工具条、多维表格工具条
  - 将多维表格转换成todo-list，多维表格多余字段可折叠展开
  - 无序列表、有序列表，实现为可拖动的树
  - 每个block可外挂插件能力，缩进、可折叠、设置人、设置时间

## 0317

- 交付测试问题
  - bibtex文中引用问题
  - 登录后取出空白文档
  - 现在正在有人编辑的前端实现

- css选择器选择style属性的方法
  - div[style*="display:block"]

## 0316

- bibtex列表需要虚拟化
  - 去掉竖直滚动条
  - 避免每次添加bibtex后刷新数据，列表重渲染后会跳转到顶部的问题
  - 跳转到第一条就很简单

- Shouldn't it be when useRef.current changes, the stuff in useEffect gets run?
  - Short answer, no.
  - react组件rerender的原因：
    - prop变化
    - state变化
    - parent rerender

```JS
export default function App() {
  const myRef = useRef(1);
  useEffect(() => {
    // ⚠ myRef.current变化后，effect不会执行
    console.log("myRef current changed"); // this only gets triggered when the component mounts
  }, [myRef.current]);
  return (
    <div className="App">
      <button
        onClick={() => {
          myRef.current = myRef.current + 1;
          console.log("myRef.current", myRef.current);
        }}
      >
        change ref
      </button>
    </div>
  );
}
```

## 0314

- dev-plan
  - bibtex支持更多类型
  - 有时插入bibtex不会触发文末参考文献的更新
  - bibtex refList 可以添加同名文件，然后控制台会打印异常信息
  - 点击标题名跳转路由后，文末参考文献消失了，为什么
  - undo-redo 未处理恢复和删除参考文献、双链的情况，文末参考文献也应该同步更新
  - [ ] 双链从文中删除时，却没有从尾部删除
  - [ ] 默认字体修改为衬线体
  - [ ] 修复字体突然变小的问题
  - [ ] 定制标题样式
  - [x] ~~编辑器中普通双链文章也无法点击跳转了~~，url也变化，但需要手动刷新浏览器

- 需求讨论
  - 其他人有权限删除我的文档
  - 更新bibtex的流程，推荐先删除再添加，如一个book bibtex，开始没有chapter，后面添加了chapter，那系统会认为是2条文献，对于title/booktitle/chapter字段的增删默认认为是2条

- 不能稳定复现的bug
  - 文档树一直显示转圈加载中

```bibtex
@inbook{CitekeyInbook,
  author    = "Lisa A. Urry and Michael L. Cain and Steven A. Wasserman and Peter V. Minorsky and Jane B. Reece",
  title     = "Photosynthesis",
  booktitle = "Campbell Biology",
  year      = "2016",
  publisher = "Pearson",
  address   = "New York, NY",
  pages     = "187--221"
}

@phdthesis{CitekeyPhdthesis,
    address = { Stanford, CA },
    author = { Rempel, Robert Charles },
    month = { 06 },
    school = { Stanford University },
    title = { Relaxation effects for coupled nuclear spins }
}

@inbook{test,
  author={Grandstrand, O.},
  year= 2004, 
  chapter={Innovation and Intellectual Property Rights}, 
  editor = {J. Fagerberg and D. C. Mowery and R. R. Nelson}, 
  title= {Oxford Handbook of Innovation}, 
  publisher= {Oxford University Press},
  address= {Oxford}, 
}

```

- continue和break支持在各种for循环中使用
  - By loops I mean for, for...in, for...of, while and do...while, not forEach, which is actually a function defined on the Array prototype.
  - forEach中要用return

## 0311

- 🤔 debug为什么删除bibtex失效的问题
  - 原因出现在useEffect里面注册db更新的监听器时，每次add后，马上就remove了
  - 解决方法是只在组件卸载时移除监听器
  - 如何定位此问题
    - a. 用浏览器的debug工具，发现useEffect的cleanup函数被执行多次
    - b. 打印注册监听器和移除监听器的log，观察数量不对应
  - The clean-up function runs before the component is removed from the UI to prevent memory leaks. Additionally, if a component renders multiple times (as they typically do), the previous effect is cleaned up before executing the next effect.

## 0310

- bibtex列表和文末文献列表都应该使用ErrorBoundary拦截局部错误，避免整个页面坏掉
  - 也可以完善解析容错的逻辑

```bibtex
@article{CitekeyArticle,
  author   = "P. J. Cohen",
  title    = "The independence of the continuum hypothesis",
  journal  = "Proceedings of the National Academy of Sciences",
  year     = 1963,
  volume   = "50",
  number   = "6",
  pages    = "1143--1148",
}

@book{CitekeyBook,
  author    = "Leonard Susskind and George Hrabovsky",
  title     = "Classical mechanics: the theoretical minimum",
  publisher = "Penguin Random House",
  address   = "New York, NY",
  year      = 2014
}

@booklet{CitekeyBooklet,
  title        = "Canoe tours in {S}weden",
  author       = "Maria Swetla", 
  howpublished = "Distributed at the Stockholm Tourist Office",
  month        = jul,
  year         = 2015
}

@inbook{CitekeyInbook,
  author    = "Lisa A. Urry and Michael L. Cain and Steven A. Wasserman and Peter V. Minorsky and Jane B. Reece",
  title     = "Photosynthesis",
  booktitle = "Campbell Biology",
  year      = "2016",
  publisher = "Pearson",
  address   = "New York, NY",
  pages     = "187--221"
}

@manual{CitekeyManual,
  title        = "{R}: A Language and Environment for Statistical Computing",
  author       = "{R Core Team}",
  organization = "R Foundation for Statistical Computing",
  address      = "Vienna, Austria",
  year         = 2018
}

@unpublished{CitekeyUnpublished,
  author = "Mohinder Suresh",
  title  = "Evolution: a revised theory",
  year   = 2006
}

@proceedings{CitekeyProceedings,
  editor    = "Susan Stepney and Sergey Verlan",
  title     = "Proceedings of the 17th International Conference on Computation and Natural Computation, Fontainebleau, France",
  series    = "Lecture Notes in Computer Science",
  volume    = "10867",
  publisher = "Springer",
  address   = "Cham, Switzerland",
  year      = 2018
}

@inproceedings{CitekeyInproceedings,
  author    = "Holleis, Paul and Wagner, Matthias and Koolwaaij, Johan",
  title     = "Studying mobile context-aware social services in the wild",
  booktitle = "Proc. of the 6th Nordic Conf. on Human-Computer Interaction",
  series    = "NordiCHI",
  year      = 2010,
  pages     = "207--216",
  publisher = "ACM",
  address   = "New York, NY"
}

@incollection{CitekeyIncollection,
  author    = "Shapiro, Howard M.",
  editor    = "Hawley, Teresa S. and Hawley, Robert G.",
  title     = "Flow Cytometry: The Glass Is Half Full",
  booktitle = "Flow Cytometry Protocols",
  year      = 2018,
  publisher = "Springer",
  address   = "New York, NY",
  pages     = "1--10"
}

@mastersthesis{CitekeyMastersthesis,
  author  = "Jian Tang",
  title   = "Spin structure of the nucleon in the asymptotic limit",
  school  = "Massachusetts Institute of Technology",
  year    = 1996,
  address = "Cambridge, MA",
  month   = sep
}

@phdthesis{CitekeyPhdthesis,
  author  = "Rempel, Robert Charles",
  title   = "Relaxation Effects for Coupled Nuclear Spins",
  school  = "Stanford University",
  address = "Stanford, CA",
  year    = 1956,
  month   = jun
}

@techreport{CitekeyTechreport,
  title       = "{W}asatch {S}olar {P}roject Final Report",
  author      = "Bennett, Vicki and Bowman, Kate and Wright, Sarah",
  institution = "Salt Lake City Corporation",
  address     = "Salt Lake City, UT",
  number      = "DOE-SLC-6903-1",
  year        = 2018,
  month       = sep
}

@misc{CitekeyMisc,
  title        = "Pluto: The 'Other' Red Planet",
  author       = "{NASA}",
  howpublished = "\url{https://www.nasa.gov/nh/pluto-the-other-red-planet}",
  year         = 2015,
  note         = "Accessed: 2018-12-06"
}

```

## 0309

- 异步保存编辑器数据到本地数据库，导致新数据被旧数据覆盖的问题
  - 先解决新数据一定要覆盖旧数据的问题，用闭包
  - react组件useEffect如何书写节流防抖，应该包装请求方法，而不是包装setState
    - [React use debounce with setState](https://stackoverflow.com/questions/60789246)
      - 示例将防抖过的请求方法声明在了react组件之外，算是一个普通的js方法
      - [debounce in useEffect](https://stackoverflow.com/questions/61785903)
      - [React Hooks 搞定 Race Condition](https://segmentfault.com/a/1190000019893237)

```JS
 useEffect(() => {
   const saveContent = async () => {
     console.log(';; save编辑器数据-闭包 ', content);
     const title =
       new DOMParser().parseFromString(content, 'text/html').querySelector('h1')?.innerText || 'No Title';
     await docInstance.save(content, { metadata: { title } });
     console.log(';; save完成后编辑器数据 ', await docInstance.getDecodedContent());
   };
   if (content !== undefined) {
     saveContent();
   }
 }, [content, docInstance]);
```

```JS
const saveContent2 = useCallback(
  throttle(async (text) => {
    console.log(';; save编辑器数据-闭包 ', content);

    const title =
      new DOMParser().parseFromString(text, 'text/html').querySelector('h1')?.innerText || 'No Title';
    await docInstance.save(text, { metadata: { title } });
  }, 2000),
  [docInstance]
);

useEffect(() => {
  if (content !== undefined) {
    saveContent2(content);
  }
}, [content, docInstance, saveContent2]);
```

## 0307

- VM827:1 Uncaught TypeError: oo is not iterable at anonymous:1:21
  - for (const [k, v] of oo) { console.log(k, v)}
  - 应该使用 for-in

## 0306

- dev-plan
  - [x] 从侧边栏插入bibtex到编辑器时，应用层必须执行 addRef，因为编辑器的command也没有
  - [x] 文末参考文献按作者、年份排序
  - [x] 解决数据请求切换到listener模式后编辑器rerender过多的问题
    - 解决办法 debounce
  - [x] bibtex未显示页码
- 🤔️ 排查添加bibtex需要点击2次的问题 和 文末参考文献无法显示的问题
  - console.log打印出来的是引用，其实打印时刻是3，后面变成了4
  - 👉🏻️ 问题出在数据库层

```JS
// ⚠️️ 获取一篇文章的ref需要传递额外的参数 resolve: 1
(await editor.db.get('1e98d1b3-35d9-47e3-94c0-f7f78d7a0ac7', { resolve: 1 })).getRefsByType('binary')
```

## 0305

- 排查图片无法显示的问题，依次检查渲染层、数据库层
  - 发现编辑器初始化的数据丢失了图片信息
  - 此bug有时不会复现
  - 在frontend项目也能复现出编辑器初始数据图片model缺少源数据id信息

```JS
const docContent = await doc.getDecodedContent();
console.log(`editor取回的数据1`, docContent);
```

## 0304

- dev-plan
  - [x] 完善所有文档列表
    - [ ] 快速查看我的文档
    - [ ] 当前编辑的文章，应该高亮显示？ 不许删除？
    - [ ] 在文档列表点击当前文档时，应当不跳转路由
    - [x] 重构更多操作按钮组
    - [x] 新建文档操作应该传入类似bibtex的数据
      - 新建文档传入bibtex数据后，侧边栏bibtex初始化时search type reference却搜索出来了
    - [x] 文档树和文件列表数据同步
      - 通过双链创建的新文章能立即显示在文档列表，但通过新建按钮创建的文档不会立即显示在文档列表，需要先输入标题
  - [x] 从侧边栏bibtex列表中删除项目
  - [x] 添加bibtex后，未实时取到数据，应该在应用层，还是在数据库层实现？
    - 问题出在数据库层
  - [x] fix 默认显示文末参考文献
  - [x] 通过新建文档按钮创建的新文档没有出现在左侧目录树
  - 待讨论
    - bibtex是归属到workspace，还是归属到文章？
      - 暂时整个workspace共享
    - 新建的空文档(无标题文档、无内容文档)是否要保存？

## 0303

- bibtex与文献的设计
  - 侧边栏的bibtex是数据源
    - 删除后所有地方会消失
  - 文末参考文献完全自动生成，不可编辑
  - 文中引用
    - 只能通过侧边栏插入
    - 能通过键盘退格键删除
- 分享文章的功能
- 清空本地数据库的方法，方便测试
  - editor.db.inspector().clear()
- 文档数据库修改操作丢失的问题
  - ⚠ 当editor在操作currentDoc对象时，若在其他react业务组件中也要操作当前文档，必须使用全局共享的currentDoc对象，不能用db.get(id)得到的对象，否则某处的修改会丢失

## 0302

- 文档数据库问题测试
  - ⚠ 碰到数据库显示有延迟/需要刷新才更新的问题，一定要先检查调用函数时是不是少写了await

```JS
await editor.db.get('article')
// 创建文章后，一定要set，否则下面get返回的是一篇新文档
await editor.db.get(id)
```

## 0301

- 开会小结
  - 新的基座工程项目
    - 路由管控
    - 接入子项目
    - 在test站点能上线
    - 登录保留authing
  - block editor 后端可以很简单
    - 单个拉取
    - 批量拉取
    - version解决同步冲突的问题，但yjs也可以解决冲突问题
  - 客户端如何拉取数据
    - 一批一批
    - 同步数据库
  - yjs的二进制数据包含了历史记录，但二进制默认不可识别，服务器实现搜索需要额外功能
  - 设计block数据表
  - 数据同步放在编辑器层，还是数据库层？ 编辑器变了，通知数据库？还是数据库变了，通知编辑器？
    - yjs提供了合并编辑器多个操作的方法
    - 光标的同步更适合通过yjs
- bug定位，通过vscode-git-graph
  - refactor: docActionsMenu state
    - 无法分页
  - fix table types
    - 无法正常运行
  - chore: remove unused code
    - 可正常分页
    - 65b141e7fcabd98511e73f49aced5d714d044812
- 测试新建文章时文件列表不实时更新的原因
  - 前端读取文件列表是异步，当文件列表在服务端生成也是异步时，可能会出现前端新建文档后，马上打开文档列表时，服务端还没更新索引，前端的列表总是少一项的情况

```JS
await dbClient.getByDocumentType('article').then(docs => Array.from(docs.values()).filter(doc => !doc.metadata?.ttl))
```

- forEach中不能写await的解决办法
  - https://stackoverflow.com/questions/37576685/using-async-await-with-a-foreach-loop
  - await y.forEach(async (x) => {
    - await Promise.all(y.map(async (x) => {
# dev-02

## 0228

- dev-plan
  - [x] 添加bibtex去重，根据标题
  - [x] 所有文档列表

## 0225

- 路由部分重构思路
  - 使用isLoading和user对象来判断，而不是userStatus

## 0224

- dev-plan
  - [x] 登录后打开的最近一篇文档，所有人都是相同的
  - [x] 恢复插入数学公式的按钮
  - [x] 用户设置项保存到本地数据库
- 紧急bug
  - bibtex无法添加
  - 协作编辑时，第2个人的输入无法同步到第1个人
  - 打开链接文档会卡顿，打开目录树会卡顿
  - ~~分享功能~~
- 需要修改图标的大小
  - m
    - 上极限
    - 下极限
    - 所有三角函数，如 余弦
  - l
    - 所有矩阵，如 多行对齐等式
- [How to change font-size to a SVG?](https://stackoverflow.com/questions/64914200)
  - You can not change the font size or font width because SVG is not a font. It is Scalable Vector Graphics. 
  - If you would have some text in your SVG, then you could do something with the font from the text element.
  - The trick is to assign with and height the em unit

## 0223

- bugs整理
  - 切换文章相关 (bugs自己消失了)
    - createImgDataRefConverterPlugin() 创建的图片插件有问题，每次切换文章会抛出异常
      - plugincollection-plugin-name-conflict {"pluginName":"ImgDataRefConverterPlugin"}
    - 点击新建文档按钮时，控制台抛出异常  (reading 'model') at Pr._save
  - 创建新文章时，目录树组件更新有问题
  - [x] 登录用户没有workspace时弹窗提醒

## 0222

- 站点测试
  - 重新登录后，编辑器无法显示
- 路由验证的场景
  - 没spaceId就进不去编辑器页面
    - 首次登录时
    - 刷新页面时
  - 退出登录时
    - `location.reload()` method reloads the current URL, like the Refresh button.
    - `location.assign(url)` method causes the window to load and display the document at the URL specified.
- location.href property vs. location.assign() 
  - it may be true that `location.href = url;` is faster than `location.assign(url)`, although it may depend on the JavaScript engine implementation
  - Calling a function should be slightly slower than accessing the property, but in terms of memory there should not be a big difference in my humble opinion.

## 0221

- dev-plan
  - [x] alert-block plugin upcast
  - 设置项保存到本地数据库
  - [x] 高亮块 或 窄宽度的段落
  - ~~通用的文档列表弹窗~~
- ckeditor的默认图标文件导出位置
  - packages/ckeditor5-core/src/index.js

## 0220

- 高亮块功能设计
  - 可调整宽度
  - 可设置背景色
  - 支持编辑高亮块内容
  - 不支持
    - 不支持嵌套高亮块
    - 不支持 > 快捷键
- 高亮块api设计
  - width 0.5, 0.75, 1
  - backgroundColor none, gray, rgby
  - showBorder
- 高亮块ui交互设计
  - 参考 ckeditor blockquote/link/codeblock
  - 配置项放在balloon toolbar
- documentdb接入yjs前的版本是 1.0.32

## 0218

- [How to align horizontal icon and text in MUI](https://stackoverflow.com/questions/51940157)
- [How to keep showing the 'popover' on hovering on the anchorEl and 'popover' as well?](https://stackoverflow.com/questions/54705254)
  - 要点在设置 pointerEvents

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
@article{Ota1981,
        author = {Terukazu Ota, Yoshihisa Asano and Jun-ichi Okawa},
        title = {Teattachment length and transition of the separated flow over blunt flat plates},
        journal = {Bulletin of the JSME},
        volume = {24},
        No = {192-7},
        year = {June 1981},
        pages = {941--947},
        }
@article{myers1986ano,
    title={An {O(ND)} difference algorithm and its variations},
    author={Myers, Eugene W},
    journal={Algorithmica},
    volume={1},
    number={1-4},
    pages={251--266},
    year={1986},
    publisher={Springer},
    url = {http://web.archive.org/web/20080207010024/http://www.808multimedia.com/winnt/kernel.htm}
}
@article{grishchenko_2010, title={Deep hypertext with embedded revision control implemented in regular expressions}, DOI={10.1145/1832772.1832777}, journal={Proceedings of the 6th International Symposium on Wikis and Open Collaboration - WikiSym 10}, author={Grishchenko, Victor}, year={2010}}
@article{CitekeyArticle,
  author   = "P. J. Cohen",
  title    = "The independence of the continuum hypothesis",
  journal  = "Proceedings of the National Academy of Sciences",
  year     = 1963,
  volume   = "50",
  number   = "6",
  pages    = "1143--1148",
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

- 编辑器设置选项分类 功能设计
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
temp1.getMap('recent-docs').set('d', 'id')
temp3.set('d', 'id')
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
# dev-01

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

```bibtex
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
