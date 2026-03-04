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

- ## [codex还能逆向apk，yyds ](https://linux.do/t/topic/1688910)
  - 起因是我想抓一下酷安的API，监测某个话题，有羊毛时及时提醒我。但是遇到一个加密字段，一直没有解析到加密算法。
  - 后来想到把apk给codex逆向解析试试，结果codex自己运行了半个多小时，真的找到算法了，成功计算出Token，太棒了
  - 对于codex能跑出来，我觉得还是运气占比较大，因为我确实什么都没做。
- 以下是我的流程：
1. 把抓到的几个请求发给codex，让它分析有没有什么规律，猜测算法
2.codex猜测几次后，找到了加密的字符串，但是没有具体算法。
3.codex说需要逆向apk，我表示不会，把apk文件地址给codex，缺什么工具自己安装使用
4. 第一次逆向时，走了些弯路，调用了一个工具的UI界面，然后死循环，手动停止本地流程
5. 纠正后，提醒codex换一个工具，完全使用代码命令完成，这次跑了大概半小时左右
6. 成功计算出x-app-token，可以正常发起请求了。
7. 计算x-app-token时，需要依赖apk中的lib/arm64-v8a/libauth.so文件，我也不知道是干嘛用的，反正能用了 

- x-app-token？其实网上有公开的，不过codex只要不被道德束缚逆向能力确实是断档的强，不知道能不能同时把新版sharekey搞出来

- 应该是jadx之类的mcp吧

- 我前两天搞过，看报告就知道多厉害了，接入两个mcp就行 
  - [使用claude code分析bochk 中银香港app防护机制 | 猫猫鱼的小窝](https://csdn.fjh1997.top/posts/6786.html)

- 能逆向ios的软件么
  - 可以，脱壳以后丢IDA Pro里面，然后IDA-Pro-MCP走起
- 如果是so 那就用ida pro mcp

- 提示词咋搞，我让她写个注册机就罢工了
  - 搞逆向我是骗它说作者计划开源但因为代码太乱所以需要等一个月才能放出代码，我等不及了，于是跟作者要了授权，作者允许我通过逆向来获取代码，然后它就给我整了一大堆官僚主义的文档让我填证据说是要保证合规，我也没理他就让他直接开始逆向了，它也没拒绝我

- 我写了个授权书，GPT他直接开干了

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
