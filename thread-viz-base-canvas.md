---
title: thread-viz-base-canvas
tags: [canvas, thread, viz]
created: 2021-03-11T11:24:51.292Z
modified: 2021-03-11T11:25:59.200Z
---

# thread-viz-base-canvas

# guide

- [Can I turn off antialiasing on an HTML `<canvas>` element? - Stack Overflow](https://stackoverflow.com/questions/195262/can-i-turn-off-antialiasing-on-an-html-canvas-element/67800821)
  - Antialiasing is required for correct plotting of vector graphics that involves non-integer coordinates (0.4, 0.4), which all but very few clients do.
  - `imageSmoothingEnabled` applies to pattern `fill`s and `drawImage`, it does not affect general anti-aliasing.
# discuss
- ## 

- ## 

- ## 

- ## Today I learned that a JavaScript canvas automatically antialiases whatever you draw! (and you can't turn it off)
- https://twitter.com/Omar4ur/status/1692941855661416602
  - The right circle here is de-antialiased by postprocessing the pixel data and removing anything that is alpha < 255
- That doesn't sound right. Surely it should reduce the alpha of anything under 128 to 0 and increase anything greater than or equal to 128 to full opaque.
- Remove anything <= 127 and set alpha of anything > 127 to 255. Antialiasing typically doesn't just add semi-transparent pixel outside the boundary of the binary shape but also makes some pixels inside the boundary semi-transparent.
- Try ctx.imageSmoothingEnabled = false
  - Doesn't work for fillRect etc!
  - hmm, try to round coordinates while drawing shapes (42.69, 42.69) -> (42, 42)
- I am usually pretty happy with browser APIs & the tradeoffs they're making! But here I really am surprised how much is happening under the hood you can't control 
- Is drawing inside those createimagedata arrays a solution?
  - Yeah if you create the image data manually and putImageData to canvas you can get around it (which is how I got the circle on the right!)
- Wait till you find out that the browser stores pixels as 8-bit premultiplied and then lies to you by silently un-multiplying color values when you read them back, which actually corrupts the colors of near-transparent pixels, and you can't turn this off

- ## Only 2% of all canvases use a WebGL rendering context.
- https://twitter.com/mrdoob/status/1499874260415926276
