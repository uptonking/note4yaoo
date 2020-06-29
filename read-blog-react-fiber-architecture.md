---
tags: [blog, react]
title: read-blog-react-fiber-architecture
created: '2020-06-27T05:10:19.958Z'
modified: '2020-06-29T04:20:19.734Z'
---

# read-blog-react-fiber-architecture

## pieces
- The Fiber architecture can solve blocking (and a host of other problems) because Fiber made it possible to split reconciliation and rendering to the DOM into two separate phases.
  - Phase 1 is called Render/Reconciliation.
  - Phase 2 is called Commit.
- In phase 1, React is called to render new and/or updated components
  - React will schedule the work to be done (changes to be rendered) by creating a list of changes (called an effect list) that will be executed in the Commit phase. 
  - React will fully compute this list of changes before the second phase is executed.
  - After collecting the render output from the entire component tree, React will diff the new tree (the virtual DOM) with the current DOM tree and collect the list of changes that need to be made to the DOM to produce the desired UI structure. 
- In phase 2, React actually tells the DOM to render the effect list created in phase one.
- The Reconciliation/Render phase can be interrupted, but the Commit phase cannot, and it's only in the Commit phase that React will actually render to the DOM.
- ref
  - https://dev.to/afairlie/to-understand-react-fiber-you-need-to-know-about-threads-3dof
  - https://kentcdodds.com/blog/fix-the-slow-render-before-you-fix-the-re-render


