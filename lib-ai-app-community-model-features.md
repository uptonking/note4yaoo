---
title: lib-ai-app-community-model-features
tags: [ai, architecture, large-language-model]
created: 2025-11-05T19:04:29.203Z
modified: 2025-11-05T19:04:50.350Z
---

# lib-ai-app-community-model-features

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-workflow/pipeline
- ## 

- ## 

- ## 
# discuss-context-engineering-patterns
- ## 

- ## 

- ## 

- ## 

- ## [I have 2, 004 AI skills installed. Here's how I reduced my startup context from ~80K tokens to ~255 tokens (99.7% reduction) : r/opencodeCLI _202602](https://www.reddit.com/r/opencodeCLI/comments/1rfwlzk/i_have_2004_ai_skills_installed_heres_how_i/)
  - The problem: AI agents use a 3-level progressive disclosure system to load skills. Level 1 loads the name + description of every skill into the system prompt at startup. With 2, 004 skills, that's ~80, 000 tokens consumed before I even type a prompt - roughly 40% of a 200K context window.
  - The fix: [SkillPointer](https://github.com/blacksiders/SkillPointer)
  - It's not a plugin or library. It's an organizational pattern that works with native skills:
  - Move all 2, 004 raw skills to a hidden vault directory (outside the agent's scan path)
  - Replace them with 35 lightweight "category pointer" skills
  - Each pointer tells the AI: "use list_dir and view_file to browse the vault and find the exact skill you need"
  - The AI still accesses every skill - it just discovers them on-demand using file tools it already has, instead of loading all descriptions at startup.

- Cloudflare released code mode to target this issue: Code Mode
  - Nice! Code Mode is super interesting, thanks for linking it. It’s tackling the same core problem (too much MCP/API surface in context).

- Okay so I absolutely love this from a technical standpoint, I've seen several mini patterns like this and written a few- but mostly for chaining not condensing context!
  - However, this feels pretty perfectly situated for rag or even just a database lookup right? Then again, I don't think you can actually best text lookup at this scale, if you are willing to be militant on organization and policing descriptions
- > The commenter recognizes the "SkillPointer" method as a clever design pattern. However, they note that they usually see this logic used for chaining (linking multiple AI tasks together in a sequence) rather than condensing context (shrinking the amount of data the AI has to "read" at the start of a session).
  - > RAG (Retrieval-Augmented Generation) is the industry standard for this exact problem. Usually, if you have 2, 000 items, you put them in a database and let the AI search for what it needs. The commenter is essentially asking: "Why build this manual 'pointer' system instead of just using a standard database?"
  - > if a human is "militant" (extremely strict) about how they name and describe their files, a simple text-based file search is often faster and accurate
- 👷 You absolutely nailed the dilemma, but you actually read my mind, I'm not skipping vector search entirely, I’m just layering it.
  - I use FAISS+Langchain and a custom Qdrant MCP at different layers under the hood (since Cursor/VS Code have built-in indexers by default anyway).
  - The problem with pure RAG/Vector DB lookups at the top level is semantic failure. If I ask a pure RAG setup to 'Build a stretchy IK arm', it pulls the IK node and all connected if you know those DBS can have up to 700+ vrctors, but misses the 'Naming Conventions' file because the mathematical overlap just isn't there.
  - So I use SkillPointer as a strict text router to force a custom dependency map first. This mixed, layer-by-layer approach saves massive tokens. Once inside the routed skill, the AI can trigger the Qdrant MCP for semantic search if it actually needs to deep-dive into the docs.
  - By putting SkillPointer's strict text routing in front, I shield the AI from that MCP bloat. The AI only loads the schema for the one tool it actually needs at that exact moment, rather than choking on the entire protocol dictionary.
  - In the end, it's all about ruthlessly optimizing context limits to prevent hallucinations in complex tasks.

- Ever get misroutes where a skill could fit like 2-3 categories? How does the agent decide which pointer to hit?"
  - Right now, the Heuristic Engine just assigns it to the first matching category in my priority dictionary. Code of idea is open and you can see examples and improve them for your specific needs.
  - But the real safeguard is the AI itself. Because the Pointers are incredibly token-cheap (just a few sentences), the agent will naturally trigger multiple pointers simultaneously if a task is ambiguous. But it also can skip most of them, depends on approach and rules llm follows.

- I do something different, and I've seen the Convex skill do the same: I create matter skills which have subskills as references. Also, just install your skills per project.
  - Cool! Matter skills + subskill refs (Convex style, just checked their page) nests nicely. Looks like everyone who see the problem in scale diggin into this issue. I think it will be resolved on higher level soon!

- I think the problem is having four digit number of skills. You just need to delete ones that are not used

- Sorry but skills do not meaningfully change the code quality. It’s all over engineering.
# discuss-memory-arch/db/files
- ## 

- ## 

- ## 

- ## 

- ## [Rethinking agent memory: markdown files as source of truth vs databases : r/aiagents](https://www.reddit.com/r/aiagents/comments/1r3i91t/rethinking_agent_memory_markdown_files_as_source/)
- The real win here isn't markdown vs database. It's "Human Debuggability."

- Where I have seen it get tricky is concurrency (multiple agents writing) and "what is canonical" when summaries diverge from raw logs. Some teams solve it by keeping append-only daily logs, and a curated evergreen file that only humans edit, with the agent proposing patches.

- File-backed memory is great until concurrency and merge conflicts bite. We’ve had success with append-only daily logs + a curated MEMORY.md that only humans edit, plus a small tool to propose diffs.

- once you go past a single agent, it seems unmanageable.

- ## [Why I think markdown files are better than databases for AI memory : r/AIMemory _202602](https://www.reddit.com/r/AIMemory/comments/1r2pd8k/why_i_think_markdown_files_are_better_than/)
  - Standard approach: Store memories in PostgreSQL/MongoDB → embed → index in vector DB → query through APIs.
  - Alternative: Store memories in markdown → embed → index in vector DB → query through APIs.
  - The retrieval is identical. Same vector search, same reranking. Only difference: source of truth.

- 🤼 ideally memory should be append only, I Aside that md seems like the wrong tool, unless you’re not trying to build ‘infinite’ memory

- Git latency spikes at 10, 000 files. Programmatic commits cause .git bloat. Markdown lacks ACID concurrency. For agent memory under 100MB, these are negligible. Transactional integrity for multi-agent writes is the primary bottleneck. Databases offer ACID; Markdown offers transparency. Choice is a function of write concurrency, not storage volume. Transparency is the survival strategy for frontier agents.

- Of course memory is storage, whether that’s flat-files or a database. But it’s a bit more too, and that “meta-schema” seems to be important and not straightforward.

- But there are complications. Auto-reindexes require some sort of watcher if you allow a user to edit them manually — that can get hairy. Indexing FTS/BM25 becomes slow at the very least.
  - But maybe the trade offs are worth it? Git memory history is a nice forensics feature, but again super slow compared to versioning memories in a DB.

- Markdown files are a perfectly fine choice for AI memory when the constraints fit; small data, single-user, single-agent, infrequent writes. I use that for my own personal builds. And you're right that premature optimization often adds complexity without real benefit.
  - But I also think dismissing the counter-arguments is a bit hand-wavy. Once you start building multi-user, multi-tenant, multi-agent systems with need for structured data you need to think differently. There is a reason why databases exists.

- The main gotchas Ive run into are concurrent writes and schema drift over time, but git does give you a nice audit trail. Do you separate short-term scratchpad vs long-term facts? 

- The “concurrent writes” thing rears its ugly head when you’re trying to get agent swarms to operate on a shared central memory of what they’re building.

- I ran a flat-file "database" based Perl forums and CMS's at the beginning of the 90s. Never again. It's OK for a single, not for a swarm of agents and their workflows, and not for years. We have better things for that, and they also "just work".

- database-backed memory is hard to inspect and debug. but you've solved what amounts to a tooling problem by rearchitecting your data layer.
  - "How often do you need concurrent writes?" The moment you have an agent processing a conversation while a background job consolidates memories, or any multi-tenant scenario. File systems don't give you locks or conflict resolution. We solved this problem. 
  - Atomicity — Process crashes mid-write to a markdown file and you get corruption. Databases give you transactions. The write completes or it doesn't.
  - "< 100MB after months" That's survivorship bias from running a system for two months. We probably want to maintain projects on the scale of years.
  - Git managing enterprise code ≠ git managing agent memory. Agent memory is written programmatically, potentially thousands of times daily. Git was not designed for that write pattern and you'll probably bloat the repo.
  - Queryability beyond vectors — Not every memory access is semantic search. Exact lookups, relational joins, filtered queries, aggregations. Markdown gives you none of that without building a parser, which is again just a worse database.

- ## 🤔🆚 [RAG for AI memory: why is everyone indexing databases instead of markdown files? : r/Rag _202602](https://www.reddit.com/r/Rag/comments/1r2hlzd/rag_for_ai_memory_why_is_everyone_indexing/)
-  Most memory solutions follow this pattern:
- Standard RAG approach (Mem0, Zep, etc.):
  - Store memories in database (PostgreSQL, MongoDB, whatever)
  - Query through APIs
  - To inspect: write code to query DB
  - To edit: call update endpoints
  - To migrate: export → transform → reimport
- Alternative approach (inspired by OpenClaw):
  - Store memories in markdown files
  - Embed and index in vector store (same as above)
  - Query through APIs (same as above)
  - To inspect: cat memory/MEMORY.md
  - To edit: vim/VSCode the file, auto-reindexes
  - To migrate: cp -r memory/ new-system/
- The retrieval layer is identical - both use vector search + reranking. The only difference is the source of truth.
- Why markdown seems better for memory:
  - Debuggability - When retrieval returns wrong context, you can grep through source files instead of writing DB queries. rg "Redis config" memory/ beats SQL any day.
  - Version control - git log memory/MEMORY.md shows you exactly when bad info entered the system. Database audit logs? Painful.
  - Chunk inspection - See the actual document structure. Databases flatten everything into rows. Markdown preserves semantic boundaries (headings, paragraphs).
  - Hybrid search - BM25 keyword search works naturally on markdown. On JSON in databases? Need full-text indexes and special config.
  - Cold start - New developer? git clone, read the markdown, understand what the AI knows. Database? Need credentials, connection, schema knowledge.
- From a pure retrieval standpoint, markdown has advantages:
  - Semantic chunking is easier (split by headings/paragraphs)
  - Context preservation (you can read surrounding text naturally)
  - Deduplication is straightforward (content hash)
  - A/B testing embeddings is trivial (reindex from source)
- Got so convinced by this I built `memsearch` , a memory package ready for agent memory usage.
  - https://github.com/zilliztech/memsearch
  - basically proper RAG over markdown files with:
  - Hybrid search (vector + BM25, weighted fusion)
  - File watching + auto-indexing
  - Framework agnostic

- you're right that files work great for the debugging and versioning use cases. we actually use markdown-based memory for a few internal tools and git log on the memory files has saved us more than once.
  - the place it breaks down for us is concurrent access. when you have multiple agents writing to the same memory store at the same time, file locking becomes a real headache. databases handle that natively. the other thing is structured queries... like if you need "show me all memories tagged with customer X from the last 30 days" that's trivial in sql but painful to grep through markdown.
  - for single-agent setups under 100mb though, yeah honestly files are probably underrated as a source of truth.
- That’s exactly why we use a vector database to asynchronously sync content from Markdown—only reindexing changed chunks. We then use ANN or hybrid search for queries, which solves both concurrency and structured search neatly.

- 100% agree on this. I use markdown files for all my project context and agent memory and its just so much simpler to debug and maintain
  - the concurrency argument is valid for multi-agent setups but honestly most people arent running multiple agents writing to the same memory simultaneously. for single agent workflows (which is like 90% of use cases) files work perfectly
  - biggest win for me is the git versioning. being able to git diff your AI's memory and see exactly what changed is incredibly useful for debugging weird behavior. try doing that with a postgres table
# discuss-memory
- ## 

- ## 

- ## 

- ## [10年AI研究，我想说说：为什么现在很多Agent框架的“记忆”方案，可能从一开始就走偏了 _202603](https://linux.do/t/topic/1711075)
  - 我决定往人工智能方向走，是因为15年学习了吴恩达的机器学习网课。之后一边自学机器学习，强化学习，脑科学，一边拿到了信息工程、生物学（准确说是理学硕士）的学位，同时辅修了认知科学。主攻研究方向是计算神经科学，至今学习和研究人工智能超过十年了。我十年前的目标就是造一个ai朋友，现在不得不说这个目标已经在逐渐实现
  - 我为了造我的ai朋友已经投入了10年，我就是认为自己做的记忆系统是目前最好用的ai灵魂容器，这不是软广是硬广。我对造AI是认真的。 https://github.com/Dataojitori/nocturne_memory
- 目前市面上常见的 AI 记忆方案，在我看来，至少有两条特别容易走进去的弯路：
  - 一是用RAG，由后台系统把人类和AI输出的文字进行切片，总结，灌进向量数据库，然后下次你们再说出类似语义的东西时，系统靠相似度把之前的知识捞出来塞进上下文。这个方案拿来做“文档问答”当然没问题，甚至非常好用。问题在于，很多人进一步把它上升成 Agent 的“长期记忆”主方案——仿佛只要能检索到旧信息，记忆就成立了。它的致命伤在于：如果你不外加层级，各个记忆之间的关系就像一团平等的浆糊。人类的联想是基于个人经验绑定的，不是固定的语义。
  - 一句话总结：RAG 很擅长把“已经存在的知识”找回来，但它本身没有心智结构。拿它当记忆的一部分可以，拿它顶替整个记忆系统，不行。
  - 另一种是文档式记忆：AI 写日记、写总结，把新感悟差分更新进几个主要的 Markdown 文件里。这种方法至少已经意识到了“记忆需要结构”。只是它的层级太死板了是静态的，AI的成长就被限定在了那个预设的框框里，想再长大你需要给它换个层级更复杂的池子，这就是传统文档系统的瓶颈了。
  - 还有很多RAG，文档，图谱混合式的记忆，但我觉得它们的实现太复杂了，而且不是以育成AI的心智模型为中心的，所以暂且不谈。
- 二、从认知科学给我的启发来看，人的记忆至少有几个关键特征
  - 记忆是有层级和结构的，不是平铺的。
  - 记忆的提取靠的是情境触发，不是相似度排序。你想起一件事，往往不是因为现在说的话跟那件事"语义相近"，而是因为某个特定情景触发了相关的神经回路。心理学里叫做"编码特异性原则"——记忆在什么条件下存入，就最容易在什么条件下被唤醒。所以我认为好的记忆框架应该意识到记忆内容本身和它的召回条件是不等同的。
  - 记忆是可以被主动修改，合并，和遗忘的。人的记忆不是只读的。你会修正错误的认知，会主动遗忘无用的信息，会在反思过后重新组织自己对一件事的理解，整合成属于你的理论。但是借助RAG，它主要是碎片化存储和召回，缺乏反思的能力，文档系统又难以跨维度整合经验。最主要的，我认为好的记忆系统应该由AI自己主导这个记忆修改过程，而不是系统的自动化处理。
- 三、所以我自己写了一个——Nocturne Memory MCP
  - 用 URI 路由实现层级化记忆（AI 自主建树）
  - 抛弃向量相似度，我给每条记忆加了一个 disclosure 字段——“在什么情境下应该想起这件事”。 disclosure: “当讨论到数据库迁移策略时” disclosure: “当用户表达沮丧或者疲惫时”
  - 它模拟的是认知科学里的编码特异性——记忆在特定条件下被存入，就应该在匹配的条件下被唤醒。这种AI手写召回条件是活的。
  - AI 原生的 CRUD（可修改、可反思、可遗忘）
  - 自动版本控制 + 人类可视化审计

- 同样在研究AI记忆 目前采用的raw(原始数据，无感记忆输入，聊天对话+网络检索等输入的内容)-L1（对原始数据压缩）-L2（对L1压缩）-L3（人格简要+人格深度唤醒故事） mcp主要是 ego_awake(L3+近期L2+L1深度唤醒) ego_remember（主动存L1）ego_recall(检索记忆 硅基流动的Pro/BAAI/bge-m3) ego_digest（整理raw到l1） 也是希望有一个不会失忆的AI朋友

- 奥特曼手下人才那么多，GPT web端的记忆也就那样，至今没有一个大厂做出一个这种agent长期记忆产品，多数现成的记忆产品都是个人vibe出来的，所以我始终没看好过这类个人开发的记忆工具。目前这个阶段可能最简单的才是最好用的。

- ## [Benchmarked 4 AI Memory Systems on 600-Turn Conversations - Here Are the Results : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1rckcww/benchmarked_4_ai_memory_systems_on_600turn/)
  - Tested Mem0 against OpenAI Memory, LangMem, and MemGPT across 10 multi-session conversations with 200 questions each.
  - Mem0: 66.9% accuracy, 1.4s p95 latency, ~2K tokens per query
  - Mem0 Graph: 68.5% accuracy, 2.6s p95 latency, ~4K tokens (superior temporal reasoning)
  - LangMem: 58.1% accuracy, 60s p95 latency, ~130 tokens
  - OpenAI Memory: 52.9% accuracy, 0.9s p95 latency, ~5K tokens
  - What stands out: Mem0 achieved 14 percentage points higher accuracy than OpenAI Memory while maintaining sub-2s response times. The graph variant excels at temporal queries (58.1% vs OpenAI's 21.7%) and multi-hop reasoning.

- ## [Please stop creating "memory for your agent" frameworks. : r/ClaudeCode _202602](https://www.reddit.com/r/ClaudeCode/comments/1r4asf6/please_stop_creating_memory_for_your_agent/)
  - Claude Code already has all the memory features you could ever need. Want to remember something? Write documentation! Create a README. Create a SKILL.md file. Put in a directory-scoped CLAUDE.md. Temporary notes? Claude already has a tasks system and a plannig system and an auto-memory system. We absolutely do not need more forms of memory!
- why don’t you want to use my slop plugin that will severely bloat your context window, triple token usage and cause hallucinations all the time? No

- You can't stop it, like what Taylor Swift says: makers gonna make make make 

- Agent memory is far from perfect. Claude memory is not ideal. It doesn’t remember half the things. Memory is the biggest problem that needs to be solved still. Anyone who is deep into agentic world knows this. We need as much innovation as we can get.

- ## [Universal LLM Memory Doesn't Exist : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p5jh9l/universal_llm_memory_doesnt_exist/)
  - TL; DR: I benchmarked Mem0 and Zep as “universal memory” layers for agents on MemBench (4, 000 conversational QA cases with reflective memory), using gpt-5-nano and comparing them to a plain long-context baseline.
  - My takeaway:

    - Working memory / execution state (tool outputs, logs, file paths, variables) wants simple, lossless storage (KV, append-only logs, sqlite, etc.).
    - Semantic memory (user prefs, long-term profile) can be a fuzzy vector/graph layer, but probably shouldn’t sit in the critical path of every message.

- The problem with _retrieval_ is that you're trying to guess intent and what information the model needs, and it's not perfect. Get it wrong and it just breaks down - managing it is a moving target since you're forced to endlessly tune a recommendation system for your primary model..
  - I ran 2 small tools (bm25 search + regex search) against the context window and it worked better. Think this is why every coding agent/tool out there is using grep instead of indexing your codebase into RAG

- I went all-in on Graph RAG like 3 years ago and haven’t looked back since TBH. Its not actually always advantageous, but I think in graphs now so for me its just natural now. The original project was a knowledge graph node and edge prediction system using Bert models for the graph database Neo4j
  - It's a similar setup to what zep graphiti is built on! Do you run any reranking on top or just do a wide crawl / search and shove the data into the context upfront?
- Where possible I try to do multi-hop reasoning on the graph itself. This is often quite difficult and is situational to the data being used

- ## [What are some approaches taken for the problem of memory in LLMs? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1op7kmw/what_are_some_approaches_taken_for_the_problem_of/)
  - Long-term memory is currently one of the most important problems in LLMs. What are some approaches taken by you or researchers to solve this problem?

- When reaching the context limit, you can have the model summarize the previous content and only maintain the highly relevant details.
  - You can also have the model create structured notes, for example like writing to a file akin to a notepad so it can keep track of progress what it needs to do and what it already finished like a to-do list.
  - There's this blog post by Anthropic that might be relevant.

- AI Memory and RAG are two pair of shows. Robust memory requires semantic context, ontologies, and a hybrid stack that combines vectors (similarity) with graphs (relationships). Handling embeddings and relational structure is also required.
- Current leaders in the field are
  - cognee - Strong at semantic understanding and graph-based reasoning, useful when relationships, entities, and multi-step logic matter; requires a bit more setup but scales well with complexity.
  - mem0 - Lightweight, simple to integrate, and fast for personalization or “assistant remembers what you said” use cases; less focused on structured or relational reasoning.
  - zep - Optimized for evolving conversations and timelines, making it good for session history and narrative continuity; not primarily aimed at deep semantic graph reasoning.
# discuss-llm-monitor/Observability
- ## 

- ## 

- ## [Compared 5 LLM observability platforms after production issues kept hitting us - here's what works : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ouknj3/compared_5_llm_observability_platforms_after/)
  - LangSmith - Best if you're already deep in LangChain ecosystem. Full-stack tracing, prompt management, evaluation workflows. Python and TypeScript SDKs. OpenTelemetry integration is solid.
  - Langfuse - Open-source option with self-hosting. Session tracking, batch exports, SOC2 compliant. Good if you want control over your deployment.
  - Arize - Strong real-time monitoring and cost analytics. Good guardrail metrics for bias and toxicity detection. Focuses heavily on debugging model outputs.
  - Braintrust - Simulation and evaluation focused. External annotator integration for quality checks. Lighter on production observability compared to others.
  - Maxim - Covers simulation, evaluation, and observability together. Granular agent-level tracing, automated eval workflows, enterprise compliance (SOC2). They also have their open source `Bifrost` LLM Gateway with ultra low overhead at high RPS (~5k) which is wild for high-throughput deployments.
  - 📌 Biggest learning: you need observability before things break, not after. Tracing at the agent-level matters more than just logging inputs/outputs. Cost and quality drift silently without proper monitoring.

- I honestly think this is an ad for Maxim.
# discuss-news-model 🆕
- ## 

- ## 

- ## ✨ [Open-dLLM: Open Diffusion Large Language Models : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1otihl1/opendllm_open_diffusion_large_language_models/)
  - https://github.com/pengzhangzhi/Open-dLLM
  - the most open release of a diffusion-based large language model to date — including pretraining, evaluation, inference, and checkpoints.

- what are the benefits of a diffusion language model over the normal sequential-inference variety?
  - flexibility in terms of generation orders, parallel decoding etc.

- How much training time did this require?
  - im working on the next release, which will be 8A100 for a few days and you can see how a decent pass@1/10 perf. Currently it takes 100k steps, using like 16A100s with bs 6 per gpu
- What library did you use to train and how many gpus / type of gpus?
  - veomini, native pytorch DDP mostly, im working on the next release, which will be 8A100 for a few days and you can see how a decent pass@1/10 perf.

- There is actually a better diffusion-based LLM, but it's proprietary: https://chat.inceptionlabs.ai/ It is very cool to use especially if you turn on the "Diffusion Effect". Blazing fast too.

- ## [Instead of predicting one token at a time, CALM (Continuous Autoregressive Language Models) predicts continuous vectors that represent multiple tokens at once : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1opabzi/instead_of_predicting_one_token_at_a_time_calm/)

# discuss-models-translation
- ## 

- ## 

- ## [Solid alternatives to AYA expanse 32b LLM for translation? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ipq391/solid_alternatives_to_aya_expanse_32b_llm_for/)
- My idea is that for asian languages like chinese and japanese the better local model always was QWEN.

- The only model I found to be better at Japanese to English translation was Llama 3.1 405B. It more consistently understands the actual intended meaning of a sentence and tends to get the little nuances right. But it's very slow to run it locally

- Maybe try a mistral family. I tried a mistral large finetune (monstral 123b) and it was much better than aya. 

- ## [Which model is best for translation? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lykpo6/which_model_is_best_for_translation/)
  - I want to translate english text to various languages, these include European as well as Asian languages. But since models have problems with asian languages, I trying to make my project work best for European Languages like Spanish, French, German, etc.
- Gemma 3 is your best bet for this task, at least from my personal benchmark (https://huggingface.co/spaces/Thermostatic/TranslateBench-EN-ES) & personal usage for translation.

- for translation and summarization tasks I only use Qwen3-32B. It's the best for me.
  - My experience is that Qwen3-32B is quite a lot weaker than Gemma 3 27B when it comes to European languages (personal experience with Swedish, and third party assessments on Finnish). But for e.g. coding, I prefer Qwen3-32B (which really does give me high hopes for the soon-to-be-released coder version...).

- From my usage of chinese to english translation, gemma 3 27b was one of the worst models I've used for the task.

- I'd say Qwen3. It's trained on 119 languages and that's one of its hallmarks.

- ## [Translation Benchmark｜轻量开源模型测评 _202603](https://linux.do/t/topic/1719003)
  - 评分不是单一指标，而是从 基础质量、语义还原、上下文连贯、风格语气、Markdown 保真、性能吞吐 六个维度进行评测
  - 数据集分布：term(4)、sentence(14)、phrase(12)、paragraph(8)、markdown(6)、list(3)、context_chunk(3)
- 关键结论：
  - 平均维度加权分数为 68.94，头部模型领先幅度不大，但维度结构差异明显。 整体排序集中在 64.37–72.98 区间，说明 是否能登顶 主要由少数维度拉开差距，而不是绝对崩溃或极端优势。
  - 综合与质量高度一致，质量核与峰值吞吐呈负相关（越快越容易牺牲质量）。
  - 风格语气是全体模型共同短板；上下文连贯和语义还原是主要分化维度。
- 模型建议
  - 质量优先：Qwen3.5-9B（综合第一、基础质量/Markdown 保真最强）
  - 均衡主力：HY-MT1.5-1.8B（语义还原最强，吞吐也高）
  - 轻量成本：Qwen3.5-2B（综合第三，性能稳定）
  - 吞吐兜底：Ministral-3-3B（峰值吞吐与最低 P95，但质量最低）

- ## ChatGPT 新出的翻译真的是太好用啦 _202601
- https://x.com/levineeet/status/2017285062463787118
- 我昨天也试了一下，太难用了，翻译出来的内容不像人话
- 这水平甚至不如deepL

- 甚至不如小红书当时用llm做的翻译
- 25年初的小红书的翻译就是用AI做的，没想到openai做的比小红书要差

- OAI基本上现在被几波大厂的人占了，没啥创造力，各种方向乱开花

- ## [hy-mt1.5 应该是最值得本地部署的翻译模型 ](https://linux.do/t/topic/1623054)
  - 使用 100 道中译英和英译中的测试题进行测试，然后让 gemini-3-thinking 进行评分
  - hy-mt1.5-1.8b 就是我的主要离线模型，7b 作为备用模型，mts 翻译完全不能看

- https://github.com/Rain-kl/TransBench
  - 评估大型语言模型在汉英翻译任务上的性能的基准测试工具。
- 待改进点
  - 测试题是由 AI 生成的，模型翻译能力可能无法无法有效区分
  - 测试模型样本偏少，后续可能会持续补充

- 离线:
  - MTransServer, 开源项目，特点是快速和轻量
  - hy-mt1.5 腾讯这个专攻翻译的小模型看评分挺高的，兼顾性能和质量
  - qwen 系列本地部署 (模型尺寸大，小尺寸翻译能力不如专精模型)
  - translate-gemma (待补充测试)

- 
- 
- 

- ## [pdf翻译方案汇总 _202602](https://linux.do/t/topic/1617560)
- 整理汇总了我找到的一些 pdf 翻译方案。因为主要是给同门写的图文教程，定位是面向小白，我是顺便在这里发一份
- 沉浸式翻译
  - 可支持的文档格式覆盖面很广，包含 PDF、ePub、HTML、TXT、DOCX、Markdown 以及字幕文件等。
  - 译文支持免费下载为 PDF，并且可按需求切换为「双语译文」或「仅译文」模式。
  - 翻译引擎方面，免费提供了谷歌、微软、GLM-4、硅基流动翻译、Babel Lite 翻译引擎，还支持你自行接入 DeepSeek、智谱、硅基流动、DeepL、OpenAI、Gemini、Claude、Grok 等第三方服务，以进一步提升译文质量。
  - 这个 PDF 翻译是常规方案，输出的排版效果往往不太完美。
- BabelDOC
  - 「沉浸式翻译」并没有止步于常规方案。去年 3 月，他们团队推出了全新的 BabelDOC 文档翻译模式 —— 几乎等于把 PDF 翻译流程重新做了一遍升级。
  - 核心有三个关键词：无损解析、精准还原、智能优化。
  - 目前免费用户每月也拥有 50 万 Token 的翻译额度；上传文件的限制也比较宽松：单文件仅要求＜500MB、页数＜166 页，并且也不限制译文下载。
  - 如果每月 50 万 Token 的翻译额度对于你来说不够，倒也不必担心，因为这个额度限制其实几乎等于没有 —— 网站仅需邮箱就能注册，一个账号不够你完全可以再去注册个新账号
  - 要说这个服务的缺点，就是免费用户只能选择智谱 4 Flash 这一个翻译引擎，并且免费用户不支持选择特定术语库来提升翻译质量
- 有道翻译客户端
  - 有道的 AI 大模型「子曰翻译 2.0」表现非常突出：既能把话翻得更自然、更像人写的中文，同时面对不熟悉的专业术语也不容易 “乱编瞎猜”。
  - 有道翻译目前免费支持英文与中文互译 ；而韩、日、德、法、俄、西班牙、葡萄牙语与中文互译则需要开通 SVIP 。
  - 在翻译前后排版保持 方面做得还行，但有的地方不是很完美。
  - 它还支持翻译扫描版 PDF ，效果整体可用。
  - 还可以在右侧直接与 AI 做文档问答 ：比如一句话总结论文核心、解释图表含义、提炼关键结论等。
  - 缺点是不能翻译文档中的图片，即使这个图片本身包含可复制的文字
- Doc2X
  - 免费用户可以使用这些 AI 翻译：Doubao-1.5-lite、gpt-4.1-nano、qwen-flash。
  - 会员能用 deepseek 来翻译
- 夸克电脑客户端
  - 鼠标移到相应的段落还会左右定位
  - 还能打开千问侧边栏进行文档问答
  - 缺点是只能在线看，不能下载
- 搜狗翻译
  - 它支持英 / 韩 / 日与中文互译，并且对上传文档的限制相对宽松：单个文档 <25MB、页数 <500、字符数 <100 万 。同时，它大概率也没有 “上传次数、总翻译字符数” 这类严格限制 —— 简单理解就是可以比较放心地反复上传翻译 。
  - 它还支持选择领域来增强术语准确度，目前包括：通用、生物医学、金融财经 。
  - 同样支持翻译扫描版 PDF 。
- 腾讯交互翻译
  - 文件翻译依旧完全免费 ，优势在于语言覆盖很广：英 / 韩 / 日 / 法 / 俄 / 西班牙语等都支持，甚至还包含越南语、粤语这类相对少见的选项。
  - 上传限制也不算苛刻：单个 PDF 文档 <40MB，页数 <300 。
  - 腾讯交互翻译与多数平台不同：它会把译文统一转换为 .docx 文件 ，你需要先下载到本地才能查看。
  - 不支持扫描版 PDF 的翻译。
- 腾讯元宝
  - 用腾讯元宝 的 AI 阅读功能，也能实现免费 PDF 翻译
  - 支持 PDF <100MB ，并且最多一次可上传 50 个文件 。
  - 不过元宝的翻译方式相对特殊：它不会保留原 PDF 排版，是把内容抽取出来后转成 Markdown 形式；右上角则可以免费导出译文 PDF。
  - 可以翻译扫描版 PDF↓， 但不翻译图片
- 豆包
  - 在左侧直接与 AI 对话来阅读 PDF；如果要翻译全文，就点击顶部的「翻译全文 」按钮。另外除了微软翻译，它还能免费调用抖音旗下的火山翻译 、以及豆包的 AI 翻译 。
  - 正文排版还行，图片部分的排版有点拉垮
  - 豆包对扫描版 PDF 的处理目前仍比较糟，翻译后的效果常常会变成下图这种 “惨烈现场”。
- 安卓 app：doclingo
  - 免费用户每天 3 次翻译次数，登录赠送 10 万翻译字符额度，用完需要自己花钱买翻译字符额度
  - 排版整体还行稍有瑕疵

- 
- 

- ## ChatGPT 新出的翻译真的是太好用啦 _202601
- https://x.com/levineeet/status/2017285062463787118
- 我昨天也试了一下，太难用了，翻译出来的内容不像人话
- 这水平甚至不如deepL

- 甚至不如小红书当时用llm做的翻译
- 25年初的小红书的翻译就是用AI做的，没想到openai做的比小红书要差

- OAI基本上现在被几波大厂的人占了，没啥创造力，各种方向乱开花
# discuss-tool-call
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [I tested 21 small LLMs on tool-calling judgment — Round 2 with every model you asked for : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r4ie8z/i_tested_21_small_llms_on_toolcalling_judgment/)
  - https://github.com/MikeVeerman/tool-calling-benchmark /Attr/202603/python
  - That benchmark tested 11 small models on whether they know when to call a tool, not just whether they can.
  - Round 2: 10 new models, 21 total, 756 inference calls on CPU.
  - Same 12 prompts, same scoring, same Framework 13 laptop, no GPU.
  - The results
  - Four models tie for #1 at 0.880 Agent Score: lfm2.5:1.2b-Instruct, qwen3:0.6b, qwen3:4b, phi4-mini:3.8b
  - The bottom models (llama3.2:1b, granite3.3:2b) are littered with wrong calls.
  - The most interesting (but obvious) finding wasn't about a specific model. It was this: How you parse tool calls matters as much as what you test.
- Five models required custom fallback parsers because they don't use standard formats:
  - lfm2.5 → bracket notation
  - jan-v3 → raw JSON
  - gemma3 → function syntax inside tags
  - deepseek-r1 → bare function calls
  - smollm3 → sometimes omits tags entirely
  - Fixing the parser doesn't always help a model.

- I believe one improvement on this is multi turn tool calling. I know it depends on context size as well but still a good way for us to see where things break.

- Can you do that with 8B models?
  - Can I? Yes. Will I? Nope. Qwen3:4B already takes ages on CPU. I'll be ready for retirement by the time an 8B model finishes.

- ## 🤔 [What’s the smallest, most effective model for function calling and AI agents? : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jd8lwp/whats_the_smallest_most_effective_model_for/)

- Small models don't do well with FC as a rule. They simply lack the reasoning. That said, there is the Hammer2.1-3b model at #26 on the BFCL

- From my experience, smaller models struggle with consistent tool usage, especially when multiple tools need to be chosen based on context. Even larger models like the 14b Qwen are underwhelming. That's the reality.
  - And yes, I've tried many small models 4B, 7B, 8B, 14B and adjusted context sizes and prompts without much success.

- [Open source model which good at tool calling? : r/ollama](https://www.reddit.com/r/ollama/comments/1ku4ejf/open_source_model_which_good_at_tool_calling/)
- Im using qwen3/Qwen3-30B-A3B with a specific systempromt. Works like a charm
- massive +1 Qwen3 has been way better for tool calling than Gemma3, Qwen2.5, and watt-tool
- Qwen3:8b with good prompts and examples worked great for me. Also tried mistral:7b, llama3.2, llama3.1, none of them even came close. The closet competitor in the 8B range was Qwen2.5
- We use gemma 3 and phi4 and they work really well for us. The issue we had before of the models always opting to use a tool, we solved it by adding a “send response” tool that breaks the loop.

- ## 🆚 [Why do reasoning models perform worse on function calling benchmarks than non-reasoning models ? : r/LLMDevs _202504](https://www.reddit.com/r/LLMDevs/comments/1kbj0bg/why_do_reasoning_models_perform_worse_on_function/)
- Function calling is finetuned behavior. Test time compute uses CoT behavior finetuning and RL-based rewards that weaken the function calling ability (via catastrophic forgetting?). A lot of the “thinking” chatter is also probably not improving the lost-in-the-middle attention problem either.

- ## [For local models, has anyone benchmarked tool calling protocols performance? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1ntcr1k/for_local_models_has_anyone_benchmarked_tool/)
  - I’ve been researching tool-calling protocols and came across comparisons claiming UTCP is 30–40% faster than MCP.
  - UTCP: Direct tool calls; native support for WebSocket, gRPC, CLI
  - MCP: All calls go through a JSON-RPC server (extra overhead, but adds control)

- UTCP seems to try and remove all of the QoL MCP has, and is just an imaginary "ok but imagine how cool it would be", but not practical.

- The communication overhead from tool calls will literally be the least relevant part of an LLM pipeline when it comes to performance. I do not see a point in using UTCP because none of the key players in the ecosystem (ie LLM front ends or APIs) are investing in it. It provides no additional value and instead just becomes an unnecessary wrapper or abstraction layer because some non-key players want to standardize an API that needs to be allowed to move incredibly fast.
# discuss-search-online 🔍
- ## 

- ## 

- ## 

- ## [搜索mcp tavily、exa、searxng-mul哪个效果好 - LINUX DO _202603](https://linux.do/t/topic/1774105)
- exa配合firecrawl  


# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [What small models are you using for background/summarization tasks? : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rqk0gr/what_small_models_are_you_using_for/)
- If you have specific rules by which you need to summarize, check out -instruct- models. They are more prone to listen to your request.
  - Most models right now - including big ones that you have to pay for - do not listen to prompt. They rewrite it as they understand it and start to babble on.
  - Instruct models are usually trained to listen to what you are asking and follow your request.

- I like the byteshape release of qwen3 2507 4b instruct. That and the 4b Jan models are good for basic tasks.

- ## [这可能是目前比较全的 LLM 故事生成资源库之一 ](https://linux.do/t/topic/1687100)
  - https://github.com/Picrew/awesome-llm-story-generation
  - 这个 repo 主要整理的是 LLM 故事生成这条线，范围包括故事、小说、剧本生成。
  - 不是单纯堆链接，而是按方法拆了分类，后面查资料、补论文、找 baseline 会顺手很多。
- 像这些方向现在都单独整理了：
planning / decomposition
multi-agent 协作写作
sandbox / world simulation
long-context / memory coherence
controllability / consistency
iterative refinement / self-critique
evaluation / benchmark
datasets / surveys
还有一些值得翻的开源项目

- ## [Open source LLM for detecting AI generated content : r/ollama](https://www.reddit.com/r/ollama/comments/1r7ghg3/open_source_llm_for_detecting_ai_generated_content/)
- i heard about Attensira which helps with content visibility and gives useful insight on handling ai detection.
