---
title: lib-aisaas-ragflow-docs
tags: [docs, ragflow]
created: 2025-12-06T13:26:07.138Z
modified: 2025-12-06T13:26:33.899Z
---

# lib-aisaas-ragflow-docs

# guide

# overview
- Once you have selected an embedding model and used it to parse a file, you are no longer allowed to change it. 
  - The obvious reason is that we must ensure that all files in a specific dataset are parsed using the same embedding model (ensure that they are being compared in the same embedding space).

- RAGFlow also offers HTTP and Python APIs for you to integrate RAGFlow's capabilities into your applications.
# docs
- RAGFlow features visibility and explainability, allowing you to view the chunking results and intervene where necessary. 
  - Double click the chunked texts to add keywords or make manual changes where necessary
  - You can add keywords or questions to a file chunk to improve its ranking for queries containing those keywords. This action increases its keyword weight and can improve its position in search list.
# more
