---
title: tool-iot-devices-gpu-ai-ml-hardware
tags: [ai, gpu, hardware, iot, machine-learning]
created: 2026-01-15T15:43:36.953Z
modified: 2026-01-15T15:44:10.647Z
---

# tool-iot-devices-gpu-ai-ml-hardware

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 
# discuss-iot-unified-memory
- ## 

- ## 

- ## [Advice: Which MiniPC To Buy? (Framework, Bosgame, Minisforum) - AI MAX 395+/128GB : r/StrixHalo _202602](https://www.reddit.com/r/StrixHalo/comments/1r18v84/advice_which_minipc_to_buy_framework_bosgame/)
  - Framework - $3700
  - Minisforum MS-S1 - $3900
  - Bosgame M5 - $2850
  - The BOSGAME is significantly cheaper than the other options, but doesn't have a lot of the connectivity options that Minisforum and Framework have.

- I faced a similar question a few weeks ago. I went with a fourth option and ended up purchasing a Corsair AI 300 workstation. It is a little bit more expensive than Bosgame, but cheaper than the alternatives, and it comes with good support and a two-year warranty.

- Framework. They support LVFS so firmware updates are simple under Linux. Standard power supply so easy to replace in future. mITX so easy to move to different case. Basically good flexibility for the future.

- Having proper mini-itx board with normal PC power supply played a role in my choice. I can resell it later as a beefy server if push comes to shove or as a small gaming PC with the original case.

- ## 🆚 [Tested: AMD's Strix Halo vs Nvidia's DGX Spark : r/Amd _202512](https://www.reddit.com/r/Amd/comments/1pxs0dd/tested_amds_strix_halo_vs_nvidias_dgx_spark/)
- Strix halo doesn’t support FP8 since it’s on rdna 3.5. That’s a tough sell. If these machines used rdna4 they’d be absolute monsters. It’s unfortunate that only the 9070 xt and 9060 xt use rdna4. All of these awesome APUs being released would do so much better with rdna4 imo. Hopefully rdna5/udna1 is implemented in all products when it’s released.

- The Samsung Xclipse GPUs are based on RDNA, and they were used in the past in phones like Galaxy S24 (non-US/non-Qualcomm versions).

- Don't worry, AMD will continue releasing old RDNA iGPUs until Intel miraculously survive Intel's mismanagement crisis.

- ## 🆚 [DGX Spark vs AI Max 395+ : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o6izz2/dgx_spark_vs_ai_max_395/)
- I just ran some benchmarks to compare the M2 ultra.
- OSS-120B
  - DGX PP=817, TG=41
  - 395 PP512=350, TG=34 (Vulkan)
  - 395 PP512=645, TG=46 (Rocm) *per Sillylilbear’s tests
  - M2U PP=590, TG=70
- OSS-20B
  - DGX PP512=2053, TG=48
  - 395 PP512=1000, TG=47
  - M2U PP512=1000, TG=80
- Llama 3
  - DGX PP512=7991, TG=21
  - 395 PP512=1000, TG=47
  - M2U PP512=2500, TG=70

- NVIDIA didn't build this for our community. It's a dev platform for GB200 clusters, meant to be purchased by institutions. For an MLE prototyping a training loop, it's much more important that they can complete 1 training step to prove that it's working than that they can run inference on it or even train at a different pace. 
  - If you want to replicate GB200 environment as closely as possible, you need three things: NVIDIA Grace ARM CPU, Infiniband, and CUDA support. RTX 6000 Pro Blackwell only provides one of those three. Buy two DGX Sparks and you've nailed all three requirements for under $10k.

- If you want LLMs with working speeds and diffusion models with slow speeds, both devices are fine. Vulkan support for AI Max 395+ is really good, so you can get better performance with most llms than DGX Sparks (or at least the same) for LLM uses.
  - However, the main problem arrives when you try to use the latest non-LLM models such as TTS, openmcp, and omni models with video support, where you are dependent on ROCm for HIP. Most of these latest models are optimized and tested for CUDA, and they usually fail on Halo (even with ROCm 7.0).
  - I own a 395+, and since I am a developer, I am really happy with my purchase. I can keep multiple 30B MOE models in memory and can get a very fast response. Every day, I try to run new AI models on my system, but the success rate for non-LLMs is 40% compared to my 4090, where it is 90%.
# discuss-multi-gpu
- ## 

- ## 

- ## 

- ## 

- ## [128GB VRAM quad R9700 server : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qfscp5/128gb_vram_quad_r9700_server/)
  - I originally planned to pick up another pair of MI100s and an Infinity Fabric Bridge
  - But then I saw benchmarks for the R9700, particularly in the llama.cpp ROCm thread, and saw the much better prompt processing performance for a small token generation loss. The MI100 also went up in price to about $1000, so factoring in the cost of a bridge, it'd come to about the same price. So I sold the MI100s, picked up 4 R9700s and called it a day.
  - llama 7B Q4_0, 90.89
  - qwen3moe 30B. A3B Q8_0, 72.51
  - qwen3vl 32B Q8_0, 14.75

- It starts with you using the hardware you've got, then buying cheap ex-datacenter cards on ebay, then next thing you know you're buying every card in town. I cleared out my local Micro Center's stock of these GPUs lmao.

