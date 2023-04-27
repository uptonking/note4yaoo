---
title: dev-ing
tags: [dev]
created: 2022-05-24T17:52:58.048Z
modified: 2022-05-24T17:53:08.400Z
---

# dev-ing

# dev-2023
- 分析核心需求和问题，拆分问题，梳理任务、子任务，排期开发

金瑶 邀请您加入【金瑶的个人会议室】
点击链接直接加入腾讯会议：
https://meeting.tencent.com/p/9606972663
#腾讯会议：960-697-2663

# dev-xp
- ui-starter
  - css: open-props, glass-ui, 渐变字体
- dev-starter
  - patterns: react, typescript
- list-grid-starter
  - plain
    - no sort/filter/group
    - no reorder
    - no column width resize
    - custom cell renderer
  - searchable
  - virtualizable
- list-grid-solutions
  - checkbox
  - draggable/reorder list
  - fields menu - filter/groupable
  - inline editing
  - orm integration
  - sortable-filterable-groupable-table
- 产品日历组件
  - headless-date-picker
- module/fwk/server
  - 灵活的tag/bookmark系统
  - cms, tables, bi
- 编辑器参考
  - atlassian-editor
    - https://atlaskit.atlassian.com/packages/editor/editor-core
    - https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-minimal
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-with-toolbar
    - https://ckeditor.com/docs/ckeditor5/latest/examples/builds-custom/full-featured-editor.html
  - more-editor
    - https://demo.grammarly.com/
# dev-review

```shell
DEBUG=* npm install --legacy-peer-deps --loglevel silly

$$('[contenteditable]')
```

- dev-goals
  - rich-editor: text/code/block
  - pivot-table
  - collaboration
  - local-first-database
  - annotation/comment/whiteboard/pdf
  - 事项--截止日期(0730+休整)--重要性(hml/s1-s3)
  - rich-editor-vanillajs
  - pivot-table-grid--0828--h
    - dropdown-menu vs tabs
  - app-wiki-knowledge-base--0904
  - dashboard/webapp-template--0901
  - ui: zag/ark, ariakit, radix-ui, mantine

- deep into lib/fwk
  - src-code, issues, pr, forks, extensions/alternatives
# dev-2023-方向+方法+时间
- 👉🏻 output: 代码、产品、生态积累
- slate-wangeditor
  - model, view, sync, collab
  - slate-docs-examples
- 👉🏻 eg-focalboard
  - table view
  - kanban view
- 👉🏻 eg-tanstack-table-v8
  - [x] 内存数据: nedb, blinkdb
  - [x] 流式数据: linvodb, tingodb
  - [ ] 方便接入已有的外部数据源
  - tuple-database 支持内存和持久化
  - tinybase 支持内存和持久化

- 若slate-model层采用扁平化Node
  - 如何保持path和key同步，参考 getKeysToPathsTable, getByKey实现上基于getByPath
  - 优化方向可参考tree的crud及协作
  - 协作时还应该考虑 json patch + last-write-win
  - Node定义采用unist
  - lww的字符串改为针对crdt优化的类型

- collab-sync
  - 👉🏻 string-crdt: ? list-crdt
  - collab-data-structure: lww-with-hlc
  - remoteStorage: google-drive、网盘、七牛对象存储
  - lo-fi-sync-server
  - pouchdb

- sqlite-web
  - evolu(hlc)
  - kikko
  - absurd-sql-ts: read ArrayBuffer

- long-term
  - cms, airtable, lowcode
- techstacks
  - async/generator, stream, buffer, binary, scheduler, arrow
  - 样式片段也可在 w3schools.com 在线尝试

- 支持切换内存和持久化的示例
  - abstract-level, localforage
  - tanstack-table server-side row model
  - tupledb

- 内容的存储与更新如何与数据库集成
  - 编辑器内容自动保存一般通过在onChange方法中执行saveToDB
    - 也可以在onChange方法中创建内存db、更新索引，通过索引提高计算效率
    - 应该避免维护2份数据
  - 将编辑器的计算密集部分的数据模型不使用普通json对象，而直接用类似数据库模型的设计
  - 为了性能，尽量不要直接读写持久化数据源，要使用缓存object pool

- log2022 数据同步、冲突处理、本地存储
  - 07-focalboard-views
  - 08-block-editor-tiny-write
  - 09-prosemirror-examples
  - 10-prosemirror-collab - otjs - crdt-hlc
  - 11-idb-sync-crdt
  - 12-nedb-linvodb

- log2023 编辑器、表格、协作、cms
  - 01-linvo-search + tinybase-sync-hlc-wip
  - 02-typewriter-quill + tanstack-table + slate-table
  - 03-crdt-rga + slate-yjs + slate-editor
  - 04-slate-dnd/table/image-sequelize

- why use es6 class
  - 运行时类型检查，instanceof
  - 既包含类型定义，又包含逻辑工具方法
    - 注意class有时也采用先定义interface再实现，此时ts type也合理了
    - 但应用层业务代码一般不需要定义单独interface
  - 方便调试，可直接log到对象及方法，函数里面的闭包变量更新难以定位
    - 也可以提前将需要调试的属性或方法添加到闭包暴露的对象上

- dev-xp-editor
  - 不仅要保持编辑器内容和视图同步，还要保持选区和内容同步

- dev-later
  - crdt tutorials
  - 默认 last-write-win, 出现冲突时，提示用户选择版本
  - 腰包掉到床头版与墙的夹缝中了
  - 离屏渲染，keep-alive
  - 分层渲染

## 040

- not-yet
  - todo remove hash在编辑器中有什么作用

- dev-to
  - streaming-infinite-list/tree
  - focalboard-views
  - slate-docs-examples
  - noseditor-docs
  - unit-tests
    - test in firefox
  - drag
    - [ ] dnd-kit tree performance, 支持向左拖动更新层级，自定义冲突解决
    - 拖拽到页面顶部或底部时，自动滚动
    - 拖拽时原布局不变，只显示预期位置的指示线
    - remove zustand
  - toolbar
    - [ ] dropdown 组件样式、active值
    - [x] 工具条按钮处理跨选区的情况
    - [x] 当前 block type 指示与转换
    - [x] 点击按钮时保存选区，逻辑+视觉
    - [x] 高亮当前光标对应的格式按钮
    - [x] 字体大小、颜色
    - [x] 按钮按功能分组
  - image
    - 上传图片时，默认图片原大小
    - upload by drag-drop
    - paste
    - [x] upload by filePicker
  - table to tanstack
    - 删除表格
    - 删除行时，若只有一行，则应该删除表格
    - [x] 隐藏浏览器selection
    - 优化model
    - copy from word
  - list
    - [x] rename todoList to checkboxList
  - scss to linaria
    - list-item
  - callout 高亮块
  - keyboard-shortcuts
  - copy-paste
    - images
  - 去掉依赖
    - plate-serializer
    - zustand
  - emoji
  - embeds
    - video
    - iframe
    - notion
    - apitable
  - formats
    - 清除格式
  - link
    - 粘贴图片url时提示显示为图片
  - 高亮块
  - 格式刷
  - 斜杠菜单
  - resume with noseditor
  - editor-features-playground
    - rewrite lexical for slate
    - with devtools

- dev-to-collab
  - 🐷 每次刷新页面，空白行会多一行
    - 每次刷新，observeDeep会执行
  - 🐷 yOffset out of bounds
    - 位置：getSlatePath > yOffsetToSlateOffsets
    - 复现方法，在一个浏览器输入，在另一个浏览器全选+删除

- dev-later
  - 悬浮工具条
  - merge-cells 逻辑优化
  - cell-floating-menu 右上角
  - list
    - 第一个列表项无法向左拖实现提升到父级
      - 列表项A的兄弟项B无法拖到A的位置，即无法替换A，B会自动变成A的子级
    - 列表折叠图标在item内容多行时，会竖直居中
    - 将无序列表项拖进数字列表项时，数字列表项会增加？数字编号或自动变动
    - 数字列表跟在符号列表后时，数字不会从0开始，需要在前面插入一个空行
    - 列表组件设置面板，设置折叠、可拖动
    - 拖拽时，不相关的列表项也会抖动
    - checkboxList完成后可选变灰
    - bulletList支持emoji
  - initialDataLong示例，无法删除首行列表项
  - remove ramda
  - drag
    - paragraph的drag handle有时无法选中
  - collab
    - 2个编辑器同一页面协同的示例未完成
    - cursor光标位置经常对不上
# dev-04

## 042

## 0427

### [告别JS keyCode](https://www.zhangxinxu.com/wordpress/2021/01/js-keycode-deprecated/)

- MDN上的解释是对打印字符不友好。
- 不同字符共用keyCode
  - 键盘上有很多按键是同时对应两个字符的，例如“<, ”和“>.”
  - keyCode值是跟着键盘走的，而不是字符内容，也就是，当我们输入“<, ”和“>.”等字符的时候，返回的keyCode值是一样的
  - 我们需要通过判断用户是否按下了Shift键才知道究竟输入的是哪个字符。比较繁琐
- 相同按键不同keyCode
  - 数字键按住Shift键可以输出其他内容

- `event.code`指明按下的是具体哪个物理键，键盘上每一个按键都对应一个唯一的event.code值，均使用大写英文单词表示。
- `event.key`指明具体输入的字符内容，如果是非打印字符（例如Enter键、Esc键、Shift键、Alt键等），则返回具体的非打印字符的英文名称，如果输入内容与输入法有关则返回固定的Process名称。
  - 对于英文场景，只需要使用event.key就可以知道键盘输入的内容了。
  - 在中文输入框开启的场景下，如果按键的内容和非中文输入法下的内容不一样，则event.key的返回值是固定的Process，表示输入的字符内容和键盘对应的原始内容进行了处理。

## 0426

