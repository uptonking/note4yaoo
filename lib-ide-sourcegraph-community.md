---
title: lib-ide-sourcegraph-community
tags: [code-search, sourcegraph]
created: 2024-12-27T17:27:58.886Z
modified: 2024-12-27T17:28:57.941Z
---

# lib-ide-sourcegraph-community

# guide

# not-yet
- ❓vscode默认的搜索 vs sourcegraph
# discuss-stars
- ## 

- ## 

- ## 
# discuss-code-search
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [Toward a URL for every function | Hacker News _201606](https://news.ycombinator.com/item?id=11855638)
- 👷🏻 Sourcegraph founder here. We built this to make it much easier to grok code.
  - Sourcegraph supports Go and Java right now
  - Sourcegrapher here. This is for linking to the source code of functions (and other definitions), for when you are discussing or explaining code. It's not for importing code at compile time or runtime.

- > These URLs always refer to the latest definition and won’t break if the file is edited, unlike links to a specific line number.
  - You can always get the URL on GitHub for a particular line number at a particular revision which won't break when the file changes. 

- When I read the title, I was imagining something more theoretical, e.g. a URL encoding of lambda calculus terms.
  - The more general idea is a content-addressable function repository, where, as you point out, code would have to be in some kind of normal form.

- Sourcegraph folk, are you aware of Rich Hickey's codeq  for clojure
  - It lacks the ability to track changes, but BBQ http://browsebyquery.sourceforge.net/ can query JVM and CLR programs
  - It lacks the ability to track changes, but BBQ http://browsebyquery.sourceforge.net/ can query JVM and CLR programs

- Any plans to support Hg or TFS?
  - Yep, we will, but we don't have a timeline for those right now. Any VCS that can implement this Repository interface is fine. We have some code written to support Hg, but nothing ready to release yet.

- Please don't do this if you want future-proof URLs - that's the whole point of linking to a specific commit. Functions and files will get moved, renamed, refactored and deleted.

- Don't we already have this in the form of NPM?

- Would make a lot of node modules as functions redundant
