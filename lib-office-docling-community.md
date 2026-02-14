---
title: lib-office-docling-community
tags: [community, docling, format, office, pdf]
created: 2025-09-19T16:28:46.784Z
modified: 2025-09-21T13:57:50.332Z
---

# lib-office-docling-community

# guide

# draft
- roadmap
  - ppt
# discuss-stars
- ## 

- ## 

- ## 

- ## [How to extract images when using Docling with VLM? Also wondering can we use VLM in the OCR pipeline? _202601](https://github.com/docling-project/docling/discussions/2833)
  - I was testing Docling's PDF parsing capablities with OCR and VLM pipelines against scanned PDF files, but seems the `generate_picture_images` option doesn't work with VLM pipline, I cannot see any images been extracted like the OCR pipeline did.
- This is expected: in Docling's VLM pipeline, the generate_picture_images option only works if the VLM model output includes explicit image references (like tokens in Markdown or DocTags). If the model/prompt doesn't produce PictureItem elements, no images will be extracted or saved
  - This is different from the standard OCR pipeline, which always extracts images from the PDF itself regardless of model output. 
- I wrote a PoC, the WER is definitely lower, but the layout shifted, moreover, style and table structure all lost...

- [Does VlmPipeline ignore pipeline_options.do_picture_description = True? _202510](https://github.com/docling-project/docling/discussions/2434)
  - it seems the markdown format that works
# discuss-llamaIndex
- ## 

- ## 

- ## 

- ## [[Feature Request]: Update BM25 Retriever to Fully Support bm25s Non-ASCII and UTF-8 Options · Issue · run-llama/llama_index _202501](https://github.com/run-llama/llama_index/issues/17461)
  - The current implementation of `BM25Retriever` in LlamaIndex relies on an older version of bm25s (0.2.3 or 0.2.4), which does not support non-ASCII tokenization or UTF-8 encoding. 
- May I ask if this has already been updated? Which version of `BM25Retriever` should I use？
  - version 0.6.5 has encoding support. I used this version to handle persisting and loading Portuguese nodes.
- Can it be used to process Chinese?
  - Yep. Also, I advise you to use file_extractor to avoid losing any context, since if you don’t set return_full_document=True, each page will be treated as a separate document
- I have some questions. I have upgraded llama-index-retrievers-bm25 to version 0.6.5 and found that the bm25s version is 0.2.14. Then I used a document with Chinese and English code to test retrievers and found that the retrievers results were inaccurate and not ideal. It works not fine with pure Chinese code also，I'm not sure where I went wrong. What is the file that "persists and from_persist_dir " mean in your code?
  -  I think I have mislead you early, sorry, but apparently bm25 retriever does not support chinese, therefore you need to use another snippet of the code, there is a thread about it doesnt supporting chinese and japanese because of the stemmer and tokenizer
- I've seen that comment, so I think the BM25S doesn't support Chinese. I felt the earliest article was a bit misleading. If you need Chinese support, you still need the jieba word segmenter. Also, I'd like to ask about using vectorized queries for Chinese

- ## 🇨🇳 [[Bug]: BM25Retriever cannot work on chinese · Issue · run-llama/llama_index _202405](https://github.com/run-llama/llama_index/issues/13866)
  - `BM25Retriever` cannot work on chinese.

- In the version 0.10.57, the tokenizer option is marked as deprecated and suggest to use a stemmer instead. How can I make use of stemmer for Chinese?
- this interests me. checked bm25s and a new BM25Retriever. my current understanding is below:
  - bm25s has a built-in tokenizer but it does not support Chinese and also Japanese (in my case). so need to implement tokenizer by myself in some ways such as implemet tokenizer outside of bm25s, or making a subclass for bm25s and override tokenize method implemented by myself, etc.
  - llamaindex's BM25Retriever imports bm25s and calls tokenizer method inside of BM25Retriever, this means other languages which bm25s does not support are not suppoted as default.
  - only thing we can in current implementation, we can pass bm25s. BM25() object which contains an index created using bm25s, not llamaindex.
  - as a result, we don't use llamaindex for indexing stage, only for querying stage.

- Thanks for your suggestion. Yes, I agree with you that BM25Retriever and BM25SRetriever should be different things. And I made myself a Chinese vesion of BM25Retriver using bm25s finally.
# discuss-solutions
- ## 

- ## 

- ## 🆚 [I benchmarked 7 OCR solutions on a complex academic document (with images, tables, footnotes...) : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jz80f1/i_benchmarked_7_ocr_solutions_on_a_complex/)
  - I ran a comparison of 7 different OCR solutions using the Mistral 7B paper as a reference document (pdf), which I found complex enough to properly stress-test these tools
  - The document includes footnotes, tables, figures, math, page numbers, ... making it a solid candidate to test how well these tools handle real-world complexity.
  - Goal: Convert a PDF document into a well-structured Markdown file, preserving text formatting, figures, tables and equations.
- Results (Ranked):
  - MistralAPI [cloud] → BEST
  - Marker + Gemini (--use_llm flag) [cloud] → VERY GOOD
  - Marker / Docling [local] → GOOD
  - PyMuPDF4LLM [local] → OKAY
  - Gemini 2.5 Pro [cloud] → BEST* (...but doesn't extract images)
  - Markitdown (without AzureAI) [local] → POOR* (doesn't extract images)

- I had used paddleOCR in production. actually It worked best after adding a LLM summarizer and guard-rail for checking accurate JSON output
- It's not directly supported by Docling (`--ocr-engine: easyocr, ocrmac, rapidocr, tesserocr, tesseract`), but I suspect it would behave similarly to the EasyOCR engine.
  - nop. paddle is much better than EasyOCR, especially for numbers. offtopic: also, no memory leaks in prod.

- Please try Qwen2.5-VL, InternVL3 and GPT 4.1 and report back
  - Qwen2.5-VL supports absolute position coordinates with bounding boxes, so it should be able to detect images and provide coordinates. 
  - With this its possible to extract the images and interleave references to them at the correct place in the text, in theory! 
  - It also has powerful document parsing capabilities not only for text but also layout position information and a "Qwen HTML format".
- I’ve tried using qwen for bounding boxes on images from pdfs - sadly they only seem to work for photographs and object grounding. It wasn’t able to ex. Give me coords of a table or a drawing in an image. It is however very good for markdown 
  - 32B is better.

- Olmocr has a great model as well if you want to check it out: https://github.com/allenai/olmocr
  - I concur, especially it was trained on academic papers.

- ## [Best (non-paid) way to turn complex PDFs into markdown : r/LangChain _202502](https://www.reddit.com/r/LangChain/comments/1ilnftx/best_nonpaid_way_to_turn_complex_pdfs_into/)
  - What I’ve found to be the best fit, based on a combination of speed and accuracy, is `pymupdf4llm` . It does what I need it to and is super fast. 
  - Docling is accurate too but at least the default settings for it were very slow. 
  - Another user suggested they were able to get it to be faster but for right now pymupdf4llm is doing to job.

- docling worked the best out of all the suggestions but took 10 minutes for an 11 page PDF
  - Docling supports different backends for for pdf parsing and ocr. You could get some speed improvements by playing around with those.

- i just did a 15 page pdf conversion to md jst to confirm it is slow(20 seconds), but its manageable then earlier a user said about pymupdf4llm which is blazzingly fast(5 seconds ish) jst tried it but the structure is lost 
  - docling structure is very neat

- Docling doesn’t have a way of maintaining the original page numbers (important for citations) in the conversion, and doing the conversion page by page is extremely slow. On the other hand PyMuPdf4llm has a fast page by page conversion to markdown.

- I had been using docling or marker-pdf but now mostly only using a local hosted qwen 2.5 vl

- AFAIK, Markitdown doesn’t support images or sort of... since you can use llm_client for image descriptions. However, it's fast but in general, it struggles with complex documents (especially papers that include figures, tables, or vertical text) compared to Docling, which is really good. That said, it’s good enough for simpler use cases.

- Marker with gemini (--use_llm) is insanely good. Better than the rest. Although the king is still MistralOCR

- ## 🆚 [Marker vs Docling for document ingestion in a RAG stack: looking for real-world feedback : r/Rag _202509](https://www.reddit.com/r/Rag/comments/1niaqzd/marker_vs_docling_for_document_ingestion_in_a_rag/)
  - I’ve been testing Marker and Docling for document ingestion in a RAG stack.
  - Marker = fast, pretty Markdown/JSON + good tables/math; 
  - Docling = robust multi-format parsing + structured JSON/DocTags + friendly MIT license + nice LangChain/LlamaIndex hooks.

- Tested both. Ended with Kreuzberg , faster and cheaper.

- Docling all the way. Once things get complex (like all RAG eventually do) you will appreciate the docling format and how much you can make with it.
  - But i don't like the smoldocling VLM it is not working on their website as they promote it, and thats my problem.

- From my experience, Docling tends to handle complex multi-column PDFs and OCR tasks better. For throughput, it scales well on a CPU for mid-sized batches. If you're looking into post-processing, semantic chunking really refines context accuracy, especially for layout-sensitive docs. Watch out for licensing terms if you switch to commercial options.

- Pandoc worked best for me
  - not handle different file types as well OCR

- I tried both but ended up with unstructured platform. I rly didn't feel like setting up scaffolding code to run things on my cpu + vector store compatability also saved me some time

- Docling works well and supports OCR. Google's new tool, langextract, could also be an option, but it still needs testing. https://github.com/google/langextract /apache2/python

- In my tests Docling is extremeeeeeely slow
  - Thats because it uses CPU
- Even using gpu (H100) I serve a small vlm there it takes 11 minutes for a 400 page pdf.
- Do you use smoldocling or which ocr library?
  - nanonets-ocr-s vlm. I find it the best for document parsing by far.

- ## [LlamaParse vs Docling for extracting information from bank account statements (PDF)? : r/LangChain _202411](https://www.reddit.com/r/LangChain/comments/1gzdnev/llamaparse_vs_docling_for_extracting_information/)
- One challenge was that the LLM which minerU uses doesnt understand images, Iam finding a way to use a Vision model which can parse the images too in the PDF but I reckon it shouldnt be hard to swap the models.
  - This is why I dont like cloud based services like Llamaparse because the lack of sensitive data handling.
- Investigated MinerU recently, it do not support image understanding, it do optical layout analysis and OCR, also save cropped image as md link
  - Yeah it doesnt, im wondering if the underlying LLM can be changed to a vision model like llama3.2 vision for better image recognition and summary.
- it use some small specialized model, such as doc layout analysis, table recognizing, formula analysis. Maybe you can just process the cropped images directly using you local VLM, even replace them in the markdown document
  - Yup you are right, I eventually went with ChatGPT for $20 and uploaded the screenshot of the documentations and told it to summerize it and write the contents in text. I did have to give the previous and after context from the text for it to connect the dots and I just replaced the img in markdown with text.

- can you run llamaparse locally? 
  - I don’t think it’s a local thing. My understanding is that it’s tied to some cloud service but I could be wrong

- I did some tests, I needed to parse tables in the PDF documents. Out of number pdf parsers only Llamaparse and AWS Textraxt gave me good results, but they are cloud based and you have to pay. I could not get Docling working, I had some issues while installing it. Also, omni did good job as well.

- We switched to Docling from Unstructured so can't say about Llamaparse but Docling definitely beats unstructured by a lot.
  - It extracts more content than Unstructured cand and automatically deals with switching between text and OCR. Got a few examples where Unstructured gave me no text but Docling fetches everything just fine

- ## 🆚 [Comparison between Apache Tika and Docling for Text Extraction : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1h4ix0o/comparison_between_apache_tika_and_docling_for/)
- tike: java, support docx/doc/pdf/...
  - limited support for pdf-format/table
- docling: support pdf-format/table/layout, slow-pdf-ocr, not support doc/xls

- I have used PyMuPDF4LLM. Performs well in most cases. Only issues I see are when there are watermarks in the background, and some issues with clipping images

- txtai is fantastic! There is a new library called extractous that takes Tikas benefits and does away with some of the cons you listed: https://github.com/yobix-ai/extractous
  - It’s using GraalVM and Rust to compile to native. Also has python bindings.
  - If it wasn’t for tables I’d say Tika fits 90% of use cases great while being extremely affordable in terms of compute + delivering speed.

- My recent experience with docling is that it needs supervision because it will make cuts (which I do not want) and is imperfect with tables. It is still very good at document analysis and conversion to Markdown, though. 
  - My experience with this compared to the existing solutions is that they also need supervision and significantly more time to fix the output compared to docling. 
  - The cuts are more manageable than a word jumble and there being no attempt at formatting, but possibly something that can be overlooked completely.
- There are things that are straight out not working for Tika. Character count per page is not working, there is a ofter of few dozen of character per page, it it makes the whole count entirely wrong after few pages. Tika literally keeps errroring after few thousands of PDF ingested.

- 🆚 [PDF Data Extraction Benchmark 2025: Comparing Docling, Unstructured, and LlamaParse for Document Processing Pipelines - Procycons _202503](https://procycons.com/en/blogs/pdf-data-extraction-benchmark/)
- Our comprehensive evaluation of Docling, Unstructured, and LlamaParse reveals Docling as the superior framework for extracting structured data from sustainability reports, with 97, 9% accuracy in complex table extraction and excellent text fidelity. 
  - While LlamaParse offers impressive processing speed (consistently ~6 seconds regardless of document size) and Unstructured provides strong OCR capabilities (achieving 100% accuracy on simple tables but only 75% on complex structures), Docling’s balanced performance makes it ideal for enterprise sustainability analytics pipelines.

- Conclusion
- Docling emerges as the most robust framework for processing complex business documents. 
  - It offers high text extraction accuracy, superior table structure preservation, and effective ToC reconstruction, supported by moderate and predictable processing speeds (e.g., 6.28s for 1 page, scaling linearly to 65.12s for 50 pages).
  - Its use of advanced models like DocLayNet and TableFormer ensures reliable handling of diverse document elements, with only minor omissions (e.g., “5” in the Bayer table). 
  - This balance of precision, structural fidelity, and efficient performance makes Docling the recommended choice for applications requiring scalability and accuracy, such as enterprise data processing and business intelligence.

- Unstructured performs well in text and simple table extraction, achieving 100% numerical accuracy in straightforward cases, 
  - but its inconsistencies such as column shifts in complex tables and incomplete ToC generation limit its reliability. 
  - Its significantly slower speed (e.g., 51.06s for 1 page, 141.02s for 50 pages) further hinder its practicality, suggesting it is best suited for less complex documents or scenarios where speed and resource constraints are not critical. 
  - Addressing its speed inefficiencies and structural parsing could enhance its competitiveness.

- LlamaParse stands out for its exceptional processing speed (~6s consistently across all page counts), offering unparalleled efficiency and scalability. 
  - It performs adequately for basic extractions, with strong numerical accuracy in simple tables and text, but struggles with complex formatting (e.g., multi-column text, intricate tables) and ToC reconstruction. 
  - This speed advantage makes it ideal for lightweight, straightforward tasks, but its structural weaknesses and accuracy trade-offs render it less suitable for comprehensive document processing compared to Docling.
# discuss-elements
- ## 

- ## 

- ## 

- ## [Image in PDF, description into markdown _202511](https://github.com/docling-project/docling/issues/2560)
  - VLM based description of imaged from PDF does not show up in markdown file (only `<!-- image -->` appears). 
- The behaviour you see is not considered a bug. Export formats such as Markdown, HTML or others are by nature lossy in some ways, since they have no native markup to cover every possible data representation that a DoclingDocument can store. Since there is no one-fits-all solution, we are keeping the default Markdown and HTML serialization clean and encourage implementing your own serializer if you need particular outputs, such as the picture descriptions. You can then decide how that should output to Markdown. The serializer API in docling is user-extensible

- this should now be fixed with docling-core v2.51.0
# discuss-ai/llm-format
- ## 

- ## 

- ## 

- ## 🚀 [IBM just released Granite Docling : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1njet2z/ibm_just_released_granite_docling/)
- What is the difference with Docling library ? Is it that it’s not using EasyOCR but homemade OCR ?
  - 👷 I’m one of the authors of Granite Docling and Docling.
  - Docling uses a multi-stage pipeline with specialized models, layout, tables, equations, image descriptions, plus a PDF parser/OCR (like EasyOCR).
  - With SmolDocling and Granite Docling, we’re working on an ultra-compact VLM that can handle all of these tasks in a single model (no parsing needed).
  - The VLM approach has the advantage of capturing the full document context, while the multi-stage pipeline offers more modularity and flexibility. 
  - Other VLMs out there export to formats that we think aren't complete, so with SmolDocling and now Granite Docling we predict in a format that can be transformed to DoclingDocument.
  - Docling actually supports both: you can run inference with the traditional multi-stage setup or with Granite Docling, depending on what works best for your use case.
  - Yep, and also VLLM supported! Check it out!

- Basically this model outputs text that resembles the `DoclingDocument` format. That text is then converted into a `DoclingDocument` object. Instead of using OCR and parsing libraries such as the ones integrated into Docling you just use this model

- It's a 258M param model, it's not for VQA or understanding the content of charts and figures. It's for document conversion into DoclingDocuments.
  - Yes, our model is primarily focused on document conversion. While it’s possible to use it for QA-style tasks, that’s more of a side capability not something we position as a core feature.
- maybe I misunderstood. In the past I've used SmolDocling for generating image captions and, so, expect/expected some level of understanding on top of extraction.

- Tried this on an image-based PDF and it has a lot of repeating issues. The native docling library itself without the vlm did a near perfect job OCRing the file, but the VLM, it failed pretty bad. I'm using the MLX version fwiw, on an m4 128gb. I thought it might be my settings, but I saw that this is a common issue. Anyone else experience this and know a workaround?

- 0.3B? impressive. Almost like even low end phones will have solid local LLM inferencing in the future.
  - Thanks, we are trying to push as much as we could with the smaller models, as some tasks do not need such large models.

- ## 🚀 [SmolDocling - 256M VLM for document understanding : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1je4eka/smoldocling_256m_vlm_for_document_understanding/)
  - a new smol model (256M parameters) to transcribe PDFs into markdown, it's state-of-the-art and outperforms much larger models 
  - The text is rendered into markdown and has a new format called DocTags, which contains location info of objects in a PDF (images, charts), it can caption images inside PDFs.
  - Inference takes 0.35s on single A100 
  - This model is supported by transformers and friends, and is loadable to MLX and you can serve it in vLLM
  - We have a new checkpoint coming that improves tables significantly. We were aiming with SmolDocling to have base on how we aim to do document conversion with VLMs.

- How does it perform vs the original docling?
  - This model comes from the team behind Docling, it was a collaboration with my team at Hugging Face. The goal is for SmolDocling to be better than full docling, but I'm not sure if it's quite there yet. The team is working on integrating it into Docling and we should have a more clear answer in the next few weeks. On the other side, we are also training new checkpoints improving the model based on the feedback we are receiving

- Do you think that the VLMs will replace the extraction pipelines that user layout model and traditional OCRs?
  - That's the plan! but it will take some time. Hopefully a year or so, could be more.

- in my tests involving tables to markdown/html it hallucinates a lot (other multimodal LLMs also do)

- I have had pretty good results actually with using Qwen 2.5 VL 7b to extract data out of both PDFs and engineering drawings

- What languages are supported?
  - we trained and evaluated on English. Anecdotally, it seems to work well for other languages with the same notation, I think training on so much code and equations made the model very resilient to “fixing” the text, so it pretty much writes what it sees and then the language is less important. But expanding to more multilingual support is definitely the next step if this gets a good reception 

- multilinguality?
  - People have been reporting good results on European languages, but we didn't properly evaluate it yet.
- Very cool! It seems that it reads arabic but from couldn’t check it and verify 100% because the words are read from left to right instead of right to left. Any idea how to make it read Arabic properly?

- Was Granite used in any way to produce this?
  - We used Granite Vision to weakly annotate charts within full pages in some cases.

- How does it compare to qwen2.5 VL?
  - It beats Qwen2.5 VL 7B in all the document understanding evaluations we did! You can check more details in the paper: https://huggingface.co/papers/2503.11576

- Chinese OCR performance is poor
  - I would expect that. Next release hopefully we can expand to chinese and more

- Does it support structured outputs ? I went through Docling documentation and could only see DoclingDocument to Markdown or HTML. As well, could a document template be used as input to increase key pair value accuracy (Template + Document to extract)?
  - We have plans for Key Value extraction
  - We just wanted the output when you do document conversion to be as minimal and produce as less tokens as possible, but be compatible with DoclingDocuments so then you are able to utilize all the different features Docling provides. However you are free to parse out the key values as you wish!

- How does it do with CPU only?
  - The base model is smolvlm. We still haven’t optimised it for cpu only, but I suspect that it could be done and would be good

- Fast Batch Inference Using VLLM

- A question related to fine-tuning: is it feasible to tune this model to support domain-specific document tags?
  - Yes it is possible to fine-tune or extend, that's why we are open sourcing it. We however encourage you if you think there are extensions that could be made to checkout our package docling-core and contribute this for everyone.

- I have seen aot of small models for Ocr recently, what makes OCR so suited for smaller model sizes, what other type of tasks can be shrunk to smaller models.
  - Small LLMs are basically pretty dumb, and OCR is just reading stuff without reasoning at all. Seems like a match made in heaven. Large LLMs struggle because they want to "fix" what they read, ie, they tend to avoid gramatical mistakes that are present in the text.

- Really liked the concept of Doctags. I tried on few images and it works well not perfect.
# discuss-devops/toolchain
- ## 

- ## 

- ## [Hosting Docling : r/LLMDevs _202502](https://www.reddit.com/r/LLMDevs/comments/1im5g48/hosting_docling/)
  - We want to use Docling. Our app is web-based so we have to host it. Ideally, we would go AWS, bug GCP is also an option.
  - In our first tests, we could run a fairly large PDF in a n1-standard-2 VM from GCP (packing an Nvidia T4) in around 35s. This instance costs around $220 monthly.

- Creating Docker images gives you numerous deployment options. I have created for myself two images: one with CPU support and another optimized for GPU acceleration, along with a sample FastAPI API.
  - All you need is a server from any provider (I am using OVH, very cost-effective). Simply deploy using docker-compose and set up the internal routing. I’m using Cloudflare Tunnels for routing (but it is not ideal, maybe nginx directly is better).
  - If you need a better speed, you can deploy the GPU image to Lightning. AI and set auto-scale (with the minimum option as 0, so you will save costs, when not used)

- I have a related question. I was trying to use Docling to parse a 220 page pdf using gpu accelerators. When monitoring the load, it seemed like CPU was doing majority of the processing with short periods of GPU bursts. But the overall boost remained low when compared to cpu only processing.
# discuss-roadmap
- ## 

- ## 

- ## [DocumentStream only accepts a BytesIO, but it should instead accept an abstract class like ` IO[bytes]` ](https://github.com/docling-project/docling/issues/2279)
  - It appears that you can only construct a DocumentStream from a BytesIO concrete class. And this is great for most general purpose use cases, 
  - but if you happen to have a custom type that implements the IO abstract class methods such as read, seek, etc, then DocumentStream should allow this as well.

- ## [Improve backend resolution logic ](https://github.com/docling-project/docling/issues/802)
  - Document conversion currently contains a logic for "guessing" / resolving the backend to use for a given input (ref).
  - This logic has some limitations, e.g. when working with streams, it relies on the first 8KB to detect the backend to use — which may or may not be enough for a correct detection (e.g. deciding info could only appear at the end of a 10KB stream).
- One possible high-level approach to examine could be to:
  - remove the current layer of "guessing" a backend a priori and then committing to that guess, and
  - instead, keep for each format, e.g. XML, a list of backends to try one after another, until one successfully parses (can have a default list, parametrizable by the user).

- It turns out also the `filetype` library is loading only 8K bytes ref, so this happens also in file inputs.

- 
- 

- ## [How to optimize PDF to Markdown extraction for large PDFs? ](https://github.com/docling-project/docling/issues/2120)

- ## [Question regarding supporting file streaming _202506](https://github.com/docling-project/docling/discussions/1798)
  - I am using docling for parsing long PDF documents (1000s of pages). I wanted to ask if docling supports parsing with file streams (i.e., not downloading the entire file into memory before starting the docling conversion).
  - I saw that docling supports inputs of types Path, str or DocumentStream (which is basically a BytesIO object, but even this requires copying the entire file into BytesIO memory before sending it to docling?).
  - Can you help clarify my question in this regard?

- ## [LMStudio, Remote Services, smoldocling · docling-project/docling _202506](https://github.com/docling-project/docling/discussions/1849)
- It looks like it got stuck in a loop. It seems to do well, then gets stuck over and over

# discuss-mineru
- ## 

- ## 

- ## 

- ## [mineru vl是有内置paddleocr v5吗，我不熟的时候似乎在日志还是哪里看到过，后面找不到了，我想用paddleocr v5替换单张图片的ocr · opendatalab/MinerU _202512](https://github.com/opendatalab/MinerU/discussions/4254)
  - mineru vl对与某些旋转、倾斜、纵向的图片里面的文字表格识别没有paddleocr v5效果好

- MinerU 的 PaddleOCR v5 只集成在 pipeline 后端，不在 VL（vlm-*）后端内置。你在日志里看到的 PaddleOCR v5 相关内容，实际上是 pipeline 模式下的 OCR 日志，VL 后端的 OCR 逻辑是独立实现的，不会直接调用 PaddleOCR v5

- ## [请问lite版和full版的主要差别 · opendatalab/MinerU _202411](https://github.com/opendatalab/MinerU/issues/1127)
- lite是早期开发的时候测试用的，使用了paddleocr的PP-StructureV2作为layout模型，结合paddleocr本身的ocr能力，用来做可行性验证的，实际上结果并不准确，在正式版本中没有开放lite的使用能力。

# discuss
- ## 

- ## 

- ## 

- ## [Love-hate relationship with Docling, or am I missing something? : r/Rag](https://www.reddit.com/r/Rag/comments/1r3kk3b/lovehate_relationship_with_docling_or_am_i/)
  - I can use texts to get any text block from the pdf.
  - This is given that nothing is lost in the docling conversion, and for most pdfs I try this on there always is. There's always some block either missing or not part of the correct group, for example:
  - list items interpreted as being text block, thus not being part of a list group
  - With my projects demand for accuracy Docling is not enough, but it's so so close!

- You are not fighting Docling, you are fighting PDF. If you would try the same with Azure Document Intelligence, you'd end up with a similar experience.
  - What can help (but does not always) is post-processing. You use all sorts of tricks to re-establish relationships that were missed by the OCRing tool. For example, you could use an LLM and ask it to put things together in a coherent way.

- Docling is not the end game.. use it just to parse but there is a whole lot of post processing before ingestion begins. But yes depends upon on the need

- ## [FileNotFoundError: Missing safe tensors file: D:\docling\docling\_model\model.safetensors  ](https://github.com/docling-project/docling/issues/2310)
- I managed to solve it by downloading specific configs and models. This command helped in my case:
 `docling-tools models download layout tableformer rapidocr -o <folder_path>`

- ## [Doubts about requirements to use docling in server : r/LangChain _202505](https://www.reddit.com/r/LangChain/comments/1kivf0m/doubts_about_requirements_to_use_docling_in_server/)
- We run Docling on CPU on dedicated servers from OVHCloud with min 32gb ram. Takes anywhere from 1 ot 5 seconds of parsing per page, more with OCR.
- How many CPUs?
  - 4

- ## [Docling just pounds my machine for PDF docs : r/Rag _202508](https://www.reddit.com/r/Rag/comments/1n3txpl/docling_just_pounds_my_machine_for_pdf_docs/)
  - it's slow on PDF documents. I haven't tried another tool to parse my documents, because for Word and other documents Docling is great. But on PDF documents, it kills my (admittedly not super fast) machine. Look at the CPU charts for while Docling is running on a 4.5 Mb document!
  - Interestingly enough...before I tried anything else, I took Docling out of the docker container it was running in. I wanted to run it in a container for obvious reasons, but I thought I would test it's performance outside of a container, just running natively on my system (M1 Macbook Air w/16 Gb). Go figure...the performance was night and day different. I knew there was container overhead, but it was staggering - 15 minute parses when down to ~3 minutes.

- Hey try my exaOCR (https://github.com/ikantkode/exaOCR). It is extremely lightweight. I’m putting together a benchmark. But in my tests 78 documents with a little over 1000 pages took about 3 minutes. The pages are processed in parallel.
  - I built it for my RAG app (https://github.com/ikantkode/pdfLLM) - it’s current OCR processor takes about 1 min.
  - I’m improving OCR capabilities and trying to make a tool with existing tech.
  - It’s actually FastAPI based, streamlit interface is mainly to test it out.
  - After deploying on your server, you can go to http://localhost:8000/api/ for FastAPI documentation. Or replace localhost with server IP accordingly.
- https://github.com/ikantkode/exaOCR /202508/python
  - A simple CPU only OCR for pdf/images/word/excel to markdown. With streamlit.
  - Built with FastAPI + Streamlit, optimized for CPU-only environments, and battle-tested on 800+ page contracts, exaOCR delivers sub-3-minute processing while preserving tables, forms, and layout structure.

- ## [Docling: Great quality, but painfully slow : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mpmhxj/docling_great_quality_but_painfully_slow/)
  - I've been using Docling for a while now, and I have to say the output quality is good. It really nails accuracy and formatting in a way that most other tools don't.
  - The problem? Speed. It's painfully slow. Even relatively small documents take far longer than I’d expect, and without a GPU, large ones can take over an hour. I get that good processing takes time, but in my case, the wait often outweighs the benefits.
  - Is anyone else experiencing the same thing? Have you found any tweaks, settings, or workarounds that make Docling faster without sacrificing quality?

- Not Docling optimisation or workaround but perhaps viable alternatives depending on your workflow:
  - You may want to have a look at GROBID (https://grobid.readthedocs.io/en/latest/). I have used the lightweight version (CRF-only) and was pretty impressed by the output quality even with complex PDF layouts. 
  - I recently came across Kreuzberg (https://github.com/Goldziher/kreuzberg) which I didn't have time to test yet. The benchmarks look good so probably worth a try.
- After conducting several simple tests, I confirmed the following points:
  - Docling's performance is overwhelmingly superior.
  - Both of the two options you recommended have excellent speed, but Kreuzberg is slightly faster.
  - In particular, Docling has a high likelihood of successfully parsing even the most complex tables, while the other two options appear to have a higher probability of incorrect parsing.
  - However, Docling is 'extremely unstable.' The symptoms described in several GitHub issues manifest directly, making it too unstable to recommend for either enterprise or personal use. These symptoms are particularly evident when processing large files.

- Yes, it's slow by design for accuracy, but you can speed it up by using flags like `--no-ocr` if you don't need it or switching to the faster `--pdf-backend=dlparse_v2`

- Docling is slow because of the OCR and the models it uses to detect layout, formulas, pictures, etc... You can make it run faster if you disable all those features but then the output won't be as good. So the sad truth is you'll probably need better hardware.
  - Run `docling-tools models download --all` and you'll see the models it might eventually use and where they are being stored.

- ## [Docling is a new library from IBM that efficiently parses PDF, DOCX, and PPTX and exports them to Markdown and JSON. : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1ghbmoq/docling_is_a_new_library_from_ibm_that/)
- I have many use cases locally where I was calling external gemini api for the ocr + extraction bit (because it was just easier). Now I can simply do this and simply call my local nice little llm that work on text and markdown. So nice

- 🆚 Is Docling better than MarkItDown ?
  - Absolutely, Docling is far superior to Markitdown. I gave it a shot this week and was really impressed—it’s incredibly fast with docs, CSVs and other file types. 
  - PDFs do take longer if you process every page, but I’m planning to test it with specific page ranges and use multiprocessing to see if that speeds things up. 
  - Overall, Docling saves a ton of time on parsing and is a much better option than Markitdown.
- Is docling capable of converting/translating a complex image chart or table from a PDF to markdown?
  - yes at least for tables in financial docs and 10k reports. It does take a minute or 2 for pdfs that are 50 page plus, but the quality of output in my testing was much better than markitdown.
- MarkItDown completely sucks for PDFs (just tested today, wasted a bit of time to self-host it and link it to my AI automation workflow) - it outputs PDFs as text... Huge 'PDF' support 

- 🆚 Docling is at least 50x slower than PyMuPDF. But it does have categorization when you need structured output, the tradeoff.
  - yes, for one task docling took 8mins something minutes but pymupdf did it in 8 seconds something, but I think the quality of extraction of docling is better but still the time taken is too much to be overseen.
- PyMuPDF is AGPL, useless for any serious SaaS use case.

- I’ve been using docling for about a month or so. The processing speed could definitely be improved, and apparently they are working on it, but the output quality is the best of all the open-source solutions

- what are some closed source solutions that are as good or better than docling?
  - aws textract, azure doc intelligence

- I wonder how well this would work for non searchable pdfs.
  - You can make OCR with Surya or Tesseract.

- ## IBM开源了一款轻量多模态文档处理模型：Granite-Docling (apache2)，能执行OCR、文档QA，258M _202509
- https://x.com/aigclink/status/1968584313064276374
  - 公式识别96.8%准确率、代码识别98.8%、表格结构97%
