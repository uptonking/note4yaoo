---
title: lib-editor-codemirror-community-lang-syntax-highlight
tags: [code-editor, codemirror, community]
created: 2023-06-16T10:52:26.160Z
modified: 2024-08-11T07:59:35.617Z
---

# lib-editor-codemirror-community-lang-syntax-highlight

# guide

# solutions-docs
- [Get started | OpenCtx](https://openctx.org/docs/start)
  - OpenCtx shows you contextual info about code from your dev tools, in your editor, in code review, and anywhere else you read code
# solutions-highlight
- [Twoslash Code Samples](https://www.typescriptlang.org/dev/twoslash/)
  - A markup format for TypeScript code, ideal for creating self-contained code samples which let the TypeScript compiler do the extra leg-work.
  - [Twoslash – Vocs: extract/completion/highlight](https://vocs.dev/docs/guides/twoslash)
# discuss-stars
- ## 

- ## 

- ## 
# discuss-sql
- ## 

- ## 

- ## 
# discuss-lezer
- resources
  - [Comparison of Leading Language Parsers – ANTLR, JavaCC, SableCC, Tree-sitter, Yacc, Bison _202310](https://www.researchgate.net/publication/376883410_Comparison_of_Leading_Language_Parsers_-_ANTLR_JavaCC_SableCC_Tree-sitter_Yacc_Bison)

- ## 

- ## 

- ## 

- ## 

- ## Looking for examples on how to use @codemirror / Lezer's incremental parsing mode.
- https://x.com/MarijnJH/status/1582604809718202368
  - I see ensureSyntaxTree() takes a max line number param, but I'm not sure how it expects you to save+restore state between calls.

- That's automatic. Parsing work is kept in a mutable cache and reused when possible on the next editor state update (and on further calls to that function).

- ## 🧮 [Lezer: A parsing system for CodeMirror, inspired by Tree-sitter | Hacker News _202403](https://news.ycombinator.com/item?id=39805591)
- lezer is a parser generator( which by itself is not a trivial feat with novel ideas like incremental computations applied to parsing) to power his mainstream project which is CodeMirror.
- it would be great if CodeMirror could just work with Tree-sitter or similar. There’s a lot of ecosystem around other parsing systems, and needing to figure out Lezer stuff is a big friction for adopting CodeMirror 6 for me. There are not a lot of language packages listed
- Unfortunately, tree-sitter is written in C, which is still awkward to run in the browser (and CodeMirror targets non-WASM browsers). It also generates very hefty(大的，重的) grammar files because it makes the size/speed trade-off in a different way than a web system would.
  - Tree-sitter does run on the web. I got it working for my editor, but it did involve several days' worth of effort and getting into the weeds with emscripten.
- I've been using both codemirror and lezer in Yaade (https://github.com/EsperoTech/yaade). Thanks to lezer I was able to write a JSON extension language that supports Yaade environment variables. Pretty cool project and very nicely documented! I love building OSS on top of OSS.

- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 🌰 [How to define highlighting styles for blocks? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-define-highlighting-styles-for-blocks/4029)
  - Is there any way to define styles for blocks (e.g., blockquote, codeblock)?
- Not without defining an additional extension that adds some class to the lines that contain a code block (using `Decoration.line` ).

- ## [Syntax Highlighting inside widget decoration - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/syntax-highlighting-inside-widget-decoration/6160)
- Is it possible to apply syntax highlighting inside the widget’s content?
  - Not directly using the editor’s syntax highlighting. Though I guess you could run `highlightTree` on the subtree for the text inside the widget, feeding it the same highlighters that your editor uses, and then construct the highlighted DOM directly and put that in the widget.
- You could apply marker widgets to the content you want to alter, and put empty replace widgets on the stuff you want to hide, skiping the whole need to redecorate it inside a new widget.

- To fully support the recursion for widgets I was thinking, would it be a bad idea to start a separate instances of CM6 view inside the widget? For example of I have a widget of a matrix, where each cell is a separate CM6 editor. Then I can make matrixes inside matrixes and so one. I tried, not too bad I would say

- ## 🎨 Heikki Lotvonen 魔改了一款字体，Colr Fonts ，原生就支持语法高亮，不需要任何 JS 的处理，任何的语法高亮被直接内置在这款字体中，就是 plain text。
- https://x.com/vikingmute/status/1824253104625422699
  - 支持暗黑模式，目前支持 CSS/HTML/JS

- ## Can you Syntax Highlight a code snippet on the web without overloading the DOM with a ton of `<span>` elements wrapped around the tokens?
- https://x.com/RogersKonnor/status/1758318286633091467
  - Thanks to the Custom Highlight API, you can!
- Only a matter of time before syntax highlighting libs start supporting this out of the box too
  - It's unpolyfillable, you'd have to use a different strategy when that's unavailable.
- Was afraid you'd say that. Then again it's true for most CSS stuff. I'd be curious to compare the difference performance of the native highlight vs span highlighting. I imagine more DOM nodes will be worse, but you never know until you try!

- I think Prism itself is probably also unsuitable for this, I don't think one can pause syntax highlighting and give back control to the main thread, right? You'd want something that can do that for a real editor or it will freeze on big-enough files.
  - Well im only using Prism for the overlaid `<pre>`. Under the hood it's just a `<textarea>`. Which is why I was thinking of virtualizing the highlighting to only what is visible which could probably result in "incorrect" highlighting if you don't run it on the whole document.

- The textarea overlay approach is cool, but the "problem" is that just editing a big enough string in it can be too slow, so that has to go in order to make something that works as well as vscode. No idea why even monospaced textareas are that slow 
