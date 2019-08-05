---
title: note-lang-js
created: '2019-06-09T05:36:13.734Z'
modified: '2019-08-03T06:22:54.350Z'
tags: [lang/js]
---

# note-lang-js

## 前端框架通用问题
- 前端国际化
- 主题切换
- css样式处理
- 静态资源处理

## mdn docs

- `arr.slice()`   
	- arr.slice();  // [0, end]
	- arr.slice(begin);
	- arr.slice(begin, end)     
	- 方法返回一个新的数组对象，这一对象是一个由 begin和 end（不包括end）决定的原数组的浅拷贝。原始数组不会被改变。
- `array.splice(start[, deleteCount[, item1[, item2[, ...]]]])`    
	- start 指定修改的开始位置（从0计数）
	- deleteCount 整数，表示要移除的数组元素的个数
	- item1, item2, .. 要添加进数组的元素,从start 位置开始
	- 返回由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。
	- splice()与slice()的作用是不同的，splice()会直接对数组进行修改
-  `arr.reverse()`  
	- reverse 方法颠倒数组中元素的位置，并返回该数组的引用
- `Object.assign(target, ...sources)`
	- method is used to copy the values of all enumerable own properties from one or more source objects to a target object. It will return the target object.
		- shallow copies property values. If the source value is a reference to an object, it only copies that reference value.

## nodejs  

- path
    - path.join():方法使用平台特定的分隔符把全部给定的 path 片段连接到一起，并规范化生成的路
    - path.resolve:方法会把一个路径或路径片段的序列解析为一个绝对路径。 
    
## dev tips

- js对象的属性
    - writable
    - enumerable
    - configurable

- js闭包
    - 「函数」和「函数内部能访问到的变量」（也叫环境）的总和，就是一个闭包
        - https://zhuanlan.zhihu.com/p/22486908
    - 将外部作用域中的局部变量封闭起来的函数对象称为闭包。被封闭起来的变量与封闭它的函数对象有相同的生命周期。
    - 返回函数的函数
    - 能读取函数内部的变量
    - 应用场景
        - 保护函数内的变量安全：如迭代器、生成器
    　　- 在内存中维持变量：如果缓存数据、柯里化
    - 闭包的特点很鲜明，闭包内，变量无法释放，无法被直接访问；闭包可以被延迟执行

- 函数中的 this
    - this的指向是由它所在函数调用的上下文决定的，而不是由它所在函数定义的上下文决定的
    - 由于函数可以在不同的运行环境执行，所以需要有一种机制，能够在函数体内部获得当前的运行环境（context）。所以，this就出现了，它的设计目的就是在函数体内部，指代函数当前的运行环境。
    - 例子
    ```
    var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
            console.log(this.name); // my object
　　　　　　return function(){
                console.log(this.name); // the window
　　　　　　　　return this.name;
　　　　　　};
　　　　}
　　};
　　const v=object.getNameFunc()();
    console.log(v); // the window
    ```
    - object.getnameFunc() 返回的匿名闭包函数被全局变量所引用，其中的this指向全局变量，当执行时打印The Window 。
    - 闭包的两个作用：一个是可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。

- js equals
    - `==`：等同，比较运算符，两边值类型不同的时候，先进行类型转换，再比较；
    - `===`：恒等，严格比较运算符，不做类型转换，类型不同就是不等；
    - `Object.is()`是ES6新增的用来比较两个值是否严格相等的方法，与===的行为基本一致。
- window.location.assign(url) ： 加载 URL 指定的新的 HTML 文档，支持返回上个页面
- window.location.replace(url) ： 通过加载 URL 指定的文档来替换当前文档 ，不支持返回
- Object.assign()与spread operator扩展运算符 区别
	- 扩展运算符支持遍历数组
	- 扩展运算符 is A proposal, not standardized, Literal, not dynamic.
		- 动态示例 `options = Object.assign.apply(Object, [{}].concat(sources))`

- core-js
    - core-js是babel-polyfill的底层依赖，用ES3实现了大部分的ES2017原生标准库

