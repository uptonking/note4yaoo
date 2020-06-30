---
tags: [book, cs, js]
title: read-cs-js
created: '2020-06-30T05:30:33.786Z'
modified: '2020-06-30T05:32:35.602Z'
---

# read-cs-js

## book-JavaScript语言精粹. 修订版_Douglas Crockford_2012

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
  - `'c'+'a'+'t'==='cat'` 返回true
  - type of运算符检查属性类型返回的值就是js数据类型，6种
    - string
    - number
    - boolean
    - undefined
    - object
    - function
- js运算符与表达式
  - 每个 `<script>` 标签提供一个被编译且立即执行的编译单元，因为缺少链接器，js把它们一起抛到一个公共的全局命名空间中
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
  - 从对象取属性值的方式包括 `obj["attrName"]` 和 `obj.attrName`
      - []的方式属性名不能使保留字
      - 推荐使用点号运算符取值
      - 若属性名不存在，则返回undefined
      - undefined可通过&&处理
  - 给对象添加属性值的方式也是2种
      - 若属性存在，则值覆盖
      - 若属性不存在，则添加
  - 对象传递传的是引用
  - 全局变量削弱了程序的灵活性和健壮性，推荐为应用只创建唯一的全局变量 `var v={};`
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

``` js
      var sum = function() {
        var i, sum = 0;
        for (i = 0; i < arguments.length; i += 1) {
          sum += arguments[i];
        }
        return sum;
      };
      console.log(sum(4, 8, 15, 16, 23, 42)); // 108
```

  - 方法调用模式
      - 当一个函数被保存为对象的一个属性肘，我们称它为一个方法
      - 一个方站被调用肘， this被绑定到该对象
      - 典型使用： 点号和[]取属性
      - 示例

``` js
      var myObject = {
        value: 0,
        increment: function(inc) {
          this.value += typeof inc === 'number' ? inc : 1;
        }
      }；
      myObject.increment();
      console.log(myObject.value); // 1
      myObject.increment(2);
      console.log(myObject.value); // 3
```

  - 函数调用模式
      - 当一个函数并非一个对象的属性时，那么它就是被当做一个函数来调用的
      - 以此模式调用函数时，this被绑定到全局对象
      - 这个设计的后果就是方法不能利用内部函数来帮助它工作
      - 示例

``` js
      var add = function(x, y) { return x + y; };
      myObject.double = function() {
        var that = this; //解决方法是将外部函数的this保存一份传给内部函数
        var helper = function() {
          that.value = add(that.value, that.value);
        };
        helper(); //以函数的形式调用helper()
      }；
      //以方法的形式调用double
      myObject.double();
      console.log(myObject.value); // 
```

  - 构造器调用模式
      - 如果在一个函数前面带上new来调用，那将会创建一个连接到该函数的prototype属性的新对象，同时this会被绑定到那个新对象上
      - 一个函数，如果创建的目的就是希望结合new来调用，那它就被称为构造器函数
          - 按照约定，它们保存在以大写格式命名的变量里
          - 如果调用构造器函数时没有在前面加上new，可能会发生非常糟糕的事情，既没有编译时警告，也没有运行时警告
      - 不推荐使用构造器函数
      - 示例

``` js
      //创建一个名为Quo的构造器函数
      var Quo = function(string) { this.status = string; }
      //给Quo的所有实例提供一个名为get_status的公共方法
      Quo.prototype.get_status = function() { return this.status; }
      var myQuo = new Quo("confused");
      console.log(myQuo.get_status()); // confused
```

  - apply调用模式
      - apply()方法让我们构建一个参数数组传递给调用函数，它也允许我们选择this的值 - apply()接收两个参数，第1个是要绑定给this的值，第2个就是一个参数数组
      - 示例

