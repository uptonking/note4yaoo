---
title: toc-repos-solutions-devops
tags: [devops, repos, solutions, toc]
created: 2020-10-05T11:00:14.905Z
modified: 2020-12-12T19:01:56.749Z
---

# toc-repos-solutions-devops

# guide

# devops
- https://github.com/xuxueli/xxl-job
  - /15.8kStar/GPLv3/202009
  - 分布式任务调度平台
# tunnel
- https://github.com/Rob--W/cors-anywhere /MIT/202109/js/inactive
  - CORS Anywhere is a NodeJS reverse proxy which adds CORS headers to the proxied request
  - https://github.com/jefferson-calmon/corsbypass /202307/ts
    - i've just created a repository with the code for an unrestricted self-hosted solution
# shortlink
- https://github.com/dubinc/dub /AGPLv3/202402/ts
  - https://dub.co/
  - An open-source link management tool for modern marketing teams to create, share, and track short links.
  - 依赖NextAuth.js、PlanetScale、Tinybird – analytics、Upstash – redis
# status-page
- https://github.com/upptime/upptime /17.1kStar/MIT/202608/yaml
  - https://upptime.js.org/
  - open-source uptime monitor and status page, powered entirely by GitHub Actions, Issues, and Pages
  - GitHub Actions is used as an uptime monitor: Every 5 minutes, a workflow visits your website to make sure it's up
  - Response time is recorded every 6 hours and committed to git
  - GitHub Issues is used for incident reports
  - GitHub Pages is used for the status website

- https://github.com/openstatusHQ/openstatus /AGPLv3/202402/ts
  - https://openstatus.dev/
  - The Open-source Status Page and Alerting System
  - The Statuspage Open Source Alternative.

- https://github.com/OneUptime/oneuptime /apache2/202403/ts
  - https://oneuptime.com/
  - a comprehensive solution for monitoring and managing your online services
  - Monitor the availability and response time of your online services from multiple locations around the world.
  - Replace tools like StatusPage.io.
  - Create incident reports, assign tasks, update stakeholders, and document resolutions. Replace tools like Incident.io.
  - Collect, store, and analyze logs from your online services. Search, filter, and visualize log data to gain insights and troubleshoot issues. Replace tools like Loggly.

- https://github.com/RafalWilinski/express-status-monitor /MIT/202204/js/inactive
  - https://dynobase.dev/
  - Realtime Monitoring solution for Node.js/Express.js apps, inspired by status.github.com

- https://github.com/webmin/webmin /perl
  - http://www.webmin.com/
  - a web-based system administration tool for Unix-like servers, and services
  - it is possible to configure operating system internals, such as users, disk quotas, services or configuration files, as well as modify, and control open-source apps, such as BIND DNS Server, Apache HTTP Server, PHP, MySQL, and many more.
# scheduler
- https://github.com/Hexagon/croner /MIT/js/NoDeps
  - Trigger functions or evaluate cron expressions in JavaScript or TypeScript. 
  - No dependencies. Most features. Node. Deno. Bun. Browser.
