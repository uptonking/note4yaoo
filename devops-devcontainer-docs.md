---
title: devops-devcontainer-docs
tags: [dev-env, devcontainer, devops, docs]
created: 2024-05-22T04:20:59.910Z
modified: 2024-05-22T04:21:34.726Z
---

# devops-devcontainer-docs

# guide

- resources
  - [Developing inside a Container using Visual Studio Code Remote Development](https://code.visualstudio.com/docs/devcontainers/containers)
# blogs

## [配置VSCode的Dev Container - 知乎 _202305](https://zhuanlan.zhihu.com/p/627102373)

- 本地环境中有VSCode和项目源代码。开发者会在本地的VSCode中编写代码。之所以将源代码放在本地的文件系统中，因为我们将代码和容器分离，即使我们删除了容器，代码的修改也不会丢失。
- 容器除了包含编译/运行项目代码的环境之外，会挂载(mount)项目源代码，
  - 除了挂载源代码，我们很多时候还会挂载数据、编译结果输出文件夹、git credentials等等，VSCode的默认配置会替我们做了。
  - 容器中会有VSCode的服务端，服务端将相关信息传递给本地的VSCode，本地VSCode只有一个UI的功能。
  - 我们还可以在容器中安装相关的VSCode插件，由于开发环境全部都在容器中，和源代码有关的插件都被安装在容器中。
- 我们先来看看一个VSCode提供的一个样板项目vscode-remote-try-cpp。

- 
- 

## [“在我的电脑上明明可以的” — 图解 DevContainer 构建干净的开发环境 - 知乎 _202302](https://zhuanlan.zhihu.com/p/604545087)

- 可以通过 devcontainers.json 甚至 docker export 将开发环境分发给其他人，快速实现团队统一
- Github Codespaces 可以直接使用 devcontainers.json 配置，有条件的可以直接上云了
- 在开发容器中安装的插件只会关联到这个容器，可以避免大量插件出现的冲突
- 可以同时启动多个开发容器
- 一个开发容器中也可以创建多个项目
# docs
- devcontainer allows you to use a container as a full-featured development environment. 
  - It can be used to run an application, to separate tools, libraries, or runtimes needed for working with a codebase, and to aid in continuous integration and testing.
- As containerizing production workloads becomes commonplace, more developers are using containers for scenarios beyond deployment, including continuous integration, test automation, and even full-featured coding environments.

- `devcontainer.json` is a structured JSON with Comments (jsonc) metadata format that tools can use to store any needed configuration required to develop inside of local or cloud-based containerized coding.
  - dev container metadata can now be stored in image labels and in reusable chunks of metadata and install scripts known as Dev Container Features.
- Beyond repeatable setup, these same development containers provide consistency to avoid environment specific problems across developers and centralized build and test automation services.

- Development container “Features” are self-contained, shareable units of installation code and development container configuration. 
  - The name comes from the idea that referencing one of them allows you to quickly and easily add more tooling, runtime, or library “features” into your development container for you or your collaborators to use.
  - They are applied to container images as a secondary build step and can affect a number of dev container configuration settings. 

- The project workspace folder is where an implementing tool should begin to search for `devcontainer.json` files. 
  - If the target project on disk is using git, the project workspace folder is typically the root of the git repository.

- 
- 
- 

## Features

- Features are self-contained, shareable units of installation code and development container configuration.
  - Feature metadata is captured by a `devcontainer-feature.json` file in the root folder of the feature.
- A Feature is a self contained entity in a folder with at least a `devcontainer-feature.json` and `install.sh` entrypoint script
- Features are referenced in a user’s `devcontainer.json` under the top level `features` object.
  - A user can specify an arbitrary number of Features. At build time, these Features will be installed in an order defined by a combination of the installation order rules and implementation.

- `install.sh` script for each Feature should be executed as root during a container image build
  - This allows the script to add needed OS dependencies or settings 
  - This also allows the script to switch into another user’s context using the `su` command
  - It is recommended that Feature authors write install.sh using a shell available by default in their supported distributions (e.g., bash in Debian/Ubuntu or Fedora, sh in Alpine). 

- 
- 
- 

# more
