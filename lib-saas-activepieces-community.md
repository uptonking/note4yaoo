---
title: lib-saas-activepieces-community
tags: [activepieces, community]
created: 2025-03-31T17:38:20.324Z
modified: 2025-03-31T17:39:01.892Z
---

# lib-saas-activepieces-community

# guide

# discuss-stars
- ## 

- ## 

- ## ✨ [Approval Step · Issue · activepieces/activepieces _202304](https://github.com/activepieces/activepieces/issues/1078)
  - Because these workflows can have branches, loops, events etc, they are very much like programming languages. 
  - There exist standards like BPMN, SMMN, DMN etc and various software like jBPM, Camunda, Flowable to model and execute these.
  - It would be really great to be able to create workflows like these in ActivePieces because so much of the required work has already been done.
  - This will make it possible to embed ActivePieces based automations right inside actual business processes while making use of ActivePieces's existing infra that supports branching/looping/delay and a canvas-based workflow editor.

- ✅ Done and will be released in 0.5.0_202307

- This is a good start but a YES/NO, APPROVE/REJECT flow fundamentally, is about collecting a single bit of data from a human actor. 
  - IMHO, a more general and powerful flow would be sending an incomplete JSON object - to be rendered as an HTML form - and receiving a completed one from the person.

- ## 🚀 [Launch HN: Activepieces (YC S22) – Open-Source Zapier Alternative | Hacker News _202302](https://news.ycombinator.com/item?id=34723989)
  - we decided to build an open source automation tool under a permissive license (MIT) with a simple user experience that doesn’t require technical knowledge, and can be self-hosted. 
  - We plan to make money from the cloud version and a future enterprise edition with advanced features - maybe advanced roles and permissions.

- 🤔 Are there any programmatic methods to detect integration breakages? Simply relying on unit/integration testing with mock endpoint is not effective, as it cannot capture changes made by third parties. Being notified of breakages is a solution, but not the most ideal one. I've considered sourcing open API specs, like APIsguru.com, to scan for changes, but I was wondering if you have any other suggestions.
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

- 🆚️ I believe trigger is more focused on devs while this is more focused on others

- My biggest concern with these zapier alternatives is how easy is it to add an integration for services that aren't already in the system? I use several products which have APIs but are too small for n8n or this to have it baked in. Is there good documentation for this? A boilerplate "new plugin" setup so I can add my own?
  - Our framework streamlines the process by making pieces simple to define. You only need to specify the properties and the function to carry out the action. The core takes care of everything else, from authentication to the user interface.

- The goal is of course to build Enterprise features which are hard to replicate for others, but these imply more complex engineering challenges are being solved.
  - That could be plugins to integrate into other Enterprise tools like Snowflake or Salesforce for e.g.

- Lovely app. N8N's community contributions are licensed under the Apache license so would it be possible to download all their integrations and convert them into your format? Then you would have almost 400 apps.

- 🆚️ Can you talk about some of the differences with n8n except for the license?
  - I actually forgot to mention a very important differentiator. If you self-host N8n and you'd like to connect say your Asana or Gmail account, you have to own your own app or get an API key.
  - We have a cloud auth service, that even if you self-host us, you have the option to automatically connect your account with our predefine OAuth 2.0 app which makes the experience seamless if you don't want to take care of auth. We found that this is a very important feature to simplify the UX!
  - We think our UX is simpler for users who don't wish to get involved in too much technical understanding. We heard from many users that N8n was a bit too technical to them. 

- My perfect workflow is something like Config as code. So basically i could declare a JSON/TOML config, then when deployed, the visual diagram is set.
  - That's a decent feature. The main reasons we know of are versioning and IDE experience. We were designed API-first. They are clean, but undocumented yet. We currently have a draft PR that generates an OpenAPI specification. I think the next step for us would be a CLI to bring the code experience into the IDE.
  - That's a decent feature. The main reasons we know of are versioning and IDE experience. We were designed API-first. They are clean, but undocumented yet. We currently have a draft PR that generates an OpenAPI specification. I think the next step for us would be a CLI to bring the code experience into the IDE.
# discuss-news
- ## 

- ## 

- ## 

- ## ⚖️ Introducing Activepieces MCP servers _20250401
- https://x.com/activepieces/status/1906765827460026842
  - we've turned every integration on our platform (all 280+ of them) into an MCP server that you can run completely free on our cloud or self-host it.
  - every new community-contributed Piece (integration) added to our platform will automatically become a new MCP server available to everyone.
  - Activepieces handles all app authentication, letting you connect your AI to any app with just a click.
  - In the coming weeks, we’ll be rolling out improvements to our MCP servers that will make building powerful AI agents and workflows 100x better.

- ## 📈 Google Sheets is your most used piece. That's why we are so excited to introduce Tables _20250316
- https://x.com/activepieces/status/1901006256049131750
  - This is another step in our growing suite of products designed to empower the future of work and eliminate those "No Joy" tasks in the most user-friendly way possible.  
  - you get fast, built-in sheets right inside your workflows.  
- no more
  - Creating sheets just to support automation  
  - Waiting on slow webhook responses and connectivity issues with Google Sheets  
  - Data scattered everywhere between Activepieces and other 3rd party platforms

- We just slipped in 2 new upgrades for table _20250330:
  - https://x.com/activepieces/status/1906280824682459578
  - single select fields
  - rename field. These updates are live 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## 

- ## [Parallel execution · Issue · activepieces/activepieces _202305](https://github.com/activepieces/activepieces/issues/1204)
  - There are some use cases where having a parallel branch could be more comfortable. An example is when you have to send multiple notifications using different pieces, you don't care about fails nor of their sequence execution.
  - The same could be achieved in other ways, such as sending multiple requests on other flows, but this would be uncomfortable.

- These ideas (Parallel converging gateways) have been explored in BPMN
# discuss
- ## 

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

- ## [Simplify Docker Container · Issue · activepieces/activepieces _202302](https://github.com/activepieces/activepieces/issues/627)
  - I am currently using CasaOS as a docker container manager and I have noticed that to install activepieces in docker is a bit complex, since it requires several containers connected in the same docker network to work.
  - This is offered by n8n and I think it is a drawback for activepieces.

- I agree with you, and I will provide some background for the team. It's worth noting that CasaOS and RailwayApp do not offer support for Docker Compose. As a result, users are required to individually deploy and configure each Docker container, which can make the process more complex.
  - Currently, the activepieces are contained in a single Docker, but Redis and Postgres are kept separate. If you import it directly into CasaOS, the networks should function automatically. Additionally, I have renamed the services to correspond with the container names.

- ## [We built Activepieces: open source alternative to Zapier (business automation) : r/selfhosted _202301](https://www.reddit.com/r/selfhosted/comments/10pxkao/we_built_activepieces_open_source_alternative_to/)
- How is this different from n8n.io?
  - We released it under MIT which is a very permissive open source license, N8n is not open source in terms of its license. And we built the UX for non-technical users, N8n requires a higher technical understanding.

- I use Zapier & Integromat/Make on a daily basis. I'm a dev/marketer. The only issue I see with switching to your product is the lack of apps I need. Facebook Conversions, Google Conversions, TikTok Lead Forms, receiving webhook data, etc.

- 大多数讨论都是在请求integrations
