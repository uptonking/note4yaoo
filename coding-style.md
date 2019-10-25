---
tags: [coding]
title: coding-style
created: '2019-09-03T14:06:29.976Z'
modified: '2019-09-04T05:58:55.495Z'
---

# coding-style

## js
- export 导出
    - 结论是使用命名导出，少用default
        - 使用命名导出应该在声明时导出，还是在文件末尾导出本模块所有对象？？？
        - 不能在一个文件中使用上述方法export两次，因为export的对象不可变
    - `export {default as Module} from './module';` is the standard ES6 way
    - `export Module from './module;` is a proposed ESnext way
    - A default export is actually a named export with the name default
    - When exporting one thing, and inline export is nicer because it ensures that you can not change the binding later (ie, `export default function foo() {};` is better than `function foo() {} ; export default foo;`)
    - In most cases, you should be exporting one conceptual thing from a module. In other words, if you have both "foo" and "boo", those are two modules and thus should be export defaulted from two separate files.If you insist on having them in the same file, then you should be using multiple named exports.
    - As far as positioning, there will soon be a linter rule in `eslint-plugin-import` that will require that all export statements are grouped together - so I'd recommend grouping them together and putting them at the bottom of the file.
    - 参考
        - https://github.com/airbnb/javascript/issues/710
        - https://juejin.im/post/5b2b2d8de51d4558ba1a64e0


## java


