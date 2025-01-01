---
title: lib-ide-vscode-community-web
tags: [community, vscode, web-ide]
created: 2024-12-31T21:06:59.021Z
modified: 2024-12-31T21:07:14.052Z
---

# lib-ide-vscode-community-web

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## [Vscode.dev | Hacker News _202110](https://news.ycombinator.com/item?id=28932206)
- >Well, offline VSCode is a glorified browser as well.
  - Not really, it may use electron for the front end, but a huge amount of what makes vscode useful and fast is the native binaries that power all of its functionality.
- What are those native binaries? I know that VSCode ships with ripgrep, but that's the limit of my knowledge. Those binaries probably could be compiled to WASM to make VSCode fully run in a browser too.
  - The Language Servers that power all of the intellisense and syntax highlighting and stuff are all native code. As are the compilers and everything that make VSCode more than just a text editor.

- Why bother with all of that when you could just ssh (nee telnet), remote X or VNC sessions to a server?

- check the discussion about their differences https://github.com/cdr/code-server/discussions/4267 (IMO both are much slower and worse than vscode.dev)
  - There is no direct comparison, so unfair to call them slower or worse. Both these services are for running your own private server and for browser IDEs to be thin clients. You can configure the server with your language tooling, build scripts and whatever else. You can also pause and resume your session from a different device (since a majority of business logic is handled by the server).
  - vscode.dev runs fully in your web browser, and files are read from local disk. There is nothing in the cloud. So yes it is faster, but serves a different use case.

- theia has a nodejs server backing its web experience. This vscode.dev is an entirely client side JS application that runs in your browser--there's no backend server beyond something to serve a pile of static JS and html.

- The blog post says it's using a brand new local file access API only in cutting edge browsers (edge and chrome) so you can access the files on your machine directly from the browser. There is no server upload of anything.

- Interesting they're using tree-sitter for syntax highlighting. Obviously they can't run LSPs in the browser so this must have been an alternative. 
  - The article points out that the Typescript/Javascript and Python LSPs run in the browser providing "better" experience than the tree-sitter experiences for languages without browser capable LSPs today.
- They don't use tree-sitter for syntax highlighting unless the extension you're using uses it. By default (and almost everything uses the default) VSCode uses the Textmate syntax highlighting system.
  - And there's no reason they can't use the LSP in the browser as long as the actual language servers can run in the browser - pretty easy with most languages these days.

- Two features missing right away: Terminal and Remote SSH.
  - From my understanding, since their vscode uses browser file access api with zero installation, adding terminal seems non-trivial. I have been working on something that solves that: https://tym.so (shameless plug here). I’m trying to build a vscode on the browser that can be connected to any computer with a one line install and has easy multiplayer features. Love to know what you all think about it

- It's crazy how much the dev tooling space has evolved in just the last few years. VS Code is of course a big part of it, but there are a hundred offshoots providing CI/CD, dev VPS, source control integrations, language tools, static hosting, staging, functions. The next step, IMO, is more clarity. How do all these puzzle pieces fit together, and what is the "ideal" solution for me as an individual developer or a small team to use day-to-day?

- ## [Visual Studio online available for public preview | Hacker News _201911](https://news.ycombinator.com/item?id=21442088)
- The use case for VSCode Online is the same as any other remote development environment, combine it with deployment workflows and or integrated services like Azure and it practically sells itself. Just like Slack the secret sauce here isn't the service itself, it is how it ties into everything else.
- What other remote development environments exist? I can only think of cloud9.
  - Nano/vim/emacs/etc over a remote (SSH) terminal, remote VM, or remote session via other means (e.g. VNC/RDC/etc). People use Visual Studio itself remotely via VMs and RDC.

- ## [Microsoft’s web-based version of Visual Studio | Hacker News _201911](https://news.ycombinator.com/item?id=21461681)
- Because VSCode is an electron app, meaning that it probably relies on Chromium-only features that they have to find workarounds for in Firefox before things like keyboard shortcuts work.
