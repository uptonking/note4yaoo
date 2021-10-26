---
title: lib-editor-atlassian-community-stars
tags: [atlaskit-editor, community]
created: '2021-06-30T19:45:22.053Z'
modified: '2021-06-30T19:45:44.068Z'
---

# lib-editor-atlassian-community-stars

# repeat

- ## A modified version of Atlassian’s React+TypeScript PM editor_202101
- https://discuss.prosemirror.net/t/a-modified-version-of-atlassians-react-typescript-pm-editor/3441
- I finally have had a chance to fully immerse myself into understanding how to build a real, production-level ProseMirror editor that leverages React and TypeScript.
  - In my previous attempt I wandered off a little bit to a wrong direction by trying to come up with my own solution. 
  - Now, knowing the complexity of the task, I had a more pragmatic(实用的) approach and emulated as best as I could the existing implementations, namely Atlassian’s open-source PM editor 
- My goal was to re-implement an MVP using their architecture and after some struggle, I managed to pull it off. 
  - they have very generously open-sourced their editor. 
  - If you play around with their hosted example here Atlaskit by Atlassian, you’ll, however, might notice some performance issues. 
  - At least I found the With plugin state example to be quite sluggish and it registers keypresses with a noticeable latency. So it’s not all perfect.
- During my development process there has been various smaller and larger matters that I have needed to solve. 
  - For example, once I was able to implement the rendering with React portals, I noticed my approach to be quite unusable when rendering large numbers of nodeviews.
  - This was mainly due to how the rendering of the portals was done in one big loop that every update caused to re-render. 
  - From the Atlassian editor’s commit history you can find a similar observation which they solved by using `unstable_renderSubtreeIntoContainer`.
  - [Revert usage of `createPortal` in favour of `unstable_renderSubtreeIntoContainer` to improve perf_201807](https://bitbucket.org/atlassian/atlaskit-mk-2/commits/d520a6fb6dab1027d3873eec9317c4e8574d07fb)
- What I myself did was revert back to `ReactDOM.render` which was a lot faster than using portals, 
  - but I think a bigger performance boost was pooling all the updates per each PM’s `updateState` call and flushing them then all at once. 
  - I guess this could also make portals work but I haven’t done any benchmarking. 
  - The problem with using the `ReactDOM.render` is, in addition to not being able to share React context, that the render calls are not batched which I assume is really un-optimal for React as it is designed to update large trees fast, not dozens of little trees in separate renders. I don’t know if this is prevented with portals.
- Other curious aspects I have had to solve was the interface for the editor-plugin that wraps the PM plugins.
  - Compared to PM-based editor frameworks, Atlassian’s editor doesn’t store schema alongside the editor-plugins but in a separate repository. 
  - This isn’t really a modular approach to create shareable editor-plugins, but for a purpose-built editor I think it makes dealing with the schema a lot easier.
- Another interesting thing I did was trial the editors with SSR, mainly Next.js, and while it worked all right there are some caveats to be aware of. 
  - Mainly not being able to access document or window object in server-side requires some if’fing to do.
- Some of the major things I have not yet completely worked out is the toolbar components that are provided by the editor-plugins as React components. 
  - For now the toolbar is just fixed to one layout.
- With the Atlassian editor as reference, implementing new features should be a lot easier since you can just look at how they have done it and then working out your own solution.
- If you wanted to compare this approach to purely React-based rich-text editors, such as Slate.js, I have come to a conclusion that you will never achieve a similar synchronization in the DOM management if you had React with full control of the rendering and event dispatching. 
  - But at the same time I am pretty sure that having PM handle the DOM and React the occasional UI widgets, this approach is a lot more performant and customizable. 
  - The time required to work out how to setup a working React+PM scaffolding is another question, can’t say this was a trivial job even with a help of a good example. Maybe now however the job got easier
- EDIT: 
  - I also did some benchmarking with `ReactDOM.render` vs `createPortal` and noticed portals to be faster (350ms vs 230ms) in an operation where I create a large number of nodeviews in one big transaction.
  - In deletion portals seem to be magnitudes faster as `unmountComponentAtNode` forces React to immediately remove the node whereas by simply removing the portal from the map and then rerendering them incurs almost no latency.
  - But hmm, I think the rendering is now actually done outside of the `dispatchTransaction` where I track these latencies and therefore I can’t accurately calculate how long the unmounting of components take vs calling `unmountComponentAtNode` directly. Probably it’s a bit faster. In the meantime I guess I’ll revert back to portals.
- EDIT EDIT: 
  - Ok about 184ms and 270ms with portals vs 362ms and 573ms the old-fashioned way in the main task without the smaller tasks numbered in.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 
