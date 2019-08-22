---
tags: [lang/js]
title: note-lang-js
created: '2019-06-09T05:36:13.734Z'
modified: '2019-08-21T14:09:38.681Z'
---

# note-lang-js

## 前端框架通用问题
- 前端国际化/切换语言翻译
    - react-intl
- 切换主题
    - react-with-styles
- css解决方案
    - css-in-js
- 静态资源处理

## tips
- all in js as frontend

## js guide
- https://github.com/airbnb/javascript

## faq
- js虚拟机和jvm有什么关系
    - JS的虚拟机有JSC、spidermonkey、v8等，跟JVM没有什么直接的联系
    - V8的team leader是Lars Bak，jvm的Hotspot正是Lars Bak领导开发的
    - 在V8出现之前，JS引擎的技术比较原始，正是Lars Bak率先将JVM中先进的技术带到了JS引擎中的，如分代式GC、机器码直接生成等



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


## booking-JavaScript语言精粹.修订版_Douglas Crockford_2012
- 为什么要使用javascript
    - 因为没有其他选择，js是唯一一种所有浏览器都支持的语言
    - 尽管js有很多缺点，但js也有很多优秀的设计
- js优点
    - 自由的弱类型、动态对象、对象字面量表示法
- js缺点
    - 基于全局变量的编程模型
- js数据类型
    - NaN是一个数值，它表示一个不能产生正常结果的运算结果，NaN不等于任何值，包括它自己
    - js字符串中字符使用的是16位的Unicode
    - js没有字符类型，要表示一个字符，只需创建仅包含一个字符的字符串即可
    - 字符串是不可变的，通过+号实际是创建了一个新字符串
    - 两个包含着完全相同的字符且字符顺序也相同的字符串被认为是相同的字符串
    - `'c'+'a'+'t'==='cat'`返回true
    - type of运算符检查属性类型返回的值就是js数据类型，6种
        - string
        - number
        - boolean
        - undefined
        - object
        - function
- js运算符与表达式
    - 每个`<script>`标签提供一个被编译且立即执行的编译单元，因为缺少链接器，js把它们一起抛到一个公共的全局命名空间中
    - 能配合break使用的语句：switch、for、while、do
    - 代码块是包在一对花括号中的一组语句，不像许多其他语言，js中的代码块不会创建新的作用域，因此变量应该被定义在函数的头部，而不是在代码块中
    - if表达式为假的情况
        - false
        - null
        - undefined
        - 空白字符串
        - 数字0
        - 数字NaN
        - 其他情况表达式的值都为true，包括true、字符串"false"、所有对象
    - for in语句会遍历对象的所有属性名
        - 通常你需要检测obj.hasOwnProperty(var)来确定这个属性名是该对象的成员， 还是来自于原型链
    - return语句会导致从函数中返回
        - 如果没有指定返回表达式，那么返回值是undefined
    - 运算符优先级
        - 属性提取运算符.[]与函数调用运算符()优先级最高
        - delete/new/type of/! 一元运算符
        - 乘除取余
        - 加减
        - 比较
        - 逻辑与&& 高于 逻辑或||
        - ?:三元运算符
- js对象
    - js的简单数据类型包括number、string、boolean 、null、undefined，**其他所有的值都是对象**
    - number、string、boolean貌似对象，因为它们拥有方法，但它们是不可变的。js的对象是**可变**的键控集合 (keyed collections) ，比如数组是对象，函数是对象，正则表达式也是对象
    - 对象是属性的容器，其中每个属性都拥有名字和值
        - 属性的名字可以是**包括空字符串**在内的任意字符串
        - 属性的值可以是除undefined值之外的任何值
    - js的对象是无类型( class-free )的。它对新属性的名字和属性的值没有限制。对象可以包含其他对象，所以它们可以容易地表示成树状或网状结构
    - js包含一种原型链的特性，允许对象继承另一个对象的属性，正确地使用它能减少对象初始化时消耗的时间和内存
