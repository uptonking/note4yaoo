---
title: lib-editor-vscode-blog-ide
tags: [blog, ide, vscode]
created: 2024-05-09T09:39:24.099Z
modified: 2024-05-09T09:39:33.338Z
---

# lib-editor-vscode-blog-ide

# guide

# ide-products

## ide/cde

- https://github.com/styfle/awesome-online-ide
  - An "Online IDE" has the features mentioned above but runs in a web browser instead of installing as a native application.
  - AWS Cloud9, codenvy, Theia

## [Theia - Cloud and Desktop IDE Platform](https://theia-ide.org/)

- Cloud & Desktop
- designed in a modular way to allow extenders and adopters to customize and extend every aspect.
- vendor-neutral and developed by a diverse community.
- provides language support via LSP and DAP. Further, it can host VS Code extensions and provides full terminal access.
# blogs-vendors

## 

## 🆚️ [Comparing Coder vs. Codespaces vs. GitPod vs. DevPod _202309](https://loft.sh/blog/comparing-coder-vs-codespaces-vs-gitpod-vs-devpod/)

- Coder promotes itself as a “Self-Hosted Remote Development Platform” which is open source and focuses on “shifting software development from local machines to the cloud”. 
  - You provision the underlying infrastructure with Terraform on Kubernetes, Docker or VMs, as required. 
  - This can be done locally or remotely in the cloud. 
  - Coder does not offer a hosted solution, so everything is self-hosted.

- Codespaces is a Software as a Service (SaaS) remote development environment that hosts Docker containers on Azure VM. 
  - the product is the only one in the list that is not open source and is tied to GitHub, with limited 3rd party source-code host integration.

- GitPod was launched as a SaaS product in 2019, making it one of the early startups in this space. 
  - GitPod operates with containers on Kubernetes cluster on Google Cloud, but they require a `gitpod.yml` file instead of the `devcontainer.json` to be present which is the standard.
  - It can be difficult to switch to other tools, such as Codespace, Coder, and DevPod, because they rely on the devcontainer.json file. 
  - This can result in vendor lock-in since you would also need to migrate the instructions in gitpod.yml.
  - Also, the important to note that GitPod does not offer GPU options, making it less ideal for AI/ML workloads.

- DevPod is one of the latest projects in the ecosystem, which is an open source alternative to GitHub codespaces. 
  - It is also based on the `devcontainer.json` standard, so you can easily move your projects from Codespaces to DevPod without the need for modification.
  - The main advantage of DevPod is that it supports client-side development with the DevPod CLI (there is also a lightweight GUI version). 
  - This allows you to use any git repositories, as DevPod simply checks out your repos using git with the backend of your choice through providers.
  - DevPod works with the provider concept which defines how your target environment needs to be set up anywhere else. 
  - By using DevPod providers, you can create your dev environments on various backends - including your local computer, a Kubernetes cluster, any accessible remote machine, or a virtual machine in the cloud.

- GitPod and Codespaces are SaaS services that offer 50 free hours and 30 free hours, respectively, on standard 4-core machines, which is quite appealing. However, as a developer commits more hours and scales up, it can become more expensive, being approximately two times the price of Azure Compute Pricing.
  - Alternatively, solutions like Coder and DevPod provide the flexibility to pay for cloud and take advantage of committed usage discounts when needed or use the local system for simplicity. The tools themselves are free which allows for a more cost-effective and practical approach to managing costs as well as isolation, both in the cloud and locally.

- Coder and DevPod, can be used for VMs/Docker/Cloud which brings more components under your control. 

- Ease of Usage
- Coder requires everyone to understand a bit of Terraform and templates, since that’s how the infrastructure is deployed.there’s no internal API for provisioning VMs, which can be challenging to deploy on infrastructure with no Terraform providers.
  - GitPod and Codespaces are user-friendly platforms that require only a sign-up process for easy access. However, it is important to be mindful of data sharing and compliance when using them, as an internet connection is always required.
  - DevPod operates on native APIs, making it easy to interact with new providers and requiring no internet connection if you’re in an air-gapped environment. If you’re using a cloud provider then of course you’ll need the connection. One added benefit is that the complete client-side nature simplifies the process of propagating user-level secrets to the system and allows for easy development and testing both locally and on the cloud.

- if you’re using DevPod or Codespaces, they are only compatible with Multi Devcontainers support for mono repos, which can be necessary for some software teams.

- Team collaboration is crucial, and having the right tools to support development is essential and Codespaces and DevPod are at the forefront of the industry with their production devcontainer.json support.

- Coder also has a way to support community-provided providers, but it has a limitation with Terraform.
- The success of DevPod is indeed not unexpected, given the track record of the team at Loft Labs and their previous involvement in the open-source community. 
  - Their prior projects, such as vCluster and DevSpace, have been highly successful and have contributed significantly to the developer ecosystem.

## [Thanks Microsoft for open-sourcing VS Code Server _202111](https://www.gitpod.io/blog/vscode-server)

- After Gitpod launched OpenVSCode Server in September, Microsoft now open-sourced the server code powering VS Code remote development and GitHub Codespaces
  - Within a few days we switched Gitpod VS Code and OpenVSCode Server Insiders builds to the upstream implementation

- OpenVSCode Server adds some much-needed, yet minimal changes on top of VS Code to:
  - enable the marketplace using Open VSX
  - enable HTTPS and WebSocket Secure (wss) by default

