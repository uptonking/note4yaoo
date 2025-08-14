---
title: lib-ai-app-community-generation
tags: [ai, community]
created: 2023-04-16T12:51:38.350Z
modified: 2023-04-16T12:52:03.130Z
---

# lib-ai-app-community-generation

# guide

- resources
  - [【轻科普】StableDiffusion那些事儿，关于LoRA、DreamBooth、模型分层融合等](https://www.bilibili.com/video/BV1RT411D7h7/)
# discuss-video
- ## 

- ## 

- ## 

- ## 想问下这种视频是AI做的么？ 类似短剧
- https://x.com/ilovek8s/status/1911305338239983988
- 4o出图，然后3D化，底图不好说拿啥做的，可能图生视频是既梦
  - 我搜了一下既梦的模版里，目前还没看到比这个更逼真些的

- 我觉得 以后的书 都会变成这个样子
# discuss-tts/audio
- ## 

- ## 

- ## In-browser TTS in 3 lines of code
- https://twitter.com/xenovacom/status/1716711760982319429
  - `import { pipeline } from '@​xenova/transformers';`

# discuss-comfyui/sd
- resources
  - [【SD + ComfyUI】合集 - 知乎](https://zhuanlan.zhihu.com/c_1625633809227010048)
  - [Flux.1 ComfyUI 对应模型安装及教程指南 | ComfyUI Wiki](https://comfyui-wiki.com/zh/tutorial/advanced/image/flux/flux-1-dev-t2i)

- flux-guff
  - https://huggingface.co/city96/FLUX.1-schnell-gguf/tree/main
  - https://huggingface.co/city96/FLUX.1-dev-gguf/tree/main
  - https://hf-mirror.com/city96/FLUX.1-schnell-gguf/tree/main
  - https://hf-mirror.com/city96/FLUX.1-dev-gguf/tree/main
  - 🌰 [How to Run Flux Dev GGUF Models in ComfyUI (Low VRAM Guide) - Next Diffusion _202506](https://www.nextdiffusion.ai/tutorials/how-to-run-flux-dev-gguf-in-comfyui-low-vram-guide)
  - [如何用ComfyUI运行FLUX GGUF文件模型_慕课手记](https://www.imooc.com/article/371309)

- qwen-image
  - https://huggingface.co/city96/Qwen-Image-gguf/tree/main
  - https://modelscope.cn/models/city96/Qwen-Image-gguf/files
- ## 

- ## 

- ## [m4 mac mini本地部署ComfyUI, 测试Flux-dev-GGUF的workflow模型10步出图, 测试AI绘图性能, 基于MPS(fp16), 优点是能耗小和静音 - 刘悦的技术博客 - 博客园 _202505](https://www.cnblogs.com/v3ucn/p/18593990)
- [How to Use FLUX GGUF Files in ComfyUI _202505](https://promptingpixels.com/tutorial/flux-gguf)

- 最后是10步迭代的出图效果，可以看到，精度没有下降太多，主要问题还是出图速度太慢

- ## [Flux.1 GGUF模型说明及使用](https://www.zhihu.com/tardis/zm/art/16474690938)

- GGUF 版本 是 Flux 模型的一种优化版本，专门为低显存设备设计
- GGUF 是 GPT-Generated Unified Format 的缩写，是一种高效的模型存储和交换格式。它通过量化技术（如 4 位、6 位、8 位等）压缩模型权重，从而减少显存占用，同时保持较高的生成质量。
  - 量化原理：量化通过减少模型权重的精度（如从 32 位浮点数压缩到 4 位），降低显存需求，但可能会略微影响生成质量。
  - 优势：GGUF 版本可以在低显存设备（如 6GB 显存）上运行，适合没有高端显卡的用户。
- 原始版本（如 Flux.1 Dev 和 Schnell）对显存要求较高，通常需要 16GB 或更多的显存才能流畅运行。
  - Q4 和 Q5：适合大多数用户，显存需求适中，生成质量较好。

```table
量化级别	      显存需求	 生成质量
Q2/Q3（2/3 位）	6GB	     较低
Q4（4 位）	    8GB	     中等
Q5（5 位）	    10GB	   较高
Q8（8 位）	    16GB+	   接近原始版本
```

- GGUF 版本的优势与局限​
- 优势​
  - 低显存需求：最低仅需 6GB 显存，适合老显卡或低端设备。
  - 快速生成：量化后的模型推理速度更快，适合需要快速出图的场景。
  - 高质量生成：尽管是量化版本，但 Flux GGUF 的生成质量仍然非常出色，尤其是在 8 步或更多步数的情况下。
- 局限​
  - 生成质量略低：与原始版本相比，GGUF 版本的生成质量略有下降，尤其是在低量化级别（如 Q2 或 Q4）时。
  - 不支持负提示：Flux GGUF 版本不支持负提示功能。

- ## 📌 [FLUX.1入门教程：模型资源汇总与详细说明 - 知乎 _202503](https://zhuanlan.zhihu.com/p/10106104364)
- 一般情况：完整版（fp16）需要 24G 显存才能正常驾驭，阉割版（fp8）16G 就足够，nf4 版本 8-12G 显存可正常驾驭，
  - 而 gguf 格式量化的如最小的 Q2 版本 6G 显存也能够正常驾驭，而且由于 gguf 近期展现出强劲的技术发展，充分体现降低内存需求而质量更好的特点，黑暗森林官方开始全面支持，所以 nf4 的版本将逐渐淘汰。

- ## [How well does ComfyUI perform on macOS with the M4 Max and 64GB RAM? : r/comfyui _202503](https://www.reddit.com/r/comfyui/comments/1jhifyi/how_well_does_comfyui_perform_on_macos_with_the/)
- TLDR - if you want to work linear on one image, a Mac is a huge waste of time. Maybe 25% of the speed of a decent NVIDIA PC for AI generation. 
  - However, if you know how or want to multitask, it’s easily the best system you can purchase.

- for generative AI stuff, compared with my Linux PC with a RTX 4090 - mac m4 pales in comparison. 
  - We are talking minutes vs seconds here for a 1024x1024 Flux generation. Most of it is tuned for Nivida CUDA and that is the key. 
  - Apple Silicon offers great performance for everyday computing, but its support for machine learning frameworks like PyTorch sucks butt compared to CUDA.
  - i can drive Comfui remotely from the mac with the server running on the linux pc.

- AI image and video generation require cuda cores to function properly so Apple or even AMD gpus are not recommended.

- Not well. Most local AI is still tied to having CUDA. Honestly the biggest missing link is getting Pytorch to run accelerated on Apple silicon. That will speed up most of the tasks that do CPU fallback which is where you get your abysmal performance.

- Apple has been so far behind in AI. Best just go for PC with Nvidia gpu.

- M4 Max MBP with 128 GB memory here. Let’s just say I never, ever run image gen on that machine. Even for models/pipelines that ARE supported, it’s not worth the agonizing wait.

- my Mac M4 16gb is much more slower than my old PC with the good old Geforce 3060. An Apple a day keeps the Comfyui away.

- ## 把ComfyUI工作流无缝转为MCP Tool的一款工具：Pixelle-MCP
- https://x.com/aigclink/status/1955163038035914972
  - 也就是说用自然语言即可让LLM控制ComfyUI执行复杂的生成任务
  - 自动化和批量化，LLM可以自动化执行重复性的任务，比如批量生成不同风格的图像，或者根据预设的规则自动调整参数

- ## ComfyUI 现在是不是没人学了。时间线上的 ComfyUI 大佬好像都不发新教程了 _202508
- https://x.com/hylarucoder/status/1954857846987968542
- 现在很多通用生图模型的能力已经足够覆盖很多工作流了，而且comfyUI铺天盖地的配置，看的让人头疼，我现在做的 YOOART IMAGE 都是接入的通用模型，比如gpt-4o-image、即梦、midjourney、qwen-image、imagen4 这些，普通任务都可以完成，只需要输入提示词就好
- 是不是可以这么理解，只要不是很专精的或者需要批量生成的图片，基本就告别 comfyui 了？
  - comfyui 在一些比较垂直的领域比如电商的细分场景，需要自己部署的训练的模型，批量化作业才需要它，对于大众普通人来说，随着模型能力越来越强，那么提示词就会替代越来越多的工作流，典型的就是 Chatgpt 4o、flux-kontext、即梦、这来能生图，能改图的胜任大部分，未来应该还是生图 Agent 的天下吧。
  - 在一些需要固定工作流，固定结果的场景我觉得还是需要comfyui，类似传统的PS，AE 吧，现在普通大模型会占据的应该是类似美图秀秀，剪映这种简单化的生态位，但是这种生态位人数多，但是comfyui的商业价值，其实还是不小的，专业重活儿还是得靠它。

- 新的开源模型很大，运行门槛过高，而且效果没办法打过好的闭源模型

- 我一直认为工作流是过渡产物，注定被模型干掉

- 感觉comfyUI很麻烦，租个云电脑配置半天还不如直接花钱在平台生图 生视频

- https://x.com/hylarucoder/status/1955106887407653234
  - 汇总一下大家的观点, 早期 ComfyUI 火是因为生图必须「会搭工作流」
  - 现在 通用模型就能解决 80% 的场景。搭节点的边际价值下降，而 ComfyUI 生态商业化分叉进一步拉大了用户和开发者学习和维护成本
  - 而开源世界里面又有很多一键化套件，ComfyUI 进一步成为了牛夫人。。。。
# discuss-image
- ## 

- ## 

- ## 

- ## 

- ## [Qwen image 20B is coming : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mhf0kl/qwen_image_20b_is_coming/)
- ComfyUI is just a simple visual programming language with custom node support. 
  - If you want a simpler approach use some UI for it like https://github.com/mcmonkeyprojects/SwarmUI and if you need more control no need to pack everything into a workflow just use Krita AI or sth...

- ## 有分析称，GPT-4o 图片生成效果这么好是因为采用了自回归模型（autoregressive model）而不再是扩散模型（diffusion model）。
- https://x.com/jason2be/status/1905834259547361645
  - 如果真是这样的话，那我将再次称 DeepSeek 为神，因他们一月份开源的 Janus-Pro 图像生成模型就是自回归框架，虽然目前效果还待提升，但技术路线选择上相当于又踩对了一次。
- 这跟deepseek 没啥关系，基于transformer的图像生成22年23年就开始有了，也是一个研究热点，因为大家都想要一个统一的端到端模型既能生成文字也能生成图像。别说图像，openai 的sora 也是基于transformers
  - 是的。DeepSeek 的 Janus-Pro 创新是将自回归（AR）和扩散模型结合，但这也是有其他团队在研究的。DeepSeek 选 AR 和 GPT 选 Transformer 一样，其实都是行业技术演进的一部分。虽然是独立事件，但也暗示一些必然。
- 早就是研究热点了，包括nips24的best paper就是给了自回归的视频生成

- 机器学习就那几种模型，论文都是公开的，什么叫踩对一次？

- ## 揭秘一下一键大胸技术原理，顺便请教一下有没有更好的解决方案:
- https://twitter.com/moeimiku/status/1769285829586022574
  1. 通过 SagmentAnyThing + Grounding-DINO识别乳沟和胸部，然后做叠加遮罩~  
  2. 利用StableDiffution对遮罩区域做基于原图的重绘
  - 现在遇到的问题是，灵敏度默认0.3的情况下不能覆盖所有图片：有的图片识别不出来，需要降低到0.25. 有的图片把全身都识别出来了，则需要增加灵敏度。
- 可以加个遮罩层区域抹涂编辑功能，既能解决准确性的问题，又会大大增加产品的趣味性和粘性。
  - 靠谱，还想做一键穿丝袜功能
- 这个通过拖拽构建系统的框架是什么？
  - comfyUI 关注我回头出教程

- ## [how to image generate locally? : r/ollama _202505](https://www.reddit.com/r/ollama/comments/1kjhul8/how_to_image_generate_locally/)
- r/StableDiffusion would be the place to ask. There are a couple different UIs like ComfyUI, Fooocus, Forge, and SwarmUI that can be used to do local generation.

- ## [How to generate text to image with ollama? · Issue · ollama/ollama-python _202409](https://github.com/ollama/ollama-python/issues/280)
- You need to know what's a LLM and how it work: llm stand for large language model, which basically mean it a model made to understand language, and can reply with similar language, understandable for human.
  - what you're trying to do is to have this llm generate an image, without being train on generating image but only generating text... So its impossible to have the model nativly provide you an image by its own.
  - If you're looking to have a chatbot capable of chatting and generating image, you must have two AI, one LLM and one made to generate image (like stable diffusion, etc), if you have a good computer, you can run both locally

# discuss-designer/builder
- ## 

- ## 

- ## ✨ we're bringing vision to Bolt.new _202502
- https://x.com/boltdotnew/status/1892620446106886396
  - Bolt now sees your app exactly like users do, enabling faster, more precise edits pixel by pixel (& fewer tokens!)
  - The Visual Inspector works across all web frameworks (React, Vue, Svelte, Next & others) and mobile apps (Expo).

- Does this send a screenshot with html2canvas so the app can see any layout issues and you don’t need to take a screenshot? Or does it just send the raw html that you click on.
  - it's using https://github.com/qq15725/modern-screenshot to send images!

- I built this in 25 minutes using MCP tools
# discuss-ai-example 🌰 
- ## 

- ## 

- ## 

- ## Google Gemini 的 StoryBook 功能用了 20+ 个 Agents，其中 6 个是专门为故事书功能设计的核心 Agents
- https://x.com/iguangzhengli/status/1953770970680000637
  1. Writer - 负责创作故事内容
  2. Storyboarder - 分镜和插图说明
  3. NewStorybook - 核心 Agent
  4. IllustratorSingleCall - 插画导演
  5. Animator - 动画导演
  6. Photos - Google Photos 集成
- StroyBook 的 System Prompt 很容易逆向出来，估计现在根本没有设防(后面看到后估计马上要加过滤了)

- 各国文学的叙事风格有很大差异，不知道这些Agents是如何实现的。
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 用可灵AI 让专辑封面动起来
- https://x.com/Nin19536/status/1804523356311765400
  - 特别喜欢 Aimer！！ 她的专辑封面基本都是超现实风格, 特别适合 AI 图生视频
- 感觉桌面、移动端有一个动态壁纸小工具的机会

- ## 这几天在研究Stable Diffusion。需求是把客户做的衣服穿到AI生成的模特身上。
- https://twitter.com/felixding/status/1768511354208739692
  - 如果用一张衣服的照片+ControlNet，结果的细节总是不够，因为本来就只用了一张照片。
  - 如果用多张衣服的照片训练个Lora，结果就变得不可控了，比如衣服的细节总是和真实情况不完全一样。
- 细节还原很难，看看这几个方案呢
  - 1、OOTDiffusion
  - 2、一张参考服装、一张参考动作
  - 3、OutfitAnyone，未开源，可以在线用
- 我试过了。唯一可行的技术方案是用身模实拍，用sd生成人头和背景然后组合起来。最大的BUG在于同样的输入条件，语言输入的扩散模型，结果一定会有至少15%的偏差。用图生图的话，流程复杂，边缘结合部还处理不好。技术上暂时无解。
- 你用ControlNet了吗？我用Inpaint Anything+Segment Anything，然后丢给ContrlNet，这样似乎还行，但是就会遇到我说的第一个问题。
  - ControlNet我玩得透透的，这是SD最有价值的插件，本意就是用来解决结果偏差问题的。透过骨骼、边界、边缘三层约束，可以最大化的解决结果偏差问题。但也只能缩小结果偏差。只要无法做到可复制、可控制，就没有产量，无法成为可规模生产的工具，这个我早就看穿了。

- ## #DALLE3 ChatGPT 输出的风格似乎很稳定，太美了！
- https://twitter.com/lencx_/status/1721331238219506111

- ## 🆚️ 用 Midjourney、DALL-E 3、Adobe Firefly 2 还是 Stable Diffusion？
- https://twitter.com/FinanceYF5/status/1716288468186431811
  - 在过去的 6 个月里，作者在所有 4 个平台上生成了 50, 000 多张图像。

- ## Generated Photos：这个网站提供了10万个不存在的人的照片，这些照片全部由AI生成。
- https://twitter.com/xiaohuggg/status/1675480188023615489
  - 你可以在任何地方免费使用它们，而不必担心任何法律问题。这些照片符合GDPR和CCPA标准，没有版权、没有肖像权。
  - 同时他还有人工生成的面孔库，共有2675894张人脸照片。还有多种工具和数十万张多样化的数据集。

- ## 开个 thread 来做个人人都难懂的 AI 作画科普。
- https://twitter.com/haoel/status/1632211302356783104
- 目前主要流行的AI作画有，OpenAI的Dall-E2, Google 的 Imagen，Midjourney，有还Stability AI 公司开的 Stable Diffusion 等等。
  - 它们都是2022年才出来的，无一例外，全部都是基于 Diffusion 算法模型，这个算法的原理其实并不复杂

- 💡 最后说一下Stable Diffusion，他使用了一种图片压缩算法可以大规模的减少训练的内存和时间，在工程上可以用更少的GPU和时间来计算更大量的数据，于是让“大力出奇迹”成为了可能，
  - 因为开源，所以，它的社区是非常活跃的。开源和封闭的竞争永远都在，OpenAI 和Stability AI之间就像苹果和安卓

- Diffusion算法需要先找一堆高质量的图片，训练就是对每张图片一步一步的按一种公式（高斯噪声公式）来加噪点，直到整张图片变成一个完全噪点的图像（就像电视的雪花点），把所有的步骤都保存下来，然后用神经网络的方式来反向学习如何从一个完全是噪点的图像变成一张高清的图
  - 一旦这个模型产生，机器就可以通过“噪点”来预测图形，所以，整个绘画的过程就是用一组随机数（随机的噪点）来预测会是一个什么样的画。很令人惊讶吧，AI就是从一堆乱七八糟的随机数中来画画的。这种个算法很机器，就是以大力出奇迹，但牛逼的地方是，可以产生清晰度和细节度巨高无比的图片
- 这个过程需要依赖于几个事，一个是训练的图片，一个初始化的随机噪点，还有就是 Prompt 的预测路径，整个过程非常地机械，而且这个模型也不保证能生成让人觉得舒服的图片，所以需要各种人为的调参，并需要人通过在生成的图片中选择自己喜欢的图片后再度生成，类似于ChatGPT用上下文来调整内容
- 💡 所以，像Midjourney这种通过聊天机器人来让人选择最喜欢的图片，其实就是让人来告诉机器哪些随机数，哪些预测路径，哪些Prompt更靠谱可生成更好的图片，在用户生成图片的同时让用户来反哺了AI 模型，而生成出来的图片又可以成为下一轮的图片训练集，于是，AI以后就再也不需要使用人类的图片
- 再说一下 **Prompt**，这是一种Transformer语言模型，它接受文本提示并产生Token，
  - Stable Diffusion 以前使用的是 OpenAI的CLIP，但去年11月切到了OpenCLIP，使用了3.5亿的参数，而CLIP只有6千万的参数，
  - Prompt对高质量的图片的生成有非常大的影响因素，我认为这是一种未来的更接近自然语言的编程语言
