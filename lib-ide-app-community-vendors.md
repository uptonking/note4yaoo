---
title: lib-ide-app-community-vendors
tags: [ide, monaco-editor, vendors, vscode]
created: 2024-05-09T10:20:03.010Z
modified: 2024-08-24T16:28:27.099Z
---

# lib-ide-app-community-vendors

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-ide
- ## 

- ## [Atom now opens files larger than 2MB | Hacker News _201506](https://news.ycombinator.com/item?id=9690653)
- Visual Studio disables all editor services (cold folding, intellisense, etc.) except syntax highlighting on XML files bigger than 10MB.

- The editor (codename "Monaco") is from Erich Gamma (ex-IBM/Rational), the "Design Patterns" book author from Switzerland. Microsoft bought the Monaco editor with him and its the single reason why TypeScript exists and why JavaScript ES6 looks like it looks ("class" syntax) and why he leads the Visual Studio team

- ## 🗑️ [Atom was archived today | Hacker News _202212](https://news.ycombinator.com/item?id=34010065)
- I was an early adopter of Atom
  - The Atom developers made some technology choices that in retrospect were ill-advised, CoffeeScript being the worst of them and splitting everything into dozens of packages a close second. 
  - They tried to backpedal(撤退或撤出) on both of these later on, but by that time VSCode, with its far superior engineering built around TypeScript, was rapidly taking over.
  - While the Atom project ultimately failed, it did give us Electron and Tree-Sitter, two technologies that will certainly outlive it.

- Atom predated the LSP and leaned heavily into customizations with all the plugins running inside the UI thread (more like a traditional web page and 3p scripts). At the time they viewed the extreme customization support as a feature, and there was a thriving ecosystem of folks making plugins.
  - That architecture has a major flaw though. A default install was fast, but a real configuration with all the plugins ended up quite slow.
  - VSCode's architecture worked much better in real world configurations, and it turns out better performance wins in the editor space, even if it meant losing certain customizations (up to a limit). The architecture also allowed seamless remote editing, something Atom never could have done.

- VSCode did almost everything right: The choice of TypeScript as the base language (with which VSCode has a symbiotic relationship), the limited, slowly expanding extension API, LSP, the monorepo, the monthly release cadence, the built-in terminal, and the list goes on and on.

- the StackOverflow developer survey. 2022 edition says 
  - 74% of respondents use VSCode regularly, 23% use Vim regularly, and 4% use Emacs regularly.

- VSCode’s Jupyter Notebooks is slightly different from Hydrogen in that it’s basically a MarkDown document with executable code blocks (cells) in the text editor that show their output in the text editor.

- ## 🗑️ [Sunsetting Atom | Hacker News _202206](https://news.ycombinator.com/item?id=31668426)
  - 👷🏻 Founder of Atom here. We're building the spiritual successor to Atom over at https://zed.dev.

- The history of Zulip is one of my favorite counter-examples to this trend. They have seen great growth and success since spinning off from Dropbox

- It's what kickstarted Electron which eventually gave us VSCode, Slack, and lots of HN comments about memory usage. It also had the sweetest default theme of any code editor. RIP.
  - Electron was originally known as "Atom Shell"
- Before Electron (f.k.a. Atom-Shell), there was Node-Webkit (l.k.a. NW.js), which also was a foundation for plenty of apps 

- The killer feature of VS Code for me is that when you open a source file for python, or C++, or whatever it pops up a dialogue: “would you like to install the extension for this file type?”. Click that and you’ve got working IDE features for that language with none of the hassle of tracking down which is the right extension, how do I keep my plugins up to date, which dependencies do I have to install first, etc.

- 🤔 Monaco code editor got a huge amount of performance testing and work years before Atom arrived and built Electron.
  - the core editor (named Monaco) had been built for very early stages of the Azure Portal and then been adopted into IE 10/11's Developer Tools to replace an aging code viewer/editor.
  - It also sounds like VS Code took a much more measured approach to extension APIs than Atom did. In Atom nearly every part of the product was an extension, which is a great approach to dogfooding extension APIs and making sure everything including the kitchen sink has an extension API, but getting that performant is tough. Whereas VS Code was very careful in the early days in what extension APIs they declared and started from a place of performance first. In many cases if only a single extension doesn't perform well in VS Code you almost don't notice because it's mostly isolated from the rest of application performance. Atom had a lot more situations, from what I heard, where one badly performing extension brought everything to a crawl.

