---
title: lib-ai-app-community-chat-office-docs-knowledge-base
tags: [community, documentation, knowledge-base, large-language-model, office]
created: 2025-08-30T18:15:47.850Z
modified: 2025-08-30T18:16:57.201Z
---

# lib-ai-app-community-chat-office-docs-knowledge-base

# guide

- kb-patterns
  - 对通用的知识库的需求，类似于需要一个通用的搜索引擎，很难做好
  - 本地知识库 + 在线搜索 能减少幻觉、紧急结合本地
  - 基于文档和基于数据库的知识库在实现层面区别不大, 都需要chunking+embedding+vector-search, 难点都是更新问题

- pm-kb
  - 🛢️ 数据源: local-files, web-search, external-personal-apps(gmail, slack, office, notion, github)
    - 同时支持3种数据源的产品很少
    - 可优先集成主流产品如notion/obsidian
    - ⛓️ 还要支持 search with citation
  - doc search + source(wikipedia/books/journals)
  - 通用的聊天系统在处理大文档/ocr的能力方面性能差
  - image-gen/editing: 还原低质量绘本
  - image rag + search
# discuss-stars
- ## 

- ## 

- ## 

- ## 📌 现在大模型一天一个样，一直在思考 LlM 应用中哪些是不变的，梳理了一下 RAG 中那些值得投入的技术栈 _202503
- https://x.com/ZeroZ_JQ/status/1906255737845690372
  - 文档解析： unstructed-io，docling，MinerU
  - 数据层：qdrant
  - 搜索引擎：meilisearch
  - 流处理：kafka，flink
  - 工作流：airflow，prefect
  - 搞定数据，搞定 RAG
- 还有文件存储比如 cos，另外我觉得 kafka 可以换成 pulsa

- unstructed-io一般，hires解析太慢，语义切片开源版不支持

- ## 现在RAG+LLM那套太成熟了…亲自体验两百行代码就可以实现一个包括前端在内的定制化Chatbot（比如某个人/某个领域的定制化知识库） _202403
- https://x.com/VoidAsuka/status/1768328842056499654
  - 从完全不懂这一套的小白程序员从开发到部署两小时就能搞定，反而还是爬数据、洗数据花的时间更多…果然数据是新时代的黄金
  - Langchain + Streamlit 几百行搞定
- 不是成熟，是本来就简单吧, 不用langchain不差哪里的，只是他更全
  - 简单就是成熟的体现之一啊
- 搭起来很简单，做到效果好很难，做一套评测标准也很难
- 就是chatbot这个形态有点不三不四

# discuss-local/llama
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

- ## [Show HN: RedactMyPDF.com - AI-assisted PDF redaction with human review | Hacker News](https://news.ycombinator.com/item?id=44930853)
  - uses AI (Gemini) + OCR + human review to make redaction fast but safe
  - Works on scanned PDFs (OCR with Tesseract)

- ## [Ask HN: I have many PDFs – what is the best local way to leverage AI for search? | Hacker News _202405](https://news.ycombinator.com/item?id=40528192)
- RAG cli from llamaindex, allow you to do it 100% locally when used with ollama or llamacpp instead of OpenAI.

- Paperless supports OCR + full text indexing

- The primary challenge is not just about harnessing AI for search; it's about preparing complex documents of various formats, structures, designs, scans, multi-layout tables, and even poorly captured images for LLM consumption. This is a crucial issue.
  - To parse PDFs for RAG applications, you'll need tools like LLMwhisperer or unstructured.io.

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

- ## [Kotaemon: An open-source RAG-based tool for chatting with your documents | Hacker News _202501](https://news.ycombinator.com/item?id=42571272)
- At this point there are multiple home RAG systems, pretty much using the same components, so does anyone know how this compares to others? I see that it imports GraphRAG which most other don’t
  - I think a lot of AI chat services have recognized that document search is table stakes and are building this functionality into their tools, so I don't know whether Kotaemon as a standalone tool will be needed for much longer.
  - For example, my company was originally going to push out Kotaemon for private document search, but we have now put that on pause because we're exploring whether we can get the same results through our primary AI chat service, without having to point users to a separate tool.

- How well do these kind of pre built systems work? RAG in my experience usually requires a decent amount of customization to your input data for chunk formatting and other things to work well, are these systems flexible enough? What if you want to integrate it into an existing system, are these for local use only? So everyone on e.g. a team has to set it up themselves?
  - For longer documents or for groups of documents you need a kind of search to extract the most relevant passages to throw in the context.

