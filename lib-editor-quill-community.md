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
# discuss-storage
- ## 

- ## 

- ## 

- ## [which format of content should be stored into database postgresql? _201904](https://github.com/quilljs/quill/issues/2590)
- You should store the Delta returned from getContents(). 

- ## 💡 [Proposal: (Doc) write about **the correct way** to store & display quill editor content _201808](https://github.com/quilljs/quill/issues/2276)
- There are 2 way to store and then display content when using quill editor to write content.
  - (Delta) Store Delta into database (MySQL/PostgreSQL as JSON). then, when Display, use some library convert Delta to HTML and then display
  - (HTML) Store HTML using `quill.root.innerHTML` into database (MySQL/PostgreSQL) and then just Display these HTML

- HTML from users is unsafe. Best way is to store Delta in the database and render it to HTML if needed.

- In case anyone comes across this and finds this useful. You don't need to use innerHTML to render the delta, you can instantiate a new quill object with the settings of readonly and no toolbar
# discuss-news
- ## 

- ## 

- ## 

- ## [Support OT for table _202205](https://github.com/quilljs/quill/pull/3590)
- This adds the OT ability for table format and also supports nested scrolls.

# discuss
- ## 

- ## 

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

- 
- 
- 
- 
- 
- 

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
