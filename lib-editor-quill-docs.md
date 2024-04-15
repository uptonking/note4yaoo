---
title: lib-editor-quill-docs
tags: [docs, quill]
created: 2023-02-09T18:23:49.039Z
modified: 2023-02-09T18:24:06.718Z
---

# lib-editor-quill-docs

# guide
- delta
  - 内容元素: block, inline-text, inline-non-text
  - 更新操作: insert, delete, retain, format
# docs
- By default all formats defined by Quill are supported in the editor contents through a shared registry between editor instances.

- Quill supports a number of formats, both in UI controls and API calls.

- Modules allow Quill's behavior and functionality to be customized. 
  - To enable a module, simply include it in Quill's configuration
  - The Clipboard, Keyboard, and History modules are required by Quill and do not need to be included explicitly
- Modules may also be extended and re-registered, replacing the original module.

- Registries allow multiple editors with different formats to coexist on the same page.
  - If you register a format with `Quill.register()`, the format will be registered to a global registry, which will be used by all Quill instances.
  - const quill = new Quill('#editor', { registry})

- A custom registry doesn't come with any formats by default. You should register the formats that you need with registry.register().
  - The toolbar module doesn't detect whether a format is available or not, so it will always show the buttons. 
  - customize the toolbar

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

# docs-delta

## ⚖️ [Parchment](https://github.com/quilljs/parchment)

- Parchment is Quill's document model. 
- It is a parallel tree structure to the DOM tree, and provides functionality useful for content editors, like Quill. 
- A Parchment tree is made up of Blots, which mirror a DOM node counterpart. 
  - Blots can provide structure, formatting, and/or content. 
- Blots are the basic building blocks of a Parchment document. 
  - Several basic implementations such as Block, Inline, and Embed are provided. 
- Attributors are the alternative, more lightweight, way to represent formats.

## ⚖️ [Delta](https://quilljs.com/docs/delta/)

- Deltas are a simple, yet expressive format that can be used to describe Quill’s contents and changes. 
  - The format is a strict subset of JSON, is human readable
- Deltas represents both documents and changes to documents. 
  - If you think of Deltas as the instructions from going from one document to another, the way Deltas represent a document is by expressing the instructions starting from an empty document.
  - When Deltas are used to describe content, it can be thought of as the content that would be created if the Delta was applied to an empty document.

- Deltas are implemented as a separate standalone library, allowing its use outside of Quill. 
  - It is suitable for Operational Transform and can be used in realtime, Google Docs like applications. 

- For non-text content such as images or formulas, the value of insert key can be an object. 
  - The object should have one key, which will be used to determine its type. 
  - This is the `blotName` if you are building custom content with Parchment. 
  - All embeds have a length of one

- Line Formatting
  - Attributes associated with a newline character describes formatting for that line.
  - All Quill documents must end with a newline character, even if there is no formatting applied to the last line. This way, you will always have a character position to apply line formatting to.

- The delete operation instructs exactly what it implies: delete the next number of characters.
  - Since delete operations do not include what was deleted, a Delta is not reversible.

- A retain operation simply means keep the next number of characters, without modification. 

- Delta's instructions always starts at the beginning of the document. 
  - And because of plain retain operations, we never need to specify an index for a delete or insert operation.

## ⚖️⌛️ [Designing the Delta Format - Quill](https://quilljs.com/guides/designing-the-delta-format/)

- Rich text editors lack a specification to express its own contents.
- Deltas, the specification describing rich text, is designed to be easy to understand and use
- There already is a ubiquitous format to store plain text: the string. 
  - Now if we want to build upon this and describe formatted text
  - Arrays are the only other ordered data type available, so we use an array of objects. 
- Compact
  - we add the constraint that Deltas must be compact. 
  - 无格式的字符需要合并
- Canonical
  - If two Deltas are equal, the content they represent must be equal
  - Programmatically, this allows you to simply deep compare two Deltas to determine if the content they represent is equal.

