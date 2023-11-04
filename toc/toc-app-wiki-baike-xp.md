---
title: toc-app-wiki-baike-xp
tags: [app, saas, wiki, xp]
created: 2020-10-05T07:51:09.046Z
modified: 2023-02-08T10:47:32.359Z
---

# toc-app-wiki-baike-xp

# guide

# spell-checker
- [LanguageTool - Online Grammar, Style & Spell Checker](https://languagetool.org/)
  - LanguageTool is your intelligent writing assistant for all common browsers and word processors. 
# wiki-mirror
- wikipedia
  - [Wikipedia (TheFreeDictionary.com mirror)](https://encyclopedia.thefreedictionary.com/)
# wiki-browser-extensions
- https://github.com/emir-munoz/wikitables
  - This project aims to extract relationships as RDF triples from tables found in Wikipedia's articles
  - 依赖java
# scholar
- google-scholar-mirrors
  - http://scholar.scqylaw.com/
# format-html-web
- https://kapeli.com/mdn_offline
  - These doc archives are supposed to be used without a documentation app, just by opening the files in your browser. 
  - If you'd like to use a documentation app, like Dash, you should download the docs from within Dash's Preferences and not from here.
# format-zim
- refs
  - https://library.kiwix.org/?lang=eng
  - 不方便修改编辑

- https://github.com/kiwix/kiwix-js /js/c
  - https://pwa.kiwix.org
  - https://browser-extension.kiwix.org/current
  - Fully portable & lightweight ZIM reader in Javascript
  - Kiwix JS is an official HTML5/Javascript implementation of the Kiwix software, principally targeting browser extensions or add-ons.
  - There is also a version, primarily intended for use within extensions, implemented as an offline-first Progressive Web App (PWA)
  - The Kiwix browser also works with other content in the OpenZIM format, but our main targets are Mediawiki-based content (Wikipedia, Wikivoyage, Wikitionary, etc.), StackExchange, Project Gutenberg and TED Talks.
- https://github.com/kiwix/kiwix-desktop /js/cpp
  - a viewer/manager of ZIM files for GNU/Linux and Microsoft Windows OSes.
  - 依赖qt、libkiwix
- https://github.com/kiwix/kiwix-js-windows
  - Kiwix JS Offline Browser for Windows and Linux, packaged as PWA, Electron, NWJS and UWP

- https://github.com/openzim/mwoffliner /GPLv3/ts
  - Mediawiki scraper: all your wiki articles in one highly compressed ZIM file
  - 依赖linux/mac环境、redis、libzim
  - MWoffliner is a tool for making a local offline HTML snapshot of any online MediaWiki instance.
  - It goes through all online articles (or a selection if specified) and create the corresponding ZIM file. 
  - **It has mainly been tested against Wikimedia projects like Wikipedia and Wiktionary** --- but it should also work for any recent MediaWiki.

- https://github.com/vss-devel/zimmer /js
  - nodejs ZIM file creator
# goldendict
- 全文索引fts的位置
  - ~/.var/app/org.goldendict. GoldenDict/cache/goldendict/index/

## discuss

- ## 

- ## 

- ## 

- ## 

- ## [GoldenDict always fully occupies 1 CPU core](https://github.com/goldendict/goldendict/issues/640)
- Have you read GD help about full-text search? It is FTS indexing process. Indexing statistic you can see in full-text search dialog.

- Can we cache results of the FTS indexing process to not start it again every time program runs?
  - It should be one time process. If the process was interrupted, it will continue, just give it time
  - You can disable Full Text Search in the Preferences (F4).

- ## [Indexing wikipedia zim - once and for all](https://github.com/goldendict/goldendict/issues/914)
- If your machine doesn't have enough memory to complete the indexing of wikipedia_nopic_201?.zim, use the following workaround:
  - set the limit indicated in the image above. somewhere between 2000000 and 10000000 should work. This eliminates FTS indexing for very large files.
  - anything between 2M and 10M should work. This reduces title indexing to be less extensive for files with more then 2M articles.
