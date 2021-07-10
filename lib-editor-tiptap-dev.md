---
title: lib-editor-tiptap-dev
tags: [lib, prosemirror, text-editor, tiptap]
created: '2021-05-06T09:45:58.536Z'
modified: '2021-05-06T09:46:30.944Z'
---

# lib-editor-tiptap-dev

# guide

- features
  - headless without any css
  - framework-agnostic
  - realtime collaboration
  - customizable with a ton of extensions
  - typescript

- tiptap-examples
  - dante
  - more: shiki-editor(vue)
# faq-not-yet

# discuss-stars
- ## [Markdown input and output_201810](https://github.com/ueberdosis/tiptap/issues/66)
- [prosemirror official Friendly Markdown example](https://prosemirror.net/examples/markdown/)
  - 支持在markdown和wysiwyg间切换，无外部依赖
- At the moment it's not possible to add this functionality with extensions. That's something I have to add to the core.
- I don’t see us adding this to the core, it’s just too different. So I’m closing this here for now. Consider using CodeMirror, if you really want to work with Markdown.

- ## Comparison to raw ProseMirror, esp. regarding collaboration. 
- https://github.com/ueberdosis/tiptap/discussions/1507
- Everything you can do with ProseMirror, you can also do with tiptap. 
  - The goal of tiptap is to bundle some related logic into extensions (e.g. schema, commands, input rules), and to make some complex APIs more accessible (e.g. chained commands). 
  - We also provide a documentation with many examples and extensions so it’s way easier to start than with plain ProseMirror.
- y.js builds on top of CRDT instead of OT. 
- Anyway, we’re doing a big bet on Y.js. 
  - CRDT are the future, and Y.js is the most performant implementation. 
  - It has a huge ecosystem, and new community projects pop up every week. 
  - If you want to go the OT-way, you can do that with tiptap as you would do it with ProseMirror. 
  - All parts and APIs of ProseMirror are accessible through tiptap.
# discuss
- ## Tiptap 2 beta is here_202104
- https://discuss.prosemirror.net/t/tiptap-2-beta-is-here/3710
  - Commands are chainable. 
  - Support for text align. 
  - Render nodes as react components or vue components
  - Show suggestions for things like mentions 2 or slash commands 
- I’ve been taking a sneak peak at your new API and decided to use a similar approach myself. 
  - Basically just turning PM plugins into React components that have their own props instead of one massive EditorProps object.
- So having dabbled myself mostly with React+PM integration, I’ll ask the basic ones that are on my mind - how do components subscribe to the global editor state? Observables? Also, do you intend to allow the use of some central event message bus, a la Redux?
- by looking into your ReactNodeView - it seems you have avoided the use of ReactDOM completely? No portals nothing?
  - I’m using portals! You can see it in react/src/EditorContent.tsx 
- One thing I’ve been thinking about is how to manage the state fetched from the API. For example collaboration participants
  - We provide first class support with Y.js collab.
  - It’s definitely a PITA to implement with the bare collab module. Yet I’m still a bit ambivalent about Yjs, like is it easy to switch between single and multiplayer editing and how much memory it actually consumes in the server.
  - But what I was getting at that do you implement the API providers as extensions or as separate services. Not a huge difference but something I myself am pondering. I guess having one entity for everything makes things simple.
- Also, I have a tricky question that’s been on my mind. What’s your approach for rolling out breaking schema changes?
  - We do not currently provide anything for this. However, I find it best to migrate the JSON data manually on the server side.
- One thing I’d like to see, for Tiptap and PM in general, is good testing support with jsdom. Seems pretty important considering how complicated the editors can get.
  - I haven’t had good experiences with JSDOM, so we run all tests with Cypress. Works great! 
- What do you mean by global editor state? State from the editor or from your react app?
  - Yeah I meant the whole app: editor plugin state, extension state, UI state, API state and so forth. It seems that to manage the whole thing you need message passing of some sorts, which you seem to provide as well with editor pub/sub events, but I was wondering if you had some interesting new angle to it.
- Well in theory that’s all you need and useContext does work for providing state but. React doesn’t have as nice built-in state management as Vue and useContext can get quite tedious to work with. Moreover, the nature of PM’s event loop combined with the handling collaboration events and whatnot does seem the steer the whole architecture towards more event-based state management.
  - As one example let’s consider updating a component based on a plugin state change. So the simplest way is to make one context that has the editorState which you can replace in the dispatchTransaction call. 
  - Yet the component would update on every transaction and you’d have to check inside the component to see if the plugin state has changed. 
  - So you want to slice the state to make the updates as minimal as possible but it’s not very convenient with pure useContext. 
  - I myself made some hacky pub/sub pattern where I trigger a provider in the plugin’s apply function whenever plugin state changes but I definitely have to refactor it when I have the time. 
  - Curvenote put everything into Redux which seems nice but I don’t want to deal with its boilerplate.
  - To be frank it may be even impossible to add in a similar state management into an editor framework versus making your custom editor. So it’s a bit tricky.
- Why would the component update on every transaction. I was able to create a very simple hook for https://bangle.dev that reads a plugin state, it is working great for me and doesn’t utilize the event pub sub pattern.
  - Because EditorState is recreated on every transaction thus it would always update if the component was subscribed to changes to it. 
  - From what I can tell from your code, you are doing precisely what I said you have to do which is to slice the state somehow to the components. 
  - And sure, you’re not using pub/sub per say although one could think of editor transactions that change the plugin state as published events. 
  - But any state that would not be inside plugin state and still be relevant, eg API/UI stuff, you would have to engineer your own method of triggering changes somehow and relaying them forward.
  - Using React context for that purpose sucks.
# examples-repos
- dante3 /1.5kStar/MIT/202106/js
  - https://github.com/michelson/Dante
  - https://www.dante-editor.dev/
  - 依赖 emotion、polished、react-json-view、yjs
  - Just another medium clone built on top of ProseMirror/TipTap
  - Dante3(tiptap2): a Tiptap port of Dante2
  - Dante2(draftjs): Bad mobile support, big size(immutablejs), no realtime collab
  - Dante1(vanillajs): rely a lot on DOM manipulation

- wix-tiptap-editor
  - https://github.com/wix/ricos
  - https://ricos.js.org/docs/ricos/ricos-intro
  - A React-based rich content editor with an extensible plugin system
  - wix公司开源了自己的内容编辑器，公开了自己的json schema规范，提供了wix-rich-content-editor、wix-rich-content-viewer
  - 还支持在基于tiptap v2的编辑器中编辑内容，提供了draftToTiptap()转换方法，将ricos-draft的json格式转换成tiptap支持的json格式
  - 内部插件大多严重依赖自研ui库和基础库，如wix-rich-content-ui-components、ricos-content

- @sensenet/editor-react
  - https://github.com/SenseNet/sn-client
  - Text editor library behind rich text editor is changed to tiptap@2.0
  - As a first step only those text editing features are implemented
  - More new things (managing tables, embedding, etc.) are coming in the following releases.

- https://github.com/primo-af/primo
  - https://primo.af/
  - /76Star/AGPLv3/202106/svelte
  - an all-in-one ide, cms, component library, and static site generator
  - a next-gen, dev-friendly alternative to WordPress.
- https://github.com/shikimori/shiki-editor /vue
  - a wysiwyg editor based on prosemirror
  - highly inspired by tiptap source code. Many parts of the code are taken from there.
