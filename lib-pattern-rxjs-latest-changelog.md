---
title: lib-pattern-rxjs-latest-changelog
tags: [changelog, pattern, rxjs]
created: '2020-12-14T14:42:29.382Z'
modified: '2020-12-14T14:44:23.079Z'
---

# lib-pattern-rxjs-latest-changelog

## guide

- [RxJS v5.x to v6 Update Guide](https://rxjs.dev/guide/v6/migration)
  - A backward-compatibility layer eases the update process, allowing you to keep your apps working while you address most code changes at your own pace.
- Before RxJS releases v7, you will need to remove and replace all use of deprecated functionality.
  - Observable.if and Observable.throw  > iif(), throwError
  - merge, concat, combineLatest, race, zip
  - Convert dot-chained operators to pipeable operators
  - Convert deprecated methods
  - In RxJS v5.x, a number of operators have an optional `resultSelector` argument
    - in which you can pass a function for handling the result of the operations.
    - you must update your code by moving your result-selection function out of the original operator call, and applying it to the results of the call.

- Problems with the patched operators for dot-chaining are
  - Any library that imports a patch operator will augment the `Observable.prototype` for all consumers of that library, creating blind dependencies. 
    - If the library removes their usage, they unknowingly break everyone else. 
    - With pipeables, you have to import the operators you need into each file you use them in.
  - Operators patched directly onto the prototype are not "tree-shakeable" by tools like rollup or webpack. 
    - Pipeable operators will be as they are just functions pulled in from modules directly.
  - Unused operators that are being imported in apps cannot be detected reliably by any sort of build tool or lint rule. 
    - That means that you might import scan, but stop using it, and it's still being added to your output bundle. 
    - With pipeable operators, if you're not using it, a lint rule can pick it up for you.
  - Functional composition is awesome. 
    - Building your own custom operators becomes much easier, and now they work and look just like all other operators in rxjs. 
    - You don't need to extend Observable or override lift anymore.

## changelog
