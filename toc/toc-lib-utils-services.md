---
title: toc-lib-utils-services
tags: [backend, mq, redis, search, utils]
created: 2025-12-26T08:55:30.089Z
modified: 2025-12-26T08:56:31.035Z
---

# toc-lib-utils-services

# guide

# cache
- https://github.com/redis/node-redis /17.4kStar/MIT/202512/ts
  - https://redis.js.org/
  - a modern, high performance Redis client for Node.js.
  - [ioredis vs node-redis _202311](https://github.com/redis/node-redis/issues/2658)
    - ioredis was created as an alternative client 9 years ago by an individual: @luin. It was acquired by Redis Ltd. in 2023.
    - it's effectively unmaintained now.
    - For a long time, it had more functionality than this library (including sentinel support). However, over time there was an increasing amount of functionality with no direct support, and those had to be hand-rolled using raw commands. e.g. JSON commands. This is especially painful with TypeScript,
    - This project is now a monorepo that's written in TypeScript and includes direct support for more of the modern features
# message-queue

# middlewares

# toolbox
- https://github.com/microsoft/PowerToys /131kStar/MIT/202604/csharp/cpp
  - Microsoft PowerToys is a collection of utilities that help you customize Windows and streamline everyday tasks.
  - 📡
    - 可尝试开发mac/linux版

- https://github.com/iib0011/omni-tools /9kStar/MIT/202604/ts
  - https://omnitools.app/
  - a self-hosted web app offering a variety of online tools to simplify everyday tasks. 
  - All files are processed entirely on the client side: nothing ever leaves your device. Plus, the Docker image is super lightweight at just 28MB
  - i18n uses Locize
  - 主要工具
    - image
    - pdf
    - video
    - developer

- https://github.com/CorentinTh/it-tools /37.9kStar/GPL/202602/ts/vue
  - https://it-tools.tech/
  - Collection of handy online tools for developers, with great UX.
  - 非常典型的list-article导航结构

- https://github.com/ikenai-lab/convert.gg /MIT/202512/python/ts/inactive
  - powerful, privacy-focused desktop application designed to handle your day-to-day file manipulation
  - Whether you're merging PDFs, compressing images, or extracting archives, everything happens securely on your own machine.
  - PDF, image, zip
  - Frontend: Electron, React, Vite, TypeScript, TailwindCSS
  - Backend: Python (PySidecars): Heavy lifting is delegated to specialized Python scripts.
  - [I built an open source desktop alternative to iLovePDF to avoid uploading private files : r/SideProject _202512](https://www.reddit.com/r/SideProject/comments/1pwzhlo/i_built_an_open_source_desktop_alternative_to/)

- https://github.com/gchq/CyberChef /34.5kStar/apache2/202604/js
  - https://gchq.github.io/CyberChef
  - a web app for encryption, encoding, compression and data analysis
  - web app for carrying out all manner of "cyber" operations within a web browser. These operations include simple encoding like XOR and Base64, more complex encryption like AES, DES and Blowfish, creating binary and hexdumps, compression and decompression of data
  - 交互设计支持multi-step顺序执行
  - The tool is designed to enable both technical and non-technical analysts to manipulate data in complex ways without having to deal with complex tools or algorithms.
  - CyberChef is entirely client-side
    - all processing is carried out within your browser, on your own computer.

- https://github.com/rangeva/online-dev-tools /MIT/202507/ts/inactive
  - https://onlinedevtools.io/
  - collection of essential online tools for developers, including text utilities, encoding/decoding tools, date converters, JSON formatters, security tools, and much more.
  - How can I edit this code?
    - Simply visit the Lovable Project and start prompting.

- https://github.com/VERT-sh/VERT /14.5kStar/AGPL/202604/ts/svelte
  - https://vert.sh/
  - The next-generation file converter. Open source, fully local* and free forever.
  - a file conversion utility that uses WebAssembly to convert files on your device instead of a cloud.
  - No file or file size limits
  - Convert images, audio, documents, and video*

- https://github.com/C4illin/ConvertX /16.4kStar/AGPL/202603/ts
  - Self-hosted online file converter. Supports 1000+ formats
  - Written with TypeScript, Bun and Elysia.

- https://github.com/p2r3/convert /GPL/202603/ts
  - https://convert.to.it/
  - Truly universal online file converter
# more
