---
title: pattern-arch-flux-elm
tags: [architecture, elm, flux, redux]
created: 2023-11-17T10:25:45.016Z
modified: 2023-11-18T09:48:30.897Z
---

# pattern-arch-flux-elm

# guide

- flux with event-sourcing
# faq

## flux vs redux

- flux支持多store
- redux推荐单store
# dev
- 基于event实现undo的两种思路
  - 每个event的op同时保存inverse-op，每次undo时执行inverse-op
  - 每个event保存op，undo时从头开始计算一遍
# more
