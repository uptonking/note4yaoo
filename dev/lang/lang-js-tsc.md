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

- resources
  - [Nx, NodeJS and TypeScript Compatibility Matrix | Nx](https://nx.dev/nx-api/workspace/documents/nx-nodejs-typescript-version-matrix)
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
# docs

# tsconfig

- `rootDir` does not affect which files become part of the compilation. It has no interaction with the `include, exclude, or files` tsconfig.json settings.
  - Note that TypeScript will never write an output file to a directory outside of `outDir`, and will never skip emitting a file. For this reason,  `rootDir` also enforces that all files which need to be emitted are underneath the `rootDir` path.

- `files` : Specifies an allowlist of files to include in the program
  - An error occurs if any of the files can’t be found.
  - Default: false
  - stuff in "files" will never be ruled out by "exclude" patterns

- `include` Specifies an array of filenames or patterns to include in the program. 
  - These filenames are resolved relative to the directory containing the tsconfig.json file.
  - If the last path segment in a pattern does not contain a file extension or wildcard character, then it is treated as a directory, and files with supported extensions inside that directory are included (e.g. `.ts, .tsx, and .d.ts` by default, with `.js and .jsx` if allowJs is set to true).

- `exclude` only changes which files are included as a result of the include setting. 
  - A file specified by exclude can still become part of your codebase due to an import statement in your code, a types inclusion, a `/// <reference` directive, or being specified in the `files` list.
  - It is not a mechanism that prevents a file from being included in the codebase - it simply changes what the include setting finds.

- `outDir` :
  - If specified, .js (as well as .d.ts, .js.map, etc.) files will be emitted into this directory. 
  - If not specified, .js files will be emitted in the same directory as the .ts files they were generated from
- `outFile`: If specified, all global (non-module) files will be concatenated into the single output file specified.
  - outFile cannot be used unless module is `None, System, or AMD`. 
  - This option cannot be used to bundle `CommonJS` or `ES6` modules.

- `listFiles`: Print names of files part of the compilation. 
  - This is useful when you are not sure that TypeScript has included a file you expected.
  - Note if using TypeScript 4.2, prefer `explainFiles` which offers an explanation of why a file was added too.
- `explainFiles`: Print names of files which TypeScript sees as a part of your project and the reason they are part of the compilation.

- 
- 
- 
- 

# faq

# more
- [tsc性能优化 -- Project References - 掘金](https://juejin.cn/post/7165429078470688781)
# discuss-not-yet
- ## 

- ## 

- ## 

- ## [Suggestion: an option to make `--showConfig` more verbose · Issue · microsoft/TypeScript](https://github.com/microsoft/TypeScript/issues/33211)
  - Currently, the --showConfig option will only print the compiler options that are provided by the given tsconfig.json.

- 202501: I guess to make the command output all effective compiler options is not easy, as code for that seems to be distributed in the codebase.
  - Meaning as of today, tsc does not compute the full list of compiler options at some central place (which could just be printed via --showConfig).
# discuss
- ## 

- ## 

- ## 

- ## [Error "Cannot write file ... because it would overwrite input file." · Issue #27436 · microsoft/TypeScript](https://github.com/microsoft/TypeScript/issues/27436)
- I'm attempting to compile and deploy a NestJS app, and was getting this error on npm run build.
  - I resolved this by editing tsconfig.build.json, and adding my build directory to the exclude list. In NestJS, the build dir appears to default to dist.

- 
- 
- 

- ## [TypeScript error: Cannot write file 'index.d.ts' because it would overwrite input file - Stack Overflow](https://stackoverflow.com/questions/37013665/typescript-error-cannot-write-file-index-d-ts-because-it-would-overwrite-inpu)
- Adding `include` to my configuration solved the problem for me.
  - As said in the doc, exclude specifies an array of filenames or patterns that should be skipped when resolving include.
  - I deduce that exclude can't work if include hasn't been defined.

```JS
{
  "compilerOptions": {
    /* ... */
  },
  "include": ["src"],
  "exclude": ["**/*.test.*"]
}
```

- ## [How to compile Typescript project into one file without system/amd overhead? - Stack Overflow](https://stackoverflow.com/questions/72738931/how-to-compile-typescript-project-into-one-file-without-system-amd-overhead)
- TypeScript is a compiler. So it compiles files to newer files preserving the directory structure.
- Compiling into a single file is essentially a definition of module bundler. So, it is Webpack, Rollup, Parcel or equivalent.

- ## [Monorepo with `rootDirs` produces unwanted sudirectories such as `src` in `outDir` - Stack Overflow](https://stackoverflow.com/questions/60896829/monorepo-with-rootdirs-produces-unwanted-sudirectories-such-as-src-in-outdi)
  - In the above, dist contains backend and shared BUT each of them contains src under it. I wanted backend and shared under dist contain compiled JS files without src
- prescription: Structure your monorepo as separate Typescript sub-projects
  - You can have multiple a projects (e.g. a main and a set of libs) each in their own directory with their own tsconfig, with their own rootDir. 
  - Dependencies between them are managed in the tsconfig files using Typescript Project References.
