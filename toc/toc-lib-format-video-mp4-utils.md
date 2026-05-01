---
title: toc-lib-format-video-mp4-utils
tags: [format, mp4, toc, utils, video]
created: 2024-04-14T12:18:31.158Z
modified: 2024-04-14T12:19:52.096Z
---

# toc-lib-format-video-mp4-utils

# guide

# popular
- https://github.com/motion-canvas/motion-canvas /16.2kStar/MIT/202410/ts
  - https://motioncanvas.io/
  - A TypeScript library that uses generators to program animations.
  - An editor providing a real-time preview of said animations.
  - It's a specialized tool designed to create informative vector animations and synchronize them with voice-overs.

- https://github.com/redotvideo/revideo /MIT/202410/ts
  - https://re.video/
  - Revideo is an open source framework for programmatic video editing. 
  - It is forked from the amazing Motion Canvas editor, with the goal of turning it from a standalone application into a library that developers can use to build entire video editing apps.
  - Revideo lets you create video templates in Typescript and deploy an API endpoint to render them with dynamic inputs. It also provides a React player component to preview changes in the browser in real-time. 

- https://github.com/liqvidjs/liqvid /MIT/202406/ts
  - https://liqvidjs.org/
  - a library for creating interactive videos in React
  - https://github.com/liqvidjs/plugins
    - While these were built for Liqvid, they are compatible with other animation libraries.

