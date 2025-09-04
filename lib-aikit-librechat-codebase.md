---
title: lib-aikit-librechat-codebase
tags: [codebase, langchainjs, librechat]
created: 2025-09-04T17:54:23.637Z
modified: 2025-09-04T17:54:44.603Z
---

# lib-aikit-librechat-codebase

# guide

# overview

# image-gen
- 添加自定义tool需要修改代码，不能在ui上添加stable-diffusion-webui/comfyui
- stable-diffusion-webui tool的实现原理
  - 通过axios POST请求发送到Stable Diffusion WebUI的 `/sdapi/v1/txt2img` api
  - 响应的图片数据`generationResponse.data.images[0]`, 拼接为base64编码`data:image/png;base64,${image}`，并保存到文件系统
  - 在`api/config/paths.js`文件中定义了图片输出目录`imageOutput`为 `client/public/images/{userId}/imageName.png`, 系统中 text2image的输出目录/聊天时上传文件的目录 都是这个目录
    - 每个用户有自己的独立图片存储子目录，支持多用户环境下的文件隔离

- 🐛 存在问题，首次生成图片时chat聊天显示图片失败, 此时`<img>`的`src`属性值为 
  - `/images/68b49d698d571b3ee771f13e/e0bf0068-596f-412f-b75b-90fb1053f5fa-stable-diffusion_402432726_img_CYZC_aZ6AGo--XYzoxL0p.png`; 
  - 刷新页面后图片能正常显示, url未变化
# backend

# frontend

# more
