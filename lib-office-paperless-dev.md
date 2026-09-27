---
title: lib-office-paperless-dev
tags: [paperless]
created: 2026-09-27T10:49:02.751Z
modified: 2026-09-27T10:50:57.055Z
---

# lib-office-paperless-dev

# guide

- pros
  - Keep multiple versions of a document's file under a single entry, sharing one set of metadata.
  - OCR on your documents, adding searchable and selectable text
    - use `Tesseract` engine to recognize more than 100 languages
    - Supports remote OCR with Azure AI (opt-in).
  - optionally leverage AI/LLM for document suggestions, chatting 
  - Uses machine-learning to automatically add tags, correspondents and document types 
  - Shareable public links with optional expiration.
  - Full text search
    - Results are sorted by relevance to your search query.
    - Highlighting shows you which parts of the document matched the query.
  - Supports PDF documents, images, plain text files, Office documents (Word, Excel, PowerPoint, and LibreOffice equivalents) and more.
    - Office document and email consumption support is optional and provided by Apache Tika
  - Bulk editing of tags, correspondents, types and more.
  - built-in robust multi-user permissions system that supports 'global' permissions as well as per document or object.
  - Optimized for multi core systems: Paperless-ngx consumes multiple documents in parallel.

- cons
  - license: GPL
  - ? 未实现流式处理大的pdf文件

- features
  - Organize and index your scanned documents with tags, correspondents, types...
  - Documents are saved as PDF/A format which is designed for long term storage, alongside the unaltered originals.
  - Customizable dashboard with statistics.
  - powerful workflow system that gives you even more control.

- 优化提取中文pdf文字的方案
  - 可参考华人团队的方案, 如 mineru
# issues

# draft

# dev-xp

# more
