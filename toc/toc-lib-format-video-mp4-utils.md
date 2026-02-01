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
# nsfw
- https://github.com/stashapp/stash /11.5kStar/AGPLv3/202512/go/ts
  - https://docs.stashapp.cc/
  - https://stashapp.cc/
  - a self-hosted webapp written in Go which organizes and serves your diverse content collection, catering to both your SFW and NSFW needs.
  - supports a wide variety of both video and image formats.
  - statistics about performers, tags, studios and more.
# more
