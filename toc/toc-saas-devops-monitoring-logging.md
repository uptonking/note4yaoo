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
- https://github.com/hyperdxio/hyperdx /MIT/202506/ts
  - https://hyperdx.io/
  - open source observability platform unifying session replays, logs, metrics, traces and errors powered by Clickhouse and OpenTelemetry.
  - open source and developer-friendly alternative to Datadog and New Relic.
  - 依赖rrweb、@clickhouse/client、@hyperdx/lucene、express-session、mongoose、passport、zod、nextjs、mantine6、jotai、swr、tanstack-table
  - We provide a set of SDKs and integration options to make it easier to get started with HyperDX, such as Browser, Node.js, and Python
  - HyperDX is compatible with OpenTelemetry, a vendor-neutral standard for instrumenting your application

- https://github.com/pydantic/logfire /3.2kStar/MIT/202506/python
  - https://logfire.pydantic.dev/docs/
  - From the team behind Pydantic, Logfire is an observability platform built on the same belief as our open source library
  - Python-centric Insights: From rich display of Python objects, to event-loop telemetry, to profiling Python code and database queries
  - 未使用rrweb
  - SQL: Query your data using standard SQL
  - Pydantic Integration: Understand the data flowing through your Pydantic models and get built-in analytics on validations.

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

