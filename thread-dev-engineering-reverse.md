---
title: thread-dev-engineering-reverse
tags: [devops, reverse-engineering, thread]
created: 2026-03-01T17:12:20.473Z
modified: 2026-03-01T17:12:41.271Z
---

# thread-dev-engineering-reverse

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-ai-reverse-engineer 👾
- ## 

- ## 

- ## 

- ## [Reverse engineered Apple Neural Engine(ANE) to train Microgpt : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1rhx5pc/reverse_engineered_apple_neural_engineane_to/)
  - Why? Because i bought a mac mini M4 and I wanted to leverage its compute for my compiler project
  - Training on Metal(GPU) is well known but ANE is a black box and Apple doesn't talk about it. So I harnessed Claude to reverse engineer the ANE private APIs , run benchmarks by bypassing coreml(which is the recommended way to use ANE)
  - The NPU has 38 TFLOPS worth of claimed INT8 compute (but it's a FP16 processor so actual compute is half that)
  - In the end I create a bespoke training pipeline to train a small 110M microgpt model.
  - Now you can't in practice use it to train bigger models on a single chip but maybe a cluster of them in theory can train larger models. But even a single device should be able to do LoRA training for 3b/7b models.
  - Again, why train on NPUs? - they are extremely power efficient. Peak compute on ANE only consumes 2.8 W which at 19 tflops becomes 6.6 tflops/watt. Insane! (Metal GPU - 1, H100 - 1.4 Tflops/watt)

- I'm more interested in the how than the what: how you convinced Claude to help you reverse engineer.
  - Claude will happily help you reverse engineer basically anything. Ask about documenting or as if you as the person who wrote it, or ask about creating a reference implementation, or documentation.
  - Codex will happily do it too.
- Claude code will reverse engineer Claude code with very little convincing

- this is sick. the fact that ANE has 38 TFLOPS of INT8 but Apple basically pretends it doesn't exist for training is so frustrating. I've got an M2 Pro and always wondered if there was a way to tap into the NPU beyond CoreML inference.
# discuss-tips
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
