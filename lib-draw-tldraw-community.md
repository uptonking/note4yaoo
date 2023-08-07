---
title: lib-draw-tldraw-community
tags: [community, drawing, tldraw]
created: 2023-06-19T12:32:06.159Z
modified: 2023-06-19T12:33:38.006Z
---

# lib-draw-tldraw-community

# guide

# dev

# examples
- https://github.com/nimeshnayaju/yjs-tldraw
  - Yjs multiplayer implementation on tldraw v1 (POC)

## collab

# discuss-collab
- ## 

- ## [Self Hosting the webapp?_202111](https://github.com/tldraw/tldraw-v1/discussions/547)
- the real-time collaboration features of tldraw seem to rely on Liveblocks
  - This situation is known and a reflection is in progress by @steveruizok to address this aspect.
  - The basic idea was to use yjs like @nimeshnayaju did on his fork (POC) nimeshnayaju/yjs-tldraw

- ## I'm going to give a live coding session next Tuesday 6pm CET. We are going to build a collaborative drawing app with Yjs and @steveruizok 's perfect-freehand_202109
- https://twitter.com/kevin_jahns/status/1440635129928380418
  - https://www.youtube.com/watch?v=Dkn72yYEqNk

# discuss-kickstarter
- ## 

- ## We’ve been spending the last few weeks figuring out our product strategy around tldraw’s developer library. 
- https://twitter.com/glipsman/status/1681319437285359619
  - The original plan was extremely loose: build something that people liked, make it available in alpha, and see what our users were asking for.
  - Granted I’m only seeing the engaged users in our community, who might be more on the experimental customization and extension side: folks who are looking for an canvas engine rather than a drop-in whiteboard. The latter might be well served, numerous, but silent about it.
  - Our sales would tell that story… which is all the more reason to find the seam between the open source product and the commercial offering.

- We’ve got a lot of options there.
- The easiest would be to fold tldraw into a single close source library, create a lot of docs and demos, and then sell licenses / distributions on a customer-by-customer basis.
  - We could split the library into a free offering (permissively licensed) with fewer features and a customer library with the rest. This dual licensed approach would also rely on separate distributions.
- Another option would be to release the full version under a restrictive license (eg with a watermark that should not be removed) and the same version without that watermark.
  - Possibly the same distribution but with a prop that accepts either “I’m a customer” or “I’m using this in a non commercial product” and rely on good faith.
  - The benefit of this approach is that everyone gets to evaluate the full version, we wouldn’t need a separate distribution, and it gives a more clear purpose to the free offering.
  - The downside would be that it would greatly reduce the amount of permissibly licensed stuff that we offer.
  - In order to keep this option open and interesting, I’ve spent the last week extracting almost all of the tldraw-product-specific code out of our editor library, so that the core can remain open and permissively licensed in any case.
- Another direction, and one we’ve also been exploring this summer, is rearchitecting tldraw as an extensions first library.
  - That would open up other options: having a free core, free packages, and then premium packages and premium products.
  - Here the core would be the tldraw library, while the current tldraw-like experience would become something like “tldraw whiteboard”, a product that we could market separately.
  - This would address the “drop in whiteboard” crowd without muddying that water with our open source / customization narrative.
  - What I like about this last approach is that it opens up more product offerings: with tldraw as an engine, we can make tldraw/whiteboard, tldraw/mindmap, tldraw/slides—all of which can exist as siblings, with their own developer markets, end user products, etc.
  - Of course the current library isn’t architected in an extensions first way, so there would be more work to do there. And maybe one of the other options could work in the meantime.

- TipTap has an open source platform / commercial extension approach. I'm not sure how it's working for them financially, but the platform they wrap (ProseMirror) is sufficiently complicated that I can imagine many developers and companies shelling out(shell out sth for sth 付款-常指不情愿地 ) the $29 subscription fee.

- CodeMirror is extension-first, but I see a lot of people picking Monaco even though it’s much worse on mobile & for accessibility because shrink wrap is easier than build-it-yourself. Extensions are great but make sure you keep a compelling and easy drop in
  - Extension API is always kind of awkward if you ship big extensions — I wanna customize the UI/UX of the extension; now your extensions need extensions? This is annoying in CodeMirror as I read extension source to see how I can inject my logic through eye of needle to customize

