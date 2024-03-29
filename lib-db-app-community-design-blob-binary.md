---
title: lib-db-app-community-design-blob-binary
tags: [attachment, binary, blob, community, database-design]
created: 2023-11-07T16:48:35.979Z
modified: 2023-11-07T16:49:03.314Z
---

# lib-db-app-community-design-blob-binary

# guide

- tips
  - 图床的用途
# discuss-stars
- ## 

- ## 

- ## 

- ## 🛢️ [Which DB is best for folder structure applications similar to Google Drive : r/node _202310](https://www.reddit.com/r/node/comments/17ca9dy/which_db_is_best_for_folder_structure/)
- You want to use object storage for something like this. 
  - Databases are not for files generally. 
  - Something AwS S3, GCP Cloud Storage, or if you want something you can self host, MinIO.

- Ive built this a few times using postgres and s3, basicallt store the folders in a postgres table and a bit of meta data about the uploaded file in another. Folders can have a parent-_d to another folder to build ”depth”, files can have a ”folder_id”.
  - I have then uploaded to file to s3 naming it the same as the uuid of the meta data of the file, this way i have a reference to it in the s3 bucket.
  - So in s3 its basically been a flat list of files, no depth.

- You should not store the files themselves in the db, store those in AWS S3 / Backblaze B2 or similar service. In the db just store the folder structure, file/folder metadata and whatever info you need to retrieve a file from storage.
  - If this is just a demo project or something like that, with not many users or files, you could store the file data in the db or even on the server hard drive but this will not scale well at all.
  -  If there's any chance this app will grow then it's probably worth building it the right way and spending a bit of money to use S3 or similar.

- Even if not at scale having large blob objects will cripple your database rather fast. While they can hold big objects they are just not made for that and just using a simple pattern of object path and separate object storage (or something more dedicated like s3 or minio) is future proof without too much hassle.

- ## 📎🔥 [Xata File Attachments: Databases can now store files and images | Hacker News_202308](https://news.ycombinator.com/item?id=37324370)
- I think for smaller projects just storing images as BLOBs in e.g. PostgreSQL works quite well. I know this is controversial. People will claim it's bad for performance. But that's only bad if performance is something you're having problems with, or going to have problems with. If the system you're working on is small, and going to stay small, then that doesn't matter.
  - Storing the images directly in the database has a lot of advantages. 👍🏻 They share a transactional context with the other updates you're doing. They get backed up at the same time, and if you do a "point in time" restore they're consistent with the rest of your data. No additional infrastructure to manage to store the files.
- I think the one big problem with BLOBs, especially if you have a heavily read-biased DB, is you're going to run up against bandwidth/throughput as a bottleneck. One of the DBs I help maintain has some very large JSON columns and we frequently see this problem when traffic is at its peak: simply pulling the data down from Postgres is the problem.
  - If the data is frequently accessed, it also means there are extra hops the data has to take before getting to the user. It's a lot faster to pull static files from S3 or a CDN (or even just a dumb static file server) than it is to round trip through your application to the DB and back. For one, it's almost impossible to stream the response, so the whole BLOB needs to be copied in memory in each system it passes through.
  - It's rare that any request for, say, user data would also return the user avatar, and so you ultimately just end up with one endpoint for structured data and one to serve binary BLOB data which have very little overlap except for ACL stuff, but signed S3 URLs will get you the same security properties with much better performance overall.
