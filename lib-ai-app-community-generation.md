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
# discuss-tts/audio
- ## 

- ## 

- ## In-browser TTS in 3 lines of code
- https://twitter.com/xenovacom/status/1716711760982319429
  - `import { pipeline } from '@​xenova/transformers';`

# discuss-image
- ## 

- ## 揭秘一下一键大胸技术原理，顺便请教一下有没有更好的解决方案:
- https://twitter.com/moeimiku/status/1769285829586022574
  1. 通过 SagmentAnyThing + Grounding-DINO识别乳沟和胸部，然后做叠加遮罩~  
  2. 利用StableDiffution对遮罩区域做基于原图的重绘
  - 现在遇到的问题是，灵敏度默认0.3的情况下不能覆盖所有图片：有的图片识别不出来，需要降低到0.25. 有的图片把全身都识别出来了，则需要增加灵敏度。
- 可以加个遮罩层区域抹涂编辑功能，既能解决准确性的问题，又会大大增加产品的趣味性和粘性。
  - 靠谱，还想做一键穿丝袜功能
- 这个通过拖拽构建系统的框架是什么？
  - comfyUI 关注我回头出教程

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