- 对象字面量
    - 提供了一种非常方便地创建新对象的表示法，一个对象字面量就是包围在一对花括号中的零或多个键值对
    - 在对象字面量中，如果属性名是一个合法的标识符且不是保留字，则并不强制要求用引号括住属性名，所以用引号括住"first-name"是必需的，但是否括住first_name则是可选的
    - 从对象取属性值的方式包括obj["attrName"]和obj.attrName
        - []的方式属性名不能使保留字
        - 推荐使用点号运算符取值
        - 若属性名不存在，则返回undefined
        - undefined可通过&&处理
    - 给对象添加属性值的方式也是2种
        - 若属性存在，则值覆盖
        - 若属性不存在，则添加
    - 对象传递传的是引用
    - 全局变量削弱了程序的灵活性和健壮性，推荐为应用只创建唯一的全局变量`var v={};`
        - 将全局资源都作为这个全局变量的属性，以减少冲突可能
        - 另一种减少全局污染的方法是使用闭包
- prototype 原型
    - 每个对象都连接到一个原型对象，并且它可以从中继承属性
    - **所有通过对象字面量创建的对象都连接到原型对象Object.prototype**
    - 当你创建一个新对象时，你可以选择某个对象作为它的原型
    - 原型连接在更新时是不起作用的，当我们对某个对象做出改变时，不会触及该对象的原型
    - 原型连接只有在检索值的时候才被用到
        - 如果我们尝试去获取对象的某个属性值，但该对象没有此属性名，那么js会试着从原型对象中获取属性值
        - 如果那个原型对象也没有该属性，那么再从它的原型中寻找，依此类推，直到该过程最后到达终点Object.prototype
        - 如果想要的属性完全不存在于原型链中，那么结果就是undefined值
        - 这个过程称为委托
    - 原型关系是一种动态的关系，如果我们添加一个新的属性到原型中，该属性会立即对所有基于该原型创建的对象可见
    - 清除无用属性值的方法
        - 通过type of检查属性值类型，然后手动去掉某种类型的属性，比如去掉function
        - 通过obj.hasOwnProperty('attrN')确定属性值是否存在，此方法不检查原型链
    - for in语句会遍历对象的所有属性
        - 包括原型链中的属性，包括函数类型的属性
        - 属性名遍历的顺序不确定
        - 先取出所有属性名，再通过for语句+i次序遍历可以得到一致的顺序 ///to-test
        - for in语句用在原型上表现很糟糕 ///to-test
    - 通过delete运算符可以删除属性，不会删除原型链上游的同名属性
- 函数
    - 函数的作用
        - 代码复用、功能复用
        - 信息隐藏
        - 组合调用
    - js的函数也是对象
        - **函数对象都连接到原型对象Function.prototype**
        - Function.prototype该原型对象本身连接到Object.prototype
    - 每个函数在创建时会附加两个隐藏属性：函数上下文和实现函数行为的代码
    - **每个函数对象在创建时也会有一个prototype属性**，它的值是一个拥有constructor属性且值即为该函数的对象，这和隐藏连接到Function.prototype完全不同
        - 类似 `this.prototype = {constructor: this};`
    - 因为函数是对象，所以它们可以像任何其他的值一样被使用
        - 函数可以保存在变量、对象 和数组中
        - 函数可以被当做参数传递给其他函数，函数也可以再返回函数
        - 因为函数是对象，所以函数可以拥有方法
    - 柯里化允许我们把函数与传递给它的参数相结合，产生出一个新的函数
