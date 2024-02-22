---
title: toc-saas-devops-monitoring-logging
tags: [devops, logging, monitoring, toc]
created: 2024-02-11T15:10:59.275Z
modified: 2024-02-11T15:11:31.598Z
---

# toc-saas-devops-monitoring-logging

# guide

# monitoring
- https://github.com/hyperdxio/hyperdx /MIT/202402/ts
  - https://hyperdx.io/
  - open source observability platform unifying session replays, logs, metrics, traces and errors powered by Clickhouse and OpenTelemetry.
  - open source and developer-friendly alternative to Datadog and New Relic.
  - 依赖@clickhouse/client、@hyperdx/lucene、express-session、mongoose、passport、zod、nextjs、mantine6、jotai、swr、tanstack-table、rrweb
  - We provide a set of SDKs and integration options to make it easier to get started with HyperDX, such as Browser, Node.js, and Python
  - HyperDX is compatible with OpenTelemetry, a vendor-neutral standard for instrumenting your application

- https://github.com/openreplay/openreplay /8.2kStar/Elastic/202311/ts/go/python
  - https://openreplay.com/
  - a session replay suite you can host yourself, that lets you see what users do on your web app, helping you troubleshoot issues faster.

- https://github.com/parseablehq/parseable /AGPLv3/202402/rust
  - https://parseable.com/
  - a lightweight, cloud native log observability and analytics engine. 
  - It is written in Rust and uses Apache Arrow and Parquet.
  - Parseable uses a simple, index-free mechanism to organize and query data allowing low latency, and high throughput ingestion and query. 
  - It can use either a local mount point or object storage (S3/compatible stores) for data storage.
  - For comparison, Parseable consumes up to ~80% lower memory and ~50% lower CPU than `Elastic` for similar ingestion throughput. 

- https://github.com/openobserve/openobserve /AGPLv3/202402/rust/ts/vue
  - https://openobserve.ai/
  - a cloud-native observability platform built specifically for logs, metrics, traces, analytics, RUM (Real User Monitoring - Performance, Errors, Session Replay) designed to work at petabyte scale
  - Elasticsearch/Splunk/Datadog alternative for (logs, metrics, traces, RUM, Error tracking, Session replay)

- https://github.com/spiritLHLS/ecs /shell
  - VPS融合怪服务器测评脚本(VPS Fusion Monster Server Test Script)(尽量做最全能测试服务器的脚本)

- https://github.com/M-cheng-web/web-tracing /ts
  - 为前端项目提供【 埋点、行为、性能、异常、请求、资源、路由、曝光、录屏 】监控手段

- https://github.com/del-systems/swatcher /202311/js
  - https://del.systems/2021/06/22/swatcher.html
  - This project aimed to collect screenshots from UI tests and store them to S3 compatible storage.

- https://github.com/PostHog/posthog /MIT/202402/python/ts
  - https://posthog.com/
  - open-source product analytics, session recording, feature flagging and A/B testing that you can self-host.
  - Analyze data with ready-made visualizations, or do it yourself with SQL
# examples
- https://github.com/dillionverma/llm.report /GPLv3/202402/ts
  - open-source logging and analytics platform for OpenAI: Log your ChatGPT API requests, analyze costs, and improve your prompts.
  - No-code solution to analyze your OpenAI API costs and token usage.
# utils
- https://github.com/Tencent/TSW /MIT/202310/ts
  - https://tswjs.org/
  - 一套面向 WEB 前端开发者，以提升问题定位效率为初衷，提供 染色抓包 和 全息日志 的 Node.js 基础设施
  - TSW 关注业务的运维监控能力，适用于 http、https 协议的业务场景，可无缝与现有应用（Koa、Express）进行整合。
  - 2.0 没有包含日志清理工具，建议选择 winston-rotating-file 类似工具来完成清理

- https://github.com/NarrativeScience-old/log.io /apache2/202005/ts/inactive
  - http://logio.org/
  - Real-time log monitoring in your browser
  - Powered by node.js + socket.io
  - A file input watches log files for changes, sends new messages to the server via TCP, which broadcasts to browsers via socket.io.
  - log.io has no persistence layer. File inputs are informed of file changes via inotify, and log messages hop from input to server to web client via TCP and socket.io, respectively.
  - Users can watch adhoc log streams by activating inputs and binding them to multiple screens via the web UI.
  - log.io uses a stateless TCP API to receive log messages.
# more
