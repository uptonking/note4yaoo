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

- Zapier has a python / JS code step (basically a AWS lambda) you can use to do something like this. Downside is that it has a timeout of 10s
  - And the second downside is that you don't necessarily get the same data as the normal no-code steps... It's still a mess to manage arrays and arguments auto-split by commas

- I tried node-red and I got frustrated having to do all this drag and drop stuff for something I could code easily.

- 
- 
- 
- 
- 

- ## [Ask HN: Why the Deluge(泛滥，洪水) of Zapier Alternatives? | Hacker News _202302](https://news.ycombinator.com/item?id=34763790)
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

- ## 

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
# discuss-activepieces
- ## 

- ## 

- ## [We do this at Activepieces (activepieces.com).](https://news.ycombinator.com/item?id=34615835)
- Is there an API or SDK for creating/managing flows? I want the flexibility to programmatically wire these integrations together rather than a nocode UI
  - Not yet, we're probably on the way there as we're exposing all our pieces (connectors) as typesafe npm packages. But for now, flows are built with the no-code UI. 
  - The workaround is to write all your code in one main Code step in any flow. Our web IDE is VS Code so it's not too much different, and we can be self-hosted.
  - On the UI, you can customize the credentials with a connection variable which is what enables in-app product integrations. We have users who are doing this. 

- 
- 
- 

- ## [We, at activepieces, had been using Depot. | Hacker News _202302](https://news.ycombinator.com/item?id=34902773)
  - Before depot we faced extreme slow builds for ARM-based images on github machines. 
  - However, using Depot helped us reduce the image build time from 2 hours (with an emulator) to just 3 minutes.
- I guess this is a good point, we all can easily have a cheap VPS/EC2 to speed up own docker image build. But maintaining a matrix of ARMv7, ARM64, X86/X64 instances, it is much more work to do. Than a simple powerful x64 instance.

- ## [Activepieces slow processing vs N8N - Discussions - Activepieces Community _202404](https://community.activepieces.com/t/activepieces-slow-processing-vs-n8n/3864)
  - I have been doing some testing with my ActivePieces setup vs N8N setup and where I love a lot the interface and to build flows much more than N8N… the processing time is just too slow I can’t use it in prod

- I have many ideas to make it faster. Do you mind decreasing Activepieces to a single worker and benchmarking again?

- The difference is that our sandboxing method requires a separate processor. So, if you call node index.js, the node itself has a large overhead (with separate namespaces). This is great for isolation and to support multi-tenancy.
  - In n8n, it uses a lightweight isolation (Whack a mole), which prevents it from supporting multi-tenancy with any npm packages or accessing the file system.
- There are many trade-offs to consider:
  - Security: Process Isolation + namespaces are stronger in terms of isolation because you are isolating the file system, CPU, and memory.
  - For Context: vm2 - npm 1 the n8n uses is already compromised. If you have a code piece, you can shut down the server from a code piece, which in a multi-tenant environment, you have to disable code pieces and other pieces like bash or pieces that access the file system.
  - Speed: Isolation without a new process is the clear winner.

- ## [Simplify Docker Container · Issue #627 · activepieces/activepieces _202302](https://github.com/activepieces/activepieces/issues/627)
  - I am currently using CasaOS as a docker container manager and I have noticed that to install activepieces in docker is a bit complex, since it requires several containers connected in the same docker network to work.
  - This is offered by n8n and I think it is a drawback for activepieces.

- I agree with you, and I will provide some background for the team. It's worth noting that CasaOS and RailwayApp do not offer support for Docker Compose. As a result, users are required to individually deploy and configure each Docker container, which can make the process more complex.
  - Currently, the activepieces are contained in a single Docker, but Redis and Postgres are kept separate. If you import it directly into CasaOS, the networks should function automatically. Additionally, I have renamed the services to correspond with the container names.

- ## [We built Activepieces: open source alternative to Zapier (business automation) : r/selfhosted _202301](https://www.reddit.com/r/selfhosted/comments/10pxkao/we_built_activepieces_open_source_alternative_to/)
- How is this different from n8n.io?
  - We released it under MIT which is a very permissive open source license, N8n is not open source in terms of its license. And we built the UX for non-technical users, N8n requires a higher technical understanding.

- I use Zapier & Integromat/Make on a daily basis. I'm a dev/marketer. The only issue I see with switching to your product is the lack of apps I need. Facebook Conversions, Google Conversions, TikTok Lead Forms, receiving webhook data, etc.

- 大多数讨论都是在请求integrations

