---
title: lib-editor-codemirror-community
tags: [code-editor, codemirror, community]
created: 2023-01-29T10:52:26.160Z
modified: 2023-01-29T10:52:44.183Z
---

# lib-editor-codemirror-community

# guide

# discuss
- ## 

- ## 

- ## [Anyone Explored a Codemirror 6 Canvas/WebGL Renderer? - discuss. CodeMirror](https://discuss.codemirror.net/t/anyone-explored-a-codemirror-6-canvas-webgl-renderer/3779)
- The Bespin 9 project in 2009 worked this way, but was given up due to, I believe, problems with the approach. Some things to keep in mind:
  - In most situations, for text layout, the DOM will be faster than a canvas
  - Accessibility will be terrible if your text is just pixels on a canvas
  - Doing text positioning, styling, and wrapping is a whole lot more difficult with fillText

- I haven’t worked with WebVR—seems like there’s a proposed 8 standard for making it capable of showing regular DOM elements, but nothing actually implemented at the time. I guess as a workaround for that limitation, mirroring a CM instance to a canvas is a more or less reasonable thing to do.

- ## 🆚️ [v6 Comparison with approach of react-simple-code-editor _201907](https://github.com/codemirror/dev/issues/109)
- react-simple-code-editor: works by allowing users to edit inside a native `textarea` , while overlaying syntax-highlighted code on top of it. On the face of it this seems like quite an elegant and simple approach that works well.

- I find myself wondering what makes the more complex approach taken by CodeMirror superior to that approach, which seems so simple by comparison.
- I can only think of the following drawbacks to the approach taken by react-simple-code-editor:
  - Syntax highlight requires a complete parse on each keystroke. This could be addressed by using `tree-sitter` or `lezer` for maintaing the AST.
  - The syntax-highlighted DOM tree is clobbered and regenerated on each keystroke. This could be addressed by using virtual DOM to update the DOM based on the fresh AST (e.g. using preact or react).
  - Really large files would render in full with this approach, whereas CodeMirror only renders what's visible.
- The above problems can be ignored for use cases where the files will not be large, or syntax highlighting is not required when the amount of text is above a certain threshold.
  - I'm posting this issue as a sanity check, to see if I'm missing some important points that make the complex update patterns within CodeMirror inherently a better choice than the approach taken by react-simple-code-editor. 

- This isn't a new idea—it was also the approach used by Editarea, the only halfway serious predecessor of CodeMirror.
  - Can't use anything but single-font single-style text inside the editor or the characters get misaligned.
  - Reading from a textarea is all-or-nothing, so when the document is big, even if you manage to do incremental highlighting, you have to read the entire string and then diff it against the previous value, which is expensive. (Have you tried pasting a big document into their demo? It becomes unusable.)
- In short, most of the features that CodeMirror provides couldn't be built on top of this approach, and forget about scalability. A component like this is perfectly appropriate if you know your snippets are going to be small and you don't need much extra functionality, but doesn't scale beyond that.

- FWIW I came across this video that I found very informative, regarding why CodeMirror operates the way it does: YouTube: Marijn Haverbeke - Grammar-based language modes for text editors. I'm beginning to grok that by comparison, the approach taken by react-simple-code-editor is extremely crude and wasteful of compute resources.
  - Note that the system I describe there never made it into mainstream CodeMirror (though you can use it if you install it separately), and lezer is a new, different approach.