- 函数对象通过函数字面量创建 
    - `var fName = function(param1){ }`
    - 函数字面量包括4部分
        1. 保留字function
        2. 函数名，可省略(如上)，省略名称后为匿名函数
        3. 参数
        4. 函数主体语句{ // }
    - 函数可以被定义在函数中
    - 通过函数字面量创建的函数对象包含一个连到外部上下文的连接，这被称为闭包(closure)
- 函数调用
    - 调用一个函数会暂停当前函数的执行，传递控制权和参数给新函数
    - 除了声明时定义的形式参数，每个函数还接收两个附加的参数: this和arguments
    - 参数this在面向对象编程中非常重要，它的值取决于调用的模式，在js中一共有4种调用模式：方法/函数/构造器/apply调用模式
    - this到对象的绑定发生在调用的时候
    - 若实参比形参多，多余的实参会被忽略
    - 若实参比形参少，不足的参数换初始化为undefined
    - 对参数值不会进行类型检查
    - 函数可以通过arguments问所有它被调用时传递给它的参数列表，包括那些没有被分配给函数声明时定义的形式参数的多余参数
        - 因为js语言设计的缺陷，arguments对象并不是一个真正的数组
        - arguments对象拥有一个length属性，但它没有任何数组的方法
        - 示例(不推荐这样使用)
        ```
        var sum = function () { 
            var i , sum = 0; 
            for (i = 0; i < arguments.length; i += 1) {
              sum += arguments[i]; 
            } 
            return sum;
        };
        console.log(sum(4 , 8 , 15 , 16 , 23 , 42));   // 108
        ```
    - 方法调用模式
        - 当一个函数被保存为对象的一个属性肘，我们称它为一个方法
        - 一个方站被调用肘， this被绑定到该对象
        - 典型使用： 点号和[]取属性
        - 示例
        ```
        var myObject = { 
            value: 0 ,
            increment: function (inc) { 
              this.value += typeof inc === 'number' ? inc : 1;
            }
        }；
        myObject.increment(); 
        console.log(myObject.value);  // 1
        myObject.increment(2); 
        console.log(myObject.value);  // 3
        ```
    - 函数调用模式
        - 当一个函数并非一个对象的属性时，那么它就是被当做一个函数来调用的
        - 以此模式调用函数时，this被绑定到全局对象
        - 这个设计的后果就是方法不能利用内部函数来帮助它工作
        - 示例
        ```
        var add = function(x,y){ return x+y; };
        myObject.double = function () { 
          var that = this; //解决方法是将外部函数的this保存一份传给内部函数
          var helper = function () { 
              that.value = add(that.value , that.value);
          };
          helper () ; //以函数的形式调用helper()
          }；
        //以方法的形式调用double
        myObject.double(); 
        console.log(myObject.value);   // 
        ```
    - 构造器调用模式
        - 如果在一个函数前面带上new来调用，那将会创建一个连接到该函数的prototype属性的新对象，同时this会被绑定到那个新对象上
        - 一个函数，如果创建的目的就是希望结合new来调用，那它就被称为构造器函数
            - 按照约定，它们保存在以大写格式命名的变量里
            - 如果调用构造器函数时没有在前面加上new，可能会发生非常糟糕的事情，既没有编译时警告，也没有运行时警告
        - 不推荐使用构造器函数
        - 示例
        ```
        //创建一个名为Quo的构造器函数
        var Quo = function (string) { this.status = string;}
        //给Quo的所有实例提供一个名为get_status的公共方法
        Quo.prototype.get_status = function () { return this.status;}
        var myQuo = new Quo("confused");
        console.log(myQuo.get_status()); // confused
        ```
    - apply调用模式
        - apply()方法让我们构建一个参数数组传递给调用函数，它也允许我们选择this的值 - apply()接收两个参数，第1个是要绑定给this的值，第2个就是一个参数数组
        - 示例
        ```
        var array = [3 , 4]; 
        var sum = add.apply(null , array); 
        console.log(sum);   // 7
        var statusObject = { status: 'OK' };
        var status = Quo.prototype.get_status.apply(statusObject);
        console.log(status); // OK
        ```
- 递归函数可以非常高效地操作树形结构
    - 尾递归是在函数最后执行递归调用语句
    - 尾递归优化是指将递归替换为循环，js语言未提供尾递归优化
- 作用域
    - 作用域控制着变量与参数的可见性及生命周期
    - 在处理命名冲突和自动内存管理方面很有用
    - js并不支持块级作用域
    - js支持函数作用域
        - 定义在函数中的参数和变量在函数外部是不可见的
        - 在一个函数内部任何位置定义的变量，在该函数内部任何地方都可见
    - 最好的做法是在函数体的顶部声明函数中可能用到的所有变量
    - 要避免在循环中创建函数，它可能只会带来无谓的计算，还会引起棍淆，可以先在循环之外创建一个辅助函数  
-  闭包
    - 作用域的好处是内部函数可以访问定义它们的外部函数的参数和变量(除了this和args)
    - 内部函数比它的外部函数拥有更长的生命周期，闭包的优势
- 回调
    - 常用于异步处理
- 模块
    - 模块是一个提供接口但隐藏状态与实现的对象
    - 利用闭包和函数创建模块
    - 模块一般形式
        - 模块整体是一个定义了私有变量和函数的函数
        - 利用闭包创建可以访问私有变量和函数的特权函数
        - 最后返回这个特权函数，或者把它们保存到一个可访问到的地方
    - 通过使用模块可以避免使用全局变量
    - 模块模式通常结合单例模式使用，js的单例就是用对象字面量表示法创建的对象，对象的属性位可以是数值或函数，并且属性值在该对象的生命周期中不会发生变化，通常作为工具为程序其他部分提供功能支持
- 继承
    - Java继承优点
        - 代码重用
        - 引入了类型系统的规范
    - js提供了一套更为丰富的代码重用模式，它可以模拟那些基于类的模式
    - 当采用构造器调用模式，即用new前缀去调用一个函数时，函数执行的方式会被修改
    - 构造器函数默认首字母大写
    - 一个更好的备选方案就是根本不使用 new
    - 基于原型的继承相比基于类的继承在概念上更为简单:一个新对象可以继承一个旧对象的属性
        - 指明与所基于的基本对象的区别
    - 使用函数化模块可以复用现有对象的功能，也可以作为一种继承
- 数组
    - 一个数组字面量是在一对`[]`中包围零个或多个用逗号分隔的值的表达式
    - 数组默认的属性名依次是'0’，'1'...
    - 对于超出范围的属性名，属性值为undefined
    - 数组继承自Array.prototype，而普通对象继承自Object.prototype
    - 多数语言要求一个数组的所有元素是相同的类型，但js允许数组包含任意混合类型的值
    - 每个数组对象有个length属性，js的length无上界，若下标大于当前length，那数组自动扩容
    - 你可以直接设置length的值，设置更大的length不会给数组分配更多的空间，而把length设小将导致所有下标大于等于新length的属性被删除
    - 由于js的数组其实就是对象，所以delete运算符可以用来从数组中移除元素
        - 示例 `delete numbers[2];`，执行后该位置的属性值会变为undefined，仍占位
        - 若要删除后后面元素都前移，要用 `splice(start,num)`，效率可能不高/to-test
    - 因为js数组其实就是对象，所以for in 语句可以用来遍历一个数组的所有属性，但无法保证属性的顺序，特别是原型链中有意外属性时，直接使用for循环可避免此问题
    - 当属性名是小而连续的整数肘，应该使用数组，否则该使用对象
    - typeof运算符报告数组的类型是object，js没有一个好的机制来区别数组和对象
    - 可以通过定义自己的函数来区分数组和对象
        - 示例
        ```
        var isArray = function (va1ue) { 
            return va1ue && 
                   typeof va1ue === 'object' &&
                   va1ue.constructor === Array;
        }
        ```
    - Array.prototype提供了操作数组的方法
    - 因为数组其实就是对象，所以我们可以直接给一个单独的数组添加方法
        - 直接给数组添加方法时，因为属性名不是整数，所有不会改变数组的length
    - js的数组通常不会预置值
        - 如果你用 [] 得到一个新数组，它将是空的
        - 如果你访问一个不存在的元素，得到的值则是 undefined
        - js支持元素为数组的数组
- 正则表达式
    - js的正则借鉴自Perl
    - 可处理正则表达式的方法
        - regexp.exec/.test
        - string.match/.replace/.search/.split
    - 在js程序中，正则表达式必须写在一行中
    - 创建正则表达式
        - 使用正则表达式字面量，正则表达式字面量被包围在一对斜杠中
        - 使用构造器方法： new RegExp("字符串表示的规则")，要用双反斜杠
- Array
    - arr.concat(item...)  产生一个新数组，包含arr浅复制
    - arr.join(separator)  将arr构造出一个字符串，用来连接字符串时比+运算符快
    - arr.pop()  移除arr最后一个元素，并返回该元素
    - arr.push(item...)  将item添加到arr尾部，返回数组新长度
    - arr.reverse()  反转arr中元素顺序，返回arr本身
    - arr.shift()  移除arr中第一个元素，并返回该元素，比pop()慢
    - arr.slice(start,[end])  对arr中一部分做浅复制，返回新数组，前闭后开
    - arr.splice(start,delCount,item) 从arr中移除元素并插入item，返回移除元素数组
    - arr.sort()  对arr所有元素进行排序，不能给数字排序，排序元素默认被视为字符串
        - 通过将自定义函数传入sort()可实现排序数字数组
        - js的sort()不具有稳定性，不同浏览器实现方式不同
    - arr.unshift(item...)  将元素添加到arr头部，返回arr新length
- Function
    - func.apply(thisArg,argArray)
    - 调用func()时指定传入的this和参数
- Number
    - number.toFixed(fractionDigits)  转换成十进制形式的字符串，传入小数位数
- Object
    - obj.hasOwunProperty(name)  若obj包含name属性，则返回true
- RegExp
    - re.exec(string)  匹配正则表达式并返回匹配结果数组
    - re.test(String)  若匹配存在，则返回true
- String
    - str.charAt(pos)  返回在str的pos位置处的字符
    - str.concat(str2) 连接现有字符串构造一个新字符串
    - str.indexOf(searchStr,pos)  在str内查找另一个字符串searchStr，返回位置索引
    - str.match(regexp)  若无g标识，则功能相等于regexp.exec(str)
    - str.replace(oldVal,newVal)  查找替换，返回一个新字符串
        - 若oldVal是字符串，则只会替换第一次出现oldVal的地方
        - 若oldVal是正则表达式且带有g标识，则会替换所有匹配
        - newVal可以是字符串或函数
    - str.search(regexp)  类似indexOf
    - str.slice(start,end) 复制str的一部分来构造一个新的字符串
    - str.split(sperator,limit)  分割字符串，返回数组
    - str.substring(start,end)  同slice，但参数不能为负数，推荐使用slice
- js问题
    - 全局变量
    - 没有快捷作用域
    - +运算符
        - 都是数字，才会求和，否则作为字符串连接
    - typeof很多时候判断类型不明确
        - typeof null // object
        - typeof NaN  // number
        - typeof arr  // object
    - parseInt()，建议总是加上基数，因为以0开头的字符串会作为八进制求值
    - 浮点数设计有一点缺陷
        - 0.1+0.2 = 0.3000000000000000000004
        - 小数中的错误可以通过指定精度来避免
    - NaN
        - 它是一个特殊的数值，表示不是一个数字
        - + 'abc' // NaN
        - NaN === NaN // false
        - isNaN(NaN)  // true
        - isNaN('abc) // true
        - isNaN('0')  // false
        - 判断一个值是否是数字推荐使用 isFinite(val)
    - if中可以作为假的值
        - false
        - 0
        - NaN
        - '' 空字符串
        - null
        - undefined
    - if中可以作为真的值
        - '0' 字符串0
        - [] 空数组
        - {} 空对象
    - 相对比较
        - ==的两个运算数若是不同类型，会先强制转换类型
        - 推荐使用 ===
    - eval(str)需要运行编译器，降低程序性能
    - 推荐使用function表达式，理解函数就是对象
    - 不推荐使用new
    - with语句的本意是提供一个访问深层嵌套对象成员的快捷方式，不推荐使用

## 深入理解ES6_Nicholas C. Zakas_2016
- ES历史
    - js的标准在1999年发布es3后就未改变过
    - 2007年由于ajax的流行开始了制定标准es4
    - 2008年集中精力制定ECMAScript 3.1，也开始计划4
    - ECMAScript 3.1最终发展成ES5
    - ES6最终在2015年发布，包含大量新特性
- 块级绑定
    - const可用于for-in
- 字符串
    - 模板字面量基本语法用反引号`包裹普通字符串
    - 模板字面量中无需对单引号或双引号进行转义，若要包含反引号需用反斜杠转义
    - 模板字面量中所有空白符都是字符串的一部分，要注意处理缩进
    - 模板字面量中的替换位是js表达式，可以轻松嵌入计算、函数调用
    - 模板字面量本身也是js表达式，可以将模板字面量嵌入另一个模板字面量内部
    - 模板标签是一个函数，能控制模板字面量的拼接过程
- 函数
    - js函数可以接受任意数量的实参，而不用考虑函数声明处形参的数量
    - 箭头函数自身没有this,arguments,super
- 对象
    - 对面字面量重复属性会覆盖
    - ES6正式将方法定义为：一个拥有 [[HomeObject]] 内部属性的函数，此内部属性指向该方法所属的对象
- 集合
    - Set
        - 无重复值的有序列表
        - Set不会使用强制类型转换来判断值是否重复，所以可以同时包含数值5与字符串"5"
        - Set内部Object.is()方法判断是否相等
        - WeakSet不可迭代，没有forEach()方法和size属性
    - Map
        - 键值对的有序列表，键和值多可以是任意类型
        - key的比较使用的是Object.is()
        - WeakMap的键必须是对象，内部存储键的弱引用，值无限制
        - WeakMap是无序列表，键必须是非null的对象
        - WeakMap的主要用途是关联数据与DOM元素
        - WeakMap没有forEach(),clear(),size
- 迭代器与生成器
    - 可迭代对象包括数组、Set、Map、字符串，都有默认的迭代器
    - for-of循环会先调用集合对象的Symbol.iterator()方法获取迭代器，然后调用iterator.next()获取value对应的对象
        - for-of不能用于不可迭代对象、null、undefined
    - 开发者自定义的对象默认不可迭代
    - Set获取默认迭代器values()，Map获取默认迭代器entries(),WeakSet/Map无迭代器
    - 字符串的方括号表示法str[1]作用于码元上，而非字符上，无法正确获取双码元字符
    - 字符串的默认迭代器默认迭代的是字符，而不是码元 for(let c of str)
    - HTML规范中规定NodeList带有默认迭代器，表现与数组迭代器一致
    - 扩展运算符`...`能作用于所有可迭代对象，是创建数组最简单的方法
- 异步编程
    - Promise
    - async await

     
## js-guide-google
- 字符串优先使用单引号，方便包含html属性中的双引号
- 声明常量要使用大写字符, 并用下划线分隔，不用简单地只使用const，IE不支持const
- 总是使用分号，便于区分语句
- 不要在块内声明一个函数
    - ECMAScript只允许在脚本的根语句或函数中声明函数，部分浏览器支持块内
    - 如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量
    - 示例
    ```
    if (x) { 
        var foo = function() {}
    }
    ```
- 不要使用封装类型，如new Boolean(
- 小心使用闭包，闭包保留了一个指向它封闭作用域的指针, 所以在给DOM元素附加闭包时, 很可能会产生循环引用, 进一步导致内存泄漏
- eval()只用于解析序列化串，如解析RPC响应，最好不要使用eval
    - 解析序列化串是指将字节流转换成内存中的数据结构
- with(){}让你的代码在语义上变得不清晰，不要用
- this仅在对象构造器, 方法, 闭包中使用，易出错
- for-in只用于 object/map/hash 的遍历，对Array的遍历用for-in会出现不按顺序遍历
- 不要修改内置对象如 Object.prototype 和 Array.prototype 的原型


## js-guide-es6-airbnb
- 
