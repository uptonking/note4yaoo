---
title: thread-products-ocr
tags: [image, ocr, pm, thread]
created: 2023-12-18T15:14:59.375Z
modified: 2023-12-18T15:15:36.887Z
---

# thread-products-ocr

# guide

# discuss
- ## 

- ## 

- ## 

- ## Announcing llama-ocr –  a free + open source OCR tool
- https://x.com/nutlope/status/1856402928086725020
  - It takes documents (images for now) & outputs markdown, and does really well for complex receipts, PDFs with tables/charts, ect...
  - Powered by Llama 3.2 vision on @togethercompute & available on npm today

- I already compared the llama 3.2 visión in groq with other models and it performs quite good in general but when analyzing receipts if its a bit rotated then it starts to fail when assigning correct item prices and so on. If you need an example I can dm you
- Is there any comparison with llama parse? What are the things generally we should consider while switching from llama parse to llama ocr?

- ## 开源中文 OCR 最好用的是哪个? 甲方不想用云服务.
- https://twitter.com/hylarucoder/status/1766782291651575871

- PaddleOCR是百度开源的中文OCR项目，在GitHub上star数非常多，项目很活跃。它专门针对中文进行了模型训练优化，识别精度很高。而且有详尽的中文文档，易于使用。
- CnOCR基于Python开发，支持简繁中文、英文和数字识别，也支持竖排文字。模型轻量，执行速度快，甚至略快于PaddleOCR。而且支持pip直接安装，使用方便。识别效果与PaddleOCR不相上下。

- 强推paddleOCR，经得住落地验证
- Paddle准确率没有百度云那么高，百度有保留
- 现在基本上都在paddleocr上finetuning，我在大厂
- 恐怕只有paddle可用, 但是他的分拆較差, 有丟行的情況
- OneNote自带的OCR功能。
  - 这个不行呢, 要在服务端跑的
- 
- 
- 
- 
- 

- ## Is there some library to run OCR on any image, get text and also exact position of the text in the image?
- https://twitter.com/dobroslav_dev/status/1736407254138527774
- If you want to do any OCR (non-diagrammatic/flow charts etc), google cloud vision is the industry standard. have tried almost all the managed and open-source solutions over the years - for millions of images

- AWS Textract has been good for my OCR use case, might be able to do what you're looking for but haven't tried
- I ended up going with AWS Textract. Then sending the results through LLM to make better sense out of them. 

- Azure is the way forward for this right now. The quality is unmatched and free for early stage.

- just used Adobe PDF Services API for this
