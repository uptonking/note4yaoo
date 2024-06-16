---
title: lib-editor-quill-community
tags: [community, quill]
created: 2023-02-09T18:23:29.864Z
modified: 2023-02-09T18:23:43.486Z
---

# lib-editor-quill-community

# guide

# not-yet
- ## 

- ## [Add support for tables](https://github.com/quilljs/quill/issues/117)
- https://github.com/volser/quill-table-ui
  - https://codepen.io/volser/pen/QWWpOpr

# discuss-stars
- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## [Handle text replacements explicitly _202306](https://github.com/quilljs/quill/pull/3807)
- Definition of Text Replacements
  - The most common scenario occurs when a range of text is selected, and the user presses any keystrokes.
  - Additionally, built-in spell checks and some platform-specific operations (e.g., emoji picker, text replacement settings on macOS) can also be considered as text replacements.
  - It's important to note that the selection does not necessarily need to encompass the text that is about to be replaced. for example, floating toolbar
- In the case of text replacements, we currently rely on the browser's default behavior and then utilize MutationObserver to synchronize DOM changes with the model. Sometimes, this approach doesn't work well, as browsers may generate unexpected mutations that Quill is unable to process.
  - At Slab, we handle text replacements explicitly with Input Event
  - This PR mostly moves the code to Quill but also handles IME as well.

- ## 🔀 [pr已合并: Support OT for table _202205](https://github.com/quilljs/quill/pull/3590)
- This adds the OT ability for table format and also supports nested scrolls.

# discuss
- ## 

- ## 

- ## The popular editor Quill v1 uses a deprecated API that will break in July. _202404
- https://x.com/kevin_jahns/status/1782779684805062773
  - Quill v2 just got released and fixes the issue.
  - I already upgraded the Yjs bindings for Quill v2

- Will this also affect other Yjs based libs?
  - I don't think so. None of my libraries use mutation events. The API was already deprecated when I started Yjs. It is used to listen to DOM manipulations. Prosemirror and Codemirror should be fine.

- ## [Single line only ](https://github.com/quilljs/quill/issues/1432)
  - Is it possible to setup Quill to only allow for one line of text, and no line breaks? I'd also like to get rid of the wrapping paragraph tag if possible.
- You cannot get rid of the wrapping tag (though you can change it to some other wrapper other than paragraph). There is no configuration to limit the number of lines, though you can use keyboard listeners to prevent the possible inputs. You can also just listen on `text-change` and if a newline is inserted, use `deleteText` to reverse it.

