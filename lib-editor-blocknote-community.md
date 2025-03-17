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

- ## 🚀 [Docs – Open source alternative to Notion or Outline | Hacker News _202503](https://news.ycombinator.com/item?id=43378239)

- https://x.com/YousefED/status/1901367050435465362
  - The open source and collaborative document editor we're building with the French and German governments just hit the top of HN. _202503
  - Really wish there is a proper browser based Notion Alternative but with the Obsidian Editing Experience (Liveview). All those Notion like Block Editors really struggle with copy/paste the content imo, especially when using it with LLMs.

- The hard part in a project like Docs is the text editor. We built Docs on top of [Blocknotejs]

- What led to the choice of using Blocknote over other editor packages? 
  - We've built BlockNote to come "batteries-included" with common UI components and a simpler API to make it easy for you to add a modern, block-based editor to your app.
  - The BlockNotejs team researched the live editing space thoroughly so we could just follow the tracks: BlockNotejs, HocusPocus, Yjs. We "just" had to build the wrapper around with authentication, docs permissions and search and boom you have Docs!

- Does this provide database functionality like seen in Notion?
  - The database of La Suite is `Grist`.

- Did you consider building on top of some existing open source solutions like Docmost, Appflowy, or AFFiNE?
  - we dedided to take an approach where we build on top of libraries like BlockNotejs, Yjs, HocusPocus but build our own wrapper around it in Django and Next.js. This allows to iterate really fast and to catter our own need (we are large organizations we don't have the same as startups or SMEs).

- Tchap looks neat as a Slack alternative, but it seems like it's still only for government workers.
  - Tchap is just Element/Matrix with some gov specific features.

- Honestly it's a reasonable set of dependencies:
  * Postgres for permanent storage
  * an OIDC identity provider so you don't have to make your own password system
  * Redis for caching
  * S3-compatible object storage (so you don't have to reinvent file uploads)
  * The app itself

- Have you tried TriliumNext? It doesn't have collaboration for editing but sharing is built in, It lets you structure your notes in a way that's reminiscent of object oriented programming (you've got templates to define types, inheritance of attributes to instantiate and specialize them, etc). I have hierarchies of hundreds/thousands of notes that for all intent and purposes are as good as Notion's Databases

- This is a really great project from both the French and German governments.
  - I think state-funded open source solutions to digital platforms is a fantastic opportunity to get away from the big tech walled gardens. 
  - Of course, there is always the risk that this becomes unmaintained in the future, but the community at least can take over.

- Notion has a very flexible data model. We use it mainly for documents, but it also can contain databases, which can be viewed as kanban boards, timelines, etc.
  - It's really nice to have one place to go for all kinds of content, but that content can link within itself, @mention other pieces of content, etc.

- Evernote had the best mechanism, giving you an XML file and an official XSLT to read/verify/transform what they give you. However, Evernote feels very underpowered when you start to use formulae and automation across your database.

- please name some open source (or lower priced) alternatives that support: comments on documents, database functionality to a similar level, publishing websites, scripting for properties. I'm very curious!
  - I was going to say git, but really you need the whole environment.

- 
- 
- 
- 
- 
- 
- 
- 

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

```HTML
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

```HTML
<h1>
  <text>Parent element 1</text>
  <childgroup>
    <p><text>Nested / child / indented item</text></p>
  </childgroup>
</h1>
```
