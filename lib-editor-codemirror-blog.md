---
title: lib-editor-codemirror-blog
tags: [blog, codemirror]
created: 2024-05-02T02:00:52.507Z
modified: 2024-05-02T02:01:04.255Z
---

# lib-editor-codemirror-blog

# guide

# blogs

## [(Re-) Implementing A Syntax-Highlighting Editor in JavaScript _201111](https://codemirror.net/5/doc/internals.html)

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
# blogs-vendors

## 

## 

## 

## [Replit — Betting on CodeMirror _202203](https://blog.replit.com/codemirror)

- Monaco did not support mobile, which was becoming increasingly important for us to achieve our goal of making programming more accessible.
  - Overall, we’re excited to be placing such a huge bet on the next generation of online code editors and continuing to advance the future of writing software on the web. 

## [Why we developed a code block widget in Miro _202307](https://medium.com/miro-engineering/why-we-developed-a-code-block-widget-in-miro-f6c5ec23085c)

- Our code widget is a code block with a rich editing experience comparable to a native code editor. It has features like syntax highlighting, auto-closing brackets and indentations, various hotkeys, and more.
- Miro boards are heavily based on Canvas API. 
  - Almost everything visible on the board, except for the user interface on top of the board, is essentially a continuously updated and re-rendered image. 
  - Our custom rendering engine consumes HTML with inline styles and draws text by using `canvasContext2D` API.
- Option 1: Reuse existing approach — Quill Editor
  - It is well-integrated in Miro and has a native plugin for syntax highlighting that uses the highlightjs
  - Highlight.js, which Quill uses for syntax highlighting, isn’t the best library available
- Option 2: Use HTML elements and syntax highlighting libraries
  - By using various approaches based on HTML elements like this one using textarea and highlightjs/prismjs, we can make editable code blocks with real-time syntax highlightiing
  - By using various approaches based on HTML elements like this one using textarea and highlightjs/prismjs, we can make editable code blocks with real-time syntax highlightiing
- Option 3: Integrate a web-based code editor
  - we used the web-based code editor CodeMirror. 
  - we can highlight the heavy weight of the editor, which may result in a longer load time. 
- In the end, we wanted to provide as smooth and rich of an editing experience as possible. We also wanted to future-proof our editor in case we want to support longer text (more than 6000 characters) and extend functionality, such as implementing collaboration or code execution.
  - Considering that both Quill and HTML elements didn’t fully meet our functional requirements, we chose instead to take a risk and invest in integrating a code editor. It has all the desired features out of the box, provides very solid performance and user experience, and offers a lot of extensions.

### [How we integrated a code editor on the Miro canvas _202310](https://medium.com/miro-engineering/how-we-integrated-a-code-editor-on-the-miro-canvas-a41e0eff7f21)

- The scaling of the rendered widgets is managed by our canvas engine, but in Edit mode we need to scale the HTML element with the editor manually. The scale factor is a multiplication of the board scale (zoom in/out) and the widget scale (widget size). To scale the widget, we apply the CSS property on the editor container: `transform: scale($scale)`.
  - During the prototyping with CodeMirror 5 and CodeMirror 6, we met this problem: if the editor is scaled, then the mouse events’ positions, as well as the visual elements’ sizes and positions are calculated wrong. Attempts to deal with those issues were unsuccessful: there is no easy fix or built-in support for this in CodeMirror.
  - We discovered that the Ace and Monaco editors, on the other hand, support the CSS transformations.

- To highlight the plain text, we’re using the native static highlighter extension for the Ace editor. It starts a minimal version of the Ace editor that outputs the HTML string.
- 🤔 For us, although it was less attractive at the beginning, the Ace editor was the best and the only option. It is very lightweight, supports scale out of the box, has the static syntax highlighting extension, and has been battle-tested for more than a decade. 

## [Moving to Monaco — A Journey to a Better Code Editing Experience | DataCamp Engineering _202107](https://blog.datacamp.engineering/moving-to-monaco-a-journey-to-a-better-code-editing-experience-8c2aa5360be5)

- The starting point of our journey is a custom code editor built on top of the Ace Editor library. This editor had served as the reliable backbone of Campus — our interactive course application — for several years.
  - Poor accessibility
  - Poor abstraction
  - Bad page performance
- We evaluated several solutions along the way, but ultimately settled on building our editing experience on top of Monaco.
# more
- [CodeMirror Accessible](https://bgrins.github.io/codemirror-accessible/)
