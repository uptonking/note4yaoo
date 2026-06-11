---
title: lib-db-app-community-security-auth
tags: [auth, community, database, security]
created: 2023-10-31T11:48:24.472Z
modified: 2023-10-31T11:48:54.805Z
---

# lib-db-app-community-security-auth

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-db-security
- ## 

- ## 

- ## 
# discuss-security-config/env/files
- ## 

- ## 

- ## 

- ## 

- ## You likely didn't know that Docker is building a native Secrets Engine.
- https://x.com/psviderski/status/2064675044681503086
  - The idea is to stop hardcoding plaintext secrets in .env or compose files. 
  - `docker run -e API_KEY=se://my/secret/key` ...
  - Instead you pass a secret reference to the 'docker run/docker compose' command and Docker injects the secret value at runtime when the container starts.
  - Secrets are sourced from a pluggable provider.
  - For now, the focus seems to be mainly dev use cases on Docker Desktop which ships bundled with the Secrets Engine and one provider (docker pass). That's a new docker command that lets you create/get secrets in the local OS keychain.

- It's weird that it took so long for docker to build this natively. 1Password and other pw managers have also done a great job with implementing developer related features.
# discuss-security
- ## 

- ## 

- ## 

- ## [红蓝对抗：浅谈Red Team服务对防护能力的提升 - 知乎 _201905](https://zhuanlan.zhihu.com/p/67649785)
- 笔者所在的公司（安全狗）在今年年初，也把原来做渗透测试的团队升级成为了可提供Red Team服务的队伍，一方面是因为渗透测试服务市场受到了众测服务一定程度的冲击，另外一方面是随着攻击手段隐蔽性和复杂性的逐年提升，国内Red Team服务需求会大幅上升。现在回过头来看，我们的预判很准确。
- RedTeam服务(国内团队也称为蓝军)旨在通过全场景、多维度的“真实”攻击来检验企业实际的安全防护水平和发现安全防护体系的缺陷。
- 笔者所在公司的Red Team方案把整个攻击链条总结为“从外到内、从内到内和从内到外”三个环节，从这三个环节基本能完整检验一个企业的真实防守能力

- 因为国外习惯以红队为攻击方，蓝队为防守方，这与我们国家的习惯恰好相反。你看军事演习的反派都叫“蓝军”嘛，“红军”才代表“我军”
