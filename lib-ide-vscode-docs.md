---
title: lib-ide-vscode-docs
tags: [docs, vscode]
created: 2024-12-01T18:13:30.550Z
modified: 2024-12-01T18:13:48.944Z
---

# lib-ide-vscode-docs

# guide

- resources
  - [Basic editing in Visual Studio Code](https://code.visualstudio.com/docs/editor/codebasics)
# overview

# docs

- 
- 
- 
- 

## layout

- vscode user interface is divided into five main areas:
- Editor - The main area to edit your files. 
  - You can open as many editors as you like side by side vertically and horizontally.
- Primary Side Bar - Contains different views like the Explorer to assist you while working on your project.
- Activity Bar - Located on the far left-hand side. 
  - Lets you switch between views and gives you additional context-specific indicators, like the number of outgoing changes when Git is enabled. 
- A Secondary Side Bar is also available to display views opposite the Primary Side Bar.
- Status Bar - Information about the opened project and the files you edit.
- Panel - An additional space for views below the editor region. 
  - By default, it contains output, debug information, errors and warnings, and an integrated terminal. 
  - The Panel can also be moved to the left or right for more vertical space.

## [Visual Studio Code Server](https://code.visualstudio.com/docs/remote/vscode-server)

- The Visual Studio Code Server is a service you can run on a remote development machine, like your desktop PC or a virtual machine (VM). 
  - It allows you to securely connect to that remote machine from anywhere through a local VS Code client, without the requirement of SSH.
- We now provide a standalone "VS Code Server, " which is a service built off the same underlying server used by the remote extensions, plus some additional functionality, like an interactive CLI and facilitating secure connections to vscode.dev.

- The CLI establishes a tunnel between a VS Code client and your remote machine. Tunneling securely transmits data from one network to another.

- 🐛 Is the VS Code Server designed for multiple users to access the same remote instance?
  - No, an instance of the server is designed to be accessed by a single user.
- Can I host the VS Code Server as a service?
  - No, hosting it as a service is not allowed, as specified in the VS Code Server license.

- 
- 
- 
- 
- 
- 

# licensing
- some extensions like Wallaby.js, Google Cloud Code, and the VS Code Remote Development extensions use proprietary licenses.
# more
