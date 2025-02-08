---
title: thread-lang-js-ts-validate
tags: [typescript, validate]
created: 2023-08-16T15:49:25.219Z
modified: 2023-08-16T15:50:16.335Z
---

# thread-lang-js-ts-validate

# guide

- resources
  - [Zod Tutorial | Total TypeScript](https://www.totaltypescript.com/tutorials/zod)
# discuss-stars
- ## 

- ## Introducing Standard Schema 1.0 _202501
- https://x.com/colinhacks/status/1883907825384190418
  - It's a specification for a "common interface" to be implemented by all TypeScript schema libraries, written collaboratively by the the creators of Zod, Valibot, and ArkType to promote interoperability.

- https://x.com/gregberge_/status/1887482628347248696
  - The creators of Zod, Valibot and ArkType have agreed on a common interface for schema validation libraries!

- ## Did you know you can use the built-in browser validation API with JavaScript to control how error messages are rendered? Besides the simplicity, you also get i18n for free.
- https://twitter.com/diegohaz/status/1526874008049811461

# discuss
- ## 

- ## 

- ## Valibot looks nice and smaller but the API is less intuitive.
- https://twitter.com/gregberge_/status/1757268398504071561
  - [Migrating from Zod to Valibot: A Comparative Experience | Matthew Kwong](https://mwskwong.com/blog/migrating-from-zod-to-valibot-a-comparative-experience)

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

- ## Zod is a fantastic, powerful primitive to have in a dev's toolkit. 
- https://twitter.com/mattpocockuk/status/1612397810183274497
  - It lets you validate data at runtime - making a whole class of problems easier.
  - So, when should you use it? And when should you NOT use it?

- when you don't trust the data coming into your app, Zod is a priceless addition. That means:
  - Forms
  - Public API Endpoints/Webhooks
  - localStorage
