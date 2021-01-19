---
title: cli-frontend-dev
tags: [cli, frontend]
created: '2020-06-19T04:40:23.543Z'
modified: '2021-01-01T22:14:19.469Z'
---

# cli-frontend-dev

# guide

- 发包工作流：version bump -> changelog -> git release -> npm publish
  - lerna提供了主流的解决方案，但并不是每步都必须执行

# react

- cra
  - `npm x -- create-react-app react-cra-ts --template typescript --use-npm`

# npm-cli

- config-settings
  - prefix
    - The location to install global items. 
    - If set on the command line, then it forces non-global commands to run in the specified folder.

- `npm install --legacy-peer-deps --ignore-scripts`
  - --ignore-scripts: do not execute any scripts defined in the package.json.
  - ref
    - [npm install 之 gRPC](hhttps://www.jianshu.com/p/61e3cfb9c623)
      - `npm install grpc --ignore-scripts`
      - 进入node_modules目录。进入grpc的项目。修改相关源码文件：c++源码在deps/grpc/src/core/lib中。
      - 重新build grpc：npm run-script install grpc --fallback-to-build --library=static_library 或者 `npm rebuild`
    - [–ignore-scripts ignores *all* scripts](https://npm.community/t/ignore-scripts-ignores-all-scripts/1403)
      - to allow only specific preinstall and postinstall scripts to run, I have used a strategy similar to this one:
      - `npm install --ignore-scripts && ( cd ./node_modules/nose-sass && npm run install )`
      - in order to not have to remember and type the exact invocation every time, I added it into my package.json's scripts section
      - You can do `npm rebuild node-sass`. 
        - This will leave your package.json/package-lock.json files intact but still make sure you get your native dep built.
      - `npm rebuild` looks like the best solution for now.running `npm install node-sass` will modify package.json.

- `npm build [<package-folder>]`
  - This is the plumbing(管道系统；管道安装及修理) command called by `npm link` and `npm install`.

- `npm rebuild`
  - This command runs the `npm build` command on the matched folders. 
  - This is useful when you install a new version of node, and must recompile all your C++ addons with the new binary.

# nvm

- To set a default Node version to be used in any new shell, use the alias 'default':
  - Use `nvm alias default node` to make the "latest" the default.
  - `nvm alias default 6.11.5` if you want it pegged to that specific version.
  - You can also do `nvm alias default 6`.
  - alias works as long as you're not installing new versions. 
    - After installing a new node the node will be your current node to use. 
    - So if you want to prevent this behavior, you have to explicitly set up nvm alias default desiredVersionOfNode after each installation or just reopen a terminal

# 前端开发工具

- storybook
  - UI component dev & test: React, Vue, Angular, Web Components & more
  - addon
- codesandbox
  - Online Code Editor Tailored for Web Application
- lint: eslint
- tes
  - tjest
  - enzyme
- webpack
  - entry
  - output
  - module
    - loader
  - resolve：设置模块如何被解析
    - alias选项设置别名
    - extensions指定解析器接受的扩展名
- npm
  - 前端包管理器 
  - 常用命令
    - `npm config list` ：查看npm配置信息
    - `npm ls -g --depth=0` ：查看本地全局安装的包
    - `npm i -D webpack --registry=https://registry.npm.taobao.org`
  - npm vs yarn
  - npm包名规范
    - 把包名中的标点符号去掉并与现有的包进行比较，相同则不允许发布
    - 找到一个独一无二包名最简单方法就是使用作用域 `@+用户名` ，被划了作用域的包默认是私有的，所以要通过 `--access=public` 让它变为公有的包
- yarn
  - a package manager for your code
  - Running `yarn` with no command will run `yarn install`
  - workspaces
      - 提升依赖下载到根目录，减少重复下载
      - Nested workspaces are not supported at this time.
  - yarn vs lerna
      - lerna管理构建时的相互依赖和发布，yarn专注于依赖下载
      - Yarn’s workspaces are the low-level primitives that tools like Lerna can (and do!) use. 
      - They will never try to support the high-level feature that Lerna offers, but by implementing the core logic of the resolution and linking steps inside Yarn itself we hope to enable new usages and improve performance.
- lerna
  - A tool for managing JavaScript projects with multiple packages
  - 多个package是放在单个仓库里维护还是放在多个仓库里单独维护
      - monorepo：方便相互依赖的项目自动测试，但repo体积较大
      - 多仓库维护：方便多人协作
  - 多仓库包管理常见问题
      - package之间相互依赖，开发人员需要在本地手动执行npm link，维护版本号的更替
      - 每一个package都包含独立的node_modules，而且大部分都包含babel等开发时依赖，安装耗时冗余并且占用过多空间
  - 多个包管理方案
      - lerna
      - yarn workspace
      - npm link
  - lerna使用体验
      - 构建时自动解决packages之间的依赖关系，直接依赖本地项目源码
      - 根据git提交记录，自动生成changelog
      - 发布时一起发布多个包
      - 统一管理依赖版本
  - 包管理常用命令
      - `lerna init` ：以所有子包共用版本号的固定模式初始化项目， --independent
      - `lerna bootstrap` ：为所有项目安装依赖，类似于npm i/yarn
      - `lerna add pkgA --scope=pkgB` ：将A安装到B的字段， --dev，一次只能一包
      - `lerna publish` ：先确定哪些包需要publish，--skip-git/npm
          - 先设置version，先打tag，再push到github，再上传npm，可通过参数拆分流程
          - `lerna publish from-package --yes --registry http:// `
          - 参考 https://github.com/lerna/lerna/issues/1648
      - `lerna ls` ：显示packages下的各个package的version
      - `npm link` ：可添加本地正在开发的包作为依赖

## webpack

- 对于typescript + monorepo的hot reload热加载
  - 基本思路是将package.json的main属性值直接配置到源码如 `src/index.tsx` ，参考例子react-workspaces-playground
  - 对于某些特别复杂的项目，如ag-grid，由于使用的ts特性特别多，样式引用scss，编译需要的插件可能变得很复杂，热加载很可能编译不通
    - 可以先采取过渡方案，将main属性值配置到 `dist/index.js` ，然后 `tsc --watch` 编译依赖项目，这样修改时会自动编译出新的dist/index.js
    - 等到对项目源码思路熟练掌握时，可自定义重新构建
- [tsconfig-paths-webpack-plugin](https://github.com/dividab/tsconfig-paths-webpack-plugin)
  - Use this to load modules whose location is specified in the `paths` section of `tsconfig.json` when using webpack. 
  - This package provides the functionality of the `tsconfig-paths` package but as a webpack plug-in.
  - Using this plugin means that you should no longer need to add `alias` entries in your `webpack.config.js` which correspond to the paths entries in your `tsconfig.json` . This plugin creates those `alias` entries for you, so you don't have to!
- [babel-plugin-module-resolver](https://github.com/tleunen/babel-plugin-module-resolver)
  - This plugin allows you to add new "root" directories that contain your modules. 
  - It also allows you to setup a custom alias for directories, specific files, or even other npm modules.
- terser-webpack-plugin
  - uses terser to minify your JavaScript

## babel

- [babel-plugin-transform-typescript-metadata](https://github.com/leonardfactory/babel-plugin-transform-typescript-metadata)
  - Current `@babel/preset-typescript` implementation however just strips all types and does not emit the relative Metadata in the output code.
  - Babel plugin to emit decorator metadata like typescript compiler

# 开发常用工具

- Conventional Commits
  - add human and machine readable meaning to commit messages
  - https://www.conventionalcommits.org
  - fix, feat, chore, docs, style, refactor, perf, test

# 前端依赖工具库

- date-fns
  - 方便在浏览器和Node中操作时间日期
  - provides the most comprehensive, yet simple and consistent toolset for manipulating JavaScript dates in a browser & Node.js
- react-markdown
  - Renders Markdown as pure React components
- marked
  - A markdown parser built for speed
- raf
  - requestAnimationFrame polyfill for node and the browser
- fast-memoize
  - fastest memoization library in js that supports N arguments
  - memoization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again
- memoize-one
  - Unlike other memoization libraries, memoize-one only remembers the latest arguments and result
  - memoize-one simply remembers the last arguments, and if the function is next called with the same arguments then it returns the previous result
- classnames
  - js utility for conditionally joining classNames together
- immutable-js
  - v4
    - The Iterable class has been renamed to Collection
    - improve Record impl, Record is no longer an Immutable Collection type
    - Flowtype and TypeScript type definitions have been completely rewritten

# 前端工程辅助工具

- rimraf
  - 作用是以包的形式封装rm -rf命令，用来删除文件和文件夹，不管文件夹是否为空，都可删
  - `rm -rf` for node 
  - 命令也可在windows下使用
- husky
  - 能够防止不规范代码被commit、push、merge等等
  - 在执行 `git commit` 之前会先执行script字段的precommit指定的命令，如yarn test
  - pre-commit包功能更灵活
- plop
  - 设置好模板内容和生成文件路径后，可在命令行输入参数，自动生成组件到路径位置
- replace-in-file
  - A simple utility to quickly replace text in one or more files or globs
- kkt
  - Create React apps with no build configuration, Cli tool for creating react apps
- tsbb
  - a zero-config CLI that helps you develop, test, and publish modern TypeScript Node.js project.
  - TypeScript + Babel = TSBB
- KaTeX
  - library for TeX math rendering on the web
- tslib
  - tslib将仅用于您的编译目标不支持的功能，以便我们生出的代码更小
