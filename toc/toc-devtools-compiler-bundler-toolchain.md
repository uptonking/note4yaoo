---
title: toc-devtools-compiler-bundler-toolchain
tags: [compiler, devops, devtools, engineering, toc]
created: 2020-10-05T08:14:22.192Z
modified: 2022-11-01T01:05:07.873Z
---

# toc-devtools-compiler-bundler-toolchain

# guide

- transpile
  - babel, swc

- compiler
  - esbuild, wmr

- dev-server
# frontend-compiler
- https://github.com/JinJieTan/mini-webpack
  - 本文会先介绍webpack的打包流程，运行原理，然后去实现一个简单的webpack

- https://github.com/yangyfeng/mypack
  - 0、读取webpack.config.js
  - 1、解析文件依赖
  - 2、替换require为__webpack_require__
  - 3、本地使用{}存储所有的文件，然后通过使用为__webpack_require__获取文件内容，执行函数方式为evel的包裹代码字符串

- webpack
  - https://github.com/dykily/simple_webpack
  - https://github.com/gracehui88/HMR
  - https://github.com/pmmmwh/react-refresh-webpack-plugin
- https://github.com/jgraph/drawio
  - online diagramming tool
- https://github.com/evolus/pencil
  - tool for making diagrams and GUI prototyping
# test
- https://github.com/YMFE/yapi
  - /18.1kStar/Apache2/202010
  - 依赖mongodb、axios、json5、jsonwebtoken、koa、markdown-it、mockjs
  - YApi是dd一个可本地部署的、打通前后端及QA的可视化接口管理平台
  - features
    - 基于 Json5 和 Mockjs 定义接口返回数据的结构和文档
    - 扁平化权限设计
    - 类似 postman 的接口调试
    - 支持 postman, har, swagger 数据导入
    - 免费开源，内网部署
  - [开发不活跃，YApi开源项目作者，目前在美团优选工作](https://github.com/YMFE/yapi/issues/1173)
- RAP 阿里
  - https://github.com/thx/rap2-delos
  - /6.4kStar/MIT/202009
  - 依赖Koa、MySQL
  - https://github.com/thx/rap2-dolores
  - 依赖react、@material-ui/core、chart.js、codemirror、formik、jquery、react-redux
  - 阿里妈妈前端团队出品的开源接口管理工具RAP第二代
- https://github.com/NEIAPI/nei
  - https://nei.netease.com/
  - NEI 网易接口管理平台 源代码
  - 前端依赖：网易自研开源nej、regularjs
  - 后端依赖：koa、mysql、redis、mongodb
- https://github.com/trueleaf/moyu
  - 基于 Vue 和 Electron 的在线协同api接口管理工具。
  - 接口文档管理工具、接口工具、接口文档、api文档、api工具、快乐摸鱼
# database-manager
- https://github.com/405go/pdman
  - 开源免费的数据库模型建模工具
  - 是PowerDesigner之外，更好的免费的替代方案
# site
- https://github.com/jbake-org/jbake
  - Java based open source static site/blog generator
# java
- https://github.com/alibaba/arthas
  - Alibaba Java Diagnostic Tool
- https://github.com/RohitAwate/Everest
  - cross-platform REST client.
- https://github.com/zxh0/classpy
  - GUI tool for investigating Java class files
- https://github.com/vanzin/jEdit
  - copy of jEdit's repository from jedit.sourceforge.net.
- https://github.com/JFormDesigner/markdown-writer-fx
  - open source Markdown editor written in JavaFX 8.
