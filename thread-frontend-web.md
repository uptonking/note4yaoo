---
title: thread-frontend-web
tags: [frontend, web]
created: '2020-12-05T07:43:47.005Z'
modified: '2020-12-05T07:44:12.022Z'
---

# thread-frontend-web

## pieces

 

- ### A year ago I made a bet on full-stack JS and switched my focus from @laravelphp to Node.js. A year later, I found that Node mostly just slowed me down.
- https://twitter.com/tylerlwsmith/status/1341557868571422722
- Server-rendered React components look really exciting. 
  - I just wish the Node ecosystem was less fragmented and more productive so it would be easier to take full advantage of it.
  - Until then, I can continue to get a ton of productivity out of Laravel 
- React Router is the reason I love React. 
  - It also has the most innovative front-end libraries, and the front-end is the part that users interact with. 
  - React also works great with extremely complicated state management.

- ### [Reflecting on a year with Node.js and why I should have stuck with Laravel_202012](https://dev.to/tylerlwsmith/reflecting-on-a-year-with-node-js-and-why-i-should-have-stuck-with-laravel-e5a)
- Earlier this year, I was two months into building a full-stack JavaScript app. 
  - I used an Express server, set up Next.js for server-side rendering, added Chokidar for instant server reloading, used Next.js's Webpack config to compile my server's TypeScript code, hooked up cookie authentication with Argon2 encryption, found the perfect Node ORM, and had the app running in separate containers for Node, PostgreSQL and Redis.
- After two months of hard work, all I had built was a mediocre server-rendered CRUD app hacked together with two-dozen NPM libraries. 
  - If I had used Laravel and jQuery, I could have built this all in a weekend.
- After a year of building Node.js apps, I discovered I was spending more time piecing together tools than writing application code. 
  - 这是因为基于php的传统web开发框架laravel已经非常成熟，工具丰富
    - 基于nodejs作为服务端的web开发框架，还处于快速发展阶段，可选工具不够多，并且功能不够丰富
  - Laravel gives me 80% of my tooling out-of-the-box for 20% of the work. 
  - If moving fast is important to you, you should consider batteries-included frameworks like Laravel and Rails first.
- What I've learned is if you want to develop applications quickly, it isn't about staying in one language: 
  - it's about reaching for the tools that let you move quickly, whatever those are.
  - I use React for most of my front-end web applications, and Laravel gives me the tools I need to spin up the backend quickly. 
- Rather than sharing code between the front-end and back-end, I've learned to 
  - move almost all of my business and validation logic to the back-end, 
  - and I consume it on the front-end via API. 
  - Just because you're using two different languages doesn't mean you need to write the same code twice.
- I prefer Laravel over Node.js because it lets me move fast.

- discussion
- I like Adonis. And Sails.js. And Nest.js. Loopback also looks cool.
  - I've never adopted any of them for a few reasons though:
    - 总结：支持node的大公司少了，工具不多
    - Lack of adoption. 
      - None of the batteries-included Node.js frameworks have major adoption, so I have to figure out how to integrate other tools myself.
      - It also means if I run into a problem, there are far fewer resources available than Laravel.
    - Uncertain future. 
      - Adonis is mostly carried by one person. Sails is maintained by a company out of Texas. 
      - For long term projects, using Adonis feels like a risk.
    - Lack of first-party integrations
      - Laravel kills it with the amount of first party integrations they have. 
      - It's a compelling reason to choose Laravel over Node

- ### if I was building a CMS using MongoDB would you tell me to stop immediately? If so, why?
- https://twitter.com/JakeDohm/status/1341892219511459842
- Every developer build a CMS at some point in their career. 
  - Might as well check it off of your bucket list.
- I’m going to get technical and ask what type of content your CMS would be housing. 
- That would determine DB for me. 
- Mongo doesn’t seem appropriate for most content I’ve worked with, as CMS tends to be highly relational.
- Maker me: Build whatever you want with whatever tools you want.
- Developer me: Don't use MongoDB, most of your stuff with be relational, 
  - and in the event you cannot use relational, use JSONB data type in PostgreSQL.
