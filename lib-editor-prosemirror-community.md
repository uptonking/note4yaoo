---
title: lib-editor-prosemirror-community
tags: [community, editor, prosemirror]
created: 2021-06-12T02:40:46.194Z
modified: 2021-06-12T02:41:33.389Z
---

# lib-editor-prosemirror-community

# guide
- search
  - notion block editor
  - save to database
  - block data model
  - virtualize/viewport
  - form
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 时隔多日再次跑 #ProseMirror 的 Hello World，这次有了不一样的感受。简单总结下。
- https://twitter.com/zQwQs/status/1619400529049960449
- 首先编辑器就是个 View，它的功能
  - 一是把 State（包括文档内容、光标和选区位置）以及 props里的Decoration（比如搜索结果高亮标记）给渲染出来。
  - 二是接收其他地方（例如dom事件、插件、调用等）传来的对state的修改
- State 包含了文档内容doc、选区光标selection。每次移动光标或者输入，都等于更新state然后导致view渲染。
  - 遵循『不可变』理念，我们不直接改 state，而是通过 Transaction（就是总看到的 tr 对象）来改。它暴露了诸如插入文字，替换选区等变换函数，每一次变换都产生新tr，且里面包含最新的doc和选区
  - 因此修改文档的过程，可以总结为创建新 tr（有多个步骤就一步步产生，但是只保留最后那个tr），再一次性提交最终修改结果到 view 里。
- 回到 view 也就是整个编辑器本体，它渲染的样子不仅仅依赖于它的 state，还依赖于 props。
  - 使用 props 可以实现很多能力。比如，要处理键盘事件，可传入 handleKeyDown。或者，做了个全文搜索功能，要高亮一些区域，则可通过 decorations 传入要高亮的区域和样式。
- 在 #ProseMirror 中还有插件（Plugin）机制。插件可以为 view 设置 props，并且插件之间不会出现 prop 互相覆盖的问题，有完善的处理机制：
  - 例如：多个插件对不同区域做高亮，都会生效；多个插件响应同一快捷键，则根据插件注册顺序执行，且先注册的可以阻止后面的执行。
- 类似我们开发 React 组件，插件也可以有状态state、需要渲染view。这些都可在插件里定义
  - 【初始化】插件的state.init、view的初始化函数
  - 【更新】编辑器state即将因tr而更新
  - →触发插件state.apply更新状态
  - →更新传给编辑器view的props
  - →触发插件view.update回调更新渲染
  - 【销毁】view.destroy 回调

- ## ProseMirror is now a TypeScript project_v20220520
- https://discuss.prosemirror.net/t/prosemirror-is-now-a-typescript-project/4624
- the code is now typed using strict TypeScript
- No breaking changes should have been made to the JavaScript interface.

- ## Why did you pick that over Slate or Draft?
- https://twitter.com/nikgraf/status/1415726807446401024
- Afaik all of the are maintained.
  - Draft’s data updates don’t allow for an integration with a CRDT.
  - Slate is awesome, but the API changed a lot over the years and still lacks Android support.
  - Every team that I know where the editor is part of the core UX switched to Prosemirror.

- ## Minimal UI Math Editor - Treena
- https://discuss.prosemirror.net/t/minimal-ui-math-editor-treena/3117
- can you share how you implemented the type ahead. i know there are a bunch of open source implementations ( `atlaskit` , `prosemirror-suggest` ), did you use any of those ?
  - So i based the insert menu on the code in the `prosemirror-mentions` package. 
  - I basically refactored the code to remove reliance on the included schemas in that package. 
  - The code is quite flexible so i just added a `fuzzy-search` for the displayed elements and a custom callback for each of the options. 
  - The callbacks are super similar to the included prose functions such as toggleMark! I hope thats helpful!

- ## parseDom Content for Inline Node (footnotes)
- https://discuss.prosemirror.net/t/parsedom-content-for-inline-node-footnotes/642
- Your node doesn’t allow content, so indeed, as you noticed, the parser won’t it won’t look for content.
  - Still, to be able to properly edit these, your node view is going to have to do a bunch more work (at the very least, it’ll have to set the `contenteditable` – or create a textarea with the content). Embedding an extra ProseMirror to edit a node like this will also get easier in the next release.
- I plan on adding a textarea to the nodeView’s dom for editing the annotation comment. And will be storing the value of the comment in an attribute when serialized into my dom structure.

- ## Using DOMSerializer inside a NodeView
- https://discuss.prosemirror.net/t/using-domserializer-inside-a-nodeview/1498
  - I’m trying to use `DOMSerializer` to produce DOM nodes so i can set the dom property inside a NodeView:
