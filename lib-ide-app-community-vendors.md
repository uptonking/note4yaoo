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

- ## 

- ## 
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
