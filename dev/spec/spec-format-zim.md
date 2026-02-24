---
title: spec-format-zim
tags: [format, wiki, zim]
created: 2023-07-05T10:22:42.846Z
modified: 2023-07-05T10:22:57.942Z
---

# spec-format-zim

# guide

- tips

- resources
  - [ZIM file format](https://wiki.openzim.org/wiki/ZIM_file_format)
  - https://library.kiwix.org/
# draft
- datasources
  - mozilla mdn docs 未提供 zim 格式
# spec

- 

## [OpenZIM](https://wiki.openzim.org/wiki/OpenZIM)

- The openZIM project proposes offline storage solutions for content coming from the Web. 
- The project has two different targets:
  - Definition of the ZIM file format: an open and standardized file format, 
  - Implementation of the libzim: an open source (GPLv2) implementation of the ZIM file format.

- 
- 
- 

# faq

- 

# summary

- 

# dev

## kiwix

- Kiwix是一个用于浏览离线内容的自由开源浏览器，最初用于离线浏览维基百科。
  - Kiwix可以读取以压缩形式存储在ZIM格式文件中的内容，使用户能够在没有网络连接的情况下浏览维基百科及其他支持的内容。

## zim file format

- tips
  - 不方便修改编辑

- ZIM文件格式是一种自由档案格式，用于存储 Wiki 内容，以便离线浏览。
  - 它主要用于维基百科和其它维基百科项目。
  - 这种格式**允许压缩文章，支持全文搜索索引以及本地分类和图像管理**，类似 MediaWiki。
  - 和原始的 Wikipedia XML 维基百科: 数据库下载 不同，整个文件可以容易的索引，并且可以被类似Kiwix的程序读取。
  - 维基百科在2012年一月的镜像大概有三百八十万篇不含图片的文章，有 7.5 GiB，对应的 ZIM 文件有 9.7 GiB（大约30%的额外开销）。
  - 除了自由文件格式，openZIM 项目还提供一个开源的 ZIM 阅读器。
- ZIM 文件格式替代了早期的 Zeno 文件格式。 ZIM 意为“ Zeno Improved ”（改进的 Zeno）
  - The ZIM file format is based on the Zeno File Format

- The standard encoding for ZIM archive content is UTF-8. So both article data and URLs should be handled accordingly.
  - All types are little-endian.
  - All integers are unsigned integers (uint_16, uint_32, uint_64).
  - All lengths are bytes.

- ZIM archives can be split in multiple files. 
  - This is necessary to be able to store big (over 4GB for example) ZIM archives to limited file systems (like FAT32). 
  - That said, the files can be of any size, but the naming is really important. 
  - The ZIM files should be named like following (the file name extensions matter): `foobar.zimaa, foobar.zimab, foobar.zimac`...

- Beginning 2021, we change the way we handle namespaces in ZIM file format.

- A ZIM archive starts with a header 
  - magicNumber
  - majorVersion
  - minorVersion
  - uuid
  - entryCount
  - clusterCOunt
  - urlPtrPos
  - titlePtrPos
  - clusterPtrPos
  - mimeListPos(defines the end and size of the ZIM file header)
  - mainPage
  - layoutPage
  - checksumPos
- A zim archive may be embedded in another file at a specific offset. 
  - In the context of zim format, the start of the zim header is the offset 0. 
  - Readers allowing to read an embedded archive must adapt offset accordingly.
- The MIME type list always follows directly after the header, so the mimeListPos also defines the end and size of the ZIM file header.

- **The current major version is `6`**. 
  - You may found old zim archives with major version 5. 
  - They are the same than 6 less extended cluster, so you can read a 5 major version as if it was a 6.

- Directory entries hold the meta information about all entries, images and other objects in a ZIM archive.
- The clusters contain the actual data of the directory entries. 
  - Clusters can be compressed or uncompressed. 
  - The purpose of the clusters are that data of more than one directory entry can be compressed inside one cluster, making the compression much more efficient. 
  - Typically clusters have a size of about 1 MB.

- Namespaces separate different types of directory entries - which might have the same title or url - stored in the ZIM archive Format.
  - The libzim hide the namespace to the user, so a entry `foo.html` in namespace `C` will be accessible as `foo.html`. 
  - libzim provides specific API to access metadata.

- 
- 
- 
- 

# examples
- https://github.com/openzim/libzim /cpp
  - Reference implementation of the ZIM specification

- https://github.com/epheterson/zimi /MIT/202602/python
  - Search and read 100M+ articles offline. API-first knowledge server for ZIM files.
  - Kiwix packages the world's knowledge into ZIM files — offline archives of Wikipedia, Stack Overflow, dev docs, and thousands of other sources
  - Zimi makes them useful: JSON API for AI agents — search, read, and browse articles programmatically
  - Library manager — browse the Kiwix catalog and download ZIMs from the UI
  - Cross-ZIM search with relevance ranking, deduplication, and time budgets
  - Persistent cache — instant startup on subsequent runs
  - [Zimi – ZIM file access for AI agents and humans (UI, API, more...) : r/Kiwix _202602](https://www.reddit.com/r/Kiwix/comments/1r4f6vv/zimi_zim_file_access_for_ai_agents_and_humans_ui/)
    - I tried to use Claude Code to access my ZIM files and realized there's no great way to do that, so I built one.
    - It runs locally or in Docker and can be used via API, CLI, MCP, or a web UI in the browser.
# more

# discuss-kiwix

- ## 

- ## 

- ## 

- ## 

- ## [Is Kiwix free or not? : r/Kiwix _202602](https://www.reddit.com/r/Kiwix/comments/1r5n8g2/is_kiwix_free_or_not/)
- It's free and Open Source. The github repositories are under this organization. You can build it youself using kiwix-build. Or you can simply download any of the existing builds. One you may find particularily interesting for an emergency hotspot is kiwix-serve (part of kiwix-tools).

# discuss
- ## 

- ## 

- ## 

- ## [Using the ZIM format to distribute a bounded archive of AI responses (experimental project) : r/Kiwix](https://www.reddit.com/r/Kiwix/comments/1rcssey/using_the_zim_format_to_distribute_a_bounded/)
  - Originally, I explored whether a ZIM file could function as a fully offline AI chatbot. After thinking through memory constraints and performance consistency across devices, it became clear that bundling a live model inside a ZIM was not practical.
  - That led to a different idea: Instead of live inference, what if I systematically enumerated a bounded prompt space, generated responses once, and distributed the entire prompt-response corpus as a static ZIM artifact?
  - Are there other applications for a "bounded inference archive" like this?

- It's an intriguing idea, but I'd suggest a different approach: be word-based rahter than character based and use n-grams to truncate "all possible combinations" to "reasonable likely combinations". That would allow you to include much more meaningful prompts while maintaining a somewhat acceptable growth pattern.
  - Actually, you could probably shift completely to a tree like strcuture. The user could enter one or two keywords. For every possible keyword combination (e.g. "wikipedia history" or "nuclear power"), generate X interesting prompts during the ZIM creation using an LLM. The user could then be shown a list of those prompts and an answer to them.

- ## [TV/Movie DB zim? : r/Kiwix](https://www.reddit.com/r/Kiwix/comments/1qpemqu/tvmovie_db_zim/)
- there's an official dataset available here, so someone could create a ZIM, just not be allowed to share it.
  - The data can only be used for personal and non-commercial use and must not be altered/republished/resold/repurposed to create any kind of online/offline database of movie information (except for individual personal use). 

- ## [Anywhere to get ZIM files other than the official Kiwix website? : r/Kiwix](https://www.reddit.com/r/Kiwix/comments/1qov4mv/anywhere_to_get_zim_files_other_than_the_official/)
- You could make ZIMs by yourself https://github.com/openzim/zimit if you are a bit technical or have time to learn.
  - If you aren't aware, you can make your own zim files using either the docker image or https://zimit.kiwix.org/. 

- [Is there a website/hub where one can share zim's created zimit.kiwix.org or manually? : r/Kiwix](https://www.reddit.com/r/Kiwix/comments/1oys2en/is_there_a_websitehub_where_one_can_share_zims/)
  - No, but we are looking into it - the main issue at this stage is figuring out a way to prevent people from sharing illegal stuff (child pr0n and so on).

- The best approach is a simple approval process to filter out the worst offenders coupled with a report feature so that people can inform you in case they find something you missed.
