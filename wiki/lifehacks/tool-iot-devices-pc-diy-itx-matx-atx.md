---
title: tool-iot-devices-pc-diy-itx-matx-atx
tags: [atx, iot, itx, matx, pc]
created: 2026-01-15T16:09:57.489Z
modified: 2026-01-15T16:10:18.077Z
---

# tool-iot-devices-pc-diy-itx-matx-atx

# guide

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
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Quiet Threadripper AI Workstation - 768GB DDR5 and 160GB VRAM (RTX 5090 + 4x R9700) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1qkghpk/quiet_threadripper_ai_workstation_768gb_ddr5_and/)
  - I managed to squeeze in RTX 5090 and four R9700 into a workstation build by fitting some GPUs vertically in the front section. Two power supplies: 1600W for the main system and most of the components, and a smaller 850W power supply for 3 of the Radeons (the power cable is threaded through the system popping out through a small gap left by RTX 5090).
  - DeepSeek-V3.1-Terminus with context = 37279 tokens: PP = 151.76 tps, TG = 10.85 tps
  - Motherboard - Pro WS WRX90E-SAGE SE
  - CPU - AMD Ryzen Threadripper PRO 7975WX
  - RAM - 8x KINGSTON 96GB DDR5 5600MHz CL46
  - GPU1 - ASUS TUF GeForce RTX 5090
  - GPU2 - 4x ASRock Creator Radeon AI Pro R9700
  - NVMe - 4x Samsung 9100 PRO 2TB
  - Power1 - Dark Power Pro 13 1600W 80+ Titanium
  - Power2 - Seasonic FOCUS V3 GX-850, 850W 80+ Gold
  - Case - Fractal Design Define 7 XL

- ## [为什么ITX架构的短显卡大部分都是Nvidia的，而AMD的高端ITX显卡则一卡难求？ - 知乎](https://www.zhihu.com/question/318806879)
- ITX 短卡就是一个细分市场, 事实上除了我国有一堆 K39, 鱼潮S3 这样的机箱, 其他国家基本都找不到类似的机箱.
  - 目前 N 卡阵营里的短卡主要以 [技嘉] 为代表, 包含 1060/1070/1080, 2060/2070 和 1660. 所以除了 1080Ti/2080 这些顶级旗舰货, 基本上甜品卡都有了.

- 最根本的原因在我看来是源自于n卡对笔记本市场的重视。笔记本受制于电源适配器，拢共就200w左右的供电能力，CPU和GPU（显卡核心）都要吃电的情况下，两位大哥都得控制住自己的功耗。
  - 一般就分给显卡90-140w，给cpu 60-90w，多了要么电源扛不住，要么散热顶不住。
  - 有了笔记本控制散热和电源的前提，设计芯片时，才会控制能耗比和发热，最终也就能做出适合itx的短卡、刀卡。
  - 由于nv在笔记本市场的排挤，amd很难把自己的芯片推销给成熟、有名气的笔记本厂商，并做出调教完美的好产品。

- 成本，公版vega就用上了均热板(而且大多数高端卡也都用上均热板了)，所以NANO用均热板是不会有什么成本增加的。

- ITX显卡市场是显卡市场下的另一个细分市场，太小众，AMD作为弱势方也没余力发展。
  - 而且ITX卡对能耗比要求较高，AMD在这方面没有优势。

- ## [贵的机箱和便宜的机箱，在使用体验上到底有多大区别？ - 知乎](https://www.zhihu.com/question/589948503)
- 真正好用的机箱，往往不算非常贵，其实是“[Silver Bullet]”级别的设计，假如题主需要个非常能“装”的机箱，那么无脑推荐追风者PK620，仅仅699的[E-AT]机箱，超级能装，比什么1499的酷冷H500M，两千多块的酷冷C700M都能装。
- 贵的机箱和便宜的机箱往往在功能方面区别不大，设计这个东西，不是简单用钱就能买到的。在机箱上花更多钱买到的一般是闪亮的钢化玻璃侧透，阳极氧化彩色铝合金外壳，RGB灯板等等并不是机箱内涵的主要成分。炫彩透亮的海景房，雪景房机箱。但是这不代表使用体验优秀。

- 一般来说200左右及以内的机箱撑死了就是个样子货。主要作用是把零件组合成一个箱子方便你搬走。
  - 用料实在太差。铁皮薄，塑料基本上都是二次料，脆的一批而且极易老化，接口质量差，这些大家可能都在说。不重复。
  - 基础结构设计不合理。比如[显卡] 装好后，[HDMI] 会把接口挡一半；背板空间狭小走不了大线；前面板线跳线长不够只能斜拉飞线（往往还不是全黑线）；等等类似的情况。太常见了。
  - 公差大。这个装机的人才能体会到……如果你玩模型的话就会知道一个东西叫做“组合度”，200左右的机箱基本都有这个毛病。从内到外的那种。你会发现主板上螺丝的时候螺丝孔位都对不上，需要稍微用一点点力才能把螺丝钻进去。
- 如果你预算再高一点，能提到500左右，一般能在上面1-3中改善或者解决一部分
  - 使用起来说实话，绝大多数人四五百的机箱就可以了。到这个价位，做工用料——尤其是接口和开关的质量基本就靠谱了。
- 更高价格的机箱更多的是给你更好的外形和功能，在“满足使用需求”方面没有什么更大的优势。
  - 静音全塔
  - 有说法是静音箱比侧透箱的电磁屏蔽能力要好一些。但实际上使用起来没有收集到什么肉眼可见的差异。

- 一般来说200左右及以内的机箱撑死了就是个样子货。这句话放在以前我高低给你举例反驳一下，现在反驳不了
  - 自从开始流行侧透之后基本就全是一天比一天烂，所以我才放心说这话的

- 大的安装的时候很方便，小机箱要是机器要维修故障了你会想砸了它
  - 所以不是特殊需求我都推荐买全塔机箱，或者上面或者前面能拆开的中塔

- ## [迎广和乔思伯的机箱为什么都那么贵？ - 知乎](https://www.zhihu.com/question/59837988)
- 乔思伯就是以低价格让群众享受到做工凑合还行的全铝机箱而出名的

- 乔思伯是我待选机箱里唯一一个用SGCC板材和5mm玻璃的。其它再良心一点的就是SECC和4mm玻璃，还有就是SPCC。但是乔思伯设计的觉得太差劲，不论是风冷还是水冷散热让人心里没底。迎广303确实漂亮，但是吐槽点有二：1、玻璃0.3，2、上置电源。以上只是个人观点，不喜勿喷！

- spcc就是冷轧钢，secc是电镀锌钢板，sgcc是热解锌钢板；
  - secc和sgcc比spcc好，但secc和sgcc各有优势，sgcc耐腐蚀更强，但secc保持了冷板的力学特性，在薄板的情况下强度有优势

- ## 📦 [机械大师C34 Pro机箱好用吗？缺点是什么？ - 知乎](https://zhuanlan.zhihu.com/p/642308682)
- 机箱使用了模块化设计，无论是上置电源还是下置电源，直插显卡还是竖装显卡，我们只需调节相应的模块即可，对硬件的包容性极高。
  - 比如尾部的7个PCIe槽位设计，中间的第2与3挡板是可以拆卸的，然后通过移动来实现ATX/MATX主板规格的转换。

- 在设计细节上，机箱最大可支持420mm显卡，让我后续在升级时也有了一定的选择。并且自带显卡支撑架设计，不必担心显卡太长会产生变形。不过显卡长度超过336mm的话，电源就不能下置安装。

- 作为一款适合摆放在桌面的机箱，其I/O面板放在了右下角处。从上至下依次为两个USB3.0 TypeA口、Type-C插口、3.5mm耳麦二合一孔、电源开关（内置白色LED）。

- 机械大师C34 Pro预留有2个3.5/2.5寸硬盘支架以及后置2个2.5寸固盘位，达成共计4个硬盘位的支持，满足不同用户的需求。考虑到我现在多是使用M.2 SSD固态硬盘，机箱通常也就只会用到后置的2.5寸硬盘位而已。

- 机箱底部预留了两个散热风扇安装位，可以进一步加速机箱内部的热量排出。

- 机箱背面拥有18mm理线空间，并且配备了穿线孔，线材走向不用过于拘谨，利于理线。

- C34 Pro是我见过配件方面最走心的机箱。第一次见螺丝钉自带配件盒，还附赠了磁吸螺丝刀、ATX/MATX切换组件以及防尘网。至于便携提手我并没有安装到机箱上，因为装入电源和显卡后的整体重量太大，单手提拿不动。

