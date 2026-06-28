---
title: tool-iot-devices-gpu-diy
tags: [diy, gpu, iot, pc]
created: 2026-06-23T09:00:20.510Z
modified: 2026-06-23T09:00:34.414Z
---

# tool-iot-devices-gpu-diy

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-oculink
- ## 

- ## 

- ## 

- ## [Has anyone tried setting up eGPU with halo strix through OCuLink? : r/StrixHalo _202606](https://www.reddit.com/r/StrixHalo/comments/1udnym5/has_anyone_tried_setting_up_egpu_with_halo_strix/)
- as long as there is nvme slot, egpu is most likely possible
- Yes, I used nvme to oculink. On Fedora it worked no problem.

- I've done it, albeit with TB4 rather than occulink. Works fine now, I'm using an aoostar ag02 with a RTX5080.
- I havent bothered with oculink but I have a blackwell 5000 working over tb4.

- Yea, I have an old RX 6600 XT connected via oculink via a PCIE 4.0 x4 to Oculink card on my framework desktop mainboard. I use it to run embedding and reranker models and it has been working great so far on Fedora 44 & RADV llama.cpp vulkan backend.

- Can do. My devices: Strix Halo -> NVMe -> OCuLink -> V100 GPU. The Ubuntu update feature automatically installed the 580 driver, and I then manually installed CUDA 12.8. I tried this because CUDA performs much better in many scenarios.

- ## [Has anyone used a NVME to PCIe riser successfully with Strix Halo? : r/StrixHalo _202606](https://www.reddit.com/r/StrixHalo/comments/1uctbiw/has_anyone_used_a_nvme_to_pcie_riser_successfully/)
- https://strixhalo.wiki/Guides/External_GPU

# discuss-gpu-mod
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [96gb+ 4090's and 5090 are literally a scam. I mods these cards myself : r/LocalLLaMA _202606](https://www.reddit.com/r/LocalLLaMA/comments/1uh1lc7/96gb_4090s_and_5090_are_literally_a_scam_i_mods/)
  - I run a small gpu lab in the USA and work closely with two factories in china designing/producing 48gb 4090 PCB's.
  - The only recent card weve gotten was the 32gb 4080 super.
- Nobody can mod 5090 adding extra VRAM at the moment. No leaked VBIOS and many other issues and the memory shortage isn’t even at the top of the list.

- ## [V100 4-card AI large model, Tesla 128G server : r/LocalLLaMA _202606](https://www.reddit.com/r/LocalLLaMA/comments/1udd8a9/v100_4card_ai_large_model_tesla_128g_server/)
  - cost for USD 3687.76 V100 128G Liquid-Cooled Graphics Card Dock, 360° Liquid Cooling for the Entire System.

- idle power draw = 300W, thanks but no
  - They are 40W idle per V100. About 60-70W with model loaded but idle. Nvidia-pstated will get back down to 40W with model loaded but idle. 300W is TDP. Can only achieve that with training or another heavy duty operation. Inference maxes out at half that. Multi-GPU round robins, so most at 40W while they take turns peaking out at 150W.

- they don't support CUDA 13. Last gen not to do it. Not a problem for a couple years, will get more problematic as time goes on.
- Nope, up to 12.x. At my last job we had a cluster of v100s, when using newer packages you end up running into a lot of cuda kernel incompatibility issues. Given the V100 isn’t supported anymore no one is developing with them in mind.

- there is always place for open source enthusiasts: there is guy maintaining VLLM for specifically for V100: https://github.com/1CatAI/1Cat-vLLM

- ## [显卡仙人 TESLA V4 16G 1499人民币 _202606](https://t.bilibili.com/1211458176581369862)
  - TESLA V4 32G 3999人民币
  - NVLINK桥接器 199人民币
  - 互联:100G/S NVLINK互联
  - FP16 90+TFLOPS  /FP32 11TFLOPS  /FP64 6TFLOPS
  - [【垃圾佬】绝世大活？DIY制作显卡？单槽半高V100  _202606](https://www.bilibili.com/video/BV13JEa6sEtb/?vd_source=deff4d2e2efa3273948dd6911a08fd39)

- [Chinese Hackers Latest Masterpiece with NVIDIA : r/LocalLLaMA _202606](https://www.reddit.com/r/LocalLLaMA/comments/1ucokod/chinese_hackers_latest_masterpiece_with_nvidia/)
  - They spent a year to reverse-engineered the Tesla v100's 2, 963 pinouts signals, soldered it onto a half height PCB, with full NVLink support (up to 8 way capable), then naming it Tesla v100 v4.

- Some Chinese people also reverse engineered that generation of nvlink so that you can now buy a 4 way adapter card that connects to MCIO cards in your computer with 100GB per second of bandwidth between all 4 GPUs.
  - 128GB of HBM memory split over 4 cards with that link speed is looking quite tempting.

- Price seems about the same as v100 on ebay, so why buy this? Smaller physical size?
  - yeah low profile single slot. they basically grafted the whole gpu and necessary components onto a new custom designed PCB.
- Nvlink
- inference also benefits from NVLINK. Not so much for 2x cards, 4x cards significantly, 8x cards (typical server setup) it benefits A LOT. RTX Pro 6000 Blackwell is ~3/4 H100 in fp8/f16 compute, but 8x H100 servers absolutely TROUNCE 8x RTX Pro 6000 setups in total throughput

- The water blocks already exist... I bought 2 of the 32gb for$ 450 each on eBay. Admittedly I use them for Flux2 Klein, but it handles the 25gb model handily.
  - The post is talking about more heavily modified versions of what I have. I have the 2x sxm2 Nvlink board, was $300 then I put the $450 ea v100s on it. It's an older architecture, so I have to be more picky about the models I run... But after a bit of research I get 2/3 the speed of my 3090 for 1/4 the cost, so it's worth it for me.

- I wonder do they really reverse engineered or Schematic fell off the truck. I know the V100 SXM PCB file is readily avaliable everywhere.
  - NVIDIA has never leak the definition for the 2, 693 pinouts on the back of the V100 chip, so engineer used tools they wrote themselves to reverse-engineer them.

- It’s wild how much effort went into this. Reverse-engineering nearly 3, 000 pinouts just to bring SXM2 V100s to a custom low-profile PCIe board with working NVLink is absolute peak tinkerer energy.
  - For anyone looking to host larger models locally on a budget, 128GB of HBM2 across a 4-way cluster for under $2, 500 is incredibly tempting, even if the lack of native BF16 and newer CUDA support hurts token-per-watt efficiency.
  - I wonder how the community will handle the cooling though. A custom active cooler or water block is going to be mandatory if anyone plans to actually run these at a full 250W–300W without melting their rig.

- These are NVidia chips, not a new chip. It's taking old Tesla server GPUs and mounting them on top of consumer PCIe cards together with power and cooling, so you can put them on your home PC.
  - With that said, it's an old tech, doesn't support BF16, doesn't support Cuda 12.x+, and is really slow (5X slower than RTX 5090 for local inference), so suddenly power consumption becomes a big deal.

- they need to figure out how to make it 64gb or 96gb and then we can dance.
  - Just buy 8 of them and nvlink them, lol.
- I think that is actually unfeasable, this is not GDDR memory that you solder onto a PCB, the HBM memory sits on the GPU die itself (technically rit next to the actual die but the point stands). I really do not not think there is anyway to do it

- That cooler looks rather small compared to the official pcie v100
  - video mentioned that they are planning on an actively cooled version with a fan
