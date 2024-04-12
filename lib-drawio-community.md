---
title: lib-drawio-community
tags: [community, drawio]
created: 2024-04-12T11:58:55.847Z
modified: 2024-04-12T11:59:11.017Z
---

# lib-drawio-community

# guide

# discuss-stars
- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Draw.io: Open Source Online Diagramming | Hacker News _202308](https://news.ycombinator.com/item?id=37137448)
- > draw.io is not open source software. The complete source code required to build the app from scratch is not available. The Apache license allows you to deploy the project and make changes to the source code that is available on the site.
  - Everything needed to run it locally on your ownmachine or self host it is open source (Apache v2.0); 
  - its the integrations with various other services (Google Drive, Atlassian and the like) that are kept proprietary.
  - The file for converting the mermaid code to mxgaph xml is available only in minified version. the unminified version "mermaid2drawio.js" is missing.
- Draw.io has one of the most well-executed open source business models I've ever come across. 
  - They have a minimum core product available open-source (which I like because I have confidence I can make changes to SVG files I create years from now), but they keep all of their integration code proprietary (Google Drive, Jira/Confluence, etc) to keep enough of a moat from other companies stealing their SAAS.
- they took the bulk of the renderer behind closed doors a while ago. Behold(看，注视) https://github.com/jgraph/drawio/blob/dev/src/main/webapp/mxgraph/mxClient.js

- The fact that you cannot create an arbitrary filled polygon in drawio baffles me.
