---
title: thread-lang-js-ts-validate
tags: [typescript, validate]
created: 2023-08-16T15:49:25.219Z
modified: 2023-08-16T15:50:16.335Z
---

# thread-lang-js-ts-validate

# guide

# discuss
- ## 

- ## 

- ## 

- ## Valibot is a schema library like @zodtypes , except that Valibot is modular and can be code split to a few hundred bytes
- https://twitter.com/FabianHiller/status/1683841850401251333
  - [Introducing Valibot, a < 1kb Zod Alternative_202307](https://www.builder.io/blog/introducing-valibot)
- looks like a clone of Superstruct

- ## I’ve been spiking on runtime validation today using zod
- https://twitter.com/steveruizok/status/1600512479305539585
  - We were finding some edgy cases in @tldraw where shapes would have null values in one of their points, or some other obscure issue that wouldn’t be immediately recognized.
  - Sometimes the bad shape would render fine, but it’s indicator would crash when a user would hover or select the shape, or when it was resized or duplicated.
- Defensive coding? Sure, we can do that. But we would always be chasing bugs, one step behind the complexity of the project, unless we had a way to describe how shapes should look at runtime: no zero-width shapes, no Infinity rotations, etc.
  - Hence run time checking! zod provides a really great API for this sort of validation.
- My only concern there is that inferring types from the library’s definitions seems substantially slower than declaring them straight out; and that our opaque type tricks don’t work with the lib, so we may have to change that
  - Have you tried the alternatives? I've used Valita with no issues, but ts-runtime-checks looks pretty interesting.
  - You can use tozod to define a zod schema from an existing interface
