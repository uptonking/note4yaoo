---
title: thread-pm-app-tool-products
tags: [products, thread, tool]
created: '2021-03-15T05:21:25.780Z'
modified: '2021-04-19T14:53:36.883Z'
---

# thread-pm-app-tool-products

# pieces

- ## 

- ## 

- ## Starting to feel like the @tldraw engine really wants to be a “render react components in a canvas paradigm” engine.
- https://twitter.com/steveruizok/status/1435515509756338177
  - This isn’t too far from what it is currently. Right now you’re limited to only elements that can go inside of an svg `<g>` tag.
- One of the limitations with that canvas is the limited way that a custom/code component could behave on the canvas. Components with nonstandard behaviors, like their Graphics shape, were all baked in.
- So more work for the lab. As with all hobby projects, part of the fun is seeing where things go—and if @tldraw points to a “next” project, then I think that project would be a similarly generic “interactive canvas for components”.

- ## Just pushed a BIG update to @tldraw
- https://twitter.com/steveruizok/status/1434190045238472704
  - a full rewrite, six weeks in the making, that includes new faster state management, an architecture made up of three packages, and tons of bug fixes and improvements.
- The whole app is built on the @tldraw/core package, which is an excellent renderer for custom primitives. 
  - It's fast and efficient—but there's still plenty of room for improvement, too. 
- Me: Decides on the button variants for 6 weeks

- ## CODECHECK
- https://codecheck.org.uk/
- CODECHECK tackles one of the main challenges of computational research by supporting codecheckers with a workflow, guidelines and tools to evaluate computer programs underlying scientific papers. 
- The independent time-stamped runs conducted by codecheckers will award a “certificate of executable computation” and increase availability, discovery and reproducibility of crucial artefacts for computational sciences.

- ## Figma really is a much better tool for basic vector image editing than Inkscape. 
- https://twitter.com/stevage1/status/1417354508464574465
  - Upload some SVGs, easily export to PNG. And keep them organised however you want.
- also the ceo of figma write esbuild in his spare time
- And you can share workspaces

- ## natto.dev is a canvas for JavaScript.
- https://www.notion.so/Documentation-44fea11f393a4e46b5a22f5799de58ca
  - creates an eval pane which consists of an expression editor and output. 
  - This is very much like a JavaScript console. 

- ## Cloudflare Pages is now in GA! 
- https://twitter.com/Cloudflare/status/1381593197311315973
  - It's hard to believe how much the product has matured in just a few months.
  - Dogfooding through and through, on Workers, SSL for SaaS, and on top of Cloudflare's network allows us to go FAST
- Awesome! I love the addition of custom redirects with the _redirects file. Looking forward to being able to add workers to an /api directory within the same page too! 
- This is great! Any chance we might get to use the same tooling to deploy workers without a path prefix for a fully dynamic edge rendered site? 
- I get the idea from this post that Polish and Mirage are included for free as part of pages - is this correct? If so, amazing
- I get the idea from this post that Polish and Mirage are included for free as part of pages - is this correct? If so, amazing

- ## I'm excited to share a preview of natto.dev, a canvas for writing and manipulating JavaScript.
- https://twitter.com/_paulshen/status/1370402539720503298
  - It's kinda like a JS playground, script runner, API client, JSON viewer, datavis tool, .. not sure exactly but it feels like something!
- nice! dragging a column out of a table is awesome. I also like the design of the wires, ambiently visible but light enough to not feel too "in the way"
  - I could imagine a non-programmer playing with this, and gradually picking up JS by messing w the code snippets
- each pane is an expression but you could fit arbitrary long content in a single expression.
  - it's kinda like a Swift playground but you choose where the logpoints are.
