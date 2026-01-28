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
# more

# discuss

- ## 

- ## 

- ## [TV/Movie DB zim? : r/Kiwix](https://www.reddit.com/r/Kiwix/comments/1qpemqu/tvmovie_db_zim/)
- there's an official dataset available here, so someone could create a ZIM, just not be allowed to share it.
  - The data can only be used for personal and non-commercial use and must not be altered/republished/resold/repurposed to create any kind of online/offline database of movie information (except for individual personal use). 

- ## [Anywhere to get ZIM files other than the official Kiwix website? : r/Kiwix](https://www.reddit.com/r/Kiwix/comments/1qov4mv/anywhere_to_get_zim_files_other_than_the_official/)
- You could make ZIMs by yourself https://github.com/openzim/zimit if you are a bit technical or have time to learn.
  - If you aren't aware, you can make your own zim files using either the docker image or https://zimit.kiwix.org/. 

- [Is there a website/hub where one can share zim's created zimit.kiwix.org or manually? : r/Kiwix](https://www.reddit.com/r/Kiwix/comments/1oys2en/is_there_a_websitehub_where_one_can_share_zims/)
  - No, but we are looking into it - the main issue at this stage is figuring out a way to prevent people from sharing illegal stuff (child pr0n and so on).

- The best approach is a simple approval process to filter out the worst offenders coupled with a report feature so that people can inform you in case they find something you missed.
