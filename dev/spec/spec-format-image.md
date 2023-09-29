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

- ## 