- Line Formatting
  - Line formats affect the contents of an entire line
  - To solve this, Quill “adds” a newline to all documents and always ends Deltas with “\n”.
- Embedded Content
  - Strings were natural to use for text but we have a lot more options for embeds. 

- Describing Changes
- Delta can describe changes to documents, as well as documents themselves.
  - In fact we can think of documents as the changes we would make to the empty document, to get to the one we are describing. 
  - We call each element in our Delta array an Operation.

- Delete/Insert
  - To describe deleting text, we need to know where and how many characters to delete. 
  - To delete embeds, there needs not be any special treatment, other than to understand the length of an embed. **embeds are all of length one**.
  - One reasonable way to describe a deletion is to explicitly store its index and length.
- Format
  - The special case is when we want to remove formatting. We will use { bold: null }

- Pitfalls(问题（困难），隐患，陷阱)
  - First, we should be clear that an index must refer to its position in the document before any Operations are applied. 
  - Operations must also be strictly ordered to satisfy our canonical constraint. Operations must also be strictly ordered to satisfy our canonical constraint. Ordering by index, then length, and then type is one valid way this can be accomplished.
  - delete ranges cannot overlap. The case against overlapping format ranges is less brief, but it turns out we do not want overlapping formats either.

- Retain
  - Since every character is described, explicit indexes and lengths are no longer necessary.
  - If the last Operation is a retain, we can simply drop it
  - retain is in some ways just a special case of format, { format: 1, attributes: {} }

- Ops
  - At the time of Delta’s inception(开端，创始), it was not possible to sub-class an Array. 
  - For this reason Deltas are expressed as Objects, with a single property `ops` that stores an array of Operations

- Finally, we arrive at the Delta format, as it exists today.
# docs-blog

## 🎯 [Upgrading to 2.0 - Quill Rich Text Editor](https://quilljs.com/guides/upgrading-to-2-0)

- The Quill repository has been rewritten in TypeScript
- SVG icons are now inlined in the source code, eliminating the need to set up loaders for `.svg` files in your bundler.
- `registry` - added to allow multiple editors with different formats to coexist on the same page.
- `scrollingContainer` removed: Quill will now automatically detect the scrollable ancestor
- pasteHTML removed - Deprecated alias to dangerouslyPasteHTML.
- Native keyboard event object is now also passed into handlers.

- All lists use `<ol>` instead of both `<ul>` and `<ol>` allowing better nesting between the two.
- Attributors are exported as top-level classes.

- delta
  - Support for the deprecated delta format, where embeds had integer values and list attributes had different keys, is now removed

- 
- 
- 
- 

## [Why Quill - Quill Rich Text Editor](https://quilljs.com/guides/why-quill)

- `<textarea>` provides a native and essential solution to almost any web application. But at some point you may need to add formatting to text input. This is where rich text editors come in

- most rich text editors have no idea what text the user composed. These editors see their content through the same lens a web developer does: the DOM. This presents an impedance mismatch since the DOM is made up of Nodes organized in an unbalanced tree, whereas text is made up of lines, words and characters.
  - There is no DOM API where characters is the unit of measure. 
- Quill was designed for editing and characters in mind, and built its APIs on top of these natural text centric units.
  - All of its core API calls allow arbitrary indexes and lengths for access or modification. 
  - Its event API also reports changes in an intuitive JSON format. No need to parse HTML or diff DOM trees.

- Only some rich text editors can even support simple media like images and videos; almost none can embed a tweet or interactive graph
  - Quill exposes its own document model, a powerful abstraction over the DOM, allowing for extension and customization.

## [How to Customize Quill](https://quilljs.com/guides/how-to-customize-quill)

- Quill was designed with customization and extension in mind.
  - The core is augmented by modules, using the same APIs you have access to.
- In general, common customizations are handled in configurations, user interfaces by Themes and CSS, functionality by modules, and editor contents by Parchment.
- all modules use the same public API exposed to the developer, even interchanging core modules is possible, when necessary.
- Quill uses classes, instead of inline style attributes, when possible, but both are implemented for you to pick and choose.
# more
