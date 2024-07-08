---
title: lib-fwk-nodejs-feathers-community
tags: [backend, community, feathers]
created: 2023-01-12T16:33:42.410Z
modified: 2023-01-12T16:33:52.048Z
---

# lib-fwk-nodejs-feathers-community

# guide

# discuss-stars
- ## 

- ## 
# discuss-roadmap
- ## 

- ## [Forward to Feathers v6 - back to the basics _202406](https://github.com/feathersjs/feathers/discussions/3498)
- Feathers v6 (no bird name) will be a return back to the basics, focusing on the things that Feathers has always been good at - services, hooks and HTTP and real-time APIs
  - It will be based on modern web standards and work with NodeJS, Deno, BunJS and Cloudflare Workers. 
  - Everything else will be moved back to the ecosystem - making things a little less batteries included and better separated will leave more options for choosing the best database, authentication and framework integration for your needs.

- v5 was a very ambitious release. Too ambitious as it turned out. We've always accomplished a lot for the very limited resources that this project had but this time, the direction wasn't ideal
  - It was also bad timing with some tough times in the tech industry combined with GPT and friends essentially killing open source consulting as a business (at least in this case).
  - Since the beginning of last year things have gone from the previously one or two paid support/consulting requests per month to literally zero.
  - While before it may have made sense to officially support multiple databases, frameworks, languages and authentication methods in order to drive consulting, that is no longer the case and I am not expecting that to come back

- To this day, Feathers is the only one that has a unified approach for HTTP and real-time APIs. 

- Authentication is hard. we finally came to the conclusion that the best way to continue solving this problem in a sustainable way is a developer-friendly service. For the past few months we have been working on Feathers Cloud Auth which lets you add scalable and secure, user-owned authentication to any NodeJS, Deno, Cloudflare, BunJS and browser application with just a few lines of code. 

- We really like our database adapters. The common syntax and CRUD functionality makes it easy to get started quickly. However, we made a mistake in the separation of concerns by having the adapter be the same thing as the externally accessible service. You end up having to do a lot of convoluted things when you want different data returned than what is in the database or depending on whether it is accessed internally vs external.
  - This is why we started Wings. It's the same thing as the existing data adapters but not intended for external access. 
  - They can also be used with any framework and are no longer limited to just Feathers.

- everything else - the authentication modules, the Express, Koa and Socket.io adapters, schema and TypeBox integrations will be moved to the Ecosystem. 

- my point is simplicity and loosely coupled libraries may have lead to the freedom of choice yet they have made the JS echo-system to expand exponentially in such a way that is killing clustered adoption and community contribution , looking at Laravel, Ruby in Rails and the following tweet from Laravel maintainer might shed some light on the topic
- https://x.com/taylorotwell/status/1791468060903096422
  - When Laravel and Rails developers say "full stack", they mean something totally different than when Next or Remix (React Router?) developers say "full stack".
  - In Laravel and Rails, it means there are built-in, opinionated solutions to things like validation, interacting with a database, authenticating users, scheduling background work, sending an email.
  - In Next and Remix, it seems to mean that there is simply the bare ability to run code on the server at all and an advertisement for Clerk.
  - Rails and Laravel were built with the express purpose of allowing a single developer to build the next GitHub... or the next AirBnb... or the next Shopify. Prototyped from beginning to end. 
  - I don't see a full-stack story in JavaScript yet that would allow me to realistically sit down and build something like Forge or Vapor from start to finish.
