---
title: lib-excel-focalboard-community-stars
tags: [community, focalboard]
created: 2022-03-16T20:46:11.316Z
modified: 2022-08-21T09:56:48.062Z
---

# lib-excel-focalboard-community-stars

# discuss

- ## 

- ## [Focalboard Personal and Plugin Editions Announcement_20230430](https://github.com/mattermost/focalboard/discussions/4645)
- we’re reaching a point where we can no longer maintain multiple versions to the same standard. 
  - In order for us to continue to ship a high quality product, we’ll be focusing solely on the in-product version (formerly known as “plugin”) of Mattermost Boards. 
  - We’ll be transitioning Focalboard Personal Server and Personal Desktop editions to being fully community supported as of April 30th, 2023.
- The codebase for Focalboard Personal Editions was separated from the ongoing Mattermost Boards Plugin code on March 09, 2023.
  - The existing Focalboard repository will become the Personal Edition repository, and will remain open indefinitely. 
  - However, we won’t be adding any new enhancements

- ## [Focalboard – a self-hosted alternative to Trello, Notion, and Asana | Hacker News_20210318](https://news.ycombinator.com/item?id=26499062)
- you can find that Mac app is written in Swift: https://github.com/mattermost/focalboard/tree/main/mac and 
  - Windows application in C# uses WPF: https://github.com/mattermost/focalboard/tree/main/win-wpf
  - Linux app seems to be just a local server supposedly with web browser as an interface.
- Both these apps contain a few source files and all they do seem to be rendering and handling a webview. The "real" app seems to be this: https://github.com/mattermost/focalboard/tree/main/webapp.
