---
title: spec-format-image
tags: [format, image, spec]
created: 2023-09-29T09:49:02.171Z
modified: 2023-09-29T09:49:22.589Z
---

# spec-format-image

# guide

- 画板或批注类产品要参考规范 [Web Annotation Data Model](https://www.w3.org/TR/annotation-model/)
# spec

- 

## [IIIF | International Image Interoperability Framework](https://iiif.io/)

- resources
  - [Image API Playground](https://www.learniiif.org/image-api/playground)

- IIIF (generally pronounced “triple-eye-eff”) is a set of open standards for delivering high-quality, attributed digital objects online at scale. 
  - It’s also an international community developing and implementing the IIIF APIs. 
- IIIF is a way to standardize the delivery of images and audio/visual files from servers to different environments on the Web where they can then be viewed and interacted with in many ways.

### [How It Works — IIIF](https://iiif.io/get-started/how-iiif-works/)

- Modern Web browsers understand how to display formats like .jpg and .mp4 at defined sizes, but cannot do much else. 
- The IIIF specifications align with general Web standards that define how all browsers work to enable richer functionality beyond viewing an image or audio/visual files. 
  - For images, that means enabling deep zoom, comparison, structure (i.e., for an object such as a book, structure = page order) and annotation. 
  - For audio/visual materials, that means being able to deliver complex structures (such as several reels of film that make up a single movie) along with things like captions, transcriptions/translations, annotations, and more.
- IIIF makes these objects work in a consistent way. That enables portability across viewers, the ability to connect and unite materials across institutional boundaries, and more.

- There are two main components to IIIF: delivering digital objects to sites and viewing them.

- Delivering objects
- The Image API defines how image servers deliver image pixels to a viewer. 
  - It allows the image to be sent as a full-sized image or as a smaller size, a zoomed portion, a rotated view, or as a black and white version. 
  - All of these settings are designated by changing portions of the URL for an Image API resource. 

- Viewing objects
- The Presentation API attaches basic metadata and structure to digital objects, defining how they appear in viewers. 
  - It does this via the Manifest, a JSON file which bundles up all the different elements of an IIIF object (such as a single image, or a series of images) with basic metadata (like title, description, and rights information) and structural information (such as page order).
- IIIF-compatible viewers generally allow users to pan, zoom, rotate, and resize image objects, and play audio/visual files. 
  - Some allow annotation with text, audio, location, and more. 
  - Others allow comparison of objects from a single collection side-by-side
# faq
- 如何解决在单元格位置的内容中也含有逗号的问题
# summary

- 

# dev

- 

# discuss
- ## 

- ## 

- ## 

- ## 因为 WebP 是谷歌主导的项目，而 HEIF 是苹果主推的格式，
- https://x.com/_Xheldon/status/1821038576630710750
  - 至今，苹果系统的预览或者命令行工具都只能查看不能编辑 webp 图片；
  - 而 Chrome 也是同样不能查看 HEIC 文件（更别提编辑了）

# discuss-gif
- ## 

- ## 

- ## 

- ## 🆚️ I still don't get the point of animated AVIF. 
- https://x.com/jaffathecake/status/1798289240004137194
  - AVIF is an image format derived from a video format, AV1. We don't need a video version of image format.
- One thing you can do with animated AVIF: Animation with an alpha channel. 
  - But… this really just highlights how dumb it is that AV1 doesn't support transparency. 
  - Also, with animated AVIF, the alpha channel is a separate image per frame. It's really bad for compression.
- There should be video containers that allow you to make video with alpha by muxing two video streams. I don't know much about video containers but I think MP4, MKV and OGV can all do that.

- Is there a more efficient way of storing per-frame alpha channels that would compress better?
  - The same way other channels are compressed in video: motion vectors, inter/intra-prediction… basically most of the stuff that makes modern video formats better than MJPEG. Whereas for alpha, AVIF does the MJPEG thing. Every frame is a keyframe.

- I’m not sure if it’s what Apple uses internally, but the animated memoji feature lets you send a video clip of your animation via iMessage and it uses transparency. The result is it’s very crisp and precise around the edges (you’d almost not know it was a video).
  - Yeah, HEVC supports an alpha channel, and I'm pretty sure it isn't keyframe-only (it certainly compresses better)
  - with HEVC the alpha channel is essentially a separate b&w video interleaved with the main video, and that's used as the alpha channel for the main video.

- Would animated GIF be better than `<video>` in these cases?
  - It looks like sometimes people just want to infinitely play something without users needing to click▶️everywhere ... and I find that particular article a good example and a smooth experience while reading it: I enjoyed it.
- Auto playing video is a thing (when the video is muted, which is easily done)

- Safari supports video files as an img src. Other browsers should just do this.
  - I agree completely. The only difference between `<img>` and `<video>` should be that img does not have player controls and cannot produce sound.
  - It does not make sense to artificially distinguish video formats from animated image formats. Especially if the payload codec is the same.

- Before support for `<source>` was re-added for `<video>`, the benefit was clearer. Positioning using background-image in CSS is slightly easier than positioning a `<video>`, when you want to display something on top.
  - I do think all browsers should do what WebKit does an allow video files to be used anywhere images can, including CSS.

- Most GIF sites use WEBP instead of GIFs afaik, and WEBP is also derived from a video codec

- APNG is the animated version of PNG, and it does support alpha transparency.
- Transparency is a big deal. Try using an animated GIF in a background that can change color (website's with white or dark themes). Quality as well, try making a GIF from a picture, like a face. APNG solves both problems for small, short animated graphics.
  - Sure, but for this case animated AVIF will perform better. HEVC will perform better still.
- Using a video file for 5-10 frames is overkill.
  - File size, loading a video player on the website, having the user press play to start it... 
  - An image just works in all browsers, 1-3 second for help article that shows where to click is one example, memes another. I don't expect a video to last 3 seconds.
- Videos can autoplay. 
  - Most "gif" websites are actually using video, because it performs better.
  - File size will be smaller. You don't need to load a video player, it's built into the browser.
- I might actually look into WebM now as the size reduction is quite impressive. I wish more creators desktop tools supported the format, since it's probably time to move to WebP and WebM for the web. Bandwidth savings can be huge.
  - In terms of images, AVIF significantly outperforms WebP. 
  - WebM is just a container format. The video format I used was VP9, which 10 years old. HEVC would perform even better. Animated AVIF was 9 kb, since it's alpha support is unoptimised.
