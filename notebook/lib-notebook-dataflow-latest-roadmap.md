---
title: lib-notebook-dataflow-latest-roadmap
tags: [dataflow, notebook, roadmap]
created: '2021-05-21T18:51:59.211Z'
modified: '2021-05-21T18:52:34.253Z'
---

# lib-notebook-dataflow-latest-roadmap

# guide

- compiler
  - jsx -> ojs
  - mdx -> ojs
  - ojs通过unofficial-compiler编译成es6标准模块
    - 编译前的ojs大部分无需修改就可以拷贝到observablehq notebook
    - 编译后的es6可以灵活在自己的项目中使用
# roadmap

## [Compiler v1 - Current problems, potential solutions](https://github.com/asg017/unofficial-observablehq-compiler/issues/26)

- this compiler was built on top of my ill-defined idea of how the project should be structured. 
  - I've spent some time using this library in another project, dataflow, 
  - and I've found many issues/confusing things in this library that I think we can improve on.

### This library is an interpreter and compiler

- My original take of this library was an interpreter, NOT a compiler. 
  - I named it "compiler" because that's what Observable called their closed-source library
  - the original take of this library was like so:

```JS
const compile = new Compiler();
const main = await compile.module(`a =1; b = 2; c = a + b;`);
console.log(main.value('c')); // 3
```

- The above doesn't compile observable javascript into "real" javascript, it interprets it and executes it on the fly. 
  - This library didn't have "compiler" features until @bryangingechen added it like so:

```JS
const compile = new Compiler();
const src = compile.moduleToESModule(`a = 1; b = 2; c = a + b`);
console.log(src); // "export default function define(runtime, observer) { ..."
```

- I think we can do a better job at distinguishing this in the API. 
  - Maybe separate Interpreter and Compiler classes that you interact with. 
  - In dataflow, I found myself using the "Interpreter" functions (`.cell, .module, createCellDefinition`) when building the "live editor" features, and the "Compiler" functions (`.moduleToESModule`) when building "export" features. 
  - I would assume other users of this library would want something similar, and an easier-to-understand API would be very helpful.

### define/redefine doesn't help, but raw Runtime variables do

- Many of the current "interpreter" functions return explicit define/redefine functions
  - I found only define useful, and instead of redefine
- What's key here we need to return runtime variable references in interpreter commands
  - With those variables, people can delete/redefine the variable directly as they please, instead of dealing with these cryptic(晦涩难懂的；隐晦的、秘密的) define/redefine methods.

### I found pre-parsing input important

- Sometimes, I would pre-parse source code with `@observablehq/parser` to check for specific references, like `FileAttachment` and `Secret`, or to keep track of source code -> runtime variable references to rearrange when code was re-arranged. 
  - I would also do this to find import statements and import remote notebooks when interpreting 
  - (our current interpreter assumes remote modules are pre-fetched, which is also NOT good).
- I think we should either 
  - (a) only allow people to pass in pre-parsed source code instead of source code directly
  - (b) offer some sort of utility functions that make this easier
  - (c) return more than just runtime variables / offer better hooks to customize behavior (e.g. return whether a cell is referencing FileAttachment/secrets, adding a "resolveNotebookPath" function in function calls, etc.).
- I haven't thought too much about what this would look like, but I think this can be done last when most of the other changes are made.
# changelog
