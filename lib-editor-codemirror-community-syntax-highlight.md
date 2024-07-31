---
title: lib-editor-codemirror-community-syntax-highlight
tags: [code-editor, codemirror, community]
created: 2023-06-16T10:52:26.160Z
modified: 2023-06-16T10:52:44.183Z
---

# lib-editor-codemirror-community-syntax-highlight

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
# discuss
- ## 

- ## 

- ## Can you Syntax Highlight a code snippet on the web without overloading the DOM with a ton of `<span>` elements wrapped around the tokens?
- https://x.com/RogersKonnor/status/1758318286633091467
  - Thanks to the Custom Highlight API, you can!
- Only a matter of time before syntax highlighting libs start supporting this out of the box too
  - It's unpolyfillable, you'd have to use a different strategy when that's unavailable.
- Was afraid you'd say that. Then again it's true for most CSS stuff. I'd be curious to compare the difference performance of the native highlight vs span highlighting. I imagine more DOM nodes will be worse, but you never know until you try!

- I think Prism itself is probably also unsuitable for this, I don't think one can pause syntax highlighting and give back control to the main thread, right? You'd want something that can do that for a real editor or it will freeze on big-enough files.
  - Well im only using Prism for the overlaid `<pre>`. Under the hood it's just a `<textarea>`. Which is why I was thinking of virtualizing the highlighting to only what is visible which could probably result in "incorrect" highlighting if you don't run it on the whole document.

- The textarea overlay approach is cool, but the "problem" is that just editing a big enough string in it can be too slow, so that has to go in order to make something that works as well as vscode. No idea why even monospaced textareas are that slow 
