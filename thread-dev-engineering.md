---
title: thread-dev-engineering
tags: [dev, engineering, thread]
created: '2021-01-21T17:51:54.496Z'
modified: '2021-01-21T17:52:13.333Z'
---

# thread-dev-engineering

# guide

# pieces

- ## 

- ## 

- ## How are some of you actually working on _side tech projects_? I'm struggling to even maintain energy for day-job projects lately.
- https://twitter.com/brian_d_vaughn/status/1361520253604421634
- I get anxious without side project. It’s how I relax.
  - When the brain is full of errant(错误的、行为不当的) thoughts and ideas, only way to get anything done at work is to regularly clean the brain.
- don't believe everyone on twitter. Specially in the Dev community.
  -  I have experienced it a lot that people try to talk them selfs better than they actually are. Per se it is not a problem. 
  -  But it promotes a bad reputation for devs. We don't code 24/7

- ## Offline support has been part of the PWA installability criteria since the beginning. 
- https://twitter.com/ChromiumDev/status/1358817467661967365
  - In Chrome 89, we'll warn you if your PWA doesn't have an offline experience. 
  - In Chrome 93, we'll start enforcing the updated install criteria for new PWAs.
- If all you need is a baseline offline fallback page without actually delivering a true offline experience (which, acknowledgedly, many apps don’t need or can’t), then give my article a read
  - [Create an offline fallback page](https://web.dev/offline-fallback-page/)

- ## When learning something new, it’s easy to fall in to the trap of comparing your work to seasoned professionals and think everything you’re doing is wrong. 
- https://twitter.com/steveschoger/status/1358588140328538115
  - Lately I’ve been trying to embrace this learning period because it’s a small window of great discoveries.
- Constant learning from seasoned profs, using my previous dev knowledge mixed with theirs, change code as I find better or more efficient solutions, seasoned profs's solutions are not always right or appropriate for the current app.  Having a blast and always learning.

- ## which companies are using @GraphQL in production nowadays?
- https://twitter.com/mxstbr/status/1358351658078634014
- Frontend teams at Danske Bank use GraphQL, mostly driven through Apollo. 
  - Microservices are still on REST so there's redundancy maintaining a mid-tier just for conversion.
  - GraphQL has most significant advantages when adopted by backend teams which isn't the case at most places.
- Using it in production at @skillshare . 
  - Running Apollo Gateway as API composition layer to allow frontend decoupled monolith -> microservices migration.
- @OrbitalChat uses it for admin-based stuff. 
  - The more interactive part is done with Firebase Real-time database and Firestore direct from the client. 
  - Also @SketchADay is 98% GraphQL and a couple of little plain JSON-over-HTTP bits
- GitHub and Contentful
- @AirbnbEng uses it quite a lot

- ## If you don't know which code is calling your function, use console.trance()
- https://twitter.com/sseraphini/status/1356654950198239233
- I used `console.log(new Error)`

- I usually also do “console.log = console.trace” to locate and remove some console.log

- ## Hyphens are pretty. Underscores are ugly and don’t belong in URLs
- https://twitter.com/mscccc/status/1355525419152384002
- What about emojis in URLs? 
- [URL as UI](https://www.nngroup.com/articles/url-as-ui/)

- ## "The DOM is bad for apps" makes me laugh pretty hard. 
- https://twitter.com/_developit/status/1355670204366393347
  - It's effectively the same type of abstraction as a scene graph, but because we use it poorly it must be bad!
- I think the dom is very much bad for apps, who in their right mind would say otherwise. 
  - Why else do we have frameworks abstracting it. 
  - Most people don't know or see a dom when they make apps and that is a good thing.
  - That is the same reason why we have rejected a component model built on that pile of perpetual backward compat which is the dom.
- The browsers dom is virtual, bc it's faster. 
  - Every GUI system is split into a logical/virtual & a visual tree, otherwise you wouldn't be able to schedule, or, well, virtualize. 
  - Ever used a virtual list, I suppose you did. 
  - FBs "vdom" has better scheduling than the "dom", facts. 
- aren't some of the most popular apps just app shells with a web-view?
  - that, or react-native which uses a tree abstraction very similar to the DOM anyway
- Well, if we just used fixed height for everything and there was never a need to refresh layout I think most html apps would be as fast as 'native' - as if running apps in a JVM/runtime is native anyway - if it's not assembly writing directly to a framebuffer it's trash

- ## Software tradeoffs
- https://twitter.com/housecor/status/1355144710185230336
  - Build vs Buy
  - Reuse vs Copy
  - Sync vs Async
  - Serial vs Parallel
  - Dynamic vs Static
  - Concise vs Explicit
  - Unified vs Separate
  - Secure vs Convenient
  - Simple vs Configurable
  - Centralized vs Distributed
  - Convention vs Configuration
  - **Avoid picking sides. Think tradeoffs.**
- I am not sure you want to trade off security for convenient
  - Perhaps, but companies do so everyday. 
  - Using other people’s software is convenient, but adds security risk by trusting other people’s code.

- ## Will Vite replace vue-cli? 
- https://twitter.com/youyuxi/status/1354584410482499585
  - Initially I wasn't sure, but at this stage I believe it will eventually be the case.
  - The main disparity(不同；差异，悬殊) now is just test runner integrations.
- Check out uvu by @lukeed05 . 
  - Native ESM support, very much in the spirit of Vite. 
  - No test compilation step by default, no special integration needed.
  -  When I need to test in the browser, I just start my Vite dev server and use puppeteer in uvu tests. It's refreshingly simple
- We could make a plugin for web test runner
  - It should be relatively straightforward if we can proxy browser requests to some transform API or middleware. 
  - We already have a plugin for snowpack
- There was discussion in vue-cli about letting plugins replace webpack as the builder
- after a few years of running large enterprise apps on vue-cli, I've had to break out of the test runner integrations to avoid the lag time between test runner updates, and vue-cli updates. 
  - vue-cli is still a great tool... 
  - But would love to see a more decoupled approach in vite

- ##  what are your team’s package.json script naming conventions for development mode, your build stage, and potentially running the built thing?
- https://twitter.com/jaredpalmer/status/1353083840424763392
  - I used to be in the ‘start, build, start:prod’ team 
  - but now I’m actually leaning toward ‘dev, build, start’

- ## A little technique we use all the time to audit the layout shifts and avoid performance issues.
- https://twitter.com/smashingmag/status/1352185650091581441
1. Add * { outline: 3px solid red } to your CSS.
2. Record the loading of your site/app.
3. Review it by exploring what happens in slow motion.
4. Adjust and minimize shifts.

- Great tip, thanks! This one's less visual and more programmatic from the 'Performance' tab in Chrome.
  - You can hover over the 'Moved from' keys and this will visualise the movement in the browser window.
  - And using this method you can even see down to the shift caused by web fonts loading.
- We can also use a `PerformanceObserver` to log elements causing layout shift to the console
- Remember this trick from when i started to learn css.
  - Always use to troubleshoot when some problem arises while postioning elements..