# linux-monitor
- https://github.com/henrygd/beszel /24.4kStar/MIT/202608/go
  - https://beszel.dev/
  - lightweight server monitoring platform that includes Docker statistics, historical data, and alert functions.
  - It supports automatic backup, multi-user, OAuth authentication, and API access.
  - Docker stats: Tracks CPU, memory, and network usage history for each container.
  - Alerts: Configurable alerts for CPU, memory, disk, bandwidth, temperature, fan speed, load average, and status.
  - Multi-user: Users manage their own systems. Admins can share systems across users.
  - Automatic backups: Save to and restore from disk or S3-compatible storage.
  - Beszel consists of two main components: the hub and the agent.
    - Hub: A web application built on `PocketBase` that provides a dashboard for viewing and managing connected systems.
    - Agent: Runs on each system you want to monitor and communicates system metrics to the hub.
  - Does it support adding custom metrics? E.g. getting the result of some external shell script or app and taking values from its output as plaintext/regex/JSON for graphs and alerts?
    - AFAICT, it does not.
  - [[Bug]: Systemd + AppArmor  _202511](https://github.com/henrygd/beszel/issues/1408)
    - AppArmor (Application Armor) is a Linux security module that protects an operating system and its applications from security threats.
    - The `apparmor:unconfined` actually solved my problem and the systemd information is being fetched and transmitted to the hub.

- https://github.com/nicolargo/glances /32.3kStar/LGPL/202608/python/vue
  - open-source system cross-platform monitoring tool. 
  - It allows real-time monitoring of various aspects of your system such as CPU, memory, disk, network usage etc. 
  - It also allows monitoring of running processes, logged in users, temperatures, voltages, fan speeds etc.

- https://github.com/cockpit-project/cockpit /14.9kStar/MIT/202608/python/js
  - http://www.cockpit-project.org/
  - Cockpit is a web-based graphical interface for servers.
  - Cockpit interacts directly with the operating system from a real Linux session in a browser.
  - Cockpit makes Linux discoverable, allowing sysadmins to easily perform tasks such as starting containers, storage administration, network configuration, inspecting logs and so on.

- https://github.com/hhftechnology/vps-monitor /GPL/202604/go/ts
  - https://vps-monitor.hhf.technology/
  - lightweight, Go-based VPS monitoring solution with real-time web dashboard supporting multiple agents. 
  - Monitor unlimited servers from a single dashboard overview analytics.
  - Start, stop, restart, and remove containers
  - Image Management
  - Network Management
  - Multi-Host Docker Support: Connect to local Unix sockets, remote SSH, or TCP endpoints
  - React + Vite + Capacitor mobile client under mobile/

## vps-deploy

- https://github.com/ovexro/dockpanel /AGPL/202608/rust/ts
  - https://dockpanel.dev/
  - Modern server management panel built with Rust and React. Sites, databases, Docker apps, Git deploy, mail, DNS, monitoring, backups, and security — all in one panel.
  - Self-hosted. Docker-native. Written in Rust. Panel services run on ~49MB of RAM. 823 HTTP routes. 148 app templates. 2585 regression assertions. ~46MB binaries. Zero subscriptions.
  - No other free panel gives you Git push-to-deploy with blue-green zero-downtime updates, 148 one-click Docker app templates, per-image CVE scanning with deploy gating, a WAF, passkey login, GPU passthrough, multi-server management, reseller accounts, a developer CLI, and Infrastructure as Code 

## vps-more

- https://github.com/LloydAsp/NodeQuality /2.1kStar/AGPL/202603/sh
  - 在沙箱环境中运行vps测试脚本，并排版测试结果
  - 本项目本质上是测试工具集合的前置加载器和结果后处理项目。把服务器测试工作的流程给规范化自动化了。 让测试仅仅是测试，不要留下一堆痕迹；让测试可以更舒服省心，自动排版截图。
  - 为了减少测试过程中安装的软件和产生的临时文件占用空间，将所有测试放在BenchOS内。 chroot特别适合作为测试脚本的沙箱工具，因为其不用额外安装、极致的轻量、只有文件隔离而没有网络和内存隔离。
  - 使用一个debian系统的rootfs作为测试的准系统
  - 使用chroot临时切换到准系统(称为BenchOS)，无需重装系统或者安装docker/虚拟机
  - 除了需要curl下载文件的命令，不需要额外安装任何程序到vps上
  - [『升级推新』“无痕测试，基准系统，一键导出”，NodeQuality测试脚本发布 _202503](https://www.nodeseek.com/post-297125-1)
    - 脚本是原NodeBench脚本和粘贴板的升级项目
    - 全面拥抱 xykt 脚本方案，补充其他测试信息，减少重复测试
    - 切换到一个专用的临时准系统内测试，测完自动清理，极致的干净，做到无痕测试
    - 目前方案是选取了Yabs + IP质量 + 网络质量 + 融合怪的部分功能，重新整合后的脚本。这种组合兼顾信息的全面性和直观性。

- https://github.com/nuver-labs/vps-audit /2.5kStar/MIT/202608/sh
  - comprehensive Bash script for auditing the security and performance of your VPS (Virtual Private Server). This tool performs various security checks and provides a detailed report with recommendations for improvements.

- https://github.com/kejilion/sh /3.1kStar/apache2/202608/sh
  - https://kejilion.sh/
  - 面向 Linux 服务器的综合脚本工具箱，集成系统管理、网络测试、Docker、LDNMP 建站、 应用市场、备份迁移与安全防护。
  - 脚本包含软件安装、网络、防火墙、磁盘和网站环境等系统级操作。 请在执行前阅读终端提示，并提前备份重要网站、数据库、容器和配置。
  - 不同发行版的软件包、网络栈和服务管理方式存在差异，脚本会根据当前系统能力开放对应功能。

- https://github.com/kadidalax/cf-vps-monitor /MIT/202608/ts
  - 用cloudflare worker搭建的vps探针+网站检测 面板，部署简单，不需要服务器。
  - 一个轻量 VPS 探针面板，使用 Cloudflare Workers 承载前端、API、实时连接和定时任务，使用 Durable Objects 协调实时状态，使用 Supabase Postgres 保存配置和历史数据，使用 Go Agent 在服务器上采集指标。

- https://github.com/tanelpoder/0xtools /GPL/202511/python/c/inactive
  - https://0x.tools/
  - a set of open-source utilities for analyzing application performance on Linux
  - It has a goal of deployment simplicity and minimal dependencies, to reduce friction of systematic troubleshooting. 
  - No need to install kernel modules or heavy monitoring frameworks.
  - 0x.tools allow you to measure individual thread level activity, like executed code, sleep states, system calls and wait locations - by tracking (not tracing) and then sampling the right events at the right time.
# ci/cd
- https://github.com/woodpecker-ci/woodpecker /7.7kStar/apache2/202608/go
  - https://woodpecker-ci.org/
  - a simple, yet powerful CI/CD engine with great extensibility.
  - Woodpecker can be installed in various ways (see the Installation Instructions) and runs with SQLite as database by default. It requires around 100 MB of RAM (Server) and 30 MB (Agent) at runtime in idle mode.
  - Woodpecker is used as the main CI/CD engine at Codeberg, an alternative Git hosting platform with a focus on privacy and free software development.

- https://github.com/moghtech/komodo /12kStar/GPL/202608/rust/ts
  - https://komo.do/
  - A tool to build and deploy software across many servers.

- https://github.com/intuit/auto /MIT/202502/ts
  - Generate releases based on semantic version labels on pull requests.

## github-cicd

- https://github.com/youssefbrr/self-hosted-runner /MIT/202607
  - Dockerized GitHub Actions self-hosted runners for Linux (x64) and macOS (ARM64). Deploy in minutes, scale with replicas, deregister cleanly on shutdown.
  - This repo is not a deploy-to-VPS pipeline. It packages a GitHub Actions self-hosted runner as Docker images so you can run Actions jobs on your own machine (e.g. a VPS).
    - Its own workflows only build/publish runner images to GHCR when you push version tags — they do not deploy your apps.
# network-tunnel
- https://github.com/GyulyVGC/sniffnet /26.2kStar/MIT/202507/rust
  - https://sniffnet.net/
  - comfortably monitor your Internet traffic. Cross-platform.
  - import and export comprehensive capture reports as PCAP files
  - https://x.com/abskoop/status/2048066454361461157
    - Sniffnet 把本机网络连接、应用流量和远程主机信息做成可视化面板，让你像看系统仪表盘一样，直观了解电脑正在和谁通信、哪些程序正在占用带宽
    - 支持 Windows、macOS 和 Linux
    - 提供直观的可视化面板，可查看本机网络连接、域名、ASN、地理位置和应用流量来源

- https://github.com/tinkink-net/devns /202511/js
  - a lightweight local DNS server for development purposes, it listens on UDP port 53 (configurable) and answers DNS queries by resolving them via Node's built-in dns module, with support for local hosts file overrides.
  - DevNS is developed by AI
  - Minimal dependencies, built on Node.js built-in modules
# caddy

## utils-caddy

- https://github.com/mhupfauer/caddy-md4agents /MIT/202607/go
  - Caddy v2 plugin: serve Markdown for AI agents via content negotiation, with pre-generation and cached serving
  - A Caddy v2 HTTP middleware that serves a Markdown rendition of HTML pages when a client (typically an AI agent) negotiates for it. 
  - It implements Cloudflare's Markdown for Agents conventions on top of Caddy's static and dynamic handlers.
  - Static-first. When root is set, requests resolve to disk: an author-written *.md wins, otherwise the matching * .html is converted on first hit and written to a sidecar cache.
  - Lazy in-memory + disk write-through. First request to a page pays the conversion cost (~ms); subsequent requests serve from a sized LRU. Disk sidecars survive restarts and worker recycling.
  - Stat-based invalidation. Every request stats the source HTML and keys the cache on path | mtime | size. Edits invalidate automatically, no watcher required.
  - https://github.com/avvertix/caddy-content-negotiation /MIT/202605/go
    - A Caddy middleware module that intercepts HTTP requests containing Accept: text/markdown and serves precomputed .md files located alongside the originally requested resources.

## caddy-boilerplate/template/example

- examples
  - [3X-UI + Caddy Setup Guide (Docker Version) ](https://gist.github.com/ReturnFI/995e990faa155053515537734493fa81)

- https://github.com/AiratTop/caddy-self-hosted /MIT/202604
  - simple and production-ready Docker Compose setup for self-hosting the Caddy web server
  - Uses the official Caddy Docker image.
  - Automatic HTTPS via Let's Encrypt.
  - Data is persisted in a local volume.
  - Pre-configured for a shared network.

- https://github.com/GrantBirki/caddy-fastapi /MIT/202608
  - This is a template repo to deploy Caddy + FastAPI with docker compose

- https://github.com/barelyhuman/docker-caddy-example /MIT/202410
  - container applications with Caddy + docker compose
  - If you prefer `traefik` over caddy, you can go through this template instead

- https://github.com/dhawansolanki/docker-caddy-boilerplate /202410
  - This project uses Docker to run a Caddy server as a reverse proxy for a Node.js application.
# nginx
- https://github.com/Adewagold/nginx-server-manager /202509/python
  - web interface that transforms nginx administration from complex command-line operations into simple point-and-click actions. 
# app-store
- https://github.com/toolsetlink/upgradelink /233Star/apache2/202512/go/ts/vue
  - https://www.toolsetlink.com/
  - 为开发者和企业提供一站式应用升级解决方案
  - 全端应用升级与分发平台 | 为开发者省去90%升级服务搭建成本
  - 全端覆盖：Windows/Linux/Mac/安卓/Tauri/Electron等全场景支持
# docker
- https://github.com/mbakgun/DockerFlex /MIT/202512/js
  - a modern web-based application that simplifies Docker container file management
  - Browse, edit, and manage container files with ease through a modern web interface
# port-forwarding
- https://github.com/vercel-labs/portless /742Star/apache2/202602/ts
  - Replace port numbers with stable, named .localhost URLs. For humans and agents.
  - cookies set on localhost bleed across apps on different ports; localStorage is lost when ports shift
  - Browser history is useless -- your history for localhost:3000 is a jumble of unrelated projects
  - https://x.com/geekbb/status/2023645651092075008
    - Vercel Labs 做了个端口转发工具，用稳定的命名 .localhost URL 替换 localhost:3000 这些端口号，让人类和 AI 代理都能轻松访问本地服务。
    - 以前开几个本地项目，端口记不住、端口冲突，现在代理自动分配随机端口，用命名URL替代数字端口。
    - 工作原理就是：跑一个本地代理在1355端口，所有 *.localhost:1355 都路由到它，然后它根据子域名转发到实际的应用端口。
  - https://x.com/akazwz_/status/2051909177765994875
    - 本地开发用自定义域名和 HTTPS 已经挺常见了。 但如果再支持泛域名 HTTPS，比如 *.hostc.test，就可以在本地模拟多租户、子域名路由、SaaS 自定义站点、预览环境等真实线上结构。
    - 可以买一个域名，然后dns-01申请*.域名的证书。配置个nginx或者caddy就好了。caddy申请证书更方便。有CF token还可以自动申请。
# more