- Interesting, so you're getting PCIe 4.0 x8/x4/x4 (from the CPU) for the first 3 and then one more Pcie 4.0/3.0 x4 (probably from the chipset).. the 9700 is PCIe 5.0, so I'm guessing your memory interactions are slow, and probably worth bumping up to 96GB?
  - To get the necessary PCIe lanes, you can either bump up to Threadripper or Siena (I've got an 8224P), which breaks your AM5 desire...
# discuss-ai/ml-hardware
- ## 

- ## 

- ## 

- ## 🆚 [Mac Studi M3 Ultra vs Nvidia 6000 Blackwell : r/LocalLLM _202602](https://www.reddit.com/r/LocalLLM/comments/1qsv2p0/mac_studi_m3_ultra_vs_nvidia_6000_blackwell/)
- Nvidia RTX 6000 Pro if you need it to be fast. Mac if you need to run the best possible model and can accept that it might be slow. Simple as that.

- I have an RTX PRO 6000 and a M3 Ultra with 256GB RAM. The RTX PRO 6000 is quite a bit faster at both prompt processing (10x?) and token generation (3x?). Speed matters to me so I only use the RTX PRO 6000. I would only use the M3 Ultra if I wanted to run a model that was too big for the RTX PRO 6000. So far I have not needed to run a model that didn't fit on the RTX PRO 6000 but it is nice to know that I can with the M3 Ultra when/if I might need to some day.
  - The other thing about Mac is that you can now build clusters of them over TB5 for even faster AI - checkout exo:

- If you’re just asking it questions and you want the smartest possible answers, mac is probably the way to go. M3 ultra 512gb is by far the most convenient way to run big sota models at home.
  - If you are going to try agentic coding, image or video generation or anything that uses long context, be warned mac will be very very slow. For giving it a page or three of text and asking for an answer, you’ll be fine, maybe wait 10 to 30 seconds before it starts answering. More than that and it will slow to a crawl. Expect to wait half an hour or more for a response to finish if you’re using coding agents.
  - Rtx pro on the other hand, will be way faster but can’t fit the big sota models like glm 4.7, deepseek 3.2, kimi k2.5 etc
  - If you get an rtx pro plus a ton of ram you can run the big sota models maybe at the same speed as mac (possible with lower wait time for the answer to start) but then you have an engineering problem on your hands as to how to keep all that ram cool, not to mention it’s probably about as expensive as the m3 ultra now

- ## ["Introducing AMD Ryzen AI Halo, a mini-PC powered by Ryzen AI Max+ that delivers desktop-class AI compute and integrated graphics for running LLMs locally." - AMD is on the move! Would you get one? : r/LovingAI _202601](https://www.reddit.com/r/LovingAI/comments/1qiybwp/introducing_amd_ryzen_ai_halo_a_minipc_powered_by/)
- unified 128 Gb, lpddr5 8000.

- It's just a minisforum ms max

- ## [Gigabyte Announces Support for 256GB of DDR5-7200 CQDIMMs at CES 2026 : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q9xn78/gigabyte_announces_support_for_256gb_of_ddr57200/)
- Dual channel is useless, with model that make use of 256gb the speed'd be unuseablely slow
- This makes zero sense because Threadripper Pro exists.
  - 256GB (2x128) CQDIMM 7200 will probably cost about $4000 (based on upcharge for rarity and speed from 4x64 6400 currently at ~$3200)
  - But you can get 256GB (8x32) 6400 RDIMM for about $2100. Threadripper Pro has 8 channel memory so 8 channel @ 6400 is faster than dual channel @ 7200 for any task that you would actually need 256GB RAM for.
  - Threadripper Pro 9955WX 16c: $1799 + Asus Pro WS WRX90E-SAGE SE motherboard $1249 + 8x32 6400 RDIMM $2100 = $5148
  - Ryzen 9950X 16c $549 + Gigabyte Aorus Tachyon $600 + 2x128 7200 CQDIMM $4000 = $5149
  - Not to mention that on the Threadripper Pro system you get 7 real x16 slots, dual 10GbE, etc

- Two comments saying that its useless, but I don't think so.
  - 256GB of 7200MT/s dual channel is very good. In fact it's faster than older Threadripper (quad-channel DDR4-3200) and on top of that this is initial support with initial modules, it will scale to higher transfers.
  - In 2025 we saw that MoEs are becoming more sparse (Qwen Next 80B A3B, GPT-OSS 120B A5B, MiniMax 230B A10B). If this trend continues (It's very likely) and we get models like 200B A5B then this combined with just one GPU would be a killer combo for local LLMs.
- Strix halo exists now with quad channel at 8000 Mt/s, and people call it slow for dense large models.
  - I have a Strix Point LPdDR5X with dual channel 8000 Mt/s and it gets the job done but not really fast. 

- ## [Does it make sense to have a lot of RAM (96 or even 128GB) if VRAM is limited to only 8GB? : r/LocalLLM](https://www.reddit.com/r/LocalLLM/comments/1q7e34g/does_it_make_sense_to_have_a_lot_of_ram_96_or/)

- Since you can't upgrade VRAM, that bulk RAM is decent alternative.

- The limitation is speed.
  - Typical DDR5 RAM bandwidth is around 80 GB/s. With 128 GB of system RAM, you could run an 80B model (quantized to Q8) at roughly 1 token/s. (you can very roughly calculate t/s by dividing memory bandwidth/model size, in this case 80GB/s / 80B@Q8 = 1)
  - Typical VRAM bandwidth varies widely, from about 200 GB/s to 2000 GB/s on high-end gaming GPUs. If you somehow had 128 GB of VRAM, you could run an 80B Q8 model at roughly 2.5 tokens/s on the low GPU end and up to 25 tokens/s on the high end GPU.
  - While MOE may be 100B-parameter models overall, they do not use the entire model for every token, only a subset, for example ~5B parameters. Because of this, even with a 100B MoE model running from system RAM, you could still achieve something like 20 tokens/s.

- I have M3 Ultra with 256GB and the entire model of 120b gpt-oss is in UMA RAM. It generates around 70 tokens per second.

- The model will overflow into RAM, so it will run, but very slowly, dependent on your RAM bandwidth. Most people have only dual channel RAM setups so it'll be very slow, even on DDR5.

- ## [[TweakTown] Minisforum BD395i MAX motherboard at CES 2026: built-in AMD Strix Halo APU, use your own GPU : r/hardware](https://www.reddit.com/r/hardware/comments/1q8jo44/tweaktown_minisforum_bd395i_max_motherboard_at/)
- The dGPU can offload the compute intensive attention part of a large MoE LLM model while retaining most of the memory usage on the iGPU.

- You could already do that with the Framework Desktop's ITX board

- I already have the Strix Halo chip (Evo-X2) running a 5080 via OcuLink on the 2nd M.2 adapter. This gaming setup is 4K Heaven, and chews through MOE LLMs on the side.
  - Honestly the onboard graphics 8060s is going to be more than fine for most people, I was playing 4K at 100+ fps (DLSS, FG, No RT) and it felt great. Then I tried Path-Tracing in Cyberpunk with the 5080 and couldn’t go back.

- I’ve seen 395+ clusters but they were always limited by I/O.

- ## [Minisforum BD395i MAX motherboard at CES 2026: built-in AMD Strix Halo APU, use your own GPU : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q8x9yp/minisforum_bd395i_max_motherboard_at_ces_2026/)
- The new board's PCI slot is not PCIe 5.0 x16, it is PCIe 4.0 x4. The Minisforum product brochure for the new board is very clear. The reporting was sloppy.
  - yeah afaik the strix halo chip itself is using all its big pcie lanes for its integrated gpu, leaving very few lanes available for external stuff.
- Panther lake with 20 pcie lanes and lpddr5x will make obsolete

- [Minisforum shows desktop Mini-ITX board with Ryzen AI Max+ 395 “Strix Halo” and 128GB LPDDR5X memory - VideoCardz.com : r/sffpc](https://www.reddit.com/r/sffpc/comments/1q8k3ng/minisforum_shows_desktop_miniitx_board_with_ryzen/)
- Look at framework desktop benchmarks. Your games will never take advantage of those 128GB of RAM. You could maybe expect to use something like 20GB on big games...

- This is good to have another alternative to Framework. And with a full x16 slot this time.
  - physical slot but it will only be x8 capable as the chip only has 16 total PCIe 4 lanes.
- Oh, then that's not made clear by the article saying "full PCIe 5.0x16 interface". Still that's better than the x4 slot on the Framework.
  - Won’t be PCIe 5.0 either, Strix Halo is PCIe 4.0.
  - Unless we see a definitive statement from Minisforum that the slot will be x8 or x16, I’d expect the slot to be x4 electrically like all the other boards. The issue is there just aren’t a lot of spare PCI lanes, and to get to x8 requires some really tough cuts elsewhere such as an M.2 slot or the Wi-Fi/BT/some of the USB.

- ## [What do we think about Gorgon Point (Ryzen AI 9 HX 470)? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1q4jc99/what_do_we_think_about_gorgon_point_ryzen_ai_9_hx/)
  - The new APU is promised to support DDR5-6400 (102.4 GB/s) and LPDDR5X-8533 (136.5 GB/s) which should move some models that were barely usable on Strix Point to the usable territory.
  - However, it really seems that to utilise these capabilities, manufacturers would have to get chips that are basically inaccessible right now.

- 470 is the successor of 370. Big HELL NO. Still worse than 395.

- Gorgon Point is a mid-cycle refresh, its not a replacement for strix halo. That will only come around 2027 as medusa halo (as announced before). 
- Looks better than HX 370, but still less interesting than Ryzen AI Max 395 with his 256 bits bus.

- It takes a long time for software to catch up to the hardware. For example, Qualcomm released the Snapdragon X chips back in May 2024 with Llama being shown to run on it, but NPU support for LLMs only dropped a year after release. CPU and GPU support on llama.cpp also took a couple of months to show up and this was with Qualcomm engineers pitching in.
  - AMD needs to do a heck of a lot more on the software side if it wants these APUs to be useful for LLMs and local AI.

- I think that the real revolution will come once this kind of APUs use DDR6. But apple will be the first. And will do it with more memory lanes too

- It's going to be worse than Strix Halo which offers not only 256 GB/s but also has over 75 TOPS from igpu alone (same NPU). Heck, Intel's Nova Lake is gonna offer 75+ TOPS from NPU alone.

- ## 等这波AI泡沫破裂，我都不敢想会有多少下架的服务器硬件会冲击垃圾佬市场。搓手等待
- https://x.com/riaqn_zh/status/2004907309336875298
- “我兄弟在等房价崩盘”
  - 没那么快，你看22年还有一波暴涨呢。

- 不用太久，服务器会把旧硬件淘汰的，大厂不差钱，而且会主动追求最新显卡，即使不破裂也能捡到硬件
- 不用破裂，很多数据中心的服务器2-3年就淘汰了

- 这次的泡沫可不像房地产和元宇宙呀。如果真的算力足够，是可以从底层教育到生活的各种方面都可以改革。就要看谁把蛋糕画大还实现它。

- ## [Would a Ryzen AI Max+ 395 benefit from dedicated GPU? : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1ps2cjk/would_a_ryzen_ai_max_395_benefit_from_dedicated/)
  - I just ordered a Framework desktop motherboard, first time I will have some hardware that let me play with some local AI.
  - The motherboard has a 4x pci express port, so with an adapter I could put a gpu on it.
  - I was wondering if it would benefit from a dedicated GPU like a 5060 or 5070 ti (or should it be an AMD GPU?)?

- The 395 combined with the 128 GB of memory is a somewhat affortable System for use of "large" LLMs. It isn't the fasted, but it is a compromise and gets more t/s than LLMs larger than the VRAM of a regular GPU.
  - A GPU combined with a 395 makes no real sense to me, except if you have a mix of models were some fit into the GPU VRAM. A real upgrade would be a GPU with similar sized VRAM than the 395 like a RTX 6000.

- I guess an 395 together with an 5090 could be currently the best AI machine when it comes to cost and power consumption. It should do well with LLM (395 brings the RAM and the 5090 is a very capable extension) as well as with image generation tasks (5090 in lead, 395 is just the host). But at least the Framework case doesn't support it.
  - The 5090 is limited to the 32 GB VRAM onboard. The performance advantage of the 5090 is lost by communication overhead.
- Only when you have something communication heavy. When it's fitting in the 32 GB, like most text2image models, it'll work very well.

- ## 🆚 [Studio + Air combo vs MacBook Pro : r/MacStudio _202512](https://www.reddit.com/r/MacStudio/comments/1pfl6hk/studio_air_combo_vs_macbook_pro/)
- I used to have a MBP for my work and travel machine. After three years I realized I had it docked 90% of the time as I didn’t like taking it when I traveled so I got a cheap M2 Air for travel. 
  - In August of this year I moved to an M4 Max Studio plus M4 Air (24/512 version) combo. I don’t need heavy lifting when I travel so the Air meets all my needs. Most of my computing is done on my Studio. 
  - For me, it’s worked out great. The Studio is awesome and I have everything synced to my Air with my NAS and iCloud. I have a nice and small Crucial 4TB external SSD hooked up to my Studio for large files and projects, and when I travel I just take it with me. 

- Im going back and forth with the same question for years now and after quite a few MacBooks running as a main machine, I’d gladly stay with faster desktop and laptop you don’t need to care about.
  - Price to performance with desktop
  - Better cooling
  - Better longevity
  - and better workflow for your mind - now you have one work machine and other one for private use (and sometimes work related). Less time spend in front of main, work computer means less distractions when doing work. If you work and have fun with the same machine it’s pretty hard to differentiate work from having fun, which leads to burnout and other issues.

- I’ve used Mac laptops exclusively since 1993, and MacBook Pros exclusively since 2012. I bought a Mac Studio M3 Ultra base model this summer and, when my MacBook Pro died, I replaced it with the base model M4 MacBook Air.
  - One thing I haven’t really worked out yet is syncing the two machines. I’ve been meaning to try ChronoSync and its Agent application and have the trials downloaded. For now I just make sure I have the files I need on the Air. I think it’s a great combination.

- Performance wise, the M4 Max Mac Studio and MacBook Pros can both be configured identically, though the M4 Max in the MacBook (especially the 14”) can thermal throttle, whereas the Studio has more robust cooling. Ultimately the right choice for you will depend on how you prefer to work.

- I have this exact setup. 16GB M1 Air and a 64GB M4 Max. But the air is more of personal computer, I don't try to sync them. I use Rust Desk to phone into the studio with varying degrees of success.

- ## [AMD 395+ and NVIDIA GPU : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p9dier/amd_395_and_nvidia_gpu/)
  - Is there any reason I can’t put an NVIDIA GPU in an AMD 395+ machine?
- It works fine simultaneously, several of us have done it
- Nvidia dGPUs work better in the Strix Halo than do either Intel or AMD, apparently.

- Is there a 395+ machine that you can fit an Nvidia GPU in?
  - I'm looking into doing it with a Framework Desktop motherboard, which is mITX sized.

- Physical space, cooling, power would be the first 3 problems...
  - External GPU docks exist

- NVIDIA GPUs work fine on 395 platform as long as you can put them together physically (with M.2 to PCIe adapters or 395 boards with standard PCIe slots). AMD dGPUs may be more problematic due to VBIOS compatibility issues.

- ## [Need some honest opinions on GPU Ai in a box : r/ollama](https://www.reddit.com/r/ollama/comments/1p4z140/need_some_honest_opinions_on_gpu_ai_in_a_box/)
  - For my use case my models and software burn about $2000 per month if I rent a pod using runpod and I have to be extra careful due to rate limits. I want to consider running my models using llamacpp or ollama or offering direct inference for customer using their own on prem machine shipped by me.

- The DGX Spark and similar are not meant to be servers. Could you use them? I guess. But for 8b models you don’t need $3000 of anything. At full 16bit you’d need 16GB of memory plus some context. 24GB tops. Less with quants.
  - And don’t deploy with llama.cpp based anything. Those are personal use tools. Use vLLM, SGLang or TensorRT.
- Why can’t you use it as a server? Is it only for inference via vLLM?
  - tldr the ones I mentioned are built for production and high parallel work loads.

- Have you tried your models on various Mac minis or studios? Very stable and speedy enough.
  - Yes i run my models on Mac mini m4 but running multiple models at the same time is a pain

- ## 🏠 [Most Economical Way to Run GPT-OSS-120B for ~10 Users : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p4evyr/most_economical_way_to_run_gptoss120b_for_10_users/)
- A quad of 3090s will get you there cheapest, assuming you have a way of mounting four 3-slot GPUs in a reasonably secure manner! It’s probably going to need a bunch of PCIe riser cables and a mining frame to accommodate the space, noise and cooling requirements… you’d have 1500W of GPU alone!

- 4x 3090 with vLLM

- What's your use case? Are you running documents through it (RAG)? or just Q&A to the base model?
  - If its the latter, you mainly need something with sufficient VARM. As once the model its loaded in VRAM it can server multiple users. I'm running 20B on RTX 4090. For 120B you can do it on 4x 3090

- 3 x Radeon R 9700 AI PRO 32 GB = 96 GB total mit Vulkan. Cards will be around 4K USD. Then u need some reasonble CPU and some 128 GB RAM.

- ## [Macbook pro 128gb RAM owners, whats the best AI you're running for reasoning & knowledge? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p0yu23/macbook_pro_128gb_ram_owners_whats_the_best_ai/)
- GLM-4.5-Air
  - minimax is next to it but it’s hard to fit in the good quant. 
- Agree! I use MiniMax-M2 @ Q3 and it works mostly great, with a relatively long context. But I am not sure it’s better than GLM-4.5-Air @Q6. Both on par for my coding and agentic tasks. MMM2 is faster though.
- what do you serve GLM with? I really like using LM Studio for tools parsing on MLX quants, but LM Studio doesn’t offer native tools parsing for GLM which causes issues for opencode and zed.
  - I serve GLM-4.5-Air with LM Studio. Use this fixed Jinja template to replace the original one in LM Studio for GLM
  - I really don't get why they never fixed it officially for such popular and useful local model. Maybe with the GLM-4.6-Air release

- I actually use GPT-OSS 120b and GLM 4.5 Air a lot. Qwen Next is pretty good too. Was running an unsloth IQ2 of Minimax M2 today- fun model to chat with but makes a lot of small mistakes at that quantization. Can do similar with Qwen3 235b a22b. Those are cool big models, and nice for low stakes, lower context stuff, but that may not be right for your uses.

- ## 🧩 [Apple is considering putting miniHBM on iPhones in 2027 : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1oz9vs3/apple_is_considering_putting_minihbm_on_iphones/)
- Mobile HBM will be very expensive though, i think it is possible they will do a hybrid for macs
  - At 20 watts tdp don't expect gpu type performance, probably like nvidia orin order of magnitude
- It will probably be slower due to the battery constraints but they will improve the battery too. However when hbm reaches the mac studio, there will be way less power constraints , it will run real fast like 2.8-8TB/s.. even on the m7 or m8 max macnooks, it will be fast

- What's mini-HBM?
  - Mini-HBM isn’t “VRAM stacked on a wafer” and it isn’t literally on top of the GPU. It’s a small HBM-style DRAM stack placed next to the SoC on a silicon interposer.

- Looking at mobile devices, the memory bandwidth for the most part is less than 100GB/s so they really need to up those. And companies are too focused on getting their proprietary models to run well rather than let people just run the open weights models.
  - I do agree, but there is a world that models are introduced in the background before users are able to directly chat with them. Small models can unlock categorization and data collection workflows that are not time sensitive, and will give users improved recommendations and insights without sending data off site. Realistically they could even have a nightly processing step that runs through data over night so it doesn't affect UX.

- I fear on-device inference will greatly reduce battery life which is quite important on a mobile device.

- HBM for bandwidth, Neural block in each GPU core for prefill, 3nm and arm64 for energy efficiency. Apple is shaping up to be a good consumer AI company.
  - Yeah, it is gonna be good, the 2nm process ( 20 nm metal pitch) will come in 2026 and fp 8 native compute will likely come too.. they make good hardware but real expensive on the ram and ssd configs But still so much cheaper than nvidia.

- Ironically Huawei uses LPDDR phone RAM on GPU.

- I don’t understand why it’s Iphone first and then Mac not the other way around.
  - Apple is a mobile first company, they usually test on iphones first then implement it for ipads and macs … if it works on iphones, it will be easier and better on macs. M series chips are essentially scaled up iphone chipa

- ## [AMD Ryzen AI Max 395+ 256/512 GB Ram? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oyy0fy/amd_ryzen_ai_max_395_256512_gb_ram/)
  - I’m looking at the new AI boxes using the Ryzen AI Max+ 395 (GMKtec EVO-X2, Minisforum’s upcoming units, etc.) and I’m wondering if we’ll actually see higher-end RAM configs — specifically 256GB or even 512GB LPDDR5X.

- There’s little point in producing a box with more RAM if the bandwidth isn’t sufficient. 
- Will not see higher RAM configs for Strix Halo. The 256 bit bus width and available LPDDR5X density prohibit this. Even if somehow someone would make a more dense module, the limited bandwidth would not make it useful for LLMs.

- AMD to my knowledge has no interest in supporting this SoC with a 128GB+ config, and the more likely result is a more bespoke SoC in a successor that goes up to 256GB/512GB, possibly with higher bandwidth or a better programming model.
- AMD will never do any powerful AI consumer products, that they wont eat their workststion/server shit

- AMD's next iteration of this chip, Medusa Halo, and that is expected to use either 384-bit LPDDR6 or 256-bit LPDDR5X meaning possible configurations of: 273, 342, and all the way up to 691GB/s in the extreme case.

- Samsung is releasing lpddr6x modules with more 10k mhz modules, which if utilized would increase the memory bandwidth for more than 330 Gb/s. Another way is if AMD uses octa channel method as used in threadripper pro, it can be a game changer. It can increase the memory bandwidth to more than 650 gb/s. With octa channel they can easily go upto 256gb using 32gb modules or 192gb with 24gb modules. It would increase cost, but AMD can capture numerous clients from mac lineup.

- ## [Is it possible we ever get CPU native LLMs? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oyj16n/is_it_possible_we_ever_get_cpu_native_llms/)
- CPUs aren't really suitable for the type of calculations AI uses. "CPU native LLMs" will be just regular LLMs that are running in NPU unit inside of a regular cpu. One day, when NPUs will get decent, it'll be normal.

- MoE models run pretty well on CPU, I have a 21B running on an SBC at 15 tps.

- it's common knowledge on machine learning 101 . Machine learning /AI is mostly about matrix calculations , and which can be done by CPU’s as well however it depends on your CPU core size. Meanwhile GPU is meant todo this operation for each pixel 100times per second. CPU is costly consumes a lot more power per core and its core isn’t scalable . You can’t have cpu with 1million core. If you do it will be size of a watermelon and cost you 10million dolar to buy and 10K electric bill.

- ## [Mac studio ultra M3 512GB : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1oy9kkv/mac_studio_ultra_m3_512gb/)
  - Is there anyone use it in production environment? I didn't find serious benchmark data about it, is it possible to run such as kimi-k2 thinking with two Mac studio 512GB ? 
- Yes, you can run a quantized version of Kimi K2 on two clustered Mac Studio M3 Ultras, but it's not ideal for a production environment. 
  - The main issue is that processing a large 256k context window will be extremely slow, as the M3 Ultra's GPU performance creates a bottleneck despite the large amount of unified memory. 
  - While tools like MLX or Exo can link the machines, this setup is better suited for a single developer's workstation than for serving multiple requests with low latency.

- I recently saw a post showing someone getting 15 tps on Kimi-K2 on two linked M3 Ultra Mac Studios. So it can be done, and 15 tps is certainly usable.
  - I just finished building a server using an EPYC 9455P and RTX Pro 6000 (just one) which can hit the same 15 tps on Kimi-K2 for about the same price and without any of the other drawbacks of the Mac (like trying to link two machines, being stuck on a Mac, etc.).
  - The EPYC 9005 series has 12 independent DDR5 channels at 6400 MT/s, giving it 614 GB/s of memory bandwidth. Not quite as high as the M3 Ultra's 800 GB, but not far off, especially considering you aren't limited to 512 GB and you have 96 lanes of PCIe 5.0 to use for whatever you feel like.

- Problems is with lack of continuous batching. you have to queue incoming requests, vLLM does them in async way but do it support Apple GPU. I do a lot of tests with aider and prefill was never a problem.. but I test only small models

- ## [Model recommendations for 128GB Strix Halo and other big unified RAM machines? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oy1v7q/model_recommendations_for_128gb_strix_halo_and/)

- GPT-OSS-120B is the best model you can run on the Strix Halo. 
  - GLM Air fits, but it runs less than half the speed, and GPT-OSS-120B is already super slow in practice. 
  - You can get 50 tokens/sec, but in real use the prompt processing is so slow it feels like 1 token/second for anything but light chatting.

- ## [Ryzen AI MAX+ 395 - LLM metrics : r/ollama _202511](https://www.reddit.com/r/ollama/comments/1oxw4ir/ryzen_ai_max_395_llm_metrics/)
  - MACHINE: AMD Ryzen AI MAX+ 395 "Strix Halo" (Radeon 8060s) 128GB Ram
  - OS: Windows 11 pro 25H2 build 26200.7171 (15/11/25)
  - INFERENCE ENGINES: Lemonade V9.0.2, LMstudio 0.3.31 (build7)
  - I would reccomend Lemonade (supported by AMD) but the python API is the generic OpenAI style while LMstudio Python API is more friendly. Up to you.
  - LMstudio (No NPU) is faster with Vulkan llama.cpp engine rather than Rocm llama.cpp engine (bad bad AMD).
  - Lemonade offers also NPU only mode (very power efficient but at 20% of GPU speed) perfect for overnight activities, and Hybrid mode (NPU+GPU) useful for large context/complex prompts.

- Framework has an ITX sized board which you can put in a server or desktop case. It even has 1 PCIE4x4 slot. The CPU doesn't have enough PCIe lanes for more slots
  - Easy, buy a Xeon or a threadripper server. Dual CPU with lots of lanes.

- ## [Why aren't there cheap NVLink adapters for RTX 3090s? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1owxob9/why_arent_there_cheap_nvlink_adapters_for_rtx/)
  - Is the NVLink only a wire jumper linking both cards together? Can I make my own homemade connections?
- 4 slot bridges go for $600-700 on eBay

- I believe they are passive but contain 128x high speed lanes with two 90 degree connectors, that's a signal integrity nightmare all those traces need to be matched in length. Does this justify them being $600 tho? Not at all
  - This is the correct answer. You can't just jumper a high-speed interconnect. They went from flexible ribbon to PCB for a reason.
  - That being said, it IS 100% supply and demand (similar to current DDR4/DDR5 prices). The 4-slot adapters were $59-$79 when I got mine a few years back. The 3-slot were like $120-150. BECAUSE gamers didn't care about them. The current demand is from people re-using 3090's for compute work.

- ## [Nvidia Tesla H100 80GB PCIe vs mac Studio 512GB unified memory : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1owy5sm/nvidia_tesla_h100_80gb_pcie_vs_mac_studio_512gb/)
  - A Nvidia Tesla H100 80GB PCIe costs about ~30, 000
  - A max out mac studio with M4 ultra with 512 gb unified memory costs $13, 749.00 CAD

- H100 is not 10, 000 times faster, more like 10X for training and 20X for inference, so one order of magnitude.

- H100 costs $30, 000 because they allow clustering with HBM 3tb/s allowing you to combine multiple H100s into a single giant GPU super computer. Cant do that with the Mac. Can't do that with the Pro 6000.
  - These LLMs are trained with clusters as large at 500 - 15, 000 H100s...

- ## [Kimi K2 Thinking Q4_K_XL Running on Strix Halo : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ouuko3/kimi_k2_thinking_q4_k_xl_running_on_strix_halo/)
- When file size is larger than your mem+vram, there's little you can do since bottleneck is the disk read speed(besides bad system managed caching). You can buy 3 more machine and use RPC to speed up

- ## [Half-trillion parameter model on a machine with 128 GB RAM + 24 GB VRAM : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oueiuj/halftrillion_parameter_model_on_a_machine_with/)
  - CPU: Intel i9-13900KS
  - RAM: 128 GB (DDR5 4800 MT/s)
  - GPU: RTX 4090 (24 GB VRAM)
  - I’ve successfully run Qwen3-Coder-480B on llama.cpp
  - UD-Q3_K_XL: ~2.0 tokens/sec (generation)
  - UD-Q4_K_XL: ~1.0 token/sec (generation)

- Be careful with any method of running a model that heavily leverages swapping in and out of your SSD, it can kill it prematurely. Enterprise grade SSD can take more of a beating but even then it's not a great practice.
  - This is only half correct. Repeatedly writing to an ssd shortens its lifespan. But repeatedly reading from an ssd is not harmful.
  - When you use mmap() for models exceeding RAM capacity, 100% of the activity on the ssd will be read activity. No writing is involved other than initially storing the model on the ssd.
- writing and erasing data on ssd’s are intensive, and ssd’s generally have a limit on how many times you can do that before they become read only or inoperable.
- Memory mapping is reading to memory and discarded as needed. It isn't writing to disk so no concern on excessive writing like swap space / Windows virtual memory.
- It is not swapping! It is using mmap (memory-map model). So it is only reading from SSD (there are no writes, context is kept in RAM).

- ## [What is the best hardware under 10k to run local big models with over 200b parameters? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1otdr19/what_is_the_best_hardware_under_10k_to_run_local/)
  - Short term I will use this to refactor codebases, coding features, etc. I don't mind if it runs slow, but I need to be able to run thinking/high quality models that can follow long processes (like splitting big tasks into smaller ones, and following procedures). 
  - But long term I just want to learn and experiment, so anything that can actually run big models would be good enough, even if slow.

- Caution: buying hardware to run specific models is not sustainable unless you are 110% satisfied with the model at hand and will not find the urge to upgrade to something even better. Its a race against big datacenters and you might as well just rent the hardware.
  - Actual answer: Stack 3090s, 4090s, however cheap you can get them. thats how you run big models fast and "cheap" (relatively speaking). RAM Prices are skyrocketing and it is entirely unfeasable imo to buy (64gb 6000mhz is $360+++). 3090s for 700-800 are way higher performance. 
  - Rule of thumb i use: DDR5 6000Mhz is 10x slower than a 4070's VRAM. If u can get 10x more RAM than VRAM for the same price, speeds *can* be compared, but then u start looking at 6-channel motherboards etc.
  - tl; dr: due to ram situation, just stack 3090s while you can. nothing else beats its price/performance. good luck

- A good alternative to the 3090 for running large MoE models is the AMD Mi50 32gb, much cheaper and has 1tb memory bandwidth due to the HBM2 memory
- 8xMI50: qwen3 235B Q4_1 runs at ~21t/s with 350t/s prompt processing (llama.cpp)

- an M3 ultra will have very bad prompt processing, so if you use any prompts longer than 8k or so, get ready for a world of pain. MoE only helps so much too.
  - Partial offloading, especially with MoE, is still mainly RAM Bandwidth bound, im not 100% sure what 4 or 6 channel motherboards are available, and if you can get enough high speed RAM at any price below 10k to make that worthwhile.
  - If you want an out of the box option that isnt speed optimized, m3 ultra works. If you at all have speed requirements (and by that i mean, not waiting half an hour for a big response), i dont think 10k will cut it without some heavy DIY (e.g. crazy motherboard with tons of PCIe, think older threadrippers, to use all those gpus)
- Remember there are models such as Qwen 3 Next with closer to linear prompt processing time, and more such models will continue to appear over the coming years :) also even with large system prompts (ie for agentic uses), you can cache those and get decent performance. At the moment we're just throwing compute at everything, but the algorithms and implementations will become more efficient over time.

- ## 🆚 [Benchmark Results: GLM-4.5-Air (Q4) at Full Context on Strix Halo vs. Dual RTX 3090 : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1osuat7/benchmark_results_glm45air_q4_at_full_context_on/)
  - I benchmarked the GLM-4.5-Air (Q4) model running at a near-maximum context on two very different systems: a Strix Halo APU and a dual RTX 3090 server. Both tests were conducted under Debian GNU/Linux with the latest llama.cpp 
- Why is the prompt processing for RTX is so low? It should be hundreds if not thousands. The model is too big and you have to spill some part to regular system RAM? These prompt processing figures make it unusable in such setup then
  - This is essentially a pp119702 test. I'm sure their numbers are MUCH higher at 0 context.

- Numbers from my system: RTX 5090 + pcie5 x16 + DDR5-6000 and 46 MoE layers offloaded to the CPU:
  - PP 31.2x faster than your Strix Halo machine
  - PP 10.7x faster than your Dual 3090 machine (you are prob limited by slow pcie)
  - TG 2.1x faster than your Strix Halo machine
  - TG 1.7x faster than your Dual 3090 machine

- vllm will be much faster for dual GPUs.

- ## [I tested Strix Halo clustering w/ ~50Gig IB to see if networking is really the bottleneck : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ot3lxv/i_tested_strix_halo_clustering_w_50gig_ib_to_see/)
  - TLDR: While InfiniBand is cool, 10 Gbps Thunderbolt is sufficient for llama.cpp.
  - During inference, I observed that the network was never used at more than maybe ~100 Mbps or 10 MB/s most of the time, suggesting the gain might not come from bandwidth—maybe latency? But I don't have a way to prove what exactly is affecting the performance gain from 2.5 Gbps to 10 Gbps IP over Thunderbolt.

- Llama cpp doesn’t use tensor parallel so everything is done sequentially. This test was meaningless. You need to test it with TP on VLLM or Sglang
  - As I state in the post, there is no RCCL support. Without RCCL support, frameworks like vLLM and PyTorch can't perform collective operations (all-reduce, all-gather, etc.) across multiple nodes. This is the fundamental blocker for tensor-parallel inference on Strix Halo—you literally can't split a model across nodes without these primitives. It's always the software support that's lacking on the AMD side
- It's meaningless because:
  - Pipeline parallelism only help you run models that you can't fit in a single node. It can't be faster than the single slowest node. So there is no sense testing it for performance, unless you want to test for performance bugs in implementation.
  - Using pipeline parallelism, the network transfer between nodes are minimal. Each token only has 2880 elements of embedding. Even you use 100Mbps network it's only like 1ms time for a token. So what are you trying to test?

- I believe you can use GLOO instead if NCCL is not available (I assume RCCL is the rocm version).

- It is not meaningless at all. It's quite meaningful since network speed is a topic that often comes up. You don't have just be doing TP for it to be of interest.

- As expected. I don't find the difference to be substantial between 2.5 to 10 to 50. Sure, it gets a little faster but not nearly as much as the increase in network speed would suggest. Not enough for me to pay several times more for a 10GBE network versus 2.5GBE.

- ## [Mac vs. Nvidia Part 2 : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1opo89e/mac_vs_nvidia_part_2/)
  - I recently purchased a Mac Studio M4 Max w/ 64GB (128 was out of my budget). I also was able to get my hands on a laptop at work with a 24GB Nvidia GPU (I think it’s a 5090?).
  - I was shocked how less capable the Nvidia GPU is! I loaded gpt-oss-20B with 4096 token context window and was only getting 13tok/sec max. Loaded the same model on my Mac and it’s 110tok/sec. I’m running LM Studio on both machines with the same model parameters. 
- The laptop 5090 has 24gb
  - Yep and it is essentially a 5080 desktop crammed into a laptop (Nvidia always does this).

- 13 tokens/second sounds right if you load gpt-oss-20b into some dual channel DDR5 system memory. I don't use LM Studio personally but by any chance did you not tell the 5090 rig to load any layers into the GPU?
  - So I had that problem at first where LM studio was not loading all the layers into the GPU and the utilization stayed low. But I changed a setting that forces the model to be loaded exclusively to the GPU and utilization when up, but the gain was only like 3-4tok/sec speed up
- You must be running that model with layers on the CPU or you're mistaken about which GPU your laptop has

- Remember the 5090 mobile is the 5080 desktop chip (GB203) but upgraded to use 3GB memory modukes instead of 2GB like the 5080. Like most laptop gpus it is comparably power and heat limited compared to the desktop equivalent (5080).

- Make sure you have all the layers of the model loaded onto the GPU. 

- ## [If I want to train, fine tune, and do image gen then... DGX Spark? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1om7ccz/if_i_want_to_train_fine_tune_and_do_image_gen/)
- Apple is no good for finetuning/training, only for inference afaik.
  - AMD works, I guess. Story of their hardware in AI.
  - Both Apple and AMD probably don't work for image stuff (especially for anything niche, less supported). It's usually based on CUDA.
  - If you just want to "do everything AI", DGX will work and it will be slow-ish and if you can live with that (or optimize using MXFP4 etc.), it's perfect for you. If you got dem cash of course.

- ## 🤔 [Best setup for running local LLMs? Budget up to $4, 000 : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1olsh0j/best_setup_for_running_local_llms_budget_up_to/)
- Depends on what kind of route you want to go. Do you want an open mining rack style build with the potential to have 8 GPUs? Do you want a system that fits into a standard ATX case? What size models do you want to run? Do you want to do image or video generation?
- I've done a few builds recently and the two best value routes I found are for a DDR4 based system:
  - Huananzhi H12D-8D  华南金牌
  - AMD EPYC 7532 (The cheapest EPYC Rome that gives you full memory bandwidth.)
  - AMD EPYC 7D12 (Best value EPYC, downside is missing half of the memory bandwidth.)
  - DDR4 2133 to 3200 RDIMM 8x16GB (128GB) or 8x32GB (256GB).
- For a DDR5 system:
  - GIGABYTE MS03-CE0
  - Intel 8480+ QYFS 
  - DDR5 4800 RDIMM 8x16GB (128GB) or 8x32GB (256GB)
  - I built/purchased the above parts with 256GB of memory for around $2, 000, the price of the memory was half of the build. Currently the memory price has risen by +50% and 256GB of memory is around $1, 500.
- For the GPUs the best value for text only inference is still the MI50 16GB (~$150) and the MI50 32GB (~$250-300, price has risen could have been had for around ~$150 1-2 months ago). 
  - If you want a more plug and play experience or want to do image/video generation, then you're probably still looking at getting 3090s (~$700). 
  - There are other GPUs to look for, but I'm sure they'll be recommended by others in this thread.
- With the above parts you have two routes. 
  - You can either go for GPUs and run smaller models fast, or you can go for a hybrid approach with a single 3090 for prompt processing and put the rest of the money into memory to run a larger model at a slower speed (Deepseek at home). 
  - If you want an example build of the top end you can have with CPU+GPU hybrid, then this video is a good comparison point. The video showcases 12-channels of DDR5 5600 with a 3090 getting 15t/s with DeepSeek_V3_0324 Q4_K_M. Using that as a comparison point, you'd expect the DDR5 4800 system above to be around ~7-9t/s and the DDR4 3200 system to get ~4-6t/s.

- 4x 3090s and whatever else supports this
- My 4x3090 rig is loud, uses a lot of power, puts off a lot of heat, and seems to require constant care and feeding. The DGX Spark sits on my desk, is quiet, and "just works". Unless you need to eek out the absolute most inference performance per $ spent, I would go with the turn-key solution and call it a day.

- If you go with multiple GPUs, you need a server mobo in order to get a server CPU that has enough pci-e lanes. GPUs want 16x each even though you can get by on less
  - Server motherboards are meant to run in very loud 2U chasis' with high airflow. I stuffed mine into a large PC case but have extra fans and an AIO CPU cooler for SP5.
  - Also, server CPUs a generally woser at gaming and single threaded performance than consumer CPUs.
  - If money is no object a ThreadRipper is the way to go.

- ## [Building PC in 2026 for local LLMs. : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1ol3lcy/building_pc_in_2026_for_local_llms/)
- you can run a quantized deepseek-v3.1-terminus with 671b params at roughly 20 t/s, with full 128k context, using a single 5090 if your CPU + RAM is beefy enough, and if you're using `ik_llama.cpp` .
  - 2x AMD Epyc 9355 and a shit ton of RAM ought do it. My server build has 768 gb RAM and I use it to power Roo Code and SillyTavern

- You will get much closer to your goal with an nVidia RTX pro 5000 blackwell, with 72 gb of vram, >$6K. Another option is something like strix halo computers, ~$2k. Will be slow around 10 tps, but is faster than most can read.
  - Rumor has it that in more than a year, AMD will release medusa halo, that has twice the memory and twice the speed of strix halo

- No. No local model running on a single GPU (or even several) can match the huge professional cloud models in quality. We do local models for privacy and for the fun of hobbying.
  - local models can be fine tuned locally into very specialized models that can do specific things much better than the SoTA cloud models. This gets pretty niche

- ## [DGX Spark Benchmarks (Stable Diffusion edition) : r/StableDiffusion _202510](https://www.reddit.com/r/StableDiffusion/comments/1ogjjlj/dgx_spark_benchmarks_stable_diffusion_edition/)
  - tl; dr: DGX Spark is slower than a RTX5090 by around 3.1 times for diffusion tasks.
  - I happened to procure a DGX Spark (Asus Ascent GX10 variant). This is a cheaper variant of the DGX Spark costing ~US$3k, and this price reduction was achieved by switching out the PCIe 5.0 4TB NVMe disk for a PCIe 4.0 1TB one.
  - Based on profiling this variant using llama.cpp, it can be determined that in spite of the cost reduction the GPU and memory bandwidth performance appears to be comparable to the regular DGX Spark baseline.
  - Now on to the benchmarks focusing on diffusion models. Because the DGX Spark is more compute oriented, this is one of the few cases where the DGX Spark can have an advantage compared to its other competitors such as the AMD's Strix Halo and Apple Sillicon.
  - While the DGX Spark is not as fast as the Blackwell desktop GPU, its performance puts it close in performance to a RTX3090 for diffusion tasks, but having access to a much larger amount of memory.

- 3 times slower than a 5090 so…. Roughly the equivalent of a 5060ti?
  - Their benchmark for SDXL 3.13it/s makes it roughly equal to 3090, that also has about 3it/s.
- If we did the math purely based on TFLOPs/ in FP16/BF16, it would indicate closer to 5070-like performance.

- You can find many benchmarks for AMD AI MAX and compare. Nothing spectacular here, because inference performance limited by memory bandwidth, and DGX has 270Gb/s while AMD thingy has 250Gb/s.

- ## [Running DeepSeek-R1 671B (Q4) Locally on a MINISFORUM MS-S1 MAX 4-Node AI Cluster : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1oevvyu/running_deepseekr1_671b_q4_locally_on_a/)

- So you spend $20, 000 to get 5 TPS. You could have spent $1000 and run it on ram/cpu and got the same speed.

- ## [Fast loading and initialization of LLMs : r/LocalLLaMA _202407](https://www.reddit.com/r/LocalLLaMA/comments/1e3hknt/fast_loading_and_initialization_of_llms/)
  - Now normally I use vLLM to serve LLMs, but it seems to be very slow at loading up models. For Llama 8 FP16 it takes 8s to be ready from a warm cache. Qwen 14 takes 11s with a warm cache. Way too slow.
  - The above is for a single 3090 on PCIe 4.0 x16, 4 sticks of DDR4 RAM rated at 3200 on a X570s motherboard with a Ryzen 5600X CPU.

- A co-worker and I are building a local LLM server for testing (see my profile) and we have looked at various ways to maximize loading of LLM files across different CPU brands/architecture for a customer.
  - We did consult with one of our biggest customers who has a few dozen local LLM workstations and they all have AMD Threadripper 7980X boxes, 192GB of RAM (4x48GB) with a pair of RTX A6000 48GB cards w/ NVLink bridge and dual 15TB U.2 NVMe drives. They have moved to ZFS w/o L2ARC and storing all their LLM files on 30TB worth of U.2 NVMe drives and a 168GB ARC.
  - We are building a Splunk app for them to monitor their usage of LLM apps and models.
  - TL; DR: Use ZFS and set ARC to cache as many LLMs as you can for faster transfer to VRAM. Or if you only need to test a coupe of LLM constantly, then create a RAM disk and copy your LLM files there.

- ## 🆚 [What laptop would you choose? Ryzen AI MAX+ 395 with 128GB of unified RAM or Intel 275HX + Nvidia RTX 5090 (128GB of RAM + 24GB of VRAM)? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o3evon/what_laptop_would_you_choose_ryzen_ai_max_395/)
- more net RAM = more net model + context size, at whatever speed.

- The Ryzen and run the larger models like gpt oss 120b or glm 4.5 air. The 5090 will run models that fit much faster like Qwen3 30b variants.
  - The Ryzen may be very slow on promo processing. A big deal if you are dropping 50k or more tokens. You may be waiting a few minutes before the output starts.

- Depends, do you want to run larger models somewhat slowly - 395 Or do you want to run smaller models and larger MoE models very quickly - 5090

- depends what you want to do, if you are gaming then the 5090 makes more sense, for ai the 395 makes more sense since you will be able to run better stuff.

- For LLMs the Ryzen can run large MOE models much faster, but the one with the 5090 can run smaller models that fit into the 24 GB vram really really fast. For image or video generation, Nvidia unfortunately is still the top choice, it usually takes some time until new models are supported on Amd 

- I have GMK x2 and I'm killing this machine with everything you can think about, run everything even Q2 GLM4.6 with 10 tokens (not bad for 115G) model all in ram.

- 
- 
- 
- 
- 
- 
- 

- ## [4x64 DDR5 - 256GB consumer grade build for LLMs? : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1k6p20z/4x64_ddr5_256gb_consumer_grade_build_for_llms/)
  - I have recently discovered that there are 64GB single sticks of DDR5 available - unregistered, unbuffered, no ECC, so the should in theory be compatible with our consumer grade gaming PCs.
  - Both AMD 7950x specs and most motherboards (with 4 DDR slots) only list 128GB as their max supported memory - I know for a fact that its possible to go above this, as there are some Ryzen 7950X dedicated servers with 192GB (4x48GB) available.

- I have 64GB of DDR5-6000 and it is great at inference - of models that don't take more than around 16GB (preferably 10GB) - anything bigger becomes too slow to use.

- If you're going for a CPU based build, you want to go for epyc, not a consumer CPU.
  - It won't be super fast; expect memory speed of around 200GB/s, so about 1/5th the performance of a 3090 or 4090 in token generation, and maybe 1/10th in processing speed.

- Yeah, I've got 128Gb of DDR4 3200, now I am running 110Gb models with 0.3t/s

- On desktop Zen 4/Zen 5, I wouldn't recommend doing that.
  - You're quite limited by the Infinity fabric bandwidth, limiting you to a max of 62-68GB/s on DDR5-6000 to 6400, while theoritical DDR5 6000 128-bit is 100GB/s.

- I'm running a Ryzen 9 7900X on MSI PRO B650M-A WIFI AM5 Micro-ATX with 256GB using 4 of those 64GB DDR5 sticks. So it is possible. Your memory bandwidth drops, as you need to slow the memory down to stay stable. If you are building from scratch you may want to use a CPU with more memory channels.

- ## [Did someone ever benchmark how cpu inference performs with quad and eight channel memory ? : r/LocalLLaMA _202401](https://www.reddit.com/r/LocalLLaMA/comments/1920l93/did_someone_ever_benchmark_how_cpu_inference/)
  - Since people always say that bandwidth is the problem. And a full 8 channel memory board with ddr4 3200 would be about 200gb/s per second i was wondering if anyone ever benchmarks that stuff and how it scales with cores ?

- I have a 8ch epyc build, after some experiments i have found that the effective bandwidth is about 135 gb/s, so a 40gb model is ~ 3, 3 t/s, a 20gb is twice the speed.

- Intel Xeon E5-2680 v4, 128GB DDR4 2400 RAM 4 chanels. llama.cpp, model: mixtral8x7b Q5_K_M 6 tokens/sec

- R720 2x xeon 2670, 192gb ddr3-1333 dram, llama.cpp running mixtral q3_k_m quant w/ 10k context, pure cpu inference: 3.6 t/s. If use installed P40: 9.1 t/s

- ## [AI setup for cheap? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ovbzi3/ai_setup_for_cheap/)
  - My current setup is: i7-9700f, RTX 4080, 128GB RAM, 3745MHz. In GPT, I get ~10.5 tokens per second with 120b OSS, and only 3.0-3.5 tokens per second with QWEN3 VL 235b A22b Thinking. 
- If you're only getting 10 tok/s, you're probably not using GPU at all. I have i7 13700k with a 4090. I get 38 tok/s with GPU, and 11 tok/s with only CPU.
  - If you're running llama.cpp, did you compile with CUDA support. Did you remember to set your -ngl 99 flag? using --n-cpu-moe instead of -ot exps=CPU?
  - Try llama-server -ngl 99 --n-cpu-moe 32 -ngl 99 -c 50000 -fa on -m file/to/model.gguf --no-mmap -t 8 -ub 2048 -b 2048 --jinja

- The CPU doesn't matter, the CPU's memory speed (i.e. your ram) determines TPS

- ## [AI LLM Workstation setup - Run up to 100B models : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ov7idh/ai_llm_workstation_setup_run_up_to_100b_models/)
  - Planning to buy 320GB DDR5 RAM (5 * 64GB) first. Also with high MT/s(6000-6800 minimum) as much as possible to get better CPU-only performance. In future, I'll buy some more DDR5 RAM to make that 320GB to 512GB or 1TB.

- 50+t/s with 30-50B Dense models is not possible for CPUs. As you need 20GB(32B Q4)x 50 ~= 1000GB/s of bandwidth, which is impossible before Epyc Venice or Diamond Rapids Xeon.

- Planning to buy 320GB DDR5 RAM (5 * 64GB) first
  - Don't do 5. In order to get maximum bandwidth you need to have an even number of DIMMs all the same size (and there might be some restrictions beyond that depending on CPU). If you have 5 you'll have 4*64GB of 'fast' memory and 64GB of slow memory. Keep in mind also that if you only have 5 out of 8 DIMMs installed you only get 5/8 the maximum memory bandwidth for the platform which directly impact your performance.

- "50+t/s with 30-50B Dense models"? A 6000 Blackwell can barely do that: I get 58t/s with Qwen3-32B-Q4. My 400W Epyc with 12x 5200MHz RAM only gets 14-18t/s.
  - The only reason CPU is usable with MoE is because the amount of RAM needed and the fact that bandwidth is often the bottleneck before compute and even then it's medeocre unless you offload the attention calculations which are more compute than memory bound.

- Optimized Power saving Setup
  - You seem to be confusing power draw with efficiency. Running a 200W CPU for 5min is not better than a 600W GPU for 1min. Get a RTX 6000 Max-Q, which runs the models you want and is one of the most efficient inference engines that are available. My Epyc system idles at ~90W while a Max-Q idles at ~15W and can be put in some <40W desktop.

- ## 🤔 [Budget LLM pc builds, new CPU only approaches : r/LocalLLaMA _202410](https://www.reddit.com/r/LocalLLaMA/comments/1fycnc1/budget_llm_pc_builds_new_cpu_only_approaches/)
  - iGPU and lot's of memory: Like using 192gb of DDR5 RAM on the AMD Ryzen 9 7950x iGPU, or the budget Ryzen 5 8500G?
  - AVX-512: Llamafile now has AVX-512 Support, meaning 10x Faster Prompt Eval Times For AMD Zen 4, like AMD Ryzen 9 5900X?

- Unfortunately the answer is no. Even if you can build a consumer PC with a lot of DDR5 Ram, they cannot take advantage of it for LLMs, for the following reasons:
  - they have limited memory bandwidth for large models.
  - they have limited compute throughput for long context.
- Only 64-96 core Genoa EPYCs with 12-channel DDR5 RAM (and the new Intel Granite Rapids) can approach practical levels of performance, and this is only for models up to 70GB . But these are certainly not budget options.

- 2 channels of ddr5 9000/10000 should be something like 150 GB/s. Thats more than enough to have a real time conversation with the current gen 10B class models. Even the 30B+.

- Faster RAM, more channels (e.g. Strix Halo and HEDT with 4, EPYC with 8-12), and faster/more cores+AVX512 can enable the practical use of slightly bigger models but still far smaller than the 96-192GB people are discussing about.

- let's define model performance first. There are 2 stages: Prompt Processing (the model reading your input) which is compute bound, and Token Generation (the model writing its response) which is memory bound.
- The rule of thumb for token generation is:
  - `tokens/sec = memory_bandwidth_in_gb_per_sec / model_size_in_gb`
- The actual bandwidth which can be achieved is ~70-75% of the theoretical.
  - A dual-channel 3600MT/s DDR4 system has 51.2 GB/s theoretical memory bandwidth. Therefore, the actual achievable bandwidth is between 35.8 - 38.4 GB/sec.
  - An example model: Qwen2.5 7b when quantized to 8 bits is 8.1GB (by default models are shipped to FP16 which is double that).
  - So, you may expect a token generation speed between 4.4 and 4.7 tokens/sec (38.4 / 8.1) for this model. Half of that for the FP16 version of the model, and double of that for the Q4 version of the model.
- That's why large (dense) models don't make sense in CPUs. A 70GB model (e.g. Llama-3.1 70b q8_0) would be slower than 1 t/s. You need 8+ channel memory to reach practical speeds.
- 🤔 But if you need to process long context (summarize documents, explain/debug/enhance code, continue a story, have long chat sessions) then the Prompt processing is compute bound, therefore compute throughput is very important and this is where modern GPUs seriously outperform CPUs by 25-100x due to their tensor cores.
  - For the above model, you may achieve 60 tokens/sec for prompt processing with a CPU and about 2500 tokens/sec with a RTX 3090. Therefore, if you want to summarize a 1500 words document, it will take 1 second in the GPU and 40 seconds in the CPU (just for the model to ingest your input).
- P. S. CPUs become practical with Mixture of Experts (MOE) models because the active parameters are usually 15-25% of the total, therefore the speed is 4-6x of that of a dense model.

- My understanding is that due to the memory bandwidth being a bottleneck, using a NPU or iGPU isn't any faster than simply using the normal CPU cores themselves when you're limited to two channel memory. CPU only can certainly be useful, and I think people are too quick to discount it as an option for small context sizes and smaller models 

- ## 🆚 [Thread for CPU-only LLM performance comparison : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nj4axf/thread_for_cpuonly_llm_performance_comparison/)
  - I could not find any recent posts about CPU only performance comparison of different CPUs. 
  - With recent advancements in CPUs, we are seeing incredible memory bandwidth speeds with DDR5 6400 12 channel EPYC 9005 (614.4 GB/s theoretical bw). 
  - AMD also announced that Zen 6 CPUs will have 1.6TB/s memory bw. The future of CPUs looks exciting. 
  - For this CPU only comparison, I want to use ik_llama 
  - use CPU only inference (No APUs, NPUs, or build-in GPUs allowed)
- llama-bench benchmark (make sure GPUs are disabled with CUDA_VISIBLE_DEVICES="" just in case if you compiled for GPUs):
  - qwen3moe 30B Q4_1: 38.9
  - GPT-OSS 120B Q8_0: 24.7

- those dusty EPYCs/Xeons with fat memory channels you see on eBay suddenly look like budget LLM toys..it; s crazy that decommissioned gear can outpace shiny new desktop CPUs for this niche.

- That's my server, I think there are some config issue here as using thread 64 would be much slower, maybe I should enable HT.
  - CPU: 1S Epyc 7B13(64c, HT disabled manually)
  - RAM: 8 x 64GB DDR4 2666
  - Motherboard: Tyan S8030GM2NE
  -  qwen3moe 30B Q4_K: 31.0 
  -  gpt-oss 120B F16: 14.9
-  Yes, there is definitely something wrong with the server in your case. You should get better results than my server.

- [CPU Only OSS 120 : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o6d4a6/cpu_only_oss_120/)
  - just try it on CPU only (gulp) on my home lab server and actually it's more than usable at a fraction of the power cost too. This is also running in a VM with only half cores given.
  - prompt eval time = 260.39 ms / 13 tokens ( 20.03 ms per token, 49.92 tokens per second)
  - eval time = 51470.09 ms / 911 tokens ( 56.50 ms per token, 17.70 tokens per second)total time = 51730.48 ms / 924 tokens

- ## [Looks like Intel Arrow Lake can support 4 DIMMs @ up to 6400 speeds : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gindy1/looks_like_intel_arrow_lake_can_support_4_dimms/)
  - After searching through a few boards, it looks like Arrow Lake can do 4 Dimms @ 6400. For an ASrock example, see below - select vendor "Corsair", and there is a 24GB per DIMM options @ 6400. Crucial and ADATA have 48GB "4 channel" options @ 5600.
  - Anyway just wanted to pass along that we may see "certified" 6400+ speed 4 DIMM setups become common with Arrow Lake (Core Ultra 200 series). An x86 way to have 192GB-256GB (when DIMMs are available) on a standard desktop at reasonable speed.

- But they are only dual channel, so you can expect at most around 100 GB/s of memory bandwidth.
  - Missed opportunity...

- I’m running 6200 stable on 128gb 4 dimms with Ryzen 7950x3D since 1+ year lol

- 4 dimms does not mean 4 channels. MBs have had 4 slots forever. Arrow Lake is dual channel.
- Arrow lake is dual channel. 4 dimms does not mean 4 channels. MBs have had 4 slots forever.

- it actually has 4 channels. It has the ability to address each half of the ram seperately. And it's a 4 channel controller, for 4x 32Bit. It's just that that's the same bandwidth as 2x 64 bit.

- [Is 96GB of DDR5 6800Hz RAM enough for training? : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1b1e4z8/is_96gb_of_ddr5_6800hz_ram_enough_for_training/)
  - I went with 96GB of fast RAM thinking that it would be more than enough, but I've been seeing that people recommend at least 128GB for training and interfacing.
- What is your ram capacity and ram speed, I'm running 4x32gb at 6200mhz which speeds up inference. You can run AIDA to benchmark your ddr memory speed bandwidth
  - I want to get 128 gb of ram 6000MT/s. Cl30. But most people say that there is no way the ryzen 9 7950x3d could reach that at all without it melting or being unstable. Even 5200 would be a miracle. Apparently for am5, 4 DIMMS should not be used. You shouldn’t quadrank. The most you can go for is 96 gb ram 6400MT/s (2x48). So how did you do it? Please teach me

- ## [CPU RAM only speeds on 65B? : r/LocalLLaMA _202307](https://www.reddit.com/r/LocalLLaMA/comments/14q4d0a/cpu_ram_only_speeds_on_65b/)
- I have both Dual RTX 3090s+NVLink and 128GB RAM (@3200) and for 65B models, using the CPU (i have a 3rd gen 8 core Ryzen) is just too slow. It's around 1 token per second, far from 7/s. From what i've seen getting a better CPU (16 cores) doesn't help much.

- The 7950x with DDR5 6000 on a 65b_4_ks model is 1.75t/s.
  - When it comes to token generation speed, the core count doesn't really matter. What does matter is the RAM bandwidth.
  - However, if you don't have a GPU, then the core count becomes important for prompt evaluation speed. But it's not worth buying a high-end CPU just for this.
  - In my opinion, if you can tolerate a speed of 2t/s on 65b models, the most cost-effective option would be to go for the 13400f($170)processor (disable the E-cores), paired with 64GB of high-frequency DDR5 RAM, and a second hand RTX 2060 for just $100. This GPU can be used for prompt processing and offloading as many layers as possible.

- I have CPU Ryzen 9 3950X and 64Gb RAM at 3600MHZ. The airoboros-65b-gpt4-1.4.ggmlv3.q5_K_M.bin generates at the average of 1077ms per token, with very small variance actually.

- ## [Is RAM latency very relevant for LLMs (Ollama)? : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gws9yp/is_ram_latency_very_relevant_for_llms_ollama/)
- No overclocking will not produce notable gains. When you offload to CPU your major bottleneck is the processing not memory bandwidth. You'll do a lot of work and adding potential instability for something that you won't really notice, maybe an extra token per hundred generated.
  - You are confidently wrong. I went from 3.45 tokens/s to 5.29 tokens/s just by enabling XMP profile (2666 MHz to 3600 MHz).

- ## [Will DDR6 be the answer to LLM? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o0i4fz/will_ddr6_be_the_answer_to_llm/)
  - Bandwidth doubles every generation of system memory. And we need that for LLMs.

- I think the combination of smart quantization, smarter small models and rapidly improving RAM will make local LLM's inevitable in 5 years.

- Prompt processing will be even more critical with faster RAM - you need lots of compute for larger models, DDR6 will be used for, and CPUs do not have enough compute. You still absolutely would need GPU.

- Isn't Apple unified memory just multi channel RAM? It does deepseek fairly well.
  - Unified memory without upgradable ram is such a double-edge sword. I want it but I don't want it to be "The future"

- ## [How fast big LLMs can work on consumer CPU and RAM instead of GPU? : r/LocalLLaMA _202407](https://www.reddit.com/r/LocalLLaMA/comments/1edryd2/how_fast_big_llms_can_work_on_consumer_cpu_and/)
  - Would not it be cheaper to build a PC with 256-512 GB of RAM and run very big models on it than buying two Rtx 3090 and having only 48gb of VRAM?

- I'll get some example numbers with Llama 3.1 8B Instruct Q6_K with a context size of 8192 tokens.
  - Running on my RTX 4060 Ti: 25.46 tokens/s
  - Running on my Ryzen 5 7600: 6.66 tokens/s
  - As you can see, CPUs are the devil.
  - The RTX 4060 Ti's memory bandwidth is 288 GB/s, and my RAM is 81.25 GB/s (dual-channel DDR5 5200), and dividing those numbers comes out to close to the same ratio--while the GPU memory is 3.54x as fast, using the GPU for inference is 3.82x as fast.
  - Using shared memory with the GPU is far worse because PCI-e 4.0 x8 is only about 16 GB/s one way (PCI-e 5.0 is only twice that fast).

- I built a pc with 128G RAM , I9 14900K and one 4090 GPU. I have loaded Llama3.1 70B Q2 with Ollama, and test it, the token per second is about 9. Then I loaded Mistral Large 2 123B Q2, the token per second is about 2

- 14900K has only two memory channels which gets bandwidth bottleneck at 6 threads alone! So you get almost same CPU performance as me with 12700H in a laptop. I wish you researched more before building such a system there was no point of buying 14900K at all neither for LLMs or gaming expect you use it for something else ofc..

- For running LLMs on CPU you must buy something with at least 8 memory channels. Dual channel CPUs get bandwidth bottleneck at 6 threads alone and begin loosing performance severely as you increase thread count. Not cores rather only threads! So with 8 memory channels you can use 24 threads and gain around 4 times more performance. (Exact performance depends on clock, memory speed etc ofc but it is roughly like this.)

- ## [Running LLMs partially on cpu. DDR5 R1(single rank) vs R2(dual rank) : r/LocalLLaMA _202403](https://www.reddit.com/r/LocalLLaMA/comments/1b3vhc7/running_llms_partially_on_cpu_ddr5_r1single_rank/)
  - 2x32gb, dual rank(8x32bit/256bit), 6800mhz, 13600 MT/s, total bandwidth 217.6 GBps
  - 2x24gb, single rank(4x32bit/128bit), 7800mhz, 15600 MT/s , total bandwidth 124.8 GBps

- I would go for the first one with much more bandwith. As far as I know this usually is the bottleneck. But I haven't benchmarked anything like it myself.
  - 217 GBps sounds almost too good to be true. Only 3.5x slower than 4080's bandwidth.

- ## [Anyone actully try to run gpt-oss-120b (or 20b) on a Ryzen AI Max+ 395? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nabcek/anyone_actully_try_to_run_gptoss120b_or_20b_on_a/)
- people post actual good benchmarks, 49T/s on TG and 700T/s on PP. 
  - Better than my 14900k (96GB 6800) + RTX3090: (32T/s on TG and 220-280T/s on PP).

- Ryzen 7950X + 3080 + 96GB DDR5-6000 gets me around 330T/s on PP and 15 on TG for the 120b

- ## [Most economical way to run GPT-OSS-120B? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n13rsq/most_economical_way_to_run_gptoss120b/)
- I get 100t/s on short (2-3k) context and ~85t/s on longer context (12-14k) using three 3090s.
  - Two Mi50s and a Cascade Lake ES Xeon get me ~25t/s on the same 12-14k context. 

- Framework PC - 128GB LPDDR5x-8000 ! I have 5090 + DDR4-2933 = 18 t/s for GPT-OSS-120B

- Also 5090 + DDR5-6000 (offloading 22 layers) = ~35 t/s for GPT-OSS-120B (full precision ≈ 60GB)

- Given that you already have a PC, I think, the most economical way to run gpt-oss 120b at good speeds is to buy 3 used rtx 3090. It will give you 72gb of vram and it will cost you around 1800 + PSU. It will be roughly the x4 speed of the Framework. 

- I have a Framework Desktop with 64GB. It almost explodes with GPT-OSS-120b loaded but I can actually run the 4bit version for a question or two until it fails and it runs at 50 tokens/s, even with the system having been exiled to SWAP. (openSUSE Tumbleweed, llama.cpp)

- ## [gpt-oss-120b on CPU and 5200Mt/s dual channel memory : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mj6xif/gptoss120b_on_cpu_and_5200mts_dual_channel_memory/)
  - I have run gpt-oss-120b on CPU, I am using 96GB dual channel DDR5 5200Mt/s memory, Ryzen 9 7945HX CPU. I am getting 8-11 tok/s. I am using CPU llama cpp Linux runtime.

- 5800x with 96gb of system ram DDR4 3200 in dual channel. Getting just over 5t/s with the 120, nothing offloaded to GPU

- ## [How to run gpt-oss-120b faster? 4090 and 64GB of RAM. : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mnsg6d/how_to_run_gptoss120b_faster_4090_and_64gb_of_ram/)
  - llama-server --hf-repo unsloth/gpt-oss-120b-GGUF --hf-file gpt-oss-120b-F16.gguf ^ -c 16384 -ngl 99 -ot ".ffn_.*_exps.=CPU" -fa ^
  - with 16k context here, I am getting around 14tps 

- I'm getting 35T/s and 120T/s prefill on a 3090 and 14900K but that is with 96GB of fast DDR5 (6800)

- ## [gpt-oss-120b performance with only 16 GB VRAM- surprisingly decent : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1miprwe/gptoss120b_performance_with_only_16_gb_vram/)
  - GPU: RTX 4070 TI Super (16 GB VRAM)
  - CPU: i7 14700K
  - System RAM: 96 GB DDR5 @ 6200 MT/s (total usage, including all Windows processes, is 61 GB, so only having 64GB RAM is probably sufficient)
  - Model runner: LM Studio
  - 13 t/s is a speed that I'd consider "usable"

- Just posting my numbers too! 5090 + 60GB of DDR5, 22 cpu moe layers offloaded:
  - 36.61 tokens per second

- ## [10.48 tok/sec - GPT-OSS-120B on RTX 5090 32 VRAM + 96 RAM in LM Studio (default settings + FlashAttention + Guardrails: OFF) : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mk9c1u/1048_toksec_gptoss120b_on_rtx_5090_32_vram_96_ram/)
  - Just tested GPT-OSS-120B (MXFP4) locally using LM Studio v0.3.22 (Beta build 2) on my machine with an RTX 5090 (32 GB VRAM) + Ryzen 9 9950X3D + 96 GB RAM.
  - Everything is mostly default. I only enabled Flash Attention manually and adjusted GPU offload to 30/36 layers + Guardrails OFF + Limit Model Offload to dedicated GPU Memory OFF.

- Try llama.cpp with-ot ".ffn_(up|down)_exps.=CPU" This offloads up and down projection MoE layers instead of full MoE layers. You should get 30 t/s
  - I have a budget workstation that costs less than your GPU alone and I get 20 t/s with Unsloth their 120b. That is 20 t/s for the first 1K tokens, it slows down to 13 t/s at 30K context.
  - My specs: 16 GB RTX 5060 Ti + 16 GB P5000 + 64 GB DDR5 6000

- I can second that: With the same (short) prompt I get 17.9 t/s
  - Specs: 16 GB RTX 5060 Ti + 128 GB DDR5 5600 / Ryzen 9 9900X
  - .\llama-server.exe -c 60000 --chat-template-kwargs "{\"reasoning_effort\": \"low\"}" -fa -ctk f16 -ctv f16 -m "c:/....../gpt-oss-120b-GGUF/gpt-oss-120b-BF16.gguf" -ub 512 --temp 1.0 --top-p 1.0 --top-k 0 --min-p 0 --repeat-penalty 1.0 --no-mmap -sm none -ngl 99 --n-cpu-moe 44

- Thats really bad. I get 30T/s for 3090 + 14900K 96GB. 25T/s for the 14900K with just 8GB VRAM usage.
  - This is the trick: 
  - --n-cpu-moe 36 \    #this model has 36 MOE blocks. So cpu-moe 36 means all moe are running on the CPU. You can adjust this to move some MOE to the GPU, but it doesn't even make things that much faster.
  - --n-gpu-layers 999 \   #everything else on the GPU, about 8GB

- I get 9 t/s on integrated gpu in my thinkpad, you are doing something wrong

- I'll trade my 4070 Ti Super that gets 50 tokens/second for your ridiculously slow 5090.

- GPU: NVIDIA RTX 4000 SFF Ada Generation GPU: AMD ATI 04:00.0 Raphael Memory: 54.6GiB / 94.2GiB
  - eval rate: 8.03 tokens/s 

- ## [16→31 Tok/Sec on GPT OSS 120B : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1ndit0a/1631_toksec_on_gpt_oss_120b/)
  - CPU: Intel 13600k
  - GPU: NVIDIA RTX 5090
  - Old RAM: DDR4-3600MHz - 64gb
  - New RAM: DDR5-6000MHz - 96gb
  - Model: unsloth gpt-oss-120b-F16.gguf
  - 16 tok/sec with LM Studio → ~24 tok/sec by switching to llama.cpp → ~31 tok/sec upgrading RAM to DDR5
  - `llama-server --n-gpu-layers 999 --n-cpu-moe 22 --flash-attn on --ctx-size 48768 --jinja --reasoning-format auto -m C:\Users\Path\To\models\unsloth\gpt-oss-120b-F16\gpt-oss-120b-F16.gguf  --host 0.0.0.0 --port 6969 --api-key "redacted" --temp 1.0 --top-p 1.0 --min-p 0.005 --top-k 100  --threads 8 -ub 2048 -b 2048`

- You can get more speed on computers with hybrid cores (a mix of p and e cores) by pinning llama.cpp to p-cores only. 

- Maybe even some more speed to win by offloading only up and down projection MoE layers: https://docs.unsloth.ai/basics/gpt-oss-how-to-run-and-fine-tune#improving-generation-speed
  - In my testing, the suggestion in that link is outdated.

- You should spend money on unified memory systems for models like this instead of on a strong GPU like 5090. For example, M4 Max has GPU equivalent to 4070 mobile, which is not super fast, but it can run this model at 75 t/s on llama.cpp and 95 t/s on mlx (though mlx implementation currently has slow PP speed).

- You want to only use 2 lanes if possible so 48x2. If you use all 4 ram slots your speed will be limited.

- For more "long running" sessions, servers, permanent agent running etc, llama.cpp, vLLM and especially ktransformers are FAAAAR better options.

- I am getting 10-11 tokens per second with GPT-OSS-120b on DDR5 4800, 7940HS CPU, 96GB RAM in LM Studio. Guessing I could get at least another 50% performance based on what you're saying
  - GLM 4.5 Air is running at 4-5 TPS with this setup. Qwen3 30b-A3B runs at about the same speed as GPT-OSS-120b.

- ## [gpt-oss-120b in 7840HS with 96GB DDR5 : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nf3fof/gptoss120b_in_7840hs_with_96gb_ddr5/)
  - With this setting in LM Studio Windows, I am able to get high context length and 7 t/s speed (noy good, but still acceptable for slow reading).
  - Is there a better configuration to make it run faster with iGPU (vulkan) & CPU only? I tried to decrease/increase GPU offload but got similar speed.
  - I read that using llama.cpp will guarantee a better result. Is it significantly faster?

- Don't force the experts onto CPU, just load them all in gpu, that's why you have the iGPU in the first place! You should be able to load ALL the layers on GPU as well.

- Loading all layer to iGPU will result unable to load vulkan0 buffer, I think because only 48GB can be allocated to my iGPU
  - No, . Put them all there, it will work. If dont, put 23 or so, do a tryout load. VRAM is also your shared ram, all equal. I got ryzen 7940hs, runing unsloth Q4-K-XL, with 20K context, its about 63Gb of space, i just put all on the GPU on LMstudio, ans just one processor on inference. I get 11 tokens per second, linux mint.

- Thoughts from someone who has the same iGPU and used to have 96GB memory:
  - Your offload config looks about right for your memory size (I wrote a comment about it on a lower message thread)

- ## [Managed to get GPT-OSS 120B running locally on my mini PC! : r/selfhosted _202508](https://www.reddit.com/r/selfhosted/comments/1mk6jlt/managed_to_get_gptoss_120b_running_locally_on_my/)
  - I was able to get the GPT-OSS 120B model running locally on my mini PC with an Intel U5 125H CPU and 96GB of RAM to run this massive model without a dedicated GPU, and it was a surprisingly straightforward process. The performance is really impressive for a CPU-only setup. 
  - MINIPC: Minisforum UH125 Pro
  - CPU: Intel u5 125H
  - RAM: 96GB
  - Model: GPT-OSS 120B (Ollama)
  - prompt eval rate: 31.83 tokens/s
  - eval rate: 2.77 tokens/s
  - This is running on a mini pc with a total cost of $460 ($300 uh125p + $160 96gb ddr5)

- ## [You can now run OpenAI's gpt-oss model on your local device! (14GB RAM) : r/selfhosted _202508](https://www.reddit.com/r/selfhosted/comments/1mjbwgn/you_can_now_run_openais_gptoss_model_on_your/)
  - The 20B model runs at >10 tokens/s in full precision, with 14GB RAM/unified memory. Smaller versions use 12GB RAM.
  - The 120B model runs in full precision at >40 token/s with ~64GB RAM/unified mem.
  - There is no minimum requirement to run the models as they run even if you only have a 6GB CPU, but it will be slower inference.
  - Thus, no is GPU required, especially for the 20B model, but having one significantly boosts inference speeds (~80 tokens/s). With something like an H100 you can get 140 tokens/s throughput which is way faster than the ChatGPT app

- ## [What hardware to run gpt-oss-120b? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1miggb2/what_hardware_to_run_gptoss120b/)
- 64GB RAM with ~16GB - 24GB VRAM offloading, or just 128GB RAM.

- Is it really possible to run it with just 128 GB RAM and no VRAM?
  - I'm running it with 96GB RAM and 12GB VRAM and it's usable
  - my setup: 2x RTX 4070, 96GB DDR5 6400MHz RAM, Ryzen 9 7900X
  - It's not a memory issue with WSL (I know that an I've allocated 80 GB of memory to WSL), it just doesn't run very fast. I hit around 10-15 tokens/sec with CPU on Windows using LM Studio, but running it in the same LM Studio (or Ollama) on Linux does not go well. I'm getting around 0.8 tokens/sec, not sure why.
  - I'm running the 20B version at around 200-250 tokens/sec though, which is great
  - I can run it straight from CPU on 96GB and it seems to run about the same. I'm not sure. to stop LM Studio from using my GPUs, I ran it on a WSL instance without GPU access, it got the same-issue Tok/s, maybe slightly lower by the token per second, but really not that big of a difference when it's already that slow

- I was able to run gpt-oss-120b in LM-studio on a 5060ti 16Gb video card + 64Gb DDR4 RAM. I placed 8 layers in video memory, the rest in RAM. The performance was 10 tokens per second, for comparison, the younger model worked at a speed of 85 tokens per second.

- ## 💡🚧 [gpt-oss 120B is running at 20t/s with $500 AMD M780 iGPU mini PC and 96GB DDR5 RAM : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nxztlx/gptoss_120b_is_running_at_20ts_with_500_amd_m780/)
  - Everyone here is talking about how great AMD Ryzen AI MAX+ 395 128GB is. But mini PCs with those specs cost almost $2k. 
  - I searched for mini PCs that supported removable DDR5 sticks and had PCIE4.0 slots for future external GPU upgrades. 
  - I focused on AMD CPU/iGPU based setups since Intel specs were not as performant as AMD ones. The iGPU that came before AI MAX 395 (8060S iGPU) was AMD Radeon 890M (still RDNA3.5). Mini PCs with 890M iGPU were still expensive.
  - The cheapest I could find was Minisforum EliteMini AI370 (32GB RAM with 1TB SSD) for $600. Otherwise, these AI 370 based mini PCs are still going for around $1000.
  - Next, I looked at previous generation of AMD iGPUs which are based on RDNA3. I found out AMD Radeon 780M iGPU based mini PC start from $300 for barebone setup (no RAM and no SSD). 780M iGPU based mini PCs are 2x times cheaper and is only 20% behind 890M performance metrics. 
  - I checked many online forums if there was ROCm support for 780M. Even though there is no official support for 780M, I found out there were multiple repositories that added ROCm support for 780M (gfx1103)
  - 🖥️ I bought MINISFORUM UM870 Slim Mini PC barebone for $300 and 2x48GB Crucial DDR5 5600Mhz for $200. I already had 2TB SSD, so I paid $500 in total for this setup.
  - There was no guidelines on how to install ROCm or allocate most of the RAM for iGPU for 780M. So, I did the research and this is how I did it.
  - I know ROCm support is not great but vulkan is better at text generation for most models (even though it is 2x slower for prompt processing than ROCm).
  - Mini PCs with 780M are great value and enables us to run large MoE models at acceptable speeds. Overall, this mini PC is more than enough for my daily LLM usage (mostly asking math/CS related questions, coding and brainstorming).
  - I was getting great numbers that aligned with dual DDR5 5600Mhz speeds (~80GB/s).
  - I know ROCm support is not great but vulkan is better at text generation for most models (even though it is 2x slower for prompt processing than ROCm).

- ROCM with gpt-oss 120B mxfp4
  - tg128: 18.7 
- VULKAN (RADV only) all with Flash attention enabled
  - qwen3moe 30B. A3B Q4_1:  32.6, 22.3
  - gpt-oss 20B MXFP4 MoE: 28.1, 24.8
  - gpt-oss 120B MXFP4 MoE:  20.4, 18.1
  - qwen3moe 235B. A22B Q3_K:4.3
  - glm4moe 106B. A12B Q4_1:9.1

- just in case someone wants to compare with strix halo:
- STRIX-HALO @ Debian 13 6.16.3+deb13-amd64 (kernel >= 6.16.x for optimal memory sharing)
- ROCm
  - gpt-oss 120B MXFP4 MoE: 47.8
- Vulkan
  - gpt-oss 120B MXFP4 MoE: 51.5

- For me also same but the problem is when context become big speed decrease
  - I get 18t/s at 8k context 

- DDR5 is almost 2x faster than my DDR4 tower PC with AMD Ryzen 5950x CPU. DDR6 should come soon (2026 or 2027?). Also, It is high time that consumer PC industry embraced quad channel memory setup (e.g. DDR5 with 4 channels in mini PC would be amazing).

- Pretty incredible is 96gb the max or can it go 128?
  - it can potentially go up to 256GB but I could not find SO-DIMM DDR5 with that size. But yes, 2x64GB = 128GB is possible but those sticks are expensive! From $200 for 96GB to $400 for 128GB. So, 96GB is cost effective.

- with 90GB RAM allocated to iGPU, gpt-oss-120b-GGUF should comfortably fit 64k context. Also, running with that context will be slow for the initial cache loading (it may take hours).
  - Update: just laoded gpt-oss 120b with 130k context. With flash attention, that context took extra 5GB only. So, I would say it is possible to load the full context.

- 2x64GB dual channel near or above 6000 mt/s are not seen yet. 2x48GB dual channle can go up to 6800mst/s and some may overclock(超频) it to even higher speed depending your luck, may not be stable.
  - The key is to use 2 slots only. 4 slots will drop the speed significantly even from the exact same brand model spec.

- Is this a one-off for only running gpt-oss 120B or is this platform expected to be somewhat future proof and newer models a likely to work on it?
  - Yes. This is future proof as long as llama.cpp and vulkan exist. Yes, this will run Qwen3 235B. Q3 should run at 6t/s.

- did you also compare the performance against running it on the CPU only, without iGPU? If I remember correctly, using the iGPU mostly improves pp performance while tg is still limited by the (shared) memory bandwidth speed? Is that (still) true?
  - Also, since you seem into getting the most out of (relatively) limited hardware, I think it could be an interesting experiment to run a bigger MoE using mmap and a PCIe Gen 4 NVMe SSD (max. ~8 GB/s). I think this might be surprisingly usable for use cases without limited context, etc.
- Yes, I tested with ik-llama for CPU. The best I got for gpt-oss 120b with CPU was 13t/s. So, iGPU improves TG by ~65-70%. I also tried glm 4.5 air in vulkan. I got 9t/s TG. I haven't tried SSD offloading. But yes, I could try qwen3 235B Q4 for that.

- Excellent results! My M4 Max 128GB was more like $6k and is only about 2.5X faster (55tok/s) with flash attention. Without flash attention, it’s down around <10tok/sec.
  - What a cool budget option you found! gpt-oss-120b is a great tool-using, private, safe LLM.

- I squeeze 11 tokens/ s with mini pc ryzen 7940hs, 780M and 64 GB 5600 mhz ddr5. Vulkan cpp. I fit 21 Layers. The rest goes to cpu. Inference 6 cpu cores. Context 18000. Maybe 20000. Linux mint mate latest version. Do not use last vulcan cpp 1.51. Use 1.50.2
  - I get 13 t/s with CPU only in ik-llama cpp

- Can you give AMDVLK a try in addition to RADV for your Vulkan perf? On my (completely different but still AMD so it may transfer to yours) hardware AMDVLK basically matches ROCm in PP while still being slightly faster than ROCm at TG (not as fast as RADV though).
  - you're right, RADV starts off slower, but then doesn't slow down as much when context increases.

- Can someone do the same with a Ryzen AI HX 370? They are on Alibaba for around 400$ now (Mini PCs incl an Oculink port) and can be equipped with 128GB DDR5.

- Whats the max context it can run?
  - I have not tested it yet. But with 90GB RAM allocated to iGPU, gpt-oss-120b-GGUF should comfortably fit 64k context. Also, running with that context will be slow for the initial cache loading (it may take hours).
  - Update: just laoded gpt-oss 120b with 130k context. With flash attention, that context took extra 5GB only. So, I would say it is possible to load the full context.
- The problem with context is not at the ininitial run, it tends to deminish the infererence speed as the context filled up.

- I wonder what speedup you would get if you slapped a 3060 12gb EGPU onto it
  - much slower. I have a mini PC with an even older iGPU (680m), and I run almost all MoE models > 20B sometimes faster than folks with 12GB vRAM

- Would a similar approach work with say an Intel iGPU on a desktop motherboard using vulkan? I've got an older 12th Gen i7 but 4x64gb DDR4 (will be slow I know) and wondering how it would compare to just CPU-only.
  - It should be possible but ddr4 will be 2 times slower
- No, desktop iGPUs are very weak, usually. They just exist to provide video out. AMD has some large desktop iGPUs (the G series processors), but I don't think Intel does. Intel iGPUs are also generally not as good as AMD's, at least for llama.cpp.

- ## [More RAM or faster RAM? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nzf0zf/more_ram_or_faster_ram/)
  - If I were to run LLMs off the CPU and had to choose between 48GB 7200MHz RAM (around S$250 to S$280) or 64GB 6400MHz (around S$380 to S$400), which one would give me the better bang for the buck? This will be with an Intel Core Ultra.
- Little to no difference in speed. You need to optimize for the number of memory channels you have to ensure the highest bandwidth possible.
  - This is why folks opt for older Xeon or Epyc machines, because even with slower ram, they have oodles(大量或很多) more ram bandwidth.

- I bought 2x64 sticks at 6400 on paper but only 5600 stable for my system. I can run GLM 4.6 at 5 t/s and q2, but it beats anything else I could run easily. Cost me 380 euros, totally worth it.

- More Ram.. I use all 32 GB Vram from RTX5090 and 50+ GB Ram just to run Wan2.2.
  - I would say at the minimum you should get 128 GB ram if you want to run LLM (so you can offload and run 70B model). 
  - Personally my spec is 5090 + 256 GB ram so I can offloading most mid size LLM.

- VRAM is up to 20 times faster than 6000MHz RAM, there lies your answer
  - Those models are MoE models and will run at usable speed. Even a 355b GLM 4.6 runs at 4 to 5 tokens per second on 128gb ram on my system. 
  - With upcoming implementations of MTP this might get uplifted into the 10 tokens per second range. MoE models are also getting sparser and sparser. 128 GB ram even if it's just dual channel is absolutely worth it in my opinion.

- Neither of those rams will make a significant difference in inference speeds for llms, both are quite slow bandwidth wise. The useful bit of those ram kits is the capacity, could you get a cheaper 64gb kit instead?

- You even sure your CPU and mobo can utilize these speeds?

- 
- 
- 
- 
- 
- 
- 

- ## 🖥️ 我想买个 已装好但可自己配置的台式机工作站 或 自己买机箱/cpu/2张3090显卡自己装台式机, 要求台式机的机箱要尽量小，同时能发挥多张显卡的计算能力，散热要正常
- 铭瑄 ARL-HX 迷你双卡工作站
  - 内部搭载了两张Intel Arc Pro B60显卡，合计提供48GB GDDR6显存

- [求推荐一款小型机箱？ - 知乎](https://www.zhihu.com/question/1945481402184364122)
  - 坚定小型化，就得把预算提到600以上。个人推荐方糖机械大师c28这个型号，建议直接上闲鱼搜二手的
  - 坚持要小机箱不仅是提高预算的问题，后面装机会有一堆麻烦

- ### [2025年5月更新，电脑机箱推荐。推荐一波高颜值的机箱。包含ITX, M-ATX, ATX, E-ATX机箱](https://www.zhihu.com/tardis/zm/art/210537601?source_id=1003)
- ITX：专门为小型电脑机箱设计的主板规格，尺寸 170mm×170mm。
  - mini-itx机箱的特点是比较小巧，携带相比大机箱要方便些，但是散热相对大机箱要差一点点，也有散热很好的ITX机箱。ITX机箱的另一个缺点就是配套的主板及电源要贵不少。
- DTX：尺寸为170mm×203mm。这个尺寸的主板很少见，ROG的部分高端主板是这个规格（如ROG C8I主板），这个规格也是为小钢炮设计的，部分ITX钢炮机箱支持这个尺寸，购买机箱的时候需要仔细看看
- ATX：ATX 可以理解为全尺寸主板，尺寸305mm×244mm。
  - ATX（中塔）机箱是目前大部分用户的选择，这类的机箱尺寸偏大，基本都支持ATX，M-ATX，ITX版型，部分支持包括E-ATX在内的所有版型。
  - 优点在于散热好，ATX机箱基本都支持240及360水冷，对大型双塔风冷散热的支持也更好。
  - 扩展位多，方便安装更多的硬盘等设备。
- M-ATX：就是缩小版的 ATX。长244mm，宽度有多种规格。主流为244mm×244mm。
  - M-ATX机箱的优点在于大小适中，配套的M-ATX主板价格合适，性价比高，扩展性也够用，是大部分用的选择。
  - M-ATX机箱的散热也不错，很多都支持240水冷及中等尺寸的风冷。
  - 但是目前优秀的M-ATX机箱比较少，尤其是高端的M-ATX机箱几乎是空白。
- E-ATX：加大型主板，尺寸305mm × 330 mm。主要用于服务器主板。例如搭配AMD 3990X的主板。
  - E-ATX（中塔，全塔）机箱推荐, 这类型的机箱比较大，通常都支持360水冷，大型风冷，散热基本都非常优秀。硬盘位也很多。
  - 这类型的机箱比较适合游戏发烧友，或服务器工作站。
  - 做服务器或工作站用的朋友建议考虑使用分形工艺的Meshify 2和D7，以及这两款机箱的XL型号（双显卡用）。我个人在使用这两款机箱，散热优秀，设计，用料，做工都非常不错。Meshify 2是突出散热，D7是突出静音。
  - 分形工艺 Torrent: 箱体长宽高（mm）544（长）*242（宽）*530（高）mm

- ### [25L Portable NV-linked Dual 3090 LLM Rig : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1l0zsv7/25l_portable_nvlinked_dual_3090_llm_rig/)
  - cpu: AMD Ryzen 7 5800X 3.8 GHz 8-Core Processor
  - Motherboard: Asus ROG Strix X570-E Gaming ATX AM4 Motherboard
  - NVlink SLI bridge
  - Mechanic Master C34Plus Portable Desktop ATX Case with Aluminum Handle: 5.2 Kilograms, 39.1 x 18.5 x 34.3 cm.
  - CORSAIR RMe Series Fully Modular Low-Noise Power Supplies: 1200 watts
  - ⚠️ WARNING - these components don't fit if you try to copy this build. The bottom GPU is resting on the Arctic p12 slim fans at the bottom of the case and pushing up on the GPU. Also the top arctic p14 Max fans don't have mounting points for half of their screw holes
  - All that being said, with a 300w power limit applied to both gpus in a silent fan profile, this rig has surprisingly good temperatures and noise levels considering how compact it is.
  - During Cinebench 24 with both gpus being 100% utilized, the CPU runs at 63 C and both gpus at 67 Celsius somehow with almost zero gap between them and the glass closed. All the while running at about 37 to 40 decibels from 1 meter away.
- I did a bunch of testing back when I had a 4x 3090 rig. The sweet spot was always between 250-300W for inference. Above that I saw no improvement in inference speed (this was a DDR4 system, YMMV with DDR5). Below 250 speed would start dropping off quite quickly.
  - If memory serves me, I settled on 275W and enjoyed the power savings while not sweating the .05 tokens/sec it cost me for not running over 300W
- Neat build. Even power limiting to 200W doesn't have that big of a hit on inference. (Exl2)
  - I power limit all mine to 200w. It's perfectly fine.

- ### [Smallest case possible for dual gpu? : r/sffpc _202312](https://www.reddit.com/r/sffpc/comments/187og11/smallest_case_possible_for_dual_gpu/)
- Someone else just posted details of their NR200 build with dual 4090s, might be worth a look?
  - 18.49 x 37.49 x 29.18 cm
  - 新款mini-itx是 NR200P V2
- Didn't realise the NR200 had the possibility of going dual GPU. I'mm super new to SFF.
  - pretty sure you would have to do PCIe birfurcation for that
- Yeah, max mobo you're going to fit in there is an ITX, and building round it already a squeeze with one GPU to think about (with any kind of air CPU cooler)

- check out Cerberus (mATX) or Cerberus X (full ATX)

- Generally sff cases are designed around ITX motherboards with only one pcie slot, finding a sff case that will fit an m-ATX motherboard is going to be near I possible. I have a nr200p same as the guy with dual 4090s, it only officially supports ITX boards.. it's also not really small form anymore (I have a tophat with a radiator it)

- [Smallest case for mATX + air cooled cpu + 2 gpu : r/buildapc _202308](https://www.reddit.com/r/buildapc/comments/15x7h9h/smallest_case_for_matx_air_cooled_cpu_2_gpu/)
  - Asus Prime AP201 MicroATX Mini Tower Case: 20 x 35 x 46
  - Sliger Cerberus. mATX case much smaller than the Asus AP201 (huge at 33L, when the Sliger Cerberus is 19.6L).

- [Good pc case for dual gpu setup? : r/VFIO _202402](https://www.reddit.com/r/VFIO/comments/1ao7gsj/good_pc_case_for_dual_gpu_setup/)
  - Take a look at Fractal Design Meshify 2, or even the XL version. It should have plenty room for what you want.

- ### [Small-form-factor all-air-cooled dual RTX 3090 SLI 1000W build : r/sffpc _202107](https://www.reddit.com/r/sffpc/comments/orug4s/smallformfactor_allaircooled_dual_rtx_3090_sli/)
  - Case: Sliger Cerberus X
  - Motherboard: MSI MEG X570 Godlike
  - CPU: AMD Ryzen 5600X
  - RAM: HyperX Predator 32GB 3333Mhz
  - GPU: 2x RTX 3090 Founder's Edition SLI
  - PSU: Silverstone SX1000 Platinum SFX-L
  - CPU Cooler: Cryorig H7
  - Case fans: 2x Arctic P14 140mm, 3x BeQuiet Pure Wings 2 92mm
  - Temps under full load: GPU core 66/50, GPU memory junction 102/102, CPU 85
  - Using software to estimate power draw at full load I'm guessing around 800W. I am confident the PSU can handle a 5900X even without undervolting but temps would be an issue so I'm leaving it with the 5600X for now. The 5600X is slightly undervolted using PPT 70W, negligible performance hit compared to stock but a few degrees lower temps.

- ### [Looking for a 2 x 3090 case : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j3h23g/looking_for_a_2_x_3090_case/)
  - I am looking for either a case or an open air rig where I could fit two 3090 FE connected with nvlink.
  - I need to be able to use pcie extender otherwise there is not enough spacing on the Mobo for putting the nvlink because of the 3 slots GPUs.

- I feel like this shouldn't require too much special consideration. I have a standard mid-tower case and it fits 2 3090s in it just fine.

- If you can afford it, phanteks enthoo pro 2 server edition is amazing. Internal fan bracket lets you direct air onto the gpus. My 2x3090s stay below 30 C at idle, and never go above 70 on load.
  - 24 x 56 x 58, 77L

- I can just barely fit 3 MSI 3090s in my Corsair 7000D Airflow, 2 horizontal and one vertical with riser. Tons of fans.
  - 24 x 55 x 60

- Almost any full ATX case with 8 pcie slots would work fine. Antec P101 for example.

- [Smallest case for dual air-cooled 3090's? : r/sffpc _202104](https://www.reddit.com/r/sffpc/comments/mzfg3p/smallest_case_for_dual_aircooled_3090s/)
- Wondering if getting a smaller case with Quadro A6000 would be better option than bigger case with Dual 3090?
  - An A6000 would be amazing but it’s just so damn expensive. It doesn’t make sense to me from a value perspective.
  - And since the 3090 and A6000 have the same amount of cuda cores, having dual 3090’s would actually give me up to twice the performance as a single A6000, but with the same amount of total memory.
- Are you sure you can combine the VRAM in your workload? You'd most likely need an NVLink bridge aswell.
  - The 3090 has NVLink, although certain features are disabled in software. For ML training though I’m pretty sure I would be getting the full NVLink bandwidth.

- Fractal R6 has a lot of room. So does the 7

- If you need the NVLink, you'll need one with two 16x slots spaced 4 slots apart (NVidia only sells 4-slot spacing NVLink-bridges). 
  - Also: Do you need the PCIE bandwith for your workload? Most consumer CPUs don't have enough PCIE lanes, so the two GPUs will be running in only 8x each.
- Yeah, Cerberus X won't be an option if you wanna aircool the CPU. The O11D is a pretty giant case (57L).
  - If you want something smaller, I'd recommend the Meshify C. It's just under 40L, has a standard mid-tower layout, can fit big ATX PSUs, a big aircooler like the NH-D15 and has good ventilation (if you add 3x 120mm fans in the front) so your GPUs will get enough airflow.

- ## [一次性价比爆棚的显卡升级之旅：折腾 V100 显卡续集，二手神卡跑ComfyUI！ - 知乎 _202507](https://zhuanlan.zhihu.com/p/1929587520502498303)
- Tesla V100 SXM2	
- V100 是 Volta 架构（sm_70），而现在一堆 AI 框架都要求 Ampere 起步（sm_75 以上）。导致这些模块直接报错
- LTX-Video-Q8-Kernels 的 setup.py 未适配 Tesla V100 的 sm_70 架构，仅支持 Ampere（sm_80+）等较新架构。
- Triton 3.3.0 与 sm_70 兼容性差，sageattention 的 INT8 优化可能不支持 V100。PyTorch 2.7.1+ 要求 sm_75，而 PyTorch 2.4.1 是最后一个支持 sm_70 的版本。 解决： 回退到 PyTorch 2.4.1 和 Triton 3.0.0
- is_flash_attention_available 是 PyTorch 2.5.0+ 的 API，PyTorch 2.4.1 不支持。
- FlashAttention-2 的 flash_attn_func 不存在于 FlashAttention-1（1.0.9），而 V100（sm_70）不支持 FlashAttention-2。 解决： 安装 FlashAttention-1
- PyTorch 的 注意力机制，FlashAttention-1或者xformers内存效率低，视频生成模型（如 Wan2.1、Hunyuan）需 大量显存，V100 的 16GB 不足。而sageattention又不支持V100，所以暂时无解

- ## [Laptop with 32 GB VRAM for Stable Diffusion : r/StableDiffusion _202305](https://www.reddit.com/r/StableDiffusion/comments/1353g26/laptop_with_32_gb_vram_for_stable_diffusion/)
- I don't think so, unless you do an "egpu" with a card in a separate case connected via thunderbolt. My card has 16gb VRAM and I can run a 2048x2048 without tiling. Tiling lets that go much higher, so that's the way to go if you want to do large images. Generally speaking the vram stuff is mostly an issue if you want to train LoRAs/embeddings/hypernetworks/etc.

- Is 16 GB of VRAM on your machine enough to train LoRAs and checkpoints? I can do very limited training with my current 8 GB VRAM machine, and I'd be very interested in training LoRAs and checkpoints to personalize my work. 
  - Yes, 16gb is enough. Until recently I was able to do batch sizes of 8 for Dreambooth fine-tuning, generally in other AI training it's good to do that or accumulate gradients

- ## [AMD 计划于 2026 年推出 Zen 6 架构 Ryzen 处理器，有何亮点值得期待？ - 知乎 _202506](https://www.zhihu.com/question/1944114025425269198)
- 2006年，ATi被AMD以54亿美元收购，“Fusion融合”成为新AMD最高战略。CPU、GPU、主板芯片组三者合一，集成为前所未有的SOC单芯片，即“APU”，异构运算以提升运算效能
- 2017年，“Zen禅”架构的锐龙处理器上市。单芯片设计的APU力挽狂澜，桌面处理器触底反弹、移动处理器迅速崛起、拿下双游戏主机大单。但称雄桌面、制霸服务器端，AMD依靠的是Zen2开始的Chiplet多晶粒模块化设计，多核堆死老师傅。
- 摩尔定律失效，单芯片面积有限，先进制程代价昂贵，剥离了GF格罗方德工厂、几近破产边缘抢救回来的AMD，必须得精打细算
- 新一代Zen6架构，CCD计算核首发2纳米制程，连财大气粗的苹果、高通都没敢下这么重的本。
- AMD选择将Chiplet进行到底： 2nm的Zen6 CCD计算核，2-3种3nm的RDNA5GPU，用4种以上3nm的APU组合在一起
  - Strix Halo架构那颗AI MAX+ 395上取得的经验，成为日后的封装标准

- Strix Halo架构的AI MAX+ 395，性能足以媲美RTX4060；只是双CCD计算核拉高了成本，试水新封装良率不高，又遇上AI推理本地化热潮，造成出厂价奇高，单U价格超过4060游戏本整机，叫好不叫座。

- 2027年末上市的AI MAX 500系列新品，是APU，也是一颗可以做成独显的GPU：
  - 【小杯】Medusa Halo mini，也是 AT4 GPU，12大小核2LP，24CU RDNA5，PTX 1050同芯，对标4060
  - 【大杯】Medusa Halo，也是 AT3 GPU，至少具备12核，可选CCD计算核桥接补齐，48CU RDNA5，PTX 1060同芯，对标4070
  - 小杯使用128bit LPDDR5X内存控制器，显存可达128G，更适合经济游戏本
  - 大杯采用384bit LPDDR6内存控制器，显存可达512G，针对价格不敏感的AI行业用户

- ## [How well does ComfyUI perform on macOS with the M4 Max and 64GB RAM? : r/comfyui _202503](https://www.reddit.com/r/comfyui/comments/1jhifyi/how_well_does_comfyui_perform_on_macos_with_the/)
- TLDR - if you want to work linear on one image, a Mac is a huge waste of time. Maybe 25% of the speed of a decent NVIDIA PC for AI generation. 
  - However, if you know how or want to multitask, it’s easily the best system you can purchase.

- I don't know if you'll find this information but based on estimates comparing to the M4 Pro, it should reach close to half the performance of an $800 PC with an RTX 3060

- I have a Mac Mini M4 Pro with 48GB of unified RAM. As my daily driver for everyday things, it's great, even great at media encoding, but for generative AI stuff, compared with my Linux PC with a RTX 4090 - it pales in comparison. We are talking minutes vs seconds here for a 1024x1024 Flux generation. Most of it is tuned for Nivida CUDA and that is the key. Apple Silicon offers great performance for everyday computing, but its support for machine learning frameworks like PyTorch sucks butt compared to CUDA.

- I transitioned from dabbling with generative AI images on M1 Max Macbook to using a PC that I owned with Nvidia RTX 3060 graphics card. 
  - The PC with ComfyUI was 3 times faster than my Mac which was using DrawThings (I installed ComfyUI on Mac but abandoned it because DrawThings was more convenient and faster). 
  - After getting more involved I ended up buying a PC with Nvidia RTX 4090 graphics card. Very happy with that decision. I love the Mac for most things but most likely even the M4 Max might prove to be frustrating to use to keep up with the rapid advances in the ComfyUI - Stable Diffusion world.

- AI image and video generation require cuda cores to function properly so Apple or even AMD gpus are not recommended.

- I ran ComyUI Flux Schnell, Pro and several LORAs on Mac studio Max4 base model and most models will run fine. I only ran into memory issues with video generation therefore moved to M3 Ultra 96GB. I dont have a reference point with PC but i am getting 15-30sec for 1024x1024 img generation for most workflows.
  - That's pretty slow. A NVIDIA 3090ti 24gb PC can do that in under half that

- my Mac M4 16gb is much more slower than my old PC with the good old Geforce 3060. An Apple a day keeps the Comfyui away.

- ## [Setting up ComfyUI with AI MAX+ 395 in Bazzite : r/StableDiffusion _202510](https://www.reddit.com/r/StableDiffusion/comments/1nux1f0/setting_up_comfyui_with_ai_max_395_in_bazzite/)
  - Qwen took 3 min 20s with fp8 image and clip at 20 steps
  - 1 min 22s for Qwen 4-step lightning lora with 8 steps - 8-step lora doesn't work since it's bf16
  - Flux was super slow first time, running flux-dev at fp8, but after that it was about 1 min 51s
  - WAN 2.2 fp8 high-lo 20 steps took 4 min 14s for an image (no speed up lora)
  - WAN 2.2 fp8 with Lightx2v took 18 seconds for an image

- 3 times more expensive than 4070 but 3 times slower than 4070?
  - The purpose is the 128gb of unified ram, it's meant for LLM use, not image generation. 
  - Obviously if you only care about small models that fit in 16gb vram there are way cheaper and faster methods.

- [System Question: AMD Ryzen AI Max + 395 with 128GB LPDDR5x 8000mhz Memory -- Will this work to run ComfyUI? : r/comfyui](https://www.reddit.com/r/comfyui/comments/1nr9ttv/system_question_amd_ryzen_ai_max_395_with_128gb/)
  - It would be really sloooooow. Assuming you’re talking about ai max. There is a YouTube video of a review in Chinese. He shows running some T2i and t2v using some Chinese software. Regardless it was super slow.
  - TLDR CUDA is still king.
- You can load large LLMs and run them decently on that machine but it is not meant for heavy image and video work. 
  - A dedicated GPU will run rings around that machine for rendering time. With a 5090 I can generate 8 seconds of 720p video with FP16 high and low noise models and Loras using sage attention 2 in about 3 to 5 minutes, you don’t need to be running them as high as I am if you want good results with 16 a 24gb vram. 
  - The main difference is that VRAM is faster (much faster) than ram and the GPU chip turns out many more TFLOPS of 16 floating point precision than the tiny 8060S can, not to mention the LPPDR 8000 ddr ram is much slower than GDDR7. 
  - If you just want to run language models get that machine. Otherwise, you’ll be badly equipped and your render times will be forever

- ## [DIY vs Nvidia dgx spark? : r/StableDiffusion _202509](https://www.reddit.com/r/StableDiffusion/comments/1nfoi9d/diy_vs_nvidia_dgx_spark/)
- As already suggested, go for 5090. Or if you need more VRAM and have the budget, go for RTX PRO 6000 (if you are planning some video work, that may be a better option).

- The spark can be a good option for LLMs but not for image generation. Here the currently best options that you can run in an office are the 5090 and the RTX Pro 6000.
  - When it's coming to training you could (should) even consider multiple 5090 like 2 or 4.

- just buy 5090, DGX spark is 40/5060 Ti ish performance

- Spark can do nvlink? did you mean network based NCCL?
  - You want to train Stable Diffusion, i assume UNET based model like XL and 1.5 variant. The less pain in the ass way to train in multi gpu setup is DDP. splitting unet is pain you need special libs like https://github.com/mit-han-lab/distrifuser
  - Incur communication cost, no free meal, DDP even though less demanding than FSDP in communication, it stilll need allreduce the gradient across rank.
  - Is 128G VRAM really important for your use case? DGX Spark is mainly for LLM workflow, large weight model but low active compute sequence (tokens), since LLM sequence isn't as crazy as diffusion models.
  - Engineering and salary cost. Your engineer need to learn to parallelizing gpu, manage networking, setting up torch distribution
  - Most SD trainer is mainly for single gpu
  - DGX Spark is not GDDR memory but LPDDR, and boy moving tensor from GDDR to share memory (gpu internal memory) is already slow, relative to SM speed, and now LPDDR is much slower

- ## [Will this thing work for Video Generation? NVIDIA DGX Spark with 128GB : r/StableDiffusion _202504](https://www.reddit.com/r/StableDiffusion/comments/1ju2mfk/will_this_thing_work_for_video_generation_nvidia/)
- For a machine with 128 GB of LPDDR5 with 273 GB/s memory bandwidth and a paltry 200 GbE ConnectX-7 I find $4k a bit much.

- 4090 still superior to this despite the 128GB of memory. That memory speed is much slower and the TOPS is lower. A 4090 is still best dollar value if your focus is SD and video.

- Check out the HP Z2 G1a that's dropping on Monday. Allocate up to 96GB of RAM to the GPU (I've heard that on Linux you can allocate even more) and the price has surprised me. I'll be getting one as soon as I know Ollama and SD support its APU.
  - Yes, it's 110GB on Linux. Are you surprised that the price is so high? Other Strix Halo machines also with the same APU and the same 128GB of RAM are much cheaper. The Framework Desktop starts at $2000 or just $1700 to buy the motherboard. The GTK is well spec'ed out for around $1800 ready to run. Those are like half the cost of the HP.

- ## [DGX Spark? : r/comfyui _202506](https://www.reddit.com/r/comfyui/comments/1ljbgxn/dgx_spark/)
- 4090 or 5090 for images. RTX 6000 Pro if you're doing video. DGX Spark is for running medium to large-ish LLMs slowly and does not have the right mix of performance for image/video work.
  - The 6000 is about 3x the price of a 5090 so I'll have to think about that one.
  - 96GB of RAM on one GPU. Video models were mostly engineered to run on 80GB H100s. You can run them on less VRAM but with hokey compromises and limitations. Not saying people don’t do it but I don’t have the appetite, would rather just use models as intended.
- Yes, any RTX *90 series card will be faster. DGX Spark is targeted at large text based models. I would not buy this if you plan on using it for image/video gen.

- Just get a nuc and a pro 6000 Blackwell and you'll be set for a long while.
  - Wow it's at least 10k€ just for the gpu!

- [NVIDIA says DGX Spark releasing in July : r/comfyui](https://www.reddit.com/r/comfyui/comments/1labkat/nvidia_says_dgx_spark_releasing_in_july/)
  - Lmao. It has 1/5 the memory bandwidth and cuda cores of a rtx6000 pro. 
  - comfyUI would need to be able to run on arm CPU. All Mac users have ARM CPU 

- ## 🧮🤔 [NVIDIA says DGX Spark releasing in July : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kq4ey4/nvidia_says_dgx_spark_releasing_in_july/)
- Let's do some quick napkin math on the expected tokens per second:
  - If you're lucky you might get 80% out of 273 GB/s in practice, so 218 GB/s.
  - Qwen 3 32B Q6_K is 27 GB.
  - A low-context "tell me a joke" will thus give you about 8 t/s.
  - When running with 32K context there's 8 GB KV cache + 4 GB compute buffer on top: 39 GB, so still 5.5 t/s. If you have a larger.
  - If you run a larger (72B) model with long context to fill all the RAM then it drops to 1.8 t/s.
- Yes, these architectures aren't the best for dense models, but they can be quite useful for MoE. Qwen 3 30B A3B should probably yield 40+ t/s. Now we just need a bit more RAM to fit DeepSeek R1.

- Is that how you can calculate the maximum speed? Just bandwidth / model size => tokens / second? I guess it makes sense, I've just never thought about it that way. I didn't realize you would need to transfer the entire model size constantly.
  - You don't transfer the model, but for every token generated it needs to go through the whole model, which is why it is bandwidth limited for single user local inference.
  - As for bandwidth, it's a MT/s multiplied by the bus width. Normally in desktop systems one channel = 64bit so dual channel is 128bit etc. Spark uses 8 of DDR5X chips of which each is connected with 32bits, so 256bit total. The speed is 8533MT/s and that give you the 273GB/s bandwidth. So (256/8)*8533=273056MB/s or 273GB/s.
- > "You don't transfer the model, but for every token generated it needs to go through the whole model"
  - Except when you use models with "sparse" support, apparently. Which is why its a big deal the things have hardware accel for sparse models.

- My MacBook Pro M1 Pro is close to 5yo and it runs qwen3 30B-a3B q4 at 45-47t/s on commands with context. It might drop to 37t/s with long context.
  - when you run a smaller quant like Q4 of the 30B A3B model you might get close to 60 t/s in your not-long-context case.

- Running the same Qwen model with a 32k context size, I can get 13+ tokens a second on my M4 Max.
  - With just 32k context size set, or also mostly filled with text? Anyway, 13 tps * 39 GB gives us about 500 GB/s. The M4 Max has 546GB/s memory bandwidth, so this sounds about right, even though it's a bit higher than expected.

- thank you. those numbers look terrible. I have a 3090, I can easily get 29 t/s for the models you mentioned.
  - I don't think you can fit a 27 GB model file fully into 24 GB VRAM. I think you could fit about Q4_K_M version of Qwen 3 32B (20 GB file) with maybe 8K context into 3090, but it would be really close. So comparison would be more like Q4 quant and 8K context at 30 t/s with risk of slowdown/out of memory vs. Q6 quant and 32K context at 5 t/s and not being near capacity.

- But 128GB of memory will be amazing for ComfyUI. Operating on 12GB is impossible, you can generate a random image, but you can't then take the character created and iterate on it in any way or use it again in another scene without getting an OOM error. At least not within the same workflow. For those of us who don't want an Apple for our desktops this is going to bring a whole new range of desktops we can use alternatively. They are starting at $3k from partnered manufactures and might down to the same price as a good desktop at $1-2k in just another year.
  - You're probably better off with an RTX 4090 (and a full desktop PC to support it, so it is going to be more expensive) for image generation, as the Spark is going to be slower than a gpu. It can run far bigger models, yes. But 128GB is too much for just image generation while the speed will suffer due the limited bandwith. A sweetspot would be half the memory at twice the speed, but that doesn't quite exist, at least in that price range. A modded RTX 4090 with 48GB of ram (and the accompanying desktop) is going to perform better - although the entire thing would probably cost more than twice as much. BUT, if you already have a desktop, upgrading your gpu will give you better bang per buck.
- It likely depends on how big your workflows are. Your right in that if I don't run out of memory on my gaming graphics card, image generation is super fast, but if I do run out of memory all the speed in the world is not going to help me finish my workflow. Also the speed is not as important for developing, since your the only user. I can let this little guy do the work while I game on my gaming card and the power draw is so low it can share the same circuit.
  - This is similar to my thoughts. You have CUDA-capable running in the background and reasonably low wattage. Just throw some stuff at it and come back later to see the results. It won't bog down your main system and hopefully it won't waste too much electricity (maxing at 170 watts? Each, since you could have multiple linked). Having an always available local LLM is also just nice. MSTY or similar can make it available to your whole home network rather easily.

- So, basically like a 128 GB strix halo but almost triple the price. Yawn.
  - But it has CUDA man. CUDA!!!!!

- Just a note that DGX Spark is listed as $3999 on their page currently. There are some licensed competitors that have cheaper machines available but they all sacrifice something to get there.

- You can get an Apple Studio M4 128 GB for a little less than DGX Spark. The Apple device will have slower prompt processing but more memory bandwidth and thus faster token generation. So there is a choice to make there.

- ## [Comparing AI Performance of DGX Spark to Jetson Thor - DGX Spark / GB10 User Forum / DGX Spark / GB10 - NVIDIA Developer Forums _202508](https://forums.developer.nvidia.com/t/comparing-ai-performance-of-dgx-spark-to-jetson-thor/343159)
  - Jetson Thor: “NVIDIA® Jetson Thor™ series modules give you the ultimate platform for physical AI and robotics, delivering up to 2070 FP4 TFLOPS of AI compute and 128 GB of memory with power configurable between 40 W and 130 W.”
  - DGX Spark: “Powered by the NVIDIA GB10 Grace Blackwell Superchip, NVIDIA DGX™Spark delivers 1 petaFLOP of AI performance in a power-efficient, compact form factor.”
  - Is this a case of marketing terminology conflation, or might the Jetson AGX Thor provide better local inference performance compared to DGX Spark?

- The NVIDIA Jetson Thor Developer Kit is a purpose-built developer platform targeted at developers creating robotics and physical AI solutions that deploy with embedded Jetson modules. 
  - DGX Spark is a purpose-build compute to build and run AI, targeted at AI developers and data scientists who need to augment current laptop, desktop, cloud, or data center resources to provide large local memory and access to the NVIDIA AI software stack for their AI prototyping, fine-tuning, inference, data science, and general edge workloads.

- The RAM being similar but performance different could be down to scaling with power draw. The DGX Spark ships with a 240w USB-C brick, and I think it’s specced to draw significantly higher than the Thor at 170W.

- The DGX Spark has 6144 CUDA cores, or just as many as RTX 5070. I believe I saw numbers claiming 1000 TOPS in FP4 sparse mode. I’m not sure how many tensor cores, or what type of tensor cores even, if any?
  - The AGX Thor has 2560 CUDA cores, with 96 fifth-generation Tensor cores; benchmarks I’ve seen so far indicate it performs on LLMs about as fast as an RTX 5070. I’m unsure if these were tests used in FP4 Sparse mode, as NVIDIA rates it for 2070 TOPS in FP4 sparse mode
  - I suppose I can see the Spark using more power due to using CUDA cores instead of Tensor Cores as the main source of processing, offering FP32 performance needed for precision during training and perhaps greatly versatility

- Some other differences that are noteworthy
  - DGX Spark has one NVENC/ NVDEC chip. Thor has Two.
  - DGX Spark has a connect-x nic. Thor is not connect-x but a 4x25g nic. It doesn’t appear to support RDMA among other features you get with connect-x. which also means you probably can’t combine the thor modules very easily.

- ## [AGX Thor LLM Inference Performance & Implications for DGX Spark? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n0rheb/agx_thor_llm_inference_performance_implications/)
  - Excited to see the initial benchmarks rolling in for the AGX Thor following yesterday's release. A recent YouTube video showed around 30 tokens/sec generation speed with gpt-oss-120b using llama.cpp
  - This got me thinking about the DGX Spark. NVIDIA advertises the AGX Thor as having 2 PFLOPS of FP4 performance, while the DGX Spark is listed at 1 PFLOP

- Why would LLM inference scale with available FLOPs? 
  - Most of the operations used are dot produces (particularly matrix-matrix products) which are memory bound operations fundamentally; the number of FLOPs don't matter (within reason). Even a 4 core CPU with sufficient bandwidth can still run an LLM like GPT OSS
  - Where the FLOPs might matter is prefill (long context operation) or for concurrent inference serving, like maybe if you were doing async agents or something in parallel. These operations are compute bound, and FLOPs do matter (though in the case of prefill, with KV caching it doesn't matter for iterative workflows like chatting or iterative coding, and you're memory bandwidth bound again).

- I think one of the biggest drawbacks of the Spark (and something that is holding back many current offerings for AI and Handheld gaming) is the memory bandwidth
  - The one benefit that Spark might bring is NVIDIA MIG, which would allow us to partition GB10 into several instances and maybe run several models in parallel. Might be interesting for exploring LM Agents, especially if you got several of them working at the same time.

- I think there are two versions of the future: MXFP4 - will become the standard. MXFP4 - will not become the standard. 
  - In the first case, DGX Spark and Blackwell will make other solutions garbage. In the second case, DGX Spark will be garbage.

- ## [Nvidia DGX Spark | Hacker News _202508](https://news.ycombinator.com/item?id=45008434)

```markdown
<!-- FP4-sparse -->
| GPU Model | FP4-sparse (TFLOPS) | Price ($) | $/TF4s |
|-----------|---------------------|-----------|--------|
| 5090      | 3352                | 1999      | 0.60   |
| Thor      | 2070                | 3499      | 1.69   |
| Spark     | 1000                | 3999      | 4.00   |

<!-- FP8-dense -->
| Model        | FP8-dense (TFLOPS) | Price | $/TF8d (4090s have no FP4) |
|--------------|---------------------|-------|----------------------------|
| 4090         | 661                 | 1599  | 2.42                      |
| 4090 Laptop  | 343                 | vary  | -                         |

<!-- Geekbench -->
| Model      | Geekbench 6 (compute score) | Price | $/100k |
|------------|-----------------------------|-------|--------|
| 4090       | 317800                      | 1599  | 503    |
| 5090       | 387800                      | 1999  | 516    |
| M4 Max     | 180700                      | 1999  | 1106   |
| M3 Ultra   | 259700                      | 3999  | 1540   |

```

- Memory is the bottleneck. It limits the size of the models you can run and what you pay for.
  - Spark: 200B 
  - 5090 : 12B (raw)

- spark is $3, 999 and current M3 Max 28-Core CPU 60-Core GPU is the same price.

- I run 4 Mac Studio ultras at work (they’re pricy when maxed out), for local-first AI dev services. But there’s a few things that make me want to switch to the Spark. 
  - Networking is the biggest one, the Macs have Thunderbolt and Ethernet, but if I run distributed inference with EXO over Thunderbolt; the drop in tokens/second is massive. These Sparks get RDMA and can stack nicely. 
  - The other big one is access to CUDA, MLX has come a long way but being able to have CUDA and GPU access in containers would simplify the stack so nicely. 
  - If I had a USB-C/Thunderbolt backplane it might compare, but scaling with the Spark is likely a lot more straightforward.

- Biggest problem with Macs is that they don't have dedicated tensor cores in the GPU which makes prompt processing very slow compared to Nvidia and AMD.
  - there's been a little speculation that Apple adding TensorOps to Metal 4 suggests M5/M6 may get tensor cores.

- If that would be true why aren't Mac sales banned in China instead of Nvidia GPUs?
  - Because it's only a superior solution if you just want one box, and that mostly for inference. Once you start scaling to larger loads, it's much trickier to get a clusters of Macs to efficiently process them in parallel, whereas datacenter GPUs are designed for clusters.

- ## [What is the estimated token/sec for Nvidia DGX Spark : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1krsast/what_is_the_estimated_tokensec_for_nvidia_dgx/)
- generation rate (tokens / s) are almost always bound by memory bandwidth not compute. 
  - It will be bound by the LPDDR5x memory to 273 GB/s.
  - Of course the compute will help with prompt processing and batching multiple queries, and the huge RAM will allow you to (slowly) run big models

- Slightly more than Strix Halo, due to better GPU/drivers, but nothing major.

- Ohhh.. now i see why they are willing to sell this high memory product to the general public. This is straight up trash tier performance. Fast enough that it will be bought and used by AI developers and enthusiasts... but slow enough as to not be hoarded and abused by cloud providers.

- Strix Halo devices are all at $2000 and are now widely shipping from many manufacturers. These are RDNA3.5 devices and while WIP, have full PyTorch support.

- ## [Nvidia digits specs released and renamed to DGX Spark : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jedy17/nvidia_digits_specs_released_and_renamed_to_dgx/)
- Framework Desktop is 256GB/s for $2000… much cheaper for running 70gb - 200 gb models than a Spark.
  - Yup, and being X86 is much more usable. These small AMD APUs are quite nice for a console/multi-media box purposes when not using LLMs. 
  - Nvidia offering is ARM so Linux only and not even X86 Linux so pretty much no gaming will be possible.

- ## [Local inference with Snapdragon X Elite : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1l5k290/local_inference_with_snapdragon_x_elite/)
- I've been using mine (Surface Laptop 7) since it came out. It's good, but not in the exact way marketed.
  - I use it with LM Studio and AnythingLLM running models up to about 21B, the model size is limited by my 32GB integrated RAM. The token rate on an 8B is like 17-20 per second. 
  - But the NPU doesn't seem to have to do with anything. All the inference is on CPU, but not in that bad way people complain about if they have Intel products, more in the good way people talk about if they have Macs.

- I've been using local inference on multiple Snapdragon X Elite and X Plus laptops.
  - In a nutshell, llama.cpp or Ollama or LM Studio for general LLM inference, using ARM accelerated CPU instructions or OpenCL on the Adreno GPU. CPU is faster but uses a ton of power and puts out plenty of heat; the GPU is about 25% slower but uses less than half the power, so that's my usual choice.
  - I can run everything from small 4B and 8B Gemma and Qwen models to 49B Nemotron, as long as it fits completely into unified RAM. 64 GB RAM is the max for this platform.

- NPU support for LLMs is here, at least by Microsoft. 
  - You can download AI Toolkit under Visual Studio Code or Foundry Local. 
  - Both of them allow running of ONNX-format models on the NPU. 
  - Phi-4-mini-reasoning, deepseek-r1-distill-qwen-7b-qnn-npu and deepseek-r1-distill-qwen-14b-qnn-npu are available for now.
- Microsoft has AI Foundry which uses the Hexagon NPU. You're limited to Phi models and DeepSeek Distill Qwen models. Performance is fine but the models are old.
- Microsoft just added Qwen 7B and 14B DeepSeek Distill models that run on NPUs. I think for the moment, only the Snapdragon X Hexagon NPU is supported using the QNN framework. These are ONNX models that require Microsoft's AI Toolkit to run. 

- the X elite, would maybe use the gpu for the transformers i dont know if it would be possible for the llm since im using llama cpp
  - I don't think it's possible. A lot of Python ML-related frameworks don't have ARM64 Windows wheels or they can't be compiled without getting into a dependency nightmare. They won't work under WSL Linux because there's no Vulkan or OpenCL GPU passthrough.
  - If you want to use the Adreno GPU for inference, you're stuck with llama.cpp, LM Studio or Ollama, which all use the same ggml backend code.

- [Snapdragon X CPU inference is fast! (Q\_4\_0\_4\_8 quantization) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1emd3bg/snapdragon_x_cpu_inference_is_fast_q_4_0_4_8/)
  - On a Surface Pro 11 with a Snapdragon X Plus 10-core chip, running CPU inference for Llama 3.1 8B, I'm getting the following:
  - llama_print_timings: prompt eval time = 895.37 ms / 126 tokens ( 7.11 ms per token, 140.72 tokens per second)
  - llama_print_timings: eval time = 90360.33 ms / 1391 runs ( 64.96 ms per token, 15.39 tokens per second)
- I get ~5.5 tokens/s with Llama 3.1 8B Q8_0 and DDR4-3600 memory, so ~15.5 tokens/s for Q4 and dual-channel LPDDR5X-8400 memory doesn't seem that impressive.
- Well it's not close to m2 levels at all. M2 max gets 66 t/s and 671 pp/s at q4
- Wow, I have ~5.8 tokens/s on 8+gen1 in llama 3.1 8b

- ## [Snapdragon X Elite - local llm? : r/LocalLLaMA _202406](https://www.reddit.com/r/LocalLLaMA/comments/1ddyc51/snapdragon_x_elite_local_llm/)
- I have purchased the new Surface Pro CoPilot+PC and am struggling to get the LLMs to run using the embedded NPU. I guess I was spoiled by using Ollama and Llama.cpp, now I am having to learn the basics of quantizing a model and using HuggingFace APIs to host the models.

- Should be good for 13B. There is a video out there showing it’s real world performance already on a model called “Phi Silica”

- [Snapdragon X Elite llama.cpp ? : r/LocalLLaMA _202406](https://www.reddit.com/r/LocalLLaMA/comments/1dj6h6x/snapdragon_x_elite_llamacpp/)

- [$899 mini PC puts Snapdragon X Elite into a mini desktop for developers (with 32GB RAM) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1cxhh1q/899_mini_pc_puts_snapdragon_x_elite_into_a_mini/)
  - every modern CPU since AMD phenom is a SoC with unified memory architecture. The key thing is the memory controller and how many steps it needs. CPUs benefit from being able to quickly go back and forth between ram compared to GPUs, which is why RAM performance isnt a direct competitor to VRAM in GB/s because the MT/s is more important for RAM and how efficiently your data and instructions are packed into every transfer.
  - Thanks for correcting that AMD and other competitors have had UMA for years. My mistake. But still stands that apple has 800GB/s memory bandwidth vs things like Snapdragon X Elite’s 136GB/s

- ## [骁龙X Elite再遭痛殴, 第二代酷睿Ultra 英特尔Meteor Lake有多强？ - 知乎 _202406](https://zhuanlan.zhihu.com/p/701851374)
- 第一代酷睿Ultra平台（流星湖，Meteor Lake）的四大模块中，除了计算模块采用了自家的Intel 4工艺，其他三个模块都是台积电代工。
  - 到了【月亮湖】，就连最核心的计算模块也改用了台积电的N3B工艺，英特尔仅保留了自己的先进封装工艺（Foveros）。
  - 在【月亮湖】上，英特尔还带来了类似苹果统一内存架构的设计，直接将LPDDR5X-8533内存封装在了芯片之上，可选16GB或32GB容量。
  - 这种设计的好处是，能使数据传输负载降低大约40%，延迟更低，相较传统的板载内存还能节省大约250平方毫米的主板空间
- 【月亮湖】的核心竞争力，就是计算模块中的CPU、GPU和NPU三大单元都迎来了全面提升。
  - 首先就是NPU，从第一代酷睿Ultra的11TOPS，大涨到48TOPS
  - 【月亮湖】CPU部分的AI算力为5TOPS，GPU为67TOPS，在异构计算的加持下，整体AI算力高达120TOPS，一举超越了骁龙X Elite的整体75TOPS（NPU为45TOPS），和锐龙AI 300的整体80TOPS（NPU为50TOPS）。
  - AI PC时代之所以格外强调AI算力，就是因为微软即将在Windows操作系统层面，就把生成式AI技术应用到基础体验之中。如果使用CPU和GPU进行处理，笔记本的续航会尿崩。此时，唯有低功耗高AI性能的NPU，才能在兼顾续航的同时，随时随地享受AI带来的便利
  - 在GPU方面，【月亮湖】升级到了新一代的Xe2架构，性能有了平均50%的提升，有机会与AMD锐龙AI 9 HX 370集成的Radeon 890M掰掰手腕

- ## 🆚🌰 [AMD AI Max+ 395 CPU 本地大模型推理性能评测报告 - 知乎 _202509](https://zhuanlan.zhihu.com/p/1952045270763283746)
- 针对搭载AMD AI Max+ 395 CPU的零刻GTR9迷你主机进行了一系列严格的大模型推理速度测试。
  - 硬件平台: 零刻 (MINISFORUM) GTR9 迷你主机
  - 核心组件: AMD AI Max+ 395 CPU
  - 任务类型: 本地大语言模型推理
  - 性能指标: Tokens/s (每秒生成Token数) — 该数值越高，代表推理速度越快
- 设计了涵盖多种任务类型的标准化问题：
  - 综合能力: "你是谁？请详细介绍一下你能干什么。"
  - 知识问答: "作为专业人工智能专家，请告诉我如何学习深度学习？"
  - 数学计算: "如果A+B=12, A-B=10，则A的值是？"
  - 自然语言理解: "识别句子‘我将会在明天早上的8点到湖北黄陂的森林公园’中的所有地名。"
  - 代码生成: "请使用Python编写一个贪吃蛇游戏。"

- 参评大模型:
  - deepseek-r1:70b, 30
  - qwen3 系列（32b / 30b / 14b / 8b）
  - gpt-oss（120b / 20b）

```markdown
| Model          | Ollama | LM Studio |
|----------------|--------|-----------|
| deepseek-r1:70b | 4.43  | 4.97      |
| qwen3:32b      | 8.97   | 10.12     |
| qwen3:14b      | 19.47  | 21.70     |
| qwen3:8b       | 29.93  | 35.96     |
| gpt-oss:120b   | 30.84  | 42.07     |
| gpt-oss:20b    | 42.57  | 60.54     |
| qwen3:30b      | 48.93  | 68.70     |
```

- 对比两组数据可见，同一模型在LM-Studio中的推理速度普遍优于Ollama
- AMD AI Max+ 395 CPU采用CPU/GPU共享内存的统一内存架构（UMA），这种设计天然适合运行混合专家（MoE）模型（如gpt-oss系列、qwen3:30b）。
  - MoE模型虽然总参数量庞大，但每次推理仅激活部分"专家"参数，非常契合这种大容量内存但绝对算力相对有限的硬件。
  - 相比之下，对于参数密集的传统稠密模型（如deepseek-r1:70b、qwen3:32b），由于需要更高的绝对算力，该处理器的集成显卡则稍显吃力。

- DFRobot作为在单板计算机（SBC）、AI边缘计算和开源硬件领域的创新者，此次测试结果意义非凡。若未来DFRobot推出基于AMD AI Max+ 395 CPU的单板计算机，将其强大的本地AI推理能力与DFRobot成熟的模块化传感器生态（如Gravity系列）相结合，将催生出更多实时、智能的物联网与机器人应用

- ## 🆚 [AI max+ 395 128gb vs 5090 for beginner with ~$2k budget? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nunlls/ai_max_395_128gb_vs_5090_for_beginner_with_2k/)
- ComfyUI? 5090.  LLMs? AI Max
  - FWIW, you can also use a thunderbolt eGPU with the AI Max.

- I've been able to run ComfyUI on max+ 395. It's a pain, but it's possible.

- As for ComfyUI, I run that just fine on my Max+ 395 as well. But saying ComfyUI doesn't mean much. It's just a framework to run things. What exactly do you want to do? If it's just image gen, then the Max+ is as good as anything else. If it's video gen, it does work but uses way more memory than Nvidia. If it's voice cloning, that just works too. So other than using way so much memory, which you have plenty of on a Max+ 128GB, what is this bugginess you are talking about?
  - Max+ 395 owner, and I agree, the level of experimenting i've reached has been great with the device.
- I love my 395+ 128 GB, and I've got LLM, image generation, voice, etc. working, but I cannot for the life of me get video working. Mainly trying to experiment with I2V with WAN 2.1 and 2.2, but have never got a successful run. Either get OOM or seemingly infinite time per iteration. Not sure if you can provide any tips. Using the pytorch 2.9.0+rocm7 RC since that was the most stable for everything else.

- I’d personally go 395, because almost all AI labs are going with MoE architecture at this point. So big RAM can accomplish a lot even if it’s not the fastest.

- The AI Max+ 395 handles all my AI needs for now and it’s pretty snappy once you get things working in Linux.
  - The downside is if you need/want to run anything super fast - you will need a different setup. Eventually I might get a setup like that, and use the Max+ 395 for my mobile AI needs.
  - Still, I can get 20+ TPS on GLM Air 4.5, and even faster with the GPT-OSS models.

- How much memory ddr5 with 5090? Just 32gb is limited 128gb can run huge Moe's.
  - If your running 30b models and under 5090 all day. 
  - If your running large 120b moe models or smaller dense models 395plus all day.

- if you want to do some training stuff, CUDA, and ... maybe gaming, go for the 5090
  - if you just want to run some local model to try them or serve them locally 24/7, strix halo is probably a better option, almost all the best latest open model are MoE and they need a lot of ram/vram (glm 4.5 air, gpt oss 120b, some qwant of qwen 235, qwen 3 next, ... will all run better on strix halo vs 5090+128gb ram). Also strix halo is usually a full machine, while the 5090 you still need the rest of the PC

- AMD AI 395 miniPC preferably with Oculink (there are couple) where you can hook later external dGPU like AMD AI PRO R9700.

- If you're interested in image/video gen, you need the 5090. That is going to be miserably slow on CPU.
  - If you just want to run MoE models interactively, the AI 395 will be enough.
  - Personally? I'd go with both. You can in fact attach a 5090 to an AI 395 system. Then you can run LLMs for your prompt generation/improvement workflows while generating video and imagery to your heart's content.
  - I don't think people who have not experienced a Blackwell GPU understand how much faster they are for image/video work. Even against a 4090 my workflow times cut in half.
- I agree, I think I start with 395 and add the 5090 if it becomes necessary.

- if it was only to play around and learn llm stuff i'd lean towards the framework 128.
  - but the moment you mention comfy, amd is off the table. get the 5090 instead.

- If you're looking mostly to be able to inference bigger MoE models with llama.cpp then I think the 395 can be a good choice.
  - However, if you have an interest in playing round w/ image/video generation, doing any further poking around (vLLM/SGLang, voice, PyTorch, model training/fine tuning, etc) then I think the 5090 is the clear way to go.
  - If you're working w/ smaller models btw it's not just about stability either, the 5090 is a whole different animal in performance - as long as you're OK w/ running ~30B/smaller models.

- ## [Advice: 2× RTX 5090 vs RTX Pro 5000 (48GB) for RAG + local LLM + AI development : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1nsyiag/advice_2_rtx_5090_vs_rtx_pro_5000_48gb_for_rag/)
- As someone with 2x 5090s, started from 1.. don't do it. Go straight to the pro 6000. Thank me later. It'll save you time, money, and effort. :) I now have a pro 6000. You can pick one up from Exxact for $7200.
  - Dual 5090s are great… you can run many models. 
  - However, even with quantized KV cache it’ll crash often. You can’t max out the 1million context Qwen coder. You can’t really fine tune models that don’t fit in a single GPU. You’ll have issues with accelerate. 
  - Heat is very hot. At least 10 degrees warmer in a whole room when fine tuning. Power usage is very high. You’ll need to run new electrical or have your machine shut off when someone plugs in a vacuum. You’ll need to run dual psus or buy a 2000w+ psu. 
  - Case options are very limited. The cards are massive in size. You’ll need 8 slot pc cases minimum for 2 cards. 
  - You’ll want to run 70b+ models guaranteed. Even Qwen next 80b. 2x 5090s isn’t enough. 
  - This is all solved with a single pro 6000. So for an extra $1000 you can save yourself a lot of headaches and get access to nvidia enterprise

- Rent GPUs online unless you have a reason other than inference

- Remember the most important thing: whatever you choose initially, you will have to switch to RTX 6000 PRO 96Gb on Epic or Threadripper platrofm eventually if you want to continue running large local llms efficiently. The cost of those things will dwarf your current current setup. So, do not sweat much while deciding on the current config. Just make sure that your case and motherboard allow to connect at least 2 GPUs via riser cards with PCI 5.0 on each, even if at x8 speed. 

- Be sure you get a motherboard with dual x8 pcie slots if you go with two GPUs. Most AM5 boards don’t support that but a handful do. Just wanted to give you a heads up
  - Yeps, Asus Pro Art 2x pice 5.0

- ## [The NVIDIA DGX Spark at $4, 299 can run 200B parameter models locally - This is our PC/Internet/Mobile moment all over again : r/LlamaFarm _202509](https://www.reddit.com/r/LlamaFarm/comments/1nee9fq/the_nvidia_dgx_spark_at_4299_can_run_200b/)
- DGX has 273gb/s versus 1.7Tb/s for a rtx 5090...
  - The bandwidth is terrible. You'll run your models at 5 tps
  - I literally don't see who's gonna buy this aside from people who just got blinded by the unified RAM...
- At 273 GB/s memory bandwidth this unified RAM there will make inference VERY SLOW... For comparison: RTX 4090 has 1008 GB/s and RTX 5090 has 1792 GB/s memory bandwidth

- u can easily get an m1 max with 128 gb of unified memory for 1k cheaper than that and double the memory bandwidth. Don’t see how this is a good deal.
  - It's not a good deal. It is more of a sign. MLX is growing, but the ecosystem is still tiny compared to CUDA. With Blackwells coming to PCs and AMD shipping powerful GPUs, there will be real competition in this area for the first time.

- M3 Ultra with 256GB RAM does cost roughly $1000 more, but has 256GB unified memory
  - And 819 gb/s vs Spark's 273.

- Mac Studio, Ultra series, either M1 or M2 with 96GB or 128GB RAM. And more recently, the M4 Max. I bet by next year the Mini will likely have a 128GB configuration too.
  - What I am NOT saying is that Apple’s offerings are the best local inference for 128GB workloads. I am saying they are relatively cheap and capable, and the inflection point for fairly large local models (>60GB) was two years ago.
  - I bought my M4 Max 128GB last year for local models. It does not disappoint.

- No thanks, I'm not taking my wallet out until I see the AMD Medusa Halo 128GB AI mini-PCs in two years. I CAN WAIT.

- Jetson AGX Thor claims 2000 TOPS of AI at FP4, but it is the same memory bandwidth as DGX spark so I have my doubts. Guess we have to wait for some benchmarks.

- [DGX spark vs MAC studio vs Server (Advice Needed: First Server for a 3D Vision AI Startup (\~$15k-$22k Budget) : r/deeplearning](https://www.reddit.com/r/deeplearning/comments/1lylfuw/dgx_spark_vs_mac_studio_vs_server_advice_needed/)
- Macs are decent for inference, but nobody "real" is training models on Mac. Even Apple was using TPUs earlier (when that team was still run by the ex-Google guy) and grapevine says they're on Nvidia now

- DGX Spark is like a RTX 5060(70?) class GPU with 128GB of slowish (for GPU) memory.
  - The only thing Spark really has going for it is it might be SM100 (real Blackwell with Tensor Memory) instead of SM120 (basically Ada++) which may be useful for developing SM100 CUDA kernels without needing a B200.
  - Much better off I think with a NVIDIA RTX PRO 6000 Blackwell Series (96GB) for most people, or 512GB Mac Studio if you need very large LLMs but less GPU perf.

- ## 🍎 [MacBook M4 Max isn't great for LLMs : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jn5uto/macbook_m4_max_isnt_great_for_llms/)
- M4 Max is about 50% faster than an Nvidia P40 (both in compute throughput and memory bandwidth). 
  - It is about 2.5x slower than a 3060 in compute¹ throughput (FP16) and 50% faster in memory bandwidth. 
  - Compared to 3090, it is about 7x slower in compute¹ throughput (FP16) and almost 2x slower in memory bandwidth.
- P40s (and generally Pascal) were the last ones without tensor cores (which increase FP16 throughout by 4x).
  - The lack of tensor cores is also the reason Apple M3 Ultra/M4 Max and AMD 395 Max, lag in Prompt Processing throughput compared to Nvidia, even if the M3 Ultra almost matches a 3080/4070 in raster throughput (FP32).
  - Compared to CPU-only inference, P40s are still great value, since they cost $150-300 and are only matched by dual 96-core Epycs with 8-12 channel DDR5 which start from $5000 used.
- Pascal doesn't even have FP16 support, all the operations are done through fp32 units afaik so throughput is effectively halved. It wasn't until Ampere that NVidia had FP16 support.

- Try swapping to serving with LMStudio - then use MLX, and speculative decoding with 0.5b as draft for 14b! Tripled my speed on my M1 Max
  - Speculative decoding really is great. It at least doubled my speeds. In token generation. Prompt processing didn't get and bump though. I'd love to have a 128gb+ RAM machine to also activate KV Cache

- ## [本地部署大模型性价比之王真的是Apple Mac Studio M3 Ultra 192或512吗？ - 知乎 _202503](https://www.zhihu.com/question/14548406514)
- deepseek r1 用mac studio测试
  - ollama: 16 tops
  - lmstudio: 18 tops
  - 512Gb内存还是只能部署4bit量化版本，8bit不行
- 如果按照18.11token/s的输出速度，不考虑其他，全天24小时运行（不考虑prefill等时间）18.11×86400s=156.5万tokens，而官网百万tokens售价才16块，156.5万售价25块钱
  - 而Mac studio 512G内存，1t硬盘版本售价7.3w教育优惠也要6.7w，需要365×24h不停运行8年/7.3年才能回本

- 那要看你怎么定义性价比了，[ktransformers] + [epyc] 现在也已经玩得很强了，苹果胜在上手就能用不用折腾装，在那个价位算一个可行方案，但并非算唯一性价比方案

- ## [MAC mini M4芯片32G+256能跑大模型吗？ - 知乎 _202503](https://www.zhihu.com/question/14795834393)
- 真跑ai只推荐Pro以上的芯片。
  - m4的内存带宽其实和普通核显win机子差不多。而到了Pro，内存带宽就达到256了，达到4060的水准。
  - max和ultra带宽分别是400＋和800＋，基本是显卡级别的带宽，用来跑ai推理很合适。

- 主要是内存大啊，我用一万出头的mac能跑27B的gemma3 8bit量化，如果用显卡的话至少得是个3090级别的

- Mac Mini 当副机可以，统一内存看着香，但很多模型不支持 MPS，或者用 MPS 跑得比 CPU 还慢。

- ## [Apple M5 could ditch unified memory architecture for split CPU and GPU designs | Hacker News _202412](https://news.ycombinator.com/item?id=42552494)
- UMA hurts the GPU too much. Widely parallel processing wants to access memory in bigger chunks than a CPU. If you try to mix access and modification, you lose the benefit of widely parallel processing. 
  - Other GPU designers have considered and eschewed unified memory models, to the tune of hundreds of millions in research dollars.
- I agree that single cache-line fetches are pretty poor for parallel vector units, but supporting the former in an environment designed for the latter doesn't seem to off-putting (the CM-5 did this).

- You can split the CPU and GPU and still have UMA. Splitting CPU/GPU is a packaging and interconnect concern and is not mutually exclusive with UMA.

- ## [求推荐！想组一台256G➕笔记本跑大模型🥹 - 小红书](https://www.xiaohongshu.com/explore/6892017700000000030274de?xsec_token=ABHUpmj6nmLewRxGBOYsEYt2FVRxDHjqOHSnhQfgUJJnc=&xsec_source=pc_search&source=web_explore_feed)
- 普通笔记本不支持256，别异想天开
  - 笔记本内存有是有，但是笔记本不支持，买了也没用，到时候插上去不识别就老实了
- 别想了，笔记本不支持ecc内存，跑时间长容易出错
- 哪个苹果笔记本有512内存 你找出来我看看，我就知道推出过2t内存的mac pro还有512内存的mac studio，mbp最大的就128g内存吧 m4max

- 散热压不住的

- 笔记本目前能本地部署大模型的只有m系芯片的mbp内存拉满（仍然是勉强够用水平）和ryzen ai max+395板载内存拉满128（这个的内存和效率估计不太够，唯一优势x86日常方便），因此主要往itx上面去凑，现有产品也就是我说的这两套即苹果m系和amd ai，因为有统一内存可以用核显来跑ai免去多路gpu的麻烦。

- 如果你需要cpu高性能，那么可以考虑用比较新的服务器平台（因为我估计连hedt都无法满足你的内存需求）和itx主板（当然，华擎不一定还在做这类奇特的产品）。你只需求单卡的话可以勉强塞一套itx，但是各方面都很极限了，包括供电和散热，大概是跑不满的。如果你需求多卡的话，可能得几张卡用扩展卡连接以分着用itx主板仅有的那一两个pcie x16接口，这样做性能肯定会有折损，并且100%需要做分体的两个itx机箱，这种情况你需要自己画设计图去tb之类的平台找工厂定做板材，好处是供电和散热没之前那么极限，坏处是这一套下来估计不比eatx机箱轻便多少。

- ## [选个能本地跑70B大模型的笔记本当主力机试 - 小红书](https://www.xiaohongshu.com/explore/6811b115000000002301de1a?xsec_token=ABZEBEajWMF79jFUPp-RsmTEccFriosXMc79IFdgiGHWo=&xsec_source=pc_search&source=web_explore_feed)
  - 之前一直用灵刃16 2024版的当主力机，跑起来风扇实在是响，开个线上会别人都听不清，而且重量实在无法移动。
  - 最近看到HP 战99 Ultra到货就直接拿下了 128G。用了一天，感觉AMD AI395+跟之前i9-14900hx性能差别不大 不过噪音好了很多，集显8060s的性能虽然不如之前4070，但是跑个本地小模型也没什么压力。
  - 重量上1.6KG稍微重了一点点，跟X1C没法比，跟macbook pro 14差不多，比灵刃强太多了。
  - 触屏的

- pd充电能有原厂充电器几成的性能？
  - 原厂130w的，65w的PD会提示慢速充电器，只有一半不到的速度

- 本地70B速度怎么样？
  - 有个20-30 token/s 凑合用
- 我qwrn32量化8也才5个token，你这个70b 20-30token是怎么来的
  - 70量化4可以的，量化8肯定不行

- ## 🆚 [关于几个桌面级的AI统一内存集成方案的对比 - 知乎 _202503](https://zhuanlan.zhihu.com/p/31599083340)
- 目前桌面级别的AI方案，除了nv的独显外，还有几个统一内存的集成方案
  - 苹果Mac mini和Mac studio
  - AMD AI 395 MAX
  - 英伟达 DGX Spark

- 带宽 ：(❓推理/部署时重要)
  - m4pro 64G 和nv dgx spark 128G都是 273 GB/s
  - amd AI 395 max+128G 是            256 GB/s
  - m3ultra 96G是                     400 GB/s (m3u无128G，256G以上才有800GB/s)
  - m4max 128G 是                     546 GB/s

- AI算力：(❓训练时重要)
  - nv dgx spark是  1000 TOPS (FP4)
  - amd AI395max是  126 TOPS（int4）
  - m3ultra是       72 TOPS(int4)
  - m4max和m4pro都是 38 TOPS(int4)

- 价格：
  - nv dgx spark  3000 美元（估计23000人民币？）
  - amd ai395max  25999 人民币
  - m3ultra 96G   32999 人民币
  - m4max 128G    29249 人民币
  - m4pro 64G+1T  16999 人民币

- 综合看来如果性价比和通用性比较好的选择应该是nv DGX Spark（生图，生视频之类的算力比带宽更重要），
  - 如果单纯为了LLM性能（统一内存带宽比算力更重要）m3ultra 96G 可能是比较好的选择。
- 至于之前有看到的一些用mac mini通过雷电口堆叠的虽然可以低成本做到大显存，但是几乎没啥实用价值，因为雷电口带宽只有15GB/s。。。
  - 雷电堆叠是为了低延迟跑tensor parallelism吧，又不是remote访问内存。PCIE带宽也不如内存，但多卡并行还是有效的

- 现在网上ai max 395的小主机已经卖到14000左右了，这样比下来，感觉ai max 395性价比还不错。

- ## [如何评价售价 18999 元的惠普暗影精灵 MAX 游戏本? 哪些亮点值得关注? - 知乎 _202503](https://www.zhihu.com/question/15023061538/answers/updated)
- 暗影精灵MAX这个新模具就用来取代暗影精灵Plus的，依然是主打一个“一线品牌中的性价比”定位。
- 一线品牌高端游戏本的守门员，原来暗影精灵PLUS的替代者。

- 这代Max整体的升级点：
  - 散热规格升级：采用了VC均热板设计，加上液金散热与4出风口设计，整体可以做到250W+的性能释放，双烤75+175W；
  - 屏幕改为更主流的16寸：2.5K分辨率16:10比例高分屏，500nit亮度240Hz刷新率；
  - 新增大师模式，允许用户手动超频。

- 其他配置只能说中规中矩了：
  - 32GB DDR5-5600内存+1TB硬盘，双硬盘位双内存插槽；
  - 只给了2A2C（2个雷电4）+HDMI+RJ45的接口，在游戏本里面算比较少的了；
  - 给了RGB背光键盘，但目前来看还是四区RGB而非单键RGB，并且方向键依旧为半高；
  - 电池容量83Wh，主流旗舰定位的游戏本都90Wh+了，有的甚至99Wh

- 目前惠普精灵遇到一个比较尴尬的问题，比上没有品牌力，比下没有性价比：
  - 加3000可以上逼格更高、更有氛围感、可玩性更高的且品牌更强的ROG枪神9系列；
  - 预算更低，等二线品牌上了之后，大概率1W4不到就可以拿下低U高显的RTX5080游戏本了，性价比更高。
- 国内游戏本市场目前还是以性价比为主导，就连ROG这两年都变得有性价比起来，所以对于暗影精灵MAX这类的不上不下的主流系列旗舰本，我是谨慎看好的，比上无品牌力，比下无性价比。

- 小米G的目标客户是追求性价比的用户，但这帮用户会因为小米G没有性价比不选择小米G……

- ## 🆚📈 [2025买个RTX 5090笔记本，有什么推荐吗？ - 知乎](https://www.zhihu.com/question/1890528801219405195)

> 不太在意便携，主要是看性能+性价比。神舟性价比太高了，但是又有点害怕翻船。

- 在圈定要RTX5090游戏本的前提下，题主的最佳选择肯定是一线品牌高端游戏本一直以来的性价比扛把子，暗影精灵MAX啊
  - U9-275HX+RTX5090+2.5k 240hz 500nit IPS+32/1T PCIe 5.0的核心配置，250w+的整机性能释放表现中等偏上，拓展性一个5.0 M.2一个4.0 M.2，重量2.75kg，接口是俩雷电4，俩USB-A，HDMI和rj45。
  - 上面这个配置也就22999，国补后才20000出头
  - ROG也完全没必要看枪神9 Plus超竞版吧，捆绑了64G内存后价格直接33999了，实在是太夸张。枪神9 超竞版除了内存硬盘都缩小一半以及尺寸为16吋之外，几乎没啥区别，价格则直接下降到了29999，立省4000.

- ## [有没有24g显存的笔记本电脑推荐？ - 知乎 _202409](https://www.zhihu.com/question/666131987)

> 想要买个新电脑来玩AI。主要还是想考虑笔记本，但是看了一圈，好像都是8g显存。最大的也就16g显存。没有找到有24g显存。

- 目前做AI推荐N卡，N卡24G显存只有4090，4090做成便携式只有这一个方法

- 有三个方案：
- 第一个方案是内置显卡的笔记本电脑，优点是便携性好，缺点是性能差点，也得做好散热。
  - 想要16G显存只能RTX4090的型号，绝大部分RTX4080移动端是12G显存，目前使用RTX4090的笔记本电脑不算多，想要性价比就机械革命耀世16Super，想要更强的整机性能释放可以考虑ROG枪神。
- 第二个方案是拓展坞外接桌面显卡，优点是性能强不用考虑散热，并且后期还能随时无痛升级显卡，缺点是丧失了便携性，并且要注意别没断电就拔显卡。
  - 笔记本有雷电3/4或者USB4接口就行，RTX4080会有性能损失，但是能接受，毕竟怎么都比移动端强
- 第三个方案就是放弃繁文缛节，直接上台式机吧。

- ## [纠结选哪款笔记本电脑？主要用于stable diffusion? - 知乎](https://www.zhihu.com/question/620893866)
- 看到楼下有个好点的建议，雷电接口的笔记本+显卡拓展坞+独立显卡
  - 这个方案的话，拓展坞不做推荐确实不知道怎么选，但显卡4090普遍10000以上了

- ## [AI绘画（Stable Diffusion）用什么显卡比较好？ - 知乎](https://www.zhihu.com/question/638915747)
- 在你能承受的范围内，选显存最大的

- 目前的条件下只有N卡能正常玩AI。
- 想要低价拉满AI。就用RTX TITAN 24GB（不到5000，但需要加水冷压，或者魔改的RTX 2080Ti 22G（不到3000）非涡轮卡的版本。但现在目前看24G的3090性价比最高。

- 推荐一块性价比高的显卡，RTX 2080ti 22g。ai画图性能接近RTX 4090的一半，价格只要五分之一。而且22g大内存，对模型训练也很友好。不过RTX 2080ti 已经上市很多年了，要淘到一块好卡不容易，最好有几年保修的更好

- 跑4K以上稳稳的，显存为32G的显卡一定是首选，不是魔改款，那就只有即将上架的5090了。
  - 跑2K以上的话，12G-16G的卡都可以，不过12G跑某些大模型可能不够用
  - 2K将就用，目前选4060TI 16G的用户多点，不过这款显卡只是预算少的选择，毕竟显存位宽被阉割，GPU性能也一般。
  - 没短板，出图快，首推4070TIS 16G，这款卡，我用下来很满意，缺点就是溢价高。
  - 跑1K以上的话，3060 12G，2060 12G，都已经可以跑了

- 经过不断的优化，现在的Stable Diffusion对显卡要求不算太高，
  - 如果只是跑图，4060Ti 16G就够用，炼丹的话，4090也足够了。

- 至于也是3000多的2080Ti-22G，魔改的有风险，多几G显存对这个软件来说用处不大，有新还是买新。
  - 之后就是7000这一档的，5070Ti，为什么不是4070Tis呢，因为50系显卡可以用4位模型，40系只能8位。

- 10系显卡不支持4bit（其实也不支持8bit、16bit），但是Q4能跑啊，就是慢呗。工作原理是按原位数大小装显存中，跑的时候分段转换成fp32来跑。

- ## [如何评价HP最新发布的搭载AI MAX 300系列处理器的战99 Ultra？ “战 99 Ultra”移动工作站已于3月17号上架京东  - 知乎](https://www.zhihu.com/question/15255805038)
- 今年唯二的Strix Halo笔记本（另一个是幻X），同时可能是唯一的常规形态产品。
  - 这机器在海外的名称是Zbook Ultra G1a，实质上是EliteBook X G1a的复用模具但加厚+增强散热的版本。定位就是旗舰轻薄移动工作站的小尺寸版本，类似ThinkPad P1，但是做了14吋的版本。
  - CPU方面，除了和之前已经上市的幻X一样的AI MAX 390/395（分别对应16C+40CU/12C+32CU）之外，还多了一高一低两个新的配置，更低的AI MAX 385是8C+32CU的规格，同时还有个顶配的商用版AI MAX+ Pro 395，这颗CPU是惠普独占的。
- 其他地方就基本和原版的EliteBook一致了：
  - 2.8k 120hz的OLED触摸屏
  - 74.5wh电池，支持PD 3.1快充
  - 单硬盘位

- 这价格只能说是好家伙了，55w性能释放的常规形态机器，卖的比隔壁幻X的平板形态+80w性能的还贵... 如果一定买考虑，只推荐顶配版本，起码还是有独占CPU的

- 如果主要是冲着Strix Halo这颗CPU来的，那还是更推荐幻X，因为性价比更高，AI MAX+ 395+128/1T的版本也就20999，如果是32G的版本，就只要14999了。

- 为什么STX Halo这颗CPU看起来很好，但实际上无OEM愿意用？个人认为主要原因是两点：
  - 一个是这颗处理器原本应该在2024年和STX Point一起上，却因为种种原因延误到了今年，因此对标的对象也从原来的RTX 4060变成了RTX 5050，这时候STX Halo的核显性能实际上就没有太大的吸引力了
  - 另一点在于STX Halo产生的最大意义在于在空间尺寸受限的平台上做到尽可能高的性能，但现在ROG已经在14.0吋的轻薄平台上做出来BD1的卡了（RTX 5080 on 幻14 Air），幻X的上一代也早已经挑战过在13吋的平板上做H45+BD2显卡
- STX Halo这么个怪物CPU本身存在的意义就已经受到了严重的动摇了。继续往小尺寸做？那散热更完蛋，性能也跟着寄。继续往大尺寸做？做到15吋及以上的平台上，传统的CPU+GPU方案成本低，散热更好做，整体效果还更好
  - 不会有人真的觉得A卡游戏体验好吧，尤其是移动端A卡

- 最大的缺点还是价格。2.5万的价格，如果以他对标的7945HX+RTX 4060的笔记本电脑，都可以买3台了，选择R9000P也就8000多出头。那就看你愿不愿意为了轻薄付出溢价了。

- 惠普战99 Ultra，海外对应型号Zbook Ultra G1a，便携移动工作站定位。常规的配置例如全金属机身、2.8K OLED屏幕、惠普工作站的祖传接口3C+HDMI+1A、74.5Wh电池就不再赘述了。
  - 最大的亮点就是AMD锐龙AI MAX 300系列的处理器。AI MAX+ 395处理器是惠普独占，CPU规格和桌面端9950X相当，只不过受制于笔记本电脑散热不能完全发挥；说是集显，但是性能堪比RTX 4060的独显。
  - 同时另一大好处在于实现类似于苹果一样的128GB统一内存，最多可以分配96GB给显存。128GB内存版本为4通道，内存吞吐速度能够达到200GB/s出头，比常规的双通道100GB/s直接翻倍了
- 14寸的笔记本电脑，重量到了1.6kg，属于是偏重的。性能释放也就在55W，不能发挥出完整性能。作为移动工作站只有单硬盘位。

- 问题是性能释放还不如幻x，这个只有55w。

- ## [ROG幻X 2025对于运行AI应用（如本地大模型）有没有显著优势？能否助力用户提升AI体验？ - 知乎 _202503](https://www.zhihu.com/question/14670046303/answers/updated)
- 属于什么都能干，什么都干不好的富哥玩具。
  - 便携和离电性能比不过几千块的mac air。
  - 游戏性能比不过同价位的4080m（马上就5080m了）
  - 大模型被同价位mac studio m4打爆。

- 这玩意跑大模型的能力就是个3060 12g或者最多4060ti 16g的水平，反正12g～16g显存跑不起来的东西395也没速度了，而只要用显存能跑起来，速度绝对吊打395。
- 按我理解这玩意的意义是具备轻薄本少有的同时具备64g以上内存、不尿崩的续航、足够强的显卡以应付图片和视频编辑。然而在这个场合下，却被MacBook pro全方位爆杀。

- [独家首发AI Max+395处理器 ROG 幻X 2025跑分解禁，是否值得购买？ - 知乎 _202502](https://www.zhihu.com/question/12616419565)
- 最近我看到业内新出现了2种桌面级AI计算/PC类产品，一个是在NVIDIA GTC大会上正式发布的DGX Spark（芯片代号GB10），还有基于AMD Ryzen AI MAX PRO处理器的笔记本/移动工作站/台式机，都宣称能支持70B乃至更高参数的模型。
  - NVIDIA DGX Spark号称“最小的 AI 超级计算机”，它的处理器有点像微缩版的DGX计算系统（参考下图），在GB10单芯片上集成了Grace CPU——20个Arm Core，以及Blackwell架构的GPU。
  - AMD Ryzen AI MAX PRO系列（代号Stirx Halo），更接近传统集成显卡的x86 CPU，但整合GPU的性能却比较强。其默认TDP功耗55W，根据不同系统设计，cTDP可调功耗在45-120W范围。
  - 无论使用CPU还是GPU做AI计算，在LLM推理的Prefill（内容输入理解）阶段的瓶颈是算力；而在Decode输出时的性能（Token/s）则主要受制于内存带宽。
  - 我们看到上面2款产品都使用了256位LPDDR5x-8533内存（AMD的实际运行速率为8000），比传统AI PC的64位双通道内存提高了一倍，相当于4通道。
- 由于Grace ARM CPU只认证了DGX™ OS操作系统，应该只能跑Linux（不兼容Windows），所以DGX Spark主要就是用于计算，图形性能方面不知是否做了优化？
  - DGX Spark的AI性能，与GeForce RTX 5070桌面显卡较为接近。不过有一点，5070的显存带宽高达672GB/s，这一点即使是256bit LPDDR5x内存的集显也忘尘莫及。毕竟一块5070独显就是250W TGP功耗，其空间占用也很难做到Mini机箱/轻薄笔记本里面。

- ## [AI绘画（Stable Diffusion）用什么显卡比较好？ - 知乎](https://www.zhihu.com/question/638915747)

- ## [不计预算，帮我买一台性能超强，外观简约的笔记本电脑？用于本地部署各种大模型，暂定微软，还有别的选吗？ - 知乎](https://www.zhihu.com/question/624402976)
- Windows笔记本这边的性能天花板是 i9-13980HX/R9-7945HX +RTX4090（175W）
  - 这俩CPU性能差不多，7945HS便宜点
  - 推荐你选i9-13980HX，因为Intel对各种生产力工具的兼容性更好。
  - 移动端RTX4090的性能相当于桌面端的4070Ti，但是它有16G显存，比12G显存的4070Ti更适合跑模型。
  - 目前，搭载13980HS和RTX 4090笔记本的价格普遍在22000元以上。比如ROG枪神7和微星GP78HS
  - 同样的价格你可以买到i7 13700K和RTX4090 24G的台式机（惠普暗影精灵9plus）

- 当前笔记本端最强的4090笔记本显卡，规格上持平桌面4080，跑分性能上与桌面4070ti相当
  - 笔记本端次强的4080笔记本显卡，规格上接近于桌面4070ti，跑分性能与桌面3090相当

- 建议还是戴尔，惠普，联想这三家的工作站笔记本吧。工作站配置的独立图形显卡适合的要求的大量模型，再就是工作站的内部结构、配置都是针对处理大型3D模型做了加强、优化的，其工作稳定性是普通笔记本无法比拟的。

- ## [amd发布新的芯片，这次芯片跟苹果的m4一样，将gpu和npu集成到同一块芯片上去，说明了什么？ - 知乎 _202501](https://www.zhihu.com/question/9253691862)
  - AMD 在 CES 2025 上发布了锐龙 AI Max 300“Strix Halo”系列 APU，搭载了最高 40CU 的超强核显，此外集成了 50 TOPS“XDNA 2” NPU。
  - 这种将强力 CPU、GPU、NPU 等集成到一个芯片的做法，看起来有点像苹果在 M 系列芯片中的设计。

- 苏妈看到apple M系列芯片被拿来跑AI大模型推理的时候，也鼓捣了一个Ryzen AI Max 300 系列处理器规格曝光，最高16核心、40CU核显 。最高可以从内存中分配96GB超大显存，结合ROCm（开放计算平台）系统支持，或能变成新一代小型工作站神U

- ## [如何看待英伟达公司发布的桌面级AI超算? - 知乎](https://www.zhihu.com/question/8970511370)
- Project Digits 现在改名叫：NVIDIA DGX™ Spark 。
  - 其定位是：个人桌面端的 AI 超级计算机。
  - 由 GB10 超级芯片驱动
  - 使用 FP4，AI 性能达 1000 TOPS
  - 配备 NVIDIA Blackwell GPU，⽀持第五代 Tensor Core 技术
  - NVIDIA Grace CPU 实现，采用 20-core 高性能 Arm 架构
  - 128 GB 统一寻址系统内存
  - 支持高达 4 TB 的 NVMe 存储
  - 支持高达 200B 参数的大语言模型
  - 通过 NVIDIA Connect-X 网络进行连接，可连接两个 DGX Spark，支持高达 405B 参数的模型

- ## 🚀 [如何评价英伟达新发布的桌面 AI 超级电脑 Project Digits？ - 知乎 _202501](https://www.zhihu.com/question/8953765123)
- 上午还在看AMD strix halo，下午Nvidia突然就放了一个相同定位的...

- 想买的同学注意下这个设备的内存，它是统一内存，即CPU和GPU共享LPDDR5X. 它不是GDDR6，也不是HBM2的。
  - 虽然有 128GB，但是根据 Grace 架构 CPU 的 Product Brief，单 CPU 的内存带宽最大只有512GB/s
  - 所以如果用这个设备来运行大语言模型，瓶颈就会变成这个内存带宽。
  - 简单来讲，大语言模型每生成一个token，就需要将整个模型扫一遍进行计算（实际上比这个描述复杂很多）。这意味着，当浮点算力充裕的时候，扫描的速度就决定了生成文本的速度上限。
  - 目前这个设备的内存带宽水平跟 M4 Max 的 MacBook 没什么区别（Apple MacBook Pro M4 Max 128GB 内存带宽是546GB/s）
- 拿 [Llama-3.3-70b-instruct-4bit] 举例，这个4bit量化模型大小约为40GB，那么扫一遍就意味着GPU要处理40GB的数据，如果想要每秒钟生成10 token，简单计算可得，40GB\*10 = 400GB, 这意味着内存带宽至少有 400GB/s 才能保证每秒钟能生成 10 token.
  - 回到 digits 这个设备，在512GB/s 的情况下，**运行 70b-4bit 规模的模型，生成速度理论最大值是 512/40 = 12.8 token/s**

- nv版的mac mini。当然mac mini有macos，project digits只有linux，操作系统生态上以及桌面级定位上估计会导致拉胯掉，nv虽然有cuda生态，但是在桌面级相比os的生态，还是有点困难的。
- 大模型推理其实是个很微妙的产品需求，大显存容量很重要，memory bound也是事实。
  - 总体来讲，容量比带宽重要，毕竟容量决定了yes/no，带宽决定了token/s的体验。但是体验差到一定程度也是个yes/no的问题。
- 以ai pc今天事实上的超级应用为例ai编程而言，10 token/s以下基本就是玩票，加上ai啰哩啰嗦要分析一大堆，基本要做到可用还是得30～40 token/s
  - 按照激活量算，30～40token/s，如果10GB的激活量就300～400GB/s的内存带宽
  - dense模型10B上下做ai编程几乎没法用，moe可以搏一搏。
  - 目前的模型主流的基本都是70b以下的dense，以及200b以上的moe，70b以下的dense很尴尬，效果上比较难接近200b以上的moe，容量需求小，但带宽需求可是实打实的超级高。比较适配[gddr显存] 的正经游戏卡。

- GB10的芯片，应该是从服务器的GB100当中砍一刀下来用的。CPU是联发科定制的一颗ARM，GPU部分算力达到1个P，fp算力。最大的亮点直接拿了128GB的 LPDDR 5x内存做显存。
  - 很多人其实不知道，现在跑大模型无论是训练还是推理，最大的瓶颈是显存容量不足（Memory bound），而不是算力不足(Compute bound)。
  - 比如一个200B的模型，在fp4或者int 4的前提下，光是显存占用就要有100GB大小。运行起来之后还要有kv cache随着上下文长度占用而增大。一张显卡装不下，就要分布在多张卡上，那么就会产生通信开销从而导致算力无法被充分利用，不得不等待通信完成之后再进行计算。
  - 之前消费级的RTX 4090，最大的显存只有24GB。RTX 5090，也只有32GB显存而已。数据中心卡例如A100有40G和80G，但价格又会显著比消费级显卡贵。
  - 所以现在这个128GB的内存作为统一显存使用，至少解决了显存不够用的问题。3000美元的售价，甚至可以说良心了。

- CPU是联发科定制的一颗ARM，跑Linux玩毛游戏

- 其实前两年AI刚开始起头的时候，local LLM和文生图爱好者就发现多数任务都是memory bound的了，市面上除了比汽车还贵N家推理卡，只有Mac的统一内存能装的下。
- 这个具有可用性，cuda生态与性能是不用担心的，mac跑ai就是行为艺术，速度慢到爆炸，生态也是残缺的
- 只是为了 128G 统一内存现在也不需要买这玩意儿啊.. $4799 的 Mac Studio 或者 $4999 的 MacBook Pro 就行. 当然只是为了 AI 目的的话, 老黄这个盒子确实更有性价比.

- 三千刀，128GB，这个价格其实不比苹果好多少。而且三千刀是starting price

- 经典的72B的Llama模型，8比特精度需要84GB的显存，那就需要2块A100或者4块24GB的4090/3090，这两种方案都要比3000美元多且复杂。
  - 要知道Project digits是一整个机器，72B的经典模型可以直接跑，这样就基本上可以做绝大多数的微调工作。
  - 甚至两台机器，就可以跑4比特精度的200B模型，这么大的模型放到之前基本上只有大的公司或者实验室才有可能跑的起来，而现在6000美元就能完美解决，这对于绝大多数的穷Lab来说都是天大的福音。

- Strix Halo和M4 Max是高规格的消费级产品，搭载Strix Halo的是各种品牌开发的笔记本电脑、SFF主机，甚至是准系统、MoDT主板，它们搭载Windows 11操作系统，也可以安装任意GNU/Linux操作系统，就像一个普通的x86电脑一样
  - Project Digits的CPU，是联发科定制的20核ARM CPU，10大核为Cortex-X925，10中核为Cortex-A725。A725和M4小核大性能接近，而X925则不如M4大核和Zen5。另一方面，ARM Linux的生态并不如x86，这和ARM macOS完全不同。Strix Halo的16核32线程的zen5 CPU，基本上是顶级的CPU配置，其多线程性能是拉满的。
  - Project Digits的内存，虽然官方没有说明，但很大可能也是256位的，此时Project Digits在使用LPDDR5X的8533MT/s的内存时，其速率同样为272GB/s，而这一带宽，仅与Strix Halo/M4 Pro相同，是M4 Max的一半；如果是512位，则强于Strix Halo一倍，并与M4 Max持平。
- halo的npu总共就50tops，8060s也没有硬件wmma，2.5ghz下也就51.2tops，加起来不到gb10的1/4
- 可惜halo不是统一内存架构
  - halo是uma架构，15年前初代apu就已经是uma架构了

- 这个东西3000刀是真的很贵，不过project digits是挑战冯诺依曼架构，CPU 访问内存、硬盘，显卡处理数据需要把数据先传到显存。统一内存架构就是把GPU核心直接与内存相连，弄大内存。
  - 目前除了大公司有钱买几百上千卡跑训练，普通人真跑不起LLM大模型。对于普通人来说，核心算力不重要，问题是怎么在显卡load大模型。而统一内存就是用超高性价比的内存代替显存，不用GDDR7，用DDR5 。
