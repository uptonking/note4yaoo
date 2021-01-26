---
title: thread-web-fwk
tags: [framework, frontend, thread, web]
created: '2020-12-05T17:52:28.808Z'
modified: '2021-01-08T17:13:53.965Z'
---

# thread-web-fwk

# pieces

- ## 

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
