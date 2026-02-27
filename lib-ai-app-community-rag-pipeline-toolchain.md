---
title: lib-ai-app-community-rag-pipeline-toolchain
tags: [community, grep, rag, search, toolchain]
created: 2026-02-18T04:13:21.281Z
modified: 2026-02-18T04:15:19.228Z
---

#  lib-ai-app-community-rag-pipeline-toolchain

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-rag-tools/saas
- ## 

- ## 

- ## 

- ## 

- ## [Looking for feedback: Building an Open Source one shot installer for local AI. : r/LocalLLM _202602](https://www.reddit.com/r/LocalLLM/comments/1rco6la/looking_for_feedback_building_an_open_source_one/)
  - I’ve been working full time in local AI for about six months and got tired of configuring everything separately every time. So I built an installer that takes bare metal to a fully working local AI stack off one command 
  - It detects your GPU and VRAM, picks appropriate models
- https://github.com/Light-Heart-Labs/Lighthouse-AI /apache2/202602/python/js
  - https://lightheartlabs.io/
  - One command to a full local AI stack — LLM inference, chat UI, voice agents, workflows, RAG, and privacy tools.
  - vLLM for inference
  - Open WebUI for chat
  - Qdrant for RAG / vector search
  - LiteLLM as a unified model gateway
  - PII redaction proxy
  - n8n for workflow automation

- I really want a full agent stack in a box with nice attachment support and full computer-use.
  - Qwen3, for example, supports audio reasoning, video reasoning, and is fully trained for computer use. Getting all that to work? Get ready for weeks of coding.
  - Efficient file-search primitives work better than RAG. Id skip vector search

- I think the problem is that the people who care about this would rather tinker and customize themselves, and the people that don’t care won’t even know why they would need a RAG or use this process at all vs just using ChatGPT
  - I agree which is why it’s open source and not a closed project. You could use the setup, modify it, do whatever you want with it etc.

- 
- 
- 
- 
- 

# discuss-search-grep
- ## 

- ## 

- ## 

- ## I tested 7 semantic code search tools so you don't have to.
- https://x.com/c0mm0n_dev_us3r/status/2024343367732351151
  - The problem: grep is literal.
- In 2026, there are 3 categories of "better than grep":
  1. Deterministic code rules (AST)
  2. Semantic retrieval (embeddings)
  3. LLM reasoning over files
- ColGREP — the local-first king
  - Tree-sitter parses your code into semantic units. 
  - ColBERT multi-vector embeddings understand context. NextPlaid indexes locally.
  - Fully private. Fast. Incremental updates. Perfect for coding agents + private repos.
- osgrep — ColGREP's beefier cousin
  - Same tree-sitter foundation but adds:
  - Dual embeddings (dense + ColBERT int8)
  - LanceDB + FTS fusion via RRF
  - Staged reranking + structural boosts
  - Hot daemon mode for low-latency
  - Best for: when you need richer local ranking.
- mgrep — cloud-powered team search
  - Syncs your repo to Mixedbread Store. Search + rerank via API. Merges web + local sources in one query.
  - Multi-user friendly. Multimodal.
  - Tradeoff: code leaves your machine.
- rlmgrep — the thinker
  - Not embedding-first. Uses DSPy RLM to REASON iteratively over your files. Handles PDFs, Office docs, media.
  - Returns (path, line) matches + narrative answers.
  - Slower, costs tokens. But handles fuzzy investigative queries nothing else can.
- qmd — your local knowledge brain
  - SQLite FTS5 + vector search + GGUF query expansion + reranking. All local. Perfect for markdown/docs/notes knowledge bases.
- semtools — lighter entry point. 
  - Parses docs via LlamaParse, embeds lines, cosine search. Good starter.
- Semgrep — the deterministic guard
  - Not semantic search. AST-based pattern matching with rules.
  - Find SQL injections, enforce coding standards, catch bugs — zero false-positive ambiguity.
  - Use ALONGSIDE semantic tools, not instead of them.

