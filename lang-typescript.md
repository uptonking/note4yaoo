---
tags: [lang/typescript]
title: lang-typescript
created: '2019-08-26T15:07:33.910Z'
modified: '2020-07-07T08:10:51.705Z'
---

# lang-typescript

## tips

- ts vs flow
  - ts特性 > flow静态类型检查 + ES6新语法 + vscode支持

## dev-log

- 使用is操作符而不用boolean，可以帮助编译器进一步进行类型检查
  - https://stackoverflow.com/questions/40081332/what-does-the-is-keyword-do-in-typescript
  - TypeScript will narrow the type to string in any block guarded by a call to the function. 

## faq

- typescript generic type with equal operator means?
  - TypeScript 2.3 adds support for declaring defaults for generic type parameters.
    - https://github.com/Microsoft/TypeScript/wiki/What's-new-in-TypeScript#generic-parameter-defaults
  - 使用泛型定义的接口或类时，若不提供具体实现类，则使用=等号设置的默认类型，如any
- type vs interface
  - type特有
    - Type Alias不会创建新的类型，体现在错误信息上
    - type不能直接extends，能可以通过交叉类型&模拟继承
    - 在进行类型合并（Declaration Merging）的时候，type alias不会被合并，而同名的多个interface会合并成一个
    - type可以声明基本类型别名，联合类型，元组等类型
    - type语句中还可以使用typeof获取实例的类型进行赋值
  - interface特有
    - 接口可被extends和implements
    - interface能够声明合并
  - 建议
    - 编写三方库时使用interface
    - 如果想保持代码统一，可尽量选择使用type alias
  - ref
    - 接口定义的成员必须全部实现，不能少，也不能多
    - 接口声明可选成员要用问号 `?`
    - 接口支持更多成员要用 `[propName: string]: any;` ，这样数量和类型都不限制
    - type operands can be type parameters;
    - interface... extends operands must be concrete types.
    - https://stackoverflow.com/questions/42735611/why-can-intersection-types-contain-conflicting-types

## ts-react

- 所有用到jsx语法的文件都需要以 `tsx` 后缀命名
- 组件声明时使用 `Component<P, S>` 泛型参数来代替PropTypes
- 全局变量或者自定义的window对象属性，统一在项目根下的 `global.d.ts` 中进行声明定义
- 对于项目中常用到的接口数据对象，在 `types/` 目录下定义好其结构化类型声明
- 高阶组件的使用，既可以使用函数式方法调用，也可以使用装饰器
  - 但在TS中，编译器会对装饰器作用的值做签名一致性检查
  - 而我们在高阶组件中一般都会返回新的组件，并且对被作用的组件的props进行修改，这些会导致签名一致性校验失败，TS会给出错误提示
  - https://juejin.im/post/5bed5f03e51d453c9515e69b

## summary

- 获取数组中元素类型的方法，使用 indexed access operator `T[K]`

``` typescript
type Foo = Array<{ name: string; test: number; }>;
type FooItem = Foo[0];

// or

type FooItem = Foo[number];
```

- any vs unknown
  - unknown is the type-safe counterpart of any. 
  - Anything is assignable to unknown, but unknown isn't assignable to anything but itself and any without a type assertion or a control flow based narrowing. 
  - Likewise, no operations are permitted on an unknown without first asserting or narrowing to a more specific type
- `object` vs `Object`
  - object represents anything that's not a primitive; so anything that's not number, string, boolean, symbol, null, or undefined.
  - Don’t ever use the types Number, String, Boolean, Symbol, or Object 
      - These types refer to non-primitive boxed objects that are almost never used appropriately in JavaScript code
  - Instead of Object, use the non-primitive object type
- `any` vs `Object`
  - Object is more restrictive than any
  - Object exposes the functions/properties defined in the Object class
  - `Object` contains stuff that is present in all JavaScript objects. Any value (primitive, non-primitive, null and etc) can be assigned to Object type.
  - `{}` is an empty object. It is the same as `Object`
  - `object` was introduced in TypeScript 2.2. It is any non-primitive type. You can't assign to it any primitive type like number, string...

``` typescript
let a: any;
let b: Object;

a.nomethod(); // Transpiles just fine
b.nomethod(); // Error: Property 'nomethod' not exist on type 'Object'
```

- `Array<Type>` vs `Type[]`
  - There is no difference. `Type[]` is the shorthand syntax for an array of Type. `Array<Type>` is the generic syntax. 
  - `var arr: Array<any>;` is equivalent to `var arr: any[];`
  - https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#a-new-syntax-for-readonlyarray
- the operation x! produces a value of the type of x with null and undefined excluded
- ts高级类型
  - 交叉类型 `&` 会获取所有类型属性的并集，同名属性最终的类型会是Type1 & Type2
      - 交叉类型的实例对象必须包含所有类型的所有属性，访问任意属性都可以
  - 联合类型 `|` 会获取所有类型属性的交集，
      - 联合类型的实例对象必须包含声明类型之一的全部属性，访问属性只能访问交集
      - 若一定要访问非共有属性，方法一是用类型断言，方法二是自定义类型保护
  - 在实际应用中，字符串字面量类型可以与联合类型，类型保护和类型别名很好的配合。通过结合使用这些特性，你可以实现**类似枚举类型的字符串**
      - `type Easing = "ease-in" | "ease-out" | "ease-in-out";`
