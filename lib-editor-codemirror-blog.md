---
title: lib-editor-codemirror-blog
tags: [blog, codemirror]
created: 2024-05-02T02:00:52.507Z
modified: 2024-05-02T02:01:04.255Z
---

# lib-editor-codemirror-blog

# guide

# blogs-internals

## 👷 [Facets as Composable Extension Points _202206](https://marijnhaverbeke.nl/blog/facets.html)

- A good extensible system also makes sure multiple extensions that don't know anything about each other can be combined, and compose in ways that don't cause problems.
- The problem has several aspects.
  - Composition, Precedence, Grouping, Change

- A facet, in this system, defines an extension point. It takes any number of input values and produces an output value. 
- Examples of facets are
  - Event handlers, configuration, 
  - The set of markers to style the content with, 
  - The set of gutters to show next to the content
- Facets are defined as values and (optionally) exported so that third-party code can provide inputs. 
  - The core system defines a number of facets, but facets defined outside it work exactly the same as those defined by the core.

## 👷 [(Re-) Implementing A Syntax-Highlighting Editor in JavaScript _201111](https://codemirror.net/5/doc/internals.html)

- CodeMirror 1 was heavily reliant on designMode or contentEditable (depending on the browser)
  - Neither of these are well specified (HTML5 tries to specify their basics), and, more importantly, they tend to be one of the more obscure and buggy areas of browser functionality
- What CodeMirror 2 does is try to sidestep most of the hairy hacks 
  - I absolutely did not want to be completely reliant on key events to generate my input.
  - Some people (most awesomely Mihai Bazon with Ymacs) have been able to build more or less functioning editors by directly reading key events, but it takes a lot of work (the kind of never-ending, fragile work I described earlier), and will never be able to properly support things like multi-keystoke international character input.
  - 👉🏻 So what I do is focus a hidden textarea, and let the browser believe that the user is typing into that. What we show to the user is a DOM structure we built to represent his document. If this is updated quickly enough, and shows some kind of believable cursor, it feels like a real text-input control.
  - Another big win is that this DOM representation does not have to span the whole document. 
- ACE uses its hidden textarea only as a text input shim, and does all cursor movement and things like text deletion itself by directly handling key events. 
- CodeMirror's way is to let the browser do its thing as much as possible, and not, for example, define its own set of key bindings. 
  - One way to do this would have been to have the whole document inside the hidden textarea, and after each key event update the display DOM to reflect what's in that textarea.
- That'd be simple, but it is not realistic. For even medium-sized document the editor would be constantly munging huge strings, and get terribly slow. 
  - 👉🏻 What CodeMirror 2 does is put the current selection, along with an extra line on the top and on the bottom, into the textarea.
- 201111 Recently, I've made some changes to the codebase that cause some of the text above to no longer be current. I've left the text intact, but added markers at the passages that are now inaccurate. 

- The original implementation of CodeMirror 2 represented the document as a flat array of line objects.
  - However, I recently added line wrapping and code folding (line collapsing, basically). Once lines start taking up a non-constant amount of vertical space, looking up a line by vertical position (which is needed when someone clicks the document, and to determine the visible part of the document during scrolling) can only be done with a linear scan through the whole array, summing up line heights as you go. Seeing how I've been going out of my way to make big documents fast, this is not acceptable.
- The new representation is based on a B-tree. The leaves of the tree contain arrays of line objects, with a fixed minimum and maximum size, and the non-leaf nodes simply hold arrays of child nodes. 
  - Each node stores both the amount of lines that live below them and the vertical space taken up by these lines. 
  - This allows the tree to be indexed both by line number and by vertical position, and all access has logarithmic complexity in relation to the document size.
- I chose B-trees, not regular binary trees, mostly because they allow for very fast bulk insertions and deletions. 

- The hidden textarea now only holds the current selection, with no extra characters around it. This has a nice advantage: polling for input becomes much, much faster
  - The reason that cheap polling is important is that many browsers do not fire useful events on IME (input method engine) input, which is the thing where people inputting a language like Japanese or Chinese use multiple keystrokes to create a character or sequence of characters. 
  - Most modern browsers fire input when the composing is finished, but many don't fire anything when the character is updated during composition. 
  - So we poll, whenever the editor is focused, to provide immediate updates of the display.

## [codemirror源码阅读：history相关 | Marvin's Blog【程式人生】 _202209](https://marvinsblog.net/post/2022-09-07-codemirror-src-history/)

- 定义了一个annotation：fromHistory，值为{side: BranchName, rest: Branch}
  - BranchName是redo、undo二选一，Branch是历史事件合集
# blogs-lsp

## 🌰 [Bringing the TypeScript Language Server to Observable | Observable _202211](https://observablehq.com/blog/bringing-the-typescript-language-server-to-observable)

- We represent each cell in a notebook as a separate file in the VFS, and keep the TypeScript virtual environment in sync with changes made in the CodeMirror cell editors. 
  - Then, we can query the language service for signature help and autocompletions at any position in the CodeMirror editor. 
- Next, we moved the virtual TypeScript environment to a WebWorker. 

- 
- 
- 

## [Connecting ANTLR to CodeMirror 6: Building a Language Server _202402](https://thetrevorharmon.com/blog/connecting-antlr-to-codemirror-6-building-a-language-server/)