- TL; DR decision tree:
  - Private local code search? ColGREP or osgrep
  - Cloud/team search? mgrep
  - Docs/KB retrieval? qmd (or semtools)
  - Reasoning Q&A over mixed files? rlmgrep
  - Security/compliance? Semgrep
  - No single tool wins. Stack them.
  - My setup: ColGREP + rg + Semgrep.

- ## grep uses exact text pattern matching. But sometimes exact matches aren’t enough. Here are 4 semantic search alternatives for grep:
- https://x.com/helloiamleonie/status/2023757180701147597
- semtools (by LlamaIndex)
  - https://github.com/run-llama/semtools /MIT/202602/rust
• Model: static embeddings (minishlab/potion-multilingual-128M)
• Processing: LlamaParse API (Cloud)
• Search: Local

- mgrep (by Mixedbread)
  - https://github.com/mixedbread-ai/mgrep /apache2/core未开源
• Model: Mixedbread model family
• Processing: Cloud-based via Mixedbread Search API
• Search: Cloud-based via Mixedbread Search API

- ColGrep (by LightOn)
  - https://github.com/lightonai/next-plaid/tree/main/colgrep /apache2/202602/rust
  - Combines regex filtering with semantic ranking with LateOn-Code-edge multi-vector embeddings.
  - A single Rust binary. No server. No API. 
  - 100% local, your code never leaves your machine
  - The Claude Code integration installs session and task hooks that: Inject colgrep usage instructions into the agent's system prompt
• Model: multi-vector embeddings (LateOn-Code family of models)
• Processing: local (tree-sitter)
• Search: Local (NextPlaid)

- osgrep (built on mgrep)
  - https://github.com/Ryandonofrio3/osgrep /apache2/202601/ts
• Model: dense embeddings (granite-embedding-30m-english-ONNX) + Mixedbread ColBERT-based reranker
• Processing: local (tree-sitter)
• Search: local

- rlmgrep
  - https://github.com/halfprice06/rlmgrep
  - Grep-shaped search and question answering powered by DSPy RLM. 
  - It accepts a natural-language query, scans the files you point at, and prints matching lines in a grep-like format. 

- I need a timed comparison between grep and semantic search. I’m slowly becoming grep-pilled tbh!
  - I doubt it's going to be faster but probably better results for natural language queries

- How do you pick between ColGrep and osgrep? I'll grep first, then rerank.
# discuss-rag-vector-db
- ## 

- ## 

- ## 

- ## 

- ## we launched Notion AI Q&A in Nov 2023, Notion vector search over the past 2 years: 10x scale, then 1/10th cost. 
- https://x.com/nxlouie/status/2024525357672808844
  - we evaluated alternative search engines—and @turbopuffer emerged as our top pick.
  - We achieved an incremental 60% reduction in search engine cost and 25% improved query latency just by switching
  - We built a way to detect incremental span changes in an edited page and utilized Turbopuffer’s PATCH functionality to skip embedding costs entirely for metadata changes.
  - Now we’re migrating near real-time embeddings to Ray running on @anyscalecompute
  - All in, we are at 90%+ reduction in embeddings infrastructure costs from our peak ramp up days!

- ## 🧮🧩 Hierarchical Navigable Small World (HNSW) is the algorithm that makes vector search actually fast at scale, letting us search through billions of vectors in milliseconds. 
- https://x.com/victorialslocum/status/2019003231456686375
  - HNSW builds a multi-layer graph structure where each layer has exponentially fewer nodes than the one below it.
  - So every vector exists in the bottom layer (layer 0), which is super well-connected. But only some vectors appear in layer 1, even fewer in layer 2, and so on. The higher layers act as "highways" that let you skip over tons of irrelevant data.
  - When you search, HNSW starts at the top layer, finds the closest node, then travels down to the next layer and repeats. By the time you reach the bottom layer, you've already narrowed down to the most relevant neighborhood - no need to search through everything.
  - This is why HNSW is so memory efficient compared to other approaches. It's able to "skip" through large amounts of data without scoring it.

