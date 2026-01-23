---
title: lib-ai-app-community-model-small-edge
tags: [community, large-language-model, mobile, phone]
created: 2026-01-23T13:08:23.483Z
modified: 2026-01-23T13:10:20.291Z
---

# lib-ai-app-community-model-small-edge

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-browser-ai
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🧭 [Chrome's Local AI Model in production (Gemini Nano) 41% eligibility, 6x slower and $0 cost : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qkph45/chromes_local_ai_model_in_production_gemini_nano/)
  - reading about Chrome's built in AI model (Gemini Nano 1.8b) and tried implementing it, this is my story.
  - Google ships Chrome with the capability to run Gemini Nano, but not the model itself.
  - Multiple models, no control. Which model you get depends on an undocumented benchmark. You don't get to pick.
  - ~1.5-2GB download. Downloads to Chrome's profile directory. Multiple users on one machine each need their own copy.
  - On-demand. The model downloads the first time any site requests it.
  - Background download. Happens asynchronously, independent of page load.
  - Think of the requirements like a AAA video game, not a browser feature.
  - Inference Performance:
  - Gemini Nano (on-device)	7.7s
- 👀 At p99, Nano hits 52.9 seconds while Gemma is at 2.4 seconds. Worst case for Nano was over 9 minutes. Gemma's worst was 31 seconds.
  - prompt-processing 速度太慢
- What Surprised Us
  - No download prompt. The 1.5GB model download is completely invisible. No confirmation, no progress bar. Great for adoption. I have mixed feelings about silently dropping multi-gigabyte files onto users' machines though.
  - Abandoned downloads aren't a problem. Close the tab and the download continues in the background. Close Chrome entirely and it resumes on next launch (within 30 days).
  - Local inference isn't faster. I assumed "no network latency" would win. Nope. The compute power difference between a laptop GPU and a datacenter overwhelms any latency savings.
  - You can really mess up site performance with it We ended up accidentally calling it multiple times on a page due to a bug..and it was real bad for users in the same way loading a massive video file or something on a page might be.
- By the numbers, there's no reason to use Gemini Nano in production:
  - It's slow
  - ~60% of users can't use it
  - It's not cheaper than API calls (OpenRouter is free for Gemma)
- We're keeping it anyway. I think it's the future. Other browsers will add their own AI models. We'll get consistent cross-platform APIs. I also like the privacy aspects of local inference. The more we use it, the more we'll see optimizations from OS, browser, and hardware vendors.

# discuss-small-llm-hot
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 