- Mixing up commercial and open source parts always backfired for me.
  - My current approach is to develop two completely separate projects, one for-profit offering/product and one pure, open source branch.
  - I don‘t like extension-first anymore, copy+remix is much better.
- How did it backfire(事与愿违; 产生反作用)?
  - You start with a pure, self-contained open source implementation and end up with a monster because you need to integrate business demands. No plugin system will save the core from being affected.
  - To make my point a bit more nuanced, I was mainly referring to higher level UI things, where libraries create lots of indirection. But on the lower-level side core+plugins makes sense from a maintainability point of view. E.g. I'm using ProseMirror+custom plugins under the hood.

- Free with logo, pay to remove logo has worked pretty well for amCharts for more than 15 years now.

- ## I'm in the descending phase of the product diamond_202307
- https://twitter.com/steveruizok/status/1676332626293014528
  - with tldraw, I initially wanted to build a general purpose abstraction for "infinite canvas" user interfaces. But taking stock of the project, I'm not sure we've done that.
  - What we have _built_ is a hackable, customizable, and fundamentally excellent whiteboard. If I presented it (or sold it) as anything more than that, I think that would be misleading.
  - Whiteboards are complex enough on their own. In order to make it better for being a whiteboard, we've made it worse for other things. It certainly can be extended in some really powerful ways but it does not quite contain the multitudes that I initially imagined.
- 👉🏻 If I squint(眯眼/斜视) at it, I can make out the borders of the general abstraction. 
  - A lot would be the same: the **in memory database and signals**, most of the **event system**, the way we approach **camera control and culling(挑选/挑出)**, the use of outlines and transforms...
- I think we could do that. I think it would be extremely useful and cool and successful as an open source project. I don't think it would be as strictly valuable as creating a very good whiteboard, though.
- A little art school lesson is that you're never really "starting from scratch". Your creativity is always bounded by conditions, materials, time, place, light, etc; and so your work is never completely your own. Relax!
  - Have an outcome in mind but always be ready to treat the present state as a fresh set of initial circumstances. Stop drawing A and start drawing B, same drawing. It's no less your own, the twists and turns are yours too.
- Anyway, for tldraw, I think we need to look where we're at and adjust the direction to be more of what it is rather than more of what it isn't.

- ## we’re talking about how to roll out a commercial product around tldraw’s open source library
- https://twitter.com/steveruizok/status/1675946321637969920
  - I’ve looked at a lot of different similar products here, mainly text editors and image editors and maps, how they do it, and where the successful ones end up
  - It seems like everyone ends up with some variation on “if you want to use this in a commercial product, you need to be a customer”
  - Originally I thought we would do a free editor as the wedge + services and stuff on top, but that seems like the main value in these kinds of things is the thing itself

- I find a lot of value in the OSS code separate from the product/app. I am recently taking some snippets from tldraw around zooming, panning, cursors etc that have been invaluable, and so tldraw helps ‘lifts all boats’ on the web. but, wouldn’t be possible with commercial licenses

- From my experience, offering users who are willing to pay more features on top makes the most sense for projects where the delineation between business/non-business required features is clear. People who would not respect a license do value their time and reliability.
# discuss-breaking-changes
- ## 

- ## 

- ## 

- ## What are the best multitouch interactions you’ve seen, apart from the obvious pan / pinch?
- https://twitter.com/steveruizok/status/1688113371420168192
  - Some of my other surprise favorites are in Apple’s native apps, or maybe they’re just baked into the OS, where I  dragging one item but can still perform other multitouch gestures, like scrolling or swiping between pages.

- The two finger tap to undo / three finger tap to redo from @Procreate and other apps is great, too. 
  - I’ve implemented that a few times in tldraw, it’s crazy complex but when done right feels totally natural.

- ## Design the API first in JavaScript. Don’t let the constraints of TypeScript’s compiler (or your skill in type crafting) lead you to design a worse API
- https://twitter.com/steveruizok/status/1685738781977018368
  - (ofc do as I say, not as I do)
