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
- https://github.com/kiwix/kiwix-js-pwa /231Star/GPL/202601/js
  - Kiwix JS Offline Browser implemented as a Progressive Web App (PWA), and packaged as Electron, NWJS and UWP apps for Windows and Linux
  - this app is available either as an offline-capable, installable Progressive Web App (PWA), for almost all modern browsers and devices, or else as app packages for various Windows, Linux and macOS
  - For iOS and Android, use the offline PWA.
  - We also have packaged apps of WikiMed by Kiwix (a complete medical encyclopaedia), and Wikivoyage by Kiwix (a complete travel guide) in English -- no extra download needed

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

## discuss-spell-checker

- https://github.com/streetsidesoftware/cspell-dicts /GPL
  - Various cspell dictionaries. Each dictionary is its own package. 
  - ⚖️ 词典文件.txt 是 MIT
  - https://github.com/streetsidesoftware/cspell-dicts/blob/main/dictionaries/software-terms/dict/softwareTerms.txt

- https://github.com/bartosz-antosik/vscode-spellright /377Star/MIT/202410/js/cpp
  - Multilingual, Offline and Lightweight Spellchecker for Visual Studio Code
  - spells plain text/markdown/LaTeX
  - Case sensitive 
  - Small memory & CPU usage footprint - uses offline, OS native spell checking backends: Windows Spell Checking API (windows 8/10), NSSpellChecker (macOS) and Hunspell (Linux, Windows 7).
  - Extension uses background processing (on idle) and differential edit notifications to minimize area spelled during editing only to lines touched by changes.
  - 🤼 实测内存占用比cspell还大, 后面测试内存占用又变小了
  - 关闭`add to system dictionary`时, 单词会添加到 `~/Library/Application Support/Code/User/spellright.dict` 文件
    - 开启`add to system dictionary`时, 单词会添加到 `~/Library/Group Containers/group.com.apple.AppleSpell/Library/Spelling/LocalDictionary/en` 文件
  - 🐛 limitations
    - There is a limit, imposed by VSCode, on the number of diagnostics that an extension (Spell Right among) can provide for one file. The number is 1000
    - Due to bug in `NSSpellChecker` layer of macOS Spell Right cannot currently use dictionaries installed in `~/Library/Spelling` folder
  - [Chinese dictionary doesn't work on Win10 _202003](https://github.com/bartosz-antosik/vscode-spellright/issues/352)
    - I have to use `"spellright.ignoreRegExps": [ "/[\u4e00-\u9fa5]/g" ]`,  to ignore checking Chinese characters now, just to avoid seeing the wavy lines filling my screen
    - Confirmed. There's an issue with Asian languages. The Asian languages use a Microsoft IME keyboard while the other languages don't. Windows obvious handles Asian languages very differently behing the curtain.

- https://github.com/hunspell/hunspell /2.3kStar/MPL/202507/cpp
  - https://hunspell.github.io/
  - Hunspell is the spell checker of LibreOffice, OpenOffice.org, Mozilla Firefox & Thunderbird, Google Chrome, and it is also used by proprietary software packages, like macOS, InDesign, memoQ, Opera and SDL Trados.
  - It is designed for quick and high quality spell checking and correcting for languages with word-level writing system
  - https://chromium.googlesource.com/chromium/deps/hunspell_dictionaries/+/refs/heads/main
  - https://cgit.freedesktop.org/libreoffice/dictionaries/tree/
  - [OpenOffice Spell Checking and Dictionaries](https://www.openoffice.org/lingucomponent/dictionary.html)
  - [How about Chinese/Japanese support? _201706](https://github.com/hunspell/hunspell/issues/502)
    - Chinese/Japanese words (after being separated) cannot be checked directly based on edit distance.
    - 🤔 Applications that use Hunspell break a sentence into words and check those words. For Chinese and Japanese, this will most of the cases result in single-character words. For the cases where it concerns multi-character words, you (or the application using Hunspell) should be able to make this distinction and filter out those words and feed only those to Hunspell. Hunspell itself is not built for this, unless a space or punctuation is used.
    - I tried Language Tools. But unfortunately, Chinese has very incomplete support in LanguageTool and there is nobody taking care of it.

- https://github.com/languagetool-org/languagetool /13.6kStar/LGPL/202509/java
  - https://languagetool.org/
  - Open Source proofreading software for English, Spanish, French, German, Portuguese, Polish, Dutch, and more than 20 other languages
  - https://github.com/davidlday/vscode-languagetool-linter /apache2/202412/ts/inactive
    - A from scratch redesign of LanguageTool integration for VS Code
    - Support Markdown, MDX, HTML, and plain text files.
    - Option 1: Use an External Service
    - Option 2: Use an Extension-Managed Service
    - Option 3: Public API Service
  - https://github.com/valentjn/vscode-ltex /MPL/202111/python/ts/inactive

- ## 

- ## 

- ## 

- ## 

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
