---
title: dev-ing
tags: [dev]
created: 2022-05-24T17:52:58.048Z
modified: 2022-05-24T17:53:08.400Z
---

# dev-ing

# dev-2022
- 分析核心需求和问题，拆分问题，梳理任务、子任务

金瑶 邀请您加入【金瑶的个人会议室】
点击链接直接加入腾讯会议：
https://meeting.tencent.com/p/9606972663
#腾讯会议：960-697-2663

# dev-xp
- my-next
  - dev-starter
    - react patterns
    - typescript patterns
    - mvc dev pattern(for app/data-grid)
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
- 编辑器参考
  - atlassian-editor
    - https://atlaskit.atlassian.com/packages/editor/editor-core
    - https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-minimal
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-with-toolbar
    - https://ckeditor.com/docs/ckeditor5/latest/examples/builds-custom/full-featured-editor.html

```JS
console.log(';; r1-user-spaces ', pathname, user, userSpaces, currentSpaceId);
```

# dev-review
- dev-to
  - 事项--重要性(ll/ml/hl)--截止日期(0730+放松)
  - search notion like block editor for recursive rendering
# dev-08

## 0818

- RESTFul 架构下的两个缺点：
  - 在一个 RESTful 架构下，因为后端开发人员定义在各个 URL 的资源上返回的数据，而不是前端开发人员来提出数据需求，使得按需获取数据会非常困难。经常前端需要请求一个资源中所有的信息，即便只需要其中的一部分数据。这个问题被称之为过度获取（overfetching）。
  - 最恶劣的场景下，一个客户端应用不得不请求多个而不是一个资源，这通常会发起多个网络请求。这不仅会造成过度获取的问题，也会造成瀑布式的网络请求（waterfall network requests）。
- GraphQL最初就是为了解决上述两个问题设计的
  - GraphQL schema提供了一个所有可用数据检索的源头，通常会在服务端定义，客户端可以基于 schema 读取（query）和写入（mutation）数据
  - 但是呢，因为GraphQL获取数据是动态的，随机的，所以肯定会有人对数据的缓存提出较大的疑问

## 0815

- js基础 数据类型、运算符operator、表达式、流程控制
  - 新的数据类型，bigint
  - typeof
  - 流程控制：顺序、条件、循环
  - if使用场景，切换主题
    - https://codepen.io/uptonking/pen/xxWzYJq
  - 循环使用场景，批量生成html元素
    - https://codepen.io/uptonking/pen/LYdpPBW

## 0812

- 百度网盘倍速播放的扩展
  - global speed

## 0810