- ## DocsGPT is an open-source document Q&A system by Arc53, built on RAG _202508
- https://x.com/andrea_89757/status/1954192824540467256
  - RAG = split your docs → store in a vector DB → retrieve relevant chunks → feed to an LLM.
  - You get precise answers with citations, not AI guesses.

- What it can read
• Text: PDF, DOCX, TXT, Markdown, HTML
• Spreadsheets: CSV, XLSX
• Slides: PPTX
• Code & sites: GitHub repos, Sitemaps, scraped pages
• OCR: images → searchable text

- Data sources
• Local folders
• URLs
• GitHub / GitLab
• Reddit threads
• APIs

- Smart retrieval + answers
• Searches your own data first
• Returns answers with references (file + section)
• Adjustable search scope & answer length

- Model support
• Cloud LLMs: OpenAI, Claude, Gemini
• Local LLMs: LLaMA, Mistral, Ollama
Switch anytime for cost, speed, or privacy.

- Integrations
• Web chat UI (ChatGPT-style)
• Embed as website widget (customer support)
• Slack / Discord / Telegram bots
• API endpoints for your own apps

- Why it’s useful
• Enterprise search: Find answers in 1, 000+ pages instantly
• Dev/API docs: “How do I use this endpoint?” without scrolling
• Customer support: AI answers from your FAQ & manuals
• Legal/compliance: Search laws/contracts and get exact citations

- Deploy your way
• Hosted version (fast start)
• Local/private via Docker or manual setup
• Hybrid: local retrieval + cloud LLM

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

- ## [Designing NotebookLM | Hacker News _202509](https://news.ycombinator.com/item?id=45315312)
- This post has the same issues as NotebookLM for me -- overdesigned, overengineered for what at its core is a simple and valuable UX.
  - NotebookLM: obviously useful, but I just wanna select some files and chat w/ them or have them summarized for me. It's got low info density, way too many cards/buttons/sections/icons, and it makes the core UX really difficult for me to navigate.

- Took me ages to figure out you can copy paste simple text. Editing any text isn't great either.

- What do you use it for? Aside from audio overviews, what does it do better for you compared to vanilla chat interfaces or docs integration?
  - I am a post sales consultant. Meaning I’m the first deeply technical person that a client talks to after they sign the contract that pre-sales has worked on. Pre-sales has already had a couple of meetings by the time it gets to me. I put the transcripts of their calls and the contract (statement of work) into Notebook LLM to ask the high level questions like the objectives, the challenges, priorities, risks they have already surfaced etc. After my set of discovery sessions, I put those transcripts into the notebook too. I can then use Notebook LLM to give me a first draft of the management style assessment report
- I use it for asking questions about a specific board games. It is INVALUABLE for learning very complex games. Instead of hunting through a rulebook trying to find an obscure rule, I just ask it and it answers, citing where it finds it.
- Video explainers, for me, are better than the audio overviews.
- NotebookLM gives you sources across powerpoints, pdfs, etc.
- I like the mindmap tool

- When working with documents, the citations that NotebookLM provide increase the confidence in answers. This allows to use NotebookLM for team-level knowledge bases.

- ## [Best LLM or program for large amounts of document parsing (read + write) : r/LocalLLM _202501](https://www.reddit.com/r/LocalLLM/comments/1i32o6j/best_llm_or_program_for_large_amounts_of_document/)
- Ive been working on similar projects, and my workflow for efficiency has been to use vLLMs (colpali/byaldi) for quick embeddings or pypdf4llm for md files. My next steps are querying, generating relevant metadata & summaries to make it more cohesive for llm (so basically in the same boat as you - posting for updates to see how people are tackling this).

- From what you described I think an LLM is overkill. Topic classification and summarization can be done with models specific to those tasks.
  - What you are looking for is zero-shot classification. Hugging face has models you can run locally. The only caveat is that you need to be able to define the categories before hand. The benefit is that you can also save a “confidence score” or how closely the text matches the topics.
  - Summarization has a problem as well. Your summarization is only as good as the prompt and model. And for small models like Llama 8b, I have found that even a “good” prompt can still return some garbage.

- ## [AI and Knowledge Base? : r/CustomerSuccess _202507](https://www.reddit.com/r/CustomerSuccess/comments/1lp13br/ai_and_knowledge_base/)
- Results can be great but what I’ve seen is fully dependent on how good the knowledge is and if you can get the AI any other relevant data (order tracking info, scheduling services, product catalogues). Otherwise it’s garbage in/garbage out.
  - Upvoting this. We built an agent for internal knowledge base for retail operations (to speed up onboarding and FAQ), totally dependent on quality of the underlying KB.
