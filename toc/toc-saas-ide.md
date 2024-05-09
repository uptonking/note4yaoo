---
title: toc-saas-ide
tags: [ide, pm, toc]
created: 2020-08-18T09:18:24.127Z
modified: 2021-05-14T15:06:46.615Z
---

# toc-saas-ide

# ide-local

- vscode
- atom
- visual studio
- intellij idea
- eclipse
- geany
- jedit
- qt-creator
  - https://github.com/mervick/Qt-Creator-Darcula
- hbuilder
# ide-cloud
- eclipse-theia-ide
  - https://theia-ide
  - VSCode和Theia用的都是Monaco editor
  - VSCode虽然也是开源的但是他对第三方的支持不是很好

- https://github.com/gitpod-io/gitpod /AGPLv3/202405/go/java/ts
  - https://www.gitpod.io/
  - The developer platform for on-demand cloud development environments to create software faster and more securely.
  - Run any language on a full Linux VM complete with terminals, GitHub and Git integration
  - 支持生态: gitlab

- https://github.com/coder/coder /AGPLv3/202405/go
  - https://coder.com/
  - Coder enables organizations to set up development environments in their public or private cloud infrastructure.
  - Cloud development environments are defined with Terraform, connected through a secure high-speed Wireguard® tunnel, and are automatically shut down when not in use to save on costs.
  - Define cloud development environments in Terraform: EC2 VMs, Kubernetes Pods, Docker Containers, etc.
  - The most convenient way to try Coder is to install it on your local machine and experiment with provisioning cloud development environments using Docker (works on Linux, macOS, and Windows).
  - Coder/Coder is AGPL. Coder/Code-Server is MIT

- https://github.com/loft-sh/devpod /MPLv2/202405/go
  - https://devpod.sh/
  - Codespaces but open-source, client-only and unopinionated: Works with any IDE and lets you use any cloud, kubernetes or just localhost docker.
  - DevPod is a client-only tool to create reproducible developer environments based on a devcontainer.json on any backend. 
  - Each developer environment runs in a container and is specified through a devcontainer.json. 
  - Through DevPod providers, these environments can be created on any backend, such as the local computer, a Kubernetes cluster, any reachable remote machine, or in a VM in the cloud.
  - DevPod reuses the open DevContainer standard (used by GitHub Codespaces and VSCode DevContainers) to create a consistent developer experience no matter what backend you want to use.
  - No vendor lock-in: Choose whatever cloud provider suits you best, be it the cheapest one or the most powerful, DevPod supports all cloud providers. 
  - Cross IDE support: VSCode and the full JetBrains suite is supported, all others can be connected through simple ssh.

- https://github.com/eclipse-theia/theia /EPLv2/202405/ts
  - http://theia-ide.org/
  - Theia is a cloud & desktop IDE framework implemented in TypeScript.
  - Eclipse Theia is an extensible framework to develop full-fledged multi-language Cloud & Desktop IDE-like products with state-of-the-art web technologies.
  - Support VS Code Extension protocol

- https://github.com/codenvy/codenvy /EPL/201802/java/inactive
  - Cloud workspaces for development teams. One-click Docker environments to create workspaces with production runtimes. 

- https://github.com/eclipse-che/che-theia /EPLv2/202303/ts/archived
  - Eclipse Che provides a default web IDE for the workspaces which is based on the Theia project. 
  - It’s a subtle different version than a plain Theia as there are functionalities that have been added based on the nature of the Eclipse Che workspaces. 
  - We are calling this version of Eclipse Theia for Che: Che-Theia.
  - So, Che-Theia is the default Che editor provided with developer workspaces created in Eclipse Che 7
  - Che-Theia contains additional extensions and plugins which have been added based on the nature of Eclipse Che workspaces and to provide the best IDE experience of Theia within Che.

- https://github.com/wasdk/WebAssemblyStudio /MIT/201901/ts/inactive
  - http://webassembly.studio/
  - Run C, Rust, Wat, or AssemblyScript code as WebAssembly in the browser.

- https://github.com/Atheos/Atheos /202402/php/js
  - https://www.atheos.io/
  - Atheos is an updated and currently maintained fork of Codiad, a web-based IDE framework with a small footprint and minimal requirements. 
  - Atheos has been completely rewritten from the original Codiad project to utilize more modern tooling, cleaner code, and a wider arrange of features.
  - https://gitlab.com/xevidos/codiad /202003/inactive
    - This is the Telaaedifex team's custom version of Codiad. 
# ide-paid
- sublime text
- ultra edit
# examples-ide
- https://github.com/withfig/autocomplete
  - https://fig.io/
  - IDE-style autocomplete for your existing terminal & shell
# discuss
- ## 
