---
title: devops-deploy-examples-mjj
tags: [devops, examples, mjj]
created: 2026-10-08T05:05:43.456Z
modified: 2026-10-08T05:05:56.528Z
---

# devops-deploy-examples-mjj

# guide

# popular

# bootstrap

# ip/network
- https://github.com/hotyue/IP-Sentinel /AGPL/202610/python/shell
  - 轻量化、模块化的分布式 VPS 资产养护系统，通过地理位置信号锚定与高拟真本土流量注入，精准解决 IP 定位偏移（IP送中）及风控分过高的痛点，并配合 Telegram 实现全球多节点“低功耗、拟真、无人值守”的自动化资产养护。
  - 专为解决 VPS IP 被 Google 等数据库错误定位到中国大陆/香港（俗称“送中”）等问题而生。
    - IP-Sentinel 已从单机脚本全面跃升为 Master-Agent 分布式架构。它像影子一样潜伏在全球各地的服务器后台，通过高度拟真的真实用户行为为你默默积累 IP 权重，并允许你通过 Telegram 随时随地对整个舰队进行毫秒级“点名”与“遥控”。
  - 极速部署 
    - 模式 A：私有独立模式 (全自主、强烈推荐), 找一台 VPS 作为司令部（仅需部署一台,可以与Agent装在同一台VPS）, 部署 Agent (边缘哨兵)：在需要养护的机器上执行 Agent 脚本，安装时选择私有独立中枢
    - 模式 B：官方公共模式 (最简体验)， 适合不想折腾、只想快速体验养护效果的用户。 采用官方BOT，您将失去 OTA 远程静默升级 权限
  - [智控全局：IP-Sentinel Master (控制中枢) 部署指南 - System Architect _202604](https://blog.iot-architect.com/engineering-practice/ip-sentinel-master-deployment-guide/)
  - [分布式边缘哨兵：IP-Sentinel 节点安装与平滑升级全攻略 - System Architect _202604](https://blog.iot-architect.com/engineering-practice/ip-sentinel-installation-and-upgrade-guide/)
# more