- Most modern AI support agent solutions supports tool use, so you should be able to plug in Shopify, Calcom, Paddle, etc. to get that information at the time the chatbot requires it.

- how to make sure the KB is kept up to date / high quality?
  - Data stewardship (as a function) for key knowledge items/domains. The most difficult part is to find a person who will take the topic of knowledge accuracy and completeness seriously, borderline personally.
- We have success metrics we can review by topic area and can drill in to review convos to see which KBs or data was leveraged. Helps in reviewing unsuccessful conversations and finding opportunities to improve or add knowledge.

- I think this is table stakes in customer support these days. People should at a minimum be able to "speak" to the KB. But yes, garbage in, garbage out. From what I've seen of people's KBs, they are outdated and often times inaccurate. If I were to start an AI program from scratch, this is where I would start.

- From my personally experience, incredibly shitty and frustrating as a customer (ATT, xcel, and Allstate).
  - Internally, we use notepad so we can minimize pinging product/engineering for questions. It requires a decent amount of maintenance to stay accurate.
  - The only roi I could see from these tools is keeping overhead down by having less support reps.

- Definitely using AI with KBs is common now. Tools like SiteSpeak, Intercom or even custom RAG setups can power chatbots and speed up support.
  - It's all going to depend on what data and how much you are able to get into the chatbot to use as context. 
  - With the larger context windows of newer LLMs it becomes easy to feed a lot of data in and get pretty good results.

- ## [How would I build a highly specific knowledge base resource? : r/AI_Agents _202502](https://www.reddit.com/r/AI_Agents/comments/1ig7251/how_would_i_build_a_highly_specific_knowledge/)
- RAG is your best solution, and then a data pipeline to update your vector db

- Id suggest chunked and heavily tagged content, use a retrieval agent for the actual lookup, another agent to actually decide what content should get returned, and your final (original) agent delivering that back to the user.
  - If you keep the bots focused on a single task it's often more reliable and if you are dealing with data that requires precision answers (all or nothing, where partial data is bad data) a rag isn't going to perform how you would like, hence my suggestion for tagged and chunked into sections content.
  - A search ends up getting related tags, then uses a second step to get data tied to that tag, then a bot that decides on the best answer(s), finally providing multiple choices narrowed down to the original bot that makes its own judgement call and returns the answer.
  - To me the RAG approach you see all over is overblown and not as practical in practice when it comes to specific data vs broad market knowledge.

- ## 🤔 [How useful are llm's as knowledge bases? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kderkz/how_useful_are_llms_as_knowledge_bases/)
- They are not very useful, really. Use RAG and web search with it and all of a sudden it's a different story.
  - they can be really useful. But the answers needs to be validated after the fact. Often I ask them to answer based on their own knowledge and understanding of a subject, and then I ask them to google it to verify what they said is factually correct and correct any inaccuracies.

- LLMs strictly speaking do not have "knowledge", they represent (with loss) a large amount of textual information from multiple sources, some which are considered by most human as knowledge, others of questionable reliability.
  - LLMs are great as a fuzzy index to massive amounts of information, once you get a results you need to cross check with actual sources. That is why cross checking (even of automatically, using the LLM) with actual full documents you get better results. After that, only human review, and even with humans you can get different interpretations or hallucinations

- ## 📌 [Top AI Knowledge Management Tools : r/PKMS _202505](https://www.reddit.com/r/PKMS/comments/1km72fp/top_ai_knowledge_management_tools/)
- https://textcortex.com is also a good European solution for AI knowledge management

