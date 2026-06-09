---
title: lib-ai-ml-cv
created: 2026-02-19T14:38:16.543Z
modified: 2026-02-19T14:38:28.823Z
---

# lib-ai-ml-cv

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-segmentation
- ## 

- ## 

- ## 

- ## 

- ## [[Remote Sensing] How do you segment individual trees in dense forests? (My models just output giant "blobs") : r/computervision _202602](https://www.reddit.com/r/computervision/comments/1r8vzm6/remote_sensing_how_do_you_segment_individual/)
  - I've tested several approaches on standard orthophotos, but I always run into the same issues:
  * Manual: It's incredibly time-consuming, and the border between two trees is often impossible to see with the naked eye.
  * Classic Algorithms (e.g., Watershed): Works great for isolated trees in a city, but in a dense forest, the algorithm just merges everything together.
  * AI Models (Computer Vision): I've tried segmentation models, but they always output giant "blobs" that group 10 or 20 trees together, without separating the individual crowns.

- Another thing you might consider is temporal data, assuming you have good quality geolocation. Differences in colour change or leaf loss, or simply looking at your images in autumn when there are fewer leaves, may help.

- i would recommend a research on "cell segmentation" models. From top view it indeed looks a lot like cell seg problem, and instance segmentation is a necessity in this area exactly because cells tend to form dense blobs.
  - The short answer is: It's hard as hell. The way i solved this in my masters was create a diffusion map for each individual cell from the segmentations ground truth, and teach the model this diffusion map instead of regular segmentation. Each difusion peak turned into a singular instance and watershed segmentation to separate the masks.
# discuss-solutions
- ## 

- ## 

- ## 

- ## 

- ## Roboflow 把多目标追踪彻底开源
- https://x.com/berryxia/status/2037755337537982923
  - 任意检测器即插即用（YOLO / RF-DETR / 随便接）
- https://github.com/roboflow/trackers /3.2kStar/apache2/202603/python
  - https://trackers.roboflow.com/
  - Plug-and-play multi-object tracking for any detection model.

# discuss-models-object-detection
- ## 

- ## 

- ## 

- ## 

- ## I am working on porting SAM models and harness into Apple silicon. 
- https://x.com/neural_avb/status/2056094418013433895
  - Already seeing 1.25x inference speed increase on mlx with the sam2.1-small model. Quantized versions soon.

- Ive played with mlx vlm sam-3.1! I wanted to do some off the cuff experiments for a new project. I’m mainly doing it with Sam 2 and soon some grounding Dino and pointing models.
# discuss-tools-opencv
- ## 

- ## 

- ## 

- ## 

- ## OpenCV 5 is  here _202606
- https://x.com/mfranz_on/status/2064379347478163704
  - Brand new DNN engine with 80%+ ONNX coverage
  - Built-in LLM & VLM support
  - Faster performance (often beating ONNX Runtime)
  - Better 3D vision, Python integration, and hardware acceleration 

- cv is the other face of the AI but it can be used also without an ML approach. You can obtain production ready results just with the old but gold cv algos
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