- [Redux DevTools 扩展的使用说明](https://juejin.cn/post/6998924455984496671)
  - [使用 redux-devtools-extension 查看 Redux 中状态变化](https://lufanfan.github.io/20190109/redux-devtools/)
  - `const store = createStore(reducer, composeWithDevTools());`

## 0807

- 视图公共的 addCard 的逻辑分析
  - createCard 创建一个业务层对象
  - mutator 执行持久化数据操作
- 👉🏻 action都被mutator和undoManager封装过了，需要进一步理清思路

## 0805

- [What is the difference between dpkg and aptitude/apt-get?](https://askubuntu.com/questions/309113)
- `dpkg -i packageName.deb` will only install this Deb package, and will notify you of any dependencies that need to be installed, 
  - but it will not install them, and 
  - it will not configure the packageName.deb because well...the dependencies are not there.
- `apt-get` is basically dpkg (I like to think of it as apt-get being a front-end for dpkg), but a clever one that will look for the dependencies and install them. 
  - It even looks at the currently installed dependencies and determines ones that are not being used by any other packages, and will inform you that you can remove them.
- `aptitude` then came along. It uses the libraries apt-get uses and actually has an interactive UI (user interface). 
  - aptitude will automatically remove eligible packages, while apt-get needs a separate command to do so. 
  - aptitude provides the functionality of dselect and apt-get as well as many additional features not found in either program.
# dev-07

## 0730

- replace mutator with reduxStore

## 0729

- [fedora flatpak.. sudo or not sudo?](https://forums.fedoraforum.org/showthread.php?327857-fedora-flatpak-sudo-or-not-sudo&p=1855999)
  - 无一致答案
  - It's not a "SAFER" thing! As I see it, it's rather about if you're installing for yourself, or for all users. If for yourself, then you won't need sudo.
  - 参考apt安装命令用了sudo

### [http请求方式： post put patch 总结](https://blog.csdn.net/qianxing111/article/details/79791499)

- idempotent 幂等的
  - 如果一个方法重复执行多次，产生的效果是一样的，那就是idempotent的；
  - idempotent的意思是如果相同的操作再執行第二遍第三遍，結果還是一樣。
  - “Methods can also have the property of ‘idempotence’ in that (aside from error or expiration issues) the side-effects of N > 0 identical requests is the same as for a single request.”
- POST方法不是幂等的，多次执行，将导致多条相同的用户被创建（users/1，users/2)
- PUT比較正確的定義是 Replace (Create or Update)，
  - 例如 PUT /items/1 的意思是替換 /items/1 ，如果已經存在就替換，沒有就新增；
  - 因此，PUT方法一般会用来更新一个已知资源，除非在创建前，你完全知道自己要创建的对象的URI
- PATCH方法是新引入的，是对PUT方法的补充，用来对已知资源进行局部更新
  - HTTP PATCH method require a feature to do partial resource modification.
  - The existing HTTP PUT method only allows a complete replacement of a document.

## 0728

- 对于多维表格，一般将数据更新的方法定义在所有视图渲染的上层
  - 添加 card/row 时，状态如何变化？
  - 调用同一个 addCard 方法，但不同视图下传入的参数不同

## 0727

- Cannot read properties of null (reading 'pickAlgorithm')
  - ~~npm cache clear --force~~
    - 多看一眼，异常上一行就是导致问题的依赖包名称
  - 解决方法应该是将 .npmrc 里面的自定义npm镜像源注释掉，然后重新 npm i

## 0726

- shop-iot-外接显示器
  - 对显示器不太了解，请教了一下大佬，跟我说直接买他的那款就行。于是我买了两台，一台在家一台在公司，直到昨天我才知道这个显示器除了可以 65W 反向充电外，还可以直接插 USB 连键盘鼠标，不用再在电脑上接转接线连了...
  - VX2780-4K-HDU 经济又便宜
  - [优派 VX2780-4K-HDU 27"UHD三边微边框IPS技术HDR400支持PD65W充电滤蓝光不闪屏HDMI/DP/TypeC显示器](https://www.viewsonic.com.cn/products/lcd/VX2780-4K-HDU.php)

## 0725

- innerText vs textContent
  - `innerText` is aware of things like `<br>` elements, and ignores hidden elements
  - `innerText` is aware of styling and won't return the text of "hidden" elements.
  - `textContent` gets the content of all elements, including `<script>` and `<style>` elements. In contrast,  `innerText` only shows "human-readable" elements.

- [Is it possible to calculate the Viewport Width (vw) without scrollbar?](https://stackoverflow.com/questions/33606565)
  - the viewport relative length units do not take scrollbars into account (and in fact, assume that they don't exist).
  - According to the [specs](https://drafts.csswg.org/css-values-3/#viewport-relative-lengths),  `vw` does take scrollbar width away UNLESS the overflow is on auto, then it works like "hidden" for the vw value. So if the page must overflow, set it to "scroll". With overflow-x & overflow-y you choose which scrollbar to display

- 100vw会在超长内容时出现水平滚动条的问题
  - 具体宽度需要实测，很多资料的信息是过时的
    - https://codepen.io/uptonking/pen/zYWdRLO
  - chrome-linux 
    - window.innerWidth  625
    - document.documentElement.clientWidth  610
    - 100vw.div.clientWidth  625
    - 给容器设置100vw时，若出现竖直滚动条，因为vw默认没考虑滚动条，此时总宽度是100vw+竖直滚动条宽度，就会导致出现水平滚动条

- [解决 100vw 下滚动条引发的问题](https://juejin.cn/post/6844904062702321672)
  - 通过js工具函数计算滚动条宽度
  - 解决100vw出现水平滚动条的问题
    - .container  { width: calc(100vw - var(--scrollbar)); }
  - 解决出现滚动条时右边距和上边距不相同的问题
    - right: calc(40px + var(--scrollbar));

- [深入浅出 Viewport 设计原理](https://www.cnblogs.com/onepixel/p/12144364.html)
- css 中写的 px 指的就是逻辑像素，而不是物理像素，一个逻辑像素可以代表一个或多个物理像素
- 简单来说：viewport 是屏幕背后的一张画布。
- 浏览器会先把页面内容绘制到画布上，然后再通过屏幕窗口呈现出来。
- 如果没有在 html 中加 viewport 的设置，画布其实也是存在的，浏览器会给画布设置一个默认宽度 ，不同平台的默认值
- width=device-width 就是把画布的宽度设置为可视窗口的宽度，让画布上的内容完全呈现出来。
- 在没有给页面设置 viewport 的情况下，当画布宽度大于可视窗口的时候，浏览器会自动对画布进行缩放，以适配可视窗口大小。这样页面在不滚动的情况下也能呈现全部内容。

### [Viewport concepts](https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_concepts)

- 小结
  - vw单位未考虑滚动条宽度，容易造成出现滚动条
  - 100vw  === innerWidth
  - layout viewport 是innerWidth/Height内区域
  - visual viewport是layout viewport去掉不可见部分，一般是 键盘

- [Visual Viewport API](https://developer.mozilla.org/en-US/docs/Web/API/Visual_Viewport_API)
  - The visual viewport is the visual portion of a screen excluding on-screen keyboards, areas outside of a pinch-zoom area, or any other on-screen artifact that doesn't scale with the dimensions of a page.
- What happens when a web page element needs to be visible on screen regardless of the visible portion of a web page? 
  - For example, what if you need a set of image controls to remain on screen regardless of the pinch zoom level of the device? Current browsers vary in how they handle this. 
  - The visual viewport lets web developers solve this by positioning elements relative to what's shown on screen.

- A viewport represents the area in computer graphics being currently viewed. 
  - In web browser terms, it is generally the same as the browser window, excluding the UI, menu bar, etc. 
  - That is the part of the document you are viewing.
- Your viewport is everything that is currently visible
  - The size of the viewport depends on the size of the screen, whether the browser is in fullscreen mode or not, and whether or not the user zoomed in. 
  - On larger monitors where applications aren't necessarily full screen, the viewport is the size of the browser window.
  - On most mobile devices and when the browser is in fullscreen mode, the viewport is the entire screen.
  - In fullscreen mode, the viewport is the device screen, the window is the browser window, which can be as big as the viewport or smaller, and the document is the website, which can be much taller or wider than the viewport.
  - To recap, the viewport is basically the part of the document that is currently visible.
- The width of the viewport is not always the width of the window.
  - The document element's `Element.clientWidth` is the inner width of a document in CSS pixels, including padding (but not borders, margins, or vertical scrollbars, if present). This is the viewport width. 不包含 border/margin/竖直滚动条宽度
  - The `Window.innerWidth` is the width, in CSS pixels, of the browser window viewport including, if rendered, the vertical scrollbar. 包含竖直滚动条宽度
  - The `Window.outerWidth` is the width of the outside of the browser window including all the window chrome.
- The web contains two viewports, the layout viewport and the visual viewport. 
  - The **area within the `innerHeight` and `innerWidth` is generally considered the layout viewport**. The browser chrome is not considered part of the viewport.
  - The visual viewport is the part of the web page that is currently visible in the browser and can change. When the user pinch-zooms(双指缩放) the page, pops open a dynamic keyboard, or when a previously hidden address bar becomes visible, the visual viewport shrinks but the layout viewport is unchanged.
- The visual viewport is the currently visible portion of the layout viewport. 
  - The **visual viewport** is the visual portion of a screen **not including** on-screen keyboards, areas outside of a pinch-zoom area, or other feature that doesn't scale with the dimensions of a page. 
  - The visual viewport is the same size as the layout viewport or smaller.
- Sticky headers or footers, as discussed above, stick to the top and bottom of the layout viewport, and therefore remain in view when we zoom in with the keyboard. 
  - If you pinch-zoom, the layout viewport may not be fully visible. 
  - If you magnify from the middle of the layout viewport, the content will expand in all four directions. 
  - If you have a sticky header or footer, they will still be stuck to the top or bottom of the layout viewport, but they may not be visible at the top and bottom of the device's screen — which is the visual viewport. 
  - The visual viewport is the currently visible portion of the layout viewport.
  - If you scroll down, you are changing the contents of the visual viewport and bringing the bottom of the layout viewport into view, displaying the sticky footer, which will then stay stuck at the bottom.

- 现代桌面浏览器有两种缩放操作。
  - 你在菜单栏上的缩放是改变像素大小（同时缩放layout viewport和visual viewport），
  - 用触摸板双指操作才是只缩放visual viewport。
  - （古代浏览器如IE还有另一种缩放，缩放字体大小，类似于改变rem的值）

## 0724

- [Does adding too many event listeners affect performance?](https://stackoverflow.com/questions/28627606)
  - dding additional event handlers to an element DOES decrease performance. 
  - Keep in mind that those tests are done with an empty function. When adding a real function that performs some additional tasks, the performance will slow down even further.

- [git error: failed to push some refs to remote](https://stackoverflow.com/questions/24114676)
  - 修改git仓库地址后，其他分支无法push
  - 简单的解决办法是直接重命名无法push的分支
  - git branch -m old-name new-name

## 0723

- 产品设计
  - 需求列表
  - 细分客户，定位准确

## 0722

- display: list-item 默认在内容前加上列表黑点
- display: inline 行内元素设置width/height默认无效，行内元素宽高默认由内容决定
  - flex item弹性项目默认都是 display: block，所以弹性容器内的span弹性项目设置width/height有效
- [`<span>` element refuses to go inline in flexbox](https://stackoverflow.com/questions/20363441)
  - by the flexbox spec -- children of a flex container are forced to have a block-flavored display type.
  - If you don't want this behavior, just wrap your `<span>` in a `<div>`, and then the `<div>` will play the role of the flex item so that the `<span>` can keep its display type.

- [css flex-item default height issue](https://stackoverflow.com/questions/47106934)
  - All items in a flex row will take the largest height of them by default.
  - After calling container as display:flex, may i consider all its contained items will behave like inline-block elements?

### [python 字符串转列表出现\ufeff的解决方法](https://www.cnblogs.com/mjiang2017/p/8431977.html)

- 在Windows下用文本编辑器创建的文本文件，如果选择以UTF-8等Unicode格式保存，会在文件头（第一个字符）加入一个BOM标识。
  - BOM = Byte Order Mark
  - BOM是Unicode规范中推荐的标记字节顺序的方法。比如说对于UTF-16，如果接收者收到的BOM是FEFF，表明这个字节流是Big-Endian的；如果收到FFFE，就表明这个字节流是Little-Endian的。
  - UTF-8不需要BOM来表明字节顺序，但可以用BOM来表明“我是UTF-8编码”。BOM的UTF-8编码是EF BB BF（用UltraEdit打开文本、切换到16进制可以看到）。所以如果接收者收到以EF BB BF开头的字节流，就知道这是UTF-8编码了。
- [Python 读取文件首行多了"\ufeff"字符串](https://blog.csdn.net/chenmozhe22/article/details/89472790)

- [json字符串头部出现非法字符“\ufeff”的问题处理](https://segmentfault.com/a/1190000010292346)
  - 今天在处理将数组转为json 字符串后，然后获取到解析时，出现解析的json字符串为空的现象，首先看了下，我的json转换脚本之前没有任何输出，但还是出现json转化乱码，后来查了下，原来是脚本编码格式的问题。
  - 其实解决方法很简单，就是涉及json转换的脚本文件的UTF-8格式编码 改成 UTF-8无BOM格式编码即可。

### [什么零宽度字符，以及零宽度字符在JavaScript中的应用](https://juejin.cn/post/6844904164057677831)

- 一种不可打印的Unicode字符, 在浏览器等环境不可见, 但是真是存在, 获取字符串长度时也会占位置, 表示某一种控制功能的字符.
- 常见的零宽字符有哪些
- 零宽空格（zero-width space, ZWSP）用于可能需要换行处。
  - Unicode: U+200B  HTML: &#8203; 
- 零宽不连字 (zero-width non-joiner，ZWNJ)放在电子文本的两个字符之间，抑制本来会发生的连字，而是以这两个字符原本的字形来绘制。
  - Unicode: U+200C  HTML: &#8204; 
- 零宽连字（zero-width joiner，ZWJ）是一个控制字符，放在某些需要复杂排版语言（如阿拉伯语、印地语）的两个字符之间，使得这两个本不会发生连字的字符产生了连字效果。
  - Unicode: U+200D  HTML: &#8205; 
- 左至右符号（Left-to-right mark，LRM）是一种控制字符，用于计算机的双向文稿排版中。
  - Unicode: U+200E  HTML: &lrm; &#x200E; 或&#8206; 
- 右至左符号（Right-to-left mark，RLM）是一种控制字符，用于计算机的双向文稿排版中。
  - Unicode: U+200F  HTML: &rlm; &#x200F; 或&#8207; 
- 字节顺序标记（byte-order mark，BOM）常被用来当做标示文件是以UTF-8、UTF-16或UTF-32编码的标记。
  - Unicode: U+FEFF

- 零宽度字符在JavaScript的应用
- 数据防爬
  - 将零宽度字符插入文本中, 干扰关键字匹配。
  - 爬虫得到的带有零宽度字符的数据会影响他们的分析，但不会影响用户的阅读数据。
- 信息传递
  - 将自定义组合的零宽度字符插入文本中，用户复制后会携带不可见信息，达到传递作用。
- 使用零宽度字符加密解密
  - 信息加密解密的思路是, 把字符串转成二进制0和1, 并用空格把字符隔开, 然后用三种零宽表示0、1、空格, 然后用第四种零宽字符拼起来; 解密反向操作即可.
- excel表格 中经常出现零宽字符 \u202c \u202d, 上传后解析或复制到 input 就会有问题, 
  - 在 excel表格 中获取到的数据一般需要先过滤.

## 0721

### [How to use throttle or debounce with React Hook?](https://stackoverflow.com/questions/54666401)

- After some time passed I'm sure it's much easier to handle things by your own with setTimeout/clearTimeout(and moving that into separate custom hook) than working with functional helpers.

```JS
const App = () => {
  const [value, setValue] = useState(0)
  const throttled = useRef(throttle((newValue) => console.log(newValue), 1000))

  useEffect(() => throttled.current(value), [value])

  return (
    <button onClick={() => setValue(value + 1)}>{value}</button>
  )
}

// It may work too
const throttled = useCallback(throttle(newValue => console.log(newValue), 1000), []);
```

### [How to autosave small changes to big settings file without lag?](https://stackoverflow.com/questions/41232606)

- Provided that you want to keep the model with a multi-MB settings file, the most reasonable solution would be to use **atomic writes** to avoid the problem of the app being quit in the middle of a save.
- Assuming your file is called `settings.json`, atomic writes would work something like this:
  - App decides to update settings, starts writing to a temporary file (to avoid overwriting the existing file halfway), say `settings.json.tmp-1482198169` (1482198169 being current unix timestamp).
  - Once writing to `settings.json.tmp-1482198169` is complete, copy the current `settings.json` to `settings.json.bak`.
  - Rename `settings.json.tmp-1482198169` to `settings.json`, overwriting the old one.
- The basic idea is to construct a process where you always have a valid copy of `settings.json`, so it's only replaced with a complete copy.
- npm has a number of implementations of this, like this one. I'd recommend you try one of those instead of writing your own, since any bugs in the implementation of the atomic write dance could cause you data loss, and it's tricky to get everything right when dealing with asynchronous code.
  - https://github.com/npm/write-file-atomic
  - Write files in an atomic fashion w/configurable ownership
  - This is an extension for node's fs.writeFile that makes its operation atomic and allows you set ownership (uid/gid of the file).

### [Is any solution to do localstorage setItem in asynchronous way](https://stackoverflow.com/questions/42921220)

```JS
const asyncLocalStorage = {
  setItem: function(key, value) {
    return Promise.resolve().then(function() {
      localStorage.setItem(key, value);
    });
  },
  getItem: function(key) {
    return Promise.resolve().then(function() {
      return localStorage.getItem(key);
    });
  }
};

const asyncLocalStorage2 = {
  setItem: async function(key, value) {
    await null;
    return localStorage.setItem(key, value);
  },
  getItem: async function(key) {
    await null;
    return localStorage.getItem(key);
  }
};
```
