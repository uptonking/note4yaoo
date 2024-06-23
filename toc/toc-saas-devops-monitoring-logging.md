---
title: toc-saas-devops-monitoring-logging
tags: [devops, logging, monitoring, toc]
created: 2024-02-11T15:10:59.275Z
modified: 2024-02-11T15:11:31.598Z
---

# toc-saas-devops-monitoring-logging

# guide

# grafana/kibana-like
- https://github.com/metrico/qryn /AGPLv3/202403/js/go
  - https://qryn.dev/
  - polyglot, lighweight, multi-standard drop-in observability framework for Logs, Metrics and Traces
  - All-in-one Polyglot Observability stack with OLAP storage. 
  - Drop-in LGTM compatible with Loki, Prometheus, Tempo, Pyroscope, Opentelemetry and more
  - wasm powered 
- https://github.com/metrico/qryn-view /AGPLv3/202402/ts
  - http://view.cloki.org/
  - qryn polyglot user interface to explore logs, metrics and traces 
  - Grafana Explore alternative compatible with Loki, Prometheus and Tempo
# monitoring/observability
- https://github.com/hyperdxio/hyperdx /MIT/202402/ts
  - https://hyperdx.io/
  - open source observability platform unifying session replays, logs, metrics, traces and errors powered by Clickhouse and OpenTelemetry.
  - open source and developer-friendly alternative to Datadog and New Relic.
  - 依赖@clickhouse/client、@hyperdx/lucene、express-session、mongoose、passport、zod、nextjs、mantine6、jotai、swr、tanstack-table、rrweb
  - We provide a set of SDKs and integration options to make it easier to get started with HyperDX, such as Browser, Node.js, and Python
  - HyperDX is compatible with OpenTelemetry, a vendor-neutral standard for instrumenting your application

- https://github.com/Openpanel-dev/openpanel /AGPLv3/202403/ts
  - https://openpanel.dev/
  - a simple analytics tool for logging events on web, apps and backend
  - All the goodies from both Mixpanel and Plausible combined into one tool.
  - Access all your visitors and there history
  - Cloud or Self-Hosting
  - Nextjs - the dashboard
  - Postgres - storing basic information
  - Clickhouse - storing events
  - Fastify - event api
  - Redis - cache layer, pub/sub and queue

- https://github.com/quickwit-oss/quickwit /AGPLv3/202403/rust
  - https://quickwit.io/
  - Cloud-native search engine for observability. 
  - An open-source alternative to Datadog, Elasticsearch, Loki, and Tempo.
  - Elasticsearch-compatible API, use Quickwit with any Elasticsearch or OpenSearch client

- https://github.com/openreplay/openreplay /8.2kStar/Elastic/202311/ts/go/python
  - https://openreplay.com/
  - a session replay suite you can host yourself, that lets you see what users do on your web app, helping you troubleshoot issues faster.
- https://github.com/SigNoz/signoz /202403/go/ts
  - open-source observability platform native to OpenTelemetry with logs, traces and metrics in a single application. 
  - An open-source alternative to DataDog, NewRelic, etc
- https://github.com/highlight/highlight /202403/go/ts
  - open source, full-stack monitoring platform.

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

- https://github.com/perses/perses /apache2/202403/go/ts
  - https://demo.perses.dev/
  - The CNCF candidate for observability visualisation. 
  - Already supports Prometheus - more data sources to come
  - we want to promote the project to the Cloud Native Computing Foundation and be part of the monitoring tools like Prometheus or Thanos.

- https://github.com/ccfos/nightingale /go/python
  - 夜莺 Nightingale 是中国计算机学会接受捐赠并托管的第一个开源项目，是一个 All-in-One 的云原生监控工具，
  - 集合了 Prometheus 和 Grafana 的优点，你可以在 WebUI 上管理和配置告警策略，也可以对分布在多个 Region 的指标、日志、链路追踪数据进行统一的可视化和分析。
# google-analytics-like
- https://github.com/umami-software/umami /19.3kStar/MIT/202406/ts
  - https://umami.is/
  - a simple, fast, privacy-focused alternative to Google Analytics.
  - supports MySQL and Postgresql databases.
  - https://twitter.com/vikingmute/status/1768823778581303460
    - 现在类似的解决方案也太多了，而且界面都类似，不知道各家竞争是这么活下去的。

- countly /4.7kStar/AGPLv3/202403/js
  - https://github.com/Countly/countly-server
  - built with mongodb, express
  - Countly is a product analytics solution that helps teams track product performance and customer journey and behavior across mobile, web, and desktop applications. 
  - Countly relies on a wide diversity of SDKs for deployment
  - 依赖express、mongoose
  - [Download & Install Countly](https://github.com/osoner/countly-documentation/blob/master/installation/countly-server-installation.md)
# feature-flag
- https://github.com/Unleash/unleash /10.1kStar/apache2/202403/ts
  - https://getunleash.io/
  - https://demo.unleash-hosted.com/
  - Unleash is the open source feature toggle service.
  - Unleash increases efficiency and gives teams full control of how and when they enable new functionality for end users.

- https://github.com/PostHog/posthog /MIT/202402/python/ts
  - https://posthog.com/
  - open-source product analytics, session recording, feature flagging and A/B testing that you can self-host.
  - Analyze data with ready-made visualizations, or do it yourself with SQL

- https://github.com/flipt-io/flipt /go
  - https://flipt.io/
  - open source, self-hosted feature flag solution

- https://github.com/growthbook/growthbook
  - Open Source Feature Flagging and A/B Testing
  - SDKs for React, Javascript, PHP, Ruby, Python, Go, and Kotlin (Android) with more coming soon

- https://github.com/marcellothiry/feature-flags
  - This is the complementary repository for our video series Implementing Feature Flags from Scratch

- https://github.com/configcat/trello-powerup /202403/ts
  - ConfigCat Power-Up to manage feature flags from any Trello board. 
  - ConfigCat is a hosted feature flag service
  - Provides open-source SDKs for easy integration with any web, mobile or backend application.
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
# cloudflare-like-integration
- https://github.com/benvinegar/counterscale /MIT/202406/ts
  - https://counterscale.dev/
  - Counterscale is a simple web analytics tracker and dashboard that you self-host on Cloudflare.
  - designed to be easy to deploy and maintain, and should cost you near-zero to operate – even at high levels of traffic (Cloudflare's free tier could hypothetically support up to 100k hits/day).


# more
- https://github.com/anthonygauthier/jmeter-es-backendlistener-dashboard /201810/js
  - Dashboard to visualize JMeter results generated via the ElasticSearch Backend Listener. 
  - Alternative to Grafana & Kibana.
