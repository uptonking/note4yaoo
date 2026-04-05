---
title: spec-office-pdfjs
tags: [pdfjs]
created: 2026-04-05T20:12:19.452Z
modified: 2026-04-05T20:12:26.553Z
---

# spec-office-pdfjs

# guide

# dev-xp

# more

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss-tips
- ## 

- ## 

- ## 

- ## [Retrieve bounding box of text on a page _202501](https://github.com/mozilla/pdf.js/issues/5643)
  - I would like to determine the margins of the text in a PDF document. One possibility would be to render the PDF and look at the text layer of each page, specifically the positionins of their div children (which represent rows of text). That strikes me as a little too cumbersome, though. Is there a way to retrieve the bounding box of all text on a page from the PDFJS object?
- You would want to use getTextContent()  instead -- it is used by TextLayerBuilder. TextItem has transform and width/height
- PDF user unit, you have to use PageViewport to map it to the screen presentation

- For others digging around for what pdf.js is actually doing with transformation vectors, the PDF Reference includes a definition of how transformation vectors are laid out and how they relate to mapping into a two dimensional coordinate space.
# discuss-bbox/anno/highlighting
- ## 

- ## 

- ## 

- ## [How to highlight sentence over multiple lines? · Issue · wojtekmaj/react-pdf _202007](https://github.com/wojtekmaj/react-pdf/issues/614)
- Implement `customTextRenderer` to hook into text rendering mechanism

- here is a working solution
  - Step 1: Extract Text Content from PDF Pages
  - Step 2: Understanding the Transform Matrix (Affine Transformation)
  - Step 3: Finding Multi-Line Text Matches
  - Step 4: Creating a Custom Highlight Layer
  - Step 5: Calculate Precise Highlight Positions
  - Step 6: Putting It All Together
  - Takeaways
  - Text items are individual fragments - text on multiple lines = multiple items
  - Transform matrices contain position data - element [3] is font size, [4] is X, [5] is Y
  - Everything must be scaled - multiply all dimensions by the page scale
  - Character-level precision - divide text width by string length for approximation

- [Highlighting by rectangle bounds and not text _202204](https://github.com/wojtekmaj/react-pdf/discussions/980)
  - I've tried the recipe for highlighting text here. It works fairly well, but it does not work with multiple lines. Lets say I know the bounds of a rectangle on a specified page (or I know multiple bounds), Is there a way to highlight by these bounds instead of matching text?
- You can use `canvasRef` prop to draw whatever you want on a given canvas. Here's an example with watermark added dynamically
# discuss
- ## 

- ## 

- ## 

- ## 
