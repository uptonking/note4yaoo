---
title: pm-dev-xp-github
tags: [devtools, github, pm, xp]
created: '2020-07-31T11:59:56.787Z'
modified: '2021-06-02T18:26:20.133Z'
---

# pm-dev-xp-github

# github-usage

- nice-to-have
  - 空仓库标记，如搜索时标记出空仓库可省去点开查看
  - 搜索时显示 latest-push-time, 而不是bot机器人push的时间，方便判断废弃仓库
  - 若仓库是一个library，查找依赖本仓库的仓库中star最多的，没必要如此做，关注重点依赖即可
    - https://github.com/hacker-DOM/github-by-stars
      - /inactive
  - repo项目名支持中文名，url中部分path支持中文名

- search
  - 搜索时变通的方法
    - 在github直接搜索导入库 import from react，再限制语言如js
    - 或者搜索关键词 data-mdc-auto-init 的 code，而不是repositories
  - 搜索使用js或ts的项目
    - `https://github.com/search?o=desc&q=data+grid+language%3Ajavascript+language%3Atypescript&s=updated&type=Repositories`
    - `https://api.github.com/search/repositories?q=angular+language:javascript+language:typescript&per_page=5&page=1`
  - 搜索一个organization的仓库，可使用 `user/org:orgName` ，注意冒号后无空格
    - https://github.com/search?o=desc&q=user%3A+pentaho&s=stars&type=Repositories
  - 搜索org，可用`type:org`
    - `https://github.com/search?q=design+type%3Aorg&type=users`
  - 搜索自己评论过的issues `commenter:uptonking type:issue`
    - https://github.com/search?o=desc&q=commenter%3Auptonking+type%3Aissue&s=updated&type=Issues
  - 按标签或主题搜索
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

- github proxy(解决下载慢的问题)
  - http://g.widyun.com/
  - https://d.serctl.com/
- github mirror
  - https://github.wuyanzheshui.workers.dev/

- ref
  - [Automated Data Scraping with Github Actions](https://www.swyx.io/github-scraping/)
    - https://github.com/sw-yx/gh-action-data-scraping
# github-pkg-npm
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
# github-proxy
- download release and repo
  - https://pd.zwc365.com/
  - https://shrill-pond-3e81.hunsh.workers.dev/
# github-data-apps
- https://githubwrapped.tech/
  - take a look at all the contributions you as an individual made to the open-source community

- https://copilot.github.com/
  - With GitHub Copilot, get suggestions for whole lines or entire functions right inside your editor.
  - https://twitter.com/fabiospampinato/status/1409956406745255936
  - Autopilot seems cool but:
    - Most of the time is spent thinking not typing.
    - Autocomplete is predictable, Autopilot much less so.
    - Spotting issues is IMO harder when reading code than when writing it.
    - You want perfect code, not code that the average dev would write.
