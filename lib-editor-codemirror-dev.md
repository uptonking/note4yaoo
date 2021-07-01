---
title: lib-editor-codemirror-dev
tags: [codemirror, lib, text-editor]
created: '2021-05-06T09:37:37.030Z'
modified: '2021-05-06T09:38:31.520Z'
---

# lib-editor-codemirror-dev

# guide

# docs

# [styling](https://codemirror.net/6/examples/styling/)

- CodeMirror uses a CSS-in-JS system to be able to include its styles directly in the script files. 
  - This means you don't have to include a library CSS file in your page for the editor to work—both the editor view's own styling and any styling defined for dependencies are automatically pulled in through the JavaScript module system.
- Themes are simply extensions that tell the editor to mount an additional style module and add the (generated) class name that enables those styles to its outer DOM element.
# roadmap

## [CodeMirror 6 Status Update_201908](https://marijnhaverbeke.nl/blog/codemirror-6-progress.html)

- It has been almost a year since we officially announced the CodeMirror 6 project, which aims to rewrite CodeMirror (a code editor for in the browser) to align its design with the technological realities and fashions of the late 2010s.
- we integrate a new approach to code parsing.
- we finished a doc comment extractor for TypeScript
- I'm definitely suffering from second system syndrome, where after eight years with the old system, I am acutely aware of its limitations and want to fix them all this time around. 
  - That sometimes leads me into overly-ambitious design rabbit holes, and then it takes me a week or two to dig myself out again.
- Composition Support
  - Handling composition/IME (input method editor) in the browser is its own special kind of hell.
- Behaviors as Extension Primitive
  - A design where a generic core provides a platform for all kinds of features to be implemented in plugins has to, in a way, provide an extendable extension mechanism
  - I think we landed on a nice architecture. 
- CSS Modules
  - Since the browser platform's CSS support is still more or less completely unhelpful when it comes to modularized system, we've decided to use a CSS-in-JS approach where extensions can define their own styles from within JavaScript code and make sure they are included in the document or shadow DOM where the editor is placed.
- View Fields and Updates
  - I've added a new abstraction, view fields, for pieces of state that live in the view and affect things like decorations (styling and widgets in the content) and the attributes of the editor's wrapper DOM nodes.
- Block Widgets
  - Block widgets are a way to insert a block element into the document, either on a line boundary, in the middle of a line, or covering some content.
- Generic Gutters
- Doc Generation
- Lezer
  - tree-sitter, which is a practical implementation of an incremental LR parser, giving you a real syntax tree for your code and updating it cheaply when you make changes. It is used in the Atom editor.
  - I set out to clone tree-sitter in JavaScript. I didn't exactly clone it, but rather built a different system inspired by it. 
  - That system is Lezer, an incremental parser generator and runtime system for JavaScript.
# discuss
- ## 

- ## 

- ## 

- ## Meta: Observable editor in observable
- https://talk.observablehq.com/t/meta-observable-editor-in-observable/2376
  - One thing that I would like to do is to create a view with a nice text editor (ideally the same as the one used in observable) where users of my notebook can write some code with another linter (e.g. python) 
- Observable’s editor is based on CodeMirror. There’s a nice and simple example of CodeMirror in this notebook
- [CodeMirror inside of Observable](https://observablehq.com/@tmcw/codemirror-inside-of-observable)
  - We use CodeMirror to power a lot of the editing abilities of Observable, but we can also embed CodeMirror inside of a notebook to provide an in-notebook editing experience.

- ## codemirror 6 
- https://news.ycombinator.com/item?id=26039111
- One of the things I was hoping to see in this release was first-class LSP (language server protocol) support.
  - Sorbet (Ruby type checker) implements the LSP protocol and can be compiled to WASM
  - I'm especially excited to see mobile support as a headline feature, because that's completely lacking in Monaco. 
  - Maybe LSP support can be a future improvement.
- There's still no way to use create-react-app with monaco out of the box with offline support (@monaco-editor/react includes calls to a CDN instead of using the bundled JS).

- ## codemirror6: Decide how to distribute/manage CSS_201812
- https://github.com/codemirror/codemirror.next/issues/40
- Connecting modules to the CSS they rely on doesn't seem to be a solved problem in the JS ecosystem yet. Our plugins will often need a few lines of CSS to work. Requiring people to manually add `<link>` tags for each of those (which come from NPM and are probably not even in their web root by default) is a poor user experience.
  - I'm also not partial to schemes that inject the CSS into the page at run-time. When users are optimizing their page, they'd prefer to have control over how and when CSS is loaded, and not have that done at unpredictable moments by a script.
  - Who knows any existing approaches that we could take inspiration from?
- making it easy to write themes that integrate with the various plugins would be an advantage. 
  - This is one reason current codemirror.css defines all kinds of non-core styles—themes will want to include all of those as well.
- FWIW I took a stab a creating an Ubuntu theme package for CodeMirror 6. It was fun! The biggest difference from CM5 is having to deal with native selections, which can be styled with ::selection.
  - The main suggestion I have after doing this is to more clearly separate the "core" CSS (required for correct layout) vs. "theme" CSS (that sets colors).
  - Regarding distribution, my gut feeling is that well organized plain old CSS would be best.
- Being a packaged component, we have somewhat different requirements than what most CSS-in-JS/CSS modules libraries are written for.
  - I was somewhat attracted to the idea of making all styles inline at first, since it nicely avoids the problem of having to create `<style>` tags and CSS rules at all, but that will often create really ugly DOM, and (more importantly) makes it impossible to support things like pseudo-classes and media queries, so I think we don't want that.
  - The alternative is to provide a way for scripts to generate class names from descriptions, and directly use those class names in the DOM. That doesn't work very well for highly dynamic CSS, but I guess the bulk of our CSS will fit the pattern just fine, and we can fall back to the `style` attribute for the rest.
- I was also working with styled-components for the past few days (I'm making a file tree component with react-virtualized).
  - I dropped CSSinJS at least for this case where performance IS the core component of the thing.
- Functional CSS makes the DOM directly reference the style. This works fine if you're in full control of the website, but a reusable component that wants to allow outside styling can't do that.
- style-module is much like a classical CSS module library, but works with sets of classes, rather than individual classes.
  - https://github.com/marijnh/style-mod
  - The idea behind that is that a plugin would define its styling as a style module containing classes for all the styleable elements it creates, and export that module. 
  - Client code can then extend this module and pass it back to the plugin as part of a configuration. 
  - If all plugins make sure they do this, and use the configured style module (with their own base module as a fallback) when styling, that should help with the overriding problem (without relying on side effects or global scopes).
  - The editor view itself would use a similar mechanism to allow the editor to be themed.

- ## We are rewriting CodeMirror
- https://news.ycombinator.com/item?id=17858672
- Now I use Monaco aka Visual Studio Code. 
  - What would CodeMirror offer ? 
  - With Monaco I get all the lastest feature of VSCode . Current versions of Monaco include Intellisense etc.
  - I'm honestly curious both what CodeMirror will offer and why even try to compete. 
- CodeMirror aims to be slimmer, and less of a cut-off piece of vs code. I also think our API is more well designed and expressive. And, as Adrian mentioned below, though he got downvoted, CodeMirror works on phones
  - The fact that it works on mobile is the biggest advantage imho. We use it for that reason.
- monaco doesn't even try to work on mobile browsers.
