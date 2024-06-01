---
title: lang-js-npm
tags: [devtools, lang-js, npm, package-manager]
created: 2020-11-18T10:18:22.406Z
modified: 2024-01-02T07:49:41.237Z
---

# lang-js-npm

# guide

- cons
  - 未实现 pnpm workspaces protocol
  - 批量执行某个命令如build时，若涉及的仓库存在依赖关系，由于npm未实现按依赖顺序编译，可能执行失败或输出的文件是旧逻辑

- tips
  - npmjs.com支持按作者搜索，如`electron author:authorName`

- proxy
  - [常用网络问题库的url，部分地址失效待检查](https://github.com/cnpm/binary-mirror-config/blob/master/package.json)
# not-yet
- [[BUG] workspace scripts should be run in topological order by default · Issue · npm/cli](https://github.com/npm/cli/issues/4139)
  - A workaround here is to order your packages in the `workspaces` property of the top level `package.json` in the desired order of script execution.
  - [feat(workspaces): add `--topological-order` flag](https://github.com/npm/statusboard/issues/517)
    - 这个issue一直未开始处理

- [[QUESTION] xxx is not a valid npm option](https://github.com/npm/cli/issues/5852)
  - node.js 18 comes with npm v9, which disallows 3rd party configs and breaks our pipeline. A new pr for upgrading is recommended. 
  - [Cannot set store-dir in NPM v9](https://github.com/pnpm/pnpm/issues/5621)
    - `echo 'store-dir=/some/path/.pnpm-store' >> /usr/local/etc/npmrc`

- [npx doesn't work when in child workspace](https://github.com/npm/cli/issues/2826)
  - npm exec -w website -- docusaurus
# faq
- [[BUG] ^7.20.3 no longer resolves local package first on install (workspaces)](https://github.com/npm/cli/issues/3637)
  - you can update your package.json files directly. The format is `"<package_name>": "*"` where the version number is `"*"`. If you do this, npm will recognize it as a local dependency

- [workspaces — require local package - Stack Overflow](https://stackoverflow.com/questions/68737632/node-workspaces-require-local-package)

```JSON
{
  "dependencies": {
    "p1": "file:../p1"
  }
}
```

- [How to specify an npm workspace as a dependency - Stack Overflow](https://stackoverflow.com/questions/72851445/how-to-specify-an-npm-workspace-as-a-dependency)
  - "@project/another-package": "file:another-package"
  - Dependency from another workspace package is referenced using `file:` prefix.

- 如何执行某个workspace子包的package.json中预定义的命令
  - (~~暂不支持~~)现已支持
  - [[BUG] npm 7 workspace package script execution](https://github.com/npm/cli/issues/1904)
    - 临时方案：npm run --prefix applications/app1 build

- 是否支持将root目录也作为一个代表workspace的package
  - 暂不支持
  - [package-lock not generating properly when using "." as a workspace](https://github.com/npm/cli/issues/2233)
    - 临时方案：手动在顶层node_modules创建根项目的symlink
    - I had a chat with the @npm/cli team yesterday and the conclusion is that 
      - this is not something we want to just quickly patch 
      - but rather it's a signal that arborist is not properly handling symlinks in some cases and that warrants a more elaborate inspection/refactor of that part of the code.
      - the good news is that this use case is supported! the not so great news is that it might take a little bit more time until we get to the proper refactor and make sure that works

- package.json中scripts的循环命令如`"dev": "npm run dev"`会如何执行
  - 控制台不停打印npm run dev，然后陷入死循环

- [如何在本地调试npm包](https://github.com/allenGKC/Blog/issues/13)
  - 示例： 在 my-project 项目中测试本地的 test-npm-util 包

```

|-- project
    |-- my-project
        | -- package.json
    |-- test-npm-util

方法1: 使用相对路径安装test-npm-util测试

cd my-project
npm install ../test-npm-util

方法2: 使用 npm link 连接到全局测试

cd test-npm-util
npm link

cd my-project
npm link test-npm-util

测试完取消
cd test-npm-util
npm unlink

```

# npm-cli
- `npm install`; 
  - `install-links`: When set true,  `file: protocol` dependencies that exist outside of the project root will be packed and installed as regular dependencies instead of creating a symlink. This option has no effect on workspaces.

- `npm run-script <command> [--silent] [-- <args>...]`; 
  - This runs an arbitrary command from a package's "scripts" object.
  - The `env` script is a special built-in command that can be used to list environment variables that will be available to the script at runtime.
  - In addition to the shell's pre-existing PATH, npm run adds `node_modules/.bin` to the PATH provided to scripts. 
    - Any binaries provided by locally-installed dependencies can be used without the `node_modules/.bin` prefix.
  - Scripts are run from the root of the module, regardless of what your current working directory is when you call `npm run`. 
    - If you want your script to use different behavior based on what subdirectory you're in, you can use the `INIT_CWD` environment variable, which holds the full path you were in when you ran `npm run`.
  - "scripts": { "test": "node test/test.js" }
    - If I change directory to /dir1/dir2 and execute `npm test`
    - and the script I wrote on test property is executed properly without the use of ./ 
  - We can reference the root directory of the project through the environment variable `INIT_CWD` that npm set for us!
# package.json-config
- 关于main-module
  - 测试使用的是main
  - ide跳转使用的时main
  - webpack先检查module，再检查main
  - babel-cli只是转译，并不关心从哪里import
  - 解决方案
    - 若main指向src，则可直接测试/跳转，方便了开发
    - 若main指向dist，必须先build，再测试/跳转
    - 将编译后的文件放在相同目录，只发布js，开发时用ts

- main
  - The `main` field is a module ID that is the primary entry point to your program. 
  - That is, if your package is named `foo`, and a user installs it, and then does `require("foo")`, then your main module's exports object will be returned.
  - The key `main` refers to the standard from package.json, and `module` to a proposal to allow the JavaScript ecosystem upgrade to use ES2015 modules without breaking backwards compatibility.
- browser
  - If your module is meant to be used client-side, the `browser` field should be used instead of the `main` field. 
  - This is helpful to hint users that it might rely on primitives that aren't available in Node.js modules
- module
  - This is used by bundler tools for ESM (ECMAScript Module) detection. 
  - The `main` field makes sure that Node users using require will be served the UMD version. 
  - The `module` field is not an official npm feature but a common convention among bundlers to designate how to import an ESM version of our library.
  - The `module` property should point to a script that utilizes ES2015 module syntax but no other syntax features that aren't yet supported by browsers or node. 
  - This enables webpack to parse the module syntax itself, allowing for lighter bundles via tree shaking if users are only consuming certain parts of the library.
# npm-utils
- [npmjs.com displays per-version download counts](https://github.blog/changelog/2021-01-27-npmjs-com-displays-per-version-download-counts/)

- [npmgraph - enter npm module name to see the dependency graph](https://npmgraph.js.org/)

- https://github.com/plantain-00/clean-scripts
  - A CLI tool to make scripts in package.json clean.
  - 支持任务依赖

- https://github.com/ranyitz/qnm /202309/ts
  - cli utility for querying the node_modules directory
  - Current solutions like running `npm list` are slow and produce a lot of irrelevant output. 
  - It supports both npm and yarn and allows you to quickly identify the versions of the modules you are interested in.
  - Explain why a package was installed
  - Supports monorepos

- typesync
  - Install missing TypeScript typings for dependencies in your package.json

- syncpack

- private-npm-registry
  - https://github.com/verdaccio/verdaccio

- https://github.com/sk770/npm-offline-packager /MIT/202011/js
  - Fetch and publish npm packages for private npm registry
  - A CLI tool to download and publish NPM packages tarboll (with all dependencies) for offline npm registry (verdaccio, artifactory, etc.)
# workspaces
- ref
  - [docs: workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces)
  - [rfc: npm workspaces](https://github.com/npm/rfcs/blob/latest/implemented/0026-workspaces.md)

- Workspaces is a generic term that refers to the set of features in the npm cli that provides support to managing multiple packages from your local files system from within a singular top-level, root package.
  - This set of features makes up for a much more streamlined workflow handling linked packages from the local file system. 
  - Automating the linking process as part of `npm install` and avoiding manually having to use `npm link` in order to add references to packages that should be symlinked into the current `node_modules` folder.
  - We also refer to these packages being auto-symlinked during `npm install` as a single workspace, 
  - meaning it's a nested package within the current local file system that is explicitly defined in the `package.json` `workspaces` configuration.

- Managing individual versions in a monorepo is really hard. 
  - https://twitter.com/devongovett/status/1294367192754950144
  - Even tools like lerna basically assume you bump all changed packages in lock-step.
  - Feels like a case where an actual UI is better than a CLI. Started building a basic one for our needs.
- Have a look at Microsoft Rush. It has versioning, changelogs and monorepos absolutely nailed. I've completely dropped lerna.
  - How much does it require you to buy into their way of doing things? Would it be difficult to move over from yarn workspaces/lerna?
  - It depends how complex your setup with lerna is. It supports pnpm, yarn and npm. I would say that it's fairly opinionated, but the opinions are quite in line with lerna's usage patterns. The docs focus on a migration making testing it out with minimal work easy
  - What is a bit different is the publish steps. Open a PR, make changes 'rush change' to generate diff and change log + define versions.
    - Then you publish and it makes changelogs, tags, merges... So smooth and robust.
    - Doing the same with lerna always felt like fingers crossed!
- Combination of commitizen and conventional commits allowed my last team to determine versions automatically, 
  - it actually worked really well - but you have to be a stickler about commit messages
- If modules leave in a single repo, they are probably very coupled and it makes sense to release them all together.
  - If that's not the case, should they move into separate repos?
- I ended up ditching lerna for a custom publish script that determines the changed package from the changed directory, 
  - and the semver bump based on the commit message. 
  - Works pretty well because each version is an aggregate of many commits, I just don't need to think about it.

- pnpm has built-in support for monorepos (a.k.a. multi-package repositories, multi-project repositories, or monolithic repositories). 
  - You can create a workspace to unite multiple projects inside a single repository.
  - A workspace must have a pnpm-workspace.yaml file in its root.
# mirror/proxy
- https://github.com/Pana/nrm /MIT/202111/js/inactive
  - NPM registry manager, fast switch between different registries: npm, cnpm, nj, taobao

- https://github.com/zjunbin1286/npm-registry-nrs /202404/js
  - npm 源管理器，允许你快速地在 npm 源间切换

- https://github.com/cnpm/binary-mirror-config
  - Binary mirror config for prebuild and node-pre-gyp

- https://github.com/gucong3000/mirror-config-china /MIT/202305/js
  - 为中国内地的Node.js开发者准备的镜像配置，大大提高node模块安装速度
  - 支持Windows和其他操作系统
  - 🍴 forks
  - https://github.com/cloudyan/npm-config-china
# yarn
- [Yarn doesn't read from .npmrc Files for custom registry settings · yarnpkg/yarn](https://github.com/yarnpkg/yarn/issues/606)
  - fallback to npm config if it exists after getting default yarn config value
# lerna
- 优点
  - 安装依赖时自动link
    - workspace也可以实现，扁平化依赖减少重复下载和体积
  - bump version：若package A变了，依赖A的其他package也会变
    - independent的版本需要额外说明兼容范围
    - fixed的版本经常加入不必要的升级
  - publish：可配置registry
    - I'd like to use conventional commits for changelogs, not atlassian/changesets
  - 批量执行命令
    - build
  - 统一团队工作流
    - version bump -> changelog -> git release -> npm publish
    - 统一依赖版本
    - 统一更新项目版本、commit规范，但可能不会每步都需要

- 缺点
  - monorepo难以利用tsc的增量编译
  - 非父子结构文件夹时难以共享babel配置
  - apply `nohoist` to all modules that contain native code (ios & android code)

- Ah I'd very much encourage you to move from having lerna manage the monorepo to having yarn workspaces do it. 
  - You can still use all the other lerna helpers, but yarn handles the inter-package links way better. 
  - I almost never have to delete node_modules any more.

- I'm using Lerna currently, but the way its change detection works results in lots of unnecessary publishes.
# more
- [npm v7 Series - Beta Release!](https://blog.npmjs.org/post/626173315965468672/npm-v7-series-beta-release-and-semver-major)
- [Simplify your monorepo with npm 7 workspaces](https://dev.to/limal/simplify-your-monorepo-with-npm-7-workspaces-5gmj)
  - The most common reason to set up a monorepo is to streamline work within a dev team that maintains multiple apps that are using a shared piece of code, for example a common User Interface library.
  - Just remember that npm has a different philosophy than yarn. 
    - For example you cannot run a script inside a workspace from the monorepo's root folder.
- [pounchdb Remove Lerna_201608](https://github.com/pouchdb/pouchdb/issues/5545)
  - we can remove our Lerna dependency and vastly speed up our build times by avoiding lerna bootstrap.
  - We already don't use Lerna for building (because lerna run is slow due to running multiple processes, so I wrote one big top-level build script) 
  - or for publishing (because I didn't take enough time to grok the Lerna docs on this, we're not using version: independent, and I found a bash loop with npm publish to be simpler)
- [Why we dropped Lerna from PouchDB](https://gist.github.com/nolanlawson/457cdb309c9ec5b39f0d420266a9faa4)
  - We dropped Lerna from our monorepo architecture in PouchDB 6.0.0
  - `lerna bootstrap`, which links all of your sub-packages together so you can easily test them without a lot of `npm link`ing.
  - For `lerna boostrap`, we were actually using this in PouchDB, and this was the main benefit we were getting out of Lerna.
  - For `lerna run`, we were originally using it to run Rollup in each sub-package, 
    - but quickly realized that with ~30 packages, running 30 Node processes for each one (i.e. doing npm run build 30 times) was too slow. 
    - It made more sense to just write one big build.js script that built each sub-package inside of a single Node process.
  - For `lerna publish`, we actually don't use Lerna's "independent" mode (which is what Babel uses. correction: Babel uses "locked" mode).
    - Independent mode would mean that every sub-package would have its own semver and would get updated accordingly when its dependencies got updated, 
    - but we figured this would be way too complicated for PouchDB users, 
    - and it was simpler to just lock everything to a single version. 
    - Therefore we didn't really need `lerna publish`
    - we could just run `npm publish` in a loop, and that was good enough (along with a script to update the version number in every `package.json`, which is equally easy to write).
  - we could avoid `lerna bootstrap` entirely by simply renaming the `packages/` folder to `packages/node_modules`. 
    - Because of how the `require()` algorithm works, any reference to e.g. `require('pouchdb-ajax')` from within `packages/node_modules/pouchdb` will resolve to `packages/node_modules/pouchdb-ajax`, 
    - because `require()` just walks up the file tree until it finds a `node_modules` folder with a sub-folder that matches the package name. 
    - This cuts out the lerna boostrap step, which shaved about 30 seconds off of our npm install time(which is huge when we have dozens of Travis builds).
  - Using the "Alle" model also allowed us to move all of the sub-package's dependencies up to the top-level package.json
  - We actually don't use `lerna run` either in Babel. You can just build with your own script/gulp task on a glob.
  - I like this idea but wonder if it can be easily extended to use yarn workspaces to do the linking for you
- [The highs and lows of using Lerna to manage your JavaScript projects_201709](https://hackernoon.com/the-highs-and-lows-of-using-lerna-to-manage-your-javascript-projects-ff5c5cd82a99)
  - Why it can be annoying
  - If you have a lot of dependencies in each application, bootstrapping can take a very long time.
  - Tests take a long time to run and lose syntax highlighting.
  - Ways of working with one gigantic repo.
- [Why you should switch from Lerna to Nx_201909](https://blog.nrwl.io/why-you-should-switch-from-lerna-to-nx-463bcaf6821)
  - Babel, Angular, React, Jest and many other open source projects switched to using monorepos. Many of them use Lerna
  - We built Nx based on our experience of working at Google. I like to think of it as the Webpack of monorepo tools.
  - Monorepos are useful for both open source projects and companies building applications.
  - A monorepo for an open source project can consist of a dozen similar packages, built by a single team using similar tools.
  - A monorepo for an organization can consist of hundreds of packages, many of them are applications, built by multiple independent team using different tools.
  - Lerna is optimized for the former. Nx is optimized for the latter.
- [团队工程实践 - 基于lerna打造monorepo工作流](https://juejin.im/post/6894434733355188232)
