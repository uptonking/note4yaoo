---
title: lib-ai-app-community-rag-pdf-ocr
tags: [community, image, ocr, pdf, rag]
created: 2026-01-25T17:22:38.106Z
modified: 2026-01-25T17:23:01.510Z
---

# lib-ai-app-community-rag-pdf-ocr

# guide

# discuss-stars
- ## 

- ## 

- ## [Architecture breakdown: Processing 2GB+ of docs for RAG without OOM errors (Python + Generators) : r/Rag _202602](https://www.reddit.com/r/Rag/comments/1qv2ks2/architecture_breakdown_processing_2gb_of_docs_for/)
  - Most RAG tutorials teach you to load a PDF into a list. That works for 5MB, but it crashes when you have 2GB of manuals or logs.
  - I built a pipeline to handle large-scale ingestion efficiently on a consumer laptop. 
  - I made a full code-along video explaining the implementation line-by-line using Python and LangChain concepts.
  - Here is the architecture I used to solve RAM bottlenecks and API rate limits:
  - Lazy Loading with Generators: Instead of docs = loader.load(), I implemented a Python Generator (yield). This processes one file at a time, keeping RAM usage flat regardless of total dataset size.
  - Persistent Storage: Using ChromaDB in persistent mode (on disk), not in-memory. Index once, query forever.
  - Smart Batching: Sending embeddings in batches of 100 to the API with tqdm for monitoring, handling rate limits gracefully.
  - Recursive Chunking with Overlap: Critical for maintaining semantic context across cuts.

- ## [AI开发者工具(2)——2024 年 12 个开源文档解析项目的选型对比评测：PDF解析、OCR识别功能解读、应用场景分析及优缺点比较 - 莫尔索随笔](https://liduos.com/ai-develope-tools-series-2-open-source-doucment-parsing.html)

