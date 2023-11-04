---
title: lib-ai-app-examples
tags: [ai, examples]
created: 2023-02-08T07:20:33.048Z
modified: 2023-02-08T07:20:48.475Z
---

# lib-ai-app-examples

# guide

# popular

# LLM

- https://github.com/xenova/transformers.js
  - Run Transformers in your browser! We currently support BERT, ALBERT, DistilBERT, MobileBERT, SqueezeBERT, T5, T5v1.1, FLAN-T5, mT5, BART
  - [宝玉 on Twitter: "这有必要吗？"](https://twitter.com/dotey/status/1643801825580122115)
    - 毕竟浏览器有沙盒，相对在本地运行一个没审计过的程序放心一点，但现在浏览器对gpu硬件支持还是拉胯。
    - 这是分布式算力啊，这不就是挖矿嘛
# chatgpt
- app-site
  - https://github.com/LiLittleCat/awesome-free-chatgpt
  - [免费 chatgpt](https://twitter.com/search?q=%E5%85%8D%E8%B4%B9%20chatgpt&src=typed_query&f=live)

- api-free
  - [一口气送了350个免费的key](http://freeopenai.xyz/)

- https://freechatgpt.chat/
  - 类似官网，需要key
  - 可选内置不稳定key

- [ChatGPT API Demo](https://ai.ls/)
  - https://ai.ls/
  - Powered by gpt-3.5-turbo

- [free ChatGPT](https://freegpt.one/)
  - using gpt-3.5-turbo

- [OpenGPT](https://open-gpt.app/)
  - 立即使用海量的 ChatGPT 应用，或在几秒钟内创建属于自己的应用

- https://github.com/lencx/ChatGPT /rust
  - ChatGPT Desktop Application (Mac, Windows and Linux)
  - 国内ip无法访问

## gpt-apps

- 写了个基于 ChatGPT 的 AI 维权律师，根据事实和诉求帮当事人生成起诉书。
  - https://twitter.com/imyuanx/status/1641715695762436098
  - https://github.com/imyuanx/ai-lawyer

- https://github.com/nicepkg/gpt-runner
  - Conversations with your files! Manage and run your AI presets!

## api

- [https://www.steamship.com](https://www.steamship.com/)
  - SteamShip 开放了 GPT-4 的模型接口，只需要注册SteamShip 账号，无需付费，几行代码直接就能调用 GPT-4

## prompts

- [Open Prompt](https://openprompt.co/)

## gpt-impl

- https://github.com/newhouseb/potatogpt
  - Pure Typescript, dependency free, ridiculously slow implementation of GPT2 for educational purposes
# chat
- https://github.com/PKU-YuanGroup/ChatLaw
  - https://chatlaw.cloud/lawchat/
  - 中文法律大模型

- https://github.com/LAION-AI/Open-Assistant
  - OpenAssistant is a chat-based assistant that understands tasks, can interact with third-party systems, and retrieve information dynamically to do so.
# coding-copilot
- https://github.com/TabbyML/tabby
  - https://tabbyml.github.io/tabby
  - Self-hosted AI coding assistant. 
  - An opensource / on-prem alternative to GitHub Copilot.
  - Self-contained, with no need for a DBMS or cloud service
  - OpenAPI interface, easy to integrate with existing infrastructure (e.g Cloud IDE).
  - Tabby 是一个自我托管的 #GitHub #Copliot 开源替代品，自带可视化界面与 #OpenAPI 接口，还支持消费者级别的 #GPU，具有 FP-16 重量加载和各种优化功能，提供了 #Docker 镜像
# text2image
- https://github.com/Stability-AI/stablediffusion
  - https://github.com/CompVis/stable-diffusion
  - A latent text-to-image diffusion model

- https://github.com/camenduru/stable-diffusion-webui-portable
  - This Project Aims for 100% Offline Stable Diffusion (People without internet or with slow internet can get it via USB or HD-DVD)

- https://github.com/AUTOMATIC1111/stable-diffusion-webui
  - A browser interface based on Gradio library for Stable Diffusion.

- https://github.com/cmdr2/stable-diffusion-ui
  - The easiest way to install and use Stable Diffusion on your computer.
# ml-neural-network
- https://github.com/AlloyTeam/netural
  - JavaScript的前向神经网络和反向传播的实现。

- https://github.com/TrevorBlythe/MentisJS
  - A javascript neural network library. 
  - It can train with backpropagation or neural evolution! 
  - [A better alternative to convnetjs](https://github.com/karpathy/convnetjs/issues/122)
    - This library has Deconv layers and other new features that not even convnetjs has.
    - It also doesn't require you to put your data in a custom data type.

- https://github.com/mlc-ai/web-llm
  - Introducing WebLLM, an open-source chatbot that brings language models (LLMs) directly onto web browsers. 
  - We can now run instruction fine-tuned LLaMA (Vicuna) models natively on your browser tab via @WebGPU with no server support.

- https://github.com/photopea/UNN.js
  - Deep Learning in Javascript. Alternative to ConvNetJS, that is 4x faster.
  - [A 4x faster alternative to ConvNetJS](https://github.com/karpathy/convnetjs/issues/115)
    - It has capabilities similar to ConvNetJS, but both training and testing are 4x faster (while still running in a single JS thread on the CPU).

- https://github.com/mil-tokyo/webdnn
  - The Fastest DNN Running Framework on Web Browser

- https://github.com/karpathy/convnetjs
  - Deep Learning in Javascript. Train Convolutional Neural Networks (or ordinary ones) in your browser.
  - [[Question] Why use javascript ?](https://github.com/karpathy/convnetjs/issues/72)
    - Performance-wise there is no reason to believe that JavaScript would perform significantly slower than Python. The reason why Python is used over C++ is not performance, it is the ecosystem.
    - For fast execution Python or C++ might not even be the best for neural networks as GPGPU computing could be the ultimate solution for fast parallel computing of lots of artificial neurons. In that case JavaScript would yield roughly the same performances as Python of C++.

- https://github.com/BrainJS/brain.js
  - robot GPU accelerated Neural networks in JavaScript for Browsers and Node.js
# ml-dl
- https://github.com/visheratin/web-ai /MIT/ts
  - run modern deep learning models directly in the web browser or in Node.js
  - Powered by ONNX runtime. Web AI runs the models using ONNX Runtime, which has rich support for of all kinds of operators.
  - Web worker support. All heavy operations - model creation and inference - are offloaded to a separate thread so the UI does not freeze.

- https://github.com/xenova/transformers.js /js
  - https://huggingface.co/docs/transformers.js
  - State-of-the-art Machine Learning for the web. 
  - Run Transformers directly in your browser, with no need for a server!
  - Transformers.js is designed to be functionally equivalent to Hugging Face's transformers python library
  - Transformers.js uses ONNX Runtime to run models in the browser. The best part about it, is that you can easily convert your pretrained PyTorch, TensorFlow, or JAX models to ONNX using Optimum.

- https://github.com/ml5js/ml5-library /js
  - provides access to machine learning algorithms and models in the browser, building on top of TensorFlow.js

- https://github.com/alibaba/pipcook /ts
  - https://alibaba.github.io/pipcook/
  - provides subprojects including machine learning pipeline framework, management tools, a JavaScript runtime for machine learning, and these can be also used as building blocks in conjunction with other projects.
  - provides access to Python packages by bridging the interface of `CPython` using N-API. so pytorch/tensorflow/scikit is available

- https://github.com/mljs/ml /js
  - Machine learning tools in JavaScript
# more