- One of my favorite parts of TypeScript is the ability to gradually type things rather than splitting this into two separate phases. My early API designs have lots of ‘any’s

- ## v2: We’ve prioritized building features ahead of building APIs, with the intention to later build APIs around the requirements of those features._20230715
- https://discord.com/channels/859816885297741824/1104089016955048007/1129708419427876886
  - That’s the phase that we’re in now: taking the tldraw v2 library, with it’s basically complete feature set but somewhat hacky APIs, and designing an architecture where those features can be extracted out into plugins.
  - Really the challenge is to take all of the things we’re doing in tldraw (for example, the text shape, the tools you use to create or select a text shape, and behaviors like creating a text shape when you double click the canvas) and building APIs that allow anyone to create those from user land

- ## Is there a list somewhere of the key improvements in v2?_20230518
- https://discord.com/channels/859816885297741824/911921430617284638/1108429858163404893
  - We've dedicated many many man months of building custom functionality on top of the tldraw v1 and it's unclear what benefits we'll gain from the likely massive work we'd have to do to reimplement things for v2.
  - We have already deployed our whiteboard to a number of commercial customers like Swarovski, ASICS, and Restoration Hardware. We especially use it for our powerpoint/pdf export functionality.
  - We've also intimately tied the board to elasticsearch as we have custom shapes that wrap complex business objects like a company's product that may be rendered in one of any number of ways (cards/carousels/floorplans/etc) but at the end of the day are some reference to an object + options as to how to render it + size/position info for TLDraw.  We have our own data model so that each 'shape' is a row in a database that can be independently queried/updated/full-text-searched/etc
  - I'd be very interested to pickup some of your performance improvements - I've noticed that the way you do the shape transforms is very different in v2 (matrix transforms)

- 👉🏻 I should draft a list of the major changes, but in short:
  - nested / masked shapes (ie frames)
  - embeds and bookmarks
  - better text handling / export
  - better file handling / image export
  - better clipboard handling

- I am still built on tldraw/core, vect, etc
  - But not tlrdraw/app at all as I completely reimplemented everything there + a zillion things
  - But if there are core features to the renderer I could backport to v1 without violating a new license or whatever, I'd love to do so - you must have changed your transforms for a good reason
  - I have super complex copy/paste/drag drop functionality
  - All that stuff is more 'app' featureset
- yeah, you might be on your own if you want to re-implement things. We're deciding now between keeping the core Apache and then commercializing on pro features, or whether instead of license the core as AGPL and commercialize on non-AGPL licenses.
  - Which I'm not too concerned about picking up, it's easy enough for me to reimplement anything that looks useful from userspace, but I'm much more concerned with core/renderer sort of stuff.  The absolutely killer feature for me with tldraw is that it's html/css and NOT canvas - which means any component can be used with it
  - I added a hook in my version to override your getShapeTree stuff, I memoize it and such - reduces a lot of churn. This way if a shape breaks it doesn't crash the board
  - The whiteboard is very much a secondary feature in the platform but it's been extremely useful to allow for building free form UIs and I plan to use it in the future to do all sorts of crazy stuff like let customers define what a 'product card' looks like by building a template in the whiteboard bound to live data, saving it as a reusable template, and then rendering their entire catalog view (grouped/filtered/sorted cards) with the 'card' being that whiteboard template realized.
  - There's so little overhead in rendering N whiteboards that it's really no different than any other react component
  - We're about to kickoff building a 3d configurator sub-application using the whiteboard as a building block, basically a three JS 'shape' set to the viewport's bounds and then tool windows on top of it
# discuss
- ## 

- ## 

- ## This refactor switches most of our hit testing from DOM based (with listeners on every element) to pure js. 
- https://twitter.com/steveruizok/status/1683609271194329088
  - It will roughly halve(减半) the number of DOM nodes on the canvas in any given project, while giving us so much more control over what gets selected.
  - Our selection / overlays / inputs still use DOM events / hit tests. The system works with both!
- We don’t rely on rendering for any information so we can test interactions and their results without using visual tests. (We do have visual tests but they just guarantee that the rendered output corresponds correctly to our data)

