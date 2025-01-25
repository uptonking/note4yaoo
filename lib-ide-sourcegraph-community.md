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

- ## Vercel刚推出的一款强大的代码搜索工具叫grep，覆盖超过50万个GitHub仓库。
- https://x.com/vista8/status/1880945126220218452
  - 支持代码、文件和路径多维度搜索，支持跨仓库代码搜索，能用正则和区分大小写，非常好用。

- 这个也是独立开发者做的 被vercel收购了

- ## ⚖️ [Sourcegraph is no longer open source | Hacker News _202307](https://news.ycombinator.com/item?id=36584656)
- It was open first. Then closed. Then open again. So, now it's closed again...

- Sourcegraph only provided non-OSS images and the build process was difficult and broken for a long time
  - It's no wonder, that the usage of OSS version was pretty low, when few were able to build it

- If anyone's looking for an open-source search tool for grepping across repos (or even one large repo) at insane speed, I highly recommend livegrep
  - We used it at Stripe and it was quite popular; often, searching even a single repo was faster on livegrep than with ripgrep locally.
- livegrep is... fine. It's literally what it says it is. It's a web version of grep. livegrep is definitely not a replacement for sourcegraph, which actually understands the underlying code, and lets you follow code paths, search for references, etc.

- https://oracle.github.io/opengrok/ is open source and very good at huge source base, e.g. for the whole android and linux kernel together, fast and useful.
  - It’s a Sun tool that Oracle inherited and never made an attempt to monetize.

- I'll add something I have been working on https://github.com/boyter/cs which is aimed at a smaller scale. It works fine for multiple repositories so long as they aren't too large.

- Did anyone actually use the open version? I dimly remember that I looked into it like 2-3 years ago, but all the really interesting stuff was not included in that. 
  - OSS version didn't have official Docker images prebuilt, you had to build them yourself and for a long time the OSS build was broken. 
- Yes, I remember the Docker thing, but I also remember that at least the language parsers we were interested in were only supported through some kind of plugin mechanism, which the OSS version did not support, so it was useless for us, so I didn't ever bother testing it.
- So basically their "open source" offering wasn't really open source, it wasn't even open core, as you had to build it yourself, the build wasn't working for a long time and even if you managed that, some languages were enterprise-only.

- https://github.com/sourcegraph/sourcegraph/issues/53528#issu... appears to be a comment from someone in the project laying out why they've changed.

- Tools like sourcegraph are cool, but it is not like they are going to make you X times more productive.
  - The marginal efficiency gain over the free ripgrep is so small

- There is a lot of competing technology now, from GitHub’s improved search to new open source LangChain and LlamaIndex support for better document chunking of source code in several languages.
  - That's part of the impetus behind their Cody product. It uses the code search system as a semantic index. It actually works very well in my experience.

- Cloud9, Elastic, Sourcegraph, CockroachDB, what is it with companies making things closed source?

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
