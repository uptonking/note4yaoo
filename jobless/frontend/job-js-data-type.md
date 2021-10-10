---
title: job-js-data-type
tags: [data-type, frontend, job, js]
created: '2021-10-10T09:06:56.283Z'
modified: '2021-10-10T09:31:00.229Z'
---

# job-js-data-type

# guide

## js数据类型

- JavaScript 中有八（7+1）种基本的数据类型（七种基本数据类型，也称为原始类型，object 为复杂数据类型）
  - string：用于字符串
  - number：用于整数或浮点数，在 ±(2^53-1) 范围内的整数
  - boolean：用于 true 和 false
  - null：只有一个 null 值的独立类型
  - undefined：只有一个 undefined 值的独立类型
  - bigInt：用于任意长度的整数
  - symbol：用于唯一的标识符
  - object：用于更复杂的数据结构

## 类型转换

```JS
String(null); // 'null'
String(undefined); // 'undefined'
String(1e21); // '1e+21'
String([null]); // ''
String([1, undefined, 3]); // '1,,3'
String([]); // ''
String({}); // '[object Object]'

Number(null); // 0
Number(undefined); // NaN
Number("10a"); // NaN
Number(""); // 0
Number(true); // 1
Number(false); // 0
Number(["1"]); // 1
Number([]); // 0
Number({}); // NaN

Boolean(Infinity); // true

[] == [] //false： 类型相同， 但是堆上不同对象， false
[] == ![] // true： 右侧由 false 转为 0， 左侧 toPrimitive() 转为 0
[] == 0 // true： 同上 
  [] == "" // true： 左侧 toPrimitive() 转为 "" 和右侧相等
```

## string

- 字符串字面量 (通过单引号或双引号定义) 和 直接调用 String 方法(没有通过 new 生成字符串对象实例)的字符串都是基本字符串
  - 当基本字符串需要调用一个字符串对象才有的方法或者查询值的时候(基本字符串是没有这些方法的)，JS会自动将基本字符串转化为字符串对象并且调用相应的方法或者执行查询

- 字符串可以使用类似数组索引下标的方式来访问字符元素
  - 如 aa = 'string'; aa[1] === 't'

- `substr(start, length)` vs `slice(beginIndex, endIndex)` 提取字符串片段
  - 👀️ 第2个参数是不同的

### [ `string.charAt(x)` or `string[x]` ](https://stackoverflow.com/questions/5943726)

- There is a difference when you try to access an index which is out of bounds or not an integer.
  - `string[x]` returns the character at the xth position in string if x is an integer between 0 and string.length-1, and returns `undefined` otherwise.
  - `string.charAt(x)` converts x to an integer and then returns the character at the that position if the integer is between 0 and string.length-1, and returns an empty string `''` otherwise.
- Word of caution: using either syntax for emojis or any other unicode characters past the Basic Multilingual Plane BPM (AKA the "Astral Plane") "😃".charAt(0) will return an unusable character
  - using either syntax for emojis will return an unusable character
  - That’s why Array.from("😃")[0] or [..."😃"][0] should be used in this case. 

```JS
// They can give different results in edge cases.
'hello' [NaN] // undefined
'hello'.charAt(NaN) // 'h'

'hello' [true] //undefined
'hello'.charAt(true) // 'e'
```

## number

```JS
NaN === NaN // false; 但作为Map的key时是被认为相等的
```

## 数字处理

- JS 的 Number 类型遵循的是 IEEE 754 标准，使用的是 64 位固定长度来表示
- 0.1 转换为 IEEE 754 标准，转换过程主要经历 3 个过程：
  - 将 0.1 转换为二进制表示：乘2取整，自上而下，得到0.00011
  - 将转换后的二进制通过科学计数法表示：0.00011=1.1001*10-4
  - 将通过科学计数法表示的二进制转换为 IEEE 754 标准表示
    - 求阶码
    - 求尾数