- 👉🏻 Also cost is a factor, databases are usually attached to expensive disk and their storage layer is tuned for iops, and blobs will be using gigs of that for just sitting there being sequentially scanned.
- I have to worked with BLOBs in DB fields in almost a decade, but when I worked with them one really annoying problem I ran into was that the DB wanted to morph the blob in transit by default. So JPEGs and PDFs etc would get corrupted because SQL Server wanted to add its own little byte signature to it during read/write operations. Not sure if that was an endemic problem or a specific SQL server shiftiness
- Do you have any thoughts on when a JSON column is too large? I've been wondering about the tradeoffs between a jsonb column in postgres that may have values, at the extreme, as large as 10 MB, usually just 100 KB, versus using S3.
  - Wouldn't the same reasoning for BLOBs apply to JSON columns? Unless you're frequently querying for data within those columns (eg, filtering by one of the JSON fields), then you probably don't need to store all the JSON data in the DB. And even if that is the case, you could probably work out a schema where the JSON data is stored elsewhere and only the relevant fields are stored in the DB.
  - At the same time, I'm working with systems where we often store MBs of data in JSON columns and it's working fine so it's really up to you to make the tradeoff.
- Using PostgreSQL as a document database so everything is stored as JSONB and it’s only around 800gb but it’s still lightning fast.

- 🐘 BLOB on Postgres are awesome, but there's also a full-featured file API called Large Objects for when the use-case requires seeking/streaming. Large Objects: https://www.postgresql.org/docs/current/largeobjects.html
  - Large Objects works great for images and stylesheets and other file assets for my small PostgREST projects.

- 👉🏻 I think there is too much emphasis on 'the right way' sometimes, which leads people to skip over an analysis for the problem they are solving right now.
  - For example, if you are building something that will have thousands or millions of records, and storing small binaries in postgresql lets you avoid integrating with S3 at all, then you should seriously consider doing it. The simplification gain almost certainly pays for any 'badness' and then some.
  - If you are working on something that you hope to scale to millions of users then you should just bite the bullet and integrate with S3 or something, because you will use too much db capacity to store binaries and that will force you to scale-out the database far before you would otherwise be forced to do so.
- It always depends on the problem you're trying to solve. What Xata did, was integrate files as a database column, BUT stored the binary content in S3. Thus offering both transactional file management and point in time recovery as well as high performance direct (S3) file access, through a CDN. Basically Xata implements the orchestration and takes away the pain of managing 2 services.

- There are plenty of oss solutions that talk "s3", like swift, ceph and seaweedfs.
- 🤔 Why object storage? 
  - Its easier to backup, version and to scale horizontally. 
  - Most solutions will also provide encryption capabilities that can be commanded either via external key management systems or from the client application. 
  - Also, custom access policies are great for private documents and file uploads.
- Using static files is a good solution in some cases, nothing against it. But in many scenarios, there are huge benefits on using object storage instead, even if it is quite slower.
- Minio is easy enough to spin up, S3-compatible. That seems like my default path to persistence going forward. More and more deployments options seem like they'll benefit from not using the disk directly but instead using the dedicated storage service path, so might as well use a tool designed for that.
  - S3 can be a bit of a mismatch for people who want to work with FS objects as well, but there are a couple options that are a lot easier than dealing with blob files in PGsql. S3cmd, S3fs; perhaps SSHfs to the backing directory of Minio or direct access on the host 

- 🤔 Disk space is cheap, even when it's on a DB server and not S3. Why worry that much about it?
  - Disk I/O less so. An average RDBMS writing a 10MB BLOB is actually writing at minimum 20-30MB to disk - once to journal/WAL, once to table storage, and for updates/deletes a third copy in the redo/undo log. You also get a less efficient buffer manager with a higher eviction rate, which can further exasperate disk I/O.
- there is a hard limit to db scale up and you don't want to hit it.

- 🍃 You may not like Mongo, but it's had this feature for a long time. https://www.mongodb.com/docs/manual/core/gridfs/ 
  - With built in replication, horizontal scalability, sharding, detailed monitoring, built in LRU memory cache, reading your own writes, automatic file expiration, etc.
  - It's hard to find when CouchDB and MongoDB got attachments, but I suspect CouchDB had them first, so it may have been an obvious choice for MongoDB.
