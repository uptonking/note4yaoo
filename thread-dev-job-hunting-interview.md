---
title: thread-dev-job-hunting-interview
tags: [interview, job-hunting, thread]
created: 2023-04-25T17:57:04.669Z
modified: 2024-01-07T15:00:50.079Z
---

# thread-dev-job-hunting-interview

# guide

# discuss-stars
- ## 

- ## 

- ## 今年的冬天确实冷。感觉很多互联网公司都只招架构师级别的了_202312
- https://twitter.com/YuTengjing/status/1739176978899755047
  - （怀疑也是为了骗方案或者营造招人的假象），都收紧裤腰带过日子，想去混个大头兵都感觉没啥面试机会
- 虽然只是参加了两场面试，但是感觉社招的时候业务匹配度和项目经历太重要了，反倒还没问什么八股。但是小厂出身+业务比较偏感觉项目就很难出彩啊，难顶。虽然我感觉进去也是🔧，但是他们确实是要求有造过🚀的经验。

- 📝 貌似我了解过的大厂的前端招聘有个业务都缺人：在线文档
- 为什么都要做自己的在线文档呢
  - 搞在线文档的一般都是先搞了自己的 IM，可能是不想泄露数据? 更方便和自己的  IM 打通?

- 最近在知乎经常看到类似 node 凉了的帖子，但是之前面 wxg 的时候好像视频直播带货那边 node 服务端用的挺多的。国内太多博客喜欢搞标题党了，deno 出来的时候说 node 💊，bun 出来的时候说 node 💊，tauri 出来的时候说 electron  💊，oxlint 正式发布的时候说 ESLint 💊
# discuss-boss/hr
- ## 

- ## 

- ## 
# discuss-algorithm
- ## 

- ## 

- ## If you want to become good at solving recursion problems, learn these 6 templates:
- https://twitter.com/Franc0Fernand0/status/1743912605909918083
- 1. Iteration
- 2. Subproblems
- 3. Selection 
- 4. Ordering
- 5. Divide & Conquer
- 6. Depth First Search

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 面经不写了，写个thread写点我遇到的不会的题目吧
- https://twitter.com/wulianwen1/status/1726793525956862125

- 同时发起1w个请求，http1.0/1.1/2.0分别需要建立多少个tcp连接（抖音电商二面）
  - http1.0 应该是1w个，因为连接会立即断开
  - http1.1 应该是浏览器支持的并发数量，因为是长连接
  - http2.0 应该是1个，多路复用支持在一个连接上并发多个请求

- React和Vue更新视图的区别？为什么React上粗粒度更新，Vue是细粒度更新？
  - 简单来说, React是比较渲染树新旧DOM的差异, 并且可能会重新渲染整个组件树，而Vue是精确的更新受影响的部份。

