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
- dev-summary
  - 使用最多的组件
    - icon
    - button
    - input/TextField
    - list
    - modal/popover/tooltip/dropdown
    - dnd-kit
    - collapse
  - 将组件中操作blockDB的逻辑分离到service层
    - 降低前端业务开发对后端的依赖
      - 分离dbBlock和editorBlock，两者没有直接关系，但可以转换得到
    - 在service层提供observe这类自动更新的方法，不需要websocket
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
  - 支持不同行类型的list
  - 多种类型数据的转换和渲染
    - 多种类型的bibtex，使用对应的转换器，渲染成不同样式的
    - 多种类型的单元格，渲染成不同的组件
  - 文本以打字动画的形式动态展示 typed.js
    - 书写动画、回退动画
    - to-do
      - 实现多行文本依次展示
  - css模式
    - hover-show-otherwise-hidden
  - react开发模式
    - enum vs switch-case
    - 折叠列表时，如何添加事件监听器的能减少rerender
- almanac体验-feat-版本控制
  - 亮点：创建分支 + 合并修改
  - merge分支文档到主文档时，头部图片不会自动迁移，需要手动修改
  - 分支文档被合并到主文档后，分支文档的状态会改变为locked只读，不能再次编辑
    - 已被合并过的分支文档，只有被再次复制创建副本，才能修改
  - 版本控制cons
    - 没有显示分支的时间先后关系，只显示了已合并未合并
      - 类似github insights里面不同fork的顺序
- material-ui缺点
  - ~~没有dropdown，select组件默认会遮挡触发元素~~
# 2022-dev
- my-next
  - dev-starter
    - react patterns
    - typescript patterns
    - mvc dev pattern(for app)  ~~in data grid~~
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
  - sortable-filterable-groupable-table

- 产品日历组件
  - headless-date-picker

