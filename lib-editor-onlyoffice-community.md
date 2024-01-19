---
title: lib-editor-onlyoffice-community
tags: [editor, excel, microsoft-word, office-suite, onlyoffice, ppt]
created: 2024-01-19T18:27:14.649Z
modified: 2024-01-19T18:27:51.917Z
---

# lib-editor-onlyoffice-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

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