- chatgpt等平台为什么使用SSE的方式进行流式打字？
  - [ChatGPT对话为什么不用Websocket而使用EventSource？ - 掘金](https://juejin.cn/post/7246955055109210149)
  - 在ChatGPT官网我们可以看到，对话的方式仅仅只有一个post请求，而没有使用IM中使用的websocket链接。
  - 与普通的post请求不一样的是，返回信息Response没有了，取而代之的是EventStream。
  - EventSource 接口是 web 内容与服务器发送事件 一个 EventSource 实例会对HTTP服务器开启一个持久化的连接，以 text/event-stream 格式发送事件
  - EventSource只支持从服务器到客户端的单向通信，客户端无法向服务器发送数据。

- react为什么要推出fiber架构?  
  - react15只能同步地更新 相当于while(true) 很卡 
  - fiber是一种协程的实现，可以中断让出js线程

- ## 站酷上看到的UI作品集，大部分都只能用“人云亦云”来形容，
- https://twitter.com/cosmoslee007/status/1650542502943031296
  - 这么多年了，明知道设计前期根本没有“用户画像”、“体验地图”这回事，有的就是PM对老板需求的传话，但大家还是一如既往的堆砌这种没有意义、互相欺骗的页面。行业内好像也都对此心照不宣…
- 最近在面试也有同样的感受，大多数时候面试者也说不出从这些方法论里面得到了什么设计决策，而是再给我介绍这些理论，十分不耐烦。

# discuss-base-location
- ## 

- ## 

- ## 

- ## [重庆互联网环境为什么这么差？ - 知乎](https://www.zhihu.com/question/628041980)
- 没有顶流计算机高校，没有区位优势，还特么处在内陆，搞个锤子互联网。
- 重庆更多以制造业为主，人才储备相对也要差点

# job-desc
- hc: editor/编辑器, 在线表格, 协作/协同, cms, 低代码

- ## 

- ## 

- ## 成都 [「前端架构师（低代码自研部门招募）招聘」\_宇信科技招聘-BOSS直聘](https://www.zhipin.com/job_detail/28972918671d348e1HR80tS9ElFY.html?lid=8GZwAC4lQxf.search.1&securityId=De8aaJIg8RgYk-b14FUydVe6Mkln_4qVDIkqb3qzQ47KR-r1Z2eto9c1wW7bp_7HGZcP4okTpaVtrvGVybaJ1H1_y4_G5326UvVxSKY9PphCw4I%7E&sessionId=)
- 参与前端&低代码平台搭建及架构设计，开源组件预研及引入
- 能够接受出差的优先考虑；

- ## 成都 [「前端-外派互联网大厂/视频面试/双休/包三餐招聘」\_软通动力招聘-BOSS直聘](https://www.zhipin.com/job_detail/a2022d31259122101XF83dS9EFJT.html?lid=8H2UD9BWYbz.search.4&securityId=0WeSv5UgRwoFR-i11HK9aNUmNvhc_05I__h0oSrTUPNaHDiwYO4aIw4qEzo0yUylpK8CY1u5zHnyFOtjmor7x--SthCT34rd3vKdw76lC3o9ayUhwQU%7E&sessionId=)

- ## 深圳 [「腾讯文档Alloyteam前端工程师招聘」_腾讯招聘-BOSS直聘](https://www.zhipin.com/job_detail/42870e881fdd1a9e1nR92d6_E1pY.html?lid=8HxKPAvnPAt.search.11&securityId=_RMwKSOSLghHh-P1FGNuFdJvHFTCNy-es2h4KOVVJXMMykcy2L_9qLJgQRaDgmulxW9q15CpDTox0Y5Cc2DfO7x949fIeA1cyLXEphMPUDTf&sessionId=)

- [腾讯文档 Alloyteam Web 前端开发招聘」\_腾讯招聘-BOSS直聘](https://www.zhipin.com/job_detail/cf1c9a7c06094cfd1nZz29S1FFVS.html?lid=8HxKPAvnPAt.search.26&securityId=nl9muIPqIaoGY-h1j_k1Q721MTUbs6IdALGkvJZMroc4WGoRWc63ewOgfIGsxjelmlFLmwfdIrzzLHNQXei1Qy-3ErEHlKYIK8psrREZ0cCn&sessionId=)

- ## 深圳 [「高级web前端开发工程师招聘」_数联天下招聘-BOSS直聘](https://www.zhipin.com/job_detail/c140149a04cd83f81HZz2N29F1tU.html?lid=8ID4quVvfs3.search.10&securityId=5V0OEWLfqj_Vm-P1EHwg-rPKfsNuqlAGbktUfg5YXgnp5QRydc6qlDt30F6Q1XdJv8xnSo7PsF8hKd9Atfe8lFsMRGZEiiOilAq75aA_rIrzWXOmsQ%7E%7E&sessionId=)

- ## 深圳 [「前端开发工程师（低代码）招聘」_SHEIN招聘-BOSS直聘](https://www.zhipin.com/job_detail/d9db8df004bec59f1HV_2N60FlRX.html?lid=8JcWKxhDwk8.search.15&securityId=h9paudmkgVYle-e1vcF4duajrwtbES3uKg4YYXNk3B5MQsFremlVcD3cW3k36f2_LMcYlahJtEW1KAdpyJsrZIZdjX6K1LLAMOak6IN17rKopNWU5PPS&sessionId=)
- 支撑 CMS 相关领域的控制台日常需求分析和功能开发，优化用户体验; 
- 熟悉会场搭投、动态表单、低代码、可视化等领域优先。
- 有大型电商经验，招选搭投等项目相关经验者优先

- ## 深圳 [「字节跳动飞书文档前端开发工程师招聘」\_今日头条招聘-BOSS直聘](https://www.zhipin.com/job_detail/b4365b045674ce7e1XZ809S6FlpS.html?lid=8HxKPAvnPAt.search.6&securityId=A8UTE5Fv5zmFX-b1tYx1R3MYSb-jgAD8viEOzAzROGkeuGls5fy-BysObpUSwzHJ84etbvT_1AqLzD-rn9DRbxfMm3WmW9b3kJg1QthEBB_mgR0%7E&sessionId=)

- [「前端开发-飞书文档招聘」\_字节跳动招聘-BOSS直聘](https://www.zhipin.com/job_detail/69fc26753172447c1XZ43964FlNU.html?lid=8HrlhjhaXRB.search.1&securityId=0i-CgYepnWKQ_-w1I15j88qVw5fXTtd9J4NkoK3F_d9vVhIcW6XOXFspd8zdlD4ArvV7dnxLCuq7APUwm47Xofl4Q81s8ZBx9Hu_MLk1ihD-VcdiEfQ%7E&sessionId=)
  - 负责飞书文档产品的前端研发工作

- [「前端开发-飞书文档招聘」\_字节跳动招聘-BOSS直聘](https://www.zhipin.com/job_detail/69fc26753172447c1XZ43964FlNU.html?lid=8HxKPAvnPAt.search.9&securityId=vRHb1j8I0cvlv-p1YC3zRVGT1j8WKfhzTJD9AkLGP5-rVH5VFM2Sk0VHpzC6lNcmsjYz6Jv_5iu6FOn6t-tVRTi5pI6Vw73JlTpZ-f82AbXJGm_bbNc%7E&sessionId=)

- ## 杭州 [「资深前端开发工程师 - 飞书招聘」\_字节跳动招聘-BOSS直聘](https://www.zhipin.com/job_detail/0c32dd01a77c14a61HZ93Nm6FVdW.html?lid=8HJdCfZlEMh.search.17&securityId=761QuLbfZSDgC-c1yQAPmhxItqF4_mZwR9RJzWUvHM_lBLNGowzRGKMKHQpDnPW9vf2bu6Bjffn0NpJ1GpTdDir2RKQnZ1BntE9lEsZa5Dcc4bU58w%7E%7E&sessionId=)

- ## 杭州 [「资深前端开发工程师（报表引擎）招聘」\_网易招聘-BOSS直聘](https://www.zhipin.com/job_detail/a9cef5f4ceeb24be1HZy0969FVVX.html?lid=8HJdCfZlEMh.search.13&securityId=wGEvbO8NjI1YG-m1ZfHM_P0XUqlWrsS3rPKWLMwLy-Gnv7yZmiddodX52QVtkakg_-I9vrT9kaiRCA96OElA43bG1FRLyMvepwPlVqpaDG9B&sessionId=)
- 负责低代码平台 BI 报表设计器的架构设计、技术方案与实现
- 负责低代码平台图形可视化（柱形图、折线图、饼图等）设计器的架构设计、技术方案与实现；
- 负责低代码平台在线 Excel/在线表格设计器的架构设计、技术方案与实现

- ## 杭州 [「钉钉高级前端技术工程师(专家)-文档协同招聘」_阿里巴巴集团招聘-BOSS直聘](https://www.zhipin.com/job_detail/01a10b3d306c1e3d33R52dq5FFY~.html?lid=8IoCdDmuqZB.search.15&securityId=kGpfBE_FsKt84-b1s7-8mNWFuQD5-zV3wvjZ4-nHFBvGOSdY5ireJUn5Z-LNlYY14if4FmCH7A_qpDJ-eSEyF7Mv0B2n5tBGntVZjZd1B68~&sessionId=)

- [「高级前端工程师/专家招聘」\_阿里巴巴招聘-BOSS直聘](https://www.zhipin.com/job_detail/c6d49c236304aaeb1HZy2d28FFRY.html?lid=8HpQrvmZ62z.search.14&securityId=VcMS6j15v6IVk-71EBAXzZg7W8xPwCmttRH8VHQjWBOasMu9bPVwqM2IBBFV-78jchBi9HR3uUE195VrWWBKeRIs8blpTWQPEbUfjvu3MPRPgPswni4%7E&sessionId=)

- [「钉钉前端开发工程师招聘」_阿里巴巴集团招聘-BOSS直聘](https://www.zhipin.com/job_detail/ab909e5a952a83d71HZz2N61FVBQ.html?lid=8HJdCfZlEMh.search.6&securityId=ej6iP6T9CSn7f-V13uBpmzfUghueoSGoaBPsLeClQP-qANBYlyqwgO7usMehXb6sH50B6ZF1jP5_wukaM47TmHMmlQRchP-SCxzSJlaQ3FOU&sessionId=)

- [「前端技术专家 —— 文档协同【急速招聘】招聘」_阿里巴巴集团招聘-BOSS直聘](https://www.zhipin.com/job_detail/8f3c3df0a3cc5cba1nR829u4EFNX.html?lid=8HJdCfZlEMh.search.4&securityId=egF5Pm4MWsKQn-K1LZrMBgRZ3V8H6vzyT-00He23Ai8AQmshLeeTk6dCknLtRLbdAb9EG8R7gdR79sIddj5vICwue7hvrkDuVMU4U3O2AulK&sessionId=)

- ## 上海 [Insomnia 招聘 Senior Frontend Software Engineer（Electron 方向）  - V2EX](https://v2ex.com/t/1008399#reply1)
- 前端技术栈主要是 Electron ，目前前端的 3 个同事都在欧洲，要在上海组建前端团队，计划第一季度招 3 个人。

- ## 北京 [「前端开发工程师-飞书文档-云表格(急招)招聘」\_今日头条招聘-BOSS直聘](https://www.zhipin.com/job_detail/025cf270b1e3a4b91HR63N26FVdT.html?lid=8Hlw0onwvoP.search.2&securityId=dxTytDsP92P2N-n122ahvI_G-kQjKqAAWS6b0dnmBPyaRlRB3haWijkiwL7hjvTSYL6HsSwtaycdYmY0i7BLph5ITcJbSYqtzasd0Jw2IYltsZPZ&sessionId=)
- 负责飞书表格产品的研发

- [「资深前端开发工程师-飞书多维表格招聘」\_北京字节跳动招聘-BOSS直聘](https://www.zhipin.com/job_detail/10e1b705ba28d1cb1Hd73Ny1F1JU.html?lid=8Hlw0onwvoP.search.3&securityId=5wj1DpRjbKidt-n1bdl8eehmSKZHtfTz5ScoS863q4XDRvo2kd8ZeTaT9f-EPKRJGXZgAX7FiAuOtXyZ3uC0_4WFEIxmOqCNVsITckM9DKwhnisZ&sessionId=)
  - 负责飞书多维表格产品的研发

- ## 北京 [「前端开发工程师（编辑器）招聘」_即时设计招聘-BOSS直聘](https://www.zhipin.com/job_detail/82b1beb3b7ef26811HZ73tq0EFdV.html?lid=8IeyzC2CQz3.search.2&securityId=rxyklhFD2lJW5-v1JYFyHhcxV4eddlu9o-5ZMdSFPKAnFBmLFVRzCxgTGu01oJmXcVQD-u-DkVpXoRFqjw1Y6b6OoinU0H3BLABCqPtneMIj-t_FfmA%7E&sessionId=)
- 主导即时设计主站业务的前端研发
- 探索和尝试 PWA, WebAssembly等前沿技术提升产品体验
- 对数据驱动视图有深入认识; 有Typescript实战经验
- 较强的业务抽象和 UI 建模能力，有架构过大型互联网项目经验者优先

- ## 北京 [「前端开发（编辑器方向）招聘」_快手招聘-BOSS直聘](https://www.zhipin.com/job_detail/f1f4bf49469c58cc33V_3d66FlU~.html?lid=8IeyzC2CQz3.search.23&securityId=sFHYgAWLbwTg3-R1m8KQcMqu9IStqJWPr-pbwlvjEEIOY6g06MERV4JF3lAYhpDKbTIpNyVXA200YB-6zmM5u5Tk351KIg5kTkK7gQc7QvaOag%7E%7E&sessionId=)
- 负责公司大型协同文档项目的研发与技术重构优化
- 挑战高并发协同、多端状态管理、UI仿真渲染等技术难题的攻坚
- 熟悉浏览器底层原理和机制，较强的trouble shooting能力，有多人项目协作经验

- ## 北京 [中教云智 [base 北京, 无锡] 寻找[前端，后端，客户端]同学 - V2EX](https://v2ex.com/t/1008451#reply9)
- 公司致力于通过人工智能、大数据、云计算等新一代互联网技术，汇聚多元优质的数字化教育资源，实现多版本数字教材、适配数字资源的互惠共享，打造集资源、工具、服务为一体的综合性智慧教育平台
  - 目前产研团队核心成员全部来自于字节跳动, 腾讯
