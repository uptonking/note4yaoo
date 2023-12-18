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

- ## Is there some library to run OCR on any image, get text and also exact position of the text in the image?
- https://twitter.com/dobroslav_dev/status/1736407254138527774
- If you want to do any OCR (non-diagrammatic/flow charts etc), google cloud vision is the industry standard. have tried almost all the managed and open-source solutions over the years - for millions of images

- AWS Textract has been good for my OCR use case, might be able to do what you're looking for but haven't tried
- I ended up going with AWS Textract. Then sending the results through LLM to make better sense out of them. 

- Azure is the way forward for this right now. The quality is unmatched and free for early stage.

- just used Adobe PDF Services API for this
