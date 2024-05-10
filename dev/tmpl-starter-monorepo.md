---
title: tmpl-starter-monorepo
tags: [engineering, starter]
created: 2020-11-24T10:42:09.474Z
modified: 2020-12-08T13:53:36.730Z
---

# tmpl-starter-monorepo
- 快速开始开发项目的模板
# frontend-spec
- [我是如何带领团队从零到一建立前端规范的？ - 掘金](https://juejin.cn/post/7085257325165936648)
  - 操作规范不是一开始定就行，需要在实际项目以及组员的表现进一步完善的
  - [前端团队如何做规范 - 掘金](https://juejin.cn/post/6963549273346539527)
  - [分享自定义前端web开发规范（命名、文本、开发、html、css、js、vue） - 掘金](https://juejin.cn/post/7052121157822054414)
  - [前端团队代码统一规范最佳实践 - 掘金](https://juejin.cn/post/7086383019551883272)
  - [前端团队需要的工程规范 - 掘金](https://juejin.cn/post/7091202054680985630)

- [前端规范指南，让团队代码如出一辙！ESLint + Prettier + husky + lint-staged](https://www.yuque.com/itwangtian/ycsiao/pe1n3uneypxse0fq)
  - [前端开发规范 高灯云产品前端基建小组](https://www.yuque.com/gmyoon/dfy2l5/zyhdyd)
  - [前端开发管理规范](https://www.yuque.com/ailun-ychwc/wp9stg/ks1vhg5w8g7u3thz)
  - [JDC 前端代码规范](https://jdf2e.github.io/jdc_fe_guide/docs/index/)
  - [阿里最新前端规范](https://www.yuque.com/qiaoxiansheng-fevtn/abx3hp/sehudq3iz9knpgdo)
  - [团队技术规范](https://www.yuque.com/ngcohau/pbupgq/yw1m3n)
  - [前端开发、联调、调试工具（推荐）](https://www.yuque.com/jimmie/web-cooperation-standard/yw02pg)

- [nanxiaobei/front-end-dev-guide: 前端开发行为指导规范](https://github.com/nanxiaobei/front-end-dev-guide)
  - 以应用业界最佳实践为佳

- https://github.com/alibaba/f2e-spec
  - https://alibaba.github.io/f2e-spec/zh/
  - 阿里巴巴集团内广泛使用的一套前端编码和工程规范，致力于通过统一编码风格、普及最佳实践和代码缺陷检查帮助团队降低协作成本、提升前端项目的可维护性和稳定性。
  - 本规约主要包括规约文档和规约工具两部分

- https://github.com/jd-antelope/s-lint
  - [原创：如何在前端团队快速制定并落地代码规范 · zxyue25/blog](https://github.com/zxyue25/blog/issues/8)
  - 第一步收集团队的技术栈情况，确定规范要包括的范围, 把规范梳理为三部分ESLint、StyleLint、CommitLint
  - 靠人来保证代码规范存在不可靠，且需要人为review代码不规范，效率低

- https://github.com/encode-studio-fe/fe-spec
  - https://encode-studio-fe.github.io/fe-spec/
  - 印客学院 前端编码规范工程化
  - 支持对全部前端配置实现一键接入、一键扫描、一键修复、一键升级
# popular
- [Create React App](https://github.com/facebook/create-react-app)
  - Create React apps with no build configuration by running one command 
- [electron-webpack](https://github.com/electron-userland/electron-webpack)
  - The primary aim of electron-webpack is to eliminate all preliminary setup with one simple install so you can get back to developing your application.
  - HMR for both renderer and main processes
# mono-nostalgia-studio
- 全局依赖 
  - typescript, ts-node, react, @types/node
  - nanoid
  - 暂不解决: rollup-[plugin]
# nx-tooling
- docs
  - [nx:run-commands | Nx](https://nx.dev/nx-api/nx/executors/run-commands)

- drawbacks
  - 难以修改next启动的端口，查看文档3小时都改不了
  - 不使用package.json会导致无法看清项目的deps
  - 为了命令能统一执行，自己在定义scripts/executor上另立规范
  - next-intl无法识别 next.config.mjs 的配置，只能用默认的cjs配置

- 
- 
- 
- 

# frontend-starter
- monorepo
  - 基于workspace、lerna、nx
  - 优点
    - 统一管理版本、构建流程
    - 统一devDependencies，减少开发工具的体积
  - 缺点
    - 各子项目的issues会杂糅在论坛

- todo
  - npm workspaces暂不支持使用`.`添加顶层包作为workspace
    - 临时方案：直接在顶层加代码，或在packages/*子目录再复制一份源码
  - jest测试中import三方包时优先根据main，可自定义defaultResolver and packageFilter设置优先使用module
    - jest-module-field-resolver使用module后react导入出现问题
    - 不能轻易改

- dependencies
  - 对于大多数重复的devDependencies，提升到顶层
  - npm 7过渡阶段，使用npm install --legacy-peer-deps避免冲突
  - 对于依赖冲突的版本
    - npm shrinkwrap
    - 采用类似yarn的Selective dependency resolutions指定具体版本，npm对应的非官方实现是pm-force-resolutions(不支持npm7)
    - [npm equivalent of yarn resolutions?](https://stackoverflow.com/questions/52416312/npm-equivalent-of-yarn-resolutions) (提供了自定义脚本)

- build
  - 编译tips
    - 不需单独编译的库可不编译
  - node
    - 使用ts-node时，main字段必须是.ts文件
  - tsc
    - 适合单独库
    - `tsc -p tsconfig.json --traceResolution`打印日志
  - babel
    - 不适合后面扩展到ts,css
    - 共享的babel配置文件建议放在顶层
    - babel-cli适合单独库，支持watch目录
    - babel-node is a CLI that works exactly the same as the Node.js CLI, with the added benefit of compiling with Babel presets and plugins before running it.
      - Due to technical limitations, ES6-style module-loading is not fully supported in a babel-node REPL.
    - 所有简单包的编译命令可相似甚至相同，`babel --root-mode upward src -d lib`
      - lerna-yarn-workspaces-monorepo-js
      - monorepo-babel-ts-lerna-starter
      - `BABEL_ENV=build babel src --root-mode upward --out-dir dist --source-maps --extensions .ts,.tsx --delete-dir-on-start --no-comments`
  - webpack/webpack-dev-server
    - 适合复杂应用，支持各种文件格式，易于实现基于module federation的微服务
    - 共享的webpack配置文件建议放在顶层，可在子项目中直接通过require相对路径读取
  - rollup
  - 编译参考
    - 还可以利用现有脚本如react-scripts-ts编译，但不直观

- test
  - jest
    - 测试monorepo时，import子目录包的main默认指向dist，不方便

- hot-reload
  - 不是简单的watch增量编译，而是修改后自动编译且应用状态数据保持

- lint
  - eslint: tslint已废弃
  - stylelint

- framework
  - vanillajs
  - react
  - vue
  - components

- css
  - css
  - scss
  - styled-components
  - css-in-js

- more-tools-required
  - prettier

---

- storybook
  - 展示单个组件的不同状态
  - 缺点
    - 最终展示的文档灵活性不够高
    - breaking changes太多

- more-tools-optional
  - vscode
  - github: issue-template, pr, code-conduct