- ts配置文件tsconfig.json
  - 指定编译参数compilerOptions
      - outDir：指定编译生成的文件存放路径，默认与.ts文件相同
      - module：指定生成的js中应该采用什么模块化组织方式，如cjs,umd,es2015,none
      - target：指定生成的js代码的版本，如esnext,es2015,es5,es3
      - lib：指定编译时引入的ES功能库
      - moduleResolution：指定模块解析方式，选择classic、node
      - noImplicitThis：this可能为any时抛错
      - typeRoots：指定编译时要包含的类型声明文件，默认所有./node_modules/types包会在编译过程中被包含进来
  - 指定待编译的文件
      - files和include取并集
  - 指定不会被编译的文件exclude
      - 使用"outDir"指定的目录下的文件永远会被编译器排除，除非你明确地使用"files"将其包含进来
  - 参考
      - [CN](https://www.tslang.cn/docs/handbook/compiler-options.html)
      - [tsconfig.json](https://github.com/hstarorg/HstarDoc/blob/master/%E5%89%8D%E7%AB%AF%E7%9B%B8%E5%85%B3/TypeScript%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6tsconfig%E7%AE%80%E6%9E%90.md)
- js特点
  - 语言具有动态性，无需编译，浏览器直接解释执行
  - 任何事物均为对象，包括函数
  - 弱类型变量，无需声明也可使用，变量可以被赋予任何类型，包括函数
  - `null == undefined` 返回true，但 `null === undefined` 返回false
- ts特性
  - 可选的编译时类型
      - 类型本身就是很重要的注释
  - 特有数据类型
      - Tuple元组(长度固定、类型固定的数组)
      - enum枚举
      - 联合类型
      - 不支持Map,Set,ES6 has a Map type, you can use it in typescript by referencing the ES6 definitions
  - 接口
      - 支持定义属性和方法
      - 接口之间可继承
  - 泛型支持
      - 用来定义一种可以操作一组类型的函数
  - 增强的class
      - 属性和方法支持访问修饰符public，private，protected
      - 可重载
  - 类型定义文件*.d.ts
      - 在ts中使用已有的js库
- ts与es6共有特性
  - 块级作用域与变量let/const
  - 模板字符串
  - class
      - 支持类属性，类方法
      - 支持继承
  - 箭头函数
  - 模块
  - 扩展运算符与解构赋值
  - promise
  - 生成器函数
  - 迭代器
  - Symbol支持
      - 不重复的属性名
  - 装饰器
      - 类似java的注解、python的装饰器
      - 用于修改预定义好的逻辑，或者给各种结构添加一些元数据，还可用于实现aop
      - ts的装饰器还可以装饰参数
- typescript
  - https://www.typescriptlang.org
  - https://github.com/Microsoft/TypeScript 
  - /Apache2.0/53kStar/201908
  - version
    - 3.5.3-201907
    - 3.0.0-201807
    - 2.0.2-201608
    - 1.5.3-201507
    - 1.1-201409
    - initial-2012
- flow
  - https://flow.org/
  - https://github.com/facebook/flow
  - /MIT/2kStar/201908
  - version
      - 0.106-201908

## book-Learning TypeScript_Remo H. Jansen_2016

- ts基本数据类型
  - string
  - number
  - boolean
  - array
    - `var list:number[] = [1, 2, 3];`
    - `var list:Array<number> = [1, 2, 3];`
  - void
    - any的对立面就是void，即所有的类型都不存在的时候
  - enum
      - 成员默认从0开始
- any类型
  - 所有这些类型在TypeScript中，都是一个唯一的顶层的Any Type类型的子类型， `any` 关键字代表这种类型
  - any类型可以表示任意JavaScript值
  - 一个any类型的值支持所有在JavaScript中对它的操作
  - 对一个any类型的值操作时仅进行最小化静态检查
  - 当一个变量的类型无法被推测时，一个特殊的类型any会作为它的类型
  - 使用any类型是与现存的JavaScript代码一起工作的一种高效的方式
  - any类型在你只知道一部分类型的情况下也很方便，如 `var list:any[] = [1,"a"];`
- 在TypeScript1.0中，不能把null或undefined当作类型使用，2.0有变化
- 联合类型
  - 联合类型用来声明那些可以存储多种类型值的变量
- 环境声明
  - declare操作符在作用域中增加一个声明对象
  - TypeScript默认包含一个名为 `lib.d.ts` 内置库的接口声明
      - 提供了js内置对象、DOM、BOM
  - `.d.ts` 结尾的文件是类型定义/描述文件，通常包含对第三方库API的类型声明
  - tsd是管理类型定义文件的工具
- 可以使用接口来确保类拥有指定的结构