- 🏘️⚡️ On the topic of performance - one of the architecture decisions that VSCode nailed was the 'extension host'. all VSCode extensions are sandboxed in a child Node process, and can only communicate back with the main IDE process via the VSCode API. This has huge benefits for performance:
  - (1) extensions can never block editor startup. this was a huge problem for Atom as package loads were startup blocking and it wasn't uncommon to have multi-second startup times with lots of packages installed - especially due to the fact that JS packages typically repeat dependencies, resulting in tons of bloat. Also extension authors are rarely performance-conscious
  - (2) extension code can never block the core rendering thread, another huge problem in Atom - you'd often have stuttering/frame drops if extensions were doing blocking work on character or cursor changes, which was more often the case than not..
  - The tradeoff of course is that VSCode extensions are very limited in the set of UI customizations they can make but MS did a very good job of designing their APIs to be sufficiently extensible in this aspect (i.e. having APIs for extensions to hook into all core IDE features). Atom's extension ecosystem was much more fragmented resulting in dependency/versioning hell.
  - As a side note, another benefit of the extension host model is how it enables extensions to semi-magically work on remote filesystems (including inside WSL) without needing complete rewrites.

- LSP, better performance, better defaults, better plugins ecosystem, better (subjectively) UI.

- Atom might be retiring, but One Dark lives on in every other editor.
# discuss
- ## 

- ## 

- ## 

- ## [腾讯全资子公司腾云扣钉(coding)这个公司的编制是外包吗？ - 知乎](https://www.zhihu.com/question/378970420)
- 实际上产品也没有多高端，代码托管打不过gitlab，更别提github了，code server完全是扒了vscode的server版本部署到它们的服务器，就对外宣称是它们自主开发的了。还有两个满嘴脏话素质低下的领导，直接会在会议上当着员工的面说员工提出的方案是垃圾。更加搞笑的是，公司内部用的腾讯云的产品，经常一边用着腾讯云的服务一边骂腾讯云做的东西是垃圾。

- 绿牌，腾讯外包一样的

- ## 🌰 [Gitlab: Web IDE Beta | Hacker News _202212](https://news.ycombinator.com/item?id=34078225)
- TL; DR (meta phrased)
  - Microsoft is forking VSCode open source community by split licensing for source code and and official build of VSCode. If you build by yourself you can’t connect to VSCode is marketplace.
  - This allows them to fully control VSCode telemetry and reporting along with use on platforms such as Gitpod. It’s similar to how Apple controls apps on iPhone and in turn control how much you need to pay them

- lsp actually came out of the .net opensource community. omnisharp to be exact. It's funny how much is actually attributed to MS in this case, when most of VSCode did not originate there.

- It really needs to have a good competitor in this space, and I hope JetBrains can match that eventually with partnerships of their own.
  - Was a happy VSCode user for years but not very comfortable with how they’re starting to push more and more proprietary pieces, so started looking for alternatives. Neovim fits the bill perfectly.
- the community can just switch to VSCodium

- ✨ VScode’s killer feature is its remote development capability.
  - 💰 VSCode's remote plugin is proprietary, and FOSS is explicitly forbidden from using it. So we're back at "they pretend to care for OSS" and "Microsoft is in the embrace phase".
- The default Python extension is already proprietary.

- 
- 
- 

- ## 🌰 [Gitlab: The Future of the Gitlab Web IDE | Hacker News _202205](https://news.ycombinator.com/item?id=31487079)
- > we asked ourselves the question: Do we want to continue to invest in implementing custom features for the Web IDE that ultimately deliver the same value as those already available in VS Code? Or do we embrace VS Code inside GitLab, and invest in extending the experience to more tightly integrate with GitLab and the DevOps workflow?
  - 👷🏻 GitLab PM and author of the OP here. We have faith in the future of VS Code as an open source project but I'll also say that this isn't a one-way door. If things change in the future, we're not so heavily leveraged that we couldn't replace the Web IDE's underlying editor again.
- GitLab team member here. We have considered Theia in the past. Here are a couple of related epics/issues: 
  - https://gitlab.com/groups/gitlab-org/-/epics/1619 
  - https://gitlab.com/gitlab-org/gitlab-foss/-/issues/56812

- ✨ I would argue that the best thing to come out of VS Code isn't even "VS Code" the overall environment, it's LSP, and MS has given that back to the community such that anybody can use it in a competing editor. I don't really think "VS Code" the product has a "moat" here and (up to now, at least) MS hasn't demonstrated much intent on creating one.
  - yet they failed. Remember Atom or Brackets
- As a small anecdote as someone who switched from atom, the killer feature for VS Code is being extendable AND performant. I used to use atom for a flexible text editor, and then still have to use sublime text if I wanted to open a large file 

- I miss c9 which was bought by Amazon. It had a VM running behind it with a terminal so I was able to do .net core development. A couple times I wasn't home and wanted to fix a bug in my project so I was able to login to c9, spin up my project in the browser and it committed back to github.
  - Personally, I’m using Tailscale + VS Code with the Remote-SSH plug-in, accessing my home server.

- Running VSCode remotely introduces many interesting challenges, mostly due to security. (You are letting your users run any arbitrary code on your infrastructure.)

- 
- 
- 
