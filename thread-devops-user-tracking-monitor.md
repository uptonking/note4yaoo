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

- ## I don't understand why people prefer to store log lines as text vs structured data. 
- https://x.com/matteocollina/status/1798385291016737264
  - The latter is easier to post-process, search, filter, etc. Why would you not do it?
- Easier for tools to do those things, harder for humans to do so. Many projects are single individuals with a small number of users. Setting up tooling for logging is overkill and time not spent implementing features. Plain text is fine for such environments.
- Scraping text is so inbuilt into Linux/Unix mindset that people don't even realise it's scraping.
- Because any sizeable infra will have logs centralized and that is their already solved problem.
- force of habit

- Because the number of times I had to go through the logs for anything but exceptions/error is zero
- Depends on if/how often you need to search, filter, etc. A lot of logs are never read and just get deleted after a period of time.

- Unstructured (aka classic) log files, although less sophisticated, require less specific tooling, are well known and documented, and present sometimes fewer caveats (e.g. structured log drain(下水管；下水道) incompatibilities between a source and a remote sink are more likely).

- structured data take more storage than text based, search/filter is not something we do frequently so we let cpu/disk handle that load couple of times/day

- What do you consider to be structured data? I feel like it’s pretty common to do something in-between, e.g. storing logs as “structured data” in a format like JSONL, which I would also consider to be storing log lines as text.

- I use debug flags to log it as a readable text line in local development and JSON structure in production.

- Requires a structure and logging is often used for debugging, so it changes often. Updating the structure is harder than simply adding a log statement.
- Cost of storage, is that not obvious?

- Text files are much easier for quick consumption in a text editor. It doesn't preclude injesting into a DB but writing a sql statement is much less convenient that doing a find in a text editor.

- 
- 
- 
- 
- 

- ## Tried to explain why OpenTelemetry format for metrics is bloated and over-engineered, and why Prometheus remote_write format is better 
- https://twitter.com/valyala/status/1779061261524775371
  - [OpenTelemetry Is Too Complicated, VictoriaMetrics Says | Lobsters _202404](https://lobste.rs/s/0srgrw/opentelemetry_is_too_complicated)

- ## 网站上线之后，下一步就是添加 APM 了。APM 就是 Application Performance Management (应用性能管理)。
- https://twitter.com/beihuo/status/1774530839201845335
  - 这类的服务一般都提供监控服务性能、错误报告，还有查看日志等。今天比较一下不同的 APM 服务，看看哪个最适合个人或者小团队的预算
- 虽然 Datadog 的功能强大，但是被第一个排除了。原因很简单：贵，特别贵。
  - 截图中每一个功能都有单独的费用计算方式；而且重要的 APM 是按照 host 来计算费用的。也就是你上线两个 App 就要交两份的钱，哪怕没有什么流量。这对 indie maker 特别不友好。
- 我正在使用 Sentry 的免费 Plan 记录多个网站的错误信息。刚才又自己看了一下其他功能，发现 Sentry 的性能监控做得也不错。 目前免费的 Plan 包括：5K errors，10K performance units，50 replays，1 GB attachments，1 cron monitors。
- 可以用 elk stack 可以用他们的云服务也可以自建，云服务十几刀一个月，自建可能差不多
- 我不想自建，节约时间成本对我来说更重要。我刚才看了一下 ELK Stack 的 Plan 最低要 $95 per month，相比起啊的选项有点贵。
- 排名前几的都是我们经常抄的产品

- ## There are 4 pillars of API observability:
- https://twitter.com/mjovanovictech/status/1765052411394097462
  - Metrics
  - Events
  - Logs
  - Traces
- Metrics measure values that determine API health. A few interesting metrics are throughput, latency, CPU usage, and memory usage.
- Events capture significant changes in the system. They also include contextual information about what happened.
- Logs capture important activity in the application and record the system actions. 
- Traces represent a record of a request's path through a distributed system.
- To make your API observable, you must instrument it with event listeners, agents, or libraries, which can collect metrics, events, logs, and traces.

- You can use telemetry data to create alerts to notify your team about potential issues. Another use case is visualization. Some services can ingest telemetry data and present them in a dashboard.

- ## Your job doesn't end when you deploy to production.
- https://twitter.com/RaulJuncoV/status/1729870028806443352
  - Logging
  - Monitoring
  - Alerting

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
