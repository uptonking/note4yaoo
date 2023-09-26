---
title: thread-pm-base-office-whiteboard-draw
tags: [office, whiteboard]
created: 2023-05-30T21:36:19.919Z
modified: 2023-05-30T21:36:55.391Z
---

# thread-pm-base-office-whiteboard-draw

# guide

- [Rendering like Butter - a Confluence Whiteboards Story - Atlassian Engineering_202308](https://www.atlassian.com/engineering/rendering-like-butter-a-confluence-whiteboards-story)
  - Great insight into building high performance whiteboard for the Web
  - Finite State Machine
  - Entity Component System
  - WebGL
  - Tiling
  - While the essay concluded that the most efficient way to render things was using WebGL, the benchmark also showed that DOM+React was not that bad (3~4x slower than Raw WebGL)—small products and personal projects may not need the burden of WebGL.
# discuss
- ## 

- ## 

- ## What if @figma had a cursor video chat?
- https://twitter.com/alexeinars/status/1706333517242618342
  - 鼠标光标移动时，光标旁显示用户视频界面而不是偷笑

- ## Do you prefer @tldraw to @excalidraw ?
- https://twitter.com/jitl/status/1643764436660899840
  - Excalidraw is ahead on features, TLDraw is ahead in my heart
- I like the code a lot more than the Excalidraw code, and I've learned a ton from following @steveruizok's work over the years

- ## meeting Steve and spending the day understanding @tldraw ’s vision (not as “another excalidraw”, but an embeddable canvas for everyone) 
- https://twitter.com/swyx/status/1598558782388256768

- ## A tangent thread is about how spatial canvases come into play. 
- https://twitter.com/chrisshank23/status/1663296920150999040
  - Particularly thinking about @tldraw 's early vision to provide a platform for other to build spatial canvases...
- I see a gap between unstructured spatial canvases and meaningful, structured diagramming tools. Spatial canvases nudge you to create your own conceptual framework for a task. Diagramming tools are domain-specific and have little extensibility.
  - The unstructured nature of a spatial canvas likely manifests in its implementation of a bunch of lines/shapes with coordinates that you move around. These shapes have no inherent relationship or meaning in the data representation only the human perceiving the canvas.

- What's cool is that the "nextgen" spatial canvases like @excalidraw and @tldraw are starting to explore this a little. 
  - For example, both have the first-class concept of arrows/lines connecting shapes together!