- I've worked on a project where MongoDB GridFS was used quite successfully as the backing store for a CMS system. If I recall correctly, GridFS gives you versioning out of the box, which the CMS leveraged to let users roll back files/images/videos to older versions.
  - That was a production system and used to get hammered with requests. It didn't even have a CDN in front of it for the first few years. 
  - And that was MongoDB 2.4 so I'm assuming GridFS has matured even more since then.

- 
- 

# discuss
- ## 

- ## [Open Source online file storage I created - MyDrive _202101](https://www.reddit.com/r/reactjs/comments/koyf74/open_source_online_file_storage_i_created_mydrive/)
- You needed MongoDB and Amazon s3 together?
  - So Amazon S3 is where you store the file chunks. While In mongoDB it stores file object and metadata, such as the owner of the file, filename, size, ect. 
  - You can choose to just use mongoDB if you choose too, this will use a library called `gridfs` to store the file chunks in mongoDB. Although, this is not recommended since it puts more strain on the CPU, plus mongoDB storage is expensive if you are using a service such as atlas.
  - The reason you cannot use just Amazon S3 is that it is not really suitable for storing the a file object that you query, delete, and modify.
- MongoDB is a database. S3 is file storage.

- ## [I created an Open Source Google Drive Clone - MyDrive _202006](https://www.reddit.com/r/selfhosted/comments/h8tvtg/i_created_an_open_source_google_drive_clone/)
- myDrive uses the HTTP protocol to transfer files.

- FTP is File Transfer Protocol, an older protocol used for transferring files. It would make no sense implementing it in an app like yours (and it's a shitty old protocol anyway).
- Samba (or more specifically SMB) is a protocol used for transfering files over a (usually) local network, 
  - it's what Microsoft Windows uses to connect to network drives and whatnot. 
  - There is an open source implementation, Samba, that's interoperable with SMB, and just like FTP it would make little sense to have it in an app like this, especially since it's very complicated to implement and has tons of security concerns.
- You are using HTTP with Express I believe.
  - The only thing that would make sense would be implementing WebDAV. 
  - It's a standardized protocol on top of HTTP that allows compatible apps (which there are plenty of) to connect to a given endpoint and browse, download and upload files. 
  - Nextcloud uses this for their apps and such, and a lot of other web-based file-storage services use it as well. It also has a lot of client apps that support it.

- Any advantages to Filerun? That's what I'm currently using that fits in this space. The only thing it doesn't do (or at least I don't use) is auto-syncing. But file sharing, browsing, utility, etc, it does a great job.

- I just want something that can sync files to my phone and is light weight and fast enough and can handle photos and videos while looking good lol. Is that too much to ask for?

- ## [My first open source project! MyDrive _202003](https://www.reddit.com/r/node/comments/feg12q/my_first_open_source_project_mydrive_a/)
- After looking at your code, I'm very impressed at how clean & well organized it is. Especially the routes folder. When I do my routes, it's a total mess. Thanks man, I learned a lot from this.

- It uses mongoDB for storage, and that number is from how much storage space is left on this computer/server. When you run myDrives startup script it asks for a path so it can check how much storage space you have left.

- ## Images get loaded differently than JavaScript. 
- https://twitter.com/RogersKonnor/status/1745704080163369407
  - They generally have better compression, don't need to be evaluated by the V8 engine, multi-threaded loading, native lazy loading, etc...  
  - Comparing JS bytes to binary bytes is not the same.
- You can still compare certainly. Shoddy internet/ low bandwidth are common enough thanks to mobile. Just have to be accurate in reason for comparison, yes.

- ## [Is it worth sticking to mongodb with GridFS or should I just use MySQL? : node_201705](https://www.reddit.com/r/node/comments/6bzf1d/is_it_worth_sticking_to_mongodb_with_gridfs_or/)
- 
- 
- 

- ## [Self-hosted photo and video backups directly from your mobile phone | Hacker News_202307](https://news.ycombinator.com/item?id=36673224)
- 
- 
- 