- [PHP: Laravel, Ruby: Rails, JavaScript:? | ZenStack](https://zenstack.dev/blog/js-fullstack)
  - In short, he suggested that the whole JavaScript ecosystem lacks a real "full stack" framework like Laravel or Rails, which could allow a single developer to build the next GitHub, AirBnb, or Shopify.
# discuss-cluster
- ## 

- ## 

- ## [Doc on Clustering not clear ](https://github.com/feathersjs/feathers/issues/2101)
- With pm2 cluster mode, each instance has to run on a different port, is that correct
  - Nope, it's not correct, you can setup pm2 to run all instances on one port.

- ## [SocketCluster _201603](https://github.com/feathersjs/feathers/issues/265)
- Feathers itself, achieves socket clustering via two mechanisms:
- The crude manual method
  - You can register a client on each server manually for every other server you want to communicate with. It does work with JWT auth and will do retries and reconnects.
- Using feathers-sync
  - You can use a central pub-sub mechanism via feathersjs/feathers-sync. It totally works but we'll be spending more time in the near future on the scaling part of Feathers.

- Looking at FeathersJS code, I don't think you would be able to create a plugin for the full SocketCluster framework (with multi-core scalability and all) BUT you could easily make a plugin for the standalone (more lightweight) socketcluster-server (socketcluster/socketcluster-server). Users will be able to connect to it using socketcluster-client (socketcluster/socketcluster-client) as normal.
  - socketcluster-server behaves exactly the same as the full SocketCluster framework except that you don't get the automatic scalability and opinionated structure so it offers more flexibility when it comes to integration into existing systems and high-level structural frameworks like Feathers

- you mean ultimately you just want to be able to attach Feathers to a raw Node.js http server like Express allows? 
  - Not just the HTTP server - that's a no-brainer :). But also the ability to interact with SC's "real time API" through the uniform API of FeatherJS
  - The basic idea is to teach FeathersJS to understand SC's basics and obtain the information it requires from it to run. The user can still define all the usual things possible with SC.

- I'm a big fan of Feathers and Socket.io but didn't realize until last week that clustering (standard Node way) breaks the WS communication. Which makes sense because the master proc dispatches requests to worker procs via RR (round robin). There's no way for master to know which WS belonged to which worker (at least that's how I'm interpreting the problem). And that's a bummer because you loose the performance benefit of "clustering" Node. But if Feathers could easily integrate with SocketCluster, as mentioned here... that would be HUGE
- Feathers integration with SC Worker: polst/feathers-socketcluster

- We're still happy to support anybody interested in implementing this but I am going to close this issue since it has been inactive for a while and the team is going to focus on the already supported transport providers.
# discuss
- ## 

- ## 

- ## [Help in deciding between ExpressJs and FeatherJs. : r/node _202401](https://www.reddit.com/r/node/comments/191g3cx/help_in_deciding_between_expressjs_and_featherjs/)
- Ultimately, all backend frameworks are doing the same thing so the underlying concepts are transferable across many platforms, tbh, but I'm definitely on Express side of things for this one. Sooooo easy to use and unopinionated. Lots of flexibility, too. My go to, for sure.
- Feathers uses express (or koa). You'd probably want to compare feathers vs nestjs vs adonis.
  - Feathers is my go to for building service based backends. It's reliable, conceptually simple, leverages existing packages as much as possible without adding additional abstraction layers, and gives you direct access to their apis.

- ## [Feathers 4: A framework for Real-Time apps and REST APIs | Hacker News _201909](https://news.ycombinator.com/item?id=20977475)
- The real time feature is 2-fold:
  1. Feathers supports websockets, so you can push data to clients as the data is created/updated, etc.
  2. The Feathers server can decide what types of events to send to the client. If you have multiple servers, you can keep the events in-sync by using redis/activemq with the feathers-sync module.

- ## [How does scaling horizontally work with Feathers.js? : r/node _202211](https://www.reddit.com/r/node/comments/yw1edn/how_does_scaling_horizontally_work_with_feathersjs/)
  - If each instance of Feathers.js manages its own websockets if you scale horizontally ins't it possible that the load balancer/router routes the requests to the wrong instance and realtime functionality won't work?

- That's not really a Feathers problem imo. That's just a challenge of doing real time data. You're always going to have to have a sync for source of truth. If you want to have multi-server websockets, you'll probably need a Redis instance to keep them all in sync. But when you plug into a website, you should be pinned to a single IP. I don't think a load balancer can send you to another IP.

- What if the instance restarts for whatever reason? Happens pretty frequently when using container orchestration tools.
  - Then the client connects to a new server. Any state should be handled outside Node in something like Redis or Memcache or something. If you want to broadcast between nodes such that any message received from A goes to all participants, have each server connect to itself and send messages other servers send it. If you want to make sure that Message 123 goes to User 123, use logic to route your messages to the correct client across your servers, maybe with Redis as a "User 123 is at Server 123 and Connection ABC"

- ## [Component-based architecture](https://github.com/feathersjs/feathers/discussions/2915)
- Since we have @feathersjs/schema and resolvers, now, there's less of a need for Model-based adapters. 
  - We can focus more on adapters that don't have the Model class overhead, like Knex, MongoDB, and Memory. 
  - With the new data loader that @DaddyWarbucks is working on, I feel like we'll finally have a unified solution for populating data, removing even more dependency on Model-based adapters.

- ## [Dove: We want to cheer... but have some mixed feelings about v5](https://github.com/feathersjs/feathers/issues/2760)
- The thing is that everybody will have to define their data model and validations somewhere somehow. 
  - So while everything in Feathers used to look super simple at the first glance, you end up getting that complexity somewhere else (how to convert the query, do validation, define and populate associations or get shared types were always big topics that didn't really have a good answer).

- ## [[Dove] v5 Migration Learnings and Feedback](https://github.com/feathersjs/feathers/discussions/2410)
- socket.io has reduced the max size of socket messages to lessen the effect of DoS attacks.

- ## [Feathers 2.0 – a minimalist real-time JavaScript framework | Hacker News _201603](https://news.ycombinator.com/item?id=11290577)
- 🔁 How does the realtime work when there are multiple node processes or servers? If my client is connected to server A and an update occurs on server B, will my client get the event on the web socket? If so, how does server A know about the event that occurred on server B?
  - To handle the real-time event syncing we created https://github.com/feathersjs/feathers-sync. It uses a central Redis DB or a MongoDB tailable collection to to synchronize service events between different application instances. 
  - Another option is to use your websocket libraries' clustering library, for Socket.io for example there is https://github.com/socketio/socket.io-redis. 
  - This is a very good question. We're definitely planning on adding a section about performance and scaling to the documentation very soon.

- I really like that it builds on the work of others instead of reinventing the wheel. Also, mentioning Meteor, totally not needed.
- The usage of NPM packages without needing to roll my own Meteor NPM bindings for each one is huge.
- there's no real-time db support like what Meteor with livequery does. The term 'real-time' is abused a lot here. Not only does neither Meteor, nor feathers offer real-time in the real meaning of the word. A better word is 'reactive'. But feathers just provides the very basic infrastructure (basically just websockets). Meteor also supports any type of DB, but only Mongo comes with reactivity... (Although their 'apollo' project is looking to change this).

- Feathers also supports Primus (https://github.com/primus/primus) so you can a bunch of other socket transports.

- > exposes both a RESTful and real-time API automatically through HTTP/HTTPS and over websockets. 
- Why not both at once with HTML5 SSE?
- I think SSE has two limitations that might not make it too useful for some scenarios:
  - Each SSE channel would require a separate TCP connection. And as the connections for a browser are limited, you can not support a lot of of different SSE channels. This is mainly a HTTP/1.1 problem, HTTP/2 fixes this. But as browser and server support for HTTP/2 is still limited you might not bet on it.
  - SSE can only send chunks of text in each notification, where the possible payload is additionally limited by the SSE encoding (you can't send text with \n\n in it). So if you need binary or abritrary (JSON?) text objects you would need some additional encoding. Like object -> json string -> byte-array representation -> base64 string. This works, but the overhead for your application (must do the encoding) and the browser (must to all the decoding and look for the \n\n) is not ideal.
  - I'm currently experimenting with using HTTP/2 and fetch API with readable streams to stream arbitrary objects on a bigger number of parallel channels from server to client. This seems to work and looks quite promising for the future, but due to missing browser and partly also missing server support the solution is definitely in it's infancy.
  - So the current safe bet for enabling lots of notification channels or enabling realtime queries would still be websockets.

- What happens when the connection between the server and a client is broken? Will Feathers automatically (and invisibly) restore it?
  - Yes, Feathers relies on either Socket.io or Primus (your choice) for the websocket interface, both of which provide auto-reconnect with back off out-of-the-box.
