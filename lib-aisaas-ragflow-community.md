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

- ## [RAGFlow 能扛住 10万+文件的本地知识库吗？顺便求 Embedding 模型性价比推荐 _202601](https://linux.do/t/topic/1407408)
  - 我这边需要帮朋友搭建一个必须本地部署的知识库系统，主要用于生成专业性、针对性很强的报告
  - 知识来源为大量文件，规模在 10 万 + 文件（后续可能继续增长） 
  - 通过填写结构化信息（表单 / 要点），希望能在 10 分钟内生成 1.5 万字以上的专业报告
  - 对检索准确率、稳定性要求较高，同时需要成本可控

- 性价比embedding请花10元在gitee.ai模力方舟上，embedding和rerank免费用

- 之前dify上搞过上百G的知识库，内存给干崩好几次，最后换到qdrant了，用的qwen的embedding

- 你这是企业级需求了，如果准确度能达到，那就可以接ToB的活了

- 文档数量上去检索准确度就会下来，这是RAG目前的难点，建议分主题建库，检索的时候先召回主题，再在主题知识库中检索效果会好很多，10W+只放在一个库中效果肯定不好的，检索的噪声太多了

- 之前用的ragflow 12的版本，但是会卡解析，就是上传的文件特别多，然后解析状态就不更新了，也不知道是它内部哪里出的问题。不知道新版本有没有解决这个问题。
  - 而且它早期用的es，es这个比较占内存，有时候问答会特别慢，现在好像用了一个新的检索库，效率好像好一点。
  - embediing不能用本地的么？ragflow好像内置一个bge-large-zh-v1.5, 实在不行本地部署一个ollama, 然后添加embedding模型，在ragflow里边添加上，这个是没问题的。
  - 我们也没测试那么多，没有量化的东西，但是使用的时候小问题还是有的。现在好像都到19, 20了，感觉可以尝试下，直接拉个docker跑一跑。

- 背后用个云向量数据库 比如zilliz pinecone, 线上用过zilliz的serverless 跑过1亿+chunk（至少有十万+文件了）, serverless存储便宜, 就是按照请求数收费 请求多了 容易掏空钱包

- 如果你有私密的话 你embedding都不能用三方服务了。。。
  - 那还得搞台好点的服务器 自己跑embedding+搭qdrant集群吧

- 我做的没到10万，大概3万个文件，大概一下100w个实体
  - 当时也看了ragflow，但是由于工作流很难用，所以用了dify，
  - 第一次用的weaviate存的向量给干崩了，后面换成milvus可以正常使用，
  - 需要注意一下内存占用，存的越多，内存占用越多，现在3万文件，日常占用大概在7g这样，存入数据的话可能到12g这样
  - embedding用的硅基流动的BAAI/bge-m3，没太研究向量模型选型，只是图它免费，我觉得主要是看工作流怎么设计
  - 向量检索时间大概2-3s
  - 目前主要通过文档的元数据标签先圈选范围再进行检索，所以准确率倒还好
  - 另外向量化的时候，也遇到各种问题，重建了很多次，有的是文件格式问题，有的是dify限制，有时候量化到一半直接卡住了，一定要分步上传

- 现在据我所知，大规模的RAG行业内很少有做的好的，基本都是检索精度上不去。有很多优化方向：
  - 1. 查询重写：（不知道你是什么行业的知识库），有一些行业内的专业术语可能会有歧义，所以要建立标准词库，把用户问的问题不明确的全部在检索阶段替换成标准表达 
  - 2. 综合化查询：有些问题不是一个文档能查出来的，有可能会关联多个文档，所以要用Agent的方式多轮查询 
  - 3. 意图确认：有些提问太笼统，必须对问题进行确认，明确清晰化
  - 当然，企业级的RAG需要优化的地方太多了，对于embedding和大模型的能力只要花钱就可以解决，就我们做的来说，模型能力不是瓶颈，难的是准确的检索。要生成高质量的报告的前提是，必须检索做的准，如果检索做的准确的话，生成报告基本就是一套固定的流程往里面填数据就行

- 现阶段的检索精度很难提高，而且不灵活，嵌入话以后，如果文档经常会发生变化，又要重新再嵌入

- 做过某地档案馆千万级的知识库。 先说结论。10W级别的RAG想要做容易，想要做的好很困难，原生开源方案更困难。
  - embedding模型智谱的qwen的, bge的还是海外几家的不关键，关键是你要微调。
  - 困难在哪，原因很多其中一个关键原因是，单向量 embedding 的检索能力存在容量上限，当语料规模继续增大时，会不可避免地出现“向量空间装不下组合关系”的问题。简单说就是，你文档特别多的时候，高维空间里的向量也会挤在一起，不相关的或者相关性很低的向量距离也会变小，很容易混到你的TOP-K里。各种BM25, 图谱，关键词筛选的方案，大多都是在弥补这个问题。但实际来看，你加入了查缺补漏的各种各样的召回方案，在文档量越来越大的时候，效果还是在下降。
- 再说一下为啥开源方案可靠性更低，（我记得我在论坛里说过好几次了）。最关键3点：
  - 开源模型没见过私域数据，你所有的embedding, reranker, llm在私域数据里都达不到官方测评的结果。中文的语义在不同的上下文中，表达的含义是不一样的，你在用embedding模型做向量召回的时候，你的文本和训练时的设定可能天差地别导致结果不理想。
  - 文档解析和切片方案对整个召回的设计影响非常大。开源往往就是那几种按长度切，字母切，滑窗切。但是你的文档可能需要按照文档树形结构切，才能不把同一个语义的文本分开。
  - 用户问题的理解和重写，用户问题是千奇百怪的，你不改写用户的query，补充关键词（比如时间，比如追问获取更多的信息量），你就没办法获取充足的信息来进行检索。
- 对于你的问题，你可以：
  - 开源方案上线很低，你魔改起来比较困难。最好直接用langgraph甚至从头搓一个，很容易。
  - embeding模型和reranker模型用哪家都无所谓，但是一定要微调，微调不微调效果差距至少20%
  - 如果你是大文档，你必须分桶，给每个桶打标签，做一个分级标签体系，树的最底层桶里的数据不要特别多，比如200-1000这个量级。给你的向量库以及embeding模型降低压力。

- 按照现有的一些优化方法，感觉很多时候就要放大人工的工作量，例如查询重写的时候，需要建立标准词库；切片的时候遇到表格跨行，表格语义难理解的问题；页眉、页脚、版权等无关信息干扰的问题。佬有没有可以分享一下的比较好的实践

- 我当时测试的时候，几乎同样的检索内容，LLM的影响比想象中大很多，甚至一个简单的分类，都有天壤之别。因为当时想部分地方用小一点的模型替代，节省成本，以及速度能更快些。但是结果确实差一截。

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

# discuss-news 🆕
- ## 

- ## 

- ## 

- ## [feat: add paddleocr parser _202601](https://github.com/infiniflow/ragflow/pull/12513)
  - Add PaddleOCR as a new PDF parser.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
