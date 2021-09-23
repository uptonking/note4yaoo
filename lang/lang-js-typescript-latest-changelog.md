---
title: lang-js-typescript-latest-changelog
tags: [changelog, lang, typescript]
created: '2020-07-14T02:36:53.471Z'
modified: '2020-07-14T12:06:37.292Z'
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

## [Looks like @TypeScript is getting Tail Call Recursion before @nodejs does, just at a completely different level of the software stack.](https://twitter.com/orta/status/1433835302431428617)

- It's tail recursion at the type level, not at the runtime level.
- How long is it going go take before TS becomes pluggable types engine for any other language

## changelog-overview

- Between TypeScript 1.0 and up until 2.0, the language added union types, type guards, modern ECMAScript support, type aliases, JSX support, literal types, and polymorphic this types. 
- If we include TypeScript 2.0 with its introduction of non-nullable types, control flow analysis, tagged union support, this-types, and a simplified model around .d.ts file acquisition, that era truly defined the fundamentals of using TypeScript.
- TypeScript 2.1 was a foundational release that introduced a static model for metaprogramming in JavaScript. The key query ( `keyof` ), indexed access ( `T[K]` ), and mapped object ( `{ [K in keyof T]: T[K] }` ) types have been instrumental in better modeling libraries like React, Ember, Lodash, and more.
- TypeScript 2.2 and 2.3 brought support for mixin patterns, the non-primitive object type, and generic defaults, used by a number of projects like Angular Material and Polymer.
- TypeScript 2.4 and 2.6 tightened up the story for strict checking on function types
- TypeScript 2.8 introduced conditional types, a powerful tool for statically expressing decisions based on types, and 2.9 generalized keyof and provided easier imports for types.
# changelog

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
