---
title: lib-ai-app-community-model-vlm-ocr
tags: [large-language-model, ocr, vision, vlm]
created: 2025-11-06T18:48:41.322Z
modified: 2025-11-06T18:49:13.977Z
---

# lib-ai-app-community-model-vlm-ocr

# guide

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
# discuss-tips
- ## 

- ## 

- ## 
# discuss-solutions/tools
- ## 

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

- [PaddlePaddle/PaddleOCR-VL · GGUF or MLX support?](https://huggingface.co/PaddlePaddle/PaddleOCR-VL/discussions/2)
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
# discuss
- ## 

- ## 

- ## 