- 0.1+0.2 计算结果不等于0.3，而是 0.30000000000000004
  - 解决方法：
  - 放大，先各放大100倍，求和后除以100
  - 使用 Number. EPSILON，小于该值的即认为是机器误差，可认为结果正确

```JS
function numbersequal(a, b) {
  return Math.abs(a - b) < Number.EPSILON;
}

var a = 0.1 + 0.2， b = 0.3;
console.log(numbersequal(a, b)); //true
```

- 基于 IEEE754 的 JS 能够安全存储的整数范围在 (-2^53, 2^53)之间。
  - 后端返回的数据一般都是 JSON 格式的字符串，当其中的超过区间的字符串数字经过 JSON.parse() 转换为数字后可能出错
- 以前需要使用外部库，如 JSON-bigint，现在可以使原生 bigInt 类型，借助 JSON.parse() 的 reviver 函数，判断在不安全值时转换为 bigInt 值，注意使用 reviver 后需要针对所有值都有返回值

```JS
console.log(
  JSON.parse(
    '{ "id": 9007199254740995, "name": "Jack", "age": 18 }',
    (k, v) => {
      if (typeof v == "number" && !Number.isSafeInteger(v)) return BigInt(v);
      else return v;
    }
  )
);
```

## Object 对象

- 从对象中删除属性的方法
  - const {prop, ...newObj} = obj; 
  - delete obj['prop']
  - Reflect.deleteProperty(myJSONObject, 'regex'); 
  - The difference between `delete` and `deleteProperty` is when using strict mode

- 对象属性的特征
  - [[Configurable]]：属性是否可通过 delete 删除并重新定义，默认 true
  - [[Enumerable]]：属性是否可通过 for-in 或 Object.keys() 枚举，默认 true
  - [[Writable]]：属性是否可被修改，默认 true
  - [[Value]]：属性值，默认 undefined
- Object.keys()返回一个由一个给定对象的自身可枚举属性组成的数组
  - 作为对比 for-in 循环则会遍历对象自身+其原型链上可枚举属性，每次获取的索引都是字符串类型
- `Object.freeze()` 不可加、不可删、不可改
  - 冻结对象，使其不能被修改（冻结一层）
  - 不能新增、删除、修改属性
  - 对象 [[prototype]] 不可修改
- `Object.seal()` 不可加、不可删、可改
  - 不能新增属性
  - 现有属性标记为不可配置，即不可删除
  - 已有可写属性可以修改
  - 对象 [[prototype]] 不可修改
- Object.preventExtensions() 不可加、可删、不可改
  - 不能新增属性
  - 可删除已有属性
  - 对象 [[prototype]] 不可修改
  - 其余属性都可修改
- 从限制的严格性来说：Object.preventExtensions() [不可增，可删可改] < Object.seal() [不可增不可删，可改] < Object.freeze() [不可增不可删不可改] 

## array

- 扁平化
  - reduce，递归
  - map，递归
  - 基于队列，非递归

- 判断Array类型
  - Array.isArray(arr)
  - arr.constructor === Array
  - arr instanceof Array

- 数组去重
  - [... new Set(arr)]

- 创建数组的方法
  - 二维数组 Array(m).fill(Array(n)); 

- indexOf vs includes
  - [NaN].indexOf(NaN) // -1，因为indexOf使用的是严格相等
  - NaN].includes(NaN) // true

- indexOf vs findIndex
  - indexOf() expects a value
  - findIndex() expects a callback; good for objects

- 从数组中删除元素
  - immutable： arr.filter( item => item!==target)
  - arr.splice(arr.indexOf(target), 1)
  - delete arr[ arr.indexOf(target) ]
  - 还可以考虑直接赋值覆盖 arr[index] = undefined
- 从数组中删除多个元素
  - arr.filter( item => !targets.includes(item))

- 不要再forEach里面return，因为forEach循环无法终止

