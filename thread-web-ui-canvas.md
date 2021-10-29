---
title: thread-web-ui-canvas
tags: [canvas, thread, ui]
created: '2021-08-06T07:35:46.825Z'
modified: '2021-08-06T07:36:05.864Z'
---

# thread-web-ui-canvas

# guide
- https://github.com/tldraw/core
  - This package contains the Renderer and core utilities used by tldraw.
  - You can use this package to render React components in a canvas user interface.
# discuss
- ## 

- ## 

- ## 

- ## The perfect-freehand algorithm starts from scratch every time, with nothing kept in memory, and this makes it both inefficient (in a minor way) but more importantly limited in what it can do.
- https://twitter.com/steveruizok/status/1444397702251429890
  - In other words, if you're drawing with perfect-freehand, you're re-computing all of the points on every frame, even if most of those points come back the same each time. That repeated work could be saved, making the 1000th point as expensive as the 10th point.
  - I really am re-writing this
- For 90% of use cases, that's no problem—and it usually takes very long lines with 1000s of points before the algorithm causes any performance issues. So yeah, a little 'inefficient' but it's fast and O(n), and honestly easier to use than managing something that sits in memory.
  - But as far as features go, its limited because the points given back by perfect-freehand don't know their relationship to other points, or to their input point—and this makes features like erasing very difficult to implement. I've had lots of folks ask me about this.
- PS. it's also MUCH more easy to start from scratch each time than it is to manage nodes and linked lists of outline points. Tapering and corners are especially difficult, as these can change as points are added or options change (both could use their own threads tbh)

- ## right now the minimap is part of the renderer, but it really works like its own renderer, and may make more sense as something entirely separate. 
- https://twitter.com/steveruizok/status/1441472275639832577
  - This would make it easier to style or place (or not include)
- The renderer is an infinite canvas and so this minimap is positioning things relative to the “expanded bounds”, ie the bounding box that fits around all of the other bounding boxes. Which makes for some cool visuals as that changes.
  - We normally only “render” shapes that are on screen, but this needs to render shapes that are off screen too. Which could be a performance issue? Even if the shapes render more simple elements into an SVG, it still might be a lot of elements.

- ##  When we made a shape, we need to make the the bounding box a little bigger than the shape itself.
- https://twitter.com/steveruizok/status/1437514372520284163
  - SVGs clip their content, so if the shape is rendering an SVG image (like this one is), we want to leave some padding in case there's any overlap.
  - We might improve this by doing a better job of calculating the bounding box: we could use the freehand shape's points, rather than the input points. To get it *really* right, we'd need to use the curves between each point. Not worth it imo
- We adjust this padding based on the camera scale. This helps us leave room for the bounding box and any other controls we might want to put there.
  - But how we calculate the bounding box does matter. On the arrow, I'm calculating a box based on the three handles. Looks like that's the wrong approach!
- Previously, I’ve been using a measurement div to get the size and shape of text layers content. But now that shapes are components, we can get the size data from inside of the shape’s component!

- ## Starting to feel like the @tldraw engine really wants to be a “render react components in a canvas paradigm” engine.
- https://twitter.com/steveruizok/status/1435515509756338177
  - This isn’t too far from what it is currently. Right now you’re limited to only elements that can go inside of an svg `<g>` tag.
- One of the limitations with that canvas is the limited way that a custom/code component could behave on the canvas. Components with nonstandard behaviors, like their Graphics shape, were all baked in.
- So more work for the lab. As with all hobby projects, part of the fun is seeing where things go—and if @tldraw points to a “next” project, then I think that project would be a similarly generic “interactive canvas for components”.

- ## Just pushed a BIG update to @tldraw
- https://twitter.com/steveruizok/status/1434190045238472704
  - a full rewrite, six weeks in the making, that includes new faster state management, an architecture made up of three packages, and tons of bug fixes and improvements.
- The whole app is built on the @tldraw/core package, which is an excellent renderer for custom primitives. 
  - It's fast and efficient—but there's still plenty of room for improvement, too. 
- Me: Decides on the button variants for 6 weeks

- ## Shapes in @tldraw are essentially React components with extra methods for hit testing, bounds calculation, etc. So what’s the best way of organizing that?
- https://twitter.com/steveruizok/status/1436982621528109061
- I think my current solution is confusing. To define a shape, you write a “shape utils” class that overrides certain utility methods that will be used for all shapes of that type in the project.
  - In the data model, shapes are stored as plain objects. We use the shape’s utils class (as a singleton) to answer questions about shapes of that type: given this shape, what are its bounds? Given this shape and this transformation, what should we change?
  - We also use the shape utils class to render the shape. Its “render” method (likely to be renamed) is a React ForwardRefExoticComponent to that receives a shape and some contextual info (hovered?) as props.
  - So far it would sound like all of those class methods could be static. But we also use caches for things like bounds, or sometimes path data, depending on what’s efficient for that kind of shape. Which means we need that singleton model, I think, to access the mutable data.
  - I could put this mutable stuff outside of the class… but then if a page had more than one `<TLDraw>` component, then they would both share their caches. Maybe this doesn’t matter?
  - It would be easier if the whole model was OOP (storing instances of a shape class rather than using objects+utilities), but that’s tough to make work with React.
- I like to separate data model and React render tree just because it’ll be cleaner in the long term. It’s easy to write an adapter hook if your data model supports listening on changes on a per-entity level. 
  - Same, I currently have the store in a zustand store. Though for multiplayer I might need to move to some more multiplayery data structures
  - Yeah you may just wanna use Yjs for the entire in-memory data structure (storage after multiplayer is closed could still be something else tho).
- I generally store everything as plain objects so they are easily serialisable for structured clone algorithm and stringify.

- ## here's one of the quirkiest browser quirks for a canvas-type of a UI
- https://twitter.com/steveruizok/status/1436816229268959241
  - If an absolutely positioned text elements changes its width in a way that would cause the cursor to go off screen, the browser automatically scrolls the container to the cursor's location. 
  - It doesn't matter if you've set overflow to hidden—the container is going to scroll!
  - The only fix I've found is to use the element's onScroll to reset the scroll if it ever happens.
  - This allows the cursor to go offscreen, which is alright IMO. On each keystroke, the browser is scrolling the container and then we are **synchronously resetting the scroll**. Problem solved, I hope!
- Ugh, it's similar to inserting dom at the end of an page that is scrolled to the bottom, most browsers will increase the scroll top offset.

- ## Just found React Designer for the first time. Wild how similar their API is to what I'm doing with @tldraw 
- https://twitter.com/steveruizok/status/1423631926884196352
  - in both cases, it's "here are my objects" and "here are some classes used to interpret those objects"
- https://github.com/react-designer/react-designer /CC BY 4.0
  - Easy to configure, lightweight, editable vector graphics in your react components.

- ## here's a blog post about how to create a "zoom ui" (aka a "canvas ui") where a user can pan and zoom around.
- https://twitter.com/steveruizok/status/1423326505011195907
  - [Creating a Zoom UI](https://www.steveruiz.me/posts/zoom-ui)
- You might also consider something like https://pixijs.com which offers all of this stuff out of the box on a OpenGL accelerated "canvas".
  - Does Pixi have its own zoom UI system? Last time I used it it did not (though I loved Pixi for other reasons). Two.js does ship with some started zoom ui code though