- NSW is a beautiful example of structural efficiency: multi-layer navigation turns brute-force similarity into logarithmic traversal. 
  - But it also formalizes an approximation regime: search quality depends on graph topology, ef, connectivity, and metric choice.
  - At scale, the relevant question becomes: what invariants survive these index-induced transformations, and when does retrieval drift become structurally irreversible? This is exactly the kind of post-hoc boundary/coherence layer we study (OMNIA).

- HNSW is a great example of an algorithm thats elegant on paper and powerful in practice, but most real world issues end up coming from tuning and update patterns rather than the search itself.

- HNSW is not known for being memory efficient though compared to other vector indices like IVFFlat. Also HNSW indices are great for incremental inserts and thus do not have to be rebuild often.

- yep, SkipLists like structure but for graphs

- ## [I built a desktop GUI for vector databases (Qdrant, Weaviate, Milvus) - looking for feedback! : r/vectordatabase](https://www.reddit.com/r/vectordatabase/comments/1po6ela/i_built_a_desktop_gui_for_vector_databases_qdrant/)
  - VectorDBZ - a desktop app for exploring and managing vector databases.

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

- ## [Increasing your chunk size solves lots of problems - the default 1024 bit chunk size is too small : r/Rag _202602](https://www.reddit.com/r/Rag/comments/1r36f72/increasing_your_chunk_size_solves_lots_of/)
- you are wrong, but given you are only here to inform us that you are right, i think i'll let you find out yourself.
  - input-token costs off the charts, particularly with said big context models
  - amount of consulted sources decreases
  - granular information gets lost in the haystack
  - llm context gets polluted to absolute hell
  - what this guy pointed out niceley: search accuracy gets diluted
  - multi-step or multi-retrieval agents will despite what OP says absolutely hit context ceiling
  - while providers claim context windows of N, performance usually massively drops at arround max 0.4 N. Big context window doesnt mean its best to fill it to the brim, in the contrary.
  - Generally: for contextual-understandig-type things, rather big chunks are fine, for exact granular data retrieval smaller are better.

- The bottleneck for chunk size was never the context window of the reader, but rather the context window of the embedder as well as the “effective” context size of the embedder.
  - Even SOTA embedding models today don’t have much more than a few thousand tokens of context max, which is a hard limit on your chunk size assuming you are going to use vector search.
  - Additionally there is a very significant regression to the mean issue with embeddings, where if you put too many sentences together you start losing the signal of that piece of text.
  - I think the larger effective context size of the readers (decoder LLMs) means more context can be retrieved, but it shouldn’t have too much impact on the size of the chunks you are embedding.

- the point about embedder context being the actual bottleneck is the real answer here. you can feed 50 pages to gemini all day but if your embedding model only meaningfully represents the first 512 tokens of each chunk then your retrieval quality tanks regardless of chunk size
  - in practice what worked for me is chunking larger (2-4k tokens) but with overlap AND storing a summary embedding alongside the full chunk. retrieve on the summary, pass the full chunk to the LLM. best of both worlds

- Increasing chunk size feels like a win until you realize you’re just paying for 'Context Dilution.'
  - Mathematically, when you bloat chunks, your cosine similarity starts measuring the 'average' of a 6, 000-token soup rather than the specific needle you’re looking for. You end up with higher latency, higher token costs, and a model that gets 'Lost in the Middle'. The latter won't happen in case the answer fits in 1 or 2 chunks, but with pushing more chunks into the answer and agentic workflows where context is bloated by all the instructions and tools, it will take a significant toll.
  - Besides, by nature it's an endless optimization process. It must be based on evals to see, if it's a gain or a loss in your specific case. We automate experimentation and just find the mathematical 'sweet spot' for each specific use case.

