---
title: lib-ai-app-community-chat-office-docs-knowledge-base
tags: [community, documentation, knowledge-base, large-language-model, office]
created: 2025-08-30T18:15:47.850Z
modified: 2025-08-30T18:16:57.201Z
---

# lib-ai-app-community-chat-office-docs-knowledge-base

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 现在RAG+LLM那套太成熟了…亲自体验两百行代码就可以实现一个包括前端在内的定制化Chatbot（比如某个人/某个领域的定制化知识库） _202403
- https://x.com/VoidAsuka/status/1768328842056499654
  - 从完全不懂这一套的小白程序员从开发到部署两小时就能搞定，反而还是爬数据、洗数据花的时间更多…果然数据是新时代的黄金
  - Langchain + Streamlit 几百行搞定
- 不是成熟，是本来就简单吧, 不用langchain不差哪里的，只是他更全
  - 简单就是成熟的体现之一啊
- 搭起来很简单，做到效果好很难，做一套评测标准也很难
- 就是chatbot这个形态有点不三不四

# discuss-local/llama/models
- ## 

- ## 

- ## 

- ## 

- ## [Which LLM to chat with your documents? (and restrict knowledge to documents) : r/ollama _202506](https://www.reddit.com/r/ollama/comments/1lo78f4/which_llm_to_chat_with_your_documents_and/)
- Have you tried increasing the context window? I've seen lots of hallucinating when the context is too small for the prompt + document. 
  - You'll need to increase the `num_ctx` value, either globally for a model or per chat in Open-WebUI. 
  - IIRC the default is 2048 for Open-WebUI and Ollama models usually have a default of 4096. 
  - I've used QWEN3 and Gemma3 for conversation with documents and for docs less than three page, I usually go with 12288 and for larger ones I go with 32768, which were both selected arbitrarily. 
  - Definitely depends on the model's available context size and your GPU's vRAM.

- You can create a custom solution by generating vector embeddings from your documents and storing them in a vector database. Then, retrieve relevant embeddings based on your query and use them as context. 
  - Alternatively, you can use Google NotebookLM.

- Qwen3-30B-A3B. It’s excellent at this, and blazing fast. Very good scores on the hallucination leaderboard, also.

- Restricting an LLM to just your docs (and avoiding outside hallucinations) is one of the hardest open problems.
  - context size and prompt tricks help a bit, but there are about 16 recurring failure modes that keep leaking outside knowledge or blending in hallucinated facts.

- ## [How do I make chatting about documents not suck? : r/ollama _202502](https://www.reddit.com/r/ollama/comments/1ik3m98/how_do_i_make_chatting_about_documents_not_suck/)
  - The various models I've tried mostly fail miserably, often telling me the information I'm looking for is not in the document (it is) or returning incomplete information.

- You need RAG for such a lengthy context. You can always continuously scale up resources to unlock larger and larger context windows. The issue will be computing those tokens while overloading the output. For example llama3.2 has a max context of 128K tokens, that probably still isnt enough for 40 pages of content!
  - It makes much more sense to chunk, vectorized and then on query rerank the releavnt snippets of text and inject only partial content into the window. You can do this "full text comprehension" on large context models like Claude and Gemini because they are backed by GPU's you could never afford, but local is a whole different approach.
  - There are hundreds of locally running apps with built in RAG, agents, vectordb, etc etc to handle all of this for you. Popular apps are AnythingLLM Desktop, OpenWebUI, and JanAi to name a few.
  - Tools like Ollama or LMStudio are for running models and pulling them in. They lack a lot of the tooling you require here to get good results with just an LLM alone.

- You can fine-tine with unsloth with a dataset that matches your use case. Makes it quite a bit smarter.

- use ollama's --verbose flag when loading the model and it will show tokens when you paste the doc into the chat and run inference

- A typical page might contain around 300 to 400 words, and each word on average is about 1.5 tokens. So, a rough estimate would be: • 300 to 400 words per page • 1.5 tokens per word
  - This is: • 450 to 600 tokens per page
  - So 40 pages: • 18, 000 to 24, 000 tokens.
  - So, 40 pages would fit into a context of 128, 000 tokens.
  - You must have a different problem

- For insurance-related extra large files (like the entire policies), I had to use Claude projects feature, which worked out great.
- Try Claude. It's supposed to handle 200k tokens.

