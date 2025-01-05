---
title: lib-ide-lsp-community
tags: [community, lsp]
created: 2025-01-05T15:00:42.659Z
modified: 2025-01-05T15:00:51.509Z
---

# lib-ide-lsp-community

# guide

# discuss-stars
- ## 

- ## 

- ## [Why LSP? | Hacker News _202204](https://news.ycombinator.com/item?id=31151048)
- The existence of multiple LSP clients demonstrates the success of LSP and is a strength, not a weakness as the author suggests.
  - Often, it's because LSP clients have differences not in interacting with the LSP Server, but in how that is surfaced to the user. Some LSP clients are written in different languages, and that can make some implementations faster than others. This is why LSP is a success. It allows for clients to be written in many ways but for all of them to do the most basic thing they need to (go to def, rename, refactor, search symbols etc).

- One thing I have difficulty understanding is that given MS is (was?) the primary proponent of LSP, and the spec was originally written with TS in mind, and VSCode has first class support for LSP, why do community projects like typescript-language-server (along with a bunch of others like the one by sourcegraph) need to exist ? Why can't arbitrary LSP clients connect directly to tsserver (maintained by MS) ?
  - As far as I'm informed, they can. For example, NeoVim language client has a pretty wide range of officially supported servers, including tsserver.
- It connects to a community maintained lsp server that wraps tsserver. 
  - TSServer predates lsp iirc
- tsserver isn't LSP compliant, iirc they started with tsserver way before LSP was out, but since then didn't migrated to LSP. I think they didn't migrated because:
  - It's a big selling point for vscode. 
  - It might hard to migrate what they have to LSP, they might implement a lot of non LSP standards. 
  - Migrate to LSP could possibly delay new features because of the rewrite in tsserver.
# discuss-lsp-vendors
- ## 

- ## 

- ## [Building an Intelligent Emacs | Hacker News _202202](https://news.ycombinator.com/item?id=30308272)
- there's an analogous tool for debuggers called dap-mode
  - Like lsp-mode, it is also built on top of an open standard from Microsoft, the Debug Adapter Protocol

