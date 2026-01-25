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

- ## 

- ## 
# discuss-YOLO/traditional
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [From YOLO to VLMs: Advancing Zero-Shot and Few-Shot Detection of Wastewater Treatment Plants Using Satellite Imagery in MENA Region | Abstract _202512](https://arxiv.org/abs/2512.14312)

# discuss-vlm
- ## 

- ## 

- ## 

- ## 
# discuss-tips
- ## 

- ## 

- ## 

- ## [Information extraction with long document (images included) : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nuvwak/information_extraction_with_long_document_images/)
- The document parsing step you outlined is solid but you're overcomplicating the image-text mapping part.
  - Your approach of converting pages to images first then using VLM is actually the right direction, but I'd simplify step 1. Instead of doing separate OCR for bounding boxes then trying to map cropped images back to text tags, just let the VLM handle both text extraction AND image positioning in one pass. Most decent VLMs can already tell you "there's an image here between paragraph X and Y" without needing separate OCR tools. For the actual implementation, yeah OpenAI's vision models work great for this but if you want to keep it local, try running something like LLaVA or the newer Qwen2-VL models. The key thing is being really specific in your prompts about maintaining spatial relationships and hierarchical structure. 
  - For step 2, instead of trying to get the LLM to cite page numbers (which honestly isn't super reliable), consider keeping a metadata mapping where each extracted section links back to the original page ranges from step 1. 
  - The RAG approach you mentioned as a backup is actually pretty smart because it gives you flexibility when section titles are vague or when content spans weird boundaries. We've seen similar challenges with educational content processing using Docstrange and the hybrid approach tends to work better than trying to make one method handle all edge cases perfectly.

# discuss-solutions
- ## 

- ## 

- ## 

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

- ## 

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
