---
title: lib-ide-sourcegraph-community
tags: [code-search, sourcegraph]
created: 2024-12-27T17:27:58.886Z
modified: 2024-12-27T17:28:57.941Z
---

# lib-ide-sourcegraph-community

# guide

- tips
  - 不必过早在搜索上投入太多精力，类似vscode的ripgrep方案对大多数场景都够用
# not-yet
- ❓vscode默认的搜索 vs sourcegraph
# discuss-stars
- ## 

- ## 

- ## 
# discuss-code-search
- ## 

- ## 

- ## [Repository X-Ray (#11733) · Epic · gitlab-org _202310](https://gitlab.com/groups/gitlab-org/-/epics/11733)
  - The idea is to have a container based scanner for repositories that gathers as much information as possible from a repository, saves the data to a database that can also run locally in IDE's and the server.

- Is tree sitter something we can use?
  - With tree sitter poses significant challenge to deliver onto multiple platform because it is run as native extension and requires dedicated compilation process adjusted for different platforms. There was already research around tree sitter that was concluded with &11568 (closed) that you can check to get more context
- the tree-sitter project provides WASM bindings for every major programming language. By definition this does not require special handling for cross-platform compilation. It is the defacto standard for editor extensions that need to do AST parsing for this very reason. VSCode extensions, for example, are not compiled for multiple architectures, they are just JavaScript.

- After diving more into resources available around code indexing tasks available in the web I got to conclusion that at this stage the best option forward would be SQLite. My attempts to find reliable and portable graphDB wasn't successful. 
  - That discussed very similar challenge, and how solution evolved over time. Despite that sourcegraph finally decided to move away from the SQLite as storage for code index, I still believe that in our case their papers can be seen as production proven solution. 
  - It is important to notice that sourcegraph use cases where overlapping with the ones that we are aiming for, and to achieve them they used graph like data formats (LSIF and later SCIP), which were server from SQLite instead of any graphDB.
- The fact that before the migration there had 796Gb of data stored in SQlite dbs shows that it can deliver.
  - Another argument speaking for SQLite is that it offers WebAssembly distribution, which might be very helpful for WebIDE
- What in my opinion is another great benefit of SQLite approach is that it could use CI artifacts feature (at least in the initial iterations) that would handle significant part of infrastructure foundations required to server repo x-ray data. 

- Why would we want a portable DB?
  - Moving load towards the client, which in general are less busy then GitLab instances as they serve a single user instead of all of them at once
  - Some operations can be preprocessed on client side, eg: client can preload list of related files based on active tab, before even code creation request is send. GitLab rails application on the other hand would have to reload that kind of data for each request
  - Clients will have up most fresh data in some cases, for example with related files map being stored in portable DB, client will be able include local state of those files into the context, while monolith would only have committed version which might be behind local development

- https://lsif.dev/ - which seemed promising at the begging, but after closer look it appears that it has not got enough adoption in community to be reliable
  - scip - which was announced to be improvement / replacement over lsif, but for now it seem to be only used by sourcegraph, which might not be again reliable tool to build upon
- you can notice that LSIF and SCIP formats was considered in the research but were not selected as suitable solutions for the MVC scope.
  - It is worth to notice that LSIF despite being promising at the begging comes with its own challenges, and might raise future support concerns.

- LSIF provide information about structure of a source code, helping to create dependency graph, extracting function/classes/structures names etc. However LFIS does not provide any information about purposes or application of source code. So LSIF (or tree-sitter parser) can provide valuable input that can be used by RAG system to build its context database, but further processing would be also required (eg: create embeddings out of function body, and suggesting users to reuse existing code if it is similar to the newly inputted one) to fetch most relevant pieces of context that can help improve answer returned to a user.

- ## ⚖️ [srctx: a LSIF parser for understanding what happened in every lines of your code : r/golang _202304](https://www.reddit.com/r/golang/comments/12di427/srctx_a_lsif_parser_for_understanding_what/)
  - The LSIF defines a standard format for language servers or other programming tools to emit their knowledge about a code workspace.
  - LSIF is a standard format for persisted code analyzer output. Today, several companies are working to support its growth, including Sourcegraph and GitHub/Microsoft. 

- 👷 I work at Sourcegraph. Not trying to take anything away from your tool, but I wanted to communicate where we're at
  - Over the last ~9 months or so, we've been moving away from LSIF and have been using SCIP instead.
  - The Sourcegraph backend also natively accepts SCIP instead of LSIF, and converts LSIF to SCIP for maintaining backwardws compatibility.

