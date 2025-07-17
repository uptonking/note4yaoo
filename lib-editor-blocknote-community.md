---
title: lib-editor-blocknote-community
tags: [blocknote, community, notion-like]
created: 2022-10-21T21:03:04.684Z
modified: 2022-10-21T21:03:38.124Z
---

# lib-editor-blocknote-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## poc: Blocknote lexical_202210
- https://github.com/YousefED/BlockNote/pull/45
  - [Decoupling plugin and nodes · Issue #1262 · facebook/lexical](https://github.com/facebook/lexical/issues/1262)
- This PR is a PoC of an implementation of BlockNote on top of Lexical
- We're currently investigating the structure of "nested" blocks. 
- In editors like Notion and also in BlockNote ProseMirror, indented blocks are considered children of their parent blocks. 
- This has some advantages:
  - makes it possible to create container elements such as "toggles" or "callouts", while allowing rich children
  - easier to work with drag and drop (dragging a parent node also drags the contents)
  - in general; it makes tabs/indents part of the structure of the document, instead of purely a UI aspect. With this, editing a block-based document feels more like editing a coherent(有条理的，表达能力强的) structure instead of a freeform document (like word/google docs)
- I think there are two ways to go about this

- 👉🏻 Extended schema
- Make all core nodes (paragraph, quote, heading, etc.) `block` types, which contain `content` and an optional `childgroup`, that represent nested items. This is how BlockNote currently works 
- Pros:
  - this worked ok for prosemirror
  - "schema" is close to the DOM structure that we'd like
- Cons:
  - It doesn't seem clean. 
    - We introduce a lot of extra structure in the schema (editor state), only to achieve the concept of children. 
    - Instead of designing it so that "a paragraph can have children", we are now saying "a paragraph is represented as a block, with a paragraph as a child"; i.e.: extra level of complexity
  - All core nodes are now represented as a block. This will probably break compatibility with other Lexical plugins in the future
  - It's going to be confusing for developers, as it differs significantly with how Lexical normally works (this is feedback we got on our PM implementation as well)

```jsx
 <block type="heading">
   <content>
     <h1><text>Parent element 1</text></h1>
   </content>
   <childgroup>
     <block type="paragraph">
       <content>
         <p><text>Nested / child / indented item</text></p>
       </content>
     </block>
   </childgroup>
 </block>
```

- 👉🏻 Clean schema
- Alternatively, (which is what we do in this PR) we can try to keep the schema / structure cleaner
- Pros:
  - cleaner schema
  - We keep more semantic node types, hopefully easier to work with other plugins in the future
- Cons:
  - We have to modify/extend nodes to add a "childgroup"
  - We need to modify how the elements are rendered in the DOM. The DOM schema that we like is closer to "Extended schema" mentioned above (i.e.: we want a root div with the h1 and childgroup as children, instead of having the childgroup inside the DOM `<h1>`).

```jsx
<h1>
  <text>Parent element 1</text>
  <childgroup>
    <p><text>Nested / child / indented item</text></p>
  </childgroup>
</h1>
```
