---
title: thread-frontend-web-fwk
tags: [framework, frontend, thread, web]
created: '2020-12-05T17:52:28.808Z'
modified: '2021-01-06T14:40:03.364Z'
---

# thread-frontend-web-fwk

## guide

## pieces

- Maybe you don’t need that SPA
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

- Which frontend frameworks support UIs that mostly work without JS?
  - https://twitter.com/rauschma/status/1274737114794659842
  - E.g.: Initially, there is server-rendered HTML that links to other pages. JS is injected into that HTML, but the URLs remain. Benefit: You can open links in new tabs.
  - I faintly remember Ember supporting this.
  - This has always been th default in preact-cli, 
    - but I'll be th first to admit there's a ton of progressive enhancement we don't do that we could be doing.
    - Preact team has a couple things underway that I think will help shift the status-quo in this area.
  - Gatsby is built with the idea that JS enhances the experience, 
    - but Gatsby outputs plain HTML, all the links work. 
    - Many Gatsby sites work with JS disabled. So I think it qualifies
