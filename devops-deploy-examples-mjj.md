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
  - 🛝
    - 巡逻 (Patrol): Every 20 minutes 72 times / day, Runs at minute :00, :20, and :40 of every hour (OnCalendar=* :0/20).
    - Google 纠偏: Driven by Patrol, 70%, ~50 times / day
    - 信用净化: Driven by Patrol, 30%, ~22 times / day
    - Both "触发google纠偏" and "触发信用净化" can also be executed immediately at any time by clicking the corresponding buttons in the Telegram Bot
  - [智控全局：IP-Sentinel Master (控制中枢) 部署指南 - System Architect _202604](https://blog.iot-architect.com/engineering-practice/ip-sentinel-master-deployment-guide/)
  - [分布式边缘哨兵：IP-Sentinel 节点安装与平滑升级全攻略 - System Architect _202604](https://blog.iot-architect.com/engineering-practice/ip-sentinel-installation-and-upgrade-guide/)
# server-monitor/探针
- https://github.com/huilang-me/CF-Server-Monitor /2.5kStar/MIT/202610/js/vue
  - https://demo.huilang.me/
  - 基于 Cloudflare Workers、D1 和 Durable Objects 的轻量级多服务器监控面板。
  - 服务器端安装 Agent 后会单向上报指标到 Worker，数据写入 D1，并通过 Durable Objects + WebSocket 推送到前端，实现免费托管、低维护的实时监控。
  - 支持主流 Linux 发行版、Alpine Linux、OpenWrt、macOS、群晖 DSM、飞牛 fnOS、Windows 等系统，并提供 Docker 镜像部署方式。
  - 高安全性：Agent 仅单向上报指标，不提供 WebSSH、远程命令下发或主控通道；支持非 root 运行
  - 前置要求: Cloudflare 账户, GitHub 账户, 一个足够复杂的 API_SECRET，同时作为 Agent 上报密钥和初始后台密码
  - 进入 /admin#/admin。 点击添加服务器。选择目标系统和 Agent 版本。在目标服务器上执行复制出的安装命令。
    - V2.8.3 起默认使用独立项目 cfsm-agent，安装后服务名为 cf-probe。新增服务器后建议直接从管理后台复制安装命令，后台会按目标系统、服务器 ID、Worker 地址和当前参数生成完整命令。
  - [[开源自荐] CF-Server-Monitor 部署在Cloudflare Workers的免费探针 - LINUX DO _202606](https://linux.do/t/topic/2391991)
# more
