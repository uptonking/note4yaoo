---
title: lib-fwk-nodejs-express-community
tags: [community, express]
created: 2023-02-05T18:55:55.398Z
modified: 2023-02-05T18:56:12.643Z
---

# lib-fwk-nodejs-express-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🤔 [Serve Static Files Using Express or Use Express To Only Access Backend? - Stack Overflow](https://stackoverflow.com/questions/66737274/serve-static-files-using-express-or-use-express-to-only-access-backend)
- If your files are truly static (no dynamic content in them at all), then it doesn't really matter who serves them.
  - You can even use the same domain and use a proxy like NGINX that serves up just the static content while forwarding everything else through to your Express server.
- If you are dynamically generating any content (like many web sites that use a template engine and generate HTML content from a database from the server), then it makes all the sense in the world to serve your content from the Express server.

- The main reason to get static content off the Express server is when you want to increase scalability and your current load is too much for just the Express server.


# discuss-alternatives
- ## 

- ## 

- ## 

- ## [Anything wrong with Express? What's so good about hono.js? : r/node _202307](https://www.reddit.com/r/node/comments/1502t43/anything_wrong_with_express_whats_so_good_about/)
- people still default to it because they’re familiar with its API and ecosystem.
  - Not supporting HTTP2 (or HTTP3 while we’re at it), or even not supporting TLS is fine for the vast majority of use cases, because you’d host your application server behind a reverse proxy anyway, which can (and imho should) deal with handling TLS, terminating HTTP2/3 and serving static content. That reverse proxy will most likely be much, much faster doing these tasks than any V8-optimized execution of JS ever will be.
- Express is falling behind because it doesn't support new web standards. Http2 has been out for 8 years and express never bothered implementing it. 
  - Of course you can get http2 through a proxy like nginx without implementing it in node but it shows that express will fall behind more and more. Express is also quite slow

- if you need raw performance, there are HTTP server libraries now that make use of the Web Platform’s vast diversity and completely sidestep(回避, 规避) Node’s HTTP implementation instead of just abstracting it away, by using a HTTP server running in WebAssembly or plugging into Node itself, e.g. 0http using low-http-server

- 99.9% of use cases don't have traffic requirements above what Express can handle anyway.

- What 's great about Hono is that it can run on almost any Js runtime not just node. It can run on Deno, cloud flare worker, bun AWS lambda... You can write small piece of API and deploy it as edge function on your favorite platform.
  - Do you really ship your code in all of these platform? Do you use Hono in your projects?

- Express works, but was created in 2009 and the author's last commit was in Feb 2014. It doesn't align with modern web standards (like the Fetch API with its Request, Response objects), and Express far from the fastest web server any longer.
  - Check out the more standards-focused HatTip as well, and the more full-featured Bun-only framework Elysia (templates, RPC, e2e type safety, validation).
# discuss-roadmap
- ## 

- ## [Builtin Typescript support _202502](https://github.com/expressjs/express/issues/6311)
- 👷: There are no plans to redo Express with TypeScript, maybe we could launch Express with types, but not redo the library

- [EFI: Publish and maintain types _202402](https://github.com/expressjs/discussions/issues/192)

- ## [It's 2023 and still no native async support for routes? _202301](https://github.com/expressjs/express/discussions/5111)

- 👷: I'm not familiar with TypeScript and don't have interest in using it, either. I believe the other members have expressed the same. 
  - Coverting the code base from JavaScript to TypeScript would essentially fork the code, as everyone who works on it would disband (like myself) and probably just work on the JavaScript version of Express. 
  - So, to summarize I don't think it would be worth the change, as it would effectively leave Express unmaintained at that point.
# discuss-features
- ## 

- ## 

- ## 

- ## 

- ## 🆚 [serve-static vs express.static() : r/node _202010](https://www.reddit.com/r/node/comments/jf87rh/servestatic_vs_expressstatic/)
- Basically doing the same. But you should not use either of them. 
  - Its best practice to server static content via Apache/Nginx/alike.

- `express.static` is simply a reference to the `serve-static` middleware. 
  - Express includes serve-static as a dependency and exposes it directly via express.static for convenience.
  - express.static is simply an alias provided by Express that calls into the serve-static module.
- serve-static is a standalone middleware module that can be used in any Node.js application regardless of whether Express is used.






- 
- 
- 
- 
- 

- ## [asynchronous error handling in expressjs _202410](https://www.michelleenos.com/notes/asynchronous-error-handling-expressjs/)
- It seems like support for async/await in ExpressJS has been a long time in the works - see this github thread which has been going since 2014! 
  - Express 5.0 apparently does include this support, but the stable/default version (something like 4.2.x) still does not.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🐛 [Cons of Express.js : r/node _202207](https://www.reddit.com/r/node/comments/voyv0i/cons_of_expressjs/)
- I have used Express, Ruby on Rails, Spring (including Spring Boot) and a few other frameworks. Express is much lighter weight than most frameworks, which generally means writing a lot of boilerplate to get things working. I think the ecosystem of middlewares is great, but there is no "one way" of doing things, so it can be easy to build a mess.

- No support of async error handling, async middlewares.
  - Express will try to match all routes, not only first, so it's possible to have multiple routes handling single request.
  - Express is not really a framework, so quite often people who use express start to write custom wrappers around express router.
  - In TS req.body has `any` type, so even if you're using typescript and thinking you're cool, still easy to forget about validation.
  - And giving that express is simply a router + middlewares, and it doesn't support promises in both, and you can't define validations on router to have correct params and body types, it seems to me that express is doing just one thing and doing it bad.

- It's one try/catch per route handler, which means filler code with lots of copypasta.

- ## [Is express bad for large projects ? : r/node](https://www.reddit.com/r/node/comments/skoggh/is_express_bad_for_large_projects/)
- If your server can only handle 16K users, you can launch 10 servers and put reverse proxies in front of them. You can now handle 100K users with lots of room to spare.
  - You can design your infrastructure to scale out or scale in, depending on the load. This is where Cloud-based infrastructure truly shines. You can also go serverless.

- A well written reverse proxy + cache (nginx, cloudfront, etc) can get great performance out of even a terrible server. And that's before you get into things like load balancing.
  - TL; DR Express by itself is relatively performant but at that scale traffic related issues should be solved elsewhere, regardless of your servers language / framework / etc.

- Express is fine. PHP still runs half the web. Just build your thing!

- Ruby is even slower but some big companies still using it. Because there are a lot of ways to distribute load and scale

- ## I used #npm library `fast-json-stringify` , and replaced Express default `res.json()` on get requests to serialize the response. 
- https://twitter.com/SternTwena/status/1766589057616822394
  - I got around 20% improvement in my API performance.
  - Really simple code . stringify is usage of fast-json-strigify with the matching schema.