- 🆚️🤔 Actually one of my main questions about Lezer is why not just use tree-sitter, which appears to do the same thing more or less. That could be a good point to address on the Lezer home page (which surprisingly doesn't mention tree-sitter), as many people will probably be wondering the same thing when they discover the project. The point is partially addressed in the README here lezer-parser/lezer , but it requires a lot of the reader to figure out exactly what Lezer has or does, that tree-sitter doesn't.

- ## 🆚️ Does anybody need a new code editor for the web that's 2x faster than Monaco, 10x smaller than CodeMirror, and works well on mobile?
- https://twitter.com/fabiospampinato/status/1618807374973911046
  - I'm syntax highlighting with the CSS Custom Highlight API, which hasn't shipped elsewhere yet. 

- highlight.js supports rendering to string plugins (the library “marked” uses it) but lacks the line numbers for it
  - I think Highlight.js isn't appropriate for this use case, it doesn't support tokenizing incrementally so it would block the main thread, potentially for multiple seconds for large files, and it doesn't support TextMate grammars, so the syntax highlighting will be sub-par.
- https://copenhagen.autocode.com 1/50 the size of Monaco, with most of the features.
  - It may be the best of its kind that I've seen so far. 
  - Mine uses TextMate grammars so syntax highlighting should be higher quality and smoother. And while scrolling it does ~5x less work (~10x less if we only look at the JS portion). It's  just PoC for now though.
- On a closer inspection Copenhagen seems to weigh 1/9th the size of Monaco (~190kb), not 1/50th. Like the instance of Monaco that I use is ~1.7MB, not ~10MB. And editing doesn't seem to work on mobile for me. Still interesting though.
- What grammar do you end up? tree-sitter? Also, is it canvas2d?
  - I'm using TextMate grammars at the moment, but I want to eventually add support for something else to it, like Monarch grammars, as otherwise it won't be 10x smaller than CM. No canvas, pure DOM.
- Can you use tree sitter for highlighting and ide like features?
  - Maybe in the future, it's very much a work in progress thing right now, currently only a TextMate-based syntax highlighter is supported.
- I think also http://repl.it also was working on something similar.
  - I think they are happy with CodeMirror, which is a fine choice

- ## Meta: Observable editor in observable_201909
- https://talk.observablehq.com/t/meta-observable-editor-in-observable/2376
  - One thing that I would like to do is to create a view with a nice text editor (ideally the same as the one used in observable) where users of my notebook can write some code with another linter (e.g. python) 
- Observable’s editor is based on CodeMirror. There’s a nice and simple example of CodeMirror in this notebook
- [CodeMirror inside of Observable](https://observablehq.com/@tmcw/codemirror-inside-of-observable)
  - We use CodeMirror to power a lot of the editing abilities of Observable, but we can also embed CodeMirror inside of a notebook to provide an in-notebook editing experience.

- ## [codemirror 6 _202102](https://news.ycombinator.com/item?id=26039111)
- One of the things I was hoping to see in this release was first-class LSP (language server protocol) support.
  - Sorbet (Ruby type checker) implements the LSP protocol and can be compiled to WASM
  - I'm especially excited to see mobile support as a headline feature, because that's completely lacking in Monaco. 
  - Maybe LSP support can be a future improvement.
- There's still no way to use create-react-app with monaco out of the box with offline support (@monaco-editor/react includes calls to a CDN instead of using the bundled JS).

- ## codemirror6: Decide how to distribute/manage CSS _201812
- https://github.com/codemirror/codemirror.next/issues/40
- Connecting modules to the CSS they rely on doesn't seem to be a solved problem in the JS ecosystem yet. Our plugins will often need a few lines of CSS to work. Requiring people to manually add `<link>` tags for each of those (which come from NPM and are probably not even in their web root by default) is a poor user experience.
  - I'm also not partial to schemes that inject the CSS into the page at run-time. When users are optimizing their page, they'd prefer to have control over how and when CSS is loaded, and not have that done at unpredictable moments by a script.
  - Who knows any existing approaches that we could take inspiration from?
- making it easy to write themes that integrate with the various plugins would be an advantage. 
  - This is one reason current codemirror.css defines all kinds of non-core styles—themes will want to include all of those as well.
- FWIW I took a stab a creating an Ubuntu theme package for CodeMirror 6. It was fun! 🆚️ The biggest difference from CM5 is having to deal with native selections, which can be styled with `::selection` .
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

- ## We are rewriting CodeMirror _201808
- https://news.ycombinator.com/item?id=17858672
- Now I use Monaco aka Visual Studio Code. 
  - What would CodeMirror offer ? 
  - With Monaco I get all the lastest feature of VSCode . Current versions of Monaco include Intellisense etc.
  - I'm honestly curious both what CodeMirror will offer and why even try to compete. 
- CodeMirror aims to be slimmer, and less of a cut-off piece of vs code. I also think our API is more well designed and expressive. And, as Adrian mentioned below, though he got downvoted, CodeMirror works on phones
  - The fact that it works on mobile is the biggest advantage imho. We use it for that reason.
- monaco doesn't even try to work on mobile browsers.

- ## 🎯 [CodeMirror 6.0 Stable Release | Hacker News _202206](https://news.ycombinator.com/item?id=31666186)
- Why wasn't ProseMirror a fit for Obsidian? Seems like that would be better for structured documents.
  - For a good portion of its users, an important feature of Obsidian is the use of flat Markdown files.
  - I'm inquiring about actual implementation not Markdown. Markdown -> AST -> CodeMirror vs Markdown -> AST -> ProseMirror.

- We're currently integrating CodeMirror 6 into Overleaf, and you can try it out by joining our beta program (which will give the option to select the beta source editor, which is the one built using CM6). 

- CodeMirror is also much more usable on touch devices than Monaco (VS Code’s editor component).