- ## [Which web based solutions are best to chat with documents? : r/ollama _202410](https://www.reddit.com/r/ollama/comments/1fxocll/which_web_based_solutions_are_best_to_chat_with/)
- OpenWebUI can do it, and so far it's the most reliable way I tried.
  - I've tried lots of models, embedding models, reranking, chunk sizes, and tons of prompts in Open WebUI. I cannot get any combo to only provide exact quotes or have the right page numbers for a book of about 200 pages. Am I just missing something?
- at 200 pages you aren't speaking to documents, you are actually speaking with books, which is different level of complexity.
  - First of all if you're using Ollama - I'd recommend to increase the context window, and stick with models which has fairly big context windows like phi3.5-medium-128k
  - Also keep in mind that ollama by default limits context window to 2k, so you will need to adjust your models and provide `num_ctx` parameter to match the desired context size.
  - Then try to increase chunk sizes so whenever your RAG provides context from the vector database that would be enough context for LLM model to analyse and do additional search.
  - But I agree with you modern solutions are still rather context limited so you cannot speak to a book easily.

- Embedding splits docs onto chunks. You're no longer 'chatting' with the entire document. Relevant parts are retrieved instead, based on your prompt, and the LLM generates a response based on retrieved context.
  - Ollama doesn't (yet) quantize the cache. So 12gb of VRAM won't hold much context at all. Run 8b quantized in Ollama and you should be able to get 4k context or so?
  - While 128k context sounds wonderful if you have the VRAM for it, the accuracy really suffers at that size

- ## [Retrieval Augmented Generation optimised Llm's : r/LocalLLaMA _202308](https://www.reddit.com/r/LocalLLaMA/comments/15ttegi/retrieval_augmented_generation_optimised_llms/)
  - It's super excited to show you newly published DocsGPT llm’s on Hugging Fac
- Are you considering releasing the dataset too?
  - Absolutely, just want to clean up few things around it and add more of the just summarisation tasks that are important for “map reduce”

- Do you have any plans for training these for 8k/16k context? Context size has been the biggest hurdle for me so far using RAG.
  - Yep, my only worry is the way llms “forget” about the middle context, but I think if we create synthetic dataset, and hide useful information randomly amongst useless context, it might work very well
- That's an interesting idea

- We will soon publish a 3b, high context model, still in the middle of making sure it works well.
# discuss-ai-pdf
- ## 

- ## 

- ## 

- ## [Is there a model that actually can examine and read all of a pdf? : r/ollama _202502](https://www.reddit.com/r/ollama/comments/1ipw9og/is_there_a_model_that_actually_can_examine_and/)
- No model can "read" the pdf - what you need to do is RAG. This is what happens when you upload a file to chatgpt for example.
  - And depending on the size of the pdf you might need to chunk it and iterate over that. What you are doing is creating embeddings and a vectorDB of those embeddings representing the various dimensions.
  - Also if it is a technical doc with nested tables etc then you would need to think about other techniques to OCR it - and as others suggested a multi-modal model might be easier but more expensive.

- Convert each page of the PDF to a png file and have the vision model do the work

- The only reliable AI I use for this purpose is notebookLM by Google.

- For an LLM to read a PDF, it needs to be converted to text first. Most local models have a small context window, so it won't fit the whole contents of a long PDF. You could try to split the contents and summarize it by parts that fit into the context window.

- ## I have a script that splits all the pages of a PDF, calls OpenAI for OCR into Markdown, and assembles the output. 
- https://x.com/ccorcos/status/1878308491158589820
  - https://github.com/ccorcos/ask-pdf/blob/master/src/pdf2md
  - PDFs are a pain. The format is optimized for printing, not for machine readability. 
  - The best and most general solution I’ve found is just to use GPT as OCR.

- What about tesseract?
  - Tried it. Not very good
  - Aside from doing a poor job recognizing text, it doesn’t do any high level structural arrangement of the only markdown. You’d have to do that yourself. 

- which model of gpt you use as ocr?
  - OpenAI GPT4o-mini
# discuss-ai-excel/spreadsheet
- ## 

- ## 

- ## 

- ## 
# discuss-ai-docs
- ## 

- ## 

- ## 

- ## [Show HN: DocsGPT, open-source documentation assistant, fully aware of libraries | Hacker News _202302](https://news.ycombinator.com/item?id=34648266)
- It's like the new crud but instead of designing the database tables and columns you're tweaking the prompts.
  - I know its crazy, there are also some other promts that I have not edited from LangChain that actually run in the background

