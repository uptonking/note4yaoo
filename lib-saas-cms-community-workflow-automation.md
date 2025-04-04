---
title: lib-saas-cms-community-workflow-automation
tags: [automation, community, saas, workflow]
created: 2025-03-25T19:15:06.939Z
modified: 2025-03-25T19:15:23.591Z
---

# lib-saas-cms-community-workflow-automation

# guide
- features
  - k8s
  - sandbox
  - bpmn
# pm-workflow
- tips
  - 与外部系统通信可考虑使用统一workflow平台, 内部模块间通信优先events/rpc

- products
  - ifttt
  - zapier alternative
# discuss-stars
- ## 

- ## 

- ## 
# discuss-bpmn(Business Process Management Initiative)
- ## 

- ## 

- ## 

- ## [Do you plan your automations in BPMN? : r/n8n _202502](https://www.reddit.com/r/n8n/comments/1ifzevz/do_you_plan_your_automations_in_bpmn/)
  - I am quite new to n8n. I worked 2 years in SAP Consulting (Junior Lvl) and what we used to do was bring all the planned processes in BPMN on paper and then actually implement it.

- There are two good reasons for BPMN diagrams:
  - you might be required to have them from regulatory perspective in some industries (e.g. banking, pharma, airplanes)
  - you want to improve a complex process with dependencies, multiple participants, interfaces, conditions - and then BPMN is just the beginning

- ## [换掉bpmn-js，让前端更熟悉工作流业务 - 知乎 _202206](https://zhuanlan.zhihu.com/p/528711473)
- 这里我们站在前端的角度先明确一下工作流、工作流管理系统、工作流引擎、BPMN规范、bpmn-js的关系。
- 我们把事情的拆分、组织、执行、最后到管理都搬到计算机上面来，就可以叫做工作流。
- 工作流引擎有很多，最常见的有Activiti、Camunda BPM、Flowable。
- 目前大部分开源的工作流引擎都支持BPMN规范，从图上节点、连线的具体含义到提交给工作流引擎的数据格式，都有给出了具体的定义
- bpmn-js是一个开源的实现BPMN2.0规范的web建模器。但是并不是提出BPMN规范的官方组织开发的。所以不代表工作流引擎支持BPMN规范，前端就一定要用bpmn-js。
  - 我们也可以基于BPMN规范重新开发一套符合自己业务的流程设计器。
- bpmn-js给我们带来了下面几个痛点。
  - 业务逻辑黑盒, 由于bpmn-js将所有的业务逻辑都在其内部实现，前端无法直接从代码层面对业务逻辑有直观的感受。这个时候如果出现一些在前端层面的修改，往往会因为缺乏一个约束，导致代码被修改的十分混乱。
  - bpmn-js对自定义并不是完全开放，虽然有很多预设场景的示例，但是并不能满足实际项目中所有的场景。
- 对前端来说，花费大量的精力去学习bpmn-js源码意义不大
  - 我们代码中更多的是对业务和UI的定义，并没有过多的去涉及BPMN规范。
  - 那么我们如何把这类业务的代码产生的数据转换为流程引擎可识别的内容呢？最方便的方法当前是让后端自己去转换，比如后端用Java就让他写一个filter。当然，很多时候后端不愿意做，我们也可以前端来转。
  - LogicFlow本身提供了一个插件bpmnAdapter，来实现LogicFlow数据与bpmn数据互转（json格式和xml格式都支持）。
- 在工作流项目中，一开始为了快速出成果，直接用bpmn-js也没有问题。而且很多项目可能只是给研发使用B端管理类项目，对UI也没有啥要求。
  - 但是随着项目的发展，特别是项目中开始出现产品角色，打算拿出去做商业化应用的时候。这个时候如果还是保留bpmn-js作为流程设计器，会给前端研发带来巨大的压力。在必要的时候，建议前端同学激进一点，选择更易维护的流程设计器来开发。
  - LogicFlow确实是一个比较好的选择，文档全、源码也易理解，使用后会将你从bpmn-js的痛苦中解脱出来。

- 虽然在BPMN2.0中，将流程执行语义分为Events(事件)、Gateways(网关)、Activities(活动)这三类要素，但是在实际项目中，我们并不需要按照BPMN规范来定义流程图的中内容，而是需要按照我们项目业务来定义流程图的内容。

- 
- 
- 
- 

# discuss-ai-flow
- ## 

- ## 

- ## 
# discuss-automation-vendors
- ## 

- ## 

