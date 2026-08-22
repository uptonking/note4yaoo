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
  - paid: permissions, Audit logs, Collaborate using Git, Customize branding
    - open: Flow History, Custom Pieces	
    - [Editions - Activepieces](https://www.activepieces.com/docs/about/editions)
  - 💫 node节点的执行进度无法实时显示，动画体验不如triggerdotdev
    - 动画进度比较成熟的是comfyui，但体验待改进

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

- tips
  - ?

- resources
  - [280+ Open Source MCPs · Activepieces](https://www.activepieces.com/mcp)
# draft
- workflow ui by maxgraph/logicFlow

- bpmn adapter/pieces
# dev-xp
- published flow在off状态也会一直执行?
  - 似乎与flow重命名相关，在flow列表重命名后，存在旧flow和新flow同时执行的问题
  - 临时方案是，手动设置为off，再设置为on
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
