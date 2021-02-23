---
tags: [coding, dev]
title: coding-style
created: '2019-09-03T14:06:29.976Z'
modified: '2020-06-30T05:17:43.290Z'
---

# coding-style

# naming is hard

## Function naming conventions

- One of the more universal, yet simple rules is: 
  - consistent
  - Function names should be verbs if the function changes the state of the program, and nouns if they're used to return a certain value.

- [Coding like Shakespeare: Practical Function Naming Conventions](https://dmitripavlutin.com/coding-like-shakespeare-practical-function-naming-conventions/)

# js

- export 导出
  - 结论是使用命名导出，少用default
    - 使用命名导出应该在声明时导出，还是在文件末尾导出本模块所有对象？？？
    - 不能在一个文件中使用上述方法export两次，因为export的对象不可变
  - [Avoid Export Default](https://basarat.gitbook.io/typescript/main-1/defaultisbad)
    - Poor Discoverability
    - Autocomplete
    - CommonJS interop
    - Re-exporting
    - Typo Protection
    - TypeScript auto-import
    - Dynamic Imports
    - Needs two lines for non-class / non-function
  - `export {default as Module} from './module';` is the standard ES6 way
  - `export Module from './module;` is a proposed ESnext way
  - A default export is actually a named export with the name default
  - When exporting one thing, and inline export is nicer
    - because it ensures that you can not change the binding later (ie, `export default function foo() {};` is better than `function foo() {} ; export default foo;` )
  - In most cases, you should be exporting one conceptual thing from a module. 
    - In other words, if you have both "foo" and "boo", those are two modules and thus should be export defaulted from two separate files.
    - If you insist on having them in the same file, then you should be using multiple named exports.
  - As far as positioning, there will soon be a linter rule in `eslint-plugin-import` that will require that all export statements are grouped together - so I'd recommend grouping them together and putting them at the bottom of the file.
  - 参考
    - https://github.com/airbnb/javascript/issues/710
    - https://juejin.im/post/5b2b2d8de51d4558ba1a64e0

# java

# git

- Conventional Commits (8种)
  - `<type>[(optional scope)]: <description>`
  - fix: patches a bug in your codebase
  - feat: introduces a new feature to the codebase (minor
  - refactor: A code change that neither fixes a bug nor adds a feature
  - perf: A code change that improves performance
  - test: Adding missing tests or correcting existing tests
  - docs: Documentation only changes
  - build: Changes that affect the build system or external dependencies
  - chore: update version or dependencies, release...
  - misc: revert, ci, mark, step
  - BREAKING CHANGE: a commit that has a footer BREAKING CHANGE:, or appends a ! after the type/scope
  - ref
      - https://www.conventionalcommits.org/en/v1.0.0/
      - https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines
      - https://github.com/conventional-changelog/conventional-changelog
