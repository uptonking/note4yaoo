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

# discuss-stars
- ## 

- ## 

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
# discuss
- ## 

- ## 

- ## 

- ## 

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