- The reason i’m doing this is that i want to set up event handlers on the resulting dom. 
  - The expected dom is too complicated to produce with the `document.createElement` method, so i tried to do it with `DOMSerializer` .
  - This almost works: the view is rendered, but it is not possible to interact with it.

```JS
class TodoListView {
  constructor(node, view, getPos) {
    const domSerializer = DOMSerializer.fromSchema(mySchema)

    const serializedDom = domSerializer.serializeNode(node, {})

    this.dom = serializedDom;
  }
}
```

- By defining a node view like this, you’re telling ProseMirror that the node is an opaque element that it shouldn’t manage. 
  - For things to be editable, you have to let the editor render them. 
  - So don’t render the children in the node view implementation, just provide a `contentDOM` property that the editor will render the children into.

- ## Understanding the interaction between parseDOM, DOMChange and NodeView
- https://discuss.prosemirror.net/t/understanding-the-interaction-between-parsedom-domchange-and-nodeview/678
- The issue centers around the way that dom mutations are parsed by PM, and this interacting poorly with my custom node view.
  - When you enter a character directly after the node view (and I suspect in other cases), PM tries to figure out what changed by parsing the content of the view, and analyzing the diff against the previous state. 
  - During general operation, this seems to happen pretty infrequently (the transactions are generated through some other means, that don’t rely on diffing the dom).
  - My custom view has a rather complex DOM structure
  - I initially didn’t realize that my NodeView would be parsed this way, and it seems that I lose the latex annotations inside my node during this parsing.
- the parser will get the node’s type and attributes from the node view.
- as long as you go through a transaction you should be fine.

- ## 🆚🤔 Inlining a node for a comment plugin or best to use marks?
- https://discuss.prosemirror.net/t/inlining-a-node-for-a-comment-plugin-or-best-to-use-marks/2391
- Comments are usually not modeled as document nodes—rather, they are references to ranges, that are tracked separately, outside of the document.
- I will try with references to ranges outside the document. One downside is that it could be a bit trickier to preserving comments when users copy to clipboard.
  - That is absolutely true. I’m not aware of an actual good solution to that problem, though you can get pretty far by storing metadata to the side when copying and consulting that, comparing it to the pasted slice, when pasting.

- ❓️ what are other arguments to not use marks for comments?
- For decoration approach, there is clear separation of non-editable document with ability to comment in “read only” mode.
  - The same is possible via mark approach if you have a centralized collab server and assert on transaction metadata, but this is again, more complicated and some don’t have a centralized collab server. 
  - If you don’t have a centralized collab server, you’ll probably (shouldn’t trust only client) need to diff the entire document JSON to ensure a user isn’t editing a document in non-authorized ways.
- The data structure for decoration comments are a more straightforward model defined solely by a single from/to.
  - The mark approach will mark each discrete block that is contained in the user’s selection and add each to the doc JSON.
  - The decoration solution will eventually produce DOM with multiple comment wrapper blocks (if necessary, ) but they are a view concern rather than something that is persisted into a data model
- That being said, decoration solution undo/redo indeed is difficult and I don’t have a working solution for that yet. But I eventually need to implement something of the sort.

- Right now the inline references are a decoration, but if that reference gets lost (e.g. through a cut/delete), the comments fall back to being referenced at the “block” level, which seems ok for now. The sidenote framework does work with multiple inline references pointing to the same note/comment though, so looking forward to getting this feature in. I will see if there is anything we can do to make it generalizable.
- how do you manage syncing? Do you use some library that utilizes IndexedDB (such as RxDB)
  - With regard to syncing, we are currently just using the standard prosemirror collaboration module. Our product is built on top of firebase at the moment, and we are using their real-time infrastructure to help keep things in sync. All of our changes are dispatched to our redux state as a middleware of sorts to prosemirror - and that is where we add the collaboration, and keep various views of the editor in sync.
- With regard to the web-components, we were using them as just other nodes (not even node-views) for a while, and then wrapped them in this class which basically adds right click ability. The only reason we didn’t do that in the web-components directly was that it is a different library and that was out of scope. 
- Making everything flow through Redux seems appropriate as it avoids managing various event listeners. It seems you’ve separated the UI & API state into Redux stores and PM specific state into plugins?
  - To connect back up to application logic, we are just using the same redux store in both places (including relevant prosemirror-plugin state). That redux store is also responsible for the editor state (just holds a reference to prosemirror-state). This also means that the state is available for other application components through selectors/actions/etc.

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

- ## 🎯 [ProseMirror 1.0 _201710](https://news.ycombinator.com/item?id=15465125)
- 👷🏻 Author of Quill here. 
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