- This is really the quality of projects we're upvoting? This is a python script that calls another API.
  - I agree, the code is pretty average, inconsistently using quotation marks, looks copy pasted and developer comments trying to understand what they're doing. 
  - The concept isn't too novel either, LLM usage in knowledge base querying is nothing new, I know some lawyers looking into it for regulatory compliance.

- So just so I understand- this is all based on taking input from the user, injecting it in a template prompt that instructs chatgpt to answer the question based on providing it all the source material? What happened to building your own models to run offline?
  - A trained AI model is a platform that you can build applications on. Pretty sure >90% of the developers in this space will be building applications, not models. 
  - Kinda like how the vast majority of mobile developers build mobile apps, not mobile operating systems. True, this particular application is pretty simple, but early applications are.

- All you need is to 1. convert documents to embeddings (OpenAI or some other local library for this), 2. store all embeddings in an index like (SaaS like Pinecone or FAISS locally), 3. run query against embeddings. Just a document search is likely good enough, but if not you can use a completion algorithm in a simple LLM of the docs to generate answers.

- ## 🚀 [DocsGPT, open-source documentation assistant, fully aware of libraries : r/Python _202302](https://www.reddit.com/r/Python/comments/10th3lq/docsgpt_opensource_documentation_assistant_fully/)
- Neat project, and to answer some of the earlier comments, this is not just a chatgpt clone, there are other mechanisms involved to enhance the responses and give them a context. 

# discuss-ai-knowledgebase
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🤔 一些企业描述为知识库的需求，实际上是没有办法通过当前的 RAG 来满足的，更像是一个本地的 Deepresearch 或者其他的 agent 可以 cover 的场景。 不要被带到坑里。
- https://x.com/YinsenHo_/status/1954741140307235282
- 根据我的日常经验。企业其实更倾向于半自动。通过AI大模型快速找到相关的几个类，最后汇总一下。由于审核的存在，根本无法做到全自动

# discuss-etl
- ## 

- ## 

- ## 

- ## 

- ## Excited to share Latticework, a text-editing environment aimed to help synthesize freeform, unstructured documents _202408
- https://x.com/andy_matuschak/status/1828928979656683581 
  - It aims to help with making sense of messy piles of unstructured documents. 
  - The key idea is unifying annotation (direct reaction in context) w/ freeform text-editing (for fluid sensemaking).
- sorry, the PDF story doesn’t really exist in this prototype, but I think the design applies without alteration—just need someone to build it

- https://x.com/MatthewWSiu/status/1828929032718872734
- I explored some closely related ideas with @MagicPaperAI . You guys have pulled off the synthesis of highlights and copied fragments. I’d posit that the next key synthesis is between copied fragments and revisions of a document. Edits are partial copies.
- Great work! I like the flow of adding & organizing snippets -> augmented synthesis. The more snippets you grab under a heading, the clearer a cluster forms. That then generates 'what you're getting at' summaries & gives AI bounds to forage for related snippets. Good loop there.

- ## 🆚️ 这几天在给公司产品的 AI 助手选择知识库的数据处理工具，重新看了一遍 Marker、MinerU、Docling、Markitdown、Llamaparse 这五个工具
- https://x.com/shao__meng/status/1893984985998365096
1. Marker
技术架构
· 基于 PyMuPDF 和 Tesseract OCR，支持 GPU 加速（Surya OCR 引擎），开源轻量化
功能特性
· 专注 PDF 转 Markdown，支持公式转 LaTeX、图片内嵌保存，OCR 识别扫描版 PDF
· 多语言文档处理，但表格转换易错位，复杂公式识别精度一般
适用场景
· 科研文献、书籍等基础 PDF 转换需求，适合技术背景用户快速部署
优劣势
✅ 开源免费、处理速度快（比同类快 4 倍）
❌ 缺乏复杂布局解析能力，依赖本地 GPU 资源

1. MinerU
技术架构
· 集成 LayoutLMv3、YOLOv8 等模型，支持多模态解析（表格/公式/图像），依赖 Docker 和 CUDA 环境
功能特性
· 精准提取 PDF 正文（自动过滤页眉/页脚），支持 EPUB/MOBI/DOCX 转 Markdown 或 JSON
· 多语言 OCR（84 种语言），内置 UniMERNet 模型优化公式识别
适用场景
· 学术文献管理、财务报表解析等需高精度结构化的场景
优劣势
✅ 企业级安全合规，支持 API 和图形界面
❌ 依赖 GPU，表格处理速度较慢，配置复杂

