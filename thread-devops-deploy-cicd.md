---
title: thread-devops-deploy-cicd
tags: [cicd, deploy, devops]
created: 2023-10-12T14:06:13.077Z
modified: 2024-04-05T06:34:05.602Z
---

# thread-devops-deploy-cicd

# guide

# discuss-stars
- ## 

- ## CI/CD explained in simple terms.
- https://twitter.com/NikkiSiapno/status/1720810644713455793
  - [CI/CD Demystified — Build, Test, Deploy, Repeat](https://blog.levelupcoding.co/p/luc-26-cicd-demystified-build-test-deploy-repeat)
  - 使用流程图解释

# discuss-release-publish-changelog
- ## 

- ## I prefer keeping CHANGELOG.md in git for my open source projects.
- https://twitter.com/sitnikcode/status/1756657599485735044
  - But Github gives some handy features on top of Releases.
  - @edloidas wrote a script for Github Action to create a release when a new tag appears.

- I use Changesets for this. They have GHA to release packages to npm registry (and you can release packages for different languages too), update changelogs and create a release
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 修了一个有趣的 bug。之前 CI 一直稳过，还以为自己代码写得好呢，今天发现是有问题，挂了ci也认为过了。
- https://x.com/laixintao/status/1810629972715020606
  - 出问题的地方是 ci 脚本开子进程，子进程如果失败，直接用子进程的 return code 来 sys.exit()。 实际上如果code大于255 Python 就用0退出，神奇。

- 在我的 Linux 上，返回的值范围是 0 到 255，实际上的返回值是 result & 0xFF，而不是大于 255 返回 0
- 和python好像没关系，bash也是这样的 bash -c 'exit 257'; echo $?
- 你再测试下 257 和 258， 就会发现是 code & 0xFF

- ## 把静态网站，next.js 网站部署在 Cloudflare 上，和部署在 Vercel 上相比，有什么优势呢？
- https://twitter.com/xqliu/status/1775874477538320521
1. 大体上体验非常接近，包括 GitHub 导入、构建脚本支持、版本预览等等
2. Vercel 好处：
   1. 域名放在哪里都可以；
   2. 集成数据服务（KV，DB，Config）非常方便
   3. 团队管理更好用
3. CF 好处：
   1. 提供很好用的分析工具，包含 Web Vitals
   2. 免费额度更高
   3. 全球最近接入

- CF Workers 也有 KV 和 D1 做存储。
  - 不过 D1 不是基于 Postgresql 而是 Sqlite 的
- 昨天刚宣布了prisma集成，可以连第三方PG了

- 区别就是能在vercel跑起来的next项目在cloudflare有可能失败

- 静态随便，nextjs 的server 用cf的话，想連Postgres或者redis都不行。Vercel 则可以

- 超过免费额度后，Vercel 的费用远高于 Cloudflare。

- ## 优化 golang 项目 CICD 速度的技巧, CD 耗时爆降超过 50%
- https://twitter.com/jarredsumner/status/1712218329413489011
  - pr 的描述写的也非常好, 不仅有 how 还有 why
  - [ci: optimize build](https://github.com/Ehco1996/ehco/pull/242)
- 原来这个不用 push 中间镜像的写法是 Docker 文档建议的, 学到了新的合并镜像（不用 push 中间镜像）的技巧
- 学习了，还有这种操作，本来想法是该动docker，build两种架构的binary，然后分别copy到不同的镜像中，但是那样就没法buildx 了
- webp也分享过, 混合部署 GitHub Actions Runner：Multi Arch 镜像构建速度飙升 10 倍