## ⌛️ [gitpod: From Theia to OpenVSCode Server - A history of Cloud IDEs - Blog _202110](https://www.gitpod.io/blog/cloud-ide-history)

- We learned the intricacies of different desktop IDEs (Eclipse, IntelliJ, VS Code) and web editors (Monaco, Ace, Orion, and CodeMirror) - and eventually ended up building Gitpod.
- While IDEs are an important building block, platforms such as Gitpod are so much more. Think orchestration, provisioning, operating system, databases, compilers and all other tools you require to be productive.
- Back in late 2017 VS Code could not run in a browser and was not (yet) refactored to support remote development. 
- Because we wanted to offer a VS Code-like developer experience in Gitpod, we started the open-source project `Theia` under the roof of the Eclipse Foundation. 
  - The idea was to use VS Code technology (i.e. Monaco editor, LSP, DAP protocols, Xterm.js) to implement a vendor-neutral, remote-first IDE framework accessible from both browser and desktop. 
  - The framework was widely adopted by companies such as Gitpod, Google, Ericsson, SAP, RedHat, ARM, Arduino, and several others. 
  - While we at Gitpod moved to VS Code in late 2020 (more on that below), today Theia powers online IDEs such as Eclipse Che, Stackblitz, Google Cloud Shell Editor, Acquia Cloud IDE and several others.

- From the start the number one feature request for Theia was to support VS Code extensions out of the box.
  - Building that required a steep learning curve as you need to understand the semantics behind all VS Code extensions APIs and port them to Theia. 
  - By early 2020, Theia was compatible with the most important APIs.
- To fill that gap we built and released the Open VSX marketplace as an open-source alternative, which we also donated to Eclipse. 
  - Today OpenVSX has almost extension parity for the most popular VS Code extensions and is used by Gitpod, OpenVSCode Server, code-server, Eclipse Che and can be Self-Hosted on your own infrastructure.

- By 2020 the brilliant team behind VS Code added remote support and the web workbench ultimately powering github.dev was already open-sourced.
  - However, they decided to not open-source the server implementing the remote protocol. 
  - In summer 2020, while porting a new VS Code file system API in Theia, I began to understand how the internal remote protocols are working and decided to build a quick prototype for a server implementation of stock VS Code. 
  - After 4 days of focused work we had a first working version at the beginning of September. There were still many missing pieces (auto-sync settings, port forwarding etc.), but it became clear that we can run stock VS Code in Gitpod.

- Gitpod is an open-source orchestration and provisioning platform for developer environments. 
  - The goal was always to open Gitpod to all IDEs as soon as they support remote development
- I admit that it was a hard decision to stop supporting Theia after almost 4 years, but the maintenance and catch-up effort required to support the ever growing and changing API surface became increasingly a burden. 
  - And more importantly: Theia did not allow us to provide the best developer experience we could.
- We spent the next months polishing the server implementation and added missing pieces such as the setting sync server and port tunneling via the local companion app. 
  - In December 2020 we started giving users the choice between Theia and VS Code and officially switched to VS Code as the default editing experience in Gitpod in early 2021.
- our server implementation still was bound to Gitpod services. For example, we had a custom remote terminal implementation while MS open-sourced its pty service. 
  - After the requests became more and more frequent we decided to separate concerns and provide a clean-cut between the server and parts which we add to integrate with Gitpod. OpenVSCode Server was born.
  - Within several days we were joined by large companies such as GitLab, VMware, Uber, SAP, Sourcegraph, RStudio and SUSE. 
- By imposing constraints such as never changing Microsoft code, we enabled a straightforward, fully automated upgrade path
  - As the project’s scope is to keep the changes to upstream VS Code as minimal as possible we will not bloat the server, but (similar to upstream VS Code) use their extension model and external services to add missing functionality. 

- With Gitpod you can provision, automate and orchestrate those workloads for yourself and your team with the least friction possible. 

## [Gitpod is now Open Source - Blog _202008](https://www.gitpod.io/blog/opensource)

- Gitpod Self-Hosted is free for unlimited users. 
- Organisations using Gitpod Self-Hosted can purchase an enterprise license in order to get additional features like:
  - Snapshots (share a reproducible workspace with your team)
  - Live Share (invite others into your running workspace)
  - Unlimited Prebuilds (making ephemeral dev environments possible)
  - Admin Dashboard

## [A first look at the new GitLab Web IDE and remote development experience _202212](https://about.gitlab.com/blog/2022/12/15/get-ready-for-new-gitlab-web-ide/)

- A little while back I wrote about the future of the GitLab Web IDE and our decision to rebuild the Web IDE on top of the open source VS Code project
  - Today, I am happy to announce that we are preparing to launch the new Web IDE experience as a beta
- We're working on adding support for VS Code extensions and enabling project-wide search

- [The Future of the GitLab Web IDE _20205](https://about.gitlab.com/blog/2022/05/23/the-future-of-the-gitlab-web-ide/)
  - [Replace Web IDE with client-only VS Code (&7683) · Epics · GitLab.org · GitLab](https://gitlab.com/groups/gitlab-org/-/epics/7683)
    - Replace the current Web IDE, which is based on the open sourced Monaco editor, with a client-side instance of VS Code and implement custom extensions for creating commits and interacting with MRs.
# blogs

# more
