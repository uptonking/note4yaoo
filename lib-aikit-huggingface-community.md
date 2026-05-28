---
title: lib-aikit-huggingface-community
tags: [ai, community, huggingface, large-language-model, machine-learning]
created: 2026-05-28T19:24:41.458Z
modified: 2026-05-28T19:25:14.480Z
---

# lib-aikit-huggingface-community

# guide

# docs
- Hugging Face Spaces are configured using a YAML metadata block located at the very top of the repository's README.md file
- When you push code to a Space, the Hugging Face runtime builder inspects this YAML block
  - The sdk: gradio (or streamlit, docker) tag tells the Hugging Face engine which pre-configured runtime container to use.
  - The sdk_version: 4.36.1 tag tells the engine exactly which version of Gradio to inject into that environment
- Common system packages used in machine learning and computer vision are pre-installed, including ffmpeg (for video/audio processing), cmake, and libsm6 (often required by OpenCV).
- Historically, Hugging Face provided built-in Streamlit support exactly the same way it did for Gradio
  - However, according to the latest Hugging Face documentation updates: The option to use streamlit as a default built-in SDK is currently marked as deprecated
  - While older spaces using sdk: streamlit might still run, Hugging Face now officially advises that if you want to deploy a Streamlit Space, you should select the Docker SDK (sdk: docker) and choose their provided Streamlit template
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 

- ## 
# discuss-toolchain
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