- HTTP cookies
	- An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user's web browser. 
	- The browser may store it and send it back with the next request to the same server. 
	- Typically, it's used to tell if two requests came from the same browser — keeping a user logged-in, for example. 
	- It remembers stateful information for the stateless HTTP protocol.
	- Cookies are mainly used for three purposes:
		- Session management
			- Logins, shopping carts, game scores, or anything else the server should remember
		- Personalization
			- User preferences, themes, and other settings
		- Tracking
			- Recording and analyzing user behavior
	- 浏览器在发送请求之前，首先会根据请求url中的域名在cookie列表中找所有与当前域名一样的cookie，然后再根据指定的路径进行匹配，
	   如果当前请求在域匹配的基础上还与路径匹配那么就会将所有匹配的cookie发送给服务器，这里要注意的是最大匹配和最小匹配问题，
	   有些cookie服务器在发送之前会有意扩大当前页面cookie的匹配范围，此时这些被扩大范围的cookie也会一起发送给服务器。

- XMLHttpRequest与fetch   
	- XMLHttpRequest是对象，fetch()是window的一个方法
	- 服务器返回400、500错误码时并不会 reject，只有网络错误这些导致请求不能完成时，fetch 才会被 reject 
	- 在默认情况下fetch不会接受或者发送cookies，需要设置 `fetch(url, {credentials: 'include'})`
	- 所有的IE浏览器都不会支持 fetch()方法
	- fetch不支持JSONP
	- fetch不支持progress事件
	- fetch不支持超时timeout处理

- 函数去抖（debounce）与 函数节流（throttle）
	-  以下场景往往由于事件频繁被触发，因而频繁执行DOM操作、资源加载等重行为，导致UI停顿甚至浏览器崩溃。
		- window对象的resize、scroll事件
		- 拖拽时的mousemove事件
		- 射击游戏中的mousedown、keydown事件
		- 文字输入、自动完成的keyup事件
		- 实际上对于window的resize事件，实际需求大多为停止改变大小n毫秒后执行后续处理；而其他事件大多的需求是以一定的频率执行后续处理。针对这两种需求就出现了debounce和throttle两种解决办法。
	- js debounce 去抖
	
		- 当调用动作n毫秒后，才会执行该动作，若在这n毫秒内又调用此动作则将重新计算执行时间。
		- 示例
		```
		var debounce = function(idle, action){
		  var last
		  return function(){
			var ctx = this, args = arguments
			clearTimeout(last)
			last = setTimeout(function(){
				action.apply(ctx, args)
			}, idle)
		  }
		}
		```  
	- js throttle 节流   
		- 预先设定一个执行周期，当调用动作的时刻大于等于执行周期则执行该动作，然后进入下一个新周期
		- 示例
		```
		var throttle = function(delay, action){
		  var last = 0return function(){
			var curr = +new Date()
			if (curr - last > delay){
			  action.apply(this, arguments)
			  last = curr 
			}
		  }
		}
		```
	- 函数节流和函数去抖都是通过减少实际逻辑处理过程的执行来提高事件处理函数运行性能的手段，并没有实质上减少事件的触发次数

- npm    
	- npx makes it easy to use CLI tools and other executables hosted on the registry.

