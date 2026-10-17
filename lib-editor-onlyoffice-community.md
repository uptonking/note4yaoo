---
title: lib-editor-onlyoffice-community
tags: [editor, excel, microsoft-word, office-suite, onlyoffice, ppt]
created: 2024-01-19T18:27:14.649Z
modified: 2024-01-19T18:27:51.917Z
---

# lib-editor-onlyoffice-community

# guide

# changelog
- [ONLYOFFICE Docs 8.1 released   _202406](https://www.onlyoffice.com/blog/2024/06/onlyoffice-docs-8-1-released)
  - Text editing: Included in BOTH Desktop Editors AND Document Server (web-based)
  - PDF forms: say goodbye to our DOCXF format
- [ONLYOFFICE Desktop Editors v7.5: a new PDF editor and more _202310](https://www.onlyoffice.com/blog/2023/10/onlyoffice-desktop-editors-v7-5)
  - open PDF files and perform basic editing operations, such as text annotating, form filling, commenting and drawing.
# discuss-stars
- ## 

- ## 

- ## 
# discuss-devops
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Host Onlyoffice what to choose : r/OnlyOffice _202402](https://www.reddit.com/r/OnlyOffice/comments/1at2be4/host_onlyoffice_what_to_choose/)
- What is the differene between Onlyoffice Groups and OnlyOffice Workspace?
  - ONLYFFICE Groups (also known as ONLYOFFICE Community Server) is a collaborative platform with a bunch of functional modules, such as Projects, Mail, Comunity, CRM, Talk, etc. However, it doesn't provide document editing features.
  - ONLYOFFICE Workspace is a productivity platform that combines ONLYOFFICE Groups and ONLYOFFICE Docs (ONLYOFFICE Document Server) and allows you to edit and collaborate on documents in real time. You can deploy Workspace and disable the modules that you don't need, such CRM, Community, People, Talk, etc.

- What is the difference between Document server and Community Server?
  - Community Server is another name for ONLYOFFICE Groups
  - Document Server is another name for ONLYOFFICE Docs, an online office suite
  - If you want to collaborate on documents in real rime, I suggest hosting ONLYOFFICE DocSpace. It's a relatively new product. It's a room-based collaborative platform that allows you to store, share, manage and collaborate on office files with other users. 

- you need to install Document Server. The community edition has a limit of 20 simultaneous connections where a connection is a browser tab with an open file. So you can reach the limit even with a single user id he keeps open 20 files in his browser.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## #OnlyOffice无意间发现了这么个产品，刚开始我以为是LibreOffice的一个商业版本的fork，看了一下wiki发现不是，这是个纯网页版本的办公软件和office兼容。
- https://x.com/imwsl90/status/1826470133835141274
- 比LibreOffice有一个好，有pdf编辑工具
- 这个结合nextcloud就可以私有化一个百度网盘加腾讯文档，非常合适小公司做私有化的云办公。

- ## [OnlyOffice: Free open source office suite with business productivity tools | Hacker News_202309](https://news.ycombinator.com/item?id=37701884)
- My only serious gripe with OnlyOffice is that when opening a CSV, you have to choose an encoding and delimiter, and there is no way to set a default. You must click twice, in two places, every single time you open a CSV.
  - You have to do this with Excel as well to avoid your data automagically being formatted and/or truncated.
- CSV is not a standard (rfc4180 exists but only very few things actually pay attention to it) so no behavior is a sane behavior when trying to import it.

- 🆚️ Anyone have a good comparison between this and LibreOffice?
  - OnlyOffice seems to be the only FOSS office suite that handles Microsoft Office documents correctly.
  - in my recent (less than a year ago) experiments both struggled with excel files in different ways (some content missing), so can't be trusted as a drop-in-replacement, at least not for already existing documents.
- Seems like Collabora and OnlyOffice are the two big players right now.

- You can also self-host Office
  - [Office Online Server | Microsoft Learn](https://learn.microsoft.com/en-us/officeonlineserver/office-online-server)
  - ⚖️ The protocol that connects the office suite to the file sharing platform is called WOPI
  - OneDrive/Dropbox/Nextcloud all seem to support it.

- @ONLYOFFICE, FYI to add bi-directional support (LTR, RTL and mixed) in Web interface is as simple to add to element `dir=auto`.
  - If I remember correctly, they are using canvas with custom rendering logic. Hence many native browser capabilities might not be available.

- ## [OnlyOffice is an alternative to LibreOffice | Hacker News_202009](https://news.ycombinator.com/item?id=24385532)
- One deal breaker for me regarding OnlyOffice is that they have absolutely no support for RTL
  - Softmaker on the other had does support RTL. They still have a long way to go to be at the level of Microsoft office, but they are the best Linux office suite that I found

- Unfortunately, OnlyOffice doesn't offer a Zotero integration tool. That's a huge deal breaker for any academic.
