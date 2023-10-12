---
title: thread-devops-cicd
tags: [cicd, devops]
created: 2023-10-12T14:06:13.077Z
modified: 2023-10-12T14:06:30.848Z
---

# thread-devops-cicd

# guide

# discuss
- ## 

- ## 

- ## 优化 golang 项目 CICD 速度的技巧, CD 耗时爆降超过 50%
- https://twitter.com/jarredsumner/status/1712218329413489011
  - pr 的描述写的也非常好, 不仅有 how 还有 why
  - [ci: optimize build](https://github.com/Ehco1996/ehco/pull/242)
- 原来这个不用 push 中间镜像的写法是 Docker 文档建议的, 学到了新的合并镜像（不用 push 中间镜像）的技巧
- 学习了，还有这种操作，本来想法是该动docker，build两种架构的binary，然后分别copy到不同的镜像中，但是那样就没法buildx 了
- webp也分享过, 混合部署 GitHub Actions Runner：Multi Arch 镜像构建速度飙升 10 倍