- TLDR: lsp-mode is the future of emacs.
- Eglot is written by a regular Emacs contributor and maintainer, and as a result is much higher quality code. lsp-mode is written by volunteers on Github without a lot of Emacs Lisp experience (it shows), the code is pretty bad at places, definitely over-engineered and I wouldn't recommend it.
- Even if the things you say about lsp-mode are true (which I don't think they are), lsp-mode has many features that eglot has no alternative to at all.
  - An example of such a feature is lsp-mode's project integration, it uses projectile which is much more powerful and useful than the built in project.el. Another example is using flycheck instead of flymake for on-the-fly diagnostics.
  - Eglot is much more minimal and tries to use native emacs features when possible, preferring minimalism over features. lsp-mode brings in a lot of features and prefers to use third party packages instead of built ins.
- 
- 
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Ask HN: Programmers who don't use autocomplete/LSP, how do you do it? | Hacker News _202412](https://news.ycombinator.com/item?id=42492508)
- I work almost exclusively in Emacs without the modern LSP-based tools. I believe I do keep more in my head than programmers that use more advanced IDEs.
  - In code I have control over myself I avoid imports that doesn't enumerate all imported symbols. That is I always use the import Library (symbol) syntax in Haskell and never do wildcard import in Python.

- I use vim with ctags. vim has good autocomplete but I don't use it much -- I rely on memory and looking things up in the docs. With ctags I can jump to definition/implementation of a function. ctags has worked since the early 1990s.

- ## [How LSP could have been better | Hacker News _202310](https://news.ycombinator.com/item?id=37852944)
- > The problem, column is counted using UTF-16 code units.
  - Rather than fixing the problem by using code points, they made it worse by allowing any encoding. Now, not only do you need to support UTF-16, but also UTF-8 and UTF-32
- You don’t need to; UTF-16 is mandatory (ugh), but support for other encodings is negotiated (see `ClientCapabilities.positionEncoding` and `ServerCapabilities.positionEncoding` ).
- This seems somewhat pointless, because for compatibility you need to support UTF-16 anyway, so why bother implementing any of the other encodings in addition.
  - Because if the server and client both use UTF-8 internally, they can get better performance by agreeing to use UTF-8.
- Or use UTF-8 everywhere to fix the problem. Code points have their own issues (as does UTF-8, but on balance these seem like better engineering tradeoffs).
  - Using UTF-8 only has better engineering trade offs if you represent text as UTF-8. If you don’t (like JavaScript) then it’s just extra complexity. It’s no better than UTF-16. Only advantage it has is it’s more common among newer languages.
  - Code points is the only thing that makes sense for a multi-language protocol. It’s unambiguous and every Unicode client can talk in code points, even if they use some exotic encoding.

- Does anyone know why LSP uses UTF-16 for encoding columns? It seems like everyone agrees it is a bad choice, so I'm curious about the original reasoning. Are there any benefits at all to using UTF-16, or was it something to do with Microsoft legacy code?
  - The JavaScript VM, Java VM, . NET VM, and several other runtimes (including effectively the entire Windows API) have their fundamental definition of strings be based on UTF-16 baked in.
  - I believe the original producers and consumers of LSP were written in languages that had string lengths based on UTF-16, so it was the literal easiest way to do it, even though UTF-16 is probably objectively the most painful thing to compute if your string system isn't UTF-16.
- There was a lengthy discussion on this. UTF-16 was used because it was convenient: it's what Microsoft API's and JavaScript already use (the latter being the language VS Code is written in).

- Sadly there is some standard to that. JavaScript source maps also use the same definition for columns.

- The biggest problem with LSP is that it's a lowest common denominator solution. If I try to edit OCaml using an LSP solution, I don't get features like "query type of symbol", presumably because JavaScript doesn't need it.

- Overall very informative. Really like the comparison with the Dart analytics protocol and the Jetbrains protocol. I think the comments on state synchronization with subscription based feature providers sounds very promising.

- 🤔 One thing that has annoyed me with some personal implementation work is why does DAP use a cosmetically similar but not following spec version of JSONRPC? Why not just use JSONRPC especially considering LSP already does?
  - Because of organizational disorganization within the VS Code development teams. LSP and DAP are basically the VSCode APIs for implementing language support and debuggers but bolted onto an RPC layer without synchronization or consistency between the people/teams that develop them.

- LSP stands for Language Server Protocol. It's a communication protocol between the clients (text editors, debuggers, source viewers, etc) and the language servers.

- 
- 
- 
- 

- The way a language server should work, imo, is it holds all the code and serves projections of the code on the fly to the editor. The user of the editor makes changes to the code and commits it back, at which point the language server parses the code and integrates it into the codebase, pretty-printing it to files as necessary for source control. But, the file layout should be an implementation detail that the editor knows nothing about.
  - That's exactly how LSP is designed. The editor e.g. requests 'the user is hovering over code `<here>`, what should I show?' and the server responds with some Markdown text. Or 'the user wants to navigate to the thing under their cursor `<here>`, where should I go?' and the server responds with a file/line.

- I use lsp for three things: jumping to the definition of a symbol, auto completion of symbols and keywords and showing documentation.
  - None of this is new. We've had TAGS tables forever. Certain editors would provide the rest for certain languages in language-specific ways. LSP is just a general solution to the any editor/any language problem. It seems to work at least as good and often better than the custom solutions before.

- ## 🤼🏻 [LSP: The good, the bad, and the ugly | Hacker News _202409](https://news.ycombinator.com/item?id=41440275)
- The paradox is that it was meant to avoid to write language support for each editor. Yet, if you want to support vscode you must create a specific extension for it and can't just have a language client.
  - The article mention the configuration problem, but I'd add the problem that Microsoft refuses to specify a way for the server to tell the client what are the config options so that the client can show some kind UI showing the possible configuration options with a description of what they do
- That's because the LSP makes no assumptions about stuff like (1) what the language server is, (2) how it is launched and managed, (3) how the editor communicates with it, etc. It only defines the format of the communication, nothing else.

- Rust-analýzer is an example of what not to do, which is reimplementing a compiler frontend.

- How much easier is it to get the tree-sitter spec implemented for a new language compared to LSP? Are there synergies in getting both to work?
  - Tree Sitter doesn't do a tenth of what most LSP servers do, so it's much easier. But they aren't really related. Tree Sitter is a parser that you might use in an LSP server (I have done; worked decently).
- Treesitter is the wrong solution anyway. The biggest advantage of LSP is that the parser, type checker, ... used by the LSP is (well, can and should be) the same as the one used in the compiler (or at least another _complete_ implementation of the language, like clang for gcc/g++).
  - 🤔 Worth noting that major languages seem to be moving away from this model. Rust and C# both concluded that the needs of your actual compiler are very different than the needs of an incremental tool that can run on partially written code.
