---
title: lib-lowcode-tiddlywiki-community
tags: [cms, community, tiddlywiki, wiki]
created: 2023-11-14T16:09:12.446Z
modified: 2023-11-14T16:10:21.108Z
---

# lib-lowcode-tiddlywiki-community

# guide

# discuss
- ## 

- ## [TiddlyPWA: putting TiddlyWiki on modern web app steroids | Hacker News_202307](https://news.ycombinator.com/item?id=36885753)
- Tiddlywiki was great because it was a single file, the whole point of tiddlywiki was being a single self-modifying html file. No app needed.

- This effort is remarkable as the mobile side of saving is not as robust as on the desktop side of things and there is a scaling limit on performance as the number of tiddlers grows. Also the syncing between tw documents between different desktop/mobile clients can be a challenge with diffing.

- One of the main reasons I switched away from tiddly wiki was I needed better mobile support and syncing was always a monumental pain. Not to mention saving the HTML file was fundamentally broken in modern browsers at the time.

- I'd like to see a proper tiddlywiki in an Electron application. The one that exists now is quite ugly and annoying to use. Maybe what I really want is someone to re-imagine TW as something similar to Obsidian (or Obsidian->TW?)

- If you're on windows, you can give the tiddlywiki file an . HTA extension and it will behave like an HTML app. It does double the filesize due to encoding changes if I'm not mistaken but it works

- ## [TiddlyWiki 5.1.23 | Hacker News_202012](https://news.ycombinator.com/item?id=25527581)
- TiddlyWiki 5 has no feature or plugin to have revision history integrated into the UI, although one might come in the future
  - There is a plug-in for revisions, but it may be too simple for your needs?

- I'm interested in the idea of dividing information into smaller-than-a-normal-wiki-page 'tiddlers', and I like the UI design. Overall, I can't find any other software that quite matches TiddlyWiki's capabilities.

- It's hard to find a good solution since the main Tiddlywiki is built as a single-user rather than multi-user solution.

- What's the best way to persist state with TiddlyWiki? I really would like to save without any browser extensions.
  - I've found setting up the Git integration to be the best way

- Was a happy user of TiddlyWiki 5+ years ago but eventually left when adding too many pictures made that HTML file so bloated it could barely open.
  - There is lazy-loading now you can use with the server edition, but I don't like either that they're still served out as base64 embedded content. I suspect the most elegant solution is to have your images live hosted somewhere else, and just add references to them.

- ## [Tiddlywiki – A non-linear personal web notebook | Hacker News_201809](https://news.ycombinator.com/item?id=18107271)
- I personally think Tiddlywiki is a fascinating project and I even used it professionally for a few years. But, these days, I think you likely do better with either a Dropbox directory full of Markdown files or installing the free tool Simplenote everywhere (mobile/desktop) and using its support for notes/Markdown. 
  - It's true that if you go with these simple schemes, you lose wiki-style linking. But, I've found that YAGNI applies here.

- The only annoying thing are:
  - we need to press 2 carriage return to go to the next line
  - the markup languages are never standard. we use redmine with textile which is kinda compatible with TW, but not 100%

- I look at TW every couple of years or so, and there has never been either:
  - a sane way to keep a wiki on something like Dropbox (at the time, the only way to have persistence was to disable browser security and allow JavaScript to write to disk directly) or
  - a service to sync a wiki between machines
  - Has that changed nowadays?

- The most unique thing for me is the fact that it's an .html file that you can just download and run. The data/saving mechanism is completely separate. This "unhosted-ness" seems to be a growing trend.

- ## [TiddlyWiki: a local, single-page wiki | Hacker News_201701](https://news.ycombinator.com/item?id=13523660)
- I built a TiddlyWiki site for an RV park circa 2008. It was easy to do and looked great. It was easy for the non-technical owners to update. But Google completely ignored it, and so the park was invisible to most tourists. It folded a few years back, and I partly blame myself, for picking TiddlyWiki.
  - By now you can export static pages from it

- I am also a TiddlyWiki user. I use it as personal note taking + bookmarking + daily reading log. The best feature it has is a Wiki feature, not any TiddlyWiki feature: backlinks. I could make the backlinks show up in the footer of every page (tiddlers) and this reminds me connections I might have forgot. Tiddlywiki is also a great system for bookmarks. This is different from restrictive categories.
- Couple of problems I face:
  - No converter to convert files to other Wikis or formats
  - Static pages has awful URLS
  - Duplicate titles
  - Data corruption

- I think we still don't have a free opensource version of a personal wiki that supports the following:
  - 1. Easy copy and paste (or import) of Web pages (including embedded images) 
  - 2. Embedding and resizing images 
  - 3. No server requirement. 
  - 4. Cross platform 
  - 5. Extensible
# discuss-altertives-wiki
- ## 

- ## 