- ## 🆚 [We Benchmarked 7 Chunking Strategies. Most 'Best Practice' Advice Was Wrong. : r/Rag _202602](https://www.reddit.com/r/Rag/comments/1r47duk/we_benchmarked_7_chunking_strategies_most_best/)
  - Somebody on your team (or a Medium post) told you to "just use 512 tokens with 50-token overlap" or "semantic chunking is strictly better."
  - We (hello from the R&D team at Vecta!) decided to test these claims. We created a small corpus of real academic papers spanning AI, astrophysics, mathematics, economics, social science, physics, chemistry, and computer vision. Then, we ran every document through seven different chunking strategies and measured retrieval quality and downstream answer accuracy.
  - Critically, we designed the evaluation to be fair: each strategy retrieves a different number of chunks, calibrated so that every strategy gets approximately 2, 000 tokens of context in the generation prompt. This eliminates the confound where strategies with larger chunks get more context per retrieval, and ensures we're measuring chunking quality, not context window size.
  - The "boring" strategies won. The hyped strategies failed. And the relationship between chunk granularity and answer quality is more nuanced than most advice suggests.
  - We assembled a diverse corpus of 50 academic papers (905, 746 total tokens) deliberately spanning similar disciplines, writing styles, and document structures: Papers ranged from 3 to 112 pages and included technical dense mathematical proofs pertaining to fundamental ML research. All PDFs were converted to clean markdown using MarkItDown, with OCR artifacts and single-character fragments stripped before chunking.
- Chunking Strategies Tested
  - Fixed-size, 512 tokens, 50-token overlap
  - Fixed-size, 1024 tokens, 100-token overlap
  - Recursive character splitting, LangChain-style 
  - RecursiveCharacterTextSplitter at 512 tokens
  - Semantic chunking, embedding-based boundary detection (cosine similarity threshold 0.7)
  - Document-structure-aware, splitting on markdown headings/sections, max 1024 tokens
  - Page-per-chunk, one chunk per PDF page, using MarkItDown's form-feed (\f) page boundaries
  - Proposition chunking, LLM-decomposed atomic propositions following Dense X Retrieval with the paper's exact extraction prompt
- All chunks were embedded with text-embedding-3-small and stored in local ChromaDB. Answer generation used gemini-2.5-flash-lite via OpenRouter. We generated 30 ground-truth Q&A pairs using Vecta's synthetic benchmark pipeline.
- How We Score Retrieval: Precision, Recall, and F1
  - We evaluate retrieval at two granularities: page-level (did we retrieve the right pages?) and document-level (did we retrieve the right documents?). At each level, the core metrics are precision, recall, and F1.
  - Precision measures: of everything we retrieved, what fraction was actually relevant? A retriever that returns 5 pages, 4 of which contain the answer, has a precision of 0.8. High precision means low noise in the context window.
  - Recall measures: of everything that was relevant, what fraction did we find? If 3 pages contain the answer and we retrieved 2 of them, recall is 0.67. High recall means we're not missing important information.
  - F1 is the harmonic mean of precision and recall. It penalizes strategies that trade one for the other and rewards balanced retrieval.
  - Why two granularities matter. Page-level metrics tell you whether you're pulling the right passages. Document-level metrics tell you whether you're pulling from the right sources. A strategy can score high page-level recall (finding many relevant pages) while scoring low document-level precision (those pages are scattered across too many irrelevant documents). As we'll see, the tension between these two levels is one of the main findings.
- Results
  - Recursive splitting wins on accuracy (69%) and page-level retrieval (0.92 F1). The 512-token strategies lead on generation quality, while larger-chunk strategies lead on document-level retrieval but fall behind on accuracy.
  - Finding 1: Recursive and Fixed Splitting Often Outperforms Fancier Strategies
  - Finding 2: The Granularity-Retrieval Tradeoff Is Real
  - Finding 3: Semantic Chunking Collapses at Scale. The fundamental problem: semantic chunking optimizes for retrieval-boundary purity at the expense of context coherence. Each chunk is a "clean" semantic unit, but a single sentence chunk may lack the surrounding context needed for generation.
  - Finding 4: The Page-Level Retrieval Story. Recursive 512 at k=5 hits the best balance: 0.92 page F1 and 0.86 doc F1. 
- My team built Vecta specifically to meet the need for precise RAG evaluation software. It generates synthetic benchmark Q&A pairs across multiple semantic granularities, then measures precision, recall, F1, accuracy, and groundedness against your actual retrieval pipeline.

