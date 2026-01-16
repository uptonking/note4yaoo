---
title: tool-iot-devices-gpu-cn
tags: [ascend, gpu, iot, moorethreads]
created: 2026-01-15T15:33:38.278Z
modified: 2026-01-15T15:37:59.667Z
---

# tool-iot-devices-gpu-cn

# guide

- 华为昇腾
  - 不要考虑香橙派orange-pi-ai-studio, 主板定制、驱动定制
  - [昇腾兼容性认证硬件目录-昇腾社区](https://www.hiascend.com/ecosystem/ascendpartner/qualified-servers-catalog)

- cann
  - 需要检查是否支持了最新模型
# discuss-stars
- ## 

- ## 

- ## 

- ## [利润这么大，为什么华为不研发生产游戏显卡？ - 知乎](https://www.zhihu.com/question/1913887436712424481)
- 大个锤子，看看黄皮子卖计算卡挣多少钱，游戏显卡才挣几个钱，华为为了产昇腾计算卡恨不得把麒麟给停掉，一个[阿特拉斯集群] 什么价，一块910什么价，要不是华子消费者业务被这么多人看着还涉及战略规划，我估计华子真敢把麒麟踢后边去

- 华为与其把这宝贵的产能用去造游戏显卡，还不如拿去造麒麟装在平板和手机
  - 起码造出来的麒麟装在手机平板上还能用来给鸿蒙next铺路，加深鸿蒙生态的护城河。

- ## 🆚 [砺算科技和摩尔线程的自研架构到底谁是真的？ - 知乎](https://www.zhihu.com/question/1982051710546511191)
- 仅到目前为止，如果是对于图形计算来说，砺算的自主程度更高。
- 目前MTT的主要产品核心硬件微架构IP来自英国老牌GPU厂商imagination的IP授权，MTT S80的GPU部分主要用的就是IMG的[PowerVR BXT架构] ，而musa压根就不是硬件微架构...
  - 而imagination虽然被凯桥资本收购，但是专利技术，研发中心全都被留在海外，中方想往IMG的高层塞人都困难重重，更别说技术的自主化
  - 到摩尔线程S4000为止，核心IP仍然来自IMG，S80和S4000是同代架构，前者我长期跟踪，今年还持续跟进了优化表现。
  - IMG只提供DX9的图形驱动，DX11/12的特性无法原生支持，只能依赖转译、映射，也就是说2015年以后的绝大多数游戏它都没法原生运行，驱动优化一言难尽。
- 但这也不是没有解决办法的，再怎么说现在有了[DXVK] ，DXVK可以实现VULKAN到DX11/10/9的高效率转译，Intel的独显就依靠这个解决了很多问题，性能暂且不谈，至少运行是没问题的。而且到目前，很多新游戏也都原生支持[Vulkan渲染] ，跨平台生态的影响之下Vulkan的影响力很大，更不存在问题了。
  - 摩尔线程在图形方面至今对Vulkan的支持都是缺失的，这真的很奇怪，一个为移动平台而生的PowerVR架构天生就对Vulkan有很好的兼容性，可摩尔线程一直在强兼DX让人实在摸不着头脑，从长期发展来看，支持Vulkan比强兼DX要合理得多得多
  - 从发布到今天，三年过去了，他们当初的决策很可能就是踩了坑——要么纯粹选错方向，要么根本没对技术路线做过真正的评估，只选了一个讨论度最高，最容易带来流量的打法，这也暴露了他们对现有技术和未来路线的迷茫，没准可能压根就没规划过。
  - 在硬件部分，槽点更多，这卡待机功耗110w，待机不会自动降频，而且3年未解决，这种基础功能都完全没做的离谱的状态怎么看也不像摩尔线程有能力独立解决硬件问题，叽里咕噜折腾三年还不知道要干些什么。
- 砺算最大的问题是他出货效率比较低，你有本事你拿货来卖啊？
  - 虽然砺算也不是从0开始，他们的团队是来自原[S3 Graphics] ，但他们自己把持技术路径和核心IP，对于GPU有很多的技术积累，也拿出来过一些产品。砺算很清楚的知道自己的定位，第一款产品就是自主IP，并且原生兼容DX11/12，还知道Windows ARM生态的空缺，极力寻找自己的细分领域赛道，这在自研GPU就是唯一一个独苗了。
  - 只要7G106能开始卖，它大概率会是一款比MTT S80好不止一个次元的产品，自主程度也显然高的多得多。
- 摩尔线程的CEO和联合创始人虽然来自英伟达，但他们都是市场/销售端出来的，他们更懂如何制造声量和营销，活下去才能解决技术问题。
  - 而砺算的高层团队几乎是原来S3的核心人马，不管是CEO还是核心管理层大都是一线工程师出身，问题可能也会出在这里，只能说塞翁失马焉知非福了。

- 意思是砺算是真有技术，但是不懂得如何营销。摩尔是真拿到钱了，但是不知道该如何搞技术？
  - 摩尔搞到钱了不知道怎么搞技术，只能买理财了
- 砺算出货慢大概率是因为没钱
- 摩尔把理算收购就完美了，让理算的专心研发，摩尔的搞销售。

- dxvk对dx12支持不好，而且只能用户拿来替换系统库。摩尔线程自己可不能直接用dxvk，必须自己写dx驱动。至少景嘉微和砺算都是自己实现，我面试套出来的
  - dxvk是dx8-dx11，wine上面支持dx12的库叫vkd3d，dxvk是完全不支持dx12的

- S3当年性能也不太好，不过还能在主流低端上混混。。。。s80就难顶了，只能在超旧款低端勉强度日了，出的时候就跟750ti打，当时主流都是30系列了吧，不仅摸不到最低端的3050，连多年前的950都摸不到。。。到现在还是只能打上古时期的750ti。。。顺便待机功耗比GTX950满载还高。。。

- 砺算缺2亿流片幸得东芯相助不至于解散

- 摩尔这家目前看是纯粹的资本运作公司，买img的ip赶工出一张“图形显卡”目前来看是纯为了曝光量和炒热度，炒起来之后“显卡”这事基本也就不提了，现在看这招玩的也很成功，拉了很多投资人下注进去，投资人下注以后为了不打水漂不管有没有实际技术水平也只能跟着一起抱团炒，最后成功炒出一个市盈率没眼看的“摩王”股，股票炒的离谱，一看产品基本属于是没一个有点实用性的，都是用来挂名放在ppt上宣称我们“有”某某产品用来炒做的，这点来看真不如一些没什么名气做低端芯片的小厂，成立几年现在还能活着的基本都还能有两个爆款产品真的在卖。

- 在芯片这个领域，技术含量最高的就是IP核心设计。我们打开一张芯片的die shot来看，决定每个模块的具体晶体管怎么安排的就是IP核心设计
  - 其中典型的像华为的麒麟芯片或者砺算的这颗GPU, 它的ip核心都是自己设计的。
  - 另外一类典型的就是小米的玄界O1和摩尔线程的S80，都是主要采用外部采购ARM/imgtec所提供的IP核心设计做出的硬件实现。
- 在摩尔线程拿出自研的IP之前，砺算科技的硬件实现是自研的，摩尔线程的硬件实现则是主要依靠imgtec的。不过摩尔线程可以学习苹果，早期苹果也是采购imgtec的GPU架构，后来转自研了。
# discuss-news
- ## 

- ## 

- ## 
# discuss-moorethreads
- ## 

- ## 

- ## 

- ## [摩尔线程新架构游戏显卡, 比S80提升15倍? _202512](https://linux.do/t/topic/1346213)
  - 原话是比S80 3A游戏性能提升15倍, 意思应该是本来10帧的游戏, 现在能跑150帧吧.

- 今年效益增加就是因为推理卡，s5000，虽然我严重怀疑这里面，包括寒武纪，政府、银行订单居多，企业少

- 摩尔家终于想起自己家消费级产品三年没迭代啦？

- 当时那个显卡好像是 2999 元，算很贵了
  - 清仓的时候卖过1199…官方价格
- 显卡挣不挣钱不知道，反正股票是真挣钱了！

- 武汉弘芯知道吧？让国家损失了 1000 亿。 其实上面也是草台班子，并没有你想的那么厉害。

- ## [重磅发现：国产显卡也能跑Ollama了 _202412](https://linux.do/t/topic/318016)
  - 不过玩Ollama得提前安装MTT S80/S3000/S4000最新驱动和MT Container Toolkit 

- 摩尔线程，国产显卡，堆的料能有3060水平，但是驱动差太多了，实际玩游戏啥的只有1060水平。不过非游戏场景应该是能发挥出来他堆料的作用的

- 现在英特尔的卡也便宜是不是买个那个跑也行

- Ollama用cpu都能跑啊，主要是效率不同
- 主要是上游 llama.cpp支持了摩尔线程的GPU加速，很厉害。
- 另外llama.cpp也支持华为的NPU，不过个人用户应该搞不太到

- 去年国庆我入手的时候就是1650的水平了, s80最神秘的地方是走的cpu供电
# discuss-ascend
- ## 

- ## 

- ## 

- ## 

- ## [请教这个硬件配置可以兼容昇腾Atlas 300I Duo 96G显卡么  _202502](https://www.hiascend.com/forum/thread-0292175922617889142-1-1.html)
- 个人台式服务器不建议使用此标卡，因为他的散热不能满足，同时供电可能不够稳定，您可以参考300I duo此链接查看散热规格

- 涉及两个点需要重点考虑：
  - 1、要有独立的供电能力
  - 2、卡是被动散热，需要考虑散热是否满足

- 这个我可以帮忙解答一下。
  - 理论上你这个配置是可以跑起来的，我没有baidu你的电源型号，但是电源建议用模块化的电源，cpu多路供电最好。
  - 1、300i duo的供电不是普通的显卡供电，你需要自己做一根供电的转接线，duo的电源接口定义你可以在使用说明里找到，建议使用cpu8路供电进行改造；
  - 2、卡是被动散热，你需要taobao一个显卡散热器，侧面吹风的那种。

- ## [关于家用PC机使用Atlas 300I duo无法开机的问题 _202504](https://www.hiascend.com/forum/thread-0255181734244120049-1-1.html)
  - 我手上有一块Atlas 300I duo 96G显卡，刚好还富裕一台PC机想着是不是可以利用起来，但是安装好之后无法开机，我更换成其他显卡是可以正常开机的
  - 我的主板是精粤b760i snow dream，CPU为Intel I5 12490F, 内存DDR4 3200 32Gx2 ，一块亮机卡RTX4060
  - 👷: 是线的问题，更换成CPU的电源线就可以了

- duo卡需要外接电源，家用PC供电可能不够稳定，其次还有散热问题，不建议使用个人电脑

- [安装驱动时Do you want to try build driver after input kernel absolute path?  ](https://www.hiascend.com/forum/thread-0272154087318885058-1-1.html)
  - 设备的配置为 飞腾2000+主板 搭配创见32G的内存测试
  - 您好，Atlas200DK硬件已经EOS，当前Atlas200DK板块已与Atlas 200I DK A2合并，后续若遇到相关问题请您整理最新信息在Atlas 200I DK A2板块发起新帖

- [在Ubuntu20.04系统上，用自编译内核安装300V pro驱动 ](https://www.hiascend.com/forum/thread-0259193387493453967-1-1.html)
  - 硬件为D2000主板，加速卡为atlas 300v pro

- ## [关于Atlas 300 的疑问 _201911](https://bbs.huaweicloud.com/forum/thread-29229-1-1.html)
- Atlas 300是否支持 Intel和AMD的主板，是否系统换成乌班图的就能查到一般家用台式机用于推理呢？
  - Atlas 300可以用在X86的主板上，有2个前提，1是操作系统要求是Ubuntu或CentOS，2，台式机的散热能力要满足规格要求。
  - 尤其第二点，由于Atlas 300是被动散热的卡，需要系统提供一定规格的风量，一般台式机需要改造散热系统才能满足。
- 算力部分，可以参考昇腾310的介绍。Atlas 300是由4颗昇腾310组成的。

- MindStudio 是否支持鲲鹏台式机，还是说只能配和昇腾芯片使用？
  - 鲲鹏+昇腾的方案，要求满足第一条，操作系统和散热。鲲鹏台式机散热是有风险的，同x86台式机。

- ## [英伟达L20 48g和华为昇腾300I DUO 96g计算卡 性能对比测试 ](https://www.xiaohongshu.com/explore/6880f03f000000000d01b329?xsec_token=ABge3b_SaA9VIBmz7VuwF34db01XOS5eSaGWyh61vEMvg=&xsec_source=pc_search&source=unknown)
- 300I DUO在国产化场景中具有优势，支持256路1080P视频实时解析，能效比更高，且与国产框架深度适配。
- 测试大模型为Qwen2.5-32B-Instruct版本，分别准备了2U机架式服务器和4U高度的浪潮元脑 NF5468M6机架式服务器。
  - L20单并发推理性能 34 tokens/s，并发数500时吞吐量2540.71tokens/s。
  - 华为Atlas 300I DUO单并发推理性能 13.43 tokens/s，并发数500时吞吐量686.13 tokens/s
- L20与 300I DUO性能差距2.6倍，价格差距2.6倍，能效比L20更高，300I DUO支持国产化场景，具有优势。

- ## [华为昇腾300I Duo 部署 Qwen3-32B 模型，能跑多快？](https://www.xiaohongshu.com/explore/69533a18000000001e0245e6?xsec_token=ABZtHALwoOCtJw60tf4YbykT0MsOkKIN2PPsTchhuDDzo=&xsec_source=pc_search&source=unknown)
  - 推理卡：4×华为Atlas 300I DUO  48G
  - 推理引擎：MINDIE2.2
  - TPS  361.8836 token/s, 含了并发的 TPS
  - TTFT  1265.511 ms
  - TPOT 114.1151 ms

- 为什么我最多20多tokens每秒

- mindIE好像挺难用的, 为什么不用vllmascend
  - 因为没有atb

- ## [Orange Pi AI Studio Pro mini PC with 408GB/s bandwidth : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1im141p/orange_pi_ai_studio_pro_mini_pc_with_408gbs/)
  - [OrangePi AI Studio Pro](http://www.orangepi.cn/html/hardWare/computerAndMicrocontrollers/parameter/Orange-Pi-AI-Studio-Pro.html)
- As always, hardware is only one part. Where's the software support? Is there a Linux kernel driver? Is it supported in any good inference engine? Will it keep working 6 months after launch? Orange Pi are traditionally really really bad at the software side of their devices.
  - For all their fruit clone boards they release one distro once and never update it ever again. The device tree or GPU drivers were proprietary so you can't just compile your own either.

- Rumored to have an Atlas 300I Duo inference card inside, but with double memory and a better price. Now the 192GB version is pre-ordering at ¥15, 698 (~USD $2150).
  - 12-channel 64-bit 4266 MHz LPDDR4X = 409.5 GB/s
  - Atlas 300I Duo specs: 408 GB/s
- So it’ll be about 10-15% slower than M4 Max and about 80-90% faster than M4 Pro. If that’s really true than 2100$ is an amazing price point provided we also get the needed software support.

- ### [AI Studio Pro mini PC from Orange Pi pairs dual Huawei Ascend 310 processors with up to 192GB of RAM : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1o3k9zr/ai_studio_pro_mini_pc_from_orange_pi_pairs_dual/)
- It is not a PC, it is a external multi GPU connected via USB-C 4.0 40gbit

- AMD sells a 128GB device with half the bandwidth and 1/4 the AI TOPS for the same price.... clearly you did your research
  - The price is pretty fair for the compute/bandwidth you get... Btw. its not a computer, it is a external NPU accelerator connected via USB-C 4.0 40gbit. Meaning you can use all of the 192GB memory, not like in the AMD system where 32 are reserved for the system...

- 192gb M2 Ultra is better than this and similar priced…

- funny part of spec is that power supply is 12V 20A for pro version, i'm curious how the plug looks like, since it's 5.5/2.5mm DC jack

- ## [本地dsr1 671b8位 性价比最高的方案是华为300i duo吗？ _202502](https://www.chiphell.com/thread-2670953-1-1.html)
- 我现在就是用 32 张昇腾 910B2 本地部署的 DeepSeek R1 671B 模型，只是推理部署没有这么麻烦，MindIE 框架照着教程挺快就完事了。昇腾和其他厂的卡在推理方面从来都不是很麻烦，麻烦的是训练里面有些算子不兼容。
- 没有这么麻烦，华为的 MindIE 框架基本上就是一条龙服务，照着教程就是起个 Docker，里面都是推理各种模型的脚本，也是可以一键向外提供 API 服务的
- 300i duo 是昇腾 310B，我看目前 MindIE 框架的文档都是 910B 系列的。可能是因为 310B 的互联带宽有限制，不确定 310B 是否支持。

- 智普的小视觉模型就是 修改的llama 运行时，没有迁入到官方库。 这种模型，你要适配就麻烦的要命。。

- MindIE更新的还是挺快的，更不用说还是国产模型了，工程师跟进非常积极

- 香橙派OrangePi AIStudio Pro 看了以下说明书，这东西就是一个外置显卡啊， 用雷电PCIE通道外接。。到系统。。 本质就是是300I，不过价格好像要便宜很多
- 300i duo我记得是单卡双芯，这两个芯片可以跑两卡并行，但并不能跟其他卡进行hccl或者rdma互联

- 要说910b还凑合, 300I duo且不提r1, 不如先看看怎么在没有专人技术支持的情况下把常见2bit量化格式的7b dense模型跑起来再说...(甚至都不用提2bit, 这玩意烂大街的4bit和8bit量化都几乎没有支持), 300I全系都是pre llm时代的东西, 设计目标是给114514路监控摄像头CNN模型推理用的, 现在硬往llm上凑根本不可能好用得起来
  - 更何况你为什么会觉得哪怕能跑起来r1, 300I duo能比cpu快, 这玩意几乎没有互联能力

- 优点是 纸面规格确实够高，1.5W价格可以获得 192G NPU计算卡
- 但是由于和第三方合作搞的，所以很多地方压缩很厉害，以下是缺点（仅供参考，目前没看到实物）
  - 1. 显存速度不快， 设备使用LPDDR4X 作为了显存， 实际速率在4266Mbps （宣传截图，但这里没说具体 现存带宽）
  - 2. 只支持 雷电4（USB4） 的PCIE扩展链接， 总带宽只有40Gbps ， 因此加载模型需要先在电脑端加载到内存，然后再传输到NPU中。
  - 3. 软件方面的兼容性有待考证， 从初步资料来看，升腾方案 目前就只支持FP8和FP16运算， 其他规格量化目前支持度不是很好， 也就说要运行模型需要的显存至少约等于模型参数大小， 即 30B模型需要大约30G显存（FP8）或者60G显存（FP16）
  - 4. 硬件扩展性不高， 虽然理论上是雷电4的“外置显卡（npu）设备”， 但是 目前电脑上能提供原生雷电4接口不多，而且大多数都电脑还没有雷电4 接口
  - 5. 内部架构存疑，（猜测） 根据现有Duo 显卡规格来看，是两个 48G NPU 组合一起的， 那么 这个192G怪物 可能就是4个 48G NPU模块组合在一起，至于内部如何协同，通讯带宽多少，都是未知。  但有一点可以肯定是，与电脑连接带宽就只有40Gbps，也就说即便多卡互联成立，多卡之间速度只有40Gbps ，性能影响是巨大的。

- ## [千元32GB显存？全球封禁的华为昇腾变身AI神器 _202505](https://post.smzdm.com/p/amvo0gvv/)
  - 谁能想到，​24GB HBM2显存​​、​​88TOPS INT8算力​​，功耗仅67W的​​华为昇腾Atlas 300I推理卡​​，如今在闲鱼上只要千元出头？
  - Atlas 300I Duo 指标基本是 Atlas 300I Pro 的 两倍，而 Atlas 300I pro 可以看做是 Atlas 300I 的 全方位升级 。
  - Atlas 300I 最便宜，想玩AI的可以捡来试试，但是要注意这个卡的是分型号：3000/3010，意思是区分 CPU处理器 是 ARM 的还是 X86 的，两者不能互通，也就是说 你在华为自家鲲鹏机器上能用的卡，插在英特尔机器上是不能用的。而 Atlas 300I Pro 是能很好的做到兼容 ARM 和 X86。
  - 这个卡不能玩游戏，它是AI推理卡，Linux专属加速硬件，只有linux的驱动，目前大部分是搭配鲲鹏的服务器来使用，未来也有可能适配鸿蒙系统。
  - 也看到有人尝试在普通PC上尝试的，理论上也是可以支持，但是意义不是很大。想玩的话建议捡一套国产处理器和主板搭配来玩。

- 🐛 这个卡被动散热，普通机器拿个风扇对着吹，这个卡都会死机掉卡。
  - 必须要有风道才行。台式机也能用。
  - 服务器被动散热很正常，都是暴力涵道风扇在前面吹，你要放塔式机箱得改散热

- MI50 32GB差不多的价格，ROCm生态，带一个miniDP

- 为了这个一千块的卡，需要配一个月薪数万的软件工程师来使用，或者你本身是也行，普通网友是玩不转的。

- ## [看昇腾新推出的 Atlas300 系列新卡 - 知乎 _202208](https://zhuanlan.zhihu.com/p/547678061)
  - [Atlas 300I Duo 推理卡 用户指南 13 - 华为](https://support.huawei.com/enterprise/zh/doc/EDOC1100245754/c0338d05?idPath=23710424|251366513|22892968|252309139|252823107)
  - [Product Specifications - Atlas 300I Duo Inference Card User Guide 12 - Huawei](https://support.huawei.com/enterprise/en/doc/EDOC1100285916/181ae99a/specifications#EN-US_TOPIC_0000001222892225)
  - [计算产品3D展示](https://info.support.huawei.com/computing/server3D/res/server/atlas300-3010/index.html?lang=cn)

- 推理：(原有 升级) Atlas 300I ==> (up up) Atlas 300I Duo、Atlas 300I Pro；
  - 视频解析：(新增) Atlas 300V Pro；
  - 训练：(原有 升级) Atlas 300T ==> (up up) Atlas 300T Pro; 

- 差不多两年前，昇腾推出了第一代 半高半长 的推理卡 Atlas 300I 以对标 Nvidia T4，从算力上来看 Atlas 300I 会逊色一截 (Atlas 300I 单卡 int8 算力为 88 TOPS，Nvidia T4 单卡 int8 算力为 130 TOPS，但跑实际网络的性能并不一定是这样)
  - 那时的 Atlas 300I 推理卡分型号：3000/3010，意思是区分 CPU处理器 是 ARM 的还是 X86 的，两者不能互通，也就是说 你在华为自家鲲鹏机器上能用的卡，插在英特尔机器上是不能用的。而现在的 Atlas 300I Pro 是能很好的做到兼容 ARM 和 X86 ( 灵活度高了 )。
- Atlas 300I 卡内置 4个 device，芯片为 昇腾310，而 Atlas 300I Pro 直接升级到了 昇腾710，这也导致推理卡算力从原来的 int8 88 TOS -> int8 140 TOS (超越了 Nvidia T4，注: 这其实拿T4来比就不太公平了，现在T4都要停产了)
- 拿 Atlas 300I 和 Atlas 300I Pro 对比会更有意义，因为这两个都是 半高半长卡，而 Atlas 300I Duo 则是 全高全长卡

- 打游戏，建模怎么样
  - 肯定不行。这些卡甚至没有图形驱动。

- [国产系列 | Atlas 300I Pro 推理卡性能、应用场景、技术规格介绍 - 知乎](https://zhuanlan.zhihu.com/p/664551221)

- ## [Huawei 96GB GPU card-Atlas 300I Duo : r/LocalLLM _202508](https://www.reddit.com/r/LocalLLM/comments/1n4f1gs/huawei_96gb_gpu_cardatlas_300i_duo/)
- 96GB Single Slot, 150W, very interesting combination

- Also keep in mind they will specialize in one of the domestic LLM’s like qwen. They will pour all the driver support into it and something like optimizing sglang. It’s the first step into the same playbook intel is doing with arc. But my guess is they will be much better at making it as optimized for just a single family of models and nothing more. Kinda like thinking about how a ps/xbox/switch etc can out perform a consumer grade GPU because they just keep doubling down on optimizing the chipset for a specific workload.

- That’s an NPU card. Here we have basically the same thing with an optional 192 GB. http://www.orangepi.cn/html/hardWare/computerAndMicrocontrollers/parameter/Orange-Pi-AI-Studio-Pro.html

- M4 pro only 273GB/s

- 395 max is like 225gbps bandwidth, so faster but slightly less vram. Would depend on so many other factors... Driver support, how well 2+ interact, price, workload

- The 300I Duo is sitting at 204 GB/s bandwidth per GPU.
  - A z790 mobo running 96GB DDR5 RAM achieves a theoretical bandwidth of 89. GB/s in dual channel mode.
  - That indicates it could be around 2.1x times faster than a modern PC with dual channel DDR5 RAM.

- ## 🧩 Atlas 300I 96g [Finally China entering the GPU market to destroy the unchallenged monopoly abuse. 96 GB VRAM GPUs under 2000 USD, meanwhile NVIDIA sells from 10000+ (RTX 6000 PRO) : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n46ify/finally_china_entering_the_gpu_market_to_destroy/)
  - 👀 偏向推理，而非训练
- Huawei Atlas 300i Duo 96GB
  - 96GB or 48GB LPDDR4X at 408GB/s, supports ECC
  - 280 TOPS INT8, 140 TFLOPS FP16
  - PCIe Gen4.0 ×16 interface
  - Single PCIe slot (!)
  - 150W power TDP
  - Released May 2022, 3 year enterprise service contracts expiring in 2025
  - Linux drivers
  - vLLM support seems slow
  - llama.cpp support seems better
- For reference, the RTX 3090 does 284 TOPS INT8, 71 TFLOPS FP16 (tensor FMA performance) and 936 GB/s memory bandwidth. So about half a 3090 in speed for token generation (comparing memory bandwidth), and slightly faster than a 3090 for prompt processing (which is about 2/3 int8 for ffn, and 1/3 fp16 for attention).

- 1 slot, no fan
  - 4GPU on board
  - Performance 1/10 of 3090
  - 88 TOPS INT8 and 44 TFLOPS FP16
- that's the slow one. this one is LPDDR4X 96GB或48GB，总带宽408GB/s

- Pytorch and llama.cpp support it (Ascend NPU).

- 2 GPUs with 204 GB/s memory bandwidth each. Pretty terrible, and even Strix Halo is better, but it's a start.
- This is a dual-CPU card - 2x 16-core CPUs with 48GB dog-slow LPDDR4X @ 204 GB/s, and some AI acceleration hardware. $2000 is still super overpriced for this.
  - The RTX Pro 6000 is also 4x the price...
- It's a dual NPU solution. Which already limits it for running large LLMs. And it has lass bandwith than Strix Halo for each NPU. It's also more expensive than Strix Halo, and it doesn't have anything close to ROCm. Plus Strix Halo is a whole APU with 16 Zen5 cores.
- Internally, it has two 48GB NPUs connecting through PCIe, so say goodbye to memory bandwidth cross chip.

- Actually, this card came out about three years ago. It’s essentially two chips on a single board, and they work together in a way that’s more efficient than Intel’s dual-chip approach. To use it properly, you need a specialized PCIe 5.0 motherboard that can split the port into two x8 lanes.
  - In terms of performance, it’s not necessarily faster than running inference on CPUs with AVX2, and it would almost certainly lose against CPUs with AVX512. Its main advantage is price, since it’s cheaper than many alternatives, but that comes with tradeoffs.
  - 👀 You can’t just load up a model like with Ollama and expect it to work. Models have to be specially prepared and rewritten using Huawei’s own tools before they’ll run. The problem is, after that kind of transformation, there’s no guarantee the model will behave exactly the same as the original.
  - If it could run CUDA then that would have been a totally different story btw..

- Might as well just get a refurb Mac for $2000-3000 with 128GB RAM.
- Everyone comparing this to the Strix misses the point of this card entirely, the two important things are:
  - This form factor scales for large scale inferencing for full fat frontier models.
  - Huawei have entered the GPU market which will drive competition and GPU prices down.
- it isn't a gpu. it's purely neural processing
  - no video encoder/decoder and no vulkan or opengl :/

- 🆚 Atlas 300i vs AMD 395+ AI Max
  - 408 GB BW vs 256 GB BW (60% better TPS theoretical)
  - 140 TFlops fp16 vs 59 TFlops fp16 (240% faster PPS theoretically, though this is very software dependent)
  - 96GB LPDDR4X vs 128GB LPDDRX5 (96 VRAM max allocation)
  - Both are supported by llama.cpp, AMD by Vulkan too, unsure if atlas works on vulkan atm.
- I'd also compare to the Jetson Thor Nvidia just announced. Which is $3500 but I think the extra cost is probably worth it. At least relative to this or the Ryzen Max AI.

- better bandwidth, that's about it. strix halo has decent support and you can run just about whatever you want, including comfyui

- CANN has llama.cpp support.
  - So does Intel SYCL but is still not nearly as optimized as CUDA, with for example graph optimizations being broken and Vulkan runs better than native SYCL. Support alone doesn’t matter.

- Today, llama.cpp (and some others) works well enough with Vulkan that if anyone can ship hardware that supports Vulkan with good price and availability in the > 64GB VRAM segment CUDA will stop mattering within a year or so.

- Yeah, the problem is that they are using lpddr4x memory on these models, your bandwitch will be extremely low, it's more comparable to a mac studio than a Nvidia card. Great buy for large Moe with under 3b active parameters though
  - Its fine for image gen I'm sure, just not as fast. you should only consider a card for the vram to the degree you will be running large models/workflows. for the price point, imo the new strix halo boards are a better deal, but aren't a pcie card obviously. after that maybe two b60s once they're out.

- Anyone have inference benchmarks?
  - The 300I is not new. you can find it

- only 400 GB/s bandwidth? That seems low for a discrete GPU? 
  - It's certainly slower than an m3 ultra (I think that's around 800 GB/s). I think an M4 Max (what I use) is around 400-500 GB/s but I don't recall.

- Deepseek already publicly declared that these cards aren't good enough for them. The Atlas uses 4 Ascend processors, which Deepseek says are useless.
  - They still use them for inference which is what most people here would use them for as well and a new report just came out stating they use them for training smaller models

- Doesn't have Tensor cores....
  - Pretty sure it's all tensor cores, it doesn't have shaders. Tensor core is just a branding for matrix multiplication units and these processors are NPUs which usually have nothing but matrix multiplication units (or tensor cores).

- That is not a GPU but a npu card.

- The entire software ecosystem is missing. Not a hardware problem. Glad to see it but takes years to build the software ecosystem

- Don’t you know the orange pi ai studio pro? The problem is they are using lpddr4x.

- big ram is usefull for local AI, but the performance.... i think id wait for next gen with even more ram on lpddr5x and at least quadruple the TOPS, a noble first attempt

- As someone who’s had to force engineers to access their Huawei servers headless because there were NO Linux video drivers for them, I find this hilarious.

- These Huawei Atlas 300i Duo cards aren’t new tho. They’re 2022 datacenter pulls with 96GB LPDDR4x and low bandwidth. They’re fine for cheap inference where memory matters more than speed, but nowhere near a 4090 for performance or training. The bigger problem is software... CUDA dominates, while Huawei’s stack is still rough with driver issues and limited support. 

- They only need to pull request Pytorch to natively support the GPUs. Thats it. They can do it with software team. Moroever, a CUDA wrapper like ZLUDA and you are ready to roll. Currently VRAM or GPU can be weak but this is just the beginning. Still i would buy GDDR4 96 GB RTX 5090 over 32 GB RTX 5090 which they sell right now

- Huawei needs to sponsor the Zluda project for their cards. https://github.com/vosen/ZLUDA

- ## [如何评价华为 910D 昇腾芯片？ - 知乎 _202505](https://www.zhihu.com/question/1901443872082601331)
- 重点是对FP8 HIFLOAT8的支持。
  - 在910D之前，国内主流的计算卡都是fp16，部分例如摩尔线程实现了软件fp8+硬件fp16。
  - fp8比fp16有两个优点：快和省内存。
  - 现在昇腾910D支持fp8/hifp8，也有可能支持fp4/hifp4——这意味着昇腾910D很有可能是第一个可以原生fp8训练deepseek模型的国产卡。

- 昇腾910D的FP16算力达到800 TFLOPS和H100的989 TFLOPS差距缩小到20%以内。
  - 在TF32精度下算力（512 TFLOPS）首次反超H100（495 TFLOPS）。

- 2024年华为昇腾910B/C两款计算芯片销售额超200亿，也没啥热度。

- ## [京东已经上架了华为昇腾显卡，为什么网上一点讨论的声音都没有？ - 知乎](https://www.zhihu.com/question/656417645)
- 你把兼容性和性能做好了用户自然会买账。

- 倒是拿来评测一下啊，怎么找不到一个评测视频
  - 这玩意一套下来最基础的都要190万, 而且不包含后续服务费, 你告诉我谁特么钱多到去评测这个

- ## [Ascend选手 _202601](https://linux.do/t/topic/1448162)
  - 有没有在CANN昇腾生态上面玩的？我一直都是国产芯片的选手，感觉cann生态实在是差劲，开发起来很痛苦

- 这显卡真的折磨，平心而论，真国产算力，我用过平头哥的，兼容性好不知道多少倍了。。。
  - 用过沐曦曦云C500，也更好使，最起码 VLLM能跑起 HY-MT1.5-7B

- 是用的vllm-ascend，但是对新手也不友好，很多模型不支持，也许老手能调出来，但是对我这样有一点点基础都困难，对新手来说肯定是抓瞎的。

- 用了gpustack还算方便，就是好多模型不支持，mindie 多卡要比vllm好一些

- mindie 接口不完全兼容openai协议，用起来也挺痛苦的

- 就是跑起来还行，但是要在上面搞出好东西比较难受，比如提升训练的mfu之类的

- ## [国产显卡包括但不限于昇腾可以用来训练大模型吗？ _202501](https://linux.do/t/topic/375234)
- 昇腾有的 我们公司有采购910B，他们的售前和技术都有支持，建议看 mind 系列文档
- 看看华子有没有适配？最好使用他的框架和适配的框架
- 昇腾这套是自家的 NPU。。 他官方没做适配的话是用不了的 所以如果要采购的话可以问问售前和他们的技术

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 砺算科技发布了7G100 [国产显卡宣布春节前上市，宣称性能「硬刚」RTX4060 并配备 12GB 显存，其竞争力几何？ - 知乎](https://www.zhihu.com/question/1990339821793740257)
  - 2025年7月份砺算科技发布了7G100系列GPU，跑分性能堪比RTX 4060，引发轰动。
  - 之前表态是9月份上市，但实际上没有，消息称消费级的7G106显卡会在26年1月到2月上市
  - 7G100系列GPU采用6nm工艺，消费级型号配备 12GB GDDR6 显存，面向工作站的专业版

- 早期的国产GPU多是购买 Imagination等公司的IP进行套壳。但现在的砺算、摩尔线程等企业已经是属于真正的自研指令集与架构。
  - 砺算的[TrueGPU天图架构] 是真自研，能持续迭代。7G100系列已经可以真实运行[黑神话悟空] 或赛博朋克 2077这类3A大作，在跑分来看，理论上能基本能对标[RTX 4060] 。能把这些复杂的图形 API 吃透，说明国内团队对图形底层协议的层次已经达到了世界二流，甚至局部一流的水平。
  - 砺算这次交付的的7G100只是企业级的，主要流向了数字孪生、智能座舱和云游戏等 B 端领域消费级7G106春节前能不能上市，我们拭目以待。
  - 从跑分来看，7G100的纸面实力确实非常接近 RTX 4060。但是显卡性能的50%取决于驱动优化。英伟达与全球数万家游戏工作室已经深度合作几十年了。国产显卡可能在A款游戏跑分惊人，但到了B款游戏里可能就会出现闪退、贴图错误。这种稳定性和兼容性的积累，不是一两年能补齐的。在实际使用中，要做好性能差距10%-15%的准备。
  - 消费级7G106确实配备了12GB [GDDR6] 显存，但这仅仅是目前 1080P/2K游戏的基本配置。不过显存目前并不是技术门槛。砺算科技的7G105/7G100 已经配置了 24GB GDDR6/[GDDR6X] 。摩尔线程两年前的MTT S80就标配了16G，后续的 S90也有了32G版本。
  - 估计到2026年下半年，应该会看到16G版本的 7G106或加强版7G108成为主流。

- ## [为什么中国一直造不出4090显卡，显卡研发有多难？ - 知乎](https://www.zhihu.com/question/614979051)
- 显卡倒也不算太难，国产里摩尔线程和景嘉微都有能用的卡，死命堆堆规模性能也不是提不上去。虽然人景嘉微的卡跟消费级没关系。
  - 摩尔线程的MTT S80，靠着规格在适配过的软件上(剪映)转h265格式的视频的时候甚至可以小赢4060。(不过转av1的时候完全没有在动)，也可以通过厂家提供的MUSIFY借用CUDA生态，跑跑诸如stable diffusion之类的东西。还能正常运行maya，3dmax，cad之类的生产力软件。
  - 但为什么MTT S80仍只是将就能用的水平？ 因为驱动，MTT S80只支持DX11不支持DX12和vulkan，效率也很低。(能赢1060就算成功) ，在PR里甚至无法调用gpu加速。
  - 不过也别太悲观。毕竟除了皮衣黄和苏妈，哪家pc显卡的驱动都很答辩(甚至苏妈也挺答辩的)，不信咱们就看看牙膏厂，作为有着多年核显驱动经验，在PC上显卡占有率最高的厂商。他们的ARC770首发时仍然只能用接近3060两倍的规模去实现和3060四六开的性能(dx12和高分小赢，dx11直接输麻了)

- ## [如何看待国产消费级显卡的游戏性能被卡在GTX750ti-GTX1060级别? - 知乎](https://www.zhihu.com/question/1984237429566219284)
- 可能没关注到最近半年国产 GPU 的关键突破——尤其是砺算科技（Lisuan Tech）即将上市的 7G100 系列显卡。
  - 先说结论：7G100 的实测游戏性能已经全面超越 GTX 1060，甚至对标 RTX 4060，完全跳出了你提到的GTX750ti-GTX1060性能区间。
  - 全自研 TrueGPU 天图架构：从指令集到渲染管线全部自主设计，不再依赖公版方案；
  - 支持 NRSS 动态超分技术（对标 DLSS/FSR），帧率提升显著（如从 62 → 78 FPS）；
  - FP32 算力达 24 TFLOPS，远超 GTX 1060（约 4.4 TFLOPS），甚至超过 RTX 4060（15.11 TFLOPS）。

- 摩尔线程 MTT S80 虽然硬件规格亮眼（16GB GDDR6、14.4 TFLOPS FP32），号称对标3060，但由于早期IP是购自IMG迭代困难，导致大量现代 3A 游戏无法正常运行或优化极差。
  - 它的定位更偏向轻度游戏+生产力场景，游戏性能确实还卡在 GTX 1060 上下水平。

- 消费级显卡是需要时间慢慢堆驱动修bug出来的，牢英搞个i卡驱动做了多长时间团队加班是常态，到现在i卡还是有些小问题和老游戏DX9兼容之类的也差。
  - 包括A卡最新驱动FSR红石说是支持一堆游戏，结果打开根本没有开启选项。
  - 有优势的就是老黄家，毕竟有资源投可以让团队直接入驻游戏公司现场调，其他家都没这个资源。

- 英特尔核显市场占有率世界第一，写驱动历史悠久且经验丰富，即便如此，英特尔的独显A770大多数游戏里也只能做到拿着3060Ti的跑分跑出3060的游戏性能。由此可见显卡驱动想优化到N/A的程度有多困难！

- ## [如何看待中国显卡的性能被卡在RTX3060级别? - 知乎](https://www.zhihu.com/question/1915898789887207311)
- 现实是:5060的价格，3060的能耗，1050的规格。最后测出来750ti的性能。

- 摩尔线程自己心里也清楚自家成品到底几斤几两。在22年底，它家的显卡是不公开售卖的，甚至需要必购码才能买到。并且买显卡要搭一张华硕主板。
  - 经过一年时间的开发，s80、s70都有了实用性，摩尔线程就开始正常售卖了。并且在双十一、六一八等大促期间把显卡价格降到1299、899进行售卖。
  - 首先是奇葩的CPU供电。正常的显卡都是用PCIe供电，不知道摩尔线程出于什么考虑，居然选择CPU供电。总之，因为我的主板已经用了2根CPU供电线，没有多余的CPU供电线，所以只得使用附带的转接线。
  - 装好以后开机，能看到BIOS界面，但进系统就黑屏。
  - 驱动拖了硬件的大腿是不争的事实。
  - 单纯看跑分的话，s80确实有gtx1060的水平。
- 目前国产游戏显卡表现最好的摩尔线程s80，它的实际游戏性能大约在gtx1050-gtx960之间。
  - 作为一张三年前的老卡，s80与它同期的a770、3060、6650xt相比差距明显。
  - 很可惜的是，三年过去，它依旧后继无人，也难有后人。游戏显卡已经是夕阳产业，就连AMD都对其意兴阑珊。

- AV1、HEVC这俩，4K60帧，解得明白的有几家。

- 
- 
