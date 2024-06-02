---
title: toc-app-github-xp
tags: [devtools, github, pm, xp]
created: 2020-07-31T11:59:56.787Z
modified: 2023-02-08T10:46:26.912Z
---

# toc-app-github-xp

# guide
- tips
  - 下载慢先尝试修改dns，或将 git://github.com/ 前缀替换成 https://github.com/
# git-usage
- 统计仓库人员贡献比例
  - git shortlog -sn
    - 统计每人commit次数
# github-usage
- github邮箱帐号绑定
  - commit的帐号
  - npm相关

- preview html
  - https://github.com/htmlpreview/htmlpreview.github.com
  - https://htmlpreview.github.io/?https://github.com/Futur3Sn0w/materialyou/blob/main/index.html
  - It is a client-side solution using a CORS proxy to fetch assets.
  - 对于那些没有将repo作为github pages托管网站的，可加上前缀直接在浏览器查看网页内容，而不是查看源码

- 排行榜
  - [GitHub-Chinese-Top-Charts](https://github.com/kon9chunkit/GitHub-Chinese-Top-Charts)
  - [Github User Ranking 中国和全球用户排名](https://github.com/jaywcjlove/github-rank)
  - [GitHub star ranking for users, organizations and repositories](https://github.com/k0kubun/gitstar-ranking)
    - https://gitstar-ranking.com/

- license
  - 先检查确保只存在一个文件，其名称中包含license单词，可以是license.txt/md，不能是wiki-license.md
  - 若要给没有license文件的repo添加license，直接本地上传一个即可
  - 若要给已有license文件的repo修改license，修改后可能github显示不出来，可以先删除再上传新的

## nice-to-have

- 空仓库标记，如搜索时标记出空仓库可省去点开查看
- 搜索时显示 latest-push-time, 而不是bot机器人push的时间，方便判断废弃仓库
- 若仓库是一个library，查找依赖本仓库的仓库中star最多的，没必要如此做，关注重点依赖即可
  - https://github.com/hacker-DOM/github-by-stars
    - /inactive
- repo项目名支持中文名，url中部分path支持中文名

- GitHub 的这个 Used by 不能按 star 排序，导致我没法好奇到底哪些项目在用这个包
  - https://twitter.com/0xhyoban/status/1746737169220383227
  - https://izon.vercel.app/
  - https://github.com/nvuillam/github-dependents-info /202401/python
  - https://github.com/github-tooling/ghtopdep /202212/python/inactive

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

## unsupported

- [Bring back `sort:indexed` for code searches](https://github.com/orgs/community/discussions/52932)
  - NA
# 🔍 search
- [Github search cheatsheet from official docs](https://gist.github.com/bonniss/4f0de4f599708c5268134225dda003e0)

## not-yet

- 搜索名称为folder11的文件夹

- 搜索repo名称包含关键词如directus的用户，按仓库数量最多排序，可发现directus的爱好者
  - 甚至可以再按年份排序

- [Search & Sort by number of commits ](https://github.com/orgs/community/discussions/63611)
  - For now, Most forks, Most Stars might be alternatives

## search-issues/pr

- is:unmerged

- 对于更名后的repo，issues中的auto linking仍然连接到更名前repo的url，可以在hovercard中提示

- 搜索自己评论过的issues `commenter:uptonking type:issue`; 
  - https://github.com/search?o=desc&q=commenter%3Auptonking+type%3Aissue&s=updated&type=Issues

- search-issues/discussions
  - 搜索仓库时指定语言后，当下搜索结果中的issues也是指定语言的

## search-code

- resources
  - [Understanding GitHub Code Search syntax - GitHub Docs](https://docs.github.com/en/search-github/github-code-search/understanding-github-code-search-syntax)

- A bare term with no qualifiers will match either the content of a file or the file's path.
  - Searching for multiple terms separated by whitespace is the equivalent to the search `hello AND world`.
  - Other boolean operations, such as `hello OR world`, are also supported.

- To search for an exact string, including whitespace, you can surround the string in quotes. You can also use quoted strings in qualifiers
  - `"sparse index" path:git language:"protocol buffers"`
- to find the exact string name = "tensorflow", use `"name = \"tensorflow\""`

- `NOT is:fork` 排除fork

- To search within a set of repositories, you can combine multiple repo: qualifiers with the boolean operator OR
  - `repo:github-linguist/linguist OR repo:tree-sitter/tree-sitter`

- To narrow down to a specific languages, use `language:ruby OR language:cpp OR language:csharp`

- Path qualifier
  - `path: qualifier` will match files containing the term anywhere in their file path. 
  - `path:unit_tests` 可搜索文件名和文件夹名
- To match only a specific filename (and not part of the path), use `path:/(^|\/)README\.md$/`
- You can also use some limited glob expressions in the path: qualifier.
  - `path:src/*.js` : search for JavaScript files within a `src` directory
  - By default, glob expressions are not anchored to the start of the path, so the above expression would still match a path like `app/src/main.js`. 
  - But if you prefix the expression with `/`, it will anchor to the start. For example: `path:/src/*.js`

- All parts of a search, such as search terms, exact strings, regular expressions, qualifiers, parentheses, and the boolean keywords AND, OR, and NOT, must be separated from one another with spaces. 
  - The one exception is that items inside parentheses `( )`, don't need to be separated from the parentheses.

## search-repos

- resources
  - [Searching for repositories - GitHub Docs](https://docs.github.com/en/search-github/searching-on-github/searching-for-repositories)

- Search is not case sensitive.

- If your search query contains whitespace, you will need to surround it with quotation marks.
  - `react NOT "hello world"` matches repositories with the word "react" but not the words "hello world."
  - `build label:"bug fix"` matches issues with the word "build" that have the label "bug fix."

- `in:repoName/desc/topics/readme`; 
  - When you omit this qualifier, only the repository name, description, and topics are searched.

- 搜索时的变通方法
  - 在github直接搜索导入库的代码 import from react，再限制语言如js
  - 搜索独特关键词 data-mdc-auto-init 的代码，而不是repositories
  - 对于最新的库或版本，直接搜索import是最准确的方式

- 搜索代码的变通方式 filename
  - ~~可作为查找dependents被依赖被使用项目的一种变通方式~~
  - react-table filename:package.json
    - 此时搜索的是 Code，而不是 Repositories
    - 新版搜索要将filename改为path
  - 甚至可以搜索同时包含多个依赖的仓库
    - https://github.com/search?q=%22next-mdx-enhanced%22+%22%40tailwindcss%2Ftypography%22+filename%3Apackage.json&type=Code

- 搜索条件使用日期 pushed:>=2021-11-11
  - editor created:<2011-01-01 
  - editor pushed:>=2013-03-06 fork:only 
- 搜索指定日期范围内仓库
  - react-table in:name language:javascript  pushed:2020-10-01..2020-12-05 fork:only
  - Hooks for building fast and extendable tables and datagrids for React in:description language:javascript  pushed:2020-10-01..2020-12-05 fork:only

- To exclude all results that are matched by a qualifier, prefix the search qualifier with a hyphen `-`.
  - `mentions:uptonking -org:github`

- 搜索js或ts的项目 language:javascript language:typescript
  - `https://github.com/search?o=desc&q=data+grid+language%3Ajavascript+language%3Atypescript&s=updated&type=Repositories`
  - `https://api.github.com/search/repositories?q=angular+language:javascript+language:typescript&per_page=5&page=1`

- 搜索一个organization的仓库，可使用 `user/org:orgName` ，注意冒号后无空格
  - https://github.com/search?o=desc&q=user%3A+pentaho&s=stars&type=Repositories
- 搜索org，可用`type:org`
  - `https://github.com/search?q=design+type%3Aorg&type=users`
  - 既可以搜索出repositories，也可以搜索出org类型的users

- 按标签或主题搜索
  - topics
  - awesome类型的repositories

- 搜索收藏最多的仓库，可使用 `stars:>1` ，然后再排序
  - most starred/forked

## search-forks

- To include forks in the search results, you will need to add `fork:true` or `fork:only`

- 查找一个仓库最活跃的fork仓库
  - https://github.com/techgaun/active-forks
    - https://techgaun.github.io/active-forks/index.html
  - https://github.com/useful-forks/useful-forks.github.io
    - https://useful-forks.github.io/
# github-actions
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
# github-mirrors/proxy
- [Gitee极速下载，每日同步一次](https://gitee.com/mirrors)
  - https://gitee.com/organizations/mirrors/projects

- github-mirrors
  - https://hub.nuaa.cf/
  - https://github.wuyanzheshui.workers.dev/

- git-only
  - https://github.zhlh6.cn/
    - git clone git@git.zhlh6.cn:tinyplex/tinybase.git
  - https://gitclone.com/
- github proxy(解决下载慢的问题)
  - http://g.widyun.com/
  - https://d.serctl.com/

- git-download
  - https://gh.api.99988866.xyz/
  - https://ghproxy.com/
  - http://toolwa.com/github/

- dead?
  - https://hub.fastgit.xyz/

- questions
  - google-search github 镜像 一月内
  - [Github国内镜像网站，解决Github访问的神器 - 知乎](https://zhuanlan.zhihu.com/p/360677731)

- [Using a socks proxy with git for the http transport - Stack Overflow](https://stackoverflow.com/questions/15227130/using-a-socks-proxy-with-git-for-the-http-transport)
  - ALL_PROXY=socks5://127.0.0.1:1080 git clone https://github.com/some/one.git
  - If you also want the host name to be resolved using the proxy, use thuzhf's solution below, which uses socks5h instead of socks5

- https://github.com/521xueweihan/GitHub520
  - https://raw.hellogithub.com/hosts 服务器续费了3年到2024.12
- https://github.com/ineo6/hosts
  - https://gitlab.com/ineo6/hosts
  - 通过修改host的方式加速GitHub访问，解决图片无法加载以及访问速度慢的问题。
  - 域名对应的ip与github520基本相同

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

- https://github.com/amplemarket/github-repo-size-public
  - display repository size on GitHub
# github-theming
- https://github.com/imfunniee/gitfolio
  - https://imfunniee.github.io/gitfolio/
  - personal website + blog for every github user
  - 重新组织了个人信息
# apps
- https://github.com/devhubapp/devhub /ts
  - TweetDeck for GitHub - Filter Issues, Activities & Notifications 
  - Web, Mobile & Desktop with 99% code sharing between them
# discuss-xp-github
- ## 

- ## 分享一个做过的小工具：github star统计（https://stars.yangerxiao.com）。
- https://x.com/wsygc/status/1797163494170918985
  - 当时有个小需求：想知道某个 github 项目下每日新增多少 star，网上找了一通，没找到，于是自己就做了个，算是填补了某个需求的空白。
  - 因为要分页拉取数据，所以会多次调用Github API，而Github API每天是有调用次数限制的，有一天有人联系上我，说这个小工具出bug啦，真是又惊又喜：嘿，还真有人用，而且还把API次数用完了。不过这个限制避免不了，于是就“贴心”地加了个“API余额”小飘窗

- 为什么不是付费增加限额的 pop windows?
  - 因为付费也增加不了限额, 代码都是开源的, 可以自己部署一个

- https://star-history.com 这个好像很早了吧

- ## 今天知道了 github 有个用 https 的 443 端口使用 ssh 协议的服务 http://ssh.github.com。
- https://twitter.com/_a_wing/status/1750177058872054083
  - 这样就可以在被禁了 22 端口的情况下继续用 ssh 协议来传输代码了
- 我第一次用这个端口是因为机场被SSH爆破，然后机场主一声不吭把所有路线的22端口全给关了，被迫查了资料才知道原来还有这个端口解了燃眉之急把代码推上去
- 嗯，而且这个域名 22 和 443 都能走
