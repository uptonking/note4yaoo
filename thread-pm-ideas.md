---
title: thread-pm-ideas
tags: [ideas, thread]
created: '2021-01-17T17:13:54.678Z'
modified: '2021-01-17T17:14:34.313Z'
---

# thread-pm-ideas

# repeat

- ## Harsh truth: Reading about other successful creators won't make you one. Start creating so that you have your own success story to tell.
- https://twitter.com/mkhundmiri/status/1383688592099135498

# ideas

- ## 

- ## Things web apps can do by default that I wish native apps could do, too:
- https://twitter.com/rauschma/status/1383350431619837955
  - Zoom in anywhere
  - Copy any UI text
  - Clone the current view(open the current page in new tab)
  - Bookmark the current location
- May I add?
  - allow for script blocking (ads, tracking etc)
  - allow for loading custom stylesheets (reader mode, dark mode, accessibility - this requires a bit technical knowledge on HTML/CSS)
  - allow for being consumed on any device (even via terminal!)
- Android 11 can copy any text, but it's not really pretty.
  - Note: you must be in app switcher mode (app not maximized) to enable text selection.

- ## Every repo, issue, commit, etc will get a generated card like it.
- https://twitter.com/JasonEtco/status/1380194813140725761
  - And an even more special card for issues, PRs or commits!
- This is sweet. Visual + text is a great way to help people engage and not miss important information.
- I believe we'll be doing a larger blog post about it soon, but we use Puppeteer to generate a screenshot from some HTML.
  - Just out of curiosity: wouldn't something like a Canvas with html2canvas for Example be faster or more efficient Memory wise? Nice Idea btw! Love it!
- I did an open-source server for doing that exact thing some time ago
  - https://github.com/micheleriva/gauguin
  - High performances Golang server for generating open graph images dynamically. 
- I just had a look at how the @vercel team did it in their OG img generator and it’s also Puppeteer and headless chromium
  - https://github.com/vercel/og-image

- ## If you use Next.js, what is your favourite part about it?
- https://twitter.com/heybereket/status/1378889849235775489
- Speed, fast refresh, next/image, SSR, ISR!
- The examples folder on GitHub. Every important OS project should have sth like that

- ## I'm so glad I used MDX for my blog. 
- https://twitter.com/joshwcomeau/status/1243136771652751360
  - It enables things that otherwise would not be possible with Markdown or a CMS, while still being a consumable data source (unlike having the posts be all-JSX)
- I created an `<Asterisk>` component because I wanted to add XKCD-style "jokes on hover". 
  - Plus, I tend to be very verbose, and this means I can pack some of that away into an opt-in annotation.
  - For tangential information, I have a `Sidenote` component. It has a `title` prop which accepts JSX, so I can use any special formatting within it. Also a `type` which accepts info/warning/error/success.
  - For code snippets, I built a little playground component on top of react-live. You can pass props using the typical Markdown code-snippet syntax. 
  - Because animated GIFs tend to be huge, I use "video GIFs", similar to social media platforms. I created a component for this, and allowed it to support both `light` and `dark` variants, to swap out the src depending on the user's color theme.
  - The examples I'm showing are JSX-heavy, which might give you the wrong idea. For the most part, my blog posts look like any other Markdown doc.
- Because HTML is valid Markdown I like using Web Components to do the same thing. 

- ## cascading data updates
- https://twitter.com/chris_whong/status/1376626993614184452
  - Wouldn't it be rad if you could tell a dataset to check its source data every hour and create an updated version of itself if there are changes?

