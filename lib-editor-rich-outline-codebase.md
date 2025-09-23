---
title: lib-editor-rich-outline-codebase
tags: [codebase, outline-wiki]
created: 2021-09-09T20:54:15.243Z
modified: 2021-09-09T20:54:36.354Z
---

# lib-editor-rich-outline-codebase

# guide

- 对源码的处理
  - 重新写，参考最新代码
  - 大量改，参考旧版有许可的代码

- later
  - 文章内容存储到数据库的格式是文本字符串，参考payloadcms保存json

- run-starter
  - yarn install --frozen-lockfile
  - yarn build
  - yarn sequelize db:create --env=production-ssl-disabled
  - yarn dev/start

```sh
# yarn dev not working
yarn dev:watch
```

- open http://localhost:4400
# issues

# backend

# frontend
