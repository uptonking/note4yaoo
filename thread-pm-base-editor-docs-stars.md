---
title: thread-pm-base-editor-docs-stars
tags: [documentation, editor, pm, thread]
created: '2021-08-22T07:28:43.964Z'
modified: '2021-08-22T07:29:34.045Z'
---

# thread-pm-base-editor-docs-stars

# discuss
- ## 

- ## 

- ## 

- ## storybook Component Encyclopedia is in beta
- https://twitter.com/storybookjs/status/1491806826739941377
- We’re on a mission catalog the world’s UI components for you to learn from—3, 490 components & 44 projects so far.
  - Reference components from top teams
  - Play with live implementation 
  - view source

- ## Notion、WordPress 等有基于Block概念的编辑器。人们喜欢 Block。我们似乎标准化了一件事：插入新 Block 的 / 键。但是其他所有的内容都是完全专有且非标准的
- https://twitter.com/EryouHao/status/1486954447943057409
  - 如果在网络上的 Block 是可互换和可重复使用的，不是很酷吗？
  - 于是一个开放的、免费的、非专有的协议诞生了
- https://blockprotocol.org/
  - https://github.com/blockprotocol/blockprotocol
  - An open standard for building and using data-driven blocks. Make your applications both human and machine-readable.
  - Any valid HTML is already a block.

- ## I’m working on a spike(尖刺) for TLDraw’s renderer, replacing the current “one big SVG” approach with lots of divs for each shape instead.
- https://twitter.com/steveruizok/status/1436638874432851968
  - The goal is to support “shapes” that render regular HTML, not just SVG elements like `<rect>` or `<path>` , which is the current limitation.
  - Instead, the renderer should be able to put any React component on the page. Most of the current shapes will return SVG elements, but shapes like Text wouldn’t have to.
  - The biggest trade off here is auto-sizing `<g>` elements, which are awesome. Since SVG elements are basically `overflow:hidden` , we’ll need to pad the shapes more based on the zoom level.
- My one concern would be files will tend to stop being SVG compatible as the files gets laden with non SVG components. So no clean export. I want non-SVG components though too. Perhaps being able to have constrained parent objects that only allow SVG children so people can intent.
  - **SVG export is more of a “app level” feature vs a “renderer level” feature**, so it’s really up to what you do with it. No reason we can’t still have good SVG export in the tldraw app.
  - For example, if I had a post-it component that I rendered in HTML, in order to make it easier to edit on the page, I could still write my export code to create an SVG shape from its data.
- Is `foreignObject` not an option? I was hoping that we can start using it in projects that don’t need to support IE (which I’m assume TLDraw doesn’t).
- I'm basically doing something similar to this for the visual editor. It's still one big SVG, but also a `foreignElement` that positions HTML elements (single one for perf reasons)

- ## So, dumb question: you're building a (small) Postgres/Node/Vue web application that has a feature where user can upload file, and retrieve it later. Where do you store the file?
- https://twitter.com/stevage1/status/1433215485051613187
  - 结论是避免过早优化
  1. In the DB
  2. On disk on the Node server
  3. In S3
  4. Some other third party?
- If it's a small number of files and there are no big files, I'd definitely go with 1. That way you cut out the AWS dependency and you have all the data in a single place.
- No.1 is also good because of the concurrency guarantees - can use as a rudimentary message queue
- Must be some library out there to make 3 easy? In Python/Django, there's a package that just shims it in so it looks like reading/writing to local disk, and generates signed URLs as needed.
- Depending on how hard you anticipate making the switch later if it starts to cause issues... I'd probably give 1 a crack. Avoid premature optimisation, a bit easier in the short term etc
  - The aws-sdk for node is not that complicated, but you wanna be mindful of security then

- ## I'm super impressed by the approach @craftdocsapp is taking to data ownership. 
- https://twitter.com/geoffreylitt/status/1374144532976168967
  - 提出了制定markdown在线多人共同编辑协议的建议
  - At the same time, I think they're hitting the limits of modern data storage platforms, and hinting at precisely why we need a new kind of "collaborative filesystem".
- As context, Craft is an iOS/Mac notetaking app w/ a "blocks" model that feels inspired by Notion.
  - Unlike Notion it's offline-first (= very fast!). 
  - The interesting thing is they offer two different ways to store your data
- Option 1 is to sync your notes to Craft's servers.
  - The benefit of this is you get realtime collaboration, and you can share a web link with anyone to get comments. 
  - Feels similar to GDocs/Notion, just with much better offline mode.
- Option 2 is to store data on your filesystem. 
  - The benefit here is data ownership: more privacy, and you can open the files in other apps without issue.
- Now, if you want sync with Option 2, you can bring your own w/ iCloud Drive etc. But if two devices edit concurrently, you'll hit conflicts.
  - They currently store data in a JSON format but are trying to move to Markdown as a canonical storage format. Would make the "data ownership" even more meaningful since you could just edit their files w/ any Markdown editor!
- So, to review -- user gets to choose either Option 1 or 2 for any note. Which is already amazing and beyond most other apps!
  - But... it's also annoying that I have to choose. Could we have an Option 3 where we get the best of both worlds?
  - Concretely, what I want is something like a "filesystem", where I own the data and can open it in whatever app I choose.
  - But I don't want manual conflict merging every time two people simultaneously edit a doc. The "filesystem" needs to know how to merge changes.
- In other words: why does Craft (and Figma and GDocs and Notion and Pitch...) have to implement their own custom realtime sync protocol?
  - Could we just have a user-owned "filesystem" that deals w/ that part? So I can open a file in multiple apps, and have them sync in realtime?
- **The world I'm imagining** is one where I have Craft open, and you have Notion open, and another collaborator has VSCode open and we're all editing the same document live, perhaps from slightly different perspectives.
  - Curious if people think this "new collaborative filesystem" would be valuable and what the biggest challenges are.
  - To me, feels like the biggest tension is standardizing vs. diverging "file formats", and seeing how much common ground can be found between apps.
- Some intriguing projects which are taking on aspects of this challenge:
  - Braid (braid.org), a generic protocol for state sync
  - Fission (fission.codes), platform for building apps where users own the data
- The original local-first article from I&S is always worth a re-read for thinking about this tradeoff space.
  - But I think the extra tricky part is going beyond "individual devs should do local-first" to "we should have a cross-app local-first FS"
- I believe that future is possible with event sourcing. @todoist somewhat done this with their sync API.
- As long as we have:
  - websocket/web etc
  - ordered list of events 
  - SDK that convert events to data
