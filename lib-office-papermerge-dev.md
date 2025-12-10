---
title: lib-office-papermerge-dev
tags: [docs, papermerge, pdf]
created: 2025-12-09T13:50:35.379Z
modified: 2025-12-09T13:50:57.426Z
---

# lib-office-papermerge-dev

# guide

- pros
  - Document versioning
  - 存储支持: filesystem, configure S3 compatible storage for you documents
  - 🏘️ built upon microservice architecture
  - Tags - assign colored tags to documents or folders
  - Share documents and folders between users and/or groups of users
  - Pluggable Authentication: SSO - single sign on using standard protocols such as OIDC
  - Page Management - delete, reorder, rotate, merge, move, extract pages
  - audit logs

- cons
  - 🐛 实测在ui上删除文件后, 文件系统并未删除
  - 不支持文件/文件夹的 trash & restore
  - 支持的文件类型太少: PDF/JPEG/PNG/TIFF, 不支持docx/xlsx
  - 查看纯文字的pdf时，不支持选择文本， 查看功能太弱
  - 编辑功能弱

- features
  - OCRed text overlay (you can download document with OCRed text overlay)
  - Full text search (supports multiple search engines)
  - 支持backup/dump

- 🏘️ built upon microservice architecture: different parts can be combined in different ways to match your needs
  - database (SQLite, PostgreSQL, MariaDB)
  - search engine (currently only Solr is supported)
  - search indexer (syncs database with search engine)
  - OCR worker - performs OCRs on the documents using Tesseract
  - websockets service - use it if you want user to receive real time notifications about background events
  - path template service - moves documents into target path based on the document metadata
  - S3 service - syncs documents with S3 storage
    - all your documents will be copied to remote S3 storage
  - Each service is deployed as docker image. 

- who is using #readability
  - papermerge

- cons-paperless-ngx
  - 官方未提供使用s3/minio作为存储层的方案, 社区有多种方案

- features-paperless-ngx
  - Performs OCR on your documents
  - Utilizes the open-source Tesseract engine to recognize more than 100 languages
  - Uses machine-learning to automatically add tags, correspondents and document types to your documents.
  - Supports PDF documents, images, plain text files, Office documents (Word, Excel, PowerPoint, and LibreOffice equivalents) and more.
  - Paperless stores your documents plain on disk. Filenames and folders are managed by paperless and their format can be configured freely with different configurations assigned to different documents.
  - Full text search
  - built-in robust multi-user permissions system that supports 'global' permissions as well as per document or object.
  - A powerful workflow system that gives you even more control.
  - Optimized for multi core systems: Paperless-ngx consumes multiple documents in parallel.
  - 社区实现了多种ai集成的方案

- tips
  - ?

- resources
  - changelog: [What's new? - Papermerge DMS](https://docs.papermerge.io/3.5/whatsnew/)
# draft
- 支持 web-clipper 收藏的内容

- 支持singleFile格式的html
  - 采用 readability 对html的内容进行优化

- pdf的查看采用bentopdf的方案来实现更好的体验

- gallery/icon-view 支持配置字段

- vlm

- images
  - 支持浏览comfyui生成图片的元数据

- 迁移 paperless-ai 到 papermerge-ai
# dev-xp
- 🤔 上传的pdf文件会保存在server文件系统, 目录结构为 `docvers/ranNumber/uuid/原文件名`
  - 作者解释是为了避免单目录的文件数量超过某些系统限制的数量
  - 这种方法简单, 对超大规模文件是否存在问题?

## devops

- resources
  - [High-Level Architecture - Papermerge DMS](https://docs.papermerge.io/3.5/developer-manual/architecture/)

- this project provides a webapp that supports pdf/image uploading and document management.
  - i have run this project fully locally without docker for local development and debugging, using local postgresql/redis.
  - the backend starts by `uv run --env-file .env -- task server`, the frontend starts by `cd frontend/apps/ui && npm run dev`.

```sh
# backend
uv run --env-file .env -- task migrate
uv run --env-file .env -- papermerge-cli users create --username admin --password 11111111 --superuser
uv run --env-file .env -- task server

# frontend
cd frontend/apps/ui
npm run dev
```

# docs
- One document has one or multiple versions. The original document version - is version number 1.
  - When we say "change applied to a document" - we mean things like rotate pages, reorder pages or merge two documents.

- Node is an abstraction of two concepts: document and folder. Every time you read node, you can mentally replace that term with either document or folder and the statement will still hold.

- In order to assist you to quickly move around documents, folders and pages - there is a special mode - dual panel model. 
  - In dual panel mode there are two panels displayed side by side. 
  - Between two panels documents (as well as folders and pages) can be moved with one simple drag'n drop.
  - Main panel is the one which is always visible and secondary panel is the on which opens and closes i.e. the one with "close button" in upper right corner.

- Viewer is the panel in which document is opened. 
  - There can be two Viewers opened side by side. This mode (i.e. dual panel mode with a Viewer in each panel) is very handy when it comes to moving pages between documents.

- 🏠 Workers are small background applications that handle long-running or asynchronous tasks. They don’t use HTTP to communicate. Instead, they interact with the main app via a message queue.
  - The main app acts as the producer, placing tasks onto the queue.
  - The workers act as consumers, picking up and executing those tasks.
  - The transport mechanism is Redis, which functions as the message bus. Communication happens via named queues.
  - Papermerge DMS uses the following workers: Path Template Worker, S3 Worker, OCR Worker, i3 Worker

- Inbox folder is where all incoming documents land first. 
  - Home folder is where all user documents are.
  - Internally their title is actually ".inbox" and ".home". By convention special folders start with dot character.

- inbox is just temporary location, so you'll need to move documents to their "final destination" - target folder.
  - The idea is simple: you need to decide where to place your receipts only once. Once you decide where you put to them - you write it down as "path template" and then all your receipts will automatically be placed to that path.
  - for each document type you create a "template" of the place where documents of that type will be stored. And then Papermerge DMS will use that information to move the document to the target folder automatically

- Papermerge DMS supports S3 object storage.
  - all your documents will be copied to remote S3 storage.
  - If you delete a document, then both copies - the local one and S3 one will be deleted as well - this is what "synchronized" means. 
  - Stated other way: in simple scenarios when you have only one web app running - S3 storage is exact copy of you local media storage.

- OCR Workers may get document's to be processed as well store their processing results to S3 Object Storage. 
  - S3 object storage may be used as storage medium between webapp and OCRWorkers. This is useful in advanced scenarios where OCR workers run on separate machines.

- I3 Worker's job is to synchronize database data with search index. 
  - after each OCR processing OCR worker notifies I3 to update search index with newly extract content.

- documents merging is the process of combining two documents into one: all pages from the source document are transferred into destination document and then source document is deleted.

- By default, ocr process is triggered automatically on document file upload. 
  - When OCR process is completed new document version is created and document becomes searchable.

- 
- 
- 
- 
- 
- 
- 
- 

# more
- PDF/A differs from PDF by prohibiting features unsuitable for long-term archiving, such as font linking and encryption.
