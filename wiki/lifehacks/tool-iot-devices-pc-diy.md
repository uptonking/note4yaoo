---
title: tool-iot-devices-pc-diy
tags: [devices, diy, iot, pc]
created: 2026-01-15T15:45:46.766Z
modified: 2026-01-15T15:46:21.626Z
---

# tool-iot-devices-pc-diy

# guide

- tips
  - 不推荐买整机工作站，购买单独的算力卡即可
# discuss-stars
- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 
# discuss-tips/xp
- ## 

- ## 

- ## 
# discuss-server-epyc
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [如何评价intel放弃NUC产品线？ - 知乎 _202307](https://www.zhihu.com/question/611600066)
- 虽然NUC是Next Unit of Computing的简称，可以理解为“下一代准系统”。
  - 即通常提供一个足够迷你的主板+CPU，而内存和存储部分你可以DIY，包含了主板和CPU的平台我们一般就叫“准系统”，不过准系统并不完全一定是主板+CPU的绑定；比如后期妖板华擎做的系列就是可以自己选择CPU，且支持桌面级CPU，只是CPU有一定的功耗限制等。
- NUC本身是介于办公电脑和一体式电脑之间的产物
  - NUC就感觉是一体式电脑把显示器和主机部分又剥离出来，只不过把主机做得足够小
  - 所以一开始NUC的设计就支持把NUC 挂在显示器后面，只需要一个扩展铁皮就行了。

- NUC我也买了, 性能很普通. 看中的就是一个小巧和稳定. 大家可以看下网上同样的小电脑的对比, 能支持7*24H当个人服务器的运行的, 也就Intel的了.(Dell惠普的那些机器也行, 但是发热低的性能还是比intel差一点)

- NUC大部分产品线 miniPC（除开独显部分）在产品定义上都是很好的产品：性能够用/扩展性够用/体积小/可靠性也不错/整体持有成本低
  - 但市场营销的用户教育存在问题，大部分用户甚至都不了解这条产品线存在，即使知道，对其性能和持有成本也没正确认知，想当然的认为小机器性能差/价格贵。

- 作为解决方案的制定者，又不能完全霸占市场，需要给合作伙伴们分一杯羹，所以，英特尔的NUC溢价非常高，如果不是像我一样入了魔，就是想要那个LOGO，只是需要一台小巧的迷你主机的化，其实有非常多的品牌和产品可以选

- ## [20寸行李箱尺寸长宽高（20寸拉杆箱到底到底有多大）](https://www.zhihu.com/tardis/zm/art/320648263?source_id=1003)
- 不管是行李箱还是电视，统一用的都是这个斜对角尺寸测量方法。
  - 1寸=2.54cm
  - 20寸=50.8cm
- 20英寸并没有一个固定的长宽高，但是我们可以给一个相对标准的拉杆箱尺寸作为参照。
  - 20inch: 50 x 34 x 19 cm, 32.3L
  - 22inch: 55 x 42 x 23 cm, 53.1L(可用约47L)
  - 28inch: 70 x 47 x 27 cm

- ## [AMD EPYC 9654的主板为什么这么贵？单路9654能打7763双路吗？ - 知乎](https://www.zhihu.com/question/598929770)
- 多项测试里单路 96核 9654 都优于 双路 128核 7003（7763/7773x）。
  - 架构制程升级、频率（大幅）提升（全核满载提升0.5GHz+）、12通道DDR5 4800、单路本就更低的多的CCD间通讯延迟等，都是不小的优势
- 现在9004主板也没那么贵了，**单路板子5k价位就能拿下**，没比双路7003贵多少，ddr5 reg价格也在下降，整套还是比较超值的。

- 5k真的不会赔本么？每个内存通道是不是72跟信号线，12通道是864，除此以外还有那么些PCI-E，这些还要和电源线地线混在一起，感觉很不容易了。当然了，要说每根信号线频率其实不算高，跟nvlink之类的没得比

- ## [震惊！华南金牌对标超微H12SSL干了一个EPYC单路主板H12D-8D - 知乎](https://www.zhihu.com/zvideo/1883448198976218443)
  - 这款H12D-8D是直接对标H12SSL，支持AMD EPYC 7002/7003 ，Rome和Milan
  - 8个 DDR4 内存插槽
  - 4个 PCIe 3.0/4.0 x16 插槽

- ## 🐛 [为什么华南、精粤这种寨厂不做EPYC主板？ - 知乎](https://www.zhihu.com/question/4214916755)
- EPYC还真是流出来的多，但是能用的却不多
  - 看zen3同款epyc主板的架构图。是不是很简单，连个桥片都不用。
  - 为什么廉价的EPYC比较少呢？
  - 因为 EPYC 在OEM厂商那帮有个 PBS绑定政策，OEM商可以设定唯一秘钥绑定，也就是首次使用可以把CPU和主板绑定，当CPU更换主板时，触发PBS策略拒绝启动。

- 板U绑定这个策略，又不仅仅是epyc有，Core和Xeon部分OEM厂的货也有。某一线大牌的Core商用整机我就遇到过

- tb上能找到的大部分都是无锁，黄鱼上就不知道了
- 闲鱼上有很多有锁的，不过如果是双路主板的话只检测第一个CPU有没有锁，第二个CPU即使有锁也不影响使用
- 因为epyc boot只用cpu0吧
  - cpu1的io die在启动链里面不负责安全校验

- 性能够用，还没到大规模淘汰期，已经流出来的部分很多又被ai炼丹师给收走，它的PCIe通道比同期Intel Xeon多。
- epyc铺开来才几年啊，云服务器能租到epyc的u也是这两年的事
- AMD第一代第eypc和第二代eypc都是试水，开始卖起来都是第三代了，现在上游淘汰没那么快，未来大概率还算买整机嘛，其二现在你要搞64核的方案，amd的可以DDR4，6k左右搞定大内存方案，intel要大内存只能用es版的上ddr4，如果上ddr5价格就飞天了。

- 刚刚查了一下，华南金牌出3647主板了。
  - 价格不便宜，对应的架构不过是skylake而已。
- 再次更新，支持EPYC的主板来了。
  - 华南金牌 H12D 单路epyc主板 可以用来满血deepseek的装机主板 pcie4.0主板

- 成本高，设计难度高，量小，还是去伺候又没啥钱又事多的垃圾佬，何苦呢？
  - 超微x13 单路板看起来很丐只有8相供电基本没散热是不是，用下来它可以持续稳定385w输出 mos温度也就80。不是消费级那些整了十几相上超重散热装甲200w还奔七八十的垃圾供电mos能比的。

- 好像，据说Ryzen Pro和Tr Pro也开始上锁了？这类U也是专供OEM不零售的
- 这对于垃圾佬+A炮而言是个噩耗。Ryzen APU从8000G开始，核显的编码解码能力已经比较好了，加上它优秀的功耗和性能，以及Pro版支持ECC内存，未来很有潜力成为种子NAS DIY/软路由等家庭服务器的神U。但带锁可就。。。

- 主要原因是CPU不够便宜，实际上也做了几款，但没多少人去买。
  - E5装机市场繁荣，前提是性能够用+相对廉价，从核心多频率偏低的服务器用，到核心少频率高的单路工作站版本都有提供，还有利用v3系列E5的bug，强制全核睿频跑的鸡血补丁，属于多开挂机、单机玩游戏，都能上。
  - EYPC霄龙是 [锐龙] 同代，要比E5晚上好几年，性能自然是更好，也因为如此，大规模从 [IDC] 下架的时间还早，货源不多，依旧达不到“垃圾价格”。本来一代的7601配合国鑫平台便宜过一段时间，但因为QU之类的CPU矿又涨回去，后来AI火热，EPYC的核心和PCIe通道巨幅优势，又让二手市场价格难以骤降。
  - 最终结果就是，因为CPU不够便宜，下架数量少，尽管EYPC是不需要南北桥芯片组，而是基于PCIe HUB做扩展即可，但寨板们没动力和能力去做主板。
  - 抄板的话，大厂主板多层PCB，成本高到让寨厂抄不动。实际上华南已经出了的EYPC和C621主板，实际零售都是两千块一片，比超微、泰安便宜有限， 难以做到E5寨板那般热卖。

- ## 🆚💡 AMD Threadripper PRO 7985WX and Threadripper 7980X  have the same cores/threads/chiplets-ccd-numbers
- [AMD Ryzen™ Threadripper™ 7980X Drivers](https://www.amd.com/en/support/downloads/drivers.html/processors/ryzen-threadripper/ryzen-threadripper-7000-series/amd-ryzen-threadripper-7980x.html?utm_source=chatgpt.com)
  - Memory Channels: 4
  - System Memory Specification: DDR5 Up to 5200 MT/s
  - ECC Support: Yes (Default Enabled)

- [AMD Ryzen™ Threadripper™ PRO 7985WX Drivers](https://www.amd.com/en/support/downloads/drivers.html/processors/ryzen-threadripper-pro/amd-ryzen-threadripper-pro-7000-wx-series/amd-ryzen-threadripper-pro-7985wx.html)
  - Memory Channels: 8
  - System Memory Specification: DDR5 Up to 5200 MT/s
  - ECC Support: Yes (Default Enabled)

- [AMD EPYC™ 9354](https://www.amd.com/en/products/processors/server/epyc/4th-generation-9004-and-8004-series/amd-epyc-9354.html)
  - Memory Channels: 12
  - System Memory Specification: DDR5 Up to 4800 MT/s
  - Per Socket Mem BW: 460.8 GB/s

- [同样16核32线程64M缓存，EPYC 7282为什么比5950X贵很多？ - 知乎](https://www.zhihu.com/question/513604769)
  - 去看看目前海鲜市场的价格，7282价格260的样子，5950X价格还在1800左右
  - 不过配套的板子价格就一个天一个地了，EPYC二代板子1000起，能跑满5950X的 B450高配板子300起，整机还是5950X 稍贵点儿
  - 7282全核频率3.2G，5950X散热好的话可以单核4.85G, 多核4.4G
  - 对游戏性能有要求的人，远比对128个PCIE通道有要求的人多，打游戏的给个 PCIE4.0 16X + 4X NVME 就够了

- ## 🤔 [Thoughts on older/used threadripper for deep learning machine build : r/threadripper _202410](https://www.reddit.com/r/threadripper/comments/1g3meqp/thoughts_on_olderused_threadripper_for_deep/)
- what’s the difference between epyc and threadripper? It seems perfect for me and it’s a lot cheaper than a threadripper. What’s the catch?
  - Threadripper was designed for workstation users. Threadripper CPUs generally have faster cores with higher boost clocks, as they are designed to be used interactively in real-time.
  - Epyc is designed for servers. Slower cores, less boost, perhaps more outright(全部的, 彻底的) compute per watt, but not designed to maximize responsiveness for real-time user interaction.

- just saw Epyc doesn’t support windows. 
  - Epyc runs on Windows 10/11 Pro for Workstations
  - At work we use Windows VMs running on Epyc processors in Azure, and the underlying host would be Windows Server, not Linux.
  - I read somewhere that you can use the Workstation version for that
  - I've seen that option when installing from the Windows installation USB image
  - Windows 11 Pro for Workstations

- Another option is an EPYC system, which will have lower CPU performance than TR Pro, but the same memory capacity and PCIe lane count.

- ## [Where to look for cheap PCIE gen 4+ threadripper cpus at a low price on the EU : r/threadripper _202505](https://www.reddit.com/r/threadripper/comments/1kbvmfs/where_to_look_for_cheap_pcie_gen_4_threadripper/)
- I switched from tr consumer to tr pro to epyc. Originally mostly VMs and some cpu heavy work. Then mostly VMs with some AI. Now all AI. Just running a 7313p (previously 3960x and 3970x boxes, then 3975wx and 5965wx). Epyc is lower power, supports u2/sas, tons of cheap ecc ram. Worth a look. Bought a few TR combos from tugm, good seller who has both platforms.

- ## [Testing Ryzen 8700G LLama3.1 : r/LocalLLaMA _202407](https://www.reddit.com/r/LocalLLaMA/comments/1efhqol/testing_ryzen_8700g_llama31/)
- I think for a lot of gaming tasks, memory bandwidth isn't necessarily the limiter, and they're trying to max out what they can do in a 'normal' desktop. Threadripper has quad and octa channel ram, so putting one of these in that could make for a very potent LLM system as they can address something like 2TB and the 7995wx can hit like 700GB/S of ram bandwidth. I'm sure that'd make for an interesting memory controller setup on there...
  - I don't have a 7995wx but I do have a 7980x and I was disappointed in the LLM speed. That 700GB/S figure is very misleading in the marketing its the CCD to Controller Speed not the RAM. Real bandwidth is closer to 300 on 7995wx and 150-180ish on mine. I guess if you could find a 7200 RDIMM ECC module for less than a house it might do better but I paid over 1400 for 256 GB of 6000, I wouldn't want to think of what a 7200 would cost if I could even get it to run at that.

- ## [Why is EPYC faster but cheaper than Threadripper? : r/buildapc _202404](https://www.reddit.com/r/buildapc/comments/1buf060/why_is_epyc_faster_but_cheaper_than_threadripper/)

- Threadripper PRO 5955WX is a 64-core Zen 3 CPU (2020 architecture). EPYC 9654 is a 96-core Zen 4 CPU (2022 architecture). That's why the EPYC is faster.
  - Under normal circumstances, the 5995WX should be much cheaper. In my area, the 5995WX is available for ~1500 USD. And EPYC 9654 normally costs many times more than $4K, so confirm that it's legit before buying.
  - There are Zen 4 Threadripper PROs available as well. The 7995WX is faster than the EPYC 9654 thanks to higher clock speeds and higher power limits.

- First of all, Threadripper and EPYC are based upon the scalability of Ryzen CPUs and Dies. 
  - But while Ryzen CPUs offer the highest single-core performance and are suitable for desktop use, the use of a Threadripper demands very special hardware: special Mainboard, RAM, CPU cooling solution and a much higher PSU requirement. Also, Threadripper CPUs are selected Dies that offer higher clock speeds under lower voltages. To get a max. of 96 cores to work with a TDP of 350W while a 16 core 7950X asks for 170W, should show the difference in Die quality. Also, Threadripper work great in Windows and other desktop OS and even in games they work - although less optimal, as any Ryzen 7 and upwards will be faster due to higher single-core clock speeds. Scientific laboratories, professional workers (CAD, architecture, engineering, ...) love this kind of power in the machines.
  - EPYC CPUs however are designed to work very efficiently, very stable and offer basically unmatched performance in data centers. They really shouldn't be used in a desktop environment as boards are usually way less beautiful (most important point), designed to be mounted in a rack, way more expensive and not optimized to run any desktop stuff without a virtualization environment. The single core boost is 1, 4GHz slower than that of a Threadripper Pro. Also, support is business orientated. Meaning: No special support contract, no or basically no support. An adequate cooling solution is also a problem.
  - The probably best way to spend money if you have it is a Threadripper Pro 7975WX. 4GHz base clock, 5, 3GHz turbo boost and with 64 cores more than enough for basically everything you throw at it.

- The Threadripper should spank(用手掌或扁平物掴) the EPYC in workloads that don't utilize a lot of cores.
  - If your workloads can utilize all the cores (make sure they can!) the EPYC is significantly better. It does use a lot more power but that doesn't sound like a concern for you.
  - Also, that 9654 is suspiciously cheap. Like waaaaaaay too cheap. That's why the TR looks like crap in comparison.
  - You really shouldn't be looking at canned benchmarks in a situation like this. You need to find benchmarks that represent the workload(s) you'll be doing.

- ## 🧩 [旅行的好搭子拉杆背包，ta来了！ - 小红书](https://www.xiaohongshu.com/explore/6810462000000000230145b2?xsec_token=AB_QqkK7_ZF3_KbwyW1ZB1W-e9_xlRmGRCX97e_tYARKI=&xsec_source=pc_search&source=unknown)
  - 扩容书包泰格斯拉杆箱

- 日常通勤35L，出差一键扩容到40L，不用托运！
  - 拉链全可上锁，防盗设计太适合机场用了！

- ## [平替行李箱的商务双肩包，40L！还能扩容 - 小红书](https://www.xiaohongshu.com/explore/6835bf120000000021002156?xsec_token=ABatORMjMwyzFmPxDjEJEf-p8c6FH-fG8_XdNtue8G_L0=&xsec_source=pc_search&source=unknown)
  - 容量超大：主仓+扩容层40L容量，5-7天衣物+电脑+洗漱包全塞下，侧面还能插行李箱杆，赶车超方便
  - 贴心分区：电脑隔层带缓冲+独立文组仓+暗格防盗，连充电宝都有专属位和外接口

- [求一个40l左右的双肩包推荐 有背负系统的 唯一附加要求 好看！！！！ 求求 #背包客 #户外徒步 - 小红书](https://www.xiaohongshu.com/explore/6842cbd0000000002100057b?xsec_token=ABT9L2VXltMP-GUaPSRafreWyko5UR63i8ehZlDenL0as=&xsec_source=pc_search&source=unknown)
  - 神农radix47（白色）、格里高利琥珀44（红色）、始祖鸟aerios35（黑色、紫色）

- [一个人旅行系列之可登机双肩包 - 小红书](https://www.xiaohongshu.com/explore/65e1833800000000040027ab?xsec_token=ABIG1oshPpa6-_2S9Eiadw0dwjUN6w5GF6LRXEljnCLc0=&xsec_source=pc_search&source=unknown)
  - 一般来说国内航空是115原则，既55厘米×40厘米×20厘米，重量一般为7KG，（具体还是要看航司规定）。
  - 有些也分享过45，48，50l登机的，实际上我也看到过，但是！但是！但是！也有人被拦下的！所以航空公司不同，地方不同，可能导致不一样的结果。

- Peak Design backpack 45l ，2.09kg
  - 优缺点：30l模式下可登机，拉链式的可扩容45l模式（几乎没超）大容量，多用途可搭配内胆（自行购买），他是最好的旅行双肩相机包，可能没有之一。

- 最大容量的包Osprey Farpoint 40L和Osprey Porter 46L
  - 瘦长的包不合适，能放进去但是容量会比较少。

- 迪卡侬299的50l也可以上

- 
- 
- 
- 
- 

- ## [家用级主板能不能插双显卡？ - 知乎 _](https://www.zhihu.com/question/595962358)
- 这段时间正好在研究这个，也是想找个双显卡的方案。御三家的主板看了个遍，三家intel 7系主板里支持双显卡的最便宜的主板是 ￼￼[华硕ProArt Z790-CREATOR] ，4200元，支持 [PCIe 5.0]  16x/0 和 8x/8x 两种模式。其他支持双显卡的主板都要5000以上了。
  - 其他品牌的主板也看了些，华擎太极看介绍也能支持双显卡，但没看到哪里有卖，估计也不便宜的。
- 确实如此。想双显卡主板不能差了，最好得是双PCIe5.0 16X的，要不然第二个显卡速度直接慢一截，但价位直接5000了。

- 你这个需求应该去买X570带pcie bifurcation的主板，因为z690、z790和amd新的x670上了pcie5.0，5.0的拆分芯片非常昂贵，只有旗舰才会用，4.0的拆分芯片相对便宜。买个rog strix x570e就行了

- ## 🌰 [CoolerMaster Qube 500 with dual GPUs : r/mffpc _202507](https://www.reddit.com/r/mffpc/comments/1m3x31m/coolermaster_qube_500_with_dual_gpus/)
  - CPU: Ryzen 5 9600X 
  - GPU1: RTX 5070 12Gb 
  - GPU2: RTX 5060 16Gb 
  - Mboard: ASRock B650M 
  - RAM: Crucial 32Gb DDR5 6400 CL32 
  - SSD: Lexar NM1090 Pro 2Tb 
  - Cooler: Thermalright Peerless Assassin 120 风冷
  - PSU: Lian Li Edge 1200W Gold
  - case: QUBE 500 Flatpack Black & White Edition | Cooler Master, 33.5L
  - Will be updating it to a Core Ultra 9 285K, Z890 mobo and 96Gb RAM next week, but already doing productive work and having fun with it.

- Did you mount the PSU to the front panel of the case?
  - Yep, t’s the standard PSU bracket, in the top position, giving more room underneath for cables and gpu. It sits right up close to front panel, yes. Very nice case, super easy to build in.

- [Dual GPU set up was surprisingly easy : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1m3xgjo/dual_gpu_set_up_was_surprisingly_easy/)
- How's your temperatures with that thing during use?
  - Excellent so far with this biggish case and the decent size air cooler for the CPU, and plenty of room to add more fans if needed.

- is there any reason you're going for an Intel core ultra? 
  - For LLMs, Intel can have a bit of an edge with DDR5 bandwidth.
  - Ryzen memory bandwidth on AM5 is bottlenecked by the infinity fabric, which means you don’t get the full speed of dual channel DDR5. Intel doesn’t have this bottleneck, so you’d get the full bandwidth.
  - Of course this is only relevant if you’re wanting to load models larger than your VRAM. In my case I got 96GB of DDR5-6000 for occasionally loading massive models (eg Mistral Large 123B), but I don’t get the full 96GB/s theoretical bandwidth, it’s closer to 60GB/s due to the infinity fabric bottleneck.

- [Updated: Dual GPUs in a Qube 500 : r/mffpc _202508](https://www.reddit.com/r/mffpc/comments/1mmebz9/updated_dual_gpus_in_a_qube_500/)
  - CPU: Core Ultra 9 285K, 
  - MBD: Gigabyte Z890 Aero G ATX, 
  - RAM: 256Gb (4x64) Crucial DDR5 5600MHz CL46 ( with four memory sticks it’s stabilised at 5200MHz), 
  - GPU1: RTX 5070ti 16Gb, 
  - GPU2: RTX 5060ti 16Gb, both GPUs run at x8 smoothly
  - ssd * 3
  - PSU: Lian Li Edge 1200W 80+ Gold, 
  - Case: CoolerMaster Qube 500 (33 litres).
  - Getting 125+ TPS with GPT-OSS 20b, so pretty happy.

- I just bought the Qube 500 and plan on putting my rig into it. I have similar specs to yours, including a Lian Li Edge PSU (mine is 1000W). I’m worried about its size and fit in the case, especially with my 5070ti Gigabyte Gaming OC gpu. Did you run into a lot of issues from the size of the PSU? Did you have to mod anything to make it all work?
  - Yes it fits and works, no mods required, but there’s two options. There a series of rungs for the placement of the psu. 1. The top rung is harder to do, you have to push and shove the clips and the cables from the front panel a bit to get it in, but then as the psu is higher in the case, there’s better clearance of all the psu cables above the gpu. 2. Or, the second from the top rung, which is easier to fit in, but as the psu is lower then the power cables may be a bit cramped by the gpu.
  - I started with 2, then changed to 1, and recommend you start the same way. Depending on the length of your gpu, option 2 may be just fine.

- ## [为什么光威这个牌子的内存这么便宜? - 知乎](https://www.zhihu.com/question/310230307/answers/updated)
- 便宜的原因也不外乎于牌子新，品控略不如巨头。
  - 但是内存终身质保啊，你怕啥。我甚至遇到过停产的型号他们还给原价退款的，还要什么自行车。

- 有稳定性需求的用户可以买ECC用不上普通内存

- 我家的，全天24小时开机，一直用的都是光威内存，从来没出过问题，
  - 光威内存在京东的销量超过20万条，销量仅次于市场第一品牌金士顿，
  - 再加上质保是“终身质保”只换不修，根本不用担心。

- 嘉合劲威旗下只有阿斯加特和光威

- 内存天下三分，美光副厂出品

- ## [Who builds PCs that can handle 70B local LLMs? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1io811j/who_builds_pcs_that_can_handle_70b_local_llms/)
- Ryzen Threadripper CPU with 4x 3090 (with used parts it was close to $3, 000)

- For setup #2, how do you run 4x 3090 and a Threadripper cpu with a single 1600w psu? Don't the 3090's power spike from what I hear?
  - Yes that's accurate, I have one 1600 watts PSU to power it all.
  - If you see my setup guide, I also power limit 3090s to 270 watts using nvidia-smi. 270 watts per 3090 is that sweet spot that I found. I walk through it in the video and it is linked in the video, but here it is for easy reference:

- ## 🆚 [Is the difference between CL28 and CL30 6000MHz RAM noticable? : r/buildapc _202506x](https://www.reddit.com/r/buildapc/comments/1lo5iu2/is_the_difference_between_cl28_and_cl30_6000mhz/)
  - And is the difference worth an additional 20 euros?

- Nope, definitely not worth that amount. Just stick with 6000mhz CL30.

- You get a couple more FPS at most, not worth the 20 euros. Spend that money on a game with the current Steam summer sales instead.

- It depends on the game engine design too. Sometimes it does and sometimes not so much. As that video mentions, it’s much less relevant on x3d CPUs. Extra cpu cache hides latency issues with ram for some workloads.
  - If you don’t run x3d parts or do an Intel build, ram latency matters a lot more

- Not really but will be slightly faster in a few games. 6000/30 is sweet spot according to AMD too. Cheap and a nobrainer for most people.
- 6400/28 or even 26 might give you a few percent however 6000/30 and 28 is pretty much the same.
- If used with a X3D CPU the memory is even less important. Don't overpay on memory!

- [6400mhz cl30 or 6000mhz cl28 for 9800x3d? (gaming) : r/overclocking](https://www.reddit.com/r/overclocking/comments/1gxzstd/6400mhz_cl30_or_6000mhz_cl28_for_9800x3d_gaming/)
  - DDR5-6400 CL30 > DDR5-6000 CL28, but its more likely your chip will run the 6000CL28 or 30, than 6400CL30 1:1. You are the mercy of the silicon lotery, its better to bet to lose.
  - I run that 6400 kit at 6200 cl26, zero stability issues.. just depends on how much you wana fiddle. It ran 6400 cl30 expo no problem. Also run 1:1 with infinity fabric at 2067 and 1.6V. Also this kit is Hynix A-die.

- ## 🧩 [What other supermicro boards are as good or better than: SUPERMICRO MBD-H12SSL-I-O ATX Server Motherboard AMD : r/homelab _202412](https://www.reddit.com/r/homelab/comments/1h59xtp/what_other_supermicro_boards_are_as_good_or/)
  - Using Epyc processors. Is there a better board? In this generation?

- Standard ones: H12dsi: dual processor, more PCIe and more ram slots
- Nonstandard:
  - H12ssw-ntr: 12 Ram slots on a single socket board
  - H12dsu: for u(ultra) server. Dual sockets with 24 Ram slots. 4 GPU power connectors.

- ## [Amd Epyc Genoa : r/LocalLLaMA _202406](https://www.reddit.com/r/LocalLLaMA/comments/1d5u33o/amd_epyc_genoa/)
  - I’m contemplating between buying a mac studio m2 192gb(or maybe waiting for the m4) or an amd epyc with about 750gb Ram.
- I have such a system with Epyc 9374F and 12 x 32GB of RAM. I'm quite pleased with its stability and performance, but remember that its 460.8 GB/s memory bandwidth is a theoretical value. On Aida64 I had around 375 GB/s. It's possible that Genoa CPUs with 12 CCDs (mine has 8 CCDs) will perform a bit better. Avoid CPUs with 4 CCDs, they have limited memory bandwidth. If you want estimated Q8 LLM generation performance simply divide the memory bandwidth value by the number of model parameters. So for Epyc Genoa and 400b model it will be around 1 t/s.

- Do you know if getting two sockets will double the speed?
  - I have no experience with dual-socket Epyc Genoa systems, but I remember talking to u/MadSpartus who ran llama.cpp on a dual Epyc Genoa system and it performed worse than my single-socket machine. You can ask him if he found any settings that improved the performance.
- I managed to just barely beat the single socket genoa with a dual socket by using numa tuning. Not worth it unfortunately. Only using llama.cpp though.

- Im running 9374F with 12x64gb dimms.
  - Deepseek R1 0528 with 671b runs on ollama at 7-8 tokens/s.
  - Deepseek R1 0528 8b qwen3, runs on ollama at ~45 tokens/s

- ## [My ugly beast - 64 core AMD EPYC 7763 w/ 160GB 8-channel DDR4 RAM, 3x3090 (72GB VRAM) & 6TB NVME storage : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gy7xp5/my_ugly_beast_64_core_amd_epyc_7763_w_160gb/)
  - All used parts, all in just under $4000 (technically about $3300 but I already had a 3090 prior to building this).
  - The EPYC 7763 is an engineering sample I found for $600, board is an open box supermicro h12ssl-i w/ 128 PCIE lanes. 
  - The 2 3090s I just waited patiently for deals and never paid over $650. $100 Used 1600W EVGA power supply on a dedicated 20A 120V branch circuit. DDR4 RAM is crazy cheap used, though I didn't go for the fastest. No thermal or power issues, I didn't even need to power limit the cards. 
- llm
  - 15.6 tokens/sec on qwen 72b (Q4_K_M w/ 32k context) 
  - 27.5 tokens/sec on qwen 32b (Q6_K w/ 32k context)

- ## [ATX LGA 2011 single cpu motherboard with 8 DDR3 slots supporting 256GB RAM? : r/buildapc _202309](https://www.reddit.com/r/buildapc/comments/1682clw/atx_lga_2011_single_cpu_motherboard_with_8_ddr3/)
  - I am looking for an affordable ATX LGA 2011 motherboard with 8 DDR3 slots that will safely fit into normal ATX case (e.g., Chieftec ba-01) and support 1 CPU, ideally Xeon v2 or maybe v3 if needed
  - Chieftec ba-01: 540mm x 205mm x 650mm

- I found the following ATX motherboards with 8 DDR3 slots that could work, although not all of them will support 256GB RAM, depending mostly on their latest BIOS updates. On top of that, given that most of them are consumer boards, they usually do not support ECC memories.
  - MSI X79A-GD45 Plus
  - MSI Big Bang-XPower II
  - Gigabyte GA-X79-UP4
  - Gigabyte GA-X79S-UP5-WIFI (does not support registered ecc, only unbuffered)
  - ASUS X79-Deluxe
  - ASUS P9X79, P9X79-E WS
  - ASRock X79 Extreme6, X79 Extreme9
  - Supermicro X9SRi-F
  - Supermicro X9SRA
- Due to the potential ECC issues, I eventually went with Supermicro X9SRi-F, which works really well for my purposes (256 GB RAM with no problem) and later got my hands on Supermicro X9DRI-F, which I haven't tested properly, but should work fine too.
  - In the meantime, I experienced a short episode with Jingsha X99, that is in some ways more modern (m2 ports, for example) and worked semi-well, but in comparison to Supermicro, I found the lack of support and fiddling with drivers rather discouraging.
- Same, the problem was with AliExpress x79 cheap dual socket mbrd, problem was with USB 3.0 ports(which in my case was very important).so I was searching something to change

- ## [DDR5-compatible motherboards with 8 RAM slots? : r/buildapc _202312](https://www.reddit.com/r/buildapc/comments/18lmms0/ddr5compatible_motherboards_with_8_ram_slots/)
- you'll need hedt or server hardware.

- Get a threadripper 7000 motherboard. It’s a really expensive platform, but I doubt cost is your primary concern here.
  - Recent epyc and xeon platforms are also options, but Threadripper would be my recommendation.

- ## [Show me your AI rig! : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1fqwler/show_me_your_ai_rig/)
- With enough memory bandwidth and a recent CPU you can run very large models like Llama 405B in main memory and get 4 tp/s or so. You can roughly calculate it by dividing model size by memory bandwidth. Make sure you get fast RDIMMs, ideally 3200 otherwise your TPS will suffer. Without enough RAM you'll be running smaller, usually inferior models.

- I bought a used Epyc 7282, but your 7F52 looks a bit nicer! 
  - Definitely try to populate all 8 slots of RAM, this board/CPU supports 8 channels, so you can really up your memory bandwidth doing that. I am going to run 8x 32GB PC 3200 RDIMMS. 
  - If you are running DDR4 3200, you get 25.6 GB/s of memory bandwidth per channel, so if you are only single channel or dual channel now, going to 8 could take you from 25 or 50 GB/s to 205 GB/s!

- You should fill all 8 slots with a Ram module of the same size, so your total Ram would be either 128 or 256 GB. Your Cpu has a maximal memory bandwidth of 200 GB/s.

- ## [Epyc Turin (9355P) + 256 GB / 5600 mhz - Some CPU Inference Numbers : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ihpzn2/epyc_turin_9355p_256_gb_5600_mhz_some_cpu/)
  - I decided that three RTX 3090s janked together with brackets and risers just wasn’t enough; I wanted a cleaner setup and a fourth 3090.
  - My requirements were: at least four double-spaced PCIe x16 slots, ample high-speed storage interfaces, and ideally, high memory bandwidth to enable some level of CPU offloading without tanking inference speed. Intel’s new Xeon lineup didn’t appeal to me, the P/E core setup seems more geared towards datacenters, and the pricing was brutal. Initially, I considered Epyc Genoa, but with the launch of Turin and its Zen 5 cores plus higher DDR5 speeds, I decided to go straight for it.
  - Due to the size of the SP5 socket and its 12 memory channels, boards with full 12-channel support sacrifice PCIe slots. The only board that meets my PCIe requirements, the ASRock GENOAD8X-2T/TCM, has just 8 DIMM slots, meaning we have to say goodbye to four whole memory channels.
  - Getting it up and running was an adventure. At the time, ASRock hadn’t released any Turin-compatible BIOS ROMs, despite claiming that an update to 10.03 was required
  - CPU: Epyc Turin 9355P - 32 Cores (8 CCD), 256 MB cache, 3.55 GHz Boosting 4.4 GHz - $3000 USD from cafe.electronics on Ebay (now ~$3300 USD).
  - RAM: 256 GB Corsair WS (CMA256GX5M8B5600C40) @ 5600 MHz - $1499 CAD (now ~$2400 - WTF!)
  - Asrock GENOAD8X-2T/TCM Motherboard - ~$1500 CAD but going up in price

- Please add the likwid-bench memory bandwidth test results, as PassMark is known for its tendency to overstate the value in its memory threaded test. 
  - Theoretical max for 8-channel 5600 RAM is 358.4 GB/s and it shows 431 GB/s. This may be misleading.

- ## 🧮💡 [Comparing Threadripper 7000 memory bandwidth for all models : r/threadripper _202402](https://www.reddit.com/r/threadripper/comments/1azmkvg/comparing_threadripper_7000_memory_bandwidth_for/)
  - 7945WX and 7955WX (2 CCDs, 8 memory channels) have the lowest Memory Threaded test results (~102 GB/s). 
  - Next, we have 7960X and 7970X (4 CCDs, 4 memory channels), and we can observe a moderate increase in test results (167 GB/s, 179 GB/s). 
  - The results for 7965WX and 7975WX (4 CCDs, 8 memory channels) again are a little higher (236 GB/s, 246 GB/s) compared to the non-PRO models, It's definitely not a 2x bandwidth increase compared to the corresponding non-PRO models. 
  - Only when we compare the models with 8 CCDs: 7980X and 7985X, there is around 90% increase in the test result (240 GB/s vs 453 GB/s). Finally, 7995WX (12 CCDs) has the best performance in this test.
  - 🤔 The overall conclusion is that the lower-end models with 2-4 CCDs have limited memory bandwidth. We had the same situation in previous Threadripper generations. If you need a lot of bandwidth, you probably should use EPYC.

- we need to make a distinction between
  - the bandwidth between memory modules and the memory controller, 
  - the bandwidth between the memory controller and CCDs (where CPU cores are).
- These bandwidths are two independent things and they both affect the total available memory bandwidth in the system. Overall theoretical available memory bandwidth is the lower value from the two.
- First, we have the bandwidth between memory modules and the memory controller. 
  - I calculated the total available bandwidth for various numbers of memory modules (for 4x, 8x, and 12x configurations) and memory speeds (4800 MT/s is the default for EPYC Genoa, 5200 MT/s is the default for Threadripper 7000, 7200 MT/s is commercially available overclocked memory for TRX50 and WRX90).
  - This is how much bandwidth is theoretically available. It's nice that we can use overclocked memory in Threadripper since 8 7200 MT/s sticks will give us the same bandwidth as 12 4800 MT/s sticks in Epyc.
- The second bandwidth is the bandwidth of the GMI3 links between the memory controller and CCDs. 
  - Let's calculate how much bandwidth we have depending on the number of CCDs in the CPU. I assumed an FCLK of 1.8 GHz, so a single GMI3 link has 57.6 GB/s read bandwidth.
- Each CCD is connected with I/O die containing the memory controller with a GMI3 link, and this link has limited bandwidth. All CPU cores within a single CCD use this GMI3 link for memory access. So the more CCDs in CPU, the higher is the number of GMI3 links to the I/O die

- 📌 To get the best memory bandwidth, (theoretically) you should:
  - Increase FCLK for 8-channel configurations with 2 or 4 CCDs (7945WX, 7955WX, 7965WX, 7975WX), 
  - Use overclocked memory in all remaining Threadripper models, 
  - For Epyc, purchase a motherboard with 12 memory slots and an Epyc 9004 processor with at least 8 CCDs. Fill all memory slots.

- Another site (userbenchmark) mostly verifies what fairydreaming posted, shows a bit more improvement from 3000 to 7000, but lacks information on highly overclocked builds
  - Results are thin for the 7000 series (no 7945WX results) but the improvement from 3000 to 7000 appears more significant than using PassMark. Single-core more than doubled and multi-core up about 80%.

- Can you repeat this excercise for epyc processors?
  - I checked a few performance EPYC 9004 models that could be used in workstation builds: 
    - 9174F (16c) achieved 402 GB/s with 8 RAM modules, 
    - 9274F (32c) around 588 GB/s with 12 RAM modules, 
    - 9474F (64c) achieved 449 GB/s with unknown number of RAM modules.
- Thank you so much. Okay. So the 16 core epyc has 8 ccd… so the number of ccd is the memory bandwidth bottleneck. —- ryzen 7950x3d has memory threaded score of 54 MBytes/s. So the threadripper 7960x is the sweet spot for cost/clock speed/cores/167 MB bandwidth with around 3x mem bandwidth at a little over 2x cost of 8950x3d

- I can tell you the results of the threaded memory test that I found the PassMark database:
  - AMD EPYC 7F52 (16c Rome): ~145 GB/s (with 8 DDR4 RAM modules)
  - AMD EPYC 74F3 (24c Milan): ~217 GB/s (unknown number of DDR4 RAM modules)
  - AMD EPYC 9174F (16c Genoa) ~402 GB/s (with 8 DDR5 RAM modules)
  - AMD EPYC 9274F (32c Genoa) ~588 GB/s (with 12 DDR5 RAM modules)
  - All models have 8 CCDs.

- I checked a few performance EPYC 9004 models that could be used in workstation builds: 
  - 9174F (16c) achieved 402 GB/s with 8 RAM modules, 
  - 9274F (32c) around 588 GB/s with 12 RAM modules, 
  - 9474F (64c) achieved 449 GB/s with unknown number of RAM modules.

- Really wish I had seen this BEFORE I picked up my 7955WX. It's insane to me that this isn't more openly communicated somehow. Now I'm debating what my next path is. Switch to Epyc for additional bandwidth, or wait for a deal on Ebay to get a 7985WX or 7995WX.
  - I feel your pain. I purchased all components already and now IM LOST AS SHIT. Hoping vcolor will let me exchange the 256 6400 ram.

- 
- 
- 
- 
- 
- 
- 
- 

- ## 🤔 [EPYC/Threadripper CCD Memory Bandwidth Scaling : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nesi8g/epycthreadripper_ccd_memory_bandwidth_scaling/)
  - There's been a lot of discussion around how EPYC and Threadripper memory bandwidth can be limited by the CCD quantity of the CPU used. What I haven't seen discussed is how that scales with the quantity of populated memory slots. 
  - Would populating 2 dimms on an 8 channel or 12 channel capable system only give you 1/4 or 1/6th of the GMILink-Limited bandwidth (25 GB/s or 17GB/s) or would it be closer to the bandwidth of dual channel 6400MT memory (also ~100GB/s) that consumer platforms like AM5 can achieve.

- Theoretical total memory bandwidth is straightforward. For example, AMD EPYC 9XXX with 12 memory channels is 614 GB/s with 6400 MT/s DIMM
  - (64 (DQ pins per DIMM) * 6.4Gbps speed per DQ pin * 12 channels ) / 8 = 614 GB/s
  - If there are 3 channels in each NUMA quad, that's 153.6GB/s already, well over 100GB/s BW available to CCD over GMI. CCD can access all 12 channels, but not all at once, so there is the memory wall.

- Ccd numbers is easy to tell. The desktop gaming cpu maxes out a dual channel ram system and this cpu has just 1 ccd. Which means you need atleast 1 ccd per 2 channels. So for a 12 channel epyc motherboard you need a cpu with atleast 6 ccds, although higher ccd options are preferable if you can afford them.

- I’m curious to ask, have you considered Intel Xeon? I myself am in the process of comparing Xeon 6 and EPYC 9005, and I hear conflicting reports on both. EPYC has more memory channels and higher bandwidth, whereas Intel has AMX instructions. So on the face of it, assuming that prompt processing happens on VRAM, EPYC appears to be the choice. However, I still hear from some people that Xeon is more widely deployed in inference infra due to inherent advantages in its architecture and less issues with NUMA, particularly in dual-socket configurations. I’d be interested to hear what you’ve come up with in regard to this during your own search.
  - I've been eyeing Xeon W7-3565X or AMD Epyc 9355P (same price tag), equivalent 32 core TR is just too expensive. From what I could tell Intel AMX does seem promising and further research suggest has much better memory BW/latency due to monolithic die for MCC CPU CKU (like 32 core).

- [AI: Memory Bandwidth comparison for selected DDR4 CPU’s _202410](https://phoenixgamedevelopment.com/blog/ai-memory-bandwidth-comparision-for-selected-ddr4-cpus/)
- I have purchased a Threadripper PRO 3955WX CPU for the purposes of building an LLM inference machine.
  - However, I have since discovered that there is a serious issue with using some Threadripper and Epyc CPU’s (Including the 3955wx) for this purpose.
- The issue is that these CPU’s use 2 CCD’s (Core Chiplet Dies), which substantially reduces the memory bandwidth.

- The fundamental issue is that in order to reach the maximum bandwidth of 8-Channel RAM (About 200 GB/s) it is necessary to have not just 8 Channels supported, but 8 CCD’s as well.
- Only extremely expensive CPU’s have 8 CCD’s.
  - The cheaper CPU’s have only 2, which effectively limits their ram bandwidth to quad channel speeds (Around 80-100 GB/s) or slightly more.

- At my price point, it seems that 4 CCDs with 8 Channels is basically the best that can be achieved. This means that the actual read/write speeds in the real world are in the region of 150 GB/s read 100 Gb/s Write.
  - It seems, based on my research, that there is no inherent difference between Threadripper/Pro and Epyc CPUs that have the same number of CCDs.

- ## 👀 [Filling up 12 memory channels on EPYC server with 6x dual-channel kits : r/homelab _202501](https://www.reddit.com/r/homelab/comments/1i0oait/filling_up_12_memory_channels_on_epyc_server_with/)
  - Anyone foresee any issues filling up the 12 channels on a 32-core 9384x EPYC cpu build with 6 kits of identical consumer grade non-ecc memory such as these?
- You can use normal desktop memory with Epyc but why spend all of that money on a Epyc cpu just to stick it with cheap non-ecc memory? It's like putting a RTX4090 with an i3 cpu. I'm also fairly certain that 12 DIMs would limit you to 2933MT/s or maybe 3200MT/s, I can't remember off the top of my head, but there is a limit.
  - Only RDIMMs and LRDIMMs work in any SP5 CPU. You absolutely cannot use UDIMMs or CUDIMMs and if you think you can, please link to a motherboard specs that shows it supported.
  - 1DPC is 4800MT for Genoa and is a 12 channel CPU, motherboards with 1 CPU and 24 DIMMs are 2DPC
  - 🧐 9384x is an 8 CCD CPU and will gain no performance benefit from having more than 8 DIMMs installed, although you can for more RAM
  - EDIT: e.g. motherboard showing 12DIMMs/1DPC at 4800 and only RDIMMs supported https://www.supermicro.com/en/products/motherboard/h13ssl-n
- Thanks. Good to know about lanes being tied to ccds.

- ## [AMD Epyc 4004 line - General Discussion - TrueNAS Community Forums _202405](https://forums.truenas.com/t/amd-epyc-4004-line/5183)
  - AMD recently released an Epyc CPU which fits into the AM5 socket. It does have the light weight iGPU and supports ECC memory, as well as lower power than some of the newer Epycs, (which seem to make great house heaters!).
  - When I brought up a thread in the old forum for ideal, low end CPU, one thing was I thought was required, were about 40 PCIe lanes. The AM5 socket only supports 28 lanes, 4 of which appear dedicated to the companion chip. For a lower end desktop, which is what the AM5 is designed for, 24 PCIe lanes for the user is fine.

- I agree about wanting 40 PCIe lanes. Especially when you may want to add a couple of 16x or 8x NVMe bifurcation cards, and maybe an 8x dGPU for transcoding or image analysis.

- Existing boards use the B650(E) chipset. Supermicro, AsRock Rack and Gigabyte have added “EPYC 4004” to the specifications of thier existing server Ryzen boards. SATA and USB ports would then depend on the chipset (typically 6 SATA with B650, and I don’t see much use for the X chipset here); USB4 would require an additional Maple Ridge or ASM4242 controller.

- ## [Do Epyc Processors Have Integrated Graphics? : r/AMDHelp](https://www.reddit.com/r/AMDHelp/comments/cgztk3/do_epyc_processors_have_integrated_graphics/)
- Epyc processors do not have integrated GPU's, even vGPU, or however you call them.

- I got EPYC 4124 have Integrated GPU but didn't get any after that, is that true?

- [AMD Epyc Rome Server CPUs - iGPU inside, support for hypervisors like ESX? : r/Amd](https://www.reddit.com/r/Amd/comments/ctcgf8/amd_epyc_rome_server_cpus_igpu_inside_support_for/)
- > all blue servers i saw got somewhere a iGPU in the CPU or on the Motherboard
  - IIRC all server motherboards have a small GPU chip, no server CPU has an iGPU, but I might be wrong. (Epyc doesn't have iGPU, motherboards do).

- [Why does this Amd Epyc motherboard (SuperMicro H11SSL-i) have a VGA out, if the cpu has no onboard graphics? It would also need a GPU card too right? : r/homelab](https://www.reddit.com/r/homelab/comments/u17mnu/why_does_this_amd_epyc_motherboard_supermicro/)
  - Many server boards have onboard graphics. Just a small 2D chip.

- ## 🌰 [Upgraded self-hosted AI server - Epyc, Supermicro, RTX3090x3, 256GB : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1d3dh4c/upgraded_selfhosted_ai_server_epyc_supermicro/)
  - moving from AM4 to Epyc. CPU/mb/GPU/RAM/frame purchased on Ebay. 
  - CPU - AMD Epyc 7F52 CPU
  - Motherboard - Supermicro H12SSL-i
  - RAM - 8x32GB DDR4 ECC Reg 3200 Mhz, DDR5 is only supported on Epyc 8000/9000 series, the Epyc 7001/7002/7003 lines only support DDR4.
  - 3 x RTX3090 Founders Edition, all on PCIE 4.0 x16 risers
  - Veddha 6GPU miner open frame: Veddha V3C 6-GPU Mining Case Aluminum Stackable
  - Proxmox RAID Z1 (mirrored) on 2 x Kingston 256GB SSD
  - Samsung 1TB m.2 NVME for VMs
  - Samsung 4TB SSD for models & data
  - Intel X540 T2 2 x RJ45 10GBe nic
  - Corsair HX1500i, 34.6 x 23.8 x 13.2 cm, 10.8L
  - Ollama running command-r-plus:latest eval rate 12 t/s, llama3:70b Q4_0 17 t/s, llama3:70b-instruct-q6_K 13.06 t/s

- ## [What’s the deal with all the cheap EPYC mobo +cpu + ram bundles selling from China? : r/homelab _202210](https://www.reddit.com/r/homelab/comments/yemiap/whats_the_deal_with_all_the_cheap_epyc_mobo_cpu/)
  - There are hundreds of these kinds of offers on eBay and elsewhere - at ridiculously low seeming prices Eg: AMD EPYC 7551P CPU 32 Cores + Supermicro H11SSL-i Motherboard +8x 8GB 2133P RAM
  - Are these a scam?
- More likely they're decommissioned hardware from data centre.
  - This has been asked multiple times. The answer is they're old and being decommissioned. 1st gen stuff has been available for cheap for a couple years, while second gen is starting to get cheap. It's not like people are shocked when they see a 1950x for less than a quarter of the original MSRP.

- ## [AMD EPYC 9004 series 1U chassis : r/homelab _202311](https://www.reddit.com/r/homelab/comments/17nopmx/amd_epyc_9004_series_1u_chassis/)
  - EPYC 4th AMD EPYC™ 9354P
  - Motherboard Supermicro H13SSL-NT
  - 256 GB RAM + M2 storage.
  - [The new EPCY 9004 CPU's look like a great option for a low(ish) power build. : r/homelab](https://www.reddit.com/r/homelab/comments/181e2u2/the_new_epcy_9004_cpus_look_like_a_great_option/)

- The board is listed as ATX so any case thats takes that size motherboard is on the table except for one thing - trying to find a suitable case.

- ## [Xeon 6230 or Epyc 8124P or 9124 for Homelab? - Hardware Hub / Build a PC - Level1Techs Forums _202502](https://forum.level1techs.com/t/xeon-6230-or-epyc-8124p-or-9124-for-homelab/225592)
  - I’m looking to build a server for my homelab (HV + NAS). I don’t see many comparisons or benchmarks for the 8004’s and lower end 9004’s. 
  - Epyc 8004 motherboards are still pretty limited. For various IO reasons, I don’t really love the current 8004 options (ie: ME03-CE0 & SIENAD8-2L2T), making me lean toward the 9124.
  - Used DDR4 ECC is so cheap that I can max out all six memory channels (6x64GB) right away. Which would be great for TrueNAS and my VM’s. With the Epyc’s, I would start with 2x64GB and wait for DDR5 ECC prices to drop, meaning more cost later. And who knows how long until they actually drop.

- ASUS S14NA-U12 is another 8004 motherboard option. I’ve no experience with any Epyc motherboard, but this looks nice and is a bit cheaper in EU

- I have a 8024P AMD EPYC running in my home lab on a Gigabyte ME03-CE0 motherboard with 6 16GB ECC DDR5 RDIMMs and storage.
  - It’s a bit weak (wish I had found a 8124P or even a 8324P if it was somewhat affordable), but gets the job done.

- ## [Asrock vs Supermicro - AMD Epyc Genoa : r/truenas _202406](https://www.reddit.com/r/truenas/comments/1dekxey/asrock_vs_supermicro_amd_epyc_genoa/)
  - I am looking to buy a new motherboard for my server (TrueNAS Scale) and am considering the following models: ASRock GENOAD8UD-2T/X550, Supermicro H13SSL-NT
  - My previous experiences with Supermicro motherboards have been very unpleasant. The IPMI port didn’t work, the PCIe card I installed for the network didn’t appear in BIOS, and a RAID card (purchased from a trusted company) had the same issue.

- I use the Supermicro H13SSL-NT with windows at this point, in a desktop case and everything is working fine. I have the epyc 9124. And windows desktop doesn't support the 10gbe broadcom adapter.  

- ## [What are the cheapest Intel/AMD CPUs supporting Quad-channel RAM in 2023? - Quora](https://www.quora.com/What-are-the-cheapest-Intel-AMD-CPUs-supporting-Quad-channel-RAM-in-2023)
- xeon w3 2423 the latest its like 400$ but has 4 channel memory

- There are a few different candidates, depending on whether you include old or second-hand components, and how you define “quad-channel”.
- Technically the Xeon E5 2620 is the cheapest CPU you can buy in 2023 with quad-channel support.
  - It’s a very weak 6-core server CPU from 2012, and you can buy one second-hand from Aliexpress for about $2 or £1.50
  - It supports quad-channel DDR3, both registered and unbuffered, but because it only supports DDR3, it’s not a good option
- Most modern laptop CPUs support quad-channel LPDDR RAM, because LPDDR channels are half as wide as DDR channels (32 bits vs 64 bits), so you can fit twice as many channels on a given CPU, though each channel has half as much bandwidth. 

- If you want a current-gen CPU with support for at least 4 full memory channels (at least 256-bit memory bus, at least 8 DDR5 sub-channels), the cheapest option is a 6-core Intel Xeon W3-2423 (4 channels) or 8-core AMD EPYC 8024P (6 channels) which both cost about $400 or £400.

- ## [Ryzen DDR5 Quad channel resources - Hardware Hub - Level1Techs Forums _202412](https://forum.level1techs.com/t/ryzen-ddr5-quad-channel-resources/221787)
- Check your motherboard’s QVL list for compatible memory kits.
  - It’s not the number of sticks, it’s the number of memory ranks. So you can typically do 4 single rank sticks or 2 dual rank sticks at EXPO speeds. 
  - The problem is consumer memory rarely specifies the number of ranks as they may swap suppliers based on what’s cheap/available.

- ## [Does a CPU with 2 memory channels support using 4 sticks of RAM? : r/buildapc](https://www.reddit.com/r/buildapc/comments/13d83mt/does_a_cpu_with_2_memory_channels_support_using_4/)
- It CAN use up to four sticks, yes. It's still dual channel, it's just double-populated dual-channel (true quad-channel RAM CPUs do exist, but it's highly unlikely you have one).
  - Finally, if it's a situation of DDR4, RAM is so goddamn cheap right now that if you want to go from 16GB (2x8GB) to 32GB (2x16GB), you can usually just sell your old kit on like ebay, and even after the fees, it's within a few dollars of the same net cost as if you bought another 2x8GB kit.

- ## 🆚👀 [Framework strix halo vs Epyc 9115 -- is Epyc better value? : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jo50iz/framework_strix_halo_vs_epyc_9115_is_epyc_better/)
  - I've put in a reservation for the Framework desktop motherboard, which is about $1800 with 128GiB ram, 256 GiB/sec bandwidth. 
- However, I was going through some server configurations, and found this:
  - Epyc 9115 -- 16-core, 12-channel memory, $799
  - Supermicro Motherboard w/ 12 DIMM slots -- $639
  - DDR5 6400 16GiB x 12 -- $1400
  - That would give me (12 channel x 64 bit wide per channel * 6400) 614.4 GiB/sec bandwidth, about 2.5x the Strix Halo motherboard configuration. Cost would be about 1k more, but getting 50% more memory too.
  - Now this would be doing CPU only inference, which I understand is mostly memory bandwidth bound anyway. Prompt processing would suffer, but I can also throw in a smaller sized GPU to use for prompt processing.

- That Epyc has just two CCD. Even if it uses 2 GMI3 links per CCD, it would be limited to 240 GB/s.
  - AMD has this fraud of advertising bandwidth between RAM and memory controller, even when it's severly bottlenecked by bandwidth between CPU and controller.
  - In order to obtain the advertised 9005 bandwidth you need to use the 12 or 16 CCD SKUs.

- 9115 costs less than 1k, not 10k. But it has just 2 CCD and probably its actual performance is much lower than expected. A way better choice would be the 9175F, which goes for 4k.
  - Or I would consider 9274F, if the price has reduced after 9275F launch.

- I was just going to reply 9175F is $2650 on Newegg and 16CCD. I might go for that instead. Thanks for the reply! Any RAM recommendations? And amount?
  - 9175F supports 12 channel memory, so you should look for a single-CPU 12-channel mobo. Theoretically, it should be able to benefit of memory up to 7200 MT/s, but without benchmarks is hard to say.

- The cheapest Epyc Turin that will give you more bandwidth would the 9225 at 2, 500 usd. (4 ccd)

- I regularly find the previous EPYC 9554 64-core CPU with 8x CCDs (measured at 390GB/sec on STREAM) listed for $2500-2900. This is the most value for money configuration I believe and it offers more computation FLOPs for prompt processing (~5 TFLOPS in AVX2 is my estimate).

- The reason to choose Epyc is for the PCIe lanes or amount of memory, i.e. you are planning to load up GPUs in it or want to run something that requires a lot of memory.
  - 🤔 If you only want the lanes you can go cheaper with an SP3, something like 7532 which is the cheapest 8 CCD second gen you can buy, an ATX motherboard gets you 7 total PCIe slots, and in something like the H12SSL 5 of which are 16x - you could put in 5 x16 GPUs and still have lanes to spare. Placing them will be tricky because two would have to be single width but you can use cables.
  - If amount of memory matters and you can live with lower speed then SP3 wins again, because you can easily get 512Gb RAM+ for less than the cost of pretty much anything in DDR5 - DDR5 RDIMMs are eye wateringly expensive. Depending on what you're doing you may get similar or better memory bandwidth out of a 7532 compared to the low CCD count SP5.

- If you want to get a versatile CPU for other tasks as well, the previous gen AMD Epyc 9554 is better value imo (regularly under $2900) with 64 cores (~5 TFLOPS) and measured at 390GB/sec on STREAM. It achieves this with DDR5 4800 which is cheaper as well.

- Just get 5 7900 XTX. Strix Halo sucks big time in those machine where the motherboard does not support ECC. I hope some Strix Halo provider will finally create a ECC memory supported device
  - The HP Z2 G1a has ECC

- Early leaks point to Medusa Halo using a 384 bit bus, posdibly even LPDDR6.

- The 9015 was tested at 240GB/s on STREAM. I doubt that the 9115 will be much higher than that so you should temper your expectations

- ## 🧮💡 [Is DDR4 3200 MHz Any Good for Local LLMs, or It's Just Too Slow Compared to GDDR6X/7 VRAM and DDR5 RAM? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1ndg19v/is_ddr4_3200_mhz_any_good_for_local_llms_or_its/)
- For those wondering DRAM memory bandwidth can usually be calculated using following formula:
  - MT/s x 8bytes x memory channels / 1024 
  - So 3200MT/s x 8bytes x 2 channels / 1024 = 50GB/s

- Well, not only is DDR4 considered slow, it's more a question of how many memory channels you have got. 
  - Chances are that it's not going to be very many, it but really depends on the hardware you have. 
  - The rule is that each transaction is 64 bits or 8 bytes wide, so 3200 MT/s where T is for transactions means 3.2 GT/s can be performed by the hardware, and 3.2 GT/s * 8 B/T gives you 25.6 GB/s per channel. 
  - DDR5 is not hugely faster in this scale, e.g. you might have 6400 MT/s DDR5, which also has 64-bit transactions and thus double the data rate. 
  - Multiple memory channels is how you take these raw results in 50 GB/s order to the 200+ GB/s data transfer rates where inference starts to become practical. 4 are probably required, 8 or 12 is better.

- A common mistake is that something like am5 has only 2 memory channels but 4 slots for ram. This means that even with 4 sticks you only get 2 stick bandwidth (probably at an even lower speed). Make sure you check what your cpu is capable of.

- It isn't going to be as fast as pure vram obviously, but if you're using moe models it works better than you'd think. Having 256GB of ram with a large moe will do good, even with just 24GB of vram. You also can partially offload a dense model but still have super fast input prompt processing. 
  - My desktop computer for example is 96GB of system ram and 24GB of vram. I can run a 70B or a 100B model, process 200, 000 tokens of input within a couple minutes, and wait for slower tk/s but much shorter output.
  - I also use llms on my laptop that only has 2 channel 64GB ddr4 at 3200mhz. No gpu. I'm getting 2.5 tokens/sec with GLM 4.5 air @ 3Q right now. Not fast by any means but not impractical. I just let it do it's thing for a couple minutes and come back for the answer.

- I've was here not long ago as I upgraded to 128 GB of ddr4 3200 ram. The Qwen3 235B Q2 (Need 96GB ram) runs at 3.7 tk/s and with the Qwen3 235B Q4 (128GB ram) I get 2.2 tk/s. So yes very slow.

- VRAM > [LPDDR5X > DDR5 > DDR4] > Disk

- [What is the theoretical data rate limit of a DDR5 DIMM slot? : r/hardware _202106](https://www.reddit.com/r/hardware/comments/nxvsk7/what_is_the_theoretical_data_rate_limit_of_a_ddr5/)
- ram is overclockable. But first theres something you need to understand about ram speed: the MHZ speed you see listed on ram is not the actual clockspeed , the real clock is half but since modern ram is DDR (Double Data Rate), everyone advertises the 'effective clockspeed ' , which is actually the transfer rate as measured in MT/s (Mega transfers per second).
- Now each dimm slot is a 64 bit wide bus so to get the theoretical data rate, you simply take the transfer rate times the bus width , so for example with 1 dimm of '3200 mhz ram' aka 3200 MT/s ram, thats 3200 * 64 = 204, 800 Mbps or 25, 600 MBps.

- ## [Which motherboards support quad channel memory : r/buildapc](https://www.reddit.com/r/buildapc/comments/sw22cg/which_motherboards_support_quad_channel_memory/)
- Note that it's not enough for the board to support it. The CPU has to as well. Most consumer ones do not.
  - Boards that support quad channel only support CPUs that also support quad channel. 

- ## 🌰🖥️ [Built a Powerful and Silent AMD EPYC Home Server with My Kids (for a Fraction of the Price!) : r/homelab _202412](https://www.reddit.com/r/homelab/comments/1hmnnwg/built_a_powerful_and_silent_amd_epyc_home_server/)
  - we built a beast of a home server powered by an AMD EPYC 7C13 (3rd gen).
  - CPU - AMD EPYC Milan 7C13 64C/128T 2.2GHz SP3 (100-000000335 7763 7713)	
  - Motherboard - Supermicro H12SSL-NT SP3 AMD EPYC DDR4 ECC	
  - RAM - Samsung 64GB DDR4 LRDIMM ECC x8 (512GB Total), DDR4 RAM: Delivers 130GB/sec bandwidth.
  - Case - Fractal Design North Tempered Glass ATX Mid-Tower Computer Case - White/Oak: 433 x 215 x 450 mm, 41L; 从图片看，机箱有点大
  - CPU Cooler - Noctua NH-U14S TR4-SP3 (Premium-Grade)	
  - PSU - 850W SFX (ATX 3.0, PCIE 5.0 Ready, 80 Plus Gold)	
  - SSD - Samsung 990 Pro 1TB (7450 MB/s Read)	

- Regarding the CPU, I see some active listings on eBay – try searching for "AMD EPYC Milan 7B13" (or 7C13) for the same price range. Just a heads-up, though – there are engineering sample (ES) listings on eBay. Keep in mind that confidential computing (AMD SEV-SNP) won’t work on those CPUs, and there might be other feature limitations or performance issues that I’m not fully aware of.

- I've worked as a pc technician for a few years and built & repaired many machines over the years. In my experience, I would turn the cooler 90° that the airflow matches the direction of the intake fans in the front. If you ever want to add a gpu, then this layout works great. Depending on the temps, you might want an exhaust fan in the back or top

- ## [Mini ITX EPYC 64 core 128 thread SFF Build : r/homelab _202311](https://www.reddit.com/r/homelab/comments/182i7k3/mini_itx_epyc_64_core_128_thread_sff_build/)
  - Case Cooler Master Nr200: 360 x 185 x 274mm, 18.25L
  - ASRock Rack ROMED4ID-2T Deep Mini ITX motherboard.
  - Noctua NH-U12S TR4-SP3 cooler. 猫头鹰 风扇
  - AMD EPYC ROME SP3 ZEN2 7662 64-Core 128 thread
  - 256gb DDR4 RAM.
  - 4tb NVME Drive.
  - Running ESXI vSphere 8 with VCenter Server 8.
  - Ruining like a champ temps in the 40-50c range, headless server with IPMI OOB management and remote console.
  - Putting these similar spec parts in a cart on Newegg says $5101.52.
- I’m guessing the cpu / mb / memory probably cost around $1000 on the used market. I just built a similar system second hand.. hard to beat the value!

- They make Mini ITX EPIC boards? That is wild.
  - They’re not true ITX. They are Deep ITX (wider than ITX, closer to mATX, but the same height as ITX).

- 🆚 what's the difference between RDIMM and LRDIMM?
  - [UDIMM, RDIMM, and LRDIMM | Exxact Blog](https://www.exxactcorp.com/blog/HPC/differences-between-dual-in-line-memory-modules-rdimm-vs-lrdimm)
  - A DIMM (Dual In-line Memory Module) is the physical memory stick that houses DRAM (Dynamic Random-Access Memory) chips. These chips serve as RAM, the volatile memory pool CPUs use to quickly access data during tasks.
  - UDIMM (Unbuffered DIMM): Standard in desktops and laptops. Affordable, simple, and designed for everyday tasks like browsing, content consumption, and productivity.
  - RDIMM & LRDIMM: Specialized modules designed for servers and enterprise workloads, offering higher capacity and stability. These will be the focus of this guide.
  - Registered DIMMs (RDIMMs) are designed for greater stability and scalability than standard UDIMMs. They include a register buffer that improves signal integrity and reduces the electrical load on the memory controller. 
  - Load-Reduced DIMMs (LRDIMMs) push performance further by using advanced buffering to minimize electrical load and maximize capacity. They are built for systems that demand extreme memory density and efficiency.

- For the price of this even 2nd hand (~$1500 for 7662, $300 mobo) -- you could build three separate i9-12900k/ryzen-7900x systems which combined would be about 2.5x-3x the total compute of this
  - This motherboard doesn't even get you the PCIe lanes.
  - 3x the compute but also a lot more power and maintenance. There's a reason hyperscalers use Epycs for x86.

- How's the noise?
  - I put in 4 noctua fans, and it's silent. Along with the 2 cooler master fans that came with the case and its dead silent. Although I need to put more VMS and put it to the test.

- ## [[PC] AMD EPYC Milan (7763) 64c/128t Build : r/homelabsales _202501](https://www.reddit.com/r/homelabsales/comments/1ht1fdu/pc_amd_epyc_milan_7763_64c128t_build/)
  - Got an email yesterday saying electricity rates in my area are increasing. My wife gave me the look after looking at the power bill for this month (and looking over previous months...) so I'm looking into downsizing my homelab.
  - AMD EPYC 7J13 (Oracle rebrand of the 7763 with slightly higher clocks) 64 core / 128 thread CPU
  - ASRock Rack ROMED8-2T motherboard (with Intel NICs)
  - 512GB (8x64GB) DDR4 3200 Registered ECC RAM (MICRON MTA36ASF8G72PZ)
  - ARCTIC Freezer 4U heatsink
  - ICY DOCK ToughArmor MB720MK-B 4x NVMe enclosure w/ OCuLink PCIe splitter card
  - ASUS Hyper M2 PCIe 4.0 card with 2x Optane P1600X 118GB + 2x Samsung 970 EVO 1TB
  - Intel X710-DA2 10G card
  - Intel Arc A380
  - Corsair HX1000i 1000W power supply
  - Prices seem to be all over the place for the CPU and motherboard, but the RAM prices seem to be stable. I was thinking in the ballpark of $3000 for everything?

- My energy rates went up too. My solution was to buy 8 more solar panels.

- ["Sleepy Chungus"... AMD EPYC 7763 w/ 64x cores, 128 threads @ 2.450GHz in a GEEEK A30 V2 && 128GB of Quad Channel, Dual Rank, 3200MT ECC REG RAM (linux sffpc, btw) : r/sffpc _202209](https://www.reddit.com/r/sffpc/comments/x6phtn/sleepy_chungus_amd_epyc_7763_w_64x_cores_128/)
- I'm not sure if it is called sffpc with that psu and chonky cooler.

- ## [Need expert recommendations for a scalable, portable midrange AI hardware setup (2025) : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o3p83a/need_expert_recommendations_for_a_scalable/)
  - My goal is to start with a solid midrange setup that is truly expandable — meaning I want to be able to add more GPUs, RAM, and storage later on without major hassle
  - CPU: AMD Threadripper PRO or EPYC 7004 series for high core count and ECC support
  - GPU: NVIDIA RTX 4090 or RTX 6000 Ada for strong AI performance and CUDA compatibility
  - RAM: Minimum 128GB DDR5 ECC with at least 8 slots for future upgrades
  - Storage: NVMe SSDs (1TB system drive + multiple TBs for data with RAID options)
  - Mainboard: Supports multiple PCIe 5.0 x16 slots for GPU expansion, robust VRM for stable power delivery
  - Chassis: Portable midtower or flight case with good airflow and room for multiple GPUs
  - Power supply: 1200W or higher modular platinum rated PSU, with capacity for future GPU additions

- CPU & Motherboard: Maybe Epyc 9B14/9V84, or anything higher than 9354 if these "cloud" varients are not available, and pair it with a supermicro H13SSL-N(not sure whether MZ33-AR0 works). I think EMR Xeons (Xeon 6530 or "cloud" ones like 8555C) can be a cheaper replacement of Epyc, with fewer bandwidth, but it has AMX support.
  - RAM: Maybe 12x48=576GB DDR5 4800(for Zen4) or 8x 48GB=384GB DDR5 5600(for EMR)
  - Chassis: Maybe phanteks enthoo pro 2(or any ATX/E-ATX case with >=8 PCIe slots) or second hand server chassis.
  - Power supply: >=1600W platinum, depending on GPU
- why should the pc case have over 8 PCIE slots?
  - 4 x dual slot GPUs lead to 8, you can go standard ATX case with 7 slots if you only need dual GPUs.
  - For most single-socket modern server processors (Rome or later Epyc, Sapphire Rapids or later Xeon), 4 GPUs are a sweet spot. As the 80-128 PCIe lanes provided by server processor can adequately support 4 GPUs.

- If its for inference only i wouldnt put a lot of value on ECC, id prioritise ram speed . If youre going with threadripper pro it needs to be one of the top models to utilise the ram bandwith, if you cant afford those youll get more bang for your buck with a regular threadripper 

- For potable, Go to Mac Ultra M3 512 or await DGX Spark x2 EA

- I've been building systems for other people, sort of a "just-in-case" inference in a rugged case with 64-128gb vram, preloaded with models and data (wikipedia, army trauma medic guides, etc), and literally solar powered. Some customers have particular power budgets, so I'm not necessarily aiming for highest tok/s but lowest power per token/s or lowest idle power. It's not exactly in big demand, but I can speak more about it if there's interest..

- ## 🌰 [AMD EPYC mini-ITX build : r/sffpc _202207](https://www.reddit.com/r/sffpc/comments/w81afy/amd_epyc_miniitx_build/)
  - Case: Streacom DA2 V2, 340 x 286 x 180mm, 17.5L
  - Motherboard: Asrock ROMED4ID-2T
  - CPU: AMD EPYC 7443P, 24 Core, 48 Thread
  - RAM: 4x 64GB DDR4 PC4-25600 3200MHz LRDIMM ECC
  - PSU: Corsair SF Series SF600 SFX 600W
  - Boot SSD: Micron 3400 512GB NVMe M.2
  - Storage SSD: Samsung PM1723b 15.36TB NVMe U.2
  - CPU Cooler: Noctua NH-D9 DX-3647 w/ NM-AFB7b bracket for SP3
  - Exhaust Fan: Noctua NF-A9
  - Side Intake Fan: Noctua NF-F12
  - M.2 Cooler: Sabrent SB-HTSK
  - U.2 Cable: HighPoint Slim SAS SFF-8654 to 2x SFF-8639
  - TPM: Asrock TPM2-SLI
- About $5650 USD new, plus the cost of the bracket which I couldn't find. OP mentioned they bought the SSD slightly used, so probably closer to $5500

- With that PSU where it is, is it even possible to fit a GPU in there?
  - It's all been measured, 2x 40Gbps QSFP+ card is coming later

- Those are some absolutely eye watering specs (24 cores, 256gb, and a 15.36 TB ssd, I'm so jealous lmao). Truly a cut above. It's so cool to see enterprise hardware crammed into a boutique SFF.

- Only ASRock would make a mini ITX SP3 motherboard
  - Asrock rack is a true miracle, at least when I did my epyc server build, it was the only company that was selling mobos for epyc that wasn't stupidly overpriced, or required you to at least buy a barebones server (looking at you supermicro).

- Does epyc have igpu?
  - No, but the motherboard has a basic onboard GPU

- [AMD EPYC mini-ITX home hypervisor : r/homelab _202207](https://www.reddit.com/r/homelab/comments/w81bxe/amd_epyc_miniitx_home_hypervisor/)
- Some of the best features of Epyc are wasted in this configuration though. PCIE lanes, 8 channel memory etc..

- What is the power requirement for that?
  - The verdict @ 240V AC (I'm in the UK): 60-70W idle and 235W maxed out

- [如何在本地部署DeepSeek-R1模型？ - 知乎](https://www.zhihu.com/question/10630134422/answer/89240187608)
- 国外这个博主Matthew Carrigan 提供了在本地运行 Deepseek-R1 的完整硬件和软件配置，成本差不多是6000美元，token的output大概在6-8个每秒。
- 注意：这是纯CPU版本，GPU版本得10万美元+，所以也可以理解为穷鬼套餐。
  - 主板：技嘉MZ73-LM0/LM1（双路EPYC插槽，解锁24通道DDR5带宽）
  - 处理器：双路AMD EPYC 9004/9005系列（推荐9115/9015，性价比之选）
  - 内存：24×32GB DDR5-RDIMM（总量768GB，必须占满24通道！
  - 参考型号：vColor/Neumax）
  - 机箱：Enthoo Pro 2 Server版(支持服务器主板安装的消费级方案), 240 x 580 x 560 mm, 77L
  - 电源：实测功耗<400W，但需双CPU供电。海盗船HX1000i为稳妥选择（兼容型号可平替）
  - 散热：SP5插槽需特殊散热器（Ebay/Aliexpress专供型号实测可用），静音改造方案见Newegg
  - 存储：1TB+ NVMe SSD（700GB模型加载考验持续读写，PCIe4.0为佳）
  - BIOS设置：NUMA组数量设为0 → 内存全交错访问 → 吞吐性能翻倍

- ## [Is quad channel simply 4 sticks of ram together? | guru3D Forums _201203](https://forums.guru3d.com/threads/is-quad-channel-simply-4-sticks-of-ram-together.360222/)
- No, dual channel and quad channel are different.
  - To put this very simply, think of it like a road, dual channel gives you 2 lanes and quad channel gives you 4 lanes. This enables twice the traffic (data) to be sent because you've doubled the number of lanes (channels) the traffic can use to get where it's going.
  - For memory to work in dual channel you need a pair (or 2 pairs) of memory sticks and for quad channel you need 4 memory sticks (or 8 if there will be any motherboards that support 8 sticks?)

- but as you know lga775 and 1155 for eg have 4 dimm slots so if you put in 4 sticks of ram why is that still dual and not quad channel?
  - That's because it's what's supported by the chipset. X79 will be able to run quad channel, just like my x58 chipset supports tri channel and your x48 chipset only supports dual channel.
  - Just because you have 4 dimm slots doesn't mean you can run quad channel.

- quad is not just 4 sticks.

- ## [Memory Channels: Single, Dual, Triple, and Quad Channel Memory](https://storedbits.com/types-of-memory-channels/)
- Memory channels matter mainly for bandwidth and not directly the speed. It also doesn’t double your RAM size — but it can double the bandwidth, meaning more data can travel at once. That helps especially in tasks like gaming, video editing, or multitasking.

- What is a Memory Channel?
  - The CPU connects to the memory through a pathway. It is a dedicated data path between the CPU (or memory controller) and RAM modules (DIMMs). On the physical level, it is composed of copper traces (wires) etched into the motherboard, connecting the CPU socket (specifically, the memory controller) to the RAM slots (DIMMs).

- ## [为什么AMD霄龙EPYC最多只支持双路运行？ - 知乎](https://www.zhihu.com/question/7936434502)
- 处理器之间是需要高速信号互联的，每个都要和其他所有处理器有直接联系线（否则就准备好延迟爆表吧）。双路只要一根联系线。四路需要6根。八路需要。。。。每个u和其他7个一根，8*7根，由于A到B和B到A重复计算了，除以2，得到28根。这些连接线都是和内存布线一个难度的高速信号线，而且由于CPU插座的物理尺寸巨大，这些信号线还不得不变得极长，并且8路布线几乎无可避免地要与内存布线发生冲突，以至于根本没办法控制主板的成本。 

- 因为OEM厂家都反馈 4路，八路系统，全球一年卖不出100套。

- 霄龙单片处理器就是十二通道二十四条内存，俩处理器就是四十八条
  - 单个处理器就是128条pcie通道，两个就是256条，哪怕全塞都能塞32个，如果做成常规pciex16接口能塞16根，一般是不会配置这么多x16
  - 再多……主板塞不下啊，霄龙的设计本来就是单处理器塞海量核心和海量扩展，多ccd设计它单个处理器就类似多路处理器了

- ## 💡 [Local LLM Build with CPU and DDR5: Thoughts on how to build a Cost Effective Server : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kjvo1t/local_llm_build_with_cpu_and_ddr5_thoughts_on_how/)
  - DDR5 RAM: 576GB (4800MHz, 6 lanes) - Total Cost: $3, 500(230.4 gb of bandwidth)
  - CPU: AMD Epyc 8534p (64-core) - Cost: $2, 000 USD
  - 8xx Gen EPYC CPUs: Chosen for low TDP (thermal design power), resulting in minimal monthly electricity costs.
  - ASUS S14NA-U12 (imported from Germany) Features include 2x 25GB NICs for future-proof networking.
  - qwen3:32b-fp16: 1.14 tokens/s
  - qwen3:235b-a22b-q8_0: 2.70 tokens/s
  - deepseek-r1:671b_1.58bit: 3.26 tokens/s

- Older EPYC models (e.g., 9124) offer a balance between PCIe lane support and affordability.

- The GPU could be used to run attention layers and host kv cache. llama.cpp's -ot 'ffn=CPU' (or -ot 'exps=CPU' for MoE) is worth a try.

- While the hexa-channel DDR5 4800MHz configuration provides similar bandwidth to Epyc Milan's 8x 3200MHz DDR4 (204.8GB/s), Zen4 (c) might offers faster prefill performance due to AVX512 support.
  - You might want to offload MoE tensors using: `--override-tensor 'blk\.\d?\d\.ffn_.*_exps.weight=CPU'`

- Additionally, frameworks like ktransformers or ik-llamacpp are optimized for CPU-GPU hybrid inference.

- In China, there are OEM server processor options that offer comparable pricing to entry-level models while delivering significantly better prefill performance than 16-core alternatives. Notable affordable options include:
  - - **Intel**: Xeon 8455C (48C SPR 8xDDR5 4800MHz ~¥6, 000), 8481C (56C SPR ~¥7, 500), 8581C (60C EMR 8xDDR5 5600MHz ~¥9, 000)
 - **AMD**: Epyc 7B13 (64C Zen3 8xDDR4 3200MHz ~¥3, 800), Epyc 9v74 (80C Zen4 12xDDR5 4800MHz ~¥8, 500)
  - Beyond OEM models, the Epyc 9375F (32C Zen5 12x6000MHz) offers exceptional single-core performance and memory bandwidth, making it better for some tasks. 
- When comparing Intel and AMD platforms:
  - Intel's advantage lies in AMX instructions for prefill acceleration
  - AMD offers 12-channel DDR5 bandwidth and more PCIe lanes for multi-GPU setups

- ## 🆚📌 [Memory Bandwidth Comparisons - Planning Ahead : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1amepgy/memory_bandwidth_comparisons_planning_ahead/)
- Epyc actually has 12 channels of ram. The latest 9004 series has 460.8 GB/s. Threadripper is the one that comes with quad and octa channel variants.
  - Note: The upcoming Epycs(zen 5) are supposed to have even more bandwidth due to the new out-of-the-box ram speed being 6000mhz instead of the current 4800mhz
- 6000 MT/s would be nice, giving 4090-like memory bandwidth over 24 channels in a 2P system, but with a minimum of 384GB instead of a maximum of 24GB. That's assuming all else is equal/negligible, which isn't quite the case.
- Yeah, an ideal environment for sparse MoE like Mixtral

- Lpddr5x at 120gb/s I have a core ultra 7 155h with lpddr5 at 100gb/s. You can ask me for some tests if you want

- Is there any reason that regular consumer motherboards can't support quad or 8 channel RAM? I feel like if we can have 8 channels DDR6, we'd be at around 600 to 800GB/s, which is very similar to gpu vram speeds. Maybe this is what we should ask AMD to do instead of GPU's with 46gb or 96gb RAM for consumers at reasonable prices.
  - It would normalize everyone potentially having great bandwidth for local inference, wouldn't require a GPU at all, and would basically explode the number of devices that could locally inference at reasonable speed. This would open the flood gates for local llm's - open or closed source, because now everyone and their grandma would be able to use it effectively.
  - And unlike GPU's, you'd never be limited by how many GB's of RAM you want to install, and therefore not be dependent on NVIDIA (or whomever) to hopefully one day release a card with more VRAM. The power would go back to consumer. And the bandwidth would double again for DDR7 and so on.
  - I just don't know if putting quad or 8 channels on a motherboard is somehow difficult and can only done at high price to the consumer, which is why only pro-sumer or server level mobos do it.
- They could, but the main limiting factor is the memory controllers are on the CPU. Intel, AMD, and the others use number of channels as a market segmentation method. But ultimately it boils down to memory channels equal $$.

- The bandwidth numbers for the Apple M1/2/3 SoC are just the raw totals from the memory, but depending one which cluster is using it (P-cores, E-cores, GPU) they have their own limitations. Here is the explanation for the M1 series
  - On the M1 Max with 400GB/s the CPU can get maximum 204GB/s when using the P cores only or 243GB/s when using both the P and E cores.

- ## ⚡️📊📌 [有人可以做一个epyc服务器CPU的天梯榜吗？ - 知乎](https://www.zhihu.com/question/596966739)
- cpu, cinebench-r23, pricing
  - AMD Ryzen 9 7900x, 3.0w, 2469
  - AMD Ryzen 5 7500F, 1.4w, 938
  - AMD EPYC 7742/7B12, 5w, 6k
  - AMD EPYC 7552, 4.4w, 6k
  - AMD EPYC 7702, 4.9w, 7k
  - AMD EPYC 7b13/7c13/7v13/7763/7j13, 6.1w, 5850
  - AMD EPYC 9V74, 10.5w, 1.2w 
  - AMD EPYC 9654 ES, 11w, 1w 

- [AMD Server Processor Specifications](https://www.amd.com/en/products/specifications/server-processor.html)

- [Ryzen Threadripper - AMD - WikiChip](https://en.wikichip.org/wiki/amd/ryzen_threadripper)
  - 🎯 zen2(2019):
    - [Template:AMD Epyc 7002 series - Wikipedia](https://en.wikipedia.org/wiki/Template:AMD_Epyc_7002_series)
  - 🎯 zen3(202103): uni epyc 7313p/7443p/7543p/7713p; 
    - multi epyc 7313/7343/7443/7543/7713/7763
    - EPYC 7003 "Milan"
    - 8 channels per socket, up to 16 DIMMs, max. 4 TiB
    - Up to PC4-25600L (DDR4-3200)
    - [Zen 3 - Wikipedia](https://en.wikipedia.org/wiki/Zen_3)
    - [Template:AMD Epyc 7003 series - Wikipedia](https://en.wikipedia.org/wiki/Template:AMD_Epyc_7003_series)
  - 🎯 zen4(202211): uni epyc 9354P/9554p/9654p; 
    - multi epyc 9124/9174F/9224/9254/9454/9634/9654
    - lp/edge: 8324p/8324pn/8434p/8534p
    - EPYC 9004 "Genoa": 12 channels per socket, two 40-bit (32 data, 8 ECC)
    - DDR5 subchannels per channel
    - Up to 24 DIMMs, max. 6 TiB
    - Ryzen 7000 "Raphael"
    - 9124: 16-core (32-threads), 4 × CCD, I/OD, Base Clock3.0GHz, DDR5-4800, p-200w
    - 9224: 24-core (48-threads), 4 × CCD, I/OD, Base Clock2.5GHz, DDR5-4800, p-200w
    - 9254: 24-core (48-threads), 4 × CCD, I/OD, Base Clock2.9GHz, DDR5-4800, p-220w
    - EPYC 4004: 16 AMD ”Zen 4” cores, 32 threads, an L3 cache of 128MB, DDR5 memory support, and 28 PCIe® 5 lanes
      - Max DDR5 Freq (MHz) (1DPC): 5200
      - EPYC 4004 is just a rebrand of the Ryzen 7000 series, designed to make it clearer about ECC support mainly.
    - [Zen 4 - Wikipedia](https://en.wikipedia.org/wiki/Zen_4)
    - [Template:AMD Epyc 9004 Genoa - Wikipedia](https://en.wikipedia.org/wiki/Template:AMD_Epyc_9004_Genoa)
  - 🎯 zen5(202411): uni epyc 9015p/9125p/9355p/9755p
    - multi epyc 9005/9015/9115/9125/9175F/9335/9665/9755F
    - The series offers core counts ranging from 8 cores to 192 cores, 
    - with support for up to 12 channels of DDR5-6000 memory (up to 6 TiB per socket) and 128 PCIe 5.0 lanes
    - [Template:AMD Epyc 9005 series - Wikipedia](https://en.wikipedia.org/wiki/Template:AMD_Epyc_9005_series)
    - [Template:AMD EPYC 9000 Series - Wikipedia](https://en.wikipedia.org/wiki/Template:AMD_EPYC_9000_Series)

- [如何评价AMD EPYC 7B13, 7K83, 7T83, 7763? - 知乎](https://www.zhihu.com/question/542414897)
  - 这些都是7763的马甲，另外还有7J13，7V13等等。。。。可能频率设置上略有不同，TDP也都是280W，基本上满载性能是差不多的。
  - 各种云的定制版，云厂商有功耗，性能的需求，amd就帮他们定制

- 性能真强，说起来7r13最近好像降价了，感觉好像比7c13还强点。

- EPYC服务器基本上不需要调优，7003还有NPS设置，9004开始就没有了，内存频率只需要自动，自己调高必蓝屏。

- epyc很多都是用来跑cfd的，用这种跑分软件得出的结论完全是错的。都是用openfoam做benchmark对比，别说7950x了，我的9950x和我的epyc工作站比起来，都被秒到渣都不剩

- epyc系列的CPU，根本不需要做天梯图，性价比最高的应该就是7？83（7T83、7W83等）。1w出头就能拿下板+64核U。

- [EPYC或线程撕裂者或XEON有没有单核性能强又廉价的U? - 知乎](https://www.zhihu.com/question/1947237447466464324)
  - 目前是看了q30h/q2t7和ms03还有256g d内存，预算刚好卡的很死，不知道有没有啥更优的选择

- ## [I want a compact case. But the question is the motherboard Mini ITX there is 2 channels of RAM. 16+16 and 8+8+8+8 what is the difference in performance? : r/buildapc _202508](https://www.reddit.com/r/buildapc/comments/1msjal1/i_want_a_compact_case_but_the_question_is_the/)
- They're both dual channel. The four module configuration has two DIMMs per channel (2DPC). That config puts more stress on the memory controller, usually leading to slower speeds or reduced stability.

- ## [DDR5 2 vs 4 sticks, different speeds, same bandwidth? Confused : r/overclocking _202502](https://www.reddit.com/r/overclocking/comments/1ih0rfe/ddr5_2_vs_4_sticks_different_speeds_same/)
- 4 sticks will still run in dual channel. So 4x sticks @3600 will always be much slower than 2x sticks @6000
  - There are thousand of posts like this one Every week.
  - Just return 2x sticks or all 4x and just get 2x48 6000-6400MTs if you need high capacity & speed

- 2 sticks is the same bandwidth as 4 because each channel shares 2 lanes. You’re only getting half the bandwidth on each stick with 4. Not really all that much to it.

- ## [do you think i could run the new Qwen3-235B-A22B-Instruct-2507 quantised with 128gb ram + 24gb vram? : r/LocalLLM _202507](https://www.reddit.com/r/LocalLLM/comments/1m5wgcg/do_you_think_i_could_run_the_new/)
  - i am thinking about upgarding my pc from 96gb ram to 128gb ram. do you think i could run the new Qwen3-235B-A22B-Instruct-2507 quantised with 128gb ram + 24gb vram? it would be cool to run such a good model locally

- The old qwen3 235b model ran, at UD-Q4_K_XL, on my system with a R9 7950x and 96gb ram and a 4090 with 24 gb vram. ~5 t/s once it was warmed up. Processing speed was about the same though (X_X).
  - That's the best I got, so far. I tried a few different off-loading strategies, but just offloading to cpu for most of it and MMAPing the file was what did the best on my system with its constraints.

- You should be able to run the Q4 with that. How fast will it be will depend on what speed RAM you have.

- Someone ran qwen235b at iq4 on 2 sticks of 64gb ddr5 5600 with 3.5-4 tokens/s on cpu only (7950X).

- two amd mi50 & 128 gb ddr5 could gen 7 t/s With Qwen235b-Q4

- ## [How large models can I run with 128GB RAM? : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1cjtzft/how_large_models_can_i_run_with_128gb_ram/)
  - I currently have 16GB VRAM and 32GB RAM. I would be fine upgrading to 128GB RAM.
  - I can run 8B/13B-models without issues. Can I run larger models if I upgrade to 128GB? I would want to avoid buying more RAM unless it has any effect.

- I get 1.9 tokens/sec generation speed on wizardlm2 8x22b q5_k_m 128gb quad channel ddr 4 2133. No offloading to gpu.

- Adding more RAM will just allow you to run larger models ...on the CPU, which will be incredibly slow.

- ## [Mini-PC Dilemma: 96GB vs 128GB. How Much RAM is it worth buying? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nmlluu/minipc_dilemma_96gb_vs_128gb_how_much_ram_is_it/)
  - I'm planning to pick up one of the new mini-PCs powered by the AMD Ryzen AI Max+ 395 CPU, specifically the Bosgame M5. The 96GB RAM model looks more cost-effective, but I'm weighing whether it's worth spending ~15% more for the 128GB version.

- Get the 128 GB one. It's soldered RAM so not upgradable.
- Under Linux, you can use all the RAM with the GPU at full speed (215 GB/s).
  - That means qwen 235B A22B at Q3_K_XL at 15 tokens per second at 54 Watts.
- The ability to run up to 120 GB MoE models is likely to be increasingly useful as more are released.
  - It's also possible to run other models in Comfy UI but slow and unstable. This may improve when AMD makes rocm less uncompetitive with cuda.

- I have a pc with 192GB and I would use 256 if I would have purchase 4x64 instead. I run huge model (like DeepSeek-V3.1-UD-TQ1_0.gguf) on a 3090 + 172gb pc ram (ddr5) and I can get 'decent' around 3T/s, which I find acceptable since I can configure many parameters.
  - If you use GGUF versions of a model, you don't need 'pc' ram to be dedicated as a gpu, since the model can put part of the model on the pc ram by itself.

- ## 🆚 [Any downside to having 128GB of RAM on two 64GB sticks? : r/buildapc _202510](https://www.reddit.com/r/buildapc/comments/1nyso1u/any_downside_to_having_128gb_of_ram_on_two_64gb/)
  - should I split it into four 32GB sitcks or get two 64GB sticks? Is there a difference to performance? 
  - The specific product I am looking at is: Corsair Vengeance 128 GB (2 x 64 GB) DDR5-6400 CL42 Memory
  - I could get 4 32GB sticks instead. But I read that DDDR5 RAM doesn't play well on AM5 if all 4 sticks are utilized.(AM5 is the latest CPU socket from AMD for their Ryzen 7000, 8000, and 9000 series desktop processors, replacing the long-lived AM4 socket)

- You likely won't be able to run four sticks at 6400MHz, but there's a higher chance you will with two. It depends on your CPUs memory controller. I have 4x32GB 6000 CL30 and I regret not getting 2x64GB. You live and you learn, I guess.

- Much better performance-wise on two sticks than four for DDR5. Downside is lighter wallet lol

- You can buy a motherboard with 4 slots and only populate two of them. Dual slots ATX mobo are very rare
  - I have built and bought parts for at least a dozen pcs and i am pretty sure i have never seen a motherboard with 2 slots in my life
- It’s much more common in ITX boards though.
  - Only itx and ultra cheapo boards have 2 slots.
- All mini-ITX form factor board, a good chunk of the lowest end budget boards (ie stuff like A620 boards generally intended for low power office machines, that kind of thing), and a tiny few extremely high end OC boards (two slots to use larger traces and maximize stability at extreme OCs). You can just set the number of slots to 2 on PCPartPicker to see.

- If only people listened to Apple, and just accept whatever memory came on the device when they bought it
  - Shit, big Repair got to him in the middle of his sentence

- Maybe look into 2x48GB: 6000MT/s CL30 isn't extortionately priced.
  - 2x48 is your best bet. You won't have any performance penalties with that setup. 2x48 is no harder on the memory controller than 2x32.
  - I wouldn't take the performance hit of 128GB of RAM, when 96GB works so well. Unless you really need it, that is. I use my PC as a workstation for processing drone imagery into orthomosaic maps and 64GB is enough for mapping up to 150 acres. OpenDroneMap is pretty damn RAM hungry.
  - If you really need 128GB, you should still stick to 2 DIMMs. 2x64 is going to be much easier to get working and perform better than 4x32.

- 2 sticks have better performance than 4 sticks.

- As others are saying, dual channel is going to be significantly more stable (as opposed to 4x32).
  - If you’re just tinkering and have the funds, there are boards that support 196GB. Or you could jump up into professional stuff and go for 256GB.
  - All of this is assuming DDR5.

- There's not any specific significant downside, but some motherboards may not support a RAM with 64 GB per stick without a BIOS update.
  - those 64 GB sticks are slower than 32 GB sticks (6000 CL30 > 6400 CL42), as small as it might be.
  - If your PC is AM5, 6400 is highly not likely to boot with 1:1 setting. There's also going to be longer RAM training initially but that's just one time thing.
  - 99% of AM5 CPUs support 6000 at 1:1 speed, but any higher than that, the chance lowers noticeably, and 6400 1:1 is a crap shoot. It doesn't help it's a high-capacity 64 GB, dual rank stick, which puts even more stress on to the memory controller.
  - It's just the way AM5 CPU memory controllers roll. There's a G. Skill 128 GB set (2x 64GB) that is EXPO certified, at 6000 CL32, 34, or 36 that you can get instead. I have the CL34 one, then tightened RAM timings to get it down to 32-40-40-76.

- Most consumer motherboards are going to be duel channel RAM, which means there's only 2 lanes between the RAM and CPU. Duel channel motherboards with 4 RAM slots will have 2 slots share a lane, so in most cases you will get more performance out of 2 sticks then 4, as long as you follow the instruction in the manual and use the slots it tells you to put the RAM in (Often A2 and B2, but can be board specific).
  - Worth keeping in mind a lot of CPU/motherboards don't seem to like running large amounts of RAM at higher speeds, so while it might be rated for 6400MHz you might have to run it at 6000, so if there's a cheaper 6000MHz kit, especially one with a lower latency (CL42 part of the product you listed) I'd probably go for that. Having a quick look it seems common for CL40+ on 128GB kits though.
  - If you must have 128GB, look at something like the G. Skill Flare X5 128 GB (2 x 64 GB) DDR5-6000 CL32 Memory for lower latency, though depending on where you are lower latency kits might not be available. I can see a few CL32 128GB kits available on US pc part picker, but the lowest it shows in stock for the UK is CL34, still be an improvement over CL42.

- for some reason, 2x48gb 6400 CL32, is relatively easy to find
  - but once you go for 2x64gb, it's hard to find good timings.

- it's possible to get even 256GB of DDR5 to run on AM5, so 128GB should be no problem.. not at the same speeds you'll get with the "generic gaming choice of 32GB", ofc, but still.

- if you want 6400MHz, shoot for CL32
  - I believe that is the correct spread change for DDR5 above 6000MHz CL30

- I got 4 sticks CL30 Corsair Vengeance 4 x 32, could not get >5200Mhz stable with MSI Mag 870E + 9950x3D. Though running benchmarks, I ended up staying with this config instead of 2x48 @ 6000. There was negligible difference in any of my workloads, for work or for play, but I did benefit from the at the time, very drastic price difference, and the additional ram is useful in my use-cases.

- Why stop at 128gb when you can now do 256gb 6000MT? See Level1Techs video from 2 weeks ago.

- ## [有没有单条64G或者更高的内存条？ - 知乎](https://www.zhihu.com/question/518047029)
- 普通的DDR4内存单条32G到顶，要服务器用的RECC内存有单条256G, 512G的，当然，价格美丽，且需要主板支持
- 普通条也有64g
  - ddr4 有，ddr5不确定因为还没见到

- ## [为什么市面上没有单条64G的高频DDR5（8000MHz以上）？ - 知乎](https://www.zhihu.com/question/1932456730404587491)
- 你内存频率上去了，主板和CPU跟不上，白搭
- 4月份，芝奇就发布了一款DDR5-8000 128GB内存套装，也就是DDR5-8000 128GB（64GB x2），时序为CL44-58-58-127，不过这款内存条暂时还没有上市，属于第一款64G的DDR5-8000频率内存。
  - 4月份，芝奇就发布了一款DDR5-8000 128GB内存套装，也就是DDR5-8000 128GB（64GB x2），时序为CL44-58-58-127，不过这款内存条暂时还没有上市，属于第一款64G的DDR5-8000频率内存。
  - 现在DIY装机的主流依然是32G（16x2）DDR5 6000MT/s及以上频率和48G（24x2）DDR5 6000MT/s的内存条，即使你在某些生产力上面需要，也64G（32Gx2）DDR5就很足够了。
  - 正常你要是AMD的话，上套6000MT/s的DDR5就可以，而英特尔处理器的话，实际上套6800MT/s的DDR5就可以，所以不用纠结太多。

- 事实上呢，GSK4月份就发表了8000MHz的128GB套装和64GB的DDR5-9000MHz特挑套装，然而具体的供货呢？还是那些渠道才有，官方不会随便给价格，好方便他们漫天要价
  - 8000MHz超高容量比6400s的贵一倍或者两倍都是渠道商们随便喊。
  - 你要搞这种东西，其他部分可以先满上，然后坐等上货，毕竟芝奇的测试平台用的就是：
  - 处理器：Intel-265K/AMD 9950X3D
  - 主板：华硕玩家国度MAXIMUS Z890 APEX
  - 显卡：NV XPG RTX5090-24G

- ## [感觉华擎的东西做工用料都很扎实呀，为什么都说是二线？ - 知乎](https://www.zhihu.com/question/354822608)
- 华擎是现在公认的四大家，所有的跟主板相关的认证，一定是会通过华擎的认证的。
  - 在硬件支持上也一直保留自己的特色，接口和设计上一直都算是比较全且相当友好的。
  - 他最辉煌的时候应该是2011年，当年的销量冲破了1000万片，达到全球第三。
  - 前几年跟华硕分手导致的阵痛比较严重，不过自身产业转型升级很快，渠道上不太待见华擎，主要原因是不赚钱，没有补贴力度（深有体会，没有会议没有钱……）
  - 现在华擎在国内的份额只有2.8%，属实可怜，基本看不到了，而且华擎不接受个人送保，主板性价比极佳，但除非是京东自营，否则自己买，售后属实麻烦。
  - 代理商是不给予代保的（比如大仙，不是自己出的华擎主板坏了，是真的会拒绝代保）
  - 不过总销量依旧可观，全球主板出货量在2018年的时候是400万片左右，2019年好像有接近600万的出货量（数据存疑，因为找不到之前看到的数据了），相当可观，逆市增长那种。
  - 保持出货不跌的只有微星和华擎两个品牌。
  - 华擎是迄今为止，最友好的台湾系品牌商之一，中文网站访问和资料搜索都是最友好的，说出来一般人都可能不太相信。。

- 华擎支持个人送保，只需出来回运费

- 我个人感觉其实就是售后率，售后效率太扯淡了点。1所有主板售后得通过省代资格的手寄到深圳，再返回来，和微星有的一拼。
  - 从矿板就可看出售后率太高，前几年矿潮也就几K的矿板售后率硬是能大几百片，果真一分钱一分货。至今仓库里还10片矿板懒得售后也没人要，等过保修了卖垃圾。

- [如何评价华擎主板？ - 知乎](https://www.zhihu.com/question/27738363/answers/updated)

- ## [Mini server for virtualization with 128 GB ECC RAM, many CPU cores : r/selfhosted _202412](https://www.reddit.com/r/selfhosted/comments/1hbfay9/mini_server_for_virtualization_with_128_gb_ecc/)
- DDR5 is inherently ECC. You do not need explicit ECC, though the on-die ECC only protects the DRAM cells, not the link between the CPU and the RAM chips. So, run the bus slower (say, if you have LPDDR5X 7500, run it at 6400, if you have DDR5 5600, run it at 5200), and you will be fine.
  - with on-die ECC, you do not get early warning on ECC events, and you do not get unrecovered 2-bit ECC reports, so it's safer than no ECC, but not as safe as true ECC. You should not do ZFS RAM caching, for instance, with this setup. But most home server applications should be fine, though.
  - As for capacity, you can get 96GB easily. 128GB would be hard until vendors start making 64GB sticks. So far, the largest consumer grade sticks are 48GB. My setup is MS-A1+7950X+2x48GB+2x2TB+1x118GB Optane. It's been rock solid far.

- Minisforum MS01 ticks all the boxes except RAM. It can go up to 96GB, has 3 m.2 slots, a spare pcie slot, dual 10gbe SFP, dual 2.5gbe with one offering IPMI.

- I have been eyeing the Asrock B650M PG Riptide mATX board.
  - Supports AMD Ryzen™ 9000, 8000 and 7000 Series Processors
  - Supports 256GB DDR5 ECC/non-ECC, un-buffered memory up to 7200+(OC)
  - 2.5G Ethernet
  - 2 x 16x PCIe slots (One of which may only support x4)
  - 2 x M.2 Gen 4 slots
- AsRock DeskMeet seems similar. The motherboard doesn’t seem to support bifurcation to make use of PCIe slot for 4 NVMe, and there is no IPMI. Otherwise OKish, albeit 8 liters
  - I think you have to compromise if you want a small formfactor / non-server board. Have been struggling with the same compromises. But at least this have 2.5G Lan.
  - Bifurcation would have been nice.
  - I don't think it is going to be easy to find a small/non-server board with IPMI.

- ## [Mini ITX AM5 mobo that supports 2x64GB RAM sticks? : r/sffpc _202507](https://www.reddit.com/r/sffpc/comments/1m8wexd/mini_itx_am5_mobo_that_supports_2x64gb_ram_sticks/)
- check the SFF masterlist > mITX boards tab. Lots of boards support 128GB
  - https://docs.google.com/spreadsheets/d/1AddRvGWJ_f4B6UC7_IftDiVudVc8CJ8sxLUqlxVsCz4/edit?gid=523597416#gid=523597416
  - I would still double check the motherboard's website just to be sure. As this is still a community maintained page so info isn't guaranteed to be 100% accurate.

- The Asus B650E-I has a maximum capacity of 64GB per RAM slot, with 128GB total
  - Cheaper models like the MSI 650I Edge and the AsRock B650I Lightning only have a maximum capacity of 48GB per slot

- Gigabyte X870I AORUS PRO ICE supports 128GB. Saw it on Microcenter's website and doublechecked on the Gigabyte site
- If you really want to be sure you have enough RAM capacity, you can always go for an ITX X870 board, but that's a prety big upcost for pretty much no benefits in terms of features (outside of maybe more USB ports in the rear I/O)

- ## [DDR5 128GB on ITX possible nowadays? Experience? : r/sffpc _202506](https://www.reddit.com/r/sffpc/comments/1lgu72h/ddr5_128gb_on_itx_possible_nowadays_experience/)
  - I couldn't find new information on anyone trying out 64GB DDR5 Sticks in their ITX build.
  - Would two sticks work to yield 128GB DDR5?
  - Kingston FURY Beast schwarz DIMM 64GB, DDR5-5600, CL40-40-40
  - there is also a Crucial 64GB stick and an even faster Kingston 64GB stick.
  - ✅ Update: Received my 2x Kingston 64GB RAM sticks and after a 1min initial boot, setting the right EXPO profile in the BIOS, it works perfectly without any issues. To whoever reads this in the future, good luck on your build!

- If you want small with 128GB of fast RAM, then something built with the AMD AI Max 395 might be of interest? Framework are going to sell an ITX motherboard (and SFF PC) with the same chip, but it isn't available yet
  - Yes I am aware of its existence and the advantages soldered RAM has to reduce latency and improve memory bandwidth, but I already got a rig and am happy with the general performance of my 7900. 
  - I was considering upgrading form my measly 2*16GB and my most recent info is that optimum uses 2*48GB sticks, hence 96GB, but I couldn't find further info on 2*64GB.

- Even though only 96 GB of RAM is listed there, it is possible to use 128 GB. I've seen it in YouTube videos, but only with mini PCs, and the guy used SO DIMMs.

- Just did this on my homelab server. The board claims to only support 64GB but I put this 128GB kit in and all is well. (Passed prime95, etc tests. All 128GB is usable.)

- I think the biggest problem is there hasn't actually been 64GB sticks out for very long and with the price not many people have actually tried it. I would just go with a motherboard that states it supports 128GB and make sure you buy the ram from a retailer with a good return policy.

- ## [六联智能推出 AMD "Strix Halo" Thin Mini ITX 主板，板载内存设计 - IT之家 _202507](https://www.ithome.com/0/869/805.htm)
- AMD 的锐龙 AI Max 300 "Strix Halo" 平台 ODM 伙伴六联智能推出了一款板载该系列处理器和 DRAM 内存颗粒的 Thin Mini ITX 主板 STHT1。
- 这一主板目前已被六联智能的 2L 迷你主机、8L 紧凑型台式机、一体机解决方案采用，而其兼容外形规格使之存在直接安装于标准台式机机箱的可能。
- 该主板包含 8 个 LPDDR5x 焊盘，支持至高 128GB 内存容量；配备 2 个 M.2 2280 PCIe 4.0×4 盘位；提供 1 个 M.2 2230 无线网卡位。

- ## [Is a mini-itx first homelab a good idea? : r/homelab _202207](https://www.reddit.com/r/homelab/comments/w6dzji/is_a_miniitx_first_homelab_a_good_idea/)
- At the time I was fine with just one PCIe and 2 memory slots but now the lack of expansion is a pain.
  - Was also limited in the number of drives that could be connected and has a distinct lack of fan headers (not sure if newer boards would have any more - there's really no space).

- Unless you absolutely need the smallest footprint, Mini-ITX is always a bad choice, regardless of application. 
  - There's always a hardware tax, you generally lose out on features (e.g. you get fewer PCIe slots, DIMM slots, M.2 slots), you (almost) always have worse cooling, and the actual build or modifying process is more painful (literally and figuratively).
  - I'd advise going for microATX instead, which allows you to put together a relatively compact build, but should give you more value for money and more freedom than Mini-ITX.

- ## [Are there any ITX motherboards that can handle 128GB RAM? : r/buildapc _202307](https://www.reddit.com/r/buildapc/comments/15cazh5/are_there_any_itx_motherboards_that_can_handle/)
- Are there ones that you, right now, as an average consumer or even business can buy? No.
  - There are custom ITX server boards that have 4 DIMM slots, but they're for fairly old and slow server CPUs using DDR3, and have no PCIe slots.
  - DDR5 can technically support up to 512GB on a single DIMM, so an Intel 13th gen or Ryzen 7000 ITX motherboard could theoretically support up to 1TB of RAM! But the largest consumer DIMM is 48GB, so the most you can get on an ITX motherboard right now is 96GB. 

- If you need 128GB right now, you have to get an mATX motherboard. There is no other option.
- That said, the SSUPD Meshroom S can take an mATX motherboard, even a full sized ATX motherboard, and isn't much bigger than the Terra.

- ## [Can you guys recommend me a motherboard which can support 128gb ram? : r/buildapc _202412](https://www.reddit.com/r/buildapc/comments/1hbspr8/can_you_guys_recommend_me_a_motherboard_which_can/)
  - I'm looking for a motherboard which can support a lot of ram for programming. Preferably it should be mATX. I've heard that ITX boards aren't really great for that soft of thing. edit : CPU is Ryzen 9 7950x.
- ASUS rog-strix-b650e-f has 128 GB configurations on their Memory QVL for Ryzen 9 7950x. According to them it'll run at 5200.
  - I'm considering such a configuration now. I've not yet found an ASROCK Motherboard with any 128GB configurations on their QVL.

- All of the mid tier boards with 4 memory slots will support minimum 128GB.
  - First choice you have to make is which cpu you want, after that you can look for mobo recommendations.

- Since you're 7950X (though I'd strongly recommend getting a 7900X or 9700X as they're far better value - www.bestvaluecpu.com exists, filter for AM5), just get one with decent VRMs. This probably means going ATX as high end boards are usually this size.
  - I would not recommend putting a 7900X in a ITX build, it'll get spicy in there!
  - 64gb is enough even for most video editing, 128gb is "I do programming for my job and my job paid for this PC" kind of levels.

- [128GB of RAM in a tiny box? : r/buildmeapc](https://www.reddit.com/r/buildmeapc/comments/17lxgsj/128gb_of_ram_in_a_tiny_box/)
- The smallest motherboard with 4 dimms would be a micro ATX. Mini ITX only have 2 slots, that's why you can't find options for 128 GB.
  - I thought maybe DDR5 had been out long enough to be able to find a 2x64GB kit, but looks like maybe not. But, Crucial does have a 2x48GB DDR5 kit, and 96GB would be alright.

- I'd suggest the following that gets you 128GB of DDR5 RAM, a 14-core 13600K, compact 17.9L case, with very good CPU cooling capacity that will allow the CPU to run under heavy multi-core load without thermal throttling.
  - CPU: the 13600K provides a good number of cores for a lot of VM's, 
  - Motherboard: mATX motherboard with wifi and bluetooth, plus 4 RAM slots.
  - Memory: 128GB of RAM (four sticks of 32GB).
  - Storage: Good sped 2TB PCie 4 NVME.
  - Video Card: It wasn't clear if you need a separate GPU or not. Added in a decent GPU for not too much money - though if you can just use integrated graphics, you could upgrade to a 13700 for more cores.
  - Power Supply: SFX unit for space savings in the compact case.
  - Case: The Mechanic Master C28, despite being mATX, is smaller than several mITX cases 

- [Please advise on a mATX build with 128GB RAM : r/buildapc _202307](https://www.reddit.com/r/buildapc/comments/15e1r2j/please_advise_on_a_matx_build_with_128gb_ram/)
  - So far my only criteria is: - AMD 7950X, 128GB RAM, RTX4090. Likely the CPU would be under a lot most stress than the GPU for most of my use cases, 
- Asus Prime AP201 MicroATX Mini Tower Case	
  - Motherboard	MSI MAG B650M MORTAR WIFI Micro ATX AM5 Motherboard
  - Memory	G. Skill Trident Z5 Neo 64 GB (2 x 32 GB) DDR5-6000 CL30 Memory x2

- 4x DDR5 configurations barelly run with 4800MT/s and even that might need some DDR5 kit swaps till you have 4 working DIMMs.
  - Getting DDR5 6000MT/s CL30 is ridiculous.

- [Is it possible to have 128GB RAM with SFFPC? : r/sffpc _202210](https://www.reddit.com/r/sffpc/comments/yd2z0b/is_it_possible_to_have_128gb_ram_with_sffpc/)
- Matx board, 25L matax case and 4x32gb dimms?
  - Silverstone Alta g1m or asus ap201 are ones I want since they support a 360 AIO

- Should i maybe get c26 or c28 cases? It looks like even c26 can fit an ATX board so with that it should solve these issues?
  - You will not be able to properly cool the components you are aiming for in a case like the C26, which by the way will not be able to fit a 4090. C28 maybe, but I wouldn't want to travel with a case that has a TG panel. And you need all the airflow you can get.
  - The new Asus Prime AP201 looks promising. I would not advise to go smaller than that.

- [Smallest possible m-atx + 7950x + 4090.... advice appreciated! : r/sffpc _202301](https://www.reddit.com/r/sffpc/comments/107jq5o/smallest_possible_matx_7950x_4090_advice/)
- I just received C26plus, bought B660 mATX MB and 12600K, pending to get a 4090 and PSU. Will get back to you if the case is good fit for 4090 FE
  - Nope, side panel cannot close even with native 16pin cable

- AP201 is the current matx meta imho but the d31 is nice

- ## [Should I Choose a Motherboard with 128GB or 256GB RAM Max? : r/buildapc _202410](https://www.reddit.com/r/buildapc/comments/1fvoskv/should_i_choose_a_motherboard_with_128gb_or_256gb/)
  - is there a significant performance difference if I opt for the 128GB option?

- No. Chance is that you won't even reach the 128GB mark long before you make another full upgrade certain years down the road. 

- ## [64G内存+纯CPU裸跑gpt-oss:120b - 小红书](https://www.xiaohongshu.com/explore/68a6ee02000000001c03f964?xsec_token=ABIl2xpN-BcJcn0jmdi2k1RkNoJcXZiMAtj5QFwnpIark=&xsec_source=pc_search&source=unknown)
  - 64G内存+纯CPU裸跑gpt-oss:120b，一秒钟几个字儿往外蹦
- 慢主要是因为用的DDR4，内存带宽太低

- 换AMD，7840H＋96G内存，纯CPU跑30B，30t/s, Q4，我需要长上下文，Q4拉满256k要79G内存。量化再往上就加载不上了
  - 7840H没有npu

- 组一个一千多块的洋垃圾，256gddr3内存跑，效果看着还行，b站别人有类似视频

- ## [5090靠边让让，真神降临——48G的4090！ - 小红书](https://www.xiaohongshu.com/explore/67b5809e000000000e006d0c?xsec_token=ABGeo98UKSG8fjOMNixsHiBRqoxj7iqPLj_-v2GsF7NMk=&xsec_source=pc_search&source=web_search_result_notes)
  - 【CPU】AMD R9 9950X
  - 【主板】技嘉 B650M AORUS PRO AX
  - 【内存】阿斯加特 TUF 64G(32GX2) D5 6400
  - 【显卡】英伟达 4090 48G 涡轮卡
  - 【固态】三星 990PRO 2T+1T
  - 【机箱】机械大师 CMAX
  - 【散热】九州风神 冰暴 240 LCD屏
  - 【电源】全汉Hydro PTM X PRO 1200
  - 【风扇】棱镜 4PRO
  - 【定制】CMAX硅胶线

- ## [流言飞起的时代，4090真的值得入手吗？ - 哔哩哔哩](https://www.bilibili.com/opus/859701664964149281?from=search)
- 4090其实分为两个版本一款是专门用于游戏领域的显卡名为风扇卡，另一款则是用于深度学习领域名为涡轮卡。两者虽然都是4090实则内部结构、目标人群、运用场景其实都是不同的
- 风扇卡与涡轮卡的供电接口位置不同，涡轮卡的供电接口位置在接口尾部，供电线比风扇卡的线更短，这样是方便在机箱内部安装和理线，
  - 而风扇卡供电接口一般在显卡顶部，接线后线缆会高于机箱最高面，如果在服务器中使用风扇卡，服务器盖板盖不上。
- 在散热方向上面，涡轮卡散热方向是朝尾部散热，并于服务器风向是一致的，
  - 而风扇卡的散热是朝四面八方来散热的，平常的PC机箱放一张是可以适应的，但用作服务器上（很多时候是多卡）就不适合了，很容易因为散热不出机箱导致机箱内部温度过高出现宕机。

- 风扇卡的尺寸一般是2.5-3倍宽设计，而涡轮卡的尺寸大小是双宽设计，
  - 因为涡轮卡为了方便放入服务器里，所以涡轮卡的尺寸和高度都远远低于风扇卡，从而服务器可以支持4卡或者8卡，如果用风扇卡代替涡轮卡装在服务器里，那位置够不够还是一回事儿呢。

- ## [支持多指触控的开源触控板来啦！ - 小红书](https://www.xiaohongshu.com/explore/6711d2b30000000021006a5d?xsec_token=ABBAVIU5BmyEoOSC1_U-awDuJr92L8j26jKmwMyo1z8q4=&xsec_source=pc_search&source=web_search_result_notes)
  - Ploopy因其开源、3D打印的PC外设在小众市场中享有盛誉，其最新产品Ploopy Trackpad也延续了这一风格。这款“3D打印、开源的大型触控板”适用于桌面和笔记本电脑，尺寸为190 × 140 × 20毫米，比Apple的Magic Trackpad还大一些。
  - 它支持Windows和Linux上的最多五指多点触控手势，但由于macOS与QMK固件之间存在限制，苹果设备的手势支持受限
  - Ploopy Trackpad的外壳和触控表面都由PLA塑料3D打印而成，Ploopy声称这种材料比ABS更耐磨并且使用舒适。虽然最初计划使用玻璃表面，但最终选择了ABS，因为它在不同操作系统和设备上提供了更一致的跟踪效果。鉴于Ploopy的开源设计和活跃的社区，未来可能会有用户实现玻璃触控表面的改进。

- ## [妙控板有没有平替 Apple也太贵了 舍不得 #妙控板 #Apple #苹果#Macmini - 小红书](https://www.xiaohongshu.com/explore/6822f22b000000002202f95b?xsec_token=AB7ZPhxG4yCtuySva103gpkHVwVRQu1KHJQbB5APshtUc=&xsec_source=pc_search&source=web_search_result_notes)
- 没有，而且妙控有线>蓝牙连mac>蓝牙连ipad pro，很追求手感的话还要配一根长线，是连60hz的屏都能分辨出区别的程度
- 没有，尤其是破罗技，一生黑

- 买二手的吧，这个很耐用的，二手成色好和新的也没啥区别
- 买一代的二手也就一百多啊

- 是的，而且非常建议用有线连接，没有蓝牙的延迟，使用体验和mbp自带的基本一样

- [我的mac mini穷鬼套餐，不失体验 - 小红书](https://www.xiaohongshu.com/explore/68320649000000000c03825f?xsec_token=ABF0XhwOtoKDBQhKUo195eNCcCz6x5xwHH_366uEQDqSo=&xsec_source=pc_search&source=web_search_result_notes)
  - 一代妙控板可以配m4的，打开就直接连上了

- [苹果触控板理想平替 150块能实现80%功能？ - 小红书](https://www.xiaohongshu.com/explore/6728d5db000000001b01018c?xsec_token=ABXrx-jUlKOXDJg4dJl1XMWqHF5XtUK6_hozrpAJbVH9Q=&xsec_source=pc_search&source=web_search_result_notes)

- ## [最佳外接独立触摸板罗技casa touch体验 - 小红书](https://www.xiaohongshu.com/explore/6804c1f0000000001201c88a?xsec_token=ABZ7BagZ46pJM6c6btbNXwLHXUCDQ3iVwDsgN_a75SKZ8=&xsec_source=pc_search&source=web_search_result_notes)
  - 太长不看，最佳外置触摸板-妙控板替代品，可以无脑下手。
  - 罗技23年推出了一款pop-up desktop产品，里面包含了一个外置触摸板，上一次罗技推出独立的触摸板还是在十几年前。
  - 大小和笔记本上的差不多，有黑色/白色和粉红色。表面材质是玻璃，被塑料覆盖。重量157.6克，妙控板是230克，触摸面积比妙控板2小很多，
  - 可以用bolt和蓝牙进行连接，有三模，每一个都可以单独连接bolt和蓝牙，
  - Mac/Windows/ChromeOS（fydeOS）/iPadOS都支持所有功能和手势。
  - 可以连接三台设备，三个记忆点
- 没有国行
  - 闲鱼卖光了，可能要买套装了

- 比huke好用太多了

- ## [MacBook外接键盘使用分享 - 小红书](https://www.xiaohongshu.com/explore/66fbde7b000000002a034d62?xsec_token=ABuws2tsgaoDnK4grUvCbFCBwKv3VPGL8ZVJ0p8qGnHec=&xsec_source=pc_search&source=web_search_result_notes)
  - 一、苹果妙控键盘 - 桌板轴 给 Mac 配备的第一个键盘是妙控键盘。这款键盘在适配性方面堪称最佳。无论是颜值、重量、键位、多功能键还是续航，都与 Mac 实现了无缝衔接。唯一令人吐槽的地方在于按键手感，几乎没有任何反馈，打字的时候，你可以想象自己是在敲桌子，完全没有输入的乐趣。倘若你不在意手感，那么这款键盘是我的首要推荐。
  - 二、京造 K2- 红轴 受够了敲桌子般的无聊手感后，我换京东京造 K3 红轴键盘（与 Keychron 贴牌同款，当时众多自媒体都在安利的网红款，号称是 Mac 的第三方最佳适配键盘）。 这款键盘的颜值当时不错，黑橘配色，但是会打油，连接方式为蓝牙和有线双模式，轴体是佳达隆红轴，直上直下，比较轻盈。使用了一段时间后，体验尚可。槽点是键帽较高，使用时手部悬空，长时间使用会比较累。 内置电池待机时间短，充电较为频繁。对于强迫症患者来说，最难以忍受的是蓝牙断联和睡眠唤醒慢，还会吞字。
  - 三、罗技 MX Mechanical-红轴 恰好罗技新上市了一款 MX Mechanical 矮轴机械键盘，超长待机、三模连接，满足我的需求，于是入手了一把茶轴款。这款键盘的轴体与传统轴体有所不同，茶轴有点类似于黑轴，手感很重，不够轻盈，不太适应，换成了直上直下的红轴。这个矮轴相比高轴的红轴，回弹稍微重了一些。矮轴长期使用不会那么累了，连接速度也很快，没有断联和吞字的情况，整体来说还是比较满意的。这款键盘目前我也一直在使用中。说缺点的话，键帽比较小众，没有完美替换的，少了些乐趣。键轴也不支持热插拔。
  - 四、Nuphy Air75-越橘轴 给 Mac 主机配键盘，选择了 Nuphy 的 Air75 一代。键盘的包装和做工很精致，颜值是最高的，键帽好看，三模连接，采用佳达隆热插拔矮轴，连接速度快，不会出现断联和吞字的情况。后期换了Air75 二代，提高了连接速度和续航，增加新的轴体，新的轴体和垫棉带来了更好的手感。开始买的是芦荟轴，太轻，反馈弱，容易误触。换成了越橘轴，这个轴类似于 “HiFi 麻将音”，手感重一些，有更好的反馈力不会误触，长时间打字也不会累。

- 刚入手keychron K4 pro 香蕉轴，手感不错，适合办公打字。关键是可以via改键位，很香
  - 声音不大，挺柔软，适合在办公室用。

- [苹果电脑妙控键盘 最强平替 - 小红书](https://www.xiaohongshu.com/explore/67cc2e4f00000000290198e4?xsec_token=ABb9QlEEv4edez8zXqcCpR1avO8fI6BvZ09MtS_ONM62k=&xsec_source=pc_search&source=web_search_result_notes)

- [Mac book外接设备分享（穷鬼版） - 小红书](https://www.xiaohongshu.com/explore/67de16ad000000001d017c2e?xsec_token=ABYgeab4C5E3b9gpHBDeBL8QBz3tky0SCWCe9j92RoGQg=&xsec_source=pc_search&source=web_search_result_notes)
  - 键盘⌨️：京东京造k3 max（💰340r）
  - 鼠标🖱：蜻蜓VXE R1 SE+（💰70r）
  - 拓展坞：绿联五合一（💰158r）

- [可以支持Mac 的无线机械键盘，轻便静音，适合长期打字办公党的，宝子们有没有推荐呀？谁懂打字手指关节痛呀 - 小红书](https://www.xiaohongshu.com/explore/67a2ca1400000000290289d0?xsec_token=ABVfm3DcCUe0ysKmPGx8coQmEZCkPFcCZi28IS-M-_rUg=&xsec_source=pc_search&source=web_search_result_notes)
  - 可以支持Mac 的无线机械键盘，轻便静音，适合长期打字办公党的，宝子们有没有推荐呀？谁懂打字手指关节痛呀
- Nuphy Air系列或者Keychron K系列, Nuphy是静音的
- nuphy air系列，铝厂 MG65 都很好

- 宁芝静电容 mirco plum 84 35g版本

- 官方妙控键盘 轻薄 静音

- nuphy， 洛斐，渴创，都是支持苹果的成品键盘

- 京东k3max，keychron代工的，我用着还可以。矮轴不需要腕托。

- ## [Mac外接显示器使用的一些建议和优化方案 - 小红书](https://www.xiaohongshu.com/explore/67d823340000000007036b64?xsec_token=ABi4D7ISTN18_diLmfrK_nWQFIh4EdsPayzksbNRkvRgQ=&xsec_source=pc_search&source=web_search_result_notes)
- Mac外接低分辨率显示器出现的模糊问题
  - 当购买了Macbook或者Mac后 我们选择外接显示器 通常选择分辨率是 4k或者 5k的居多 但也有一些小伙伴用的是1080P或者是2k的显示器 导致Mac在此类显示器上会出现字体发虚、模糊等问题 
  - 因为Mac默认 4k以上分辨率的显示设备才会开启HiDPi  
  - 所以解决此类问题也很简单 利用软件强制开启HiDPi即可 这里推荐RDM 不仅开启HiDPi 还能开启显示器高刷 当然有条件的话 还是推荐换高分辨率的显示设备
- 外接显示器后无法利用外接键盘调节显示器亮度和音量
  - 第一次使用Mac外接显示器 用的外置键盘 却无法调节显示器的亮度 甚至音量也无法控制 这里推荐一款软件 即可解决此类问题 Monitor Control 是github上免费开源软件
- MacBook长时间外接显示器满电使用电池寿命问题
  - 这个问题也是大家很在意的 毕竟新买的设备都比较爱惜 这里推荐大家一款AIDente的软件 可以将设备电量🔋控制在 80%  还能控制MagSafe充电灯 充电的同时主动放电到 80% 的健康百分比等 还可以监控充电功率 计划充电等 网友评价很高 部分功能在Pro版本上需要付费 但一般基础功能免费开放
- Mac mini m4 本身是支持 最高 4k 240hz 的显示器 多台连接也有 4k 120 hz或者 4k 144hz 办公 60hz足够 但是高刷体验更佳 比如浏览网页更丝滑 拖动窗口也丝滑 有足够预算选是最优解

- ## [买了个超高清 4K 23.8 寸 便携显示器 - 小红书](https://www.xiaohongshu.com/explore/6810c50000000000090174b8?xsec_token=AB_QqkK7_ZF3_KbwyW1ZB1W-4U-ahovczyytBjBGhW3_A=&xsec_source=pc_search&source=web_search_result_notes)
  - 如果是长期自用办公和科研，至少要2K以上，搞艺术的最好是4K。
  - sculptor23.8寸 4K 显示屏

- ## 📌 [便携屏挑选建议 - 小红书](https://www.xiaohongshu.com/explore/678deac90000000018029a17?xsec_token=AByy4GMp8bWndvumxKkA0t2zCapY5R9quZuyaVsMR8Y_w=&xsec_source=pc_search&source=web_search_result_notes)
  - 首先明确需求: 办公还是游戏？Switch、主机或电脑？
  - 目前市场主流品牌均为非一线厂商，但不代表产品不达标，质量也有很不错的。
  - 主流品牌有，ARZOPA阿卓帕、雕塑家、EIMIO、CFORCE等，各有特色。其他品牌，若预算不足，要求不高，也可选择。 
  - 主要有两个参数需要注意
  - 帧率:60hz适合办公以及轻度游戏，包括switch、ps主机、电脑端。然后就是144hz及以上，适合FPS等竞技游戏，例如CS2
  - 色域: 主要标准有sRGB、Adobe RGB、DCI-P3、NTSC。基本上sRGB大于75%就有较好的颜色表现了，当然越高越好。
- 我相信1080p已经满足绝大多数人需求，更高分辨率不如直接上台显，对设备性能要求也会更高。
  - 这也是为啥只测试了1080p的版本，足够清晰了，屏幕又小，钱花在刀刃上。

- ## [mac mini 便携显示器难得找个完美的 - 小红书](https://www.xiaohongshu.com/explore/67be8dff00000000280368be?xsec_token=ABatyUb9Lx1XYXALQpMcvmTBAo775B3MvozPzD4EZe9RI=&xsec_source=pc_search&source=web_search_result_notes)
  - 经过多方对比，拿下arzopa 16寸的2.5k便携显示器，菜单方便，连接一根线即可，显示效果不错，不过这类显示器很难支持hidpi，目前就1280-800还行，不过感觉缩放有点大，原始分辨率字又很小

- 要么4k要么1080，m系列就是hidp有问题，得这两个分辨率，五年了都没解决很无语。intel版就不会
  - 理解为没法点对点就行

- 所以很多博主推荐苹果配4k显示器，就是要它默认1080p的hidpi。最重要的一点是mac的应用不能随意改变窗口大小，必须考虑这个问题（720p在用QQ音乐可能会与程序坞重叠）

- 一般来说2k显示器默认720p的hidpi

- [Mac外接便携屏 - 小红书](https://www.xiaohongshu.com/explore/68b697cf000000001d03b010?xsec_token=ABUJretia2o2VefwJarjPWkuB5UQVMIEKT9s7nuAqwVcs=&xsec_source=pc_search&source=web_search_result_notes)
  - 要不然 1080 要不然 4k，mac 用 2.5 是不行的
  - mac 的 hidpi 导致合并像素变成 720p，直接看 2.5k 的话小的没法看，其它分辨率会糊
  - 重新买了一个4k的 感觉不错

- [Mac mini + 2.5k 触摸便携双屏 - 小红书](https://www.xiaohongshu.com/explore/677691f1000000000902d752?xsec_token=AB-RIwo7Ptt2-VRNMWpcTa4IqKO9_fbiWVFPRQBKISJ7U=&xsec_source=pc_search&source=web_search_result_notes)
  - 2.5k 虽然开了 hidpi 只有1260*800分辨率， 但在16寸屏幕上字体显示比较舒服，不会吃力，缺点是双屏触摸屏很重（2.1kg），已经不能算便携了

- ## [mac怎么选便携外接屏？ - 知乎](https://www.zhihu.com/question/539704864)
- 便携的话就ipadpro很适合，平时可以当pad用，看看电影，记记笔记，干活的时候就可以作为外接屏，很方便。

- ## [英特尔怎么可能一年之间就没落了？ - 知乎 _202410](https://www.zhihu.com/question/2005473234)
- pc端只是表象，真正打断intel骨头的是服务器端。zen刚推出的时候，16~32核线程撕裂者，平均每核成本和售价比志强低，线程撕裂者一推出就收到市场好评，28核以下的志强市场立刻遭受线程撕裂者的瓜分。
  - 后续zen2架构下，推出最高64核心128线程的霄龙服务器，志强平台一个能打的都没有，论性能，拼不过，论价格拼不过，论能耗，拼不过，唯一可以拿出手说话的就是志强的内存延迟更低。
  - 到了zen3时期，霄龙服务器缓存进一步增大，延迟相比志强甚至略有优势，IPC也比志强好，功耗也更低，一颗64核心128线程的霄龙U，价格一万多美元，而Intel这边迟迟推不出新一代志强，还是28核心56线程的志强当道，价格也要1万多美元，你是商家，你选谁？
  - zen4时期，霄龙继续领先，志强还是被压着打，只能吃吃老本，掏不出什么让人满意的新U。
- 市场统计，志强份额还是领先于霄龙，但是那是历史，没什么卵用，新的大订单基本是霄龙吃下了，志强只能吃吃老本的更新换代，根本不解渴。
- Intel的困局本质上是性能更高的志强平台已经很久没更新技术，技术下放更是无从谈起。PC端的缝缝补补还能和amd打得有来有回，混个28开、46开、55开，服务器端真的是一败涂地。

- 不知道的以为英特尔还在挤牙膏，其实是英特尔肚里真没货。

- 服务端求稳，，路径依赖给Intel吃老本了两年，zen2的服务器我就测过了，真是性价比吊打Intel，而且为了好迁移程序AMD经常是单路对双路

- 旧的超算中心都是iU，稍微新的就是AU了；当然国产U也有，用过国产海光X86
  - 华为的前阶段国家还有补贴，对于小微企业还是有相当吸引力，毕竟云主机能用价格低就是王道。

- 就国内市场而言，我觉得是被海光打败的，我司已经2年没采购intel的服务器了，全是海光和鲲鹏。
- 海光就是zen1架构

- 性能强的的有amd，低功耗的有arm的。被挤了。

- intel技术出现了什么问题了？
  - 一切源自10nm难产……工艺上不去很难堆核…堆核了发热和功耗倍增对dc成本不划算……
  - 堆不了核，架构升级不了

- epyc 对于企业来说省的远不止是 cpu 差价的钱，整台服务器除了 cpu 外的其他硬件、机柜、电力等，用 epyc 一台能顶至强好几台，省下的钱可不是个小数字

- PC DIY市场对于厂家而言是最鸡肋的，利润不高但音量很大。商用、专业领域甚至游戏主机都是更优质的市场。但是对于一个产品导向的公司来说，他不会随意丢弃某个市场，只是支持力度的问题。PC DIY市场地位在目前基本就和讨饭的差不远

- 有没有可能，从十年前就开始没落了。intel7（10nm）这个工艺应该在2016年就出来的，结果到2024年了还在缩肛。

- intel岂止是在cpu上拉胯了，这几年砍了多少方向了？砍了，FPGA拆分了，放弃。说是要把工作重心放在cpu上，可是工艺早就被台积电甩开。最重要的服务器领域甚至拿不出和AMD旗舰型号对标的产品。要我说现在这个衰退速度还算慢的，要不是有使用惯性，intel应该更垮一些。

- ## [线程撕裂者这种核心超多的CPU主要能用来做什么，来使用掉绝大部分核心？ - 知乎](https://www.zhihu.com/question/500819181/answers/updated)
- 对于普通家用电脑来说，别说8核心，4核心基本就能满足许多需求了，这是因为大部分的常用软件并没有对多核心处理器进行优化，即使你的CPU核心数量再多也用不到，相当于浪费，但是像[线程撕裂者]这样的超多核心CPU可以在专业领域方面发挥很大的作用。
  - 3D图形渲染、数据中心和视频处理这些工作都可以非常好的利用多核心处理器的性能，更多的核心就能起到更多的作用
- 另外，CPU [X86架构] 经过多年的发展，如今想要大幅度提升单核性能已经很难了，所以英特尔和[AMD] 都在想方设法增加CPU核心数量，通过多核协同工作来提升CPU性能，未来还会有越来越多的软件和游戏对多核处理器进行优化，所谓的“一核有难，八核围观”的尴尬场景会越来越少

- 强计算生产力用途包括3D渲染，影视制作渲染，CG动画，有限元分析CFD，[Fluent]，SAS，Python，量化交易，[股票量化策略]，回测，高频交易，深度学习和机器学习，自动标记，训练，推理，平面美工，游戏程序开发，能赚钱的游戏直播主播，游戏工作室等等

- 工作站，服务器，多开虚拟机。

- 编译 ~ 比如chromium，虚幻引擎 100核也不多…

- ## [高端显卡买哪个 4090-48g vs 5090-32g - 小红书](https://www.xiaohongshu.com/explore/685fdabf000000002400c5fb?xsec_token=ABXvcJCtj5SgpnxaAuvQTSjGIPWgAdou5ozGSko5ifxSI=&xsec_source=pc_search&source=web_explore_feed)
  - 48GB版本4090是涡轮版魔改的，性能比4090主机版低20%性能。并且被改的卡不一定是一手卡，也没有官方质保。店家会保一年。
  - 5090目前的适配并不完善，要求新驱动。对少数深度学习项目有兼容性问题。

- 我其实不太理解为啥5090才给32g
  - 刀法，给多了影响算力卡出售。后续的卡可能会卖不动。
  - GTX定位不是跑模型，按最初的设想，算力卡才是跑模型的。这样就能通过Nvlink技术共享显存。
- 人家定位就是游戏显卡，什么游戏能用爆32G显存？跑推理训练去买pro6000啊

- 5090说不定能改64GB，说不定之后会有人改
  - 很难，没有bios

- 目前用 8 张 4090-48 挺稳定的
- 涡轮卡吗？
  - 我听说改48GB的基本上是涡轮版，因为这样利润最大。
  - 不但是利润，涡轮卡是双槽，一个机箱内可以塞更多的卡

- 48GB魔改版可以多张卡叠加显存嘛
  - 可以张量并行部署更大的模型
- 稳定的话应该没问题，组里有十几张都没啥问题
- 不能，多卡叠加显存必须去买老黄的专业ai计算卡

- 搞RTX pro 6000，一张就96G显存了
  - 8万多可以搞四张了
  - 现在价格6w5左右

- 还没买，我比较保守，怕48GB的有问题，倾向于5090。
  - 存在兼容性差的问题，同课题组有人买了5070，他说要求更版本的pytorch（因为支持的cuda版本必须高），所以低版本的pytorch项目跑不起来。
  - 12.8等高版本的pytorch不支持很多项目项目的

- 打游戏就老老实实买5090，ai都是伪需求，没几个用得上的，真正有需求的会去买ai卡
  - 跑模型为啥要买Geforce，买telsa的H200，H100不香么，再次点Quadro这种专业卡都有Pro 6000，跑ai完全吊打5090，真的有需求的人买不起也会去租的

- 5090配环境还是麻烦，干活的现在用4090一年后再考虑5090

- ## [8K配的工作站加4090 48G 成功跑起Deepseek - 小红书 _202504](https://www.xiaohongshu.com/explore/67fa372d000000001e00ba5a?xsec_token=ABufSAS9QghohUw1fzyX0iVOG5KQLPpvxE2fkT2okUTlk=&xsec_source=pc_search&source=web_explore_feed)
  - 运行的是ikawrakow/ik_llama.cpp/这个库，他用 AVX2 指令集做了许多优化
  - 运行的是 Q2 的版本的 deepseek v3，占用内存 222G，显存 20G，所以普通 4090 也能跑起来
  - 输入 41 t/s, 输出 8 t/s
  - 我用的是联想 P620准系统+256 内存 8K 多点的价格
  - 这个 P620 准系统也不差 5945ws 线程撕裂者 联想锁机 U 可以跑到 4.5G 十分便宜 5 6 百左右吧
  - PCIE 插槽多 128通道，每个插槽都可以拆分，以后扩展比较方便
  - 8 通道 DDR4 3200内存，不比 DDR5 慢，一条 32G 200 左右
  - 唯一缺点，主板的1000w 电源没法更大了，主板插槽也不支持两个高功率显卡，所以想在这个系统上插双 4090 是没戏，但可以插 2 个 A6000。
  - 同价位的 PC 是完全没法比的。虽然我这些都是二手，但几百块的 cpu 就是坏了换一个也没啥心疼
  - 我调查过其他的工作站服务器，epyc 志强，我觉得都不如线程撕裂者，平时当 AI 服务器，偶尔还可以剪剪片子性能也很好。

- 我买的带cpu的准系统，这个cpu锁联想的主板，所以便宜

- 问下这个机器的电源怎么接，机器本身电源只有两根显卡电源接口的线，4090至少要三根
  - 两根8pin转 4090 16pin的就可以了

- 这种魔改的显存官方驱动支持吗
  - 支持

- ## [我的RTX 4090 48G深度体验报告 - 小红书 _202503](https://www.xiaohongshu.com/explore/67ca95ca000000000d015047?xsec_token=ABqsyDIYHWnZyXfQUxpaLc8ZkBUCid6Z7dPfToCAZBfTA=&xsec_source=pc_search&source=web_explore_feed)
  - 用4K OLED电视测了《赛博朋克：往日之影》，路径光追全开+DLSS 3.5插帧，画面毛发反光真实到离谱…帧数居然稳在98！以前3080直接掉到40的酒吧霓虹灯场景，现在丝滑到想哭
  - 用Blender渲染公司新项目场景，32GB显存直接吃满！如果换成老显卡估计要崩…但4090 48G居然能边渲染边开着AE做特效预览，这才是真正的“生产力解放”
  - 偷偷试了本地部署70亿参数AI模型，48G显存跑图+训练同时进行
  - 电源建议1000W金牌起步！我旧电源带不动疯狂闪退
  - 机箱尺寸必须量好，这张卡比iPhone 15还长2cm
  - 非刚需慎入！除非你是8K剪辑/AI训练/富哥

- 适合笔记本吗？
  - 这是桌面级核弹！笔记本请认准4090移动版（完全不是一个东西）

- 跑游戏和普通4090无任何区别。甚至在没爆显存的基础上，跑AI也和普通4090速度是一样的，不要幻想有了48G就会更快。需要指出的是，跑70b模型确实能发挥48G的优势，不再是一个字一个字蹦。最后，涡轮风扇噪音极大，部分用户可能无法接受。

- ## [同预算，我发现了比4090 48g更优的卡 - 小红书](https://www.xiaohongshu.com/explore/68933df200000000250232c0?xsec_token=ABJcKpAiG7_wvbIBshcL_hTstuY3ZuJRr7DRybbzYqQno=&xsec_source=pc_search&source=web_explore_feed)
  - 公布结果：5880 ada 48g显卡，
  - 按照nvidia官方发布的datasheet，算力差距在20%。毕竟这个价位。考虑稳定性，和大显存，这卡还是比较好的选择
- a6000为啥比5880ada还贵？
  - a6000有两个版本，一个是a6000 一个是6000ada，你说的贵的，是ada版本，属于是4090一代产品，5880是6000ada的阉割版

- 4090的显存bandwidth太低了
  - 小作坊感觉也够用了，毕竟老师们的经费也不见得能买h100这类。

- 这个价格我只能想到是L20了，差不多的价格，显存比4090 48G大，关键是可以上NVLink联合显存，性价比真的高。

- ## [4090 48G真爽，给女儿的人工智能实验成功 - 小红书](https://www.xiaohongshu.com/explore/67de13d1000000000b0151d1?xsec_token=ABYgeab4C5E3b9gpHBDeBL8cszeX4XJpIaX3RvHVudVRc=&xsec_source=pc_search&source=web_explore_feed)
  - 很多朋友关心这块4090 48g。我的配置也说一下，我是联想P620 5945w的线程撕裂者加256内存，这一套系统大概8K，比起PC级的配置，经济实惠，主要是PCIE扩展可以有很多，内存通道也多，内存便宜。
  - 跑大模型，32b并发16能到400多t, 训练时，满精度只能跑1.5b, 如果是lora就无所谓了，32b也可以跑。

- 小模型参数不够推不出来怎么办？感觉有好多不确定性
  - 只要想办法让它通过思考输出和agent任务相关的token, 执行任务成功率就会很高，以前靠长cot是没法在小模型做的，通过RL训练解决了这个任务，如果只训练特定领域成本也不高
- 个人认为小模型推不出来反而是确定性太强，过于依赖提示词，用起来语言模型像文生图似的
  - 其实你这样想，学会从大量工具中挑选对的，以及写对参数，这些是不需要大量知识的，只需要输出符合逻辑的token作为上下文，它就能完成任务。RL+GRPO给了一种解决小模型提升干活能力的思路

- ## [如何评价 Framework 笔记本？ - 知乎](https://www.zhihu.com/question/475249794/answers/updated)
- 喜欢接口多惊鸿14就有3A2C，HKC，机械革命这些才是真的懂平民产品该什么样子的厂家。
  - framework? 产量和销量上不去，又没有日系的溢价的情况下根本没法做好品控，那就只能根据现有的模具改一改。

- 要模块化没问题，首先先把显卡可换，内存，网卡，硬盘，CPU，全部可换，你得去说服intel让它别改针脚，不然你这改个C口就模块化了？
  - 是啊，对于真的用笔记本的人来说，模块化应该是像00-10年代主流笔记本一样，起码能自行更换cpu吧。framework的伪模块化只是对外接口模块化罢了。

- framework要做的该是笔记本的pc架构标准，这不是一个公司可以做到的，而且还需要时间去拓展硬件生态

- cpu、显卡与主板绑定，更换直接换整个主板，所谓的模块化显卡就是接显卡坞之前还得再加个模块转换接口么？？大概了解了一下这个产品的现有信息，我只能说，眼前一黑。为了模块化而模块化的产品，请不要打diy的幌子噶韭菜了。

- 总结一下上述回答：轻薄和模块化是不可兼得的鱼和熊掌。目前很难在完全轻薄和最大程度模块化中间找到一个能让很多人满意的“度”。

- ## 🛝 [有没有前期将就用后期可以升级扩展到顶级的电脑配置？ - 知乎](https://www.zhihu.com/question/15227206505)
- 你想有钱了再搞扩展，最关键的就是主板一定要买好的，大板是必须的，而且是近期出的
  - 如果主板买的老、旧、丐版，那后期没法升级，只能全换
  - 其他CPU、显卡、内存、硬盘、电源都可以升级

- 不存在。我现在的配置是2070S，想升级，计划保留电源，硬盘和内存。结果发现ddr5的物理接口都改了，想要释放新显卡，就必须连内存一起换了。
  - 所以你要是用久了再升级，会发现当前零件全过时了。而短时间之后就升到顶配，那不如再等等直接入手顶配，毕竟电子产品，二手价格是腰斩的。
- 一般电脑升级，就是除了硬盘，电源可以保留，其他全换。

- 先买一个联想的P620准系统，它自带了机箱、80PLUS铂金电源、主板、CPU散热器以及内存散热器，这个是最贵的，大概是5000元左右，其他的我们都买丐中丐
  - CPU先用一颗最低端的线程撕裂者5945WX，联想锁的大概700-800元，区区12核24线程的低端CPU
  - 内存先简单来4条32G的 [三星DDR4 2R] x4 2666MHz的ECC内存，凑一个128G的内存容量，大概700元左右
  - 硬盘如果囊中羞涩，可以先来一根[西数的SN7100] 1T过渡一下，不过服务器主板有非常丰富的PCIE插槽，直接插PCIE固态或者用U2固态也是非常好的选择，如果需要素材比较多可以考虑上一个机械硬盘
  - 显卡我们可以挑一个亮机卡，比如[P1000]，这就只要200元了，UG、CAD并不是特别吃显卡的软件，买P1000这种低端的专业图形卡即可
  - 这样子一台简简单单的建模工作站就OK了
  - 日后想升级很简单，CPU换成5995WX，这是64核128线程的真 线程撕裂者，内存简简单单扩展到256G，硬盘往死里加就OK
- 这机箱真漂亮。玩装机，玩到最后就是机箱。

- 这种准系统工作站一个很容易忽略的问题是就是显卡无法安装游戏的显卡，机箱空间有限装不了，而且这种机箱设计本身就是面对工作站方向设计的，而且只能装那种工作站专用的涡轮显卡，那个声音很酸爽有够你受的。
  - 后来我用外接显卡方式解决了游戏显卡不能装工作站的问题，实现了能用大内存又能用高性能游戏显卡。
  - 现在游戏显卡基本上都是设计很高，而工作站对显卡高度是有限制的，里面空间也很小也不利于散热，所以如果可以重新选择我以后会倾向于用游戏主机来做设计。

- 这问题不是就给AM5定制的吗？
  - 主板：B850M带WiFi，1200左右，考虑后期升级一定要弄块好点的板子，要不然升级供电带不起来。
  - CPU：凑合用9600X或者7500F，前者1200后者800，未来可以升9800X3D或者9950X3D，游戏生产力都可以兼顾。或者搞块8500G用核显，连亮机卡都可以省。
  - 内存：16G×2 6000MHz或者6400Mhz，AMD不用上高频内存，6000频率同频用还省钱，后期ddr5普及之后可以升级32G×2 8000MHz分频用。
  - 显卡：凑合用随便淘张亮机卡就行，升级主板支持pcie5.0，别说5090，将来6090都能跑的满。
  - 硬盘：先买块4.0的固态用着，将来可以换pcie5.0的固态。
  - 电源：二手比较划算300块可以淘到海韵750W，大牌稳定可靠还安静，升级显卡也没什么瓶颈，不带90级别显卡都没什么压力。
  - 机箱：正常尺寸机箱，看个人喜好。

- ## [迄今为止，你用过的最好用的数码产品是什么？夸一夸? - 知乎](https://www.zhihu.com/question/14769217934)
- 联想P620工作站，最便宜的线撕工作站，同时各种拓展给够，有万兆、雷电、u2、nvme，还有四槽想咋拆分就咋拆分的PCIe4.0x16，也不会像t7960那样各种不认盘，继承老板们的锁平台线撕CPU还能再省一比马内，
  - 除了上不了机架和电源瓦数偏低之外没有任何缺点，当然你放到机柜最底下的托盘也不是不行
  - 想起来没得bmc用，这确实是最大的槽点，不过要是拿来当homelab的话那其实用不太到，不如小米智能插座

- [服务器里的基版管理控制器（BMC）是哪个？ - 知乎](https://www.zhihu.com/question/54716507)
  - BMC是一个独立于服务器系统的小型操作系统，作用是方便服务器远程管理、监控、安装、重启等操作。BMC接通电源即启动运行，由于独立于业务程序不受影响，避免了因死机或者重新安装系统而进入机房。
  - BMC只是一个集成在主板上的芯片（也有通过PCIE等各种形式插在主板上），对外表现形式只有一个标准RJ45网口，拥有独立IP。普通维护只需使用浏览器访问IP: PORT登录管理页面，服务器集群一般使用BMC指令进行大规模无人值守操作。
  - 一般服务器BMC网口是独立的，仔细看印有BMC字样。但是也有小型服务器BMC网口和通信网口是二合一的。
  - 当然也有不叫BMC的，只要遵守IPMI协议，都是类似的。

- ## [漫步者G1500BRA音响测评 - 小红书](https://www.xiaohongshu.com/explore/66d12cf8000000001f038e03?xsec_token=AB38kMIt8DJB5wbhI53QOtqHIYVOHf_3EnOAptaC3-TWM=&xsec_source=pc_search&source=web_search_result_notes)
  - 性价比高、7.1环绕的音效、有线输入和插电是USB二合一、内置声卡可调节等
  - 整体非常简约，包装里有音响本体、说明书、品牌贴纸、可插拔麦克风，线是一直在上面的
  - 虽然有两种连接方式，蓝牙和有线，但它还是比较倾向于有线，除非你手机或者其他不能插USB的设备使用，可以插在插座上，开启蓝牙模式，但我买回来主要是给电脑用
  - 如果是电脑有线使用，还可以去官网下载声卡软件，声卡软件里的功能非常多，虽然它默认的音效已经很完美了哈哈，但是可以自定义音效，适合不同人的需求
  - 7.1环绕音我一开始是不了解的，直到我用了这款音响以后，声音就像包裹了你的耳朵一样，非常有沉浸感
  - 音响有三种模式，音乐模式就是低音会强一些，游戏模式延迟低，声音大，电影模式声音要小一些 沉浸感强
  - 麦克风离远点就差劲了，放在显示器下面，离嘴巴太远，别买了

- 不适配ps5真的很无语
  - 但是他适配switch

- 感觉我的外放声音好小
  - 游戏模式会大一些

- 开关机的声音只需要按4 G 和5 音量加 两秒就能关掉了

- ## [为什么现在的音响大都是蓝牙音响？ - 知乎](https://www.zhihu.com/question/658012042)
- 一般好点的那些，都叫《音箱》，而叫《音响》的，都是只有玩得不多的人才会搜索的。

- 几乎所有的有源音箱都是有有线连接的，一般标注为：AUX接口，

- 一个新选择——Wi-Fi音箱。传输音频的方式，只能用蓝牙吗？是不是有其他方式？唉，那就对了！“Wi-Fi就是其一。”Wi-Fi音箱其实已经推出市场很久，只是在国内少有人知道。

- [为什么有线音箱少了？ - 知乎](https://www.zhihu.com/question/514579467)】
  - 没有少，只是有线音响（一般指有源音箱）。好点的都带蓝牙功能，方便手机平板无线连接

- ## [联想推出扬天 M4000q 台式机，i5-12400 + 16GB 内存，该款产品是否值得入手？ - 知乎](https://www.zhihu.com/question/518095107)
- DIY玩家来说肯定是看不上的，没有3080，没有16个PCIe通道。但是你把他看作一个办公主机，我觉得是非常香的。这个办公机不比那些采购用的臭鱼烂虾什么6代i5良心多了。
  - 配置上看起来和联想的家用天逸510s 比较类似，也都是7L小机箱

- ## [从笔记本转用台式机屏幕分辨率都是2k，但从16寸到27寸按理说会变糊，不会不适应吗？ - 知乎](https://www.zhihu.com/question/662562760)
- 不会，因为台式机和笔记本有个最大的区别，就是视距。
  - 笔记本是没办法的，你手是要放到键盘上的，视距几乎和臂长差不多，必须离近了看，所以ppi不够的话，颗粒感就会让人很难受
  - 台式机分辨率2k就已经够用了，只要你不是近视眼贴着屏幕看，4k和2k体验差距并不大

- 为了能让27寸显示器看起来能有一个舒适的视野范围，题主自己，不由自主地就会在更远些位置来使用
  - 无论是16寸还是27寸，为了得到更好地视觉体验，眼睛与屏幕的距离是不同的

- ## [惠普战99台式机值得买不？ - 知乎](https://www.zhihu.com/question/588726682)
- 这是有史以来性价比最高的品牌机了这个机器我也用了4个月了，给南桥、固态硬盘加了散热器和添加同型号内存条，改装电源并扩展了一张AMD W6400显卡，解决了主板过热问题，在2k环境下流畅运行。所以只能说，这个机器对得起这个价格。

- 我买的战99款式是14500集显款，也拆机研究了内部，我来说一下他几个缺点吧：
  - 1. 主机噪音过大
  - 2. 内存条是单通道 我因为是核显，想追求双通道加了600元从16g升级到32g, 其实这本身已经溢价了，但没想到这不是两根16g, 而是一根32g
  - 3. 开机按钮太细 因为按钮是窝在机器里，靠指腹根本按不下去，得用指甲掐。很不方便。

- DDR5 单根也是双通道

- ## [现在有政府20%补贴，同样配置买台式机整机是否比自己散装要更划算呢？ - 知乎](https://www.zhihu.com/question/666757762)
- 打八折后整机确实有一定优势，尤其是懒得动手或者不太懂DIY的用户，本来DIY还有价格优势，现在这波八折价格优势几乎被抹平了。
- 看了一圈电脑的，补贴主要针对的品牌整机笔记本一体机这类，单独配件不能单独补贴吧，也就是好像不能自己攒机器领补贴吧

- 即使是有20%政府补贴后依旧没看到性价比很高的整机，如果有，麻烦踢我一脚。

- 想买惠普暗影精灵10+显示器套装14代i5+4060ti+27寸2k显示器打折后6500这个价位，有点买主机送显示器的感觉

- 我也看了，确实没有。而且补贴的都是高价整机，他那个价格，你能自己挑配置攒一个更好的。

- 你如果去京东淘宝买那几个销量最高的主机应该是比自己组装更划算的，哪怕不需要补贴

- ## [为什么台式 PC 还处在组装（DIY）阶段？ - 知乎](https://www.zhihu.com/question/1899923881755678262)
- PC平台的DIY优势，使得它的每一个细节都专门化、专业化，因为它开放

- 我觉得所有消费电子产品都应该模块化, PC是唯一走在前面的

- 所谓的台式机DIY，说难听点，不过是一块大板各种插，再拧进一个足够大的箱子里。
  - 我的观点很简单，手机发展不出DIY市场，本质上是因为普通人都是手残，厂商能放心把一堆小东西扔给你自己装？
