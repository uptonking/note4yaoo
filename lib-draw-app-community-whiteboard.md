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

# discuss-ai-canvas
- ## 

- ## 

- ## 

- ## 

- ## [Best self-hosted AI UI? : r/selfhosted _202501](https://www.reddit.com/r/selfhosted/comments/1i4ef8g/best_selfhosted_ai_ui/)
- That "backend" is the actual LLM infrastructure; so, GPUs. The frontend is just some HTML/CSS/JS that communicates to that backend.
  - For instance, OpenWebUI can connect to various backends - but it is preferably used with an also selfhosted backend (like ollama or localai - which both require you to have your own GPU infra).
  - AnythingLLM is also just a frontend and has nothing to do with backend. 

- I really like LLMcord. Lets you interact with your LLM via a discord bot. No exposing ports, VPN, etc. you just pop in discord and chat with it. It supports images and files if you are using a vision-capable model

- Do any of these self-hosted UIs, using API, allow the sync of conversations across devices?

- ## 🕸️ [tangent: the AI chat canvas that grows with you : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1hgc64u/tangent_the_ai_chat_canvas_that_grows_with_you/)
  - https://github.com/itsPreto/tangent /270Star/apache2/202502/python/js/inactive
  - I just open-sourced a project I've been tinkering with called tangent. Where instead of your usual, generic, & linear chat interface, it's a canvas where you can branch off into different threads and explore ideas organically.
  - I want it to actually learn from your past conversations. The idea is to use local LLMs to analyze your chat history and build up a knowledge base that makes future discussions smarter - kind of like giving your AI assistant a real memory.
  - Another neat feature I want to add: automatically understanding why conversations branch. You know those moments when you realize "wait, let me rephrase that" or "actually, let's explore this direction instead"? I want to use LLMs to detect these patterns and make sense of how discussions evolve.

- So basically you're doing like the Obsidian document graph but for AI and it's automatically linked by the AI based on relevance of each discussion? This would also be useful for documents, any other document.

- Have you considered using an application like Obsidian for the base of the application? Thats what I decided to do after reinventing the wheel for a majority of the UI features so I could focus less on UI.
  - I haven’t even looked at Obsidian or Excalidraw’s codebase as I assumed it would be massive enough to discourage me from doing this— but now that I’ve got the prototype functional that’s definitely a path we could explore

- This UI concept for chatbot is gonna be a major thing, I'm sure. This is really great!

- ## [OpenWebUI Canvas Implementation -- Coming Soon! (Better Artifacts) : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1i3as1m/openwebui_canvas_implementation_coming_soon/)
  - I'm implementing Canvas (beefing up Artifacts) on OpenWebUI.
  - This was my only issue ever with OpenWebUI, just the very limited canvas feature (only restricted to HTML, CSS, JavaScript and SVG).
  - I've expanded support for the following languages
  - Another notable feature I'm adding is to switch between Design view and Code view for web design.

- Mermaid is already supported iirc

- Sometimes I wish OpenwebUI had the addon/extension model that browsers have where users could just go to the addon library and pick and choose what they want to add to their OpenwebUI experience.
  - unless I am misunderstanding your request, they do... https://openwebui.com/tools https://openwebui.com/functions
- These are "plugins" for the LLM backend, less so for the frontend. I think what u/Elite_Crew asked for is particularly for a frontend extension store.
  - The functions modify or enhance the behavior of the model. That's what I meant by backend. Front-end plugins would allow for adding functionality like canvas.

- Could you just have something that supports tree-sitter for syntax highlighting?

- Does OpenWebUI have the same feature from Claude where if you copy something that doesn't fit nicely in the chat window, it adds it as an attachment to the chat window? That would be pretty sick.

- ## [Is there local app that mimics OpenAI's Canvas or Anthropic's Artifacts? : r/LocalLLM _202502](https://www.reddit.com/r/LocalLLM/comments/1int9fr/is_there_local_app_that_mimics_openais_canvas_or/)
  - I've tried LM Studio and Msty, and neither are able to have a separate document that I can edit via prompts. Does such an app exist? Preferably for Windows?

- Open WebUI will let you edit and run some things directly from the generated code. I've been able to edit and run generated python code, see and edit live canvas renders of HTML
  - I haven't used it in Claude but on ChatGPT I find the edit in canvas a little clunky. It opens a separate pane to the side with the code and then you have to switch back and forth for a live preview
  - Open WebUI lets you edit the code in the midst of the chat itself and shows the updates in the live preview canvas. It's also quite clever at automatically opening a canvas

- What I'm looking for is the Google or Word doc to be the "Canvas" and there is a separate panel to enter my prompts, which will in turn edit the doc. I don't want my prompts in the doc.
  - You can have your prompts in the Add-in panel. BTW, we just released a new "Track Changes" feature as below. The demo shows that your document remains separate from your prompts."

- ## [OpenAI just released artifacts for ChatGPT called canvas : r/singularity _202410](https://www.reddit.com/r/singularity/comments/1fvct1c/openai_just_released_artifacts_for_chatgpt_called/)
- Gemini had this for ages, and allowed editing in place, and regenerating segments.

- 💡 This makes using AI to edit drafts of long emails/letters/etc actually practical. Previously it was never worth the hassle for me of copying and pasting it back and forth.

- artifacts are kinda only useful for code, this totally changes the way we use AI in general beyond code so that's why I believe this is bigger than artifacts

- The problem with Claude Artifacts was their short 200k context length and ChatGPT has even shorter one at 128k...

- ## 🚀 [Introducing canvas, a new way to write and code with ChatGPT. | OpenAI _202410](https://openai.com/index/introducing-canvas/)

- features-writing
  - suggest edits
  - ask ai from floating toolbar
  - polish
  - Adjust the length
  - Change reading level: from Kindergarten to Graduate School
  - Add emojis: Adds relevant emojis for emphasis and color.
- features-coding
  - review code
  - add comments
  - add logs
  - port to another language

- We’re introducing canvas, a new interface for working with ChatGPT on writing and coding projects that go beyond simple chat. 
  - Canvas opens in a separate window, allowing you and ChatGPT to collaborate on a project. 
  - Although the chat interface is easy to use and works well for many tasks, it’s limited when you want to work on projects that require editing and revisions.
- With canvas, You can highlight specific sections to indicate exactly what you want ChatGPT to focus on. 
  - Like a copy editor or code reviewer, it can give inline feedback and suggestions with the entire project in mind.

- We trained GPT‑4o to collaborate as a creative partner. The model knows when to open a canvas, make targeted edits, and fully rewrite. 

- 
- 
- 
- 
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
