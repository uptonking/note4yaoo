---
title: thread-web-dev
tags: [frontend, thread, web]
created: '2020-12-05T07:43:47.005Z'
modified: '2021-01-08T17:13:43.392Z'
---

# thread-web-dev

# pieces

 

- ## Let's Bring Spacer GIFs Back!
- https://www.joshwcomeau.com/react/modern-spacer-gif/
- Instead of using margin, I create a new element explicitly to add some space between the icon and text!
- In the late 90s, if you were to pop open the source of a typical website, you'd likely encounter this curious fella
  - `<img alt="" src="spacer.gif" width="1" height="1" />`
- CSS didn't exist yet, and web layouts were built using HTML tables. 
  - GIFs were used because GIFs were the only image format that supported transparency (this is pre-PNG). 
  - Our spacer friend consisted of a single transparent pixel, a completely empty image.
- CSS was added to the browser to offer an alternative to styling. 
  - The language wasn't originally designed with layout in mind, 
  - but developers quickly realized that — through the use of some clever float hacks — it could entirely replace table layouts!
- By separating our concerns
  - HTML for structure, CSS for layout and presentation, JS for behaviour
  - we had a convention that would help us keep complexity down, ultimately making it easier to maintain things.
- In the original Jambalaya table-layout days, the spacer GIF was a tasty complementary ingredient. 
  - It didn't taste so good when we switched to making deconstructed sandwiches. 
  - But now that many of us are working with component-driven architectures, our code might benefit from a pinch of spacer GIF.
- Originally, my `<Spacer>` component rendered a `div` instead of a `span`, but I found it was a little limiting. 
  - According to the HTML spec `div`s aren't supposed to be put within certain elements, like `p` and `button`.

- ## Quiz time! for histroy back
- https://twitter.com/ryanflorence/status/1346562678869790720
  - No JavaScript on the page, normal document requests:
    - You land at http://example.com
    - You click a link to /page.html
    - Again, you click a link to /page.html
    - You click the browser back button
- Turns out when you go to the same URL, the browser still makes a document request to the server, still gets the a fresh page, 
  - but it *does not* push a new entry into the stack, it *replaces* the current one!
  - It's the same as clicking "refresh", and that makes sense.
  - 结果是回到example.com
- 实践测试
  - 在空标签页打开 a.html，然后按返回键，会回到空标签页
  - 在空标签页打开 a.html，再点刷新按钮，然后按返回键，也会回到空标签页

- ## To help me decide exactly what my media query tweak points should be.
- https://twitter.com/Malarkey/status/1345873190380253187
- If I had to print something for debug purpose, I'd prefer to show a different content, with the information of the media applied, on a `body::before` pseudo element absolutely positioned.
- I went with a `content:"XS";` `content: "S"/"M" `and so on. 
  - I've got this `debug.sass` file damn full of ways to figure out common gotchas behind html classes like debug_viewport debug_grids and so on. 
  - It's annoying to maintain but it has saved me tons of time @ the job at least twice
- [Custom properties for breakpoint debugging_201802](https://thatemil.com/blog/2018/02/23/custom-properties-breakpoint-debugging/)

- ## State machines are great, so why aren’t we rewriting all of our async/await code to them?
- https://twitter.com/dan_abramov/status/1344502932704788480
- the simple answer: async/await is easier. 
  - It leaves out edge cases. When you include the edge cases, async/await is more complex... So developers just hope for the best.
- state machines are great at representing systems that have cycles & many possible transitions between each state, 
  - async await is better for relatively linear paths with limited branching
  - its a little bit like how regular expressions work well for the state machines that represent string matching, since those also tend to have lots of sequential states with no branches
  - Indeed. And regexes are generally convertible to pointer bumping string scanning code, with loops replacing eager Kleene star. 
  - See how hand-written lexers implement regex matching in code where lex would use a state machine. Instruction pointer replaces state code.
  - Regexes and automata are isomorphic, a regex is literally a state machine
- This made me think of XHR’s `onreadystatechange` event and how devs were really really happy to use `$.get` instead of considering all of the possible ready states. 
- Babel rewrites your async/await code into small state machines
  - As well as any of your code is executed on hardware state machines
  - So here you go, exactly as you asked
- I'd much rather go the other way and remove state machines and caching layers from async/await
  - [callback based, simplified async/await](https://es.discourse.group/t/callback-based-simplified-async-await/343)

- ## What advice were you given for your career that turned out to be a complete waste of time and effort?
- https://twitter.com/buildsghost/status/1343650869904986112
- I was told to go take a bunch of night classes on computer science by two MIT grads if I ever wanted to be "serious" about programming.
  - I took some free student-taught classes, 
  - and we spent months learning languages I have not used since.
- This isn't about tech, but when I was in school to be a licensed massage therapist.
  - I had a teacher tell us that we should work our first year *for free* in order to build a client base.
  - Thankfully, I didn't, but I am sure some folks listened.
- You *need* to be good in math
- Go to conferences.
- I was told that how people feel in a moment is more important than the outcome of the work. 
  - Now, I couldn't be happier to work somewhere frank, timely, respectful feedback is foundational to the culture. 
  - Spoiler alert: great work outcomes _make people feel good_
- Was also told "PHP is dead, JSP is the future" in around 2006. They were very wrong.

- ## I want to *scale* a div and all of its contents to fully fit wall-to-wall inside its container div. 
- https://twitter.com/erikras/status/1343480294654046209
- Similar to what `background-size: contain;` can do for images. Possible in CSS only? JS ok, too.
- I think scaling is the wrong thing for my use case.

- ## A year ago I made a bet on full-stack JS and switched my focus from @laravelphp to Node.js. A year later, I found that Node mostly just slowed me down.
- https://twitter.com/tylerlwsmith/status/1341557868571422722
- Server-rendered React components look really exciting. 
  - I just wish the Node ecosystem was less fragmented and more productive so it would be easier to take full advantage of it.
  - Until then, I can continue to get a ton of productivity out of Laravel 
- React Router is the reason I love React. 
  - It also has the most innovative front-end libraries, and the front-end is the part that users interact with. 
  - React also works great with extremely complicated state management.

- ## [Reflecting on a year with Node.js and why I should have stuck with Laravel_202012](https://dev.to/tylerlwsmith/reflecting-on-a-year-with-node-js-and-why-i-should-have-stuck-with-laravel-e5a)
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

- ## if I was building a CMS using MongoDB would you tell me to stop immediately? If so, why?
- https://twitter.com/JakeDohm/status/1341892219511459842
- Every developer build a CMS at some point in their career. 
  - Might as well check it off of your bucket list.
- I’m going to get technical and ask what type of content your CMS would be housing. 
- That would determine DB for me. 
- Mongo doesn’t seem appropriate for most content I’ve worked with, as CMS tends to be highly relational.
- Maker me: Build whatever you want with whatever tools you want.
- Developer me: Don't use MongoDB, most of your stuff with be relational, 
  - and in the event you cannot use relational, use JSONB data type in PostgreSQL.

# ref

- [Custom Properties as State](https://css-tricks.com/custom-properties-as-state/)
