---
title: lib-ide-vscode-community-internals
tags: [codebase, community, internals, vscode]
created: 2025-02-04T17:20:35.702Z
modified: 2025-02-04T17:21:02.875Z
---

# lib-ide-vscode-community-internals

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 
# discuss-dev-codebase
- ## 

- ## 

- ## 🤼🏻 [Visual Studio Code is designed to fracture(折断；断裂；破裂) (2022) | Hacker News _202409](https://news.ycombinator.com/item?id=41691577)
- VSCode’s ecosystem is, in many respects, quite weak:
  - cpptools is kind of amazing but also pretty bad. It regularly malfunctions for me. It’s essentially undebuggable.
  - The VSCode security story is very, very weak. Extensions are not sandboxed. The client, accessing remote repos, is wildly insecure, by design.

- >  The VSCode security story is very, very weak. Extensions are not sandboxed. The client, accessing remote repos, is wildly insecure, by design.
  - All these same things are true for emacs/vim/CLion plugins as well. You kind of either have to accept the risk cowboy style, do something in the middle (maybe only allow very well known extensions from source you trust), or live without the extensions.
- Can't you host your own extension marketplace?
  - Then you have other problems. Maintaining the store itself, obtaining the extensions people want, and keeping the extensions up to date adds some overhead.
- Extensions often rely on third-party binaries (such as Language Servers, kubectl, ssh or even git itself), internet access (SAAS providers, pulling data or definitions, ...) and on your filesystem (SSH Config, Kubernetes config, Config folder in your home, ...). Sandboxing these extensions is not easy unless everything is configured within VSCode which is rarely the case.
  - As far as I know, extensions are not sandboxed either on Emacs, (Neo)vim, Jetbrains IDEs.
- Extensions (in Emacs lingo we call them 'packages') are not sandboxed by design. Because unlike VSCode, you are allowed to override any, just about any part of a package's code. You can, for example, grab a command introduced in a third-party or a built-in package and override only specific parts of it without having to rewrite the entire thing.

- vscode tunnel is already a massive step up from vscode remote SSH here.

- ## [The Era of Visual Studio Code | Hacker News _202009](https://news.ycombinator.com/item?id=24558788)
- JetBrains products allow you to do so much out of the box, without installing a million plugins that may or may not work. 

- I completely switched to VS Code once I discovered the remote development feature

- There's a couple big knocks against VS Code that don't get brought up enough
  - The extension API is underdocumented. 
  - VSC also inherits the core weaknesses of Electron. Not overall performance/memory so much as startup time
  - 🌹 LSP and DAP are huge milestones

- The thing that bugs me about VSCode is it's labeled as open source but a lot of pretty critical and interesting components are closed source so you have no idea what's going on under the hood. 
  - The biggest feature is probably remote. 
  - Some of the language servers for popular languages are closed source too
- Live Share is probably _the most_ interesting feature of the entire editor, and is not open source or usable with VSCodium.

- ## 🎯 [A Picture of Java in 2020 | Hacker News _202009](https://news.ycombinator.com/item?id=24551390)
- In the web space it is understandable to use an editor as web developers are typically working with dynamic languages, and often use other tools like browser plugins to give them what they need.. 
  - But in Java, especially professional Java, you really get a lot out of a good tool that has integration with the application server and you can really use the analysis and refactoring and everything.
  - IME a lot of developers don't like their IDE heavily coupled to backend servers and environments, but actually prefer the "code editor + useful features" approach. It makes combining with CI/CD a lot simpler for one, since the activities run on a project can simply be the same as those run on the pipeline. A quick "mvn install" is often enough for many/most modules. Many devs only really want advanced editing + syntax highlighting + language server.

- VSC has a few first-class, officially-supported (e.g. MS) plugins that immediately give you nearly all IDE superpowers (inline debugging, intellisense, build environments, git, remote development, testing, etc) with very tight integration.

- ## [Copilot Internals | Hacker News _202212](https://news.ycombinator.com/item?id=34032872)
- Why does “cushman-ml” suggest a 12B model instead of the 175B model?
- This is about the VSCode extension, which is obfuscated (maybe compiled) JS.
  - Their JetBrains plugin is written in Kotlin / Java but it spins up a agent server written in node.js which handles the business logic (building the prompt, caching, making completion requests to their API). I assume most of the code is shared between the VSCode extension and this javascript agent.

- Free idea for GitHub: a huge bit of missing context for the model right now is the last few edits made by the user. If you move your cursor to a different part of a long file, Copilot immediately forgets about that part of the file. If it knew the last few edits you did then it would be able to make much more intelligent suggestions based on the task you're working on, rather than just current cursor position.
  - This is a pretty cool idea even for just engineering the prompt! It's a complicated tradeoff to decide what should go into the context and what should be selected from other files (2000 tokens is a lot but sometimes not long enough for the longest files). Previous cursor location is a great signal directly from the user, compared to metrics like Jaccard similarity. I'd actually like to try this out for our next release of Codeium.
