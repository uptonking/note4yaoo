---
title: lib-draw-app-community-whiteboard
tags: [community, drawing, whiteboard]
created: 2023-09-07T04:17:00.902Z
modified: 2023-09-07T04:17:31.787Z
---

# lib-draw-app-community-whiteboard

# guide

- 画板或批注类产品要参考规范 [Web Annotation Data Model](https://www.w3.org/TR/annotation-model/)

- 画板内的文本常使用多个富文本编辑器实现，可参考tldraw

- 
- 
- 

# discuss-figma/prototyping
- ## 

- ## 

- ## [Does Figma have any serious competition? : r/UXDesign _202212](https://www.reddit.com/r/UXDesign/comments/zd2odq/does_figma_have_any_serious_competition/)
- Figma is still really poor at making interactive mock-ups. Axure remains my go-to for that.
- I've been considering bringing Axure back into my workflow to prototype in-page and micro interactions. I was a bit surprised to see that they haven't made any updates in years. Has it been abandoned?
  - Axure still issues periodic updates, though I couldn’t tell you the last time a big feature was added or significantly changed.
  - I find Axure still offers a robust and relatively easy to use set of features for creating interactive mock-ups, and I greatly prefer interactive mock-ups over a series of annotated static screens. I also don’t love the infinite canvas that’s used in both Figma and Miro. It has its uses but I find it disorienting to pan and zoom all over the place.

- Figma has won this race and has became the industry standard tool. For now you can still watch the ongoing competition FigJam vs Miro

- I use Figma for design and Axure to prototype since it is so much more robust.

- Figma is big in the product designer space then sketch, etc. 
  - Axure is bigger in the UX designer/research space since it requires "if/then" tools

- Not currently, not for a long time. None of the current tools are comparable. Sketch used to have no competition for a long time as well, but Figma plug ins allow the apps to go beyond what the developers build. Also, cross OS systems arnd browser-based options are really nice. Long dead the time where design tools are strictly in for Apple.

- Framer is coming.

- ## 看了一下 http://Builder.io 新的博客，介绍了他们的从 Figma 到前端代码是如何实现的。
- https://twitter.com/iguangzhengli/status/1714976679943368985
  - 首先将 Figma 设计稿通过专门训练的 Builder AI 模型转化为JSON结构化数据，再通过开源编译器Mitosis 将结构化数据转成 React/Vue 的代码。最后通过一个微调的模型进行优化代码。
  - [Introducing Visual Copilot: A Better Figma-to-Code Workflow](https://www.builder.io/blog/figma-to-code-visual-copilot)

# discuss-stars
- ## 

- ## 🕸️ just got this nice little auto-layout algorithm working
- https://twitter.com/dragonman225/status/1714612402527109504
  - there's a catch - while it produces interesting patterns for multimedia content, it's terrible at tidying up document-like long rectangles
  - 适合自动整理短卡片，不适合自动整理长图片
- how's this done
  - pt1, put the biggest box at the center
  - pt2, pick a random box, put it to the right of the first-positioned box, with an offset down, which provides possibility for positioning the next box
  - pt3, pick another random box, put it at a vertex that is closest to the original center without overlapping
  - pt4, repeat the previous for the remaining boxes
- flatten-js is a convenient toolbox for geometric calculations
  - Use "unify" to get the polygon formed by multiple boxes
  - Use "Relations.touch" to check if a box can be placed at a vertex

- kind of reverse: auto-grouping (using AI/algorithims) based on content possible ?
  - good idea! I think that with AI, it's common to classify content by positive/negative attributes or emotions.

- a different algorithm, which looks "tidier" 
  - this one is using potpack (https://mapbox.github.io/potpack/) with some modifications, such as adding gaps between items and aiming for a rectangular bounding box with a ratio similar to the computer screen's.

- 
- 
- 

# discuss-ai-draw
- ## 

- ## 

- ## 

- ## A new open-source model StarVector with a specific focus on SVG drawing was added to Huggingface. 
- https://x.com/testingcatalog/status/1903590867564175398
  - "StarVector is a foundation model for generating Scalable Vector Graphics (SVG) code from images and text."

# discuss
- ## 

- ## 

- ## 

- ## 

- ## ⚖️ [JSON Canvas – An open file format for infinite canvas data | Hacker News _202403](https://news.ycombinator.com/item?id=39670922)
- Some context about why we created JSON Canvas:
https://obsidian.md/blog/json-canvas/
  - We just released it today, so this is still a very nascent project. A little over a year ago we released Obsidian Canvas. The .canvas file format has felt stable enough to give it a name and resources that other apps can freely use
  - The spec is conservative, and definitely does not support many features canvas apps will want to implement (yet).
  - The purpose of giving JSON Canvas a name and site is to encourage an interoperable ecosystem to grow around this format. 

- do you have any notes on why this isn't SVG? Which existing formats were considered before building your own, e.g. SVG/Excalidraw/draw.io/...?
  - Looking at the JSON, I assume this is a higher level format that may output SVG
- It makes sense if you see Obsidian as the starting point - it's a document store. While other canvas products may be more graphics-oriented, Obsidian's is about laying out documents and objects and providing simple relationships between them. For this purpose, JSON's probably a lot easier to work with than XML/SVG.
- Obsidian's philosophy is file over app and releasing a spec for their Canvas feature is fulfilling that promise. It's a strictly positive 'today is better than yesterday' thing for them to have done so.

- SVG is great and you are the first person I have ever seen who would (and did) imply that SVG might be or would be better than JSON for this kind of thing.

- I'm still glad SVG exists because it's available on the web for free, but this file format is really a mess (very hard to parse, the feature set is so broad it's never entirely implemented and the implantations diverge making it surprisingly hard to support multiple browsers).

- From my Analysis, GraphML, although specified in XML, seems to be one of the most widely used exchange formats, especially with the yWorks extensions for yEd.

- ## [Show HN: Obsidian Canvas – An infinite space for your ideas | Hacker News_202212](https://news.ycombinator.com/item?id=34066824)
- 
- 
- 
- 