- ## [Explore whether 'smart code search' (AST, stack graphs, scope graphs) would improve performance beyond the current find/grep based approach. · Issue #38 · SWE-agent/SWE-agent _202404](https://github.com/SWE-agent/SWE-agent/issues/38)
- Looking at the current 'search' command that the agent has access to, it seems it just uses `grep` for searches within a file, and `find` for searches by filename
  - It would be interesting to see whether giving some more powerful AST / 'smart' code based search functionality would improve the performance of the agent
- One direction that might be interesting to explore with regards to this is 'stack graphs' / 'scope graphs'
- [Introducing stack graphs - The GitHub Blog _202112](https://github.blog/open-source/introducing-stack-graphs/)
  - Why aren’t we using the Language Server Protocol (LSP) or Language Server Index Format (LSIF)?
  - To dig even deeper and learn more, I encourage you to check out my Strange Loop talk and the stack-graphs crate: our open source Rust implementation of these ideas.
  - Incremental, zero-config Code Navigation using stack graphs.

- ## 🚀 [Show HN: Sourcebot, an open-source Sourcegraph alternative | Hacker News _202410](https://news.ycombinator.com/item?id=41711032)
  - Using local tools like grep were ill-suited since you often only had a handful of codebases checked out at a time. 
- Zoekt already has its own UI, though it is very feature-limited and lacks syntax highlighting.

- this is a relatively small UI wrapper of a zoekt backend, it seems like the risk here is isolated to the upstream Sourcegraph-maintained search dependency. 

- I looked through the sourcecode, but I can only find UI (ie. browser) code. Does this do anything beyond delivering a more functional and prettier UI on top of an existing zoekt deployment? If no, everybody would be better served if you tried to improve the UI inside Zoekt, which currently is a live demonstration of (my lack of) web app programming skills. Have you thought of how you will achieve your further goals (eg. semantic search)? That will require server-side changes, but you currently have no Go code at all.
  - Yea that is correct - in its current state, it's functionally a UI wrapper on top of the zoekt-webserver api. 
- As for just a UI over Zoekt, let me plug https://github.com/TreeTide/zoekt-underhood
  - https://github.com/isker/neogrok

- Why not just use your IDE?
  - an IDE is often more convenient when you have the code checked-out locally. This becomes a pain when you work in a organization with potentially hundreds of repositories that you need to search across (e.g., a org stores their 100+ microservices in separate repos, and you need to find all places where they make a request to your service).
  - I cannot run Xcode on Linux, I cannot run Visual Studio on Linux
  - some languages practically require arbitrary code execution to make a build, which I'd much prefer to shove into an isolated VM.
- I use ghorg in tandem with ripgrep to address that problem. The former is for checking out the main branches of all repositories, the latter to perform the actual search.

- since GitHub copied SourceGraph, I don't have much of a need for these self-hosted solutions.
  - yeah, github has a nice search now, the only complaint is that you need to be logged on to use, besides this is really nice.
- sourcegraph is dead with advent of LLMs and AI coding tools right? Github cross repo search is also not bad anymore
  - Wrong. Unless you want to feed the LLM your entire codebase, which is usually infeasible, you need to be able to retrieve relevant context, which relies on understanding the codebase, as Sourcegraph does. Sourcegraph has a product that does precisely this, called Cody.

- Does this make a copy of each repo on ingest? Can it work against in-place repos, for example if hosted on the same server as a code forge installation?
  - Yea exactly - on ingest it clones the repos and will periodically fetch new revisions. Currently we don't support in-place repos, but feel free to file a issue and we'd be happy to take a look.

- How would this work if you want to index different branches of a repository only?

- Any plans to add Gitea/Forgejo (self-hosted) support?
- Any plans for non Github/Gitlab integrations? Gitea/Gogs/etc. maybe?

- Can you add repos after starting the container? What about persisting indexes across restarts?
  - Yes - there is a file watcher that should pickup modifications to the configuration file.
  - And you can persist indexes across restarts by mounting a volume to the `/data` directory (e.g.,    `-v $(pwd):/data`). Indexes are stored in a `.sourcebot` cache directory.

- Does it support Perforce? i couldn't find it in the schema in the repo.
  - No just GitLab and GitHub atm
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
