---
title: lang-js-typescript-latest-changelog
tags: [changelog, lang, typescript]
created: 2020-07-14T02:36:53.471Z
modified: 2020-07-14T12:06:37.292Z
---

# lang-js-typescript-latest-changelog

# guide

- typescript /Apache2/53kStar/201908
  - https://www.typescriptlang.org
  - https://github.com/Microsoft/TypeScript 
- flow /MIT/2kStar/201908
  - https://flow.org/
  - https://github.com/facebook/flow
# release-notes

## [TypeScript 4.9 正式发布[2022.11.15][官文全文翻译] - 知乎](https://zhuanlan.zhihu.com/p/584007369)

- [Announcing TypeScript 4.9 - TypeScript](https://devblogs.microsoft.com/typescript/announcing-typescript-4-9/)

- 这里是 TypeScript 4.9 更新的内容
satisfies 操作符
in 操作符中未列举的属性收束
Class 的 Auto-Accessor
对于 NaN 进行检查
File-Watching Now Uses File System Events
编辑器增强：“Remove Unused Imports” 和 “Sort Imports”
编辑器增强： Go-to-Definition on return Keywords

- [TypeScript 4.9 beta 发布：鸽置的 ES 装饰器、satisfies 操作符、类型收窄增强、单文件级别配置等 - 掘金](https://juejin.cn/post/7147587407050145806)
- 下面是夹带私货时间。
  - 如果你对 TypeScript 中的类型层级有一定了解，或是使用过其他静态类型的编程语言，很容易发现这里其实还蕴藏着一个类型层级的上下级关系：推导得到的类型实际上是我们标注类型的子类型
  - 当我们写出 `satisfies Record<Colors, string | RGB>` 时，实际上是在进行类型的向上转换，即 upcast。
  - 首先，使用类型断言的本质还是让显式提供的类型信息完全覆盖推导得到的类型信息，从这一点来看就可以毙掉了。
  - 而更可怕的一点是，类型断言是允许你把不正确的值断言成提供的类型信息的，相当于埋下了一颗定时炸弹，因此使用类型断言来实现 upcast 其实是一个不怎么安全的操作。
  - 就像 TypeScript 发现过于自由的 any 类型可能会带来问题一样，更安全的 Top Type —— unknown 类型加入解决了使用顶级类型时的安全隐患。现在，为了让 upcast 操作也能更安全一些，我们又迎来了 satisfies ，可以确定在不远的未来，它必定会成为你最好的类型工具之一。
  - upcast 很多时候是自动实现的，而 downcast 则必须要手动实现，以及附加类型检查。如果我们想要执行 downcast，通常需要配合类型守卫 instanceof
  - 这两个概念在 Java 中也是类似的，upcast 会自动执行，而 downcast 则需要通过检查，否则就会抛出错误（ClassCastException）

## [Looks like @TypeScript is getting Tail Call Recursion before @nodejs does, just at a completely different level of the software stack.](https://twitter.com/orta/status/1433835302431428617)

- It's tail recursion at the type level, not at the runtime level.
- How long is it going go take before TS becomes pluggable types engine for any other language

## changes-overview

- Between TypeScript 1.0 and up until 2.0, the language added union types, type guards, modern ECMAScript support, type aliases, JSX support, literal types, and polymorphic this types. 
- If we include TypeScript 2.0 with its introduction of non-nullable types, control flow analysis, tagged union support, this-types, and a simplified model around .d.ts file acquisition, that era truly defined the fundamentals of using TypeScript.
- TypeScript 2.1 was a foundational release that introduced a static model for metaprogramming in JavaScript. The key query ( `keyof` ), indexed access ( `T[K]` ), and mapped object ( `{ [K in keyof T]: T[K] }` ) types have been instrumental in better modeling libraries like React, Ember, Lodash, and more.
- TypeScript 2.2 and 2.3 brought support for mixin patterns, the non-primitive object type, and generic defaults, used by a number of projects like Angular Material and Polymer.
- TypeScript 2.4 and 2.6 tightened up the story for strict checking on function types
- TypeScript 2.8 introduced conditional types, a powerful tool for statically expressing decisions based on types, and 2.9 generalized keyof and provided easier imports for types.
# changelog
- v3.8 introduced type-only imports

## [v5.0 Beta - TypeScript](https://devblogs.microsoft.com/typescript/announcing-typescript-5-0-beta/)

- the new decorators standard
- const Type Parameters
- All enums Are Union enums
  - TypeScript 5.0 manages to make all enums into union enums by creating a unique type for each computed member. 
  - That means that all enums can now be narrowed and have their members referenced as types as well.
- Support for export type *
- @satisfies Support in JSDoc

## [v4](https://devblogs.microsoft.com/typescript/announcing-typescript-4-0-beta/)

- 4.0.0-beta-202006
- Variadic Tuple Types 可变元组类型
  - spreads in tuple type syntax can now be generic
  - 4.0 improves the inference process for rest parameters and rest tuple elements 
- Labeled Tuple Elements
  - lack of labels on tuple positions can make them harder to use
- Class Property Inference from Constructors
- Short-Circuiting Assignment Operators for `&&=, ||=, ??=`
- Customize the fragment factory through the new jsxFragmentFactory option
- `/** @deprecated */` JSDoc comment
  - deprecated values are typically displayed a strike-though style
- **breaking-changes**
- Operands for `delete` must be optional.

## [v3](https://devblogs.microsoft.com/typescript/announcing-typescript-3-0/)

- 3.5.3-201907

- 3.0.0-201807
- Project references
  - allow TypeScript projects to depend on other TypeScript projects
  - specifically, allowing tsconfig.json files to reference other tsconfig.json files. 
- Extracting and spreading parameter lists with tuples
  - allow rest parameters to be generic, and inferring those generics as tuple types
- Richer tuple types
  - tuples now allow trailing optional elements
- The `unknown` type
  - this can be any value, so you must perform some type of checking before you use it
  - Much like any, any value is assignable to unknown; 
  - however, unlike any, unknown is assignable to almost nothing else without a type assertion. 
- Support for `defaultProps` in JSX
- `/// <reference lib="..." />` directive
  - provides a new way for files to declare the built-in APIs 

## [v2](https://devblogs.microsoft.com/typescript/announcing-typescript-2-0/)

- 2.0.2-201608
- Null- and undefined-aware types
- The `never` type
- Specifying the type of `this` for functions
  - By default the type of `this` inside a function is `any` . 
  - `this` parameters are fake parameters that come first in the parameter list of a function
- Tagged union types
  - also called discriminated unions, disjoint unions, or algebraic data types
- Simplified Declaration File ( `.d.ts` ) Acquisition
- The `readonly` Modifier

## v1

- 1.5.3-201507

- 1.1-201409
- The 1.1 compiler is typically around 4x faster than any previous release

- initial-2012
