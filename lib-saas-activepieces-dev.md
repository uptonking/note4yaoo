---
title: lib-saas-activepieces-dev
tags: [activepieces, dev, workflow]
created: 2025-03-31T17:38:00.759Z
modified: 2025-03-31T17:38:17.881Z
---

# lib-saas-activepieces-dev

> All-in-one AI automation designed to be extensible through a type-safe pieces framework

# guide
- pros
  - MIT license + enterprise
  - Pieces are npm packages in TypeScript
    - offering full customization with the best developer experience, including hot reloading 
  - ⌛️ Flows are fully versioned
  - AI-First: Native AI pieces let you experiment with various providers, or create your own agents using our AI SDK
  - Secure by Design: Self-hosted and network-gapped for maximum security and control over your data.
  - ecosystem: supports integrations with Google Sheets, OpenAI, Discord, RSS, and over 200 other services
    - integrations are versioned and published directly to npmjs.com
  - [Autoscaling](https://www.activepieces.com/docs/install/architecture/autoscaling)

- cons
  - api keys 是付费
  - table默认按插入顺序排序， 不支持按column如date/number排序
    - Default Maximum Records per Table: 10,000
    - Default Maximum Fields (Columns) per Table: 100 
    - flow显示owner, 但table未显示owner
  - pieces search非常慢: 优先显示内置， 动态加载其他pieces
  - schedule不支持自定义间隔, 如 10s/90s
    - 如果工作流复杂， 可能一次未执行完就开始下一次
    - 💡 loop + delay 似乎支持自定义秒, 可妙用1-60来利用loop, 一个schedule内loop6个数字并设置 10s delay
  - code step似乎不支持 DOM 操作
    - 不支持prettier/format
    - `setTimeout` does NOT work inside the Code step: SANDBOX_CODE_ONLY, the Code step executes in a pure V8 isolate without Node.js web API. Use Activepieces' built-in Delay piece (Delay For), which is designed specifically for this.
  - 💰 paid: permissions, Audit logs, Collaborate using Git, Customize branding
    - templates, Control Pieces
    - Event Streaming: Forward every audit event we emit to a webhook, then handle it elsewhere
    - Embedding
    - ee: SSO, RBAC, API keys, Secret Managers
    - [Editions - Activepieces](https://www.activepieces.com/docs/about/editions)
    - open: Flow History, Custom Pieces
  - 💫 node节点的执行进度无法实时显示，动画体验不如triggerdotdev
    - 动画进度比较成熟的是comfyui，但体验待改进
  - 提供了类似dify/coze的工作流，但ai相关的feature不突出，整体功能太传统

- Technical limits 🛑
  - ⚠️ Execution Time: Each flow has a maximum execution time of 600 seconds (10 minutes). Flows exceeding this limit will be marked as a timeout.
    - Flow run in a paused state, such as Wait for Approval or Delay, do not count toward the 600 seconds.
    - The execution time limit can be worked around by splitting the flows into multiple ones, such as by having one flow call another flow using a webhook, or by having each flow process a small batch of items.
  - ⚠️ Memory Usage: During execution, a flow should not use more than 128 MB of RAM.
  - ⚠️ Maximum File Size: 10 MB
    - The files from actions or triggers are stored in the database/S3 to support retries from certain steps.
  - ⚠️ Some pieces utilize the built-in Activepieces key store, such as the Store Piece and Queue Piece.
    - Maximum Key Length: 128 characters
    - Maximum Value Size: 512 KB

- features
  - Human in the Loop: Delay execution for a period of time or require approval. 
  - Builder Features: Loops, Branches, Auto Retries, HTTP
  - Keep It Simple: accessible for everyone, regardless of their background and technical expertise
  - Keep It Extensible: Automation pieces framework has minimal abstraction and allow you to extend for any usecase
  - 将计算类的任务如文件转换都作为模版提供了

- tips
  - devops领域的cicd就是典型的工作流系统, 并且经常涉及到外部files/sandbox
  - task > workflow > pipeline

- usecases(AI也能设计实现工作流, 但AI需要server/环境/runtime来执行任务)
  - 所有的定时任务都可以是简单的工作流: All scheduled tasks go there. Mostly backups.
  - 多步骤的任务, 使用工作流操作会很清晰
  - 数据/文件处理转换， 批处理
  - 爬虫， RSS
  - 状态监控
  - 通知别人， 通知收集， 邮件处理
  - git devops: cicd

- resources
  - [280+ Open Source MCPs · Activepieces](https://www.activepieces.com/mcp)
# draft
- workflow ui by maxgraph/logicFlow

- bpmn adapter/pieces
# dev-xp
- step点击 test 后， 测试数据才会出现在下个step的输入框

- published flow在off状态也会一直执行?
  - 似乎与flow重命名相关，在flow列表重命名后，存在旧flow和新flow同时执行的问题
  - 临时方案是，手动设置为off，再设置为on

- the whole flow works now: step1-schedule-every-5-minutes, step2-send-http-get, step3-code-transform, step4-create-records-in-table.
  - If no posts match your keywords, the items array is empty ([]). If you pass an empty array to Tables: Create Record(s), Activepieces throws an error: "Error: No records provided".
  - NodeSeek posts have incremental numeric IDs (guid). Because a post stays in the RSS feed for several hours (spanning dozens of 5-minute runs), we save the latest seen ID in the built-in Storage piece. On every run, any post older than or equal to that ID is discarded.

- 
- 
- 
- 
- 
- 

- The Storage piece (piece-store) in Activepieces is a low-level Key-Value Store (persisted under the hood in the store-entry database table).
  - Because it stores raw key-value pairs (intended for cross-step caching, state tracking, and deduplication), Activepieces does not provide a dedicated standalone "Storage" viewer page in the left sidebar.
  - Method 1: The Quickest Way in UI (Add a "Storage → Get" Test Step)
  - Method 2: Check the Flow "Runs" History, look at Step Details → Input
  - Method 3: Create a new flow named Get NodeSeek Posts, Select Webhook → Catch Webhook, Publish the flow, Expose a Live Browser URL (View as JSON in your browser) 
  - Method 4: Directly on the VPS using cli, /opt/apps/llm-hub-lite/shared/data/prod/flowy/config/pglite 

## table

- table默认按插入顺序排序， 不支持按column如date/number排序
  - The Backend hardcodes the order, rows are permanently loaded in the order they were created in the database: oldest at the top, newest appended at the bottom.
  - In packages/server/api/src/app/tables/record/record.service.ts, change line 85

- If your table reaches 10, 000 rows, any future Tables: Create Record(s) step will throw an error and fail the run.
  - Default Maximum Records per Table: 10, 000 
  - Default Maximum Fields (Columns) per Table: 100 
- Because you self-host Activepieces (flowy), you can configure these limits to whatever number you want using environment variables.
  - AP_MAX_RECORDS_PER_TABLE
  - AP_MAX_FIELDS_PER_TABLE

- You can create a second small housekeeping flow
  - Step 2: Tables → Find Records: Filter: pubDate Less Than (e.g. 30 days ago).
  - Step 3: Tables → Delete Record(s).

- 
- 
- 
- 
- 

- Column names in Activepieces Tables are case-sensitive.

- 将 js 的 datetime 插入 table 的 Date & Time 列
  - option 1: new Date() , 数字可以直接插入
  - option 2: new Date().toISOString()
- NodeSeek's date format (`Sun, 20 Sep 2026 14:10:29 GMT`) is standard RFC 822 / RFC 2822. JavaScript's built-in `new Date(...)` natively parses this format without any extra library. Calling `.toISOString()` converts it directly to standard ISO 8601 (`2026-09-20T14:10:29.000Z`), which is exactly what Activepieces' "Date & Time" column expects.

- you cannot change the type of an existing column directly in-place. 
  - column updates only allow modifying the column name
  - Column data types are immutable once created.
  - You should delete the old column and re-add it as "Date & Time" (or create a new column)

## schedule/cron

- 对于schedule类型的任务， 当flow处于published状态但code未执行时， ui显示的状态是 `Paused`, 当code执行时显示的状态是 `Running`.

- i plan to create a schedule that runs every 1 minute, then try to create a  loop for number 1-6, then for every number run a code step  with 10s delay. it seems that this code step can run every 10s finally.
  - setTimeout does NOT work inside the Code step, SANDBOX_CODE_ONLY, the Code step executes in a pure V8 isolate without Node.js web APIs. Use Activepieces' built-in Delay piece (Delay For)
  - If you do 6 iterations with 10s delay, plus the HTTP request latency (~1s) and step execution time, each loop takes ~11s. Run 5 iterations with a 9-second delay.
  - 

- How to Run It Every 10 Seconds (The Webhook Method) 
  - Any interval shorter than 60, 000 ms or standard cron with seconds is rejected by the schema validator.
- The standard way to bypass the 1-minute scheduler limit is to turn your flow into an on-demand webhook, and let an external timer trigger it
  - Change the piece from Schedule to Webhook.
  - Run a lightweight loop that calls the webhook every 10 seconds

```sh
   while true; do   
     curl -s -X POST "https://flowy.aichorage.de/api/v1/webhooks/<your-webhook-id>" > /dev/null       
     sleep 10   
   done  
```

- Option B: As a systemd service (Auto-starts on VPS reboot)

- Cloudflare Rate Limiting / IP Ban (High Risk):   
  - Polling every 10 seconds = 6 times a minute = 8, 640 requests a day
  - NodeSeek is behind Cloudflare. Continuous 10-second polling from a single VPS IP will very likely trigger Cloudflare's bot challenge or return 429 Too Many Requests.
- If you check the XML header of https://rss.nodeseek.com, it includes `<ttl>60</ttl>`. NodeSeek caches its RSS feed on the server side; it does not re-generate with every second.

- Standard 5-field cron (minute hour day month weekday): Supported (e.g. * * * * * for every 1 minute).
- 6-field cron with seconds (second minute hour day month weekday): Not supported.

- 
- 
- 

## 🐛 api key

- The backend determines edition-specific module registration; API key functionality is entirely omitted in CE.
  - Although the core code includes database entities and authentication logic for API keys, they are disabled in the CE version via hardcoded plans and feature hooks. Therefore, setting the edition does not bypass CE restrictions
- Can it be enabled by simple configuration? 
  - platform.plan.apiKeysEnabled is false (which is hardcoded for CE).
- Is it easy to implement via a fork without licensing issues? 
  - very easy
  - the authentication and database layer for API keys is already built into the Community Edition core.
  - The React UI page and dialog live at packages/web/src/app/routes/platform/security/api-keys/ (MIT licensed). It is only hidden/locked
  - Option A: Fork and Implement Clean-Room in CE (Recommended for Long-term Use)
    - Create a CE API Key Service & Controller
    - Register in app.ts under Community Edition
    - Update Core Authenticate Import
    - Enable the Frontend Flag
  - Option B: Headless Usage Without Forking or Modifying Code
    - Since ApiKeyEntity and authenticateOrThrow are already compiled and active in CE
    - Generate a random 64-char key, Insert it directly into the api_key table in your Postgres/SQLite database
    - Minting Custom Long-Lived JWT Tokens 

Option B: Headless Usage Without Forking or Modifying Code
If your goal is external integration or headless usage on standard CE without maintaining a fork, there are three practical workarounds:
Direct Database Insertion (Instant API Key without code change)
Since ApiKeyEntity and authenticateOrThrow are already compiled and active in CE:
Generate a random 64-char key starting with sk- (e.g. sk- + 61 alphanumeric characters).
Compute its SHA-256 hash.
Insert it directly into the api_key table in your Postgres/SQLite database:
INSERT INTO api_key ("id", "platformId", "displayName", "hashedValue", "truncatedValue", "created", "updated")
VALUES ('apiKeyId123', 'yourPlatformId', 'External Service', '<sha256_hash>', '1234', NOW(), NOW()); 
Requests with Authorization: Bearer sk-... will be accepted by CE immediately.
Minting Custom Long-Lived JWT Tokens
Activepieces CE verifies JWT access tokens against AP_JWT_SECRET (configured in your .env or Docker environment).
You can write a 10-line script to mint a JWT signed with AP_JWT_SECRET for your user principal with an expiration of 1 to 10 years:
jwt.sign({
  id: "<user_id>", 
  type: "USER", 
  platform: { id: "<platform_id>" }
}, process.env. AP_JWT_SECRET, { expiresIn: "3650d" })
CE will accept this Bearer <jwt> token indefinitely for headless operations.
Automated Session Sign-in
Call POST /v1/authentication/sign-in with your CE email/password. It returns a standard JWT valid for 7 days, which external services can cache and rotate weekly.

# codebase

# [changelog](https://www.activepieces.com/docs/about/breaking-changes)
- 0.50.0_20250330
  - [feat: make mcp stateless](https://github.com/activepieces/activepieces/pull/7261)
  - It does no longer require the load balancer to be sticky
# more
- [Autoscaling](https://www.activepieces.com/docs/install/architecture/autoscaling)
  - Everything is queue-backed: webhooks and recurring jobs land on Redis, and workers poll them off it. A spike does not drop work.  It queues and drains as slots free. For exactly what survives a crash, what runs at-least-once, and where each promise stops
  - To scale Activepieces, add replicas of the workers, the app, or the Postgres database. A small Redis instance is enough.
  - Workers are the unit you scale — one worker runs one flow at a time 
