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

- ## [Serving Video with HTTP Range Requests _202505](https://smoores.dev/post/http_range_requests/)
- `<video>` elements can be provided a `src` attribute, which specifies the URL of the video to embed.

```HTML
<video controls width="250">
  <source src="/shared-assets/videos/flower.webm" type="video/webm" />
  <source src="/shared-assets/videos/flower.mp4" type="video/mp4" />
</video>
```

- in Network tab: Firstly, the response code for the `flower.webm` request was 206, rather than the standard 200 success/OK response. 
  - you may actually have seen multiple requests for the video file, all responding with a 206. 
  - There are also some additional headers, like Accept-Ranges: bytes and Content-Range: bytes 0-554057/554058.

- Together, these make up an HTTP range request. As the name suggests, range requests allow the client to request a specific range of bytes from the server, rather than the entire resource. This is particularly useful for video, as videos can be arbitrarily long 
# discuss-vid-ai 👾
- ## 

- ## 

- ## 

- ## 

- ## Codex + HyperFrame is eating vedio editors
- https://x.com/Saccc_c/status/2051145377865204222
  - 用纯编码的形式手搓各种视频，真tm的太爽了
  - Claude 官推通过Remotion、hyperframe 这类工具制作视频已经撸了至少10M流量

- 这个方向最值得看的不是替代剪辑师，而是把视频变成可测试的代码资产。以后改一个脚本批量重出 20 个版本，比在时间线上手搓稳定太多。

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

- ## 我的电脑在其他平台在线播放视频，风扇完全不会转得像在Bilibili里播放视频时那样夸张。
- https://x.com/sinokitatokyo/status/1904905066966114434
- 感觉像是b站特有的DASH解码方案，以及特有如H.265/HEVC视频编码格式, 对硬件还是有一定要求的, 完全依赖软件解码会导致CPU占用率飙升, 还有一个就是阿b用了HTML5，对浏览器的压力也不低
  - 但是b站这样做也有好处：弹幕互动好、流畅适应
  - 对老设备确实不如其他视频网站友好

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
# discuss-flash
- ## 

- ## 

- ## 大家都知道 FLASH 已经死了，但我发现还可以拯救一下，至少你原先做过的大量的 FLASH 资产还能利用起来赚钱。
- https://x.com/ezshine/status/1898397496642359556
  - 具体做法是这样的，利用 https://ruffle.rs 在浏览器里运行 FLASH，然后把网页用 Tauri 2.0 打包成 iOS 或者 Mac 应用。
- 这个 ruffle 项目挺屌的，用浏览器API 做了个 flash 模拟器。现在以前的 flash 游戏在浏览器里可以直接跑了。
- flash转H5的工具

# discuss-liqvid
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-solutions-plex/jellyfin
- ## 

- ## 

- ## 

- ## [Plex vs. Jellyfin for New Install : r/selfhosted _202512](https://www.reddit.com/r/selfhosted/comments/1pjoamf/plex_vs_jellyfin_for_new_install/)
- try jellyfin first since it’s free. i’ve used both plenty and much prefer jellyfin
- Plex is commercial, your account, user auth, etc, are handled by plex.tv not your server. They also recently changes rules and locked down features that didn't require their service... so you never know the future.
  - I switched to jellyfin... been happier. A few less features, but also a lot less bloat, and completely under your control and open source.

- If jellyfin had good apps I would use it over plex

- Jellyfin wasn't as polished as emby. At the time it didn't have decent intro detection with easy skipping on an android tv. That may have changed since then.
- Emby is more stable and has better performance. It is reliable.
  - Jellyfin has more features and infinitely better third party support. The intro skipper plugin is better than anything Emby offers. It detects intros, outros, recaps, previews.
  - Jellyfin customization is way better through skins and other plugins.
  - Currently the only Jellyfin drawback is related to performance, specifically with CPU usage being high and consuming a lot more RAM than Emby. The CPU thing isn't always an issue, but there is definitely something that causes Jellyfin to use way more CPU than it should. Likely something to do with DB read/write, but not positive.
  - Overall I'm happy with the switch to Jellyfin. But I would say if the main or only thing you care about is reliability and smooth performance, Emby might be the better bet for now. I think in a few years time, these issues will be resolved.
# discuss-screen-recording
- ## 

- ## 

- ## 

