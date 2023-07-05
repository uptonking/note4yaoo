---
title: spec-format-zim
tags: [format, wiki, zim]
created: 2023-07-05T10:22:42.846Z
modified: 2023-07-05T10:22:57.942Z
---

# spec-format-zim

# guide

- resources
  - [ZIM file format](https://wiki.openzim.org/wiki/ZIM_file_format)
# spec

- 

# faq

- 

# summary

- 

# dev
- ZIM文件格式是一种自由档案格式，用于存储 Wiki 内容，以便离线浏览。
  - 它主要用于维基百科和其它维基百科项目。
  - 这种格式允许压缩文章，支持全文搜索索引以及本地分类和图像管理，类似 MediaWiki。
  - 和原始的 Wikipedia XML 维基百科: 数据库下载 不同，整个文件可以容易的索引，并且可以被类似Kiwix的程序读取。
  - 维基百科在2012年一月的镜像大概有三百八十万篇不含图片的文章，有 7.5 GiB，对应的 ZIM 文件有 9.7 GiB（大约30%的额外开销）。
  - 除了自由文件格式，openZIM 项目还提供一个开源的 ZIM 阅读器。
- ZIM 文件格式替代了早期的 Zeno 文件格式。 ZIM 意为“ Zeno Improved ”（改进的 Zeno）

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

# goldendict
- 全文索引fts的位置
  - ~/.var/app/org.goldendict. GoldenDict/cache/goldendict/index/

## community

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

# more
