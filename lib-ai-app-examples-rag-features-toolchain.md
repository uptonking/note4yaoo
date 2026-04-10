---
title: lib-ai-app-examples-rag-features-toolchain
tags: [examples, rag, toolchain]
created: 2026-04-07T12:33:33.264Z
modified: 2026-04-07T12:33:48.087Z
---

# lib-ai-app-examples-rag-features-toolchain

# popular
- https://github.com/yeahhe365/InsightPDF /MIT/202601/ts
  - https://insightpdf.pages.dev/
  - 基于 AI 的 PDF 智能助手，支持见解提取、内容总结和智能文档搜索
  - 基于 Google Gemini 多模态模型构建的智能文档助手，支持精确的视觉定位与边框高亮。
  - 视觉定位 (Visual Grounding) AI 不仅回答问题，还会自动跳转到 PDF 对应页面，并用红框高亮显示答案来源（支持文本段落、图表、数据表格）
  - 聊天记录和设置均存储在浏览器本地（LocalStorage/IndexedDB），只需配置 Key，无需担心数据泄露。
  - PDF 渲染: React-PDF

- https://github.com/MrAMS/Smart-Search-PDFs /MIT/202601/python/qt5
  - 🔍 智能 PDF 搜索引擎 - 基于语义向量(embeddings)和 BM25 的混合搜索系统，可用于开卷考试离线搜索PDF课件
    - 一个基于语义向量（Embeddings）和 BM25 算法的本地化 PDF 混合搜索工具。
  - 全部在本地运行，无需 API Key，保护隐私。
    - 本地端侧：无需 GPU/API，使用 FastEmbed 和轻量级模型，CPU 也能流畅运行，无需 OpenAI API Key。
  - ux交互是双栏布局，左侧是文本，右侧是pdf原文，左侧搜索出的文本，右侧不会高亮
  - 混合搜索（智能推荐）： 结合了语义理解和关键词匹配。不仅能搜到字面一样的，还能搜到意思相近的。结果自动按相关度排序。
    - 语义搜索： 哪怕你输入的词文中没出现，只要意思对，就能搜到。（基于 Jina AI 的 Embeddings 模型）。
    - BM25 关键词： 经典的倒排索引算法，不仅是精确匹配，还能处理词频权重。
    - 大文件支持：动态加载机制，几百页的文档滚动流畅不卡顿。
  - [[开源自荐] 开卷考试/论文搜索神器 - 基于语义向量和BM25的PDF文件搜索软件 ](https://linux.do/t/topic/1408107)
    - 不管是开卷考试需要在几百页的 PPT 里瞬间定位知识点，还是写论文时需要在几十篇参考文献中寻找佐证，传统的 Ctrl+F 往往力不从心

- https://github.com/run-llama/liteparse /686Star/apache2/202603/python/ts
  - https://developers.llamaindex.ai/liteparse/
  - https://github.com/jerryjliu/liteparse_samples
  - LiteParse is a standalone OSS PDF parsing tool focused exclusively on fast and light parsing. 
  - It provides high-quality spatial text parsing with bounding boxes, without proprietary LLM features or cloud dependencies.
  - Everything runs locally on your machine.
  - Fast Text Parsing: Spatial text parsing using PDF.js
    - use a typescript wrapper called `pdfium` to simplify pdf.js integration
  - Flexible OCR System:
    - Built-in: Tesseract.js (zero setup, works out of the box!)
    - HTTP Servers: Plug in any OCR server (EasyOCR, PaddleOCR, custom)
    - Standard API: Simple, well-defined OCR API specification
  - Screenshot Generation: Generate high-quality page screenshots for LLM agents
  - 🐛
    - 仅导出文本， 丢失了文本格式， 是否丢失语义?
    - 需要支持扫描版pdf
  - Standalone Binary: No cloud dependencies, runs entirely locally
  - Multi-platform: Linux, macOS (Intel/ARM), Windows
  - https://github.com/run-llama/liteparse/tree/main/packages/python
    - Python wrapper for LiteParse 
  - https://x.com/jerryjliu0/status/2034665976428724267
    - Introducing LiteParse - the best model-free document parsing tool for AI agents 

- https://github.com/AstraBert/litesearch /202604/ts/rust
  - Fully-local search engine with `Liteparse`, transformers.js and Qdrant Edge
  - A fully-local semantic search CLI. Ingest documents, embed them locally, and run vector search — no external services required.
  - `litesearch retrieve` embeds the query with the same model and performs a cosine similarity search against the local shard.
  - Parse: extracts plain text from the file using LiteParse
  - Chunk: splits the text into overlapping segments using Chonkie (default: 512 characters)
  - Embed: generates 768-dimensional embeddings locally using nomic-ai/nomic-embed-text-v1.5 via @huggingface/transformers
  - Store: upserts vectors and payloads into a local Qdrant Edge shard persisted at .litesearch.qdrant/
    - The vector store is backed by qdrant-edge-utils, a Rust native addon (napi-rs) that wraps qdrant-edge for on-disk mmap-backed storage.
  - https://x.com/itsclelia/status/2038342859641037300
    - Probably an overkill for text-based documents, but for PDFs/images/office docs it could work
    - the path-based filtering for retrieval is the kind of feature that sounds boring until youre actually using it in a real project with dozens of doc categories. context scoping matters more than the embedding quality once your corpus gets large enough
  - https://github.com/qdrant/qdrant-edge-demo
    - https://qdrant.tech/edge/
    - POC visual search with smart glasses and Qdrant Edge.
# rag-memory/context
- https://github.com/zilliztech/memsearch /109Star/MIT/202602/python
  - https://zilliztech.github.io/memsearch/
  - A Markdown-first memory system, a standalone library for any AI agent. Inspired by OpenClaw.
  - basically proper RAG over markdown files with:
    - Hybrid search (vector + BM25, weighted fusion)
    - File watching + auto-indexing
    - Framework agnostic
  - Write memories as markdown, search them semantically. Inspired by OpenClaw's markdown-first memory architecture. Pluggable into any agent framework.
  - Ready-made Claude Code plugin — a drop-in example of agent memory built on memsearch
  - Markdown is the source of truth — the vector store is just a derived index, rebuildable anytime.
  - [RAG for AI memory: why is everyone indexing databases instead of markdown files? : r/Rag _202602](https://www.reddit.com/r/Rag/comments/1r2hlzd/rag_for_ai_memory_why_is_everyone_indexing/)

- https://github.com/volcengine/OpenViking /839Star/apache2/202602/python/cpp
  - https://openviking.ai/
  - 专为 AI Agent 设计的上下文数据库
  - OpenViking 摒弃了传统 RAG 的碎片化向量存储模式，创新性地采用 “文件系统范式”，将 Agent 所需的记忆、资源和技能进行统一的结构化组织。
  - 像管理本地文件一样构建 Agent 的大脑
  - 文件系统管理范式 → 解决碎片化问题：基于文件系统范式，将记忆、资源、技能进行统一上下文管理
  - 分层上下文按需加载 → 降低 Token 消耗：L0/L1/L2 三层结构，按需加载，大幅节省成本
  - 目录递归检索 → 提升检索效果：支持原生文件系统检索方式，融合目录定位与语义搜索，实现递归式精准上下文获取

- https://github.com/jakops88-hub/Long-Term-Memory-API /202512/ts
  - A Memory Server for AI Agents. Runs on Postgres + pgvector. 
  - Now supporting 100% Local/Offline execution via Ollama.
  - [I implemented Hybrid Search (BM25 + pgvector) in Postgres to fix RAG retrieval for exact keywords. Here is the logic. : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pcvtan/i_implemented_hybrid_search_bm25_pgvector_in/)
    - I don't stick to just one framework myself, most people jump between LangChain (for quick prototyping) and **Vercel AI SDK** (for production/streaming). MemVault is built to work with both. Regarding state, yeah, MemVault handles the state layer.
    - So the queries sent back to memvault are plain nlp texts ?
      - Exactly. You just send raw text (e.g., "What is the user's budget?")
      - The API handles the embedding/vectorization internally and matches it against the stored memories. So from the agent's perspective, it's just natural language in, relevant context out.
    - Does it work well enough for other languages? Did you try that?
      - you're right, 'english' is too aggressive with stemming. I haven't tested non-English languages extensively yet, but switching to the 'simple' config is the smart move to remove stemming issues, I'll update the config to that now.

- https://github.com/mem0ai/mem0 /apache2/202409/python
  - https://mem0.ai/
  - Mem0 (pronounced as "mem-zero") enhances AI assistants and agents with an intelligent memory layer, enabling personalized AI interactions. 
  - Mem0 remembers user preferences, adapts to individual needs, and continuously improves over time, making it ideal for customer support chatbots, AI assistants, and autonomous systems.
  - Multi-Level Memory: User, Session, and AI Agent memory retention
  - Mem0 leverages a hybrid database approach to manage and retrieve long-term memories for AI agents and assistants. 
    - Each memory is associated with a unique identifier, such as a user ID or agent ID, allowing Mem0 to organize and access memories specific to an individual or context.
    - 🛢️ When a message is added to the Mem0 using add() method, the system extracts relevant facts and preferences and stores it across data stores: a vector database, a key-value database, and a graph database. 
    - This hybrid approach ensures that different types of information are stored in the most efficient manner, making subsequent searches quick and effective.
    - Mem0 performs search across these data stores, retrieving relevant information from each source

- https://github.com/getzep/zep /apache2/202409/go
  - https://docs.getzep.com/
  - a long-term memory service for AI Assistant apps. 
  - With Zep, you can provide AI assistants with the ability to recall past conversations, no matter how distant, while also reducing hallucinations, latency, and cost.
  - Zep persists and recalls chat histories, and automatically generates summaries and other artifacts from these chat histories. 
  - Zep also provides a simple, easy to use abstraction for document vector search called Document Collections. This is designed to complement Zep's core memory features, but is not designed to be a general purpose vector database.
# graph-knowledge
- https://github.com/paukkroa/SemaTree /202603/python
  - a framework for managing and querying semantically structured graph-like knowledge bases
  - SemaTree turns documentation websites and local folders into navigable semantic file trees that AI agents can explore with simple tools. Instead of retrieving chunks statistically, agents navigate a clean directory hierarchy to find exactly what they need — with precise control over how much context they consume at each step.
  - [Experimentation with semantic file trees and agentic search : r/Rag _202603](https://www.reddit.com/r/Rag/comments/1rq6p3p/experimentation_with_semantic_file_trees_and/)

## graph-examples

- https://github.com/liujuntao123/DeepRead /MIT/202509/ts
  - https://deepread.aizhi.site/
  - AI 驱动的智能书籍知识图谱, 将书籍转化为相互关联的知识网络
  - 基于大语言模型的全书内容分析
  - 类似 deepwiki/codewiki 的书籍版本

- https://github.com/abhigyanpatwari/GitNexus /202601/ts
    - https://gitnexus.vercel.app/
    - GitNexus is a client-side knowledge graph creator that runs entirely in your browser. 
    - Drop in a GitHub repo or ZIP file, and get an interactive knowledge graph wit a built in Graph RAG Agent. Perfect for code exploration
    - Zero-Server, Graph-Based Code Intelligence Engine Works fully in-browser through WebAssembly. (DB engine, Embeddings model, AST parsing, all happens inside browser)
# chunking
- https://github.com/MichalZnalezniak/Chunking-Vis /MIT/202601/python
  - https://chunkingvis-production.up.railway.app/
  - A tool for visualizing different text-chunking methods.
  - Chunking Methods
  - [Built a tool for visualizing text chunking strategies : r/Rag](https://www.reddit.com/r/Rag/comments/1qnplpb/built_a_tool_for_visualizing_text_chunking/)
    - https://chunkviz.up.railway.app/

- https://github.com/ai-agents-buzz/rag-chunking-playground /MIT/202603/html
  - https://aiagentsbuzz.com/tools/rag-chunking-playground/
  - [Built a RAG chunking playground — paste any document, see how different chunking strategies get split : r/Rag _202604](https://www.reddit.com/r/Rag/comments/1sffdpn/built_a_rag_chunking_playground_paste_any/)
    - Compare 6 chunking strategies side by side
    - Test retrieval with a query to see what each strategy returns (BM25)

- https://github.com/lumina-ai-inc/chunkr /AGPLv3/202410/python/ts/rust
  - https://chunkr.ai/
  - Vision model based PDF chunking.
  - We have temporarily switched to Textract for OCR from PaddleOCR. Textract is provided for free until we resolve PaddleOCR issues.
  - Lumina的一款基于视觉模型的PDF分块处理工具：Chunkr，速度每秒可处理约5页
  - 基于视觉模型进行段落提取和OCR，通过 Rust Actix 服务器统一输出，可实现单个NVIDIA L4 GPU上达到每秒约5页速度
  - 支持自托管部署，兼容GPU和CPU，提供用户界面

- https://github.com/chunkhound/chunkhound /974Star/MIT/202602/python
  - https://chunkhound.github.io/
  - Deep Research for Code & Files
  - Transform your codebase into a searchable knowledge base for AI assistants using semantic search via cAST algorithm and regex search. 
  - MCP integration - Works with Claude, VS Code, Cursor, Windsurf, Zed, etc
  - cAST Algorithm - Research-backed semantic code chunking
  - Multi-Hop Semantic Search - Discovers interconnected code relationships beyond direct matches
  - Semantic search - Natural language queries like "find authentication code"
  - Regex search - Pattern matching without API keys
  - Local-first - Your code stays on your machine
  - 22 languages with structured parsing, via Tree-sitter
  - Real-time indexing - Automatic file watching, smart diffs, seamless branch switching
  - pr已合并 [refactor: Extract BaseCLIProvider and improve OpenCode integration _202512](https://github.com/chunkhound/chunkhound/pull/122)

- https://github.com/CoreyFransen08/chunk-forge /apache2/202512/python/ts
  - A self-hosted document processing platform for converting PDFs to Markdown with semantic chunking, drag-and-drop editing, rich metadata management, and multi-format export.
  - Upload PDFs and convert them to Markdown using LlamaParse, MarkItDown, or Docling.
  - Multiple strategies (recursive, paragraph, heading, semantic, sentence, token, hierarchical) with configurable chunk sizes.
  - Frontend: React + Vite + TypeScript + Tailwind CSS + dnd-kit
  - Backend: Node.js + Express + TypeScript + Drizzle ORM
  - Parser Service: Python + FastAPI + LlamaParse/MarkItDown/Docling
  - Storage: Local filesystem
  - Built-in export presets for popular vector databases: Pinecone, Chroma

- https://github.com/zirkelc/chunkdown /MIT/202512/ts
  - a tree-based markdown text splitter to create semantically meaningful chunks for RAG applications.
  - Unlike traditional splitters that use simple character or regex-based methods, this library leverages markdown's hierarchical structure for optimal chunking. 
  - Chunkdown is built around a few core ideas that guide its design:
    - Markdown as Hierarchical Tree
  - https://x.com/zirkelc_/status/2000847712884068755
    - Chunkdown now supports split rules for fenced code blocks and inline code
  - https://x.com/zirkelc_/status/1992520261325771153
    - Chunkdown now compacts markdown tables thanks to a one-line PR
    - Markdown tables can be pretty formatted with additional dashes and spaces to align the columns vertically. This makes them easier for humans to read, but wastes tokens and embedding space on useless characters

- https://github.com/speedyk-005/chunklet-py /MIT/202512/python
  - https://speedyk-005.github.io/chunklet-py/
  - One library to split them all: Sentence, Code, Docs. Chunk smarter, not harder
  - Supports over 50 natural languages for text and document chunking 
  - formats including .pdf, .docx, .epub, .txt, .tex, .html, .hml, .md, .rst, .rtf, .odt, .csv, and .xlsx.
  - Triple Interface: CLI, Library & Web
  - [[Release] Chunklet-py v2.1.0: Interactive Web Visualizer & Expanded File Support! : r/Rag](https://www.reddit.com/r/Rag/comments/1prjdjp/release_chunkletpy_v210_interactive_web/)
    - Our `CodeChunker` is rule-based and language-agnostic, using clever patterns to identify functions, classes, and logical blocks without the overhead of heavy dependencies like tree-sitter.
  - ["Docling vs Chunklet-py: Which Document Processing Library Should You Use?" : r/Rag _202511](https://www.reddit.com/r/Rag/comments/1p42qik/docling_vs_chunkletpy_which_document_processing/)
    - Key Difference: Docling focuses on document understanding with complex chunking options, while Chunklet-py focuses on accessible, intelligent chunking with superior metadata and universal language support.

- https://github.com/supermemoryai/code-chunk /MIT/202512/ts
  - AST-aware code chunking for semantic search and RAG pipelines.
  - Uses `tree-sitter` to split source code at semantic boundaries (functions, classes, methods) rather than arbitrary character limits. 
  - Each chunk includes rich context: scope chain, imports, siblings, and entity signatures.
  - Batch processing: Process entire codebases with controlled concurrency
  - Streaming: Process large files incrementally
  - [Building code-chunk: AST Aware Code Chunking _202512](https://supermemory.ai/blog/building-code-chunk-ast-aware-code-chunking/)

- https://github.com/xuzeyu91/AntSK-FileChunk /202512/python
  - 一个基于语义理解的智能文本切片服务，专门用于处理PDF和Word文档，能够根据段落语义进行合理切片，避免传统基于Token数量切分导致的语义割裂问题。
  - 支持PDF、Word（.docx/.doc）、纯文本等多种文档格式
# embedding
- https://github.com/PotentiallyARobot/EmbeddingAdapters /NC/202604/python
  - https://www.embedding-adapters.com/
  - Universal embedding-space translation library. 
  - Plug-and-play adapters that map one embedding model’s vector space into another — locally or via API — enabling cross-model retrieval, routing, and interoperability.
  - a lightweight Python library and model collection that lets you map embeddings from one model’s space into another’s.
  - [I built a Python library that translates embeddings from MiniLM to OpenAI _202512](https://www.reddit.com/r/Rag/comments/1py8l8f/i_built_a_python_library_that_translates/)

- https://github.com/AlwaysSany/huggingface-local-embedding /MIT/202507/python
  - A Fast API server that provides local text and multi-modal embedding using LlamaIndex Hugging Face Embedding

- https://github.com/huggingface/text-embeddings-inference /apache2/202511/rust
  - A blazing fast inference solution for text embeddings models.
  - From scratch implementation, no Vector DBs yet.
  - Steps to Chat with Any PDF in Gradio UI

- https://github.com/kannandreams/latentlens /202512/python
  - https://latentlens.streamlit.app/
  - a powerful visual debugger and educational tool for exploring vector embeddings. 
  - It helps you peek inside the "black box" of semantic search by projecting high-dimensional vectors into an interactive 3D map.
  - 3D Projection: PCA → UMAP reduction into an interactive 3D scatter plot.
  - Multiple Embedders: Support for Demo (synthetic), local MiniLM (sentence-transformers), and OpenAI (text-embedding-3-small).
  - Flexible Storage: Ships with an in-memory/local `ChromaDB` adapter.
  - matplotlib (for heatmap rendering)
# vectordb
- https://github.com/vectordbz/vectordbz /NonOpen
  - http://vectordbz.com/
  - modern desktop application for exploring, managing, and analyzing vector databases
  - Multiple Database Support — Connect to Qdrant, Weaviate, Milvus, ChromaDB, Pinecone, pgvector, and Elasticsearch

- https://github.com/Mintplex-Labs/vector-admin /2.2kStar/MIT/202401/ts/inactive
  - https://vectoradmin.com/
  - The universal tool suite for vector database management. Manage Pinecone, Chroma, Qdrant, Weaviate and more vector databases with ease
  - This repo and project is no longer actively maintained by Mintplex Labs. We hope one day to grow the team large enough to restart dedicated support and updates for this project. our main focus has moved to AnythingLLM.
# eval/bench-rag
- https://github.com/Aaryanverma/trustifai /MIT/202601/python
  - a Python-based observability engine designed to evaluate the trustworthiness of LLM responses and Retrieval-Augmented Generation (RAG) systems. 
  - Unlike simple evaluation frameworks that rely on a single "correctness" score, TrustifAI computes a multi-dimensional Trust Score based on grounding, consistency, alignment, and diversity.
  - It also includes visualizations to help showcase why a model output was deemed unreliable.
  - [A framework to evaluate RAG answers in production : r/Rag](https://www.reddit.com/r/Rag/comments/1qpla70/a_framework_to_evaluate_rag_answers_in_production/)

- https://huggingface.co/datasets/G4KMU/t2-ragbench
  - [T2-RAGBench - Benchmark for RAG in Finance (10K Downloads on HF) : r/Rag](https://www.reddit.com/r/Rag/comments/1pde2au/t2ragbench_benchmark_for_rag_in_finance_10k/)

- https://github.com/mburaksayici/smallevals /202512/python
  - A lightweight evaluation framework powered by tiny 0.6B models — runs 100% locally on CPU/GPU/MPS, attach any vector DB connection and run, fast and free.
  - Evaluation tools requiring LLM-as-a-judge or external, that costs/doesn't scale easily. 
# search 🔍
- https://github.com/AL-MARID/Lorph /MIT/202602/ts
  - AI chat application designed to run locally on your device, offering a seamless interactive experience with powerful large language models (LLMs) via Ollama.
  - What truly sets Lorph apart is the advanced and excellent search system I've developed. It's not just about conversation; it extends to highly dynamic and effective web search capabilities, enriching AI responses with up-to-date and relevant information.
  - Dynamic Web Search Integration: Leverages real-time web search to augment AI responses with current and relevant information.
  - Supports text extraction from images (OCR), PDF documents, Microsoft Word (.docx), and Excel (.xlsx) files, enhancing contextual understanding for AI responses.
  - [Lorph: A Local AI Chat App with Advanced Web Search via Ollama : r/ollama _202602](https://www.reddit.com/r/ollama/comments/1qy77nm/lorph_a_local_ai_chat_app_with_advanced_web/)

- https://github.com/tobi/qmd /5.1kStar/MIT/202602/python/ts
  - mini cli search engine for your docs, knowledge bases, meeting notes, whatever. 
  - Tracking current sota approaches while being all local
  - use it on the command line, it also exposes an MCP (Model Context Protocol) server for tighter integration.

- https://github.com/sovit-123/local_file_search /MIT/202510/python
  - Scripts to replicate simple file search and RAG in a directory with embeddings and Language Models.
# examples

# utils

# more