- [Chrome: Inspect elements that appear only when dragging - Stack Overflow](https://stackoverflow.com/questions/22597815/chrome-inspect-elements-that-appear-only-when-dragging)
  - Put a breakpoint in the code - inside of the `mousedown/up` event callback.
  - open chrome devtools, Expand "Event Listener Breakpoints" on the right
    - I always set the listener on `mouseup` so it will automatically break when you stop dragging

## 0425

- [css-loader localIdentName: is a hash necessary for uniqueness? - Stack Overflow](https://stackoverflow.com/questions/48889736/css-loader-localidentname-is-a-hash-necessary-for-uniqueness)
  - `localIdentName: '[name]__[local]__[hash:base64:5]'`

## 0424

- [Use Css modules add conditional transition styling to my side navigation - Stack Overflow](https://stackoverflow.com/questions/61342201/use-css-modules-add-conditional-transition-styling-to-my-side-navigation)
  - scss module 内层class类名也可以直接使用，如 `styles.hideDropIndicator`

## 0423

- [DOM变化，如何避免页面的闪烁 | 杨飞的博客](https://www.yangfei.org.cn/post/fab4823.html#more)
  - 简单来说，就有一个列表，你新增了一个元素，然后重新获取列表，界面会重新渲染，这时候有可能会导致页面闪烁。
  - 将数据修改设置为本地修改(redux或者setState)，而不是等服务端返回过来新的数据。

- [判断两个矩形相交以及求出相交的区域 - 莫水千流 - 博客园](https://www.cnblogs.com/zhoug2020/p/7451340.html)
  - 一般的思路就是判断一个矩形的四个顶点是否在另一个矩形的区域内。这个思路最简单，但是效率不高，并且存在错误
  - 另一种思路，那就是判断两个矩形的中心坐标的水平和垂直距离，只要这两个值满足某种条件就可以相交。
  - 矩形A的宽 Wa = Xa2-Xa1 高 Ha = Ya2-Ya1
  - 矩形B的宽 Wb = Xb2-Xb1 高 Hb = Yb2-Yb1
  - 矩形A的中心坐标 (Xa3, Ya3) = （ (Xa2+Xa1)/2 ，(Ya2+Ya1)/2 ）
  - 矩形B的中心坐标 (Xb3, Yb3) = （ (Xb2+Xb1)/2 ，(Yb2+Yb1)/2 ）
  - 所以只要同时满足下面两个式子，就可以说明两个矩形相交。
  - 1） | Xb3-Xa3 | <= Wa/2 + Wb/2
  - 2） | Yb3-Ya3 | <= Ha/2 + Hb/2

## 0422

- [SourceMap don't link to an src file but to webpack-internal:///[LINE\_NUMBER] · Issue #5186 · webpack/webpack](https://github.com/webpack/webpack/issues/5186)
  - In `eval-**-source-map` devtools you get a `webpack-internal://[module-id]:[line]:[column]`. 
  - In other devtools you get a url pointing to the bundle file.

## 0421

- [windows - Clipboard size limit - Stack Overflow](https://stackoverflow.com/questions/1321866/clipboard-size-limit)
  - Applications call GlobalAlloc(GMEM_MOVEABLE or GMEM_DDESHARE) to allocate the memory for data to be stored on the clipboard and make it available to other applications. 
  - For 32-bit applications GlobalAlloc can allocate blocks up to 2 GB in size or up to the amount of virtual memory the PC has, whichever is less. 
  - The Windows clipboard does not impose any other size limits.

- [Is there a maximum size for Windows clipboard data? | Hacker News](https://news.ycombinator.com/item?id=31667701)

## 0420

- [How do I merge two javascript objects together in ES6+? - Stack Overflow](https://stackoverflow.com/questions/13852852/how-do-i-merge-two-javascript-objects-together-in-es6)

```JS
export function isObject(item) {
  return (item && typeof item === 'object' && !Array.isArray(item) && item !== null);
}

/**
 * Deep merge two objects.
 * @param target
 * @param source
 */
export function mergeDeep(target, source) {
  if (isObject(target) && isObject(source)) {
    for (const key in source) {
      if (isObject(source[key])) {
        if (!target[key]) Object.assign(target, {
          [key]: {}
        });
        mergeDeep(target[key], source[key]);
      } else {
        Object.assign(target, {
          [key]: source[key]
        });
      }
    }
  }
  return target;
}
```

- [What does "go brrr" mean? : NoStupidQuestions](https://www.reddit.com/r/NoStupidQuestions/comments/kirugf/what_does_go_brrr_mean/)
  - It's a meme referring to actions done for short term benefit without regard for long term consequence. 
  - It started as a reaction to expansionary monetary policy enacted by the federal reserve during the market crash at the start of covid when they printed trillions of dollars in an attempt to correct the market.
  - The implication is that printing so much money will correct the market in the short term but cause hyperinflation later.

## 0415

- [html - jsx not working - Stack Overflow](https://stackoverflow.com/questions/37909134/nbsp-jsx-not-working)
  - `<Fragment>&nbsp;</Fragment>`; 
  - `<div>&nbsp;</div>`; 
  - `<div dangerouslySetInnerHTML={{__html: '&nbsp;'}} />`; 
  - `{'\u00A0'}`; 

- [三种空格unicode(\u00A0, \u0020, \u3000)表示的区别 - 简书](https://www.jianshu.com/p/4317e3749a13)
  - 不间断空格\u00A0, 主要用在office中, 让一个单词在结尾处不会换行显示, 快捷键ctrl+shift+space ; 
  - 半角空格(英文符号)\u0020, 代码中常用的; 
  - 全角空格(中文符号)\u3000, 中文文章中使用; 

## 0413

- [How to allow `<input type="file">` to accept only image files? - Stack Overflow](https://stackoverflow.com/questions/3828554/how-to-allow-input-type-file-to-accept-only-image-files)

```HTML
<input id="imageInput" accept="image/*" onChange="processFile(imageInput)" name="upload-photo" type="file" />
```

```JS
processFile(imageInput) {
  if (imageInput.files[0]) {
    const file: File = imageInput.files[0];
    var pattern = /image-*/;

    if (!file.type.match(pattern)) {
      alert('Invalid format');
      return;
    }

    // here you can do whatever you want with your image. Now you are sure that it is an image
  }
}
```

## 0412

- [open the file upload dialogue box onclick the image - Stack Overflow](https://stackoverflow.com/questions/22292410/open-the-file-upload-dialogue-box-onclick-the-image)

```HTML
<input type="file" id="imgUpload" style="display:none" />
<label for='imgUpload'> <button id="OpenImgUpload">Image Upload</button></label>
<!-- 
  On click of for= attribute will automatically focus on "file input" and upload dialog box will open
 -->

<a href="javascript:document.querySelector('input#imgUpload').click()">OR HERE</a>
```

## 0411

- [linux shell: The Set Builtin (Bash Reference Manual)](https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin.html)
  - The `set` command is a shell builtin command that is used to set and unset a value of the local variables in shell.
  - set -e
    - Exit immediately if a pipeline, which may consist of a single simple command, a list (see Lists of Commands), or a compound command returns a non-zero status.
  - set -x
    - Print a trace of simple commands, for commands, case commands, select commands, and arithmetic for commands and their arguments or associated word lists after they are expanded and before they are executed.

## 0410

- [colors - CSS hexadecimal RGBA? - Stack Overflow](https://stackoverflow.com/questions/7015302/css-hexadecimal-rgba)
  - `#rrggbbaa` notation is fully supported in Chrome 62+ and all other evergreen browsers
  - CSS Color Module Level 4 will probably support 4 and 8-digit hexadecimal RGBA notation!

## 0409

- [How to check null and undefined in Typescript and save the type info? - Stack Overflow](https://stackoverflow.com/questions/52095153/how-to-check-null-and-undefined-in-typescript-and-save-the-type-info)

```typescript
function isDefined<T>(value: T | undefined | null): value is T {
  return <T>value !== undefined && <T>value !== null;
}
```

## 0407

- [reactjs - How do I dynamically set HTML5 data- attributes using react? - Stack Overflow](https://stackoverflow.com/questions/27285856/how-do-i-dynamically-set-html5-data-attributes-using-react)
  - 2 options
  - `<Option data-img-src='value'   />` Don't use camel case
  - `<Option dataImgSrc='value'   />` Or use camel case

## 0405

- ### [JavaScript 里最大的安全的整数为什么是2的53次方减一？ - 知乎](https://www.zhihu.com/question/29010688)

- IEEE754规定，双精度浮点数的有效数字是52位
  - sign（S）：符号位，0是正数，1是负数
  - exponent（E）：指数位
  - fraction（F）：有效数字，IEEE754规定，在计算机内部保存有效数字时，默认第一位总是1，所以舍去，只保留后面的部分。
    - 比如保存1.01，只存01，等读取的时候再把第一位1加上去。所以52位有效数字实际可以存储53位。

- javascript 里数字类型只有一种， Number 类型，也就是64-bit 的浮点数
- javascript 里对整数的表示等同于双精度浮点数（64-bit）对整数的表示
- “安全”意思是说能够one-by-one表示的整数，也就是说在(-2^53, 2^53)范围内，双精度数表示和整数是一对一的，反过来说，在这个范围以内，所有的整数都有唯一的浮点数表示，这叫做安全整数
- 2^53是这样存的：
  - 符号位：0 指数：53 尾数：1.000000...000 （小数点后一共52个0）
- 2^53-1是这样存的：
  - 符号位：0 指数：52 尾数：1.111111....111 （小数点后一共52个1）
- 2^53+1：
  - 符号位：0 指数：53 尾数：1.000000...000 （小数点后一共52个0）
  - 注意到，2^53+1的存储和2^53一样。这样就不再“一一对应”

- ### [linux screen 命令详解](https://www.cnblogs.com/mchina/archive/2013/01/30/2880680.html)
  - 系统管理员经常需要SSH 或者telent 远程登录到Linux 服务器，经常运行一些需要很长时间才能完成的任务，比如系统备份、ftp 传输等等。
  - 通常情况下我们都是为每一个这样的任务开一个远程终端窗口，因为它们执行的时间太长了。必须等待它们执行完毕，在此期间不能关掉窗口或者断开连接，否则这个任务就会被杀掉，一切半途而废了。
  - GNU Screen是一款由GNU计划开发的用于命令行终端切换的自由软件。用户可以通过该软件同时连接多个本地或远程的命令行会话，并在其间自由切换。
  - GNU Screen可以看作是窗口管理器的命令行界面版本。它提供了统一的管理多个会话的界面和相应的功能。
  - 只要Screen本身没有终止，在其内部运行的会话都可以恢复。
    - 这一点对于远程登录的用户特别有用——即使网络连接中断，用户也不会失去对已经打开的命令行会话的控制。只要再次登录到主机上执行screen -r就可以恢复会话的运行。
    - 同样在暂时离开的时候，也可以执行分离命令detach，在保证里面的程序正常运行的情况下让Screen挂起（切换到后台）。这一点和图形界面下的VNC很相似。

- [linux Screen User’s Manual: Overview](https://www.gnu.org/software/screen/manual/html_node/Overview.html)
  - Screen is a full-screen window manager that multiplexes a physical terminal between several processes, typically interactive shells. Each virtual terminal provides the functions of the DEC VT100 terminal

## 0404

- [node.js 向下取整 - CNode技术社区](https://cnodejs.org/topic/64214ce30072087f7c9e50a9)
  - 发现了个奇怪的现象， 很多人都用的取整方式
    - ~~(2418473332.1)， 0|(2418473332.1) 竟然是负数 -1876493964；
  - js中位操作是当作Int32的，用 Math.floor() 就ok

## 0401

- [make a vertical separator line in HTML/CSS - Stack Overflow](https://stackoverflow.com/questions/61337079/make-a-vertical-separator-line-in-html-css)
  - 竖向分隔线很多案例使用div，可以使用hr

```HTML
<hr style="width:100px; transform:rotate(90deg);">
```

# dev-03

## 0331

- [typescript - How to check if a given value is in a union type array - Stack Overflow](https://stackoverflow.com/questions/50085494/how-to-check-if-a-given-value-is-in-a-union-type-array)
  - 常见场景 isAvailable  = (item:string) => array.includes(item)
  - array是union 类型数组
  - 此时 indexOf/includes 都会被ts警告，可行的方法是用 find
  - The accepted answer uses type assertions/casting but from the comments it appears the OP went with a solution using `find` that works differently

```typescript
const configKeys = ['foo', 'bar'] as const;
type ConfigKey = typeof configKeys[number]; // "foo" | "bar"

// Return a typed ConfigKey from a string read at runtime (or throw if invalid).
function getTypedConfigKey(maybeConfigKey: string): ConfigKey {
    const configKey = configKeys.find((validKey) => validKey === maybeConfigKey);
    if (configKey) {
        return configKey;
    }
    throw new Error(`String "${maybeConfigKey}" is not a valid config key.`);
}
```

- [How to use e.preventDefault inside onChange for select tag - Stack Overflow](https://stackoverflow.com/questions/61507666/how-to-use-e-preventdefault-inside-onchange-for-select-tag)
  - the `change` event in a select HTML element is not cancellable in order to call `preventDefault()`. If you log the event object you will see that it's `cancelable` property is set to `false`. Perhaps you can set the select element to disabled.

- [Webpack style-loader vs css-loader - Stack Overflow](https://stackoverflow.com/questions/34039826/webpack-style-loader-vs-css-loader)
  - The CSS loader takes a CSS file and returns the CSS with imports and url(...) resolved 
    - It doesn't actually do anything with the returned CSS.
  - the style-loader module automatically injects a `<script>` tag into the DOM, and that tag remains in the DOM until the browser window is closed or reloaded. 
    - The style loader takes CSS and actually inserts it into the page so that the styles are active on the page.
    - The style-loader module also offers a so-called "reference-counted API" that allows the developer to add styles and remove them later when they're no longer needed. 

- ### [Why are webpack loaders read from right to left in webpack? - Stack Overflow](https://stackoverflow.com/questions/32029351/why-are-loaders-read-from-right-to-left-in-webpack)

- I think it's important to note the difference between piping and composing. 
- In *nix environments, you can pipe commands from left-to-right:
  - cat file.txt | egrep cars > output.txt
- But in functional programming you can compose functions together and the functions will execute from right-to-left
  - var fn0 = compose(divide(2), add(3)); 
- It seems to me that Webpack is following the convention of composing versus piping as it's ordered right-to-left. Check out Ramda's docs for a technical specification

- [What is the loader order for webpack? - Stack Overflow](https://stackoverflow.com/questions/32234329/what-is-the-loader-order-for-webpack)
- loaders: ['loaderOne', 'loaderTwo', 'loaderThree']
  - means exactly the same as...
  - `loaderOne(loaderTwo(loaderThree(somefile.css)))`

## 0330

- umi打包不压缩
  - COMPRESS=none npx umi build

- 👀 new webpack. DefinePlugin
  - 设置的值要用`JSON.stringify()`包裹
  - Note that because the plugin does a direct text replacement, the value given to it must include actual quotes inside of the string itself. 
  - Typically, this is done either with alternate quotes, such as '"production"', or by using JSON.stringify('production')

```JS
new webpack.DefinePlugin({
  PRODUCTION: JSON.stringify(true),
  VERSION: JSON.stringify('5fa3b9'),
  BROWSER_SUPPORTS_HTML5: true,
  TWO: '1+1',
  'typeof window': JSON.stringify('object'),
  'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV),
});
```

- Bleeding Edge指那些前沿的却又不太成熟的、具有一定风险的事物，与cutting edge意思相近，多了一层风险的含义
  - 超前沿技术（Bleeding edge technology）也称为血刃科技，是具有风高险，还不一定可靠的技术，因此先行者要导入此技术时可能会有大量的支出

- [Solved - Export 'x' (imported as 'y') was not found in the filename (possible exports: X)](https://www.sharooq.com/solved-attempted-import-error-something-is-not-imported-from-some-file)
  - In the above code, we tried to import a default export with the named import "{ Sample }", which resulted in an error.

## 0329

- [css - Get button text on to one line - Stack Overflow](https://stackoverflow.com/questions/41248992/get-button-text-on-to-one-line)
  - `.btn { white-space: nowrap;  }`

- [grammar - "Are you sure to delete?" or "Are you sure you want to delete?" - English Language & Usage Stack Exchange](https://english.stackexchange.com/questions/222316/are-you-sure-to-delete-or-are-you-sure-you-want-to-delete)
  - Are you sure to delete this item?
    - this asks if they are definitely going to delete the item. This isn't something to ask the user
  - Are you sure you want to delete this item?
    - This asks not about what will happen (which is a question about the program) but what is desired (which is a question for the user). This is the one to go for.

## 0328

- dev-to
  - link hover未实现
  - 添加link时选择取消，需要处理, useClickOutside

- [各种高度clientHeight/scrollHeight/offsetHeight及应用 - 掘金](https://juejin.cn/post/6898575556796022797)
  - offsetWidth/offse tHeight 返回值包含 content + padding + border，效果与element.getBoundingClientRect() 相同
  - clientWidth/clientHeight 返回值包含 content + padding，如有滚动条，也不包含滚动条
  - scrollWidth/scrollHeight 返回值包含 content + padding + 溢出内容的尺寸
- getBoundingClientRect是DOM元素到浏览器可视范围的距离（不包含文档卷起的部分）。

- [scrollX、scrollY和scrollTop、scrollLeft的区别 | 会飞的猪9527](https://www.blogwxb.cn/scrollX%E3%80%81scrollY%E5%92%8CscrollTop%E3%80%81scrollLeft%E7%9A%84%E5%8C%BA%E5%88%AB/)
  - scrollX、scrollY只读不写; 
  - scrollTop、scrollLeft：可读可写

- [javascript - AddEventListener fires automatically upon assignment - Stack Overflow](https://stackoverflow.com/questions/27037272/addeventlistener-fires-automatically-upon-assignment)
  - 💡 非react场景也会出现此问题，document.addEventListener先注册，然后onClick触发的事件才冒泡才这里
  - What is happening is that when you click on your li element, the click is then transmitted to the container, and so on up to the window (the so-called event bubbling), and as you have added a event listener on the document (which is between your li and the window), it is being triggered.
  - The solution proposed here `e.stopPropagation` stops the propagation so that the click on the document is not triggered.

- [javascript - React document.addEventListener fire immediately - Stack Overflow](https://stackoverflow.com/questions/73604156/react-document-addeventlistener-fire-immediately)
  - You're handling a `SyntheticEvent` with your onClick handler and adding a native event listener at the `document` level. Adding the listener will complete before the event bubbles up to the top therefore you also see it execute for the original event.

- [css - Combining class selector with attribute selector - Stack Overflow](https://stackoverflow.com/questions/19498703/combining-class-selector-with-attribute-selector)

```CSS
a.button[class*=large] {
  font-size: 0.9em;
}
```

- [getBBox() vs getBoundingClientRect() vs getClientRects() - Stack Overflow](https://stackoverflow.com/questions/33688549/getbbox-vs-getboundingclientrect-vs-getclientrects)
  - `getBBox` is defined in the SVG specification it returns coordinates in the local coordinate system after the application of transforms.
  - getBoundingClientRect and getClientRects are defined in the CSSOM specification. Their main difference is that they return coordinates in the outer SVG coordinate system.
  - `getBoundingClientRect` returns a single rect that is the union of all the rects that `getClientRects` would return.

- some elements(like span tag) will have multiple `ClientRects` when they are wrapped into multiple lines
  - a `BoundingRect` is the union of ClientRects of a element.

- [html - Input size vs width - Stack Overflow](https://stackoverflow.com/questions/1480588/input-size-vs-width)
  - `<input name="txtId" type="text" size="20" />` 也可使用 style.width
  - You'll get more consistency if you use width

## 0327

- [html - css only 1 line of text - Stack Overflow](https://stackoverflow.com/questions/7546389/css-overflow-only-1-line-of-text)
  - Note that text-overflow only occurs when the container's overflow property has the value hidden, scroll or auto and white-space: nowrap; .

```CSS
text-overflow: ellipsis;
overflow: hidden;
white-space: nowrap;
```

- `z-index` CSS property sets the z-order of a positioned element and its descendants or flex items. 
  - z-index设置在flex-item元素E上时，E的position可以是static
  - 4.3. Flex Item Z-Ordering , ... and z-index values other than auto create a stacking context even if position is static.
    - Flex items paint exactly the same as inline blocks, except that order-modified document order is used in place of raw document order, and z-index values other than auto create a stacking context even if position is static.

## 0326

- [How to define css variables in `style` attribute in React and typescript - Stack Overflow](https://stackoverflow.com/questions/52005083/how-to-define-css-variables-in-style-attribute-in-react-and-typescript)

```typescript

style={{ "--my-css-var": 10 } as React.CSSProperties

declare module 'react' {
    interface CSSProperties {
        [key: `--${string}`]: string | number
    }
    // I ended up using this solution, thanks. One thing to note: it's possible to pass in values with more dashes than two (as a dash is a string).
    // style={{ ---color: 'red' }}
}
```

- [how to dynamically change global stylesheets in next js - Stack Overflow](https://stackoverflow.com/questions/68326186/how-to-dynamically-change-global-stylesheets-in-next-js)

```JSX

function MyApp({ Component, pageProps }) {
  const [theme, setTheme] = useState("light");

  useEffect(() => {
    if (theme == "dark") {
      import("primereact/resources/themes/light/theme.css");
    }
    if (theme == "light") {
      import("primereact/resources/themes/dark/theme.css");
    }
  }, [theme]);

  return (
    <ThemeContext.Provider value={[theme, setTheme]}>
        <Component {...pageProps} />
    </ThemeContext.Provider>
  );
}
```

- [javascript - ES6 variable import by reference or copy - Stack Overflow](https://stackoverflow.com/questions/46937494/es6-variable-import-by-reference-or-copy)
  - ES6 import/exports are actually bindings (references). 

## 0325

- [`<s>`: The Strikethrough element - HTML](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/s)
  - Use the `<s>` element to represent things that are no longer relevant or no longer accurate. 
  - However `<s>` is not appropriate when indicating document edits; for that, use the `<del>` and `<ins>` elements, as appropriate.

## 0324

- [reactjs - How to import standard DOM element props in React with Typescript - Stack Overflow](https://stackoverflow.com/questions/69079635/how-to-import-standard-dom-element-props-in-react-with-typescript)
  - `interface ExampleProps extends React.HTMLAttributes<HTMLDivElement> {`

- [reactjs - How do I restrict the type of React Children in TypeScript, using the newly added support in TypeScript 2.3? - Stack Overflow](https://stackoverflow.com/questions/44475309/how-do-i-restrict-the-type-of-react-children-in-typescript-using-the-newly-adde)

```typescript
interface TabbedViewProps {
    children?: React.ReactElement<TabProps>[] | React.ReactElement<TabProps>
}
```

- [Why don't `<button>` HTML elements have a CSS cursor pointer by default? - User Experience Stack Exchange](https://ux.stackexchange.com/questions/105024/why-dont-button-html-elements-have-a-css-cursor-pointer-by-default)
  - 👉🏻 W3C User Interface guidelines says the same thing again with “The cursor is a pointer that indicates a link”.
  - Apple’s Human Interface Guidelines states that the hand cursor should be used when “the content is a URL link”.

- [drop-shadow() - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/filter-function/drop-shadow)
  - similar to the box-shadow property. 
  - The box-shadow property creates a rectangular shadow behind an element's entire box, while the drop-shadow() filter function creates a shadow that conforms to the shape (alpha channel) of the **image** itself.

- [What is the difference between \`margin\` and \`padding\` in CSS? - Stack Overflow](https://stackoverflow.com/questions/2189452/what-is-the-difference-between-margin-and-padding-in-css)
  - TL; DR: By default I use margin everywhere, except when I have a border or background and want to increase the space inside that visible box.
  - To me, the biggest difference between padding and margin is that vertical margins auto-collapse, and padding doesn't.
  - The other two big differences are that padding is included in the click region and background color/image, but not the margin.

## 0323

- dev
  - 拖拽图标的位置在block左上角，而不是垂直居中

- [CSS: Flex and "min-width" - makandra dev](https://makandracards.com/makandra/66994-css-flex-and-min-width)
  - While the default min-width value is 0 (zero), for flex items it is auto. 
  - This can make block elements take up much more space than desired, even stretching their container beyond the screen edge on small screens.

- [Detecting which node is selected within a slate-react text editor - Stack Overflow](https://stackoverflow.com/questions/60708570/detecting-which-node-is-selected-within-a-slate-react-text-editor)
  - const selectedNode = editor.selection && Editor.node(editor, editor.selection.focus); 

- [获取鼠标位置（区分event对象中的 clientX、offsetX、screenX、pageX - 酷儿q - 博客园](https://www.cnblogs.com/Qooo/p/14124652.html)(https://segmentfault.com/a/1190000020949241)
  - page为页面的意思，页面的高度一般情况client游览器显示区域装不下，所以会出现垂直滚动条。
  - 鼠标距离页面初始page原点的长度。

## 0320

- slate Subsequent property declarations must have the same type. Property
  - 问题暂时解决方法是 将library中declare module slate注释掉，然后在应用层添加此声明

- [fix: replace typeof window checks with typeof document by redabacha · Pull Request · TanStack/virtual](https://github.com/TanStack/virtual/pull/516)
  - useLayoutEffect does nothing on the server warnings during ssr when using a deno runtime. this is because deno has a global window object available for browser compatibility (though is being considered for removal
  - this pr replaces all typeof window checks across all packages with typeof document instead which works in all environments.

- [PBFT Practical Byzantine Fault Tolerance 实用拜占庭容错 - 哪吒young - 博客园](https://www.cnblogs.com/NezhaYoung/p/16170948.html)
  - 实用拜占庭容错，是传统BFT的一种可用性实现，其在联盟链中有广泛应用，但由于pbft 不能动态添加删除节点且节点加入需要认证机制(女巫攻击), 时间复杂度等, 其在公链中其算法的效率, 功能仍然不足满足实际需求。
  - PBFT 适合有准入门槛(防止女巫攻击), 节点数量不多的联盟链
  - PBFT 最大容忍网络中 1/3的拜占庭节点
  - PBFT 的时间复杂度 O(n2), 节点数很多时性能急剧下降

- [了解区块链的基本（第一部分）：拜占庭容错(Byzantine Fault Tolerance)](https://medium.com/loom-network-chinese/%E4%BA%86%E8%A7%A3%E5%8C%BA%E5%9D%97%E9%93%BE%E7%9A%84%E5%9F%BA%E6%9C%AC-%E7%AC%AC%E4%B8%80%E9%83%A8%E5%88%86-%E6%8B%9C%E5%8D%A0%E5%BA%AD%E5%AE%B9%E9%94%99-byzantine-fault-tolerance-8a1912c311ba)
  - 每当一个新的交易被广播到网络中时，节点就可以选择将该交易包含在它们的帐簿副本中，或者忽略它。当组成网络的大多数成员统一意见时，达到了共识。
  - 简单讨论一下不可解的两个将军问题（Two Generals Problem）
    - 这个问题（1975首次发行，1978年被命名）描述了两个将军在攻击同一个敌人的场景。将军1号被认为是领导，而另一个被认为是跟随者。每个将军的军队都无法仅靠自己的力量成功打败敌军，所以他们需要合作并同一时间发起攻击。
    - 延伸到无限的ACK，两位将军将无法达成一致。
    - 两个将军问题已被证实无解。
  - 拜占庭将军问题
    - 它描绘了同一个场景，但两个以上的将军需要对攻打他们共同敌人的时间作出同意。增加的一层复杂性就是，其中一个或几个将军有可能是叛徒，意味着他们可以对他们的选择撒谎
    - 两个将军问题中领导者－跟随者的关系变成了指挥官－中尉的组合。为了在这里达成共识，指挥官和每个中尉必须就同一个决定达成一致（为了简单，只有攻击或撤退）。
    - 如果指挥官是叛徒，还是必须达成共识。结果，所有的中尉成为了多数票。
  - 定理：对于任意m，如果有多于3m的将军和至多m个叛徒，算法OM(m)达到共识。
    - 这说明只要2/3的成员是诚实的，算法就能达到共识。
    - 如果叛徒多于1/3，无法达到共识，这些军队无法协调他们的攻击，敌军胜利
    - 重要的是大多数中尉要选同一个决策，哪一个并不重要。
  - 拜占庭容错
    - 前面提到的算法，只要叛徒的数量不超过将军的三分之一，就是拜占庭容错。其他变形的存在使得解决问题更容易，包括使用数字签名或通过在网络中的对等体之间施加通信限制。

## 0319

- bullet list-item前的黑点，自身是cntEdit为false的button
  - 若使用::before伪元素实现黑点，则光标可点击到黑点左边
  - 若使用button普通内容实现，则光标点击不到光标左边，交互正常

- [TypeScript 2.8.3 Type must have a Symbol.iterator method that returns an iterator - Stack Overflow](https://stackoverflow.com/questions/50234481/typescript-2-8-3-type-must-have-a-symbol-iterator-method-that-returns-an-iterato)
  - "lib": [ "es5", "es6", "dom", "dom.iterable" ]

## 0318

- Array.prototype.reverse()
  - Return the reference to the original array, now reversed. 
  - Note that the array is reversed in place, and no copy is made.

- [css button set to unclickable - Stack Overflow](https://stackoverflow.com/questions/46566019/css-button-set-to-unclickable)
  - pointer-events: none; 
  - 默认值 pointer-events: auto; 

## 0317

- dev-to
  - 🚨 修复中文输入法

- [How to iterate over a WeakMap? - Stack Overflow](https://stackoverflow.com/questions/32402837/how-to-iterate-over-a-weakmap)
  - A JavaScript WeakMap does not allow you to get the key, or the length or size, by design.
  - Is it possible to nevertheless loop over entries in some way ?
  - If not .. how does the Chrome console do this ?
- No, as you say, the contents of a WeakMap are not accessible by design, and there is no iterablity.
- The console uses the debugging API of the JS engine, which allows access to the internals of objects (also to promise states, wrapped primitives, etc.) and many more.

- Things are moving and it will soon be possible to create iterable week maps thanks to weak refs. See the iterable WeakMap example in the tc39 weakrefs proposal.
  - (note that it is already possible with nodejs v12.?.? using --harmony-weak-refs flag)
  - WeakRef and FinalizationRegistry are now Stage 4, since the July 2020 TC39 meeting

- [pipeline执行引擎和一些工程优化 - 知乎](https://zhuanlan.zhihu.com/p/614907875)

## 0316

- [Changing the stroke color for an inline SVG - Stack Overflow](https://stackoverflow.com/questions/37940282/changing-the-stroke-color-for-an-inline-svg)
  - The CSS in the SVG is inline CSS and so is being applied after your stylesheet and thus is overriding it.
  - The simplest solution is to extract the CSS from the SVG and put it **all in your stylesheet**

```svg
<svg class="highlight" width="86" height="68" viewBox="0 0 85.7 68.5">
  <polygon points="11 60.7 74.7 60.7 42.8 4.4 " style="fill:none;stroke-width:3;stroke:#491EC4"/>
</svg>
```

```css
.highlight:hover {
  background-color: pink;
}

.highlight:hover polygon {
  stroke: red !important;
}
```

## 0315

- [合成事件 - 图解React](https://7kms.github.io/react-illustration-series/main/synthetic-event/)
  - 从v17.0.0开始, React 不会再将事件处理添加到 document 上, 而是将事件处理添加到渲染 React 树的根 DOM 容器中.
  - 无论是在document还是根 DOM 容器上监听事件, 都可以归为事件委托(代理)
  - 注意: react的事件体系, 不是全部都通过事件委托来实现的. 有一些特殊情况, 是直接绑定到对应 DOM 元素上的(如:scroll, load), 它们都通过listenToNonDelegatedEvent函数进行绑定.

- [javascript - what's different between Object.prototype.toString.call and typeof - Stack Overflow](https://stackoverflow.com/questions/31459821/whats-different-between-object-prototype-tostring-call-and-typeof)
  - You can't override what gets returned from typeof

```JS
typeof(new Array()) === "object";
typeof(new Date()) === "object";
typeof(new RegExp()) === "object";

Object.prototype.toString.call(new Array()).slice(8, -1) === "Array";
Object.prototype.toString.call(new Date()).slice(8, -1) === "Date";
Object.prototype.toString.call(new RegExp()).slice(8, -1) === "RegExp";
```

- [wasm调试 webAssembly介绍大全 - Bigben - 博客园](https://www.cnblogs.com/bigben0123/articles/15753240.html)
  - C/C++ 到 WebAssembly 代码的编译器 Emscripten 则支持在编译时，为代码注入相关的调试信息，生成对应的 source map，
  - 然后安装 Chrome 团队编写的 C/C++ Devtools Support 浏览器扩展，就可以使用 Chrome 开发者工具调试 C/C++ 代码了。

## 0313

- [css - Chrome DevTools converts all HEX Colors to RGB - Stack Overflow](https://stackoverflow.com/questions/29869426/chrome-devtools-converts-all-hex-colors-to-rgb)
  - open preferences, change Color format 

- [Font-size <12px doesn't have effect in Google Chrome - Stack Overflow](https://stackoverflow.com/questions/2295095/font-size-12px-doesnt-have-effect-in-google-chrome)
  - Chrome and Firefox now allow a minimum font size setting of zero. 
  - **Chrome 73** had downstream problems with this, and since then Chrome changed their policy and user interface for this setting. 
  - I don't know the history on Firefox, and I don't know the state of this setting on Safari or other browsers.

- [Urban Dictionary: shit-faced](https://www.urbandictionary.com/define.php?term=shit-faced)
  - The point at which you have consumed so much alcohol, that you are incoherent(无逻辑的；不连贯的), have difficulty remembering simple things
  - Being 'shit-faced' is usually an experience you only want to try once, and never again.

## 0312

- dev-to
  - 将rga的id从string改为number

- crypto.randomUUID(); 
  - 返回 A string containing a randomly generated, 36 character long v4 UUID.
  - 36 = 8-4-4-4-12 (算上4个连字符)

```JS
1 > null // true
0 > null // false
'aa' > null // false
  '0' > null // false
```

- [How do you JSON.stringify an ES6 Map? - Stack Overflow](https://stackoverflow.com/questions/29085197/how-do-you-json-stringify-an-es6-map)

```JS
jsonText = JSON.stringify(Array.from(map.entries()))

map = new Map(JSON.parse(jsonText))
```

- [Property 'replaceAll' does not exist on type 'string' - Stack Overflow](https://stackoverflow.com/questions/63616486/property-replaceall-does-not-exist-on-type-string)
  - "lib": [ ..., "ESNext. String" ]
  - `replace(/-/g, '')`

- [fixed-length array with optional items in Typescript interface - Stack Overflow](https://stackoverflow.com/questions/44461636/fixed-length-array-with-optional-items-in-typescript-interface)
  - late to the party but one can do simply `type X = [string, string?, number?]` to have optional typed array members 

```typescript
[K in keyof T]?: {
  0: T[K];
  1?: ValidatorFn | ValidatorFn[];
  2?: AsyncValidatorFn | AsyncValidatorFn[];
};

```

## 0310

- [Types when destructuring arrays - Stack Overflow](https://stackoverflow.com/questions/31923739/types-when-destructuring-arrays)

```typescript
const [nodes, counts] = getNodesAndCounts(); // problematic line needed type

const [nodes, counts] = <Node[], number[]>getNodesAndCounts();

// 💡 for-of 解构的折中方案，还可尝试明确backend[0]的类型
for (const [k, v] of Object.entries<any>(backend[0])) 
```

- [Difference between index signature and Record for empty object?](https://stackoverflow.com/questions/54100025/difference-between-index-signature-and-record-for-empty-object)
  - `Record<"A" | "B", boolean>` to get the type `{ A: boolean, B: boolean }` 简洁
  - The main part of this question (in my reading) is whether the two types are the same. 
  - They are obviously declared in different ways but are they the same type. 
  - While they are obviously **compatible** (that is you can assign one to the other and vice-versa) the question is are there corner cases where this is not possible.

## 0308

### [图解Gossip: 可能是最有趣的一致性协议 - charlieroro - 博客园](https://www.cnblogs.com/charlieroro/articles/12655967.html)

- Gossip协议是一个通信协议，一种传播消息的方式，灵感来自于：瘟疫、社交网络等。
- 使用Gossip协议的有：Redis Cluster、Consul、Apache Cassandra等。
- Gossip协议基本思想
  - 一个节点想要分享一些信息给网络中的其他的一些节点。
  - 于是，它周期性的随机选择一些节点，并把信息传递给这些节点。
  - 这些收到信息的节点接下来会做同样的事情，即把这些信息传递给其他一些随机选择的节点。
  - 一般而言，信息会周期性的传递给N个目标节点，而不只是一个。
  - 这个N被称为fanout（这个单词的本意是扇出）。
- Gossip协议的主要用途就是信息传播和扩散：即把一些发生的事件传播到全世界。它们也被用于数据库复制，信息扩散，集群成员身份确认，故障探测等。
- Gossip协议下，没有任何扮演特殊角色的节点（比如leader等）。任何一个节点无论什么时候下线或者加入，并不会破坏整个系统的服务质量。
- 然而，Gossip协议也有不完美的地方，例如，拜占庭问题（Byzantine）。
  - 即，如果有一个恶意传播消息的节点，Gossip协议的分布式系统就会出问题。

## 0307

- [Google diff-match-patch源代码解析：听说比GNU diff-patch更厉害？](https://blog.csdn.net/APPTITE/article/details/107691493)
  - 语义化优先的diff计算
  - 效率优先的diff计算（可以设置diff单元的最小粒度）
  - 设置ddl时间的diff计算（在n秒内完成diff计算操作）

## 0306

- [How to change the Content of a <textarea> with JavaScript - Stack Overflow](https://stackoverflow.com/questions/1642447/how-to-change-the-content-of-a-textarea-with-javascript)
  - document.getElementById('myTextarea').value = ''; 
  - myTextArea.innerHTML = ''; 
  - myTextArea.innerText = ''; 

- [Add "contenteditable" attribute to element using Javascript? - Stack Overflow](https://stackoverflow.com/questions/20906895/add-contenteditable-attribute-to-element-using-javascript)

```JS
elemText.contentEditable = "true";
elemText.setAttribute("contenteditable", "true");
```

- [Why does JSON.parse fail with the empty string? - Stack Overflow](https://stackoverflow.com/questions/30621802/why-does-json-parse-fail-with-the-empty-string)

```JS
JSON.parse('""'); // ✅ 解析为空字符串
JSON.parse(''); // SyntaxError: Unexpected end of JSON input
```

- [reactjs - How to avoid \`loaded two copies of React\` error when developing an external component? - Stack Overflow](https://stackoverflow.com/questions/33157904/how-to-avoid-loaded-two-copies-of-react-error-when-developing-an-external-comp)
  - I believe the answer is to specify react and react-dom as `peerDependencies` in your external component's package.json

## 0305

- [认识 Range 和 Selection 对象](https://coldstone.fun/post/2020/12/05/selection-and-range/)
  - 使文档中某些内容不可选
  - 使用 CSS 属性 `user-select: none` 不允许选择从 elem 开始，但是用户可以在其他地方开始选择，并将 elem 包含在内。
  - 阻止 `onselectstart` 或 `mousedown` 事件中的默认行为，这样可以防止在 elem 上开始选择，但是访问者可以在另一个元素上开始选择，然后扩展到 elem。
  - 使用 `document.getSelection().empty()` 方法在选择发生后清除选择范围。

## 0304

- [Object destructuring with types in TypeScript](https://flaviocopes.com/typescript-object-destructuring/)
  - `const { name, age }: { name: string; age: number } = body.value;`

- dev-to
  - 测试光标进出表格

## 0301

- [XML解析之SAX方式解析xml文件 - Chen洋 - 博客园](https://www.cnblogs.com/cy0628/p/14990908.html)
  - DOM , SAX属于基础方法，是官方提供的平台无关的解析方式；
  - JDOM，DOM4J属于扩展方法，他们是在基础的方法上扩展出来，只适用于Java平台；
  - SAX解析方式会逐行地去扫描XML文档，当遇到标签时会触发解析处理器，采用事件处理的方式解析XML (Simple API for XML) ，不是官方标准，但它是 XML 社区事实上的标准
  - 优点是：在读取文档的同时即可对XML进行处理，不必等到文档加载结束，相对快捷。不需要加载进内存，因此不存在占用内存的问题，可以解析超大XML。
  - 缺点是：只能用来读取XML中数据，无法进行增删改。

- [[翻译] Makefile - 失落的艺术 - 知乎](https://zhuanlan.zhihu.com/p/34284231)
  - 挺好，不过在使用 nodejs 的情况下，没有道理不使用 npm scripts (作为 Makefile 的替代品) 
  - nodejs脚本也是跨平台的，但依赖js语言，makefile有自己的语法规则

- [快速的理解MakeFile+读懂一个MakeFile - 知乎](https://zhuanlan.zhihu.com/p/350297509)
  - Make 是一种通用的构建工具，它自40年前推出以来一直在不断完善和改进。 
  - Make 非常擅长简洁的表现构建步骤，此外它并不特定用于 JavaScript 项目。 
  - 它非常适合增量构建，在更改大型项目中的一个或两个文件后重新构建时，Make 可以节省大量时间。

- [plugin-react: is it using esbuild or babel? · vitejs/vite · Discussion #8142](https://github.com/vitejs/vite/discussions/8142)
  - plugin-react uses babel (you can see the code here), there are several pieces of the React ecosystem that still requires it (babel isn't used in Vue or Svelte). 
  - esbuild is still used by Vite when you are using this plugin though.
  - A production build in general is using rollup, so you can't expect it to be as fast as bundling with esbuild. 

- Vite’s default React HMR is still babel-based, _202210
- https://twitter.com/youyuxi/status/1585040270957379585?lang=en
  - while Next/turbopack use swc/rust-based transform, so the HMR performance difference is a bit of apples to oranges.
  - Vite can switch to the swc/rust transform if necessary, we currently chose not to do that because adding swc to the deps list is extra weight, and even without it HMR is fast enough.
  - In the long run we may also consider using turbopack under the hood to replace esbuild/Rollup (where suitable), due to its strong caching capabilities.
  - [feat!: transform jsx with esbuild instead of babel by rtsao · Pull Request #9590 · vitejs/vite_202211](https://github.com/vitejs/vite/pull/9590)
# dev-02

## 0228

- [XMPP协议实现原理介绍 - Healtheon - 博客园](https://www.cnblogs.com/hanyonglu/archive/2012/03/04/2378956.html)
  - XMPP（Extensible Messageing and Presence Protocol：可扩展消息与存在协议）是目前主流的四种IM（IM：instant messaging, 即时消息）协议之一，其他三种分别为：即时信息和空间协议(IMPP)、空间和即时信息协议(PRIM)、针对即时通讯和空间平衡扩充的进程开始协议SIP(SIMPLE)。
  - 在这四种协议中，XMPP是最灵活的。XMPP是一种基于XML的协议，它继承了在XML环境中灵活的发展性。
  - 其实XMPP 是一种很类似于http协议的一种数据传输协议，它的过程就如同“解包装--〉包装”的过程，用户只需要明白它接受的类型，并理解它返回的类型，就可以很好的利用xmpp来进行数据通讯。
  - 1)客户机/服务器通信模式；(2)分布式网络；(3)简单的客户端；(4)XML的数据格式。

## 0227

- 🤔 输入字母时，为什么beforeinput的selection为5，onChange方法里的selection为6，哪里更新的
  - 首先确认更新范围，onChange执行后useEffect才执行将 slateSel-TO-domSel，所以更新sel发生在渲染前
  - 排查定位到，执行op `insert_text`时，顺便就把selection更新了
  - 不要在op-text单独执行op-selection来更新sel

- Unlike a `Range`, a `StaticRange` represents a range which is fixed in time; 
  - it does not change to try to keep the same content within it as the document changes. 
  - If any changes are made to the DOM, the actual data contained within the range specified by a StaticRange may change. 
  - This lets the user agent avoid a lot of work that is unnecessary if the web app or site doesn't need a live-updating range.

## 0225

- [JavaScript中对光标和选区的操作 - 前端简单说 - SegmentFault 思否](https://segmentfault.com/a/1190000040211043)
  - 使用 ::selection 选择器可以匹配被选中的部分。
  - 目前只有一小部分 CSS 属性可以用于 ::selection 选择器：
  - color, background-color, text-shadow

- [重新认识Selection和Range | 漫漫前端路](https://blog.renwangyu.com/2020/10/06/selection-and-range/)

- `getRootNode()` method of the Node interface returns the context object's root, which optionally includes the shadow root if it is available.
  - 一般返回`document`对象，而不是document.documentElement

```JS
document.body.ownerDocument === document // true

document.body.ownerDocument === document.body.getRootNode() // true
```

- [css - How can I inspect and tweak :before and :after pseudo-elements in-browser? - Stack Overflow](https://stackoverflow.com/questions/10174719/how-can-i-inspect-and-tweak-before-and-after-pseudo-elements-in-browser)
  - getComputedStyle(document.querySelector('html > body'), ':before'); 
  - getComputedStyle(element, pseudoElt)

- HTMLElement.contextMenu 
  - Deprecated
  - refers to the context menu assigned to an element using the contextmenu attribute
  - The menu itself is created using the `<menu>` element
  - Deprecated: The `contextmenu` global attribute is the `id` of a `<menu>` to use as the contextual menu for this element.

- contextmenu event fires when the user attempts to open a context menu
  - not deprecated

- [Difference between microtask and macrotask within an event loop context - Stack Overflow](https://stackoverflow.com/questions/25915634/difference-between-microtask-and-macrotask-within-an-event-loop-context)
  - Macro tasks include keyboard events, mouse events, timer events (setTimeout) , network events, Html parsing, changing Urletc. A macro task represents some discrete and independent work. micro task queue has higher priority so macro task will wait for all the micro tasks are executed first.
  - Microtasks, are smaller tasks that update the application state and should be executed before the browser continues with other assignments such as re-rendering the UI. Microtasks include promise callbacks and DOM mutation changes. Microtasks enable us to execute certain actions before the UI is re-rendered, thereby avoiding unnecessary UI rendering that might show an inconsistent application state.
  - Separation of macro and microtask enables the event loop to prioritize types of tasks; for example, giving priority to performance-sensitive tasks.

## 0224

- [Difference between mousedown and click in jquery - Stack Overflow](https://stackoverflow.com/questions/19109754/difference-between-mousedown-and-click-in-jquery)
  - onMouseDown will trigger when either the left or right (or middle) is pressed.
  - onClick will only trigger when the left mouse button is pressed and released on the same object.
  - order: onMouseDown, onMouseUp, then onClick

## 0223

- [Phind: AI search engine](https://phind.com/)
  - The AI search engine for developers

### [How to Measure JavaScript Execution Time](https://dev.to/saranshk/how-to-measure-javascript-execution-time-5h2)

- Using Date.now() that returns the total number of milliseconds elapsed since the Unix epoch

- console.time() method starts a timer with a label. And a subsequent call to the console.timeEnd() method with the same label will output the time elapsed since the method was started.

- Console timers do not provide high accuracy. If we want accuracy in 1-millisecond increments, we can use high-resolution timers like performance.now().

## 0222

- [The dataset cannot set dashed names · Issue #1031 · snabbdom/snabbdom](https://github.com/snabbdom/snabbdom/issues/1031)
  - the easiest correction might be using setAttribute/removeAttribute only.
- [dataset module · Issue #90 · snabbdom/snabbdom](https://github.com/snabbdom/snabbdom/issues/90)
  - Both `{attrs: {'data-foo': foo}}` and `{dataset: {foo: 'foo'}}` modify the underlying HTML so I am not sure if it is not be better to simply use some random custom property instead: {props: {datasetfoo: 'foo'}}.

- [Is there a way selecting MULTIPLE areas of text with JS in Chrome and/or IE? - Stack Overflow](https://stackoverflow.com/questions/4985284/is-there-a-way-selecting-multiple-areas-of-text-with-js-in-chrome-and-or-ie)
  - No. Of the major browsers, only Firefox supports multiple ranges within the user selection. 
  - Other browsers (WebKit, Opera, IE9) do have the Selection API to support multiple ranges but do not currently support it. 
  - WebKit is apparently not planning to add support any time soon. As to Opera and IE, I have no idea.

- [How to add more than 1 range to a windows.selection object in chrome browser? - Stack Overflow](https://stackoverflow.com/questions/54437485/how-to-add-more-than-1-range-to-a-windows-selection-object-in-chrome-browser)
  - Not really, actually it's even been removed from specs. This is an old relic from Netscape that FF did keep and which made the Selection API have things like rangeCount or removeAllRanges(), but this behavior is non-standard. 
  - 💡 To do what you wish, you'd have to keep yourself track of what the selected cells were, and to merge their content in a single hidden Node that you'll use as the source for execCommand('copy'). That's a bit of work though...

- [Can you set and/or change the user’s text selection in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/4183401/can-you-set-and-or-change-the-user-s-text-selection-in-javascript)
  - is it possible to select different ranges simultaneously. I want to be able to select multiple parts of text that are discontinuous
  - Yes, but only in Firefox. Call addRange() for each range you want to select

- [Unable to add 2nd selection range (Google Chrome) - Stack Overflow](https://stackoverflow.com/questions/61962880/unable-to-add-2nd-selection-range-google-chrome)
  - in default chrome, multiple selection ranges isn't supported. But this extension can enable it.

## 0219

- [Height limitations for browser vertical scroll bar - Stack Overflow](https://stackoverflow.com/questions/34931732/height-limitations-for-browser-vertical-scroll-bar)
  - The maximum limit for height obtained to render browser scroll bar have various values in all browsers. If increasing 1px from the limited height then the browser scroll won't render in the page.
  - FF: 17895697px
  - IE: 10737418px
  - In Chrome there is no problem to render the scroll bar, but it have always 33554400px height in the layout.

- [javascript - Will ref callbacks always be invoked in the order they are declared in render()? - Stack Overflow](https://stackoverflow.com/questions/60549295/will-ref-callbacks-always-be-invoked-in-the-order-they-are-declared-in-render)
  - React will call the ref callback with the DOM element when the component mounts, and call it with null when it unmounts. Refs are guaranteed to be up-to-date before componentDidMount or componentDidUpdate fires.

## 0215

- You can call `Document.getSelection()`, which works identically to `Window.getSelection()`.
  - getSelection() doesn't work on the content of `<textarea>` and `<input>` elements in Firefox, Edge (Legacy) and Internet Explorer.
  - `HTMLInputElement.setSelectionRange()` or the `selectionStart` and `selectionEnd` properties could be used to work around this.

## 0214

- [How can I use an object literal to make an instance of a class without useing the constructor in JavaScript ES6? - Stack Overflow](https://stackoverflow.com/questions/47881111)
  - I'll guess that this exercise is looking for a solution that uses `__proto__` as an object literal key
  - 👉🏻 The proper solution is to use `Object.create`

```JS
var fakePoint = {
  __proto__: Point.prototype,
  x: Math.random(),
  y: Math.random()
};
console.log(fakePoint instanceof Point) //true
```

- [What is the difference between typeof and instanceof and when should one be used vs. the other? - Stack Overflow](https://stackoverflow.com/questions/899574)
  - Use instanceof for custom types
  - Use typeof for simple built in types

- [Why does instanceof return false for some literals? - Stack Overflow](https://stackoverflow.com/questions/203739/why-does-instanceof-return-false-for-some-literals)
  - Primitives are a different kind of type than objects created from within Javascript.

```JS
var color1 = new String("green");
color1 instanceof String; // returns true
var color2 = "coral";
color2 instanceof String; // returns false (color2 is not a String object)
```

## 0213

- [Impossible to define static 'length' function on class · Issue #442 · microsoft/TypeScript](https://github.com/microsoft/typescript/issues/442)
  - I don't think the properties name, caller and length are doable. They are read-only properties and can't be overridden. All assignments to them will be ignored.

## 0210

- [rg process taking up all my CPU 100% · Issue #98594 · microsoft/vscode](https://github.com/microsoft/vscode/issues/98594)
  - `"search.followSymlinks": false` solved my issue too

## 0208

- [Wechaty 实现微信机器人的原理 - 知乎](https://zhuanlan.zhihu.com/p/567250559)

- [各类期刊的区别 | J. Xu](https://xujinzh.github.io/2020/10/09/journal-or-transactions/)
  - Journal学报最典型的叫法， 刊登关于某特殊主题的文章的期刊。要求有很大的创新点，比较详细的公式推导。因 Journal 面向的读者较广泛，因此发表在其上的文章需要对背景知识有更加全面的介绍。
  - Transactions 本意为商业交易和谈判，引申为公开发表的大会记录。后来有汇刊的意思。 其具体到一个相对较细的专业方向上，发表在 transactions 上的文章需要有很大的创新和详细的公式推导。
  - Proceedings 表示某行动，或行动过程或方式，引申意之一是学术团体或其他正规团体会议所讨论问题的记录，进一步有会议论文集的意思。有会刊、记录、会议录的意思。但是 IEEE 的 Proceedings 也变成了期刊 (出版周期相对长)，并没有会议支撑。

## 0205

- npm ERR! Invalid comparator: github:thecodrr/htmlparser2
  - [[BUG] \`overrides\` in \`package.json\` do not allow file paths of any kind (including fake ones) · Issue #5843 · npm/cli](https://github.com/npm/cli/issues/5843)
  - I really hope this can be fixed. Overrides otherwise only fully work in npm v8.
  - npm v9 最新版已修复
# dev-01

## 0126

- SyntaxError: Named export 'WebSocketServer' not found. The requested module 'ws' is a CommonJS module, which may not support all module.exports as named exports.
  - 原因是 ws 不在dependencies列表里

- ### [Why is there no same-origin policy for WebSockets? Why can I connect to ws://localhost? - Stack Overflow](https://stackoverflow.com/questions/23674199)
- WebSockets can cross domain communication, and they are not limited by the SOP (Same Origin Policy).
- The same security issue you described can happen without WebSockets.
- The evil JS can:
  - Create a script/image tag with a URL to evil.tld and put data in the query string.
  - Create a form tag, put the data in the fields, and invoke the "submit" action of the form, doing an HTTP POST, that can be cross domain. AJAX is limited by the SOP, but normal HTTP POST is not. Check the XSRF web security issue.
- If something injects javascript in your page, or you get malicious javascript, your security is already broken.

- SOP/CORS does not apply to WebSocket, but browsers will send an `origin` header that contains the hostname of the server that served the HTML with the JS that opened the WebSocket connection. A WebSocket server can then restrict access by checking `origin`.

## 0123

- [Difference between `process.nextTick` and `queueMicrotask` - Stack Overflow](https://stackoverflow.com/questions/55467033/difference-between-process-nexttick-and-queuemicrotask)
  - It is the same, in the way of both of them are to execute a task just after the execution of the current function or script.
  - 👉🏻 They have **different queues**. The nextTick's queue is managed by node and the microtask one is managed by v8.
  - The nextTick queue is checked first after the current function/script execution, and then the microTask one.
  - There is no performance gain, the difference is that the nextTick queue will be checked first after the function/script execution 

## 0119

- 💡 a global event emitter (could be replaced by redis, etc)

## 0121

- Downloading ripgrep failed: TypeError [ERR_INVALID_PROTOCOL]: Protocol "https:" not supported. Expected "http:"
  - https://github.com/microsoft/vscode-ripgrep/issues/26#issuecomment-1187663914

```
1. Clone ripgrep locally: git clone git@github.com:microsoft/vscode-ripgrep ~/vscode-ripgrep
2. run yarn in that folder (this seems to work even behind proxy)
3. cp bin/rg ~/vscode-repo-path/node_modules/@vscode/ripgrep
4. run yarn in your vscode repo path again
```

## 0118

### [既然有 HTTP 请求，为什么还要用 RPC 调用？ - 知乎](https://www.zhihu.com/question/41609070)

- rpc是远端过程调用，其调用协议通常包含传输协议和序列化协议。
  - 传输协议包含: 如著名的 [gRPC](grpc / grpc.io) 使用的 http2 协议，也有如dubbo一类的自定义报文的tcp协议。
  - 序列化协议包含: 如基于文本编码的 xml json，也有二进制编码的 protobuf hessian等
- 为什么要使用自定义 tcp 协议的 rpc 做后端进程通信？
  - 要解决这个问题就应该搞清楚 http 使用的 tcp 协议，和我们自定义的 tcp 协议在报文上的区别。
  - 首先要否认一点 http 协议相较于自定义tcp报文协议，增加的开销在于连接的建立与断开。http协议是支持连接池复用的，也就是建立一定数量的连接不断开，并不会频繁的创建和销毁连接。
  - 二要说的是http也可以使用protobuf这种二进制编码协议对内容进行编码，因此二者最大的区别还是在传输协议上。
- 通用定义的http1.1协议的tcp报文包含太多废信息，
  - 即使编码协议也就是body是使用二进制编码协议，报文元数据也就是header头的键值对却用了文本编码，非常占字节数。

- 所谓的效率优势是针对http1.1协议来讲的，http2.0协议已经优化编码效率问题，像grpc这种rpc库使用的就是http2.0协议。这么来说吧http容器的性能测试单位通常是kqps，自定义tpc协议则通常是以10kqps到100kqps为基准
- 简单来说成熟的rpc库相对http容器，更多的是封装了“服务发现”，"负载均衡"，“熔断降级”一类面向服务的高级特性。可以这么理解，rpc框架是面向服务的更高级的封装。如果把一个http servlet容器上封装一层服务发现和函数代理调用，那它就已经可以做一个rpc框架了。

- 用rpc和http跟业务需求有关系，其实rpc可以用http协议实现

## 0116

- 加减乘除表示运算：plus minus multiply divide
- 和差积商表示运算结果：sum difference product quotient

```JS
new Date('1970-01-01T00:00:00').getTime() // local时间， -280000

new Date('1970-01-01').getTime() // 0
```

- ⭐️ new Date().getTime() 总是13位

- [Deterministic length of JS new Date().getTime() string in the modern era: Unix Epoch Time - Stack Overflow](https://stackoverflow.com/questions/69995741/deterministic-length-of-js-new-date-gettime-string-in-the-modern-era-unix-e)
  - The timestamp is milliseconds since 1970-01-01 00:00:00 UTC (the same as the Unix epoch).
  - if it overflows to 14 digits, the , which is 8, 362, 906, 319, 000
  - 10000000000000/1000/3600/24/365 = 317 年

- [encryption - Hashing a string to a specific length - Stack Overflow](https://stackoverflow.com/questions/45221412/hashing-a-string-to-a-specific-length)
  - Non-cryptographic hashes usually have a wider range of sizes available. For a non-crypto hash I often suggest the FNV hash, which is easy to implement and offers a wide range of output sizes: 32 bits to 1024 bits.
  - 自定义编码解码即可，无需加密

## 0115

- [Typescript generic type parameters: `T` vs `T extends {}` - Stack Overflow](https://stackoverflow.com/questions/61648189/typescript-generic-type-parameters-t-vs-t-extends)
  - in TypeScript 3.5 a change was made so that generic type parameters are implicitly constrained by `unknown` instead of the empty object type `{}`
  - If you don't explicitly constrain a generic type parameter via `extends XXX`, then it will implicitly be constrained by `unknown`, the "top type" to which all types are assignable. So in practice that means the `T in funcA<T>()` could be absolutely any type you want.
  - the empty object type `{}`, is a type to which nearly all types are assignable, except for `null` and `undefined`. Even primitive types like string and number are assignable to {}.

## 0113

### [深入理解Vite核心原理 - 知乎](https://zhuanlan.zhihu.com/p/467325485)

- Vite主要利用浏览器ESM特性导入组织代码，在服务器端按需编译返回，完全跳过了打包这个概念，服务器随起随用。
  - 快速的冷启动: No Bundle + esbuild 预构建
  - 真正的按需加载: 利用浏览器ESM支持，实现真正的按需加载
- Vite相比于Webpack而言，没有打包的过程，而是直接启动了一个开发服务器devServer。
  - Vite劫持浏览器的HTTP请求，在后端进行相应的处理将项目中使用的文件通过简单的分解与整合，然后再返回给浏览器(整个过程没有对文件进行打包编译)。所以编译速度很快。
- Snowpack 首次提出利用浏览器原生ESM能力的打包工具，其理念就是减少或避免整个bundle的打包。默认在 dev 和 production 环境都使用 unbundle 的方式来部署应用。但是它的构建时却是交给用户自己选择，整体的打包体验显得有点支离破碎。

- ESM提供了更原生以及更动态的模块加载方案，最重要的就是它是浏览器原生支持的
  - 👉🏻 我们可以直接在浏览器中去执行import，动态引入我们需要的模块，而不是把所有模块打包在一起。
- ESM的执行可以分为三个步骤：
  - 构建: 确定从哪里下载该模块文件、下载并将所有的文件解析为模块记录
  - 实例化: 将模块记录转换为一个模块实例，为所有的模块分配内存空间，依照导出、导入语句把模块指向对应的内存地址。
  - 运行：运行代码，将内存空间填充
- 从上面实例化的过程可以看出，ESM使用实时绑定的模式，导出和导入的模块都指向相同的内存地址，也就是值引用。而CJS采用的是值拷贝，即所有导出值都是拷贝值。

- vite核心原理
  - 当声明一个script标签类型为 module 时 `<script type="module" src="/src/main.js"></script>`; 
  - 当浏览器解析资源时，会往当前域名发起一个GET请求main.js文件
  - 请求到了main.js文件，会检测到内部含有import引入的包，又会import 引用发起HTTP请求获取模块的内容文件，如App.vue、vue文件
- Vite其核心原理是利用浏览器现在已经支持ES6的import, 碰见import就会发送一个HTTP请求去加载文件，
  - Vite启动一个 koa 服务器拦截这些请求，并在后端进行相应的处理将项目中使用的文件通过简单的分解与整合，然后再以ESM格式返回返回给浏览器。
  - Vite整个过程中没有对文件进行打包编译，做到了真正的按需加载，所以其运行速度比原始的webpack开发编译速度快出许多！

- 在Vite出来之前，传统的打包工具如Webpack是先解析依赖、打包构建再启动开发服务器，Dev Server 必须等待所有模块构建完成，当我们修改了 bundle模块中的一个子模块， 整个 bundle 文件都会重新打包然后输出。项目应用越大，启动时间越长。

- 而Vite利用浏览器对ESM的支持，当 import 模块时，浏览器就会下载被导入的模块。先启动开发服务器，当代码执行到模块加载时再请求对应模块的文件, 本质上实现了动态加载。灰色部分是暂时没有用到的路由，所有这部分不会参与构建过程。随着项目里的应用越来越多，增加route，也不会影响其构建速度。

- 目前所有的打包工具实现热更新的思路都大同小异：主要是通过WebSocket创建浏览器和服务器的通信监听文件的改变，当文件被修改时，服务端发送消息通知客户端修改相应的代码，客户端对应不同的文件进行不同的操作的更新。

- 基于esbuild的依赖预编译优化，为什么需要预构建？
  - 支持commonJS依赖，将commonJs的文件提前处理，转化成 ESM 模块并缓存入
  - 减少模块和请求数量
  - Vite预编译之后，将文件缓存在node_modules/.vite/文件夹下。

## 0111

- [--es-module-specifier-resolution=node not working from v13.0.1 · Issue #30520 · nodejs/node](https://github.com/nodejs/node/issues/30520)
  - we have renamed the flag, but we continue to support `--es-module-specifier-resolution=node` which silently aliases to `--experimental-specifier-resolution`

## 0109

- [Feature: Documenting Promises · Issue · jsdoc/jsdoc](https://github.com/jsdoc/jsdoc/issues/509)
  - jsdoc对promise，暂不支持

- [Summary of `process.env.NODE_ENV` and its use with Webpack by markerikson(redux)](https://gist.github.com/markerikson/6776848172c33aaa4db882627c689e18)

- [Can I mark code blocks as production or development only with webpack? - Stack Overflow](https://stackoverflow.com/questions/50997670/can-i-mark-code-blocks-as-production-or-development-only-with-webpack)
  - emphasize again: The code really disappears if the condition is not met. Only an empty if statement appears on the output. 

```JS
var environment = process.env.NODE_ENV || 'development';

if (process.env.NODE_ENV === 'production') {
  // Code will only appear in production build.
}

if (process.env.NODE_ENV !== 'production') {
  // Code will be removed from production build.
  console.log("Looks like you're a developer.");
}

// process.env is a reference to your environment, so you have to set the variable.
// on windows:
SET NODE_ENV = development
// on macOS / OS X or Linux:
export NODE_ENV = development
// cross-env NODE_ENV=development node server.js
```

## 0112

- [exports is not defined in ES module scope - Stack Overflow](https://stackoverflow.com/questions/71478604/exports-is-not-defined-in-es-module-scope)
  - 使用ts-node执行ts却忘了拷贝 tsconfig.json

## 0108

- 测试mocha时，不能稳定复现 Database is not open/closed
  - db.clear: Delete all entries or a range. Not guaranteed to be atomic. 
  - 解决方法不是写多遍，而是使用 `try-catch`

```JS
// ❌
await d.store.close();
await d.store.close();

// ✅
try {
  await d.store.close();
} catch (e) {
  await d.store.close();
}
```

## 0107

- mocha的异步测试异常
  - Error: Timeout of 2000ms exceeded. For async tests and hooks, ensure "done()" is called; if returning a Promise, ensure it resolves.
  - 对于async的callback方法cb1，若cb1内部有await，可尝试在await后expect断言前使用`setTimeout(done, 50)`，让done方法异步被执行

- [Correct way to use done() while testing asyc/await with mocha - Stack Overflow](https://stackoverflow.com/questions/52449202/correct-way-to-use-done-while-testing-asyc-await-with-mocha)
  - The correct way is to not use `done` with `async..await`. 
  - Mocha supports promises and is able to chain a promise that is returned from `it`, etc. functions.
  - `done` is needed only for testing asynchronous APIs than don't involve promises. Even then, converting to promises often results in cleaner control flow.

```JS
it('Testing insertDocumentWithIndex', async () => {
  var data = await db.insertDocumentWithIndex('inspections', {
    "inspectorId": 1,
    "curStatus": 1,
    "lastUpdatedTS": 1535222623216,
    "entryTS": 1535222623216,
    "venueTypeId": 1,
    "location": [
      45.5891279,
      -45.0446183
    ]
  })
  expect(data.result.n).to.equal(1);
  expect(data.result.ok).to.equal(1);
})
```

- [Describe block with async function behaving weirdly · mochajs/mocha](https://github.com/mochajs/mocha/issues/2975)
  - Mocha's describe blocks do not support (as in waiting for resolution of) returned promises. 

## 0105

- [Import '.json' extension in ES6 Node.js throws an error](https://stackoverflow.com/questions/60205891/import-json-extension-in-es6-node-js-throws-an-error)
- `node --experimental-json-modules ./your-file.js`

```JS
import packageFile from "../../package.json"
assert { type: "json" };

const {
  name,
  version
} = packageFile;

// The dynamic import version looks like this:

const {
  default: {
    name,
    version
  }
} = await import("../../package.json", {
  assert: {
    type: "json"
  }
});
```

- [ShopifyQL Notebooks · Shopify Help Center](https://help.shopify.com/en/manual/reports-and-analytics/shopifyql-notebooks)
  - ShopifyQL Notebooks is an app that enables you to query, explore, and visualize your business’ data.

## 0104

- Each time you're introducing a Boolean field in a Database schema, use a timestamp instead. Future You will thank you. 

```JS
isPublished = true;
if (isPublished) console.log(';; true');

isPublished = new Date();
if (isPublished) console.log(';; true');
```
