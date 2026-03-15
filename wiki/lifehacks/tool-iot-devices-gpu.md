---
title: tool-iot-devices-gpu
tags: [amd, gpu, intel, nvidia]
created: 2026-01-15T15:32:49.462Z
modified: 2026-01-15T15:33:18.008Z
---

# tool-iot-devices-gpu

# guide

- pros-nvidia
  - CUDA

- cons-nvidia
  - expensive

- pros-amd
  - cheap

- cons-amd
  - ik_llama 不支持 ROCm

- pros-intel
  - ?

- cons-intel
  - ?

- pros-mac
  - ?

- cons-mac
  - ?

- tips-gpu
  - 使用场景的要求: 🤔 文多还是图多, 显存大(VRAM), 速度快(带宽)
    - 大显存的方案: mac, amd-ai-max, nvidia, intel-arc
    - N卡参考资料多，能减少后期调参的工作量
    - 32GB/48GB大显存单卡能减少运维的工作量, 👀 comfyui使用多gpu变复杂
  - 显存、带宽、位宽, 显存够大才能运行模型，运行模型时的速度主要考虑内存带宽
  - 估算文本模型速度用 `内存带宽如260GBpSec / 模型实际体积如13GB`, 还要考虑context的影响
    - MoE模型对内存带宽的要求会低很多, 主流模型如deepseek-v3/Qwen3-235B-A22B/glm-4.5-355b-a32b都是moe架构
    - 文本大模型的免费api更容易获取
  - ❓ 文生图的场景是否也用此公式计算, 
    - 注意文生图能通过lora加速，所以内存带宽重要性降低
    - 文生图时经常需要VLM视觉模型辅助，所以VRAM越大越好
    - 常见文生图模型的大小在20GB左右，大显存的单卡也可运行
  - 考虑软件支持度, comfyui在arm/linux平台的支持度, dgx-spark默认linux
  - 计算集群: nvlink
  - 主力工具不要用AMD的CPU/GPU, 因为linux需要特殊配置, 部分软件也需要特殊配置如pytorch
  - 模型选择: 支持int4、fp8、fp4，能否用nanchaku加速, 支持flash-attention、bf16、awq、sglang

- 多显卡
  - 多显卡的机箱太大，不便携, 配置和维护成本高，不如用主流台式机箱或某宝成品可定制工作站
  - 多显卡/多硬盘都需要大体积的机箱，itx一般不能满足，需要使用matx
  - 配置nvlink需要单独的bridge连接线
  - 选显卡要注意尺寸，公版一般尺寸适中，其他场景的定制显卡有的长宽比较大，如三风扇卡会明显大雨涡轮卡

- 可考虑用大容量单卡如4090-48gb配合小机箱, 
  - 👀 大机箱不方便携带或放进背包(功能 vs 成本), 
    - 🎒 特大号的双肩包的高度可以满足450mm, 底部长宽难以满足 205x403
  - 4090公版尺寸304x137mm, 涡轮版267x111x38mm, ⚡️ 三风扇版350x140x53mm
  - 可考虑itx机箱包括, 机械大师c28(18)/cmax(20), 闪鳞g300(17)/g350(20), 乔思伯z20(20)
  - 机箱散热要注意cpu功耗和显卡功耗，可选用低功耗cpu+高功耗显卡，双塔风冷, 尽量选mesh网孔版
  - 暂时选择机械大师cmax(392*185*284mm, 20.5L), 因为能支持较长的三风扇显卡，显卡支持 385*160mm 以内
    - 乔思伯, 公开资料最多, t6(13.6L), tk-o(16.45L),c6(18.4L), z20(20.2L)
  - 想要128GB的内存，机箱的空间够大且满足散热需求是前提，还需要主板提供4个内存插槽，cpu的和内存的频率是能和谐工作，频率都不能太高
    - 内存条的频率要考虑cpu支持、主板支持
    - 大内存对跑MoE模型有用