- ## A map quiz for this month's #ironquest - Game
- https://twitter.com/ShijiaWendy/status/1376465383813615620
  - [island shape quiz](https://public.tableau.com/views/IslandShapeQuiz/STARTDB?:language=en&:display_count=y&publish=yes&:origin=viz_share_link&:showVizHome=no)
- I had much fun playing with @Mapbox to make those patterns.

- ## Mermaid for Markdown is not only supported on GitHub but also in #VSCode it seems - code on left, preview on right 
- https://twitter.com/_s_hari/status/1376353291525881864
- Correction: Mermaid is supported on #AzureDevOps. 

- ## I would pay so so so much money for a Figma-based service in that:
- https://twitter.com/Allan/status/1375975277294055425
  - Adds something like tailwind and/or syncs tailwind.config.js as a Figma design system.
  - Exports frames as usable React components. Down to linking Figma symbols to JSON coming out of a fetch or axios.

- ## I just published an introduction to the @jsonstat toolkit as a notebook
- https://twitter.com/badosa/status/1375212974592421889
- This notebook shows you the main features of the jsonstat-toolkit using data from different official statistics providers like Eurostat, UNECE
  - https://observablehq.com/d/22fc6d7389380799
  - JSON-stat is a simple lightweight JSON dissemination(传播, 散布) format best suited for data visualization, mobile apps or open data initiatives, that has been designed for all kinds of disseminators.

- ## I'm really excited to announce Serenity Notes
- https://twitter.com/nikgraf/status/1374619720842944513
  - It's an end-to-end encrypted collaborative notes app allowing you to compose private & shared notes.
  - Think of a simple Google Docs, but end-to-end encrypted and offline-first.
  - and forgot to mention that the client/app code is open source
  - https://github.com/SerenityNotes/serenity-notes-clients
- Is it built on top of a decentralized protocol like  scuttlebutt.nz?
  - I initially started out building it on top of the Matrix Protocol, but hit some roadblocks and eventually went a level deeper directly building a custom protocol on top of gitlab.matrix.org/matrix-org/olm
  - It's still very much inspired by parts of the Matrix Protocol, but no federation atm
  - I would love to see it go decentralised by default and a backup to dropbox/drive by choice 
  - Encrypted backups to iCloud/GDrive are one of the next things on the roadmap
- pure CRDTs? how did you solve for undo/redo? checkpoints for docs with lots of changes?
  - I'm using https://github.com/yjs/yjs and this is the true magic behind the editor. 
- Desktop/web version is planning?
  - Yeah, started working on a Desktop (macOS) version and after that would focus on Windows.
  - Web would be great, but there are certain security implications and also the offline-first part is hard. So not planning to do this anytime soon.

- ## I'm super impressed by the approach @craftdocsapp is taking to data ownership. 
- https://twitter.com/geoffreylitt/status/1374144532976168967
  - 提出了制定markdown在线多人共同编辑协议的建议
  - At the same time, I think they're hitting the limits of modern data storage platforms, and hinting at precisely why we need a new kind of "collaborative filesystem".
- As context, Craft is an iOS/Mac notetaking app w/ a "blocks" model that feels inspired by Notion.
  - Unlike Notion it's offline-first (= very fast!). The interesting thing is they offer two different ways to store your data
- Option 1 is to sync your notes to Craft's servers.
  - The benefit of this is you get realtime collaboration, and you can share a web link with anyone to get comments. Feels similar to GDocs/Notion, just with much better offline mode.
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
  - websocket / web etc
  - ordered list of events 
  - SDK that convert events to data

- ## What are y’all using for for team collaboration on documents, product specs, etc beside Notion? I’m looking for something faster and less clunky than Notion.
- https://twitter.com/flybayer/status/1373788153207734275
- Ditto. Notion has made me appreciate Google Docs. Next up Dropbox Paper.
- Confluence, but it's definitely not faster or less clunky than Notion Face with tears of joy

- ## prototyping a tool for messing with data
- https://twitter.com/_paulshen/status/1362609484519014400
  - https://github.com/paulshen?tab=repositories&type=source
  - non-live panes (eg side effects like network requests)
  - promise values
  - pop-out expression
  - I'm trying an experiment where all the code lives in one file. see how long til i break
  - main inspiration was an interactive curl | jq
- I think there's also interesting territory to explore around not directly coding the transformation, but instead just demonstrating it "directly on the data"...
- https://github.com/stedolan/jq
  - Command-line JSON processor 
- One dream GUI builder I imagine is like:
  - Reshape from API response into the JSON underlying your UI, in something like your demo tool
  - Style the data into an actual UI in something like this:
- I've been jamming on this concept for making data-driven designs. 
  - Given some JSON, this app will provide you with an interface to describe how you want each entry styled, allowing you to gradually create a more complicated design. Here I create an airbnb-ish app.
  - So the controls make it look a lot like other "no-code" solutions like @webflow , but I think the data-first approach makes it a pretty different experience, perhaps more suitable for apps than for say landing pages.

- ## What are people using for versioned controlled diagrams/flow charts/ etc these days?  Is graphviz/plantuml still the goto?
- https://twitter.com/mat4nier/status/1369769536816226306
- I’ve gotten _really_ good at Graphviz. There’s a PlantUML plugin for Confluence, btw
- plantuml and mermaid mostly

- ## best software to create sequence diagrams like this?
- https://twitter.com/sseraphini/status/1369996346493652995
- I use plantuml for my docs diagrams. 
  - Not the slickest or most modern-looking results, but does the job well and the diagrams are text files that can be put under source control which is nice.
- Write them using mermaid syntax for better version control
- Visual Paradigm.

- ## I'm happy to announce, that basetools.io is in beta! 
- https://twitter.com/sebastianhoitz/status/1369390750404927490
  - It is a paywall for your Github repository or npm package. 
  - Just connect to GitHub, set a price, and charge for access to your repository.
- You can think of it as Gumroad but specifically targeting developers selling their UI components, frameworks, starter templates, or libraries.
  - I think there are huge opportunities for developers to sell their projects and earn a living this way. Lots of exciting projects getting started, too. 
  - People like @adamwathan or @mxstbr are leading the way. I'm sure there is going to be plenty more.
  - I want to support developers with basetools.io by basically taking care of a lot of the barriers to this: Charging money, making sure it has the correct taxes, writing invoices, granting access only to people that paid - This is what we do.
- This could go really well or really, really bad. 
  - Hopefully it doesn't turn into a situation like the Unity Asset Store where folks reskin libraries simply looking to profit. 
  - There could be an explosion of low quality libraries that only serve to add confusion.
- What's the difference between this and GumHub by @m1guelpf ?
  - Sell access to your GitHub repos with Gumroad
