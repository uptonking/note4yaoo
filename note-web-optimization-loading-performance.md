---
tags: [browser, optimization, web]
title: note-web-optimization-loading-performance
created: '2020-06-28T12:12:28.341Z'
modified: '2020-07-10T07:56:45.232Z'
---

# note-web-optimization-loading-performance

## guide

- https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction
- https://developers.google.com/web/fundamentals/performance/critical-rendering-path/constructing-the-object-model

## Critical Rendering Path

- Optimizing the critical rendering path refers to prioritizing the display of content that relates to the current user action.
- Optimizing for performance is all about understanding what happens in these intermediate steps between receiving the HTML, CSS, and JavaScript bytes and the required processing to turn them into rendered pixels - that's the **critical rendering path**.
- By optimizing the critical rendering path we can significantly improve the time to first render of our pages
- Further, understanding the critical rendering path also serves as a foundation for building well-performing interactive applications. 

## Constructing the Object Model

- Tips
  - Bytes → characters → tokens → nodes → object model.
  - HTML markup is transformed into a Document Object Model (DOM); CSS markup is transformed into a CSS Object Model (CSSOM).
  - DOM and CSSOM are independent data structures.
  - Chrome DevTools Timeline allows us to capture and inspect the construction and processing costs of DOM and CSSOM.
- Before the browser can render the page, it needs to construct the DOM and CSSOM trees. 
- We need to ensure that we deliver both the HTML and CSS to the browser as quickly as possible.
- **Document Object Model (DOM)**
  - Let’s start with the simplest possible case: a plain HTML page with some text and a single image. How does the browser process this page
  1. Conversion
    - The browser reads the raw bytes of HTML off the disk or network, and translates them to individual characters based on specified encoding of the file (for example, UTF-8).
  2. Tokenizing
    - The browser converts strings of characters into distinct tokens—as specified by the W3C HTML5 standard; for example, `<html>` , `<body>` —and other strings within angle brackets. 
    - Each token has a special meaning and its own set of rules.
  3. Lexing
    - The emitted tokens are converted into "objects," which define their properties and rules.
  4. DOM construction
    - Finally, because the HTML markup defines relationships between different tags (some tags are contained within other tags), the created objects are linked in a tree data structure that also captures the parent-child relationships defined in the original markup: the HTML object is a parent of the body object, the body is a parent of the paragraph object, and so on.
  - The final output of this entire process is the Document Object Model (DOM) of our simple page, which the browser uses for all further processing of the page.
  - Every time the browser processes HTML markup, it goes through all of the steps above: convert bytes to characters, identify tokens, convert tokens to nodes, and build the DOM tree. 
  - The DOM tree captures the properties and relationships of the document markup, but it doesn't tell us how the element will look when rendered
  - If you open up Chrome DevTools and record a timeline while the page is loaded, you can see the actual time taken to perform this step from *Parse HTML* tab.
- **CSS Object Model (CSSOM)**
  - While the browser was constructing the DOM of our simple page, it encountered a `<link>` tag in the head section of the document referencing an external CSS stylesheet: `style.css`
    - It immediately dispatches a request for this resource
  - As with HTML, we need to convert the received CSS rules into something that the browser can understand and work with. Hence, we repeat the HTML process, but for CSS instead of HTML
  - The CSS bytes are converted into characters, then tokens, then nodes, and finally they are linked into a tree structure known as the CSS Object Model(CSSOM)
  - Why does the CSSOM have a tree structure? 
    - When computing the final set of styles for any object on the page, the browser starts with the most general rule applicable to that node (for example, if it is a child of a body element, then all body styles apply) 
    - and then recursively refines the computed styles by applying more specific rules; that is, the rules "cascade down."
    - Every browser provides a default set of styles also known as "user agent styles"
      - that’s what we see when we don’t provide any of our own
      - and our styles simply override these defaults.
  - To find out how long the CSS processing takes, you can record a timeline in DevTools and look for "Recalculate Style" event
    - It captures parsing and CSSOM tree construction, plus the recursive calculation of computed styles under this one event.

## Render-Tree Construction, Layout, and Paint

