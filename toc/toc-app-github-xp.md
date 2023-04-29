---
title: toc-app-github-xp
tags: [devtools, github, pm, xp]
created: 2020-07-31T11:59:56.787Z
modified: 2023-02-08T10:46:26.912Z
---

# toc-app-github-xp

# guide

# github-mirror
- tips
  - 先尝试，修改dns，将 git://github.com 前缀替换成 https://github.com/

- [Gitee 极速下载，每日同步一次。](https://gitee.com/mirrors)
  - https://gitee.com/organizations/mirrors/projects

- github-mirrors
  - https://hub.nuaa.cf/

- git-only
  - https://github.zhlh6.cn/
    - git clone git@git.zhlh6.cn:tinyplex/tinybase.git
  - https://gitclone.com/

- git-download
  - https://gh.api.99988866.xyz/
  - https://ghproxy.com/
  - http://toolwa.com/github/

- dead?
  - https://hub.fastgit.xyz/

- questions
  - search github 镜像 一月内
  - [Github国内镜像网站，解决Github访问的神器 - 知乎](https://zhuanlan.zhihu.com/p/360677731)

- [Using a socks proxy with git for the http transport - Stack Overflow](https://stackoverflow.com/questions/15227130/using-a-socks-proxy-with-git-for-the-http-transport)
  - ALL_PROXY=socks5://127.0.0.1:1080 git clone https://github.com/some/one.git
  - If you also want the host name to be resolved using the proxy, use thuzhf's solution below, which uses socks5h instead of socks5
# improvements
- github-release
  - app store
  - pkg store

- features
  - navigation within issue answers with shortcut J
  - sort repos of an organization by stars
  - toggle github repo and github page
  - go to npm package page

- file-manager
  - 文件列表的日期，高亮最近日期
# git-usage
- 统计仓库人员贡献比例
  - git shortlog -sn
    - 统计每人commit次数
# github-usage
- nice-to-have
  - 空仓库标记，如搜索时标记出空仓库可省去点开查看
  - 搜索时显示 latest-push-time, 而不是bot机器人push的时间，方便判断废弃仓库
  - 若仓库是一个library，查找依赖本仓库的仓库中star最多的，没必要如此做，关注重点依赖即可
    - https://github.com/hacker-DOM/github-by-stars
      - /inactive
  - repo项目名支持中文名，url中部分path支持中文名
# github-search
- search-pr
  - is:unmerged

- search-code
  - NOT is:fork 排除fork

- search-repos
  - 搜索时变通的方法
    - 在github直接搜索导入库的代码 import from react，再限制语言如js
    - 或者搜索独特关键词 data-mdc-auto-init 的代码，而不是repositories
    - 对于最新的库或版本，直接搜索import是最准确的方式
  - 搜索代码的变通方式 filename:
    - ~~可作为查找dependents被依赖被使用项目的一种变通方式~~
    - react-table filename:package.json
      - 此时搜索的是 Code，而不是 Repositories
      - 新版搜索要将filename改为path
    - 甚至可以搜索同时包含多个依赖的仓库
      - https://github.com/search?q=%22next-mdx-enhanced%22+%22%40tailwindcss%2Ftypography%22+filename%3Apackage.json&type=Code
  - 搜索条件使用日期 pushed:>=2021-11-11
    - react created:<2011-01-01 
    - editor pushed:>=2013-03-06 fork:only 
  - 搜索指定日期范围内仓库
    - react-table in:name language:javascript  pushed:2020-10-01..2020-12-05 fork:only
    - Hooks for building fast and extendable tables and datagrids for React in:description language:javascript  pushed:2020-10-01..2020-12-05 fork:only
  - 搜索js或ts的项目 language:javascript language:typescript
    - `https://github.com/search?o=desc&q=data+grid+language%3Ajavascript+language%3Atypescript&s=updated&type=Repositories`
    - `https://api.github.com/search/repositories?q=angular+language:javascript+language:typescript&per_page=5&page=1`
  - 搜索一个organization的仓库，可使用 `user/org:orgName` ，注意冒号后无空格
    - https://github.com/search?o=desc&q=user%3A+pentaho&s=stars&type=Repositories
  - 搜索org，可用`type:org`
    - `https://github.com/search?q=design+type%3Aorg&type=users`
    - 既可以搜索出repositories，也可以搜索出org类型的users
  - 搜索自己评论过的issues `commenter:uptonking type:issue`
    - https://github.com/search?o=desc&q=commenter%3Auptonking+type%3Aissue&s=updated&type=Issues
  - 按标签或主题搜索
    - topics
    - awesome类型的repositories
  - 搜索收藏最多的仓库，可使用 `stars:>1` ，然后再排序
    - most starred
      - https://github.com/search?q=stars%3A%3E100&s=stars&type=Repositories
    - most forked
      - https://github.com/search?o=desc&q=stars:%3E1&s=forks&type=Repositories

- fork
  - 可利用高级搜索，搜索fork仓库中最新被fork的 `fork:only`
  - 查找一个仓库最活跃的fork仓库
    - https://github.com/techgaun/active-forks
      - https://techgaun.github.io/active-forks/index.html
    - https://github.com/useful-forks/useful-forks.github.io
      - https://useful-forks.github.io/

- preview html
  - https://github.com/htmlpreview/htmlpreview.github.com
  - https://htmlpreview.github.io/?https://github.com/Futur3Sn0w/materialyou/blob/main/index.html
  - It is a client-side solution using a CORS proxy to fetch assets.
  - 对于那些没有将repo作为github pages托管网站的，可加上前缀直接在浏览器查看网页内容，而不是查看源码

- issues
  - 对于更名后的repo，issues中的auto linking仍然连接到更名前repo的url，可以在hovercard中提示

- tips

- 排行榜
  - [GitHub-Chinese-Top-Charts](https://github.com/kon9chunkit/GitHub-Chinese-Top-Charts)
  - [Github User Ranking 中国和全球用户排名](https://github.com/jaywcjlove/github-rank)
  - [GitHub star ranking for users, organizations and repositories](https://github.com/k0kubun/gitstar-ranking)
    - https://gitstar-ranking.com/

- license
  - 先检查确保只存在一个文件，其名称中包含license单词，可以是license.txt/md，不能是wiki-license.md
  - 若要给没有license文件的repo添加license，直接本地上传一个即可
  - 若要给已有license文件的repo修改license，修改后可能github显示不出来，可以先删除再上传新的

- github.com site proxy
  - https://hub.fastgit.xyz

- github proxy(解决下载慢的问题)
  - http://g.widyun.com/
  - https://d.serctl.com/
- github mirror
  - https://github.wuyanzheshui.workers.dev/

- ref
  - [Automated Data Scraping with Github Actions](https://www.swyx.io/github-scraping/)
    - https://github.com/sw-yx/gh-action-data-scraping
# github-utils-repos-pkg-npm
- 查看依赖某个package的所有包
  - https://www.npmjs.com/browse/depended/redux
  - [Allow dependents to be sorted by stars](https://github.com/isaacs/github/issues/1537)
    - ghtopdep
    - source-reader

- 查看某个作者的所有包
  - https://www.npmjs.com/~tannerlinsley
- 查看某个组织的所有包
  - https://www.npmjs.com/org/spectrum-css

- 读取某个package的所有dependencies，查询下载量后排序
  - https://github.com/pkgjs/dependents

- https://github.com/tj/git-extras
  - GIT utilities -- repo summary, repl, changelog population, author commit percentages and more
  - git summary --line
    - 统计每人代码比例

- https://github.com/oleander/git-fame-rb
  - git fame 
    - summarize and pretty-print collaborators, based on the number of contributions.

- https://github.com/IonicaBizau/git-stats
  - Local git statistics including GitHub-like contributions calendars.
# github-proxy
- https://github.com/521xueweihan/GitHub520
  - https://raw.hellogithub.com/hosts 服务器续费了3年到2024.12

- download release and repo
  - https://pd.zwc365.com/
  - https://shrill-pond-3e81.hunsh.workers.dev/
# github-api
- https://github.com/octokit/core.js
  - Extendable client for GitHub's REST & GraphQL APIs
  - If you don't need the Plugin API then using @octokit/request or @octokit/graphql directly is a good alternative.
# github-browser-extensions
- https://github.com/octokit/octokit.js
  - The all-batteries-included GitHub SDK for Browsers, Node.js, and Deno.

- https://github.com/Mottie/GitHub-userscripts
  - Userscripts to add functionality to GitHub

- https://github.com/dwyl/hits-nodejs
  - to see how many people have viewed your GitHub Repository
# github-theming
- https://github.com/imfunniee/gitfolio
  - https://imfunniee.github.io/gitfolio/
  - personal website + blog for every github user
  - 重新组织了个人信息
