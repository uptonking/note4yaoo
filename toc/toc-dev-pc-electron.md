---
title: toc-dev-pc-electron
tags: [electron, toc]
created: 2021-01-16T20:49:44.833Z
modified: 2021-01-16T20:50:23.893Z
---

# toc-dev-pc-electron
- tips
  - 不建议基于electron实现自定义浏览器，要考虑支持各浏览器自带的扩展商店，可在自己的应用层实现

- ref
  - search: file
  - https://github.com/sindresorhus/awesome-electron
# popular
- https://github.com/Elanis/web-to-desktop-framework-comparison
  - to create an objective comparison of multiple framework that grant us to "transform" our web app to desktop application formats.

- https://github.com/microsoft/vscode
  - https://code.visualstudio.com/
  - Visual Studio Code
- https://github.com/eclipse-theia/theia
  - https://theia-ide.org/
  - Eclipse Theia is a cloud & desktop IDE framework implemented in TypeScript
  - Theia embraces many of the design decisions and even directly supports VS Code extensions.
- https://github.com/jiahaog/nativefier
  - Make any web page a desktop application
- https://github.com/jgraph/drawio-desktop
  - Official electron build of diagrams.net
  - drawio-desktop is a diagrams.net desktop app based on Electron.
  - draw.io is the old name for diagrams.net
- https://github.com/Foundry376/Mailspring
  - maintained fork of @nylas Mail by one of the original authors.

- https://github.com/low-teck/vault
  - A react-electron app that secures user data locally using AES algorithm with the help of nedb and crypto-js ans styled with chakra-ui.
  - https://github.com/codegiik/electron-react-nedb-boilerplate

- https://github.com/wavebox/waveboxapp
  - https://wavebox.io/
  - Browser for Work
  - Wavebox gives you customizable toolbars, sleeping tabs, cookie containers and multiple profile
  - Wavebox 10, a complete fork of Chromium launched in 2019, but if you're looking for the Electron based Wavebox Classic, there's an archive of the code here

- https://github.com/samuelmaddock/electron-browser-shell /ts
  - A minimal, tabbed web browser with support for Chrome extensions—built on Electron.
  - forks
  - https://github.com/fvulich/electron-chrome-extensions
# utils
- https://github.com/alexiusacademia/electron-db
  - let you simplify database creation and operation on a json file.
# extensions
- https://github.com/sindresorhus/electron-store
  - Simple data persistence for your Electron app or module
    - Save and load user preferences, app state, cache, etc

- https://github.com/weolar/miniblink49
  - 一个小巧、轻量的浏览器内核，用来取代wke和libcef
# boilerplate
- https://github.com/ccorcos/electron-architecture /4Star/CC0-1/202108/ts
  - This project is a boilerplate electron app with a thoughtfully designed architecture
  - Main and renderer processes manage state using a Redux-like state machine.
  - Electron BrowserWindows are controlled declaratively through the application state.
  - Electron IPC uses a Proxy enabling "Rename Symbol" and "Find All References" in VSCode.
- https://github.com/ccorcos/electron-boilerplate
  - uses TypeScript and demonstrates using a preload script to interact with the native APIs.

- https://github.com/electron-react-boilerplate/electron-react-boilerplate
  - https://electron-react-boilerplate.js.org/
  - Electron React Boilerplate uses Electron, React, React Router, Webpack and React Fast Refresh.
  - https://github.com/codegiik/electron-react-nedb-boilerplate
- https://github.com/sprout2000/electron-react-ts
  - An Electron boilerplate with hot reloading for React and TypeScript.
- https://github.com/fantasticit/electron-react-boilerplate
  - 各窗口均采用 React 开发，也可根据需要更改为其他框架
  - 支持多窗口：修改 erb.config.js 中 windows 配置
  - 支持 Touchbar、Tray、Dock
  - 支持更新
- https://github.com/Devtography/electron-react-typescript-webpack-boilerplate
  - Ready to use Electron project template with React, Webpack and TypeScript seamlessly integrated
  - electron-builder for app packaging, with basic build config for Windows macOS included.
- https://github.com/codesbiome/electron-react-webpack-typescript-2022
  - Electron React Webpack Typescript Boilerplate with Custom Window and Titlebar Menus.

- https://github.com/garrylachman/ElectroCRUD
  - ElectroCRUD is Open Source Database CRUD (Create, Read, Update, Delete) Software. No Code Needed

- https://github.com/ArcherGu/fast-vite-nestjs-electron
  - build vite + electron + nestjs projects. Build with Doubleshot, crazy fast!
  - https://github.com/Doubleshotjs/doubleshot
    - A split node backend and electron main process.
    - integrating the nodejs backend framework with electron to build a desktop application. 
# examples
- https://github.com/zonetti/zonote /202105/inactive
  - Cross-platform desktop note-taking app. 
  - Sticky notes with Markdown and Tabs. All in one .txt file.

- https://github.com/pkolchanov/tablesapp
  - Tablesapp is an local-first table design tool.
  - All tables are ready for one-click cloud sharing. Hosted on Google Firebase.
# tauri
- https://github.com/12joan/ping-ui
  - A simple GUI for the ping command-line utility built using Tauri.
  - Requires ping to be in the PATH and for the output of ping to have the following format
# nwjs
- https://github.com/nwutils/electron-to-nwjs /js
  - This project aims to build an Electron app as a NW.js app.
  - The Electron main file is converted into the NW.js main file using webpack, by replacing the Electron modules with compatibility layers that make them use the NW.js commands instead. 
# more
- https://github.com/uptick/react-keyed-file-browser
  - https://uptick.github.io/react-keyed-file-browser/
  - Folder based file browser given a flat keyed list of objects, powered by React.
  - 文件浏览器的ui
