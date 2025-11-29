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
  - text styles((bold, underline, etc)) are not supported in the `DoclingDocument` format
  - 未实现流式处理大的pdf文件

- features
  - custom serialization: include pic caption, annotation
# draft
- 对于任意一个文件，如何自动选择pipeline来convert

- vlm
  - 如何流式输出
# dev-xp
- 使用lmstudio的granite-docling-mlx时，lmstudio的server日志不断出现重复文字，最终返回的文本不完整

- 🤔 if i have  a very large pdf that is 1GB, can docling do stream parsing to avoid memory overflow? 
  - Docling does NOT currently support true stream parsing for large PDF files
  - Docling uses `pypdfium2` as its primary PDF backend (`pypdfium2_backend.py`). 
  - The key issue is in the initialization: `self._pdoc = pdfium.PdfDocument(self.path_or_stream, password=password)`.
  - Problem: pypdfium2 loads the entire PDF into memory when creating the `PdfDocument` object, regardless of file size.
  - The `StandardPdfPipeline` uses a threaded approach but still suffers from the same memory issue:
  - Pages can be unloaded after processing (_release_page_resources())
- `DocumentStream` itself is just a wrapper for `BytesIO` streams - it does NOT provide streaming parsing capabilities. 
  - PDF Backend Still Loads Entire File into Memory
  - DocumentStream并非真正的流式解析器, DocumentStream要求整个文件内容已经加载到`BytesIO`对象中
  - 使用 `getbuffer().nbytes` 获取文件大小，这意味着整个文件必须在内存中
  - 这不是真正的流式解析，而是内存中的缓冲区处理
  - 从测试代码可以看出当前的使用模式, 一次性读取整个文件到内存 ( `open("rb").read()` )
- DocumentStream is NOT a true streaming parser:
  - The underlying PDF backend (pypdfium2_backend.py:387) loads the entire stream into memory: `pdfium.PdfDocument(self.path_or_stream, password=password)`
  - Docling does process pages in batches to control memory usage during pipeline execution
  - Batch processing helps but doesn't solve the core issue: Pages are processed in batches, but the full PDF is still loaded

- Workaround required: For very large PDFs, you need to split them into smaller documents before processing
- I recommend pre-splitting the PDF into smaller chunks (e.g., 50-100 pages each) using tools like PyPDF2 or pdfrb, then processing each chunk individually with Docling

- Solutions for Large PDF Processing:
  - Option 1: Use Document Limits, Process in chunks by limiting pages and file size, Process 50 pages at a time
  - Option 2: Configure Batch Processing for Memory Management, Process one page at a time
  - Option 3: Manual Chunking for Very Large Files, Process in chunks by creating separate streams for each chunk

- You can convert PDFs from a binary stream instead of from the filesystem
  - [Advanced options - Docling](https://docling-project.github.io/docling/usage/advanced_options/)

- [Docling is a new library from IBM that efficiently parses PDF, DOCX, and PPTX and exports them to Markdown and JSON. : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1ghbmoq/docling_is_a_new_library_from_ibm_that/)
  - Docling is at least 50x slower than PyMuPDF. But it does have categorization when you need structured output, the tradeoff.
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
- [IBM is open-sourcing a new toolkit for document conversion - IBM Research _202411](https://research.ibm.com/blog/docling-generative-AI)