- [`Array()` vs `new Array()` 创建新数组](https://stackoverflow.com/questions/8205691)
  - Thus the function call `Array(…)` is equivalent to the object creation expression `new Array(…)` with the same arguments.
  - Array === Array.prototype.constructor //true
  - 调用Array构造函数带不带new结构都想同，但调用普通的构造函数带不带new却是不同的

### `concat vs ...rest` ([...arr1, ...arr2] vs arr1.concat(arr2))

- concat不会改变arr1和arr2，返回的也是新数组，a new Array instance.
- 最大的区别是rest操作符可读性好，测试leetcode快排算法时结尾用展开语法更快
- rest还能展开字符串、对象等
- the only honest answer is that "it depends". 
  - Browsers change all the time
- concat will preserve the empty slots in the array while the Spread will replace them with undefined values.

- 虽然concat保留了空位置，但比较起来却是相等的，都等于`undefined`

```JS
var x = [],
  y = [];

x[1] = "a";
y[1] = "b";

var usingSpread = [...x, ...y];
var usingConcat = x.concat(y);

console.log(usingSpread); // [ undefined, "a", undefined, "b"]
console.log(usingConcat); // [ empty, "a",empty , "b"] 

console.log(1 in usingSpread); // true
console.log(1 in usingConcat); // true

usingSpread[0] === usingConcat[0] // true
usingConcat[0] === undefined // true
```

- 在常见使用场景中，concat不会修改数组
  - arr1.push(...arr2)使用rest经常需要修改已有数组

```JS
const arr1 = ["dog", "cat", "hamster"];
const arr2 = ["bird", "snake"];

arr1.push(arr2);
arr1 // ['dog', 'cat', 'hamster', Array(2)]

arr1.push.apply(arr1, arr2);
arr1 // ['dog', 'cat', 'hamster', 'bird', 'snake']

// When we invoke the function, we pass it all the values in the array using the spread syntax 
arr1.push(...arr2); // ['dog', 'cat', 'hamster', 'bird', 'snake']
```

- Spread syntax is not an operator and therefore does not have a precedence.
  - It is part of the array literal and function call (and object literal) syntax.
  - Similarly, rest syntax is part of the array destructuring and function parameter (and object destructuring) syntax.

- [Array.prototype.push.apply](https://stackoverflow.com/questions/35638511)
- `arr1.push.apply(arr1, arr2); `的计算逻辑
  - `arr1.push === Array.prototype.push` // true
  - Function.prototype.apply(thisArg, argsArray)，apply的第2个参数会自动展开然后传递给函数  
  - When you use `apply()`, it will take the array that you have supplied as the second argument and convert it to multiple arguments.
- [Difference between using a spread syntax (...) and push.apply](https://stackoverflow.com/questions/39716216)
- Both `Function.prototype.apply` and the `...` spread syntax may cause a stack overflow when applied to large arrays
  - `apply: Maximum call stack size exceeded` 异常信息
  - 因为 JavaScriptCore engine 引擎限制了函数参数列表的长度为65536，但是chrome的v8引擎测试表明支持参数数量大于65536
  - Use `Array.prototype.concat` instead. Besides avoiding stack overflows,  `concat` has the advantage that it also avoids mutations. Mutations are considered harmful, because they can lead to subtle side effects.
  - But that isn't a dogma(教条). If you are within a function scope and perform mutations to improve performance and relieve garbage collection you can perform mutations, as long as they aren't visible in the parent scope.

- [Does spread operator affect performance?](https://stackoverflow.com/questions/55843097)
  - Yes, spreading a variable which refers to an object into another object requires the interpreter to look up what the variable refers to, and then look up all the enumerable own properties (and the associated values) of the object that gets spreaded so as to insert into the new object. 
  - But, on modern computers, and on modern JS engines, the processing power required is next to nothing; 
- beware of using spread with an `array.reduce()`. I suspect it leads to O(n^2) behavior or worse.

```JS
let phoneBook = inputs.reduce((acc, entry) => {
  let [name, phone] = entry.trim().split(' ');

  // ! 不要用展开运算符，返回的是在循环内创建的新对象
  return { ...acc, [name]: phone };
}, {});

let phoneBook = inputs.reduce((acc, entry) => {
  let [name, phone] = entry.trim().split(' ');

  // 返回的是同一个acc对象
  acc[name] = phone;

  return acc;
}, {});
```

- [spread operator vs array.concat()](https://stackoverflow.com/questions/48865710)
- To sum it up, when your arguments are possibly non-arrays, the choice between concat and ... depends on whether you want them to be iterated.
  - `concat` makes no attempt to iterate the generator and appends it as a whole, while `...` nicely fetches all values from it.
  - ES6 provides a way to override it with `Symbol.isConcatSpreadable`; 
- Performance-wise `concat` is faster, probably because it can benefit from array-specific optimizations, while `...` has to conform to the common iteration protocol. 

## Map vs Object

- 区别
  - Map对象默认不包含键值对
    - Object原型对象上的默认属性会添加到普通对象上
    - 但Object.create(null)也可以实现类似Map的效果
  - Map的key的类型可以是任意类型，包括对象、函数、symbol、数字
    - Object的key必须是String或Symbol
  - Map对象的keys会保持插入顺序
    - Object的keys的顺序以前没有在规范中规定保持插入顺序
    - obj的遍历机制很复杂
    - `for-in` includes only enumerable string-keyed properties，还会遍历原型对象上的kv
    - `Object.keys` includes only own, enumerable, string-keyed properties; 这里不包含原型对象上的kv
    - `Object.getOwnPropertyNames` includes own, string-keyed properties even if non-enumerable;
  - Map对象的size很容易获得
    - 获取Object的属性数量必须遍历和过滤
  - Map默认实现了 iterator protocol 
    - Object需要自己实现 Object.keys/entries
    - for-in可遍历obj及其原型链上的可迭代属性，会忽略Symbol，
  - Map在插入、删除操作较多时性能较好
    - Object没有针对插入删除进行优化
  - Map序列化默认会丢失所有内容，总是{}
    - Object对象默认提供了序列化和反序列化的方法，但有限制

- for-in遍历
  - only iterates over enumerable, non-Symbol properties.
  - 可遍历原型对象上的属性
  - for...in loop iterates over the properties of an object in an arbitrary order 
    - 而数组的遍历一般按索引顺序，所以最好不要使用for-in遍历数组
  - for-in遍历数组会遍历手动添加的属性
  - for-in为遍历对象而设计

- [es6 Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
- holds key-value pairs and remembers the original insertion order of the keys
- Key equality is based on the sameValueZero algorithm.

- Object只能使用数值、字符串或符号作为键，且会被转换为字符串，
  - Map可使用任何数据类型作为key，且保持该类型
- Map实例会维护键值对的插入顺序，因此可以根据插入顺序执行迭代操作
- Weak主要形容弱映射中的key是弱的——GC随时会回收弱映射的key，但是只要key存在，value就不会被回收

- Object.isSealed
  - 让这个对象变的不能添加新属性，且所有已有属性会变的不可配置。属性不可配置的效果就是属性变的不可删除，以及一个数据属性不能被重新定义成为访问器属性
  - 但属性的值仍然可以修改。
- Object.isFrozen
  - 属性不能被修改。

## Map/Set

- Map会记住kv的插入顺序

```JS
mm = new Map()
mm.set('a', 'aa')
mm.set('b', 'bb')
mm.keys(); // a,b

mm.set('a', 'aa11')
mm.keys() // a,b  💡️ 更新已有key时，插入顺序不变，a不会在最后
```

- 弱引用与强引用相对，是指不能确保其引用的对象不会被垃圾回收器回收的引用。 
  - 一个对象若只被弱引用所引用，则被认为是不可访问（或弱可访问）的，并因此可能在任何时刻被回收。
  - 我们默认创建一个对象：const obj = {}，就默认创建了一个强引用的对象，我们只有手动将obj = null，它才会被垃圾回收机制进行回收，如果是弱引用对象，垃圾回收机制会自动帮我们回收。
  - weakMap.set(obj, 'i can be auto recycled'); 
  - obj = null; 
  - weakMap和obj是弱引用关系，当obj断开时，obj对应的val会被自动回收

- WeakSet与Set的区别
  - 成员都是对象
  - 成员都是弱引用，可以被垃圾回收机制回收，可以用来保存 DOM 节点，不容易造成内存泄漏
  - 不能遍历；而Set可遍历

- WeakMap
  - 只接受对象最为键（null除外），不接受其他类型的值作为键
  - 不能遍历，没有keys()/entries()等方法
  - 没有size属性，没有clear()方法
  - 键名是弱引用，键值可以是任意的，键名所指向的对象可以被垃圾回收，此时键名是无效的；

- WeakSet 的成员只能是对象，而不能是其他类型的值。WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用
- WeakMap只接受对象作为键名（ null 除外），不接受其他类型的值作为键名。Weak 主要形容弱映射中的 key 是弱的——GC随时会回收弱映射的key 指向对象，但是只要 key 存在，value 就不会被回收

- [从【垃圾回收机制】的角度认识【Map与WeakMap】的区别](https://zhuanlan.zhihu.com/p/266054976)
- JavaScript最常用垃圾回收策略是"标记清理（mark-and-sweep）"
  - 遍历空间下所有的对象，并标记活着的，有被引用的并且最终可以到达根（window/global）的对象。
  - 在垃圾回收阶段的时候，将没有标记进行清除。
- 当WeakMap对象的key键所对应引用地址的 **key引用断开**或**key引用指向的地址内容发生变化**
  - 引用断开，WeakMap表现出“自动”删掉了对应value
- 所以weakMap也还是遵循垃圾回收机制对吗？栏主有没有试过多个引用指向weakMap的key，将一个引用断开，weakMap的键值是否还在内存中？
  - 只要Key的引用还在当前空间的时候，这个键值就还在。
  - 不管“复制”多少份key，只要他们引用还存在变量里面，那么垃圾回收机制并不会收回他们
- 你上面的例子 因为变量注册在最外层，不会被垃圾回收机制自动回收 所以会有用，在函数体内函数上下文执行了一般会自动释放，所以使用Map 和 WeakMap ，并没什么区别

```JS
const wm = new WeakMap();
// 给 WeakMap实例 赋值一个 占领内存足够大的 键值对
wm.set(key, new Array(114514 * 19));
global.gc();

// 此时把 key键 的引用进行断开，并观察内存占用情况
key = null;
// key = new Array(); 
global.gc();
```

- ES2021 推出了 WeakRef ，能实现保留对另一个对象的弱引用，而不会阻止该弱引用对象被GC回收

## valueOf vs toString (+号运算符) 类似java的自动拆箱装箱/隐式类型转换

### [Object.prototype.valueOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)

- returns the primitive value of the specified object.
- JavaScript automatically invokes it when encountering an object where a primitive value is expected.
- If an object has no primitive value,  `valueOf` returns the object itself.
- A (unary) plus sign can sometimes be used as a shorthand for `valueOf`, e.g. in `+new Number()`.

- The unary plus operator (`+`) precedes its operand and evaluates to its operand but attempts to convert it into a number, if it isn't already.
  - Although unary negation (`-`) also can convert non-numbers, unary plus is the fastest and preferred way of converting something into a number

```typescript
{}.valueOf(); // Uncaught SyntaxError: Unexpected token '.'
let aa = {};
aa.valueOf(); // {}
[].valueOf(); // []

// 单个+号默认是获取数值类型的原始值

+"5" // 5 (string to number)
+"" // 0 (string to number)
+"1 + 2" // NaN (doesn't evaluate)
+new Date() // same as (new Date()).getTime()
+"foo" // NaN (string to number)
+{} // NaN
+[] // 0 (toString() returns an empty string list)
+[1] // 1
+[1,2] // NaN
+new Set([1]) // NaN
+BigInt(1) // Uncaught TypeError: Cannot convert a BigInt value to a number
+undefined // NaN
+null // 0
+true // 1
+false // 0
```

### [Object.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

- returns a string representing the object.
- toString() method that is automatically called when the object is to be represented as a text value or when an object is referred to in a manner in which a string is expected.
- If this method is not overridden in a custom object, toString() returns "[object type]", where type is the object type.

```typescript

// {}.toString()  // Uncaught SyntaxError: Unexpected token '.'
let aa = {};
aa.toString(); // [object Object]
[].toString(); // '' 空字符串
[1,2].toString(); // 1,2 数组转字符串默认没有方括号
null.toString(); // Uncaught TypeError: Cannot read properties of null
null+''; // null
undefined.toString(); // Uncaught TypeError: Cannot read properties of undefined
undefined+''; //undefined

Number(); // 0
Number(''); // 0

({valueOf: () => 1, toString: () => "f"})+""    // "1" 
`${({valueOf: () => 1, toString: () => "f"})}`  // "f"

'a' === String('a')      // true
'a' === new String('a')  // false
```

### [obj.toString() vs String(obj)](https://stackoverflow.com/questions/3945202)

- `value.toString()` will cause an error if value is `null` or `undefined`. 
  - `String(value)` should not.
- The `String` constructor called as a function would be roughly equivalent to: `value +''; `

- when converting from Object-to-String, the following steps are taken:
  - If available, execute the `toString` method.
    - If the result is a primitive, return result, else go to Step 2.
  - If available, execute the `valueOf` method.
    - If the result is a primitive, return result, else go to Step 3.
  - Throw `TypeError`.

### The addition operator ( `+` ) 自动类型转换

- produces the sum of numeric operands or string concatenation.

```JS
var x = {
  toString: function() { return "foo"; },
  valueOf: function() { return 42; }
};
console.log("x=" + x); // x=42
console.log("x=" + x.toString()); // x=foo

Symbol("foo").toString() // Symbol(foo)
String(Symbol("foo")) // Symbol(foo)
Symbol("foo") + "" // Uncaught TypeError: Cannot convert a Symbol value to a string
`${Symbol("foo")}` // Uncaught TypeError: Cannot convert a Symbol value to a string
```

- Type coercion(强迫), or implicit type conversion, enables weak typing and is used throughout JavaScript. 
  - Most operators (with the notable exception of the strict equality operators `===` and `!==`), and value checking operations (eg. if(value)...), will coerce values supplied to them, if the types of those values are not immediately compatible with the operation.
  - The precise mechanism used to coerce a value depends on the expression being evaluated.
- The **addition(`+`) operator will first ensure both operands are primitives**, which, in this case, involves calling the `valueOf` method.
  - 遇到+号运算符，会先将两边操作数转为原生类型，自动调用ToPrimitive，若不给hint，默认先调用valueOf()，若返回值不为原生类型，再调用toString()
  - The `toString` method is not called in this example because the overridden `valueOf` method on object `x` returns a primitive value. 
  - Then, because one of the operands in the question is a string, both operands are converted to strings. This process uses the abstract, internal operation `ToString` (note: capitalized), and is distinct from the `toString` method on the object (or its prototype chain).

- The purpose of `valueOf` is to retrieve the primitive value associated with an object (if it has one). 
  - If an object does not have an underlying primitive value, then the object is simply returned.
- If `valueOf` is invoked against a primitive, then the primitive is auto-boxed in the normal way, and the underlying primitive value returned. 
  - Note that for strings, the underlying primitive value (ie. the value returned by `valueOf`) is the string representation itself.
- For most operations, JavaScript will silently attempt to convert one or more operand(s) to the required type. 
  - This kind of implicit type conversion is called type coercion, and it is the basis of JavaScript's loose (weak) type system.
  - The complicated rules behind this behavior are intended to move the complexity of typecasting into the language itself, and out of your code.
- **When attempting to convert non-primitive types to primitives to be operated upon, the abstract operation `ToPrimitive` is called** with an optional "hint" of 'number', or 'string'. 
  - If the hint is omitted, the default hint is 'number' (unless the `@@toPrimitive` method has been overridden). 
  - If the hint is 'string', then `toString` is tried first, and `valueOf` second if `toString` did not return a primitive. Else, vice-versa. 
- The hint depends on the operation requesting the conversion.
  - The addition(`+`) operator supplies no hint, so `valueOf` is tried first. 
  - The subtraction(`-`) operator supplies a hint of 'number', so `valueOf` is tried first. 
  - The only situations I can find in the spec in which the hint is 'string' are: `Object#toString` or `ToPropertyKey`
- **The addition operator will first use `ToPrimitive` to ensure each operand is a primitive**; 
  - then, if either operand is a string, it will then deliberately invoke the abstract operation `ToString` on each operand, to deliver the string concatenation behavior we expect with strings. 
  - If, after the `ToPrimitive` step, both operands are not strings, then arithmetic addition is performed.
- Unlike addition, the subtraction operator does not have overloaded behavior, and so will invoke `toNumeric` on each operand having first converted them to primitives using `ToPrimitive`

```typescript
 1  +  1   //  2 
'1' +  1   // '11'   Both already primitives, RHS converted to string, '1' + '1',   '11'
 1  + [2]  // '12'   [2].valueOf() returns an object, so `toString` fallback is used, 1 + String([2]), '1' + '2', 12
 1  + {}   // '1[object Object]'    {}.valueOf() is not a primitive, so toString fallback used, String(1) + String({}), '1' + '[object Object]', '1[object Object]'
 2  - {}   // NaN    {}.valueOf() is not a primitive, so toString fallback used => 2 - Number('[object Object]'), NaN
+'a'       // NaN    `ToPrimitive` passed 'number' hint), Number('a'), NaN
+''        // 0      `ToPrimitive` passed 'number' hint), Number(''), 0
+'-1'      // -1     `ToPrimitive` passed 'number' hint), Number('-1'), -1
+{}        // NaN    `ToPrimitive` passed 'number' hint', `valueOf` returns an object, so falls back to `toString`, Number('[Object object]'), NaN
 1 + 'a'   // '1a'    Both are primitives, one is a string, String(1) + 'a'
 1 + {}    // '1[object Object]'    One primitive, one object, `ToPrimitive` passed no hint, meaning conversion to string will occur, one of the operands is now a string, String(1) + String({}), `1[object Object]`
 1 - 'a'   // NaN    Both are primitives, one is a string, `ToPrimitive` passed 'number' hint, 1-Number('a'), 1-NaN, NaN
 1 - {}    // NaN    One primitive, one is an object, `ToPrimitive` passed 'number' hint, `valueOf` returns object, so falls back to `toString`, 1-Number([object Object]), 1-NaN, NaN
[] + []    // ''     Two objects, `ToPrimitive` passed no hint, String([]) + String([]), '' (empty string)
[] - []    // 0      Two objects, `ToPrimitive` passed 'number' hint => `valueOf` returns array instance, so falls back to `toString`, Number('')-Number(''), 0-0, 0

let date = new Date();
date.valueOf(); // 1632449848133
date.toString(); // 'Fri Sep 24 2021 14:34:47 GMT+0800 (China Standard Time)'
date + ''; // 'Fri Sep 24 2021 14:34:47 GMT+0800 (China Standard Time)'

```

- Note that the `Date` intrinsic object is unique, in that it is the only intrinsic to override the default `@@toPrimitive` method, in which the default hint is presumed to be 'string' (rather than 'number').
  - The reason for having this, is to have Date instances translate to readable strings by default