- ## [Windmill.dev | Hacker News _202205](https://news.ycombinator.com/item?id=31272793)
- It has some resemblances with Airflow but one aim is to make it accessible to less technical users that can treat modules like blackbox. Similar to Zapier but the code is inspectable and editable at any point. 
  - At the core, it is a scheduler/orchestrator of script execution, so it's similar to Airflow in that sense, but the product is really not meant for the same usage.

- This looks very similar to airplane.dev, is that intended?
  - Airplane is focused on support, customer success or ops use cases (e.g. "I wrote a script to delete a user record / reset a 2fa token / etc, I can use Airplane to let the customer support team have access in a safe way"). Whereas I've seen other tools in this space target more of a "programmable Zapier" type use case (e.g. "For every new customer, I want to use a Python script to hit the Slack API and generate a custom notification.")

- 
- 
- 

- ## 🤔 [Ask HN: Why the Deluge(泛滥，洪水) of Zapier Alternatives? | Hacker News _202302](https://news.ycombinator.com/item?id=34763790)
- Speaking only for us (trigger.dev founder here): In our last X products we've used two different solutions for accomplishing two tasks together: event-driven architecture and integrating 3rd party APIs. 
  - We noticed that these two concerns were intertwined, and weren't happy with how the existing solutions only solved for just 1 (leaving us to build the other). 
  - We also noticed how well tools like n8n and Zapier solved these problems, but at the UI layer, and we wanted something like those tools but in code. Hence the creation of trigger.dev.

- Cause Zapier is a business that doesn't have a moat(护城河).
  - The only thing I could think of to make a moat would be to become some sort of “compliance plumber”. Get FedRAMP High and some other capabilities and it could become the “enterprise” way to transport and transform data between cloud or other systems.

- Activepieces: We used Zapier for a long period of time and ran into many issues that we weren’t able to fix by ourselves because of the closed app ecosystem, and had to pay increasing bills for simple tasks that could cost literally zero if we do them in code.
  - Later, we came across many people with similar problems and more; like not being able to process their data on their own machines, and that’s were we got inspired.
  - the real answer imo is that there is a rising movement for open-source alternatives that are loud about being alternatives to proprietary software, that’s why you read it every week very explicitly.
# discuss-triggerdotdev
- ## 

- ## 

- ## 

- ## 💫 Move your background jobs to the foreground with Realtime _20250402
- https://x.com/triggerdotdev/status/1907117019713122749
  - Stream AI responses, with full observability built-in
  - Show progress states on your frontend by subscribing to your runs
  - Use metadata to provide detailed context for your users
  - ✨ task执行的进度动画非常友好
  - Forward streams through the Realtime API to provide real-time updates to your users from any AI providers ( @aisdk , @openai , @AnthropicAI etc).
  - We also provide Realtime React hooks that allow you to securely interact with the Trigger API from your @reactjs apps.

- ## 🚀 [Trigger.dev - Show HN: We built a developer-first open-source Zapier alternative | Hacker News _202302](https://news.ycombinator.com/item?id=34610686)
- Trigger.dev looks like it would be amazing if you want a simplified temporal that is still 100% code based and exclusively in Typescript.
  - If you are looking for a Zapier-for-developer experience, we took an alternative route at Windmill of allowing Python/Javascript/Go/Bash as steps but the workflows are still GUI based

- Zapier has a python/JS code step (basically a AWS lambda) you can use to do something like this. Downside is that it has a timeout of 10s
  - And the second downside is that you don't necessarily get the same data as the normal no-code steps... It's still a mess to manage arrays and arguments auto-split by commas

- I tried node-red and I got frustrated having to do all this drag and drop stuff for something I could code easily.

- 
- 

# discuss-n8n
- ## 

- ## [Wait for a trigger during the execution - Feature Requests - n8n Community _202311](https://community.n8n.io/t/wait-for-a-trigger-during-the-execution/32786/2)
  - The idea is: to be able to wait for an event (a trigger ideally) in the middle of an execution. 
  - Close to the current Wait block, we want to pause the execution and wait for the trigger to happen (filtered by a correlation key to select the right execution to resume) before going to the next node.

- It would be like a trigger/event in the middle of an execution.

- since this post was published this node was improved ans now includes the wait for a webhook call. So it seems to fit the need

- ## 📡 [Using reusable elements for n8n workflows - Tips & Tricks - n8n Community _202406](https://community.n8n.io/t/using-reusable-elements-for-n8n-workflows/48624)
  - This is an example of how you can create reusable steps in n8n instead of having to recreating these steps and workflows a fresh
  - You can use the execute node to call a workflow inside the workflows that will then return the desired data back
  - Use a webhook endpoint to call the workflow and set the response endpoint to last node or webhook

