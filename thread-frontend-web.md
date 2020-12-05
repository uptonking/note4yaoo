---
title: thread-frontend-web
tags: [frontend, solidjs, web]
created: '2020-12-05T07:43:47.005Z'
modified: '2020-12-05T07:44:12.022Z'
---

# thread-frontend-web

## pieces

## framework

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
