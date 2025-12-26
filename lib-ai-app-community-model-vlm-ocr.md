---
title: lib-ai-app-community-model-vlm-ocr
tags: [large-language-model, ocr, vision, vlm]
created: 2025-11-06T18:48:41.322Z
modified: 2025-11-06T18:49:13.977Z
---

# lib-ai-app-community-model-vlm-ocr

# guide

- leaderboard
  - [OCR Arena](https://www.ocrarena.ai/battle)
    - [I made a free playground for comparing 10+ OCR models side-by-side _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p35f2c/i_made_a_free_playground_for_comparing_10_ocr/)
  - [SpatialBench - AI Spatial Reasoning Benchmark](https://spicylemonade.github.io/spatialbench/)
    - Evaluating multimodal model performance on complex 3D and 2D spatial tasks.
    - https://github.com/spicylemonade/spatialbench
    - designed to evaluate the next generation of multimodal AI models on their ability to reason about space, structure, and pathing

- https://github.com/bytefer/macos-vision-ocr /MIT/202502/swift
  - A powerful command-line OCR tool built with Apple's Vision framework, supporting single image and batch processing with detailed positional information output.
# models-vlm/ocr
- qwen3-vl-4b
  - 适合作为通用图片文字识别方案，识别完后一般还会解释一段，有时解释文字会冗长

- nanonets-ocr2-3b
  - 输出的内容markdown优先，内容及格式都很准确
    - 表格中的代码也能正确输出为markdown inline code
    - 外部链接能直接输出为markdown链接
    - 同一区域的内容会输出为同一个段落，不会按原文本显示换行
  - 识别图片中的代码块输出codeblock
  - 识别mermaid流程图，输出流程图文本
  - 能正确识别页眉页脚
  - 能识别图文混排元素，输出内容时能提供方位，如插图旁边是...
  - 能识别表格，但 表格行内容有时会错位而在中间插入空行

- deepseek-ocr-3b
  - 适合识别文档，对于普通图片文本的识别有时需要特别的prompt，实测 `extact text` 会导致模型乱回复, 而 `extact text in image` 可以准确回复图片中的文本
  - 不能识别mermaid流程图
  - 不能正确识别页眉页脚，默认忽略了
  - 同一区域的内容有时不会输出为同一个段落，会按图片中的换行输出换行，适合用来还原pdf布局
  - 识别图片中的代码块输出的内容不是codeblock而是普通文本
  - 🌹
    - 识别中文的正确率高
    - 识别图片中的表格能准确输出文本，每行内容正确

- granite-docling-258m
  - 能输出带语意的自定义标签, 如 page_header, code, list_item, loc_99, text
  - 默认markdown不友好，需要手动转换自定义标签
  - 部分中文识别的错误率较高

- PaddleOCR-VL

- MinerU2.5

- 
- 
- 
- 

# discuss-stars
- ## 

- ## 

- ## 

- ## LlamaIndex - We’ve written a new blog post on the specific areas in which LLMs are useful for document OCR - beyond the naive answer of “screenshot everything into a VLM”
- https://x.com/jerryjliu0/status/1991624512656535664
  - Existing techniques were hand-tuned, brittle/didn’t generalize, and lacked general semantic understanding
  - LLMs are helpful for zero-shot semantic layout reconstruction
  - VLMs are helpful for both visual layout understanding as well as specialized element understanding (tables, charts)
  - So LLMs and VLMs are both more general and zero-shot. By themselves they don’t solve PDF parsing, but the trick is to incorporate them in targeted ways as part of this next-gen OCR pipeline.

- LLMs and VLMs aren’t magic alone but combining them smartly really moves the needle for document parsing

- How do you solve the issue of "off by one row" kind of problems when there is a table in page and the rows are kinda close to each other?
# discuss-tips
- ## 

- ## 

- ## 
# discuss-solutions
- ## 

- ## 

- ## 💡 [Qwen3-VL works really good with Zoom-in Tool : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1osiog7/qwen3vl_works_really_good_with_zoomin_tool/)
  - While Qwen3-VL-30B-A3B(Q6_ud) performs better than previous open-source models in general image recognition, it still has issues with hallucinations and inaccurate recognition.
  - On my own frontend implementation with zoom_in, Qwen3-VL can zoom in on the image, significantly improving the accuracy of content recognition. 
  - For those who haven't tried it, qwen team has released a reference implementation: https://github.com/QwenLM/Qwen-Agent/blob/main/examples/cookbook_think_with_images.ipynb

- This is what o3 did with it's visual reasoning agent, I think it should be incorporated with every VLM system it's that good - outperforms pretty much every other model in complex problems (even ones better at full-size native image comprehension like Gemini and Opus).
  - I agree that every VLM should have such tools. The official Qwen website provides these tools for Qwen-Max, but not for the 30B model. I suspect that the smaller Qwen models may suffer from repetition issues, which could cause tool usage to fail at high probabilities. (30B-A3B tends to repeat when calling multiple tools in my daily usage.)

- tools are allowed to return images???
  - MCP protocol does not work well with images. Qwen-Agent saves picture to local disks and tools receive their filenames then go to read the file.

- ## [MinerU 到底是模型还是工程产品 - V2EX](https://v2ex.com/t/1170882#reply10)
- MinerU 分为两个 backend
  - 一个是 pipeline ，集成了多种文档相关的模型，并基于后处理合并完成文档解析；
  - 另一个是 vlm backend ，目前 2.5 版本是一个 qwen 架构 1.2B 的 vlm 模型，这个模型分为两阶段，一阶段是对版面进行分析，获取区域、区域类别、区域顺序，二阶段是对区域进行解析，提取文本、表格、公式，最后后处理合并。
  - 他们的输入输出是一致的（功能一致），但使用的技术不同，效果和性能也有差异，需要根据自己场景按需选择。
- paddleocr 在 MinerU pipeline backend 被集成（完成 ocr ），但 vlm 后端两者完全没有关联

- ## LGM：生成高质量3D模型，支持文字生成模型、图片生成模型，分辨率512*512，5秒内即可生成。
- https://x.com/Gorden_Sun/status/1784230776311284205
  - https://github.com/3DTopia/LGM

- ## 免费玩的本地大模型，本地搭建环境推荐用Ollama和ChatbotAI
- https://x.com/vista8/status/1862696894172209476
- Vision 建议换成用 Llama 3.2 Vision 11b，比llava要好很多，且支持多语言（包括中文）的文字识别

# discuss-ocr
- ## 

- ## 

- ## 

- ## [OCR4all | Hacker News _202502](https://news.ycombinator.com/item?id=43043671)
- A little secret: Apple’s Vision Framework has an absurdly fast text recognition library with accuracy that beats Tesseract. It consumes almost any image format you can think of including PDFs.
  - After getting an iPhone and exploring some of their API documentation after being really impressed with system provided features, I'm blown away by the stuff that's available. My app experience on iOS vs Android is night and day. The vision features alone have been insane, but their text recognition is just fantastic. Any image and even my god awful handwriting gets picked up without issue.

- The problem with doing OCR with LLMs is hallucination. It creates character replacements like Xerox's old flawed compression algorithm. 
  - Graybeards like Tessaract has moved to neural network based pipelines, and they're re-inventing and improving themselves.
  - I was planning to train Tessaract with my own hand writing, but if OCR4All can handle that, I'll be happy.
- Paradoxically, LLMs should be the tool to fix traditional OCR by recognizing that "Charles ||I" should be "Charles III", "carrot ina box" should be "carrot in a box", the century of the event in context cannot be that construed through looking at the gliphs etc.
  - As someone who's learning how to do OCR in order to re-OCR a bunch of poorly digitized documents, this will not work with modern OCR. Modern OCR is too good.
  - If you're able to improve the preprocessing and recognition enough, then there's a point at which any post-processing step you do will introduce more errors than it fixes. LLM's are particularly bad as a post-processing step because the errors they introduce are _designed to be plausible_ even when they don't match the original text. This means they can't be caught just by reading the OCR results.
  - I've only learned this recently, but it's something OCR experts have known for over a decade, including the maintainers of Tesseract. 
  - OCR is already at the point where adding an LLM at the end is counterproductive. The state of the art now is to use an LSTM (also a type of neural network) which directly recognizes the text from the image. This performs shockingly well if trained properly. When it does fail, it fails in ways not easily corrected by LLM's. I've OCR'ed entire pages using Tesseract's new LSTM engine where the only errors were in numbers and abbreviations which an LLM obviously can't fix.
- Tesseract wildly outperforms any VLM I've tried (as of November 2024) for clean scans of machine-printed text. True, this is the best case for Tesseract, but by "wildly outperforms" I mean: given a page that Tesseract had a few errors on, the VLM misread the text everywhere that Tesseract did, plus more. I strongly suspect that traditional OCR systems will become obsolete, but we aren't there yet.

- Tesseract worked fine until the hand written part, then garbage. 

- I also made an AI assisted OCR API 
  - It combines Tesseract (for images) and Poppler-utils (PDF). A local open-source LLMs will extract document segments intelligently.

- I think the current sweet-spot for speed/efficiency/accuracy is to use Tesseract in combination with an LLM to fix any errors and to improve formatting, as in my open source project which has been shared before as a Show HN: https://github.com/Dicklesworthstone/llm_aided_ocr

- I maintain a searchable archive of historical documents for a nonprofit, OCR'd with Tesseract over several years. Tesseract 4 was a big improvement over previous versions, but since then its accuracy has not improved at the same rate as other free solutions.
  - These days, just uploading a PDF of scanned documents (typeset ones, not handwriting) to Google Drive and opening with Google Docs results in a text document generated with impressive quality OCR.
  - But this is not scriptable, and doesn't provide access position information, which is needed so we can highlight search results as color overlays on the original PDF. Tesseract's hOCR mode was great for that.
  - For the next version, we're planning to use one of the command-line wrappers to Apple's Vision framework, which is included free in MacOS. A nice one that provides position information is at https://github.com/bytefer/macos-vision-ocr

- Apple Vision and its wrappers provide bounding boxes for each line of text. That's slightly less convenient than Tesseract which can give you a bounding box for each word, but more than compensated by Apple Vision's better accuracy. I am planning to fudge the word boxes by assuming fixed-width letters and dividing up the overall width so that each word's width is proportional to its share of the total letters on the line.
  - Once you have those bounding boxes, it's pretty simple to use a library like (Python) or (JavaScript) to add overlay text in the right place
  - https://github.com/eloops/hocr2pdf /MIT/202509/js/inactive
  - take scanned image, and hocr output from tesseract, create PDF. Thats it.

- ## [LLM Aided OCR (Correcting Tesseract OCR Errors with LLMs with Python) : r/Python _202408](https://www.reddit.com/r/Python/comments/1eo6dxz/llm_aided_ocr_correcting_tesseract_ocr_errors/)
- Nice job! I was looking at your code and noticed you are using regex to split sentences. From my own experience I know that is not ideal for this kind of job. You could try using the spaCy open source library to split sentences with NLP. It has an incredible 99% accuracy (meaning that sometimes two sentences will be grouped into a paragraph). This way you can avoid false positives like “I know Dr. Evil” being split into two separate sentences because of the dot after the abbreviated word.
  - Thanks. It’s actually not that sensitive to that because each chunk shown to the LLM contains a portion of the previous chunk so that the LLM has the context. So it doesn’t really affect the quality of the output either way.

- ## [Show HN: LLM-aided OCR – Correcting Tesseract OCR errors with LLMs | Hacker News _202408](https://news.ycombinator.com/item?id=41203306)
- In my experience, this works well but doesn't scale to all kinds of documents. For scientific papers; it can't render formulas. meta's nougat is the best model to do that. For invoices and records; donut works better. Both these models will fail in some cases so you end up running LLM to fix the issues. Even with that LLM won't be able to do tables and charts justice, as the details were lost during OCR process (bold/italic/other nuances). 
  - I feel these might also be "classical" methods. I have found vision models to be much better as they have the original document/image. 

- For any one curious on automating document processing end-to-end by leveraging llms do try Unstract. It is opens source. https://github.com/Zipstack/unstract
  - Unstract also has a commercial version of document agnostic parser which you can channel to any RAG projects. https://unstract.com/llmwhisperer/

- We've been trying to solve this with https://vlm.run: the idea is to combine the character level accuracy of an OCR pipeline (like Tesseract) with the flexibility of a VLM.
  - OCR pipelines struggle with non-trivial text layouts and don't have any notion of document structure, which means there needs to be another layer on top to actually extract text content to the right place. At the other end of the spectrum, VLMs (like GPT4o) tend to perform poorly on things like dense tables (either hallucinating or giving up entirely) and complex forms, in addition to being much slower/more expensive. Part of the fix is to allow a 'manager' VLM to dispatch to OCR on dense, simple documents, while running charts, graphs etc. through the more expensive VLM pipeline.

- If anyone is looking to compare results visually, I have created an open source OCR visualiser to help identifying missing elements (especially in tables). https://github.com/orasik/parsevision

- I did something similar about a decade ago because I was using tesseract to OCR Chinese.
  - Part of the problem is that if you use Tesseract to recognize English text it's much easier to clean it up afterwards because if it makes a mistake it's usually in only a single character, and you can use Levenstein distance to spellcheck and fix which will help a lot with the accuracy.
  - Logographic languages such as Chinese present a particular challenge to "conventional post-processing" having many words represented as two characters and often a lot of words as a single "glyph". This is particularly difficult because if it gets that glyph wrong there's no way to obvious way to detect the identification error.
  - The solution was to use image magick to "munge" the image (scale, normalize, threshold, etc), send each of these variations to tesseract, and then use a Chinese-corpus based Markov model to score the statistical frequency of the recognized sentence and vote on a winner. It made a significant improvement in accuracy.
- People's handwriting vary widely, and a human reading someone's writing faces the same problems you mention. For a language like English, humans also decipher unrecognized characters by looking at what letter would fix the word or what word would fit in the sentence, etc.

- I wonder if you could feed back the results from an LLM into the OCR model to get it to make better decisions. E.g., if it's distinguishing a 1 from an I, the LLM could provide a probability distribution.
  - Or the other direction. Tesseract can give you confidence levels for the guesses it makes about a symbol 

- ## [How can I determine OCR confidence level when using a VLM? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oaum1r/how_can_i_determine_ocr_confidence_level_when/)
- One approach that works surprisingly well is running the same extraction twice with slightly different prompts and checking for consistency - if the VLM gives you different supplier names or amounts between runs, thats a strong signal the image quality is problematic and worth flagging for reupload.

- ## [Docling, how does it work with VLM? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p9zvkl/docling_how_does_it_work_with_vlm/)
  - So i have a need to convert PDF to text for data extraction. 
  - Regular/Traditional OCR does very good job but unfortunately it does not take into consideration the layout, so while each word is perfectly recognized the output is a gibberish (if you try to read it). Understood each word but actual text does not make sense.
  - VLMs, such as Qwen3-VL or OpenAI do a good job producing markdown considering layout, so it makes sense but unfortunately the actual OCR is not nearly as good. It hallucinates often and no coordinates where the word was found.

- ## [Do we really need traditional OCR and layout models at this point, since VLMs have improved so much. : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jmcbsk/do_we_really_need_traditional_ocr_and_layout/)
- An affordable top-loading scanner can scan about 25 pages per minute.
  - If you needed to scan and OCR five hundred printed pages, how long do you think it would take a vision model to get it done?
  - Traditional OCR can work faster than the scanner scans pages, and on much more modest hardware.

- We are working on a pipeline to extract text from a specific type of paper documents. The best approach we found is to detect the layout, mask, extract using 3-4 different OCR models, majority vote, validate with VLM if there's a tie, check the output text syntax, grammar, etc with a larger LLM.
  - We are experimenting with <10B models for the VLM. The VLM comes in only to resolve conflicts, not systematically, because it's slooow in comparison to Trad OCR tools

- We use Qwen2.5 VL 72B to convert PDF files into markdown. Works significantly better than many OCR solutions out there, but it's also much slower than those.

- ## 🤔 [Replace OCR with Vision Language Models | Hacker News _202502](https://news.ycombinator.com/item?id=43187209)
- It’s an interesting idea, but still way too unreliable to use in production IMO. When a traditional OCR model can’t read the text, it’ll output gibberish with low confidence; when a VLM can’t read the text, it’ll output something confidently made up, and it has no way to report confidence. (You can ask it to, but the number will itself be made up.)
  - There’s no way to ground the model using the source text when the model is your OCR.
- Thing is, the majority of OCR errors aren't character issues, but layout issues. Things like complex tables with cells being returned under the wrong header.

- We recently published an open source benchmark specifically for evaluating VLM vs OCR. And generally the VLMs did much better than the traditional OCR models.
  - https://github.com/getomni-ai/benchmark
- VLM highlights:
  - Handwriting. Being contextually aware helps here. i.e. they read the document like a human would, interpreting the whole word/sentence instead of character by character
  - Charts/Infographics. VLMs can actually interpret charts or flow diagrams into a text format. Including things like color coded lines.
- Traditional OCR highlights:
  - Standardized documents (e.x. US tax forms that they've been trained on)
  - Dense text. Imagine textbooks and multi column research papers. This is the easiest OCR use case, but VLMS really struggle as the number of output tokens increase.
  - Bounding boxes. There still isn't really a model that gives super precise bounding boxes. Supposedly Gemini and Qwen were trained for it, but they don't perform as well as traditional models.
- There's still a ton of room for improvement, but especially with models like Gemini the accuracy/cost is really competitive.
- there are a few caveats to VLMs that folks are typically unaware of (not at all exhaustive, but the ones you highlighted):
  - 1. Long-form text (dense): Token limits of 4/8K mean that dense pages may go over limits of the LLM outputs. This requires some careful work to make them work as seamlessly as OCR.
  - 2. Visual grounding a.k.a. bounding boxes are definitely one of those things that VLMs aren't natively good at (partly because the cross-entropy losses used aren't really geared for bounding box regression). We're definitely making some strides here to improve that so you're going to get an experience that is almost as good as native bounding box regression (all within the same VLM). 

- LLMs and OCR have very different failure modes. 
  - With LLMs, there is unbounded potential for hallucination, and the entire document is at risk.
  - With OCR, errors are localized and have a greater chance of being detected when read.
  - I think for a lot of cases, the best solution is to fine-tune a model like LayoutLM, which can classify the actual text tokens in a document (whether obtained from OCR or a native text layer) using visual and spatial information. Then, there are no hallucinations and you can use uncertainty information from both the OCR (if used) and the text classification. But it does mean that you have to do the work of annotating data and training a model, rather than prompt engineering
- 100% this, combining traditional OCR with VLMs that can work with bounding boxes so that you can correlate the two is the way to go.

- An effective way that usually increases accuracy is to use an ensemble(乐团; 剧团; 歌舞团) of capable models that are trained independently (e.g., gemini, gpt-4o, qwen). If >x% of them have the same output, accept it, otherwise reject and manually review

- I've been using gemini 2 flash to extract financial data, within my sample which is perhaps small (probably 1000 entries so far), I've had one single error only so like a 99.9% success rate.
  - Many hallucinations can be avoided by telling it to use null if there is no number present.

- Modern OCR is astonishingly good, more importantly it's deterministically so. It's failure modes, when it's unable to read the text, are recognizably failures.
  - Results for VLM accuracy & precision are not good

- Tesseract doesn’t use an LLM. LLMs don’t know how confident they are; Tesseract’s model does.
  - Kind of. Tesseract's confidence is just a raw model probability output. You could easily use the entropy associated with each token coming out of an LLM to do the same thing.
- True, but LLM token probability doesn't map nearly as cleanly to "how readable was the text".
  - Why not though? Both kinds of models jumble around the data and spit out a probability distribution. Why is the tesseract distribution inherently more explainable (aside from the UI/UX problem of the uncertainty being per-token instead of per-character)?

- Why do all these OCR services only show examples with flawless screenshots of digital documents? Are there that many people trying to OCR digital data? Why not just copy the HTML?
  - If it's not intended for digital documents, where are the screenshots with fold marks, slipping lines, lighting gradients, thumbs, etc etc.

- You can also use it for robustness. Looking at e.g. historical censuses, it's amazing how many ways people found to not follow the written instructions for filling them out. Often the information you want is still there, but woe to you if you look at the columns one by one and assume the information in them to be accurate and neatly within its bounding box.

- What I want: take scan/photo of a document (including a full book), pass it to the language model, and then get out a Latex document that matches the original document exactly (minus the copier/camera glitches and angles). I feel like some kind of reinforcement learning model would be possible for this. It should be able to learn to generate Latex that reproduces the exact image, pixel for pixel (learning which pixels are just noise).

- You sort of have to use both. OCR and LLM and then correlate the two results. They are bad at very different things, but a subsequent call to a 2nd LLM to pair together the results does improve quality significantly, plus you get both document understanding and context as well as bounding boxes, etc.
  - A VLM that invokes ocr tool use is a compelling idea that could result in pretty good results, I would expect.

- The AI OCR build into snipping tool in windows is better than tesseract, albeit more inconvenient than something like powertoys or Capture2Text, which use a quick shortcut.

- I wonder what the speed of this approach vs traditional ocr techniques. Also, curious if this could be used for text detection (find a bounding box containing text within an image).

- qwen 2.5 vl was specifically trained to produce bounding boxes I believe.

- Existing solutions like Tesseract already can embed text into the image, but I'm wondering if there's a way to combine LLM with Tesseract, so that LLMs can help correcting results and finding unidentified text, and finally still embed text back to the image

- Can I use this to convert flowcharts to yaml representations?

- VLM's can't replace ocr one to one.. most hosted multimodal models seem to have a classical OCR (tesseract-based) step in their inference loop

- ## 🆚 [I benchmarked 7 OCR solutions on a complex academic document (with images, tables, footnotes...) : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jz80f1/i_benchmarked_7_ocr_solutions_on_a_complex/)
  - I ran a comparison of 7 different OCR solutions using the Mistral 7B paper as a reference document (pdf), which I found complex enough to properly stress-test these tools. It's the same paper used in the team's Jupyter notebook, but whatever. The document includes footnotes, tables, figures, math, page numbers, ... making it a solid candidate to test how well these tools handle real-world complexity.
  - Goal: Convert a PDF document into a well-structured Markdown file, preserving text formatting, figures, tables and equations.
  - Results (Ranked):
  - MistralAPI [cloud] → BEST
  - Marker + Gemini (--use_llm flag) [cloud] → VERY GOOD
  - Marker / Docling [local] → GOOD
  - PyMuPDF4LLM [local] → OKAY
  - Markitdown (without AzureAI) [local] → POOR* (doesn't extract images)

- New version of gemini flash seems to have improved further in my test.

- PyMuPdf uses Tesseract for OCR (just for OCR exactly, not whole process of reading document - so it's again the same "old" core solution - of course PyMuPdf have more features).

- ## [Best open-source model for parsing messy PDFs on 16GB RAM (CPU only) - Models - Hugging Face Forums _202510](https://discuss.huggingface.co/t/best-open-source-model-for-parsing-messy-pdfs-on-16gb-ram-cpu-only/168890)
  - My issue is:
  - Larger models don’t fit in my 16GB RAM system.
  - Smaller models run but give low accuracy.

- If you’re limited to 16GB RAM on CPU only, big models won’t fit unquantized. Best option is to:
  - OCR/Extract text first → use ocrmypdf or pdfplumber to clean up messy PDFs.
  - Parsing step → run a quantized 7B model (LLaMA-2 7B or Mistral-7B, 4-bit GGUF/GGML via llama.cpp). These fit in 16GB and give decent accuracy.
  - Optimize →
    - Quantize to 4-bit (saves memory).
    - Chunk PDFs so context isn’t too large.
    - Optionally train a LoRA adapter for insurance-specific fields.
- This combo (OCR + quantized 7B + a few regex rules) should give you the best balance of speed and accuracy on your setup.

- Honestly. Your specs are extremely inadequate. You’re wasting your time.

- I’ve got decent results with Qwen2.5-VL and InternVL3.5. There are also: MarkItDown, MinerU, olmOCR, Surya OCR worth trying. See also DocVQA and OCRBench benchmark leaderboards.

- ## [Is OCR accuracy actually a blocker for anyone's RAG/automation pipelines? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oppykf/is_ocr_accuracy_actually_a_blocker_for_anyones/)
  - Or is "good enough" OCR + error handling downstream actually fine, and I'm overthinking this?

- this is literally my entire life for the past 8 years. We process millions of documents at Nanonets and OCR accuracy is absolutely the make-or-break factor. You're not overthinking it at all.
  - Financial documents are the absolute worst. Multi-column layouts, nested tables, footnotes that reference other footnotes... we spent months just on handling different invoice formats. 
  - Fine-tuning Qwen3-VL is smart - we went a similar route but ended up building our own models specifically for document understanding. Have you tried Docstrange btw? 

- Converting PDFs to images and sending each image to an LLM with context worked well, but it was too expensive.
  - Another approach was to cache the full PDF (such as a scanned or handwritten report) in the LLM, then query it later, e.g., “I need only page 5.”

- ## 在和客户沟通的时候，不在一线干活的某些专家也会说：OCR 问题已经被解决了。 直到我祭出真实场景的图。 Mistral OCR 连表格都识别成图片了
- https://x.com/9hills/status/1981603450254503992
- mineru和paddleocr应该都有试卷训练数据，可以试试。最保底的是gemini-2.5-pro

- Mistral识别表格的能力很强，你这个图其实不是OCR的问题，是还原被混淆图片的问题，如果非要OCR，那应该先用nano banana把公章去除。

- gemini-2.5-pro是通用模型，可能内部有些额外步骤，纯OCR的话Mistral已经做的非常好了，高质高速低价，你可以比较一下Gemini和Mistral OCR的速度

- 我觉得小的vlm 直接做端到端的 pdf->markdown  永远不会解决问题，稍微复杂点的edge case  就出错。最后可能还是得回到传统图像处理+vlm 的路子，先识别出格子和文字，然后连通坐标输到大模型生成markdown

- ## 🆚 [State of Open OCR models : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oe7orf/state_of_open_ocr_models/)
  - [Supercharge your OCR Pipelines with Open Models _202510](https://huggingface.co/blog/ocr-open-models)
- I just tried PaddleOCR and zero-shot worked super well
  - Indeed, that tiny 0.9B model does a perfect transcription and even beats the latest DeepSeek OCR. Impressive.
- for now you could try with vLLM I think, because PaddleOCR-VL comes in two models (one detector for layout and the actual model itself) it's sort of packaged nicely with vLLM AFAIK

- MinerU 2.5 and PaddleOCR both pretty much nail it. They don't do the subscripts but that's not native markdown so fair enough imo.

- [What are the best Open Source OCR models currently? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1okehd9/what_are_the_best_open_source_ocr_models_currently/)
- MinerU 2.5 and PaddleOCR-VL
- Paddleocr-vl, about 1B and best table extraction I’ve seen
- OLMOCR2, Deepseek-OCR, Chandra OCR

- ## [What is the best ocr model for converting PDF pages to markdown (or any text based format) for embedding? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1obha86/what_is_the_best_ocr_model_for_converting_pdf/)
- https://github.com/opendatalab/OmniDocBench
  - MinerU is best but bit annoying to get going
  - Dolphin and Marker are next best

- For the regular pdfs why not just use typical pdf text extraction tools? It is more accurate and has been done for forever. For the pdf images then yeah ocr makes sense.
  - I tried this, and some of my PDFs have corrupted text layers. I got a 114k line text file for a 10 page pdf, so I’d like to just ocr if possible for consistency

- Why even use a model for the OCR part itself? There are multiple tools designed specifically for that which will be far less consuming in both time and resources. I'm not being condescending, I'm just genuinely curious as to what's the benefits of using a model for that.

- ## [Nanonets-OCR2: An Open-Source Image-to-Markdown Model with LaTeX, Tables, flowcharts, handwritten docs, checkboxes & More : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o5nlli/nanonetsocr2_an_opensource_imagetomarkdown_model/)
  - We're excited to share Nanonets-OCR2, a state-of-the-art suite of models designed for advanced image-to-markdown conversion and Visual Question Answering (VQA).
  - It is trained on tons of financial documents. Since the output is in markdown with the tables as html, they can be converted to CSVs also. We have some samples examples for bank statements in the docstrange demo. 
  - `Nanonets-OCR2-1.5B-exp` is experimental model. Full training is not complete yet. We will release the final model when the full training is done.
  - We will add support for Ollama in coming days. Meanwhile you can use the Docstrange (https://docstrange.nanonets.com/). We do have api support there, incase of large volume.

- Can you tell me what are the exact advances over nanonets-ocr-s ? Specifically the 3B model.
  - Thanks. We have scaled our datasets by a lot (close to 3 million documents). New model should work better on multilingual, handwritten data, flowcharts, financial complex tables. 
  - This time we have added Visual Question Answering support. 
  - Fixed some of the edge-cases where model used to give infinite generation for empty tables and stuff. 
  - Also you should be able to change the prompt based on your use case. Nanonets-ocr-s does not work if you change the prompt much.

- tables will already be in html format. You can use this prompt for both getting complex table and header and footer.
  - Also for tables you should use `repetition_penalty=1` for best result. You can try in docstrange 
  - `user_prompt = """Extract the text from the above document as if you were reading it naturally. Return the tables in html format. Return the equations in LaTeX representation. If there is an image in the document and image caption is not present, add a small description of the image inside the <img></img> tag; otherwise, add the image caption inside <img></img>. Watermarks should be wrapped in brackets. Ex: <watermark>OFFICIAL COPY</watermark>. Page numbers should be wrapped in brackets. Ex: <page_number>14</page_number> or <page_number>9/22</page_number>. Prefer using ☐ and ☑ for check boxes."""`

- Can this model provide bboxes with recognized box types (header, text, table) via special prompts or special formats like it did qwen2-vl / qwen3-vl ?
  - We don't support boxes yet. That's in plan for next release.

- I do not see a comparison with the Docling document understanding pipeline from IBM.
  - We will add more evals. But generally in all evals Gemini models are in top. Thats why we first evaluated against Gemini. But for complex document these models, specially the 3B one should be better than docling.
- It will be better than mistral ocr. Our last model was better than mistral. This one is improvement on top of the last model.

- Small models like this one or Docling deliver phenomenal results when the PDFs you are dealing with are not overly complex. While they handle TeX-equations well, the difference to large LLMs becomes very obvious when presenting them graphics. 
  - Default model is trained to give small description. You can change the prompt to have detailed description. Since the model also supports VQA you can do multi-turn multiple questions.

- The issue of any ocr model its wide multilingual support. What about your model?
  - We have trained on multilingual as well as handwritten data.

- Did you also incorporate historical texts? I tried with 18th century fraktur and it often mixed up long s and f. There are quite good sets of historical training data available: https://zenodo.org/records/15764161
  - No we have not trained on historical texts, all the handwritten and multi-lingual datasets are recent data. This is because old text fonts are quite different from recent documents and texts, and these models were mainly used on recents documents. But if there is enough annotated datasets we can definitely include those in next iteration. Thanks for sharing!

- Tested with my handwritten diary (that none other model could parse anything at all) - and all text was extracted! Thank you

- Very cool and excited to see these models keep getting smaller! FWIW I've been building a collection of uv scripts that aim to make it easier to run these new VLM based OCR models across a whole dataset using vLLM for inference. They can be run locally or using HF Jobs. Just added this model to that repo! https://huggingface.co/datasets/uv-scripts/ocr

- ## [Are vision models (like qwen3-vl) good for OCR? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nu7vw8/are_vision_models_like_qwen3vl_good_for_ocr/)
- Your concern about hallucination is totally valid but honestly the accuracy issues with traditional OCR like tesseract are way worse than occasional VL model hallucinations, especially for real world documents. 
  - I've been dealing with this exact problem for years and tesseract just falls apart with anything that isnt a perfect scan - weird fonts, slight rotations, quality issues, you name it. 
  - Vision models like qwen2.5-vl actually have much better accuracy because they understand context and can handle imperfect inputs way better than traditional engines.
  - The key is setting up proper prompting to minimize hallucinations - be very specific about what fields you want extracted and ask the model to indicate confidence levels or mark uncertain text.
  - We built Docstrange specifically for this use case and found that combining good prompting with validation rules catches most issues. For invoices and licenses, the structured nature actually helps a lot since VL models can understand document layout and context much better than traditional OCR engines that just see individual characters.

- I use Qwen2.5-VL for OCR all the time. Works great. I've OCR'd entire PDF scans of documents, and traditional OCR usually OCRs decently but has layout problems, whereas AI OCR usually does a good job of understanding and flattening layout. I've used it for Chinese, Japanese, German, and (of course) English.

- My best results for processing tabular PDFs has been: https://huggingface.co/ibm-granite/granite-docling-258M
  - Qwen-2.5 oddly either gives me great results, or the first row and nothing else.

- Gemma3 27b is pretty great for OCR.
# discuss-vlm 👾
- ## 

- ## 

- ## 

- ## [Is there a VLM that has bounding box support built in? : r/computervision _202508](https://www.reddit.com/r/computervision/comments/1me7ciq/is_there_a_vlm_that_has_bounding_box_support/)
- Florence 2 and PaliGemma 2

- I think Qwen 2.5 VL might be able to do it. It was trained on document understanding and bounding boxes. Prompt it to generate html from your image.

- ## [Feature Request: Support HunyuanOCR-1B · Issue · ggml-org/llama.cpp _202511](https://github.com/ggml-org/llama.cpp/issues/17509)

- ## [I've just ordered an RTX 6000 Pro. What are the best models to use in its 96GB for inference and OCR processing of documents? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ouq7oe/ive_just_ordered_an_rtx_6000_pro_what_are_the/)
- For medical and legal docs you really want something that can handle tables and complex layouts. I've seen people get burned using generic OCR models on medical forms where the layout matters as much as the text.
  - The 6000 Pro should handle most models fine but for production use with multiple users... you might want to think about caching and load balancing. We had a client try to run everything on one GPU for their legal team and it became a bottleneck real quick. 
  - Maybe start with something like LayoutLMv3 or Donut for the document understanding part - they're built for this kind of structured extraction rather than just reading text.

- The suggestion of an OCR specific model is probably a good one. I'll mention the granite docling models. Tiny but will be blazing fast for you.
  - Expect to do a lot of downloading and testing. You need to find what works for you. Then there is the never ending stream of new models to try.

- You don’t really need a fancy LLM for this, if they’re high quality documents you could easily use tesseract. Regarding inference, any RAG approach should work
  - Any handwriting would be out. Tesseract is too old and I think shouldn't be the gold standard anymore.
- Tesseract should work well enough with high quality documents that were originally generated in Office, etc. There are plenty of other solutions out there, tesseract included, that would be drastically quicker and less resource intensive than an LLM whether tesseract, OCRopus, Calamari, Kraken.. it all depends on the nature of the documents, langauge, etc.

- ## [model : add PaddleOCR by ngxson · Pull Request · ggml-org/llama.cpp _202510](https://github.com/ggml-org/llama.cpp/pull/16701)
  - Model generate hallucinated text, likely because of the projector being incorrect
- I was really looking forward to benchmarking this model, until I saw it's limitations, on your point here "Model generate hallucinated text, likely because of the projector being incorrect" I don't think it's due to the projector, I cloned your branch to see why it's hallucinating, it seems to be due to the lack of pre-processing input done by this model "PP-DocLayoutV2"... PaddleOCR-VL is not an end to end VLM, it relies on "PP-DocLayoutV2" for detection, it's basically a glorified version of LayoutLM.
  - Yes I also almost come to the same conclusion. The main issue is that PaddleOCR is not just one monolithic model like Qwen or Deepseek-OCR, but it's more like a pipeline of multiple models glued together. Therefore, I don't think we currently have the infrastructure to bring it into llama.cpp.

- 🐛 [PaddlePaddle/PaddleOCR-VL · GGUF or MLX support?](https://huggingface.co/PaddlePaddle/PaddleOCR-VL/discussions/2)
  - We really would love to convert this model to gguf, mlx format, to make it more accessible. 
  - It has two components, one is a 0.9b VLM, another is a layout analysis model. 
  - For the VLM, it's in pytorch/transformer compatible format, and you can find the pytorch implementation in this repo, and you can run it using vLLM, and I think it's possible to convert it into gguf/mlx with not too much efforts. 
  - For the layout analysis model, i.e., PP-DocLayoutV2, it's in paddlepaddle format, and the implementation is in PaddldOCR repository using paddlepaddle, it needs porting the implementation into pytorch, and converting the weights to pytorch compatible format. There are some glue codes between the two components, which requires some efforts. 
  - The team is much more familiar at paddlepaddle than pytorch ecosystem tools, but we really love to work with the community to make this model being supported by other projects.

- ## [Practical takeaways from recent hands-on use of PaddleOCR‑VL 0.9B : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1obfwt9/practical_takeaways_from_recent_handson_use_of/)
  - Bottom line up front: I care most about whether complex layouts can be restored into structured data, whether handwriting tables and formulas are stable, and local inference speed and cost. 
  - Paddleocr‑VL 0.9B feels purpose built for production, especially for multi column PDFs, table structures, and formulas. 
  - Cloud models like GPT‑4o and Gemini 2.5 Pro are more general for commonsense cross domain understanding and conversational interaction, but you need to factor in cost and privacy compliance.
  - On multi column complex layouts and whether they can be directly restored into structured data, which I value highly because it decides how much human cleanup downstream automation needs. Paddleocr‑VL takes an engineering first approach: a NaViT dynamic visual encoder plus a lightweight ERNIE, combining layout understanding with structured outputs.

- I had similar experiences when we were testing different OCR solutions for Docstrange, and your point about structured outputs being more important than pretty-looking text really hits home. 
  - We found that PaddleOCR-VL's engineering-first approach does seem to handle the weird edge cases better than the general VLMs, especially when you're dealing with those nightmare scenarios like financial reports where a single misplaced table cell can mess up your entire downstream pipeline. 
  - The thing that caught my attention in our testing was how much more predictable the failure modes are with specialized models like PaddleOCR-VL compared to something like GPT-4o which might give you beautiful conversational output but completely miss that a footnote belongs to a specific table cell three pages back.
  - The cost factor you mentioned is huge too, especially if you're processing thousands of documents daily where those API calls add up fast.

- ## 🆚 [Comparison new qwen 32b-vl vs qwen 30a3-vl : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ocko1m/comparison_new_qwen_32bvl_vs_qwen_30a3vl/)
- Dense 32b vl is better in most benchmarks
  - Yeah but the difference is negligible in most of them. I don't know the implications behind that small gap in performance.
- 32B VL seems to be significantly better in multilingual benchmarks, at least that's a good usecase.

- So a slight increase in quality for the 32b, sacrificing a lot of speed from the MoE

- What surprises me is that the 30B is so close, knowing inference should be around 6x faster.

- ## 🆚 [[Experiment] Qwen3-VL-8B VS Qwen2.5-VL-7B test results : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1o9xf4q/experiment_qwen3vl8b_vs_qwen25vl7b_test_results/)
  - TL; DR: I tested the brand-new Qwen3-VL-8B against Qwen2.5-VL-7B on the same set of visual reasoning tasks — OCR, chart analysis, multimodal QA, and instruction following.
  - Qwen3-VL shows a clear generation-to-generation leap and delivers more accurate, nuanced, and faster multimodal reasoning.

- [Qwen3-VL testout - open-source VL GOAT : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1o9eo4f/qwen3vl_testout_opensource_vl_goat/)
  - I’ve been waiting on Qwen3-VL and finally ran the 4B on scanned tables, color-blind plates, UI screenshots, and small “sort these images” sets.
  - Tables came out clean with headers and merged cells handled better than Qwen2.5-VL.
  - Variant behavior matters. The Think build tends to over-explain and sometimes lands wrong. The Instruct build stays steadier for perception, grounding, and “read + point” jobs. 
  - My pattern is simple: let 4B handle recognition and coordinates, then hand multi-step reasoning or code-gen to a larger text model. That stays stable.
  - Net take: big lift in perception, grounding, and visual math; still weak on faithful webpage replication and hard spatial transforms. As of today, it feels like the top open-source VL at this size.

- ## 🆚 [Qwen3-VL Instruct vs Thinking : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nuhgxw/qwen3vl_instruct_vs_thinking/)
  - I am working in Vision-Language Models and notice that VLMs do not necessarily benefit from thinking as it applies for text-only LLMs. 
  - I created the following Table asking to ChatGPT (combining benchmark results found here), comparing the Instruct and Thinking versions of Qwen3-VL. You will be surprised by the results.

- I just want qwen3-30b-a3b-2507 with a vision component so I dont have to load multiple models. 

- I wonder how hybrid vision models do — GLM4.5V comes from the Air version which is hybrid.

- [Qwen3-VL-30B-A3B-Instruct & Thinking are here : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nxhfcq/qwen3vl30ba3binstruct_thinking_are_here/)
- I wonder why the thinking version got worse IFEval than the instruct and even the previous, non-vision, thinking model.
  - yes they don't discuss yet why thinking version, that uses way more inference token budget, performs worse than the Instruct. Imo Thinking for VLMs is not necessarily beneficial
- It seems to improve reasoning in the non-thinking model and hurt it in the thinking? Besides that I guess the difference is only slight and completely mixed. Except for coding, VL makes that worse.

- ## [moondream 0.5B - the world's smallest vision language model : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1h7ivts/moondream_05b_the_worlds_smallest_vision_language/)
  - https://github.com/vikhyat/moondream
  - Moondream 0.5B offers a significantly lower download size and memory usage than moondream 2B.
  - It is intended to be used as a distillation target—start building with moondream 2B, and distill your use-cases onto the 0.5B model before deployment.
  - This model was built using structured pruning on 2B with quantization-aware training. This means we can easily distill from 2B to recover accuracy on the specific target tasks an application needs, and run with int8 quantization without any loss of accuracy.
  - Today we are releasing int8 and int4 weights for moondream 0.5B, as well as fast CPU inference support in the Python client library. 16-bit weights and distillation support will be coming soon, so stay tuned!

- doesnt look like this new model has been added to ollama as yet (and no GGUFs available)

- Awesome. Florence is nice and small too, but could only really handle a finite list of specific prompts. It seems this small models retains the ability to ask free-form questions, which would make it extremely useful for mobile devices.
  - Florence 2 base is smaller. You can also fine tune it to work with any specific prompt you like if you have consistent prompts.
# discuss-toolchain-vlm/cor
- ## 

- ## 

- ## 

- ## 

- ## [How do I enable vision capabilities of a model ? Linux Mint 22.2, rx 6600. I ran this at bash/terminal to start the server: llama-server -m ./Qwen3-VL-8B-Instruct-Q4_K_M.gguf : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p9t8tz/how_do_i_enable_vision_capabilities_of_a_model/)
- `--mmproj <mmproj file>` grab `.mmproj` file where you've got your gguf

- You should read the model card on hugging face https://huggingface.co/Qwen/Qwen3-VL-8B-Instruct-GGUF#web-chat-using-llama-server
# discuss
- ## 

- ## 

- ## 