- Yeap, I’ve often ran into the need for this too, and arrived at the same solution. The downsides to this are:
  - When run, this shows up as a different workflow executions. This may make it harder to troubleshoot.
  - If you have two different instances of N8N (like separate environments) and export from one and import into the other, then the workflow ID’s will be different and this will break. I had to come up with an export/import script that patches workflow ID’s.
- It would be great if N8N implemented a native feature by which you could reuse parts of your workflow, like with BPMN Call Activities.

- ## [n8n.io - A powerful workflow automation tool | Hacker News _202308](https://news.ycombinator.com/item?id=37274052)
- free version is quite restricted when it comes to user management, etc, can't even think about oidc integration. 

- The problem I see in n8n is that a lot of the integrations seem a little half baked. 
  - you have an FTP node, but it doesn't work with FTP over TLS
  - you have an AWS SES node, but cannot attach files to the email

- I evaluated this as a sort of batch job UI for internal staff, but it doesn't handle even moderately large files and has no concept of streaming.
  - If you want to do a basic task like download and load a file into a database, n8n doesn't work well unless the file will fit entirely into memory.
- This is the default behavior. There is an env variable to store the data to disk.
  - `N8N_DEFAULT_BINARY_DATA_MODE: filesystem`

- Someone should look at a very different take on this space based on cause and effect based modeling.
  - DX based on cause and effect is a.lot more intuitive for users and reasoning agents

- ## 🚀 [N8n.io – Workflow automation alternative to Zapier | Hacker News _201910](https://news.ycombinator.com/item?id=21191676)
- Zapier has about 1, 000 integrations, more than any of their closest competitors and at a price that is far less than others in their space. 
  - What you've done here is great! The UX seems better than Zapier and the extensibility & community approach terrific. The key, though, is going to be adding integrations rapidly. 
- I might also stress: 
  - Bulk actions. 
  - Sync actions. 
  - And support for other programming languages (eg. python)

- I wonder why, in this era of Swagger / OpenAPI / Postman Collections / API Gateways ... why this is so difficult? I feel like there was a promise that integration would become more magical at a rapid clip, but as it stands it just seems like there are more options but no less headaches.
  - A lot of APIs don’t support the tooling you mentioned, have all sorts of rough edges (return improper http codes, or don't return them at all), or act...quirky at scale (based on my experience at an automation workflow org).

- Crowded space, but darn few (if any) shared source or community based solutions. Here's a several examples from a market study I did in 2018: Workato, Apiant, Inegromat, Snaplogic, CloudHQ, Boomi, Tibco, Jitterbit, AWS Lambda, Mulesoft, Tray.io, ApacheNiFi, Stringify, Adeptia, Kotive, Cazoomi, Scribesoft and several more.
  - I really think the community angle is unique.

- 🆚️ How is this different from node-red?
  - Loosely speaking Node-RED has a superset of the functionality this project has, sacrificing customization/generality for simplicity.
  - Zapier and n8n interface with the user via a catalog model.
  - Node-Red is more low-level. You can already see it in the way it describes itself "Flow-based programming for the Internet of Things". So it is "programming" what n8n does not try to be.
  - Other tools that can achieve similar results (using Directed Acyclic Graphs, where the nodes represent the execution of your code for a desired pre-programmed task) are Airflow, Flink, NiFi, Dagster, Dagobah, Celery, and many more.
# discuss
- ## 

- ## 

- ## 

- ## 🆚️ [I tried n8n, Automatisch and Activepieces: here's what I think. : r/selfhosted _202308](https://www.reddit.com/r/selfhosted/comments/163vmtt/review_i_tried_n8n_automatisch_and_activepieces/)
- They all claim to be a worthy replacement for Zapier.
- Automatisch
  - It appears it doesn't have the IMAP module so I couldn't check the mailbox so my use case was already not possible. 
  - I found it incredibly tedious to install and I wasted an entire night on this only to find basic stuff (imo) not being available
- Activepieces
  - I like the way it showed how it works on the website. It was very appealing and actually my first choice given I'd seen that n8n has paid plans for imo basic features (variables). 
  - This app has potential but I find that if all modules are setup like IMAP is they'll most likely lack too much to be able to customize the smaller details.
- n8n
  - This app is way more elaborate than the other two. By having such a greatly worked out IMAP module this became my Automator of choice to use next to Google Apps Scripts. 

- One downside of N8N is that apps have to be installed through API keys, rather than through an interactive oath authentication like some other apps, like AppSmith for instance.

- Do you know or did you manage to find the restrictions on the free self hosted n8n? 
  - The main things I saw monetized was using global variables and sharing flows.
