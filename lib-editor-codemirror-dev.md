---
title: lib-editor-codemirror-dev
tags: [codemirror, lib, text-editor]
created: 2021-05-06T09:37:37.030Z
modified: 2021-05-06T09:38:31.520Z
---

# lib-editor-codemirror-dev

# guide

- who is using #codemirror6
  - observable-notebook

- dev-xp
  - 在github页面，每行代码的行号是确定的，不会显示软换行
    - 方便实现高亮搜索结果、查找引用
  - 协作示例官方使用ot，社区有使用crdt如yjs

- 区分codemirror是v5和v6的方法
  - 👉🏻 cm6的默认css，样式名小写
    - .cm-editor
    - .cm-gutters
    - .cm-content
      - .cm-line
      - .cm-activeLine
    - .cm-layer.cm-selectionLayer
  - 👉🏻 cm5的默认css
    - .CodeMirror-lines
    - .CodeMirror-cursors
    - .CodeMirror-code
      - .CodeMirror-gutter-wrapper
      - .CodeMirror-line 
    - .CodeMirror-gutters

- resources
  - [Ace, CodeMirror, and Monaco: A Comparison of the Code Editors You Use in the Browser__202112](https://blog.replit.com/code-editors)
# examples
- https://github.com/MyoniM/mirror-code-react-js
  - https://mirror-code.web.app/
  - A collaborative Web IDE with Code Mirror's CRDT Server and Socket.io
# docs

# blogs

- [CodeMirror Accessible](https://bgrins.github.io/codemirror-accessible/)

## [(Re-) Implementing A Syntax-Highlighting Editor in JavaScript_201111](https://codemirror.net/5/doc/internals.html)

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

## [styling](https://codemirror.net/6/examples/styling/)

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