- Is there a way to block `enter`? 
  - keyboard: { bindings: { enter: { key: 13, handler: function() { return false; } } }

- ## 🗑️ [Destroy editor instance _201605](https://github.com/quilljs/quill/issues/662)
- An explicit destroy is no longer necessary as Quill no longer keeps track of all editor instances. Just remove references to the instance and remove from the DOM and it will be garbage collected.

- If you looking for more shorter solution i would wrap the editor-container in an other container (#mainContainer). Then you can clear these conatiner like that: #mainContainer.innerHTML = ''. If you wish a new clean instance afterwards you create a new editor element and appended to your #mainContainer. Then you can init a new quill instance again.

```JS
// I logged the entire quill object and went through all instances of toolbar, tooltip and clipboard in order to find a cleaner way to remove these from the DOM. I discovered that the right paths to be as follows
quill.theme.modules.toolbar.container.remove();
quill.theme.modules.clipboard.container.remove();
quill.theme.tooltip.root.remove();
```

- ## [I started rewriting using hooks and React 17 compatible APIs _201911](https://github.com/zenoamaro/react-quill/issues/547)
- Do you have something you would recommend for inclusion? Eg. code or documentation about Katex?
  - I think polling window.katex works well with async CDN script tags.

- ## [How to read in existing data into Quill JS - Stack Overflow](https://stackoverflow.com/questions/39733120/how-to-read-in-existing-data-into-quill-js)

```JS
quill.setContents({
  "ops": [
    { "insert": "this is a test bit of text\n" }
  ]
});

quill.clipboard.dangerouslyPasteHTML("<p>here is some <strong>awesome</strong> text</p>");
quill.pasteHTML(YOUR_HTML_HERE, 'silent');
```

- ## 🎯 开源富文本编辑器 Quill 2.0 刚刚发布了！这也是我第一个全职做的开源项目 _20240417
- https://x.com/luinlee/status/1780428748837593472
- 支持 markdown 输出吗
  - 没有内置支持，因为用户可以扩展自己的格式。不过 Quill 可以导出 Delta 格式 (quill.getContents())。有一些 Delta 转 Markdown 的库，或者自己写也不麻烦
- 希望内嵌表格能更完善一点。
  - 目前底层已经支持表格嵌套其它 block 了，不过表格模块本身还没有用到这个特性，下一步会优化哈
- 我们当前使用类似 ListContainer 的机制实现，数量多了性能不太好。
  - 我们的实现是每个单元格都是一个 Quill 编辑器，不过默认不渲染编辑器，只有当用户第一次互动时才初始化。基本上是 contenteditable 的性能瓶颈了
- 在quill上投入了2年多，不过当时看着不更新了，就基于dev分支进行二次开发，中间也踩了非常多的坑。目前正在做表格相关的事情，方案用table-embed的方式，看过slab的表格，目前还不支持单元格合并，希望做个类似飞书的表格

- ## 🎯 [Quill v2 – Rich text editor | Hacker News _202404](https://news.ycombinator.com/item?id=40089460)
- I've used prosemirror enough to have written custom nodes, commands, and custom code around its collaboration model. 
  - I got good results with all of this and I don't know any other platform that could have matched it. The docs are thoughtful. 
  - There's an up-front learning curve to understand the architecture. When doing highly customized things, I referred to the source when needed. 
  - For standard rich text, there are a lot of options. Prosemirror shines when you want to build on it as a platform.

- I will never use Quill for a production project again. We started using Quill 1.x around 2016, I initially liked it a lot.
  - Fast forward to 2019, we were running into some bugs, Quill 1.x was in maintenance mode, and 2.0 was effectively undocumented
  - 5 years later, Quill v2 is finally live. I'm glad to see Slab is still around, and I hope they have the bandwidth to publicly maintain Quill going forward.

- TinyMCE just changed their licensing from MIT to GPL(202402), which may impact your decision. 
  - Fun fact - TinyMCE and CKEditor are both owned by the same holding company (Tiugo Technologies).

- ## 🎯 [What Quill version to use?](https://github.com/quilljs/quill/issues/3356)
  - 1.3.7 which is installed from npm by npm install quill and was published 2 years ago.
  - 2.0.0-dev3 - this version is required for modules quill-better-table and quill-table-ui . It was published 3 years ago (???).
  - 2.0.0-dev4 - this version I found in npm versions history. It was published a year ago
- it looks like dead from current 1.1k open issues, and this Contributors Insights: 2013-2017 were the most active days, and since 2019 very low development activities

- ## 🎯 [Announcing Quill 1.0 | Hacker News _201609](https://news.ycombinator.com/item?id=12437345)
- I note that (at least in the playground example) there's zero attention paid to accessibility

- I use Quilljs because it's a great implementation of a modern-thinking WYSIWYG text editor. The underlying parchment library helps a lot to separate out the data model from the rendered view (instead of relying on contenteditable to handle your data model, like many other classic rich text editors do).
  - since rich-text is just a JSON object, I can do interesting database queries that are a bit trickier to pull off if it had been HTML
  - Quill emits delta objects on user interaction (that conform to an operational transform model), so it's pretty straightforward to wire it into a concurrent editing system. This isn't batteries-included (you have to deal with resolving the operational transforms yourself, which is of course tricky) but it's a great start in that direction.

- Quill's OT type is compatible with ShareDB, which provides a simple to use backend that takes care of all this coordination.

- Some strengths unique to Quill:
  * API Quill has the most powerful API of any editor I have seen. You can make any text or formatting change in any part of the editor at any time. Trix by contrast only allows changes to the current selection.
  * Modules Quill's internals are broken into modules that themselves can be configured or even swapped out. Many modules also include their own APIs. Trix does not have documentation in this regard, but looking at its codebase, it does not appear designed to support major modification of its internals.
  * Formats/Content Quill's document model itself is customizable, which allows users to define their own formats or customize existing ones. This capability is what kicked of 1.0 development
  * One main idea I'd like to highlight is this: Text is no longer written to be printed. It is written to be rendered on the web—a much richer canvas than paper. Quill 1.0 was designed and built to support this next generation canvas.

- 🆚️ Can anyone tell how Quill compares to Draft and ProseMirror?
  - ProseMirror's main is insight is the need to maintain a document model in parallel with the actual DOM. While most modern editors also do this, ProseMirror also allows their document model to be extended and customized, which only Quill and possibly Draft is also capable of. I think this is the right idea and foundation to build on top of (Quill also made this choice).
  - One issue I believe ProseMirror has yet to solve well is the concept of embeddable widgets.
- Looks to me like a big difference is that Quill is HTML/DOM-oriented, whereas ProseMirror has a generic document model that is format-agnostic and allows custom parsing/serialization.
  - as far as I can tell, Quill doesn't have a document model as such. It only has a flat sequence of deltas
  - ProseMirror, on the other hand, explicitly defines a document model as part of its API, arranged as a tree (DAG). The benefit is that don't need a complicated, potentially lossy translation between the flat and non-flat versions
- Most editors nowadays maintain a parallel structure to the DOM. And since the DOM is a tree, that structure is also a tree. Quill's is Parchment and goes a step further by also having an API and allow defining new nodes, which ProseMirror (and maybe Draft) also does.
  - Deltas are a simple, iterable output format for Quill. 
  - In practice it is much nicer to deal with this in many use cases than the Parchment tree.

- 🆚️ How does Quill compare technically with DraftJS?
  - Draft’s own description of itself is "Rich Text Editor Framework for React" and is more comparable with Parchment, both being a foundation in which you can build a rich text editor. But there are many pieces missing for it to be a full fledged editor like Quill.
  * UI Draft only has buttons you can toggle for formats. There are no dropdowns to select 
  * API - Quill’s API is designed for the editing use case. Draft is built on React and inherits many primitives and ideas that are more appropriate for websites, rather than linear content like text
  * Markup - With the exception of nested lists, Quill’s markup is clean and semantically correct. Draft uses `<span>` tags with inline styles with lots of attributes for bookkeeping.

- 🆚️ How does it compare with TinyMCE and CK Editors?
  - TinyMCE and CK Editors are implemented with contenteditable, which is a very flawed mechanism that isn't standard or consistent across browsers.
  - Quill relies on contenteditable in order to support certain operations, such as pasting. 
  - Quill has its own document model, and supports things like deltas/operational transforms, which are practically impossible if you use the DOM as the truth like TinyCKE et al do.

- ## [Quill – A cross browser rich text editor with an API | Hacker News _201510](https://news.ycombinator.com/item?id=10446865)
- We built Quill to because my previous company needed a modern editor with an API to manipulate the contents (our use case was collaborative coauthoring). Before I left we open sourced Quill and I have been working on it since.

- 🆚️ Could you compare and contrast Quill with some of the other editors that have popped up on HN recently? 
  - I would say the old approach was to add contenteditable=true to a `<div>`, call execCommand for formatting, and try to fix the issues this would cause. 
  - Editors in the last couple of years simply avoid using contenteditable in as many cases as possible. 
  - So the major differences would probably be when and where each of these editors tolerate native contenteditable behavior and which implement it themselves. 
    - But it's near impossible to not use contenteditable at all and all editors that I know of (including Trix and ProseMirror) use it to some degree.
    - For example to handle paste, I've found the best way is to detect a paste, shift focus to another invisible contenteditable div, interpret the pasted content, and insert that into the actual editor through the editor's API. That way no weird/unexpected markup ends up in the editor (whether or not the editor also utilizes contenteditable).
  - Another trend is a focus on the document model, which is the editor's main data structure to keep track of content. 
    - Older editors just use the DOM (or HTML strings) and hand that to you as their API. These editors really don't know themselves precisely what content they contain and cannot offer an API for the simple task of inserting text in a specific nth position. Extensibility becomes quite limited and often leads to a lot of edge case code. 
    - I think ProseMirror is right to have the document model as a focal point as I've reached the same conclusion with Quill and have worked on to improve for some time now. 
    - The upcoming 1.0 version boasts a much more powerful document model that is being open source separately as Parchment.

- All of these new browser rich text editors look really nice, but without basic table support there is no way anyone can switch from TinyMCE (which is about as horrible as you can get).
  - Tables are hard to do well and there’s ambiguity as to what constitutes basic. After being able to create an NxM table, should you be able to add/remove rows/columns? What about resizing the width or height of rows or columns.

- what are the main use cases for RTE's? 
  - Websites. RTEs are a necessary evil there.
  - basic HTML markup 
  - HTML tables
  - images
  - black magic to cope with Word's markup

- ## 🚀 [Quill – An Open Source Rich Text Editor with an API | Hacker News _201405](https://news.ycombinator.com/item?id=7716376)
- This project was started originally at Stypi where we needed an editor with a better API than just getting/setting the text to support coauthoring. 
  - Stypi was acquired by Salesforce in 2012 but we continued to work on Quill because we felt it was a missing piece of the web. 
