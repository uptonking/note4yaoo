---
title: log-dev-pieces-frontend
tags: [dev, frontend, log]
pinned: true
created: '2019-06-09T15:54:12.063Z'
modified: '2020-08-18T05:56:56.343Z'
---

# log-dev-pieces-frontend

## logging

 

- `element.innerHTML` vs `node.innerText`
  - innerText retrieves and sets the content of the tag as plain text, 
    - whereas innerHTML retrieves and sets the content in HTML format.
    - This only applies when SETTING a value. When you're GETTING the value HTML tags are simply stripped and you get the plain text.
  - element.innerHTML只去除标签，换行会打印出来
    - Sets or gets the HTML syntax describing the element's descendants
  - node.innerText会去除换行和首尾空格
    - Sets or gets the text between the start and end tags of the object
    - innerText gives you a style-aware, representation of the text that tries to match what's rendered in by the browser this means:
      - innerText applies text-transform and white-space rules
      - innerText trims white space between lines and adds line breaks between items
      - innerText will not return text for invisible items
      - innerText will return textContent for elements that are never rendered like `<style />`
  - node.textContent
    - Gets or sets the text content of a node and its descendants.
    - Is not aware of styling and will therefore return content hidden by CSS
    - **Does not trigger a reflow** (therefore more performant)
  - node.value
    - This one depends on the element that you've targeted.
    - For the above example, `x` returns an HTMLDivElement object, which does not have a `value` property defined.
    - Input tags, for example, do define a `value` property, which refers to the "current value in the control".
    - for certain input types the returned value might not match the value the user has entered. For example, if the user enters a non-numeric value into an `<input type="number">`, the returned value might be an empty string instead.
  - ref
    - [Difference between innerText, innerHTML, and childNodes[].value?](https://stackoverflow.com/questions/19030742/difference-between-innertext-innerhtml-and-childnodes-value)

- tree-shaking
  -  we can help terser by using the `/*#__PURE__*/` annotation
  - It flags a statement as side effect free. 
  - So it would make it possible to tree-shake the code
  - `var Button$1 = /*#__PURE__*/ withAppProvider()(Button);`
  - This would allow to remove this piece of code. 
  - But there are still questions with the imports which need to be included/evaluated because they could contain side effects.
  - To tackle this, we use the `sideEffects` property in package.json.
  - It's similar to `/*#__PURE__*/` but on a module level instead of a statement level. 
  - ("sideEffects" property): "If no direct export from a module flagged with no-sideEffects is used, the bundler can skip evaluating the module for side effects.".

- 弹性布局 vs 响应式布局
  - rem是弹性布局的一种实现方式，弹性布局可以算作响应式布局的一种，但响应式布局不是弹性布局
    - 弹性布局强调等比缩放，100%还原
    - 响应式布局强调不同屏幕要有不同的显示，比如媒体查询
  - 只用css，无需js，就可以实现元素大小随着屏幕宽度的变化而变化

- 如何实现1px
  - 将border设置为1px, 然后将也页面的整体根据页面的dpr缩小相应的倍数，接着将rem补偿相应的倍数，这样页面中只有1px的边框缩小了，而其他内容经过缩小和扩大，还是原来的状态
  - var fontSize = width/10*(window.devicePixelRatio) + 'px'

- 如何根据不同的屏幕尺寸去动态设置html的font-size呢
  - 利用css的media query来设置，单位是px
  - 利用js动态计算并修改，可能会有闪烁问题
  - rem布局在加载的时候会出现元素一开始很小，闪烁一下恢复正常大小的问题
    - JS动态计算并修改字体大小和媒体查询，只要选择一套方案就可以了，推荐媒体查询
    - 外部css会阻塞DOM渲染，并不阻塞js解析，外部js既阻塞渲染，也阻塞解析
  - 部分安卓手机或者webview调整了系统默认字体大小

- ### rem vs px
  - 结论
    - 考虑3类设备上的展示：手机、平板、pc、横竖屏
    - 考虑系统默认字体、浏览器默认字体
    - 在视觉稿要求固定尺寸的元素上使用px，比如1px线、4px的圆角边框
    - 在字号、（大多数）间距上使用rem
    - 不用em，因为会根据当前元素的字号按比例计算尺寸，若当前元素无字号则查找父元素
    - 推荐：用户业务样式代码以 px 为单位，并且以 iPhone6 屏幕 “物理像素” 宽度 750 为基准 (即普通 “逻辑像素” 值的 2 倍大小)， 使用 postcss-pxtorem 把 px 转成 rem 单位，转换基准为1rem=100px (使用 rem 实现不同设备等比缩放效果)。对于使用 webpack 的项目，在 webpack.config.js 里新增 pxtorem 配置
    - 将html元素的font-size设为62.5%(或10px)是为了方便计算，可以设置为625%
    - 当使用小于12px的字体时，chrome只会渲染12px大小的字
    - 若通过浏览器设置或系统设置或辅助功能设置了大字号，则内容及间隔都会变大，字号变大后，屏幕显示的内容会变少   
    - 类似这样的适配在pad横屏展示超级大，所以还是要根据业务需求设置临界值
    - 如果让html元素的font-size等于屏幕宽度的1/100，那1rem和1x就等价了，此时宽度为100rem
      - 如何让html字体大小一直等于屏幕宽度的百分之一呢？ 可以通过js来设置
      - 注意dom在ready,resize,rotate时更新宽度值
      - 那么如何把设计图中的获取的像素单位的值，转换为已rem为单位的值呢？
        - 375px/100rem = 48px/uNeedrem
    - css3带来了rem的同时，也带来了vw和vh，vw为视口宽度的1/100，vh为视口高度的 1/100
      - vw的兼容性不如rem好，android和ios的支持情况不同
      - 若要限制最大宽度，vw
    - 三方组件库是大家公用的，如果每个组件库的rem拆分不一致就会有很多问题，若一个库100rem就是100vw，有的是20rem是100vw，引入几个三放库中间大小肯定就不兼容了
    - rem基于html的font-size，所有元素都受影响，引入三方库修改成本要尽量低
    - 使用px的组件库，会利用js控制内联style进行适应屏幕
    - ref
      - https://www.zhihu.com/question/309599529
      - https://zhuanlan.zhihu.com/p/30413803
      - https://segmentfault.com/a/1190000014502172
      - https://github.com/ant-design/ant-design-mobile/wiki/HD
  - rem的特点是根据根元素按比例计算尺寸
    - 优点是使用rem时，若修改了根元素的字体大小，就可以自动显示相应的尺寸
    - 实现1px的border不精确，计算时常产生小数
    - 横竖屏切换时，可能需要动态计算并设置根html的大小
- `document.getElementsByTagName("html")[0].style.fontSize = (width)height/7.5 + "px";`
- 最近在做开发的时候遇到rem的一个大坑，就是如果用户改变了手机的字体大小，而且我们的页面样式的宽用了rem, 比如{width:1rem}, 那么页面的宽就会成倍增长，导致页面乱掉。。。还没找到办法解决，宽度还是先避免使用rem的好。
  - 字体的大小和字体宽度，并不成线性关系，所以字体大小不能使用rem；由于设置了根元素字体的大小，会影响所有没有设置字体大小的元素。可以在body上做字体修正
  - 如果用户在PC端浏览，页面过宽怎么办？一般我们都会设置一个最大宽度，大于这个宽度的话页面居中，两边留白 `body { margin: auto; width: 100rem }`
- px的特点是固定尺寸
  - 浏览器的pixel是css pixel
  - 当用图片或一些不能缩放的展示时，必须要使用固定的px值，因为缩放可能导致变形
  - px是一直是浏览器厂商以及标准的推荐单位，是未来的主流
- bootstrap选择
    - While Bootstrap uses ems or rems for defining most sizes, pxs are used for grid breakpoints and container widths.
    - This is because the viewport width is in pixels and does not change with the font size.

- 之前做dom截图用过 html2canvas 发现太慢了，然后换成 dom-to-image 好很多。
  - foreignObject 是真香啊。

- If you write "export default () => { ... }" to declare components, they:
  - will show up as Anonymous in stack traces
  - will show up as Unknown in DevTools
  - won't be checked by React-specific lint rules
  - won't work with some features like Fast Refresh
  - Give components names!

- What does % mean in CSS?

height
parent’s height
width
parent’s width
top
parent’s height
left
parent’s width
margin-top
parent’s width
margin-left
parent’s width
padding-top
parent’s width
padding-left
parent’s width
translate-top
self’s height
translate-left
self’s width

- js中对象的创建 `var thing=Object(stuff);`
  - The Object constructor returns its argument when the argument is already an object. 
  - If it's not an object, it returns the "objectified" version of the argument: a String instance if it's a string, a Number instance if it's a number, etc.
  - if `stuff` is object ,  `var thing=Object(stuff);` and `var thing=stuff;` are equivalent, 
  - [Object Construct with object parameter](https://stackoverflow.com/questions/47483438/javascript-object-construct-with-object-parameter)

- Browsers won't render elements with the `hidden` attribute set.
  - The `hidden` global attribute is a Boolean attribute indicating that the element is not yet, or is no longer, relevant. 
- `void expression`
  - The `void` operator evaluates the given expression and then returns `undefined` .
  - The `void` operator is often used merely to obtain the `undefined` primitive value, 
    - usually using `void(0)` (which is equivalent to `void 0"). 
    - In these cases, the global variable `undefined` can be used.
  - 使用场景
    - IIFE
    - javascript:void(0)
    - button.onclick = () => void doSomething()
  - undefined问题
    - The problem with using undefined was that undefined is not a reserved word
    - That is, undefined is a permissible variable name, so you could assign a new value to it at your own caprice(变化无常，反复无常)
    - This is no longer a problem in any environment that supports ECMAScript 5 or newer (i.e. in practice everywhere but IE 8), which defines the `undefined` property of the global object as read-only 
  - Why void 0, specifically?
    - Why should we use void 0? What's so special about 0? Couldn't we just as easily use 1, or 42, or 1000000 or "Hello, world!"?
    - And the answer is, yes, we could, and it would work just as well. 
    - The only benefit of passing in 0 instead of some other argument is that 0 is short and idiomatic.
  - Although `undefined` can generally be trusted in modern JavaScript environments, there is one trivial advantage of `void 0` : it's shorter. 
    - most code minifiers replace undefined with void 0 to reduce the number of bytes sent to the browser.

- typescript class Parameter properties 构造函数中带有修饰符的参数，可自动生成赋值语句

``` typescript
class Octopus {
  readonly name: string;
  readonly numberOfLegs: number = 8;

  constructor(theName: string) {
    this.name = theName;
  }
}

// We’ve consolidated the declarations and assignment into one location.
// 可使用的修饰符包括 public、protected、private、readonly
class Octopus {
  readonly numberOfLegs: number = 8;
  constructor(readonly name: string) {}
}
```

- 组件库中使用的 `.hbs` 是ui模版吗
  - Handlebars is a simple templating language.
  - A handlebars expression is a `{{` , some contents, followed by a `}}` .
  - When the template is executed, these expressions are replaced with values from an input object.
  - handlebars 的特点是兼容 Mustache 语法，多数情况下可以直接迁移
- yarn.lock中可能出现某个间接依赖下载失败
  - 可能是不小心修改了某个位置的字符，还原最初的yarn.lock，再yarn install
- appendChild有时会移动元素
  - 下面的例子执行后， `<span>` 元素会移动到b下面，并且a下没有了
    - 若通过button触发js，多次调用appendChild最终b下也只有1个

``` html
<div class="a">
  <span></span>
</div>
<div class="b"></div>
```

``` JS
const span = document.querySelector('span');
const divB = document.querySelector('.b');
divB.appendChild(span);
```

- `Node.nodeName` vs `Element.tagName`
  - The `nodeName` read-only property returns the name of the current `Node` as a string.
  - The `tagName` read-only property of the Element interface returns the tag name of the element on which it's called.
  - The `tagName` property is meant specifically for element nodes (type 1 nodes) to get the type of element.
    - There are several other `nodeType` s of nodes as well (comment, attribute, text, etc.). 
    - To get the name of any of the various node types, you can use the `nodeName` property.
  - When using `nodeName` against an element node, you'll get its tag name, so either could really be used, 
    - though you'll get better consistency between browsers when using `nodeName` .
    - Bear in mind, however, that `nodeName` will return `#text` for text nodes while `tagName` will return `undefined` .

- `setAttribute` vs `dom/obj.prop`
  - You should always use the direct `.prop` form (but see the quirksmode link below) if you want programmatic access in JavaScript. 
  - Use `getAttribute` / `setAttribute` when you wish to deal with the DOM as it is (e.g. literal text only). Different browsers confuse the two.
  - From Javascript: The Definitive Guide, it clarifies things. 
    - It notes that HTMLElement objects of a HTML doc define JS properties that correspond to all standard HTML attributes.
    - So you only need to use `setAttribute` for non-standard attributes.

``` JS
node.className = 'test'; // works
node.frameborder = '0'; // doesn't work - non standard attribute
node.setAttribute('frameborder', '0'); // works
```

  - ref
    - [When to use setAttribute vs .attribute= in JavaScript?](https://stackoverflow.com/questions/3919291/when-to-use-setattribute-vs-attribute-in-javascript)

- 利用console调试js
  - console.debug/info/warn/error, log是info
  - 使用console.trace()来获取堆栈调用记录
  - 使用console.time()开始计算时间，然后使用console.timeEnd()进行打印
  - 利用console.memory（是属性，不是函数）来检查你的堆大小状态。
  - 使用console.profile('profileName')，然后使用console.profileEnd('profileName')，从代码中启动和结束浏览器性能工具 performance profile
  - 使用console.count('?')来计算您的代码被读取的次数。
  - 使用console.assert(condition, msg)在condition为假时记录某些内容，条件日志记录并没有用if-else包装
  - console.group(‘group’) & console.groupEnd(‘group’)将控制台日志组织在一起
  - 使用字符串替换合并变量。这些引用是（％s = string，％i = integer，％o = object，％f = float）
  - console.clear()清理控制台
  - console.table()打印表格，方便查看复杂对象
- 调试js的方法
  - 除了 `console.log` ,                       `debugger` 是我们最喜欢、快速且肮脏的调试工具。
    - 执行代码后，Chrome会在执行时自动停止
    - 你甚至可以把它封装成条件，只在需要时才运行
  - 切换设备模式，调试不同尺寸下的ui
  - 在Elements面板中标记一个DOM元素，并在控制台中使用它。
    - Chrome控制台会保留选择历史的最后五个元素，最终选择的首个元素被标记为$0，第二个选择的元素为$1，依此类推。
  - 使用 console.time() 和 console.timeEnd() 测试循环执行时间
  - 快速查找要调试的函数，假设你要在函数中打断点，最常用的两种方式是
    - 在控制台查找行并添加断点
    - 在代码中添加debugger
    - 在控制台中使用debug(funcName)，当到达传入的函数时，代码将停止。
  - 在Chrome控制台中，可以观察特定的函数。
    - 每次调用该函数，就会打印出传入的参数。
    - 但不完美，没有打印形参数量
  - 控制台中比querySelector更快的方法是使用美元符号
    - $('css-selector')将返回CSS选择器的第一个匹配项。
    - $$('css-selector')将返回所有匹配项。
    - 如果多次使用一个元素，可以把它保存为一个变量。
  - 调试时，需要查找DOM中某个元素的事件监听器时， `getEventListeners($(‘selector’))` 返回一个对象数组，其中包含绑定到该元素的所有事件
  - monitorEvents($(‘selector’)) 将监视与选择器的元素关联的所有事件，然后在它们被触发时将它们打印到控制台。例如，monitore($(#firstName)) 将打印 ID 为 firstName元素的所有事件。
- ref
  - [14个你可能不知道的JavaScript调试技巧](https://www.zcfy.cc/article/the-14-javascript-debugging-tips-you-probably-didnt-know-raygun)

- 如何打印变量名 Variable name as a string in Javascript

``` JS
// 要实现的效果
var myFirstName = 'John';
alert(variablesName(myFirstName) + ":" + myFirstName); // myFirstName:John

// 一种实现
const myFirstName = 'John';
const variableName = Object.keys({ myFirstName })[0]; // myFirstName
// pop may be better than [0], for safety (variable might be null).
const variableName = Object.keys({ myFirstName }).pop();
```

  - 使用映射表或对象
    - Typically, you would use a hash table for a situation where you want to map a name to some value, and be able to retrieve both
  - 使用Object.keys

- ts: any vs Object

``` typescript
let a: any;
let b: Object;
let c: {};
let d: object;
```

- `a` has no interface, it can be anything, 
  - the compiler knows nothing about its members so no type checking is performed when accessing/assigning both to it and its members. 
- `b` has the `Object` interface, 
  - so ONLY the members defined in that interface are available for `b` . 
  - It's still JavaScript, so everything extends `Object` ; 
- `c` extends Object, like anything else in TypeScript, but adds no members. 
  - Since type compatibility in TypeScript is based on structural subtyping, not nominal subtyping,  `c` ends up being the same as `b` because they have the same interface: the `Object` interface.
- So `Object` and `{}` are equivalents in TypeScript.
- Typescript 2.2 added an `object` type, 
  - which specifies that a value is a non-primitive: (i.e. not a `number` ,                       `string` ,                       `boolean` ,                       `symbol` ,  `undefined` , or `null` ).

- 函数调用拆分

``` JS
function spread(fn) {
  return Function.apply.bind(fn, null);
}

spread(fn)

// is transformed to

args => fn.apply(null, args)
```

- 理解 `return new (Function.prototype.bind.apply(ctor, args))();`
  - 分解成多步

``` JS
var func = Function.prototype.bind.apply(ctor, args);
return new func();
```

  - Since .apply() is a function in on itself, it can be bound with .bind(), like so:
    - `Function.prototype.apply.bind(fn, null);`
    - Meaning that the `this` of `.apply()` would be `fn` and the first argument to `.apply()` would be `null` . Meaning that it would look like this:
    - `fn.apply(null, args)`
  - ref
    - [How does function.apply.bind work in the following code?](https://stackoverflow.com/questions/39906893/how-does-function-apply-bind-work-in-the-following-code)

- .apply.bind

``` JS
var sum = function(x, y) {
  console.log(x, y);
}
var foo = Function.apply.bind(sum, null);
foo([10, 20]); // 10, 20
```

  - `Function.apply.bind(sum, null)` 等价于 `sum.apply.bind(sum, null)）`
    - 可避免sum.apply被重写引发的问题
    - Function.apply.bind(sum, null)目的就是将sum.apply(…)的第一个参数固定为null
    - sum.apply(null, [10, 20])这句代码将第一个参数置为null，第二个参数是一个数组，用于拆开后作为sum的最终参数。
    - 如果将sum.apply(…)的第一个参数设置为null，那么就意味着我们并不关心sum在执行时其内部的this指向谁
    - 所以最终我们得到的foo函数就是sum.apply(null, [10, 20]); [10,20]会拆开成10和20传递给sum(…)
- .bind.apply
  - 我们将orig_fn.bind.apply(orig_fn, args)拆成两部分来看：函数orig_fn.bind(…)和.apply(orig_fn, args)
  - 在这里的关键点是：.bind(…) 函数是通过 .apply(…) 调用的，所以 .bind(…) 自身所需要的 this 对象是一个函数（函数也是对象，在这里即 origin_fn）。
  - orig_fn.bind.apply(orig_fn, args)其实就意味着我们将orig_fn.bind(…)函数的this指向orig_fn，然后.apply(orig_fn, args)的第二个参数会将剩下的参数传递给orig_fn.bind(…)函数。
- 根据构造函数创建对象的通用方法
  - The `new` keyword does the following things:
    - Creates a blank, plain JavaScript object;
    - Links (sets the constructor of) this object to another object;
    - Passes the newly created object from Step 1 as the `this` context;
    - Returns `this` if the function doesn't return an object.
  - When the code `new Foo(...)` is executed, the following things happen:
    - A new object is created, inheriting from `Foo.prototype` .
    - The constructor function `Foo` is called with the specified arguments, and with `this` bound to the newly created object. 
      - `new Foo` is equivalent to `new Foo()` , i.e. if no argument list is specified, `Foo` is called without arguments.
    - The object (not null, false, 3.1415 or other primitive types) returned by the constructor function becomes the result of the whole `new` expression. 
      - If the constructor function doesn't explicitly return an object, the object created in step 1 is used instead. 
      - (Normally constructors don't return a value, but they can choose to do so if they want to override the normal object creation process.)
    - You can always add a property to a previously defined object.
    - You can add a shared property to a previously defined object type by using the `Function.prototype` property. 
      - This defines a property that is shared by all objects created with that function, rather than by just one instance of the object type. 
    - If you didn't write the `new` operator, the Constructor Function would be invoked like any Regular Function, without creating an Object. In this case, the value of `this` is also different.
  - When a function is used as a constructor (with the `new` keyword), its `this` is bound to the new object being constructed
  - While the default for a constructor is to return the object referenced by `this` , it can instead return some other object 
    - (if the return value isn't an object, then the `this` object is returned).
    - If the function has a return statement that returns an object, that object will be the result of the `new` expression.  
    - Otherwise, the result of the `new` expression is the object currently bound to `this`
  - [Use of .apply() with 'new' operator. Is this possible?](https://stackoverflow.com/questions/1606797/use-of-apply-with-new-operator-is-this-possible)
  - [How can I call a javascript constructor using call or apply?](https://stackoverflow.com/questions/3362471/how-can-i-call-a-javascript-constructor-using-call-or-apply)

``` JS
// A bit of explanation:
var f = Cls.bind(anything, arg1, arg2, ...);
result = new f();

// The anything parameter doesn't matter much, since the new keyword resets f's context.
var f = Cls.bind.apply(Cls, [anything, arg1, arg2, ...]);
result = new f();

// Let's wrap that in a function. Cls is passed as argument 0, so it's gonna be our anything.

function newCall(Cls /*, arg1, arg2, ... */ ) {
  var f = Cls.bind.apply(Cls, arguments);
  return new f();
}

function newCall(Cls /*, arg1, arg2, ... */ ) {
  return new(Cls.bind.apply(Cls, arguments))();
}

// Finally, we should make sure that bind is really what we need. 
// (Cls.bind may have been overwritten). So replace it by Function.prototype.bind, 
// and we get the final result.
function newCall(Cls) {
  return new(Function.prototype.bind.apply(Cls, arguments));
  // or even
  // return new (Cls.bind.apply(Cls, arguments));
  // if you know that Cls.bind has not been overwritten
}
```

``` JS
// 其它实现
function conthunktor(Constructor) {
  var args = Array.prototype.slice.call(arguments, 1);
  return function() {

    var Temp = function() {}, // temporary constructor
      inst, ret; // other vars

    // Give the Temp constructor the Constructor's prototype
    Temp.prototype = Constructor.prototype;

    // Create a new instance
    inst = new Temp;

    // Call the original Constructor with the temp
    // instance as its context (i.e. its 'this' value)
    ret = Constructor.apply(inst, args);

    // If an object has been returned then return it otherwise
    // return the original instance.
    // (consistent with behavior of the new operator)
    return Object(ret) === ret ? ret : inst;

  }
}

function applyToConstructor(constructor, argArray) {
  var args = [null].concat(argArray);
  var factoryFunction = constructor.bind.apply(constructor, args);
  return new factoryFunction();
}
var d = applyToConstructor(Date, [2008, 10, 8, 00, 16, 34, 254]);

function callConstructor(constructor) {
  var factoryFunction = constructor.bind.apply(constructor, arguments);
  return new factoryFunction();
}
var d = callConstructor(Date, 2008, 10, 8, 00, 16, 34, 254);
```

- typescript compile: babel-loader vs ts-loader
  - Because Babel only does code transforms, the build step becomes incredibly fast as it skips the type-checking step and just strips out the all the TypeScript type-annotations – converting it to vanilla JS.
  - Babel has no type-safety at build time! 

    - to get around it: `"build": "tsc && webpack"`
  - Why use babel-loader instead?

    - In my case, because I wanted to take advantage of `babel-preset-env` . 
    - You pass in a list of browsers you want to support and Babel will only compile the language features that your target browsers don’t support. 
    - It will also make sure to include the required polyfills.

  - 这种使用babel的方案，当 webpack 编译的时候，babel-loader 会读取 .babelrc 里的配置，不会调用 typescript（所以本地项目无需安装 typescript），不会去检查类型
  - 配置tsconfig.json可以让ide提示编译错误
  - 使用了 TypeScript，为什么还需要 Babel 

    - 大部分已存项目依赖了 babel
    - 有些需求/功能需要 babel 的插件去实现（如：按需加载）
    - babel 有非常丰富的插件，它的生态发展得很好
    - babel 7 之前：需要前面两种方案来转译 TS
    - babel 7 之后：babel 直接移除 TS，转为 JS，这使得它的编译速度飞快

  - ts-loader has Type-safety at build time! 

    - but can be slow

  - ts-loader has one downside: We can’t pipe the output of another loader into it; it always reads the original file. 
  - ts-loader 支持 project references 的部分功能, 但babel不支持
  - 默认情况下，ts-loader 会进行 转译 和 类型检查，每当文件改动时，都会重新去 转译 和 类型检查，当文件很多的时候，就会特别慢，影响开发速度。

    - 所以需要使用 fork-ts-checker-webpack-plugin ，开辟一个单独的线程去执行类型检查的任务，这样就不会影响 webpack 重新编译的速度。

  - ts-loader 是不会读取 .babelrc 里的配置，即无法使用 babel 系列的插件，所以直接使用 ts-loader 将 ts/tsx 转成 js ，就会出现垫片无法按需加载、antd 无法按需引入的问题。

    - 所以需要用 ts-loader 把 ts/tsx 转成 js/jsx，然后再用 babel-loader 去调用 babel 系列插件，编译成最终的 js。

  - ref
    - [Webpack 转译 Typescript 现有方案](https://juejin.im/post/6844904052094926855)

- [Differences in output of Typescript compiler and Babel for classes](https://kevinwil.de/differences-in-output-of-typescript-compiler-and-babel-for-classes/)
  - Recently, I worked on switching our entire frontend codebase from using ts-loader to use babel-loader.
  - We continued to use ts-loader for some time because it was working well for us and we didn’t have a compelling reason to use Babel instead. 
  - That changed when I saw react-refresh. 
  - Our existing local development experience with react-hot-loader was often frustrating and unreliable. 
  - I realized we could drastically improve the local development experience if we could use react-refresh, but this would require us to switch to Babel. So I got to work.
  - When Typescript compiles classes, it marks class methods enumerable. 
    - This is not in line with the spec for ES6 classes, which says that class methods should be non-enumerable. 
    - When compiling typescript code with Babel, class methods are marked non-enumerable. 
    - Use class properties instead of class methods
    - Use getOwnPropertyNames in for-in
  - When Typescript compiles classes, it doesn’t generate any code for uninitialized class properties.
    - This is inconsistent with the spec for ES6 classes, which says that these properties should be initialized as undefined. Babel does this correctly.
    - Add a constructor to all subclasses
    - Initialize properties to themselves
    - Static create method in base class instead of constructor

- [TypeScript and Babel 7](https://devblogs.microsoft.com/typescript/typescript-and-babel-7/)
  - Babel is a fantastic tool with a vibrant ecosystem by transforming the latest JavaScript features to older runtimes and browsers; but it doesn’t do type-checking 
  - While TypeScript itself can do both, we wanted to make it easier to get that experience without forcing users to switch from Babel.
  - Using the TypeScript compiler is still the preferred way to build TypeScript. 
  - While Babel can take over compiling/transpiling – doing things like erasing your types and rewriting the newest ECMAScript features to work in older runtimes – it doesn’t have type-checking built in, and still requires using TypeScript to accomplish that. 
  - So even if Babel builds successfully, you might need to check in with TypeScript to catch type errors. 
  - For that reason, we feel `tsc` and the tools around the compiler pipeline will still give the most integrated and consistent experience for most projects.
  - As we mentioned above, the first thing users should be aware of is that Babel won’t perform type-checking on TypeScript code; it will only be transforming your code, and it will compile regardless of whether type errors are present. 
  - While that means Babel is free from doing things like reading `.d.ts` files and ensuring your types are compatible, presumably you’ll want some tool to do that, and so you’ll still need TypeScript. 
  - This can be done as a separate `tsc --watch` task in the background, or it can be part of a lint/CI step in your build. 
  - Second, there are certain constructs that don’t currently compile in Babel 7. Specifically, 
    - namespaces
    - bracket style type-assertion/cast syntax regardless of when JSX is enabled (i.e. writing `<Foo>x` won’t work even in .ts files if JSX support is turned on, but you can instead write `x as Foo` ).
    - enums that span multiple declarations (i.e. enum merging)
    - legacy-style import/export syntax (i.e. `import foo = require(...)` and `export = foo` )
    - babel core不支持，但社区插件可以支持
  - These omissions are largely based technical constraints in Babel’s single-file emit architecture. 

- `console.log()` is passed a reference to the object, so the value in the console changes as the object changes. 
  - To avoid that you can: `console.log(JSON.parse(JSON.stringify(obj)))`
  - Please be warned that if you log objects in the latest versions of Chrome and Firefox, what you get logged on the console is a reference to the object, which is not necessarily the 'value' of the object at the moment in time you call `console.log()` , but it is the value of the object at the moment you open the console.
  - 通过JSON.stringify(obj)序列化对象时，值类型为函数的属性会被忽略掉，数组中为函数的元素会打印成null
  - ref
    - https://stackoverflow.com/questions/11284663/console-log-shows-the-changed-value-of-a-variable-before-the-value-actually-ch

- `JSON.stringify()` converts a value to JSON notation representing it:
  - If the value has a `toJSON()` method, it's responsible to define what data will be serialized.
  - `undefined` ,                       `Function` s, and `Symbol` s are not valid JSON values. 

    - If any such values are encountered during conversion, they are either omitted (when found in an object) or changed to `null` (when found in an array). 
    - JSON.stringify() can return `undefined` when passing in "pure" values like `JSON.stringify(function(){})` or `JSON.stringify(undefined)` .

- styled-components中的样式冲突要注意计算specificity
  - `div.cls1` 的特指度高于 `.cls2` ，即使.cls2写在后面
  - `className=cls1 cls2` 最终使用的样式取决于源码import进来后，cls1和2在源码中声明的先后顺序
  - 不推荐的解决方法是采用id选择器
- 在外层div将font-size设置为1.2em后，button上的文字仍然是13.33的font-size，需要设置的是 `button {font-size: 100%}`
  - 要注意分辨文字是span，还是button
- 前端兼容性处理 caniuse 
  - 3大pc浏览器：chrome、firefox、safari
  - mobile浏览器：3大pc对应的3大移动，Android, UC，Samsung，QQ Browser 
- 副作用就是和本职无关的东西，函数的本职是接收参数，并返回值，多次同参调用都是确定的。
  - 举几个前端里的副作用例子：调接口获取数据、注册监听函数、手动操作DOM、 访问修改全局变量、打印log，使用 setTimeout 等
- console对象
  - 分级日志：console.log/info/debug/warn/error
  - 字符串占位符： `%s` 代表字符串， `%o` 代表对象， `%d` 代表数字
  - 设置样式：开头使用 `%c` , 如 `console.log('%cNull','color:gold;font-size:large')`
  - `console.dir` ：强制以JSON模式输出，如DOM会转换成json对象
  - `console.table` ：将对象属性或数组打印成表格更美观
  - `console.assert` ：仅当第一个参数为false时才打印第二个参数
  - `console.trace` ：打印调用栈
  - `console.time/End` ：打印代码执行时间
  - `console.memory` ：打印内存使用情况
  - `console.clear` ：清空控制台输出
  - `console.group` ： 分组输出，便于阅读
- 确保FMP（首次有效绘制） 尽可能的快速, 方法之一就是分阶段进行代码拆分
  - render loading-render-analytics
  - FMP所需的所有数据都可以在加载阶段获取其他代码的同时获取
  - http://www.alloyteam.com/2019/12/14174/
- RESTful APIs 缺点(GraphQL的优点)
  - 数据格式不规范
  - 猜谜游戏（如何判定一个失败的请求，400，401，还是404？）
  - 无意义的对话
  - 无合约协议
- 从输入页面URL到页面渲染完成大致流程
  - 解析URL
  - 浏览器本地缓存
  - DNS解析
  - 建立TCP/IP连接
  - 发送HTTP请求
  - 服务器处理请求并返回HTTP报文
  - 浏览器根据深度遍历的方式把html节点遍历构建DOM树
  - 遇到CSS外链，异步加载解析CSS，构建CSS规则树
  - 遇到script标签，如果是普通JS标签则同步加载并执行，阻塞页面渲染，如果标签上有defer/async属性则异步加载JS资源
  - 将dom树和CSS DOM树构造成render树
  - 渲染render树
- 浏览器加载与渲染的时间概念 
  - P：首次绘制。用于标记导航之后浏览器在屏幕上渲染像素的时间点。这个不难理解，就是浏览器开始请求网页到网页首帧绘制的时间点。这个指标表明了网页请求是否成功。
  - FCP：首次内容绘制。FCP标记的是浏览器渲染来自DOM第一位内容的时间点，该内容可能是文本、图像、SVG甚至canvas元素。
  - FMP：首次有效绘制(First Meaningful Paint)。这是一个很主观的指标。根据业务的不同，每一个网站的有效内容都是不相同的，有效内容就是网页中"主角元素"。对于视频网站而言，主角元素就是视频。对于搜索引擎而言，主角元素就是搜索框。
  - TTI：可交互时间。用于标记应用已进行视觉渲染并能可靠响应用户输入的时间点。应用可能会因为多种原因而无法响应用户输入：①页面组件运行所需的JavaScript尚未加载完成。②耗时较长的任务阻塞主线程
  - 根据devtool时间轴的结果

    - 虽然CSR(客户端渲染)配合预渲染方式（loading、骨架图）可以提前FP、FCP从而减少白屏问题，但无法提前FMP
    - SSR(服务端渲染)将FMP提前至js加载前触发，提前显示网页中的"主角元素"。SSR不仅可以减少白屏时间还可以大幅减少首屏加载时间。

  - ref
    - https://www.zhihu.com/question/308792091
    - https://zhuanlan.zhihu.com/p/90746589

- lodash引用方式
  - `import { cloneDeep } from 'lodash';`
    - 70.9KB

  - `import cloneDeep from 'lodash/cloneDeep';`
    - 17.8KB

  - `import { cloneDeep } from 'lodash-es';`
    - 14.6KB

  - Because static analysis in a dynamic language like JavaScript is hard, there will occasionally be false positives. 

    - Lodash is a good example of a module that looks like it has lots of side-effects, even in places that it doesn't. 
    - You can often mitigate those false positives by importing submodules (e.g. `import map from 'lodash-es/map'` rather than `import { map } from 'lodash-es'` ).

- named import和namespace import都可以被webpack v5和rollup进行tree shaking
  - default import对于多属性的对象，无法进行tree shaking
  - https://blog.csdn.net/qq_34629352/article/details/104258640
  - https://webpack.js.org/guides/tree-shaking/
  - Note that any imported file is subject to tree shaking. This means if you use something like css-loader in your project and import a CSS file, it needs to be added to the side effect list so it will not be unintentionally dropped in production mode
- `$` and `$$` will work on any web page (if jQuery is not included also) on Google Chrome, Firefox and Safari browsers where $ returns first element of selector passed.

    - `$` is `document.querySelector()`
    - `$$` is `document.querySelectorAll()`
    - `$x()` Returns an array of elements that match the specified XPath.
    - Warning: These functions only work when you call them from the Chrome DevTools Console. They won't work if you try to call them in your scripts.
    - They are native functions of Google Chrome and Firefox browsers, you can see $ and $$ definition in Safari as well.
    - https://developers.google.com/web/tools/chrome-devtools/console/utilities

- The `get` syntax binds an object property to a function that will be called when that property is looked up.
  - 语法： `{get prop() { ... } }` 或 `{get [expression]() { ... } }`
  - prop is the name of the property to bind to the given function.
  - you can also use expressions for a computed property name to bind to the given function.
  - It is not possible to simultaneously have a getter bound to a property and have that property actually hold a value, although it is possible to use a getter and a setter in conjunction to create a type of pseudo-property.
  - If you want to remove the getter, you can just delete it: `delete obj.latest;`
  - While using the get keyword and Object.defineProperty() have similar results, there is a subtle difference between the two when used on classes.
  - When using get the property will be defined on the instance's prototype, while using Object.defineProperty() the property will be defined on the instance it is applied to.
- js定义了两种不同的属性
- 如何区分属性的类型？
  - 通过 `Object.getOwnPropertyDescriptor()` 查看属性的描述符。有 `value` 的是数据属性，没有的是访问器属性
  - 数据属性存储值，访问器属性不存储值
  - value和set/get不能共存。因为有了set/get同时又有value，读写不明确
  - 访问器属性的功能用自定义函数也能实现，但es5原生支持更简洁
- 数据属性主要有四个特性描述对象属性行为
  - [ ] [[Configurable]]: 默认为true。表示能否通过delete删除属性来重新定义属性，或者能否把属性改为可访问属性；
  - [ ] [[Enumerable]]: 默认为true。表示能否通过for-in循环返回属性；
  - [ ] [[Writable]]: 默认为true。表示能否修改属性的值；
  - [ ] [[Value]]: 默认为underfined。表示包含属性的数据值。读写属性之都从这个位置进行；
- 访问器属性不包含数据值。访问器属性不能直接定义，必须通过Object.defineProperty()定义。但包含一对getter和setter函数
  - [ ] [[Configurable]]: 默认为true。表示能否通过delete删除属性来重新定义属性，或者能否把属性改为可访问属性；
  - [ ] [[Enumerable]]: 默认为true。表示能否通过for-in 循环返回属性；
  - [ ] [[Get]]: 默认为underfined。表示读取属性时调用的函数；
  - [ ] [[Set]]: 默认为underfined。表示写入属性时调用的函数；
- import lodash
  - import { has } from 'lodash-es'; 

      - tree shakable, but CommonJS modules are not 

  - import has from 'lodash/has'; 

      -  lodash holds all it's functions in a single file, so rather than import the whole 'lodash' library at 100k, it's better to just import lodash's has function which is maybe 2k.
      - 'lodash/has' isn't a separate package. There's a file called has.js in the root of the regular 'lodash' package, and import has from 'lodash/has' (or const has = require ('lodash/has) will load that file. 

  - import { has } from 'lodash'; 
- 前端定时器
  - setTimeout()，精确度不高，可能有延迟执行的情况发生，且因为动用了红黑树，所以消耗资源大； 
  - setImmediate()，消耗的资源小，也不会造成阻塞，但效率也是最低的。

      - 目前只支持IE10以上, 速度比setTimeOut执行延迟快一些

  - process.nextTick()，效率最高，消费资源小，但会阻塞CPU的后续调用；
  - 关于Event Loop和任务队列, 除了script整体代码，micro-task的任务优先级高于macro-task

      - macro-task: script (整体代码)，setTimeout, setInterval, setImmediate, I/O, UI rendering.
          - script(整体代码) ，可以理解为待执行的所有代码
      - micro-task: process.nextTick, Promise(原生)，Object.observe，MutationObserver
      - 执行过程
          - 第一步script整体代码被执行，创建各种macro-task,执行micro-task的部分
          - 第二步执行其他micro-task,优先级process.nextTick高于Promise
          - 第三步来执行macro-task. setTimeout的优先级高于setImmediate(一般情况,若timeout延迟大,后者可能先执行) 
          - 不同版本的node执行结果可能不同

  - ref https://segmentfault.com/a/1190000008595101
- webpack module vs chunk vs bundle
  - Webpack has three closely related terms - module, chunk, and bundle. 
  - A module is a piece of JS code that encapsulates data and provides functionality. Modules can depend on one another and thus, form a dependency graph. 
  - In the webpack bundling process, a few modules form a chunk. 
  - A bundle is an output file, produced by the bundling process. In most cases, each chunk emits exactly one bundle.
- webpack-hmr

``` js
const server = http.createServer(app);
let currentApp = app;
console.log(currentApp === app); // Returns true 

if (process.env.NODE_ENV !== 'production') {

  if (module.hot) {
    module.hot.accept('./server', () => {
      console.log(currentApp === app); // Returns false 

    })
  }
}
```

- node require json文件
    - Node.js中推崇非阻塞I/O，但是require一个模块时却是同步调用的，这会带来性能上的开销，但并不是每次require都很耗时，因为在require成功之后会缓存起来，在此加载时直接从缓存读取，并没有额外开销。
    - 当通过.json的方式加载文件时，固然方便，但大量使用时会导致这些数据被缓存。大量数据会驻留在内存中，导致GC频繁和内存泄漏。
- npm list -g -depth=0
    - 列出本地已安装的包
- npx
    - npm从5.2版开始，增加了npx命令，现已集成进npm，不需单独安装
    - npx想要解决的主要问题，就是调用项目内部安装的模块
    - 若要调用Mocha，一般只能在项目脚本和package.json的scripts字段里面，如果想在命令行下调用，必须 `node-modules/.bin/mocha --version`
    - npx让项目内部安装的模块用起来更方便 `npx mocha --version`
    - npx的原理就是运行的时候，会到node_modules/.bin路径和环境变量$PATH里面，检查命令是否存在
    - 由于npx会检查环境变量$PATH，所以系统命令也可以调用 `npx ls -ll`
- REPL 交互式编程环境 (Read-Eval-Print-Loop) 
    - jShell
    - python 
    - babel-node(有babel-cli提供)
- targe=_blank
    - 当一个外部链接使用了target=_blank的方式，这个外部链接会打开一个新的浏览器tab。此时，新页面会打开，并且和原始页面占用**同一个进程**(UI进程)。
    - 这也意味着，如果这个新页面有任何性能上的问题，比如有一个很高的加载时间，这也将会影响到原始页面的表现。
    - 如果你打开的是一个同域的页面，那么你将可以在新页面访问到原始页面的所有内容，包括document对象(window.opener.document)。
    - 如果你打开的是一个跨域的页面，你虽然无法访问到document，但是你依然可以访问到location对象。
- node依赖
    - dependencies
        - 是最常用普通业务依赖
    - devDependencies
        - 开发环境依赖，常用来指定打包、测试工具
    - peerDependencies
        - 比较适合插件库来声明所依赖的核心库，将依赖提升到根目录避免重复下载
        - 指定当前包（也就是你写的包）兼容的宿主版本
        - 可以避免类依赖库被重复下载
            - 如果用户显式依赖了核心库，则可以忽略各插件的peerDependency声明
            - 如果用户没有显式依赖核心库，则按照插件peerDependencies中声明的版本将库安装到项目根目录中
            - 当用户依赖的版本、各插件依赖的版本之间不相互兼容，貌似会报错让用户自行修复
    - optionalDependencies
        - 可选依赖，它们即使安装失败，npm仍然继续运行
    - bundleDependencies
        - 在发布时会将指定的包打包到最终的发布包里
        - undleDependencies节点的功能跟dependencies节点是一样的，区别在于，当需要构建项目并发布版本时，bundleDependencies节点下的依赖会被包含在构建结果中，不需要另外npm install来安装了
    - 参考
        - https://github.com/SamHwang1990/blog/issues/7
- html a标签属性 rel='nofollow'
    - 告诉搜索引擎不要此网页上的链接或不要追踪此特定链接
    - 使用场景
        - 屏蔽广告/付费链接的权重
        - 屏蔽恶意用户
        - 划分优先级
    - rel="noopener noreferrer"可以取消传递相关信息
- The main difference between Cyan and Teal is that the Cyan is a color visible between blue and green; subtractive (CMY) primary color and Teal is a low-saturated color, a bluish-green to dark medium, similar to medium blue-green and dark cyan.
- 语言地区代码的构成，如en-US, zh-CN
    - The syntax and registry of HTTP language tags is the same as that defined by RFC 1766 
    - a language tag is composed of 1 or more parts: A primary language tag and a possibly empty series of subtags
    - any two-letter primary-tag is an ISO-639 language abbreviation and any two-letter initial subtag is an ISO-3166 country code.
    - 参考 https://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html
- 渐进式图片  
    - JPEG、GIF和PNG这三种图像格式都提供了一种功能，让图像能够更快地显示图像可以以一种特殊方式存储，显示时先大概显示图像的草图，当文件全部下载后再填充细
- file-loader will copy files to the build folder and insert links to them where they are included. 
- url-loader will encode entire file bytes content as base64 and insert base64-encoded content where they are included. So there is no separate file.
- The url-loader works like the file-loader, but can return a DataURL if the file is smaller than a byte limit.
- 获取数组中随机元素
    - ` arr[Math.floor(Math.random()*(arr.length))]`
- `performance.now()` vs `date.now()`
    - performance.now() returns the number of milliseconds, with microseconds in the fractional part and is more precise in orders of magnitude. 精度更高，不依赖系统时间，但在大型循环中使用会明显感觉慢，输出的是相对于performance.timing.navigationStart(页面初始化)的时间
        - Use cases include benchmarking and other cases where a high-resolution time is required such as media (gaming, audio, video, etc.)
        - performance.now() is only available in newer browsers (including IE10+).可能会有兼容性问题
    - Date.now() returns the number of milliseconds elapsed since Unix epoch(1 January 1970 00:00:00 UTC) and is dependent on system clock.会因为系统时间的变化而改变，准确性有时不能保证
        - Use cases include same old date manipulation ever since the beginning of JavaScript.
- typescript typeof

``` 

let bar = {a: 0};
let TypeofBar = typeof bar;  // the value "object"
type TypeofBar = typeof bar; // the type {a: number}
```

- Object.prototype.hasOwnProperty.call(obj, attrName); 
  - obj.hasOwnProperty(prop)判断一个属性是定义在对象本身而不是继承自原型链

    - 调用的是js中Object对象原型上的hasOwnProperty()方法

  - js没有将hasOwnProperty作为一个敏感词，所以我们很有可能将对象的一个属性命名为hasOwnProperty，这样一来就无法再使用对象原型的hasOwnProperty 方法来判断属性是否是来自原型链，解决方法有几种

    - ({}).hasOwnProperty.call(foo, 'bar'); // true
    - Object.prototype.hasOwnProperty.call(foo, 'bar');

- TypeScript 3.0在JSX命名空间中引入了一个新的类型别名 `LibraryManagedAttributes`
    - 这是一个辅助类型，用于告诉TypeScript某个JSX标记可以接受哪些属性
    - TypeScript 3.0 adds support for a new type alias in the JSX namespace called LibraryManagedAttributes. 
    - This helper type defines a transformation on the component’s Props type, before using to check a JSX expression targeting it; thus allowing customization like: how conflicts between provided props and inferred props are handled, how inferences are mapped, how optionality is handled, and how inferences from differing places should be combined.
    - The default-ed properties are inferred from the defaultProps property type. If an explicit type annotation is added, e.g. static defaultProps: `Partial<Props>` ; the compiler will not be able to identify which properties have defaults
    - Use static defaultProps: `Pick<Props, "name">` as an explicit type annotation instead

- As of NPM 2.0.0, importing local dependencies is supported natively.

    - `"bar": "file:../foo/bar"`
- npm main vs module
  - 当我们在不同环境下 `import` 一个npm包时，到底加载的是npm包的哪个文件？

    - 由于我们使用的模块规范有ESM和CommonJS两种，为了能在node环境下原生执行 ESM 规范的脚本文件，.mjs文件就应运而生。当存在 index.mjs 和 index.js 这种同名不同后缀的文件时， `import './index'` 或者 `require('./index')` 是会优先加载 index.mjs 文件
    - `main` : 定义了npm包的入口文件，browser环境和node环境均可使用
    - `module` : 定义npm包的ESM规范的入口文件，browser环境和node环境均可使用
    - `browser` : 定义npm包在browser环境下的入口文件
    - 实际上的优先级是 `browser=browser+mjs > module > browser+cjs > main`
      - webpack会根据这个顺序去寻找字段指定的文件，直到找到为止

  - 最早的npm包都是基于CommonJS规范(name, version, main)，当require('package1')的时候，就会根据main字段去查找入口文件

    - ES2015后，js拥有了ES Module，相较于之前的模块化方案更优雅，并且ES模块也是官方标准（JS 规范），而CommonJS模块是一种特殊的传统格式，利用ES Module的特性可以提高打包的性能，其中提升一个便是 tree shaking
    - CommonJS规范的包都是以 `main` 字段表示入口文件了，如果使用ES Module的也用main字段，就会对使用者造成困扰
    - webpack从版本2开始也可以识别 `module` 字段。打包工具遇到 package1 的时候，如果存在 module 字段，会优先使用，如果没找到对应的文件，则会使用 main 字段，并按照 CommonJS 规范打包
    - tree-shaking的功能就是把我们JS中无用的代码给去掉，如果把打包工具通过入口文件，产生的依赖树作为tree，tree-shaking就是把依赖树中用不到的代码shaking掉

- html所有元素通用的title属性，可以作为鼠标悬浮提示，可以用来作为input前类似label的提示，可以作为a11y的补充(对键盘导航影响大)
- tsc vs babel
  - I'd probably roll plain tsc for a lib. Output the js, .d.ts and source maps into the same folder (different from source folder).
  - Babel for "endpoint" code since one would use things like HMR, useful babel plugins, etc
- ts definitions downloaded does not match the component, 定义过时了，不匹配
  - https://stackoverflow.com/questions/44043492/override-typescript-types-in-v2-2-2-downloaded-from-npm-types/44046969#44046969
  - tsconfig.json > paths: './typings/*
  - https://stackoverflow.com/questions/44067014/error-ts7016-could-not-find-a-declaration-file-for-module-implicitly-has'
  - 将tsconfig.json的noImplicitAny设为any
- babel [7.0] Deprecate env option in .babelrc #5276
  - https://github.com/babel/babel/issues/5276
  - Options specific to a certain environment are merged into and overwrite non-env specific options.
  - Because it's JS you could do this in a lot of ways
- IOS环境下的按钮都是经过美化的，但通常我们在设计web app的时候不需要这些看上去老土的样式，所以，去除这些显得很有必要
  - `-webkit-appearance` 会将webkit浏览器中的元素默认样式去除
  - 会导致无法获取checkbox值, 给这个元素重新赋上-webkit-appearance:checkbox就不会报错了
- typescript interface extends vs `&` intersect
  - the most significant is the difference in how members with the same property key are handled when present in both types.
  - extends above results in an error because the derriving interface declares a property with the same key as one in the derived interface but with an incompatible signature.
  - intersection types can contain conflicting types
  - ref
    - https://stackoverflow.com/questions/52681316/difference-between-extending-and-intersecting-interfaces-in-typescript
    - https://stackoverflow.com/questions/42735611/why-can-intersection-types-contain-conflicting-types
