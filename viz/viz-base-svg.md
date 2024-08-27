---
title: viz-base-svg
tags: [svg, viz, web]
created: 2019-08-01T05:10:56.452Z
modified: 2020-12-21T07:46:58.910Z
---

# viz-base-svg

# guide

- web-animations-js 提供了支持svg元素动画的polyfill
  - 浏览器本身支持svg使用WAAPI实现动画
  - 但可能只支持一部分，如Edge对svg transform支持不完善
  - [Animating strokeWidth doesn't work in Safari](https://github.com/web-animations/web-animations-js/issues/217)
# tools-svg
- online-editor
  - https://www.svgviewer.dev/

- online-viewer
# pieces
- Not all svg attributes can be manipulated with CSS. Only those designated as "properties" can be changed with CSS and animated.
- Do not try manipulate the properties of SVG elements until SVG 2.0 standard release. (working only Chrome correctly)
- ref
  - [SVG animate Web animate API](https://stackoverflow.com/questions/51985634/svg-animate-web-animate-api)
# svg-grammar
- transform  
  - translate(x, y)  
  - 不提供y时，默认y为0  

- 坐标变换    
  - 在每个SVG元素对象上，都有一个getScreenCTM()的方法，它会返回一个SVGMatrix来表示元素的坐标系所做过的变换。  
  - 此外SVG还有一种SVGPoint类型，它有x和y两个属性可以表示任一一个点，同时它还有一个matrixTransform()方法可以将点跟某个SVGMatrix相乘得到相应矩阵变换后的点。  
  - 通过这些再加上一些线性代数的知识，就可以轻松的进行坐标系的变换了。  
  - 要注意的是SVGPoint只能通过svg元素对象的createSVGPoint()来创建，不能用new SVGPoint()这样的方式。

- viewBox 视图框  
  - `<svg width="500" height="200" viewBox="0 0 50 20" >`
  - 500x200像素视口的 `<svg>` 元素内部使用从0, 0到50, 20的坐标系。  
  - `<svg>` 内的图形上的坐标系每一个单位对应于宽度上的500/50=10像素和高度上的200/20=10像素。

- preserveAspectRatio  
  - 属性采用由空格分割的两个值，告诉视图框如何在视口内对齐，这个值本身由两部分组成    
  - 第二个值（如果有的话）指示如何保留宽高比，可选值meet, slice, none
# svg-community

## [为什么svg格式在前端设计中未能普及？](https://www.zhihu.com/question/21376597)

- 总的来说svg在静态icon上是未来王者，在动画方面是优势利剑，在文字排版，定位布局及滤镜效果上难普及。

### svg-优缺点

- 优点
1. 用户可以任意缩放图像显示，而不会破坏图像的清晰度、细节等。 
2. SVG图像中的文字独立于图像，文字保留可编辑和可搜寻的状态。也不会再有字体的限制，用户系统即使没有安装某一字体，也会看到和他们制作时完全相同的画面。 
3. 总体来讲，SVG文件比那些GIF和JPEG格式的文件要小很多，因而下载也很快。 
4. SVG图像在屏幕上总是边缘清晰，它的清晰度适合任何屏幕分辨力和打印分辨力。 
5. SVG图像提供一个1600万种颜色的调色板，支持ICC颜色描述文件标准、RGB、线X填充、渐变和蒙版。 
6. 交互X和智能化。SVG面临的主要问题一个是如何和已经占有重要市场份额的矢量图形格式Flash竞争的问题，另一个问题就是SVG的本地运行环境下的厂家支持程度。

 

- 缺点
1. DOM比正常的图形慢，而且如果其结点多而杂，就更慢。
2. SVG画点报表还可以；在网页游戏前，就束手无策了，可以结合Canvas+SVG来实现。 
3. 不能动态的修改动画内容。 
4. 可惜的是，svg不是所有浏览器都能支持，目前他的支持情况：Internet Explorer 9、Firefox、Opera、Chrome 以及 Safari 支持内联 SVG。 

- 总的来说svg在静态icon上是未来王者，在动画方面是优势利剑，在文字排版，定位布局及滤镜效果上难普及。
# svg-blogging

## [Why you should use SVG images: how to animate your SVGs and make them lightning fast](https://www.freecodecamp.org/news/a-fresh-perspective-at-why-when-and-how-to-use-svg/)

- Benefits of SVG
  - Scalable
  - high performance with inline svg, no HTTP request
  - small size

- How to Animate SVG
  - SMIL, which is the native SVG animation specification
  - Web Animations API, which is a native JavaScript API allowing you to create more complex sequential animations without loading any external scripts
  - ​WebGL
  - CSS animation

- CSS animation is used in order to avoid overloading your service with big libraries for animating icons and loaders.
- benefits of using the CSS approach to SVG animation:
  - You do not need an external library.
  - Preprocessors (like Sass or Less) allow you to create variables.
  - You can use onAnimationEnd and some other animation hooks with native JavaScript.
  - This approach is easy to use for responsive web design development because you can modify your animation with media queries.
- downsides of using CSS animation are the following:
  - You cannot produce some complex physics effects, which would make the animation more realistic.
  - A lot of recalculation needs to be done if you adjust timing.
  - CSS and SVG graphics on mobile sometimes require strange hacks.

## [Animating SVG with CSS_201904](https://blog.logrocket.com/animating-svg-with-css-83e8e27d739c/)

- Now, you may be wondering: Why CSS? Why not animate with SMIL, the native SVG animation specification? 
  - As it turns out, there’s declining support for SMIL. 
  - Chrome is heading in the direction of deprecating SMIL in favor of CSS animations and the Web Animations API. 
  - So, on we go with CSS animations
- How to prepare SVGs
  - Simplify the SVG code
  - Create intentional groupings (if needed)
    - If you want to animate a group of elements together, wrap them in `<g></g>` , and name them with a class or ID. 
  - Beware of stacking order 
    - if you’ll be animating a shape that is going behind another shape
  - Set SVG styling to the preferred, initial state
- Applying CSS to SVGs
  - Option 1: Embed the SVG code inline in the HTML (my favorite)
    - This makes the SVG element and its contents part of the document’s DOM tree, so they’re affected by the document’s CSS. 
    - This is my favorite because it keeps the styles separate from the markup.
    - An added benefit of this method is that inlining the SVG means there’s one less HTTP request.
  - Option 2: Include the CSS in the SVG within a `<style>` tag
    - You can add CSS styles in a `<style>` tag, nested within the `<svg>` tag.
  - Option 3: Include the CSS in the SVG with an external link
    - If you’d like to keep the styling referenced in the SVG, but not actually include it within the SVG, you can use the `<?xml-stylesheet>` tag to link to an external style sheet from the SVG
  - Option 4: Use inline CSS styles in the SVG
    - CSS may also be set on an element using inline `style` attributes. 

- Transition property
  - For animations triggered on load or by a state change, such as hover or click, you can use the `transition` property. 
  - The `transition` property allows property values to change smoothly over a specified duration. 
  - Without it, the change would happen in an instant, creating a jaring look.
  - A limitation of the `transition` property is that it doesn’t give much control over what changes happen during the timeline.

- Animation property
  - For further control, use the animation property.
  - Use the ` @keyframes` at-rule to tell it how to change at intermediary steps.

## [Animating SVG with CSS_2014](https://css-tricks.com/animating-svg-css/)

- There isn’t just one way to animate SVG. 
  - There is the `<animate>` tag that goes right into the SVG code. 
  - There are libraries that help with it like `Snap.svg` or `SVG.js` . 
  - We’re going to look at another way: using inline SVG (SVG code right inside HTML) and animating the parts right through CSS.

## [Styling And Animating SVGs With CSS_2014](https://www.smashingmagazine.com/2014/11/styling-and-animating-svgs-with-css/)

- Scalable vector graphics (SVG) is an XML-based vector image format for two-dimensional graphics, with support for interactivity and animation. 
- In other words, SVGs are XML tags that render shapes and graphics, and these shapes and graphics can be interacted with and animated much like HTML elements can be.
- Animations and interactivity can be added via CSS or JavaScript. In this article, we’ll focus on CSS.
- The line between HTML and CSS is clear: HTML is about content and structure, and CSS is about the look. 
- SVG blurs this line, to say the least. SVG 1.1 did not require CSS to style SVG nodes — styles were applied to SVG elements using attributes known as “presentation attributes.”
- Presentation attributes are a shorthand for setting a CSS property on an element. Think of them as special style properties. They even contribute to the style cascade, but we’ll get to that shortly.
- The `fill` ,  `stroke` and `stroke-width` attributes are presentation attributes.
- In SVG, a subset of all CSS properties may be set by SVG attributes, and vice versa. 
- The SVG specification lists the SVG attributes that may be set as CSS properties. 
- Some of these attributes are shared with CSS, such as `opacity` and `transform` , among others, while some are not, such as `fill` ,  `stroke` and `stroke-width` , among others.
- In SVG 2, this list will include x, y, width, height, cx, cy and a few other presentation attributes that were not possible to set via CSS in SVG 1.1. The new list of attributes can be found in the SVG 2 specification.
- Another way to set the styles of an SVG element is to use CSS properties in `style` attribute. 
- Indeed, presentation attributes count as low-level “author style sheets” and are overridden by any other style definitions: external style sheets, document style sheets and inline styles.
- Most CSS selectors can be used to select SVG elements
- Because presentation attributes are expressed as XML attributes, they are case-sensitive.
- **SVGs can be animated the same way that HTML elements can, using CSS keyframes and animation properties or using CSS transitions**.
- Note that, at the time of writing, CSS 3D transformations are not hardware-accelerated when used on SVG elements; 
  - they have the same performance profile as SVG transform attributes. 
  - However, Firefox does accelerate transforms on SVGs to some extent.
- There is no way to animate an SVG path from one shape to another in CSS. 
  -  If you want to morph paths — that is, animate from one path to another — then you will need to use JavaScript for the time being. 
  -  If you do that, I recommend using Snap.svg 
- Snap.svg is described as being to SVG what jQuery is to HTML, and it makes dealing with SVGs and its quirks a lot easier.
- An SVG can be embedded in a document in six ways, each of which has its own pros and cons.
  - as an image using the `<img>` tag
  - as a background image in CSS
  - as an object using the `<object>` tag
  - as an iframe using an `<iframe>` tag
  - using the `<embed>` tag
  - inline using the `<svg>` tag
- The `<object>` tag is the primary way to include an external SVG file. 
  - The main advantage of this tag is that there is a standard mechanism for providing an image (or text) fallback in case the SVG does not render.
  - If you intend using any advanced SVG features, such as CSS or scripting, the then HTML5 `<object>` tag is your best bet.
- An SVG can also be embedded in a document inline — as a “code island” — using the `<svg>` tag. 
  - This is one of the most popular ways to embed SVGs today. 
  - Working with inline SVG and CSS is a lot easier because the SVG can be styled and animated by targeting it with style rules placed anywhere in the document. 
  - That is, the styles don’t need to be included between the opening and closing `<svg>` tags to work; whereas this condition is necessary for the other techniques.
  - Also, note that an inline SVG cannot be cached.
- After embedding an SVG, you need to make sure it is responsive.
  - Whichever technique you choose, the first thing you’ll need to do is remove the `height` and `width` attributes from the root `<svg>` element.
  - You will need to preserve the `viewBox` attribute and set the `preserveAspectRatio` attribute to `xMidYMid meet`
- SVG accepts and responds to CSS media queries as well. 
  - You can use media queries to change the styles of an SVG at different viewport sizes.
  - note that the viewport that the SVG responds to is the viewport of the SVG itself, not the page’s viewport, unless you are embedding the SVG inline in the document (using `<svg>` ).
# ref
- [Appendix H: SVG Property Index](https://www.w3.org/TR/SVG/propidx.html)
- [Appendix D: Animating SVG Documents](https://www.w3.org/TR/SVG2/animate.html)

- [A Generative SVG Starter Kit](https://dev.to/georgedoescode/a-generative-svg-starter-kit-5cm1)

- [SVG基础及其动画应用浅析](https://zhuanlan.zhihu.com/p/383245453)
