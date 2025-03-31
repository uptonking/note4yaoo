---
title: lib-saas-cms-community-workflow-automation
tags: [automation, community, saas, workflow]
created: 2025-03-25T19:15:06.939Z
modified: 2025-03-25T19:15:23.591Z
---

# lib-saas-cms-community-workflow-automation

# guide

# pm-workflow
- tips
  - ifttt
  - zapier alternative
# discuss-stars
- ## 

- ## 

- ## 
# discuss-ai-flow
- ## 

- ## 

- ## 
# discuss-automation-vendors
- ## 

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

- ## 🚀 [Trigger.dev - Show HN: We built a developer-first open-source Zapier alternative | Hacker News _202302](https://news.ycombinator.com/item?id=34610686)
- Trigger.dev looks like it would be amazing if you want a simplified temporal that is still 100% code based and exclusively in Typescript.
  - If you are looking for a Zapier-for-developer experience, we took an alternative route at Windmill of allowing Python/Javascript/Go/Bash as steps but the workflows are still GUI based

- Zapier has a python/JS code step (basically a AWS lambda) you can use to do something like this. Downside is that it has a timeout of 10s
  - And the second downside is that you don't necessarily get the same data as the normal no-code steps... It's still a mess to manage arrays and arguments auto-split by commas

- I tried node-red and I got frustrated having to do all this drag and drop stuff for something I could code easily.

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
# discuss-n8n
- ## 

- ## 

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
