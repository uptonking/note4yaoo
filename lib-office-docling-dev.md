---
title: lib-office-docling-dev
tags: [docling, format]
created: 2025-09-21T13:57:58.408Z
modified: 2025-09-21T13:58:08.942Z
---

# lib-office-docling-dev

# guide

- pros
  - 提供了2种转换方式和架构: ocr+parse, vlm

- cons
  - text styles((bold, underline, etc)) are not supported in the DoclingDocument format

- features
  - custom serialization: include pic caption, annotation
# draft
- 对于任意一个文件，如何自动选择pipeline来convert
# dev-xp

# faq
- Python 3.13 is supported from Docling 2.18.0.

- Are text styles (bold, underline, etc) supported?
  - Currently text styles are not supported in the DoclingDocument format. 

- How do I run completely offline?
  - Docling is not using any remote service, hence it can run in completely isolated air-gapped environments.
  - The only requirement is pointing the Docling runtime to the location where the model artifacts have been stored.
  - `pipeline_options = PdfPipelineOptions(artifacts_path="your location")`

- Docling supports multiple OCR engine, each one has its own list of supported languages

- Some images are missing from MS Word and Powerpoint
  - The image processing library used by Docling is able to handle embedded WMF images only on Windows platform. If you are on other operating systems, these images will be ignored.

- 
- 
- 
- 
- 
- 

# more