# discuss-YOLO/traditional
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [From YOLO to VLMs: Advancing Zero-Shot and Few-Shot Detection of Wastewater Treatment Plants Using Satellite Imagery in MENA Region | Abstract _202512](https://arxiv.org/abs/2512.14312)

# discuss-pdf-elements
- ## 

- ## 

- ## 

- ## [Best way to handle pdfs containing huge tables in RAG : r/Rag](https://www.reddit.com/r/Rag/comments/1reezcu/best_way_to_handle_pdfs_containing_huge_tables_in/)
- Docling and detect and prechunk tables

- Parse into csv and add into a SQLite, have an agent to do that, don't do programmatically. Or have the rag trigger an agent with vision capabilities to answer
  - One approach, that can be expensive, is to have a vision model to parse the content and on a second step, the data is cleaned by another LLM call and validated against the original table. If you're running models at your end, it could be worth it.

- Sounds more suitable to store them in database tables and create/use a tool that query them.
# discuss-vlm
- ## 

- ## 

- ## 

- ## 
# discuss-tips
- ## 

- ## 

- ## 🆚 [RAG知识库还有搞头吗？ _202602](https://linux.do/t/topic/1576669)
- 由于业务需求，团队需处理海量的电子文档。单个表单涉及的 PDF 数量通常在 1000 至 5000 份不等。自 2025 年 12 月启动知识库项目以来，我们在几个月的实战中遇到了以下瓶颈：
  - 超长文档解析难：部分文档页数过多，解析速度极慢，且极易触发内存溢出（OOM）。
  - 工程图纸识别精度低：项目中包含大量工程图纸，通用解析工具常将其误识别为普通图片，导致要素提取缺失或严重失真。
  - 多格式兼容性差：用户上传的文件涵盖 PDF、图片、CAD 及 Office 办公文档。虽然 PDF 解析相对成熟，但对于超多列的复杂 Excel 表单，解析效果堪称 “灾难”。
  - 深度问答可靠性不足：对于高难度的逻辑推理问答，单纯依赖通用 LLM 的语义检索往往难以达到业务精度要求。
  - 其他长尾问题：如离线部署环境下的资源分配、响应延迟等。
- 我们优先对市面主流的开源 RAG 框架进行了评测，以下是各产品的实测反馈：

1. RAGFlow
地位：RAG 领域的重量级框架。

核心优势：
多租户架构：具备完善的团队 / 租户权限管理。
工作流编排：支持灵活的问答流程定制。
DeepDoc：其自研的解析神器，是目前对复杂文档适配度较高的方案之一。
实测痛点：
精度与性能平衡：面对复杂图纸时要素遗漏较多。CPU 模式解析极慢，GPU 模式虽有提升但仍非实时；且由于是内部框架，二次开发门槛较高。
OCR 适配：第三方 OCR 引擎接入尚处于实验阶段，底层仍高度依赖内置引擎。
幻觉问题：纯向量检索难以应对结构化查询，需引入 MCP（Model Context Protocol）结合 SQL 查询来增强。
开源协议：Apache License 2.0。

2. Dify
地位：生态最丰富、上手门槛最低的 RAG 平台。

核心优势：极其出色的流程编排与插件功能，支持外挂 RAGFlow 知识库。
实测痛点：
知识库 “偏科”：Dify 的核心在于 Agent 编排，其自带的文档切割与索引功能相对基础。虽可通过插件强化，但需投入额外开发精力。
商业限制（需留意）：
其修改版的 Apache 2.0 协议规定：禁止未经授权运营多租户 SaaS；必须保留 UI 标识。
结论：若需多租户或深度去标识化商用，必须通过 API 接入自研前端。

3. Yuxi-Know（语析）
特点：界面友好，符合国人逻辑。
实测痛点：OCR 引擎对接方案较为生涩，虽然选项多，但实际落地效果不佳，更适合处理中短篇幅的简单文档。
开源协议：MIT（极度友好）。

4. Weknora (腾讯)
特点：模块化架构，融合多模态预处理，大厂出品。
实测痛点：OCR 引擎内聚程度过高，几乎无法灵活切换或自定义识别逻辑，改造难度大。
开源协议：MIT。

5. AnythingLLM
特点：功能全家桶，内置 TTS/STT，开箱即用体验好。
实测痛点：OCR 依旧是短板，面对专业领域的重度文档显得力不从心。
开源协议：MIT。

- 核心痛点汇总
  - OCR 解析能力的 “资源与精度” 悖论：在离线部署的有限硬件資源下，难以同时满足 “高速度” 与 “高精度” 的解析需求。
  - 混合检索与统计分析缺失：业务问答不只是语义匹配，往往涉及大量数据库统计（Chat2SQL）。纯 RAG 方案在处理这类问题时容易 “抓瞎”。

- 总结与反思 目前项目处于 “深水区”：通用框架在面对工业级、超长、复杂版面文档时，均出现了明显的边际效应。
- 下一步我们可能需要跳出 “全盘依赖开源框架” 的思维：
  - 解耦解析层：建立独立的 OCR 解析集群，将长文档切片并行处理，并引入 VLM 进行关键要素校准。
  - 强化 MCP 架构：不再强求 LLM 读懂整个 Excel，而是通过 Agent 调用 SQL 插件进行数据分析。

- 👥

- rag 已经被数学证明了上限，因此可以说已经是可以看到头的路了，现在更好的方法应该是学习 openclaw，做一个文件目录，制作一个只读 agent 查询文件大纲进行具体内容查询

- 我之前在小米工作的时候看别的部门的同事也有遇到你们这个问题的，最后的解决办法是魔改 dify，自己造前端，开发额外插件的形式，这个我感觉是做的最快的方式了，兼容模式都可以依靠插件解决，然后阅读超长文本这个具体得看你的需求的了，我之前做部门自己的 RAG 的时候是按照 dify 做的，用于一些诊断工作，延迟响应还是很快的

- RAG 还是得看人的设计，因为之前隔壁部门能压缩到 100ms，正确率 100%，我第一次做只能 300ms，这真的比不了，切片太吃经验了，搭建简单，优化非常难

- 
- 
- 
- 
- 

- ## [Information extraction with long document (images included) : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nuvwak/information_extraction_with_long_document_images/)
- The document parsing step you outlined is solid but you're overcomplicating the image-text mapping part.
  - Your approach of converting pages to images first then using VLM is actually the right direction, but I'd simplify step 1. Instead of doing separate OCR for bounding boxes then trying to map cropped images back to text tags, just let the VLM handle both text extraction AND image positioning in one pass. Most decent VLMs can already tell you "there's an image here between paragraph X and Y" without needing separate OCR tools. For the actual implementation, yeah OpenAI's vision models work great for this but if you want to keep it local, try running something like LLaVA or the newer Qwen2-VL models. The key thing is being really specific in your prompts about maintaining spatial relationships and hierarchical structure. 
  - For step 2, instead of trying to get the LLM to cite page numbers (which honestly isn't super reliable), consider keeping a metadata mapping where each extracted section links back to the original page ranges from step 1. 
  - The RAG approach you mentioned as a backup is actually pretty smart because it gives you flexibility when section titles are vague or when content spans weird boundaries. We've seen similar challenges with educational content processing using Docstrange and the hybrid approach tends to work better than trying to make one method handle all edge cases perfectly.

# discuss-solutions
- ## 

- ## 

- ## 

- ## 

- ## [如何提高mineru解析PDF文件中图片的分辨率？ ](https://linux.do/t/topic/1498862)
- 最好先看看原版 pdf 另存出来是不是就是高质量的

- ## [DeepSeek-OCR - Lives up to the hype : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ocrocy/deepseekocr_lives_up_to_the_hype/)
  - Hardware - 1 x A6000 ADA on a Ryzen 1700 /w 32gb ram
  - Processed prompts: 100%|██████████| 1/1 [00:00<00:00, 3.29it/s, est. speed input: 3000.81 toks/s, output: 220.20 toks/s]
- Here is a more technical analysis. The result being the model response. Going to update the OP with this data.
  * **Content and Metadata:** The `result` field within each object in the `results` array contains the core document information as a string. This string is a mix of:
  * **Markdown-like Syntax:** It uses Markdown conventions for formatting, such as `#` for headings and `**` for bold text.
  * **HTML Tags:** It directly embeds HTML `<table>` tags to structure tabular data.
  * **Custom Tags:** The format uses a set of unique tags to provide additional metadata:
  * `<|ref|>` and `<|/ref|>` : These tags appear to act as "reference" or "type" markers. They enclose a word that categorizes the succeeding content, such as `title` , `text` , or `table` .
  * `<|det|>` and `<|/det|>` : These tags likely stand for "details" or "detection" and enclose what appear to be coordinates `[[45, 90, 380, 114]]` . These represent the bounding box or location of the corresponding element on an original document page.

- How’s the quality of markdown files after processing?
  - Honestly its insane. I run qwen 3 vl 30ba3b instruct and this kind of detail that includes bbox coordinates can take 30+ seconds a page and still doesn't get it right

- The problem with this kind of OCR is, when classic OCR can't recognize a word, it writes gibberish. When Deepseek OCR can't recognize a word, it writes a word that fits the context the most. Gibberish you can pinpoint with a spellchecker. A made up but grammatically correct word you have to proofread manually.
  - But, it's also what a human would try to achieve as well.

- Does it handle forms with checkboxes ?
  - Not from my limited experience. There are multiple layers of pre and post processing im working through. The api has most of them enabled but a few are lacking.

- I would say, in terms of precision: Dots.ocr > Deepseek ocr > Docling
  - What I like about dots.ocr is that they return an array of layout elements (text, category, bbox); which you can serialize to any format—especially markdown.

- ## 🧩💡 [FinePDFs: Liberating 3T of the finest tokens from PDFs _202601](https://huggingface.co/spaces/HuggingFaceFW/FinePDFsBlog)
- At the beginning of 2025, our team faced a question that looms over the entire field of AI: Have we run out of data?
  - In creating both iterations of the FineWeb datasets (Penedo et al., 2024, 2025), we had effectively exhausted CommonCrawl’s (Common Crawl Foundation, 2024) HTML archives. At that point, self-hosted crawls or synthetic data (Maini et al., 2025) seemed to be our only options forward.
  - But wasn’t there a large amount of high-quality data still hidden in CommonCrawl for the curious to find? Indeed there was: PDFs.
  - While this format has been largely ignored by the open-source AI community for years, we found it to be a source of high-quality data for pretraining, and importantly a source of long-context documents so often missing from open data.
- Pretraining corpora have historically been derived almost entirely from processed HTML snapshots of CommonCrawl (e.g., Dolma (Soldaini et al., 2024), Nemotron-CC (Su et al., 2024), and RedStone (Chang et al., 2024)). Alternative datasets such as Harvard’s Institutional Books corpus (Institutional Data Initiative, 2025) and the PleIAs Common Corpus (Langlais et al., 2025) exist, but they are smaller in scale and less systematically analyzed. By contrast, the rich non-HTML content embedded within CommonCrawl—especially PDFs—has received comparatively little attention, leaving a large, underexplored opportunity for corpus construction.
- PDFs make up only about 0.6% of the crawl (Common Crawl Foundation, 2025). Why spend time on such a small fraction of the web?
  - The answer lies in information density. Unlike HTML pages, which are often lightweight and boilerplate-heavy, PDFs are typically long dense documents—reports, government papers, and manuals. Content that requires significant effort to create typically correlates with higher information density.
- PDFs were built to preserve appearance, not to expose structure. Where HTML gives you a clean tree of tags, a PDF gives you a set of drawing commands: put this glyph here, draw that line there, paint an image now. The result is visually faithful, but missing any sort of semantic structure.
- there are three broad strategies:
- Pure parsing (PyMuPDF (PyMuPDF contributors, 2024), pdfminer (pdfminer.six contributors, 2024))
  - Strategy: read the raw PDF text objects and infer structure with heuristics (font size → headers, proximity → columns).
  - Quality: fails on scanned PDFs and struggles with complex layouts, as well as tables and math.
- Pipeline methods (MinerU (Wang et al., 2024), Docling (Livathinos et al., 2025))
  - Strategy: detect layout blocks with a small ML model, align embedded text to those blocks, then apply specialized extractors (tables, figures, captions) before stitching output together.
  - Quality: better structure than pure parsing while staying lighter than full OCR. However, reading order and fragmented words can still be a challenge.
  - Cost: batching and good resource utilization are hard to implement (many moving parts and GPU/CPU interop). <1 page/sec on 1 core with minimal ML inference.
- End-to-end OCR / VLM (Nougat (Blecher et al., 2023), Got-OCR (Wei et al., 2024), RolmOCR (Reducto AI, 2025))
  - Strategy: render each page to an image and let a vision-language model transcribe the page directly.
  - Quality: best reading order and parsing of certain structures (tables, math, etc.). However, it can randomly hallucinate names/tables or full pages in ways that are hard to detect.
- Early qualitative checks, along with OlmOCR results (Poznanski et al., 2025), suggested that end-to-end OCR was the best-quality option. But running it on every PDF was far beyond our GPU budget. 
- Inspired by CCpdf (Turski et al., 2023), we therefore devised a hybrid approach: use GPU parsing only when needed (scanned documents) and keep everything else on the cheap CPU path. 
  - To do so, we trained a lightweight classifier that predicts whether a PDF is extractable (CPU parsing) or needs OCR (GPU parsing).
  - we trained a lightweight XGBoost classifier (Chen & Guestrin, 2016) on features aggregated from 8 random pages plus doc-level signals (inspired by MinerU (Wang et al., 2024) and Docling (Livathinos et al., 2025)). We intentionally excluded Docling’s bitmap-coverage feature because it was too expensive to compute at scale.

- We ultimately selected `Docling` as our CPU extractor, as it consistently ranks first across our eval tasks. 
  - However, if one is more CPU constrained, we strongly recommend `PyMuPDF4LLM` since it’s almost 8x faster than Docling (even after our optimizations), while staying close in quality.

- To pick an OCR model, we benchmarked model-based extractors on three suites: OlmOCR (Poznanski et al., 2025), OmniDocBench (Ouyang et al., 2024), and the multilingual slice of CC-OCR (Yang et al., 2024). 
  - Evaluations ran in May 2025, so newer OCR models released after that date are not included.
  - Finally, based on the results, we chose RolmOCR (Reducto AI, 2025) for production at the time of extraction because it delivered reasonable speed. We used a min/max resolution range of 1280–2048 to balance quality and speed.
- Since we needed the pipeline to be as fast as possible, we tested inference with the 3 most popular engines: SGLang (3.04 pages/sec), vLLM (3.64 pages/sec), and LMDeploy (4.1 pages/sec). Throughput results made the choice of engine a no-brainer: we used `LMDeploy`, the fastest by far.
- We also noticed the OCR model would sometimes go into repetition loops until it exhausted the context length (8192 tokens in our case). This hurt both quality and speed as useless tokens were being generated at long sequence lengths. To fix this, we implemented a simple repetition checker (line, character, and word-level) directly inside LMDeploy, which further increased throughput to 5.17 pages/sec.

- After extraction, we refined the raw text to steadily improve quality. 
  - The postprocessing steps focused on three things: cleaning Docling tags, removing boilerplate, and filtering out hallucinated content.
- Because Docling uses a layout model, it’s able to deduce and label many common structures (tables, figures, captions, etc.). 
  - We only cared about two: tables (`<docling_table/>`) and picture annotations (`<docling_picture_annotations/>`) as others were empty and not used due to disabling extractors for these structures.
  - For tables, we used heuristic extraction via `pymupdf4llm`, which caused many of them to be frequently broken (misaligned columns, missing headers). We therefore experimented with removing problematic tables, removing all tables, or cleaning them up.
  - Picture annotations had a similar issue. We initially kept them, but they often contained sequences of letters, tick labels, or isolated numbers disconnected from any surrounding text. Such issues are caused by charts
  - We therefore tested filtering annotations by alpha ratio (number of alphabetic characters / total characters); finding the best setting to be a threshold of 0.8, altough all the results were rather close.
- remove boilerplate: headers, footers, watermarks, company names. 
- We noticed a recurring hallucination pattern in RolmOCR outputs: on blank pages and pages that were mostly graphics/images, the model would hallucinate fluent text, always starting with "The"
  - To fix this, we did not have time to train a dedicated image classifier, and running a heavy vision model across the whole corpus was too expensive.

- The result is two SoTA datasets: FinePDFs and FinePDFs-EDU. While we tried to preserve as many documents as possible, we still removed more than 66% of our initial dataset to create FinePDFs, and more than 96% to create FinePDFs-EDU. This massive reduction was mostly due to the deduplication steps and heavy model based filtering (for the EDU variant).
# discuss
- ## 

- ## 

- ## [Structure-first RAG with metadata enrichment (stop chunking PDFs into text blocks) : r/Rag](https://www.reddit.com/r/Rag/comments/1r9updr/structurefirst_rag_with_metadata_enrichment_stop/)
  - [Metadata-Enriched RAG: Document Structure Beats Text Chunking](https://kudra.ai/metadata-enriched-rag-agent-why-document-structure-beats-text-chunking/)
  - The problem is research papers aren't random text. They're hierarchically organized (Abstract, Introduction, Methodology, Results, Discussion). Each section answers different question types. Destroying this structure makes precise retrieval impossible.
  - I've been using structure-first extraction where documents get converted to JSON objects (sections, tables, figures) enriched with metadata like section names, content types, and semantic tags. The JSON gets flattened to natural language only for embedding while metadata stays available for filtering.
  - The workflow uses Kudra for extraction (OCR → vision-based table extraction → VLM generates summaries and semantic tags). Then LangChain agents with tools that leverage the metadata. When someone asks about datasets, the agent filters by content_type="table" and semantic_tags="datasets" before running vector search.
  - This enables multi-hop reasoning, precise citations ("Table 2 from Methods section" instead of "Chunk 47"), and intelligent routing based on query intent. For structured documents where hierarchy matters, metadata enrichment during extraction seems like the right primitive.

- [Structure-first RAG with metadata enrichment (stop chunking PDFs into text blocks) : r/LangChain](https://www.reddit.com/r/LangChain/comments/1r9ur3x/structurefirst_rag_with_metadata_enrichment_stop/)
- Totally agree. Structure first extraction with metadata filtering makes RAG far more precise and lets you cite exact tables and sections.

- ## [Qwen3-VL for OCR: PDF pre-processing + prompt approach? : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q92olo/qwen3vl_for_ocr_pdf_preprocessing_prompt_approach/)
- PaddleOCR-VL. You'll lose information with just a VLM , and higher risk of hallucination.
  - There's a lot of built in features in it - drawing bounding boxes and their positions, predicting of the class of the text - headers, footers, body, tables. In my testing it's able to handle logos, signatures very well - it doesn't try to produce text for it, it'll crop them out and within the mark down/JSON it'll tell you where it belongs. It works well with scans and blurs as well. It makes post processing a lot easier.
  - And it's just 0.9B parameters.

- I think the problem with VLM is the way we are currently processing the image - models will usually cut up the image to image patches and learning features from them and the relation between the input text and the patches.
  - In my experience, providing the extracted text to "ground" or as a point of reference does help guide the model - similar to RAG
  - So my best guess is to try using OCR to extract the text, in the prompt include both the image , extracted text, and your instructions for what you want to extract.

- The preprocessing step matters more than the model choice here. PDF2image + PIL for image extraction works well, but you'll want to handle page segmentation carefully since contracts often have multi-column layouts or embedded tables that can confuse the model.
  - For Qwen3-VL specifically, you don't need a specialized package. Standard image preprocessing through transformers works fine. The key is your prompt structure. Instead of asking for "OCR, " frame it as "convert this document page to markdown" or "extract the text and structure." Qwen3 responds better to task framing than technical terms. Also watch out for token limits with 30B, contracts can get long and you might need to chunk pages.
  - I've been working on document processing pipelines at vectorflow.dev and see this pattern a lot. The bigger issue is usually downstream, once you have the text. How are you planning to handle the extracted content? Contracts have hierarchical structure that's easy to lose if you're not preserving section relationships and metadata during processing.
  - What's your target output format looking like? JSON with preserved document structure or flattened markdown?

- I'm training Qwen3-VL-2B for structured invoice extraction (to a fixed json format). Working pretty good so far. But I haven't tested other models yet, will do so because I would love to be able to go lower than 2B

- Looks like Qwen publishes an ‘OCR cookbook’ here: https://github.com/QwenLM/Qwen3-VL/blob/main/cookbooks/ocr.ipynb
