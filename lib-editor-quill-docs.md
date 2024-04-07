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

## ⚖️ [Parchment](https://github.com/quilljs/parchment)

- Parchment is Quill's document model. 
- It is a parallel tree structure to the DOM tree, and provides functionality useful for content editors, like Quill. 
- A Parchment tree is made up of Blots, which mirror a DOM node counterpart. 
  - Blots can provide structure, formatting, and/or content. 
- Blots are the basic building blocks of a Parchment document. 
  - Several basic implementations such as Block, Inline, and Embed are provided. 
- Attributors are the alternative, more lightweight, way to represent formats.

## ⚖️ [Delta - Quill Rich Text Editor](https://quilljs.com/docs/delta/)

- Deltas are a simple, yet expressive format that can be used to describe Quill’s contents and changes. 
  - The format is a strict subset of JSON, is human readable
- Deltas represents both documents and changes to documents. 
  - If you think of Deltas as the instructions from going from one document to another, the way Deltas represent a document is by expressing the instructions starting from an empty document.
  - When Deltas are used to describe content, it can be thought of as the content that would be created if the Delta was applied to an empty document.

- It is suitable for Operational Transform and can be used in realtime, Google Docs like applications. 

- Line Formatting
  - Attributes associated with a newline character describes formatting for that line.
- All Quill documents must end with a newline character, even if there is no formatting applied to the last line. This way, you will always have a character position to apply line formatting to.

- A retain operation simply means keep the next number of characters, without modification. 

## ⚖️💡 [Designing the Delta Format - Quill](https://quilljs.com/guides/designing-the-delta-format/)

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
  - If the last Operation is a retain we can simply drop it, for it simply instructs to “do nothing to the rest of the document”.
  - retain is in some ways just a special case of format, { format: 1, attributes: {} }

- Ops
  - At the time of Delta’s inception(开端，创始), it was not possible to sub-class an Array. 
  - For this reason Deltas are expressed as Objects, with a single property `ops` that stores an array of Operations
# more
