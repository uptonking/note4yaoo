---
title: lang-js-tsc
tags: [devtools, lang-ts, tsc]
created: 2024-01-02T08:59:22.597Z
modified: 2024-01-02T08:59:51.343Z
---

# lang-js-tsc

# guide

- tsc-monorepo
  - 不能bundle输出单文件
  - tsc没有 transpile- only 的选项
  - tsc不开启project-references时，会转译所有子包，输出的子文件层级很深
# dev-xp

```shell
# to see which files are included
tsc --listFiles

```

- Triple-slash references instruct the compiler to include additional files in the compilation process.
  - Similar to a `/// <reference path="..." />` directive, which serves as a declaration of dependency, a `/// <reference types="..." />` directive declares a dependency on a package.
  - `/// <reference lib="..." />` allows a file to explicitly include an existing built-in lib file, like `lib="es2015"`.
# not-yet
- 🐛 monorepo中，./app1项目执行tsc -p tsconfig.json -w 会转义输出 ./packages/lib1 的代码到dist
  - 变通方案是使用自定义打包工具webpack

- [`@ts-ignore` for the block scope and imports](https://github.com/Microsoft/TypeScript/issues/19573)
  - Why not close this and admit it will never be added?
  - People don't like it when we do that either
# faq

# more
- [tsc性能优化 -- Project References - 掘金](https://juejin.cn/post/7165429078470688781)
# discuss
- ## 

- ## 

- ## 

- ## [How to compile Typescript project into one file without system/amd overhead? - Stack Overflow](https://stackoverflow.com/questions/72738931/how-to-compile-typescript-project-into-one-file-without-system-amd-overhead)
- TypeScript is a compiler. So it compiles files to newer files preserving the directory structure.
- Compiling into a single file is essentially a definition of module bundler. So, it is Webpack, Rollup, Parcel or equivalent.

- ## [Monorepo with `rootDirs` produces unwanted sudirectories such as `src` in `outDir` - Stack Overflow](https://stackoverflow.com/questions/60896829/monorepo-with-rootdirs-produces-unwanted-sudirectories-such-as-src-in-outdi)
  - In the above, dist contains backend and shared BUT each of them contains src under it. I wanted backend and shared under dist contain compiled JS files without src
- prescription: Structure your monorepo as separate Typescript sub-projects
  - You can have multiple a projects (e.g. a main and a set of libs) each in their own directory with their own tsconfig, with their own rootDir. 
  - Dependencies between them are managed in the tsconfig files using Typescript Project References.
