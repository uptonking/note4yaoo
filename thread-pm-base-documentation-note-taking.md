---
title: thread-pm-base-documentation-note-taking
tags: [documentation, note-taking, pm, thread]
created: '2021-04-19T14:49:44.712Z'
modified: '2021-08-16T06:56:53.061Z'
---

# thread-pm-base-documentation-note-taking

# pieces

- ## 

- ## The Text2PixelArt neural network (generates pixel art based on text) already allows you to create a good cover images for articles.
- https://twitter.com/sitnikcode/status/1430213610542964740
  - 生成的图片色彩风格都很浓郁，如深红深紫深蓝

- ## Evernote used to have a feature that let you export all of your notes (1943 for me) in one go... 
- https://twitter.com/simonw/status/1430407513606791170
  - but at some point recently they dropped that down to either 50 individually selected notes at a time or everything in a specific notebook
  - github从设计上就解决了此问题，每个仓库单独下载
- More frustrating though... the notes they export used to be valid XML, but now they are not! 
  - Just hit an XML error running my evernote-to-sqlite tool against the ".enex" export file

- ## Just added Markdown, HTML, and CSS as export options. Markdown includes links to hosted assets.
- https://twitter.com/4lpine/status/1428064775372607488
- We use the Theme UI sx prop as part of our internal data structure since we want direct theme mapping and the nesting of CSS-in-JS (Emotion).
  - We're statically extracting the styles to pure CSS using some tricks I hope to write a post on (soon).
  - Also, the declarative and composable nature of a props object that handles styling is so choice for this kind of tooling.

- ## I've been diving into @replicache and I'm convinced its model is what you want for majority of SaaS apps (eg todo apps, figma)
- https://twitter.com/_paulshen/status/1415365748675907584
  - client update lifecycle with authoritative server 
  - all these things have tradeoffs and I think it chooses the right ones for most use cases
- It works a lot like git where each client keeps a list of mutations 
  - although instead of the exact "diff" itself, the log contains mutation name and args (you define mutations). pure intention preservation!
  - key here is how client rebases because server is truth
- I've also been diving into https://yjs.dev, an excellent(!) CRDT library. 
  - however, replicache's model is simpler and doesn't impact your backend as much. It's really just an excellent client library with a protocol specification (big points here)
- some tradeoffs
  - you define mutations twice (once on client, once on server)
  - flat KV data structure (hi fractional indexing)
  - authoritative server (no p2p)
  - realtime updates require roundtrip
  - again I think they're reasonable
- natto does some funky iframe sandboxing that makes replicache hard to use right now but I'd use it otherwise!
  - replicache does not handle collaborative text editing rn. yjs/automerge does a good job here. on natto, I'm okay with treating each block's code as atomic unit
- I would say more that @replicache is at a lower level of abstraction than text editing. 
  - We need some good libraries for unstructured text editing on top of Replicache. 
  - You can do it right now with fractional indexing and it will mostly work, but there are likely even better ways
  - Fractional indexing has some known deficiencies when cursors are editing concurrently at exact same position.  
- I suspect that the other CRDT approaches for text editing Martin discusses can equally be applied to Replicache but I haven't had time to dig into it.

- ## Try the omakase layout on http://natto.dev! 
- https://twitter.com/_paulshen/status/1388211716001910786
  - Panes rearrange as you move your focus. 
  - Connected panes are shown to the side (inputs on left, outputs on right)
- if there's too much motion, turn on "reduce motion" in your accessibility settings
- I am pretty excited about dynamically showing related content in tools. eg showing incoming/outgoing calls when you're focused on a function in your editor
  - seems like a natural feature
