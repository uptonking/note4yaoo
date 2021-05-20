---
title: lib-editor-community
tags: [community, editor, lib, text-editor]
created: '2021-05-14T12:04:27.547Z'
modified: '2021-05-14T12:04:55.412Z'
---

# lib-editor-community

# guide

# discuss-stars

- ## [如何不借助 contenteditable 实现富文本编辑器？](https://www.zhihu.com/question/366666295)
- 在浏览器里，打开了 contentEditable 不等于借助了 contentEditable。
- 粗略看来，一个 DOM 元素加上 contenteditable 属性后，就大致具备了这些能力：
  - 选区的拖选编辑和光标闪动支持
  - 方向键控制时的默认行为
  - 输入文字时的默认行为（牵扯到输入法）
  - 复制粘贴时的默认行为（牵扯到富文本剪贴）

- ## Which one was the one with the bad performance on long documents? ProseMirror or CodeMirror?
- https://twitter.com/thomasaull/status/1314484953686695936
- CodeMirror is normally much faster for big documents, 
  - but from the context, I suspect that in this case the magic layered on top to make CodeMirror behave like a rich text editor is the source of the slowness.

- ## Why is CodeMirror not based on or replaced by ProseMirror?
- https://twitter.com/tjconceptdk/status/1035585261198041088
- They solve different problems -- `structured rich text with configurable schema` versus `plain text with syntax highlighting and lazy rendering` . 
  - On the web you don't want to ship big, overly general code for a smaller problem

- I was doing some research and I was wondering why you didn't use the same textarea technique in ProseMirror as you did in CodeMirror? Is it planned or impossible to implement in a rich text editor? 😊
  - Because it is a more problematic hack than just using contenteditable. CodeMirror 6 will do the same

# discuss

- ## 

- ## 

- ## 

- ## ProseMirror – A toolkit for building rich-text editors on the web
- https://news.ycombinator.com/item?id=18998042
- What sets ProseMirror apart from the rest (Slate, Quill, Trix, Draft, etc.) is - ProseMirror isn't simply a library. 
  - It's an entire platform with all bits and pieces needed to build a simpler rich text library. Rightly named "toolkit" instead of a "library".
