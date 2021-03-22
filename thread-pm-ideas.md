---
title: thread-pm-ideas
tags: [ideas, thread]
created: '2021-01-17T17:13:54.678Z'
modified: '2021-01-17T17:14:34.313Z'
---

# thread-pm-ideas

# repeat

# ideas

- ## 

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
  - I want to support developers with basetools.io by basically taking care of a lot of the barriers to this: Charging money, making sure it has the correct taxes, writing invoices, granting access only to people that paid – This is what we do.
- This could go really well or really, really bad. 
  - Hopefully it doesn't turn into a situation like the Unity Asset Store where folks reskin libraries simply looking to profit. 
  - There could be an explosion of low quality libraries that only serve to add confusion.
- What's the difference between this and GumHub by @m1guelpf ?
  - Sell access to your GitHub repos with Gumroad
