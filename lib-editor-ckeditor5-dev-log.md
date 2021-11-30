---
title: lib-editor-ckeditor5-dev-log
tags: [ckeditor, dev-log]
created: '2021-10-27T03:20:11.947Z'
modified: '2021-10-27T03:20:45.841Z'
---

# lib-editor-ckeditor5-dev-log

# daily

- company-unskilled
  - 确认下一步工作计划
  - 沟通休息

- **markdown-editor for vscode**

- 工作开发问题
  - 原因定位
  - 解决方法
  - 其他方案
  - 提出问题之后，有什么更好的方案、行业内更专业的方案

- dev-xp
  - 不要执着于在旧版代码中找实现参考，有时会浪费过多时间，新的api也许自身就提供了实现

- dev-summary
  - 使用最多的组件
    - button
    - icon
    - input/TextField
  - 日历热力图 react-activity-calendar
    - 中文本地化
    - 始终显示70+N天
    - to-do
      - tooltip传入组件
  - 文件列表 react-table
    - 悬浮工具条
    - to-do
      - sticky header
  - 文本以打字动画的形式动态展示 typed.js
    - 书写动画、回退动画
    - to-do
      - 实现多行文本依次展示

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

- dev-xp
  - 一段代码排查很久没找到原因，可能是复制粘贴代码时忘了修改细节，如粘贴后false未修改为true

## not-yet

- to-do
  - workspace 文档列表
    - sticky header
    - 删除文档后，只在列表删除了，文档数据库中仍然存在
  - 全局路由守卫的时机错误
    - **应该在路由跳转前重定向，而不是在路由跳转后再次跳转**

- 任务看板
  - features
    - 切换 列表视图、看板视图、时间线(甘特图)视图
    - 从看板创建文档
    - checkbox

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

- affine新首页设计与工作计划
  - [x] 首页使用~~类似workspace的设计~~，快捷菜单跳转到workspace
  - [x] 布局改为左侧边栏
  - [x] 文档列表只显示创建的文件，最近操作的文档要跳转到单独页面
  - [ ] 文档列表：pin置顶一个日期

- 编辑器工作计划
  - 左侧目录显示参考文献锚点
  - 编辑器首页顶部显示图片

- 折叠列表时，如何添加事件监听器的能减少rerender

- 日期时间的处理
  - 可参考日历组件的实现方案

- 流程图缩放问题

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

- boxEditing, boxUI 的ui部分为什么总是toolbar界面相关的内容
  - 插入元素的位置，通常放在command

- later
  - 就算postcss-loader/style-loader版本与官方文档一致，也可能会出现demo样式异常的问题
# 2021
- TODO
  - [x] 点击任务卡片时，应该出现弹窗
  - [ ] checkbox
  - [ ] 添加日程：开始时间、结束时间
  - [ ] @其他用户
  - [ ] 创建文档
  - [ ] 看板卡片右上角的删除图标应该悬浮时才出现
  - [ ] 鼠标在卡片上方时，形状应该是pointer，而不是拖拽的grab

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
  - 考虑使用useBlockLayout
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

## 1029-31

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
  - 参考文档示例，思路实现是ui插件时ui渲染部分使用react组件
