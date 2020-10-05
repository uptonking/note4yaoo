---
title: tool-app-github-tips
tags: [app, github, tool]
created: '2020-07-31T11:59:56.787Z'
modified: '2020-10-05T07:52:42.228Z'
---

# tool-app-github-tips

## github

- 搜索
  - 搜索一个organization的仓库，可使用 `user:orgName` ，注意冒号后无空格
    - https://github.com/search?o=desc&q=user%3A+pentaho&s=stars&type=Repositories
  - 按标签或主题搜索
  - 搜索收藏最多的仓库，可使用 `stars:>1` ，然后再排序
    - most starred
      - https://github.com/search?q=stars%3A%3E100&s=stars&type=Repositories
    - most forked
      - https://github.com/search?o=desc&q=stars:%3E1&s=forks&type=Repositories

- fork
  - 查找一个仓库最活跃的fork仓库
    - https://github.com/techgaun/active-forks
    - https://techgaun.github.io/active-forks/index.html

- usage
  - 若仓库是一个library，查找依赖本仓库的仓库中star最多的
    - https://github.com/hacker-DOM/github-by-stars

- 排行榜
  - [GitHub-Chinese-Top-Charts](https://github.com/kon9chunkit/GitHub-Chinese-Top-Charts)
  - [Github User Ranking 中国和全球用户排名](https://github.com/jaywcjlove/github-rank)
  - [GitHub star ranking for users, organizations and repositories](https://github.com/k0kubun/gitstar-ranking)
    - https://gitstar-ranking.com/

## ecosystem

- npm
  - 读取一个package的所有dependencies，查询下载量后排序
    - https://github.com/pkgjs/dependents
  - [most depended upon packages](https://www.npmjs.com/browse/depended)
    - lodash, react, chalk, request, moment, express, axios, debug, bluebird
    - uuid, classnames, yargs, webpack, rxjs, glob, jquery, node-fetch
    - redux, styled-components, ramda, jest, socket.io, redis, chokidar
    - deepmerge, date-fns, marked, isomorphic-fetch
