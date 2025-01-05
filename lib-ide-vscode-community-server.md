---
title: lib-ide-vscode-community-server
tags: [community, ide, server, vscode]
created: 2024-12-01T09:34:40.620Z
modified: 2024-12-01T09:34:54.164Z
---

# lib-ide-vscode-community-server

# guide

# discuss-stars
- ## 

- ## 

- ## [Making Remote Development Even Better _202212](https://code.visualstudio.com/blogs/2022/12/07/remote-even-better)
- You may not think about it, but VS Code has a built-in command-line interface (CLI) that lets you control how you launch and manage the editor - you can open files, install extensions, and output diagnostics through command-line options

- Today, we're thrilled to share our enhanced code CLI that lets you both launch VS Code and connect to a machine remotely from VS Code Desktop or vscode.dev.

- ## 🚀 [The Visual Studio Code Server | Hacker News _202207](https://news.ycombinator.com/item?id=32024882)

- [The VS Code Server _202207](https://code.visualstudio.com/blogs/2022/07/07/vscode-server)
- VS Code is, by design, a multi-process application. 
  - the front end (where you type your code) runs in one process and a backend service (which hosts extensions, the terminal, debugging, etc.) runs in a separate process.
  - Today we are releasing a private preview of the backend service that makes this all possible, the "VS Code Server, " along with a CLI that makes it easy to install, update, manage, and connect to the service. 
  - You can install the server wherever you like (a local development machine, a VM in the cloud, etc.) and access it securely through the browser using VS Code for the Web (also known as vscode.dev), without the hassle of setting up SSH or https (although you can do that if you want as well ).

- 👷🏻 Creator of the original https://github.com/coder/code-server 
  - Microsoft’s code-server uses their official extension marketplace, allowing LiveShare, Pylance, and other proprietary extensions in their browser VS Code experience. 
  - Their license prevents users from “hosting it as a service” meaning you can’t productize their code-server like you can ours.
  - We’re disappointed that Microsoft chose to release under the `code-server` command-line name.
  - We will continue developing our code-server until Microsoft’s has parity. As for Coder, we’re focusing more on the platform side (https://github.com/coder/coder) and less on making IDEs work remotely.

- Worth mentioning that gitpod's openvscode-server is a third option. I prefer it to code-server since gitpod's has proper parity with a desktop vscode install, while coder's implementation fails to work with several plugins when loading them in manually

- If you haven't seen it already coder has a nice VS code server instance that runs like a traditional self-hosted server app and could likely be run in an airgapped environment
  - This Microsoft version also has a self-hosted version (use the serve-local command).

- There's also remote-oss, which is fairly low-level (you have to install it on), but doesn't require you to pass your traffic through the GitHub proxy that Microsoft's service requires (I believe) and is also truly open source (which means, for example, that it can also be used with Codium, not just the Microsoft's VS Code distribution).
  - https://github.com/xaberus/vscode-remote-oss

- Will Microsoft open source this ?
  - The server component was already open sourced (this is the -same- server/remote component that was previously powering all of the remote development extensions). It's here in the main vscode repo (https://github.com/microsoft/vscode/tree/main/src/vs/server).
- Open VS Code Server takes this barebones implementation and fleshes it out enough to be minimally usable: https://github.com/gitpod-io/openvscode-server (i.e. run it from a CLI command, do basic token auth, etc.)
  - Coder's code-server (what you link) is similar to open vs code server but predates it and has a bit nicer server implementation, like it can be configured to run behind a reverse proxy or under different web paths more easily.
- For anyone that stumbles upon this later, I strongly recommend gitpod's openvscode-server container over coder's code-server. Linuxserver.io has docker containers for both.
  - openvscode-server has had 1:1 parity with a full desktop install of vscode, while coder's variant always had issues with several official plugins.
  - In coder's implementation several menu options will trigger caught exceptions for basic shit like opening a jupyter notebook, typescript language server frequently crashing, environment variables not being set properly in the correct order of priority, etc.
  - Note that with both implementations the easiest way to get access to the microsoft plugins store is to compile it from source and modify preferences.json. Open source maintainers technically cant distribute it this way out of the box due to Microsoft's licensing requirements. Alternatively, you can always just download the extensions in your browser and drag and drop them into your vscode server window and install them that way.

- Install vim and use it over SSH is the easiest and most direct approach. Since the editor runs in text mode it's perfectly happy to work over SSH. Use tailscale and you can get secure, global access from anywhere like they seem to do with vscode.dev creating a tunnel (tailscale even just added explicit SSH support)

- code-server also lets you customize the marketplace URL at runtime.
# discuss-coder-server
- ## 

- ## 

- ## 

- ## 这玩意比巨硬自家的好用啊 _202308
- https://x.com/VincentMucid/status/1690977433326145536
- copilot在这上安装不了有什么办法嘛, 万事俱备就差个tab辅助了
- 似乎能干掉笔记本上的WSL2了

- 其實巨硬自己的更“好用”，它可以訪問原生的插件商店。但是這個第三方的，商店是自己的，有一些API是不兼容的，例如權限管理的部分，導致它不能用copilot之類的。我其實兩個都在用，我還給 code-server 打過些布丁。不過這個第三方的目前比微軟自己的還穩定, 微軟的tunnel 經常掛，issue已經數不清了。

- 前段时间重度使用过，体验挺不错，但有个缺点，所有需要登录的插件都仅限当前会话，重启浏览器后就要重新登录，比如Codeium。 还有Copilot没法使用。 最后还是回到了vscode ssh

- 搭建没问题，主要是微软的插件都是私有的，不能迁移过来

- ## [Using code-server with nginx and base path appended _202005](https://github.com/coder/code-server/discussions/1739)
- if code server doesn't have the ability to set base path, you can always setup nginx to rewrite requests.
- Makes sense, all our links are relative otherwise so that's why --base-path was removed.

- ## TLDR: code-server is for individuals, Coder is for teams _202309
- https://x.com/bpmct/status/1699125288410501518
  - https://www.coder.com/blog/exploring-code-server-and-coder-unleashing-the-power-of-web-based-development-en

- ## [Move vendored VScode to separate fork · coder/code-server _202107](https://github.com/coder/code-server/issues/3835)
  - We’ve since migrated a large portion of our code base to a VS Code fork, which I feel better aligns with Microsoft's conventions to code implementation and organization

# discuss-openVscode-server
- ## 

- ## 

- ## 

- ## 🚀 Introducing OpenVSCode Server - an open-source project that makes running VS Code in a browser accessible for all devs & orgs. _20210928
- https://x.com/gitpod/status/1442839494772891654
- 🆚️ what are the differences to @CoderHQ which already gives us VS Code in the browser?
  - With nightly builds OpenVSCode Server is as upstream to @code as possible and in contrast to other forks only adds a minimal set of changes

- this is what could replace Theia as the Cloud Shell Editor.

- If you’re worried about not being able to use Live Share when you switch to OpenVSCode Server, don’t be. With CodeTogether you can live share between your browser VS Code instances and desktop IDEs built on VSCode, Eclipse, or IntelliJ.

- 
- 
- 

# discuss-remote-actions
- ## 

- ## [A Whole New Quick Edit in Cloudflare Workers | Hacker News _202305](https://news.ycombinator.com/item?id=35975268)
- > how does this work at a high level? 
  - We embed VSCode for Web in the Cloudflare dashboard as an iframe, and communicate with it over a MessageChannel. 
  - When the iframe is loaded, the Cloudflare dashboard sends over the contents of your worker to a VSCode for Web extension. This extension seeds an in-memory filesystem from which VSCode for Web reads. 
  - When you edit files in VSCode for Web, the updated files are sent back over the same MessageChannel to the Cloudflare dashboard, where they’re uploaded as a previewed worker to Cloudflare's global network.

- ## [Ask HN: Best practices for editing remote code locally? | Hacker News _202204](https://news.ycombinator.com/item?id=30987770)
- VS Code + The Remote SSH extension is a remarkable solution to developing code (not just editing!) on a remote machine.
- I like vscode + remote ssh a lot, but one thing to be aware of is that the node server that it installs on the remote can be a bit memory hungry if you're on a small machine (i.e., low-end droplet or vps). One of the rsync or sftp remote adapters is much nicer to such environments.

- VS Code (now) has a super nice support for jupyter. You don't have to start the server externally, vim mode and all your extensions like github copilot work fine, proper autocompleting works, etc. Debugging is absolutely amazing. I've recently switched myself and am never going back to browser-based jupyter.

- Visual Studio Code Remote SSH? https://code.visualstudio.com/docs/remote/ssh it will however install VS Code Server on target machine. So, for permanent development it is good. Not great if you only want to change one config file in PROD environment.

- Since I like my local development environment, I mostly use `sshfs`.
  - It mounts a remote directory onto a local directory and lets you access remote files as if they're local, with slight latency. Then you can use whatever tools you use locally to edit/compile/run the software.
- I also use this setup. Works well for editing and reading the files. But be aware that some file-intensive operations don't work as well. It is better to grep or git in the remore server instead of in the local mount. Be careful if your shell prompt is configured to show git status, because that won't be instantaneous.
- JetBrains never works on sshfs as it parses files for dependencies.
  - Actually, you're right. I just tested recursively grepping a remote directory with a thousand 16KiB files. The speed is completely catastrophic
- I think it's because it's not simply a file download but instead keeps on asking for file content or meta data making a roundtrip on each files to cause excessive latencies against many files. All the tools are basically designed to work on local files and they tend to work bad interacting directly on mounted file systems.

- Yeah code-server is really nice and underrated as a remote coding option. The linuxserver.io docker container for it is super fast and easy to setup: https://docs.linuxserver.io/images/docker-code-server

- Couple of solutions (some already mentioned):
  - SSH remote editing (e.g. ssh + remote Emacs/Vim)
  - VS Code + Remote SSH
  - Emacs TRAMP
  - JetBrains Gateway
  - mutagen?
- Many editors support the rmate protocol, enabling you to open a remote file from a ssh session in your local editor.

- While there are plenty of other more powerful solutions suggested here, I prefer my fairly light weight option - WinSCP connecting to the remote server over SFTP, then opening the files I want to change in my preferred editor (Sublime Text). 
  - WinSCP handles uploading file changes to the remote server automatically; there might also be a way to trigger actions on upload, but that gets into specifics of how your codebase is setup / what you need to run to test changes. 
  - Bonuses of using WinSCP are drag-and-drop file transfers, and a pretty thorough site manager (/address book / credential storage / login manager, whatever you want to call it).
# discuss
- ## 

- ## 

- ## 

- ## [Show HN: Lapdev, a new open-source remote dev environment management software | Hacker News _202403](https://news.ycombinator.com/item?id=39801399)
  - It's installed on a remote server so it provides remote environments. If you use VSCode remote, then you can "open" it through VSCode remote ssh. The environment that Lapdev provides essentially is a container (other format is on the roadmap) with things pre-installed as defined in Devcontainer(https://containers.dev/) format.

- This isn’t open source; one of the directories is licensed under a proprietary, subscriptionware nonfree license. The remainder is AGPL, which many people (including myself) consider nonfree as well.

- A lot of remote dev environments have limitations when it comes to certain types of development. For example, ios and android app development can be tricky. Or game development where you need to have GPUs and build artifacts may be slow to download to your machine.
  - Founder of coder (https://github.com/coder/coder) here. We choose Terraform as our provisioning layer so that users can provision full blown VMs as their development environment. We have many teams using GPUs with Coder for ML workloads but doing GUI/Game remote development where interactivity is essential remains elusive.
- You can access GPUs within containers using CDI (Container Device Interface)

- 
- 
- 
- 

- ## [Ask HN: Other than VS Code, are there any good IDEs for remote development? | Hacker News _202403](https://news.ycombinator.com/item?id=39732329)
- Emacs + tramp to use local editor. Maybe not quite as good as VS-code's client/server based tools, but I believe tramp does not require any special software to be installed on the server so it pretty much always works.

- ## [Visual Studio Code is designed to fracture(折断；断裂；破裂) (2022) | Hacker News _202409](https://news.ycombinator.com/item?id=41691577)
- > Extensions are not sandboxed
  - Extensions often rely on third-party binaries (such as Language Servers, kubectl, ssh or even git itself), internet access (SAAS providers, pulling data or definitions, ...) and on your filesystem (SSH Config, Kubernetes config, Config folder in your home, ...). Sandboxing these extensions is not easy unless everything is configured within VSCode which is rarely the case.
  - As far as I know, extensions are not sandboxed either on Emacs, (Neo)vim, Jetbrains IDEs.
- Extensions (in Emacs lingo we call them 'packages') are not sandboxed by design. Because unlike VSCode, you are allowed to override any, just about any part of a package's code. You can, for example, grab a command introduced in a third-party or a built-in package and override only specific parts of it without having to rewrite the entire thing.
  - Of course, in many cases that can make your entire setup brittle - i.e., what happens when the package author decides to change some functionality that you carefully and tightly integrated into your system? At the same time, there's enormous, unmatched flexibility for making your own rules of the game - there's nothing that comes even close. 
- Sandboxing does not come for a free, as it creates more complex development APIs and a performance hits.

- ## [deVStudio – Runs VS Code on Android | Hacker News _202309](https://news.ycombinator.com/item?id=37397359)
- My only concern is the memory management -- vscode (and its extensions) is not super friendly in its memory usage, and on a phone/tablet the RAM could easily run out, even if swap is enabled.

- 💡 From the screenshots this seems to use an X/VNC server or something, it might be good to also explore using https://github.com/coder/code-server with a native Android browser to get things like graphics acceleration (though with disadvantages like not being about to develop graphical applications)

- My biggest gripe with vscode on Android (code-server pwa on DeX) is lack of mouse hover and text selection. With so much intellisense hidden behind mouse popovers not having access to that is a bit of a show stopper.

- the irony that you can't run Android Studio on Android, but can run VS Code?

- ## [Coding on iPad using self-hosted VSCode, Caddy, and code-server | Hacker News _202409](https://news.ycombinator.com/item?id=41448412)
- JupyterHub and BinderHub can spawn containers that also run code-server. Though repo2docker and REES don't yet support devcontainer.json, they do support bringing your own Dockerfile.

- ## [How OpenVSCode Server turns VS Code into a web IDE | Hacker News _202109](https://news.ycombinator.com/item?id=28685978)
- VS Code in the browser doesn't support terminals or debugging. For that you need either code-server, this project, Gitpod, or GitHub Codespaces.

- 🆚️ How is this different from https://github.com/cdr/code-server ?
  - the goal of OpenVSCode Server is to make as few changes to VS Code as possible to run it on the server, while code-server makes more opinionated changes
  - Essentially, we run nightly builds at OpenVSCode Server making it as upstream to VS Code as possible. In contrast to other forks the whole scope of the project is to add a minimal set of changes 
  - The architecture we use powers both Gitpod and GitHub Codespaces. Several of the devs and organisations that have asked for our implementation & now have adopted OpenVSCode Server

- Can multiple people edit the files together? How is concurrency handled?
- How does it handle multi tenancy? Do you need one container per environment?

- If it runs on someone else's server, they monitor everything. I have a similar concern with most productivity apps on the web, tbh.

- ## [VS Code in the Browser for Everyone | Hacker News _202109](https://news.ycombinator.com/item?id=28682477)
- 🆚️ how it is different from code-server 
  - we run nightly builds at OpenVSCode Server making it as upstream to VS Code as possible. In contrast to other forks the whole scope of the project is to add a minimal set of changes 
  - The architecture we use powers both Gitpod and GitHub Codespaces. Several of the devs and organisations that have asked for our implementation & now have adopted OpenVSCode Server 

- Is it for projects which are not hosted on github, which can be accessed using github.dev?
  - github.dev is solely the VSCode frontend/editor without access to any compute. OpenVSCode Server allows you to run VS Code on a remote machine and access it with a thin client through the browser. Unlike github.dev you get full access to the underlying OS and can run tests, compilation, install dependencies etc.

- VSCode Liveshare addon is the best experience for collaborative coding I’ve found so far.

- ## Having integrated and maintained theia on production for 4 years, I wouldn’t recommend it. They always play the catchup game with VSCode. _202306
- https://x.com/aaqaishtyaq/status/1667631785298239488
  - I would suggest going with openvscode-server for better VSCode and extensions compatibility.
  - I miss the extensibility of theia though. You can really change everything in the IDE just using extensions (Dependency Injection), whereas with VSC, it is much more involved process. 
  - However, the tradeoff comes to VSCode extensions (theia calls them plugin) compatibility.
