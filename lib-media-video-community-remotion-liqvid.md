---
title: lib-media-video-community-remotion-liqvid
tags: [community, liqvid, remotion, video]
created: 2024-06-21T09:48:28.870Z
modified: 2024-06-21T09:53:44.956Z
---

# lib-media-video-community-remotion-liqvid

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-vid-pm
- ## 

- ## 

- ## Google 正式推出 Gemini AI 驱动的视频演示应用 Vids 
- https://x.com/imxiaohu/status/1855436961131164004
  - 通过简单提示即可生成各种类型的视频演示, 你只需提供提示或 Google Drive 中的文档，系即可生成一个初始视频故事板，包括推荐的场景、脚本、背景音乐等。

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 求问，录屏或录 gif 的时候，那个“局部放大”的效果是怎么实现的，需要用什么 app？我一直用 Gifox，但它没有这个功能
- https://x.com/laike9m/status/1812350033712546288
- Screen Studio 早买早享受
- 剪映，放大镜特效，可以调节参数控制放大范围
- 微软官方的zoomit

# discuss-vid-size/bandwidth-compress
- ## 

- ## 

- ## 最方便的图片视频压缩工具 —— 微信。 三百多兆的视频，往微信里一丢，四兆，简直就是牛了个逼
- https://x.com/juransir/status/1857071258082365921

- 单向有损压缩 没法恢复

- 100M 一张的相机原片，用Windows画图打开，啥也不做，保存。 一看剩下4兆，关键是你肉眼还看不出来压缩了
- 最方便的ocr工具-微信文字识别，本来是为了监控识别用户。

- Google Photos 才是... 甚至不需要专门软件， 浏览器打开拖进去，人在墙外的话上传/压缩速度还秒杀微信... 上传之后还能直接各种方式搜索视频/图片内容

- 候选压缩工具 B站、油管、阿里盘，油管一压多得无水印。

- 有个类似的技巧，上传图片过大，截图发到微信/qq然后直接拖到桌面

- ## I wrote up a full article on how we serve 15 terabytes of 4K video per month for just $2.18.
- https://x.com/steve_tenuto/status/1857523923509981437
  - https://screencasting.com/cheap-video-hosting
- Is there a way it can be secured? I.e I assume you must prevent people from just using the playlist url outside of your site?
  - I haven’t tried this yet, but I think there’s probably a way to use R2’s signed URLs inside the manifest file.

- ## 一个月15TB的流量 4K 视频画质才花了 不到 3 美元，主要是 CloudFlare 的出口流量是免费的，所以放在 R2 可以很便宜，
- https://x.com/dotey/status/1854997844417298485
  - 另外他们用了 HLS 协议，将视频按照不同分辨率切成了块，访问时按需下载块就好了
  - 如果你有面向海外的服务但是网络流量很大，比如视频、文件下载这种，可以试试 CloudFlare 的 R2 存储服务，只收存储的费用，不收网络流量费用

- R2 视频防盗加密的问题好不好解决

- cloudflare真的牛逼，把流量搞成了免费，之前在 vercel 我就经常担心流量超标
  - Cloudflare 的masque协议被封了真的很好用啊

- 国内这种做线上课程的，小鹅通的流量和存储都很贵。这个面向国内用户可行吗？
# discuss-vid-codec
- ## 

- ## 

- ## I am picking up my WebCodecs efforts with a new website: http://convert.remotion.dev!
- https://x.com/JNYBGR/status/1854081067352793592
  - now, you can convert an MP4 to a WebM.

- So im assuming this is native JS not WASAM?, if true then thats crazy, also can it do other way around and do compression?
  - I have to look into compression, I think it's not (yet) possible with the Web APIs though
  - But I am planning the opposite WebM -> MP4! That is 100% possible
# discuss-vid-img-avif
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-vid-img-gif
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-liqvid
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-remotion
- ## 

- ## 

- ## 

- ## 

- ## 🐛 Embarassing Remotion bug: Instead of creating a new thread for each video we read, we created a new thread for every single frame in the video
- https://x.com/JNYBGR/status/1890345448986030207
  - +50% slowdown is very realistic
  - We probably had this bug because we used a “thread pool” abstraction from a library which was somehow implicit
  - We rearchitected Remotion's concurrency model in Rust to be even faster! Enjoy up to 50% faster renders in the latest version thanks to the "new architecture"

- What version is the fix on?
  - 4.0.264 Still pending validation from bigger users, but I’m standing by should any issues arise

- ## From Markdown to Video: animated code walkthroughs with Code Hike and Remotion
- https://x.com/pomber/status/1805590424716808685

- ## 怎样做出令人惊艳的代码交互视频，这位国外推友在回复中分享了他的技术栈
- https://x.com/vikingmute/status/1803607706189832373
  - CodeHike + Remotion

- ## Remotion now supports emitting arbitrary files alongside the video _202406
- https://x.com/JNYBGR/status/1803771915191881942
  - A primitive that allows for emitting programmatically generated subtitles, timestamps, YouTube descriptions...

- this is pretty awesome. No more having to prepare files before the render process.
