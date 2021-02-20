---
title: thread-fwk-web
tags: [framework, frontend, thread, web]
created: '2020-12-05T17:52:28.808Z'
modified: '2021-01-08T17:13:53.965Z'
---

# thread-fwk-web

# pieces

- ## 

- ## [I was impressed by @pmndrs valtio, so I decided to figure out how to implement a proxy state like valtio, using valtio's test cases.](https://twitter.com/lihautan/status/1361481299970592770)
  - Tips on get a deeper understanding of the library you are using
  - Try implement the library based on the public API and test cases, figure out how it might be implemented.
  - Peek into the source code if you are stucked.
  - https://www.youtube.com/watch?v=uZnO2G8pqn0
  - It's very interesting to see someone like you got interested in the vanilla version. I heard someone else is using it in vanilla. I had no idea if it's useful in vanilla when I started, as its goal was to implement an API that is compatible with React's useMutableSource.

- ## Running web apps from archives (think cross-platform executables) would be an important complement to hosted PWAs.
- https://twitter.com/rauschma/status/1362440337705365504 
  - Does anyone know why there is so little progress in this area (AFAICT)?
  - https://github.com/WICG/webpackage 
  - Web packaging format
- I think a big problem is the origin of a bundle: it's not HTTP, and it doesn't have a domain. 
  - That breaks a lot of assumptions about security and privacy on the web. 
  - Still would be interested in seeing this developed though.
