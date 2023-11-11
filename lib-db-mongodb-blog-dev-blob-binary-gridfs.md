---
title: lib-db-mongodb-blog-dev-blob-binary-gridfs
tags: [binary, blob, blog, gridfs, mongodb]
created: 2023-11-11T06:25:15.727Z
modified: 2023-11-11T06:26:48.452Z
---

# lib-db-mongodb-blog-dev-blob-binary-gridfs

# guide

# blogs

## [GridFS — MongoDB Manual](https://www.mongodb.com/docs/manual/core/gridfs/)

- GridFS is a specification for storing and retrieving files that exceed the BSON-document size limit of 16 MB.
- GridFS is a way of storing binary information larger than the maximum document size (currently 16MB). 
  - When you upload a file to GridFS the file is broken into chunks and the individual chunks are uploaded. 
  - When you download a file from GridFS the original content is reassembled from the chunks.

- Instead of storing a file in a single document, GridFS divides the file into parts, or chunks, and stores each chunk as a separate document. 
  - By default, GridFS uses a default chunk size of 255 kB; 
  - that is, GridFS divides a file into chunks of 255 kB with the exception of the last chunk. The last chunk is only as large as necessary. 
- GridFS uses two collections to store files. 
  - One collection stores the file chunks, 
  - and the other stores file metadata. 
- When you query GridFS for a file, the driver will reassemble the chunks as needed. 
  - You can perform range queries on files stored through GridFS. 
  - You can also access information from arbitrary sections of files, such as to "skip" to the middle of a video or audio file.
- GridFS is useful not only for storing files that exceed 16 MB but also for storing any files for which you want access without having to load the entire file into memory.

- When to Use GridFS
  - use GridFS for storing files larger than 16 MB.
- In some situations, storing large files may be more efficient in a MongoDB database than on a system-level filesystem.
  - If your filesystem limits the number of files in a directory, you can use GridFS to store as many files as needed.
  - When you want to access information from portions of large files without having to load whole files into memory, you can use GridFS to recall sections of files without reading the entire file into memory.
  - When you want to keep your files and metadata automatically synced and deployed across a number of systems and facilities, you can use GridFS.

- Do not use GridFS if you need to update the content of the entire file atomically. 
  - As an alternative you can store multiple versions of each file and specify the current version of the file in the metadata.
  - You can update the metadata field that indicates "latest" status in an atomic update after uploading the new version of the file, and later remove previous versions if needed.
- if your files are all smaller than the 16 MB BSON Document Size limit, consider storing each file in a single document instead of using GridFS. You may use the `BinData` data type to store the binary data.
# more

# discuss-gridfs

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [使用 MongoDB 的兄弟，有没有采用 GridFS 做分布式文件系统的？ - 知乎](https://www.zhihu.com/question/19607966/answers/updated)
- Mongo GridFS在高并发（每秒写入10M，持续半小时到一个小时）的情况下secondary会无法catch up with primary。
  - Mongo GridFS不是为分布式存储而设计的，它解决的问题领域是小型业务已经使MONOGODB，但是又需要存储一些文件，而且需要给这些文件加一些元信息。
  - 用它来存储图片以小文件是比较合适的。
  - 但是把它当大规模的分布式存储系统就不太合适的，那你应该用S3或者其它云存储解决方案了
