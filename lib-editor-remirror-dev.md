---
title: lib-editor-remirror-dev
tags: [editor, lib, prosemirror, remirror]
created: '2021-06-27T19:16:31.417Z'
modified: '2021-06-27T19:16:51.396Z'
---

# lib-editor-remirror-dev

# guide

- Features
  - A11y focused and ARIA compatible.
  - I18n support via lingui.
  - Collaborative editing with yjs.
  - 30+ extensions for creating fully customized editing experiences.
  - Zero configuration support for Server Side Rendering (SSR).
  - Cross platform and cross-framework, with an Angular solution coming later this year.
# discuss
- ## Relation between schema definition and extensions_202003
- https://github.com/remirror/remirror/discussions/272
- I've discovered this project while researching the different options for ProseMirror/React bridges. 
- While researching the code base, however, I noticed that one of the conclusions I drew (design rules that I extrapolated from my research so far) would be violated if I was to build my editor on top of Remirror.
  - Namely: The extension system is tightly coupling the schema definition to the behavior of the editor.
- I believe that any kind of ProseMirror Schema definition should be of purely semantic nature and not be tied to the interactive behavior of the editor at all.
- I think the main motivation for coupling the schema with the editor was to reduce the need for a deep prosemirror understanding when getting started.
  - However with the next version of this API the issues raised can be addressed. 
  - I think there's space for providing an optional way of predeclaring the schema that will be used. 

- ## remirror Next_202003
- https://github.com/remirror/remirror/issues/255
- Originally, remirror was built as a fun side project: a challenge to myself to see if I could create an extensible editor for React.
- It was inspired by the implementations of slate, draftjs, tiptap and @atlaskit/editor. 
- I hoped to create something with great performance, excellent built in plugins, and popular prebuilt editors for easier consumption.
- New design principles
  - Make it feel like React
  - Treat TypeScript as a first class citizen
  - Avoid magic
  - Keep the API namespace small.
- Without classes every part of the object that can be configured needs to be assigned a generic parameter. 
  - I had started with this approach, but once I reached 7 generic parameters I realised it was becoming unmanageable.
  - With TypeScript classes are types. This means that the class can have properties inferred at any time after declaration. Objects and functions don't have that luxury. The type must be declared upfront.
- Styling is now available via, CSS, emotion, styled-components and pure dom manipulation. You can choose which you prefer based on your project.
- There are no plans to change the data structure of the schema or json object. Changes to specific extensions may update attributes which may cause issues.
# docs

## overview

- remirror was started as a personal challenge. 
  - Would it be possible to build an editor that combined great performance with ease of use? 
  - It was also important to give users of all frameworks, the ability to build an editor by picking and choosing their desired building blocks.
- ProseMirror was picked as the best choice for the core editor layer.
- The second decision was to base the structure of the editor on blocks of functionality called `Extensions`. 
  - Each extension would be designed to fulfil a specific purpose in the editor. 
  - Due to this structure, users would be able to craft a fully custom implementation.
- Every single part of the editor is controlled by extensions. 
- Multi-framework support is being added in the future. Currently the focus is on React and the DOM.