2. Docling
技术架构
· 模块化设计，集成 Unstructured、LayoutParser 等库，支持本地化处理
功能特性
· 解析 PDF/DOCX/PPTX 等格式，保留阅读顺序和表格结构，支持 OCR 和 LangChain 集成。
· 输出 Markdown 或 JSON，适合构建 RAG 知识库
适用场景
· 企业合同解析、报告自动化，需结合 AI 框架的复杂应用
优劣势
✅ 与 IBM 生态兼容，支持多格式混合处理
❌ 需 CUDA 环境，部分功能依赖商业模型

3. Markitdown
技术架构
· 微软开源项目，集成 GPT-4 等模型实现 AI 增强处理，支持多格式转换
功能特性
· 支持 Word/Excel/PPT、图像（OCR）、音频（语音转录）转 Markdown，批量处理 ZIP 文件
· 可生成图片描述（需 OpenAI API），但 PDF 格式转换易丢失结构
适用场景
· 多格式混合内容创作，如 PPT 图表转文档、音视频转录
优劣势
✅ 格式支持最全，开发者友好（Python API/CLI）
❌ 依赖外部 API，部分功能需付费模型

4. Llamaparse
技术架构
· 专为 RAG 设计，结合 Azure OpenAI 和 KDB AI 向量数据库，优化语义检索
功能特性
· 解析含表格/图表的复杂 PDF，输出 Markdown/LaTeX/Mermaid 图表
· 支持生成知识图谱，企业级安全合规
适用场景
· 法律文档分析、技术手册问答等需结合 LLM 的智能应用
优劣势
✅ 解析精度高，支持半结构化数据语义优化
❌ 处理速度慢，免费额度有限，需 API 密钥

选型决策树 
需求优先级：
速度与轻量 → Marker
精度与多模态 → MinerU
企业级集成 → Docling/Llamaparse
多格式混合 → Markitdown

技术适配：
需 GPU 加速 → MinerU/Docling
需 API 扩展 → Markitdown/Llamaparse
需本地隐私 → Stirling-PDF（补充推荐）

成本考量：
免费开源 → Marker/MinerU
商业支持 → Llamaparse

- 我这里10000 页以上的企业级应用的方案可以分享下，我这个是经验累计下来的结果。这 10000 页解析都做过了人工校验，可以说市面上大部分方案都测试过了。最佳实践结论如下：
- PDF： 
  1. 离线（复杂）场景：MinerU + VLM识别 + LLM修复
  2. 离线（简单）场景：Marker 
  3. 在线（通用）：Llamaparse OR VLM
  [VLM 离线用 Qwen2.5 / VL 在线 gemini 2.0 flash]

- 根据我之前的调研，感觉目前还没有完美的支持多类型文档多模态的解析库。速度，准确性，成本三角里，最均衡的个人觉得反而是楼上有人说到的大模型多模态解析能力
  - 速度-准确性-成本三角，确实很重要，看需求中哪个角更看重了。
  - 多模态解析这种方式挺不错，我们也放在对比中，特别是 gemini 这种成本低多模态能力强的。

- 多模态解析这种方式挺不错，我们也放在对比中，特别是 gemini 这种成本低多模态能力强的。

- Docling也有点慢... 没有GPU加速的其他库也不快... 平均下来都是 1.x page/s , 比如MinerU一个20页的paper, 一个GPU L4, 最快也要十几秒 到生产环境不开多GPU并发, 时间上是个大问题, 
# discuss
- ## 

- ## 

- ## [LLM to query large documents (or sets of documents) : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1ci8868/llm_to_query_large_documents_or_sets_of_documents/)
- First  go through the documents to index them using some vector DB.  Not just stuffing them into the DB, but extracting all useful knowledge from them. An entry for each fact. If the doc is too big, read it in chunks and use additional summaristion queries. 
  - Link the knowledge to the documents. Then, when querying, query the DB and get the matching docs.

- is it possible to do this quickly with langchain / rag framework ? which one did u use ?
  - Depends. It's <50 lines of code in python/JS and most of it is just boilerplate that can be generated with llama. I don't use any frameworks, just code it myself. Don't see any benefits in using langchain.