- ## 🚀 [Launch HN: Activepieces (YC S22) – Open-Source Zapier Alternative | Hacker News _202302](https://news.ycombinator.com/item?id=34723989)
  - we decided to build an open source automation tool under a permissive license (MIT) with a simple user experience that doesn’t require technical knowledge, and can be self-hosted. 
  - We plan to make money from the cloud version and a future enterprise edition with advanced features - maybe advanced roles and permissions.

- Are there any programmatic methods to detect integration breakages? Simply relying on unit/integration testing with mock endpoint is not effective, as it cannot capture changes made by third parties. Being notified of breakages is a solution, but not the most ideal one. I've considered sourcing open API specs, like APIsguru.com, to scan for changes, but I was wondering if you have any other suggestions.
- you are likely to be alerted in a few ways of trouble with an integration:
  1. Exception handling. Whatever code you have polling API endpoints or processing inbound webhooks is likely to throw an exception if the structure of the API it's consuming or inbound webhook message formats have changed materially. I recommend handling via Sentry or a similar application error reporting mechanism for triage by your SRE or platform team.
  2. API responses. There is some peril here, as every API is different. Some APIs will behave as you'd expect with respect to error codes, error messages, and request allowances, while some APIs will reply with code 200 with the error message in the body. Again, this is the value incumbents offer;
  3. User reporting. If your unit tests didn't catch something, nor did your application error mechanisms, your users will absolutely let you know if a piece of JSON element landed where it shouldn't have in a target integration.
- Are you thinking of misc. sync errors here (auth issues, temporary downtime, etc.) or API changes? For API changes: It's not super scalable but I've used a changelog monitoring chat (Slack/Zulip/Discord) channel. Automated notifications for changelog updates for all integrated APIs. Maybe there's an assigned person for each integration and that person scans the changelog updates for their assigned services then emoji reacts to the notification messages when they have been reviewed and cleared (they create issues for required changes or confirm no changes needed).
  - That's an innovative idea, I like it! Was it straightforward to set up automated notifications for the other services? Did you encounter any challenges or problems along the way?

- What kind of testing have you done on app/DB performance under heavy load? Why are you indexing nearly the same thing thing twice in the AppConnection table?
  - You are correct, repeating the same index twice is a mistake. Thanks for hinting at that
- What kind of column is your pkey, as defined in BaseEntity? 
  - We are using `nanoid` for all entities, It's stored as varchar in the database.
- There are pros and cons to using random IDs as a PK. For RDBMS clustering on the PK (InnoDB), it's a terrible idea. If you're going to sort by the PK, it's usually a terrible idea (UUIDv1 isn't as bad since it includes the timestamp, but that assumes your access pattern is based on insertion time). There is ULID if you'd like something that's sortable. You could also just have a secondary index. An advantage can be that it _can_ be a good way (again, this depends heavily on your access patterns) to do sharding. My other concern for nano id is twofold, both around their PRNG. 

- I believe trigger is more focused on devs while this is more focused on others

- My biggest concern with these zapier alternatives is how easy is it to add an integration for services that aren't already in the system? I use several products which have APIs but are too small for n8n or this to have it baked in. Is there good documentation for this? A boilerplate "new plugin" setup so I can add my own?
  - Our framework streamlines the process by making pieces simple to define. You only need to specify the properties and the function to carry out the action. The core takes care of everything else, from authentication to the user interface.

- The goal is of course to build Enterprise features which are hard to replicate for others, but these imply more complex engineering challenges are being solved.
  - That could be plugins to integrate into other Enterprise tools like Snowflake or Salesforce for e.g.

- Lovely app. N8N's community contributions are licensed under the Apache license so would it be possible to download all their integrations and convert them into your format? Then you would have almost 400 apps.

- Can you talk about some of the differences with n8n except for the license?
  - I actually forgot to mention a very important differentiator. If you self-host N8n and you'd like to connect say your Asana or Gmail account, you have to own your own app or get an API key.
  - We have a cloud auth service, that even if you self-host us, you have the option to automatically connect your account with our predefine OAuth 2.0 app which makes the experience seamless if you don't want to take care of auth. We found that this is a very important feature to simplify the UX!
  - We think our UX is simpler for users who don't wish to get involved in too much technical understanding. We heard from many users that N8n was a bit too technical to them. 

- My perfect workflow is something like Config as code. So basically i could declare a JSON/TOML config, then when deployed, the visual diagram is set.
  - That's a decent feature. The main reasons we know of are versioning and IDE experience. We were designed API-first. They are clean, but undocumented yet. We currently have a draft PR that generates an OpenAPI specification. I think the next step for us would be a CLI to bring the code experience into the IDE.
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
