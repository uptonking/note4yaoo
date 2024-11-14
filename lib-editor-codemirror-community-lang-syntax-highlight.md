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

- ## [Language parser/syntax tree performance and debouncing - v6 - discuss. CodeMirror _202202](https://discuss.codemirror.net/t/language-parser-syntax-tree-performance-and-debouncing/3976)
  - I’ve been investigating the performance differences between CodeMirror 5 and CodeMirror 6, 
  - and one major difference I’ve noticed with respect to parsing the syntax tree is that in CM5, parsing is debounced while in CM6 it is done synchronously for each `docChanged` transaction/update.
  - This has an interesting effect where typing quickly (or holding down a key for repeated character insertion) causes CM6 to use up a ton more CPU to repeatedly re-parse the syntax tree whereas in CM5 it’s only re-parsed once.

- 👷 CodeMirror 5 also eagerly parses the lines it redraws, but I guess that ends up not drawing attention in the profile because it is generally limited to a single line.
  - Various bits of state (highlighting, folding information, bracket matching, etc) in version 6 rely on the tree to be available whenever the editor is updated. As such, ‘debouncing’ parsing would incur a rather high complexity cost.
  - The idea is that, at least once warmed up, the incremental parser is fast enough to create a new tree in about 1 millisecond. 
# discuss-lint
- ## 

- ## 

- ## [How to actually use eslint in Codemirror 6 - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-actually-use-eslint-in-codemirror-6/4184/6)
- CodeMirror 6 can use eslint-linter-browserify

- What if there’s no working linter in browser or the bundle is too big to bundle? I think using remotely lint is an option too.
  - No additional bundle size, even if you have tens of linters on one page.
  - Stay updated with the latest versions of linters without waiting for updates to an npm package.

- ## [How to do async lint - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-do-async-lint/7110)
- A lint source can return a promise. So just make your function async and make sure you only return after you have the actual result, and everything should work.

# discuss-sql
- ## 

- ## 

- ## 
# discuss-tree-sitter
- ## 

- ## 

- ## Oxc parser on the node side is compatible with estree-walker, along with types.
- https://x.com/boshen_c/status/1850179017862959128
- Is it fully compatible now? Last time I checked/tried iirc there were some differences in the ast still
  - Still not compatible. estree-walker duck types the AST for the visits ...

- ## 🧮 [Lezer: A parsing system for CodeMirror, inspired by Tree-sitter | Hacker News _202403](https://news.ycombinator.com/item?id=39805591)
- lezer is a parser generator( which by itself is not a trivial feat with novel ideas like incremental computations applied to parsing) to power his mainstream project which is CodeMirror.
- it would be great if CodeMirror could just work with Tree-sitter or similar. There’s a lot of ecosystem around other parsing systems, and needing to figure out Lezer stuff is a big friction for adopting CodeMirror 6 for me. There are not a lot of language packages listed
- Unfortunately, tree-sitter is written in C, which is still awkward to run in the browser (and CodeMirror targets non-WASM browsers). It also generates very hefty(大的，重的) grammar files because it makes the size/speed trade-off in a different way than a web system would.
  - Tree-sitter does run on the web. I got it working for my editor, but it did involve several days' worth of effort and getting into the weeds with emscripten.
- I've been using both codemirror and lezer in Yaade (https://github.com/EsperoTech/yaade). Thanks to lezer I was able to write a JSON extension language that supports Yaade environment variables. Pretty cool project and very nicely documented! I love building OSS on top of OSS.

- 
- 

# discuss-lezer
- resources
  - [Comparison of Leading Language Parsers – ANTLR, JavaCC, SableCC, Tree-sitter, Yacc, Bison _202310](https://www.researchgate.net/publication/376883410_Comparison_of_Leading_Language_Parsers_-_ANTLR_JavaCC_SableCC_Tree-sitter_Yacc_Bison)

- ## 

- ## 

- ## [How get token from updateListener.of - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-get-token-from-updatelistener-of/4158)
- `syntaxTree(state).resolve(pos)` might help here (though it doesn’t do exactly the same thing as tokenBefore, but you can see how that’s implemented and do something similar if needed).

- ## [Some thoughts (and requests) about how CM6 schedules parsing - v6 - discuss. CodeMirror _202103](https://discuss.codemirror.net/t/some-thoughts-and-requests-about-how-cm6-schedules-parsing/3045)
- 
- 
- 

- ## [Iterating skipped/whitespace nodes in a SyntaxTree - Lezer - discuss. CodeMirror _202406](https://discuss.codemirror.net/t/iterating-skipped-whitespace-nodes-in-a-syntaxtree/8283)
- Typically, whitespace isn’t encoded in the tree (as a lower-case node name), so there’s no way to see where it was matched. 
  - `isSkipped` is often used for comment nodes, so that they can be highlighted.

- ## [How to reprocess syntax tree? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-reprocess-syntax-tree/6083)
  - I’m creating a language package for Excel functions. How can I force a reprocess so that highlighting works when switching idiom?
- Pass the language as a parameter to whatever creates the parser, and update your configuration to use a new parser whenever the language setting is changed.
  - You can use dialects or reconfigured external tokenizers to make small changes 
  - Recompiling the grammar should never be necessary at run-time.

- ## Looking for examples on how to use @codemirror / Lezer's incremental parsing mode.
- https://x.com/MarijnJH/status/1582604809718202368
  - I see ensureSyntaxTree() takes a max line number param, but I'm not sure how it expects you to save+restore state between calls.

- That's automatic. Parsing work is kept in a mutable cache and reused when possible on the next editor state update (and on further calls to that function).
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🌰 [All I want to do is highlight "hello" - Lezer - discuss. CodeMirror _202305](https://discuss.codemirror.net/t/all-i-want-to-do-is-highlight-hello/6444)
  - Is there anyone here that can give me a simple example of how to highlight for example the word “hello” in a specific color?

- ## 🌰 [Syntax Highlighting in CodeMirror v6 without the editor functionality? - discuss. CodeMirror _202402](https://discuss.codemirror.net/t/syntax-highlighting-in-codemirror-v6-without-the-editor-functionality/7823)
  - I am looking to syntax highlight hundreds of blocks of code on a page, and creating editors for each will be too much performance-wise I think. I saw some threads discussing syntax highlighting being implemented for v6 (like this? Server-side highlighting with CodeMirror 6 · GitHub 17), but wasn’t sure what the status/plan was.
  - [Server-side highlighting with CodeMirror 6 _202010](https://gist.github.com/justinfagnani/7d4a4acfc4dd00dde3c62db13731f68f)
- You can use the Lezer parser system (as used in CodeMirror) to highlight code without an editor. See here for an example.

- Is there a basic way to integrate that Lezer parsing with EditorView.theme?
  - Not really—editor themes style parts of the editor, not the syntax.

- 
- 
- 

- ## [Loading syntax highlighting on demand? - v6 - discuss. CodeMirror _202402](https://discuss.codemirror.net/t/loading-syntax-highlighting-on-demand/7840)
- All the language descriptions in `@codemirror/language-data` use dynamic imports. So if your bundler supports code splitting, they should just magically get loaded on demand.
  -  Each of these holds a function that, when called, runs an `import(...)` expression that fetches the actual language mode. 
  -  If you set up Rollup or whatever you’re using to split your bundle on dynamic imports, they shouldn’t be part of the ‘main’ bundle.

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