- Tips
  - The DOM and CSSOM trees are combined to form the render tree.
  - Render tree contains only the nodes required to render the page.
  - Layout computes the exact position and size of each object.
  - The last step is paint, which takes in the final render tree and renders the pixels to the screen.
- The CSSOM and DOM trees are combined into a render tree, which is then used to compute the layout of each visible element and serves as an input to the paint process that renders the pixels to screen
- Optimizing each of these steps is critical to achieving optimal rendering performance.
- First, the browser combines the DOM and CSSOM into a "render tree, " which captures all the visible DOM content on the page and all the CSSOM style information for each node.
  1. Starting at the root of the DOM tree, traverse each visible node.
    - Some nodes are not visible (for example, script tags, meta tags, and so on), and are omitted since they are not reflected in the rendered output.
    - Some nodes are hidden via CSS and are also omitted from the render tree; for example, the span node---in the example above---is missing from the render tree because we have an explicit rule that sets the "display: none" property on it.
    - note that `visibility: hidden` is different from `display: none` . 
      - The former makes the element invisible, but the element still occupies space in the layout (that is, it's rendered as an empty box)
      - the latter ( `display: none` ) removes the element entirely from the render tree such that the element is invisible and is not part of the layout.
  2. For each visible node, find the appropriate matching CSSOM rules and apply them.
  3. Emit visible nodes with content and their computed styles.
  - The final output is a render that contains both the content and style information of all the visible content on the screen.
  - With the render tree in place, we can proceed to the "layout" stage.
- Up to this point we've calculated which nodes should be visible and their computed styles, but we have not calculated their exact position and size within the viewport of the device---that's the "**layout**" stage, also known as "**reflow**."
  - To figure out the exact size and position of each object on the page, the browser begins at the root of the render tree and traverses it.
  - The output of the layout process is a "box model, " which precisely captures the exact position and size of each element within the viewport: all of the relative measurements are converted to absolute pixels on the screen.
- Finally, now that we know which nodes are visible, and their computed styles and geometry, we can pass this information to the final stage, which converts each node in the render tree to actual pixels on the screen. This step is often referred to as "**painting**" or "rasterizing."
- Chrome DevTools can provide some insight into all three of the stages described above.
  - The "Layout" event captures the render tree construction, position, and size calculation in the Timeline.
  - When layout is complete, the browser issues "Paint Setup" and "Paint" events, which convert the render tree to pixels on the screen.
  - The time required to perform render tree construction, layout and paint varies based on the size of the document, the applied styles, and the device it is running on
- Here's a quick recap of the browser's steps:
  1. Process HTML markup and build the DOM tree.
  2. Process CSS markup and build the CSSOM tree.
  3. Combine the DOM and CSSOM into a render tree.
  4. Run layout on the render tree to compute geometry of each node.
  5. Paint the individual nodes to the screen.

## Render Blocking CSS

- Tips
  - By default, CSS is treated as a render blocking resource.
  - Media types and media queries allow us to mark some CSS resources as non-render blocking.
  - The browser downloads all CSS resources, regardless of blocking or non-blocking behavior.
- By default, CSS is treated as a render blocking resource, which means that the browser won't render any processed content until the CSSOM is constructed. 
  - Make sure to keep your CSS lean, deliver it as quickly as possible, and use media types and queries to unblock rendering.
- Both HTML and CSS are render blocking resources. 
  - The HTML is obvious, since without the DOM we would not have anything to render, 
  - but the CSS requirement may be less obvious. 
- Without CSS the page is relatively unusable. 
  - The experience on the right is often referred to as a "Flash of Unstyled Content" (FOUC).
  -  The browser blocks rendering until it has both the DOM and the CSSOM.
- CSS is a render blocking resource. 
  - Get it to the client as soon and as quickly as possible to optimize the time to first render.
- By using media queries, we can tailor our presentation to specific use cases, such as display versus print, and also to dynamic conditions such as changes in screen orientation, resize events, and more. 
- When declaring your style sheet assets, pay close attention to the media type and queries; they greatly impact critical rendering path performance
- The third declaration `<link href="portrait.css" rel="stylesheet" media="orientation:portrait">` has a dynamic media query, which is evaluated when the page is loaded. 
  - Depending on the orientation of the device while the page is loading, `portrait.css` may or may not be render blocking.
- The last declaration `<link href="print.css"  rel="stylesheet" media="print">` is only applied when the page is being printed so it is not render blocking when the page is first loaded in the browser.
- Finally, note that "render blocking" only refers to whether the browser has to hold the initial rendering of the page on that resource. The browser still downloads the CSS asset, albeit(although) with a lower priority for non-blocking resources.

## Adding Interactivity with JavaScript

- Tips
  - JavaScript can query and modify the DOM and the CSSOM.
  - JavaScript execution blocks on the CSSOM.
  - JavaScript blocks DOM construction unless explicitly declared as async.
- JavaScript allows us to modify just about every aspect of the page: content, styling, and its response to user interaction. 
- However, JavaScript can also block DOM construction and delay when the page is rendered.
- To deliver optimal performance, make your JavaScript async and eliminate any unnecessary JavaScript from the critical rendering path
- Put inline script near the bottom of the page. 
- Our script is executed at the exact point where it is inserted in the document. 
- When the HTML parser encounters a `<script>` tag, it pauses its process of constructing the DOM and yields control to the JavaScript engine; 
- after the JavaScript engine finishes running, the browser then picks up where it left off and resumes DOM construction.
- Executing our inline script blocks DOM construction, which also delays the initial render.
- What if the browser hasn't finished downloading and building the CSSOM when we want to run our script? 
  - The answer is simple and not very good for performance
  - The browser delays script execution and DOM construction, until it has finished downloading and constructing the CSSOM.
- The location of the script in the document is significant.
- When the browser encounters a script tag, DOM construction pauses until the script finishes executing.
- JavaScript can query and modify the DOM and the CSSOM.
- JavaScript execution pauses until the CSSOM is ready.
- When the browser encounters a script in the document it must pause DOM construction, hand over control to the JavaScript runtime, and let the script execute before proceeding with DOM construction. 
  - In fact, inline scripts are always parser blocking unless you write additional code to defer their execution.
  - Whether we use a `<script>` tag or an inline JavaScript snippet, you'd expect both to behave the same way. 
  - In both cases, the browser pauses and executes the script before it can process the remainder of the document. 
  - However, in the case of an external JavaScript file, the browser must pause to wait for the script to be fetched from disk, cache, or a remote server, which can add tens to thousands of milliseconds of delay to the critical rendering path.
- By default all JavaScript is parser blocking. 
  - Because the browser does not know what the script is planning to do on the page, it assumes the worst case scenario and blocks the parser
  - We can add a signal to the browser that the script does not need to be executed at the exact point where it's referenced.
    - This allows the browser to continue to construct the DOM and let the script execute when it is ready;
    - for example, after the file is fetched from cache or a remote server.
    - `<script src="app.js" async></script>`
- `async` keyword of the script tag tells the browser not to block DOM construction while it waits for the script to become available, which can significantly improve performance

## Analyzing Critical Rendering Path Performance

- So far we've focused exclusively on what happens in the browser after the resource (CSS, JS, or HTML file) is available to process. 
- We've ignored the time it takes to fetch the resource either from cache or from the network. We'll assume the following:
  - A network roundtrip (propagation latency) to the server costs 100ms.
  - Server response time is 100ms for the HTML document and 10ms for all other files.
- An asynchronous script has several advantages:
  - The script is no longer parser blocking and is not part of the critical rendering path.
  - Because there are no other critical scripts, the CSS doesn't need to block the `domContentLoaded` event.
  - The sooner the `domContentLoaded` event fires, the sooner other application logic can begin executing.

## Optimizing the Critical Rendering Path

- To deliver the fastest possible time to first render, we need to minimize three variables:
  - The number of critical resources.
  - The critical path length.
  - The number of critical bytes.
- The general sequence of steps to optimize the critical rendering path is:
  1. Analyze and characterize your critical path: number of resources, bytes, length.
  2. Minimize number of critical resources: eliminate them, defer their download, mark them as async, and so on.
  3. Optimize the number of critical bytes to reduce the download time (number of roundtrips).
  4. Optimize the order in which the remaining critical resources are loaded: download all critical assets as early as possible to shorten the critical path length.

## PageSpeed Rules and Recommendations

- ref
  - https://developers.google.com/web/fundamentals/performance/critical-rendering-path/page-speed-rules-and-recommendations
  - https://developers.google.com/speed/docs/insights/rules

- Eliminate render-blocking JavaScript and CSS
  - To deliver the fastest time to first render, minimize and (where possible) eliminate the number of critical resources on the page, minimize the number of downloaded critical bytes, and optimize the critical path length.
- Optimize JavaScript use
  - JavaScript resources are parser blocking by default unless marked as `async` or added via a special JavaScript snippet. 
  - Parser blocking JavaScript forces the browser to wait for the CSSOM and pauses construction of the DOM, which in turn can significantly delay the time to first render.
  - Avoid synchronous server calls
  - Defer parsing JavaScript
    - defer any non-essential scripts that are not critical to constructing the visible content for the initial render.
  - Avoid long running JavaScript
- Optimize CSS Use
  - Put CSS in the document head
    - Specify all CSS resources as early as possible within the HTML document so that the browser can discover the `<link>` tags and dispatch the request for the CSS as soon as possible.
  - Avoid CSS imports
    - The CSS import (`@import`) directive enables one stylesheet to import rules from another stylesheet file. 
    - However, avoid these directives because they introduce additional roundtrips into the critical path: 
    - the imported CSS resources are discovered only after the CSS stylesheet with the `@import` rule itself is received and parsed.
  - Inline render-blocking CSS
    - consider inlining the critical CSS directly into the HTML document. 
    - This eliminates additional roundtrips in the critical path 
    - and if done correctly can deliver a "one roundtrip" critical path length where only the HTML is a blocking resource.

- PageSpeed Insights Rules
  - Avoid landing page redirects
  - Enable compression
  - Improve server response time
  - Leverage browser caching
  - Minify resources
  - Optimize images
  - Optimize CSS Delivery
  - Prioritize visible content
  - Remove render-blocking JavaScript

- Optimize CSS Delivery
- If the external CSS resources are small, you can insert those directly into the HTML document, which is called inlining. 
- Inlining small CSS in this way allows the browser to proceed with rendering the page. 
- Keep in mind if the CSS file is large, completely inlining the CSS may cause PageSpeed Insights to warn that the above-the-fold portion of your page is too large via Prioritize Visible Content. 
- In the case of a large CSS file, you will need to identify and inline the CSS necessary for rendering the above-the-fold content and defer loading the remaining styles until after the above-the-fold content.
- Example of inlining a small CSS file
```html
<html>
  <head>
    <link rel="stylesheet" href="small.css">
  </head>
  <body>
    <div class="blue">
      Hello, world!
    </div>
  </body>
</html>
```

``` css
// small.css
.yellow {background-color: yellow;}
.blue {color: blue;}
.big { font-size: 8em; }
.bold { font-weight: bold; }
```
- inlined css

``` html
<html>
  <head>
    <style>
      .blue{color:blue;}
    </style>
    </head>
  <body>
    <div class="blue">
      Hello, world!
    </div>
    <noscript id="deferred-styles">
      <link rel="stylesheet" type="text/css" href="small.css"/>
    </noscript>
    <script>
      var loadDeferredStyles = function() {
        var addStylesNode = document.getElementById("deferred-styles");
        var replacement = document.createElement("div");
        replacement.innerHTML = addStylesNode.textContent;
        document.body.appendChild(replacement)
        addStylesNode.parentElement.removeChild(addStylesNode);
      };
      var raf = window.requestAnimationFrame || window.mozRequestAnimationFrame ||
          window.webkitRequestAnimationFrame || window.msRequestAnimationFrame;
      if (raf) raf(function() { window.setTimeout(loadDeferredStyles, 0); });
      else window.addEventListener('load', loadDeferredStyles);
    </script>
  </body>
</html>
```
- Don't inline large data URIs
  - While selective use of small data URIs in your CSS may make sense, inlining large data URIs can cause the size of your above-the-fold CSS to be larger, which will slow down page render time.
- Don't inline CSS attributes
  - Inlining CSS attributes on HTML elements (e.g., `<p style=...>`) should be avoided where possible, as this often leads to unnecessary code duplication. 
  - Further, inline CSS on HTML elements is blocked by default with Content Security Policy (CSP).

