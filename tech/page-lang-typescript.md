---
title: page-lang-typescript
tags: [lang, typescript]
created: '2020-08-21T08:17:22.500Z'
modified: '2020-08-21T08:17:49.726Z'
---

# page-lang-typescript

# [5 reasons why Deno will stop using TypeScript](https://startfunction.com/deno-will-stop-using-typescript/)

- TypeScript compile time when changing files takes several minutes, making continuous compiling an excruciatingly slow process
- The Typescript structure that they’re using in the source files that create the actual Deno executable and the user-facing APIs is creating runtime performance problems
- TypeScript isn’t proving itself helpful to organize Deno code. 
  - One of the issues mentioned is that they ended up with duplicate independent Body classes in two locations 
- The internal code and runtime TypeScript declarations must be manually kept in sync since the TypeScript Compiler isn’t helpful to generate the d.ts files
- They’re maintaining two TS compiler hosts: one for the internal Deno code and another other for external user code even though both have a similar goal
- The Deno team aims to remove all build-time TS type checking and bundling for internal Deno code. 
  - They’re looking forward to move all the runtime code into a single JavaScript file.
  - However, they’ll still use a companion d.ts file to keep the type definitions and documentation.
- It’s worth mentioning that Deno will stop using TypeScript only for the internal Deno code: the Deno user code will still be in TypeScript and thus type checked.

# [How to set up a TypeScript monorepo with Lerna](https://medium.com/@NiGhTTraX/how-to-set-up-a-typescript-monorepo-with-lerna-c6acda7d4559)

- 对于项目A依赖项目B的情况
  - 直接设置B的package.json的main为源码位置
  - 利用lerna run build编译所有项目，自动计算依赖拓扑结构
  - 利用typescript project references设置项目依赖，然后编译A时会自动编译B

- If you’re using imports that expose the internal structure of packages `e.g. import foo from '@pkg/bar/src/libs/file` , then you’ll most likely be fine with just the symlinks that lerna or yarn sets up.
- If however you have packages which define entry points through pkg.main that don’t point to the source code e.g. `import foo from @pkg/bar/file` (notice the missing src) then read on.
- `tsconfig.json` is the config that will be picked up by an IDE by default and maps absolute package names back to their source code in the monorepo
  - use `paths` to tell the TypeScript compiler that whenever a module tries to import another module from the monorepo, it should resolve it from the `baseUrl` + `paths` folder.
- If we try to build the `bar` package (which depends on the `foo` package) in a fresh state (no dist folders anywhere), then it will fail and complain that it can’t find `foo` , even though lerna symlinked it in its `node_modules` folder. 
  - This is because `foo` 's `package.jso` n defines its entry point via the `main` field to point to `dist/index` . 
  - When the TypeScript compiler sees `import '@pkg/foo'` in the `bar` package, it will look for `bar/node_modules/@pkg/foo/dist/index.js`
  - and, because `foo` hasn’t been built (therefore there’s no `dist/` folder in it), will fail.
  - If the `main` field pointed to the original source code, then everything would work without any surprises. 
  - A package import would be resolved to the symlink that lerna creates in `node_modules` and that points back to the source code in the monorepo.
- We can solve this problem in 2 ways:
  - Use `lerna run` to build all the packages at once and rely on it building the packages in the correct order by looking at each package’s dependencies.
  - Use the project references feature introduced in TS 3.0.
- `lerna run <script>` will run `<script>` in each package that has that script defined in its `package.json` . 
  - It will also run them in topological order
  - while `lerna run` respects the topological order of the packages, `lerna publish` doesn’t, or at least it doesn’t compute the same order.
  - build all the packages before publishing any of them. 
  - We can do this simply by calling `lerna run build` before `lerna publish` which will run each script’s build script.
- Using project references achieves the same thing as `lerna run` — building projects in the correct order — but also allows us to build one package at a time.( `lerna run` 会在所有package运行build)
  - The `references` config is an array of paths and here we manually specify the path to the `tsconfig.json` of the depending packages.
  - Now if we change the compile script in `package.json` to run `tsc -b` , we can build a single package and TypeScript will build any project dependencies for us. 
  - We also need to update the `clean` script to remove the build cache for `tsc -b`

# ref