- ## 试用了三个 开源的 ScreenStudio 类似的录屏工具 Openscreen、Recordly、以及CursorLens，
- https://x.com/LgyLight/status/2033109870187295151
  - Openscreen 是鼻祖，其他两个都是从他身上 fork 来的，
  - 但是要论功能最强，最美观好用的，我推荐 Recordly。

# discuss-remotion
- ## 

- ## 

- ## 

- ## 

- ## [CC+Remotion等于全自动帮你剪辑视频+配音，懒人神器 _202603](https://linux.do/t/topic/1707471)
  - https://www.bilibili.com/video/BV1MLNwzUEje/
  - https://github.com/zhu1090093659/minister/tree/main/video
  - 直接让CC帮我安装，然后又让CC帮我剪辑一个视频出来，初版的时候还没有声音，然后我又让CC帮我整个配音，它就吭哧吭哧的自己下载了egde_tts下来，给搞了一个配音，最后弄出来的效果个人感觉还是很不错的，适合我这种懒得动手，但是又有需求的，现在分享出来，大家也可以去试试。
- 看着效果很不错，和PPT似的。
- 用现在的Opus或者gpt 5.4操控，效果很不一样的，可以尝试一下

- 不错啊，这个效果可以做抖音那种科普和宣传类视频了。配音可以调吗，这个原声配音听着有点难受
  - 完全可以，我推荐minimax的，效果很好

- 我去年做了，然后没流量哈哈，remotion适合做ppt类的，小lin说那种

- 我也觉得效果挺好，就是搞一天opus剪完自己倒是挺满意的，就是没人看。不过确实省去学习剪辑软件的时间了。

- ## [对Remotion一次尝试，经验分享 _202602](https://linux.do/t/topic/1552235)
- https://github.com/thr980710/T-Video /202602/ts
  - 基于 Remotion 框架的程序化音乐视频生成项目。
- 经朋友介绍了个玩意 Remotion 说是可以用代码生成视频，昨晚玩了一下。整体来说是一次 "半成功" 的尝试，分享一下经验和踩过的坑。
  - 使用 Remotion + AI 生成视频素材，制作了一个约 3 分钟的音乐视频。
  - Remotion 4.0 + React 19 + TypeScript
  - AI 生成视频素材（17 个场景）
  - 中英双语字幕同步
  - 成功的部分： 视频确实渲染出来了，1080P 30fps 字幕同步、转场效果都实现了 组件化架构，后续可复用
  - 失败的部分： 发布到某音后，音频被下架了… 版权问题，并且制作过程耗时太长，且怎么说呢，有点鸡肋，应该是我水平不够
- 可行，但繁琐 
  - 用代码控制视频的每一帧确实很精确，但工作量巨大： 17 个场景需要逐个配置时间轴, 48 行歌词需要手动对齐时间戳, 每次调整都要重新渲染预览
- 技术门槛不低 需要同时掌握： 
  - React/TypeScript 开发, 视频编辑概念（帧率、转场、调色）, Remotion 框架的各种 API, AI 视频生成工具的使用
- 渲染耗时 
  - 3 分钟的视频，渲染一次要好几分钟，调试效率较低，且转换成成品时第一次出现画面抖动，后面用 ai 搞定的，转换成品速度太慢了，两百多兆用了 20 来分钟，并且不能断网哈，我用梯子途中出现节点 timeout，平台挂了，视频转换也失败了，自己玩的时候注意点。
- 发布前一定要确认音频是否允许在国内平台使用。我这次用的音乐在某音直接被下架了，白忙活一场。 
- 总结
- 代码做视频这条路是通的，但性价比不高。适合：
  - 已经有成品视频，加个水印或其他一点想法的小东西
  - 对视频有精确控制需求，本人不怎么熟悉，但是如果了解这东西应该能玩出点花样
  - 想学习 Remotion 框架
- 不适合：
  - 一次性的视频制作
  - 追求快速出片

- ## 我用 remotion + ai 写了几万行代码, 适合做资讯展示类的视频，不适合做动画。
- https://x.com/hylarucoder/status/2014547783118946608
  - 帧驱动的方案微调动画非常难受，写网页+录屏的方案可能更好。

- Remotion这类帧驱动工具本质是程序化视频，调动画就像在改代码逻辑，当然不如直接操作DOM直观。网页+录屏才是真敏捷。

- 适合做overlay，不适合直接做成视频
- 确实不适合做动画，比较单一

- 我基于remotion微调了skill，总体比自己做视频简单

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
