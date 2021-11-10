---
title: lib-editor-ckeditor5-dev-log
tags: [ckeditor, dev-log]
created: '2021-10-27T03:20:11.947Z'
modified: '2021-10-27T03:20:45.841Z'
---

# lib-editor-ckeditor5-dev-log

# daily

- 工作开发问题
  - 原因定位
  - 解决方法
  - 其他方案

- dev-xp
  - 不要执着于在旧版代码中找实现参考，有时会浪费过多时间，新的api也许自身就提供了实现

## not-yet

- 流程图缩放问题

- 检查图片的接入方式
  - toolbar打开文件选择器
  - 拖拽本地图片到编辑器光标位置
  - ctrl+v粘贴图片到编辑器

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

- boxEditing, boxUI 的ui部分为什么总是toolbar界面相关的内容
  - 插入元素的位置，通常放在command

- later
  - 就算postcss-loader/style-loader版本与官方文档一致，也可能会出现demo样式异常的问题
# 2021

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

```markdown
- 流程图

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