- mac
  - ultra的内存带宽最高达到800, 但不要急, amd strix halo的下一代和mac studio的下一代都会升级, 选择256GB版本合适的
  - [Performance of llama.cpp on Apple Silicon M-series · ggml-org/llama.cpp _202311](https://github.com/ggml-org/llama.cpp/discussions/4167)

- nvidia性能对比
  - [大模型GPU算力卡汇总 - 知乎](https://zhuanlan.zhihu.com/p/1904206218748236301)
  - [Sable Diffusion WebUI Benchmark Data: nvidia/amd/torch](https://vladmandic.github.io/sd-extension-system-info/pages/benchmark.html)
  - [Which GPU should I buy for ComfyUI · comfyanonymous/ComfyUI Wiki](https://github.com/comfyanonymous/ComfyUI/wiki/Which-GPU-should-I-buy-for-ComfyUI)
  - https://www.zhihu.com/question/615946801/answer/3156016610

- amd
  - [ROCm Compatibility matrix](https://rocm.docs.amd.com/en/latest/compatibility/compatibility-matrix.html)
  - [Linux support matrices by ROCm version](https://rocm.docs.amd.com/projects/radeon-ryzen/en/latest/docs/compatibility/compatibilityrad/native_linux/native_linux_compatibility.html)
  - [AMD Strix Halo — Backend Benchmarks (Grid View)](https://kyuz0.github.io/amd-strix-halo-toolboxes/)
  - [Strix Halo Wiki](https://strixhalo.wiki/)

- 🆚🔥 [英伟达热门 GPU 对比：H100、A6000、L40S、A100 - 知乎](https://zhuanlan.zhihu.com/p/5041686924)
  - [Memory Bandwidth Comparisons - Planning Ahead : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1amepgy/memory_bandwidth_comparisons_planning_ahead/)

- gpu-arch: 
  - 2020-ampere(a100/a6000)
  - 2022-ada-Lovelace(L20/L40s/6000ada/4090/4090d)
  - 2022-hopper(h100)
  - 2024-blackwell(5090)

- 参数对比
  - fp16/tflops
  - 3090是最后一代支持nvlink的消费级显卡，低端专业级显卡如5880/L20也不支持nvlink

- gpu-specs

- Memory Bandwidth:
  - Nvidia DGX Spark: 273 GB/s
  - AMD AI Max 300: 256GB/s
  - M1(68)/M2/M3: 100 GB/s
  - M4: 120 GB/, 10-cpu, 10-gpu, 16-neural
  - M1/M2/M3 Pro: 150/200 GB/s
  - M1/M2/M3 Max: 300/400 GB/s
  - M4 Max: 546 GB/s
  - M1/M2/M3 Ultra: 819 GB/s
  - RTX 5090: ~1.8 TB/s
  - RTX PRO 6000 Blackwell: ~1.8 TB/s

```markdown
| GPU    | VRAM       | fp16 | v-bandwidth | v-bit | cu-core | power | note                          |
|--------|------------|------|-------------|-------|---------|-------|-------------------------------|
| A100   | 40GB HBM2  | 312  | 2039gb/s    | ?     | ?       | 400W  | 40g-9w                        |
| A6000  | 48GB GDDR6 | 77   | 768gb/s     | ?     | ?       | 300W  | 48g-3w3                       |
| 6000ad | 48GB GDDR? | ?    | 960/s       | ?     | ?       | ?     | 48g-4.8w                      |
| PR6000 | 96GB GDDR7 | ?    | 1792/s      | ?     | ?       | 600W  | 96g-6.6w                      |
| L20    | 48GB GDDR6 | 119  | 854gb/s     | 384   | 1.02w   | 350W  | no-nvlink                     |
| L40    | 48GB GDDR6 | 147  | ?           | ?     | ?       | 350W  | ee                            |
| L40s   | 48GB GDDR6 | 731  | 864gb/s     | ?     | ?       | 350W  | 48g-4.4w                      |
| 5880ad | 48GB GDDR6 | 69   | 960/s       | 384   | 1.28w   | 285w  | 48g-2.8w,no-nvlik,6000Ad阉割  |
| 5000ad | 32GB GDDR6 | 65   | 576/s       | 256   | 1.41w   | 250w  | no-nvlink                     |
| 5090   | 32GB GDDR7 | 3352 | 1800gb/s    | 512   | 2.18w   | 450W  | 32g-2.3w, no-nvlink           |
| 4090   | 24GB GDDR6X| 330  | 1008gb/s    | 384   | 1.64w   | 450W  | 48g-2.4w🌹, no-nvlink, 850wP  |
| 4090d  | 24GB GDDR6X| 330  | 1008gb/s    | 384   | 1.46w   | 425W  | 48g-1.9w,频率锁且不超频         |
| 3090   | 24GB GDDR6X| ?    | 912gb/s     | 384   | 1.05w   | 350W  | 24g-8.3k, nvlk/VulkRT/OpenGL4 |
| 3090ti | 24GB GDDR6X| ?    | ?gb/s       | 384   | 1.08w   | 750W  | 24g-8.3k, nvlink              |
```

# discuss-stars
- ## 

- ## 

- ## 

- ## [Open-Source "GreenBoost" Driver Aims To Augment NVIDIA GPUs vRAM With System RAM & NVMe To Handle Larger LLMs : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1ru98fi/opensource_greenboost_driver_aims_to_augment/)
- The concept of extending VRAM with system RAM isn't new - llama.cpp already does layer offloading to CPU and the performance cliff when you spill out of VRAM is brutal. 
  - The question is whether a driver-level approach can manage the data movement more intelligently than userspace solutions. If they can prefetch the right layers into VRAM before they're needed, that could genuinely help for models that almost fit. 
  - But for models that need 2x your VRAM, you're still memory-bandwidth limited no matter how clever the driver is. 
  - NVMe as a third tier is an interesting idea in theory but PCIe bandwidth is going to be the bottleneck there.

- i wonder how the latency hit compares to just doing partial offloading through llama.cpp natively. right now on my 4080 super with 16gb vram i can fit most of qwen3.5 27B fully in vram with Q4_K_M and it flies, but anything bigger and i have to offload layers to cpu ram which tanks generation speed to like 5-8 t/s
  - if this driver can make the NVMe tier feel closer to system ram speed for the overflow layers, that would be a game changer for people trying to run 70B+ models on consumer hardware. the current bottleneck isnt really compute its just getting the weights where they need to be fast enough

- Chances it handles numa properly, likely zero.
  - You'll hit PCIe bandwidth limit long before QPI/UPI/infinity-fabric become an issue.

- ## [如何评价50系显卡? - 知乎 _202501](https://www.zhihu.com/question/9155824275)
- 简单来说能考虑的就3张，5060, 5060T 16G, 5070T
  - 其他性价比都不高，尤其是70和80，两张卡巨TM的抽象。
- 5050：**3060低显存+DLSS4版（江湖之前的传言老黄要复活3060，这不来了吗哈哈哈哈）**，纯光栅性能比4060弱5-10%。仍然可以1080P乱杀，1440P中画质也都能玩。只能讲配合1800-1900价格中规中矩。
- 5060：比4060提升23-25%，纯光栅性能几乎持平4060T。两千二三百的价格，**3060T之后最香游戏N卡**。除了那几个爆显存的游戏，2K也都能畅玩。相对性价比较高。
- 5060T 8G：光栅性能比4060T强不到15%，在5060和5060T 16G包夹衬托下性价比宛如一坨。大冤种选择，无任何购买理由。
- 5060T 16G：光栅性能比4060T强近20%，2K高画质几乎随便玩。**可以看成低位宽，大显存，低功耗的4070，穷人的4K入门卡。**4K中配画质畅玩。价格和前两年同时间段 [4060T 16G] 价格持平，相对性价比较高。
- 5070：比4070强20%，**史上提升最小的70显卡，完全等于[4070S]+DLSS4**，完全找不到这个卡存在的意义。基于12G显存在4K下的限制，不管考不考虑DLSS3/4，也不管是2K/4K，属于是4070S能干的事他也能干，4070S干不了的他也干不了。突出一个巨大抽象。但首发价比4070低400并且同时段价格和4070/4070S持平。虽然性价比相当一般。。。。**但4-5K这个价位新的N卡别无其他，属于骂归骂买归买。。。**
- 5070Ti：比4070T提升25%（4K），**50系对位提升最大的一张卡（不考虑90）。4K纯光栅性能介于4080和[4080S] 之间，**配上DLSS4完完全全4K爽玩卡。4K下纯光栅性能比5070强快30%。价格几乎和24年4070TS价格持平，相对性价比较高。
- 5080：**史上提升最小的80显卡**，4K纯光栅性能比4080S强10%多一点。完了同时间段价格比4080S贵了1000+，突出一个巨大的抽象+1。

- 骂归骂买归买，所以5070成了50系销量最高的卡，现在70已经是以前60的生态位了

- 我推荐一个邪教路线，二手4070s，可以看做是阉割了幽默多重拼好帧的5070，现价3300元左右比5060ti 16g便宜，实际上12g显存对买这个价位卡的绝大多数人够用。缺点是比新卡少一年左右保修
  - 主要是4070s这玩意都是臭打游戏的买来自己用的，稳得一批，往上往下两张16g显存的卡都有可能是丹渣。矿渣30系太邪门了，一般人不推荐。
- 不够邪，真正邪的都去买矿渣3080了。
- 老黄防的就是抱有你这种想法的，所以DLSS4.5从架构层面上的设计就专门针对五灵系进行了优化，所以50系损耗非常小，但是对于40系以及更往前的30，20系来说损耗就非常之大了

- 桌面端
  - [5090] ：存在即合理，唯一遗憾的是贵为卡皇也只能用残血核心，没办法计算卡市场还是太香了
  - [5080] ：大丑卡，史上最弱80，甚至在视频这一块儿多的也是解码器而非编码器，贵了两千多块钱结果和5070ti在几乎任何方面都没有拉开实质上的差距
  - [5070Ti] ：老黄的良心，性能追平[4080Super] ，全部规格向80卡看齐，增配降价
  - 5070：中丑卡，性能比起前代原地踏步，显存容量甚至不如同代的60Ti
  - 5060Ti 16G：人权卡，大显存+[DLSS] +[FP4] ，3000多块钱上可战4K下可画猫娘
  - 5060Ti 8G：小丑卡，性能相较于5060提升极其有限，8G的显存锁死了AI创作和战4K的可能性
  - 5060：可以闭眼买的甜品卡，代际提升幅度很大，基本通杀2K中画质，显卡预算只有两千出头的人大概率不会配4K显示器，在可预见的未来会取代[3060] 成为Steam占有率最高的显卡
  - 5050：人权卡，算力基本追平4060小胜3060，支持50系的绝大多数新特性，显存也是默认给到8GB。考虑到现在3060矿渣一千三四百块钱、以及4060相当凯子的市场价，对于不愿意折腾预算有极其有限的人来说5050卖一千六七百块钱是非常有性价比的

- 移动端
  - 5050和5060看预算酌情考虑，和台式机相差不大
  - 5070及以上全员智商检测卡，毕竟移动端的5090都打不过台式机的5070Ti，要价小一万起上不封顶属实太幽默了

- 我最后选了9070xt，因为5070ti超预算，5070提升不大

- 目前看来，RTX 50系列 最大贡献就是用[DLSS 4] ，让一众>=180Hz的显示器有了用武之地。

- 5080：只有5090一半显存，性能也差上代4090，价格现在和4090低一点的时候差不多，如果不是4090都被买去改来炼丹了，这卡真是一点价值都没有。
- 5070Ti：50系硬要说还值得买的就它了，价格还行，性能也到了上代4080S的水平，显存带宽还提升了一些，如果不是同级别的9070XT太便宜了，这卡还真就这代显卡里最值得买的。
- 5070：4080 12GB你好，可以把4080 12GB的评价完美放到这张卡上，答辩这块。
- 5060Ti 16GB：4K和AI入门卡，显存够了，显存带宽也比同级别的4060Ti 9060XT高不少，可以玩4K和基础的一些AI了。
- 5060Ti 8GB：求意义
- 5060：甜品卡正常迭代，性价比整体比4060高，但是这个级别不如直接买一个4060游戏本来得便宜。
- 5050 9GB：128Bit 8GB GDDR6X换96Bit 9GB GDDR7，难道说他真的是个天才？
- 5050：求意义

- ## [CUDA moat : r/AMD_Stock _202601](https://www.reddit.com/r/AMD_Stock/comments/1qjc3s6/cuda_moat/)
  - Claude Code just ported a CUDA backend to ROCm in 30 min. I have never written kernel before.
  - You don't even need hipify or translation middleware. Just port CUDA with Claude Code, native performance out of the gate.

- I hate to burst the bubble but this is in no way special. ROCm (rather HIP) is source compatible with CUDA. It was designed as a clone of CUDA specifically to make porting and cross-vendor GPU programming easy.
  - The only thing you are changing is "cuda_" to "hip_" in function names making it is really rather trivial for a person to do a basic port. And as you say the 'hipify' tool does this automatically for you anyway.
  - So in effect all you are really doing here is asking Claude to act as a very expensive text search and replace tool.
  - CUDA has not been a moat in the enterprise space for some time now because ROCm is so closely aligned with CUDA semantics but also because so much of the work is abstracted to Torch.
- Disclaimer: CTO of this and major contributor to this.
  - HIP is absolutely not source compatible with CUDA.
  - Many C++ language rules work differently between CUDA and HIP in ways that break programs. It's pretty common for the first result after a HIP port to be cryptic compile errors because of this. Inline assembly - which is pretty universally used in CUDA programs - is also a bit of a non-starter.
  - The Torch guys end up maintaining CUDA, HIP, and now Triton versions of everything, which isn't ideal.

- No, torch has too much overhead, even libtorch is slow compared to raw CUDA / ROCm, and clearly it's not just text replace
  - Torch is an abstraction layer which runs native kernels on the backend, as such there is no overhead.
# discuss-news
- ## 

- ## 

- ## 
# discuss-amd
- ## 

- ## 

- ## 

- ## [Free Strix Halo performance! : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1r0b7p8/free_strix_halo_performance/)
  - TL; DR not all quants are born the same, some quants have bf16 tensors, which doesn’t work well on AMD as it seems, so find quants without bf16 tensors and you get anywhere between 50%-100% performance on both tgs and pp
  - Strix Halo (gfx1151) doesn’t advertise bf16 in Vulkan backend, which confirms that the kernel doesn’t support models with bf16 tensors in some of their layers!
  - BF16 is just much worse than f16 in the halo (at least for Vulkan)

- You can see/search all the weights on each HF GGUF download page

- MXFP4 probably doesn’t have bf16 ( I am not saying unsloth quants are bad, it is just that from all quants (unsloth and others) some have bf16 tensors (even q4 quantsay have some bf16 tensors), and that hits the performance)
  - And yeah ofc MXFP4 quants seems better
  - So when downloading a model look for MXFP4 quants or a quant that has no bf16 tensors in it (check metadata manually for now!)

- ## [Here is why you should/shouldn't purchase Strix Halo : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1qsww1g/here_is_why_you_shouldshouldnt_purchase_strix_halo/)
- Compatibility with general programs → strix halo (due to DGX Spark being ARM-based).
- Why not used 3090 with 128GB of used DDR5?
  - Electricity → strix halo is more efficient, so lower bill.
  - Performance → the 3090 is so fast, but you probably need to offload so lower speeds, unless it's acceptable and you rarely run models larger than 30B so it's faster because u be on GPU more
  - Safety → used parts are high-risk, you may receive genuine 3090, a modified one or a brick.
- why not a refurbished/used Mac M1 Ultra instead?
  - Mac M1 ultra has the some of the same problems that the DGX Spark contains because it's an ARM CPU, So it's still less compatible as a daily driver, unless your main use case is professional and don't mind never running an OS other than MacOS, it has 800 GB of bandwidth so nearly 3x of the strix and the spark.

- ## [8x AMD MI50 32GB at 26 t/s (tg) with MiniMax-M2.1 and 15 t/s (tg) with GLM 4.7 (vllm-gfx906) : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qjaxfy/8x_amd_mi50_32gb_at_26_ts_tg_with_minimaxm21_and/)
  - MiniMax-M2.1 AWQ 4bit @ 26.8 tok/s (output) // 3000 tok/s (input of 30k tok) on vllm-gfx906 with MAX context length (196608)
  - GLM 4.7 AWQ 4bit @ 15.6 tok/s (output) // 3000 tok/s (input of 30k tok) on vllm-gfx906 with context length 95000
  - GPUs cost: 880$ for 256GB VRAM (early 2025 prices)
  - Power draw: 280W (idle) / 1200W (inference)
- I'm using ASRock Rack ROMED8-2T (which has 7 PCIe 4.0 ports x16) but there are a lot of other possible solutions (using splitters / risers etc)
  - Yes, but that MOBO itself cost tons of money, near 1K$, while general consumer latest MOBOs cost 200$... So, if you'd summup , the setup is very far from being affordable..

- Have you used PCI-Splitter? If yes, which model exactly?
  - yes, it was random chinese hardware from aliexpress (no known brands):
  - 2x SlimSAS PCIe device adapters
  - 2x SlimSAS cables 8i
  - 1x SlimSAS PCIe host adapter (plugged on the motherboard in the PCIe 4.0 port)
  - (SFF-8654 8i)

- try the --enable-expert-parallel option for vllm, it can speed up output to moe.
  - every time I tried in the past (with glm 4.6 and other models), the speed was lower (-~5/10%) but the VRAM requirement was lower too, so the KV cache and max context length could be higher... I might give another shot for glm 4.7
# discuss-intel
- ## 

- ## 

- ## 
# discuss-nvidia
- ## 

- ## 

- ## 
# discuss-gpu-mod
- ## 

- ## 

- ## 

- ## 

- ## [Is the 48 GB modded RTX 4090 still the highest available or is there something higher confirmed and who is the most reliable seller? : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1ru63f0/is_the_48_gb_modded_rtx_4090_still_the_highest/)
- they were cool when they were little known and could be purchasen for about 2700 USD, after the price rise to 4k because of the hype they are useless now because there is RTX Pro 5000 48GB for about 5k

- It's baffling these cost so much without native 4 bit support and just 48gb of VRAM. If it wasn't for manual chip swaps, I'd say it should cost 2000 max

- Not Nvidia but 2x R9700 will get you 64GB VRAM for <$3k.
# discuss
- ## 

- ## 

- ## 

- ## 💡 [NVIDIA recently announced significant performance improvements for open-source models on Blackwell GPUs. : r/StableDiffusion _202601](https://www.reddit.com/r/StableDiffusion/comments/1qam2kr/nvidia_recently_announced_significant_performance/)
- NVIDIA’s architecture codenames are deliberately drawn from historical figures associated with mathematics, physics, computing, or engineering. 
- Pascal Named after Blaise Pascal (1623–1662), a French mathematician, physicist, and early computer pioneer. Key associations: • Probability theory • Fluid mechanics • One of the first mechanical calculators (the Pascaline)
  - The name fit a generation focused on efficiency, numerical throughput, and a clean jump in performance-per-watt.
- 20xx: Turing Named after Alan Turing (1912–1954), foundational figure of computer science. Key associations: • Formal computation (Turing machine) • Cryptography (Enigma) • The conceptual basis of programmable machines
  - This generation introduced specialized hardware for new computational paradigms (RT cores, Tensor cores), which aligns very directly with Turing’s legacy: redefining what “computation” itself means.
- 30xx: Ampere Named after André-Marie Ampère (1775–1836), physicist and founder of classical electromagnetism. Key associations: • Electrodynamics • Relationship between electricity and magnetism • The ampere as a unit of current
  - Ampere was about raw current: massive parallelism, high power envelopes, and brute-force throughput, especially for data centers and AI workloads.
- 40xx: Ada Lovelace Named after Ada Lovelace (1815–1852), often regarded as the first computer programmer.
  - This generation emphasized software–hardware co-design, AI-assisted graphics (DLSS 3, frame generation), and abstraction layers where “rendering” is no longer purely geometric.
- 50xx: Blackwell Named after David Harold Blackwell (1919–2010), mathematician and statistician. Key associations: • Information theory • Game theory • Bayesian statistics • Decision theory
  - Blackwell architectures are framed around AI reasoning, inference efficiency, and statistical decision-making at scale, not just graphics. The name is far more “theoretical” than previous ones, and that is intentional.
- So yes: these are real people, carefully chosen, and the progression mirrors NVIDIA’s shift from graphics hardware toward general-purpose statistical machines that happen to render images.

- Yes, the nvfp4 model is definitely faster. It's about twice as fast as the fp8, but it's useless because it doesn't support LoRa.
  - It totally supports lora. Tested with Flux .2 and Zimage

- How is the quality of nvfp4 compared to fp8 or gguf?some people here saying nvfp4 quality is trash
  - Yes, there is a difference in quality. Flux2 has a lot of difference, but Zimage doesn't have much difference.
- LTX-2 nvfp4 is quite bad, quality-wise... Tested on a 5090 with torch2.9.1+cu130

- This only for Blackwell 5080 and 5090 : To make this work (nvfp4) you need : * Update comfyui to the latest version

- I have tested them most except Flux, the fact that NVFP4 for Z-image and Qwen don't put Character model lora into consideration, so no use. For LTX-2, It's just producing garbage. have not tested Flux yet but I'm sure the structure would be the same to ignore Character model lora. As for the speed, It's about the same. No improvement. RTX 5090 CUDA 13.0, Triton 2.9.1 Laptop.

- You can use FP8 and NVFP4 on other arch, it will fallback to BF16 computation. It just that FP8 is faster on Ada and Blackwell while FP4 is faster only on Blackwell

- Older GPUs (RTX 40/30-series): Use the INT4 setting; you will still see significant memory savings (3.6x) and speed improvements (up to 3x), though not the native FP4 benefit.

- ## [Do any comparison between 4x 3090 and a single RTX 6000 Blackwell gpu exist? : r/LocalLLM _202512](https://www.reddit.com/r/LocalLLM/comments/1pu62uz/do_any_comparison_between_4x_3090_and_a_single/)
- Just got here. 
  - Setup on Blackwell is still a bit of a pain, by comparison the 3090s are easy peasy
  - Prompt Processing performance - using GLM 4.6 quants in llama.cpp I get 3.5x the speed with the blackwell than I do with the 3090
  - Token Generation - essentially no difference (I think I can get a little better performance here from the Pro 6000 but between system differences and kernel differences the raw power of the Pro doesn't make up the difference in perf)
  - Power consumption - baseline consumption is very similar, with the pro sitting at around 3.5x one 3090. Under single query load the pro has been hitting 200 W
  - Sound - The pro is in my living room, I can barely hear it. The 3090s are in my office.... I can *really* hear it. Not horrible but I know when it's running.
  - I haven't played with vLLM much but for models that can be fully resident in 96 GB VRAM the Pro tentatively ran at 2x for both generation and prompt processing.
- My conclusion is:
  * For models fully resident in 96GB the Pro wins hands down (ignoring pricing)
  * For models partially resident in 96GB the Pro wins on processing but not prompt generation
  * When factoring in price, the 3090 is a great contender
  * When factoring in future improvements and the ability to easily go to 2 or 4 gpus I think the Blackwell wins.

- The 3090's will not give you 96gb of useable memory. There is VRAM overhead space being taken up to manage the communication between the cards, so you will only have about 88gb of actual useable VRAM. In addition it will run slower because it has to send information between cards.
  - Not true. I have yet to see a benchmark where the Pro 6000 wins. 4x3090 with TP and vLLM is faster, especially at long context, than anything on the Pro 6000.

- ## [Got me a 32GB RTX 4080 Super : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pstaoo/got_me_a_32gb_rtx_4080_super/)
  - I took a risk and bought a modified RTX 4080 Super from the Chinese market for around 1200 USD / 1000 EUR. Which for me because I live in Europe, the cheapest RTX 5090 I can find is around 2500 USD / 2100 EUR.
  - It's maybe not the best card for price per GB of VRAM considering the RTX 3090 is dropping a lot, but 32GB on one card for about half the price of a 5090 is nice. I do a lot of Diffusion model stuff, so it's great for that too.
  - It works with the stock Nvidia driver, no messing around, it was just literally plug and play. Card seems really good quality, metal back plate and metal case. Fan sounds like a small jet engine.
  - But running it around a month now and zero issues at all.
  - I got mine from this seller, price went up 1000 RMB though since i bought it though. I used Superbuy to handle forwarding.

- How is the temperature and what power limit. I am eyeing it for quite a while. It is about S$2400 in where i living.
  - It gets around 70C max under load, seems to hit around 300W under full load. Hasn't been an issue, the blower is pretty loud though.

- how’s the speed? 
  - Same as a stock RTX 4080 super.

- Look like they doubled the NAND chip on that GPU. Curious about how you set up the driver to receive all the VRAM.
  - I didn't touch the driver, it's stock. I guess the RTX 4080 is special in that way, if you add bigger ~~NAND~~ GDDR VRAM chips, it gets recognized without much fuss.
- the reason for this is that there is a 4090 Mobile with less vram for the gaming laptop market, and it uses the same chip as the desktop 4080. The 4080 super is just a more performant gpu compared to the stock 4080. The idea is that the vram size is "changeable" , so technically NVIDIA could put more vram in such cards, and they actually did it in professional gpu like the rtx 6000 ada series (same core as rtx 4090 desktop gpu with more vram). And such that the driver must be able to recognize the vram to function properly.

- I hope NVIDIA doesn't disable it in the GPU mainboard in the future like Apple did in the mac studio ssd slot (mac studio has a ssd slot but it refuse to recognize any ssd even from other mac studio.)

- it's not nand... it's gddr dram

- ## [NVIDIA RTX PRO 5000 Blackwell GPU with 72GB GDDR7 memory is now released : r/comfyui _202512](https://www.reddit.com/r/comfyui/comments/1prz95a/nvidia_rtx_pro_5000_blackwell_gpu_with_72gb_gddr7/)
- Nvidia seems to have settled on $100/GB of vram. AMD will sell you a 7900xtx w/ 48gb of vram for $65/GB. But it's a triple slot and as far as rocm has come, the biggest improvements are kept back for the mi instinct series.

- That might be great news for the LLM community. But we image guys here are usually compute bound. I.e. a 5090 might be more worth to us than a VRAM extended 5000

- some of the WAN models go OOM even on a 6000 PRO for 1080p resolution and 1600+ frames, so this dosen't seem so interesting now.

- Only 14k cuda cores, guys, that's a solid meh.

- several hundred cheaper than the Max-Q RTX Pro with 24GB less RAM...

- Stupid question, if you just had a stupid amount of money could you use this card for gaming and blow away a 5090 or does it not work like that?
  - Yes you could, but not with the PRO 5000. PRO 6000 with 96GB is the one you want if you wanna beat the 5090. That one has the fully unlocked GB202 with 24064 cores, instead of "only" 21760 on the 5090, and it beats the 5090 in gaming by about 10%. But it starts at $7k.

- Memory bus on these GPUs is only 384-bit, not 512-bit as the Nvidia datasheet claims.
- I mean, the 5090 has 512-bit and GDDR7. So even with the higher memory capacity, it’ll be slower, but just have more Ram to work on larger models?
  - Yes, bandwidth is severely reduced from 1792GB/s (512-bit) to 1344GB/s (384-bit).

- ## [AMD Radeon AI PRO R9700 benchmarks with ROCm and Vulkan and llama.cpp : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1prgi41/amd_radeon_ai_pro_r9700_benchmarks_with_rocm_and/)
  - Spec: AMD Ryzen 7 5800X (16) @ 5.363 GHz, 64 GiB DDR4 RAM @ 3600 MHz, AMD Radeon AI PRO R9700.
  - Software is running on Arch Linux with ROCm 7.1.1 (my Comfy install is still using a slightly older PyTorch nightly release with ROCm 7.0).
  - The LLM is instructed to summarise each chapter of a 120k-word novel individually, with a script parallelising calls to the local API to take advantage of batched inference. 
  - Mistral Small: batch=3; 479s total time; ~14k output words
  - gpt-oss 20B: batch=32; 113s; 18k output words (exluding reasoning)
  - TLDR is that ROCm usually has slightly faster prompt processing and takes less performance hit from long context, while Vulkan usually has slightly faster tg.
  - All using ComfyUI. 
  - Z-image, prompt cached, 9 steps, 1024×1024: 7.5 s (6.3 s with torch compile), ~8.1 s with prompt processing.
  - SDXL, v-pred model, 1024×1024, 50 steps, Euler ancestral cfg++, batch 4: 44.5 s (Comfy shows 1.18 it/s, so 4.72 it/s after normalising for batch size and without counting VAE decode). With torch compile I get 41.2 s and 5 it/s after normalising for batch count.
  - Flux 2 dev fp8. Keep in mind that Comfy is unoptimised regarding RAM usage, and 64 GiB is simply not enough for such a large model — without --no-cache it tried to load Flux weights for half an hour, using most of my swap, until I gave up.
  - I also successfully finished full LoRA training of Gemma 2 9B using Unsloth. It was surprisingly quick, but perhaps that should be expected given the small dataset (about 70 samples and 4 epochs). While I don’t remember exactly how long it took, it was definitely measured in minutes rather than hours. 

- A lot of people considering 5080's/4090's for LLMs would probably be happier with this card. It's 32GB in a single slot with very reasonable prompt-processing speeds and good enough token-gen.
  - also it's not bad at all with diffusion models, even with ROCm in its early days. Quite promising.

- 4-bit quant/qlora support for Radeon cards just got merged into Unsloth a day or 2 ago. It's been added to Bitsandbytes for some time now, feel free to check it out 

- ## [They're finally here (Radeon 9700) : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pnd5uf/theyre_finally_here_radeon_9700/)
- Fuck, I'm old. Radeon 9700 was a top tier GPU back in the 2000's. They have used all the code names and started a new loop
  - Yeah search results are annoying. And AMD now has a 9700x CPU as well.

- I have one R9700 and planning to get another (or whatever comes next--PRO 36GB or 72GB sku). The benefits of the R9700 isn't really for performance/price. The benefits I see:
  - blower fan design lets you pack them side by side no no slot gaps needed
  - 32GB per 300W GPU means fewer GPUs/lesser PSU for given total VRAM
  - also fewer needed PCIe lanes to GPUs for given VRAM
  - ECC memory operation can be enabled on Linux for longer/reliable operation
  - PRO sku meant to be running continuously (with sufficient cooling)
  - RDNA4 should have better long-term support than older gens.

- ## 🆚 [Is it better to upgrade from 3080 to 3090 or 5080 for video generation? : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/1pjfmrw/is_it_better_to_upgrade_from_3080_to_3090_or_5080/)
- I have both the 3090 and 5080 hooked up to my computer as I am typing this. For majority of the task, including wan 720p 480p, qwen edit, z-image, and illustrious + 4k hires fix, 
  - I find myself only use 5080 and vram has not been an issue unless I'm running a very large batch size. 
  - The 5080 is twice as fast with support for fp8 and fp4. Since buying the 5080, the 3090 has only been used for llm when i need better prompt or gaming concurrently with running the workflow.

- Just a headsup 3090 doest support 8bit calculation. You would be using fp16 versions or anything lower than 16bit will be transformed to fp16
  - It does support INT8, just not FP8.

- My vote is for more vram. Best advantage of the 5080 is speed, but with vram it opens up so much more possibilities (and that speed won't matter if it wont fit into memory).

- ## [Does ComfyUI work flawlessly with AMD graphics cards too? Which card is more stable? Is there anything that can be done with Nvidia but not with AMD? : r/comfyui _202512](https://www.reddit.com/r/comfyui/comments/1pi94ix/does_comfyui_work_flawlessly_with_amd_graphics/)
- Using an AMD Graphics card is the difficult and treacherous road currently in the world of AI (I know, I primarily use a Radeon Pro w7800 32GB). Even installing basic Custom Nodes is fraught with dangers. One must examine each requirements.txt file to make sure it is not trying to install torch, torchaudio, and/or torchvision (which is rather unnecessary to put into the requirements file for a custom_node anyway.) Those lines will need to be commented out or erased after cloning the Git. If not done, then upon ComfyUI's next startup, it will uninstall the ROCm version of pytorch and install the Nvidia one instead breaking all inference functionality (this has happened to me a couple of times before. Blast my laziness!). 
  - Furthermore, some attention algorithms currently are not compatible with AMD cards. It's a cold, hard AI world for AMD GPU users. However, it is getting better. ROCm is getting better. 
  - Many AMD cards are great, especially for gaming. 
  - However, for the time being, if you have a choice, I recommend using a Nvidia card for AI.

- ## [Can M1/M2 Macbooks use ANY eGPU as a docking station? : r/eGPU _202212](https://www.reddit.com/r/eGPU/comments/zk8yzv/can_m1m2_macbooks_use_any_egpu_as_a_docking/)
- unfortunately. The M2 MacBook Air only supports one external display up to 6K resolution. The only option is to use DisplayLink adapters/docking stations if you want more than one external display.

- eGPUs work on Apple Silicon but the driver support on macOS is nonexistent because Apple no longer has any reason to listen to GPU manufacturers since they make their own now. You'd need to install Asahi Linux and wait for Thunderbolt support to be ready, but yes theoretically it should be doable

- ## 🆚 [V100 vs 5060ti vs 3090 - Some numbers : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p4b6ti/v100_vs_5060ti_vs_3090_some_numbers/)
- Speed specs put the 3090 in first place in raw compute
  - 3090 - 35.6 TFlops FP16 (936Gb/s bandwidth)
  - V100 - 31.3 TFlops FP16 (897 Gb/s bandwidth)
  - 5060ti - 23.7 TFlops FP16 (448 Gb/s bandwidth)
- Machines:
  - 8x V100 SXM2 16G. This was the machine that I started on Vast with. Picked it up post ETH mining craze for dirt cheap. 2x E5-2690 v4 (56 threads) 512G RAM
  - 8x 5060ti 16G. Got the board and processors from a guy in the CPU mining community. Cards are running via MCIO cables and risers - Gen 5x8. 2x EPYC 9654 (384 threads) 384G RAM
  - 4x 3090, 2 NVLINK Pairs. Older processors 2x E5-2695 v3 (56 threads) 512G RAM
- Ran llama-bench with llama3.1 70B Instruct Q4 model with n_gen set to 256 (ran n_prompt numbers as well but they are just silly)

| Card    | T/s   | Relative | TFlops | Relative |
|---------|-------|----------|--------|----------|
| 3090    | 19.09 | 100%     | 36.6   | 100%     |
| V100    | 16.68 | 87.4%    | 31.3   | 87.9%    |
| 5060ti  | 9.66  | 50.6%    | 23.7   | 66.6%    |

- llm generation mostly scale with memory bandwidth rather than compute capability, for dense mode, if u use vllm and enable tensor parallel, u will get double that speed
- TG numbers do not depend much on compute capacity but almost completely on memory bandwidth

- Need prompt processing speed. Batch speeds. Tensor parallelism? Just post the raw llama bench tables and settings you used to run it. Also would be useful to have power numbers.

- ## 🏠🤔 [1x 6000 pro 96gb or 3x 5090 32gb? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p2540n/1x_6000_pro_96gb_or_3x_5090_32gb/)
- 1x 6000 not 3x 5090. 
  - A single chunk of vram is always better than a divided one - unless your intention is to run multiple concurrent small models, then the 5090s give you more compute. 
  - And Epyc 9xxx over Threadripper for more ram channels, as long as you go for the high clockspeed versions (F). Go for 9575F, 64 cores, high clockspeed, 12 channels. Only disadvantage is having to use a server board.
- RTX 6000 Pro has the ability to split into (up to) 7 independent virtual graphics cards. There is really no advantage to 3x 5090.
  - There is. Since if you run TP, then those 2x 5090s can be faster. The 3rd 5090 will have to wait for a partner.
- That is absolutely wrong. Maybe because you havent used vLLM in tensor parallel and only have used llama.cpp or Ollama? 2x5090 or 4x5090 is way faster than 1x rtx 6000 if used in tensor parallel (which Ollamas and other hoobyist inference engines cant do)

- people dont realize that bandwidth between GPU and memory IS the bottleneck. a model can not load efficiently into separate cards. you end up with three tines only 32gb usable memory
  - No, thats not true. In tensor parallel 2 or 4 pcie 5.0 16x is enough for most of the tasks. So 2 or 4 5090 connected with pcie 5.0 16x is enough fast pcie link between gpus. I have tested this and was never able to fill the full bandwidth totally. The speed does not increase lineary but 2nd gpu gives 60% more inference speed when enough simultaneous requests.

- Can’t -tp 3 with vllm
  - Pp3(Pipeline parallelism w 3 cards) works fine and is better with consumer gpus anyways since it requires less communication between cards. Data center card are connected with infinity band so tp is better

- I have 3x 5090 and 1x Pro 6000 as well as a Threadripper with 512GB RAM (and a second Threadripper and 3 3090), and my recommendation for running LLMs of that size locally is: Don't.
  - At least don't expect it to be good value or fast. 
  -  I use local for parallel workloads. 10k t/s throughput - now we are talking.

- A lot of people here are assuming the 5090 behaves like a normal single-GPU setup. It doesn’t — not with the current software stack.
  - If your workload needs contiguous VRAM (anything 70B+, large context, MoE with large expert blocks, diffusion XL, video gen, etc.), a single 96 GB slab always beats 3× 32 GB islands, regardless of raw TFLOPs.
  - Multi-GPU only wins if you’re bulk-processing smaller jobs in parallel. 

- why I vote Epyc instead of Threadripper:
  - The higher singlethread perf of Threadripper isnt worth the extra cost.
  - EPYC DDR4 platform could save you a couple thousand over DDR5. 
- Why RtX 6000 Pro and not 3x5090:
  - The convenience and simplicity of a having 1 x GPU with less wiring and less grief with management and maintenance, PCIE risers and cases and PSU selections and power draw etc its worth the little bit extra spend. (Plus with 3x GPU you cant use tensor parallel in VLLM)

- I have both a 6000 Pro (typically using llama.cpp) and a 2x3090 setup (using vllm). 
  - 3 is an awkward number since I don't think you can run tensor parallel. Moving to 4 you'd definitely want the Epyc/TR/Xeon4+ type platform and may need things like PCIe extensions and a mining rig chassis, etc.
  - If you are just using naive layer splitting (llama.cpp) you only really get the speed of what a single 5090 bandwidth is limiting you to and poor GPU utilization, and you should think seriously about getting sufficient PCIe lanes/bandwidth to a power of 2 number of GPUs (2, 4, 8) to use tensor parallel in VLLM if you are messing with this as it unlocks utilizing all the GPUs more fully. I also tested llama.cpp on the 2x3090 setup but it was substantially slower than using vllm with tensor parallel and GPU utilization hovers around 50%, which is sort of expected, still taking full power according to nvtop. VLLM with tensor parallel I peg both GPUs and even setting them down all the way to ~200W costs very little performance. I'd probably want to confirm with power draw at the wall but I think this is ultimately very wasteful not to try to use tensor parallel plus the massive performance difference.
  - tldr: as a RTX 6000 enjoyer myself having also worked on multi-gpu setups, I'd probably push you more toward 3x5090, then you have a good upgrade path later if you want to Epyc/TR + 4x5090 and that will ultimately be far superior and at least roughly similar in total cost. It is more complicated, you need to move off llama.cpp to vllm, you need a giant mining chassis and maybe PCIe extensions, more PSUs (even if you set power down, you need to physically connect everything), etc. One RTX 6000 is "simpler."

- Also, come the future selling 5090s will be easier than a single 6000.

- 5090s will give ~3x the heat, ~3x the power, ~3x the memory bandwidth, ~3x the flops and will require ~3x the physical space.

- ## [Ollares one: miniPC with RTX 5090 mobile (24GB VRAM) + Intel 275HX (96GB RAM) : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ov3x0m/ollares_one_minipc_with_rtx_5090_mobile_24gb_vram/)
  - Processor: Intel® Ultra 9 275HX 24 Cores, 5.4GHz
  - GPU: NVIDIA GeForce RTX 5090 Mobile 24GB GDDR7
  - Memory: 96GB RAM (2×48GB) DDR5 5600MHz
  - Initial price seems it would be around $4000

- the 5090 mobile is based on the 5080 desktop chip, is a bit less compute and bandwidth than a 5080 desktop owing to being a mobile part, but with 24GB instead of 16GB. The 5080 desktop is already about half the speed of a 5090. The system is still a dual channel DDR5 system after you run out of VRAM, just like a normal desktop. 
  - It feels to me like a very narrow market for the particular combination of very tiny form factor, good diffusion and smaller LLM performance (<32B), and low power usage. 
  - Otherwise, a better value is probably found for large (80-120B) MOE LLM in the 395/Spark, or a desktop 5090 which you can at least cram into a "smallish" mini ITX case like the Corsair 2000D.

- it cant compete with unified memory machines since its ram is slower by 4-8x compared to them. 

- ## 🆚 [Why Ampere Workstation/Datacenter/Server GPUs are still so expensive after 5+ years? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ove1px/why_ampere_workstationdatacenterserver_gpus_are/)
- ada
  RTX 6000 Ada (48GB), on ebay for about 5000 USD.
  RTX 5000 Ada (32GB), on ebay for about 2800-3000 USD.
  RTX 4000 Ada (24GB), on ebay for about 1200 USD.
  NVIDIA L40 (48GB), on ebay for about 7000 USD.
  NVIDIA L40S (48GB), on ebay for about 7000USD.
  NVIDIA L4 (24 GB), on ebay for about 2200 to 2800 USD.

- ampere
  RTX A6000 (48GB), on ebay for about 4000-4500 USD.
  RTX A5000 (24GB), on ebay for about 1400 USD.
  RTX A4000 (16GB), on ebay for about 750 USD.
  NVIDIA A40 (48GB), on ebay for about 4000 USD.
  NVIDIA A100 (40GB) PCIe, on ebay for about 4000 USD.
  NVIDIA A100 (80GB) PCIe, on ebay for about 7000 USD.
  NVIDIA A10 (24GB), on ebat for about 1800 USD.

- ADA generation killed nvlink for pro level gpus. This means for multi-gpu training particularly bandwidth intensive tasks the ampere generation is superior.
  - Blackwell is also a big leap over ADA generation in both compute, but crucially VRAM as well.
  - As a result if you want multi-gpu ampere can often win, and if you want single GPU Blackwell is a no brainer vs Ada, so ADA doesn't have a market niche.

- Ampere cards are slower (about half perf compared to Ada), some less VRAM and don't support FP8.

- Their memory bandwidth is stil above what is available for the consumer market + their power consumption is even lower.

- What MOBO do you recommend for 5-6 cards? If possible AMD AM5.
  - Threadripper/threadripper pro/xeon workstation or server motherboard like amd epyc or intel xeon.
  - Only workstation/server motherboards have enough pcie lanes to satisfy your needs.
  - Consumer motherboards won't properly support that much gpus A z790-p supports 4 gpu, 1 with x16 lanes from the cpu and 3 x4 from the chipset (acting link a switch).
  - You could split the x16 (if bifurcation is supported). But still this is x4 pcie 4.0, could be a bottleneck.

- Ampere cards are still pretty good all-rounders that can handle AI workloads well, they support BF16 training and inference and that's not dead.

- ## [Does AMD AI Max 395+ have 8 channel memory like image says it does? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1os6t6w/does_amd_ai_max_395_have_8_channel_memory_like/)
- 4 channels * 64-bit interface * 8000 MT/s = 256 GB/s.
  - It’s LPDDR5x not DDR5 so it’s technically 8 channels at 32 bit, but the effective bit width and bandwidth is the same.

- Probably a typo, but technically DDR5 has 2 32 bit channels per module x four dimm channels would make 8 *32-bit* channels, but it would be disingenuous to advertise it that way.

- My understanding is Halo Strix has quad channel DDR5.

- ## [AMD R9700: yea or nay? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1os2756/amd_r9700_yea_or_nay/)
- It's slower than a 3090 and doesn't offer fp4. 3090 can emulate fp8 and it's almost twice as fast. Also less of a headache...
- 3090 doesn't offer FP4 nor FP8, needs emulator and the perf tanks doing so. INT4, FP16, BF16, INT8, INT4.
  - Only Blackwell supports FP4, FP32, FP16, BF16, INT8, INT4, FP8.
- On R9700 FP8 and BF8 are fully supported, with improved perf.
  - FYI, FSR4 is FP8.

- ## [AMD Officially Prices Radeon AI PRO R9700 At $1299 - 32GB VRAM - Launch Date Oct 27 : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oeg2g6/amd_officially_prices_radeon_ai_pro_r9700_at_1299/)
- 640GB/s
  - yes, for the same price, i can get 2x3090 for 900 gb/s and 48gb vram and cuda compatibility
- Specs sheet says int4 only, not Fp4...
- 640 GB/s Memory Bandwidth - slower than the 5 year old rtx 3090 and 1/3rd of a 5090. No FP4 or CUDA.

- They're Rx 9070's with blower fans and twice the VRAM.

- FYI R9700 is slim 300W card with ECC VRAM, can easily fit 2 on any motherboard.
  - Also make no sense to buy €750 RTX3090 when R9700 is €1000 if you can deduct the sales tax (normal price €1250-€1300) in Europe.

- Used 3090 are 500-550$. Even good ones from asus or msi.

- All the AMD pro series GPUs have official ROCm support.
  - Oh I know. I just mean Vulkan actually works.
- Full ROCm works and they have ECC VRAM.

- MI50s are good after fresh updates, although R9700 has lots of new things - FP8, matrix cores, etc.

- 70% slower than 5090
- Fp16 seems much closer
  - Only when sparse

- 4 of these in parallel is a compelling alternative to an RTX Pro 6000
  - Wins on VRAM Quantity 128GB VRAM vs. 96GB VRAM
  - Wins on Price ~5200 vs ~8200
  - Wins on Collective Bandwidth (if you user tensor parallel) 640x4=2.56TB/s vs 1.8TB/s
  - Only obvious loss is power usage 300x4 = 1200W vs 600x2 or 300x2 (600 or 1200W depending which model)
  - And upgradability. Few cases/motherboards are going to support more than 4 cards unless you start getting jank with it.

- ## [8年了，为何eGPU外置显卡不能被玩家接受 - 知乎 _202507](https://zhuanlan.zhihu.com/p/1930776574258549666)
- 初代外置显卡（eGPU）曾许下诸多豪言壮语。这些看似新颖炫酷的显卡外置盒本应彻底改变游戏本市场
  - 如今，距离面向普通消费者的第一代外置显卡问世，已过去了八年，可笔记本电脑市场却没多大变化。
- 雷蛇Core并非首款外置显卡（第一款真正意义上的笔记本专用eGPU是2008年华硕推出的XG Station），但雷蛇Core是第一款引起轰动的产品。
- 外置显卡终究是一件需要额外随身携带的设备。背包里的空间本来就宝贵，完全可以用来装其他配件。更何况，还得折腾半天设置选项，确保游戏能识别外置显卡并调用它来渲染画面，这无疑增加了不少麻烦。总的来说，还不如降低画质要求，用电脑自带显卡来得便捷。
- 2025年，华硕、雷蛇和技嘉都推出了新款外置显卡。今年的各类科技展和游戏展上，主流厂商一下子拿出了四款新的外置显卡。
  - 这次算是时隔8年后，厂商们对外置显卡市场最大规模的一次发力。这一切都要归功于雷电5接口

- egpu的真正价值在于你和你的家人可以共享一块显卡，这样你们就可以把钱攒起来买一个5070一起用，而不是每个人都去买一个5090显卡。

- 网上那些做外接显卡视频的，几乎透露出兼容差、稳定性差的问题，相比起来性能损耗都是小问题。不能普及显而易见。

- 体验过一次，再也没买过。当时xps15配了个1080的egpu，结果性能还比如台式机直插的1060直接心态崩了
  - 雷电3性能缩水30%是小意思

- ## [Dual GPU, AMD & Nvidia together? : r/losslessscaling _202504](https://www.reddit.com/r/losslessscaling/comments/1jpelqr/dual_gpu_amd_nvidia_together/)
- I tested a 4090 (4.0x16) with rx6600 (4.0x4) setup a while ago. While i was too lazy to find the perfect settings for it, i did not see any issues with drivers.
  - I just tested it for a day or two and couldn't overcome some issues with the performance. I think that it had something to do with using the chipset 4x4 line rather than cpu's.

- I rock a 4090 with 6600XT. I have both full drivers installed and run win 11. They don’t clash.

- The main limitation is Nvidia's lower FP16 performance, but a 3080 TI is very good (30 TFLOPs), enough for 4k. Driver conflicts are a possibility, but nowadays everything conflicts with everything already. I've not heard of issues so far and it wouldn't do l so stop me from using the 3080. I would just get the minimal drivers for each GPU if possible.

- [Is it possible to use both and nVidia and AMD GPU? : r/LocalLLaMA _202407](https://www.reddit.com/r/LocalLLaMA/comments/1dt367v/is_it_possible_to_use_both_and_nvidia_and_amd_gpu/)
- Tested RX 7900 XTX and 4060 Ti (16GB) running together in LM Studio via Vulkan. Tried it with two models:
  - DS r1 70B Q5 — 10.05 tok/sec
  - QWQ 32b — 15.67 tok/sec
  - For comparison, RX 7900 XTX solo gets around 24.55 tok/sec in QWQ 32b.
- So you saying that dual is slower?
  - Exactly — a single 7900 XTX is better than a 7900 XTX + RTX 4060 Ti combo when the model requires less than 24GB of VRAM. In my configuration ofc, mb I did something wrong)

- [AMD + NVIDIA GPU : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1obgm8u/amd_nvidia_gpu/)
- I've got a RTX 5070 Ti (PCIe 5.0x16, CPU) and a RX 5500 XT (PCIe 4.0x4, CPU) in my AM5 PC. Is there a way to use both GPUs and the CPU to run the same gguf model?
  - You can compile multiple backends into Llamacpp and use them all at once.
  - Yup, the easiest way is to use Vulkan. Any llama.cpp-based software can do this (ie Lmstudio). Ollama not yet - experimental.

- [Is it possible to run my 9070 XT with my old RTX 3070? : r/losslessscaling _202511](https://www.reddit.com/r/losslessscaling/comments/1osolqu/is_it_possible_to_run_my_9070_xt_with_my_old_rtx/)
  - You can, but the top card will roast. And you’ll lose the AMD specific 9070XT features.
  - when mixing Nvidia and AMD GPUs, since the monitor is always connected to the 2nd GPU(3070 in your case), on desktop you will only be able to use Nvidia App for stuff like color profiles, but in game it will be using FSR4 upscaling.
  - Personally I have used all combinations, AMD 1st GPU and Nvidia 2nd GPU, vise versa, and now im using 5070ti + 3060ti. I gotta say there is no real difference, all the small features like anti lag, RSR, make negligible differences.
  - Right now my setup is 3440x1440 HDR 165hz with 5070ti and 3060ti(PCIE4.0 x4). I can comfortably boost from 50-80fps to 160fps with 3060ti usage no more than 75%.

- ## 💡🧩 [AMD and Nvidia GPUs in the same machine. IT WORKS. : r/linuxhardware _202006](https://www.reddit.com/r/linuxhardware/comments/he9nhe/amd_and_nvidia_gpus_in_the_same_machine_it_works/)
  - TLDR: Nvidia Card in slot 2 with proprietary driver (v. 440xx) + AMD card in slot 1 open source driver (mesa v20.1), no configuration needed, just prime-run what you need to run with Nvidia card as the back-end renderer. Enjoy the smooth desktop and Nvidia/proprietary bond applications
  - The solution is a simple prime-run command. No messy xorg config files. In fact no manual configuration at all.

- What software requires proprietary Nvidia drivers?
  - In my case it's Davinci Resolve. A video editing software. It only runs with proprietary driver (AMD and Nvidia). I paid for the studio version.

- My laptop has an Intel iGPU and a GTX 1650, and I use an RX 5700 XT in an eGPU enclosure. I also use Mesa and the Nvidia proprietary driver simultaneously or alternating without issues (mostly).
  - It's a little different on a laptop trying to push external graphics but it still works
- So I suppose you use hybrid driver? iGPU as default OpenGL renderer and DRI_PRIME to use dGPU or eGPU? I'm curious how you access different GPUs.
  - I have pop OS, which includes a super handy GPU mode switcher tool (Integrated/Hybrid/Dedicated). You have to reboot each time (unless doing Hybrid and telling applications to run using dGPU).
  - I also installed the gswitch tool from egpu.io, and use it to switch between internal and external graphics when connected to my Thunderbolt 3 dock.
  - The only thing that really doesn't work is staying in "internal" graphics mode and trying to drive the external monitor (or vice versa; can't drive the internal display with external GPU). It "works" but the performance hit is so bad that even GNOME's desktop is unusable.
  - Other than that the whole setup is so easy that it takes me maybe 5 minutes to do on a fresh popOS install (or Ubuntu 20.04 with system76-power tool installed).
  - I highly recommend this setup if you ever plan on going the Nvidia laptop route and don't mind needing to use the prop drivers (even if your egpu is Nvidia it works perfectly).

- I’m trying to do the same - XPS 9500 with i7 CPU and GTX1650ti dGPU… i have a razer core X enclosure and want to try an AMD RX 6600
  - basically plug and play, the drivers auto-installed and everything works smoothly!

- ## 🤔 [1x4090 24GB or 3x3060 12Gb for Comfy? : r/comfyui _202409](https://www.reddit.com/r/comfyui/comments/1fql7if/1x4090_24gb_or_3x3060_12gb_for_comfy/)
- 3x3060 won’t give you 36GB. The model can’t be split. There are variations of putting the T5 or clip into another card, but the multi GPU aspect will complicate it so much, it will drive you nuts. Especially since you say yourself you are a beginner. Don’t do it. Go for 4090, comfy ui is complicated enough, you don’t want to deal with anymore hardware setup issues on top of that. If you are tight on cash, go for a used 3090.

- In terms of AI a 4090 would still kill 3x 3060 and VRAM does not work as you think it does, you will not get 36GB VRAM with 3x 3060s

- 3x 3060 only if you're in production and your workflow can fit into 12GB VRAM and you're doing loads of parallel generations.

- 4090, speed is the key point, and there are many ways to reduce VRAM needs.

- ## [Sanity check: Using multiple GPUs in one PC via ComfyUI-MultiGPU. Will it be a benefit? : r/comfyui _202504](https://www.reddit.com/r/comfyui/comments/1k4xjxh/sanity_check_using_multiple_gpus_in_one_pc_via/)
- I own the ComfyUI-MultiGPU custom node. The two most common ways I see ComfyUI-MultiGPU are the following:
  - Moving parts of the process to a secondary GPU - typically CLIP/VAE
  - Using Distorch to offload the entirety of the UNet to another GPU or CPU (preferred).
  - In doing those two things, most people can get to a "naked" compute card, giving users the most latent space at the cost of speed. It is the way I use ComfyUI most of the time with a 2x3090 NVLink setup.
  - "Naked" in the sense that there is nothing taking up VRAM on the main compute card other than latent space. In a typical one-GPU setup, VAE, CLIP, and UNet are all resident on the card and take up VRAM that cant't be used for generations. Even a highly-quantized Q3 GGUF takes up (mostly) dead space in your card's VRAM as only one part of it is being dequantized at a time to be used actively during inference, then discarded until the next inference step.
  - In an optimal MultiGPU setup, all three componenets have been moved off the compute video card's VRAM entirely, allowing the card to be completely filled by latent spece. In this case, a 12G VRAM card can do video that fills that entire 12G of latent space, meaning either higher resolution or longer generations than if half (or more) of that VRAM was being used for component storage.

- ## [有哪些二手显卡值得玩? - 知乎](https://www.zhihu.com/question/1955229739569619499)
- 纯玩游戏还可以加个mi50刷镭7bios，比vega64新一点

- 2080ti，刚刚跌了一大波，dy叠券最便宜1100-1200就能收一张，你能得到：默认5060/3070，超频5060ti，极限摸3080屁股的游戏性能
  - 相比更早的卡如v100，有DLSS4，有光追，可以跑渲染器，甚至可以4kDLSS超级性能+插帧mod，60-70帧玩一玩2077路径追踪
  - 几乎最完美的显存扩容体验，20系显卡显存扩容只需要把显存颗粒从1G GDDR6换成2G就可以
  - 这一代的vbios还没有上锁，扩容没有驱动bug（3070 16g有），无需拆BGA（3080、4090需要），所有品牌vbios任意互刷（3080、4090需要特制vbios），完全不影响超频（3080、4090改后锁功耗），完全不影响散热（3080、4090改装后变成双面显存大火炉）
  - 没有vega系列HBM缩肛问题，没有6800系列炸核心问题
  - 唯一要担心的就是别买到早期镁光显存和黄皮股大修卡
- 说实话不如直接买5060，这玩意功耗快到5060两倍了，二手能用多久也很难说。

- 为什么3060还能卖1300吗？我觉得这个破卡根本不值钱，现在3070也是1300
  - 2g大显存，2k3a新游戏能反杀4060持平5060这种8g的卡
  - AI绘图入门卡，已经没有比它性价比还高的卡了，另外3060不建议买二手，矿卡太多，建议还是买个正规牌子的2000左右的新卡

- v100 32g 现在约2100 ；期盼降到1500 。
  - v100 16g约500；配一套水冷 900块。
  - x99 e5一套双显卡槽主机不过千元。
  - 3500搭一套32g单卡主机；
  - 但功耗难绷300-600w，所以最后用mac玩api了；

- 别折腾V100这种垃圾了，现在越来越多的新模型，都使用BF16、FP8甚至NVFP4训练模型了，就算推理，算力要求也是8.0起步，有AI需求，老老实实买新卡。

- ## [AMD 发布 AI 显卡 R9700，性能号称同级 5 倍，实际表现如何？ - 知乎 _202509](https://www.zhihu.com/question/1946144571521234533)
  - R9700的AI性能表现却引起了大家的关注，作为一款RDNA4架构的显卡，拥有32GB GDDR6、256-bit位宽、峰值带宽约640 GB/s、300W TDP，以及最多约1531 TOPS（INT4）和FP16约96 TFLOPS的AI/矩阵运算能力。

- 这个是RDNA4应该比395max那个RDNA3.5的魔改强不少吧

- [AMD发布AI神卡R9700！性能是同级5倍，英伟 - 小红书](https://www.xiaohongshu.com/explore/68c58dcb000000001c008551?xsec_token=ABxWJEP3Vpkb636xx2y79C0FRNAwvEq6parZO6uJSDPkM=&xsec_source=pc_search&source=web_search_result_notes)
- 人话：32g版本9070
- 没有 CUDA 生态支持，也就玩玩现成的 toy model
  - 用vulkan或者ZLUDA或者HIP跑呗，反正8k块的卡肯定是个人用，不需要集群，不考虑多并发或者交火啥的，能玩

- 只能在Linux平台用，llm可能还行，AIGC估计是各种不兼容报错。图便宜6000的3090就挺好的。r9700跌到6000也还是只推荐3090。
  - 补充一点，r9700性能同等级的游戏显卡是5070，跟5080不是一个级别产品，显存大确实是个亮点，但又不够大只有32GB，记得不错wan的权重好像是35GB，折腾一圈到最后还是只能选48GB的4090。
  - 不要为了推理llm，选来选去只能选m4 max，128GB 400多的带宽，苹果头一次有性价比。

- 没意义，a卡的ai卡如果性价比干不过2080ti 22g根本没出路

- 必须用HBM，试问按摩店2019年的HBM显存为什么悄咪咪的跑到老黄专业卡上了？为什么之后按摩店为什么不出HBM显存的显卡……这群幕后交易……呵呵呵！还是资本会玩

- ## [RTX 4080 SUPER 32 GB量产？显卡日报10月6日 - 知乎 _202510](https://zhuanlan.zhihu.com/p/1958257251954452012)

- [英伟达RTX4080S 32G涡轮显卡新鲜出炉 - 小红书 _202510](https://www.xiaohongshu.com/explore/68dc7ac30000000005031f93?xsec_token=ABF5bwSFkHhKX5sU6IgENqtkol2WzQxpTy_DJscw_OC8M=&xsec_source=pc_search&source=web_explore_feed)
- 那4080s是不是要涨价了
  - 多半不会，4090涨价虽然一方面有显存魔改的原因，但最主要禁售，而且也不产了，存量某种程度肯定少, 但4080市面上还是很多的
- 要是有三风扇版的就好了，涡轮的声音受不了

- [现在上4080super是不是49年入国军？ - 知乎 _202408](https://www.zhihu.com/question/664986798)
  - 除非4080s 跌倒6k 不然真的不值得购买了，顶天也就5070ti的性能， 问题人家有 大力水手4啊。

- [4080Super买哪个好？不超频，但求省心不折腾? - 知乎](https://www.zhihu.com/question/651409618)
- 区别主要就是用料、外观、品牌和售后

- 主要设计处区别：供电、散热规格
  - 华硕 ROG 猛禽：18+3 70A供电，单16PIN供电，4*8mm+3*6mm铜管，均热板
  - 华硕 TUF 电竞特工：12+2 50A供电，单16PIN供电，5*8mm+3*6mm铜管，分体式镜面铜底
- 整体而言，华硕溢价严重，规格一般，而微星只有旗舰型号能看，七彩虹的全系用料都不错，影驰显卡的性价比高，还有影驰HOF名人堂是RTX4080Super规格里面供电最高的型号，还有，万丽盖拉多虽然是价格最低的，但不是用料最丐的。
  - 下面两款为良心型号，可无脑入： 
  - **影驰RTX4080 SUPER 星耀OC，七彩虹RTX4080 SUPER AD OC**
  - 旗舰型号推荐：七彩虹火神和水神、微星超龙（降价高可考虑）、影驰名人堂

- 每个品牌也有旗舰和次旗舰之分
  - 比如微星就有万图师，魔龙，超龙之分，分别对应的入门款，进阶和期间，价格相差几百。
  - 另外就是支持个人送保的七彩虹，对于售后这块来说简直不要太省心了， 七彩虹一款Ultra W OC，另外一款AD OC 区别不是很大，主要是外观区别

- 很多都是推荐微星、华硕、七彩虹的，把御三家的技嘉给漏了？
  - 因为技嘉辱华啊

- ## [如何评价RTX2080Ti 22G魔改版？ - 知乎](https://www.zhihu.com/question/8164944069)
  - 这张卡的价格在2600上下。同价位或预算内的N卡还有RTX 4060 8G（价格差不多），TESLA P100（这张只要1600左右）

- [我买计算卡时做的功课 对比表](https://www.zhihu.com/question/8164944069/answer/1940267056307077954)

- [What are your /r/LocalLLaMA "hot-takes"? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1obb4c4/what_are_your_rlocalllama_hottakes/)
  - Currently, no so-called AI PC or unified memory device can match the performance of a similarly priced combination of GPUs and server CPUs.
  - vLLM and CUDA 13 are dropping support for GPUs with SM7.5 and below, so buying any pre-Ampere GPU (e.g., 2080 Ti, V100) is not a sustainable long-term choice. In my opinion, only NVIDIA's Ampere (and newer) architectures and AMD's RDNA 4 are truly viable for AI workloads.

- 2080Ti~22g：目前(2024年12月底)，可以找到2400-2500店保一年的，尽量选口碑好的。
  - 这张卡能力均衡，是平民/垃圾佬的Ai神器，同样也是来路不明nv骑士的典范，生产力老手。
  - 大显存，高算力，高带宽，功耗合理，噪音散热可接受，还支持nvlink扩展。
  - 它的唯一缺点就是Turing架构有一丢丢老了，但比volta又要好一丢丢。至于矿不矿

- 2500附近的同一价位，能买到：
  - V100-sxm2-16g~PCIe(转接卡，训练向)
  - V100-pcie-16g-定制(核心搬板，训练向)
  - 2080Ti~22g(显存扩容，训练推理兼顾)
  - 3070~16g(显存扩容，推理日常兼顾)
  - 4060ti-8g(16g要捡漏，推理日常环保)
- 2025年5月加几块卡
  - A3000m~pcie(12G显存，移动版魔改，挑主板， ¥1400)
  - T10(16G显存，推理性价比高，一定要搞好散热， ¥1400)
  - 3080~20G(搬板扩容，应对3090涨价，注意散热，¥3500)
  - 5060Ti-16G(代替4060ti，兼容性逐渐好转， ¥3500)

- 我认为，深度学习的生产力提升关键在于混合精度训练(mixed-precision-training)和低精度推理
  - 除非你有非常明确的目标，比如依赖显存大小的传统单精度计算，并且有严格的预算，才考虑p100/p40
  - V100可以提供超越3090/4080的混合精度算力，适合深度学习训练，但因为volta作为最初代tensor core，不支持int8/int4加速，量化推理没有优势。目前SXM版本价格不错，但转接pcie需要折腾。
  - 2080Ti~22g，特点如前，推荐。精度不支持tf32/bf16/fp8/fp4，库不支持flash-attn:2+(已有移植版本可见)，影响需要根据实际研判。
  - 3070~16g或者择机捡漏上4060ti-16g，更适合入门选手，什么都想试试，推荐新架构。这个价位上目前还能买到A2，但只有3050的性能明显不太够看
- Ampere和Ada架构相比Turing的优势，一是工艺改进带来的能耗优化，二是支持更多的数据类型在tensor加速，比如bf16甚至fp8，附带就是flash-attention(2+)依赖硬件架构
- 从CUDA **12.8**开始，英伟达官方不再对maxwell(cc 5.2/5.3)、pascal(cc 6.0/6.1)、volta(cc 7.0) 提供更新，**驱动还可以正常安装，加速卡也可以正常使用**，但它们被标记为过时架构，选择时需要评估。

- 魔改技术已经非常成熟了，稳的一批，我上了4块涡轮散热的，卖家送了NVlink, 不到1w块钱，服务器就有了88G显存

- 只能相邻两张卡互联，而且两条nvlink速率一般~当然比PCIe还是好多了
  - 实际跑ollama推理，nvlink没起什么作用

- cuda12 用不了这个2080ti
  - 能用，20系要说有啥弊端那就是不支持bf16，而且这卡现在看性能也不行了，也就5060的性能
- p106这个10系的都能装cuda12
- 别说p架构了，我tesla m40都装上了12

- 20系不支持bf16和fp8，有些新模型根本就跑不了
  - 我用的2080反正现在啥模型都能跑，主要是绘画

- 推荐，性价比是真的高，作为推理卡十分优秀，但训练的话要慎重。前段时间买了六张在家搭了一个六卡机器，用了快一年了没出过问题，总共加起来132g显存最终花费才不到2w。
  - 缺点也是有的，最大的问题就是架构比较老，不支持bf16以及一些比较新的算法。目前准备换成3080改20g或者搞两张4090改48g跑跑训练，顺便把之前2080ti的nvlink搭上
  - 最后，如果要搞训练，建议还是上30系以上的。不然会因为架构太老遇到很多坑。
  - 待机每天5度电，火力全开每张卡250w，一小时就1.5度

- 2080ti是二代NVLink，和3090三代nvlink不通用吧。

- 4090没有sli或者nvlink
  - lz的六卡机也没有往SLI上插东西啊。

- Turing架构的tensor core能跑fp16和int8，但是目前看bf16是趋势，还是得慎重
  - 30系以上的可以跑flash attention

- 4090 48G服务器都有了，我现在就在用8卡的
  - 大致讲下体验，支持bf16的混和精度模型训练在参照80GA100的batch-size的情况下，虽然4090要开grad_accumulation=2，但是速度比a100快一些，能到5.5:7.3 s/step。 不支持混和精度的模型就要慢a100一倍了
  - 没nvlink, 跑的是VLA的训练，一个是RDT，一个pi0，根本不能全参数，虽然io没卡住，但是如果模型没开bf16的混和精度训练的话慢一倍多了

- 魔改的2080ti你记得买三风不要买涡轮卡，温度高，噪音大，容易受不了的，我就是从涡轮卡换成了三风，噪音问题基本解决

- 3000以内魔改的2080ti确实就是最佳选择，
  - 这小一年群里几百号人翻来覆去讨论过无数次，最终结论都是魔改2080ti性价比最高
  - 这是你能得到的最便宜的20g以上显存且性能过得去的卡了，我自己也炼丹玩儿，卡钱是赚回来了的

- 不支持bf16是硬伤，剩下的就是你买了大概率就是接盘侠了，这卡在未来不仅打游戏的看不上，炼丹的也看不上。

- 在2k出头的价位不算差，但是V100 16GB和3080 20GB的性价比更高

- 3080 20g要3千多了
  - 能跑BF16就值回多的600-700了。如果不要保修的话闲鱼有2600左右的

- ## [2025年AI本地部署性价比之王！双卡V100！32G显存，低价高能，碾压2080Ti 22G - 知乎](https://zhuanlan.zhihu.com/p/1927666998030078159)
- 千问3 32B模型在V100上的token生成速度为每秒20.34个，2080Ti则为13.43个；DeepSeek R1 32B模型在V100上的速度为每秒21.28个，2080Ti为18个。

- V100不支持flash- attention、bf16、awq、sglang新版本也不支持v100了，显卡太老了，新的加速策略用不了，速度还不如消费卡呢。
- 对SD跑图来说，不支持int4、fp8、fp4，不能用nanchaku加速。SD也不能多卡显存叠加。
- stable Diffusion跑图，很多模型都用不了的。没啥意思

- 很多推理特性不支持，远远没有2080ti好

- V100确定一千就能买到？
  - 核心板吧，散热转接加起来16g的3k，32g的5k，毕竟是6年前的东西了
- 大概1000左右可以搞定的。我都1000一套卖的，还是改的水冷。nvlink 32g，也就2300卖了

- ## [聊一聊Mi50这张显卡（自费购入） - 知乎 _202508](https://zhuanlan.zhihu.com/p/1935428196653838934)
- 在500元价位，这张卡拥有其独有的16G大显存，想本地部署LLM的可以冲一冲。贴心的卖家已经帮我刷好了RadeonProVll的vbios（提示：这张卡只有在镭7的vbios下才会主动进行视频输出，很重要！），
  - 本地部署DeepSeek32B的模型略显吃力，毕竟架构挺老了而且我只有一张卡，有条件的可以多卡交火（支持的，有接口），
  - 游戏方面流畅运行倒是不赖，1080P下，搭配E5-2680V4、DDR4 2400的情况下，CS2高画质全局稳定150帧，流畅运行肯定称得上，
- 对我最有影响的应该就是这个沃伦卡的 噪！音！ 真的很TM吵，跟体育老师不停吹口哨一样
  - 但好在已经有双风扇版本，当时图便宜加上没买过涡轮卡，脑子一热，一失足成千古恨啊 
- 显卡光有硬件是不行的，软件层面也得打磨打磨
  - 这张卡在这个价位段，就作为一张专业生产力卡来说，我可以拍着胸脯说出AMD YES！毕竟这个价位的N卡不是1065、1063就是40hx这种要么显存小，要么视频编解码能力被砍得比路易十六还惨再或者是魔改锁驱，我是喜欢小机箱的人，小板这种只有一下x16槽的无头骑士可用不了

- 这卡的minidp好像不带音频输出
  - 我插耳机用的

- 功耗太高了，不适合看视频上网用。

- https://www.zhihu.com/question/628771017/answer/1928750084457230617
  - 关于LLM模型生成速度：N卡CUDA强，A卡一般。个人用途一般更在乎模型智商水平而不在乎生成速度，因此显存大小就是王道，无脑选大显存/内存配置，CPU推理性价比更高，可以运行超高参数，如deepseek 671B，CPU推理吃内存带宽，通道数一定要满。如有生产力速度需求，无脑选4090 48G。
  - AMD MI50 32G一代神卡，在windows下只能用Vulkan跑，在linux下可以用ROCm，70Bq4生成速度10tk/s，性价比非常高，可惜跑不了comfyUI，想要画图必须自己手组散装webui。
  - SDXL模型占用显存不大，仍然是8GB够跑。但是只能在N卡上跑的好，A卡优化很差。
  - 文生视频模型占用显存巨大，一般消费级显卡只能生成480p清晰度1分钟以内时长的视频，720p及以上必须用大于48G显存的N卡。

- [大船靠岸，AMD MI50 16/32G显卡晚来一步 - 知乎](https://zhuanlan.zhihu.com/p/1896388031436530191)

- [MI50 32g 我说这个就是史 - 知乎 _202504](https://zhuanlan.zhihu.com/p/1893227599272067712)
- 价格是720包圆，现在被jsq炒作老高了
- 这个卡刷不了bios，不可能 显示输出
- amd通病，你想玩ai生态支持稀烂
- 总结：鸡肋中的鸡肋，不如mi50，2080ti 22g
- 貌似反转了，这个卡听说能刷bios有视频输出，这个特性导致他可能不会太fw，但是我觉得32g的显存还是太大了没必要，作为低廉算力卡来说确实还可以
  - 2080Ti 22g在前面顶着呢。GCN架构玩游戏真的不错但计算性能太低，即便不考虑功耗散热噪音，玩游戏16G版够够的

- 如果生态好的话 32g 显存怎么可能才不到一千，2080 ti 22g 现在都要快三千了。一张 2080 ti 22g能买三张 mi 50 32g。

- 你忘了提一个弱点，300瓦的功耗，100瓦的性能
  - 倒不只是电费的问题，这样电源散热噪音都会增加，太麻烦了

- ROCm的支持说不定啥时候就没了，到时候干瞪眼

- 我的结论是目前单卡运行 gemma3 27B 或者 qwq 32B，Mi 50 32G 显卡就是答案。1000 元显卡带来 20tokens/s，还有谁？
  - 按 AMD 官方教程安装一下 rocm 和驱动，rocm 版本 6.3.3 已经验证， 一定是可以的。
  - 按 ollama 官方教程，手动安装 ollama 和 ollama-rocm。
- 用LMStudio的Vulkan后端即可，免折腾ROCm，Qwen3和Gemma3都能跑，速度比ROCm打七折

- 现在ktransformer支持amd显卡了，弄个512的ddr4内存+四张MI50应该可以跑通Deepseek671b，等一手最强性价比的Deepseek满血版方案，希望大佬可以试试

- 32G的，双卡可以运行70B模型，6-8tokens/S，基本上属于可以用的范畴了，如果是VLLM估计还能更快，我用的ollama，就是散热要搞好，我里面插涡轮，外面风扇吸，勉强可以控制

- 我觉得其实蛮好的, 大容量并且大带宽的显存, 并且还有服务器的稳定性, 这个卡的32 64算力高的夸张, 和V100一样, 作为一张专业卡是相当够用的

- ## [32GB Mi50's were getting so expensive that I ended up buying a 32GB w6800 for about the same price instead : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pob44f/32gb_mi50s_were_getting_so_expensive_that_i_ended/)
  - Much better prompt-processing than the Vega iGPU's
  - 512GB/s vs 1TB/s memory bandwidth on the Mi50. Per benchmarks the mi50 doesn't actually get 2x performance on token-gen, but it's definitely something. If TG is your highest priority this is reason to consider the Vega cards
- What is the performance difference? Mi50 vs 6800. Mi50 is not very useful, outside of text inferencing, which is does great. RDNA actually has compute capability, and is supported going forward CDNA looks more and more like RDNA5 or 6.
- the w6800 does pretty good. Its much faster in prompt processing. 6800 has more compute and modern design supported by amd, and works in windows without hacks. Its the much better generalist card.
- where?
  - eBay. Follow a bunch of the bigger hardware reseller accounts and you'll eventually find short-lived deals on workstation cards.

- ## [NVLINK port support for RTX 3090 Ti, RTX 4080/4090 - Gaming and Visualization Technologies / Raytracing - NVIDIA Developer Forums _202210](https://forums.developer.nvidia.com/t/nvlink-port-support-for-rtx-3090-ti-rtx-4080-4090/231140)
- I just checked RTX 3090 Ti, that also does not have NVlink port. Am I right?
  - Yes, still there is no support but data transmission over PCIe board

- Until NVIDIA thinks about bringing NVlink bridge back, RTX 3090 is the last gpu of this tech.

- ## [3090 and 3090ti sli/nvlink : r/nvidia _202203](https://www.reddit.com/r/nvidia/comments/tslbxy/3090_and_3090ti_slinvlink/)
- Nope, SLI/ NVLink needs the exact same card to be paired with in order for it to work and pool the memory. I meant to say that you need the exact same series of card, cant mix and match a 3090 with a 3090ti. But yeah it doesnt matter which brand of a particular series you get. 

  - ## [AMD MI50 32GB better buy than MI100? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o2x0bv/amd_mi50_32gb_better_buy_than_mi100/)
  - While it's officially dropped from ROCm 7, we can still get it to work if we copy some files manually.. obviously this will sooner or later stop working but then we'll have Vulkan.. which (with llama.cpp at least) seems to be almost at a performance-parity with ROCm (or faster?).
- Mi100 is still too expensive. I thought they all have vulkan support.

- As Mi50 owner, I would say this: ROCm is a pain in the ass. I see no reasons to buy better AMD cards cause you'll will constantly search for solutions for some software bugs. Vulcan won't save you on Mi50, as performance is equal or worse - vulcan seem do be not as optimized for that chip. With Mi100, you'll be in ever rpugher shape because this card is not popular amongst the enthusiasts, so nobody will optimize the software for it. Given that Mi50 33GB costs $120, buying Mi100 over it is a useless waste of money; Mi100 should go down in price significantly before it becomes reasonable for a homelabber.

- ## [rtx 4090 vs rtx 5090 vs rtx 4090 48gb vram? : r/StableDiffusion _202505](https://www.reddit.com/r/StableDiffusion/comments/1km4snx/rtx_4090_vs_rtx_5090_vs_rtx_4090_48gb_vram/)
- across various benchmarks rtx5090 is around 30% faster than rtx4090 in terms of "raw power". It also has native FP4 support, which can increase speed by ~x2 and reduce memory usage ~x2 for use-cases where fp4 models available.
  - So, choice depends really on your use-case.
  - If you run repetitive tasks and it fits into rtx5090 32GB VRAM, especially in fp4 format, then, this is the way.
  - as an all rounder and for different experiments, rtx4090 with 48GB can be more interesting.

- If you have a workflow with multiples models, vram is king as it allows you to avoid loading / unloading models. It's the slowest part of the process in generation. With enough vram, you can keep all models loaded, gaining a tremendous amount of time each generation.
  - Example: generating with model A which has very good prompt understanding but shit styles, glossy skin etc...then inpainting / upscaling with model B which has better style and so on.

- ## 🆚 [RTX 5090 vs RTX 4090 48GB (or RTX 6000) : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mo92ou/rtx_5090_vs_rtx_4090_48gb_or_rtx_6000/)
- The jump from 32GB to 48GB is a big jump, but the question is whether it's actually relevant today. 
  - With 32GB, you can run 24B, 27B, and 30B MoE at 8 bit and blazing fast speeds. You can run 32B at Q6, and even 49B at Q4. You can run basically any diffusion model as fast as possible with no limits at 8 bit.
  - 48GB lets you run the same models with higher context length, or lets you run 70B at Q4KM. The problem with this however, is that the 70B class of models has been stagnant for a very long time, so it's questionable if there's actually any benefit of running models in that size class right now. Any model larger than that is generally an MoE and will need partial offloading to RAM anyway. For example, if running GLM Air 106B, there's not going to be a massive speed difference between 32-48GB, because the bottleneck is the RAM.
  - The RTX 6000 Pro 96GB is an amazing card, but it generally has the same problem as the 48GB. With 96GB, that opens up the path for 70B and 100B, but not really any larger. You still won't be able to run 200B+ without partial offloading, which means that again, RAM is the bottleneck.

- One question I have is the context length. Using this calculator, for a 32B model at Q8, I'd have less than 4K context even with the KV cache at Q8. So if I'm adding files of any significant length to the context, then that also skews for more VRAM? Or can the context also be offloaded to RAM?
  - Yes, context does take up VRAM, and VRAM consumption scales linearly in proportion to context length. The exact amount of VRAM for a certain amount of context varies based on the size of the model, and architectural choices like Sliding Window Attention and Grouped Query Attention. Hence, the exact memory usage footprint is unique to the exact model, so that website is likely not perfectly accurate. That said, the context length takes up VRAM whether you use it or not, and does not increase automatically if you exceed it.
  - You can offload context to RAM, but that will cause a massive slowdown overall, and I can't really recommend it except for very specific use cases.

- If you're running multiple AI applications simultaneously, then yeah probably.

- FLUX for image generation needs something like 12GB.
  - WAN2.2 for video generation can be ran on as little as 8GB.
  - Qwen3-30B at Q4 requires 18.6GB, the Q8 is 36GB.
  - Blender for 3D assets recommends >8GB.
  - Photoshop recommends >4GB.

- ## [单卡双芯48GB 铭瑄Arc Pro B60 Dual Turbo专业卡规格详解 - 知乎 _202505](https://zhuanlan.zhihu.com/p/1908505488590636946)
- 第二代锐炫Pro专业卡，同样基于“BattleMage战斗法师”架构，有两款产品
  - Pro B50 16GB，16组Xe核心，2048sp，128bit显存带宽，TBP整卡功耗70w
  - Pro B60 24GB，20组Xe核心，2560sp，192bit显存带宽，TBP整卡功耗120-200w

- B580 24GB的传闻已久，不算新鲜；最出人意料的是铭瑄，拿出来的Pro B60产品是单卡双芯
  - 双DP 2.1 + 双HDMI 2.1a满血输出，均可支持8K 60hz或4K 240hz；由上至下，分属于两个不同的GPU
  - 这张显卡并未集成PCIe桥接芯片，PCIe Gen5 x8 + PCIe Gen5 x8，需要主板本身支持PCIe x16通道拆分。
  - 所以电脑设备管理器内显示，应该显示为两张Pro B60 24GB，而非单张Pro B60 48GB，只有通过相应程序，才能实现GPU、显存统一调用，料想不会有驱动程序层面的特殊支持，和其他品牌的单卡单芯无异。

- 这么说就是两个显卡，插在一个插槽，并且两个卡都是pcie5.08 这样每个卡的带宽都砍掉了pcie 5.0 *16 的一半。 这种东西有鬼用啊。还不如插两个显卡
  - 1，现在的GPU性能跑不满带宽，包括5090用PCIE x8都没问题；
  - 2，AI模型推理其实对GPU性能要求不高，主要是卡显存。
  - 3，B580原生Gen4 x8，B60升到Gen5 x8，两GPU集成到一块儿并没阉割带宽。

- 后续所有的锐炫中高端家用显卡都会复刻，Q3发布的B770 16GB当然也会有相应的32GB专业卡；连AMD也表示会跟进产品。

- 牙膏要是有类似nvlink的东西那价值还能上升，毕竟甭管训练还是推理，瓶颈都在这个pcie 5.0x16的64GB/s 上。

- 48G显存玩SD画图不得爽死。话说现在SD对intel的支持咋样了？能玩不？
  - 不怎么行，只能pf16否则加lora就会黑图，训练目前我还没跑通过。而且双芯卡实际是两张卡，常见的部署框架comfyUI不支持多卡

- ## [显卡日报10月8日｜笔电RTX5090显存容量24G？ - 知乎 _202410](https://zhuanlan.zhihu.com/p/853223258)

- 整理下笔记本RTX5090的可能参数，可以看到，和台式机的RTX5090差距还是比较远的，连台式机显卡一半的规格都没有，可能是有史以来笔记本和台式机差距最大的一张旗舰显卡
  - 此外，笔记本RTX5090相比于上代笔记本RTX4090进步也不大，最大的进步可能就是换了镁光GDDR7显存，显存带宽明显提升

- CPU能加个12400不带K不？
  - 已经不带K了

- [笔记本电脑5090和5080游戏差距较小｜显卡日报4月3日 - 知乎](https://zhuanlan.zhihu.com/p/1890877968840119676)
  - 根据VideoCardZ报道，最近著名硬件媒体Notebook Check测试了相同配置的RTX5090笔记本和RTX5080笔记本，这两台笔记本用了相同的模具，显卡功耗上限都是175瓦，都搭配锐龙9955HX CPU，据说这款XMG是机械革命的海外贴牌厂。
  - 在《赛博朋克2077》中，4K分辨率下两款笔记本的平均帧率差距仅为12%，远远小于两者的价格差距
  - 根据VideoCardZ统计，目前北美市面上最便宜的RTX5090笔记本比最便宜的RTX5080笔记本还贵了72%，所以在游戏差距这么小的情况下，毫无疑问RTX5080笔记本更值得入手。
- 多8g显存利好生产力，游戏性能的话功率给不足的情况也不大好提升

- ## [当前4090笔记本显存为什么是16g？ - 知乎](https://www.zhihu.com/question/599743802)
- 移动版4090的本质: 用了桌面4090的名字，使用了桌面4080的规格，跑出了桌面4070 Ti的性能

- 移动版的4090硬件参数基本上就是台式机4080
  - 台式机的4080最高功耗在400w左右（不同品牌型号略有差异），移动版的4090最高功耗限制在175w左右（不同散热规模笔记本可能略有差异）

- 256Bit的显存位宽咋上24GB？

- ## [笔记本端RTX4090和RTX4080差距到底有多大？ - 知乎](https://www.zhihu.com/question/581865855)
- 2024年8月更新，以华硕ROG枪神8 超竞版系列作为参考
  - 从各项跑分中可以看到RTX4090相比RTX4080，高出10-16%
  - RTX 4090 Laptop拥有完整的256位带宽，RTX 4080 Laptop其显存位宽降低到192

- ## [笔记本的4090显卡相当于台式机的什么显卡？ - 知乎](https://www.zhihu.com/question/594215351)
- 该显卡用了台式机RTX 4090的名字，硬件规格上和台式机RTX 4080相似，性能上和台式机RTX 4070 TI相近。
  - 硬件规格上，笔记本RTX 4090 Mobile使用AD103核心，采用台积电N4制程工艺，搭载9728个CUDA单元，16 GB GDDR6显存，显存位宽为256 bit；
  - 同样的，台式机RTX 4080也使用AD103核心，采用台积电N4制程工艺，搭载9728个CUDA单元，16 GB GDDR6X显存，显存位宽为256 bit。与笔记本RTX 4090 Mobile在硬件规格上代的区别就是一个是GDDR6一个是GDDR6X显存。
- 但是，笔记本RTX 4090 Mobile的性能还是远不如台式机RTX 4080，主要因为功耗喂不饱。台式机RTX 4080的TDP为320 W，对应的Boost频率为2505 MHz，而笔记本被锁了功耗墙，不同功耗限制下RTX 4090的Boost频率如下：
  - RTX 4090 Mobile 120W = 1335-1695 MHz
  - RTX 4090 Mobile 130W = 1425-1815 MHz
  - RTX 4090 Mobile 140W = 1500-1950 MHz
  - RTX 4090 Mobile 150W = 1620-2040 MHz
  - RTX 4090 Mobile 175W = 2040-2040 MHz
- 因此，最后满血的RTX 4090单精度浮点算力大概是39.69 TFLOPS的水平，和台式机RTX 4070 TI的40.09 TFLOPS差不多，未来要是RTX 4090 Mobile解锁200 W功耗墙可能有希望超过台式机RTX 4070 TI

- ## [芯动科技发布「风华 3 号」全功能 GPU，该产品都有哪些亮眼性能？ - 知乎 _20250923](https://www.zhihu.com/question/1953762444674565105)
  - 芯动科技“风华 3 号”全功能 GPU 昨日在珠海香山会议中心正式发布，其采用全国产底层设计，同时拥有 AI 智算算力和 8K 重度渲染算力，兼容 DirectX12、Vulkan1.2 等图形接口，并适配统信、Windows 等系统。
  - 芯动科技“风华 3 号”全功能 GPU 在行业内率先实现国产开源 RISC-V CPU 与 CUDA 兼容 GPU 的深度融合，可一站式覆盖大模型训推、垂类多模态应用、科学计算与重度图形渲染
  - 在生态方面，“风华 3 号”在软件端兼容 PyTorch、CUDA、Triton、OpenCL 等主流 AI 和计算生态、和 DirectX、OpenGL、VulKan 等渲染生态，适配统信、麒麟、Windows、Android 等操作系统。
  - 在大模型方面，“风华 3 号”是国内首款单卡配备 112GB + 大容量高带宽显存和自研 IP 的全功能 GPU，突破目前国产 GPU 显存和多卡搬运的上限，单卡可支持多用户 32B / 72B 大模型；单机八卡能直驱 DeepSeek 671B / 685B 满血版大模型。

- [GPU Fenghua No.3, 112GB HBM, DX12, Vulcan 1.2, Claims to Support CUDA : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1noru3p/gpu_fenghua_no3_112gb_hbm_dx12_vulcan_12_claims/)

- ## [如何使用intel的gpu和npu跑大模型？ - 知乎](https://www.zhihu.com/question/5293002844)
- 去下载ollama intel版，运行，然后就能调用核显跑模型了，但32g本子核显只能调用20G

- 目前比较适合半小白的办法，就是下载intel的ollama portable zip
  - 以上这俩应该都是基于llama.cpp的sycl后端优化的。
  - 其实在NPU或GPU上运行大语言模型还可以用OpenVINO。但不是很适合小白，OpenVINO更适合有一定开发能力的用户。

- 你需要用openvino，推理的时候指定推理的设备npu，gpu还是cpu，就可以把推理运行到你想要的设备上。你可以到openvino的notebook找到很多例子。

- intel自带的gpu不是普通显卡，不能用gpu这个选项，

- ## [3090 相当于 40 系的什么显卡呢？这款产品的优缺点分别是什么呢？ - 知乎](https://www.zhihu.com/question/681021828)
- 3090资深用户，首发购入一直用到4090首发, 
  - 3090理论跑分性能等于4070tis super。
  - 但是3090显存更大，在ai方面性能更强，可以跑一些量化大模型，4090能跑的3090都能跑。
  - 3090的<能耗比>比4090差很多，因为3090是三星8nm工艺，相对台积电5nm差距非常大。相同功耗下4090性能超3090 60%。
  - 3090功耗上限非常高，最高功耗产品为evga 1000瓦水冷款，从400瓦到1000瓦性能提升10%。由此可见能耗比之差。

- AI算力来说，cude算力表现，跟RTX4070差不多；

- ## [3090 24g和3090ti 24g从哪能买到新的? - 知乎](https://www.zhihu.com/question/585256727)
- 3090/ti基本上不会有新的了，ti还好点，但是货本来也不多，标新的店价格都高，甚至高过4080钙中钙
  - 你的情况，要么4080，要么4090，要么二手3090/ti将就点，4070ti的带宽太低了，显存12G其实也能用。
  - 其实3070、3080/ti也都是可以生产力、渲染的。非特殊场景不会随随便便爆显存的。只是4070ti的显存低、带宽低了不说，cuda核心较3090少了30%

- ## [2x4090 vs 6000 ada vs L20 vs L40s: what is the bottleneck for llm inference/finetuning? : r/LocalLLaMA _202408](https://www.reddit.com/r/LocalLLaMA/comments/1exwc04/2x4090_vs_6000_ada_vs_l20_vs_l40s_what_is_the/)
- a 6000 > 4090, less power, no moving data between PCI bus/CPU/cache to GPUs. 1 48gb will often beat 2 24gb for fine tuning.

- The l40s is essentially the 4090 with more vram. It is exactly the same chip. Nvidia released the l40s because the 4090 chips were available and demand on H100 was too high / H100 production volume too low. The 4090 has transformer engine which boosts fp8 performance. If you want inference speed on fp8 and don't need advance nccl support I would go for the 4090s

- ## [网上传的沸沸扬扬的96GB显存的4090魔改版是真实存在的么？是怎么做到的呢，有人用过么？ - 知乎 _202502](https://www.zhihu.com/question/13164350111)
- 因为有全新L20 48G（可近似当作4090D 48G）在2.5万的价位压着，实际上现在4090的价格已经涨无可涨。
  - 👀 L20不支持nvlink

- 以上这些东西你都解决了，那你准备怎么过VBIOS检测？

- ## [2w左右的预算炼丹，2张3090矿卡还是一张4090? - 知乎](https://www.zhihu.com/question/592038342)
- 两年前帮同学装过双路RTX 3090炼丹炉，个人建议还是用单卡RTX 4090。
  - 双卡RTX 3090矿渣不容易安装，市面上开放式散热的RTX 3090的厚度普遍接近3-slot，至少要预留1-slot的散热空间，也就是说每张显卡要占用4-slot，目前消费级主板常见的PCIe区域宽度是7-slot，安装两张RTX 3090有点困难。而且桥接器NVLink Bridge的常见规格是2-slot或者3-slot，和上面说的4-slot占用空间有矛盾
  - 所以，要组双卡RTX 3090优先考虑涡轮版，一般厚度只有2-slot，体积更小，但是RTX 3090涡轮版矿渣的价格比非公版贵了1000元，再加上NVLink Bridge的价格，即便你捡矿渣，两张涡轮RTX 3090的成本也超过单张全新RTX 4090了。
  - 另外，双卡RTX 3090矿渣需要的额定功率更大。单卡RTX 4090的TDP是450 W，双卡RTX 3090的TDP是700 W，电源成本也是要考虑的，而且大功率电源满载的时候挺吵。

- 两张3090矿卡+nvlink (相对于pcie，大模型DP TP 2-3倍速度提升)
  - 性能对比（gpt2 1.3B 8batch 2TP，测试环境alpa/jax）
  - TP模式：结论带nvlink在148个all reduce的条件下，可以提升200%的速度 12.95s vs 38.53
  - DP模式：结论带nvlink的条件下，可以提升150%的速度 12.03s vs 31.15s

- 2张3090要组建带nvlink的平台比你想像的还要麻烦，和单卡4090比较一下
  - 主板: 双卡3090需要一个至少atx的带双PCIEx16插槽的主板，而且两个显卡插槽距离要是标准的3槽间距才行，而显卡厂商不会给你说这些数据很麻烦，很容易买错，4090就一般的matx就行，主板价格就能便宜几百
  - 电源: 双卡3090一般要买1400w左右的电源，4090一般850w就很够了，价格估计差价300到500左右
  - 显卡: 要组双卡考虑到nvlink一般最大3槽，只能选涡轮版或水冷版，比一般3风扇风冷单卡贵2000以上
  - 机箱: 双卡3090一般要支持atx的大机箱才能保证扇热, 4090一般的matx机箱就行，差价一般不会特别大
- 另外nvlink也要1500左右
  - 价格: 实际上要比单卡4090的价格贵大概4000以上
  - 功耗: 双卡3090烤鸡功耗估计要超过800w要远远大于单卡4090的450w，整机双烤估计要突破1000w
  - 质保: 双卡3090都是矿卡无质保，能用多久看脸，而4090全新带质保
  - 保值:30系默认矿，30系已经臭大街了，以后如果用不上了要出掉，30系不好出手，而40系名声好要比30系保值多了

- 两张3090都没有一张4090贵，一张4090是一张3090的三倍有多。

- 4090没有nvlink，大显存还是选3090ti多卡

- 有无nvlink到底有多大区别
  - 模型大小不超过24g 区别不大。 2块4090一般相当于2倍的batch size, Nvlink解决的主要是——能不能的问题。 比如模型大小超24g时
- nvlink只是增大带宽，并不会增大显存，如果你不人为把模型写到两张卡上，每个iteration两张卡各跑个的，然后梯度回传的时候两张卡要同步梯度，有了nvlink这个过程会更快。如果24g不够，你不人为写到两张卡上，两张卡也跑不了。

- 3090只能双卡下nvlink，没有nvlink的卡或跨两组用nvlink连接的卡会走pcie到cpu进行数据交互。你用的pytorch会用nccl自动选择合适的方式交互。

- 关于“3090只能双卡下nvlink”，这个资料您是从来看到的？
  - 当然所有PCIE GPU应该都受这个限制，唯一例外可能是DGX station上的四块A100
  - 3090只有双卡的bridge

- ## [NVIDIA Tesla V100 SXM2 - 2025年AI本地部署性价比之王！双卡V100！32G显存，低价高能，碾压2080Ti 22G - 知乎](https://zhuanlan.zhihu.com/p/1927666998030078159)
- 年初16GB显存的V100售价1000元，如今已降至600元，远超Mai50成为性价比之王。其算力可与1500元左右的RTX 2080 Ti 22G相媲美。
  - 唯一的门槛在于其接口设计：V100采用服务器专用的SXM2接口，而非常见的PCIe x16金手指。SXM2接口一侧为PCIe，另一侧为NVLink，支持多卡互联。
  - 通过200元左右的转接板和80元的散热器改装，仅需900元即可获得2080 Ti级别的性能。
- 单张V100显卡的显存为16GB，双卡配置可达32GB。目前消费级显卡中仅有RTX 5090具备32GB显存，但价格高达2万元起。相比之下，双V100方案仅需2000余元，使得22G显存的2080Ti瞬间失去性价比优势。

- 测试平台采用华擎B650M主板，因其仅有一个PCIe插槽，需在BIOS中启用通道拆分功能以支持双显卡。安装完成后，我们将对双V100系统进行性能测试。
  - 通过NVIDIA SMI工具检测NVLINK状态，可见GPU0与GPU1的链接状态均显示相同带宽值，表明两片GPU已成功互联且NVLINK功能正常启用。
  - 在参数相同的情况下，2080Ti的每次迭代耗时约为2.17秒，而V100的每次迭代耗时约为1.39秒。

- V100不支持flash- attention、bf16、awq、sglang新版本也不支持v100了，显卡太老了，新的加速策略用不了，速度还不如消费卡呢。
  - 对SD跑图来说，不支持int4、fp8、fp4，不能用nanchaku加速。SD也不能多卡显存叠加。

- 本质上还是单卡16G，没什么卵用，而且很多推理特性不支持，远远没有2080ti好

- ## [主要做生成模型，自用深度学习服务器买双卡3090还是买单卡4090？ - 知乎](https://www.zhihu.com/question/9062530414)

- 对于低算力场景，最大的性能瓶颈永远是浮点性能，因为这会决定你的训练时长。
  - RTX3090的浮点性能（FP32/FP16）35.6TFLOPS，RTX4090则高达82.6TFLOPS，几乎高出了3090一倍，显存带宽也略高，同时TensorCore的版本也更新支持更多数据格式。
  - RTX3090看起来有NV LINK，但只是个阉割版，用户确实可以在代码中将整个模型分配在两张卡上（需要完全手动实现），但是其带宽只有112.5Gbps，不到显存带宽的1/8，训练时会出现严重的性能瓶颈。买2张RTX3090 24GB并使用NVLINK桥连接并不意味着你能将其当作一张48GB显存的卡使用。
  - 另外RTX3090是挖矿重灾区，甚至曾经有一段时间单卡日收入能到120RMB，很容易买到矿卡。

- 双卡算力是逼近单卡的，虽然有代差，熟悉双卡后，对多卡也有了经验，很容易扩展到多机多卡。生成模型的训练离不开多机多卡。

- 3090ti没有性价比，双卡3090加nvlink也不错的记得内存配尽量大。4090不支持nvlink的，训练不推荐。

- 2080ti 22gb也是香的不行。追求价格，就买4张2080ti 22gb的更爽。不过不支持flash attention和bf16数据格式。

- 如果是训练为主，毫无疑问选3090x2。
  - 如果是推理为主，且显存占用超过24G，选3090x2；显存占用小于24G，选4090。

- 双卡吧，怎么也得让自己的代码支持一下ddp，不然以后卡多了还得重新踩坑。

- 去年我给某高校实验室攒机那会儿，恰巧把两套配置都折腾过。
- 先说双3090这茬儿，乍看显存怼到48G挺唬人，但您知道跑Stable Diffusion时显存带宽被PCIE通道卡脖子的滋味吗？
  - 上个月拿双卡跑1280x720图生视频，显存倒是富裕得能养鱼，可实际吞吐量比单卡就多出23%，GPU利用率曲线跟过山车似的…
- 不过您要是搞大语言模型微调，单张4090的24G确实容易把裤子卡到脚脖子。可别听论坛那帮敲锣边儿的瞎忽悠，实测用QLoRA技术能把70亿参数模型压进18G显存，这节骨眼儿上4090的第三代Tensor Core直接让训练速度飞起～
- 前些天给某美院动画系那帮哥们装机器，他们拿双3090跑渲染以为捡着宝，结果电源三天两头跳闸——整机850W电源满载时滋啦作响的动静，跟二踢脚在机箱里开party似的
- 要是铁了心玩分布式训练且预算绷得住电费，双卡能省下17%的迭代时间；可要是就图个痛快跑单卡大模型，4090那9%的FP32性能提升配上Dlss3技术，渲染输出时绝对能让您体验什么叫 原地起飞

- NVLink桥接器可实现相邻两张3090的并联，双向带宽最高600 Gbit/s（约75 GB/s），但仅支持两卡间点对点通信，无法实现多卡全互联（如GPU0与GPU1互联后，GPU1与GPU2仍需通过PCIe通信）；
  - 可买专用NVLink桥接器（如华硕ROG NVLink Bridge）并确保主板支持；同时需在Linux系统中启用TCC模式（关闭显示输出），并依赖第三方显存管理工具（如NVIDIA MPS）。

- ## [已有3090Ti一张，再增加一张卡，是选择增加3090Ti+NVLINK，还是增加4090？ - 知乎](https://www.zhihu.com/question/623563385)
- 3090.nvlink, 提前学习一下双卡怎么用，未来大项目都是多卡，纯粹的单卡做不了什么特别大的项目，纵使H100也是大把人用8卡。

- 炼丹是自娱自乐还是将来想拿来谋生？谋生的话大显存多卡任务协同是必修课，一张卡怎么学？

- 3090Ti的Nvlink和专业版的不一样，带宽减半, 也没有显存真正池化

- ## [4090不支持nvlink，在训练深度学习模型时具体的表现是什么？ - 知乎](https://www.zhihu.com/question/603522002)
- 没有[NVLink] 功能只是不能通过桥接器进行两两互联(即不能通过NVLink两两进行p2p)，但是对于多卡并行训练是支持的，可以通过device to host to device这种走[PCIe链路] 进行数据并行处理.
  - nvlink最高可以做到800GB/S，PCIE只有128GB/S
- pcie慢很多而且受制于主板

- ## 👷 [4090 48G涡轮版深度体验 - 知乎 _202502](https://zhuanlan.zhihu.com/p/22691935175)
  - ComfyUI跑flux fp16模型，图像宽高1000*1000，step20，跑完22秒左右，显存占用36G，大显存就是好。

- 能不能测一下与双3090 NVlink的差距
  - 看拼几块3090吧，你要2块肯定比不过4090 48G，NVLINk拼显卡还是有损耗的

- 现在有4090 48g三风扇版不吵了
- 一直正常用，就是显卡温度一直上90度，暴力风扇转速没法调小

- 改完还能打游戏吗
  - 可以正常打游戏

- 哪有靠谱销售渠道啊？
  - 想玩魔改 哪会有售后啊 不都是自己玩吗

- 性价比最高的是2080ti 22g，不过要换电源

- 这种售后怎么搞呢
  - 我是拿自己的4090去改的，花了5千5， 店家说有三年质保哎

- b站修电脑的张哥能修，只要不是核心坏了都能修

- [魔改的RTX 4090 48G卡值得选吗？ - 知乎](https://zhuanlan.zhihu.com/p/1888965700464406937)
  - 这卡我买了一张用了一个月了，分了540gddr5内存跑了满血版q2半个月了，没啥问题，基本在15到20tokens

- [技嘉RTX4090涡轮卡太吵怎么办？改这个水冷 - 小红书](https://www.xiaohongshu.com/explore/6713b9e70000000026037edd?xsec_token=AB3p2aSFwZpNJgLEWUwjbY4ZRQfalBGT1nX8ghdKLP2ls=&xsec_source=pc_search&source=unknown)
  - 涡轮卡，都放在服务器里面用的，如过你想放到PC机箱里面使用，那要做的生理克服首先就是噪音
- 那你把转速调低呗
  - 涡轮版本身散热就不如风扇的，调低有风险啊

- ## [丐卡值不值得买? - 知乎](https://www.zhihu.com/question/596939079)
- 要看具体型号。 举个例子，RTX 40系首发RTX 4090、RTX 4080、RTX 4070 TI三款型号，散热模具都超规格了，即便是丐版型号都用料十足，所以一二线品牌的丐卡是最值得买的
  - 但是，从RTX 4070开始情况发生了变化，“RTX 40系显卡散热过剩”的规律也被打破了。市面上的丐版RTX 4070普遍采用低廉的悬臂式散热方案，这种散热不能完全覆盖供电区域，容易导致VRM的个别地方过热。

- 当时初衷也是想看看丐版究竟够不够用，高阶版本拥有更帅气的外观（材质），更好的散热（风扇、热管的数量等）、更好的超频性能（benchmark可能还能看，具体到游戏帧数只能说：你懂的），但真正影响显卡性能的，是GPU和显存。不过，如果高阶版本溢价可以接受，可以选，比如更好的散热性能带来的是温度的降低，温度的降低更有利于整机的稳定性。

- 微星买万图师。现在万图师比超龙性能低不到3%价格整整多一千。微星万图师和[微星超龙] 差距就是游戏满载温度高13℃。

- 一定要相信老黄和苏妈的刀法，4070你就是芯片体质再好、供电再强、散热再稳，给它超冒烟了最多能刚刚好赶上默频的4070Ti
  - 显卡最重要的是里面的PCB那一小部分，核心、显存等等，外面那3P大空调之类的，对于纯粹的性价比爱好者来说，应该放到最次一级来考虑

- 我只知道第一次买显卡买最便宜的丐图师，直接让我桌子附近温度从春天变成夏天。自此下张显卡的温度是我考虑的因素之一。

- 丐卡再丐，理论性能都超越下级[显卡]，无非是供电和散热做的差点，达不到[功耗墙]没法超频，但是芯片总归还是那颗芯片。
  - 反过来说4070做的再好，再堆用料都不可能超越[4070ti]。只要售后质保能保证，在金额预算里面，买一块高级的丐卡也是可以考虑的。

- 够用就好吧，我买的4070s万图师的卡，感觉价位挺合适的，用着也稳定。

- ## 💡 [为什么50系列显卡出来，性价比没有提升反而40系列显卡涨价了？ - 知乎](https://www.zhihu.com/question/1902322217175463161)
- - 40系涨价是因为商家都在清库存，库存减少。仅剩的40系显卡集中到少数几个商家手中。但是市场的需求没有减少。需求不变，供应减少，价格必然提高。而且这几个商家的最佳策略就是涨价，因为以后肯定是要跌的，趁现在能卖高价必须卖高价。
  - 40系是不可能再大降价了。因为没有巨量的显卡下来击穿商家的库存。现在反而是商家那里没有库存，剩下的显卡只能惜售。

- 以前老黄的产能全部由消费级市场承担，所以每次新卡一发布，就会有海量的新卡砸盘，旧卡必须降价清仓否则会烂手里。
  - 现在可不一样了，老黄8成的产能被AI计算卡吃掉，投放给消费级市场的产能寥寥无几，新卡别说砸盘了，填补市场缺口都不够，所以老卡就有了奇货可居的价值，涨价也是理所当然的了。
- 为什么不增加产能？
  - 老黄是fabless，自己没有工厂，完全依赖代工，主要是找台积电，然而台积电每年的产能是固定的，全球大客户那么多，就算是老黄也做不到产能包圆，所以老黄能分到的产能是有限的，他想增产也做不到。
  - 这也能解释为什么有时候老黄会找代工，最主要的原因是台积电那边分到的产能不足以覆盖产品线。
- 拿着设计图纸多找几家代工厂不就有产能了吗？
  - 芯片这东西，比较特殊，他必须在设计立项的时候就敲定代工厂。
  - 想要找代工厂代工，自己是必须设计到门电路一级的布线，然而不同的代工厂，他的元件布局是不一样的，比如A厂的与非门是2x2布局，那B厂的与非门布局可能就是1x4了，换厂就没法做，因此一款芯片必须在立项的时候就决定好找哪家代工，设计好原理图，然后使用代工厂提供的EDA软件进行布线。
  - 大家想象中的像机加工一样，有了设计图就能随便找个工厂加工，在芯片领域是不存在的，哪怕你拿到了完整的4090布线图，找中芯代工，也是做不了的，除非你愿意重新设计布线，那就要先掏几千万美元的设计费，再掏上亿美元的流片费用，并且有流片失败全部费用打水漂的风险，非常划不来。

- 原则上是这样的，不过换厂也未必就代价很大。8Gen1和8+就是一年内从三星换成了台积电。
  - 早就曝光了，按台积电的生产周期，8gen1找台积电做，高通会有大半年的产品真空期，所以他一开始就立项做两款，三星工艺的8gen1先顶上，半年后再推出8+。台积电的产能预定起码提前2年，发现8gen1不行再改8+你这产能都排到2年以后去了。
  - 好像是细节记不清楚了，刚开始高通就是找了台积电和三星分别做一部分，哪知道三星做的发热量严重，最后不得已订单全给台积电了.
- 苹果6S上的A9处理器直接俩版本，三星和台积电的都有

- 国内还算是有良心的，50系出来以后，40系可以买到，稍涨一点价但还算有性价比。
  - 美国市场自从50系上市以后，正价的40系一夜之间全下架了，只有黄牛的高价卡在卖。
  - 在美国，NV 50系和AMD 9070/9070xt上市以来一直处于缺货状态，都被黄牛用bot买走了，普通人很难买到。比如Amazon上面正常价格的一直缺货，一堆非自营黄牛挂高价。
- 普通商家也不允许卖吗
  - 普通商家的都被黄牛买完了

- 40系出来的时候AI热刚刚兴起，[4090] 之所以价格爆炸，也是因为很多人都拿4090当生产力卡用，炼AI
  - 老黄是看到了40系，尤其是4090卖爆了的情况下，才决定50系挤牙膏，全力押宝计算卡上
  - AI卡卖的比游戏卡贵多了，价格可以说突破天际
  - 人家资本也不是傻子，比起花真金白银买算力卡（还可能用不了几年就被淘汰），还不如卷一卷算力，用便宜卡搞大模型。

- ## [5090D显卡比4090强的话为何没有被禁？ - 知乎](https://www.zhihu.com/question/9802980796)
- 5090d是nvidia创立以来性价比最差的显卡。
  - 5090d和4090d算力一样，但比4090d还差，因为4090d可以魔改48g显存，5090d不仅不能扩显存还禁止多卡互联，跑ai软件3秒锁死，要重启才能继续用，可以说只能玩游戏

- 中国特供版旗舰显卡RTX 5090D，虽然其AI算力削减了约29%，但是游戏性能却几乎并未缩水，价格为16, 499元起（略高于RTX 5090的1999美元，即约14648元的价格），将于1月30日上市。？性能差些，价格还贵些

- ## 🚀 [如何看待新推出的Nvidia推出的4090d？ - 知乎 _202312](https://www.zhihu.com/question/637218617)
  - 12999和4090价格一样。看了cuda规格是完整的ad102的百分80

- 老黄的刀法还是很精准的，这次RTX 4090D刚好卡在3A090出口管制条例的界限上。
  - “数据中心芯片”生效范围比较复杂，但是“非数据中心芯片”一刀切在TPP = 4800上，也就是说对消费级RTX 40显卡，TPP限制是4800上。
  - 而这张RTX 4090 D，该显卡搭载14592个CUDA 核心，加速频率 2.52GHz，该显卡搭载14592个CUDA 核心，加速频率 2.52GHz，显存为 24GB 384bit GDDR6X，显卡总功耗 425W，常规游戏功耗 302W。

- 这玩意有4090九成规格，应该还是在禁售范围内的（所以nv还限制了超频）

- 4090D这张卡本身，流处理器规模是4090的89%，Tensor Core和RT Core也是等比低削减，并未专门缩掉了Tensor Core的规模，显存也未阉割，L2甚至可能不变，估计综合游戏性能可以达到4090的90%-95%吧

- 都2023年了，还能在消费市场上见到大公司减量不减价的操作，只能说垄断还是厉害
  - 技术性垄断总比政策性垄断要好，最起码人家是凭真本事垄断的

- 这小砍一刀无伤大雅，依然有73.54TFLOPs➕CUDA➕24GB GDDR6X，吊打7900XTX跟4080以及新的4080S

- 全球芯片开始转向Risc结构，美国的大部分企业选择arm， 只有NVDIA目前的GPU和谷歌的TPU不是，但谷歌似乎也拥抱arm， 至少是用在其手机部分。 中国大企业却是拥抱RISC-V，这种开源的硬体架构规格，因为不需要给arm专利。英特尔也拥抱RISC-V， 表示与arm竞争。

- ## [魔改版4090 48G显卡性价比大探讨：真的值得入手吗？ - 知乎](https://www.zhihu.com/question/14343647195)
- 40系显卡的主要性能瓶颈是[显存位宽] ，和显存容量关系不大。这一点我们可以从4090和rtx6000ada两张卡得到验证。
  - 这一点我们可以从4090和rtx6000ada两张卡得到验证。
  - 4090和rtx6000ada拥有相同的架构的gpu核心，基本相等的cuda核心数量（一个是16384的cuda核心，一个是18176的cuda核心），基本相同的显存位宽（4090是1008GB/S，rtx6000ada是960GB/S）。
  - 两张卡只有显存容量不同（4090的显存有24g，rtx6000ada显存48g）。经过测试，两张卡无论是游戏性能，ai推理，结果都是差不多的。rtx6000ada并没有因为48g的显存容量而有更加优秀的性能。
  - 同样的结论还可以分析4090和4070得到。4090拥有16384的cuda核心，4070拥有5880个cuda核心。4090的cuda核心数量是4070的将近三倍。按理说，将近三倍的显存容量应该带来三倍的性能，但是4090的实测性能只有4070的将近2倍。4090的位宽384bit，4070的位宽192bit。4090刚好是4070的两倍。

- 粗略计算，每10亿个参数大约需要4G显存来加载，所以48G显存能跑120亿参数的大模型，如果是半精度的最多可以跑240亿参数的模型，显存不够大，模型都加载不进去，48G魔改出来的都是涡轮卡，插机架服务器用的，就不是给游戏玩家折腾出来的

- 我下周去找个工厂做一下测试，魔改的原理就是在[4090主板] 上加[显存粒] ，这个分两种一种是他们买的[3090主板]，换成4090芯片，然后加焊接24G显存粒，加两个。这种俗称消费级，就是需要每天关机一次，要不然估计主板顶不住，毕竟是特么的3090改
  - 另外一种就是基于4090主板，加焊显存粒，这种理论上比较OK，但是还没有实测，准备带上显卡去深圳找人魔改一下，要是能成了，那就我就开辟一个魔改业务，本来南京也有，但是南京没有家里创啊，产业链有点拉。只能招聘那些修手机来干

- ## [导师给30w预算装4-6卡服务器，目前打算上5880ada，要噪音较低、不要液冷，求合适方案？ - 知乎](https://www.zhihu.com/question/1939707476724389292)
- 5880满载功耗仅285w，比3090都低，涡轮也很静音。

- https://zhuanlan.zhihu.com/p/1939741761053364343
  - 之前我分享过，在RTX Pro 6000 上执行ollama与gpt-oss-120b，效率麻麻哋，不过，用它来运行vLLM却是一把好手，特别是主流的32B模型: Qwen3-32B，能达到22 token/s的速度，
  - 对比上一代卡皇5880(6000 ada的小兄弟)怎么样呢？实测过，2x5880也就才24 token/s。

- [英伟达中国特供版RTX 5880发布！性能比旗舰大砍近25%，比RTX 5000只高6% - 知乎 _202401](https://zhuanlan.zhihu.com/p/676491377)
  - 相比于旗舰级RTX 6000，定制版5880在性能方面可谓是大幅降级——CUDA核心少了23%，单精度浮点性能低了24%。
  - 实际上，它的表现更加接近RTX 5000——两项参数分别提升了10%和6%。

- ## [双RTX A6000显卡做深度学习，使用nvlink桥接器能实现显存共享成96G吗？ - 知乎](https://www.zhihu.com/question/455953236)
  - 双RTX A6000（显存是48G）显卡做深度学习，使用nvlink桥接器能实现显存共享成96G吗？插上了A6000的安培架构的桥接器，输入nvidia-smi nvlink -i 0 -s 显示的是速度14GB/S，不是显示的active，然后跑训练，还是只能使用48G的显存。
- NV的桥接器功能其实在宣传上有些问题，加了桥接器其实也完全不可能二卡合一、显存倍增，还是两块完全独立的显卡，桥接器只是让两块显卡之间可以快速交换数据，不用再从CPU那边绕一大圈；至于用了双卡以后提升了多少性能，主要看应用软件本身对多GPU优化的怎样，不同的应用软件的表现完全不一样，可能1+1接近2，也可能1+1≈1.5, 也可能1+1=1，甚至可能1+1<1。
  - 最新一代的Ada Lovelace架构的旗舰卡RTX4090, RTX6000Ada和L40干脆把对NVLink的支持彻底取消了，可见目前这个功能在图形类应用的领域有多拉胯，这个功能现在成了ai计算领域的专有功能了

- 可以直接在显存间传输数据，不需要再经过内存了是吗
  - 理论上是，但是也需要应用软件支持此功能才行，这个要看算法的，实际上多卡的算法没那么简单

- NVLink不是单纯的显存叠加，48G变96G，而是会增加两张显卡之间的显存交互带宽。一般来说，多卡跑深度学习，一般是指数据并行，即每个显卡处理一部分数据。

- ## 🚀 [如何评价Nvidia A6000显卡？ - 知乎 _202010](https://www.zhihu.com/question/424306404)
  - 取消Quadro命名，采用10752 CUDA满血GA102核心，48GB的GDDR6不带X显存，供电接口为新8Pin接口（EPS-12V与传统Pcie-8Pin显卡供电口不兼容）

- 虽然说取消了Quadro卡的命名，但是这东西看起来依旧是和Quadro一脉相传，当然叫他“专业卡”或许更直观，
  - 一直以来，游戏卡和专业卡都有着一道非常明显的区别，那就是OpenGL驱动，专业卡能打，但是游戏卡不能打，虽然老黄有放出过Studio驱动出来，但是依旧是无法取代OpenGL驱动的地位

- A6000采用的还是N卡30系的安培架构，所以注意安装cuda还是需要cuda11.1及以上版本。
  - 一个有意思的点是功率300w，比3090的350w要低，可谓是低功耗高效能了。
  - A6000的48G大显存两倍于3090还是比较适合上大模型的，看过网上评价A6000的性能优势主要体现在transformer双精度推理和分布并卡训练，由于目前炼丹的模型要求real-time比较小，单卡足以

- ## [RTX A6000存在的意义是什么？ 同样的价钱为什么不买两块3090交火呢？ - 知乎](https://www.zhihu.com/question/483799457)
- 英伟达把消费级显卡和专业级显卡区分得还是很开的，游戏卡不支持多路NVENC流、不支持vGPU，不支持ECC自动纠错，openGL性能较差。
  - 如果你有跑科学计算的需求的话，ECC显存是非常重要的，可以说必备，这种情况下你只能用专业图形卡或者计算卡来跑。
  - 多路NVENC也可以很好地用在大型广播控制台内，用于录制推流。这也是游戏卡应用不到的领域。

- RTX A6000是基于NVIDIA Ampere架构的超高端专业显卡，搭载最新一代的 RT Core、Tensor Core 和 CUDA Core
  - 兼具 ECC校验、GPUDirect for Video、多GPU 支持、四重立体缓冲、Mosaic多显示器、Quadro Sync等功能。

- 因为老黄禁止数据中心使用游戏卡

- ## [8w左右的双卡4090或单卡A6000服务器，有什么好的推荐？ - 知乎](https://www.zhihu.com/question/646105848)
- 至强W的T7960塔式工作站，保守最大4*A6000的支持。
  - 上限为56C的W9-3495X；DDR5-4800内存；PCIE 5.0；应该够用的存储空间（可选RAID/NVME等高级选项）
  - W7-3465X+128GB内存+RTX4090*2/一个A6000，咬咬牙也不是搞不定。
- 搭载至强可扩展三代的双路塔式T550服务器，最大两个A6000。
  - 上限就不说了，DDR4-3200; PCIE 4.0；标配独立阵列卡以及150TB+存储空间也相当不错。
  - 这个性价比较低，不是很推荐。
- 主流的机架式解决方案，也就是PE R750服务器，支持最大3*A6000，但是建议尽量控制在两张，
  - 它有个姊妹型号叫做750XA，倒是可以支持到4*A6000，相应的也要稍微贵那么一点点。。。
- A6000优势在于桥接扩容显存，所以还是尽量选择塔式，可能用不上，但是必须要支持对不啦。
  - 所以我认为最优选择还是塔式工作站T7960, 8通道DDR5-4800+PCIE5.0啊，何其先进。

- 7960能只买机架和电源吗, 其它的想自己配
  - 最低最低，得带上处理器。内存硬盘显卡自己配去吧。

- [导师给了10w买深度学习的服务器，只要求2张a6000的卡，其他配置有什么推荐么？ - 知乎](https://www.zhihu.com/question/628269514)
  - 推荐用各个厂家的单路旗舰解决方案直接适配。 也就是基于AMD Threadripper PRO或者全新至强W相关的最新平台。
  - 例如业内非常优秀的戴尔Precision 7960 塔式。 性能上限应该是 56C112T；4TB DDR5内存（16个内存插槽）；满配10个3.5硬盘槽位；满配最大四张A6000, 属实的优秀
  - 或者说7960的小弟5860也不是不行 ，扩展能力稍差，但是支持两张A6000运行，应该也是没啥问题的。
  - 或者上一代Precision 7920也行，虽说是末期稍有涨幅，但是性价比依旧是强无敌，旗舰毕竟是旗舰，虽然说是上一代。不过两张A6000。。。。 肯定行。

- ## [装机配置讨论，单卡A6000or双卡4090？ - 知乎](https://www.zhihu.com/question/599204652)
- 6000ADA太贵，6000感觉太老，4090显存比较紧张，马上5090出来之后，肯定6000和6000ADA会降价，甚至届时5090说不定有32G显存，可能是更合适的选择。很纠结，于是目前拿之前入门时候购买的4060Ti16G在顶着用。

- 据我所知 A6000唯一的优势就是显存大，实际上考虑大显存都是考虑降低多卡并行通信开销的，一张也体现不了大显存优势...

- ## [实验室配置服务器，4090，a100和a800选哪个？ - 知乎](https://www.zhihu.com/question/595107162/answer/4153401353)
- 测试发现，L40速度与4090D相当，表现令人满意。
  - A100, 40GB, 312 TFLOPS, ¥90, 000+, 400W, 
  - A6000, 48GB GDDR6, 79 TFLOPS, 300W, ¥33, 000, 300W
  - 4090, 24GB GDDR6X, 330 TFLOPS, ¥12, 000, 450W
  - L40, 48GB GDDR6, 147 TFLOPS, ¥44, 000+, 350W
  - 厂商解释，由于中美博弈的原因，L40宣传上未定位为训练卡，但实际用于训练完全没问题。
- 虽然L40 的 FP16 性能（约 147 TFLOPS）在理论上优于 A6000（约 78.75 TFLOPS），但在实际训练大型模型时，它并不被广泛推荐，原因如下:
  - 优化与软件支持：深度学习框架（如 TensorFlow 和 PyTorch）通常会针对特定的 GPU 进行深度优化，特别是 A100 和 A6000。NVIDIA 的 Ampere 架构（如 A100 和 A6000）在训练性能上得到了广泛认可，许多训练算法和优化器都针对这些显卡进行了调整。而 L40 的推理优化可能不适合训练任务。
  - 计算架构：尽管 L40 的 FP16 性能较高，其计算架构和硬件设计可能不具备 A6000 的特性，例如 Tensor Cores 的优化使用。Tensor Cores 可以大幅提高训练过程中的计算效率，尤其在大型深度学习模型中。

- L40单卡训练是没问题，最大问题是不支持Nvlink
- a6000不比4090高多少，价格高这么多
  - 显存大

- 4090不支持多卡并联，也就是大模型是根本没法训得，它是单卡性能强，同时性价比高(阉割NVLink了，多卡带宽严重不足)。
  - a800是a100的阉割版，也就是说，有a100选，肯定优先a100。因为是要训练大模型，建议购买sxm版本的a100。

- 要玩stable diffusion，目前的版本4090足够用了，其他大模型先明白搞什么，自己训练还是跑跑lamma，glm6b之类的，自己训练稍微大点的模型基本都不够，先算清楚对显存的需求一般就能有决定了。所以个人建议，不知道跑什么或者只跑stable diffusion先上个4090，反正便宜。明确知道搞什么，根据需要可以测算出来
- 4090从头训练图片生成够用吗？有人实践过吗。这些。
  - 按原版模型原版训练方式从0训不太够，原版是A100X8X32训了15万GPU Hours，每张卡batch size=8，总批次8X256，粗暴点算24g的4090一个批次只能2~3，就算不考虑慢的问题，批次依赖也需要另外解决
- 问题的关键是为什么要从头训练，基础模型上微调耗费很小的资源
  - 有创新的诉求，然后微调不够用(具体面临的问题可能和大神们的不同)

- ## [双a6000和双4090哪个计算更快呢？ - 知乎](https://www.zhihu.com/question/664827604)
- 小规模数据，单卡能跑的情况，显然4090比A6000快的多。
  - 数据规模再大点，超出了双卡的存储空间，4090就跑不了了，毕竟A6000一块就能顶2/4块4090啊。

- [渲染建模，是一个A6000牛逼还是两个4090牛逼? - 知乎](https://www.zhihu.com/question/658932305)
  - 在不溢出显存的情况下渲染单4090比A6000起码牛逼2倍，双4090就是4倍，
  - gpu-z上面有数据，一个4090是一个a6000的140%

- ## [深度学习用什么卡比较给力？ - 知乎](https://www.zhihu.com/question/612568623)
- Nvidia的PC机显卡，分为三个系列，Tesla系列，Quadro系列，Geforce系列。。
  - 原先分别对应专业科学计算，专业图形显卡，个人消费级显卡领域等。
  - 从价格上看，同等算力的价格差不多是4：2：1。
- 在算力差不多的情况下，Tesla和Quadro系列的溢价溢在哪里了呢？
  - 主要是稳定性（加了ECC纠错机制），显存效率更高（HBM2 vs GDDR）, 显存容量更大（一般Geforce卡显存在10G左右，但Quadro和Tesla一般都是24G，甚至48G，还有卡间互联技术NVlink等）。
  - 个人用的话，Geforce就差不多了，如上一代的3090，价格～13000¥，算力也足
  - 可以上A6000，～30000¥，也还不错
- 在CES 2025展览会上，英伟达发布的采用Blackwell架构的显卡是GeForce RTX 50系列，包括RTX 5090、RTX 5080、RTX 5070Ti和RTX 5070等型号，对标40xx的显卡
  - Tesla系列，推出了B200，给数据中心用的，死贵死贵。
  - 目前暂未有Quadro系列的最新架构显卡发布，这个系列国内可用的最高配置是Ada5880, 大概5万块一张吧，次一点可用Ada 5000, 3万多一张吧。。

- 现在行情不好，价格丑陋。别说4090了，就连3090也涨价了不少。干脆搞魔改2080ti吧22G的。改好的一张2500块钱，买3张也就现在（2023.11.4号）一张3090的钱。然后上洋垃圾至强x99平台，服务器内存随便插满128g。电源用矿电源1600w，反正放实验室，不心疼。
  - 我半个月前想买4090，商家不发货。只能退款，当天晚上立马去问rtx a6000能不能发货，当时2w6的价格。那会商家还没反应过来。只是晚上不发货，凉凉。第二天商家已经改价成3w了。

- H100 ￥23.5W, A100 ￥13W，但现在一般人或公司不好买了，已经被禁购了

- ## [有没有便宜点的AI算力显卡? - 知乎](https://www.zhihu.com/question/634145498)
- 2080ti 22G，仅需2000出头
- 3080 20G，3090 24G 便宜且支持bf16

- 要便宜，大显存，L40系列看看。英伟达Ada Lovelace 架构，48GB支持ECC的GDDR6显存，两者的显存带宽都是864GB/S, 
  - L40S作为L40的升级版本，主要在FP32运算能力提示幅度为1.1TFLOPS，在TF32 Tensor Core TFLOPS、FP16 Tensor Core、FP8 Tensor Core、INT8 Tensor Core运算能力均提升 一倍左右。

- 要便宜，大显存，p40最合适。24g显存，价格800左右就可以入手。记得一起买风扇和电源转接线。
  - 900块拿下过p100，感觉已经是平民价里面最好性能的了，还有hmb显存。

- 租云服务呀，能选的专业卡多还能开票让老师走经费

- ## [4090 魔改 48g 显存是怎么做到的？ - 知乎 _202502](https://www.zhihu.com/question/11803840385)
- 4090显卡有两个兄弟，叫做l40s和a6000 ada，都用的ad102内核，这两个兄弟显存都是48g的。
  - 没有a6000 ada，要么是30系的a6000，要么是40系的6000 ada。我之前也搞错过。

- 魔改的4090 48G价格是2万2左右（给料的加工费是5.5k左右），同一代（40系显卡）核心的6000 ada 48G要5万2左右，上一代（30系显卡）核心的A6000 48G是3万2左右

- 3090芯片发售时，显存颗粒最大1GB，24GB显存需要24颗，PCB板正反面都有。
  - 4090芯片发售时，显存颗粒达到2GB，24GB显存只需要12颗，PCB板只有一面有焊盘。
  - 流出的4090 48GB改版显卡bios，正好发现4090针脚定义和3090一样，可以焊在3090PCB上
  - 这样4090芯片+3090PCB+24颗2GB显存+流出魔改显卡bios=4090 48GB显卡。
  - 显卡bios大概率不是x86指令，否则早就有个人魔改版，诱惑太大了。
- 有能力改的，大概率不想得罪英伟达。所以这种只能偷偷搞，没保障

- 它就是个混合体：4090核心+3090的PCB板+24颗2GB显存颗粒，而且还有下面几个巧合，任何一个失效都不成立：
  - 4090的核心和3090的核心针脚一样，所以它可以焊到3090的PCB板子上并被识别；
  - 3090用的是24*1GB的显存颗粒，板子没有限制显存颗粒容量，可以换成2GB的；
  - N厂内部流出了显存驱动、显卡固件居然能完美支持。

- 网上测评显示4090 48G 显卡还可以支持 FP8，甚至这款显卡也已经出走海外，来自加拿大的小哥在平台上晒出了自己在 eBay 上买的 RTX 4090 48G，售价要 3 万人民币起步。

- 不得不佩服皮衣刀客的刀法了。科技是第一生产力，刀客在逆天而行。
  - 皮刀客目标在于赚钱， 发展生产力只是你想法而已，人家才不管你发展狗屁生产力呢

- 和3090同一级别的专业卡是RTX A6000，48G显存，其它参数和3090差不多的，现在的售价仍然是3万元
  - 和4090同一级别的专业卡是RTX 6000ADA，48G显存，Cuda核心比4090多约2000个，售价现在6万元；
  - 略低一个级别的RTX 5880ADA，Cuda核心比4090少约2000个，售价在5万左右； 
  - 所以4090 48G 2.3W的售价，性价比极高

- a100性能远不如4090
  - 4090推理王者

- 驱动？卡的bios才更重要
  - 你说得对

- 其实就是传言流出来那版vbios，没有那版vbios，就没有后续48G。
  - vbios有数字签名会和芯片内的安全芯片作相互校验，因此绕不过去，而在2023年流出来了一个工具，可以把不同品牌的vbios（有数字签名版）互刷，所以拿到48G的vbios就等于有了48G的4090，无非是如何搬板，甚至有能力可以重新设计一张pcb来扩张，换句话说，如果未来有更大显存容量的bios流出，原则上也可以做更大显存的卡。
  - vbios签名是与GPU芯片内安全组件进行校验，校验通过时，GPU才会完全初始化。

- 既然4090 48G是用3090的PCB板魔改的 那为什么市面上都没见到魔改3090 48G的？按理来说3090成本比4090低得多啊
  - 30系没有对位的48g计算卡，bios会卡住点不亮。闲鱼上有很多3090芯片转移到4090pcb上的卡，价格还挺实惠，敢买的人不多。
- 因为3090没有48G的BIOS流出。4090的AD102核心还用于ada6000等专业显卡，出厂显存就是48G，说明AD102是可以兼容48G显存的，

- ## [为什么N卡一定要带cuda? - 知乎](https://www.zhihu.com/question/592464568)
- cuda又不是硬件……toolkit想装就装，不带也不会影响打游戏
  - 对于n卡来说，cuda本来就算是增值服务，对于很多开发者来说提供了好用又高效的开发接口。
  - 我是不认同把n卡和cuda划等号。但是cuda明显已经形成了开发者好开发-使用者体验高-N卡占有率高的良性循环。

- 因为现在的显卡的可编程管线都是通用的。除去光栅器等少数部分，像顶点着色器等等，驱动底层和硬件计算单元和CUDA其实都是共用一套东西。

- 至于说AMD没有CUDA，但是AMD有ROCm和OpenCL啊。只不过因为软件支持差，不好用，用的人少而已。

- ## [是否存在支持cuda的核显轻薄本？ - 知乎](https://www.zhihu.com/question/663409299)
- 不存在。cuda是英伟达独显的，N卡独占，是独显的功能。核显是基于CPU的，而CPU是因特尔和AMD这两家的。
- 不存在。Cuda是英伟达自研的只支持自家显卡的算法。核显是Intel和AMD CPU自带的。英伟达并不生产笔记本的CPU。

- CUDA是英伟达独家，目前核显轻薄本是Intel和AMD，自然现在市面上找不到支持CUDA的核显轻薄本。
  - 现在的Intel、AMD甚至高通主推的AI PC全靠NPU，但是目前应用软件层面能够调用NPU的寥寥无几。
  - 而CUDA支持各个软件应用的支持显然更加广泛。到时候大概率会出现英伟达的核显本才是真正意义上的AI PC。
  - 目前英伟达的GPU一大问题是显存容量较小，比如主流的甜点游戏卡RTX 4060就是8GB显存。现阶段跑本地的LLM、Stable diffusion瓶颈并不在多少多少TOPS的算力，而在于很容易爆显存，你连跑都跑不起来。
  - 未来英伟达自己的核显本，可以共享内存，本地的大模型和AI应用可能才会真正发展起来。

- ## [为什么说CUDA是NVIDIA的护城河? - 知乎](https://www.zhihu.com/question/564812763)
- 英伟达从cuda里学到的最重要的一课，就是软硬件捆绑。
  - 计算界cuda之所以厉害，不仅仅是因为它可以调用GPU计算，而是它可以调用GPU硬件加速。
  - physX也是，N卡限定。 甚至于说，如果需求量够大，英伟达把三维体积的有限差分操作，有限元的检测函数积分操作，全做成“电路板计算”也不是不可以。 同时配合着自己的软件体系一起往外推。
  - 这才是英伟达真正的组合拳。 在这套组合拳体系下，cuda扮演着胶水级核心航母的角色。还有其它护卫舰，而这些护卫舰都绕不开。

- 2007年6月，CUDA发布。在Nvidia的持续精耕细作下，CUDA已经成了科学计算领域的事实标准。
  - 等神经网络算法火了，Nvidia又大力支持，各大AI框架因此优先支持CUDA，形成了正循环。
  - 之后，Nvidia又发力与AI关系紧密的自动驾驶和机器人领域，推出了针对汽车的Drive系列芯片和针对工业机器人的Jetson系列。
  - 这一切，都是以CUDA作为软件切入点，最终，CUDA就成了今天的样子，变成了又深又宽的护城河。

- amd抛弃opencl了，推他自家的rocm

- 用fpga、甚至是更定制化的asic来加速，早就有了，性能超过nvidia的同类产品比比皆是，问题还是生态和总拥有成本。google也做了TPU，在内部用得也不少，生态还是干不过CUDA。性能有时候并不是决定性因素。
