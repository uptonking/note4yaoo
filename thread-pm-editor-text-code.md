---
title: thread-pm-editor-text-code
tags: [code-editor, text-editor, thread]
created: '2021-05-23T10:31:12.011Z'
modified: '2021-05-23T11:00:06.662Z'
---

# thread-pm-editor-text-code

# pieces

- ## 

- ## 

- ## Are there any great text editor libraries out there that work like GitHub’s? Markdown, with drag and drop upload support, APIs for things like tagging people., etc?
- https://twitter.com/adamwathan/status/1405278574337150977
- The GitHub editor is open source:
  - https://github.com/github/github-elements
  - GitHub's Web Component collection.
- I tried a whole bunch of markdown editors last month and ended up going with tiptap.dev.It was the easiest of all the editors to add custom behavior/config.
- I've built my own editor https://github.com/michelson/dante, it's like a medium editor with pluggable blocks (giphy, vlog, embeds, image, voice recording and more). ( the latest version is on top of @tiptap_editor, previous was written on draftjs ) oh, and I'm using tw for the doc site
- Any side-by-side Markdown editor/preview without scroll synchronization is a pill of poop.

- ## My favorite idea from Helix. Why don't text editors build AST support into text rendering? 
- https://twitter.com/jarredsumner/status/1399891268713422848
  - Remember what JavaScript code formatters were like before Prettier? That's every modern text editor reading your code.
- What do you mean by building in AST support?
  - Like .tmLanguage but it'd emit an AST instead of just tokens
- dependency graph would be cool too, I think there are some cool text editor features that could be built on top of ASTs and dependency graphs

- ## we've been working on a massive project to move the editor from Slate to ProseMirror in order to get everything working well on mobile.
- https://twitter.com/maccaw/status/1395868244876144647
  - I just successfully booted up the mobile app for the first time. Feels good!
- ProseMirror doesn't do weird stuff with preventDefault that stops Slate working on Android.
- I have gone through this exact migration, best of luck! You won't be disappointed with Prosemirror, it's a fantastic piece of software.