- You should publish your code to make your findings more credible. Chunking is only one small step in the whole setup and process. Each step will impact the final retrieval. Docs should be cleaned and OCR results should be reviewed since error rate normally is pretty high.
  - You should release the doc sources you have used so other people can validate your claims. There is no worse or better chunks strategy without references to doc type, quality, and relationship. A good chunk method to your doc RAG may be very bad to my.

- These are the most basic ones.. there are way more variant and strategy out there.. For starter checkout the chunking playground Chunker.veristamp.in you can tweak and play all these strategy in browser

- this is an AI slop advertisement
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
# discuss-rerank
- ## 

- ## 

- ## 

- ## [Top Reranker Models: I tested them all so You don't have to : r/LangChain _202512](https://www.reddit.com/r/LangChain/comments/1pnos8a/top_reranker_models_i_tested_them_all_so_you_dont/)
  - I've been working on LLM apps with RAG systems for the past 15 months as a forward deployed engineer. 
  - I've used the following rerank models extensively in production setups: ZeroEntropy's zerank-2, Cohere Rerank 4, Jina Reranker v2, and LangSearch Rerank V1.
  - Rerankers reorder initial retrieval results based on relevance to the query. This improves metrics like NDCG@10 and reduces irrelevant context passed to the LLM.
  - ZeroEntropy zerank-2 emerges as a versatile leader, combining accuracy, affordability, and features like instruction-following for multilingual RAG challenges. Cohere Rerank 4 suits enterprise, Jina v2 real-time, LangSearch V1 free entry.

- Great post but missing Qwen3-0.6B or Jina v3? How's zerank-2 vs bge-v2-gemma on self-host latency?
  - I only focused on what I could test deep, qwen3 lightweight is dope for multi tho. zerank-2 wins on instructions/calibration for me
# discuss-models-for-rag
- ## 

- ## 

- ## [Why does Qwen3-1.7B (and DeepSeek-distill-Qwen-1.5b) collapse with RAG? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1ndj9sf/why_does_qwen317b_and_deepseekdistillqwen15b/)
  - I’ve been running some experiments comparing different LLMs/SLMs on system log classification with Zeroshot, Fewshot, and Retrieval-Augmented Generation (RAG). The results were pretty eye-opening:
  - Qwen3-4B crushed it with RAG, jumping up to ~95% accuracy (from ~56% with Fewshot).
  - Gemma3-1B also looked great, hitting ~85% with RAG.
  - But here’s the weird part: Qwen3-1.7B actually got worse with RAG (28.9%) compared to Fewshot (43%).
  - DeepSeek-R1-Distill-Qwen-1.5B was even stranger — RAG basically tanked it from ~17% down to 3%.
  - I thought maybe it was a retrieval parameter issue, so I ran a top-k sweep (1, 3, 5) with Qwen3-1.7B, but the results were all flat (27–29%). So it doesn’t look like retrieval depth is the culprit.
  - Does anyone know why the smaller Qwen models (and the DeepSeek distill) seem to fall apart with RAG, while the slightly bigger Qwen3-4B model thrives? 

- I have used Qwen 3 1.7B a lot. That model is crazy without hefty task-specific fine tuning. Very chaotic.

- system log classification sounds like a routine task (data should be structured with clear patterns), so I don't expect any decent model to have any problems with this. If they do, then it is likely due to the distilled models being too distilled. I started off with R1-7B and progressed to larger models from there, no point with anything smaller.