- For the past couple of years, I’ve worked on ShopifyQL Notebooks, a data exploration tool offered by Shopify.
  - The tool enables Shopify merchants to query their data in a Jupiter-esque notebook using ShopifyQL
  - One of the biggest challenges in creating ShopifyQL Notebooks was building a functional code editor with all of the bells and whistles you’d expect from a world class editor.
- The primary way to use Lezer is to use its grammar engine. 
- Lezer takes in a grammar file and then exports extensions that CodeMirror uses to create parse trees. Those parse trees are then used by CodeMirror to provide various features like syntax highlighting, linting, tooltips, etc.
- 
- 

### https://thetrevorharmon.com/blog/connecting-antlr-to-code-mirror-6-connecting-a-language-server/

- 
- 

# blogs-xp

## 🌰 [My CodeMirror snippets - HackMD _202410](https://hackmd.io/@q/codemirror-snippets)

- A draggable gutter extension to allow selecting lines by dragging on the line gutter.

- (Concept only) A proposal on indented-wrapped line appearence ported from CM5.

- 
- 
- 

## 🧑‍🏫 [Advanced state management with React and CodeMirror _202403](https://thetrevorharmon.com/blog/advanced-state-management-with-react-and-codemirror/)

- https://thetrevorharmon.com/blog/codemirror-and-react/

## 🧑‍🏫 [Learning CodeMirror _202309](https://thetrevorharmon.com/blog/learning-codemirror/)

## [浅尝 CodeMirror@6 – 山维空间 _202203](https://blog.meathill.com/js/note-codemirror6.html)

- CodeMirror@6 是作者完全重写的，整体架构发生了非常大的变化，使用方式与上一个版本完全不同。
  - 以前创建编辑器只需要 codemirror.fromTextarea(element) 即可，现在麻烦了很多
- 新版本为了支持编辑代码的复杂需求，把所有变更都封装成了 transactions，通过 dispatch 告知 view 更新视图。所以修改代码就从 .setValue(code) 变成下面这种样子 this.editor.dispatch({ changes: { from: 0, to: this.editor.state.doc.length, insert: code }, }); 
- 新版本高亮错误代码会比较麻烦。以前直接 .addLineClass() 就可以了，现在则要先生成标记，然后再把标记添加到视图中。

## [Creating an Editable Textarea That Supports Syntax-Highlighted Code | CSS-Tricks _202104](https://css-tricks.com/creating-an-editable-textarea-that-supports-syntax-highlighted-code/)

- 与codemirror无关

## [(PrismJS || HighlightJS || CodeMirror 6) + CodeDetectionAPI _202203](https://tsavo.medium.com/prismjs-highlightjs-codemirror-6-codedetectionapi-%EF%B8%8F-af99dc13d83b)

- In search of a solution, HighlightJS stood out — it has Automatic Language Detection and Multi-Language Code Highlighting. That’s perfect, right!?
  - Problem 1: You still need to know if the user input is code / technical language vs plain text / natural language. (This turns out to be quite difficult to solve, but there’s a solution below.)
  - Problem 2: If it’s code, you need to know what language it is, and then, of course, syntax highlight it!
  - HighlightJS does not solve Problem 1, and for Problem 2, HighlightJS can attempt to determine the coding language but at an expensive network and compute cost.
- Given HighlightJS’s limitations, my team at Pieces built and published the `CodeDetectionAPI` to solve Problems 1 and 2 in our app with machine learning while achieving optimal network and compute performance.
# more
- https://dev.to/thinkthroo/execa-vs-using-childprocess-to-execute-cli-commands-programmatically-1mjm

- [CodeMirror Accessible](https://bgrins.github.io/codemirror-accessible/)

- [Interactive Code Editor Tutorial: Managing Dynamic Content with react-codemirror - DEV Community _202410](https://dev.to/mrsupercraft/interactive-code-editor-tutorial-managing-dynamic-content-with-react-codemirror-3i7g)
- [How to make a code editor with CodeMirror 6 _202106](https://www.raresportan.com/how-to-make-a-code-editor-with-codemirror6/)

- [Revisiting our CodeMirror 6 implementation in React after the official release _202210](https://www.codiga.io/blog/revisiting-codemirror-6-react-implementation/)
  - [Implementing CodeMirror 6 in React with Code Snippets Autocompletion _202205](https://codiga.io/blog/implement-codemirror-6-in-react/)

- [How to create Zenn's Markdown editor with CodeMirror v6 _202402](https://zenn.dev/team_zenn/articles/zenn-markdown-editor-by-cm6)

- [CodeMirror Search | by Evin Owen | Medium _202311](https://evinowen.medium.com/codemirror-search-84bc73b1b1ee)
  - [CodeMirror Decorations — Underline Example | by Evin Owen | Medium](https://evinowen.medium.com/codemirror-decorations-underline-example-dafd4ca4bda6)

- [富文本编辑器：TinyMCE、Editor.js、Lexical、CKEditor与CodeMirror对比 - ercwang](https://0x763ad28bc4436590fd61998561730b0f7790e955.xlog.app/TinyMCEEditorjsLexicalCKEditorCodeMirror)