- [Top AI knowledge management tools : r/PromptEngineering _202508](https://www.reddit.com/r/PromptEngineering/comments/1mqvte7/top_ai_knowledge_management_tools/)
- If your knowledge base lives in PDFs, emails, and scattered notes, most tools on this list hit limits.. file sizes, online access, or rigid formats. 
  - A local-first Mac setup elephas that I use avoids that. You just drop your files into a folder and they become instantly searchable, summarized, or explorable without opening a browser.

- Recently tried NotebookLM for summarise few videos to give insights. It’s does good job and also give brain map also.

- I’d also add EZFolders - it’s more focused on document structuring and folder generation than traditional PKM, but it saves a ton of time if you’re building organized knowledge spaces. Instead of manually creating hierarchies, you can either paste a list, upload a CSV, or even chat with AI to generate a clean folder structure in seconds. Super handy if you want your knowledge base files to stay audit-ready and easy to navigate.

- ## [What are the best self-hosted or open-source knowledge base solutions you've used (or recommend) for internal documentation or customer support? : r/selfhosted _202506](https://www.reddit.com/r/selfhosted/comments/1l6zr1a/what_are_the_best_selfhosted_or_opensource/)
  - Good category management
  - Role-based access control
  - Customizable design
  - Search-friendly structure
  - Easy setup and maintenance

- there really is nothing that rivals Dokuwiki. The base template looks old, kinda bad, but it has that “fast” look to it. 
  - Plaintext based, lightning fast (about 1000 pages, about 700 media files, about 17 gigabyte). Plugins are good, stable.
  - I’ve tried migrating so many times but I have found nothing that I can deploy as quickly tha Dokuwiki. Backup is a breeze. Restoring is a breeze.
  - It is all about the content not the tool.

- I used Notion but miss the self-hosted possibility and offline use (maybe it is now available).
  - I used Obsidian and kinda love it but miss an easy way to share a page and maybe collaborate without extra cost. The edition experience on mobile was not what I liked.
  - I used Outline but got issues using from work because the websocket was blocked by my employer. It also does not have a mobile app and is "online only". It is otherwise pretty good.
  - Affine is self-hosted, with a web front-end but also native apps working offline and syncing in the background, collaboration, multi user with easy way to share online or export. It has all and mobile app are in beta (hopefully coming soon). It seems that even tablet+pencil works nicely with it. This is the best obsidian-outline I found.

- We’re using bookstack internally for all our company documents. We’re fairly proficient in markdown so that was a plus. Prior to that we used dokuwiki for years, but found documentation and some pages could end up lost or even duplicated with a couple of us not finding the right pages.

- Outline is the best that i've seen for internal documentation. Have it integrated with my Authentik setup for role based access control.
  - For "customer" documentation, it has the ability to create links to pages and to set a tree as "public". 
  - The downside is there isn't a great way to give users an easy web accessible URL like "wiki.domain.com", so i've instead built a 301 to point the "wiki.domain.com" to the "docs.domain.com/s/wiki".

- I currently use Obsidian...it's wonderful for local notes. tons of plug-ins too.
  - in the past, I've used bookstack and it was fine, nothing special just worked.
  - but here's my hot take: don't self host your documentation/knowledge base tool. If you're ever needing to fix/recover your homelab setup and your docs are on that homelab setup, you're in trouble

- ## [Ask HN: Local RAG with private knowledge base | Hacker News _202410](https://news.ycombinator.com/item?id=41968366)
- The key to accuracy is use case specific knowledge graphs. 
  - Here is a YouTube video of how to do it. https://youtu.be/iWtF1Qe7QkM 
  - The key benefits are 

    - Improved data quality of the data available for genAI 
    - Reduction in risk associated with genAI’s known problems 
    - Increasing business value due to being able to hit use case driven accuracy/reliability, security, and transparency metrics

- > expected the more documents we feed the lower the accuracy
  - The LLM itself is the least important bit as long as it’s serviceable.
  - Depending on your goal you need to have a specific RAG strategy.
  - How are you breaking up the documents? Are the documents consistently formatted to make breaking them up uniform? Do you need to do some preprocessing to make them uniform?
  - When you retrieve documents how many do you stuff into your prompt as context?
  - Do you stuff the same top N chunks from a single prompt or do you have a tailored prompt chain retrieving different resourced based on the prompt and desired output?
- Wouldn't these questions be answered by the RAG solution the OP is asking for?
  - Not really you need to try different strategies for different use cases in my experience.

- Fascinating there doesn't seem to be a consensus "just use this" answer here.
  - My sentiments exactly, and given how widespread a need RAG is, I'm extremely surprised that we don't have something solid and clearly a leader in the space yet. We don't even seem to have two or three! It's "pick one of these million side-projects".
- Because RAGs are simply a list of vectors and a similarity search with some variations trying to use  knowledge graphs. 
  - So everybody is roughly using the same method with some tweaks here and there and thus getting a similar quality in results.
- Getting it running is pretty easy, but actually tuning the results to make them better is tricky, especially if you're not a domain expert in the area you're working on.
  - Evals seem like a solution, but they're very tied to specific examples, so it looks like that might be most of the issue in getting this to work, as with a good set of evals, one can actually measure performance and test out different approaches.
  - Embedding also seems to be a bit of a dark art in that every tutorial uses something small, but I haven't seen a lot of work on comparing the performance of particular embeddings for domain specific tasks.
- This was our experience trying to deploy a knowledge base for our Org.
  - You have to get the domain experts to help you build evals and you need a good pipeline for testing the LLM against those as you make changes. We were never able to get there before the project was killed.

- Just remember that retrieval is the real bottleneck in RAG, so your problem could very much be related to how you create and embed your chunks and not the model you’re using

- I would look at articles on building an open source RAG pipeline. Generation (model) is the last in a series of important steps -- you have options to choose from (retrieval, storage, etc) in each component step. Those decisions will affect the accuracy you mention.
  - Langchain, llamaindex have good resources on building such a pipeline the last I checked

- ## 🤔 一些企业描述为知识库的需求，实际上是没有办法通过当前的 RAG 来满足的，更像是一个本地的 Deepresearch 或者其他的 agent 可以 cover 的场景。 不要被带到坑里。
- https://x.com/YinsenHo_/status/1954741140307235282
- 根据我的日常经验。企业其实更倾向于半自动。通过AI大模型快速找到相关的几个类，最后汇总一下。由于审核的存在，根本无法做到全自动

# discuss-etl
- ## 

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

- ## 🆚️📄 这几天在给公司产品的 AI 助手选择知识库的数据处理工具，重新看了一遍 Marker、MinerU、Docling、Markitdown、Llamaparse 这五个工具 _202502
- https://x.com/shao__meng/status/1893984985998365096
1. Marker /GPLv3
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

1. MinerU /AGPLv3
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

1. Docling /MIT
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

1. Markitdown /MIT
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

1. Llamaparse /CloudOnly/NonOpen
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
- EXCEL: 使用某开源项目修改

- 根据我之前的调研，感觉目前还没有完美的支持多类型文档多模态的解析库。速度，准确性，成本三角里，最均衡的个人觉得反而是楼上有人说到的大模型多模态解析能力
  - 速度-准确性-成本三角，确实很重要，看需求中哪个角更看重了。
  - 多模态解析这种方式挺不错，我们也放在对比中，特别是 gemini 这种成本低多模态能力强的。
- 多模态解析这种方式挺不错，我们也放在对比中，特别是 gemini 这种成本低多模态能力强的。

- Docling也有点慢... 没有GPU加速的其他库也不快... 平均下来都是 1.x page/s , 比如MinerU一个20页的paper, 一个GPU L4, 最快也要十几秒 到生产环境不开多GPU并发, 时间上是个大问题

- 你这个结论并不严谨，你肯定是同时只处理一个文档得出的结论。我也测过，并行处理的速度和能力大不相同

- 其实可以考虑纯多模态的 LLM 的方案，这个方案的好处是性能好，便于扩展，自己优化的空间大。任何语言都可以写，比如我用 golang 写的 https://github.com/recally-io/go-markitdown
  - 这种方案也有一些限制，如果用服务商API，数据隐私问题不好解决，自己部署，成本高于专做抽取转换的模型。
- 自己部署开源到 Qwen-VL 系列，效果也很好，还可以自己基于自己的数据来 fine-tune 。 至于成本就看取舍，是更在乎隐私还是更关心成本。
  - 视觉模型确实可以考虑

- 根据我之前的调研，感觉目前还没有完美的支持多类型文档多模态的解析库。速度，准确性，成本三角里，最均衡的个人觉得反而是楼上有人说到的大模型多模态解析能力
  - 速度-准确性-成本三角，确实很重要，看需求中哪个角更看重了。

- 感觉大家都在挑工具处理 PPT 和 Excel 这种企业内部传统文档，找来找去发现还是等 VLM 成长

- 公司的知识库来源比较繁杂，想看看这几个专门做文件解析处理的库照顾会不会好一些。
- 大概率是人工作，不需要洗的数据基本都是个人知识库，企业的都要洗。
- 单纯靠技术做结构化 难
  - 单纯靠人做结构化 也难
  - 技术先怼个垃圾 反向推人 再帮人构建一点小工具校对补充 就不难了
  - AI不够人工凑  基本都能干下来

- 惯了自己用的AI工具，再做公司的，总想吐槽一句：garbage in, garbage out
# discuss
- ## 

- ## 

- ## [LLM to query large documents (or sets of documents) : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1ci8868/llm_to_query_large_documents_or_sets_of_documents/)
- First  go through the documents to index them using some vector DB.  Not just stuffing them into the DB, but extracting all useful knowledge from them. An entry for each fact. If the doc is too big, read it in chunks and use additional summaristion queries. 
  - Link the knowledge to the documents. Then, when querying, query the DB and get the matching docs.

- is it possible to do this quickly with langchain / rag framework ? which one did u use ?
  - Depends. It's <50 lines of code in python/JS and most of it is just boilerplate that can be generated with llama. I don't use any frameworks, just code it myself. Don't see any benefits in using langchain.