- [方糖机械大师 C34 Pro AIR版机箱参数 -ZOL中关村在线](https://detail.zol.com.cn/2114/2113024/param.shtml)
  - 429×205×349mm, 30.7L
  - 台式机箱（中塔），吸音降噪机箱，玻璃侧透机箱
  - 适用主板	E-ATX（加强型），ATX（标准型），M-ATX（紧凑型）
  - 显卡限长	420mm
  - CPU散热器限高	165mm
  - USB接口	2×USB3.0接口，1×USB3.1 Type-C接口纠
  - 至多支持：8×120mm风扇位
  - 支持：360/280mm水冷排
  - 我的atx的板子加170长的大电源加7900xtx超白金的显卡都塞进去了，而且用电源自带的线不带定制线也可以塞下。整个机箱大部分地方都可以卸掉螺丝拆下来，大大降低了装机难度。就是防尘网的孔太大了，感觉挡不住灰尘额。
  - 内部一个大双塔完全没问题
  - 机箱比较紧凑，就是冷排水管只有走右边，建议左边开孔稍微宽一点，其他还是很完美
  - 什么是万能机箱，这就是万能机箱，机箱永远的神，各种组装卡卡一弄很酷炫很方便便捷，ATX也能很小巧，推荐购买，物超所值，散热也很好
  - 34pro长一点比34好装多了，还能走下背线你敢信？
  - 可装下 ATX主板 + 360水冷 + 超长显卡的方案挺实用。
  - 这是我目前看到的，能装下atx主板和4080显卡的最小机箱
  - 这款机箱已经看了好久，因为贵，没舍得买，买了D40。无奈D40只支持240水冷，夹了汉堡也压不住13900f。还是选了这款，再折腾一遍
  - 适配vertex+4090公版+360水这种组合

- 🤔 [C34Pro装机兼容性完美，CS2终于跑满360决赛圈TK2和C34Pro，想到放桌下大部分时间看不到，对光污染也不感冒，选了更冷峻硬朗的机械大师，机箱兼容性吹爆，尺寸在ATX机箱中绝对算极限压缩hz - 小红书](https://www.xiaohongshu.com/explore/684bae9a000000002300fe85?xsec_token=ABDPZc4kz4GSpMhS22KwCsX8BjChgpSLV5ZsDCfogMlOE=&xsec_source=pc_search&source=web_search_result_notes)
  - 决赛圈TK2和C34Pro，想到放桌下大部分时间看不到，对光污染也不感冒，选了更冷峻硬朗的机械大师，机箱兼容性吹爆，尺寸在ATX机箱中绝对算极限压缩
  - 主板：B850战斧导弹大板，黑色机甲风配魔爪绿LOGO点缀恰到好处，遇到有线网连不上的通病
  - 显卡：瞄准5070ti，7.3K买到ADOC也算好价就当缘分
  - CPU：9800X3D对CS、吃鸡、魔兽三栖玩家致命吸引，叠券后板U套4.6K入手
  - 固态：三星990Pro 5090D富哥装机必选闭眼入
  - 电源：AMP GH850W颜值搭调，价格合适，蟒纹线和自带线梳脱颖而出
  - 风扇：联力猫头鹰超预算，龙鳞光效清爽，圆角矩形有辨识度，价格适中，两点不足：①光效不够均匀（LED少或匀光板不够厚）②噪音大带耳机都听得到，不过我能忍受
  - 水冷：5.31钛钽首发新品LG600，3.95英寸大屏出彩，差点装不下，C34Pro又是刚好兼容，屏幕跟上方风扇就1~2mm间隙

- ## 🛝 [Smallest possible ATX case that can fit a full size GPU : r/buildapc _202406](https://www.reddit.com/r/buildapc/comments/1djnxe3/smallest_possible_atx_case_that_can_fit_a_full/)
  - I currently have a mini itx setup with an i5 10400, and an rx 6700xt. It’s feeling like it’s time for an upgrade and microcenter’s CPU, MOBO, RAM combos are too good to pass up. ($370 for a Ryzen 7 7700x and 32gb of ram) Especially compared to the $700+ I would have to spend on those parts, an itx mobo and a capable SFX PSU.
- A case like the GameMax Meshbox Pro is probably the smallest you’re going to get without needing an SFX power supply, at about 33.5L in volume. Can still fit GPU’s up to 335mm in length, and is a very reasonable $62.

- ## [Looking for a Compact, Silent Server Case : r/homelab _202504](https://www.reddit.com/r/homelab/comments/1k6nbse/looking_for_a_compact_silent_server_case/)
  - Motherboard: ATX (specifically the Supermicro H13SSL, which I plan to use)
  - Support for 8 or more HDDs

- The N5 might check all the boxes—except for noise. It lacks any sound-dampening material.
  - 50L
- I'd use a Jonsbo n5 and dynamat the hell out of it if I found it too noisy. 

- ## [Looking for a compact case for my H11SSL-i - Hardware Hub / Build a PC - Level1Techs Forums _202311](https://forum.level1techs.com/t/looking-for-a-compact-case-for-my-h11ssl-i/203506)
  - I just received my H11SSL-i Supermicro motherboard with an Epyc CPU that has 16 cores and 256 GB of RAM. However, I am yet to find a suitable case for it. I am looking for a compact case that has at least 3 to 4 bays for 3.5-inch hard drives and another 3 to 4 bays for 2.5-inch drives. 
- Fractal Design Node 804 has really cornered this market, available for ~$140

- H11SSL-i is ATX, so no, it won’t fit in mATX cases.

- I can’t give advice about a case that fits your requirements, but for a reference, I’m currently using Fractal Define 7 Compact for my H11SSL-i + 7551P. The case only has 2x 3.5" drive bay with a cage underneath the bottom cover and 2x 2.5" drive behind the motherboard. I think if you don’t use the bottom PCIe slot, you may be able to fit two more 2.5" above the PSU. A standard Fractal Define 7 should fit, but it’s not compact 

- ## 📌 [求一款atx紧凑型机箱? - 知乎](https://www.zhihu.com/question/328153905)
- 最近我装了一台AMD平台的游戏PC，为了更好的扩展性我选择了ATX大板，但我又追求小巧机身和扩展性，所以还是有点难办的，在机箱的选择方面我也是研究了许久，最终结合实际、选择了设计非常独到的紧凑机箱：机械大师C34 Pro。
  - 这个机箱支持ATX/EATX板子，但尺寸只有429x205x349mm，比常规的ATX机箱小了很多，但模块化的独特设计让它具备了非常棒的扩展性和可维护性
  - CPU：AMD RYZEN 7 9700X
  - 主板：蓝宝石NiTRO+氮动B850A WIFI
  - 内存：佰维DW100 DDR5 6800C32
  - 显卡：公版RTX 4080
  - 硬盘：系统盘·西部数据SN750 500GB；游戏盘·致态TiPro9000 4TB
  - 机箱：机械大师C34 Pro, 429*205*349mm, 30.6L
  - CPU散热器：追风者Polar伯乐T6
  - 电源：安耐美白金竞蝠PK1000W
  - 机械大师C34 Pro这个机箱正面金属质感尽显，看起来极为优雅

- [有没有什么体积比较小的ATX机箱推荐. 台式机？ - 知乎](https://www.zhihu.com/question/51668457/answers/updated)

- ## [双 RTX 5060 Ti 白色家庭工作站 乔思伯 - 小红书](https://www.xiaohongshu.com/explore/687ab0d4000000002203d812?xsec_token=ABsbkh11yQDdy4hEUo0ho9xZjLdOVOCgvh31n3gg0Yyw8=&xsec_source=pc_search&source=web_explore_feed)
  - 主板：华硕 Z690 Formula
  - 机箱：乔思伯 D41 MESH
  - CPU：i7-14700
  - 显卡1：微星 RTX 5060 ti 16GB TRIO
  - 显卡1：技嘉 RTX 5060 Ti 16G
  - 内存：64GB DDR5 6400 CL32
  - 硬盘：Kioxia KXG80ZN84T09 4TB
  - 电源：海盗船 RM750e ATX 3.1
  - AIO：酷凛 FX360 PRO
  - 风扇：8 x Arctic BioniX P120

- ## 🌰 [5k2k 144Hz Dual GPU LSFG Setup : r/losslessscaling _202504](https://www.reddit.com/r/losslessscaling/comments/1k837cb/5k2k_144hz_dual_gpu_lsfg_setup/)
  - Just here to share my completed dual GPU build, managed to get stable 144fps in MH Wilds with LSFG 3.0 Fixed x3 with 80 flow scale, HDR enabled. And my goodness the gameplay looks incredible smooth.
  - CPU: AMD Ryzen 7 5800X3D 
  - GPU for Rendering: ASRock RX 9070 XT Steel Legend 
  - GPU for LSFG: VASTARMOR RX 7650 GRE (I bought it from China Taobao) 
  - GPU Undervolt settings: 9070 XT -80mV, -10% PL, 2700MHz Memory 7650 GRE -60mV, -6% PL
  - RAM: 4 x 16GB DDR4 3200MHz CL16
  - power: FSP Hydro Ti PRO 1000W
  - case: Jonsbo D41 Mesh Screen (White)
  - Fun fact: The total cost of getting these 2 GPU is still lower than any rtx5080 I can find in my region ffs.
  - My top GPU takes like 2.9 slot (only left about 2mm clearance between GPU), bottom GPU takes 2.4 slot, if I removed the bottom fans it can easily fit a full size 3 slot card, but the air flow will be worse obviously.
  - I should have mentioned my case fans arrangements too: 1 x front intake, 2 x bottom intake, 1 x top (front) intake, 1 x rear exhaust, 2 x top (rear) exhaust

- Nice looking build but that top GPU will be starving for fresh air. I tried the same with my build and ended up getting another case so I could move the bottom card into a vertical mount on a riser.

- I'm interested about temps after ~1 hour or longer game session
  - So far my top GPU hotspot temp can be kept below 83C range, VRAM temp around 95C worst case, from I have seen 9070XT memory temp is hot across all AIB partner, I will just live with it..
  - So far my top GPU hotspot temp can be kept below 83C range, VRAM temp around 95C worst case, from I have seen 9070XT memory temp is hot across all AIB partner, I will just live with it.

- ## [乔思伯推出松果 D41 ATX 系列机箱，该产品都有哪些亮点设计？ - 知乎 _202212](https://www.zhihu.com/question/572085484)
- 乔思伯为CR3000风冷散热器标成了260瓦的热解能力
  - CR3000风冷散热器为非常传统的双塔结构，整体尺寸为120x132x160mm，在选配机箱时请注意散热器兼容高度，像D41这种就能完美装入。 

- https://www.zhihu.com/question/477140818/answer/3215457076
  - 这不就是我的乔思伯D41嘛！我也在考虑风道问题。目前最合理的安置方式就是：1. 底部风扇吸气兼给显卡供风；2. 电源风扇朝前，往上吹风；3. 前置小风扇里吹气，兼吹显卡；4. CPU及后置风扇往后吹。
  - 另一种不合理的方式就是，整体从后往前吹，调转电源风扇从机箱内部吸气，前置风扇从内部吸气。

- ## [乔思伯发布松果 D31 紧凑型 M-ATX 机箱，支持到 360 水冷排, 散热性能怎么样？ - 知乎 _202210](https://www.zhihu.com/question/562398994)
- 机箱副屏是一个亮点，紧凑型机身能放下360一体水冷，想法不错。但是目测会有些问题，比如我购买就是乔思伯TF360一体水冷散热器，水泵在水管上，距离冷排进出水口不到10厘米（可能不准）位置上。若使用D31的话，电源可能无法安装在LV1或者LV2的位置

- [乔思伯松果D31机箱简介。含D31机箱推荐的装机配置方案 - 知乎](https://zhuanlan.zhihu.com/p/583985999)
- 乔思伯松果D31的总体结构和D30相似。支持M-ATX主板，电源前置，顶部安装水冷。区别在于D31更大，顶部和底部可以安装360水冷，TYPE-C接口也改成了真正的（D30是和USB并线的）。
- 目前类似结构，支持顶部安装360水冷的机箱还有华硕的冰立方AP201。

- 乔思伯松果D31仅有一个机械硬盘位置，并且这个位置是底部的一个风扇位，风扇和硬盘只能二选一安装。
  - 有2个2.5寸SATA固态硬盘位。

- ## 📌💡 [有哪些巨好看的机箱？ 机械大师 - 知乎](https://www.zhihu.com/question/347824157/answer/1841037981)
- 机械大师C系列全金属机箱了解一下
- 目前机械大师C系列有C24、C26、C28、C34一共四款机箱，这四款机箱由小到大，涵盖了从ITX超小体积到最高ATX双水冷的性能支持。
  - 不同的尺寸，统一的设计思路。全系列采用家族式设计，除了兼容硬件的不同和多变的用法外，框架材质、设计思路均保持高度的一致。
  - 全系列均采用可拆卸外壳与主体框架分离式设计
  - 因外壳的可更换替代性，所以延伸出了更多的的色彩方案
  - 为了增加便携性和更好更方便的移动机箱，在机箱的顶部均设置了一个铝合金的可拆卸式提手
  - 适应各类电源的不同朝向，电源位置均设计了不同大小的可变角度电源支架
  - 机箱除了标配的金属前面板和玻璃侧透外，还可以选择更换为带散热开孔的铝侧板和斜开孔的AIR前面板
- C24小方糖 9.9L
  - C24不仅是整个C系列中尺寸最小的一款，也是便携性最好的。实测大一点的的非分仓式双肩包都可以放的下。
  - 249 x 249 x 155 mm, 9.6L
  - 支持130mm的塔式散热，还包括显卡直插、SFX电源支持和多硬盘多风扇位的支持。不仅能保证储存空间，还能最大限度的构建有效散热风道
- C26声波 13.3L
  - 支持M-ATX主板，还增加了显卡选择上的宽容度。
  - 并且在搭配水冷硬盘拓展支架时，使用ITX主板可以安装更多的硬盘；还可以安装240水冷，实现更强散热。
  - C26 Plus 15.1L
- C28 脉冲/小视界 17.9L
  - 243 x 284 x 185 mm, 12.7L
  - C28是C系列里可手提的M-ATX机箱中体积最大的一款，但即便这样，在和市面上其他品牌的部分ITX机箱或者是紧凑型的M-ATX机箱比，C28的体积也是小的多
  - 可以在顶部和底部支持安装240水冷，即使使用风冷散热，C28最高也可支持到162MM的塔式风冷散热，丝毫不妥协散热的规格
  - 335mm的显卡长度和高塔散热的支持，保证了旗舰级性能的稳定释放
- C34视界 22.8L
  - 342 x 342 x 185 mm, 21.6L
  - C34是整个C系列中最大的存在，也是唯一一个标配没有带提手的型号，因为他相较与另外三款机箱，装满后会比较重

-  🌹 [C34 Pro](http://www.m-master.cn/pd.jsp?id=22)
  - 429mm x205mm x349mm, 30.6L; 产品尺寸 429*205*403mm, 35.4L
    - 🎒 特大号的双肩包的高度可以满足450mm, 底部长宽难以满足 205x403
  - 显卡支持 420mm以内
  - 主板支持 ATX/EATX/MATX/ITX
  - 散热支持 165mm风冷/360水冷/280水冷
  - 电源支持 ATX(200mm长以内）
  - 2.5寸硬盘位 至多4个
  - 3.5寸硬盘位 至多2个
  - 支持ITX、MATX、ATX和EATX主板，水冷也能安装360尺寸，风冷最大165mm塔式。
  - 外壳为2mm铝合金，内壳是1mm钢板，全身使用白色喷漆
  - 净重：6.2KG / 毛重：7.4KG, 🐛 比普通机箱重很多

- https://www.zhihu.com/question/391355479/answer/2789629897
- 此外C26是只支持SFX电源，C26PLUS和C28为了安装长显卡或者水冷等等情况，也只能安装SFX电源，所以在电源方面会增加一些成本。
- 另外机箱安装方面，这些机箱都不算非常好安装，基本都得拆卸所以的板材才能进行安装，所以有螺丝大师这么一个称号。此外还没有背线空间，所以最好是做定制线，才能得到一个比较完美的装机效果。
- 这几款可以背后理线吗
  - 这几款都不可以

- [用绝版机箱打造极致生产力——9950X+192G大内存 - 知乎](https://zhuanlan.zhihu.com/p/1943668215206122278)
  - 【主板】微星 B850M MORTAR WIFI 迫击炮 （1499￥）
  - 【CPU】AMD R9 9950X 全新盒装 （3999￥）
  - 【内存】海盗船 (196G) 48G*4 6000MHz C30 （5398￥）
  - 【显卡】微星 万图师 4070 Super 2X （5499￥）
  - 【机箱】机械大师 C26PLUS （停产）
  - 【散热】猫头鹰 C14S + 猫头鹰 NF-A14 PWM （579+180￥）

- ## 📌💡 [2025年5月更新，电脑机箱推荐。推荐一波高颜值的机箱。包含ITX, M-ATX, ATX, E-ATX机箱 - 知乎](https://zhuanlan.zhihu.com/p/210537601)
  - [2025年5月更新，电脑机箱推荐。推荐一波高颜值的机箱。包含ITX, M-ATX, ATX, E-ATX机箱](https://www.zhihu.com/tardis/zm/art/210537601)

- 背包的可选尺寸
  - 50L: 3.6 x 1.8 x 5.4
  - 60L: 3.8 x 2.0 x 5.6
  - 65L: 3.8 x 2.2 x 5.8   ==> 48.5L
  - 80L: 4.0 x 2.2 x 6.5   ==> 57.2L
  - 85L: 4.2 x 2.4 x 6.6   ==> 66.5L
  - 朗斐双肩包男背包 / 三栖虎 / 袋鼠旅行背包
    - 85L: 4.2 x 2.4 x 6.6 
  - 守护者70L变85升
    - 70L: 4.8 x 2.7 x 6.8  , 款式运动 ✅
    - 多处挂载系统
  - 金利来（Goldlion）长途旅行打工大容量
    - 85L: 4.3 x 2.4 x 6.7 , 上方很窄
  - 黑色85升1920# /防滑胸扣/减负腰带
    - 85L: 4.3 x 2.6 x 6.9 ==> 77.1L ,  太高了
    - 70L: 4.1 x 2.3 x 6.0 ==> 56.6L
    - 55L: 3.8 x 2.0 x 5.5 ==> 41.8L
  - 酷奇袋鼠大号80L超大容量登山包双肩包
    - 80L: 4.3 x 2.6 x 6.7 ==> 74.9L
    - 80L: 4.1 x 2.3 x 6.7
    - 80L: 4.0 x 3.0 x 6.6
  - 85升超大容量加
    - 85L: 4.2 x 3.5 x 6.2

- tips-cases
  - 找机箱时在知乎或论坛找效率低，可直接在京东店铺找，优秀的商家会把各系列的机箱尺寸都在商品详情页并排列出，对比看尺寸/功能/价格效率更高
  - 寻找产品时，直接按销量排序，然后根据热门产品的评论内容搜索竞品更快

- [Choose A Case - PCPartPicker](https://pcpartpicker.com/products/case/)

- Cooler Master Elite 361  25.1L
- Jonsbo D40  	31.6 L
- Jonsbo U4 Plus  	31.7 L
- Jonsbo D41 MESH  	35.4 L
- KOLINK Observatory MX Mesh ARGB  30.8L
- KOLINK Inspire K4  33.4L
- GameMax MeshBox Pro  33.5L
- Silverstone RM42-502  35.4L

- Cooler Master 
- Cooler Master 400L
  - 411 x 218 x 410mm, 36.7L
  - 主板: itx/matx
- Cooler Master Qube 500 / Q500L
  - 380 x 231 x 381mm, 33.4L
- Cooler Master MasterBox 600L V2 智瞳600 🤔 /非mesh版
  - 400 x 204 x 455mm, 37.15L, 仅比d41高1.5cm
- Cooler Master QUBE 500 Flatpack  38.9L
- Cooler Master Elite 371  38.7L
- Cooler Master CMP 320  38.6L
- Cooler Master Elite 330/334/500  38.2L
- Cooler Master MasterBox MB600L V2  37.7L
- DIYPC Solo-T1  38.9L
- Deepcool MACUBE 110  38.8L
- Deepcool CC360 ARGB  38.7L
- Deepcool CH370  38.3L
- Zalman P10 NAMU  38.6L
- Zalman Z1 Iceberg  38.5L
- Zalman S3/S2/Z3  38.4L
- Thermaltake V3   38.5L
- Silverstone Lucid 04  38.2L
- Lian Li PC-V650  38.2L
- Lian Li PC-C32B  37.4L
- Lian Li PC-V359W  36.6L
- Jonsbo UMX4/U5/VR4  38.0L
- Phanteks Eclipse P300  36L
- Fractal Design Core 2300/2500  37.8L
- Fractal Design Meshify C Mini  36.6L
- Fractal Design Pop Mini Air  36.5L
- Fractal Design Focus G Mini  36.4L
- Fractal Design Define Mini C /Tg  35.7L

- 迷你小钢炮ITX机箱推荐

- 酷冷至尊魔方 NR200/NR200P
  - 箱体长宽高（mm）376 x 185 x 292mm, 20.3L
  - 支持ITX和DTX规格的主板
  - 只能用SFX电源。ATX电源需要自己DIY支架，而且会限制显卡长度
  - 酷冷最近推出了NR200P MAX版本。顶部预装了280水冷。自带850W电源，显卡只能竖装。设计不错。

- 分形工艺Torrent Nano
  - 支持310mm的显卡
  - 支持20CM长的ATX电源
  - 这款属于体型偏大的ITX机箱，散热设计优秀，价格稍贵。这款机箱比较适合做风冷散热方案。

- 乔思伯（JONSBO）A4 Ver1.1版本
  - 340MM (深) x 169MM (宽) x 273MM (高)
  - 使用SFX或AFX-L电源

- M-ATX机箱推荐

- 方糖机械大师 C+Max
  - 392*185*284mm, 20.5L
  - 支持M-ATX和ITX主板。
  - 电源可以用SFX或14cm长的ATX电源。
  - 支持240水冷或162mm高的风冷
  - 价格小贵，在800元附近

- [乔思伯 Z20](https://www.jonsbo.com/products/Z20--.html)
  - 370*186*295mm, 20.3L
  - 显卡支持长度：≤363mm
  - 支持240水冷，或最高160mm的风冷
  - 1个机械硬盘位

- 乔思伯C6 MAX
  - 202 x 349 x 295mm, 20.8L
  - 显卡: ≤  300mm-335mm

- 先马（SAMA）趣造I'm Mini
  - 391（长）*185（宽）*303（高）mm, 21.9L
  - 显卡限长：≤33cm
  - 支持M-ATX和ITX主板

- 联力 A3
  - 443 x 194 x 396 mm, 34L
  - 最高支持165mm的风冷。支持360水冷
  - 最长支持415mm的显卡。底部支持安装一个机械硬盘

- 华硕AP201 冰立方
  - 205mm*350mm*460mm, 33L
  - 显卡（连供电头总长度）限长≤32cm
  - 硬盘位3个
  - 支持的主板：M-ATX，ITX, 🐛 不支持ATX
  - 支持的是M-ATX主板，总体布局和乔思伯D30类似，但是华硕AP201采用的是全打孔面板，且顶部支持360水冷，散热非常的不错，支持TYPE-C USB 3.2 GEN2（乔思伯D30的type-C是和USB并在一起的）。

- 乔思伯 D31 mesh 🌹
  - 产品尺寸：205 (宽) *347.5 (高) *440mm (深)（31.3L） 
    - 205mm（宽）*363mm（高）*452mm（深）（机箱总尺寸）
  - 显卡长度：330-400mm
  - 主板支持：ITX / DTX / M-ATX, 🐛 不支持atx
  - 机械硬盘位：2.5〞SSD*2 + 3.5〞HDD*1
  - PCI扩展槽：4
  - 电源类型：ATX

- 乔思伯 D32 STD MESH
  - 384mm * 207mm* 302mm， 24L
  - 兼容主板：MINI-ITX / MICRO-ATX标准型 / MICRO-ATX背插型

- 乔思伯 D32 PRO MESH
  - 384mm * 207mm* 302mm， 24L
  - 兼容主板：MINI-ITX / MICRO-ATX标准型 / MICRO-ATX背插型(机箱需切换至B模式)

- 乔思伯 D40 /无mesh导致散热差
  - 204mm (W) *401mm (D) *386mm (H), 31.51L
  - 硬盘位：2.5〞*3+3.5〞*1 or 2.5〞*4
  - 显卡支持长度：293-374mm
  - 主板支持：ATX/M-ATX
  - 前置接口：USB3.2 Gen 1 Type-C*1(5Gbps)     USB3.2 Gen 1 Type-A*1(5Gbps)     复合式音频接口*1
  - PCI扩展槽：7
  - 电源：ATX PSII≤140-200mm

- 乔思伯 D41 mesh 🌹 /~~放不进背包~~
  - 205mm (宽) *392mm (高) *440mm (深)（容积：35.4L）
    - 总尺寸  205mm*407mm*452mm, 37.7L
  - 显卡支持长度: 330-400mm
  - 主板支持：ATX / M-ATX
  - 电源：ATX电源
  - CPU散热器：168mm
  - 水冷支持：顶部：240/280/360*1        后部：120*1      底部：240/360*1
  - 硬盘位：2.5〞SSD*3 + 3.5〞HDD*2
  - 前置接口：USB3.2 Gen 2 Type-C*1         USB3.0*1/Audio & Mic*1
  - 净重：6.6KG        外箱+机箱：7.6KG

- 乔思伯 U4 Pro
  - 205mm(W) * 395mm(D) * 426mm(H)（含脚垫）, 34.5L
  - 显卡支持长度：≤280-330mm
  - 主板支持类型：ITX / M-ATX / ATX
  - 电源支持：ATX≤170-190mm

- ATX（中塔）机箱推荐
  - ATX（中塔）机箱是目前大部分用户的选择，这类的机箱尺寸偏大，基本都支持ATX，M-ATX，ITX版型，部分支持包括E-ATX在内的所有版型。
  - 优点在于散热好，ATX机箱基本都支持240及360水冷，对大型双塔风冷散热的支持也更好。扩展位多，方便安装更多的硬盘等设备。

- 先马（SAMA）朱雀se 🌹 /前板网孔散热
  - 3.96*2.15*4.82mm, 41.03L
  - 主板兼容: ATX/MATX/ITX
  - hdd*2, ssd*1
  - 显卡限长 345mm
  - 散热限高 163cm
  - 水冷支持 360/280/240
  - 支持显卡竖装
  - 机箱重量 <5kg
  - [朱雀se - 先马官网](http://www.sama.cn/archives/9452)
  - [【先马 朱雀SE（黑）】先马（SAMA）朱雀SE黑色 台式电脑主机箱 前板散热网孔/支持ATX主板/360水冷/竖装显卡/双面防尘/Type-C预留孔【行情 报价 价格 评测】-京东](https://item.jd.com/100135456146.html)

- 先马（SAMA）朱雀air 
  - 4.08×2.33×4.62mm, 43.9L

- 先马（SAMA）黑洞7pro 🌹
  - 4.05×2.15×4.82mm, 41.97L
  - 显卡限长 345mm
  - [【先马 黑洞7 PRO（黑）】先马（SAMA）黑洞7pro中塔式吸音降噪电脑主机箱黑色 标配2把降噪风扇/高分子树脂棉/支持ATX主板/竖装显卡【行情 报价 价格 评测】-京东](https://item.jd.com/100075167747.html)
  - 先马（SAMA）小黑洞pro  /MATX
    - 4.17×2.15×4.25mm, 38.1L
  - 先马（SAMA）黑洞7 
    - 3.9×2×4.46mm, 34.8L

- 先马（SAMA）平头哥M2 Pro
  - 4×2.1×4.45, 37.38L
  - 显卡限长 325mm
  - ATX/MATX/ITX
  - 钢化玻璃侧透

- 酷冷至尊 600L v2 🌹 /无mesh
  - 400x204x455.3mm, 37L
    - 包括突出物	405.5x204x455.3mm, 37.6L
  - 主板兼容性	Mini-ITX, Micro-ATX, ATX
  - 显卡	 350mm (w/o front fans & radiator)
  - 电源	160mm
  - CPU 散热器	161mm

- 酷冷至尊 Q500L /比D41小
  - 386 x 230 x 381mm, 33.8L
  - 主板兼容	Micro-ATX, Mini-ITX, ATX
  - 显卡限长	360mm
  - CPU散热器限高	160mm
  - 硬盘位	1*HDD+2*SSD
  - 电源支持	顶部前支架, ATX PS2
  - 净重	3.83kg

- 酷冷至尊 酷方500
  - 380 x 231 x381mm， 33.4L; 
    - 包含凸起 406 x 231 x 415mm, 38.9L
  - 主板兼容性	ATX / Micro ATX / ITX / E-ATX最大 280mm
  - CPU 散热器	164mm~172mm (移除侧面水冷支架)
  - 电源	与GPU无干涉 ：173mm, 最大尺寸：216mm(不计理线空间) 
    - 底部安装时：332mm (不计理线空间)
  - 显卡 365mm

- 酷冷至尊 MB400L
  - 411 x 218 x 410mm, 36.74L
  - MATX

- 分形 North /支持全mesh且无玻璃
  - 4.33*2.15*4.5, 41.9L; 
    - 整机尺寸 4.47*2.15*4.69, 45.07L

- 长城（Great Wall）商逸R40/R41
  - 4.09×2.03×4.4, 36.5L
- 长城（Great Wall）商逸R50
  - 4.25×2.03×4.65, 

- 长城（Great Wall）本色K13 v6
  - 3.94×2×4.56, 35.9L
- 长城（Great Wall）本色K13
  - 3.96×2×4.51, 35.7L
  - 显卡限长 340mm

- 爱国者（aigo）A15
  - 3.7*1.9*4.38, 30.8L

- 爱国者 yogo t21
  - 4.08×2.3×4.6, 43.1L

- 鑫谷无尽1 /单面玻璃侧透/有点小
  - 3.6x2.3x4.35, 36L; 
    - 整机尺寸 3.95×2.3×4.55, 41L

- 鑫谷无界1 /2面玻璃海景房/无mesh
  - 4.2x2.1x4.65, 41L; 
    - 整机尺寸 4.38x2.1x4.85, 44L

- 航嘉 GX750A 
  - 4.3x2.18x4.35, 40.7L; 
    - 产品尺寸 4.65x2.18x4.61, 46L
  - 侧边网孔散热

- 游戏帝国（GAMEMAX）冰魔方mesh
  - 401 x 204 x 386mm, 31.57L

- ## [2024年最新ATX小机箱推荐 - 知乎 _202401](https://zhuanlan.zhihu.com/p/680148767)
- 既想要主机够小，又想要ATX主板的拓展性是很难达成的，于是很多人退而求其次选择MATX主板和MATX机箱。但ATX小机箱依然是很多人的执着所在。作者对市面上目前在售的ATX机箱进行了粗略的梳理，发现目前较小的ATX机箱主要有以下这些

- 缔誓科技L59p 体积13.2 L 售价：499
  - 尺寸数据：400x90x368

- Ssupd Meshroom S 体积：14.93 L
  - 尺寸数据：247x167x362

- 傻瓜超人K99air 体积：21.48 L 售价：129
  - 尺寸数据：348x186x328

- 机械大师C34 体积：21.65 售价：799
  - 尺寸数据：342X85X342

- 乔思伯RM2 体积：22.34 L 售价：299
  - 尺寸数据：209x302x354

- 铝小宝p100 体积：24.9 L 售价：179
  - 尺寸数据：375x185x359

- 巧美 云雀plus 体积：25.03L 售价：217
  - 尺寸数据：394x165x385

- SKTC Q5 体积：27.97 L 售价：299
  - 尺寸数据：370x210x360

- [2023年ATX小机箱推荐](https://www.zhihu.com/tardis/zm/art/632965955?source_id=1003)
- 傻瓜超人K99 青春版，体积约为19L，售价：159
  - 尺寸 375x158x325mm

- 机械大师C34视界 体积21.6L 售价：729
  - 尺寸：342x342x185mm

- 机械大师c34 pro 体积30.6L 售价899
  - 尺寸：205x349x429

- 乔斯伯rm2 体积约为21.5L 售价：245
  - 尺寸：209x302x354mm

- 乔思伯 u4 体积约为30L 售价299, 已停产
  - 尺寸：205MM (W) * 340MM (D) * 428MM (H), 29.8L 
  - [乔思伯JONSBO](https://www.jonsbo.com/products/qiaosiboU4baiban.html)

- 乔思伯 u4pro 体积34.5L 售价299
  - 尺寸：205x395x426

- 乔思伯D41 体积35.4L 售价249
  - 尺寸：205x392x440

- 魔神m90pro 体积约为20L 售价199
  - 尺寸：157x325x395mm

- ## [24年市售微小型atx机箱速查表大全，最小也是最大 - 知乎](https://zhuanlan.zhihu.com/p/715494773)
- 小是体积小，大是能够容纳ATX主板和ATX电源

- 方糖机械大师 c34体积22.6L，c34pro体积30.6L
  - 特点是他有6种电源摆放方式，根据个人需求进行摆放

- 酷冷至尊特警365
  - 25.6L
  - 酷冷至尊Q500L
  - 27.9L

- 乔思伯C5, 停产型号
  - 218MM (W) * 360MM (D) * 439MM (H), 34.5L
- 乔思伯（JONSBO）U4 Pro
  - 34.5L

- 先马（SAMA）黑洞7
- 长城（Great Wall）本色K13

- ## 🤔 [Can you use an ATX server board with a consumer tower case and power supply? : r/HomeServer _202006](https://www.reddit.com/r/HomeServer/comments/gy4i70/can_you_use_an_atx_server_board_with_a_consumer/)
- If it is true ATX, then yes. ATX is ATX. For a board to claim to be ATX, it needs to fit in the standard ATX size with standard ATX standoff locations and a standard ATX motherboard and CPU connector.
  - Looking at these, they all say they are ATX formfactor and have either 20 or 24-pin mainboard power and 4 or 8 pin CPU power connectors. So yes they will work.
  - For cooling, generally the board itself doesn't need any special cooling requirements, but the motherboard may list a minimum airflow rate in the manual. Remember not all servers are rack servers.

- I think/know you can wire up and get a supermicro mobo running with a consumer psu. Many supermicro are e-atx. They do have matx boards however. It says atx so its atx. You may need a fan controller for a supermicro hacking box. Looks like it would fit. Power wont be an issue.

- The first thing I would look out for is the form factor. Some boards are larger than ATX size, e-atx is sort of a nebulous non-standard, sometimes the server boards have screws laid out in a different location than a typical computer case 
  - The second thing is power, especially if the motherboard is dual CPU, it may have one or two 8-pin EPS connectors, which can be hard to find on a consumer power supply

- [Epyc, supermicro motherboard and ram, cheap on ebay... What else to consider? Or refurbed z840 dual xeon : r/homelab _202401](https://www.reddit.com/r/homelab/comments/1989fsp/epyc_supermicro_motherboard_and_ram_cheap_on_ebay/)
  - Im not sure if the supermicro h11ssl needs some special case/ mounts? Do I need a special PSU? I'll need a heatsink fan etc for the CPU. I'll be able to reuse my graphics card, I think it's a GTX 1080.

- Supermicro H11SSL-i should be standard ATX. There is a link on the page to the motherboard manual. It will specify PSU requirements.

- supermicro h11ssl is a standard atx board. any atx chassis shall allow you mount it without issue. PSU is also standard. The board requires standard ATX power and a 8-pin CPU power.

- The H11SSL is a standard ATX board, I've got mine in a Phanteks Enthoo Pro case with no issues as far as mount holes lining up, running off a Thermaltake 1050w PSU. The 1080 will be fine on that board as well, it's new enough to support UEFI firmware, I've run a 2060S, P100, and 4080 on mine with zero issues.

- Running a 7302P here, you'd want an H12SSL for PCIe4.0 as far as I'm aware, seeing as my 4080 is still on a 3.0 link with the H11SSL.

- ## [Supermicro + 4x 3090 build: Idle Power Consumption, Case, Cooling, PCIe 4.0 riser, Noise : r/LocalLLaMA _202410](https://www.reddit.com/r/LocalLLaMA/comments/1g54h9l/supermicro_4x_3090_build_idle_power_consumption/)
  - Supermicro H12SSL-i motherboard (5x PCIe 4.0 x16)
  - AMD EPYC 7282 CPU (128 PCIe lanes)
  - 256GB (8x32GB) 2133P DDR4 ECC RAM
  - Noctua NH-U14S TR4-SP3 CPU Cooler
  - 4x RTX 3090 GPUs SilverStone HELA Series HELA 2050R Platinum 2050W ATX 3.0 Power Supply
  - 4x PCIe Riser Cables 2TB NVMe M.2 SSD
  - Case: I'm still unsure about the case - how to pack all these components while ensuring good airflow and cooling? What would you recommend to ensure proper cooling? It seems to me that there are no perfectly fitting enclosures available. It looks like I might have to build the case myself, or what do you think?

- I have a build with dual 3090s, and I’ve encountered an issue with the H12SSL-i motherboard. The Noctua fans don’t spin fast enough at low RPMs, which causes the motherboard to constantly ramp them up to 100%, then stop, then ramp them up again. I’ve tried various IPMI configurations available online, but nothing seems to work, even with settings like this:
  - Not with the H12SSL, but I have a few X11DPIs and I had your same issue initially. I can check the IPMI command I'm using tomorrow if you want, it solved it for me. Basically, you need to change the minimum rpm setting as a percentage, IIRC.

- Quad setups are physically tricky. Reconsider open frames, they give you significantly more flexibility with positioning of GPUs and risers. Airflow is fine the cards have their own coolers and at most need an intake or two aimed at them depending on how you position.

- ## 🌰 [New server build : r/homelab _202509](https://www.reddit.com/r/homelab/comments/1lve852/new_server_build/)
  - CPU: AMD Epyc 7443P
  - Motherboard: Supermicro H12SSL-i
  - Memory: 8x SK Hynix 32GB 3200MT/s ECC (265GB)
  - SAS HBA: Broadcom 9400-16i
  - NVME HBA: Supermicro AOC-SLG4-4E4T
  - NIC: Mellanox ConnectX-4 dual 25G
  - NVME Backplane: Silverstone RAC-BP-304N
  - CPU Cooler: ARCTIC Freezer 4U-M
  - PSU: Corsair RM850x
  - Case Silverstone RM43-320-RS: 442  x 175 x 660 mm, 51L

- [Academic/Cryo-EM Build: EPYC 7402 with Supermicro H12 : r/Amd](https://www.reddit.com/r/Amd/comments/ij0h5k/academiccryoem_build_epyc_7402_with_supermicro_h12/)
  - CPU	EPYC 7402
  - Motherboard	H12SSL-CT
  - Case: be quiet! Dark Base Pro 900 Rev. 2 ATX Full Tower Case, 52L

- [Finally got around to building my home server! (AMD EPYC Proxmox Build) : r/homelab](https://www.reddit.com/r/homelab/comments/10egnxx/finally_got_around_to_building_my_home_server_amd/)
  - I was hoping to get the Meshify 2 (or Meshify 2 XL) but I couldn't find a single one in stock in Europe so I settled for the Define R6 (543 x 233 x 465 mm, 58L).

- ## [[FS][USA-NY] EPYC 7232 ROME CPU + H12SSL-NT PCIe 4 Motherboard + 4U 24 Bay server case + Add ons : r/homelabsales _202501](https://www.reddit.com/r/homelabsales/comments/1idbdvk/fsusany_epyc_7232_rome_cpu_h12sslnt_pcie_4/)
  - ATX 850 Bronze PSU: 850W 80+ Gold
  - Epyc Rome 7232 8 core processer 
  - Supermicro H12SSL-NT
  - 88GB RAM DDR4 2133
  - OWC Quad NVME 3.5HDD adaptor
  - LSI 9300-16i HBA
  - Jeyi PCIe 4x16 Quad NVME Bifurcation adaptor 
  - Generic Brand PCIe 3x8 QUAD NVME adaptor
  - 40G Mellanox QSFP NIC
  - NO CPU cooler provided
  - PRICE $1150 + Shipping based on location
  - Moved to a sliger case with an EPYC Siena build, so looking to off load his server
  - RM43-324-RS: 4U 24-bay 2.5"/3.5" HDD , 442mm (W) x 175mm (H) x 660mm (D), 51.1L

- ## [[W] Supermicro H12SSL / Epyc / DDR4 3200Mhz : r/homelabsales _202308](https://www.reddit.com/r/homelabsales/comments/163s183/w_supermicro_h12ssl_epyc_ddr4_3200mhz/)
- Yeah, that board has 2x M.2 and 1x Slimline x8. So that's pretty decent, because that 1 slimline port can handle 2 U.2 drives or even 2 M.2 with an adapter. (Or you can get a cable that goes to 8x SATA or 2x Mini SAS, for a backplane) I like those connectors a lot, but the cables aren't cheap.

- I have 128GB ram, 7343 CPU
  LSI 9300 HBA 10w
  a GTX 1660 Super that idles at 13-15w
  2x U.2 that are a bit power hungry, but fast. 10-20w each
  2x M.2 at about 9w each
  and 20 WD HC530 HDD's.

- Take a look at the Gigabyte MZ32-AR0. Just got one with a 7502. It's a very nice board with a ton of features

- Hey mind sharing what cooler have you been using? Trying to find something quiet but it seems Noctua''s are the only option? Wondering if the BeQuiet DarkPro for TR4 would fit this board
  - I love Noctua and have several of them, but for EPYC and TR it seems the ARCTIC Freezer 4U for AMD TR4 is the way to go. It's very quiet and should be able to handle 300 Watts.
  - I think one reason I ended up going with it was because the Noctuas didn't fit into my 4U case.

- ## ["The Talking Cube" 4x3090 local AI server : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1aux2es/the_talking_cube_4x3090_local_ai_server/)
  - Supermicro H12SSL-i AMD EPYC 7262 256GB RAM 4xEVGA RTX 3090 FTW3 ULTRA Completely DIY / custom mounting solution for the 3 gpus on top

- ## [Cooling a server motherboard in a desktop case. : r/homelab _202403](https://www.reddit.com/r/homelab/comments/1bgpzno/cooling_a_server_motherboard_in_a_desktop_case/)
  - I have a Supermicro H12SSL-i  with an Epyc 7762 that has 64 cores. It's installed in the Fractal Define XL 7 case and is an all purpose server.
  - Fractal Design Define 7 XL: 604 x 240 x 566 mm, 82L 📦
  - It runs well in a typical workload, but if I run the cpu full throttle, it will crash, likely due to the lack of ventilation blowing over the VRMs and such when there's such a huge spike in watts.
  - Anyway, do any of you DIYers know what could be done? The quieter, the better. It's full (19) of 3.5 inch drives so ventilation is a bit tricky.

- server boards need air flow, the more the better. I would make sure all of the fans are pushing/moving the air one way, i.e. in from the front and out the back, make sure that the cpu heatsink fans are not fighting this needed air flow, and I would max out on fans and sizes, like the Fractal will take the 140mm fans, I would go with the Noctua NF-A14 Industrial PPC-3000, yeah they will be louder than the slower 1500rpm fans but they move twice the air.

- I ended up downgrading the CPU to a lower tdp - AMD EPYC 7302P.

- ## [求推荐mATX非侧透散热好的机箱 - 小红书](https://www.xiaohongshu.com/explore/688e90bf00000000250132d4?xsec_token=ABB5_uSFZrF4Fb2p-cIYUQAnzEybe1BZQKTuCoX9z-RXw=&xsec_source=pc_search&source=unknown)
- 看标题第一反应就是追风者xtm3了，水冷可以选华硕的那个，风冷对风道要求高只有追风者合适了。
  - 如果你的配件都是无光的，也无所谓非侧透了

- 酷冷至尊 MASTERBOX NR200 📌
  - [机箱_产品_酷冷至尊 - NR200](https://www.coolermaster.com.cn/product_detail/335.html)
  - 185x292x376mm, 20.3L 
  - 支持显卡尺寸 330x156x60mm

- [ASUS Prime AP201 MicroATX Case｜機殼｜ASUS 香港](https://www.asus.com/hk/motherboards-components/cases/prime/asus-prime-ap201-microatx-case/)
  - 33 公升的時尚 MicroATX
  - 可容納 360 mm 水冷散熱器、長達 338 mm 顯示卡及標準 ATX 電源供應器

- ## [多么痛的领悟，上百台ITX电脑总结出的经验 - 小红书](https://www.xiaohongshu.com/explore/64d4825a000000000c034f36?xsec_token=ABRh3ACWg_DKSLuH2VaseP_A7Mn7MpO5RifkuaugGycJM=&xsec_source=pc_search&source=unknown)
- 第一种机箱类型：ITX主板+小1U电源（个人非常不推荐）
  - 优点：体积可以做到很小，很薄。
  - 坑点：小1U电源噪音大且是你受不了的那种、CPU散热器难以选择、需要显卡延长线、需要半高显卡。
  - 建议：非必要，直接不要选择

- 第二种机箱类型：ITX主板+SFX电源（比较推荐，但也不是没有问题。）
  - 优点：可选择的电源比较多、结构合理、很多品牌的电源也可以做到没什么噪音。
  - 坑点：假的SFX电源比较多且虚标、有些也需要显卡延长线
  - 建议：优先选择类似机械大师C24这种显卡直插形式的。SFX电源尽量选择长城、TT这些品牌。

- 第三种机箱类型：小尺寸MATX主板+SFX电源（比较推荐，主要这类机箱较少，好看的不多）
  - 优点：主板选择空间大，有很多便宜的主板，可扩展空间大，装了显卡还能装网卡，费用少。
  - 坑点：没啥坑点，就是可选择的机箱有点少。
  - 建议：就选艾罗拉SS31/30、笨牛U45等，如有其他建议评论区留言帮助大家。

- 第四种机箱类型：ITX主板+MATX电源（非常推荐，但这类机箱更少了）
  - 优点：电源可选择性很多，空间富裕，显卡可直插主板等。
  - 坑点：同样没啥坑点，也是可选择的机箱有点少。
  - 建议：目前我见过的机箱有闪鳞G200，同样建议有好心人评论区留言帮助一下大家。

- 装了好多种itx，小1u那种适合功耗比较低的，而且大多数小1u电源机箱都要买显卡延长线，而且好的静音电源很贵，建议还是装那种sfx电源的，省事，也比较便宜，后期扩展性也比较大，显卡选择也更多样一些，前面提到的那种一般都是短卡，价格又上去了

- ## [u7 265k用什么风冷能压住 pa140可以吗？还是p60t，或者fc140？  ](https://www.xiaohongshu.com/explore/68d1b0a30000000013007154?xsec_token=AB9X5HvN7d3sRdmBFeEqk4N5mZwaaHkl_t8SjBmCKQI7c=&xsec_source=pc_feed)
  - 开始看到有人说pa120就可以，然后140差不了多钱性能比较好，但是去问客服，客服说不行，说fc140可以。然后也看到推荐p60tv3的，但也有说阿萨辛都压不下265k的。
- 默频满载功耗也不低啊，官标250w，我的满载跑默频260w，最好的风冷也不建议去压240w以上的u。除非你买265k就为了刷刷视频，而且对游戏帧数没要求，没生产力需求。

- 正常用随便一个设计没硬伤的双塔都能压，甚至非生产场景单塔都行，因为ultra系列的优势就是超高能耗比，低功耗也能发挥绝大部分性能，
  - 但你要以长期满载和喜欢烤鸡看温度为要求，这u满载250w风冷干不动只能水，我会选择pa120这种中小尺寸双塔或者厚单塔，相对好装省事儿，fc140这种大驼子除了安装和更新硅脂时带来痛苦带不来什么
- 这位解释的很好了。满载风冷不够，但大多数情况下双塔风冷随便选
- 降个压吧，损失一点点换个好功耗用
- 不超频降压用风冷就没问题，如果要超频那功耗就冲着300w去了，必须水冷
- 你要是做视频解码啥的还是水冷吧，撑的时间长些，不然降频了
- 可以限制啊。你玩itx追求完美释放性能吗？

- 我这pa120换扇p12e对我这个用于编译的工况是够的，p60t没对比过

- 265跟147比就是，性能一样，不缩缸，功耗还低，6热管双塔风冷就行。147一般都是360水冷

- pa140，换俩12cm的风压扇，记得额外买个12cm风扇的扣具

- 如果你会设置cpu，265k，190瓦左右，就可以发挥出97%的性能，也就是说你用b60t也行，甚至大霜塔

- ## 🤔 [itx主机CPU选哪个（AMD还是intel）？ - 知乎](https://www.zhihu.com/question/444107051/answers/updated)
- 11代是牙膏倒吸，没必要。AMD带G的也在涨，轻度使用3400G完全足够，还可以兼顾点游戏，不过还是看预算吧，肯定是预算内堆核心。
  - itx主机麻烦在散热器和机箱的选择上，体积压缩到极致还要散热强，不然容易积热。当然如果不在乎体积的话另说

- 在ITX环境中，还是intel有点优势 
  - 因为ITX优点和缺点一样明显 所以选择intel的平台，办公尽量选择低功耗的, 桌面atx/matx的diy平台，选择amd ryzen

- [10l以下ITX可以支持最高什么cpu？ - 知乎](https://www.zhihu.com/question/7439796831)

- 10L刚好能装双塔，双塔风冷散热器所能支持最高CPU是 EPYC 9004系列和R9 9950X系列。

- 现在有的10L的机箱可以装135mm的散热器。135mm双塔的解热能力在200W出头。
  - 如果以生产力需求为主，那么可以上新的ultra7 265k，新的ultra系列虽然游戏性能开倒车，但是能耗比比上一代有大幅度的提升，比较符合你的情况，但是性价比不高，按需选择。
  - 如果以打游戏为主，那么amd X3D系列的CPU可以随便用。因为工艺问题，除了最新出的9000系列x3d其他的都是限制功率的。功率比非x3d型号的CPU要低。
  - 其他的amd系列的处理器。基本可以随便上，即使是解锁了功耗的9950x也只有230W。

- 10L以下的机箱上不了三槽的标准显卡。只能核显或者有些可以用专门的itx短卡。如果是用风冷，基本就不要考虑intel带k的型号和amd的高端型号了。可能有用120水冷的，上个i5带k的就最多了。
  - 10L左右能上240水冷的机箱我以前还真研究过，这种的基本最高能跑两百瓦出头，上i7带k的型号稍微降一点电压基本能发挥出来，顶级的i9带k跑不满，但也不是彻底不能用。

- 默认用的话其实目前 [Ultra200S系列] 或者 AMD 9000系列 都对散热要求较低了，考虑10升以内的旗舰处理器也都问题不大，基本不会有i9性能损失后只有i7甚至i5性能的问题。
  - 所以不论针对游戏或者生产力主机，配置上处理器都可以放心的选择9950X或者9800X3D或者是U9 285K都是OK的。

- [U7 265K和9700X到底么选 - 小红书](https://www.xiaohongshu.com/explore/68a883b8000000001c03c2ab?xsec_token=AB2GCeMJb66g6AJnAmLcHLOqUT9Bzg3qO1V9MsHhNoFL4=&xsec_source=pc_search&source=web_search_result_notes)
  - 首先9700x有积热问题又或者说这个U太挑散热器也很难压温度 我风冷双塔散热器九州风神AK620默认频率待机温度57度 随便开个软件60来度 打3A游戏甚至70多度 散热器和机箱风扇忽吵忽静 严重影响我正常体验
  - 其次我的机箱是Z20 显卡5070Adoc 这么小的机箱 我稍微玩一下3A游戏这俩货给我机箱搞的跟个炉子似的 
  - 原先14600KF江西夏天不开空调游戏温度58度不到、显卡最高65度、换了9700X游戏温度极度不稳定平均73度 偶尔抽搐一下温度能干到80度 显卡也更热了
- 烤鸡40分钟都没你打游戏热
  - 我各种试过了 问了商家今年批次的9700X电压默认给的高 但是我不开PBO然后负压30温度还是很高 我见过最低温度53度差不多
- 你这温度应该开pbo而且还没降压吧，9700x默认88w温度不高啊，9700x不开pbo，用个百元的风冷随便压啊，打游戏噪音更多来自显卡吧

- 主要265k没法升级了 am5起码能用到2027年 但是Intel明天又要换接口 太逆天了

- 俩都不是一个等级的，97x能配几百块入门的b650，265k搭配的z板最差的也接近1k，稍微好点的b板也这个价，总拿货价比97x高一个数量级了，本来就不该拿来比，265真正的强势来源于能跟更贵的79x99x掰手腕

- 生产力265 游戏97x，还有70度对于cpu来说还太低了，85度都很正常，你这实属温度瞎焦虑

- ## [ITX | 塞个RTX5080？没问题！ - 小红书](https://www.xiaohongshu.com/explore/67bc32a90000000009039a96?xsec_token=ABBUmmsfcqVOegTyFI0DTJ4zLCSJXlG34hPsmQuX6DX3M=&xsec_source=pc_search&source=web_search_result_notes)
  - 背靠背结构的ITX机箱刚好塞入了一张三风扇的RTX5080，海韵SPX750作为扎实耐用的经典sfx电源轻松带动了i5+RTX5080的组合，顶部两个安静优雅的海韵Magflow风扇为机箱带来了更优化的风道散热
  - 机箱：FORMD T1
  - 显卡：影驰RTX5080-16G魔刃
  - 主板：微星B760i D4 Wi-Fi
  - 内存：皇家戟ddr4-4000-16g*2
  - CPU：i5-14600K
  - 散热器：超频三RC600黑色电源：海韵SPX750W
  - 风扇：海韵MagFlow RGB 120*2
  - 电源：海韵SPX750W

- [高颜值、能装三扇长显卡的13升itx主机 - 小红书](https://www.xiaohongshu.com/explore/676e9a4f0000000014026954?xsec_token=AB_LcGHuSS1a9ZxmBLSWAdGMd-OlAMXO2f9f82oya7dHg=&xsec_source=pc_search&source=web_search_result_notes)

- ## [小机箱 5090d+9950x3d 拿下！ - 小红书](https://www.xiaohongshu.com/explore/67f779020000000007036603?xsec_token=ABegebsB80NsOXLuiVvWiW-lQszDh0QuWayKWLU0ABe5c=&xsec_source=pc_search&source=web_search_result_notes)
  - 【CPU】AMD RyzenTm 9 9950X3D
  - 【显卡】微星 5090d超龙
  - 【机箱】方糖机械大师C+MAX银色
  - 【主板】微星 MAG B850M MORTAR WIFI
  - 【散热】TRYX PANORAMA展域240水冷ARGB 黑色
  - 【内存】佰维 128G（32Gx4）DDR5 6400 C34
  - 【固态】三星 9100PRO 4TB PCIe5.0*4 M.2接口
  - 【电源】 洛基1200w
  - 【风扇】 联立积木三代

- 我和你一样的卡和U，这样装冷排吸显卡尾气再加上9953这个火炉得多热啊我用的还是大机箱和展域360性能版水冷，待机就要40多度了，稍微打开几个网页登一下steam就50+了
  - 我感觉还能接受哎，待机五十多，打开 C4d 轻量干个活 70 多度，CPU 反正也烧不坏
- 我是14900k换过来的之前没用过x3d的CPU。149k虽然耐电但是待机温度不高的，浏览网页不会超过35度。还是心理上没适应高温的CPU
  - 那我老适应了之前用的 i9+3080ti 笔记本

- 如果是 LOL 这种游戏的话显卡三十多度，cpu 六十多，3a 游戏大概都在七八十度左右

- 换个联力a3就可以了，侧面还可以加三把风扇，5面打孔散热板

- 机械大师c系列侧边都是玻璃，要是换成网散热能更好点

- [C+MAX金属大师 GT银灵感 - 小红书](https://www.xiaohongshu.com/explore/65f446c20000000014005ff3?xsec_token=ABxIEa1q74egE8STTJo9DqtGHzgiBycDD0OoPvjAjGLJA=&xsec_source=pc_search&source=web_search_result_notes)
  - CPU：12600KF
  - GPU：影驰 金属大师 4080super
  - 机箱：方糖机械大师 C+max 月光银Air版
  - 主板：技嘉 B760M A ELITE AX D5
  - 散热：奥斯艾i240-B 一体式水冷
  - 硬盘：光威 弈系列 旗舰版 2T
  - 电源：海盗船SF850L

- [机械大师 CMax 老铁抄作业了 9700X搭 5070T - 小红书](https://www.xiaohongshu.com/explore/67caf20b0000000029029b83?xsec_token=ABqsyDIYHWnZyXfQUxpaLc8dJaKdhuBLrkKua73Sg89IQ=&xsec_source=pc_search&source=web_search_result_notes)
  - CPU：AMD 9700X 中文盒（全程烤机不超 70 度）
  - 显卡：技嘉 RTX5070TI 雪鹰 16G
  - 主板：技嘉 B850M 冰雕 WiFi6E
  - 散热器：酷里奥 p60t Pro 白色性能版
  - 机箱：机械大师 Cmax
  - 阿斯加特女武神二代 32G 套 6000 c28 
  - 硬盘：三星 990 Pro 4TB 固态
  - 电源：航嘉 sfx 额定 850w 白金全模 atx3.1

- ## [itx机箱有啥很难受的缺点吗，散热到底能有多差？ - 知乎](https://www.zhihu.com/question/337421059)
- 缺点是空间太小，走线麻烦，换零件麻烦(换的频率不高就不算是缺点了
  - 散热也是看机箱而定的
- 散热也是看机箱而定的, 目前装过三台c24 qbx geeek a4的温度都没啥问题
  - 现在很多a4 机箱的风道都是从下到上，肯花钱买风扇的话，散热效果还是可以的
  - 实在不行就把侧透换成防尘网呗，又能低五度了

- 风道设计在 ITX 里虽然重要，但是实际上最影响散热的是硬件选择，比如你非要在 ITX 里放 i9 + 旗舰或次旗舰的显卡注定好不了。
  - 几年前为了装个 Ubuntu 小主机，搞了一套 11900K + 6600XT 的 ITX 主机，开机就60度以上，后来给 CPU 降压降频，每个核心都降了 0.2GHz，电压 1.1v 才勉强压下来
  - 另外一点就是 ITX 对 SSD 不友好，常见 ITX 主板的 M.2 位少，且散热差，刚才提到的那机器，玩游戏的场景下不一会 SSD 就能上 70 度。背面的 SSD 就好很多，只有 50 度左右
  - 如果想要 ITX 的“小”，那么推荐全部用中端的硬件，i5 级别左右 + 中端显卡，不常移动且能接受水冷的话可以上 240 尺寸的水冷，显卡可以看看品牌拆机的涡轮卡，能够有效的降低箱内温度。

- 我之前搞了个12500H+P4的itx，热的根本没法用，CPU和显卡一直100度，最后无奈换了个ATX机箱，解决，温度没高于60度过

- 当温度上去后，带来的最直观后果就是风扇转速过高引起的噪音很大。
  - 另外itx机箱和主板对于硬盘控非常不友好。M.2一般不超过两个且温度较高，3.5机械硬盘安装困难即使装上去也一般会占用一个风扇位间接影响散热。
- 确实, 我光看小巧便携去了, 几年也搬不了一次, itx换下来比常规贵两千, 而且性能还差

- [【8.1L】 便携科研ITX本地小主机推荐1️⃣ - 小红书](https://www.xiaohongshu.com/explore/67adb5420000000029034581?xsec_token=ABakFdkTIJ1ZcM6p0CG5TD5J9V9fUMmia67ixkR6mRgtE=&xsec_source=pc_search&source=unknown)
  - 机箱：闪鳞s300 tc+usb PCIE4.0延长线（444）
  - CPU：12600kf｛也可14600kf（板u：1889）｝
  - 主板：铭瑄b760i WIFI D4（1669）
  - 散热：利民AXP90-x53 4热管（164）
  - 内存：金百达银爵3600 D4 32G*2 （741）
  - 硬盘：金士顿kc3000 1T PCIE4.0 1G独缓（473）
  - 显卡：技嘉风魔RTX4060ti-16G（3689）毫无性价比，可以考虑二手大显存的卡。
  - 电源：玄武650sfx 金牌全模组（359）
- 12600kf已经可以满足很多日常的生产力任务同时不用担心缩肛，但是和14600kf仅有200元差距，说实话我更推荐146kf，但是无奈缩肛…有动手能力的小伙伴可以上146kf
- 铭瑄b760主板性价比首选。给到9个USB接口其中有2个20Gbps的c口，带WIFI6E网卡，同时给到2个m2 2280的插槽，支持PCIE4.0的速率。再搭配4个SATA接口给硬盘扩容，满足高存储的需求。同时对显卡是PCIE5.0x16插槽。

- ## 🧩💡 [ITX机箱推荐 2025年版 80起步 ［支持MATX主板、ITX主板、常规ATX电源、SFX电源 15L 20L体积］300以内 高性价比 台式电脑机箱 K88 i8 P90 趣造等 - 知乎](https://zhuanlan.zhihu.com/p/677817218)

- resources
  - [CaseEnd filters](https://caseend.com/)

- 15升、20升机箱的结构类型：常见结构，基本是前置电源，横放显卡
  - 有一些特殊的机箱，结构：下置电源、需要显卡延长线、下压式风冷。类似酷鱼T40，但本文不做推荐（太少了，花费也可能比较高）

- 玻璃侧板：常见的侧板材质，安装时，需要注意边角不能被磕到，否则它会碎掉。
- 亚克力侧板：透明塑料侧板，如果温度较高，可能会有塑料味，时间长了，也会发黄。
- 铁侧板：相对来说，比较其他类型的侧板，这款是最好的，碎不了，也不会有塑料味。但有些厂家，铁侧板甚至不开孔，这就会让散热效果差。
- 防尘网侧板：这种侧板，一般自己DIY的比较多，多为塑料材质。部分机箱，是金属侧板+防尘网的组合。
  - 所有机箱，都可以自制防尘网侧板，成本不到10块：

- 本文推荐的所有机箱，个人都只推荐装双风扇显卡。 双风扇显卡，长度一般不会超过300毫米，多数机箱，都可以放下。

- 机械大师 cmax ◇99
  - 尺寸：392*185*284mm, 20.5L
  - 显卡：385*160mm以内
  - 散热：162毫米风冷 或 240水冷
  - 材质：内框：1mmSPCC钢材 ；外框：2mm铝合金
  - 主板支持 MATX/ITX
  - 电源支持 SFX/SFX-L/（140mm以内）ATX
  - 风扇支持 顶部：12cm*2；尾部：12cm*1；前面板：8/9cm*1
  - 2.5寸硬盘位 至多3个
  - 3.5寸硬盘位 至多1个

- 鱼巢 S9 ◇99
  - 尺寸：375×188×300, 21.15L
  - 显卡：360x150限长
  - 散热：160毫米风冷 或 240水冷
  - 材质：1.2毫米 镀锌钢板
  - 侧板：~~玻璃~~
  - 电源：ATX电源，170mm以内
  - 主打的就是便宜，99，还能走背线，让机箱内更美观一些，虽然能走的不多

- 铝小宝 E90 PRO
  - 尺寸：377×187×298, 21L
  - 显卡：355x150x80mm限长
  - 散热：160毫米风冷 或 240水冷
  - 电源：ATX电源，160mm以内, sfx/fiex电源需自备转接板
  - 铝小宝ALBOX P90 ◇158, 被E90Pro取代
    - 尺寸：375×188×300, 21L
    - 显卡：360x150x80mm限长
    - 散热：160毫米风冷 或 240水冷
    - 材质：1.5毫米+1.0毫米 冷轧钢板
    - 侧板：铝 或 亚克力
    - Motherboard(MM): 245 x 245
    - Power Supply(MM): 150 x 160 x 86
    - 木质提手，算是这个机箱的特色了。
    - 电源延长线位置，在机箱顶部，装出来的效果，就参考官方这个图吧。

- 笨牛 N20 ◇199
  - 尺寸：381×199×300mm, 22L
  - 显卡：限长364x160x85mm, 16cm的电源长度支持315mm显卡长度, 16cm以上电源仅支持290mm显卡
  - 材质：1.5毫米+0.8毫米 冷轧钢板
  - 侧板：3毫米 玻璃侧板
  - 散热：164毫米风冷 或 240水冷
  - 能走背线的小机箱，不多，也不少。不过都只能走一点点。前面板有大面积开孔，散热通风好，电源位置有一个挡板，装出来，那堆线就看不到了

- 包子星人 A88Pro ◇183
  - 尺寸：380×195×305, 22.6L
  - 显卡：360毫米限长
  - 材质：1.2毫米 镀锌钢板
  - 侧板：铁 或 玻璃

- 先马趣造 ◇139
  - 尺寸：391×185×303
  - 显卡：335毫米限长
  - 散热：155毫米风冷
  - 材质：1.5毫米+1.0毫米 冷轧钢板
  - 侧板：铝 或 亚克力
  - 趣造还有个兄弟，叫做蓝宝石银角大王，但目前只有库存货了，而且卖的比趣造贵……

- 文中提到的这些品牌，多数都是有10升的机箱，可以去搜搜看。

- 有没有多盘位（3-5个3.5HDD）小机箱推荐
  - 无

- 如果拒绝光污染，非透明侧板的15升，有推荐吗？
  - A88

- ## [有哪些可容纳 4090 显卡的 ITX 机箱？ - 知乎](https://www.zhihu.com/question/559771286/answers/updated)
- 极限尺寸itx不是不能搞，问题是溢价太高，定制的机箱就要1k-2k左右，主板（itx板型），电源（），显卡（最完美的是，三风扇的不用想了）小尺寸的全都有溢价。总体比正常配要贵30%-40%左右。
  - 4090还算好，你降频到3090这个水平玩没有散热问题，但是itx正常用散热问题很大，建议开盖，不然CPU得上水，显卡4090降频用问题不大，还有背部m2的散热，风切声音问题等等。

- 公版4090和3090一个大小，买公版然后基本上原本能装3090的都能装

- 在reddit上看到了几个案例，不提Nr200、Meshlicious那些大号的itx机箱，就看10L左右的：
  - Formd T1，这是个10L的机箱，这个机箱我也在用，外形我非常喜欢。我自己的T1里面塞了个公版3090。
  - 联力A4-H2O，这是个11L的机箱，继承了Dan A4的好传统，增加了兼容性，成本也降下来了
  - Jimu D+ V2.0，10.5L的机箱，同样塞进去了一个4090FE+AIO，这个机箱外观和内部规划跟Formd T1几乎如出一辙，但价格要便宜些
  - Ncase M1，不到13L，因为不是三明治格局，这货为了不憋死4090把机箱垫起来了，而且如果不用个90度转接头的话4090的电源线没法插。
- 基本上看到的小于14L的4090案例就这些了，如果放宽要求，reddit上有大量的ssupd meshlicious的案例，虽然体积要大不少，但因为是竖直放置的，占地空间非常小
  - 除了公版卡之外第三方的卡基本都塞不进去

- ## [各位心目中最好的ITX机箱是什么？ - 知乎](https://www.zhihu.com/question/55014071/answers/updated)
- 我自己DIY主机，喜欢在有限的空间里，充分发挥各部件的性能
  - PS：我从不考虑水冷，因此不做水冷推荐。

- 高性能兼顾小体积的选择：乔斯伯的Z20机箱（20L）
  - 高性能主机的显卡是一定要上三风扇的，基本上是4080以上级别，CPU也是13600以上的规格，这对机箱的散热有不小的要求。
  - 乔斯伯Z20机箱顶部和底部可以支持4个14cm风扇，尾部还可以装一个12cm风扇，合理规划下进上出的风道，足够压得住4080和13700的组合。
- 最佳性价比小机箱的选择：机械大师C26（12.9L）和笨牛U45（11L）
  - 2024年这个时候，三大厂的ITX主板比MATX主板贵了将近一倍，同样的配置把MATX主板换成ITX主板至少贵600块，实在没什么性价比。因此选择MAXT主板+SFX电源的组合，便成了兼顾性价比的最小机箱搭配
  - 2.1更强散热，推荐机械大师C26。对于AMD显卡+CPU组合或者13700+4070ti高性能组合的，更推荐带前面板风扇位的机械大师C26。这个规格的机箱，顶部和底部只支持9cm风扇了，这个大小的风扇还带侧边RGB样式的，我只找到鱼巢的9cm风扇。
  - 为了压13700或5800X这样的CPU，135mm高度散热器只能选利民的SS135了，但这款不带RGB风扇，为了和9cm鱼巢的风扇rgb风格统一，建议自行更换成鱼巢的12cm风扇。如果是13400规格的CPU，那么利民的AK120mini就能压得住，RGB风扇的风格就自行发挥了
  - 2.2更具性价比且更紧凑，推荐U45。U45有个缺点就是前面板没有风扇位，所以建议CPU和显卡的规格要下降一些，以防机箱闷罐。此外，U45右边那个挡板设计，虽然方便了理线和藏线，但我是真的欣赏不来这设计。

- ## [Quad 4090 48GB + 768GB DDR5 in Jonsbo N5 case : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m9uwxg/quad_4090_48gb_768gb_ddr5_in_jonsbo_n5_case/)
  - JONSBO N5 NAS Pc Case: W355*D403*H350mm
  - GPUs -- Quad 4090 48GB (Roughly 3200 USD each, 450 watts max energy use)
  - CPUs -- Intel 6530 32 Cores Emerald Rapids (1350 USD)
  - So some additional information. I'm located in China, where "top end" PC hardware can be purchased quite easily.

- Do they "just work" or do you need sketchy drivers?
  - On Ubuntu they just work with official drivers (either Ubuntu PPA or Nvidia). 
  - On Windows I've seen reports that they do not work with official drivers, but I have not tried (nor do I plan to run windows on this machine)

- ## [乔思伯Z20机箱小白首次装机分享 - 小红书](https://www.xiaohongshu.com/explore/67eadb49000000001c00c0db?xsec_token=ABhwvh4o79bh1iZJod5ETLKzRMlnZYs2oM-5p3wHmKM24=&xsec_source=pc_search&source=unknown)

- [乔思伯Z20装机分享 - 小红书](https://www.xiaohongshu.com/explore/67e7b093000000001201ed15?xsec_token=ABhmT245aHYddZ3_znj1lt9rAgzysn8wPmPsb_KU5jWH0=&xsec_source=pc_search&source=unknown)

- ## [DIY装机乔思伯z20 9600x + 5060建议帖 - 小红书](https://www.xiaohongshu.com/explore/688c38a60000000025022daa?xsec_token=ABH_IcKm-CurbXXiUGZUe0iNzqulTk75YHR2Lmgz9lyY4=&xsec_source=pc_search&source=unknown)
  - 【散热】 利民PA120 MINI BLACK双塔6热管黑色
  - 【CPU】 AMD 锐龙 5 9600X
  - 【主板】 微星 B650M GAMING PLUS WIFI
  - 【显卡】 七彩虹 战斧 RTX 5060 豪华版 8GB
  - 【内存】 金百达 32GB(16GBX2) DDR5 6000 海力士A-die颗粒 星刃
  - 【电源】 安耐美 金竞蝠GM650 黑色  ¥329 @京东

- 内存买了国产的 其他的太贵了
  - 确实是这样！我内存也准备换c30了
- 我是c36 拼多多买的

- 高u低卡了，换7500f，电源选个大厂的

- 9600x加5060高u低卡了？5060配7500f？
  - 7500f感觉都高了，但考虑到网友玩家那差不多了。
- 除非你只玩1080p的网游。但现在主流都是2k显示器或者是4k双模了。而且u还可以小超一下，显卡老黄不给你超的。

- [年轻人的第一台生产力主机乔思伯Z20 - 小红书](https://www.xiaohongshu.com/explore/6777b7c8000000000900d498?xsec_token=ABnLOUzIXMWLH-jTphfigaEnUEg3qXD4FdObm05VCiLdg=&xsec_source=pc_search&source=unknown)
  - 散热：超频三 RZ620臻+追风者M25无光

- [Jonsbo Z20 build : r/mffpc _202506](https://www.reddit.com/r/mffpc/comments/1lo5xwl/jonsbo_z20_build/)
  - CPU: AMD 9600x; 
  - GPU: Powercolor 9070xt reaper 
  - PSU: seasonic focus gx850 
  - Motherboard: Asus B850M plus wifi 
  - Memory: gskill trident 32GBx2 6000MHz CPU 
  - cooler: thermalright frozen notte 240

- [Jonsbo Z20 Build. Intel Core Ultra 7 265K + RTX 5070 : r/mffpc _202506](https://www.reddit.com/r/mffpc/comments/1lfgii7/jonsbo_z20_build_intel_core_ultra_7_265k_rtx_5070/)
  - CPU: Intel Core Ultra 7 265K
  - GPU: ASUS GeForce RTX 5070 TUF GAMING OC 12GB
  - Motherboard: MSI B860M GAMING PLUS WIFI
  - PSU: Corsair SF 850W 80 PLUS Platinum
  - RAM: 64GB Kingston Fury Beast Black RGB EXPO [2x32GB 6000MHz DDR5 CL30 DIMM]
  - SSD: Kingston FURY Renegade SSD 2TB M.2 2280
  - CPU Cooler: THERMALRIGHT Peerless Assassin 120 Digital ARGB
  - Case Fan: DEEPCOOL FC120 x3 Set

- [Jonsbo Z20 Build - RTX 5090 FE, 9800X3D : r/mffpc _202510](https://www.reddit.com/r/mffpc/comments/1nur3dl/jonsbo_z20_build_rtx_5090_fe_9800x3d/)
  - CPU - AMD Ryzen 7 9800X3D
  - GPU - RTX 5090 Founder's Edition
  - RAM - 32GB x2 Corsair Vengeance CL32 6400Mhz DDR5 RGB RAM
  - Cooler - NZXT Kraken Elite 240 RGB AIO (2024)
  - Motherboard - Asrock B650M Pro RS WiFi
  - PSU - Corsair SF1000
  - Storage - Samsung 980 Pro Gen 4 2TB, Lexar NM790 Gen 4 1TB

- [Jonsbo Z20 All white build with Gigabyte Aorus Master ICE 5090 : r/sffpc _202509](https://www.reddit.com/r/sffpc/comments/1nhzeu0/jonsbo_z20_all_white_build_with_gigabyte_aorus/)
  - Build: Mobo: Asus rog strix B850G 
  - Processor: 9950x3d 
  - GPU: Gigabyte Aorus Master ICE 5090 
  - Ram: CL28 96gb kit (2x48gb) 
  - AIO: ROG Ryujin 240mm 
  - PSU: rog loki sfx-L M.2 - 2 wd black one is 2tb gen 5 and the other is 8tb Fans: right now a mix of lian li and rog and thermaltake.

- ## [用乔思伯Z20装一台5090“手提电脑” - 小红书](https://www.xiaohongshu.com/explore/6831b59b000000002202a719?xsec_token=AB8c-JeBH72uEhbyvwZNwZ7CJy32kV-b7wXvQrGV6x6G4=&xsec_source=pc_search&source=web_search_result_notes)
  - 机箱：乔思伯 Z20
  - 显卡：华硕 TUF 5090D
  - CPU：AMD 9700X
  - 主板：微星 B850M 迫击炮
  - 内存：威刚 D300 6400 32G x2
  - 显卡：华硕 TUF 5090D
  - 固态硬盘1：三星 990 Pro 2T
  - 固态硬盘2：致态 7100 2T
  - 固态硬盘3：海力士 U.2 7.68T
  - 电源：华硕 洛基 SFX-L 1200W
  - CPU散热：酷冷至尊 Hyper 612
  - 风扇：追风者 T30 x3

- 3.5寸机械盘就不适合这种机箱。既要保证封道畅通，CPU和显卡好散热；又要保证机械盘温度不超标；还要确保机械盘防震，难以兼得。

- 显卡插几槽啊，5070ti还有机会装底部进风吗
  - 一槽。用5070ti可以装风扇，起码薄扇肯定没问题。

- [风冷极限稳压14600kf！ - 小红书](https://www.xiaohongshu.com/explore/682c48f5000000000f038872?xsec_token=ABkkbE8DDCL643O12-dpNtOGU7Vi3PMVqtoIMW9TX50Xg=&xsec_source=pc_search&source=web_search_result_notes)
  - 散热：利民 pa120
  - 显卡：讯景 rx 9070xt 16g 海外版
  - 最近14600kf价格很香 所以替换掉12600kf 经过两天的调试 双塔6铜管风冷也能极限压住这颗cpu啦
  - 2k分辨率下 这套配置打怪物猎人荒野最高画质平均帧200出头 也算比较舒服了 本来都打算放弃治疗上240水冷了 最后挣扎一下抢救回来了 风冷万岁！机箱风噪是真的大
- 14600kf 还是要降压的 负载要控制1.2v以下，高温度就控制住了
- 单塔风冷随便压，平时都不带转的

- 你加了几个风扇压住的
  - 我itx机箱没啥空间 就顶部两个 左侧一个 我显卡太厚 底部两个风扇都装不上

- 这u降压单塔也能压，一般双塔都是够的，只要不降频没啥好焦虑 你这个温度高主要是机箱差+乱装风扇，前置电源小箱本身进风受阻风道难构，底下也没有风扇进风纯靠显卡抽风(显卡下超过3cm，完全可以尝试上15mm薄扇进风)，上部的风扇尤其是前部的更是把cpu所剩不多的冷气抽走，cpu直接无气可用巧妇难为无米之炊，pa120的塔体是很优秀的

- [2024 伦敦自用手提4090 小主机 - 小红书](https://www.xiaohongshu.com/explore/6766dd2400000000130083af?xsec_token=ABboPWE_YbGyIsohkIYlHUozqKDRjLeUQCouU2QZY1chQ=&xsec_source=pc_search&source=web_search_result_notes)
  - 机箱：乔思伯 Z20, 180mm*298mm*370mm, 20L 📌
  - 风扇：乔思伯 ZK120W x3 + ZK120WR x3
  - 厂家应该出个带屏幕的风冷，把这个显示温度的换掉

- [Can the jonsbo Z20 support a quad-slot GPU? What is the GPU height clearance of the case? : r/mffpc _202501](https://www.reddit.com/r/mffpc/comments/1i8o5rp/can_the_jonsbo_z20_support_a_quadslot_gpu_what_is/)
  - Idk if this is considered 3 or 4 slots 4090? 360 mm length and 70mm height. I added 15mm fans on the bottom but honestly they are unnecessary as the temps were virtually the same before with less noise/interference.
  - Asus b850 strix I think it’s called. Itx. If I could do it again with this case I’d get a m atx board. Only thing you gotta watch out for is the pcie placement needs to be above any m.2 slots. So most of the msi boards are not an option.

- [黑橙风冷手提式小电脑 - 小红书](https://www.xiaohongshu.com/explore/66d19e28000000001d01b98b?xsec_token=AB38kMIt8DJB5wbhI53QOtqJMabGeUPzQy1DfS21GmOko=&xsec_source=pc_search&source=web_search_result_notes)
- 底部可以同时装两个风扇和一个3.5寸硬盘
- 我装了这个机箱，提醒一下，买主板看一下 pcie 槽的位置，微星迫击炮有点偏下，显卡厚了就贴底了，我看别人华硕 tuf 都挺好

- 🤔 [小闷罐乔思伯Z20的散热方案及双烤测试 - 小红书](https://www.xiaohongshu.com/explore/67b067bf0000000028028ee2?xsec_token=AB37FEjnwyYBwILr2RQtHgse2ohed1b-PXLNaQdYNbzj4=&xsec_source=pc_search&source=web_search_result_notes)
  - 散热器：利民pa120se

- 冷空气在底部，热空气在上部，还是更加科学一点

- 感觉可以尾部扇改进风，CPU散热方向改成左到右，正好可以让显卡和CPU都吸到一手冷空气然后统一在右上排出
  - 我记得有up主做过测试，这种类型的机箱这样装温度表现比传统的安装方式更好。主要还是这类机箱没有前面板进风，CPU散热吸的都是显卡尾气。其实改完之后还是下进上出，只是水平方向反一下。
- 这个一个问题就是进风量＞出风量，热量会堆积

- 其实底部进风用处不算大，倒是对pcie槽和IO槽的积灰有帮助，原因是底部有风送进来就不需要四处借风了
  - 非常有帮助，底部加了两个3000转的P12 max暴力进风扇，烤鸡显卡温度直接从76℃降到70℃以下了，最高不超过70。
- 亲测无用，我还是买的4900转工业风扇，两个加到底部发现没任何卵用，然后又费劲力气换回普通rhb

- pa120se 会跟内存条冲突嘛
  - 有一点点，装散热器内存条的风扇会略高1cm

- 普通内存应该没什么问题？多高比较好？
  - 40mm

- 天选主板三个机箱风扇接口都用上了，这样能单独控制上面，底部和后面的转速
  - 明白了，主要是同时考虑藏线，技嘉小雕主板有一个风扇接线槽太明显了，不好接线

- 没有用集线器啊 主板上的风扇位足够了

- [乔思伯Z20装机分享 - 小红书](https://www.xiaohongshu.com/explore/67e7b093000000001201ed15?xsec_token=ABhmT245aHYddZ3_znj1lt9rAgzysn8wPmPsb_KU5jWH0=&xsec_source=pc_search&source=web_search_result_notes)
  - 散热不用担心，我只装了一个单塔双风扇，室温15度玩游戏大概60度。夏天可以把玻璃面板换成散热孔的。

- [关于matx机箱乔斯伯z20的一些疑问 - 小红书](https://www.xiaohongshu.com/explore/67c32e800000000007036281?xsec_token=ABhMyCZP5HBuwkcA-x3g3Zb7JVfz1CaYgxzSIyUO-3Mgs=&xsec_source=pc_search&source=unknown)

- ## [乔思伯z20风道 - 小红书](https://www.xiaohongshu.com/explore/67a8bfb8000000002803576a?xsec_token=ABg64t-BlcmW2roSur4qqjBKnd-Tlemzg7qdIBUy2o41w=&xsec_source=pc_search&source=web_search_result_notes)
- 实际上都差不多，这机箱就是个大闷罐，侧板建议去搞块开孔的亚克力
  - 我的c26 夏天直接开侧板
- 最好的风道就是去掉侧板

- 之前 B 站看过每个位置的风扇散热效果，后出那个位置是散热效果最好的，其他的偏向是辅助而已，所以后面一定要出风效果会好点
- 其实不用想太多，我水冷大显卡，底下装不了风扇，就靠后面出风和水冷两个风扇，吹出来的风很热，顶部提手都有些烫手，但是开机玩一天也没事，这东西80来度不是正常吗
- 上出，热气默认是往上飘的，你这么会扰乱热流，除非你背面是超大工业扇
- 热气上升冷气下沉，遵循
- 上面全出风，进风从下面
- 后出上出，可以不用进风，负压下散热最好。
- 下进上出 前进后出

- 这种机箱下进风，背后排风最好，显卡温度低。上面不建议装，或者只装水冷。

- [风道求助 - 小红书](https://www.xiaohongshu.com/explore/662673150000000004018542?xsec_token=ABw3jEHfBhULZbVbZwZh-SoQYwidgEI4Cvil6t9yvhd28=&xsec_source=pc_search&source=web_search_result_notes)
- 这个机箱用单塔还是双塔散热合适啊
  - Cpu发热量高一些的话就要上双塔了。限高是指塔的高度，160能塞的应该。
- 顶部靠电源的风扇建议换个方向，对cpu散热很有好处，亲测

- [乔思伯 Z20 风冷，以上两种风道那种更合理，实际效果更好呢？ - 小红书](https://www.xiaohongshu.com/explore/673ef0a000000000060178a9?xsec_token=ABXPeGOfIrwFw2csvcwJomQbdXOQnxRyaYf8eRgRHxm0A=&xsec_source=pc_search&source=web_search_result_notes)

- ## [关于方糖机械大师c28装机时踩的一些坑 - 小红书](https://www.xiaohongshu.com/explore/686dd55d0000000017034ee3?xsec_token=ABosdtjmZ4IdMHAXii79bUC4njWXjrUmL9ULRNaDHexTw=&xsec_source=pc_search&source=web_search_result_notes)
  - 一开始买错电源，上240水冷的话只能搭配SFX小电源，普通ATX会卡水冷风扇
  - 好再发现及时，退了ATX，但是买的时候SFX电源也有个坑，因为我的显卡需要16pin接口，要求电源也必须要有16pin，于是又退了买错的SFX，重新购入鑫谷KL-M750G冰山版
  - 但是这个电源也有一个问题，跟机箱的电源支架有点不适配，电源开关的边缘会卡到支架导致无法放正（图5），最后支架是强行压着电源开关边缘装下去的。
  - 内存限高44mm，常规带灯条的基本都被限高了，只有少数符合要求，一开始也没注意看，后面及时重买了。买的没有灯带的宏基掠夺者银翼凌霜48g 6000 c28, 44mm以上的会把240水冷的两个散热风扇卡住
  - 然后就是水冷，买的是九州风神冰域240，但是这货的两个风扇接口上还有额外的接线

- 一定要注意主板显卡是一槽还是二槽 二槽底部完全不能装风扇 其次显卡长度太极限的话 9cm的风扇是装不了的
  - 这种小机箱 主板建议选技嘉b650m小雕 显卡位是一槽 下面有有空可以放风扇
- 我选的是电竞雕850，和650小雕布局好像一样的吧。包括大小
  - 对 850就是比650的槽位多一点 正常650就ok 850的贵个一两百

- 散热怎么样啊
  - 没啥大问题，待机60内，游戏90度内都没问题

- 能装双塔风冷吗
  - 要看下尺寸，说明书里是要求162mm以内，双塔风冷应该大部分都能满足

- 我那个利民电源也这样
  - 那看来机箱的电源支架设计也有问题。不过螺丝拧松一点盖上去也能固定好
- 电源支架有2款，用另一款的电源支架

- 装c26的坑： 1买风冷没注意大小，放不进去 2对风扇太过自信，买多了，上面的风扇位和风冷打架 3机箱内电源线很怪只能往内排风，因为不敢随便弯折线 4买了个显卡支架，位置不够装

- ## [纯白色美学装机小巅峰，机械大师C28 AI“学习机”配置分享](https://www.zhihu.com/tardis/zm/art/691493855?source_id=1003)
- 彩虹的主板绝对是最高性价比白色主题装机的选择。
- 内存是来自宏碁掠夺者的冰刃系列，内存顶部是哑光半透导光条，相当漂亮。
  - 冰刃的灯光很柔美，能够被七彩虹的iGame Center统一控制
- 显卡是索泰的RTX 4070 Ti Super月白
- 水冷是利民冰封视界240水冷，一块LCD屏幕给机箱增加了几分灵动。
- 由于机械大师C28机箱内存限高最多44mm，这里不得不将利民冰封视界240水冷当作120水冷来用
- 电源规格上支持140mm的ATX电源搭配ITX主板使用，也支持SFX/SFX-L搭配Matx主板使用，电源支架安装起来也蛮方便，其实机械大师的机箱只要把铝壳子拆下装机就很简单。
  - 由于超级紧凑的机箱设计，电源位被设计机箱前侧，通过电源转接线进行连接。
- 机箱设计有4个PCIe槽位，只要满足限长的显卡统统拿捏，机箱前部可以上一个9cm的风扇。

- 前置接口上给到了1只USB-A与1只Type-C接口

- 主板：七彩虹CVN B760M FROZEN WIFI D5 战列舰
  - 主板采用了12+1相直出式加强供电，CPU核心供电为12相，核显供电为1相，最大电流55A，CPU供电接口为8+4设计。B760芯片组本就是不支持CPU超频的，
  - 相对B760I推荐上14600K来说，CVN B760M FROZEN WIFI D5 V20 就更推荐配合i5-13490F或者是带核显的i5-13500使用了。

- 主板板载了4个DDR5内存插槽，单槽容量最大支持32GB，总共最多可以支持到128GB内存，内存频率最高支持XMP 6600MHz（OC），目前市面上的高性价比D5内存普遍以6000MHz、6400MHz居多，选B760M刚刚好。
- 内存时序CL32，工作电压1.4，内存PMIC不锁电压，用户可以自行体验超频的快乐，毕竟6800MHz的内存就要加400块呢

- 主板提供了1个采用了合金强化设计的PCIe 5.0 x16插槽以及1个PCIe3.0 x4插槽，其中x16插槽由CPU提供，x4插槽由PCH提供，可以用来扩展万兆网卡、采集器等PCIe配件。

- 主板提供了3个M.2接口，均为PCIe 4.0 x4，其中靠近CPU的M.2接口由CPU提供，剩余2个M.2接口由PCH提供，三个M.2接口均配备了便捷锁扣，靠近CPU的两个M.2插槽有散热装甲覆盖。正值双十一大促，加满M.2 SSD也花不了多少钱。

- 机械大师C28配240水冷+Matx主板，SFX电源是唯一选择。鑫谷SFX昆仑KL-750G冰山版ATX3.0全模组电源主打一个纯白配色，1块出头1W也还能接受。

- [小钢炮也有大能量｜13600K+B760+机械大师C28 装机实录](https://www.zhihu.com/tardis/zm/art/616613140?source_id=1003)
- 选择 C28 的理由是相比C26plus 宽度高度大了 20mm。实物并没有太大的尺寸差距，但换来更宽裕内部空间，对于机箱内部散热还是很有好处的。
  - 配件方面，13600K+ B760M +6600XT 硬件组合，日常应用不成问题，玩游戏跑个 2K@144 绰绰有余，特效稍微调低也可以流畅运行 4K 游戏。
  - 散热是超频三的风冷 K4，电源因为要考虑到后续要升级 4060ti，选用振华刚出的 13cm 白金电源 VP 1000W。 
- 机械大师的箱子都超级紧凑，尺寸较小，颜值也高，很适合桌面摆放，配合便携屏效果一流。
- 机箱可以支持 335mm 以内的显卡，6600XT 作为过渡显卡，后续会上 4060ti。
- 机箱虽然小巧，但可以支持到 280 水冷。其实我本来也是建议他直接上水冷，奈何朋友总是担心漏液，死活要上风冷。
  - 风冷的话散热高度限制在 162mm，超频三 K4 的高度是 156mm，可以说是刚刚好。
  - 四热管 + 130mm 高性能风扇，官方宣称能压住 12900K，压个 13600K 应该没啥问题。
- 振华 VP1000W 是刚出的新品，主打 13cm 短机身、全日系电容、高转换率。振华是典型的反向虚标专业户，额定 1000W 完全可以当 1200W 来用。而且标配的线材都是柔性软线，很适合用在这种紧凑型机箱里。

- 装机屏幕用的 INNOCN 15Q1F ，屏幕采用的 OLED 技术，显示效果出色，最关键的是这货支持触控，而且自带电池，装机调试都特别方便。

- 英特尔 酷睿 i5-13600K CPU处理器采用性能核+能效核混合CPU架构，拥有6个性能核和8个能效核。
  - 拥有 14 核心 20 线程，主频至高可达 5.1GHz，PCIe 5.0 至高可达20通道，DDR5 至高可达 5600MHz，24MB 的 L3和 20MB L2高速缓存。
  - 搭载英特尔 770核芯显卡，支持超频和WIFI6E网络。

- GIGABYTE B760M AORUS ELITE AX 主板
  - AORUS 系列属于技嘉产品高端阵营，定位追求极致的电竞玩家。
  - 主板采用了14+1+1相核心供电，辅助供电为 8 Pin + 4Pin 12V输入，60A 供电晶体管， 2 盎司铜电路板 + 6 层 PCB 设计，供电、SSD、芯片组等关键位置，甚至连南桥都覆盖了银白色的散热装甲，配合 6mm 热管以及高品质导热垫，让主板散热更为均匀，实现高效的散热能力。
  - 主板为标准的四槽内存设计，有D4\D5 两个版本可选。D5 版最高可支持 7600MHz（O. C），最高兼容 128GB 内存容量，其独有的超频黑科技（高带宽低延迟模式）目前也只搭载在 D5 版上。
  - 此外主板提供了双 PCI-E 插槽，靠近 CPU 的插槽采用合金装甲加固，支持 PCI-E 4.0 x16速率。下方则是普通插槽，速率也只有PCI-E4.0 x4，适合插一些扩展卡之类的。
  - 一体式挡板接口丰富，技嘉B760M小雕WIFI 提供了4个USB 2.0 接口、1个USB3.2 Gen2 Type-A接口（10Gbps）、3个USB3.2 Gen1接口（5Gbps）、1个USB 3.2 Gen2 Type-C接口（20Gbps），HDMI/DP 接口各1、以及2.5G网络接口。当然WiFi6无线网卡天线接口以及音频输入/输出接口、光纤接口都一一完备。
  - 技嘉 13代 主板开始推出的“高带宽低延迟模式”，对于内存性能提升效果明显，特别是高频内存，我之前曾经用它将 7200MHz 内存超到了 7800MHz，读写拷贝超过 10GB/s，写入更是逼近12GB/s（119.18 GB/s），延迟更是压到了 55.7ns，特别适合喜欢玩超频的朋友，有兴趣的朋友可以看看我之前做的测评。

- 技嘉从 b760 D5 主板开始，推出了个“高带宽低延迟模式”，同样的 DDR5 内存条在这块板能跑出更高的读写，更低的延迟，就拿雷克沙这套内存来说，同样的 5200MHz 开启这个模式后，相比正常XMP模式下数据都有不小的提升。

- SSD 是雷克沙定位高端的 NM800PRO 1TB。单面PCB 底板，厚度控制不错，笔记本或者游戏主机都能适配。SSD 表面覆盖新一代纳米铜箔复合材料，搭载智能温度检测模式，有助于快速降温，长时间使用不用担心高温引发的掉素问题。

- 散热用的手头的 超频三 K4。其实我本来建议上水冷，奈何朋友一直对水冷有偏见，总担心漏液的情况。K4 是 超频三的高端风冷，全金属扣具，支持 I家 / A家 全平台处理器，标配 GT-3 高导热硅脂，能够快速将 CPU 产生的热量进行传递。
  - K4 采用单塔单风扇设计，塔身为全黑色电泳工艺，独立装饰性顶盖，四热管触底导热、50 片130mm 铝制散热鳍片进行热量散发，两者通过穿Fin工艺组成鳍片群加大散热速度。整体工艺还是蛮精细的。

- 电源安排的振华 VP1000W。这款电源最大的亮点就是采用了创新的微型化技术，提高性能的同时尺寸缩减到 13cm 短机身、可以释放不少空间给其他硬件。电源本身通过了 80plus 白金认证，转换效率高，加上额定 1000W 的功率，别看身材小，拖 13900 + 4090都不成问题。

- 机械大师在紧凑型机箱里拥有不错的口碑，之前我就装过一次 C26 plus，体验极好。这次选的稍大一些的 C28
  - 机箱灵活度极高，除了基本框架，大部分面板都是可拆式组合，不过大量螺丝拆卸起来还是比较繁琐，这也是其被广大网友戏称为“螺丝大师”的原因。
- 背板可拆，方便走线的同时安装配件更加轻松。有些主板 m.2 是在主板背面，用这个机箱就可以在不拆主板的情况下加装 SSD。
- 顶部还支持 双 12cm 风扇或者 240 水冷。话说别看 C28 体积就比 C26plus 大了一点，但装机体验好了不少。

- 便携屏｜INNOCN 15Q1F
  - 装机我都是习惯用便携屏。INNOCN 15Q1F采用的 OLED 屏幕
  - 重量 0.94kg ，单手握持毫无压力，长时间使用有专用的皮套提供倾斜角度。接口是 Type C X 2 +Mini HDMI 组合，可以实现一线连功能（供电与信号传输一线达成）。
  - 这款便携屏支持手指直接操作，十点触控+内置的触摸OSD面板
  - 甚至还支持无线连接。INNOCN 15Q1F自身搭载了 WiFi 模块，通过它可以将主机、手机或者笔电的画面直接投屏显示，控制则通过触摸实现
  - 便携屏还内置 5000mAH 电池，可以脱离线材连接的不便，续航时间能达到 4小时左右，完全就是台平板电脑。

- [【17.9L】C28迷你手提主机 - 小红书](https://www.xiaohongshu.com/explore/664881a50000000014018c4a?xsec_token=ABjcFKpzYqPfIG6C1AnlqDTFCINPxDCJ7dN5lu4n9saWI=&xsec_source=pc_search&source=web_search_result_notes)
  - 开盖风冷都行

- ## [闪鳞G300支持164mm高度风冷 - 小红书](https://www.xiaohongshu.com/explore/66cd695b000000001f03a713?xsec_token=ABX2Viv4Qebp0rD6T3QkbAt8L2lTvl7qp8ds1dlZ-amvc=&xsec_source=pc_search&source=web_search_result_notes)
  - matx, 显卡340mm，没有玻璃侧板
- 如果用itx电源，电源底下能加12cm风扇吗
  - 不能
  - 因为这个如果在显卡底下装风扇噪音会比较高，前后各一比较合理的

- [有没有闪鳞 g300 平替 - 小红书](https://www.xiaohongshu.com/explore/68bfeedd000000001b03777b?xsec_token=AB7fK2DtVB9-Uox-1NRYZeZJRfF0RaYQ3O2_pLevARsAQ=&xsec_source=pc_search&source=web_search_result_notes)
  - 有没有比闪鳞 300 一样但是是铝的机箱呀，需要极限尺寸的机箱，主板标准 matx，sfx 电源，显卡是 7800xt 超白金版，
  - 不需要装水冷（g300 因为可以装水冷，所以机箱比较厚），
  - 需要背部理线，可拆卸 pcie 挡板（能拆卸后板也行，因为显卡长 320）

- 已经看了小喆的，b3，c2p，但是没有背部理线，c2p 不知道可不可以拆后板，都不大行

- G300就挺好的, 底部风扇和屁股风扇我都没见，散热完全足够

- 底部能装三把风扇吗
  - 只能装2个

- 铁的不行吗？
  - g300，3.2kg，小哲 b3，1.8kg

- Ncase M3.. 应该是综合性比较好的了

- [闪鳞G300 9700x➕5070ti风冷改造方案 - 小红书](https://www.xiaohongshu.com/explore/68be261e000000001c03c453?xsec_token=ABL-IFl_t7vNlynLFA54jExvARox4t1Q4sD_V7oRMh-_U=&xsec_source=pc_search&source=web_search_result_notes)
  - 第一次装机没经验，风冷买了乔思伯CR1000max，结果发现根本压不住，随随便便撞95度墙。
  - 后来机箱尾部加了个利民c12pro，散热塔风扇换成了零度世家风尊t30co（塔还是乔思伯的没换）。现在散热表现如下（烤鸡10分钟，均为CPU温度）：单烤CPU77
- 乔思伯的散热器拉完了
- 这个箱子没啥加的余地了，下面加风扇离显卡太近了，属于是副优化了，顶部加风扇要自己配磁吸螺丝，还是散热器换好点的改善最明显

- 换个双塔不就好了。而且不吃显卡尾气不可能的，这机箱也就这样了。
  - 好的，双塔有人说p60t最强（买塔自己配风扇），这个是真的吗
- 可以的，放远点其实也不是很吵

- [终于赶在双十一末尾买齐了 - 小红书](https://www.xiaohongshu.com/explore/673030e6000000001b012544?xsec_token=ABwBx_0AZ3zhOiWwQ_EVFjfonKMxsn0Fki4JP09JVTi8g=&xsec_source=pc_search&source=web_search_result_notes)
- 4070s功率那么高你就买个650w的电源？
  - 哪怕想后续升级，至少买个850w的也行啊
- g300通风做还行，但是加个风扇保险点
- 尾部风扇最重要……4070s厚度还好，底部也能按，不过整套功耗不算很高，有个尾扇足够用

- [闪鳞g300改装思路 - 小红书](https://www.xiaohongshu.com/explore/6810d0cf000000002100613c?xsec_token=AB_QqkK7_ZF3_KbwyW1ZB1W22MKjj0BCjU-aVf69KLO5s=&xsec_source=pc_search&source=web_search_result_notes)
  - 闪鳞g300挺好玩，在做到尽可能多兼容，支持340mm长度显卡，14cm atx电源和164mm风冷的情况下，能尽可能缩小体积，做到媲美itx机箱的体积，是我最爱的机箱。
  - 在换装闪鳞g300机箱后，我先是上了双塔散热器ak620pro，然而整机将近20斤的质量，让他变得不那么可移动，
  - 对这个窘境，我将目光移向下压式散热，为此更换idcooling-isxt67，并更换散热为12025的九州风神ft12。isxt67塔体兼容性确实不错，在做到尽可能美观的同时也不遮挡任何内存槽。后置风扇位做进风处理，为避免风切声，需要将风扇移到外面
  - idcooling-isxt67塔体优秀，更换风扇之后能稳定压制180w的13600kf（渲染最高温度80℃），同时由于风扇数量少，做到更静音，是一个不错的改装思路。

- 技嘉m650小雕主板，用哪款双塔不挡内存呢，我看您这个风冷好像很小
  - 我这个是下压式风冷，基本上用matx主板都可以不挡内存，如果你是9700x以下的cpu默频应该都是能压得住的，开pbo的话表现可能不好。双塔风冷，你可以看看九州风神阿萨辛四或者阿萨辛4s。

- 同款机箱，请问之后换的下压式，比620pro散热如何呀
  - 同一个CPU相比一下高了大概10度

- [第一台matx，闪麟g300，就喜欢这种塞满满的感觉，下一步准备换个大显卡，然后把机箱立起来摆放 - 小红书](https://www.xiaohongshu.com/explore/687222ef000000001203f6cb?xsec_token=ABMrApDT4vX1zr_5qUgsvW1ie38sgqbr-KgLksPrLadcA=&xsec_source=pc_search&source=web_search_result_notes)
- 请问右下9cm风扇是正叶还是反叶，进风的吗？叠加三个为啥
  - 出风，主要侧面换成亚克力透明板，显卡温度不好从侧面出去，所以靠这三个风扇把风从前面引出去，其实两个就够了，三个是为了饱满好看
- 塞这么满会不会影响散热啊？
  - 有风道的，侧进后出
- 右下角风扇是啥
  - 利民9cm风扇， tl-p9w-s

- 300是不是没有顶部风扇位
  - 没有，但是空间够装薄扇，就是如何固定要自己想办法

- 大佬用的内存风扇是用的什么支架？
  - 乔思伯NF-1内存条风扇自带的

- 显卡吊装温度会升高很多，尤其是小机箱大显卡
  - 这也没吊装啊……直插的
- 他说要换大显卡然后把机箱立起来

- 电源那里网孔挡板哪来的啊
  - 前面是订做透明亚克力板，电源旁边小风扇网格板是内存风扇自带的

- 这个机箱支持非模组电源么
  - 支持的，但线堆在一起比较难关侧板

- 这么紧凑散热跟得上吗？
  - 4060和12490F，配置不高，目前温度稳定，显卡最高到72

- ## [新品预告：闪鳞G350机箱 - 小红书 _202504](https://www.xiaohongshu.com/explore/680b49e4000000000f03025e?xsec_token=ABmVEaGHnouuW4by4cF_K2PztIm78YN2rgioigqEQn8-4=&xsec_source=pc_search&source=web_search_result_notes)
- g300加顶部风扇支持吗，太心动啦
  - g350支持两个顶部风扇
  - 电源底下没有，机箱一共5个风扇位

- 和g300啥区别
  - 多了背插，16厘米电源兼容，顶部两个风扇位，侧透

- 电源支持15？
  - 16cm

- 能不能出个mesh板，把玻璃换成网孔

- ## [机箱说¹ - 乔思伯和机械大师谁赢了 - 小红书](https://www.xiaohongshu.com/explore/66a61571000000002701010c?xsec_token=AB-NVtDH_xyoN48IVgN-otrQDhbPhG6D8S77xA6fATSDM=&xsec_source=pc_search&source=web_search_result_notes)
  - c+max尺寸:392mm*284mm*185mm  20.5l体积
  - z20  尺寸:370mm*295mm*186mm  20l体积
  - z20最好的方案是风冷+atx的组合
  - c+max最佳方案是水冷+atx的组合
  - c28在安装240水冷的情况下，大部分主板不支持atx电源。

- 组装的话我感觉差不多，z20对新手更好吧，防尘同一水平。

- 比较喜欢机械大师，用料是真厚实，配件相对来说也多一点，不过性价比来看比不了一点
  - 铝合金和钢的，材料就不一样，重量也轻了。不然咋降不来价格

- 两款都用过，个人倾向于z20, 超级好看

- [机械大师 c28 - 小红书](https://www.xiaohongshu.com/explore/6717559e0000000016021389?xsec_token=ABE6Ld3Qrhhpu6tuNb5p51L1Q3oe3WokQOP0_Eksi_ke4=&xsec_source=pc_search&source=web_search_result_notes)
  - 选择了 c28，装机成功
  - 和朋友的 z20 对比小那么一丢丢，c28 还是建议用 sfx 电源，这样好藏线些！atx 电源确实大了点极限安装
- 风扇是哪个型号
  - 利民s12

- [机械大师c28帅无敌，9700x+5070？ - 小红书](https://www.xiaohongshu.com/explore/68af1a1d000000001d02d18f?xsec_token=ABx7Z2Y7-KnOKMOASaKY8sp7br1TF0G7T40iVw6hcK7ww=&xsec_source=pc_search&source=web_search_result_notes)
  - 首先说一下为啥选择这个机箱。深度400mm桌面，找了很久唯一兼容风冷水冷的机箱。考虑的背后插电源线和出风。抛弃了z20，选用长度350mm左右机箱实施证明刚刚好。还有两款机箱是这个平替但是不支持水冷
  - 再说散热，散热其实hyp612，ak620，p60t都挺好。本来想要数显版本的，后面刷到目前数显bug太多，放弃了。
  - 电源这个纠结最久，按理说考虑兼容性应该一步到位sfx。但是sfx850w坑太多了。最后选了这个鑫谷的，这个电源好处是120mm，和sfxl一样长，电源线出口不太容易和显卡干上

- ## [乔思伯Z20 or 机械大师C26 - 小红书](https://www.xiaohongshu.com/explore/66d70459000000001f01e720?xsec_token=ABFpKqSuGzHOELX8EkCIc8ArGFoGzwbK104D0gsq2YzyU=&xsec_source=pc_search&source=web_search_result_notes)
  - 机械大师C26: 315*160*265mm, 13.3L
  - 乔思伯T6: 13.7L
  - 就玩下黑悟空是选择12600kf还是12490f，然后就是机箱乔思伯Z20 or 机械大师C26，怎么看都好看就是不知道怎么选了

- 玩黑神话124就足够了，现在126太贵了

- c28 大一些可以用 atx 电源，c26 装 sfx 电源和 c28 装 atx 电源差不多，藏线有些困难，看中机械大师便携和颜值，散热加装五把风扇完全够用

- z20可以atx电源+240水冷 c28只能sfx+240
  - 不用itx的哇他俩都支持matx的哇

- 5把风扇，上下14cm，后置12cm，刚刚好
- 主板微星B650M GAMING WIFI

- 下面放两个14就没地方放显卡支架了吧
  - 是的，小显卡也不需要

- z20可不闷，不是以前的炼丹炉了

- Z20好，底部可以装2把12cm风扇和1块3.5英寸机械盘。装机也比螺丝大师省力。颜值上我个人是喜欢Z20的简洁感

- ## [闪鳞g350还是乔思伯z20 - 小红书](https://www.xiaohongshu.com/explore/68b462bb000000001d02a8a5?xsec_token=ABHRfK0CgtuFDQhWIxlZF5BI37zGCq6uwnRe3ZkLYVd3I=&xsec_source=pc_search&source=web_search_result_notes)
  - 显卡29cm涡轮3090，计划用风冷。外观上偏向g350。有散热焦虑，考虑cpu和电源这一串的散热，
- 质感做工是z20更好一些，散热我用着感觉差不多，闪鳞优势在前置接口太顶了

- 我都用过散热基本没区别

- sfx电源加短显卡可以参考这个，我g350塞了个338的显卡就没辙了
  - 我用的146kf加微星b760m刀锋钛，板u套装2300
  - 另外涡轮卡不用有散热焦虑，还是比较依赖自身涡轮风扇的
- 我想用14700cpu有必要用z主板吗想买一个b760m的算了
  - 稳定运行需要挑块供电好的主板，看超不超频和差价吧

- 前置电源的就别想着散热好，没有前进风的都是焖罐
  - 九州的ch160有前进风，稍微比你发的这两大一点

- g350的话最好买背插主板，看着好看一点，散热感觉用哪个都行不用担心

- 这俩其实差不多，看你是想要UI多一点儿还是能替换玻璃板，Z20的玻璃板是可以换成私人定制的亚克力板这个是需要自己买，G350他的这个板子是没法替换的

- [想换小机箱 - 小红书](https://www.xiaohongshu.com/explore/68ce8bd3000000001300fcdc?xsec_token=ABp12HvDLqm3bcBXz75MLag9SHKyM4ALJFCDd6jzfp9_c=&xsec_source=pc_search&source=web_search_result_notes)
- g300 也行吗，就一个风扇位哎，感觉会很闷啊，散热性的话其实想选 g300，因为最小
- g300的问题是电源出风在机箱内，容易被cpu散热器抽走

- g350 有点大，我现在有点纠结 z20 和 g300
  - 一样长，高了1.5cm底下可以多塞两个风扇，宽多了2.4cm增加背线空间还可以装机械硬盘。
  - 300风扇少各有优势。选300你可以对比乔思伯c6吧，Z20是和g350同级别体积20L啊

- g350太大了 买了有点后悔 ，之前的机箱又盖不上盖子 风冷太大 机械大师c28又太贵了

- 小机箱风道都差，要舍才有得，这款机箱能放 240 水冷和 atx 电源，忘记有没有理线空间了，我就选了 ch160plus，不是很推荐 ch160plus，电源线材太长太硬就很难塞，装机贼难受

- 乔思伯z20的散热你完全不用担心！我就在用！！
- 散热没问题的 我146+5080用的z20

- ## [小机箱乔思伯z20和闪鳞g300选哪个 ](https://www.xiaohongshu.com/explore/66f7512b000000001b022ed4?xsec_token=ABeOr8Ft0HNW3FbtvsjZTd5rWYn4gt7MDLAuGVYnlQiIQ=&xsec_source=pc_search&source=web_search_result_notes)
- 乔思伯Z20, 风扇利民TL-S12，正反叶都有
  - 买的二手散热不怕坏，然后新的风扇搭一下
  - 主要是用了利民的pa120风冷和tl-s12光圈风扇
  - 黑色电源随便上，不挑

- z20底下不准备装风扇了吗
  - 我是单塔风冷，cpu单烤半个钟不超过95度，平常待机看视频等34度，玩黑悟空70度左右，感觉没什么问题
- 这种机箱打开侧板比装风扇有用
  - 侧板没开的，因为养了猫，毛太多不敢开
  - 散热器九州风神，具体型号忘了，你搜一下有数显的应该很好找

- 看你配置，z20的缺点是侧透不是快拆设计，经常想打开散热就很痛苦

- 15×15 好像塞不进 G300
- 是的，只能用利民750的，但是性价比不如玄武850 
  - 我也准备装，打算玄武 650k 的，结果大了 1 厘米
- 卧槽利民pa120普通版+鑫谷冰山版+z20跟我一样诶
  - 是，利民pa120mini+追风者650W

- z20吧 g300没有背部走线感觉太难装了 虽然这个机箱也很难装

- 风冷g300，水冷z20
  - z20比g300大一点，我用的风冷，比较偏向于g300塞满的感觉，如果用240水的话z20比较好看

- 我现在觉得无脑g300 闪鳞的mesh板实在太好看了 而且体积小上面两风扇加不加也没那么重要
  - 感觉你是对的，关键在于风道，g300用风冷的话，上风扇不重要，关键在下风扇的进风能力和侧面排风能力

- 我选的g300，不喜欢玻璃侧板的，容易爆，而且散热差

- Z20好看，质感很好

- 我也是在这两个之间犹豫，我之前淘汰下来的板U想装个小机箱带到单位摸鱼用，因为电源是SFX的，G300想装sfx电源，还要另外购买套件，注意这个套件是水冷支架+电源转换套件，是捆绑销售的，我又不用水冷我干嘛掏这个钱，这一点让我很不爽，我就买了Z20

- ## [个人购机，主观评价，欢迎提问！ - 小红书](https://www.xiaohongshu.com/explore/68c0238f000000001d004524?xsec_token=ABFuZAkrrSKYsMlqCenxgM1Y6uNePfwC_HGRX06HHxyp4=&xsec_source=pc_search&source=web_search_result_notes)
  - 1. 做功用料最好的是乔思伯的Z20，板材最厚最有质感。
  - D32PRD与CH260尺寸都非常接近。
  - D32PRO的理线布局绝对是这四台小机箱中最合理的，这一个电源挡板可以挡很多线。走线也会更轻机。我个人认为最难的是CH160plus，前面没挡板. 后面也沒有，走线全暴露。
  - CH260和CH160plus是不能装底部风扇的。

- 六台里Z20是最厚的，有些比他大的还没它重呢。闷不至于，可以底进上出。前面板有空洞的，留给电源散热的。
- 一般都是后面都是出风的，出的多进的少，就会造成负压，机箱内就会自己吸进空气

- 侧板金属板是不是好点
  - 是的

- ## 📌 [itx机箱选哪个 - 小红书](https://www.xiaohongshu.com/explore/67fa9cc6000000000b02cb14?xsec_token=ABufSAS9QghohUw1fzyX0iVNfOBOR7ae1CsQsryEQvDrQ=&xsec_source=pc_search&source=web_note_detail_r10)
  - 目前市面上的闪鳞L300/400，酷冷ncore，九州风神ch170/270等都看过了，感觉不是颜值不够就是体积太大，其他的itx只能横放，所以选了这两个进决赛圈。
  - 但这两位hyte revolt3的可玩性更高，可以装240水冷，风冷也有140mm充足的小双塔或者下压散热空间，但体积就比fdt1大了3L而且颜值肯定还是formd好看
  - formd t1 v2.5价格相对高，但是体积小，投影面积也小，颜值高。相对散热能选很薄的下压风冷，240冷排倒是也能安，烦恼是我觉得cpu散热会有风切声，而且98x3d的功耗也不低。

- [便携主机小机箱推荐！带配置推荐 - 小红书](https://www.xiaohongshu.com/explore/67ccf00b000000000603b048?xsec_token=ABb9QlEEv4edez8zXqcCpR1c6L8yELfSKA3oNbbrletUs=&xsec_source=pc_search&source=web_search_result_notes)
  - 后面附带两套性能非常不错的配置方案。
  - 小主机的安装难度会比较大，紧凑的机箱空间对于配件的安装顺序以及理线都是比较讲究的，有时候可能安装顺序错了就得拆开重来，会有一定的折腾属性，无论新手还是有经验老手都要做好心理准备

- [cpu散热搭配 一看就会 - 小红书](https://www.xiaohongshu.com/explore/68bd273b000000001c006781?xsec_token=AB3IlccEHpLqWO68RcyJXC3wJqTzyJEBj3EjpFo1z1Bhg=&xsec_source=pc_search&source=web_note_detail_r10)
  - 只要不超频 原装机够用

- [formd t1 itx风冷配置分享+经验 - 小红书](https://www.xiaohongshu.com/explore/66d53972000000001f03a988?xsec_token=AB36raZON7rhJOGKgOTp2CP7HXu79wn9eyAjSxKYmydXE=&xsec_source=pc_search&source=web_note_detail_r10)
  - cpu+显卡：12600kf+4070s公版（t1可2.25槽，散热限高68）（cpu怕压弯可以买个扣具）
  - 风扇：cpu是散热原装，机箱是2个T30，小机箱吧热量排除才是关键，嫌吵可以换猫扇？也可以用fan control（开源的）自己精确设定转速曲线。

- [极致itx风冷主机！ - 小红书](https://www.xiaohongshu.com/explore/680779ab000000001c01d6ea?xsec_token=AB4Cx2A5MWHbcyCyxcg0yIjXwSumOkgsgXOeULyDbKBQE=&xsec_source=pc_search&source=web_note_detail_r10)
  - ncase m2
  - 9950x3d➕5080公版
  - 这是啥箱子？六面全透啊，不错不错，其实下面的风扇个人觉得没啥太大必要加，下面基本贴地了
  - 六面全透，最好的是华硕AP201冰立方机箱。
  - 风扇干了小两千

- [十代CPU，黑苹果最后的倔强 - 小红书](https://www.xiaohongshu.com/explore/65499801000000002202c90b?xsec_token=AB-kwWy_ndn0QOUFCU234Q6f2t_yjutR9JJFSe8XxQYy4=&xsec_source=pc_search&source=web_search_result_notes)
  - 机械大师c28: 342*185*284mm, 18L 📌
  - 这个机箱不错啊，进3出3，外加塔式，其实塔式后面还能放个风扇组成9风扇，起码散热不用愁
  - 只是在itx里散热还不错而已，跟塔式没得比。风扇多噪音也大，小机箱理线也难（这机箱装机半小时理线3小时），一切都是为了颜值的妥协
  - 这个正好，比很多大闷罐好看多了，这个散热不差，你在给散热器加个风扇双塔三风扇，兼顾美观和散热，挺好的，我现在机箱就是9个风扇的matx, 酷冷至尊 MCB-Q500L-KANN-S00 : 386 x 230 x 381mm, 33L, 也就打游戏散热还行，topaz该螺旋桨还是螺旋桨，还是得开侧板

- [9950X用风冷实际体验 - 小红书](https://www.xiaohongshu.com/explore/68415da50000000022005234?xsec_token=ABni7f4b-fffCPxt0H6aLouKtK6gxBT1LF2_CCDAkgMZo=&xsec_source=pc_search&source=web_search_result_notes)
  - 对大多数人来说都看不大出来，或者像我这种不怎么玩FPS的，就不用考虑超频这些了，默频完全够用
  - 我感觉更重要的是配一个风道机箱(我用的是联力207)，然后上个双塔应该就够用了(单塔里也有Hyper 612 Apex这样的高手在)，我用的是160+淘来的二手利民PS120EVO，七热管双塔，甚至还有点歪歪的，不过100+买来的便宜货我也就随便了，能用就行

- [小机箱绝配，双塔逆重力热管，利民小银魂 - 小红书](https://www.xiaohongshu.com/explore/6389ca410000000022028074?xsec_token=ABFaT5DIfPsJIcxbjZdwSLk05zjfIEy_AtMNX-25fkBN0=&xsec_source=pc_search&source=web_search_result_notes)
  - 机箱是机械大师C26 plus，水冷兼容性极差，风冷也限制在140mm以内，看来看去还是利民这款小银魂最合适，顺手入了个白色的
  - 散热器尺寸为120 X 135 X 94（mm），迷你双塔，白色涂装，搭配 TL-D12PRO-G 伺服级风扇，不管是性能还是尺寸都很满足我这套主机的散热需求

- [电脑小机箱该怎么选？ - 小红书](https://www.xiaohongshu.com/explore/66518b9a0000000005007b1f?xsec_token=ABgsZawth9QaYeqFGFhvroUrQnp2-uJiFwrxEDnmydBiE=&xsec_source=pc_search&source=web_search_result_notes)
- 乔思伯(JONSBO) Z20， 主体尺寸长宽高 370*186*295 约20L, 
  - 支持240水冷 163mm双塔风冷
  - 支持限长363mm高性能显卡&全尺寸MATX主板
  - 支持背走线 电源支持ATX电源侧装 竖装
- 华硕AP 201, 主体尺寸长宽高460*205*350, 33L
  - 支持360水冷 17cm风冷
  - 显卡支持358mm 6面通风 4个硬盘位

- ## 🤔💡 [有没有适配较小机箱的高性能风冷推荐？ - 知乎](https://www.zhihu.com/question/491647469)
- 如果是小主机 可以考虑下压式的风冷
  - 下压式6管， 双风扇 还有RGB可以选 可以说是DIY玩家很合适了。
- 两种类型 一种可以随意伸缩 一种是PCIE的侧吹 可以吹 组风道。

- 🤔 与其自己研究风冷水冷风道，如何直接参考指定cpu/gpu的机箱案例

- [闪鳞g300，终于完全体，果然竖着才是最好看的  ](https://www.xiaohongshu.com/explore/68baad38000000001d028c54?xsec_token=ABltSBPxJJg2hpuRLt4eQMLjBIAoL5YNYMLjtqKfRi9_Q=&xsec_source=pc_search&source=web_search_result_notes)
  - 主板：精粤B760M-KD4 wifi 
  - 处理器：12490F 
  - 显卡：影驰4060大将白色 
  - 硬盘：爱国者P7000Z 1TB 
  - 内存：金百达银爵DDR4 3600 
  - 风冷：利民PA140WHITE+2个风扇TL-M12RW+2个显卡支架 
  - 内存风扇：乔思伯NF-1 
  - 电源：玄武650K白色 
  - 机箱风扇：底部1个15mm厚度薄扇利民TL-H12015W-S, 显卡右边9cm高度3个小风扇利民TL-P9W-S
- 显卡上边小风扇咋固定的呢？我G350也想搞个吹显卡
  - 扎带绑就好了，但我这个是吸风，把风从顶面排出去

- [可以带上飞机的风冷小钢炮，5070ti配置分享 - 小红书](https://www.xiaohongshu.com/explore/6809bcaf000000001c02e3f2?xsec_token=ABmERV5M2HyK5KDotkEXLkb7DeMGpfr5ndFUkECpUJvJQ=&xsec_source=pc_search&source=web_explore_feed)
  - 【机箱】闪鳞 G300 黑色: 188 x 345 x 260 mm, 16.8L 📌
  - 【散热】利民 PA140绝双刺客 6热管双塔
  - 【显卡】影驰 RTX5070Ti 金属大师黑金版 O16G
  - 关注了很久的风冷主机，博主搭配的配置合理，这一套基本也能满足2k高画质游戏需求了，还可以把主板显卡盒都寄来了，非常满意

- [【极鱼电脑】5K预算, 拿下RTX4060+i5 12400F - 小红书](https://www.xiaohongshu.com/explore/6707ad20000000001b023290?xsec_token=ABq7KokyP4l816ahZYziBBvJYC4Qak58_fLCWW_pIxj94=&xsec_source=pc_search&source=web_search_result_notes)
  - 【机箱】：闪鳞 G300 白色
  - 【散热】：乔思伯 CR1000EVO ARGB 白色
  - 【显卡】：影驰 RTX4060 8G 大将
  - 【CPU】：Intel i5 12400F

- [可以手提上飞机的5070ti迷你主机 - 小红书](https://www.xiaohongshu.com/explore/68148ed3000000002202ac13?xsec_token=AB-Uvho_Y0GpiJDp6zmaglVYdYNGTBg3XQwcDpwK8pUMA=&xsec_source=pc_user)
  - 【机箱】闪鳞 G300 手提桌面小机箱
  - 【散热】九州风神 阿萨辛4S 高端风冷
  - 【显卡】影驰 RTX5070Ti 金属大师 黑金OC 16G

- [有没有双塔风冷散热器适用于迫击炮主板不压内存，能压住9600X的 - 小红书](https://www.xiaohongshu.com/explore/67f87bc0000000001c001bd9?xsec_token=ABLUYzRFk1yrCyyZARJhGbzYFAAIgFouS3rVw01NAec2U=&xsec_source=pc_search&source=web_note_detail_r10)
  - 你不超频的话，单塔都行
  - 可以单塔+开侧板+电风扇
- 我准备上cmax，我看你电源下面装了一个进气吗？
  - CMAX可以的，显卡选择更多，前面板是个9cm风扇，前下进风，后上出风
- 利民rk120se
  - 你这个散热压的是啥u啊，这个和酷冷至尊612在纠结。。
  - C28，压的9700x，这个和酷冷也不是一个价位的啊，利民这个肯定够用

- 利民有一款，现在正在用, 双塔，6热管，不挡内存
- 我用的利民pa120 b650主板不压内存, 双塔就行 开pbo烤鸡145w 温度最高92
  - 我的b650e天选用不了双塔，左边一块铁右边是内存，但是装的时候没试过抬高
- 利民FC140
- 利民RK120
- 单塔双扇六热管就足够，利民制裁，我就在用，散热相当给力
- 我9700X用的利民PA120SE，目前温度正常
- 我9700X都只用利民X53下压，没那么焦虑

- 那些说四热管就随便压的是真没实际用过9系芯片，就单说9600X，睿频5.4的芯片，用4热管散热器只能让CPU跑到4.6赫兹，建议上双塔风冷或者240及以上水冷

- 单塔612apex足矣完全不档

- [9950x3d对itx机箱太友好了，既安静又高效，待机42度，玩游戏60多度还静音，双烤180w+450w ](https://www.xiaohongshu.com/explore/67ede5d3000000001202edf1?xsec_token=ABTemFrBXmKvmdgQwWJU9gnNkp5wlW6bL0Dk9uWTiJWBE=&xsec_source=pc_search&source=web_search_result_notes)
  - 配置是9950x3d+4090+利民120x67下压式风扇，
  - 利民120x67 和12015风扇，顶部一个12025一个12015
  - 下一步准备把4090换成5090d
  - 我利民90x47 压98x3d 玩个游戏轻松80度，早知道不上那么极限的itx了，想问问博主你的机箱便携性如何，上飞机方便吗，顺便想问问其他人的
  - 这就是我们 itx 玩家，盯着丐版买哈哈
  - 我用来生产力的虽然不是每时每分都在跑任务
    - 那建议上个好点的水冷或者双塔风冷

- [闲置配件重组，小机箱里塞一张4090 - 小红书](https://www.xiaohongshu.com/explore/679000e6000000002900d92c?xsec_token=ABMD6mhQ-2BymdWDpwL5hvfM8OOubZz_p0mUadq6O7lw8=&xsec_source=pc_search&source=web_search_result_notes)
  - C+MAX的箱子，白猛禽4090 oc
  - 机械大师C34pro: 这都快中塔了，有些大了

- [打造最强ITX主机，仅12L的I9+RTX4090小钢炮 - 小红书](https://www.xiaohongshu.com/explore/65a92ab2000000002a033278?xsec_token=ABSBEXLTFElYGee4WjQ7FQrmAnS3M78y8zG87vi2iVIac=&xsec_source=pc_search&source=web_search_result_notes)
  - 分形工艺Ridge

- [能装4090的10L超迷你顶配 itx主机！ - 小红书](https://www.xiaohongshu.com/explore/66feab5b000000001902e426?xsec_token=ABlu4J6--wKooejNGxnEt8DN6ozr-DSEM4a2kEPukXYkI=&xsec_source=pc_search&source=web_search_result_notes)
  - 能在这么小的体积装下9950x➕4090，估计只有 联力 T1 了。

- [整个世界都安静了，装入5080显卡的风冷主机 - 小红书](https://www.xiaohongshu.com/explore/67d78dda000000000d017cfa?xsec_token=ABlo-M2mkEksa4R6fDVfvdseBp4z5h5kgTVaUZl9pOpYg=&xsec_source=pc_search&source=unknown)
  - 分型工艺 Torrent Nano 可以说是最强风冷ITX机箱，塞入旗舰CPU和5080/5090D显卡没有问题，硬件选择和走线方案经过多次迭代趋近完美
  - CPU：AMD 锐龙 7 9800X3D
  - 显卡：影驰 GeForce RTX 5080 金属大师白金版 OC
  - 机箱：分形工艺 Torrent Nano RGB 白色, 体积太大

- [高颜值135mm小塔，利民PA120 MINI开箱安装！_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV1DH4y177Q2/?vd_source=deff4d2e2efa3273948dd6911a08fd39)
  - 塔体，总高度135mm

- 💡🌹 [除了难装，什么都挺好 - 小红书](https://www.xiaohongshu.com/explore/683a78d60000000023012638?xsec_token=AB_w2cD0Ez3Uraiu24sIOdVCNVjGP6ywl00WVNctWCHeY=&xsec_source=pc_search&source=unknown)
  - 如果需求的标签要满足大显卡、MATX、标规电源、双塔风冷、紧凑，闪鳞G350是不错的选择。
  - G350: 21 x 34 x 28 cm, 20L 📌
  - 底部风扇是 利民TL-C12PRO, 声音还能接受
  - 如果想用16cm电源来满足进风风扇在前面板左右居中位置（强迫症）、底部双进风扇，注意供电线、面板线都要预埋到主板下方
  - ROG B850小吹雪、九州风神阿萨辛4VC至尊版新品集合首秀，全白达成。
  - 98x3d，Rog b850-g，32g 8000阿斯加特，Rog 白金雷鹰1000w，阿萨辛4vc至尊版。
  - 显卡和固态没参考价值，5把机箱风扇看个人喜好
  - 这机箱自带显卡支架
- 你说g350的时候忘了它最大的特点，背插
  - 无论市场占比还是用户接受程度，背插这个点个人实在是不太关心。。何况amd平台的一线背插版好像是一个手数的出来
- G300顶部风扇位都没有，和这个比？加宽的部分在我眼里价值就能用大电源和好理线，而不是根本没几个型号可以选而且残值炸裂的背插配件。背插产品的销量能不能让这个方案撑过阵痛期都是问题

- 800多的风冷 疯了吗
  - 为颜值买单

- 我买的620，感觉到时候也把主板遮住了
  - 嗯前装挡内存后装挡主板

- 我装完了，但是玩游戏的时候拉满CPU80℃不到，gpu60多℃正常吗
  - 很低啊，75不高的

- 这个typc 接口你们的线能全插进去吗 我的苹果数据线不能完全插进去
  - 可以插，线跟机器没有完全贴合 是有缝隙的

- 电源前置还是不适合风冷吧，ch260/270要合适点吧
  - 能不撞墙降频就算能用，G350对标的是ch160/170，手提箱嘛肯定没法六边形
- 紧凑型直插机箱的电源一般都是这么装啊，前面冲网进风

- 这个的装机难度很高哦
  - 用16cm电源会稍有难度
- 这个双塔风冷造型很喜欢，侧看里面很像一块一块录音室的隔音棉
- 显卡限长多少啊，我335的卡好怕装不进去
  - 340

- io线跟底部风扇撞得一言难尽
  - 因为机箱出厂设计没给足够的弯折空间

- [利民最新性价比风冷之王？PA120后继有人？ - 小红书](https://www.xiaohongshu.com/explore/68a25df0000000001d008b69?xsec_token=AB6eEiv8Jga5YuqGHfqLGMKBS62nhuM7ceSyfjW0FC3fM=&xsec_source=pc_search&source=web_search_result_notes)
  - 两款：Royal Pretor 130 和 Royal Knight 120 （不是SE！！SE风扇是旧款！）

- [盘点利民随机十款产品，从夯到拉五个级别 - 小红书](https://www.xiaohongshu.com/explore/68b86a8a000000001d037f1d?xsec_token=ABTE1Axv-5o-X12XW6KbsOFY6VCPlbEhwKmVzBccY4g40=&xsec_source=pc_search&source=web_search_result_notes)
  - U120ex单塔风冷
  - 双塔风冷pa140，挑体质，换个配扇表现尚可，这里给到人上人

- ## [机箱小影响CPU散热吗？ - 知乎](https://www.zhihu.com/question/335865142)
- 机箱小肯定影响散热的。但是风道也很重要，有合理的风道，就可以使小机箱也能有不错的散热。
- 以我资深散热控的身份告诉你，机箱大小不是关键，所谓的风道也不是关键，关键是出风口，传统方式来说就是主板后挡板上面那个风扇口。
  - 现在大多是单风扇位，以前还有过双风扇位，这个位置一定要上一个大风量优质风扇，转速再适当调高点。
  - 进风口也一定要有，但是不敏感，大多数机箱进风口都在前部，你可以用低转速，至少要保证一个风扇吧，两个最好，没风扇，或者没有进风口也是不行的。

- 风道设计十分重要，如果你的机箱内风道没有设计，比如小机箱CPU散热直接吹到没有孔的机箱侧板或上板上，热全都锁在里面，那么自然待机50来度。
  - 对于上面无脑上水冷的，我只想说，本来机箱就已经很小了，你水箱和冷排放在哪里呢，更何况入门级水冷的散热效果比大部分风冷要差这是事实，小机箱还是设计好风道让空气在机箱里流动起来效果最好了。

- [我30来年diy才明白，最好的家用机箱就是开放式机架，风道什么都是骗人的 - 知乎](https://zhuanlan.zhihu.com/p/1931289802654855351)
  - 我吃惊的发现，开放机箱，只要机箱风扇轻转，就能形成均匀充沛的气流，根本无需机箱结构导风 ，开放机架最酷的是可以叠加，老电脑和新电脑做在一起，混合接几台显示器，键鼠弄几套，灵活性无以伦比
  - 只要家里有安全的空间（不被人泼水 宠物破坏等等），开放机箱就是diy最终归宿。
  - 板卡受力好，稳定寿命长，风扇避免了最不好的标签向下的摆放。维护管理也超级方便。灰尘也不严重，没什么怪异的乱流，就没什么顽固的灰尘积累。旁边放台空气净化器更佳。
- 家里没新风系统的别试了……灰尘和扬尘不是每个地理位置都控制得好的
- 灰太大了，不行的，我深圳离海边只有3公里30楼那灰大的。。

- ## [小机箱是怎么解决散热的？ - 小红书](https://www.xiaohongshu.com/explore/6710a2ab000000002100583d?xsec_token=ABM6aePzBDdvEmqW7AP7IWy2aQbrM8b-WUMg-puQ2H2DU=&xsec_source=pc_search&source=unknown)
  - 非常经典的机械大师C24，樱花粉配色，9.9L的体积
  - 小机箱散热到底行不行？只上风冷到底能不能压得住温度？
  - C24的机箱构造采用了菱形的开孔透气的侧板，也是非常有特色的一个设计，同时上下两面以及背面都有做开孔设计，保证了良好的透气性能；
  - 而小机箱的空间紧凑，能够实现最优风道方案的，其实就是机箱尾部的风扇，可以说是神来之笔，加装之后才能发挥小机箱的短风道优势
  - 显卡如果搭配一张双风扇的显卡温度则可以还要低上几度；

- [联力又一个有爆款潜质的机箱 - 小红书](https://www.xiaohongshu.com/explore/66e30ddd00000000120107c2?xsec_token=ABofaNF4fkho52iws-yq8ScYcAYtNeg2kdaya4XViqLIc=&xsec_source=pc_search&source=unknown)
  - 之前有人问过小型一点的MATX机箱推荐，最近刚好可以参考这台新上市的联力A3。
  - 它是联力和DAN Case联手设计的。
  - MATX结构，如果用ITX的话电源可以下置，虽然空间达到了26L多，但是毕竟它是MATX，在配件支持上也能够更加自由一些，风冷支持最高165mm，基本上市面常规风冷都能支持，水冷也能够支持到360mm的一体水冷。显卡支持则达到了比较夸张的415mm，并且支持竖装。整体模块化设计，装机难度不高。

- ## [你们的小机箱加不加散热风扇啊？感觉好闷，好烫 ](https://www.xiaohongshu.com/explore/68499022000000000f033b1b?xsec_token=ABEAH8XqEXMtphXMAXSQfa7ARcpcy6sEhThq_QezV-_NI=&xsec_source=pc_search&source=unknown)
- 看你功耗 整机150w以内随便加不加 超过建议加两把风道有进有出即可，我这日常用大概350w左右整机功耗用了4把 ，其实三把也够了。还有就如果不是很厚实的箱子，风扇越多越容易低频共振。

- 现在的电源好像都是500瓦及以上的，用不了那么多，想买小一点的都没有
  - 没必要买太小，现在650w以下都是白菜价200块钱不到这个钱就别省了。多点冗余的话不光是带设备不吃力，发热小了风扇转速低一点还更安静。

- 看了你的机箱布局，还是可以多加几把的，机箱尾部，顶部，以及显卡下加薄扇，肯定对散热有提升
  - 那基本就加满了，现在先加一个在机箱后面，试试温度
- 不想加多的话顶部正对着风冷最好也加一个

- 正常使用35度的GPU，40度的CPU

- ## [小机箱散热有问题吗？ - 小红书](https://www.xiaohongshu.com/explore/66cbb2f2000000001f016917?xsec_token=AB-BTjol0N_mwqMM3wA24XS93uB6WGXYwkAz6dvKjlB30=&xsec_source=pc_search&source=unknown)
- 不要看它小，这里有三个风扇把热量散出去，其实跟普通机箱没差的
- 不会，其实三面开网风道反而会更好。

- 小机箱，4个风扇够用了

- 我这纯闷罐都没问题
- 怕散热不行就打开侧盖呗

- 便携机箱就是因为要来回飞带着方便，水冷不能上飞机，便携还有什么意义

- 散热没问题的，我也是紧凑matx，公版3080满载也就70多度，贯穿风道

- 我7700+7900xt都随便压

- 本身atx电源前置就是不得不向空间靠拢，而舍弃了进风于妥协的一步，散热不好是先天缺陷。不过为了不影响进风，可以选择显卡cpu双240冷排，并将尾部的风扇作为进风使用，或者不追求侧透的话，直接开孔是最简单的

- 这么大已经不叫小机箱了 10-15升的大小我都嫌大

- ## [小机箱装机血泪教训——乔思伯d41 - 小红书](https://www.xiaohongshu.com/explore/67cd3148000000000e007149?xsec_token=ABQ2_O_qG8QQbUy7d9Jl_OsA4fk-MLl7s4Y__ZMDEuIUM=&xsec_source=pc_search&source=unknown)
- 提示：硬件茶谈的装机教程是个很好的小白教程，装机细节完全可以参考，但是小机箱装机顺序不能完全参照他的来！不然你就会跟我一样，拆了装装了拆装了拆拆了装
- 小机箱装机第一步：带上手套
- 小机箱装机第二步：拆开机箱，取出电源盒，准备一个小盒子（必备！！！）放机箱上拆下来的零散件：螺丝、挡板等等。
- 小机箱装机第三步：千万不要脑子一热就去装散热器！先给我拿出主板，装上cpu和ssd（NVMe），内存条这会可装可不装，
  - 然后把主板装到机箱里面，力道要恰到好处，既不要太重也不要太轻。
- 小机箱装机第四步：千万不要脑子一热就去装散热器！先给我把机箱连接线插到主板上！！！
  - 如果有显卡并且打算装ssd（sata）和机械硬盘的，请千万先给我把sata线也先插到主板上！
  - 重要补充：cpu电源一定要插好！不然后面你要么拆风扇要么在风扇和主板的夹缝中挣扎！
- 小机箱装机第五步：这会你可以装散热器了，只要记住：垂直风扇都朝下，水平风扇都朝前！
  - 先插风扇线，再固定散热器！
  - 如果用水冷散热器，现在水冷风扇一般已经固定在水冷上了，水冷和风扇应该分别插在pump_fan和cpu_fan上（
- 小机箱装机第六步：全模组电源，什么锅配什么盖，什么色插什么色的线，插好先把电源装进电源盒，把机箱电源线插入电源（别忘了打开电源开关！！！），再把电源盒固定到机箱上。
  - 有显卡先装显卡，没显卡直接插线理线。
- 小机箱装机即将完成：要装ssd（sata）和机械硬盘的，这会就可以把他们到固定位置或者硬盘架上，插上sata线和电源线。
  - 别忘了，之前要是没插内存条的要插上内存条，按照 2 → 4 → 1 → 3 顺序插满，确保双通道生效。
