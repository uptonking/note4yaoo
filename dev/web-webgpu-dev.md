---
title: web-webgpu-dev
tags: [web, webgpu]
created: 2021-01-01T21:41:42.412Z
modified: 2021-01-01T21:42:01.940Z
---

# web-webgpu-dev

# guide

- [webgpu玩家-四季留歌-小结](https://zhuanlan.zhihu.com/p/611407630)
# dev

# blogs

## [WebGL 与 WebGPU比对[8] - 系列完结总结与感想 - 知乎](https://zhuanlan.zhihu.com/p/480465528)

- WebGL 就是一个绘图的 API，你要完成炫酷的三维应用，还有很长的路要走，实时渲染技术与图形学知识、计算几何知识都有涉猎，好多入门的朋友直言渲染管线看不大懂的。

- WebGPU 并不是简简单单的“WebGL 升级版”，或者说大家应该摒弃固有认知。
  - 它是“GPU”的 Web 化，GPU 能做什么，它设计来就是用来干什么的，
  - 所以，你能在 WebGPU 中看到通用计算是与渲染计算同席而坐的，有几个 API 的行为是异步的，其设计理念也需要充分考量 CPU ~ GPU 之间的信息传递特点。
  - 所以我非常看好它的前景，但是前景不等于市场选择，市场是滞后的，是利益导向的，是希望偷懒的，非常受制于现有生态。
# more

# discuss-gpu

- ## 

- ## 

- ## 

- ## CPU上难道就不能带专用的浮点数计算单元吗，譬如tensorcore？为什么对于深度学习而言，CPU一定比GPU差呢？
- https://x.com/JXQNHZr1yUAj5Be/status/1799728380272935219
  - 以前的超算不就是这种专用的向量处理器嘛
- 感觉内存布局比较关键，GPU 能有的指令按说 CPU 都不是问题，到最后应该还是比较接近一个独显跟集显的区别，像集显容易遇到内存带宽瓶颈

- 有啊，avx512单元就是一种类似tensor core的实现

- cpu 有专门计算浮点的啊...... 但是因为 cpu 的定位是通用处理器，所以塞入了很多对于深度学习来说没有那么必要的单元，而且并行性也没有 gpu 好www
# discuss-webgpu/webgl
- ## 

- ## 

- ## 

- ## 

- ## Chrome团队计划用WebGPU（Dawn）渲染整个浏览器，除了Web内容，还包括工具栏和开发者工具（作为Skia的默认后端）
- https://twitter.com/uptonking2/status/1723203793939231033
  - 由于Vulkan已无可能成为现代图形 API 的跨平台标准（事实上转变为安卓平台的 Metal/DX12），WebGPU是村里唯一的希望了
  - [重新理解 Web - 知乎](https://zhuanlan.zhihu.com/p/581977751)