- [Dynamic bundle serving with WebBundles](https://docs.google.com/document/d/11t4Ix2bvF1_ZCV9HKfafGfWu82zbOD7aUhZ_FyDAgmA/edit#)

- ## When you set an `id` to an HTML element it... becomes a global JavaScript variable referencing that element
- https://twitter.com/stackblitz/status/1359525093601382406
  - Beware of relying on globals!
- always name your id with - in between，example layout-version
- Global variables should not be here. They should be in a seperated js file that is used as global. And also not in any dom element.

- ## creating framework-agnostic components with @stitchesjs core
- https://twitter.com/peduarte/status/1358125279303065602
- Im so happy with this API so far. One thing is spec'ing it and the other is actually using it.
- Love it! Hear me out, I'm not drunk. Variants look like state machines 
  - Now you can create finite css styles with #xstate
  - Would be cool to have stitches dev tools to visualise components variants like that 
  - Question: Are there any limitations for variants? Obviously, I can't put variants inside variants. But besides that, is there anything else? Can I use pseudo selectors, media queries etc.?
  - No limitations like that apart from obvious stuff like you mentioned
  - The cool thing about variants is that they can be “immutable”, meaning instead of changing its styles on different conditions (breakpoints), they can be *applied conditionally*
- Framework-agnostic in 2019: React, Vue, Angular
  - Framework-agnostic in 2021: different flavors of React
  - stitches supports svelte too.

- ## The existing history API (window.history, popstate, etc.) is bad for building web apps. We've been working on a proposal for a new history API, and would love your feedback
- https://twitter.com/domenic/status/1356656668222885889
- I think it should be possible to iterate on top of what window.history already provides, and just fix the problems with it instead of introducing something entirely new.

- ## After all these years there really are still only 2 types of frontend JS UI Framework. Angular(React) and KnockoutJS. 
- https://twitter.com/RyanCarniato/status/1356655576420282371
  - Work has gone into optimization, and borrowing the benefits of the other's approach, sometimes producing a hybrid. 
  - The basics haven't changed for nearly a decade.
- Thnx for putting this into words @RyanCarniato - for me as well we've got 2 fundamental patterns:
  - pull: "ask for changes" (Angular, React etc.)
  - push: "tell me that sth changed" (KnockoutJS, Solid, Svelte etc.)
  - There are  toons of hybrids and nuances of course.
  - Still can't decide if "hybrids" trying to add push-based change detection on top of a framework written with a top-down pull mentality (ex. NgRx with Angular) are a good thing or not. 
  - Having a framework designed with a push-based model from the ground-up feels so much "cleaner"
  - Yeah, Vue is another example of this. Their reactive system sits on top of a VDOM. The types of optimizations it does are not unlike Solid or Svelte, but uses them to generate VDOM nodes and then goes diff them.
- 计算机研究的问题，很多都可以总结为经典问题，但具体业务的应用场景需要修改

- ## What are folks using to split their CSS bundles to only load the CSS used by the current page?
- https://twitter.com/rob_dodson/status/1355575341696204801
- is there some system that creates shared chunks for css files? 
  - globally (80%+ pages) shared styles as a file
  - inlined page specific styles above the fold 
  - page specific styles as a file
- MiniCssExtractPlugin seems to work OOTB if you lazyload / import() page JS, though that assumes your pages have JS
  - I use that for all my apps but only lazyload pages in big apps

- ## Does any Node.js serverless function providers optimize cold start time with V8 heap snapshots?
- https://twitter.com/youyuxi/status/1353853045520674817
- Don’t think so, 
  - because node itself doesn’t support v8 snapshotting, even for node’s internals. 
  - There’s some scary blockers still remaining, so unless the clouds figured them out but didn’t tell anyone we’re all waiting for that! Docker snapshots though maybe
- Cloudflare workers are your best bet if you want to minimize cold start (was they don’t have any) but they don’t run Node.js. 
  - They have a custom runtime that’s a thin layer atop v8.
- Cloudflare is closest.

- ## My Monday off has primarily gone towards a Babel/Webpack upgrade on a public sector code-base 
- https://twitter.com/slightlylate/status/1351346159869050880
  - and my prior that all of this is suspect and complexity-for-promotion's sake has never been more strongly reinforced.
- Finally upgraded a legacy react app to webpack v4 over the summer, not fun researching every new plugin and config option.
  - 6 months later I go to spin up a new project and now here’s v5 and everything I thought I knew is a lie
- If your tool comes with a transpiler in the default toolchain, it's a distributed liability whose costs you are externalizing onto unsuspecting teams that probably can't afford it.
  - this is why I think Lit should always have CDN-loadable binaries, whatever else is possible. The common path shouldn't require any of this.
- As a once-and-likely-future vendor of transpilers, I think about this a lot. 
  - The TypeScript's and JSX's of the world are not chained to the back-compat firmaments the way languages and platforms are, 
  - and taking bets on them is something we should _culturally_ discourage.
  - The ethical thing for transpiler vendors to do is to work themselves out of a job; 
  - to find the standard or platform vendor they can influence and get their improvements written into the system such that they can fade away.  
  - It's a dual failure when those bodies don't listen.
- I think Babel has done better than most here. 
  - It's hewing a close line to the spec...the problem is its prevalence, rather than its qualities.
- After almost a decade of using various js frameworks and acquiring transient knowledge that's superseded in a few years by whatever n framework(s), I've come to appreciate the value of learning standardised APIs. 
  - They won't last forever, but they will last much longer.

- ## Maybe you don’t need that SPA
- https://twitter.com/RyanCarniato/status/1334732629808009216
- @_developit's Island Architecture keeps getting brought up as if it's this new thing, despite this being the default in Marko for over 5 years.  Maybe "Island" is just catchier?
- I've seen people talk about this stuff in other frameworks like Vue and Svelte, and theorizing how to do this. 
  - But this takes those approaches already in Marko, and explains how even better partial hydration can be done.
- I think it is also worth tinkering about this problem from a different angle too: 
  - Island Architecture in a way is solving a problem of slow js rendering on the web, what if the rendering thing was 3x faster? 
  - Would it still make sense to invest in IA?
  - You mean in the browser? Really this is mostly initial load consideration. Sans cache, the server can start doing async data fetching earlier than the browser which has to wait for the page to be rendered.
- How does Marko resolve state for the hydrated components?
  - We look at what components have state in them (have classes). 
  - From there we can determine hierarchically which stateless components are never used in a stateful context and not bundle them in the client. 
  - And then push all static data above it to the hydrate call for that island.
- It's been always like that. 
  - People follow the projects based on the hype(促销广告、促销讨论). 
  - If a big company uses technology, everyone just blindly follows that. 
  - No one really notices the other better projects if they do not have enough hype around them.

- ## Which frontend frameworks support UIs that mostly work without JS?
- https://twitter.com/rauschma/status/1274737114794659842
- E.g.: Initially, there is server-rendered HTML that links to other pages. JS is injected into that HTML, but the URLs remain. Benefit: You can open links in new tabs.
- I faintly remember Ember supporting this.
- This has always been th default in preact-cli, 
  - but I'll be th first to admit there's a ton of progressive enhancement we don't do that we could be doing.
  - Preact team has a couple things underway that I think will help shift the status-quo in this area.
- Gatsby is built with the idea that JS enhances the experience, 
  - but Gatsby outputs plain HTML, all the links work. 
  - Many Gatsby sites work with JS disabled. So I think it qualifies