- https://github.com/remotion-dev/remotion /NonCommercial/202406/ts
  - https://remotion.dev/
  - creating videos programmatically using React.
  - [Remotion 5.0 license change _202404](https://github.com/remotion-dev/remotion/pull/3750)
  - https://github.com/c0/remotion-playground
    - 水滴聚合分散的效果，基于remotion实现
  - [A Modern FREE Open Source Video Editor : r/reactjs _202308](https://www.reddit.com/r/reactjs/comments/15vv6yu/a_modern_free_open_source_video_editor/)
- https://github.com/thecmdrunner/remotion-render-alternatives
  - WIP: An alternative to using Remotion Lambda or Cloudrun for rendering Remotion videos in the cloud
  - This is a Next.js template for building programmatic video apps, with @remotion/player and @remotion/lambda built in.

- https://github.com/ZhouXiaolin/opencat /MIT/202605/rust/ts
  - http://www.catcut.cc/
  - OpenCat 是一个 纯 Rust 原生 的程序化视频合成引擎——类似 Remotion 用 React 写视频，但 OpenCat 不跑浏览器、不依赖 Node.js。它把 Skia 渲染、Taffy 布局、QuickJS 脚本和 FFmpeg 编码焊成一个独立的 Rust 二进制。一行命令或几行 JSONL，就能生成一段带转场、动画、字幕和音频的 MP4 视频。
  - Tailwind 写布局，GSAP 调动画，CanvasKit 画图形——底层是 Rust + Skia 原生渲染，不跑浏览器。
  - [OpenCat, 一个程序化视频生成制作库 - LINUX DO _202604](https://linux.do/t/topic/2090262)

- https://github.com/liangdabiao/hyperframes-fix /?open
  - 本项目目的是让 HyperFrames 生成视频适应国内需求，1 流畅的中文语音， 2 中文短视频样式新增， 3 优化整个生成视频流程。 基本上现在一键就可以完成横版竖版的快节奏短视频，例如随便丢给一个文章，一个doc，就能够制作视频
  - [【开源】HyperFrames-fix 生成快节奏短视频-丢文章就能够制作视频 - 流畅语音和样式 - 源荟萃 - LINUX DO _202605](https://linux.do/t/topic/2092060)

- https://github.com/video-db/Director /MIT/202412/python
  - https://chat.videodb.io/
  - Think of Director as ChatGPT for videos. It is a framework to build video agents that can reason through complex video tasks like search, editing, compilation, generation etc & instantly stream the results.
  - Built on top of the cutting edge 'Video-as-Data' infrastructure, VideoDB
  - Framework to build video agents that can reason through complex video tasks like search, editing, compilation, generation etc & instantly stream the results.
# apps
- https://github.com/lyonbot/video-to-gif /202404/ts
  - https://lyonbot.github.io/video-to-gif/
  - In browser, convert Video to GIF, with cropping and speed accelerating features
  - 做了一个在浏览器里「视频转 GIF 」的工具。 使用 WebCodec 解码视频，转换速度还是有保障的。而且还可以自定义颜色、抖动等参数，提高转换效果
# examples

# ffmpeg

## ffmpeg-ui

- https://github.com/mifi/lossless-cut /29.2kStar/GPLv2/202501/ts
  - https://losslesscut.app/
  - The swiss army knife of lossless video/audio editing
  - Lossless cutting of most video and audio formats
  - Fast multi-file workflow (note: no mass/batch export yet)
  - LosslessCut aims to be the ultimate cross platform `FFmpeg` GUI for extremely fast and lossless operations on video, audio, subtitle and other related media files. 
  - The main feature is lossless trimming and cutting of video and audio files, which is great for saving space by rough-cutting your large video files
  - Everything is extremely fast because it does an almost direct data copy, fueled by the awesome FFmpeg which does all the grunt work.

- https://github.com/66HEX/frame /266Star/GPL/202602/rust/svelte
  - https://www.framegui.app/
  - a high-performance media conversion utility built on the Tauri v2 framework. 
  - It provides a native interface for FFmpeg operations, allowing for granular control over video and audio transcoding parameters
  - The application leverages a Rust-based backend for concurrent task management and process execution, coupled with a Svelte 5 frontend for configuration and state monitoring.
# utils
- https://github.com/patrick-s-young/react-video-scrubber /202303/ts
  - React canvas-enabled video frame scrubber.
  - This React component is a locally-based solution for generating still frames from a video source. 
  - This method is an alternative to a server-side, Node.js/FFmpeg solution where video frames would be extracted and returned to the client as a sequence of images.
  - Redux Toolkit 
# video-player
- https://github.com/solidSpoon/DashPlayer /2.9kStar/MIT > AGPL/202502/ts
  - https://dash-player.solidspoon.xyz/
  - 为英语学习者量身打造的视频播放器，助你通过观看视频、沉浸真实语境，轻松提升英语水平。
  - 依赖@electron-forge、tailwindcss、radix-ui、better-sqlite3、drizzle-kit、monaco-editor、react-markdown、remark-gfm、zustand、react-player、react-virtuoso、swr
  - 双语字幕：支持机器翻译字幕。只展示中文/英文，或者全部隐藏都可以。
  - AI 字幕：可以使用 AI 为视频生成字幕。
  - 按字幕跳转： 重复当前句，或者跳到上一句，怎么跳都可以。
  - 查词查询：鼠标悬停生词可快速查询，不打断学习进程。
  - 视频下载：粘贴视频链接，下载视频。
  - 支持win/linux/mac
# subtitle
- https://github.com/Huanshere/VideoLingo /15.9kStar/apache2/202505/python/inactive
  - https://docs.videolingo.io/
  - Netflix级字幕切割、翻译、对齐、甚至加上配音，一键全自动视频搬运AI字幕组
  - 一站式视频翻译本地化配音工具，能够一键生成 Netflix 级别的高质量字幕，告别生硬机翻，告别多行字幕，还能加上高质量的克隆配音
  - 使用 yt-dlp 从 Youtube 链接下载视频
  - 使用 WhisperX 进行单词级和低幻觉字幕识别
  - 使用 NLP 和 AI 进行字幕分割
  - 自定义 + AI 生成术语库，保证翻译连贯性
  - 三步直译、反思、意译，实现影视级翻译质量
  - 按照 Netflix 标准检查单行长度，绝无双行字幕
  - 支持 GPT-SoVITS、Azure、OpenAI 等多种配音方案
  - 一键启动，在 streamlit 中一键出片
# nsfw
- https://github.com/stashapp/stash /11.5kStar/AGPLv3/202512/go/ts
  - https://docs.stashapp.cc/
  - https://stashapp.cc/
  - a self-hosted webapp written in Go which organizes and serves your diverse content collection, catering to both your SFW and NSFW needs.
  - supports a wide variety of both video and image formats.
  - statistics about performers, tags, studios and more.
# iot
- https://github.com/Jstudner/jcorp-nomad /CC-NC/202604/js/cpp
  - http://nomad.jcorptech.net/
  - An extremely compact offline media server for Movies, Shows, Books, and Music.
  - A portable, offline media server powered by the ESP32-S3 in a thumbdrive form factor.
  - Stream movies, music, books, and shows anywhere - no internet required.
  - [Nomad Mk3: Offline, Open-source, low-power self-hosted media server : r/selfhosted _202604](https://www.reddit.com/r/selfhosted/comments/1sdd5ny/nomad_mk3_offline_opensource_lowpower_selfhosted/)
    - The love concept! As others have stated I'd have some concerns about bandwidth limiting quality but especially as an initial project, this rocks! I wonder what options you have down the line to throw something more powerful in there to support high bitrate 1080p. Kudos on keeping it open source
    - With the current setup you can typically get 1-2 1080p 60fps streams going without buffering, though that does assume you like in the woods with no interference lol. That being tested with the big buck bunny demo files. 4k is still off the table though, one stream almost works, but still has to buffer as it can't quite keep up.
# more
