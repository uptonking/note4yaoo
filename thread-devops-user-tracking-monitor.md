---
title: thread-devops-user-tracking-monitor
tags: [analytics, devops, thread, user-tracking]
created: 2023-04-25T17:45:55.094Z
modified: 2023-04-25T17:48:06.146Z
---

# thread-devops-user-tracking-monitor

# guide

# discuss
- ## 

- ## 

- ## http://sentry.io的session replay功能也太叼了叭！！
- https://twitter.com/changwei1006/status/1726491004709327227
  - 发生错误时会自动录制用户的操作流程和鼠标轨迹，便于开发者分析错误原因。
  - 这下我debug的时候终于不用再去追问用户“你当时是先点哪里再点哪里最后点哪里然后出现错误的”，也不用各种拉群沟通请客户截图之类的操作，太方便了！（是DOM录制而非屏幕录制，所以理论上不会泄露用户隐私也几乎不占用CPU内存等运算资源）
  - 而且录制的时候会把DOM节点的innerHTML内容自动变成星号*打码，也不会泄漏客户隐私。
  - 还会顺带记录console.log和network网络请求，call stack的trace以及memory占用情况
  - 平时不接触工程开发的话都不知道世界上还有这么好用的工具
- 可惜暂时不支持mobile

- ## 在找 error tracking 工具于是试了下 LogRocket 的 demo，
- https://twitter.com/novoreorx/status/1650916871447908352
  - 能够完全追踪用户的各种操作：什么时间、什么地点、怎样滚动屏幕、鼠标在哪里停留，输入了什么内容…
  - 以这样的方式分析用户行为真的挺吓人的，这样视奸真的不够成隐私侵犯吗
