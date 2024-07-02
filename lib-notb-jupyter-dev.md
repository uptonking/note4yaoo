---
title: lib-notb-jupyter-dev
tags: [jupyter, lib, notebook]
created: 2021-05-17T11:52:36.756Z
modified: 2024-06-30T03:19:11.399Z
---

# lib-notb-jupyter-dev

# guide

- pros
  - ?

- cons
  - jupyterhub的架构设计不支持ha，内存中共享了数据库相关状态
    - jupyverse 的实现还不成熟
  - 协作实现在单个server，而不是hub，架构问题多

- features
  - ?

- who is using #jupyter
  - fwk:
  - apps: cocalc
  - companies: Yelp

- dev-xp
  - npm打包分发的方式，不如docker/ollama-run方便，但jspm在线源的设计就很方便了
# draft
- jupyterhub实现支持ha/多实例
# dev-xp

# more