- [Why does Qwen3-1.7B (and DeepSeek-distill-Qwen-1.5) collapse with RAG? : r/Qwen_AI](https://www.reddit.com/r/Qwen_AI/comments/1ndj6tp/why_does_qwen317b_and_deepseekdistillqwen15/)
  - Think about how RAG works. You type. What you typed becomes an embedding. The embedding is used as a query to the vector database. The vector database returns results of the query. The combined “you” embedding and documents embedding are fed to the LLM
  - My observation is that context size explodes if the user asks questions that broadly match queries. Most small models are trained with very small context windows. These windows are expanded at inference time using RoPE and YARN. But context aliasing is real and really detrimental to model output quality. The injection of RAG embeddings might be causing context aliasing.
  - Context aliasing due to RoPE stretching is only one facet of the problem but it’s the one I am mildly familiar with.
  - There is also weaker attention resolution, poor fine-tuning for retrieval tasks, and the brittleness of distilled models (emulating behavior without more attention heads being distributed over the context).
  - TL; DR: Your 4B Qwen has enough eyes to read the extra pages. The 1.7B and DeepSeek distill need better page placement and less rumination. It's not "model X bad at RAG" per se. It's about head allocation, positional settings, and prompt hygiene.

- ## [We built a semantic highlighting model for RAG : r/Rag _202601](https://www.reddit.com/r/Rag/comments/1qbjr5n/we_built_a_semantic_highlighting_model_for_rag/)
  - We kept running into this problem: when we retrieve documents in our RAG system, users can't find where the relevant info actually is. Keyword highlighting is useless – if someone searches "iPhone performance" and the text says "A15 Bionic chip, smooth with no lag, " nothing gets highlighted.
- We looked at existing semantic highlighting models:
  - OpenSearch's model: 512 token limit, too small for real docs
  - Provence: English-only
  - XProvence: supports Chinese but performance isn't great + NC license
  - Open Provence: solid but English/Japanese only
- None fit our needs, so we trained our own bilingual (EN/CH) model
  - https://huggingface.co/zilliz/semantic-highlight-bilingual-v1
  - This work draws its core ideas and theoretical underpinnings from Provence (https://arxiv.org/abs/2501.16214), whose seminal research laid the essential groundwork for our exploration.
  - we build entirely upon the exceptional efforts of the Open Provence project
  - We’ve moved to a larger 8k context window model—it’s much more aligned with real-world use cases in RAG/Agent scenarios.

- ## [I thousands of tests on 104 different GGUF's, >10k tokens each, to determine what quants work best on <32GB of VRAM : r/LocalLLM _202506](https://www.reddit.com/r/LocalLLM/comments/1liy7ku/i_thousands_of_tests_on_104_different_ggufs_10k/)
  - The test is a 10, 000-token “needle in a haystack” style search where I purposely introduced a few nonsensical lines of dialog to HG Well’s “The Time Machine” . A small system prompt accompanies this instruction the model to local the nonsensical dialog and repeat it back to me.
  - [I gave the same silly task to ~70 models that fit on 32GB of VRAM - thousands of times (resharing my post from /r/LocalLLM) : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1ljpo64/i_gave_the_same_silly_task_to_70_models_that_fit/)

- Nemotron UltraLong 8B actually works – it reliably outperforms Llama 3.1 8B (which was no slouch) at longer contexts

- Generally LLama 3.1 8B still is a good model. Sadly little too dumb, but handlers context well.
- In my experience (outside of this test, so this is even more-strictly going towards "just vibes") Nemotron Ultralong is cool that you can throw it massive (like, >64k contexts) and it can still extract meaning out of them where most models that size fall flat on their faces. If the context is nowhere near that, however, it's a worse-performing model than Llama 3.1 8b for me.
  - Llama 3.1 8b is extremely interesting as it handles large contexts very well and seems to be the cutoff point for handling this correctly (Q5 failed over and over again, but Q6 succeeded)

- The good thing about Nemotron UltraLong - it really does deliver its context performance. The bad thing - it is dumb and a bit wacky model, seem to treat the prompts very literally.

- ## [I tested local models on 100+ real RAG tasks. Here are the best 1B model picks : r/Rag _202510](https://www.reddit.com/r/Rag/comments/1o60ib6/i_tested_local_models_on_100_real_rag_tasks_here/)
  - A — Find facts + cite sources → Qwen3–1.7B-MLX-8bit
  - B — Compare evidence across files → LMF2–1.2B-MLX
  - C — Build timelines → LMF2–1.2B-MLX
  - D — Summarize documents → Qwen3–1.7B-MLX-8bit & LMF2–1.2B-MLX
  - E — Organize themed collections → stronger models needed

- ## [We built 3B and 8B models that rival GPT-5 at HTML extraction while costing 40-80x less - fully open source : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o8m0ti/we_built_3b_and_8b_models_that_rival_gpt5_at_html/)
  - Our goal was to make a small, fast model for taking HTML from website and extracting JSON that perfectly adheres to a schema.
  - We distilled a frontier model down to 8B params and managed to keep basically all the output quality for this task. Schematron-8B scores 4.64 on LLM-as-a-judge evals vs GPT-4.1's 4.74 and Gemma 3B's 2.24. Schematron-3B scores 4.41 while being even faster.
  - The main benefit of this model is that it costs 40-80x less than GPT-5 at comparable quality (slightly worse than GPT-5, as good as Gemini 2.5 Flash).
  - We fine-tuned `Llama-3.1-8B` , expanded it to a 128K context window, quantized to FP8 without quality loss, and trained until it outputted strict JSON with 100% schema compliance.
  - We also built a smaller 3B variant that's even cheaper and faster, but still maintains most of the accuracy of the 8B variant.
- How does this compare to jinaai/ReaderLMv2 ? I've been using q4 for that for my usecases
  - We haven't benchmarked against it (yet), but it's the most similar model that exists at the moment.

- When you add Schematron + search for the QA benchmark, what do you put for the schema? Do you use one generic schema for all the questions, or generate a custom schema for each question - and if so, what model generates the schema?
  - The schema is generated by the same model that generates the final answer based on the question (without the page as context). In all these cases it’s a GPT model.

- There is no sensible reason one should use model to do this. Both HTML and JSON are structured and parsable.
  - Cheaply being able to reliably gathering structured data from all kinds of different domains without building domain specific scrapers is an incredible feat for LLMs.

- ## [What’s your go-to combo of LLM + embedding model for RAG? : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1pba2lt/whats_your_goto_combo_of_llm_embedding_model_for/)
- Qwen3 8B is the current SOTA for embeddings with a 32k context size, which gives you much more flexibility when chunking text.
  - Gemini 2.5 Flash has very good performance and is really cheap.
  - Once you factor in maintenance costs, potential GPU issues, downtime, etc., it’s almost always better to just use Google’s service — it saves you a ton of headaches and is always online.

- ## [Nvidia releases ultralong-8b model with context lengths from 1, 2 or 4mil : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jzsp5r/nvidia_releases_ultralong8b_model_with_context/)
  - 🐛 超长context，prompt processing速度慢
- What I want to know is... How much VRAM does these kind of context windows take? Is it the same for large and small models? I think i remember reading context vram grows exponentially or quadratic, or have they found more efficient approaches?
  - It's still quadratic. AFAICT the approach here is a YaRN-based rotary positional encoding to make a shorter RoPE-based context stretch further and still stay useful. Roughly. The transformer structure is the same. No free context, sorry. :) For completeness, it is not the same for small and large models, because the cost per token goes up the bigger the model.

- This is how you sell more GPUs. Llama 4 at full context length takes 512 H200s networked. Entirely self serving by NVDA.
- I usually don't have high hopes for models from NVIDIA. their previous research seems to be just show off what you can do with large amount of compute rather than contributing anything SOTA. ofc, to sell more compute.
# discuss-rag-internals
- ## 

- ## 

- ## 

- ## 

- ## [The "Silent Bottleneck" in Production RAG: Why Cosine Similarity Fails at Scale : r/Rag _202602](https://www.reddit.com/r/Rag/comments/1rfinck/the_silent_bottleneck_in_production_rag_why/)
- This is absolutely beginner level RAG and I guarantee you that production systems that only use embedding distance don’t exist or are intended to be simple.

- I think the key takeaway here is that pure cosine similarity almost always hits a wall once you’re beyond toy corpora because it ends up returning the same document or very similar chunks over and over, which fills up your context window with redundant info instead of diverse evidence.
  - That’s why hybrid search (lexical + vectors) or diversity-aware selection strategies like MMR/DF-RAG tend to outperform vanilla RAG at scale; you want relevance and non-redundancy. 
  - If you’ve actually tested this in a production stack and found something better than MMR, it’d be great to hear from Mem0 on what empirically worked
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