``` js
      var array = [3, 4];
      var sum = add.apply(null, array);
      console.log(sum); // 7
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
  - 模块模式通常结合单例模式使用，js的单例就是用对象字面量表示法创建的对象，对象的属性位可以是数值或函数，并且属性值在该对象的生命周期中不会发生变化
    - 通常作为工具为程序其他部分提供功能支持
- 继承
  - Java继承优点
      - 代码重用
      - 引入了类型系统的规范
  - js提供了一套更为丰富的代码重用模式，它可以模拟那些基于类的模式
  - 当采用构造器调用模式，即用new前缀去调用一个函数时，函数执行的方式会被修改
  - 构造器函数默认首字母大写
  - 一个更好的备选方案就是根本不使用 new
  - 基于原型的继承相比基于类的继承在概念上更为简单: 一个新对象可以继承一个旧对象的属性
      - 指明与所基于的基本对象的区别
  - 使用函数化模块可以复用现有对象的功能，也可以作为一种继承
- 数组
  - 一个数组字面量是在一对 `[]` 中包围零个或多个用逗号分隔的值的表达式
  - 数组默认的属性名依次是'0’，'1'...
  - 对于超出范围的属性名，属性值为undefined
  - 数组继承自Array.prototype，而普通对象继承自Object.prototype
  - 多数语言要求一个数组的所有元素是相同的类型，但js允许数组包含任意混合类型的值
  - 每个数组对象有个length属性，js的length无上界，若下标大于当前length，那数组自动扩容
  - 你可以直接设置length的值，设置更大的length不会给数组分配更多的空间，而把length设小将导致所有下标大于等于新length的属性被删除
  - 由于js的数组其实就是对象，所以delete运算符可以用来从数组中移除元素
      - 示例 `delete numbers[2];` ，执行后该位置的属性值会变为undefined，仍占位
      - 若要删除后后面元素都前移，要用 `splice(start,num)` ，效率可能不高/to-test
  - 因为js数组其实就是对象，所以for in 语句可以用来遍历一个数组的所有属性，但无法保证属性的顺序，特别是原型链中有意外属性时，直接使用for循环可避免此问题
  - 当属性名是小而连续的整数肘，应该使用数组，否则该使用对象
  - typeof运算符报告数组的类型是object，js没有一个好的机制来区别数组和对象
  - 可以通过定义自己的函数来区分数组和对象
      - 示例

``` js
      var isArray = function(va1ue) {
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
  - arr.slice(start, [end])  对arr中一部分做浅复制，返回新数组，前闭后开
  - arr.splice(start, delCount, item) 从arr中移除元素并插入item，返回移除元素数组
  - arr.sort()  对arr所有元素进行排序，不能给数字排序，排序元素默认被视为字符串
      - 通过将自定义函数传入sort()可实现排序数字数组
      - js的sort()不具有稳定性，不同浏览器实现方式不同
  - arr.unshift(item...)  将元素添加到arr头部，返回arr新length
- Function
  - func.apply(thisArg, argArray)
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
  - str.indexOf(searchStr, pos)  在str内查找另一个字符串searchStr，返回位置索引
  - str.match(regexp)  若无g标识，则功能相等于regexp.exec(str)
  - str.replace(oldVal, newVal)  查找替换，返回一个新字符串
      - 若oldVal是字符串，则只会替换第一次出现oldVal的地方
      - 若oldVal是正则表达式且带有g标识，则会替换所有匹配
      - newVal可以是字符串或函数
  - str.search(regexp)  类似indexOf
  - str.slice(start, end) 复制str的一部分来构造一个新的字符串
  - str.split(sperator, limit)  分割字符串，返回数组
  - str.substring(start, end)  同slice，但参数不能为负数，推荐使用slice
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
  - 箭头函数自身没有this, arguments, super
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
  - Set获取默认迭代器values()，Map获取默认迭代器entries(), WeakSet/Map无迭代器
  - 字符串的方括号表示法str[1]作用于码元上，而非字符上，无法正确获取双码元字符
  - 字符串的默认迭代器默认迭代的是字符，而不是码元 for(let c of str)
  - HTML规范中规定NodeList带有默认迭代器，表现与数组迭代器一致
  - 扩展运算符 `...` 能作用于所有可迭代对象，是创建数组最简单的方法
- 异步编程
  - Promise
  - async await

## ES6标准入门. 第3版_阮一峰_2017

- babel
  - babel默认只转换新的js句法，不会转换只增加新API的已有对象，如新增的Array.from()
  - babel6.0开始不再直接提供浏览器环境版本
- Promise是一个对象，保存着未来才会结束的事件(异步操作)的结果
- Generator函数是一个状态机，执行它会返回一个迭代器对象生成生成函数
- async-await是Generator-yield的语法糖
- Decorator修饰器是ES2017新增的在编译时执行的函数，可以用来修改类的行为

## JavaScript高级程序设计. 第3版_Nicholas C. Zakas_2012

- js诞生于1995，最初目的是用于协助服务端处理输入与验证操作
- 完整的JavaScript组成部分
  - ECMAScript
      - 标准与环境无关，浏览器只是宿主环境之一，还有其他宿主如Node、Flash
      - 宿主环境不仅提供标准实现，还会提供语言标准功能的扩展功能，如DOM
      - ECMAScript是对标准各方面内容的描述，JavaScript和ActionScript都实现了
      - ES1.0-1997-与Netscape的JavaScript1.1大多数内容相同
      - ES2.0-1998-只是编辑加工与ISO保持一致，内容未改动
      - ES3.0-1999-新增正则表达式、异常处理，修改字符串处理、数值输出
      - ES4.0-未通过
      - ES5.0-2009-新增JSON对象、高级属性处理、严格模式
  - DOM
      - DOM是针对XML但经过扩展也可用于HTML的API，将整个文档也映射成一个多层节点结构
      - 文档中每个部分都是某种类型的节点，节点可以包含不同类型的数据
      - DOM1级(1998)-包括DOM Core(规定如何映射基于XML的结构与访问节点)和DOM HTML(添加了针对HTML的对象和方法)
      - DOM2级(199x)-添加了鼠标和事件模块、支持CSS
      - DOM3级(199x)-引入了以统一方式加载和保存文档的方法，添加文档验证方法，支持XML1.0规范
  - BOM
      - BOM可以控制浏览器显示页面以外的部分
      - HTML5将很多BOM功能写入正式规范
      - BOM先关功能包括cookie，窗口操作，xhr
- script标签
  - 6属性
      - type-指定脚本的语言类型，也是MIME类型，默认值text/javascript
      - src-指向包含待执行代码的外部文件
          - src属性可以包含跨域的脚本
      - charset-指定src属性指向的代码的字符集
      - async-标识脚本下载完成后异步执行
          - 只对外部脚本文件有效
      - defer-标识脚本会延迟到文档完全被解析和显示之后再执行
          - 立即下载但延迟执行，延迟到在 `</html>` 之后执行，若多个，仍按defer的顺序
          - 只对外部脚本文件有效
      - language-被type取代
  - 浏览器在执行HTML的时候如果遇到 `<script>` 时会停止页面的渲染, 去下载和执行js的文件，直到遇见 `</scirpt>` 才会继续渲染页面。故浏览器在执行js文件的时候浏览器表现为一片空白, 为了解决这个问题ECMAScript定义了defer和async两个属性用于控制JS的下载和执行
      - 若没有 defer 和 async，浏览器会立即加载并执行指定的脚本，“立即”指的是在渲染该script标签之下的文档元素之前，也就是说不等待后续载入的文档元素，读到就加载并执行
      - 若只有 async，加载和渲染后续文档元素的过程将和指定脚本的加载与执行并行进行，这就是异步
      - 若只有 defer，加载后续文档元素的过程将和指定脚本的加载并行进行（异步），但是脚本的执行要在所有元素解析完成之后，DOMContentLoaded事件触发之前完成
      - 若同时有async 和 defer，则为async，defer作为不支持async浏览器的fallback
      - 参考 https://segmentfault.com/q/1010000000640869
      - ！[defer和async原理顺序图](http://segmentfault.com/img/bVcQV0)
  - defer和async 相同点
      - 下载脚本文件时都是异步的，不阻塞html解析渲染，脚本执行不会和html解析不会同时
          - 脚本执行和页面的渲染是共用一个线程，不可能同时执行
      - 对于inline的script（内联脚本）无效
      - 用这两个属性的脚本中不能调用document.write方法
      - 有脚本的onload的事件回调
  - defer和async 不同点
      - 最大的不同点在于脚本下载完成后何时执行
      - html4.0中定义了defer
          - html5.0中定义了async
      - 每一个defer属性的脚本都是在页面解析完毕之后，按照原本的顺序执行，同时会在document的DOMContentLoaded之前执行
          - 每一个async属性的脚本都在它下载结束之后立刻执行，同时会在window的load事件之前执行，所以就有可能出现脚本执行顺序被打乱的情况；
  - 传统的做法是将 `<script>` 标签放在 `<head>` 标签对的尾部，这样等到全部js被下载、解析、执行完成后，才开始解析渲染 `<body>` 标签的页面内容
  - 现在的做法是将 `<script>` 标签放在 `<body>` 标签对的尾部
- ECMAScript数据类型 
  - ES提供6种数据类型(5种基本类型，1种引用类型)，且不支持创建自定义类型
      - string, number, boolean, undefined, null, object
  - typeof运算符返回值
      - string, number, boolean, undefined, object, function
      - typeof null 返回 object，视为空的对象引用
  - undefined
      - 是字面量，作为变量未初始化时的默认值
  - null
      - undefined值是派生自null值的
      - null ==  undefined 返回 true
      - null === undefined 返回 false
  - boolean
      - 只有2个字面量值
      - 可转换成true的值
          - 非空字符串
          - 非零数字值，包括无穷大
          - 任何对象
      - 可转换成false的值
          - 空字符串
          - 0，NaN
          - undefined，null
  - number
      - 使用IEEE754表示整数和浮点数值，都以64位存储
          - 默认所有整数都是有符号整数
          - 无符号整数只能是正数
      - 1.0会被转换成整数1
      - 0.1 + 0.2 > 0.3，建议不要直接比较浮点数相等
      - 超出js范围的值用字面量表示 Infinity, -Infinity
      - NaN是一个特殊的数值
          - 涉及NaN的运算都会返回NaN
          - NaN与任何值都不想等，包括自身
      - 在ES5的js引擎中，parseInt()已经不再具有解析八进制的能力，前导0被视为无效
  - string
      - ES中字符串不可变
      - String()函数转换规则
          - 判断是否有 toString()
          - 判断null
          - 判断undefined
  - object
      - 对象是一组数据和功能的集合
      - 每个都具有的属性
          - constructor:指向创建当前对象的函数
      - 每个都具有的方法
          - hasOwnProperty(propertyName)
          - isPrototypeOf(object)
          - propertyIsEnumerable(propertyName):可否可以for-in
          - toLocaleString()
          - toString()
          - valueOf()：返回对象的字符串、数值或布尔值表示，通常与toString()方法的返回值相同
              - array.valueOf();返回值是它自身的引用
- 语法基础
  - for-in循环输出的属性名的顺序是不可预测的
      - 具体来讲，所有属性都会被返回一次，但返回的先后次序可能会因浏览器而异
  - typeof通常用来检测基本数据类型，要判断一个对象的具体类型可用instanceof
      - obj instanceof Array/RegExp
      - 如果使用 instanceof 操作符检测基本类型的值，则该操作符始终会返回 false
  - 变量提升
      - 使用 var 关键字声明的变量，无论其实际声明位置在何处，都会被视为声明于所在函数的顶部
      - 如果声明不在任意函数内，则视为在全局作用域的顶部
      - 问题
          - if块内声明的变量会被提升
          - for-i循环的循环变量i在循环结束后依旧存在
          - 函数内不使用var声明的变量会提升到全局作用域顶部
  - ECMAScript 5明确规定，使用正则表达式字面量必须像直接调用RegExp构造函数一样，每次都创建新的RegExp实例
  - regexp.exec(str1)返回包含第一个匹配项信息的数组，或在无匹配项的情况下返回null
      - 返回的数组虽然是Array的实例，但包含两个额外的属性：index 和 input
- 引用类型
  - 在通过对象字面量定义对象时，实际上不会调用 Object 构造函数
      - 在使用数组字面量表示法时，也不会调用 Array 构造函数
  - 函数参数推荐的做法是对那些必需值使用命名参数，而使用对象字面量来封装多个可选参数
  - 所有对象都具有 toLocaleString()、toString()和 valueOf()方法，包括数组
- Array
  - 如果数组中的某一项的值是 null 或者 undefined，那么该值在 `join()、 toLocaleString()、toString()和、valueOf()` 方法返回的结果中以空字符串表示
  - `sort()` 方法会调用每个数组项的toString()转型方法，然后比较得到的字符串，以确定如何排序
      - 即使数组中的每一项都是数值，sort()方法比较的也是字符串
      - 通过传入比较函数可实现数值排序
  - arr1.shift()移除第一项
  - arr1.concat()不传参数时直接返回数组的拷贝
  - arr1.slice(start, end)创建新数组
  - arr1.splice(start, delCount, ...item)用于插入和删除数组项
  - 数组的5种迭代方法
      - filter()：返回true项组成的新数组
      - forEach()：无返回值
      - map()：返回每项新结果组成的新数组
      - every()：只有每一项都返回true，最终才返回true
      - some()：只要有一项返回true，就返回true
  - arr1.reduce()：归并求值
- Function
  - 每个函数都是 Function 类型的实例，数名实际上也是一个指向函数对象的指针，不会与某个函数绑定
  - ES函数没有重载，后声明的函数会覆盖前面的函数
  - 函数声明和函数表达式的区别
      - 解析器会率先读取函数声明，并使其在执行任何代码之前可以访问；至于函数表达式，必须等到解析器执行到它所在的代码行，才会真正被解释执行。函数声明会被提升，但函数表达式必须声明在前，使用在后
      - 只有这一点区别
  - 函数内部的特殊对象
      - arguments：类数组对象，包含着传入函数中的所有参数，callee属性指向函数自身
      - this：引用指向函数执行的上下文环境
      - caller：保存着调用当前函数的函数的引用，若是在全局作用域中调用当前函数，则为null
    - ES函数是对象，包含2个属性
      - length：函数希望接收的命名参数的个数
      - prototype：保存所有实例方法，用于创建自定义引用类型和实现继承，不可for-in
  - 每个函数都包含两个非继承而来的方法：apply()和 call()
      - 用途都是在特定的作用域中调用函数，实际上等于设置函数体内this对象的值
      - f.apply(this,args)
      - f.call(this,arg1,arg2...)
      - call()方法与apply()方法的作用相同，它们的区别仅在于接收参数的方式不同。使用call()方法时，传递给函数的参数必须逐个列举出来
  - f.bind(obj)：将函数对象f的this绑定到obj
- 基本包装类型
  - 实际上，每当读取一个基本类型值的时候，后台就会创建一个对应的基本包装类型的对象
  - 引用类型与基本包装类型的主要区别就是对象的生存期
      - 使用new操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存
      - 自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁
  - false instanceof Boolean   // false
  - 10 instnceof Number    // false
  - 转型函数Number()
      - 可接受任意类型作为参数，将非数值转换成数值
      - 返回值typeof为number
  - 字符串截取方法区别
      - slice()方法会将传入的负值与字符串的长度相加
      - substr()方法将负的第一个参数加上字符串的长度，而将负的第二个参数转换为0
      - substring()方法会把所有负值参数都转换为0
  - str1.trim()删除前后缀字符串，返回新字符串
- ES内置对象
  - ECMA-262对内置对象的定义是：由ECMAScript实现提供的、不依赖于宿主环境的对象，这些对象在ECMAScript程序执行之前就已经存在了
  - 代表：Object, Array, String, Global, Math
  - 所有在全局作用域中定义的属性和函数，都是Global对象的属性
  - Global
      - encodeURI()不会对本身属于URI的特殊字符进行编码，例如：、/、 ？和#
          - 只有空格被替换为20%
          - 应用于整个URI
      - encodeURIComponent()则会对它发现的任何非标准字符进行编码
          - 一般用得更多，常用于URI后面的参数字符串
      - eval(str1)，在eval()中创建的任何变量或函数都不会被提升
          - 慎用，带来安全问题
      - ECMAScript没有指出如何直接访问Global对象，浏览器都是将这个全局对象作为window对象的一部分加以实现的，因此在全局作用域中声明的所有变量和函数，就都成为了window对象的属性
      - 在没有给函数明确指定this值的情况下，this值等于Global对象
  - Math
      - random()返回0-1之间的随机数
      - 虽然ECMA-262规定了很多方法，但不同实现可能会采用不同的算法，结果精度就不同‘
- 面向对象
  - 每个对象都是基于一个引用类型创建的
  - ECMA-262第5版在定义只有内部才用的特性（attribute）时，描述了属性（property）的各种特征
      - ECMA-262定义这些特性是为了实现JavaScript引擎用的，因此在JavaScript中不能直接访问它们
      - 为了表示特性是内部值，该规范把它们放在了两对方括号中，例如[[Enumerable]]
  - 数据属性：处理数据的读写
      - [[Configurable]]：默认true。表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性
      - [[Enumerable]]：默认true。表示能否通过for-in循环返回属性
      - [[Writable]]：默认true。表示能否修改属性的值
      - [[Value]]：默认undefined。包含这个属性的数据值。读取属性值的时候，从这个位置读；写入属性值的时候，把新值保存在这个位置
      - 要修改属性默认的特性，必须使用ECMAScript 5的 `Object.defineProperty()`
  - 访问器属性：控制如何处理数据
      - [[Configurable]]：默认true。表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为数据属性
      - [[Enumerable]]：默认true。表示能否通过for-in循环返回属性
      - [[Get]]：默认undefined。在读取属性时调用的函数
      - [[Set]]：默认undefined。在写入属性时调用的函数
      - 访问器属性不能直接定义，必须使用 `Object.defineProperty()` 来定义
      - 只指定 getter 意味着属性是不能写，尝试写入属性会被忽略
  - 创建对象的方式
      - 工厂模式
          - 虽然解决了创建多个相似对象的问题，但却没有解决对象识别的问题，即怎样知道一个对象的类型
      - 构造函数模式
          - 构造函数的主要问题，就是每个方法都要在每个实例上重新创建一遍
              - 比较实例的同名方法名是不相等的
              - 若将方法移到构造函数之外，又会增加全局作用域函数的数量
          - 创建自定义的构造函数意味着将来可以将它的实例标识为一种特定的类型
              - 检测对象类型可以使用instanceof
              - 以这种方式定义的构造函数是定义在Global对象中的
      - 原型模式
          - 每个函数都有一个prototype属性，是指针，指向函数的原型对象，不是指向函数
          - 默认情况下，所有原型对象都会自动获得一个constructor属性，这个属性包含一个指向prototype属性所在函数的指针
              - Person.prototype.constructor 指向 Person
              - 原型对象默认只会取得constructor属性，至于其他方法，则都是从Object继承而来的
          - 使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法
          - 当调用构造函数创建一个新实例后，该实例的内部将包含一个指针（内部属性），指向构造函数的原型对象
              - ES5中把这个指针叫 `[[Prototype]]` ，虽然在脚本中没有标准的方式访问[[Prototype]]，但各大浏览器在每个对象上都支持一个属性 `__proto__`
          - Person.prototype.isPrototypeOf(person1)可以用来检测关系
          - obj.hasOwnProperty(pName)检测实例属性，不检测原型属性
          - for-in会遍历原型属性
          - Object.keys(obj)获取对象上所有可枚举的实例属性
          - Object.getOwnPropertyNames(obj)获取所有实例属性，包含constructor
              - 默认情况下的constructor不可枚举
          - 原生引用类型如String,Array,Object都在构造函数原型上定义了方法
          - 问题
              - 省略了为构造函数传递初始化参数，结果所有实例在默认情况下属性值相同
              - 原型中所有属性是被很多实例共享的，对引用类型值的属性进行修改影响太大
      - 组合使用构造函数模式和原型模式
          - 构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性
          - 这是目前在ECMAScript中使用最广泛的一种创建自定义类型的方法
      - 动态原型模式
          - 把所有信息都封装在了构造函数中，而通过在构造函数初始化原型
          - 若再使用对象字面量重写原型影响不可挽回
      - 寄生构造函数模式
          - 创建一个函数，该函数作用仅仅是封装创建对象的代码，然后再返回新创建的对象
              - 使用起来就是将工厂模式的方法名首字母大写
          - 构造函数返回的对象与在构造函数外部创建的对象没有什么不同，因此不能依赖 instanceof操作符来确定对象类型
      - 稳妥构造函数模式
          - 稳妥对象，指的是没有公共属性，而且其方法也不引用this的对象
              - 稳妥对象最适合在一些安全的环境中（环境中会禁止使用this和new），或者在防止数据被其他应用程序改动时使用
          - 稳妥构造函数遵循与寄生构造函数类似的模式，但有两点不同，一是新创建对象的 实例方法不引用this，二是不使用new操作符调用构造函数
          - 稳妥构造函数模式创建的对象与构造函数之间也没有什么关系，因此instanceof操作符对这种对象也没有意义
  - 原型链
      - 原型链是实现继承的主要方法，其基本思想是利用原型让一个引用类型继承另一个引用类型的属性和方法
      - 每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。
          - 如果让原型对象等于另一个类型的实例，结果会怎么样呢？
          - 此时的原型对象将包含一个指向另一个原型的指针，相应地，另一个原型中也包含着一个指向另一个构造函数的指针。
          - 假如另一个原型又是另一个类型的实例，那么上述关系依然成立，如此层层递进，就构成了实例与原型的链条
      - 当以读取模式访问一个实例属性时，首先会在实例中搜索该属性
          - 如果没有找到该属性，则会继续搜索实例的原型
          - 在通过原型链实现继承的情况下，搜索过程就得以沿着原型链继续向上
      - 所有引用类型默认都继承了Object，而这个继承也是通过原型链实现的
          - 所有函数的默认原型都是Object的实例，因此默认原型都会包含一个内部指针，指向Object.prototype
          - 这也正是所有自定义类型都会继 toString()、 valueOf()等默认方法的原因
      - 确定原型和实例的关系: instanceof, isPrototypeOf(obj)
      - 不要用对象字面量来创建原型方法，因为会重写原型链
      - 原型链问题
          - 若原型中包含引用类型属性，该属性会被所有实例共享，会导致修改影响范围过大
          - 在创建子类型的实例时，一般不能向超类型的构造函数中传递参数
    - 组合继承
        - 使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承
        - 最常用的继承模式
        - 组合继承最大的问题就是无论什么情况下，都会调用两次超类型构造函数
            - 一次是在创建子类型原型的时候
            - 另一次是在子类型构造函数内部
            - 子类型最终会包含超类型对象的全部实例属性
        - 示例

``` js
        function SuperType(name) {
          this.name = name;
          this.colors = ["red", "blue", "green"];
        }
        SuperType.prototype.sayName = function() {
          alert(this.name);
        };

        function SubType(name, age) {
          SuperType.call(this, name); //第二次调用SuperType()
          this.age = age;
        }

        SubType.prototype = new SuperType(); //第一次调用SuperType() SubType.prototype.constructor = SubType; SubType.prototype.sayAge = function(){ 
        alert(this.age);
        };
```

    - 原型式继承
        - 借助原型，可以基于已有的对象创建新对象，同时还不必因此创建自定义类型
        - ES5通过新增的 `Object.create()` 方法规范化了原型式继承
        - 包含引用类型值的属性始终都会共享相应的值，就像使用原型模式一样
    - 寄生组合式继承
        - 基本思路是：不必为了指定子类型的原型而调用超类型的构造函数，我们所需要的无非就是超类型原型的一个副本而已
        - 本质就是使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型的原型
        - 基本模式如下

``` js
        function inheritPrototype(subType, superType) {
          var prototype = object(superType.prototype); //创建对象 prototype.constructor = subType;                 //增强对象 subType.prototype = prototype;                   //指定对象 
        }
```

        - 只调用了一次SuperType构造函数
- 创建函数的两种方式
  - 函数声明
      - 示例

``` js
      function functionName(arg0, arg1, arg2) {
        //函数体 
      }
```

      - 浏览器给函数添加了一个非标准的name属性
      - 函数声明提升指在执行代码之前会先读取函数声明，可以把函数声明放在调用语句后面
  - 函数表达式
      - 示例

``` js
      var functionName = function(arg0, arg1, arg2) {
        //函数体 
      };
```

      - 这种情况下创建的函数叫做匿名函数，因为function关键字后面没有标识符
      - 匿名函数的 name 属性是空字符串
      - 函数表达式必须先声明并赋值，再使用，不会提升
- 闭包
  - 闭包是一个函数，它能访问另一个函数作用域中的变量
  - 创建闭包的常见方式，就是在一个函数内部创建另一个函数
  - 在另一个函数F1内部定义的函数F2会将包含函数（即外部函数F1）的活动对象添加到它的作用域链中
  - 闭包只能取得包含函数中任何变量的最后一个值
      - 示例1，返回的都是10

``` js
      function createFunctions() {
        var result = new Array();

        for (var i = 0; i < 10; i++) {
          result[i] = function() {
            return i;
          };
        }

        return result;
      }
```

      - 示例2，返回各自的i

``` 
        function createFunctions(){ 
        var result = new Array(); 

        for (var i=0; i < 10; i++){ 
              result[i] = function(num){ 

                    return function(){ 
                      return num; 
                    }; 

              }(i);  //调用立即执行匿名函数
          }

        return result; 
      }
```

  - this对象是在运行时基于函数的执行环境绑定的
      - 在全局函数中，this等于window
      - 当函数被作为某个对象的方法调用时，this等于那个对象。
      - 匿名函数的执行环境具有全局性，因此其this对象通常指向window
  - 每个函数在被调用时都会自动取得两个特殊变量：this 和 arguments
      - 内部函数在搜索这两个变量时，只会搜索到其活动对象为止，因此永远不可能直接访问外部函数中的这两个变量
      - this和arguments存在同样的问题。如果想访问作用域中的arguments对 象，必须将对该对象的引用保存到另一个闭包能够访问的变量中。
      - 示例1

``` js
      var name = "The Window";
      var object = {
        name: "My Object",
        getNameFunc: function() {
          return function() { //调用getNameFunc会立即调用匿名函数
            return this.name; //this指向由调用函数的执行环境决定
          };
        }
      };

      console.log(object.getNameFunc()()); // The Window
```

      - 示例2

``` js
      var name = "The Window";
      var object = {
        name: "My Object",
        getNameFunc: function() {
          var that = this; // 先将object的this保存
          return function() {
            return that.name;
          };
        }
      };

      console.log(object.getNameFunc()()); // My Object
```

  - 可以基于匿名函数模仿块级作用域
      - 将函数声明包含在一对圆括号中，表示它实际上是一个函数表达式，紧随其后的另一对圆括号会立即调用这个函数
      - 可以减少内存占用，因为没有指向匿名函数的引用，函数执行完毕就会销毁对象
      - 示例

``` js
      (function() {
        //这里是块级作用域 
      })();
```

  - JS中没有私有成员的概念，所有对象属性都是公有的
  - 任何在函数中定义的变量，都可以认为是私有变量，因为不能在函数的外部访问这些变量
  - 私有变量包括函数的参数、局部变量和在函数内部定义的其他函数
  - 可以有权访问私有变量和私有函数的公有方法称为特权方法，创建特权方法有2种方式
      - 在构造函数内部定义所有私有变量和函数，再定义并暴露一个闭包访问这些私有成员
          - 缺点是必须使用构造函数模式来实现
          - 示例

``` js
          function MyObject() {
            //私有变量和私有函数 
            var privateVariable = 10;

            function privateFunction() {
              return false;
            }

            //特权方法 
            this.publicMethod = function() {
              privateVariable++;
              return privateFunction();
            };
          }
```

      - 通过在私有作用域中定义私有变量或函数，同样也可以创建特权方法
          - 在私有作用域中不使用var定义一个构造函数表达式来暴露私有作用域中其他私有成员，利用了变量提升
          - 特权方法作为闭包总是保存着私有作用域的引用
          - 与在构造函数中定义特权方法的主要区别在于私有变量和函数是由实例共享
          - 示例

``` js
          (function() {
              //私有变量和私有函数 
              var privateVariable = 10;

              function privateFunction() {
                return false;
              }

              //构造函数 MyObject = function(){ 
            };

            //公有特权方法 
            MyObject.prototype.publicMethod = function() {
              privateVariable++;
              return privateFunction();
            };
          })();
```

  - js以对象字面量方式创建的对象是单例对象
- BOM
  - BOM提供了很多对象，用于访问浏览器的功能，这些功能与任何网页内容无关
  - BOM的核心对象是 window，它表示浏览器的一个实例
      - 在浏览器中，window对象有双重角色，它既是通过JavaScript访问浏览器窗口的一个接口，又是ECMAScript规定的Global对象
      - 这意味着在网页中定义的任何一个对象、变量和函数，都以window作为其Global对象，因此有权访问parseInt()等全局方法
  - 许多浏览器都会禁用调整浏览器窗口大小的能力，要慎用相关对象对象，如screen对象
- window
  - 所有在全局作用域中声明的变量、函数都会变成window对象的属性和方法
  - 定义全局变量与在window对象上直接定义属性还是有一点差别
      - 全局变量不能通过delete操作符删除，而直接在window对象上的定义的属性可以
  - 如果页面中包含框架frame，则每个框架都拥有自己的window对象，并且保存在frames集合
  - 每个window对象都有一个name属性，标识框架的名称
      - 除非最高层窗口是通过window.open()打开的，否则其window对象的name属性不会包含任何值
  - top对象始终指向最外层的框架，也就是浏览器窗口
  - parent对象始终指向当前框架的直接上层框架
      - 在没有框架的情况下，parent一定等于top，此时它们都等于window
  - self对象始终指向window
  - 对于在一个框架中编写的任何代码来说，其中的window对象指向的都是那个框架的特定实例，而非最外层的框架
  - 在使用框架的情况下，浏览器中会存在多个Global对象
      - 在每个框架中定义的全局变量会自动成为框架中window对象的属性
      - 由于每个window对象都包含原生类型的构造函数，因此每个框架都有一套自己的构造函数，这些构造函数一一对应，但**并不相等**。
      - 例如，top.Object并不等于top.frames[0].Object
      - 这个问题会影响到对跨框架传递的对象使用instanceof操作符
  - window.setTimeOut()第一个参数可以是函数，也可以是字符串，字符串会像eval()执行
      - 不推荐使用字符串，会有性能损耗
      - 第二个参数告诉JavaScript再过多长时间把当前任务添加到队列中
      - `clearTimeout(timeoutId);` 可用来取消
      - 超时调用的代码都是在全局作用域中执行的，因此函数中this的值在非严格模式下指向 window对象，在严格模式下是undefined
  - window.setInterval()接受的参数与setTimeout()相同
      - 在开发环境下，很少使用真正的间歇调用，原因是后一个间歇调用可能会在前一个间歇调用结束之前启动
      - 使用超时调用来模拟间调用的是一种最佳模式
- location
  - `window.location` 和 `document.location` 引用的是同一个对象
  - location对象不仅保存着当前文档的信息，还将URL解析为独立的片段
  - 如果将 location.href 或 window.location 设置为一个URL值，会调用 location.assign("url")方法
  - 最常用的方式是设置 `location.href`
  - 以上改变url的方式都会向浏览器的历史记录添加一条记录，使用 `location.replace()` 就不会
  - location.reload()可能会从缓存重载页面，传入true会强制从服务器重新加载页面
- navigator
  - navigator对象现在已经成为识别客户端浏览器的事实标准
  - registerContentHandler()和 registerProtocolHandler()，可以让一个站点指明它可以处理特定类型的信息
- history
  - 每个浏览器窗口、每个标签页乃至每个框架，都有自己的history对象与特定的window对象关联
  - 出于安全方面的考虑，开发人员无法得知用户浏览过的URL
  - history.go(int)表示向后或向前跳转的页面数的一个整数值
  - history.back(), history.forward()
  - 当页面的URL改变时，就会生成一条历史记录，这里的改变包括URL中hash的变化
- 客户端检测
  - 尽量不要使用客户端检测，只要能找到更通用的方法，就应该优先采用更通用的方法
  - 要尽量使用 typeof 进行能力检测
  - http请求的header部分会包括客户端navigator.userAgent属性的值
  - HTTP规范（包括1.0和1.1版）明确规定，浏览器应该发送简短的用户代理字符串，指明浏览器的名称和版本号
  - 知道呈现引擎和最低限度的版本就足以决定正确的操作方法了，不推荐使用浏览器名称
  - 5大呈现引擎的检测顺序
      - Opera
      - Webkit/Chrome;Safari
      - KHTML/konqueror
      - Gecko/Firefox
      - IE
  - Safari和Chrome的js引擎不同
  - navagator.platform识别运行平台，包括手机和游戏系统
- DOM1级
  - DOM1级定义了一个Node接口，该接口将由DOM中的所有节点类型实现
  - 每个节点都有一个 `nodeType` 属性，节点类型共12类
  - 每个节点都有一个 `childNodes` 属性，其中保存着一个NodeList对象
      - NodeList是一种类数组对象，用于保存一组有序的节点，虽然它有length属性，也能用[]或item()访问元素，但它并不是Array的实例
      - NodeList实际上是基于DOM结构动态执行查询的结果，能自动反映出DOM结构的变化，它不是一张不变的快照，所有length属性可能变化
  - 每个节点都有一个 `parentNode` 属性，该属性指向文档树中的父节点
      - 包含在childNodes列表中的所有节点都具有相同的父节点，因此它们的parentNode属性都指向同一个节点
      - 父节点的 `firstChild` 和 `lastChild` 属性分别指向其childNodes列表中的第一个和最后一个节点
      - 通过使用列表中每个节点的 `previousSibling` 和 `nextSibling` 属性，可以访问同一列表中的其他节点
  - 所有节点都有的最后一个属性是 `ownerDocument` ，该属性指向表示整个文档的文档节点
      - 这种关系表示的是任何节点都属于它所在的文档，任何节点都不能同时存在于两个或更多个文档中
      - 通过这个属性，可以不必在节点层次中通过层层回溯到达顶端，可以直接访问文档节点
  - `appendChild()` 方法用于向childNodes列表的末尾添加一个节点，父子节点关系指针都会相应地得到更新，更新完成后，appendChild()会返回新增的节点
  - 任何DOM节点也不能同时出现在文档中的多个位置上
  - `insertBefore()` 方法接受两个参数：要插入的节点和作为参照的节点
  - `replaceChild()` 方法接受的两个参数是：要插入的节点和要替换的节点
      - 被替换的节点仍然还在文档中，但它在文档中已经没有了自己的位置
  - `removeChild()` 方法接受一个参数，即要移除的节点，被移除的节点将成为方法的返回值
      - 与使用replaceChild()一样，通过removeChild()移除的节点仍然为文档所有，只不过在文档中已经没有了自己的位置
  - `cloneNode()` 方法创建调用这个方法的节点的一个完全相同的副本
      - 传入参数true则深复制，会复制节点及其整个子节点树，否则浅复制只复制节点本身
      - 复制后返回的节点副本属于文档所有，但并没有为它指定父节点，因此这个节点副本就成为了一个孤儿，需要再添加到文档中
      - 此方法不会复制添加到DOM节点中的JavaScript属性，例如事件处理程序等
  - `normalize()` 方法唯一的作用就是处理文档树中的文本节点
      - 如果找到了空文本节点，则删除它
      - 如果找到相邻的文本节点，则将它们合并为一个文本节点
- Document类型
  - 表示HTML页面或者其他基于XML的文档，document对象是HTMLDocument类型的一个实例
  - document.documentElement属性始终指向HTML页面中的 `<html>` 元素
  - document.documentElement、document.firstChild和document.childNodes[0]的值相同，都指向 `<html>` 元素
  - document.body属性直接指向 `<body>` 元素
  - 当页面中包含来自其他子域的框架或内嵌框架时，来自不同子域的页面无法通过 JavaScript通信。而通过将每个页面的document.domain设置为相同的值，这些页面就可以互相访问对方包含的JavaScript对象了
  - 查找元素的方法
      - getElementById()
      - getElementsByTagName()
      - getElementsByName()
  - document.anchors，包含文档中所有带name属性的 `<a>` 元素
  - document.links，包含文档中所有带href属性的 `<a>` 元素
  - document.forms，包含文档中所有的 `<form>元素`
      - 与document.getElementsByTagName("form")得到的结果相同
  - document.images，包含文档中所有的 `<img>` 元素
  - 将输出流写入到网页中的能力
      - document.write()/.writeln()，此方法可以动态地包含外部资源，如js
      - document.open()/close()分别用于打开和关闭网页的输出流
- Element类型
  - 表示XML或HTML元素，提供了对元素标签名、子节点及特性的访问
  - HTMLElement类型直接继承自Element并添加了一些属性，添加的这些属性分别对应于每个 HTML元素中都存在的下列标准特性
      - id, title, lang, dir, className(class)
  - attributes属性中包含一个NamedNodeMap，与NodeList类似，也是一个“动态”的集合
      - attributes对象中的特性，不同浏览器返回的顺序不同
  - document.createElement("div"); 并未立即添加到文档树
      - document.body.appendChild( document.createElement("div") );
- Text类型
  - 可通过nodeValue属性或data属性访问Text节点中包含的文本，这两个属性中包含的值相同
- Comment类型
  - Comment类型与Text类型继承自相同的基类
- CDATASection类型
  - 只针对基于XML的文档，表示的是CDATA区域
- Attr类型
  - 元素的属性在DOM中以Attr类型来表示，属性就是存在于元素的attributes中的节点
  - 不建议直接使用Attr类型，
      - 建议使用getAttribute()、setAttribute()和removeAttribute()
- DOM操作
  - 动态脚本，指的是在页面加载时不存在，但将来的某一时刻通过修改DOM动态添加的脚本
  - 动态样式，加载外部样式文件的过程是异步的，也就是加载样式与执行JavaScript代码的过程没有固定的次序
  - 操作表格，可直接使用行操作和单元格操作API
  - NodeList、NamedNodeMap、HTMLCollection都是动态的集合
      - 每当文档结构发生变化时，它们都会得到更新
      - 应该尽量减少访问NodeList的次数，因为每次访问NodeList，都会运行一次基于文 档的查询
      - 可以考虑将从NodeList中取得的值缓存起来
- Selectors API
  - jQuery的核心就是通过 CSS选择符查询DOM文档取得元素的引用，从而抛开了 `getElementById()` 和 `getElementsByTagName()`
  - Selectors API是由W3C发起制定的一个标准，致力于让浏览器原生支持CSS查询
  - `querySelector()` 方法接收一个CSS选择符，返回与该模式匹配的第一个元素，如果没有找到匹配的元素，返回null
      - CSS选择符可以简单也可以复杂，视情况而定。如果传入了不被支持的选择符，querySelector()会抛出错误
  - `querySelectorAll()` 方法接收的参数与querySelector()方法一样，返回的是所有匹配的元素，返回的是一个NodeList的实例
- HTML5 DOM API
  - (document/element).getElementsByClassName()
      - 返回带有指定类的所有元素的NodeList
      - 传入多个类名时，类名的先后顺序不重要
      - 返回NodeList的方法都要慎用，会有性能损耗
  - Element.classList属性会返回元素的类名，可以方便的对元素的类名进行增删改查
  - document.activeElement属性始终会引用DOM中当前获得了焦点的元素
      - 元素获得焦点的方式有页面加载、用户输入（通常是通过按Tab键）和在代码中调用 focus()方法
      - 默认情况下，文档刚刚加载完成时，document.activeElement中保存的是 document.body 元素的引用
      - 文档加载期间，document.activeElement 的值为 null
  - document.readyState === "loading"/"complete"
  - document.head引用文档的 `<head>` 元素
  - document.charset属性表示文档中实际使用的字符集，默认值为"utf-16"
  - HTML5规定可以为元素添加非标准的属性，但要添加前缀 `data-` ，目的是为元素提供与渲染无关的信息，或者提供语义信息
      - 添加了自定义属性之后，可以通过元素的dataset属性来访问自定义属性的值
      - dataset属性的值是DOMStringMap的一个实例
      - 如果需要给元素添加一些不可见的数据以便进行其他处理，那就要用到自定义数据属性
      - 比如通过自定义数据属性能方便地知道点击来自页面中的哪个部分
  - 为 `innerHTML` 设置HTML字符串后，浏览器会将这个字符串解析为相应的DOM树
      - 因此设置了innerHTML之后，再从中读取HTML字符串，会得到与设置时不一样的结果
      - 原因在于返回的字符串是根据原始HTML字符串创建的DOM树经过序列化之后的结果
      - 通过innerHTML插入 `<script>` 元素并不会执行其中的脚本
      - 并不是所有元素都支持innerHTML属性，不支持的标签包括html,head,style,table
      - `outerHTML` 返回的结果比innerHTML多一个最外层标签
      - 在使用innerHTML、outerHTML属性和insertAdjacentHTML()方法时，最好先手工删除要被替换的元素的所有事件处理程序和JavaScript对象属性，解决内存占用问题
      - 建议现在循环中拼凑HTML字符串，最后使用ele.innerHTML赋值
  - scrollIntoView()可以在所有HTML元素上调用，通过滚动浏览器窗口或某个容器元素，调用元素就可以出现在视口中
      - 若传入true或不传元素顶部会与视口顶部平齐，若false则底部
      - 为某个元素设置焦点也会导致浏览器滚动并显示出获得焦点的元素
- 浏览器开发商的专有扩展
  - 文档模式决定了你可以使用哪个级别的CSS，可以在JavaScript中使用哪些API，以及如何对待文档类型doctype
  - element.children属性与element.childNodes的区别
      - 只包含元素中同样还是元素的子节点
      - 在元素只包含元素子节点时，这两个属性的值相同
  - ele1.contains(ele2)判断节点的父子关系
  - ele.innerText可以操作元素中包括子节点的所有文本内容
- DOM2级
  - DOM1级主要定义的是HTML和XML文档的底层结构，DOM2和DOM3级则在这个结构的基础上引入了更多的交互能力，也支持了更高级的XML特性
  - DOM2级模块：Core, Views, Events, Style, HTML, Traversal
  - DOM3级模块：XPath, Load&Save
  - 任何支持style属性的HTML元素在JavaScript中都有一个对应的style属性对象，只包含内联样式指定的样式信息，不包含外部样式表或内部样式表层叠而来的样式信息，js属性名将对应的css样式名称转换成camelCase
  - CSSStyleSheet类型表示样式表，包括通过 `<link>` 元素包含的样式表和在 `<style>` 元素中定义的样式表
      - 这两个元素本身分别由 HTMLLinkElement 和 HTMLStyleElement 类型表示的
      - 但是CSSStyleSheet类型相对更加通用一些，它只表示样式表，而不管这些样式表在 HTML中是如何定义的。
      - 上述两个针对元素的类型允许修改HTML特性，但CSSStyleSheet对象则是一套只读的接口
  - document.styleSheets集合包括文档的所有样式表
  - NodeIterator和TreeWalker这两个类型能够基于给定的起点对DOM结构执行深度优先的遍历操作
  - 通过Range范围可以选择文档中的一个区域，而不必考虑节点的界限
- Events
  - js和html直接的交互通过事件来实现
  - 事件流描述的是从页面中接收事件的顺序
      - IE的事件流是事件冒泡流，而Netscape的事件流是事件捕获流
  - 事件冒泡（event bubbling）（推荐使用）
      - 事件开始时由最具体的元素（文档中嵌套层次最深的那个节点）接收，然后逐级向上传播到较为不具体的节点（文档）
  - 事件捕获（event capturing）
      - 不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件
      - 由于老版本的浏览器不支持，因此很少有人使用事件捕获
  - DOM2级事件规定的事件流包括三个阶段：事件捕获阶段、处于目标阶段和事件冒泡阶段
      - 首先发生的是事件捕获，为截获事件提供了机会
      - 然后是实际的目标接收到事件
      - 最后一个阶段是冒泡阶段，可以在这个阶段对事件做出响应
  - DOM3级规定的事件类型
      - ui
      - focus
      - mouse
      - keyboard
      - composition
      - mutation of DOM
      - html5
      - device
      - touch & gesture
- Form
  - HTMLFormElement 继承了 HTMLElement
  - 每个表单字段都有的属性(fieldset除外)
      - disabled
      - form
      - name
      - readOnly
      - tabIndex
      - type
      - vaule
  - 每个表单字段都有的方法
      - focus()
      - blur()
  - 每个表单字段支持的事件
      - focus
      - blur
      - change
          - 对于 `<input>` 和 `<textarea>` 元素，当它们从获得焦点到失去焦点且value 值改变时，才会触发change事件
          - 对于 `<select>` 元素，只要用户选择了不同的选项，就会触发change事件，换句话说，不失去焦点也会触发change事件
          - 在某些浏览器中，blur事件会先于change事件发生，而在其他浏览器中则相反
- Canvas
  - `<canvas>` 元素在页面中设定一个区域，然后就可以通过js动态地在这个区域中绘制图形
  - 除了具备基本绘图能力的2D上下文，canvas还建议了一个名为WebGL的3D上下文
  - 要使用 `<canvas>` 元素，必须先设置其 width 和 height 
  - 使用 `toDataURL()` 方法，可以导出在 `<canvas>` 元素上绘制的图像，默认导出png
  - 矩形是唯一一种可以直接在2D上下文中绘制的形状
  - 2D绘制上下文支持很多在画布上绘制路径的方法，通过路径可以创造出复杂的形状和线条
  - 2D绘图上下文也提供了绘制文本的方法：fillText() 和 strokeText()，前者用得多
  - 2D绘制上下文支持各种基本的绘制变换
      - scale(scaleX,scaleY)
      - translate(x,y)
      - rotate(angle)
      - transform(m1_1, m1_2, m2_1, m2_2, dx, dy)：直接修改变换矩阵
  - 2D绘图上下文内置了对图像的支持drawImage()
  - 2D上下文会根据属性值自动为形状或路径绘制出阴影
  - 2D上下文提供了 `getImageData()` 取得原始图像数据
      - 返回的对象是 `ImageData` 的实例，每个实例都有：width、height 和 data
      - data属性是一个数组，保存着图像中每一个像素的数据
      - 在data数组中，每一个像素用4个元素来保存，分别表示红、绿、蓝和透明度值
- WebGL
  - GLSL
  - 着色器程序
- 拖放
  - 被拖动元素发生：dragstart > drag > dragend
  - 放置目标会发生：dragenter > dragover > dragleave/drop
  - dataTransfer对象是event对象属性，用于从被拖动元素向放置目标传递字符串格式的数据
  - dropEffect 属性只有搭配 effectAllowed 属性才有用
  - 必须在 ondragstart 事件处理程序中设置 effectAllowed 属性
  - 默认情况下，图像、链接和文本是可以拖动的
      - 文本只有在被选中的情况下才能拖动，而图像和链接在任何时候都可以拖动
  - HTML5为所有HTML元素规定了一个 `draggable` 属性，表示元素是否可以拖动

## js-guide-google

- 字符串优先使用单引号，方便包含html属性中的双引号
- 声明常量要使用大写字符, 并用下划线分隔，不用简单地只使用const，IE不支持const
- 总是使用分号，便于区分语句
- 不要在块内声明一个函数
  - ECMAScript只允许在脚本的根语句或函数中声明函数，部分浏览器支持块内
  - 如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量
  - 示例

``` js
  if (x) {
    var foo = function() {}
  }
```

- 不要使用封装类型，如new Boolean()
- 小心使用闭包，闭包保留了一个指向它封闭作用域的指针, 所以在给DOM元素附加闭包时, 很可能会产生循环引用, 进一步导致内存泄漏
- eval()只用于解析序列化串，如解析RPC响应，最好不要使用eval
  - 解析序列化串是指将字节流转换成内存中的数据结构
- with(){}让你的代码在语义上变得不清晰，不要用
- this仅在对象构造器, 方法, 闭包中使用，易出错
- for-in只用于 object/map/hash 的遍历，对Array的遍历用for-in会出现不按顺序遍历
- 不要修改内置对象如 Object.prototype 和 Array.prototype 的原型

## js-guide-es6-airbnb

- 对所有引用类型使用const
- 数组
  - 创建数组尽量使用[]，少用new Array()
  - 向数组添加元素时使用 Array.push()，替代直接赋值
  - 复制数组用扩展运算符...
  - 把一个类数组对象转换成数组用Array.from()
- 需要回传多个值时，使用对象解构，而不是数组解构
- 函数
  - **使用函数声明**代替函数表达式，因为函数声明是可命名的，在调用栈中更容易被识别
  - 不要使用arguments，可以选择rest语法... 替代，rest能明确你要传入的参数，arguments只是一个类数组
  - 当你必须使用函数表达式（或传递一个匿名函数）时，使用箭头函数符号
  - 尽量不要用构造函数，用class
  - extends是一个内建的原型继承方法并且不会破坏instanceof
  - 匿名函数表达式的变量名会被提升，但函数内容并不会
  - 命名的函数表达式的变量名会被提升，但函数名和函数函数内容并不会
  - 函数声明的名称和函数体都会被提升
- Iterator  
  - 不要使用iterators，使用高阶函数例如map()和reduce()代替for-of，处理纯函数的回调值更易读，这比它带来的副作用更重要
