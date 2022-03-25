---
title: thread-web-ui-canvas
tags: [canvas, thread, ui]
created: '2021-08-06T07:35:46.825Z'
modified: '2021-08-06T07:36:05.864Z'
---

# thread-web-ui-canvas

> tldraw/react-three-fiber

# guide
- [Creating a Zoom UI](https://www.steveruiz.me/posts/zoom-ui)
  - "zoom UI" like figma/ps. This pattern lets a user explore a "canvas" of content by panning around the canvas or zooming in on a specific point.
  - an SVG implementation
    - https://codesandbox.io/s/zoom-ui-example-ep0cf
  - the same implementation with HTML canvas
    - https://codesandbox.io/s/zoom-ui-example-canvas-6j3wo

- https://github.com/tldraw/core
  - This package contains the Renderer and core utilities used by tldraw.
  - You can use this package to render React components in a canvas user interface.
# discuss
- ## 

- ## 

- ## Excited to share http://tlslides.com, a fork of @tldraw with some UI modifications to help with creation of slides on an infinite drawing canvas. It's still in early developmen
- https://twitter.com/nayajunimesh/status/1506327522857869314
  - https://github.com/nimeshnayaju/tlslides

- ## I'm only now realizing just how much I got away with by not having shapes nest in tldraw.
- https://twitter.com/steveruizok/status/1503156568380088320
  - I guess there's a reason you're not allowed to select a child and its parent at the same time

- ## ever wondered how to make context aware follow-along cursors? 
- https://twitter.com/0xca0a/status/1495791102884028416
  - it's a bit of a problem because canvas lives in another context than the dom and lifting up state is always awkward. 
  - here's a solution using @pmndrs tunnel-rat: grab state, dig a tunnel
  - https://codesandbox.io/s/basic-demo-forked-5nd0fc
- I wish there was a tunnel lib that supported SSR 😏 (not necessarily for R3f usage)

- ## I'm starting to see some interesting patterns now that the scene graph is headless / separated from the rendering solution, which has its own (and much more complex) graph.
- https://twitter.com/steveruizok/status/1497974253429403648

- graph crew, what do you call graphs where there are two types of edges between the same set of nodes? Are these two separate graphs?
  - https://twitter.com/steveruizok/status/1497852148004052993
- I think it could be described as a labelled multidigraph. But I’d definitely model your use case with two different graphs.

- ## Optimizing FPS of a 2D zoomable canvas built with React+DOM and hit a hard wall: Why does this "Recalculate Style" in the rendering pipeline takes so much time? 
- https://twitter.com/donpark/status/1492972719704477697
  - Is there any chance to improve it? 
  - For reference, @tldraw is also built with React+DOM (SVG) and has the same issue.
- AFAIK this is one of the reasons why Figma renders in a worker thread. Use something like new WebAssembly version of resvg-js to render SVG to canvas. On Chrome, mapped OffscreenCanvas can be used to avoid canvas transfer.
- I’d actually be very surprised if rendering html/svgs to canvas and stamping that over would be faster than the browser just rendering svg?
  - There is known perf issues with large scale svg scenes which is why most teams use webGL instead…because it gives you more control over performance
  - I’ve seen this with SVG (http://globs.design is one big svg and I had to cut corners to get perf decent), but regular dom scenes (eg tldraw) seem alright
- Mixing CSS style attribute w/SVG also spells trouble. Another reason I like resvg is it breaks complex SVG into Micro SVG which could be used as is w/less side-effects or target canvas, WebGL, WebGPU or whatever w/a small bucket of elbow grease. 
- Yeah for sure. We also use a lot of svg assets and just render them via webGL to have more control over perf

- ## Really learning a lot reading through @steveruizok's fantastic #tldraw codebase
- https://twitter.com/aboutgeo/status/1492055746351087637
- overall state management & abstractions. 
  - Abstraction of drawing process as a "session" (if I understood that correctly). 
- Other things similar but slightly different, e.g. abstractions around drawing new shapes vs. editing existing.

- ## I'm going to keep working on @tldraw . I'll be raising money in the new year to build a team and build an open-core platform for spatial canvas apps.
- https://twitter.com/steveruizok/status/1468630454601408518
  - Turns out everyone like an infinite canvas. I'm convinced that many of the next great products will be built on "design tool" paradigms—zoomable canvas, direct manipulation, and real-time multiplayer collaboration.
  - Bad news: these types of applications are incredibly hard to develop! Especially for the web, where there are vanishingly few resources and trade-offs everywhere. It takes a team of experts—and there just aren't enough experts.
  - Good news: spatial UI apps are 90% identical, with hundreds of "table stakes" features and services that can be abstracted away, so that a team focus on their domain problems instead of getting stuck on selection logic, arrow binding, or alignment snapping.
  - and it just so happens that I _love_ working on things like selection logic, arrow binding, and alignment snapping.
- What about the current tldraw app? It's still growing, with new contibutions and users everyday. We'll make it better together and continue to use it as a flagship product built on top of the engine, with a nice cycle of building the core to support new features.

- What do you mean by spacial UI? 
  - This one is also sometimes called a "zoom ui", or "infinite canvas". Think miro / mural / figma, etc.

- ## Hit a snag: deepObserve does not respect transactions —#mobx's way to "batch" multiple changes—so each changing multiple properties creates multiple undos.
- https://twitter.com/steveruizok/status/1489653335829458945
  - The solution is to debounce the listener and collect the patches while debouncing, so that we deliver them all together. We can use a zero-length timeout, since we're just waiting for the event loop to clear.
  - https://codesandbox.io/s/mobx-undo-redo-v3-vx2oo

- ## Here's an even more efficient undo/redo manager in mobx. 
- https://twitter.com/steveruizok/status/1488858696360861696
  - This time, instead of using snapshots/comparisons, we're using `deepObserve` and manually converting the changes it reports to JSON patches.
  - The big advantage here: we don't have to be constantly converting between the observable document and a regular JavaScript object. This gives makes the history much more efficient for performance and memory.
  - How it works: mobx-utils has a function called `deepObserve` that will call its listener whenever an observable changes. It passes along where the change occurred, what the operation was (add/remove/replace), and what the old/new values were.
- I don't plan to keep selection as part of the undo/redo stack. If I did want to do that though, then I'd either make it part of the model, or else a separate stack?

- ## Working on a new Undo/Redo manager that runs on mobx and JSON patches. Here's how it works! 
- https://twitter.com/steveruizok/status/1487052071685734410
  - https://codesandbox.io/s/mobx-undo-redo-kmifv
- In our system, we're tracking changes to a "document". 
  - Each time the document changes, we generate a "snapshot" and compare it with our previous snapshot in order to create a "patch" that describes how to get from the current snapshot back to the previous.
  - These patches are "JSON patches" (http://jsonpatch.com). Each patch is made up of a series of operations that will turn one object into another. In our case, our patches describe all of the operations needed to get from our current snapshot back to our previous snapshot.
  - We store these patches in a "stack". This is a list that has a "pointer" that refers to the current patch. We also keep around a snapshot from our last change (or the initial document, if we haven't changed anything yet).
- When our document changes, we first take a snapshot of the current document 
  - and we compare it against our previous snapshot in order to create a new patch. Again, this patch describes all the steps needed to "undo" the new change.
  - Next, we push the new patch onto the stack and move the pointer up so that it points to our new patch.
  - Finally, we save the snapshot we made of our current document as our new previous snapshot. (We can discard the old previous snapshot.)
  - Now we're ready for the next change!

- To undo a change, we apply the current patch (e.g. the one that the pointer is pointing to) to the current document. Applying a patch performs the patch's operations and will bring the state back to where it was before the most recent change.

- ## Let's talk about edge cases in an undo/redo system.
- https://twitter.com/steveruizok/status/1487072814049943552
  - In our last thread, we looked at basic change, undo and redo operations.
  - What happens if we need to "pause" the undo / redo manager? 

- ## Implemented click detection all the way up to quadruple clicks. 
- https://twitter.com/steveruizok/status/1486716043984736264
- It sort of works like this: each time the user clicks, we fire three events—we fire onPointerDown when they start clicking, then onPointerUp _and_ onClick when the they stop clicking.
  - We also keep track of a clicking state. This starts in "idle" and can be either "idle", "pendingDoubleClick", "pendingTripleClick", "pendingQuadrupleClick", or "overflow".
  - When we a pointer down event, what we do next depends on our current state.
  - If our state is idle, then we change our state to "pendingDoubleClick". We also set a timer for ~450ms. When that time goes off, it will set the state back to "idle"
  - If we get another pointer event while we're still in "pendingDoubleClick", we've got a double click! We first fire a single click, then a double click, then clear the current timer and set a new one that, when it goes off, will advance us to "pendingTripleClick".
  - Repeat for triple click—fire a single click, fire a triple click, clear the timer, move to "pendingQuadrupleClick", and set a new timer.
  - Repeat for quadruple click—fire a click, fire a quadruple click, clear the timer, move to "overflow", and set a new timer.
  - The "overflow" state is special! The overflow state prevents us from firing additional events other than regular "click" until there's been at least our ~450ms between clicks. Each click in "overflow" resets the timer but returns us to overflow.
  - That's the pattern. I'll see if I can work out a nice isolated implementation, but in the meantime here are my tests:

    - https://gist.github.com/steveruizok/007db653ab78c3f2e25aafa2a75c6c03
    - https://codesandbox.io/s/modest-hamilton-446e9

  - Also—moving the pointer more than a certain threshold (~5px) clears the timer. This prevents accidental double-clicks after finishing a drag. So "down, move, up, down" should be a single click, even if it happens quickly.
- Doesn’t this add a lag time during single click since you have to wait some window of time to see if a second click will occur or not? The same lag will be experienced for double and triple?
  - Nope, each pointer down immediately fires a single click. Like in the browser, a double click is always a single click first.
  - So a triple click will look like this: 1st click: single 2nd: single, double 3rd: single, double, triple

- ## Did the hard work today of splitting tldraw's v2 into a core library (headless) and a react library, which opens up possible futures for vue/svelte/etc. 
- https://twitter.com/steveruizok/status/1470525905328091156
  - Also extracting skeleton shapes/tools into their own packages.
- Are there any parts of the vanilla code now that looked/felt better when it was done in React?
  - The types around events were more clean before, as I’m now having to inject a map of events to event types (eg pointer: React. PointerEvent). Other than that, I’d also kept things pretty separate no big changes.

- ## Put together a quick multiplayer implementation on tldraw using Yjs
- https://twitter.com/nayajunimesh/status/1477165474622234624
  - https://opuwd.csb.app/

- ## developing a mostly-accurate mental model around CSS transforms is my hardest-won dev perk
- https://twitter.com/steveruizok/status/1478071639619383302
  - Unfortunately no one can be told how transforms work, they need to fuck around and try every possible combination for years for themselves
  - (scale comes before translate unless you have a good reason not to)
  - (you’re moving the paper, not the pen)

- ## Put together a quick multiplayer implementation on tldraw using Yjs.
- https://twitter.com/nayajunimesh/status/1477165474622234624
  - https://opuwd.csb.app/
  - https://codesandbox.io/s/yjs-tldraw-opuwd
  - Undo/redo don't work as expected a lot of times but live cursors/live shape changes work quite well.
  - he implementation is heavily inspired by the current tldraw liveblocks multiplayer implementation and @steveruizok 's yjs drawing example

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