- Interestingly, the platform design of ProseMirror is one of the key reason which drives me to Quill in one of my side projects. 
  - Don't get me wrong, if your goals mostly align with ProseMirror, it's a perfect tool, 
  - but if you want to deviate with ProseMirror in some aspects, the coupling design between different ProseMirror packages is actually a headache. 
  - On the other hand, Quill feels more like a simple library targeting exactly one use case.
  - In addition, I feel that Quill's [delta format](https://quilljs.com/docs/delta/) is much more elegant and easier to work with than ProseMirror's [changeset](https://github.com/ProseMirror/prosemirror-changeset), especially if your architecture uses a different language that's not JS.

- If any of you have used Quill and Prosemirror, what were your impressions of the differences between the two? Here's what I've observed so far:
- DraftJS (React) 
  - works on desktop, but has no plans for collaborative editing, mobile support, and limited development. 
  - We found it hard to extend the paste handling for custom behaviours too. 
  - On the other hand, there are a lot of nice libraries built around it (we used medium-draft)
- Slate (React) 
  - is definitely the way to go for React developers who don't yet need mobile support. 
  - It's mature and has a good community of developers. 
  - The one downside is that some of the popular plugins lost compatibility with the latest version of Slate
- Quill (non-React) 
  - seems very mature with a good ecosystem of plugins. 
  - Instead of relying on React Components, it relies on there being a strict mapping between the DOM and the model that you build. 
  - The "model" is the DOM, so-to-speak, but with heavy restrictions to avoid ContentEditable issues. 
  - We've found it to be very mature, and it's the only one of the 3 we've found to have great mobile and collaborative-editing support out of the box. That was important for us, so we ended up using it today

- I've briefly analysed ProseMirror as well as Quill. IMO ProseMirror seemed well built with better literature compared to Quill.
  - ProseMirror's author has truly thought out every API and has got most of the details just right.
  - For example, if I ought to build a grammar checker on top of Quill vs ProseMirror, I couldn't find any APIs in Quill that lets us decorate the view with grammar errors and suggestions, without polluting the core data-model with custom nodes/attributes. 
  - ProseMirror on the other hand had the concept of Decorators (https://prosemirror.net/docs/ref/#view.Decorations) for such a case. That was just one example.
  - More from the author of Quill himself

- ## ProseMirror 1.0 
- https://news.ycombinator.com/item?id=15465125
- Author of Quill here. 
  - Interested in hearing Marjin’s thoughts but here are some of my main observation is at a high level Prosemirror is much more willing than Quill to sacrifice simplicity for power. 
  - This value difference manifests in the target audience, architecture and API design:
  - Quill can be used for the get going quickly drop in use case. 
  - Prosemirror specifically warns against this: “If you're looking for a simple drop-in rich text editor component, ProseMirror is probably not what you need. (We do hope that such components will be built on top of it.) The library is optimized for demanding, highly-integrated use cases, at the cost of simplicity.”
- Prosemirror’s schema, as documented, is more flexible than Quill’s.
  - Prosemirror appears to allow anything, whereas Quill imposes some constraints. 
  - For example Quill requires all nodes to either be a leaf and cannot have children or a container and must at least one child. 
  - There cannot be a node that can optionally have children as is allowed in Prosemirror. 
  - In my experience the constraints Quill imposes lead to a more consistent and bug free experience across browsers. 
  - I will be curious to try out the edge cases I have encountered at this new 1.0 Prosemirror to see if it handles them the way an end user typist would expect. If Quill can benefit from a shift in the flexibility in its schema, it will do so.
- Quill is far more battle tested. Slack, Salesforce, LinkedIn, Intuit and many others are using Quill in their main user-facing production products, not an internal employee only tool. 
  - Prosemirror has a great start with the NY Times but there is a large difference in adoption at the moment.

- ## Editor.js – Block Styled Editor
- https://news.ycombinator.com/item?id=19555633
- From a data management and flexibility standpoint, I see why block editors are becoming popular with some people. 
  - But as a user, it feels like a downgraded experience.
  - When writing multi-paragraph prose, the first draft isn't always the final draft. Quite often there's some shuffling around of parts of the content. 
  - With blocks, the user can't highlight part of one paragraph and into part of the next one because of the artificial container boundary.
  - Perhaps with some well planned keyboard shortcuts and other UI improvements, the friction can be reduced. Maybe also it will require a change in the way some of us think about content (although I still object to the user needing to think of content in terms of its subtypes and storage structures).

- I'm the current maintainer of https://github.com/madebymany/sir-trevor-js which we started in 2012. 
  - At the time we had a fully block based approach and migrated to more of a document based approach when medium.com gained traction.
  - Since then we've debated what's the best approach for cross block selection as now the expected behaviour is very much that of a text editor such as word rather than a block based editing tool which it started out as. 
  - A couple of years ago we embarked on a rewrite that saw us look for a solution to the problem that would solve this. 
  - Not just a block based selection, but a cursor based selection between blocks, but this never got to a level we were happy with.
  - I think with the evolution of online editing over the years and editors such as notion.so the approach they've taken with the multiple contenteditable elements is a good first step. 
  - Over time we'll see how far they are able to take it. Adding features such as cross browser support, undo/redo and keyboard navigation.
- I'm a maintainer of Editor.js. Regarding to your questions:
- Editor.js doesn't support nested blocks.
  - We keep structure flat and want Tools API to be as simple as possible for new developers. 
  - The target audience of the Editor.js is media and blogs, usually you don't need complex structure there. 
  - However, you can implement some complex plugins for your needs, nested lists as example.
- We consider development of the editor very serious and understand importance of the test coverage. 
  - At the moment we don't have unit neither e2e tests but this is the one of our next steps on the way.

- Two long established predecessors to this: Sir Trevor JS and Colonel Kurtz
- I've used Kurtz extensively and it's been brilliant. 
  - The only downside of all these block-based editors is that you can't easily create layouts where images float to the left or right of text. 
  - Well, you can create them but you don't get a WYSIWYG idea of what it looks like right in the editor. I can live with that!
  - I've explored all sorts of editors and Colonel Kurtz is the one that's worked best: Trix, Draft, TinyMCE, CKEditor, ContentEditable, ProseMirror - just off the top of my head.

- ## Announcing: Work is underway on CodeMirror 6, a full rewrite with accessibility, mobile support, and modularity as design goals. 
- https://twitter.com/teppeis/status/1034581567551631361
- How will this affect ProseMIrror project? What is the difference?
  - ProseMirror is for structured text, CodeMirror for plain text and code. They don't really affect each other
- Will it support the native browser spellchecker?
  - Somewhat. The main issue is that in many browsers, the spell checker gets completely confused (removes most of its underlines) when you programmatically touch the DOM. And in typical situations, CodeMirror will do that to adjust the highlighting.
  - Still, we do take care to only mess with the DOM when necessary, so when in content that doesn't change it highlighting during typing (Markdown without markup, HTML text nodes) it might work pretty well. Haven't done that much testing there yet
- Monaco still doesn't support even arrow keys on iPad/iOS. Ace and codemirror are at least usable.