## ECMAScript
- 函数绑定运算符 两个冒号 ::  [doc](http://es6.ruanyifeng.com/#docs/function)
    - 双冒号左边是一个对象，右边是一个函数，该运算符会自动将左边的对象，作为上下文环境（即this对象），绑定到右边的函数上面。
    - 如果双冒号左边为空，右边是一个对象的方法，则等于将该方法绑定在该对象上面。
    - 如果双冒号运算符的运算结果，还是一个对象，就可以采用链式写法。
- js事件性能考虑  
    - debounce：强制函数在某段时间内只执行一次
    - throttle：强制函数以固定的速率执行   
    - 在处理一些高频率触发的 DOM 事件的时候，它们都能极大提高用户体验。
- js的函数调用  
    - 定义function f1(a,b){}  
    - 单参数也可以调用 f1(c)  
- 模块化开发不推荐使用css和html，可以都写在js中

## tool

- webpack
    - 前端资源模块化管理和打包工具  
    - 通过 loader 的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等
    - 4个核心概念
        - entry：webpack创建应用程序所有依赖的关系图(dependency graph)，图的起点被称之为入口起点(entry point)。入口起点告诉 webpack 从哪里开始，并根据依赖关系图确定需要打包的内容。可以将应用程序的入口起点认为是根上下文(contextual root) 或 app 第一个启动文件。
        - output：告诉 webpack 在哪里打包应用程序，webpack 的 output 属性描述了如何处理归拢在一起的代码(bundled code)。  
        通过 output.filename 和 output.path 属性，来告诉 webpack bundle 的名称，以及我们想要生成(emit)到哪里。
        - loader：loader用于对模块的源代码进行转换，loader可以使你在 import 或"加载"模块时预处理文件，定义 loader 时，要定义在 module.rules 中，loader 有两个目标         
            - test: 识别出(identify)应该被对应的 loader 进行转换(transform)的那些文件 
            - use: 转换这些文件，从而使其能够被添加到依赖图中（并且最终添加到 bundle 中）
        - plugins：插件目的在于解决loader无法实现的其他功能  
- js模块化 CommonJS、AMD、UMD  
    - CommonJS NodeJS  
    `var $ = require('jquery');`   
    `module.exports = myFunc;`   
    - AMD requirejs、dojo   
    `require(['math'], function (math) { math.add(2, 3); });`  
    `define(['jquery'], function ($) { return myFunc; });`  
    - UMD  
    ```
       (function (root, factory) {
                if (typeof define === 'function' && define.amd) {
                    // AMD
                    define(['jquery'], factory);
                } else if (typeof exports === 'object') {
                    // Node, CommonJS之类的
                    module.exports = factory(require('jquery'));
                } else {
                    // 浏览器全局变量(root 即 window)
                    root.returnExports = factory(root.jQuery);
                }
            }(this, function ($) {
                //    方法
                function myFunc(){};
    
                //    暴露公共方法
                return myFunc;
            }));
    ```
    - CMD seajs
    - es6
- UMD的实现很简单： 
    1. 先判断是否支持Node.js模块格式（exports是否存在），存在则使用Node.js模块格式。
    2. 再判断是否支持AMD（define是否存在），存在则使用AMD方式加载模块。
    3. 前两个都不存在，则将模块公开到全局（window或global）。
- js自执行函数  
    - 因为JavaScript里括号()里面不能包含语句，用括号将函数括住，解析器在解析function关键字的时候，会将相应的代码解析成function表达式，而不是function声明。
    ```
    // 下面2个括弧()都会立即执行
    ( function () { /* code */ }() ); // 推荐使用这个  
    ( function () { /* code */ }) (); // 但是这个也是可以用的  

    // 由于括弧()和JS的&&，异或，逗号等操作符是在函数表达式和函数声明上消除歧义的
    // 所以一旦解析器知道其中一个已经是表达式了，其它的也都默认为表达式了
    // 不过，请注意下一章节的内容解释
    var i = function () { return 10; } ();
    true && function () { /* code */ } ();
    0, function () { /* code */ } ();

    // 如果你不在意返回值，或者不怕难以阅读
    // 你甚至可以在function前面加一元操作符号
    !function () { /* code */ } ();
    ~function () { /* code */ } ();
    -function () { /* code */ } ();
    +function () { /* code */ } ();

    // 还有一个情况，使用new关键字,也可以用，但我不确定它的效率
    new function () { /* code */ }
    new function () { /* code */ } () // 如果需要传递参数，只需要加上括弧()
    ```
- core-js：为es5、es6提供polyfill   

## react
- 优点
    - React的理念是界面**组件化**，在桌面开发中叫控件，可复用性强，开发效率高
		- 但这个组件的含义与Web Components并无明显联系，Web Components是底层标准，而上层框架的实现是足可以抹平这个差异的
    - **Virtual DOM**让组件的渲染输出不局限于浏览器，能实现服务端渲染
        - vdom的性能只能说不低，现在vue和angular都引入了vdom
    - 自上而下的单向数据流，方便追踪状态数据和定位问题
    - react架构设计开放，组件生态丰富
- 缺点
    - react组件中js和html混写，与HTML+CSS+JS的分离思想有一定冲突
    - 并不是一个完整的框架，基本都需要加上ReactRouter和Flux才能写大型应用
    - 组件对框架依赖过重，移植到其他框架的组件不方便
- 使用体验
    - 技术只是手段，每个框架都有擅长的使用场景
    - react只是View层，对于其他的部分并没有规定，可以在vue/angular/backbone中使用
    - 强调只从this.props和this.state生成HTML，所以非常的functional programming
    - 脱离了Flux，在解决大规模UI的问题上React本身并没有拿出比MVVM更优的方案
		- 而结合Flux看的话，MVVM上也可以用Flux的思想，MVVM框架如果加上合适的优化，并不会比React慢，比如Vue的track by

### react-list
- js libraries of list/table/spreadsheet/grid
- 基于table, tr, td
    - handsontable-6.2.2 /201812/MIT/12Kstar
        - https://github.com/handsontable/handsontable/tree/6.2.2
        - https://handsontable.com/docs/6.2.2/tutorial-features.html  
        - 依赖numbro,moment,pikaday 
    - jexcel /201907/MIT/2100star
        - https://github.com/paulhodel/jexcel
        - https://bossanova.uk/jexcel/v3/examples/react
        - 依赖jsuites，是vanilla js
    - rc-table /201907/MIT/510star
        - https://github.com/react-component/table
        - http://react-component.github.io/table/examples/styled-components.html#
        - 依赖react，mini-store，component-classes，lodash  
    - react-datasheet /201905/MIT/3600star
        - https://github.com/nadbm/react-datasheet
        - https://nadbm.github.io/react-datasheet/
        - 依赖react
    - reactabular /201901/MIT/860star
        - https://github.com/reactabular/reactabular
        - https://reactabular.js.org/#/examples/crud
        - 依赖react   
    - reactable /201611/MIT/1500star  
        - https://github.com/glittershark/reactable
        - http://glittershark.github.io/reactable/
        - 依赖react,table,data-tables
    - Griddle /201907/MIT/2400star
        - http://github.com/griddlegriddle/Griddle
        - http://griddlegriddle.github.io/Griddle/
        - 依赖react，lodash，redux，reselect，recompose
- 基于div
    - react-table /201907/MIT/6300star
        - https://github.com/tannerlinsley/react-table/tree/v6.9.2
        - https://codesandbox.io/s/m5lxzzpz69
        - 依赖react，classnames    
	  - react-spreadsheet-grid /201805/MIT/879star
        - https://github.com/denisraslov/react-spreadsheet-grid
        - https://denisraslov.github.io/grid/
        - 依赖react,lodash    
	  - react-data-grid /201907/MIT/3400star
        - https://github.com/adazzle/react-data-grid
        - https://adazzle.github.io/react-data-grid/docs/examples/simple-grid
        - 依赖react,typescript,classnames,immutable,react-is,tslib
        - 项目模块化，分为core和addons
  	- react-virtualized /201907/MIT/16Kstar
        - https://github.com/bvaughn/react-virtualized
        - https://bvaughn.github.io/react-virtualized/#/components/Grid
        - 依赖react, dom-helpers, clsx
    - react-tiny-virtual-list /201807/MIT/1600star
        - https://github.com/clauderic/react-tiny-virtual-list/
        - https://clauderic.github.io/react-tiny-virtual-list/
        - 依赖react,typescript
	  - fixed-data-table-2 /201906/BSD/940star
        - https://github.com/schrodinger/fixed-data-table-2
        - http://schrodinger.github.io/fixed-data-table-2/example-resize.html
        - 依赖react
    - rsuite-table /201907/MIT/210star
        - https://github.com/rsuite/rsuite-table
        - http://rsuite.github.io/rsuite-table/
        - 依赖react，dom-lib
    - React-Spreadsheet-Component /201811/MIT/610star
        - https://github.com/felixrieseberg/React-Spreadsheet-Component
        - http://felixrieseberg.github.io/React-Spreadsheet-Component/
        - 依赖react,jquery,mousetrap   
    - react-list /201905/MIT/1600star
        - https://github.com/coderiety/react-list
        - https://coderiety.github.io/react-list/
        - 依赖react
        - 丑
	  - SlickGrid /201907/MIT/1100star
        - https://github.com/6pac/SlickGrid
        - http://slickgrid.net/
        - http://6pac.github.io/SlickGrid/examples/example4-model.html
        - 依赖jQuery,jQueryUI
    - WickedGrid /201611/MIT/570star
        - https://github.com/Spreadsheets/WickedGrid		
        - http://spreadsheets.github.io/WickedGrid/
        - 依赖jquery
- 基于canvas
    - x-spreadsheet /201907/MIT/6527star
        - https://github.com/myliang/x-spreadsheet
        - https://myliang.github.io/x-spreadsheet
        - 依赖无
- 其他list    
    - js-xlsx Community Edition /201907/Apache2.0/17Kstar
        - https://github.com/SheetJS/js-xlsx
        - https://oss.sheetjs.com/
        - 依赖cfb(Compound File Binary File Format extractor),ssf  
        - 常作为excel读写的工具库，而不用来渲染，官网示例上传excel可渲染成canvas或td
    - react-pivot 
        - https://github.com/davidguttman/react-pivot
        - http://davidguttman.github.io/react-pivot/
        - 依赖react,reactify,dataframe,xtend
        - 基于 td
    - ag-grid-community /201907/MIT/5400star
        - https://github.com/ag-grid/ag-grid
        - https://www.ag-grid.com/example.php#/
        - 依赖无
        - 基于div，模块化
    - FancyGrid /201907/commercial/120star
        - https://github.com/FancyGrid/FancyGrid
        - https://fancygrid.com/tutorials/getting-started/filtering
        - 依赖无
        - 基于div
    - 更多库
        - https://github.com/FancyGrid/awesome-grid
        - https://github.com/TonyGermaneri/canvas-datagrid
            - /201906/BSD/470star
        - https://github.com/stevelacy/react-datagrid2 
            - /201903/MIT/20star
        - https://github.com/iddan/react-spreadsheet 
            - /201907/MIT/130star

### ui library

### element-react 
- github status: /201907/MIT/2200star
- https://github.com/ElemeFE/element-react
- 依赖react,react-transition-group,classnames,popper.js,requestAnimationFrame(raf) polyfill,async-validator(Validate form asynchronous.)
- table基于td

### 其他ui库
- resuite /201907/MIT/2800star
    - https://github.com/rsuite/rsuite
    - https://rsuitejs.com/components/overview 
- uiw
    - https://gitee.com/uiw/uiw
    - https://uiw.gitee.io/#/components
- reactivebase /201802/Apache2.0/18star
    - https://github.com/appbaseio/reactivebase 
    - deprecated

## handsontable
- 6.2.2 is licensed under MIT in 2018


## d3

## ui library
### ant design

### rsuite

## web components

## 样式处理
### css modules

### css in js

#### styled-components
- 使用模板字符串
- 样式写在js文件里，可以使用变量，更加灵活
- SSR类框架处理CSS Modules变量相当棘手，使用styled-components更方便
- 无法分离成独立的css
- 优点: 
    - 1. 接触到的css in js方案中最贴近 css语法的工具。很方便的从 lesa sass 等方案迁移过来。
    - 2. 支持父子，伪类等语法，可以很方便的更改样式权重。想要复写特定组件样式只需要增加很少一部分 BEM class就行。
    - 3. 作用域隔离，这是所有css in js 的优点，但其天然契合 react，让写组件样式辛福感提升了一个台阶。
- 缺点
    - 1. 没法使用 css 预处理框架的全局变量，目前虽然可以通过 style-variable 和 js-object 互转的plugin 解决，但需要使用 ThemeProvider 注入到全局 context 中，个人非常不喜欢。
    - 2. 没法使用postcss，无法自动补全浏览器前缀，css代码压缩，postcss既不是预处理器也不是后处理器
    - 3. js 体积增大，目前没有类似 ExtractCssPlugin 的工具解决这问题。


```
import styled from 'styled-components';
import styles from './style.less';

const Wrapper = styled(div)`
  border: 1px dashed ${props => props.color};
  width: 100%;
`;

const Header = (props) => {
  return (
    <div>
      {/* 直接看 jsx，看不出来 Wrapper 的原始标签是 div */}
      <Wrapper color="#000">使用 styled-component </Wrapper>
      <div className={styles.Wrapper}>使用 CSS Modules</div>
    </div>
  );
};

链接：https://www.zhihu.com/question/266625289/answer/321576411
```

## js ecosystem
- codesanbox vs react-storybook
     -codesandbox类似于codepen
     - storybook只是测试工具

## JS Ecosystem

## resources
- https://github.com/designmodo/html-website-templates

## web builder & prototype
- 拖拽编辑器可用于界面设计、图表设计、产品原型设计
- Webcodesk /201907/MIT/40star
    - https://github.com/webcodesk/webcodesk-app
    - https://webcodesk.com/documentation/tutorial/create_main_page
    - 依赖electron，d3js
    - 直接拖拽现有组件生成项目，基于 react-app-framework
- VvvebJs /201907/Apache2.0/1200star
    - https://github.com/givanz/VvvebJs.git
    - http://www.vvveb.com/vvvebjs/editor.html
    - Drag and drop website builder javascript library.
    - 依赖jquery和bootstrap
- grapejs /201907/BSD/8900star
    - https://github.com/artf/grapesjs
    - https://grapesjs.com/demo.html
    - 依赖underscore，backbone，codemirror，
- h5ds /201907/commercial
- silex /201907/GPLv3/680star
    - https://github.com/silexlabs/Silex
    - 丑
- 基于vue
    - https://github.com/fireyy/vue-page-designer
    - https://github.com/baianat/vuse
- 其他
    - https://github.com/chriskitson/react-drag-drop-layout-builder

## WebAssembly
- 典型应用场景
    - 扩展浏览器端视音频处理能力
    - 游戏计算
- 90%的应用场景都不需要WebAssembly
    - https://www.infoq.cn/article/ytxfUWloi2wi00cQY-8a
    - js问题
        - 语法太灵活导致开发大型项目困难
        - 性能不能满足一些场景的需要
    - TypeScript是JavaScript的一个严格超集，并添加了可选的静态类型和使用看起来像基于类的面向对象编程语法操作Prototype，TypeScript最终仍然是被编译成JavaScript在浏览器中执行
    - 在2008年，Google推出了JavaScript引擎V8，首次通过JIT技术提升JavaScript的执行速度，并且它真的做到了
        - Web应用中，性能瓶颈大部分的原因已经不在JavaScript，而在于DOM。浏览器中通常会把DOM 和JavaScript独立实现，这两个模块相互访问的时候，都是通过接口访问。由于JavaScript单线程的特性，这种访问只能是单工的
        - 为了减少js访问dom的次数，可以使用Virtual Dom，Web Worker 
        - JIT执行时，可以根据代码编译进行优化，代码运行时，不需要每次都翻译成二进制汇编代码，V8就是这样优化JavaScript性能的
    - 为了进一步提升JIT优化效率，Mozilla 推出了asm.js。asm.js也是强类型的JavaScript，但是他的语法则是JavaScript的子集，是为了JIT性能优化而专门打造的，其他大厂都觉得asm.js的思路不错，于是联合起来共建WebAssembly生态
    - WebAssembly是一份字节码标准，以字节码的形式依赖虚拟机在浏览器中运行，可以依赖Emscripten等编译器将C++/Golang/Rust/Kotlin等强类型语言编译成为WebAssembly字节码.wasm 文件。
        - WebAssembly并不是Assembly（汇编），它只是看起来像汇编
    - 鉴于V8的强大性能，90%的应用场景下你不需要WebAssembly
    - 如何提高JS代码性能
        - 声明变量时提供默认类型，加快JIT介入
        - 不要轻易改变变量的类型
        - Node.js像Java一样也存在JIT预热？

### game

- 主流游戏开发引擎
    - Unity3D-免费不开源
    - Unreal Engine 4-开源但只能学习不能再次分发

- common
    - https://github.com/libgdx/libgdx -  Apache 2
        - 基于gwt，放弃
    - https://github.com/cocos2d/cocos2d-x - MIT
        -  cocos2d-js不如-x好用
    - https://github.com/pixijs/pixi.js - MIT
    - https://github.com/photonstorm/phaser - MIT
        - 从性能到底层api的易用和强大
        - 没有做模块拆分，tween,particles等全在一个包中，release的min版本大概在2M，egret在700K左右
        - Phaser 2一直采用开源的Pixi2版本作为2D渲染引擎，在Phaser3中已放弃Pixi
        - Phaser 3.0.0 is released on 20180213.
    - https://github.com/godotengine/godot - MIT
    
- misc
    - https://github.com/nicolodavis/boardgame.io - MIT    
    - https://github.com/FormidableLabs/react-game-kit - MIT
    - https://github.com/deck-of-cards/deck-of-cards - MIT
    - https://github.com/layabox/layaair 
        - 引擎全部开源并且全部免费使用，包括商用
    - https://github.com/hiloteam/Hilo - MIT，阿里h5游戏解决方案，有申请专利
    - https://github.com/egret-labs/egret-core - BSD
        - 使用Typescript