- https://github.com/SigNoz/signoz /23.9kStar/MIT+EE/202510/go/ts
  - https://signoz.io/
  - open-source observability platform native to OpenTelemetry with logs, traces and metrics in a single application
  - An open-source alternative to DataDog, NewRelic, etc
  - Built on top of OpenTelemetry, the open-source standard which frees you from any type of vendor lock-in
  - 依赖httpsnoop、go-sqlbuilder
  - Use SigNoz APM to monitor your applications and services. It comes with out-of-box charts for key application metrics like p99 latency, error rate, Apdex and operations per second. You can also monitor the database and external calls made from your application
  - SigNoz can be used as a centralized log management solution. We use ClickHouse as a datastore
  - Monitor exceptions automatically in Python, Java, Ruby, and Javascript. For other languages, just drop in a few lines of code and start monitoring exceptions.
  - [Is Signoz really open-source or not? _202312](https://github.com/SigNoz/signoz/discussions/4231)
    - SigNoz is fully open-source. However, ee folder is under SigNoz Enterprise license, while the rest of the code is under MIT Expat license.
    - Yes, you can self host SigNoz and use it in production. Only features in community edition will be available in the open source self hosted version. Some features will be only unlocked once you take the enterprise license.
    - update on this! With the demand from the community we removed any restrictions on number of dashboards and alert panels in community edition from v0.47.0
  - [SigNoz | Pricing](https://signoz.io/pricing/)
    - Anomaly Detection
    - Pre-built integrations & dashboards (AWS ElastiCache Redis, AWS RDS MySQL/PostgreSQL, ClickHouse, MongoDB, NGINX, PostgreSQL, Redis)
    - Support for Rate Limits based on Ingestion keys
    - Custom retention for different sources of logs
    - Finer RBAC with custom roles
    - Multi-tenancy

- https://github.com/highlight/highlight /8.9kStar/apache2+EE/202510/go/ts
  - https://app.highlight.io/
  - open source, full-stack monitoring platform.
  - Error monitoring, session replay, logging, distributed tracing, and more.
  - Dom-based High-fidelity Replay: powered by rrweb
  - 依赖rrweb、chi、gorm、go-sqlbuilder、httpsnoop、go-retryablehttp、httpcc、kafka-go
  - [Application Architecture](https://www.highlight.io/docs/general/company/open-source/contributing/architecture)
  - [Is Kafka the Key? The Evolution of Highlight's Ingest _202209](https://www.highlight.io/blog/scalable-data-processing-with-apache-kafka)
    - At Highlight, we face a unique challenge when it comes to adapting to the load of our customers. Because we record our customers' web apps, we need to be able to handle bursts of traffic as they come from their users.
    - When we first started, our data ingested was simple: we would stream data from our recording client to our backend and perform updates as it came in. Our data handlers would perform metadata updates and write session recordings to PostgreSQL via SQL queries
    - The initial approach worked fine for a while. But as our customer base grew, we ran into key issues with this implementation. We had to run some database migrations that ran an ALTER command with an aggressive table lock. 
    - Since we needed a way to buffer data, we considered various techniques that could accomplish the task. One idea was to abstract each backend payload into a 'message' to be put into a buffer and consumed by a worker. 
    - As we evaluated our options, we settled on a producer-consumer message strategy. Our architecture would have our backend HTTP request handlers produce 'task' messages that would block until the data was sent to our chosen broker. The messages would arrive at the broker quickly and reside until a worker machine could consume them and process their data. 
    - Focusing on the specifics of Apache Kafka, we had to define partitions that would store the sets of messages. 
  - [Self-hosted [Enterprise] paid](https://www.highlight.io/docs/general/company/open-source/hosting/self-host-enterprise)
    - Platform Integrations (Teams, Slack, Sendgrid, etc..)
    - Email Integrations (Sendgrid, SMTP, etc..)
    - User Management Support (RBAC, SSO, SSL, etc..)
    - HA Deploy & Persistent Storage
    - Custom Retention Policies
    - Automatic Upgrades
  - [add enterprise license _202309](https://github.com/highlight/highlight/pull/6562)

- https://github.com/openreplay/openreplay /8.2kStar/AGPL/202412/ts/go/python
  - https://openreplay.com/
  - a session replay suite you can host yourself, that lets you see what users do on your web app, helping you troubleshoot issues faster.

- https://github.com/ccfos/nightingale /12.5kStar/apache2/202510/go
  - 夜莺 Nightingale 是中国计算机学会接受捐赠并托管的第一个开源项目，是一个 All-in-One 的云原生监控工具，
  - 集合了 Prometheus 和 Grafana 的优点，你可以在 WebUI 上管理和配置告警策略，也可以对分布在多个 Region 的指标、日志、链路追踪数据进行统一的可视化和分析。
  - Nightingale is an open-source monitoring project that focuses on alerting. 
    - Similar to Grafana, Nightingale also connects with various existing data sources. 
    - However, while Grafana emphasizes visualization, Nightingale places greater emphasis on the alerting engine, as well as the processing and distribution of alarms.
    - initially developed and open-sourced by DiDi.inc. On May 11, 2022, it was donated
  - Nightingale itself does not provide monitoring data collection capabilities. We recommend using Categraf as the collector
    - Categraf can collect monitoring data from operating systems, network devices, various middleware, and databases. It pushes this data to Nightingale via the Prometheus Remote Write protocol. 
    - Nightingale then stores the monitoring data in a time-series database (such as Prometheus, VictoriaMetrics, etc.) and provides alerting and visualization capabilities.

- https://github.com/perses/perses /1.6kStar/apache2/202510/go/ts
  - https://demo.perses.dev/
  - The CNCF candidate for observability visualisation. 
  - Perses is first and foremost a dashboard tool that you can use to display a variety of observability data. It currently supports Prometheus metrics & Tempo traces, with plans to expand its capabilities in the future to include logging, profiling, additional technologies for monitoring and tracing, and more.

- https://github.com/quickwit-oss/quickwit /AGPLv3/202403/rust
  - https://quickwit.io/
  - Cloud-native search engine for observability. 
  - An open-source alternative to Datadog, Elasticsearch, Loki, and Tempo.
  - Elasticsearch-compatible API, use Quickwit with any Elasticsearch or OpenSearch client

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

- https://github.com/PostHog/posthog /29.7kStar/MIT+EE/202510/python/ts
  - https://posthog.com/
  - open-source product analytics, session recording, feature flagging and A/B testing that you can self-host.
  - Analyze data with ready-made visualizations, or do it yourself with SQL
  - [Consider use redpanda to replace kafka _202502](https://github.com/PostHog/posthog/issues/29283)
    - give a investigation to replace kafka with redpanda（kafka api compatible）, i think there may have a significant performance improve, self host are too much heavy use `kafka and clickhouse`
    - i use this to replace rocketMQ on my own project, it's simplicity for maintain

- https://github.com/growthbook/growthbook /7kStar/MIT+EE/202510/ts
  - https://www.growthbook.io/
  - Open Source Feature Flagging and A/B Testing Platform

- https://github.com/Flagsmith/flagsmith /6kStar/BSD/202510/python/ts
  - https://www.flagsmith.com/
  - open source feature flagging and remote config service. 
  - A/B testing: Use segments to run A/B and multivariate tests on new features
  - Segments: Release features to beta testers, collect feedback, and iterate
  - The majority of our platform is open source under the BSD-3-Clause license. A small number of repositories are under the MIT license.
    - Our core functionality stays open, always
    - Enterprise-level governance and management features are available with a valid Flagsmith Enterprise license.

- https://github.com/thomaspoignant/go-feature-flag /1.8kStar/MIT/202510/go/js
  - https://gofeatureflag.org/
  - a simple, complete and lightweight self-hosted feature flag solution 100% Open Source
  - Run A/B testing experimentation.
  - 依赖pubsub、echo、go-render
  - ⚖️ With the new standardization of feature flags by the [Openfeature](https://openfeature.dev/) project, the solution is now available for multiple languages (list of supported languages) through a simple API server called the relay proxy, which can be hosted.
  - Originally GO Feature Flag was built to be a GOlang only library, but it limits the ecosystem too much. To be compatible with more languages we have implemented the GO Feature Flag Relay Proxy. It is a service you can host that provides an API to evaluate your flags, you can call it using HTTP to get your variation.
  - [Store your flags’ configuration ](https://gofeatureflag.org/docs/integrations/store-flags-configuration)
    - The easiest way to get started with GO Feature Flag is to store your flags' configuration in a file. you can create your own custom retriever.
  - [GO Feature Flag flag edition API proposal _202409](https://github.com/thomaspoignant/go-feature-flag/discussions/2431)
    - Some developers (but also POs, SREs, DSs) may prefer a more visual interface for managing feature flags.
    - there is a common need to build an API aiming to provide a flexible and extensible solution that allows for the creation of user interfaces on top of the existing feature flag management system.
  - The repository containing a raw version of this API is available here https://github.com/go-feature-flag/flag-management

- https://github.com/openflagr/flagr /2.5kStar/apache2/202510/go/vue
  - https://openflagr.github.io/flagr
  - a feature flagging, A/B testing and dynamic configuration microservice
  - 依赖gorm、simplebox、grpc、pubsub、httpsnoop
  - [Question: Any Plans to support the Cloud Native Foundation's Open Feature standard? _202302](https://github.com/openflagr/flagr/issues/527)

- https://github.com/flipt-io/flipt /4.6kStar/FSL >> MIT/202510/go/ts
  - https://flipt.io/
  - open source, self-hosted feature flag solution
  - Flipt v2 is the first truly Git-native feature management platform that treats your feature flags as code. Store your flags in your own Git repositories
  - [chore(v2): lay groundwork for v2 _202501](https://github.com/flipt-io/flipt/pull/3829/files#diff-c693279643b8cd5d248172d9c22cb7cf4ed163a3c98c8a3f69c2717edd3eacb7)
    - license: GPL > FSL

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

## utils-logging

- https://github.com/unjs/consola /MIT/202501/ts
  - Elegant Console Logger for Node.js and Browser
  - Consistent command line interface (CLI) experience
  - Fancy output with fallback for minimal environments
  - Pluggable reporters
  - Redirect console and stdout/stderr to consola and easily restore redirect.
  - Pause/Resume support: enqueue all logs when paused and then sends them to the reported when resumed.
  - Mocking support
  - Interactive prompt support powered by clack
  - consola.log({ message: "hello" }); 
  - logger日志api参考
  - https://github.com/pinojs/pino/blob/main/docs/api.md
    - logger.info( ([mergingObject], [message], [...interpolationValues]) )
  - https://github.com/winstonjs/winston
    - logger.info('hello', { message: 'world' });
# cloudflare-like-integration
- https://github.com/benvinegar/counterscale /MIT/202406/ts
  - https://counterscale.dev/
  - Counterscale is a simple web analytics tracker and dashboard that you self-host on Cloudflare.
  - designed to be easy to deploy and maintain, and should cost you near-zero to operate – even at high levels of traffic (Cloudflare's free tier could hypothetically support up to 100k hits/day).
# crawler-like
- https://github.com/dgtlmoon/changedetection.io /apache2/202411/python
  - https://changedetection.io/
  - The best and simplest free open source web page change detection, website watcher, restock monitor and notification service. 
  - Detect website content changes and perform meaningful actions - trigger notifications via Discord, Email, Slack, Telegram, API calls and many more.
  - Chrome browser included.
  - Nothing to install, access via browser login after signup.
# more
- https://github.com/anthonygauthier/jmeter-es-backendlistener-dashboard /201810/js
  - Dashboard to visualize JMeter results generated via the ElasticSearch Backend Listener. 
  - Alternative to Grafana & Kibana.
