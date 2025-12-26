---
title: lib-aisaas-ragflow-community
tags: [community, rag, ragflow]
created: 2025-12-06T13:25:36.923Z
modified: 2025-12-06T13:25:53.871Z
---

# lib-aisaas-ragflow-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## [RAGFlow is an open-source RAG engine based on OCR and document parsing | Hacker News _202404](https://news.ycombinator.com/item?id=39896923)
- Document processing is getting better and better with new tools leveraging LLMs. If anyone is interested in exploring this space, try another similar tool LLMWhisperer (https://llmwhisperer.unstract.com/). It is a part of Unstract, an open-source document processing tool (https://github.com/Zipstack/unstract)
  - Actually we've tried almost all lof existing open source models for document processing, and none of them performs well for complex documents, especially those having complicated tables, such as tables cells without borders, cells need to be combined, ..., etc. Although adopting LLMs to perform such document understanding tasks is more scalable, it requires much more data and computation power to achieve similar results. That's why we design such models start from scratch.

- I'm partly sad at the approach this and other engines take: reimplement each part (PDF parser, etc etc) in a way where they are pretty much useless except in their specific engine.
  - If instead we had a PDF() class that did what RAGFlow is doing (dealing with all the different trade-offs of the different python PDF engines such as pdfplumber), then we could easily adapt it and improve it, and it can be useful for other projects as well.
- It is open-source though. Just rip it off and make that PDF() class.

- A lot of the yolo stuff from ultralytics is AGPL3 fyi. Recommend caution depending on what code or models / model lineage are used
  - Thanks for your nice suggestion. We train the model using YOLO, but during inference, the model is converted into ONNX and we use ONNXRuntime for the model inference. As a result, YOLO itself is not included in the software package. We will open the training code in the repo soon.
  - We've used YOLOv8 as the object detection model, and use some public datasets, such as PubTable, CDLA, together with some private data to train the model. The model on Huggingface is the one trained using public dataset, and we would open this work later. We use YOLOv8 just because we want to let the document parser run without GPU, I think you could also try any other object detection models such as Detectron, and use the public datasets to train the model as well. We've not used transfomers for this task, because given limited data, it could not outperform traditional CNN based models.
# discuss-roadmap
- ## 

- ## 

- ## 

- ## 

- ## [S3 Support apart from local upload _202509](https://github.com/orgs/infiniflow/discussions/10328)
- 20251031: We're working on it. Expected to be released in our next version.

- ## [[RAGFlow] Use OSS componets instead of source avaliable counter parts _202405](https://github.com/orgs/infiniflow/discussions/1258)
  - I wonder will the community willing to swap some of the components with source available license to FOSS alternatives to fully embrace the philosophy and spirit of open source.
  - Currently I spot two: ElasticSearch to OpenSearch, and Redis to Valkey. I believe two are drop in replacements (except ElasticSearch as the SDK refuse to work with OpenSearch but I believe the code change will be minimal).

- One question about Elasticsearch is that its license prohibits providing the software to third parties as a hosted or managed Service, so it seems like using Elasticsearch in RAGflow does not have problems?
  - In addition, using Elasticsearch for RAGflow is only a temporary solution for now, after our own database infinity is mature and stable(during this summer), it will be the main choice for RAGflow, because it provides much more powerful features than Elasticsearch with multiple recall, much better performance, and lower resource consumption.

- Regarding to Elasticsearch, it will be removed in future, as long as Infinity is totally stable. However, if the community users insist on keeping Elasticsearch as a choice, it would be replaced with OpenSearch at that time.
# discuss-issues
- ## 

- ## 

- ## 

- ## [[Bug]: Layout analysis in document parsing is way too slow _202511](https://github.com/infiniflow/ragflow/issues/11529)
- The slow layout analysis you’re seeing is a known issue on ARM-based Macs like the M3 Ultra. RAGFlow’s document parsing (especially layout analysis) is heavily optimized for x86 CPUs and NVIDIA GPUs, but lacks ARM-specific optimizations—so even with powerful hardware, performance can be much worse on Mac ARM systems

- ## [[Question]: Issue running docker compose from the quickstart (Mac) _202412](https://github.com/infiniflow/ragflow/issues/3804)
- We officially support x86 CPU and nvidia GPU. While we also test RAGFlow on ARM64 platforms, we do not plan to maintain RAGFlow Docker images for ARM.
  - You can either use a x86 CPU machine to deploy RAGFlow or follow the guide build the RAGFlow docker image on ARM platform by yourself.

# discuss-roadmap
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
