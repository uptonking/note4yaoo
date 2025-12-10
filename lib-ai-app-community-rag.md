---
title: lib-ai-app-community-rag
tags: [ai, community, rag]
created: 2024-09-08T20:08:04.573Z
modified: 2024-09-08T20:08:16.088Z
---

# lib-ai-app-community-rag

# guide

- pros-rag
  - solutions rich
  - save cost

- cons-rag
  - extra infra like vectordb/retrive-api

- who is using #PGVector
  - SurfSense
  - colanode

- usecases-rag
  - long-docs/pdf
  - chat-history
  - rag的实现还可以参考ai-coding中的实践和模式
  - 针对表格excel/脑图的rag
  - ⏳ 多版本文件的rag

- leaderboard-rag
  - [MTEB Leaderboard - a Hugging Face Space by mteb](https://huggingface.co/spaces/mteb/leaderboard)
    - https://github.com/embeddings-benchmark/mteb
    - top202509: gemini-embedding-001, embeddinggemma-300m, Qwen3-Embedding-8B/4B/0.6B, linq-mistral, jina, granite, nomic
    - 👷实测, embeddinggemma在Ollama结果差, 在LM Studio结果还行 ~~在 similaritySearch 时很差~~
      - 跟推荐qwen/granite

- resources
  - [RAG+AI工作流+Agent：LLM框架该如何选择，全面对比MaxKB、Dify、FastGPT、RagFlow、Anything-LLM, 以及更多推荐 - 知乎 _202407](https://zhuanlan.zhihu.com/p/711761781)
  - [[RAG优化] 支持中文的开源 embedding models 综述 - 知乎](https://zhuanlan. zhihu.com/p/1888778722225681562)
# draft
- rag as a service(细分市场)
  - doc-search as a service, for static-sites/note-taking/papers
  - code-search
# dev-xp
- 实测Ollama的embedding的过程对内存消耗小, 大文档chunk和embedding耗时可能较长
# discuss-stars
- ## 

- ## 

- ## 

- ## 💥 i'm building a local rag webapp that supports to upload large pdfs, then convert to text , and doing chunking/embedding, then save to a vector db for retrieval with local llm.
  - i cannot find a solution that supports very large pdf, the memory is often overflowed, even causing system crash
  - is there any existing solution or better idea to do streaming pdf rag? I think streaming reading can lower the memory usage and achieve better performance.

- goals: streaming, lazy
- 可尝试在现有方案中找实现
  - 基于vlm的识别方案，本身就是流式输出内容

- LlamaIndex with Streaming
  - Supports incremental ingestion with SimpleDirectoryReader
  - Can process PDFs in chunks using file_extractor parameter
  - Works with vector stores that support batch insertion

- Unstructured.io
  - Designed specifically for large document processing
  - Supports streaming mode for PDFs

- LangChain with PyMuPDF/PyPDF
  - `PyMuPDFLoader` can load pages incrementally

- Implementation Strategies
  - Strategy 1: Page-by-Page Streaming
  - Strategy 2: Batch Processing with Memory Limits
    - Process N pages at a time, Flush to vector DB after each batch
  - Strategy 3: Use Memory-Mapped Files
    - Libraries like `pymupdf` support memory-mapped reading
    - OS handles paging automatically
    - Good for very large PDFs (GB+)

- 
- 
- 
- 
- 
- 

- ## 🖼️📄📈 [Multi-modal RAG at scale: Processing 200K+ documents (pharma/finance/aerospace). What works with tables/Excel/charts, what breaks, and why it costs way more than you think : r/LLMDevs _202510](https://www.reddit.com/r/LLMDevs/comments/1o5oaas/multimodal_rag_at_scale_processing_200k_documents/)
  - TL; DR: Built RAG systems for 10+ enterprise clients where 40-60% of critical information was locked in tables, Excel files, and diagrams. Standard text-based RAG completely misses this. 
  - This covers what actually works, when to use vision models vs traditional parsing, and the production issues nobody warns you about.
- Here's what nobody tells you: most enterprise knowledge isn't in clean text. It's in Excel spreadsheets with 50 linked sheets, tables buried in 200-page PDFs, and charts where the visual layout matters more than any text.
- Why Text-Only RAG Fails
- Quick context: pharmaceutical client had 50K+ documents where critical dosage data lived in tables. Banks had financial models spanning 50+ Excel sheets. Aerospace client's rocket schematics contained engineering specs that text extraction would completely mangle.
  - When a researcher asks "what were cardiovascular safety signals in Phase III trials?" and the answer is in Table 4 of document 8, 432, text-based RAG returns nothing useful.
- The Three Categories (and different approaches for each)
- 📌 Simple Tables
  - Standard tables with clear headers. Financial reports, clinical trial demographics, product specifications.
  - What works: Traditional parsing with `pymupdf or pdfplumber` , extract to CSV or JSON, then embed both the structured data AND a text description. Store the table data, but also generate something like "Table showing cardiovascular adverse events by age group, n=2, 847 patients." Queries can match either.
  - Production issue: PDFs don't mark where tables start or end. Used heuristics like consistent spacing and grid patterns, but false positives were constant. Built quality scoring - if table extraction looked weird, flag for manual review.
- 📌 Complex Visual Content
  - Rocket schematics, combustion chamber diagrams, financial charts where information IS the visual layout.
  - Traditional OCR extracts gibberish. What works: Vision language models. Used Qwen2.5-VL-32b for aerospace, GPT-4o for financial charts, Claude 3.5 Sonnet for complex layouts.
  - The process: Extract images at high resolution, use vision model to generate descriptions, embed the description plus preserve image reference. During retrieval, return both description and original image so users can verify.
  - The catch: Vision models are SLOW and EXPENSIVE. Processing 125K documents with image extraction plus VLM descriptions took 200+ GPU hours.
- 📌 Excel Files (the special circle of hell)
  - Not just tables - formulas, multiple sheets, cross-sheet references, embedded charts, conditional formatting that carries meaning.
  - Financial models with 50+ linked sheets where summary depends on 12 others. Excel files where cell color indicates status. Files with millions of rows.
  - 💡 For simple Excel use pandas. 
  - For complex Excel use `openpyxl` to preserve formulas, build a dependency graph showing which sheets feed into others. 
  - For massive files, process in chunks with metadata, use filtering to find right section before pulling actual data.
  - 💡 Excel files with external links to other workbooks. Parser would crash. Solution: detect external references during preprocessing, flag for manual handling.
  - Vision model trick: For sheets with complex visual layouts like dashboards, screenshot the sheet and use vision model to understand layout, then combine with structured data extraction. Sounds crazy but worked better than pure parsing.

- When to Use What
  - Use traditional parsing when: clear grid structure, cleanly embedded text, you need exact values, high volume where cost matters.
  - Use vision models when: scanned documents, information IS the visual layout, spatial relationships matter, traditional parsers fail, you need conceptual understanding not just data extraction.
  - Use hybrid when: tables span multiple pages, mixed content on same page, you need both precise data AND contextual understanding.
  - Real example: Page has both detailed schematic (vision model) and data table with test results (traditional parsing). Process twice, combine results. 
  - 💡 Vision model explains schematic, parser extracts exact values.

- Production Issues Nobody Warns You About
  - Tables spanning multiple pages: My hacky solution detects when table ends at page boundary, checks if next page starts with similar structure, attempts to stitch. Works maybe 70% of the time.
  - Image quality degradation: Client uploads scanned PDF photocopied three times. Vision models hallucinate. 
    - 💡 Solution: document quality scoring during ingestion, flag low-quality docs, warn users results may be unreliable.
  - Memory explosions: Processing 300-page PDF with 50 embedded charts at high resolution ate 10GB+ RAM and crashed the server. 
    - 💡 Solution: lazy loading, process pages incrementally, aggressive caching.
  - Vision model hallucinations: This almost destroyed client trust. Bank client had a chart, GPT-4o returned revenue numbers that were close but WRONG. Dangerous for financial data. 
    - 💡 Solution: Always show original images alongside AI descriptions. For critical data, require human verification. Make it clear what's AI-generated vs extracted.

- The Metadata Architecture
  - This is where most implementations fail. You can't just embed a table and hope semantic search finds it.
  - For tables I tag content_type, column_headers, section, what data it contains, parent document, page number. 
  - For charts I tag visual description, diagram type, system, components. 
  - For Excel I tag sheet name, parent workbook, what sheets it depends on, data types.
  - Why this matters: When someone asks "what were Q3 revenue projections, " metadata filtering finds the right Excel sheet BEFORE semantic search runs. Without this, you're searching through every table in 50K documents.

- Cost Reality Check
  - Multi-modal processing is EXPENSIVE. For 50K documents with average 5 images each, that's 250K images. At roughly one cent per image with GPT-4o, that's around $2, 500 just for initial processing. Doesn't include re-processing or experimentation.
  - Self-hosted vision models like from Qwen need around 80GB VRAM. Processing 250K images takes 139-347 hours of compute. Way slower but cheaper long-term for high volume.
  - My approach: Self-hosted models for bulk processing, API calls for real-time complex cases, aggressive caching, filter by relevance before processing everything.

- What I'd Do Differently
  - Start with document quality assessment - don't build one pipeline for everything. 
  - Build the metadata schema first - spent weeks debugging retrieval issues that were actually metadata problems. Always show the source visual alongside AI descriptions. 
  - Test on garbage data early - production documents are never clean. Set expectations around accuracy - vision models aren't perfect.

- Multi-modal RAG pays off when critical information lives in tables and charts, document volumes are high, users waste hours manually searching, and you can handle the complexity and cost.
  - Skip it when most information is clean text, small document sets work with manual search, budget is tight and traditional RAG solves 80% of problems. 
  - Real ROI: Pharma client's researchers spent 10-15 hours per week finding trial data in tables. System reduced that to 1-2 hours. Paid for itself in three months.
- Multi-modal RAG is messy, expensive, and frustrating. But when 40-60% of your client's critical information is locked in tables, charts, and Excel files, you don't have a choice. The tech is getting better, but production challenges remain.

- My questions would be as a provider/consultant, how do provide support and maintenance moving forward? Long term, how do you ensure the old way of them putting data in tables is easily digested into the new RAG system automatically or that someone owns the knowledge base? The “data cleaning” and organization seems like a full time contract just by itself. Then, how do you test for accuracy and showcase those results to stakeholders for renewal or as case studies for other businesses?
  - support and maintenance was something i completely underestimated early on. did the typical "build it and hand off" approach with my first few clients. total disaster. systems would work great for 2-3 months then drift, new document types would break the pipeline, accuracy would drop. now i do hybrid - initial build plus ongoing support contract. usually quarterly check-ins, pipeline updates when they add new document types, on-call for critical issues.
  - for data cleaning i train someone on their team to own document quality. they become the gatekeeper, i provide the tooling. the alternative where i do it forever doesn't scale and they know their domain way better anyway. built quality detection into the ingestion pipeline that flags problematic docs automatically but someone still needs to make decisions about what to do with garbage scans from the 90s.
  - testing is golden test sets with domain experts - 100-200 real questions with known answers. run these quarterly but focus stakeholder reports on business metrics they actually care about like "researchers spend 2 hours per week searching vs 15 hours before" or "regulatory response time dropped from 5 days to 6 hours."
  - initial builds were $50k+ (currently 100k+) but support contracts run $3k-5k monthly. way more profitable long-term plus you learn edge cases that feed back into the product and i'm full-time on this, but trying to build something in the rag space as well.

- i’ve battled the same multi‑modal rag pain at scale in pharma/finance/aerospace. if you want this to survive production, bake in lineage, governance, and observability from day one, not after it drifts.
  - table-first retrieval: tag content_type, column_headers, section, page, and parent doc; prefilter by metadata before semantic search so “q3 revenue projections” lands on the right sheet/table.
  - excel lineage and verification: parse formulas with openpyxl, build a cross‑sheet dependency graph, bind screenshots of dashboards to underlying cells when layout matters, and require human verification for any financial figures the vlm “reads.”
  - vlm governance and cost controls: quality-score every image/page, batch and cache captions, separate “conceptual” descriptions from “numeric” extraction, and run a quarterly golden test set that mixes tables, scanned PDFs, and charts.
  - production observability: trace every ingestion step (parse, stitch, caption, embed), cap memory per page, add fallbacks for multi‑page table stitching, and alert on eval drift rather than waiting for user complaints.
- maxim ai helps here with end‑to‑end evaluation, simulation, experimentation, and observability for agents and rag pipelines: scenario-based tests at scale, prompt/version experiments, live tracing with online evaluations, ci/cd hooks, and enterprise deploy options. (builder here!)

- I'm currently working on a solution to address product cataloging issues for an ecommerce platform. Right now, analysts manually review Excel files and images, then fill out Excel templates with product attributes (title, description, features, etc.). My proposed solution would automatically extract attributes from files, populate templates, validate images, and extract attributes from images (like dimensions in cm, brand, model, and others). Also check images if this image is "main", "lateral", "left view", "right view" for an SKU and if these images contains a QR code.
  - The main challenge I'm facing is that the image processing workflow is too slow and expensive (using GPT-4o model). 
  - The goal is to scale up to processing 1, 000, 000 product reviews daily. I'm currently using AWS with Fargate jobs that launch dockerized processes for image processing, orchestrated by Step Functions.
  - Currently handling <1, 000 SKUs daily, which is far from the 1, 000, 000 target.
  - Any recommendations or advice for optimizing this process?

- If table with headers , and each table column is well aligned , in most scenarios, you can check the column alignment condition and assuming that table schema did not change to determine whether table contents flow over pages

- ## [Using LMStudio for RAG/File Search with LibreChat? · danny-avila/LibreChat _202506](https://github.com/danny-avila/LibreChat/discussions/7713)
  - I run LibreChat locally inside Docker, I run local models in LMStudio, and want to use LMStudio's nomic (or otherwise) embedding capabilities instead of an external provider like OpenAI.
  - (A) i want to do it for free/private locally, and (B) especially because when I tested file upload directly within LMStudio [using its RAG] it correctly pulled all text from the PDF, but when I used OpenAI cloud embedding it missed a huge chunk of the text—perhaps because the API version uses a text-only embedding model without vision
- UPDATE / SOLUTION:
  - Making a copy of the config.py file in my LibreChat root folder and pointing the compose-override to it did solve the problem and allowed me to use the openai embeddings with LMStudio. I seconded the feature request to make this an easy option for people to opt into

- been down that rabbit hole too, and yep: this kind of embedding mismatch + RAG retrieval chaos is super common when things try to speak in different tensor dialects.
  - the error from LMStudio (input field must be a string or array of strings) usually hits when the upstream retrieval returns a raw int list or malformed embedding body. 
  - i eventually got tired of patching these one by one and built a semantic rescue engine that stabilizes the entire pipeline.

- ## 🤔 [RAG（检索增强生成）会不会消亡呢？一旦大模型的Context Length变大，RAG还有存活的必要吗？ - 知乎](https://www.zhihu.com/question/637421964)
- RAG 的基本原理并不复杂：
  1.  将长文档切分成多个 **chunk**；  
  2.  通过向量化模型（如 [OpenAI Embeddings] 、Sentence-Transformer）为每个 chunk 生成向量，并存入数据库；  
  3.  在用户提问时，检索出 **Top-K 相似文档**；  
  4.  把这些文档与问题一起输入大模型，作为额外上下文；  
  5.  大模型基于问题 + 检索结果，生成更准确的回答。
- 简单来说，RAG 就像是给大模型装上了一个“外挂搜索引擎”。
  - 相比之下，传统的 微调（Fine-tuning） 方式虽然能把新知识写进模型，但往往成本高昂、不可逆，还可能“牺牲”原有能力。而 RAG 的优势在于：轻量、灵活、随取随用
- 目前大多数 RAG 系统其实是“Frozen RAG”——Retriever 与 LLM 是分开的，Retriever 固定不变，LLM 也不更新。它们拼在一起能跑，但模块之间并没有深度协同。
- RAG 2.0 的核心目标就是： 让检索器和生成器成为一个“可共同训练”的整体，从而达到端到端的优化。

- 从纯业务端的角度来说，不但不会消亡，还有可能在未来的3-5年里大行其道。
  - 表面原因非常简单：RAG几乎是目前唯一一种兼具门槛低+可观察+控制准+见效快的路线。
  - 最后提一嘴深层原因：RAG的技术路线极其符合国情，其本质是真理灌顶且可以随时替换，比大炼模型得到的醉拳幻觉可控得多。
  - To B和To G都是数据密集型对象，自身数据就是最大的筹码，不要指望人家会把身家性命交到AI厂商手里，去打造一个遥遥领先的大模型。
- 大模型目前没看到企业内好的落地场景。rag大部分是用于知识库，但是也就基本能用，如果提问不能从关键词和向量上匹配，那你给大模型的内容就和问题无关，自然答案就不对。并且文档拆分后，逻辑上就被拆分了，很多问题是要从各个文档逻辑上分析，不是简单的检索。

- 回顾下当前市场上企业 RAG 知识库落地的三种主流路径。
- 直接使用高层级开源框架
  - 这类框架如 RAGFlow, Dify, FastGPT 等，主要特点是提供相对完整、开箱即用的 RAG 工作流，
  - 目标是简化 RAG 应用的搭建过程，降低开发门槛。
  - 反之，劣势主要是定制化和灵活性受限，深度优化和集成特定组件时复杂度较高。
- 底层开发框架自主开发
  - 这类框架包括 LangChain, LlamaIndex, Haystack 等，都提供了一系列模块化的构建块、工具和接口。开发者可以根据需求灵活组合和编排 RAG 流程的各个环节（如数据加载、文本分割、嵌入、向量存储、检索策略、LLM 调用、记忆管理、Agent 构建等）。
  - 优势很明显就是灵度灵活，定制化能力强，能够针对特定业务场景进行深度优化和集成。适合对 RAG 流程有精细化控制需求的企业。
  - 反之劣势就是需要更多的开发工作量和技术深度。
- 云厂商 MaaS 平台方案
  - 如阿里云百炼, 百度智能云千帆, AWS Bedrock, Google Vertex AI Search 等的私有化部署方案，无论是国内还是国外的这些云服务商，都是把 RAG 相关的能力封装成服务或提供私有化部署包，通常与自家的大模型、计算资源、数据存储等深度集成。一般也会提供模型选择、微调、部署、监控等一站式服务。
  - 采用这种方案通常能提供稳定的基础设施、便捷的模型管理和部署、以及与其他云服务的良好兼容性。对于已经深度使用特定云生态的企业来说，集成成本较低。
  - 但劣势就如同使用大模型一体机一样，可能存在厂商锁定的风险，跨云迁移或集成非该厂商的服务可能会比较复杂。
  - 当然，费用和灵活性也需要考虑。
- 总结来说，实际生产场景中以上三种选择并非完全互斥，例如以底层框架为基础，但借助云厂商的部分模型服务或基础设施也是中目前常见的组合。

- RAG主要可以解决大模型幻觉问题，以及通过外挂知识，避免模型频繁进行知识更新
  - 即使模型可接受上下文长度为128k，但是我的知识库里有10w篇文档，远远超过模型的上下文长度，所以你还是需要检索。
  - 当然模型上下文长度变长，对于检索更加有好，粒度变大，召回变高，相辅相成。
  - 即使你可以接受128k的长度，但是你的设备消耗不起，更大的长度需要更多的显存，模型部署成本更高，速度更慢。
  - 如果你调用api，那token消耗也太大了，成本过高。

- Context Length 变大 ≠ 不需要 RAG
  - 成本问题: 上下文越长，推理成本（显存、时间、算力）会线性甚至超线性增加。 比如，100k tokens 处理一次就很烧钱，而 RAG 可以用较短上下文反复调用。
  - 信息检索效率: 如果你有 1TB 的知识库，把它全塞进上下文是不可能的。 RAG 先检索，再送进上下文，可以让模型专注于相关信息。
  - 噪音与干扰: 大上下文并不代表模型会忽略无关信息，相反太多无关内容会稀释关键信息，导致推理效果下降。RAG 的“检索+过滤”能提高信噪比。
- Context 变大后，RAG 的形态会演化
  - 从“查找资料”到“动态知识组织”: 未来的 RAG 可能不只是检索，而是自动生成一个临时的知识摘要/知识图谱再交给大模型
  - 多阶段推理（Multi-turn Reasoning）: 大上下文允许一次性放更多信息，但 RAG 可以在每一步推理时更新上下文，形成 交互式推理
  - Hybrid RAG（混合模式）: 把静态知识（常用信息）直接放在长上下文里，把动态数据（实时信息、搜索结果）用 RAG 方式插入。
- 为什么 RAG 在长上下文时代依然重要
  - 可更新性: 模型训练数据是静态的，RAG 可以在不重新训练的情况下引入最新知识。
  - 隐私与定制化: 私有企业或个人数据不会直接放到大模型里，而是通过 RAG 动态注入。
  - 减少幻觉: 模型直接引用检索到的原文，可以显著降低胡编乱造的概率。
  - 多模态检索: RAG 未来会不仅是文本，还会检索图片、视频、音频、结构化数据，再统一给大模型处理
- 未来 RAG 的重点会从“找文档”变成“构建最优推理上下文”，它会变得更智能、更动态。
  - 随着 Context > 1M tokens，部分场景可直接用大模型的长记忆，但 RAG 会演变为“智能知识编排器”。
  - 如果出现无限上下文且推理成本极低的模型，RAG 会退化成“数据索引工具”，主要用于加速数据组织而不是必须步骤。

- 不会。上下文长度变长只会让RAG更好用。从目前的情况来看，RAG的成本依旧低于微调，效果高于微调。然后目前llm应用的本质还是prompt，没有什么大花样，也脱离不了现有的人类学科。
  - 当然，如果有人强行说RAG就是用嵌入向量什么的，那么我只能说可能会消亡。retrieval 肯定是包括了其他方式的，我们用gemini发文件或者图片给他何尝不是一种RAG呢，不过只是人脑驱动罢了

- ## RAG is anti pattern.
- https://x.com/pelaseyed/status/1882471632129994914
  - I don’t do RAG anymore, get 10x the result just spinning up a pipeline and feed all content to Deepseek. And yes it scales to over 10K docs. 

- And you can cache it, so doesn’t even cost that much

- Does deepseek have caching like Google’s media.upload? How do you otherwise avoid rebuilding the context all the time (I’ve not used the DS APIs).

- I wish I could fit the entire Internet in the prompt for @ask_pandi but it doesn't fit. RAG is still needed for this.
  - Run multiple LLMs in parallell, you will have infinite context window.

- You put everything into context?
  - Everything in context(s)

- RAG is A pattern, just not useful when your context is under 128k token and when the context is known. Pick the right tool for the job.
# discuss-solutions
- ## 

- ## 

- ## [Rebuilding RAG After It Broke at 10K Documents : r/LlamaIndex _202512](https://www.reddit.com/r/LlamaIndex/comments/1pgyedh/rebuilding_rag_after_it_broke_at_10k_documents/)
  - What Broke at 10K
- Latency Explosion: Went from 100ms to 2000ms per query.
  - Root cause: scoring 10K documents with semantic similarity is expensive.
- Memory Issues
  - 10K embeddings in memory. Python process using 4GB RAM. Getting slow.
- Semantic search on 10K documents = 10K LLM evaluations eventually = money.
- What I Rebuilt To
- Step 1: Two-Stage Retrieval
  - Stage 1: Fast keyword filtering (BM25) 
  - Stage 2: Accurate semantic ranking
- Step 2: Vector Database
  - Move embeddings to a proper vector database (not in-memory).
- Step 3: Caching
- Step 4: Metadata Filtering
- Step 5: Quality Monitoring

- What I Learned
  - Two-stage retrieval is essential - Keyword filtering + semantic ranking
  - Use a vector database - Not in-memory embeddings
  - Cache aggressively - 40% hit rate is typical
  - Monitor continuously - Catch quality degradation early
  - Use metadata - Filtering improves quality and speed
  - Test at scale - What works at 500 docs breaks at 10K

- What you’re describing isn’t RAG fundamentally “breaking” at 10K docs, it’s your naive implementation breaking. 
  - Brute-force similarity in pure Python, mis-modeled costs, and in-memory everything will obviously struggle as you scale. 
  - The architecture you rebuilt (BM25 → vector DB → caching → metadata → monitoring) is solid and very standard, but 10K documents is not a meaningful scaling limit. The story is really “I started with a toy prototype and then replaced it with something closer to a normal production RAG stack, ” not “RAG inherently breaks beyond 10K docs.”
- This could have been limited to: I replaced my own in memory solution with a vector database.

- ## [RAGFlow is an open-source RAG engine based on OCR and document parsing | Hacker News _202404](https://news.ycombinator.com/item?id=39896923)
- Document processing is getting better and better with new tools leveraging LLMs. If anyone is interested in exploring this space, try another similar tool LLMWhisperer (https://llmwhisperer.unstract.com/). It is a part of Unstract, an open-source document processing tool (https://github.com/Zipstack/unstract)
  - Actually we've tried almost all lof existing open source models for document processing, and none of them performs well for complex documents, especially those having complicated tables, such as tables cells without borders, cells need to be combined, ..., etc. Although adopting LLMs to perform such document understanding tasks is more scalable, it requires much more data and computation power to achieve similar results. That's why we design such models start from scratch.

- I'm partly sad at the approach this and other engines take: reimplement each part (PDF parser, etc etc) in a way where they are pretty much useless except in their specific engine.
  - If instead we had a PDF() class that did what RAGFlow is doing (dealing with all the different trade-offs of the different python PDF engines such as pdfplumber), then we could easily adapt it and improve it, and it can be useful for other projects as well.
- It is open-source though. Just rip it off and make that PDF() class.

- A lot of the yolo stuff from ultralytics is AGPL3 fyi. Recommend caution depending on what code or models / model lineage are used
  - Thanks for your nice suggestion. We train the model using YOLO, but during inference, the model is converted into ONNX and we use ONNXRuntime for the model inference. As a result, YOLO itself is not included in the software package. We will open the training code in the repo soon.
  - We've used YOLOv8 as the object detection model, and use some public datasets, such as PubTable, CDLA, together with some private data to train the model. The model on Huggingface is the one trained using public dataset, and we would open this work later. We use YOLOv8 just because we want to let the document parser run without GPU, I think you could also try any other object detection models such as Detectron, and use the public datasets to train the model as well. We've not used transfomers for this task, because given limited data, it could not outperform traditional CNN based models.

- ## agentset - [Production RAG: what I learned from processing 5M+ documents | Hacker News _202510](https://news.ycombinator.com/item?id=45645349)
- I must be missing something, this says it can be self-hosted. But the first page of the self-hosting docs say you need accounts with no less than 6 (!) other third-party hosted services.
  - That was my observation as well. To be fair their business is to sell a hosted version, they’re under no obligation to release a truly self hosted version.

- The big LLM-based rerankers (e.g. Qwen3-reranker) are what you always wanted your cross-encoder to be, and I highly recommend giving them a try. Unfortunately they're also quite computationally expensive.

- Similar writeup I did about 1.5 years ago for processing millions of (technical) pages for RAG. Lots has stayed the same it seems

- > Reranking: the highest value 5 lines of code you'll add. The chunk ranking shifted a lot. More than you'd expect. Reranking can many times make up for a bad setup if you pass in enough chunks. We found the ideal reranker set-up to be 50 chunk input -> 15 output.
  - Reranking is a specialized LLM that takes the user query, and a list of candidate results, then re-sets the order based on which ones are more relevant to the query.
- What is the difference between reranking versus generating text embeddings and comparing with cosine similarity?
  - If you generate embeddings (of the query, and of the candidate documents) and compare them for similarity, you're essentially asking whether the documents "look like the question."
  - If you get an LLM to evaluate how well each candidate document follows from the query, you're asking whether the documents "look like an answer to the question."
- text similarity finds items that closely match. Reranking my select items that are less semantically "similar" but are more relevant to the query.
- Because LLMs are a lot smarter than embeddings and basic math. Think of the vector / lexical search as the first approximation.

- ## [28M Tokens Later: How I Unfucked My 4B Model with a smart distilled RAG : r/LocalLLM _202512](https://www.reddit.com/r/LocalLLM/comments/1pcwafx/28m_tokens_later_how_i_unfucked_my_4b_model_with/)
  - I've recently been playing around with making my SLM's more useful and reliable. I'd like to share some of the things I did
- TLDR
  - Use a strong model to write clean, didactic notes from source docs.
  - Distill + structure those notes with a local 8B model.
  - Load distilled notes into RAG (I love you, Qdrant).
  - Use a 4B model with low temp + strict style as the front‑end brain.
  - Let it consult RAG both for facts and for “who should answer this?” policy.
- With a GOOD initial summary (and distillation) you can make a VERY capable little brain, that will argue quite well from first principles. Be aware, this can be a lossy pipeline...so make sure you don't GIGO yourself into stupid. IOW, trust but verify and keep both the source material AND SUMM-file.md until you're confident with the pipeline. (And of course, re-verify anything critical as needed).
  - I tested, and retested, and re-retest a lot (literally 28 million tokens on OR to make triple sure), doing a bunch of adversarial Q&A testing, side by side with GPT5, to triple check that this worked as I hoped it would.
  - The results basically showed a 9/10 for direct recall of facts, 7-8/10 for "argue based on my knowledge stack" or "extrapolate based on knowledge stack + reference to X website" and about 6/10 on "based on knowledge, give me your best guess about X adjacent topic". That's a LOT better than just YOLOing random shit into Qdrant...and orders of magnitude better than relying on pre-trained data.
- my RAG set up -
  Chunk size: 600
  Chunk o/lap: 175
  Embedding model: e5-small-v2
  Re-ranker: TinyBERT
  Top K: 6
  Top K_reranker: 4
  Relv score: 0
  BM25 weight: 0.6
  Qdrant embeds at 384 DIM. 
- TL; DR - everything is small and fast on hardware constrained rig (I7-8700, 32GB ram, 4GB Quadro P1000)

- So I've been thinking about this a lot and might embark on the same journey. Been playing with RAG pipelines a bit and am not hating it.

- Your distilled-notes-first approach is right; layer a strict retrieve-then-rerank, corpus hygiene, and automation to keep it sharp.
  - Concrete tweaks that worked for me: chunk 800-1200 tokens with small overlap and rich metadata (doc_id, section, version, date). Generate multi-query variants or HyDE to lift recall, then rerank with a local cross-encoder (bge-reranker-v2) before the 4B synthesizes. Add a confidence gate: if top reranked scores fall below threshold, return “insufficient evidence” or escalate to the 8B. Use Qdrant payload filters to scope “buckets” and set MMR to avoid near-duplicate chunks. Hash paragraphs and re-embed only changed ones
  - Bottom line: distill first, then tight retrieve-then-rerank with guardrails, thresholds, and evals.

- ## 💡 [I spent 2 years building privacy-first local AI. My conclusion: Ingestion is the bottleneck, not the Model. (Showcase: Ollama + Docling RAG Kit) : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pamu5t/i_spent_2_years_building_privacyfirst_local_ai_my/)
  - I’ve been working on strictly local, data-privacy-compliant AI solutions for about two years
  - The biggest lesson I learned: We spend 90% of our time debating model quantization, VRAM, and context windows. But in real-world implementations, the project usually fails long before the prompt hits the LLM. It fails at Ingestion.
  - I built a self-hosting starter kit that focuses heavily on fixing the Input Layer before worrying about the model.
  - Ingestion: Docling (v2). I chose this over PyPDF/LangChain splitters because it actually performs layout analysis. It reconstructs tables and headers into Markdown, so the LLM isn't guessing when reading a row.
  - I’d love to hear your thoughts on the "Ingestion First" approach. For me, switching from simple text-splitting to layout-aware parsing was the game changer for retrieval accuracy.

- I chose Docling primarily for Structure and Integration.
  - Structure vs. OCR: Paddle is great for raw OCR, but I needed Layout Analysis (reconstructing tables to Markdown). Paddle gives me text boxes; Docling gives me semantic context. For RAG, context is king.
  - Simplicity: Since I'm building a local desktop app, Docling felt much more 'native' to integrate into a Python backend than the Mineru stack. However, I'm pragmatic, not married to a tool.
  - I designed the ingestion pipeline to be modular. If Mineru proves to be significantly lighter or better at tables tomorrow, I can swap the engine. But right now, Docling hits the sweet spot between performance and setup pain.

- It took me a few months to understand quality of OCR matters the most, and anyone working on RAG that has used VLMs for OCR knows in their heart and soul that VLMs make the best OCR. Obviously this means, in addition to LLMs/Embedding Models there is a new expensive overhead of VLMs, unless you use higher up models, then you can do text gen + OCR from a single model.
  - How can you make an effective RAG project without decent hardware? 
  - You need 98% accurate OCR or your pipeline fails. 
  - You need a large context window so that full context of the document being retrieved can be loaded, granted, we can use chunking like we do with embeddings, but to me, this is an untested theory.
  - 8, 000 tokens is a lot of tokens, requires just a little less than 24 GB VRAM, issue is, how may people doing this locally on their potato laptop actually have 24 GB VRAM.
  - Not to mention re-rankers.
- Sounds like in-depth knowledge from my point of view ; ) VLMs produce better OCR than traditional parsers, but I think you're optimizing for the wrong bottleneck.
  - The 98% accuracy trap: You don't actually need 98% OCR accuracy if your pipeline is error-tolerant. A 90% accurate parse + a reranker + a small cleanup LLM can outperform a 98% parse that costs 10x more to run.
  - Why I optimize for 'good enough' hardware: My clients are mostly in Germany (GDPR-heavy industries). They prioritize local/privacy over raw performance. For them, the ROI calculation is simple:
  - The real question isn't 'How do I get 98% OCR?' It's: 'How do I build a system that works even when OCR fails 10% of the time, and runs 100% locally?'
  - That's why I focus on the pipeline (repair -> parse -> cleanup -> chunk -> rerank) rather than just throwing a bigger GPU at the problem. I still believe we focused on the wrong side and were blindsided vor the longterm issues

- looking at the flood of 'Why is my RAG hallucinating?' posts, it seems to be news for the 90% of developers who just joined the party via LangChain
  - And yes, even Docling struggles. That's exactly why I argue for a 'Sanitized Pipeline' (repair -> parse -> post-process) rather than just looking for a magic OCR tool. The 'pain' never goes away completely, but you can engineer around it. There is more after docling and bevor db ; )

- ## [Best open source document PARSER??!! : r/LlamaIndex](https://www.reddit.com/r/LlamaIndex/comments/1dicqkt/best_open_source_document_parser/)
  - Right now I’m using LlamaParse and it works really well. I want to know what is the best open source tool out there for parsing my PDFs before sending it to the other parts of my RAG.

- Marker is quite nice but not enough to get quality data from complex PDFs.

- I'd look into Unstructured, PyMuPDF, PyPDF, PDF.js

- Try RAGFlow https://github.com/infiniflow/ragflow which is based on deepdoc based document undertanding for better chunking results.

- i made marker+pix2tex combo and lamaParser/mathpix for complex documents

- Docling and Marker are really good open source document parsers. But obviously nothing compared to paid services. But is good enough. Docling especially works well with tabular data and layout analysis. And it also read images

- ## [How to Efficiently Parse Large PDF and DOCX Files (in GBs) for Embeddings Without Loading Fully in Memory? : r/Rag _202411](https://www.reddit.com/r/Rag/comments/1gjz2dj/how_to_efficiently_parse_large_pdf_and_docx_files/)
- Most pdf reading libraries use a .load function for each page. You can just control which pages it's called on and use garbage collectors if necessary

- pymupdf can load by page I think

- For handling massive PDFs or DOCX files, you’ll want to look into libraries that support lazy loading and streaming. For PDFs, PyMuPDF (with fitz) or PDFMiner allows you to read specific pages directly without loading the whole thing into memory. For DOCX, python-docx doesn’t have native streaming, but using it with smaller chunks of extracted text can work. If you’re embedding, try handling these chunks individually instead of full files, as it cuts down memory use.

- Snapshot each page as an image > pixstral > markdown > chunk > use something like Antrhopics contextual retrieval to embed global context in each chunk

- this might be exactly what you need. its very fast and has buffered streaming: https://github.com/yobix-ai/extractous

- ## [I've been noticing more and more people are using GraphRAG instead of embedding and vector databases...is it really helpful or just the hype? : r/LangChain _202507](https://www.reddit.com/r/LangChain/comments/1e66e9r/graphrag/)
- Been working with graphrag on my current project. It is good, but it has its fallbacks. The good thing is that you can model you data to preserve relations. 
- The bad thing is:
  - you rely on your LLM to create queries based on your question to the answer. Lots of times the query created is pure shit, even with the most advanced models.
  - It gets really expensive. Like really expensive. Imagine that for every document you're storing in your graphDB you need to pass it to a LLM so it can extract the content and create relations so you can store it on your DB.

- If you ask me, people just follow the trends without understanding whether their application really needs something (eg GraphRAG here). 

- This is all basically more of a hype I would say. Why? Because you can use your own database that handles multiple data types and construct a knowledge graph. The knowledge graph basically shows the entity relationship between different nodes and this can be easily fed into your databases as tables and then, using retrieval methods, you can easily retrieve the most relevant chunk and the relationship score. 
  - I mean, the specialise databases like vector databases or even graph databases are really hyped, your own databases whether it is MongoDB, SingleStore, MariaDB, or even Couchbase can easily help you with creating graph knowledge and store them and then retrieve whenever required.

- how GraphRAG works with existing graphs, meaning if I already have entities and relationships, how would I load this graph in GraphRAG? 

- ## 有没有想过将自己的代码库打包然后直接塞给大语言模型来处理？也许你会想到用RAG或者用windsurf或cursor。现在有了更简单的办法——Repomix
- https://x.com/karminski3/status/1881150047276138689
  - 这个库可将整个存储库打包到一个 AI 友好的文件中，方便给大语言模型使用。

- ## 📌 A list of software that allows searching the web with the assistance of AI.
- https://x.com/tom_doerr/status/1856778512612667838

# discuss-pdf/docs
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Practical (online & offline) RAG Setups for Long Documents on Consumer Laptops with <16GB RAM : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1hq36dn/practical_online_offline_rag_setups_for_long/)
  - there are a ton of different frameworks and libraries to implement a RAG system. For the purpose of my tests, I only focused on those with a UI or offering an already made RAG pipeline, because I did not yet learn how to implement RAG by myself.
  - Various offline and online LLM models: phi-3.5-mini, gemma2-2b-it, mistral, phi-4, Hermes2.5, Ghost, Qwen2.5:1.5b, Qwen2.5:7b, 
  - RAG Frontends: msty, anythingLLM, Witsy, RAGFlow, Kotaemon, khoj.dev, Dify, etc. (OpenWebUI failed to install on my machine, QwenAgent remains to be tested)
  - Backend: ollama, ChatGPT, Gemini.
  - I found only two working solutions for the multi-needles test to succeed 4 out of 4 (4/4):
  - Either without RAG using LLM models that implement infini-attention. Although the method has been published openly, currently, only the Gemini models (online, including the free Flash models) implement it, offering 1M tokens context size. 
  - Either with a RAG that somehow mimics infinite attention. 
  - Note that in all successful cases, I found that making the prompt to be iterative (which is a change I did over ggerganov's original prompt) was necessary to increase the reliability of the retrieval, otherwise some questions (up to half of the questions) failed (even with Gemini IIRC).

- ## 🔡 [MongoDBAtlasVectorSearch the PDF exceeding 100 pages cannot be processed. How can this be resolved? · Issue · langchain-ai/langchain _202409](https://github.com/langchain-ai/langchain/issues/26518)
- We tried splitting a long PDF using this code

- ## [Best practices for handling large-scale RAG implementation with thousands of lengthy PDF documents _202508](https://community.latenode.com/t/best-practices-for-handling-large-scale-rag-implementation-with-thousands-of-lengthy-pdf-documents/34950)
  - Many of these documents are quite large, with some containing up to 300 pages each. All the PDFs have been processed through OCR, so I’m dealing with plain text content.
  - My main challenge is with the document ingestion phase into the knowledge base. I initially attempted to use an open webui setup with an ollama backend, but the performance was unacceptably slow for this volume of data.

- Been there with similar document volumes - the ingestion bottleneck will absolutely kill your project if you don’t handle it right.
  - Break this into parallel chunks instead of processing everything sequentially. Split those 300-page docs into smaller sections (10-20 pages each), then run multiple processing pipelines at once.
  - Don’t build this manually. Coordinating document splitting, embedding generation, vector storage, and error handling gets messy fast. You’ll debug pipeline issues more than actually using your RAG system.
  - I handled 25k documents last year using automation for the entire flow. Set up parallel streams processing ~500 documents simultaneously, with automatic retry for failed chunks and smart batching for vector database writes.
  - Latenode makes complex document pipelines like this really straightforward to build and manage. Check it out at https://latenode.com

- Had the same scalability nightmare building a RAG system for legal docs last year. Game changer was ditching sequential processing for parallel with a proper queue system. Used Celery + Redis to spread the work across multiple workers - cut processing time from weeks down to 2 days for ~25k documents. Also stopped using fixed-size chunks and parsed by sections/paragraphs instead to keep the meaning intact. Switched from Chroma to Weaviate for the vector DB - handles scale way better. Heads up on memory requirements - you’ll need tons of RAM or go with disk-based storage. Pro tip: test retrieval quality early because what works for hundreds of docs can fall apart at this scale.

- ## 🌰 [Chatting with Large PDFs (100–500 Pages): Using RAG with OpenAI Embeddings (Local vs. API) _202504](https://medium.com/coxit/chatting-with-large-pdfs-100-500-pages-using-rag-with-openai-embeddings-local-vs-api-2be2a73c20d4)

- COXIT decided to invest resources to evaluate research and develop a prototype
- COXIT wanted to validate and then evaluate approaches to consciously embed large documents (100–500 pages) into LLM’s context, how to make LLM operate, refer to, quote information from those PDFs, what document extraction and processing pipelines should look like.
- I keep intentionally avoiding Agentic Frameworks like LangChain, as they show no benefit from a long-term perspective, as they are generally poorly optimized and overbloated.

- Speaking about App’s Architecture (Figure 1): I designed it to consist of 4 microservices:
  - ChatUI — React-powered WebUI. I declare that the React code is notoriously badly written
    - https://github.com/v4ler11/llm-chat
  - Chat Tools Service — Handles completion requests, implements message history limiting, local tools execution and model validation, and files handling, including file stream uploads.
    - https://github.com/v4ler11/llm-tools-server
  - Chat Proxy Streamer — re-routes incoming chat completion requests to various LLM Providers e.g. OpenAI, Anthropic, Google using a standardized OpenAI Format, provides authentication, usage stats collecting.
    - https://github.com/v4ler11/llm-portal
  - Document Search MCP — a dedicated service that is only used to perform operations with documents: extraction, processing, storage, and vector search.
    - https://github.com/COXIT-CO/chat-with-pdf-poc

- Approach 1: OpenAI-based vector search
  - For each text-chunk or a paragraph (in case you are OK with OpenAI’s chunking strategies), you’d need to perform 2 requests to upload a paragraph as a file
- Approach 2: local vector search and storage, external embedding requests
  - an approach that is based on storing vectors locally and, consequently, performing vector search also locally, uses only 6* requests to fully process a given document. That’s a 200x improvement over the previous approach. Total waiting time for processing a document resulted in 11s — that’s 14x improvement.
  - For 100-page document embeddings requests with batch-size = 128 were sent. For documents of other sizes, batch-size should also be adjusted to keep a minimal response time from an external embedding model. E.g., for 400-page document you might try 128 × 4 = 512 batch-size.

- When this prototype is used in real-life projects, we’d have to set up a more precise validation pipeline, taking into account documents’ domain. That pipeline should be centered about the same idea: measure the difference between model response in 2 cases: when the model has all context needed to answer a question e.g., provide a complete document and a 2nd case: when the model will have to use RAG calls to retrieve that context.

- ## [Best Python library for fast and accurate PDF text extraction (PyPDF2 vs alternatives) : r/LangChain _202508](https://www.reddit.com/r/LangChain/comments/1mxye53/best_python_library_for_fast_and_accurate_pdf/)
- Pymupdf is faster than docling. 10-50x

- Check out `pdfplumber` for its flexibility and ability to handle complex PDF layouts. It might improve efficiency if PyPDF2 isn't meeting your needs.

- ## [Best way to extract data from PDFs and HTML : r/Rag _202510](https://www.reddit.com/r/Rag/comments/1oavnx4/best_way_to_extract_data_from_pdfs_and_html/)
- During my experience extracting data from PDFs and HTML files for use in RAG systems, I usually follow one of the two approaches shown in this notebook I created (VLM or docling/paddleOCR)— I hope you find it helpful. 

- Have you looked at Pinecone Assistant? You can upload PDFs (up to 100MB) and it manages the chunking, embedding, and search for you. If you already have chat/model generation, you could use just the /context API to get search results to feed into your own model.

- At PipesHub, we use docling, pymupdf (faster than docling but need to use layout parser on top of it), ocrmupdf/Azure DI (scanned pdfs).
  - On top of docling, we have specialized logic for extracting metadata, deep understanding of document, tables, etc. 
  - We use VLM/Mulitimodal AI models for handling images, diagrams and more.
  - You can use docling (only issue it's parsing is slow) if you are looking for open source, free solution.
  - If you are looking for Higher Accuracy, Visual Citations, Cleaner UI, Direct integration with Google Drive, OneDrive, SharePoint Online, Dropbox and more. PipesHub is free and fully open source, extensible. 

- I have done two approaches so far. Docling was good, but I was not happy that it took long on larger PDFs. 
  - Another approach was converting the pdf to docx, then docx to html and finally to markdown. This approach was quite fast, but `pdf2docx` library had some trouble converting certain documents.
  - Docling to me was quite a good solution, and if you are okay with the amount of time to process larger documents.
  - Overall, a hybrid approach is always the best solution.
# discuss-rag-local
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [I tested what small LLMs (1B/3B) can actually do with local RAG - Here's what I learned : r/LocalLLaMA _202410](https://www.reddit.com/r/LocalLLaMA/comments/1gdqlw7/i_tested_what_small_llms_1b3b_can_actually_do/)
  - Langchain RAG workflow
  - Nomic's embedding model
  - Chroma DB
  - Llama3.2 3B instruct
  - the smaller models (Llama3.2 3B in this case) start to break down with complex stuff. Ask it to compare year-over-year growth between different segments and explain the trends? Yeah... it start outputting nonsense.

- My use case would be finding rules for board games and tabletop RPGs when I only have a vague idea of what the rule does, or the name. I haven't found one that works too well yet- lots of false positives and no page numbers.

- While RAG systems typically search for relevant content from the source and pass it to an LLM as input for the LLM to write new content.  Maybe you just want to see the relevant content directly?  That's computationally cheap.

- 137M parameters isn't tiny for an embedding model! Embedding models are naturally much smaller than LLMs since they only convert text to vectors, rather than generating text and reasoning.
- Yes, I tested several small embedding models (under 1B parameters), including MXBai, but Nomic 1.5 performed the best. 

- ## 💡 [Embedding With LM Studio - what am i doing wrong : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1lharbh/embedding_with_lm_studio_what_am_i_doing_wrong/)
  - "text-embedding-nomic-embed-text-v1.5" loads fine and works with Anything.
  - but text-embedding-qwen3-embedding-0.6b & 8B and any other Embed model i use i get the below error: Failed to load embedding model. Internal error: Failed to initialize the context: failed to allocate compute pp buffers

- SOLVED
  - LM Studio was defaulting to 4096 Tokens where as the model can only handle 1024. Same goes for AnythingLLM , that defaults to 8192 tokens. set everything to 1024 and now its working

- Your "SOLVED" update is wrong. I ended up on this post after also having memory allocation issues with Qwen3 embedding models. 
  - The "1024" value you are quoting is the number of output dimensions of the model that clients would use to interpret results. You don't set that anywhere in LM Studio.
  - all you did by lowering the context length to 1024 tokens is reduce memory usage enough to fix your issue. You also made the output quality worse. Your clients will have to make more requests for more chunks for indexing since the model only accepts 1024 tokens at a time. This will in turn increase the number of vector entries that need to be stored.

- I had to "Override Domain Type" to Text Embedding to get it to work my computer (Models -> settings gear -> bottom setting). Not sure what else to try if you've already done that.
  - yep, did forget to mention that i tried both configurations

- try using any model you have as an embedder. It works just fine.

- ## [What Embedding Models Are You Using For RAG? : r/LocalLLaMA _202312](https://www.reddit.com/r/LocalLLaMA/comments/18j39qt/what_embedding_models_are_you_using_for_rag/)
- For RAG, I have been using multilingual minilm model from HF hub (I have multiligual requirement), and qdrant vector database. Happy with both. Specially, minilm embeddings are 368 dims, so some space saving there as well.

- Chinese embedding models and llms are now the top performers. Qwen-1.5B Yi-34B gte-large bge-large

- I chose the most lightweight stack possible— using all-MiniLM-L6-v2 for embeddings and HyperDB for local storage/retrieval (this is super fast for <100k documents)

- I am currently using all-MiniLM-L6-v2 but responses are generally not that good my data size is almost 600mb and it is giving me not that good results, what kind of embedding should i choose considering the size of data and database of pgvector postgres

- What Embedding model is best for Text-To-SQL for Financial data? Currently I'm using OpenAIEmbeddings
  - Text-to-SQL is a sequence to sequence task. My very first thought was "zero shot learning" because I have done this successfully in other domains. 

- I use whatever models are on top 1-5 on the MTEB leaderboard and run my custom evaluation 
# discuss-rag-tips/tricks
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [I rewrote hybrid search four times - here's what actually matters : r/Rag](https://www.reddit.com/r/Rag/comments/1pd7tao/i_rewrote_hybrid_search_four_times_heres_what/)
  - The actual problem Most resources tell you "combine vector search with keyword search" and show you a 0.5/0.5 weight split. That's it. But when you actually build it with real product data, you hit these issues: SKU codes like "MBP-M3MAX-32-1TB" return garbage from vector search; Score ranges don't match (vectors give you 0.3-0.4, BM25 gives you 15-50)
  - How I approached it
  - Each product has multiple fields - not just the description. This matters for multi-field indexing.
  - You can't just add vector scores (0.3-0.4 range) to BM25 scores (15-50 range). I implemented three normalization methods in the example
  - Query patterns should determine your weights. Instead of hardcoding 0.5/0.5, I built pattern detection
  - Multi-field indexing is critical. For product search you need to index multiple fields separately
  - When keyword search returns zero results (user searches "Microsoft laptop" but you only sell Apple/Dell), you need a fallback
  - https://github.com/pguso/rag-from-scratch /MIT/js

- ## [What’s your go-to combo of LLM + embedding model for RAG? : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pba2lt/whats_your_goto_combo_of_llm_embedding_model_for/)
- Qwen3 8B is the current SOTA for embeddings with a 32k context size, which gives you much more flexibility when chunking text.
  - Gemini 2.5 Flash has very good performance and is really cheap.
  - Once you factor in maintenance costs, potential GPU issues, downtime, etc., it’s almost always better to just use Google’s service — it saves you a ton of headaches and is always online.

- ## 💡 [I built RAG for a rocket research company: 125K docs (1970s-present), vision models for rocket diagrams. Lessons from the technical challenges : r/LLMDevs _202509](https://www.reddit.com/r/LLMDevs/comments/1nr59iw/i_built_rag_for_a_rocket_research_company_125k/)
  - 125K documents from typewritten 1970s reports to modern digital standards
  - 40% weren't properly digitized - scanned PDFs that had been photocopied, faxed, and re-scanned over decades
  - Going Vision-First with Local Models
  - Dual embedding strategy
  - Fine-Tuning for Domain Knowledge

- 
- 

- ## 🤔 [Companies need to stop applauding vanilla RAG : r/Rag](https://www.reddit.com/r/Rag/comments/1mj0tlh/companies_need_to_stop_applauding_vanilla_rag/)
  - I built a RAG system for internal documents pulled from a mix of formats, like PDFs and wikis. At first, the results were clean and useful.
  - But that was at the start. as the document set grew, the answers werent as reliable. Some of them werent using the most up to date policy section, or they were mixing information when it shouldnt be.
  - We had been using Jamba for generation. It worked well in most cases because it tended to preserve the phrasing from retrieved chunks, which made answers easier to trace. 
  - You have to keep your documentation up to date and/or have a more structured retrieval layer. If you want your setup to reason about the task, RAG is not enough. It’s retrieval, not orchestration, not a multi-layered workflow.

- vanilla RAG probably means your typical quick langchain setup (fixed chunk, embed, hybrid search). A step upwards would be something like hierarchical chunking and embedding, and then more advanced stuffs like Hyde, agentic, or even just rule based retrieval

- A more structured approach so that the LLM can understand the key entities of the business (companies, customers, projects, etc) and the key artifacts that make up your store of documents/knowledge (sales presentation, quotes, meeting notes, etc). And then the ability to connect the dots between those items… eg this sales deck mentions this company, which matches to this record in our CRM.
  - The main difference with all these new tools we have is that you don’t have to do all that definition as part of some crazy data orchestration flow… but rather can do a lot of it at retrieval time.

- Semantic chunking is basically a way of using document context like headings as part of the chunking process and than retaining a contextual map across all chunks in json format to help have more context when you. Retrieve chunks in searches.

- I agree completely. The core issue with RAG is that it's a passive system, it can only retrieve what's already there. I saw this exact problem at my last job, and now I'm building an MVP to solve it.
  - My approach is to make a better RAG system that not only retrieves information but also identifies knowledge gaps and initiates a question workflows for employees to verify and answer, creating a truly dynamic and complete knowledge base.
- Bottleneck is the rag that's limiting the amount of queries, it'll probably be fixed if we went towards higher tier but that cost isn't justified yet.

- This is a realistic issue in practice. There can be various ways to make the system smarter. One is to use an agentic design and give agents hints to decide whether newer contents should be retrieved (some people may prefer this way to leverage "the I in AI" more). On the other hand, you may also design your database tables and refine the query, for example by adding a timestamp with each vector when it's injected, then during query, sort the top K results by timestamp, or even make a cut off by the timestamp.

- rag needs reranking folks
  - yes reranking folks is a brilliant way to phrase it, other people need to feed it in!

- ## 🔢 [How to dynamically prioritize numeric or structured fields in vector search? : r/LangChain _202510](https://www.reddit.com/r/LangChain/comments/1oclpn4/how_to_dynamically_prioritize_numeric_or/)
- This will not happen automatically. Either you have to rewrite the query or do a query classification and let this be handled by a database query.
  - You may be able to store the numerics as metadata and use the metadata to rerank, but to do even that, you need to classify the query first.
  - You can have a set of ranking attributes as metadata, and classify the query using a pretrained classification model, to find which ranking attributes to use and implement the reranking on those metada attributes.

- Yeah, this is a common puzzle when you move beyond basic semantic search. Post-processing reranking is probably your cleanest bet.
- The general idea is to do a two-step retrieval:
  - Use the vector search to get a broad set of semantically relevant candidates (e.g., the top 20-50 documents).
  - Then, in your application layer, iterate over just those candidates. You can parse the query to see if it mentions "top" or "most, " then extract the relevant numeric field (ranking, publications, etc.) from the metadata of those candidates and re-score them.
- This way you're not trying to cram structured logic into the embedding space. 
  - LlamaIndex has postprocessors for exactly this kind of thing, you can even write a custom one. It's way more flexible than trying to make the vector DB do everything.

- milvus supports hybrid search (vector + bm25) with reranking strategies. you can filter metadata pre-search using comparison operators on numeric fields, or build a custom llamaindex postprocessor that combines vector similarity with dynamic metadata scoring. retrieve top-k, then rescore as: new_score = similarity_weight * vector_score + metadata_weight * normalize(field). this avoids hardcoding thresholds. alternatively use llmrerank to let the llm judge relevance based on metadata context, but slower/costlier.

- ## [RAG over Database : r/LangChain _202407](https://www.reddit.com/r/LangChain/comments/1efnx5u/rag_over_database/)
  - I have been trying to build a RAG over a database that has mulitple tables. Often times, for a user query, the data has to be searched by joining multiple tables. I followed this approach as mentioned in Langchain documents.
  - What I am observing is that many times the query generated by LLM is not correct and the data that user wants is incorrect. 

- Try to make all the joins yourself in the form of view and provide a simple view for the LLM

- dont use joins. use views or make stored procs to call for summaries etc you want.

- I would use the traditional RAG-based approach more in cases when the knowledge base is made of documents instead of structured data.
# discuss-code-rag
- ## 

- ## 

- ## 

- ## [What’s the best way to chunk large Java codebases for a vector store in a RAG system? : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pgliqi/whats_the_best_way_to_chunk_large_java_codebases/)
- AST-based chunking is definitely the way to go for Java codebases. Simple token or line-based splits will break methods and classes in weird places, making it harder for the model to understand context and relationships between code elements. Tree-sitter is solid for this, and there are some decent parsers out there, but honestly the tooling ecosystem for experimenting with different chunking strategies is pretty fragmented.

- That’s not going to be particularly useful. Look at Claude code, Gemini cli, codex etc. none of them create embedding from your code

- tree-sitter is great. https://cocoindex.io/docs/examples/code_index this project does codebase indexing and supporting java & large codebase, and is open sourced.

- ## [[D] What I learned building code RAG without embeddings : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pfxl6x/d_what_i_learned_building_code_rag_without/)
  - I've been building a system to give LLMs relevant code context from any repo. The idea seemed simple: let an LLM look at the file tree + function signatures and pick which files to include. No embeddings, no vector DB.
- File paths aren’t enough. I added AST-extracted symbols
  - Retrieval quality jumped noticeably (NDCG went from ~0.85 to ~0.92). The model doesn’t need to read the full file to know “this smells like auth.”
- Generic eval criteria reward BS
  - Anchoring eval on specific symbols/files made it much easier to spot hand-wavy nonsense.
- So the “LLM looks at the tree + symbols and picks files” setup landed roughly on par with embeddings on answer quality, without the indexing infrastructure. Good enough for me to keep using it.

- ## [How vscode team is making copilot smarter with “less” tools : r/vscode _202511](https://www.reddit.com/r/vscode/comments/1p4ucl5/how_vscode_team_is_making_copilot_smarter_with/)
  - how RAG came back into fashion after being declared “dead, ” and how that revival gives new life to another technology people are prematurely burying — tool calling, or by its full name: MCP.
  - All the tools that make an agent actually agentic - searching, editing, creating files, and more - are built directly into agents and exposed through classic tool calling. It’s very similar to MCP, and it brings the same problem with it: every tool consumes context in every single request.
  - So what did the Visual Studio Code team do?
  - They combined two approaches:
  - Adaptive Tool Clustering - They use embeddings to compute a vector for each tool, then cluster similar tools based on cosine similarity. This creates “virtual groups” of tools that belong together.
  - Embedding-Guided Tool Routing - When the user asks something, the embedding of the query is compared to the group vectors, routing the agent straight to the relevant group without scanning all of them. Less trial-and-error, less wasted context.
  - What does that give us? A real reduction: from 40 tools the agent could call - down to 13 smart clusters.
  - And what’s next? They’re aiming for long-term memory - the ability to remember which clusters and tools worked for similar tasks, prioritize them, and understand how to use each tool optimally.
  - And what about MCP? If this mechanism is expanded into the MCP client layer (not just the built-in Copilot tools), it could also solve the well-known context overload issue in MCP.
  - The interesting question: will this become part of the official spec, or remain in userland where each client implements it differently?
  - In the meantime, sub-agents with clearly defined tool scopes are a solid workaround - which, honestly, is exactly what we’d want the agent to learn to do by itself.

- The first thing I do is to disable all this crap from VS.

- ## 🆚 [Does grep perform better than vector DB + embeddings in large code bases? : r/ClaudeCode _202511](https://www.reddit.com/r/ClaudeCode/comments/1osyrpu/does_grep_perform_better_than_vector_db/)
  - Unlike Cursor or Github Copilot, I see that Claude Code seems to leave it up to the user to either do the indexing or not. Is there a reason? Does it perform better?
- Short answer: grep ≠ BM25 ≠ vectors. They each win on different axes.
  - grep/ripgrep — exact string/regex scan over files. Zero indexing, blazing on rare tokens and precise patterns (“def foo(|GUIDs|error codes”). Great for “I know the string.”
  - BM25 (inverted index) — lexical retrieval with ranking. It tokenizes code/text and returns files that share the same terms, weighted by `tf-idf` . Faster than grep on huge repos (no full scan) and returns a ranked list, but it’s still keyword-based (no synonym/semantics unless you add query expansion). Think Zoekt/Sourcegraph style code search.
  - Embeddings (vector DB) — semantic retrieval. Finds conceptually similar code/comments (e.g., “exponential backoff retry” locating retry_with_jitter() in another lang with no “backoff” keyword). Costs an index build + memory, but best when you don’t know exact strings.
- Trade-offs:
  - Speed: grep (no index) < BM25 (indexed) < vectors (indexed + compute)
  - Recall: grep (exact) < BM25 (lexical fuzzy) < vectors (semantic)
  - Precision out-of-the-box: grep high for exact needles; BM25 good for term overlap; vectors need a reranker to avoid drift.
- Best practice in large codebases:
  - Hybrid: BM25 (or Zoekt) for lexical + a small vector index for semantics.
  - Fuse results (Reciprocal Rank Fusion or LLM rerank) so you get both “known string” hits and conceptual matches.
  - Keep grep/ripgrep handy for one-off precise hunts; use the indexes when scale/recall matter.
- So “does grep perform better?” 
  - For exact, known strings on your machine, often yes. 
  - For concept queries across languages/renames, vectors win. 
  - For day-to-day, hybrid > either alone. Edit: reworded

- People @Cursor have written a bunch about their belief that strong semantic embeddings are way better for coding tasks perf  [Improving agent with semantic search · Cursor _202511](https://cursor.com/blog/semsearch)
  - Closed benchmark, proprietary embeddings model... Even if it works  (the improvements aren't huge to begin with ) there is no way to reproduce their setup. 

- ## [Cline doesn't index your codebase. No RAG, no embeddings, no vector databases. : r/CLine _202505](https://www.reddit.com/r/CLine/comments/1kwhcz0/cline_doesnt_index_your_codebase_no_rag_no/)
- Does Roo Code also do that or is this just a Cline thing?
  - Roo recently added it for code search. It works with local models
  - They also added prompt caching for Gemini flash.

- Exceedingly large context windows don't just result in extreme costs but it also will slow down your every operation.
  - While prompt caching reduce costs it is not entirely free, nor does every model or provider support it. It's also like treating a symptom rather than the disease.

- RAG can be good. See how fast and precise is AUgment Code search
  - ive found Augment to miss obvious things at times

- cursor has code indexing

- RAG shines when you don’t know the exact function / class names in a repo. ripgrep file search that Cline uses for context search is awesome—if you already have the right keywords. That’s easy on your own project, but on a massive, unfamiliar codebase ripgrep can stall while RAG keeps rolling (although it can return the wrong chunks).

- Privacy issue first. Never is sending low quality windows off the code base to the LLM is bad for quality.

- ## 🤼 Cline doesn't index your codebase. No RAG, no embeddings, no vector databases. _202505
- https://x.com/cline/status/1927226680206131530
  - [Why Cline Doesn't Index Your Codebase (And Why That's a Good Thing) - Cline Blog _202505](https://cline.bot/blog/why-cline-doesnt-index-your-codebase-and-why-thats-a-good-thing)
  - This isn't a limitation -- it's a deliberate design choice. 
  - As context windows increase, this approach enhances Cline's ability to understand your code.
  - The industry default: chunk your codebase, create embeddings, store in vector databases, retrieve "relevant" pieces.
  - But code doesn't work in chunks. A function call in chunk 47, its definition in chunk 892, the context that explains why? Scattered everywhere.
  - We believe in the agentic power of the modesl, and with Claude's 200K+ context window, we don't need clever retrieval. We need intelligent exploration.
  - So Cline reads code the way you do -- following imports, tracing dependencies, building connected understanding.
  - 💡 Instead of indexing, Cline starts with structure. Using ASTs, it maps your codebase architecture -- classes, functions, relationships.
  - Then it explores. Need to add error handling? It traces from your function to your error utilities to similar patterns. Connected comprehension.
- The problems with RAG for code run deeper:
  - Chunking breaks the logical connections between functions and their dependencies
  - Indexes become stale the moment you push a commit
  - Your IP gets duplicated in vector embeddings (security nightmare)

- ## [Unpopular opinion: RAG is actively hurting your coding agents : r/ChatGPTCoding _202505](https://www.reddit.com/r/ChatGPTCoding/comments/1ktt4ab/unpopular_opinion_rag_is_actively_hurting_your/)
- I've been saying this since RAG first became the term used to describe the method. And you are exactly right, the whole reason it became a thing was because, back when context windows were 4k or 8k max, it was out of necessity. Now, in the age where context windows are 1M or 10M tokens, it only makes sense in specific enterprise cases where you have vast datasets to query for specific, isolated information.

- RAG isn’t just calling vector stores, it’s also prompt priming before generation using various sources. Dynamically priming the prompt with relevant information before the LLM generates a response. 
  - A lot of the large context models drop off in accuracy after 100k tokens, anyway.

- frontier models have large context windows, but they all equate to a token, which equals a cost
  - Knowledge Graphs + RAG. An syntax tree is constructed of the code , where each class, function , method etc become nodes in the graph. The LLM can then traverse the graph to get only what it needs.

- One thing Aider has that Roo and Cline don't, is what they call a "RepoMap" (and it ties aider to git). 
  - But the advantage of it is, given a class, it can easily determine all the related classes, so it doesn't have to go digging through folders, trying to figure out which file is actually relevant, it knows, because the RepoMap shows which classes use which classes.
  - I pulled the RepoMap class out of aider and eventually managed to remove all the aider dependencies and got running as a command-line app. I might try making an MCP with it and giving that to Cline and see if it can improve its ability to understand the app structure.
- I thought cline already had a tree sitter which did the same thing.
  - it does use tree-sitter, but not in the same way and not to the same effect. 
  - How Aider understands you program vs how Cline understands it is very apparent in working with them. Aider has a much better understanding of which bits of code are related to which other bits, whereas Cline is frequently guessing based on the filenames.
  - Using tree-sitter isn't enough. You need to actually map out the relationships and Cline doesn't seem to do this, at least not nearly as effectively as Aider does.
- using the LSP if available surley is the best approach?
  - No, beyond getting LSP diagnostic, which you can get somewhere else anyway. Using LSP server requires counting rows and columns, and LLMs are bad at it.
- but you don't have to use the interface literally
  - Then I'm not using LSP, I'm using something that uses LSP under the hood to point that is an implementation detail. Take a look at your favorite LSP server, tell me what is useful there to LLM agent besides diagnostics?
  - I can see how you give LLM diagnostics after it update the file is useful, but giving LLM access to LSP overall is IMO utterly useless.

- I was watching an interview video with Claude Code engineers and they mentioned along the lines of not using RAG or GraphRAG because they found that Claude Code performed better without it and just relying on tools, memory and agentic search.

- RAG still makes sense for latency sensitive use cases like real-time chat, although prompt caching helps with this. 

- ## [Lessons learned from implementing RAG for code generation : r/LLMDevs _202501](https://www.reddit.com/r/LLMDevs/comments/1hw1n5o/lessons_learned_from_implementing_rag_for_code/)
  - 📝 [A Recipe for a Better AI-based Code Generator | Pulumi Blog _202501](https://www.pulumi.com/blog/codegen-learnings/)
  - We wrote a blog post documenting how we do retrieval augmented generation (RAG) for code generation in our AI assistant, Pulumi Copilot. 
  - Measure and tune recall (how many relevant documents are retrieved out of all relevant documents) and precision (how many of the retrieved documents are relevant)
  - Implement end-to-end testing and monitoring across development and production
  - Create self-debugging capabilities to handle common issues like type checking errors

- when I need understanding a medium sized code base I have dumped the whole thing into gemini in Google AI workbench. It can do 2 million tokens, though it is SLOOW.

- I wonder if you've considered feeding more tokens from your retrieval result into your code gen step? Why 20k? Is that always enough? How would you even know if it weren't?
  - You've got part of the answer right there: SLOOW :-) Also expensive!
  - Seriously though, you want to optimize for both recall and precision. Too much irrelevant data (poor precision) can confuse the LLM leading to hallucinations.
  - 20k is based on "it feels right" and empirical data but honestly we have not done enough analysis to conclude that it is the perfect number for all scenarios - we will continue to measure and adjust.

- Did you experiment with other retrieval methods besides or in addition to semantic similarity? I've done some work using different techniques, like parsing dependency trees out of the current file, with promising results for code RAG.
  - We did look into BM25 for FT search but did not see measurable benefits for our use cases. Our approach relies on getting a lot of documents first and then pruning - it would be better to get just what's needed in the first place, I still hope BM25 can help there. Worth another look!
# discuss-rag-graph
- ## 

- ## 

- ## 

- ## 

- ## [Why do GraphRAGs perform worser than standard vector-based RAGs? : r/Rag](https://www.reddit.com/r/Rag/comments/1pi2q68/why_do_graphrags_perform_worser_than_standard/)
  - You'd expect GraphRAG to win, right? Graphs capture relationships. Relationships are context. More context should mean better answers.
  - that's not what they found. In several tests, GraphRAG actually degraded retrieval quality compared to plain old vector search.
  - Because I've also seen production systems where knowledge graphs and graph neural networks massively improve retrieval. We're talking significant gains in precision and recall, with measurably fewer hallucinations.

- In my experience, the issue isn't that graphs don't help - it's exactly what you said about the implementation approach. I've seen GraphRAG work incredibly well, but only when teams treat the graph construction as an ML problem that needs iteration and measurement.

- Vector RAGs are based on Similarity. Graph RAGs are based on relationships. As such at the best they can compete with relational databases only

- They model the statistical dependencies between data. Standard vector-based RAG assumes all day are independent and identically distributed (i.i.d.)
# discuss-rag-vector-db
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Built a deterministic RAG database - same query, same context, every time (Rust, local embeddings, $0 API cost) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1pisow5/built_a_deterministic_rag_database_same_query/)
  - Built AvocadoDB to fix it
  - Local embeddings via fastembed (6x faster than OpenAI)

- In what situations is the same query giving different retrieved results ? If you have the literal exact query, why not cache the LLM response too? That is the more time consuming part and does give meaningful different results even with a temperature of 0 through providers.
- Why Same Query Can Give Different Results in Traditional RAG
  - Traditional vector databases (Qdrant, Pinecone, Weaviate, etc.) return non-deterministic results because:
  - Approximate Nearest Neighbor (ANN): HNSW and similar algorithms trade exactness for speed. The search path through the graph can vary, especially with concurrent queries or after index updates. Floating point non-determinism: Different execution orders (parallelism, SIMD) can produce slightly different similarity scores, changing ranking.
  - Index mutations: Adding/removing documents changes the HNSW graph structure, affecting which neighbors are found even for unchanged documents.
  - Tie-breaking: When multiple chunks have identical/near-identical scores, the order is arbitrary.
  - Embedding API variability: Some embedding providers return slightly different vectors for the same text across calls.
- You're right that caching LLM responses is the logical next step - retrieval determinism is really just the foundation for response caching. Once you guarantee the same query produces the same context, you can cache the full response:
  - cache_key = hash(query + context_hash + model + temperature + system_prompt)
  - So the answer to "why not just cache LLM responses?" is: you can't safely cache responses if your retrieval is non-deterministic. You'd return cached answers that were generated from different context than what the current retrieval would produce.
  - Consider an AI coding assistant exploring a large codebase. Without deterministic retrieval:
    - User: "How does authentication work?"
    - First ask - LLM reads 15 files, 4000 tokens of context
    - Second ask (same question) - different retrieval, reads 12 different files
    - LLM has to re-process everything from scratch
  - With deterministic retrieval + caching: The LLM doesn't need to read entire files - it gets precise line-number citations (e.g., src/auth.rs:45-78) with just the relevant spans. 

- How does this tool maintain contextual or metadata relationships between chunks? Can it maintain distinction between multiple documents on a similar topic, and identify which source makes which claim?
  - Yes - this is core to how AvocadoDB works:
  - Span-level tracking: Every chunk (span) is tied to its source file with exact line numbers. When you compile context, each span includes [1] docs/auth.md Lines 1-23 so you know exactly where every claim comes from. Citation in output: The compiled context includes a citations array mapping each span to its artifact (file), start/end lines, and relevance score. Your LLM can reference these directly. Cross-document deduplication: Hybrid retrieval (semantic + lexical) combined with MMR diversification ensures you get diverse sources, not 5 chunks from the same file saying the same thing.
  - Metadata preservation: Each span stores the parent artifact ID, so you can always trace back which claim came from api-docs.md versus security-policy.md.
  - The deterministic sort ensures the same sources appear in the same order every time, so you can reliably say source 1 said X, source 2 said Y.

- Deterministic RAG is the right call; debugging and evals don’t work if the context shifts.
  - I’ve run similar stacks with Qdrant and Tantivy; DreamFactory helped expose a read-only REST layer so agents hit stable endpoints, not raw DBs.
  - Bottom line: end-to-end determinism plus explainable retrieval is the win.

- Would be cool to have optional Postgres backend

- ## [Best Vector Database for RAG : r/vectordatabase _202501](https://www.reddit.com/r/vectordatabase/comments/1hzovpy/best_vector_database_for_rag/)
- All vector databases work well for RAG. The selection of a vector database usually depends on your preference: cloud based vs self-hosted, open source vs private, programming languages / clients, API access, already part of SQL etc.
- Some common ones are (not in any order, I'm not affiliated with any):
  - Pinecone: private, cloud based, very popular
  - pgvector: Postres vector search extension, useful if you have already data in Postgres.
  - Faiss: A library for efficient similarity search and clustering of dense vectors.
  - Qdrant: Open source vector search engine written in Rust.
  - Chroma: Yet another vector database
  - Milvus: An open-source similarity search engine for embedding vectors.
  - Weaviate: Open source vector database written in Go.

- Pgvector because it is part of Postgres. In the end Vectors are just a data type in a databases. If you only need vectoring and not SQL then it is better to look search engine that does that I think.
  - PGVector, is like PostGIS for geospatial ops, an extension for Postgre to support vector search, it is not a true vector-native DB, so it adds operational overhead and lacks advanced features that a vector DB provides. 

- Quadrant, it's a vector DB designed specifically for RAG/AI workflows. It offers advanced filtering features (multi-tenancy) that are natively baked-in into its core architecture. These features would require more legwork using other data stores like Redis etc...
- FAISS: great for vector search is not really a DB, it's a lib and not a true DB

- ## 🆚 [Vector db comparison : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ph7njc/vector_db_comparison/)
  - Key findings:
  - RAG systems under ~10M vectors, standard HNSW is fine. Above that, you'll need to choose a different index.
  - Large dataset + cost-sensitive*:* Turbopuffer. Object storage makes it cheap at scale.
  - pgvector is good for small scale and local experiments. Specialized vector dbs perform better at scale.
  - Chroma - Lightweight, good for running in notebooks or small servers
  - [Best Vector Databases for RAG - Agentset](https://agentset.ai/blog/best-vector-db-for-rag)

- My decision tree looks like this: Use pgvector until I have a very specific reason not to.

- Missing from this is Vespa. But everything else is spot on. I think it goes into teh last column along with Qdrant, Milvus, Weaviate etc.
  - For me Vespa is on another level. It is a production ready and very capable of "regular search" (textual). SO you can do very good hybrid serachs. For me is even leaps ahead of ElasticSearch. We migrate a medium workload(5 nodes) from ES to Vespa 4 years ago and was the best decision we ever made.
- Agree with this assessment. But I think overall it's a lot more complex than others here too. It's a very steep hill to climb but once you do the power is there.

- Our rag team (afaik) uses elastic / weaviate because of hybrid search, we have lots of cases where search could be about some named entity (like people = name + surname), so hybrid is a must. IDK on which basis they chose which one to use for cases. Also, Qdrant has bm42 hybrid search, by any chance you know anything about how it performs compared to other solutions?
  - Hybrid search is incredible. But in my experience it's better to do parallel queries for semantic and keyword and then put all the results in a reranker

- Or just use SQLite and don't overcomplicate things
  - You need a vector search extension for it. And there aren't any particularly good ones that I know of.

- Definitely Elasticsearch if you need extreme levels of horizontal scalability.

- S3 vector is now a thing .
# discuss-chunking
- ## 

- ## 

- ## 

- ## 
# discuss-embedding
- ## 

- ## 

- ## 

- ## 

- ## [Show HN: We cut RAG latency ~2× by switching embedding model | Hacker News _202511](https://news.ycombinator.com/item?id=46043354)
- I always feel that the choice of embedding model is quite important, but it's seldom mentioned. Most tutorials about RAG just tell you to use a common model like OpenAI's text embedding, making it seem as though it's okay to use anything else. But even though I'm somewhat aware of this, I lack the knowledge and methods to determine which model is best suited for my scenario.

- The biggest latency improvement I saw was switching off OpenAI's API that would have a latency anywhere between 0.3 - 6 seconds(!) for the same two word search embedding...

- ## 🤔 [[Discussion] Anyone else doing “summary-only embeddings + full-text context” for RAG? : r/Rag _202511](https://www.reddit.com/r/Rag/comments/1p05u0f/discussion_anyone_else_doing_summaryonly/)
  - 1) For each doc/section: I generate a tiny synthetic text (title + LLM summary). → This is the ONLY thing I embed.
  - 2) At query time: I search over those short summaries.
  - 3) For answering: I take all retrieved sections and feed the full original text straight into the LLM. No reranking, no chunk scoring, nothing fancy.
  - Because chunking was slow, expensive, and honestly ruined the semantic boundaries of my data. Summary vectors are way cleaner, and long-context LLMs can handle the raw text way better.
  - Anyone else trying this “lightweight retriever + heavy context input” style?

- I wouldn’t blindly trust the summarizer though. The summaries are lossy by design but the good news is there’s models dedicated to this task.
  - Adding a sumeval model of some variety will give you much greater debugability and interpretability. It can help you surface where the summarizer is struggling or even better serve as the backbone for an RL loop.

- This is very similar to the contextual chunking anthropic proposed. Yes, this is standard now. Problem is still going to be latency and cost with the LLMs

- The idea works because one of the techniques used in chunking enrichment is adding keywords and summaries to the chunks. However, relying only on the summaries may work in some contexts but can still be less accurate, as you might lose information. Imagine 20-page sections where you have, for example, 5 chunks; in this case, they would be compressed into a single summary, which could not be enough.

- You are doing what industry needed but still their are room to improve the latency by implementing cache and have more meta data for the docs to get better context before going to LLM

- I've tried this- performed worse in my case. I would run an eval and decide for myself.

- I did follow the same approach to feed more context to MCP client hosted in IDEs through RAG. Vectorize the only metadata and source is returned as a result which contains the full document to feed to the LLM

- I didn't test it myself but I read about 'voyage-context-3' which seems to address the issue of global context without the need for an extra summarization step.

- This is almost the same as what the RAPTOR paper from last year suggested: https://arxiv.org/abs/2401.18059
  - Create summaries, cluster based on summary, then create a summary of those, etc. 
  - It’s a solid approach, especially since, when summarizing, you can ensure the LLM uses a consistent style.

- ## 🆚 [Embedding models have converged : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ozf9al/embedding_models_have_converged/)
  - I ran 13 models on 8 datasets and checked latency, accuracy, and an LLM-judged ELO score. Honestly, the results were not what I expected - most models ended up clustered pretty tightly.
  - rank 1 → 10 is around a 3% gap

- This is a case of saturated benchmarks not a case of the quality being the same
  - 100% this. It's like saying LLMs have converged because they all ace SuperGLUE.

- Why use LLM as a judge for this? You have a query and a matching document. You know which document you want for which query. What matters is the rank of that document for that particular query. I'm not sure I get what do the LLM's have to judge here.
  - Because a lot of the datasets in real life don’t have a single correct doc. And LLM judge evaluates the quality of the retrieved list, not just "did u hit the label".
  - We used 2 private datasets and 6 public datasets. Publc datasets that do have perfect ground truth also have ncdg and recall for accuracy. So we calculated both elo score and classical metrics.

- Did you try with different judge models and slightly different judge prompts, just to see if the judge influence on the results might be larger than the actual score differences?
  - great suggestion, will try that!

- Interesting - do we have a similar subset of benchmarks for rerankers?
  - yess! before embedding models, I also ran rerankers on multiple datasets and pretty much used the same elo scoring. check this out: https://agentset.ai/rerankers

- I've found embedding model benchmarks... Useless as of late? Qwen 3 models especially, they are killer on paper, but I found them near useless after a top_k of 5 in my semantic search engine use case. The first couple of results are great, but seemed almost random after about 5 results, which is a no-go for our search pages returning ~40 items per page. We found "worse" models have much more consistent results, we went with e5-large-v2
  - yes, agree! using ELO actually helps with that, it basically checks how consistent a model(looks at the win rate) is across all datasets, not just the first few hits

- ## [what free model should i use for codebase indexing with speed indexing : r/RooCode](https://www.reddit.com/r/RooCode/comments/1oiw4w7/what_free_model_should_i_use_for_codebase/)
- Use text-embedding-004 model from google (fast and free)

- ## [Open-source embedding models: which one's the best? : r/Rag _202509](https://www.reddit.com/r/Rag/comments/1nro65j/opensource_embedding_models_which_ones_the_best/)
- tried embeddinggemma:300m and qwen3-embedding-0.6b and 4b

- [Open-source embedding models: which one's the best? : r/ollama](https://www.reddit.com/r/ollama/comments/1nro30i/opensource_embedding_models_which_ones_the_best/)
- I find the latest Qwen embeddings and reranker models the best out there today even when comparing with offerings from OpenAI and VoyageAI
  - I tried BGE, Nomic, and Qwen using ChunkHound I don't care so much about the raw numbers but about the end to end result. You can easily see the difference in results by running the chunkhound search command

- [Open-source embedding models: which one to use? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nrgklt/opensource_embedding_models_which_one_to_use/)
- I've had my best results with bge-m3 or qwen3-embedding

- ## [Is there a classification of worst vs best ai models for RAG : r/Rag _202509](https://www.reddit.com/r/Rag/comments/1nk2rza/is_there_a_classification_of_worst_vs_best_ai/)
- For small models, most of our users have converged around: Gemma3, Qwen3, and DeepSeek
  - I always use for demos Mistral Medium 3.1 (mistral-medium-2508), which is a very good middle ground.
  - For the "large" LLMs, Gemini Flash variants and Claude Sonnet or Haiku. OpenAI models have *never* been good at this use case. The GPT-OSS models have been abysmally bad in testing.

- For an embeddings model, we've been using all-MiniLM-L6-v2 since we released TrustGraph, and haven't really seen any need to change. The platform allows you to choose any embeddings model from HF, but all-MiniLM-L6-v2 seems to do just fine in most use cases. If you want be able to try out all these model combinations, you can give them a try with TrustGraph (open source).

- gemma3 worked best in my case(turkish docs)
  - but rag mostly depends on understanding and memorization abilities

- I have tried several OpenAI models for our RAG system, and got great results using gpt-4.1-mini.
  - Via the API, it is the OpenAI model that has the largest context window right now.

- ## [embeddinggemma has higher memory footprint than qwen3:0.6b? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nbbi1c/embeddinggemma_has_higher_memory_footprint_than/)
- For whatever reason, Gemma models have a larger vocab size of 256K whereas most models have a vocab size of around 120k. This adds to the size

- confirmed, i use ollama just for embedding, download it from official ollama library. The size is 621MB on command ollama list. But getting bigger like 2.8GB on ollama ps
  - and it very slow compared to qwen embedding 4b.

- ## [Real life experience with Qwen3 embeddings? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nezmfi/real_life_experience_with_qwen3_embeddings/)
  - I need to decide on an embedding model for our new vector store and I’m torn between Qwen3 0.6b and OpenAI v3 small.
  - The qwen3 embeddings top the MTEB leaderboards scoring even higher than the new Gemini embeddings. Qwen3 has been killing it, but embeddings can be a fragile thing.

- I don't think Qwen3-Embedding-0.6B performs better than previous encoder models of similar size (e.g., bge-m3); 
  - its main advantage is long-context support. 
  - Overall, it's only a little bit better than other prior state-of-the-art LLM-based embedding models (e.g., Kalm-v2), with advantages mainly comes from instruction tuning on the query side, which improves adaptability.
- Qwen3-Embedding-4B is good. It outperforms bge by 2–3 points (on my own dataset, using NDCG@10), and maintains strong retrieval performance at 2–4k tokens per chunk. 
  - However, the GGUF version of this model seems inconsistent with the original checkpoint—this discrepancy is unclear (I suspect it may be related to the pooling configuration).
- Qwen3-Embedding-8B might indeed be a SOTA model, but it costs too much.

- I never tested that quant. There are so many mistakes you can make with embeddings (omitting required eot tokens, missing instructions, wrong padding alignment etc.) 

- I always include something like an embedding version so it is always possible to change embedding algo without reencoding old data so long as you are willing to do a search per algo and re-rank them.

- I've used 8B and 4B as GGUF at Q4_K_M and never had issues some are pointing.
  - Found the 4B most efficient as the difference between the 8B is small for such resource difference.
  - Been using for code bases, currently over 380 files with code. No issues.

- ## [Are Qwen3 Embedding GGUF faulty? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lt18hg/are_qwen3_embedding_gguf_faulty/)
  - Qwen3 Embedding has great retrieval results on MTEB.
  - However, I tried it in llama.cpp. The results were much worse than competitors.

- You have to add the EOS Token manually "<|endoftext|>" as of here: https://github.com/ggml-org/llama.cpp/issues/14234

- In multilingual, I was very disappointed with qwen3 embedding compared to jinaai/jina-embeddings-v3 which remains my favorite for the moment
- v4 is out btw: https://huggingface.co/jinaai/jina-embeddings-v4
  - It does work much better, getting 48.11% on the same benchmark.
  - The official JINA API is very slow though. Half a minute for a batch of 32.

- Would you believe I was just trying it out today and it was all messed up. Swapped from Q3 4B and 0.6B to granite 278m and all my problems went away.

- Yes, though if I tried generating the embeddings through the SentenceTransformers module instead, I got the state-of-the-art results I was hoping for on my benchmark. A code snippet for how to do so is listed on their HF page.
# discuss-rag-elements
- ## 

- ## 

- ## [How to Intelligently Chunk Document with Charts, Tables, Graphs etc? : r/LangChain _202510](https://www.reddit.com/r/LangChain/comments/1oe4wh4/how_to_intelligently_chunk_document_with_charts/)
- when i was working on extraction, i faced the same issue with tables. a simple parsing tool was not enough, so we added a prompt before processing the document by saying that whenever you encounter a table, first mark it by saying #Table Start# and end it with a #Table End# and take a screenshot of the whole table , feed it to the llm for ocr operation and get a parseable text based table. then during chunking, we made sure that a separate logic was being used for cases when we encounter the #Table Start# and #Table End# cause we would want to keep the whole table as one big chunk else it would lose context for the other half of the table since it would be starting with just some numbers and no context even with the overlaps. 
  - Other than this you can use MarkdownHeaderTextSplitter since it helps with the other part of documents aswell

- It is really simple. First split each pdf into multiple files, one page = one file.
  - Then, write a program that detects pages with tables, graphs etc and move them into a separate folder. When you move, assign a meaningful filename.
  - Then chunk all other pages. Only meaningful chunking is hierarchical.while chunking, build a graph or a tree view, and visualise this. This verifies that you have preserved the hierarchical integrity of the document.
  - Now, using an LLM, process each visual page to provide summary. Insert these chunks in the tree view at their correct location. The image page should be available as a link in metadata.
  - Now design a context template. It should have document id, current chunk, prev chunk, subtitle summary, title and book title.
  - Embed the chunk with this template into a vectordb. Then also embed a sparse vector.
  - While querying use both vectors and rerank them.

- For complex documents (with tables, charts, and images), RAGFlow works surprisingly well — it can intelligently recognize and preserve layouts like tables and embedded figures during parsing.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [RAG beginner - Help me understand the "Why" of RAG. : r/Rag _202510](https://www.reddit.com/r/Rag/comments/1phkzw6/rag_beginner_help_me_understand_the_why_of_rag/)
  - Is RAG even necessary for this usecase? Now LLM models have become so good that RAG is not required for tasks like this. (Evaluator asked me this question)

- For evaluation I would treat “with RAG” and “no RAG” as two systems. Build a small gold set of quiz questions and grading decisions from a human teacher, then
  - That gives you a concrete argument: RAG is not “philosophically nicer”, it either improves faithfulness and coverage on real data or it does not.

- Where RAG becomes valuable is when correctness and grounding matter—ensuring questions and answers come only from the uploaded content and not from the model’s prior knowledge or hallucinations. That distinction is especially important in educational assessment.

- ## [Why RAG Fails on Tables, Graphs, and Structured Data : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pfuxis/why_rag_fails_on_tables_graphs_and_structured_data/)
  - Most RAG pipelines are built for unstructured text, not for structured data.
  - Tables don’t fit semantic embeddings well
  - Graph-shaped knowledge gets crushed into linear chunks
  - SQL-shaped questions don’t want vectors
- The real fix is multi-engine retrieval, not “better vectors”
  - Vectors for semantic meaning and fuzzy matches
  - Sparse / keyword search for exact terms, IDs, codes, SKUs, citations
  - SQL for structured fields, filters, and aggregations
  - Graph queries for multi-hop and relationship-heavy questions
  - Layout- or table-aware parsers for preserving structure in complex docs

- Setting the questionable AI slop style aside, while the diagnosis is correct, the proposed solution is pretty generic and simplistic. Sure, tables belong into a relational DB. So, hybrid search. But if your docs have no unified table structure, well, that’s a problem this post fails to address. And that’s a very common situation.

- At iGPT, we handle this by treating different data types as first-class citizens from ingestion onward. Emails get thread reconstruction and role detection, tables get parsed with column-header preservation, and attachments trigger format-specific pipelines before anything hits the vector layer.
  - The retrieval stack uses hybrid search (semantic + keyword + metadata filters) with post-retrieval rescoring, so structured queries don't get drowned out by "relevant-ish" prose.

- ## [My Experience with Table Extraction and Data Extraction Tools for complex documents. : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pfwfvy/my_experience_with_table_extraction_and_data/)
- Tables:
  - For documents with simple tables I mostly use Camelot. Other options are pdfplumber, pymupdf (AGPL license), tabula.
  - For scanned documents or images I try using paddleocr or easyocr but recreating the table structure is often not simple. For straightforward tables it works but not for complex tables.
  - Then when the above mentioned option does not work I use APIs like ParseExtract, MistralOCR.
  - When Conversion of Tables to CSV/Excel is required I use ParseExtract and when I only need Parsing/OCR then I use either ParseExtract or MistralOCR. ExtractTable is also a good option for csv/excel conversion. 
  - Apart from the above two options, other options are either costly for similar accuracy or subscription based.
  - Google Document AI is also a good pay-as-you-go option but I first use ParseExtract then MistralOCR for table OCR requirement & ParseExtract then ExtractTable for CSV/Excel conversion.
  - I have used open source options like Docling, DeepSeek-OCR, dotsOCR, NanonetsOCR, MinerU, PaddleOCR-VL etc. for clients that are willing to invest in GPU for privacy reasons. I will later share a separate post to compare them for table extraction.
- Data Extraction:
  - I have worked for use cases like data extraction from invoice, financial documents, images and general data extraction as this is one area where AI tools have been very useful.
  - If document structure is fixed then I try using regex or string manipulations, getting text from OCR tools like paddleocr, easyocr, pymupdf, pdfplumber. But most documents are complex and come with varying structure.
  - First I try using various LLMs directly for data extraction then use ParseExtract APIs due to its good accuracy and pricing. Another good option is LlamaExtract but it becomes costly for higher volume.
  - ParseExtract do not provide direct solutions for multi page data extraction for which they provide custom solutions. I have connected with ParseExtract for such a multipage solution and they provided such a solution for good pay-as-you-go pricing. Llamaextract has multi page support but if you can wait for a few days then ParseExtract works with better pricing.

- https://github.com/camelot-dev/camelot /MIT/python
  - A Python library to extract tabular data from PDFs

- I haven’t found a single thing, other than custom vision based LLM workflows, that is good at extracting tables with complex structures (spanning multiple pages, merger cells, hierarchical rows/column headings, etc…). But that is slow and expensive.

- ## [Struggling with finding good RAG LLM : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jwtn6j/struggling_with_finding_good_rag_llm/)
- Would strongly recommend reading up on the basic RAG process and the systems around it. The LLM itself typically isn't involved in the data lookup/search unless it's been extended to work as an agent. The quality of the sources will heavily influence the answer quality : garbage in/ garbage out sort of deal. Beyond that, check out mistral small 3.1, a bunch of the qwen models, and command-r series.
- Your RAG has to return good results. So you should be querying the rag with the embedding model directly and looking at the top 10 results. Are they what you expected? If not, you need to change your embedding model, change the way you format/chunk the input data, increase metadata, etc.
  - The info from the RAG results will be fed into the LLM for inference.

- I think this is more to do with how RAG is implemented rather than the model itself, but of course you want to use a reliable model.

- You need two models: one for embeddings and another for chat. For embeddings Llama-3.2-1B will be a good choice: reasonable fast and capable to understand anything in any language. And you will not use it to speak or think at all.
  - Next use any strong model to chat and to ask questions to rag.

- ## [Successful RAGFlow in Prod : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pawrzj/successful_ragflow_in_prod/)
- TL; DR: RAGFlow is powerful for complex documents but resource-hungry.
  - Stress Testing: It is heavier than "vanilla" RAG because of the deep document understanding (OCR/Layout analysis). Expect higher ingestion latency. For query latency, it depends entirely on your backing vector database (e.g., Elasticsearch/Infinity). You must scale your parsing workers separately from your query services.
  - Maintenance: The visual graph builder makes logic errors easy to spot, but debugging specific parsing failures (e.g., a specific weird PDF format) requires digging into container logs.
  - Performance: Retrieval precision is significantly better than standard recursive chunking because it respects document structure (tables, headers, sections).
  - The Killer Feature: Table Parsing/Layout Analysis. It handles complex tables in PDFs where other frameworks (like standard LangChain) produce garbage.
  - Must-Know Tip: Don't rely on vector search alone. Configure Hybrid Search (Keyword + Vector) and Re-ranking from day one. It dramatically improves accuracy for technical jargon and specific IDs. 

- ## [How to make a RAG pipeline near real-time : r/LangChain](https://www.reddit.com/r/LangChain/comments/1p623zt/how_to_make_a_rag_pipeline_near_realtime/)
- There are specific models that exceeds at this. I know AWS’s Nova Sonic can do this well. Although for RAG 3-4 seconds ain’t bad especially for a voice bot.

- RAG latency is usually a combination of retrieval tuning and orchestration choices, so try reducing candidate counts, sharding vectors for faster nearest neighbor lookups, precomputing and caching top-k results for common queries, and parallelizing embedding and retrieval steps so STT and retrieval overlap.
  - Also check chunk sizes and embedding model choice because those affect recall and speed, and consider a lightweight semantic cache to answer repeated context queries instantly.
  - People mix FAISS tuning or an alternative vector store with a caching layer and async streaming to get sub-second responses, and teams that need observability and easy orchestration prototype these flows in visual builders or frameworks like LlmFlowDesigner, while others tune Milvus or FAISS directly.

- ## 🤔 [Which model is good for making a highly efficient RAG? : r/LocalLLM _202506](https://www.reddit.com/r/LocalLLM/comments/1l0pncp/which_model_is_good_for_making_a_highly_efficient/)
- Founder of agentset here. I'd say the quality of the embedding model + vector db caries a lot more weight than the generation model. We generally found any non trivially small model to be able to answer questions as long as the context is short and concise.
- What embeddings approach would you recommend?
  - Most of the working is in the parsing and chunking strategy. Embedding just comes down to choosing a model. If you're doing multi-lingual or technical work, you should go with a big embedding model like text-large-3. If you're doing english only there are plenty of cheaper and lighter weight models.

- Qwen3 14B and Qwen3 32B (crazy good, they fetch, think then provide a comprehensive answer) and those boys are not afraid of follow up questions either.. ask away!
  - 32B uses citations functions following every statement he says. 14B does not for some reason.. but that does not mean it's bad or anything. Still a very decent RAG AI.

- I found Qwen 3 and Gemma 3 work the best.

- I use Linq-Embed-Mistral because it's high on MTEB. But I haven't compared it with other models.

- [What's the best model for RAG with docs? : r/ollama _202506](https://www.reddit.com/r/ollama/comments/1l9wvnr/whats_the_best_model_for_rag_with_docs/)
- I've had good success with simple models such as Qwen3 4B using Open WebUI and Ollama. There are probably better RAG backends though (planning to try LightRag).
  - Basically you need a good embedding engine (try bge-m3, which is actually available through Ollama if that is your poison).
  - Then you also need a good content extraction engine, to suck out the right information out of your specific type of document. Try Tika, which is working great.
  - Then you'll need a good re-ranking model to do some magic on the proposal the RAG comes up with. Try BAAI/bge-reranker-v2-m3.
  - Those are the main things you need.
  - Then there are some settings of course that you can toy around with (temperature, top k, min probability, for example), but with those main components you'll be able to ask detailed questions.
  - Then .. depending on your knowledge base, you should structure the data (documents, contents) in a smart way. But if you just want to ask questions on a pdf-specification or such then you'll fine with the above components.
  - That works for me at least, feeding lots of specifications, requirements, manuals etc. into my system.
  - Try it out in Open-Webui (frontend and backend solution). It works, but you'll probably want a separate backend solution going forward (with GPU re-ranking support for instance, since it's slow).

- Try out granite3.3:8b - its designed specifically for enterprise tool use & rag. Really slept on & everyone else defaults to the text gen llms, but youll be pleasantly surprised especially since its so efficient your video card would be overkill.

- ## 💥 [Best RAG Architecture & Stack for 10M+ Text Files? (Semantic Search Assistant) : r/LangChain _202511](https://www.reddit.com/r/LangChain/comments/1p2klni/best_rag_architecture_stack_for_10m_text_files/)
  - I am building an AI assistant for a dataset of 10 million text documents (PostgreSQL). The goal is to enable deep semantic search and chat capabilities over this data.
  - Scale: The system must handle 10M files efficiently (likely resulting in 100M+ vectors).
  - Updates: I need to easily add/remove documents monthly without re-indexing the whole database.

- Most RAG pipelines suck at two main points processing unstructured data while splitting and context aware retrieval

- [Best RAG Architecture & Stack for 10M+ Text Files? (Semantic Search Assistant) : r/Rag](https://www.reddit.com/r/Rag/comments/1p2kkua/best_rag_architecture_stack_for_10m_text_files/)
- To get any decent results, you need to build a distributed RAG, if there is such a thing.
  First create a taxonomy of the assets. This is like Table contents for the entire collection. You can keep this in a graph db.
  Then build a classifier with positive and negative targets. Use this to classify the query first to determine which groups/clusters of the documents are the best to use. Once you know the target collections you can focus only on those.
  You can perhaps supply the classifier as an MCP service to the LLM.
  For each asset, create a chunking model. Keep in mind, not all documents would fit the same model. Store chunks in a vectordb.
  Along with chunks, extract entities. Build a BM25S database (relational) with these keywords.
  Then extract entities and relationships from the documents and build a ER knowledge graph for each of the documents.
  All databases should have the same metadata to enable reranking or hybridization.
  How to manage the CDC on the document mountain is another post.

- If you are generating vectors, you can track signatures of your text chunks and reuse vectors if the text chunk didn't change. That saves you cost of new vectors when you reindex.

- ## [Stop fine-tuning your model for every little thing. You're probably wasting your time. : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ov7ogq/stop_finetuning_your_model_for_every_little_thing/)
  - confession time. I just wasted three weeks and a chunk of my compute budget trying to fine-tune a model to answer questions about our internal API. The results were... mediocre(平庸的；普通的；不够好的) at best. It kinda knew the stuff, but it also started hallucinating in new and creative ways, and forgot how to do basic things it was good at before.
  - I feel like "fine-tuning" has become this default magic wand people wave when an LLM isn't perfect. But 80% of the time, what you actually need is RAG
  - RAG is like giving your AI a cheat sheet. You've got a mountain of internal docs, PDFs, or knowledge that the model wasn't trained on? Don't shove it down the model's throat and hope it digests it. Just keep it in a database (a "vector store, " if we're being fancy) and teach the AI to look things up before it answers. 
  - It's faster, cheaper, and the AI can't "forget" or misremember the source material. Fine-tuning is for changing the AI's personality or teaching it a new skill. This is when you need the model to fundamentally write or reason differently. 
  - So, the dumb-simple rule I go by now: · Problem:- "The AI doesn't know about X." -> Use RAG. "The AI doesn't act or sound the way I want." -> Consider Fine-Tuning.

- RAG is for knowledge
  - Finetuning is best for style
  - Don't mix up the two

- I thought you can't SFT modern reasoning LLMs anymore? all this does is fuck up their complex post train since GRPO/RLHF happens after SFT and you can't replicate that with a simple pipe.
  - I think it depends on the model? Like, Qwen3 models are pretty good for SFT training.

- ## [After Building Multiple Production RAGs, I Realized — No One Really Wants "Just a RAG" : r/Rag _202511](https://www.reddit.com/r/Rag/comments/1oly866/after_building_multiple_production_rags_i/)
- I get asked to RAGify :) company documents, but just RAG isn't enough. It needs to be able to analyze code without a single click, able to produce similar documents similar to provided document, able to chat with documents, and needs to completely run offline, no data outside. More requirements keep coming as the week go on.

- thanks mr chatgpt

- ## 🆚 [I tested local models on 100+ real RAG tasks. Here are the best 1B model picks : r/Rag _202510](https://www.reddit.com/r/Rag/comments/1o60ib6/i_tested_local_models_on_100_real_rag_tasks_here/)
- Best model by real-life file QA tasks (Tested on 16GB Macbook Air M2)
  - I’m building this local file agent for RAG - Hyperlink. The idea of this test is to really understand how models perform in privacy-concerned real-life tasks
- tests result
  - A — Find facts + cite sources → Qwen3–1.7B-MLX-8bit
  - B — Compare evidence across files → LMF2–1.2B-MLX
  - C — Build timelines → LMF2–1.2B-MLX
  - D — Summarize documents → Qwen3–1.7B-MLX-8bit & LMF2–1.2B-MLX
  - E — Organize themed collections → stronger models needed
- Tasks Types (High Frequency, Low NPS file RAG scenarios)
  - Find facts + cite sources — 10 PDFs consisting of project management documents
  - Compare evidence across documents — 12 PDFs of contract and pricing review documents
  - Build timelines — 13 deposition transcripts in PDF format
  - Summarize documents — 13 deposition transcripts in PDF format.
  - Organize themed collections — 1158 MD files of an Obsidian note-taking user.

- ## [The “new RAG every week” problem — do we really need to switch frameworks this often? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o764lj/the_new_rag_every_week_problem_do_we_really_need/)
  - It feels like every couple of weeks, there’s a brand-new “next-generation” RAG framework popping up — R2R, LightRAG, RAGFlow, and now a few others that just launched on GitHub.
  - But when you look closer, most of them aren’t new paradigms at all.
  - They’re slight variations of existing pipelines — same retrieval backbone, same chunking strategies — maybe with a bit of optimization in one step (say, hybrid retriever logic, graph-based context linking, or compression on long contexts).

- AI is a rapidly growing tech space. There will be 10 technologies that mildly differ each other and then there will be that 1 that will make some kind of a breakthrough. That's how it is. It's far too early for any real standards yet, and honestly that's the exciting part of following the AI space.

- ## 🆚 [Tested 9 RAG query transformation techniques – HydE is absurdly underrated : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o6s89n/tested_9_rag_query_transformation_techniques_hyde/)
  - Your RAG system isn't bad. Your queries are.
- I just tested 9 query transformation techniques. Here's what actually moved the needle
- Top 3:
  - HydE – Generate a hypothetical answer, search for docs similar to that. Sounds dumb, works incredibly well. Solves the semantic gap problem.
  - RAG-Fusion – Multi-query + reranking. Simple, effective, production-ready.
  - Step-Back – Ask abstract questions first. "What is photosynthesis?" before "How do C4 plants fix carbon?"
- Meh tier:
  - Multi-Query: Good baseline, nothing special
  - Decomposition: Works but adds complexity
  - Recursive: Slow, minimal quality gain for simple queries
- Key insight: You're spending time optimizing embeddings when your query formulation is the actual bottleneck.

- Many larger RAG platforms I've worked on or seen in use are making embeddings from the text to be retrieved and also generating a couple of questions that can be answered by the same chunk, saving those embeddings as well (so you have several embeddings pointing at the same chunk).
  - This performs a lot like HydE, but shifting the extra compute (generation step) to the ingestion stages instead of query time for better latency/performance in exchange for a larger index to store and query, which is usually the desired tradeoff for interactive systems.

- ## 🤔 [Is RAG system actually slow because of tool calling protocol? : r/Rag _202509](https://www.reddit.com/r/Rag/comments/1ntc1ky/is_rag_system_actually_slow_because_of_tool/)
  - Just came across few wild comparison between MCP and UTCP protocols and honestly... my mind is blown.
  - For RAG systems where every millisecond counts when we are retrieving documents. UTCP is 30-40% faster performance than MCP. that's HUGE.

- Why would you use mcp in RAG to begin with?
  - The consumer of a RAG might use tools, but ‘the’ RAG components do not need tools.

- Find it funny everyone so focused on speed, but go ask gpt and wait 15min is fine

- ## 🆚 [Does anyone know how much of a performance difference between knowledge graphs and vector based searches? : r/LangChain _202408](https://www.reddit.com/r/LangChain/comments/1eragqk/does_anyone_know_how_much_of_a_performance/)
  - I made a pretty simple vector based RAG search, and it performs "okay" and doesn't always generate the expected results. I have the pieces for a knowledge graph, but I was wondering if people knew the expected improvements that I should expect to see by moving to knowledge graphs?

- Vector search alone is usually faster. Without any bells and whistles like metadata filtering or stepback, it's just an optimized KNN. 
  - Graph based RAG involves traversing a graph in addition to searching for the appropriate starting node, which often times is a done via vector search. 
  - The graph structure usually leads to good results though.

- ## LobeChat v1.85.0 优化了对话上传文件的逻辑，把大家呼声比较高的全文上传的能力做好了，不再走 分块 + embedding 的朴素 RAG 。带来的好处是速度变快了，效果也更加理想了。
- https://x.com/arvin17x/status/1921101310004179082
  - 感觉大模型再迭代个一年，朴素 RAG 可能就要退出历史舞台了
  - 比如一个文件 10w 字的内容，全文上传就是10w字全放上下文里。 RAG 是找出最相关的 N 个内容片段（假设一个片段1k，加起来 N k个字）放上下文里。 全文上传的效果在大多数情况下一定是比 RAG 要好的。
  - 现在默认上传就是全文。不过知识库读取还是原来的
- 不用 RAG，直接传给 LLM，钱包顶不住啊
- 全文上传，只有Google家才有很大的上下文吧？其他家效果就不好了
  - 不啊，现在gpt4.1mini都有1M上下文了，也便宜。测下来效果非常好

- ## 开源的 llm 系统里，带知识库功能的，目前还没找到一个做的好的。
- https://x.com/wwwgoubuli/status/1830227047173751206
  - 不过这么说倒也不是要贬低什么，我自己帮客户定制过的知识库中，做的稍微好一点的，也投入了大量的精力和成本来实现数据预处理，单单一个文本分段都找不到通用范式，得大量定制。

- 问题就是 to b 里。 to c 那一个用户丢个 pdf 算不上什么知识库。 到了 to b  领域，你看着一堆 excel ，pdf， 你的梦魇才刚开始

- 我们自己做售后客服机器人，起步是找实习生撸了1万条问答对，上线后每周根据bad case迭代继续做数据。这玩意效果就是看标注数据，想要好的效果，就好好做数据。

- 知识库如果像编程语法手册一样，那rag效果会非常好，如果像散文诗，rag效果就会很差。我们拿到手的文档一般介于两者之间，所以想提高rag效果，只好把文档本身往编程语法手册方向改

- 我现在最头疼的是pdf文档，里面全是图片的那种。，
  - 让甲方加钱，图片到文字的转换不仅需要工具，还需要人工审阅，不加钱没法干