- [新产品设计稿figma](https://www.figma.com/file/7pyx5gMz6CN0qSRADmScQ7/AFFINE?node-id=0%3A1)

```JS
console.log(';; r1-user-spaces ', pathname, user, userSpaces, currentSpaceId);
```

- daily-notes
  - 日历关联的部分
    - 实现大日历
    - 实现大日历与小日历切换的交互
    - 弹窗modal中展示大日历
  - 顶部日期导航条可用
  - daily文章部分由多维表格实现，提前准备好daily数据逻辑

- new-daily-notes-page，四个部分都是普通文档形式
  - pinned desktop icons
    - 可折叠
  - tasks收集，以多维表格的形式自动生成标签，可切换看板
    - in-progress
    - overdue
    - completed
  - imported info
    - 笔记
    - 代办
  - activities
    - 创建文档
    - 更新文档

- block-editor产品需求讨论
- ✨️ subpage相关
  - 创建subpage
    - 通过斜杠菜单
  - subpage标题同步
    - 在service层对一个page中引用的所有page添加监听器
  - subpage与page-tree同步
    - 🤔️更好的方案
    - 创建subpage时更新db里面tree数据源
- ✨️ backlinks功能讨论
  - 双[[唤起的交互面板
    - 创建backlink时需要能搜索并选择已有page
    - 面板功能和交互设计
  - link和backlink如何区别
    - 🤔️notion似乎没有普通超链接，media细分为 image/video/audio/file/web-bookmark/code
    - notion粘贴普通url后会自动提示创建bookmark或embed，都会展示为卡片
  - page全局backlinks统计
    - notion显示在题头位置
    - 功能上能相互跳转
      - 🤔️ pageA引用pageB，如何从pageB跳转到pageA的引用位置
  - backlink的title会统一动态更新
  - 交互细节
    - 双[[默认唤起双链搜索的交互，但按退格键后可以默认展示双[[文本
    - 在当前文档中可以链接当前文档自身

- dev-to-later-v0429
  - [x] calendar-heatmap sync
  - daily notes pages init
  - calendar-big 进度沟通
  - authing-overseas 变更收集
  - 重构editor
  - 顶部七天周日，是否始终将当天放在第4个居中的位置
  - 顶部七天周日，是否要支持键盘横向滚动，前后滚动7天？10天？
  - 修改默认workspace名称的逻辑，presetWorkspace
  - [] page和page-tree同步正常，page和navbar同步不正常

- 备份带斜杠菜单的编辑器-bak20220506
  - commit-id b9d74bacb33198d073afb2b2331d1210ce476dc7
  - [旧架构的使用示例](https://github.com/toeverything/Ligo-Virgo/blob/b9d74bacb33198d073afb2b2331d1210ce476dc7/libs/components/heading/src/block.tsx)

- dev-to-later-v0518
  - 将page-tree相关的逻辑提取到顶层命名空间，方便复用，如斜杠菜单、全局快捷键
    - 参SelectionManager实现
  - [ ] 先实现单例弹窗
    - 获取当前选区及在viewport中的物理位置
  - [ ] 实现静态悬浮菜单
  - [ ] 实现动态菜单项
  - [ ] 自定义菜单项事件
  - [ ] 重构Text组件，底层Text不处理业务，只处理编辑器相关逻辑
    - 上层BusinessTextHoc获取数据和操作方法

- 本周3个菜单
  - command menu
  - inline format menu: bold/italic
  - block menu

## 0519

- page初始渲染时，title是如何渲染的
  - PageView渲染的不是title，而是普通Text组件，但传入了标题样式名

- KeyboardEvent.metaKey
  - On Macintosh keyboards, this is the ⌘ Command key
  - 对windows，若按过windows键，则metaKey为true

- 弹层应该实现为plugin，因为不处理编辑器核心的输入、渲染逻辑

- block-left-menu、斜杠菜单、文本悬浮工具条、mention面板、group/ungroup悬浮菜单，可以有一个统一的唤起隐藏逻辑，根据所在block类型和数据动态渲染菜单项。

- Editor层主要关注于编辑器核心能力的提供，例如编辑、选区、各种block的管理和控制，可以认为Editor是一个编辑器内核的sdk，类似于操作系统shell层；
  - plugin是对Editor的能力增强，例如弹出菜单、下拉菜单、筛选过滤查找、导入导出等交互，这些交互形式不是编辑器内核关注的内容；
  - plugin和Editor的交互，通过Editor层对外接口进行沟通，通过Editor的各种hook完成对plugin的回调

- 可能的风险，现在大家都还没有使用plugin，我可能会根据需求增加plugin的api和方法的参数

- undo/redo不仅回滚输入内容，还要回滚光标

## 0518

- 浮动工具条 FloatingToolbarPlugin
  - 在plugin构造函数中注册ON_ENTER显示隐藏浮动工具条的方法
  - 触发条件
    - 在自定义block的useEffect中，onSelectionChange/输入变化时
  - 在TextBlock或CodeBlock中触发 editor.getHooks().onEnter/onKeydown/onBeforeInput

- dev-to-topic-selection
  - 向selectionManager中setSelection
  - 从selectionManager中getSelection
  - 下拉小弹窗、悬浮工具条，都需要从selection中 getBoundingClientRect
    - 获取一个range的text

- dev-to-topic-inline-menus
  - 👉 如何注册菜单项，斜杠commandMenuItems、inlineMenuItems
    - ✔ 不需要在全局注册菜单项，每个block自己传入自己支持的菜单项及事件
    - ckeditor采用的是初始化编辑器器传入toolbarConfig属性
    - slate示例给的是创建一个自定义Menu组件
  - 👉 如何实现动态菜单项
    - ✔ 根据block type和block自身传入的配置
  - 👉 与设计沟通文本悬浮工具条设计图
  - 👉 悬浮工具条及下拉框是放在全局单例，还是和每个Text组件写在一起
    - ✔ 放在全局，方便在不同block间复用
  - 💡 commandMenu和inlineMenu的实现放在哪里更好
    - 可以放在封装的TextView组件
      - 优点是方便直接获取SlateEditor的selection数据和其他属性方法
      - 容易获取editor command
      - 触发条件 输入斜杠或选中
    - 可以放在BlockEditor的plugin
      - 优点是非TextView组件也能唤起斜杠菜单
      - 缺点是针对工具条的不同操作，不同的按钮事件需要传入额外的不同的编辑器相关的参数
      - 触发条件是 showCommandMenu

- 关于编辑器中选中文字或其他元素才会出现的悬浮工具条的命名
  - slate: hovering-toolbar 🤔 并不是hover就会出现的
  - ckeditor/slate-plate: balloon-toolbar
  - prosemirror: tooltip
  - medium-editor: inline/block-toolbar

- innos的编辑器可以将block拖入拖出card/group
  - 可以将block拖到行内并列，并且保留样式背景色
  - innos的设计强调卡片自适应变宽，占满一行
  - innos的缺点，容器元素过多，心智成本高

- block可以嵌套block
  - group不要嵌套group

- 拖动时应该默认带上子集一起拖动，因为子集数量可能很多超出屏幕
  - 另一种设计是，按住其他键如shift可以只拖动父级单行
  - shift可能白板也能用

- 回退删除键的逻辑要讨论
  - a. 直接跳过分隔线，直接在上一个block末尾删除文本
  - b. 先focus分隔线，再删除分隔线

## 0517

- slate
  - mention输完@后，如何弹出下拉框
    - 整体架构为 `<Slate><Editable></Editable><Portal></Portal></Slate>`，注意只有在@x用户输入x非空时才渲染下拉框
    - 下拉框出现的条件@后用户输入文字非空，且搜索结果非空
    - 下拉框portal定位样式 position: 'absolute', 动态修改style.left/top
  - mention下拉列表中选中文字后，如何插入编辑器
    - 在Editable组件的onKeyDown事件中，检测到enter按键时插入文字到编辑器
    - Transforms.insertNodes(editor, mentionNode);
    - 上下键可以在下拉列表切换当前选择高亮项

- slate的selection和block-editor的selection有什么关系
  - 如何存取slate编辑器的selection

- 将block级的onMouseMove事件注册到root根节点的onMouseMove，然后在block级事件内判断位置只在block内才执行逻辑

- 主要改动是createView返回react组件 -> 直接使用View组件 。
  - 原来RenderBlock中是直接调用createView方法，这样会导致 react 的 hook 会报错，因为react会将这个函数理解为普通函数调用，hook会合并到RenderBlock的hook stack中。如果组件重渲染会报错（warning级别，不会影响build，因为createView调用位置保持一致，且在最后面)
  - 写法明明就是 FunctionComponent，但是多加了一层，完全没必要。所以直接改为FC了

## 0516

- dev-to
  - command-menu
  - inline-menu
  - sub-page实现设计方案文档

- 紧密联系功能
  - backlinks
  - slash command menu
  - link page

- 公司集体断网的原因
  - maximum number of concurrent DNS queries reached.(max: 150)

### oneOnOne-terry-表格研发体验

- google docs dom转canvas的原因
  - 最开始是基于dom实现滚动
  - 每次滚动一行高度，不够平滑
  - 虚拟滚动append缓冲行执行会卡顿
  - 合并单元格基于colspan

- 友商都在用spreadjs
  - 石墨文档 handsontable -> spreadjs
  - 腾讯文档 spreadjs

- spreadjs基于canvas实现，且逻辑分层非常好
  - spreadjs的模型是比较通用的，**数据模型层特别重要**
  - spreadjs下性能并不是很优秀
  - spreadjs不支持协同
- 只保留spreadjs的渲染视图层，模型换成google-docs的数据层
  - 行数量、每行的列、单元格输入内容、单元格文本格式/条件格式、单元格样式、单元格评论
  - row[], cell[]
  - 合并单元格保存在全局
- 全局属性
  - 行冻结、列冻结
  - 全局边框色

- canvas的性能一定能够更好吗
  - canvas像素级绘制，dom依赖浏览器渲染
  - canvas也能实现虚拟滚动，还能实现双缓存画布
    - 利用双画布复用canvas内存对象
    - dom的虚拟渲染未考虑，文字斜体；canvas直接复用2d的位置信息
  - canvas的性能瓶颈，一行的高度取决于所有行中单元格所有文本的高度，word-segment分词算法，优化了排版算法
  - canvas的兼容性在移动端更好

- canvas上线后还会出现移动端黑屏的问题
  - 部分移动端由于gpu的问题，导致渲染
  - 页面canvas特别多，会出现粉屏

- 要优化性能
  - 一都会增加链路，使用简化的指令，传递指令
  - 更现代的基础设置，不存对象数组，直接存数组，如用protobuff

- 实现表格
  - 稳健的架构
    - 渲染可支持svg/canvas
    - 离线需要优秀的模型设计 数据库模型、编辑器模型、视图层模型
    - 协作需要指令，用户操作 -> taco -> 取缓存 -> 缓存中没有就刷新

- crdt更新是整体block更新
  - 性能不会比ot更好

- 在效率和功能间取得平衡

## 0513

- dev-to
  - 确定斜杠命令菜单的实现思路
  - 确定获取斜杠锚点dom元素位置的思路
  - 初步实现在焦点行的下一行唤起斜杠命令菜单

- 编辑器基础
  - 光标显示、是否可focus
  - 选区拖拽：当block高度大于屏幕高度时，选区的实现
  - 快捷键
  - 滚动条

- forEach 循环里面不能await，改普通for循环

## 0512

- dev-to
  - [x] authing登录已经接入海外版，目前支持google登录和用户自己注册邮箱登录，不支持注册手机号登录

- 编辑器的几种menu
  - add-menu，如创建添加各种block
  - block-menu，如复制、粘贴、上移、下移
  - slash-command-menu，弹窗内容同add-menu

- 左侧菜单的触发条件 onMouseMove
  - 斜杠菜单的触发条件 用户手动刚刚手动输入/

## 0511

- 创建subpage的两种方式
  - 斜杠菜单 /
  - 双链热键 [[
  - 实现可以参考 menu/hover-toolbar

- [python 字符串转列表出现\ufeff的解决方法](https://www.cnblogs.com/mjiang2017/p/8431977.html)
  - 在Windows下用文本编辑器创建的文本文件，如果选择以UTF-8等Unicode格式保存，会在文件头（第一个字符）加入一个BOM标识。
  - BOM = Byte Order Mark
  - BOM是Unicode规范中推荐的标记字节顺序的方法。比如说对于UTF-16，如果接收者收到的BOM是FEFF，表明这个字节流是Big-Endian的；如果收到FFFE，就表明这个字节流是Little-Endian的。
  - UTF-8不需要BOM来表明字节顺序，但可以用BOM来表明“我是UTF-8编码”。BOM的UTF-8编码是EF BB BF（用UltraEdit打开文本、切换到16进制可以看到）。所以如果接收者收到以EF BB BF开头的字节流，就知道这是UTF-8编码了。
- [Python 读取文件首行多了"\ufeff"字符串](https://blog.csdn.net/chenmozhe22/article/details/89472790)

- 👉🏻️ authing海外迁移
  - 我对接authing的技术支持
  - https://core.authing.cn/api/v2/applications/61961a7b8b90af37e7c422e0/public-config

- authing海外版的2个问题
  - google登录暂时未生效，authing控制后配置后需要等待一段时间，生效前需要每个人重新注册一个帐号
  - 切换到海外版后，后端的/user和/spaces接口请求出现异常，需要后端修改一下请求authing用户的url

## 0510

- dev-log
  - [x] 测试接入authing海外版，需要等authing的人对接修改配置

- services之间的相互调用，考虑用依赖注入实现

- `/usr/bin/env: ‘sh\r’`: No such file or directory

## 0509

- 迁移到包含service层的架构后，顶部导航条获取page标题的时机难以确定
  - 原因1: 导航条NavigationBar是未被route_private包裹的，渲染时机非常早
  - 原因2: 顶导航条通过router的useParams只能获取到workspace_id，不能获取到page_id
  - 就算用魔法强制在page初始化后注册title更新的事件监听器，navbar更新title还是失败

## 0506

- 为方便调试编辑器开发，应该提供一个单独的编辑器页面，不包含获取用户数据等逻辑

## 0505

- 登录流程设计
  - 登录路由守备要支持offline

- page-tree的状态同步
  - 未调完的分支不要commit到主分支，会导致协作者debug很混乱

- 👉🏻️ workspace初始化过程讨论
  - 离线功能支持的程度
    - 是否要离线可登录
    - 是否支持离线切换page、跳转page
  - 初始化workspace实现的细节
  - 创建workspace的ui和交互
  - 删除workspace的ui和交互
- 👉🏻️ 其他task
  - page-tree创建page后ui和state要视觉上立即更新

### oneOnOne-terry-文档基建closure

- google closure 运行时
  - 扩展了js、dom
  - ui库

- google closure compiler 编译器
  - 提高js压缩率
  - 编辑css为atomic css
  - 从compiler迁移到webpack，体积增大了，但便于协作开发
  - closure-templates 支持模板，类似handlebar/pug

- goog.disposable.prototype.disposeInternal 在基类实现dispose方法

- dev-to-login-issues
  - 🤔 workspaceName为用户名带来的问题
      - 邮箱名冲突的问题，如a@qq.com/a@163.com
          - 暂时解决命名冲突的问题，用户名_邮箱的方式，a_qq
      - useBlockDatabase传入的workspaceName，取回来的id是一致的吗
  - 🤔 上次的workspaceId/workspaceName存放在哪里，怎么获取？
      - 计划存放在localStorage
      - 先向服务端请求最近workspace列表，若为空，则使用localStorage中保存的
      - 如果存放在database中，则需要修改现在的初始化逻辑，在useInitEditor之前先初始化database
  - 🤔 有没有必要在每次登录或刷新页面时，从服务器请求用户的所有workspaceId列表？
      - 我认为有必要，在新浏览器登录时可恢复上次workspace，而不是在本地新建workspace
      - 若离线，则自动创建新的workspace，id为 用户名_创建日期
  - 🤔 若用户上午在设备A登录workspaceA，下午在设备B登录workspaceB(先自动登录A然后手动切换到workspaceB)，晚上离线/在线时，在设备A打开自动进入哪个workspace？
      - ? 若离线， workspaceId默认先用本地的，然后比较远程同步得到的id和访问时间

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
# 2021-dev

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
- 首页的打字效果
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

- 产品站点操作流程
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
  - 自定义方块 14x14
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