- ## is this kind of a memory leaky pattern?
- https://twitter.com/steveruizok/status/1675762561008951296

- Check with —expose-gc
  - And WeakRef

- ## Let’s say you have an editor with extensions that add functionality (eg a history extension that adds undo/redo commands to the editor API). 
- https://twitter.com/steveruizok/status/1675470978447441920
  - How would you do this with Typescript? 

```typescript
// @tiptap_editor uses declarations, any other way?
declare module '@tiptap/core' {
  interface Commands<ReturnType> {
    history: {
      undo: () => ReturnType,
      redo: () => ReturnType,
    }
  }
}

editor
  .addCommand(undo)
  .addKeyboardShortcut(“mod+z”, () => editor.commands.undo())
```

```typescript
// slate solution
const editor = withReact(withHistory(createEditor()));

// it seems to cast types explicitly
const withHistory = <T extends Editor>(editor: T) => {
const e = editor as T & HistoryEditor;

e.undo = ()=>{}

e.redo = ()=>{}

return e;
}

```

- I would look at lexicals plugin system for inspiration. Very well thought out! Let’s you register handlers with priority (so that plugin order doesn’t matter)

- In playwright, you can call `test.extend` with fixtures to return a new “test” object you can use those fixtures in. I love that pattern, since it means the test objects are immutable; no worry about the command being loaded as a side effect somewhere, just use the correct editor
  - Yeah interface declarations like this are the ONLY way to mutate a type in Typescript. Basic function composition tends to be simpler.

- Rich-Harris explored autogenerating types for SvelteKit packages and end up at declarations. Do with that what you will.

- ## API design question. For tldraw, our extension / customization story is quite a ride. 
- https://twitter.com/steveruizok/status/1675075608613728256
  - We have a common interface for all of our shapes, however that interface is very large/flexible due to the variety of things it supports: drawn lines, editable text, arrows, etc
  - Add to this the validation and migration features, which are important but maybe tertiary, and the concept of creating a “tool” to generate your shapes, and there’s just a lot going on.
  - There’s also the added step of customizing our UI to include a button for the shape, controls for the shape’s properties, and possibly new commands or shortcuts related to the shape.
  - As a result, the simple stories become more difficult. If you want to just create a rectangular shape that renders with a react component, you need to write a bunch of code that touches several APIs and concepts in order to get there.
  - If we want to make that easier, we could restructure our APIs to make them easier; or we could create some higher level APIs like “createCustomShape” that drove our current APIs behind a friendlier interface.

- I’m a little wary of this kind of layering though. Has anyone had good experiences in this direction? Bad?
  - I like higher level thingies as an introduction to lower level thingies, but be wary(谨慎care) of people wanting to extend the higher level thingy – discourage `const myTool = { …makeEzTool(…), someOverride: 2 }`. “Config extension” is a swamp(沼泽地)!
  - Tanstack Table does this in an interesting way. There’s a “helper” that streamlines declaring column definitions. And default “model” impls for filter/sort but it’s clear the user can totally customize that by writing their own model (I don’t need that tho)

- Keep the extensive api but have if well documented with good examples and maybe a boilerplate project. Simpler APIs almost always hit it's limitations rather sooner than later and then you have to learn from scratch
  - api和文档都需要长期维护

- Layering good, bad layering bad.
  - 2 tiers is likely enough, you want to make the common customisation tasks easy, because if it’s not, people will be overwhelmed by how many concepts they have to learn. 
  - The essence of good abstraction is reducing the number of concepts in play.
  - You *could* use more advanced gravitational equations and relativity to calculate how long it will take something to hit the floor when you drop it, or you could use the simple abstraction: F=MA

- Keep the low level API, provide a bunch of recipes for doing common things either in the form of a package or copy/paste code. Grow the library as more common use cases emerge.
  - At some point the commonalities will scream at you for an abstraction and you'll just provide that as an additional layer / API

- ## I’d like to dog food our shapes as plugins but there are so many logical cutouts associated with that shape
- https://twitter.com/steveruizok/status/1672973458165178369
