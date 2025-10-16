---
title: lib-drawio-community
tags: [community, drawio]
created: 2024-04-12T11:58:55.847Z
modified: 2024-04-12T11:59:11.017Z
---

# lib-drawio-community

# guide

# dev-xp

# usage-xp
- 自由画笔 [Draw freehand shapes and annotate diagrams](https://www.drawio.com/blog/freehand-drawing)
  - Select Arrange > Insert > Freehand
  - freehand模式下，如果启用brush，则不可以给所画图形填充颜色，否则可以
  - 用画笔自由绘画闭合图形如不规则的圆后， drawio/tldraw/excalidraw 都支持填充颜色
# resources/templates

- 
- 
- 
- 

- [20+ UML Diagram Templates for Visual Modeling | Miro](https://miro.com/templates/uml-diagram/)
# discuss-stars
- ## 

- ## 
# discuss-format-uml
- ## 

- ## 

- ## [Standard UML file format - Stack Overflow](https://stackoverflow.com/questions/7930199/standard-uml-file-format)
  - I cannot open my old UML diagrams because the tool is obsolete.
  - I would like to know if there is a standard format for UML diagrams. 

- In theory the standard exchange format for UML models is XMI but it´s true that each vendor implements a slightly different version so interchange is not a reality.

- The OMG is working on a new standard : Diagram Definition that is supposed to fix the problems with the current XMI one 
# discuss-not-yet
- ## 

- ## 

- ## [XMI import/export · Issue · jgraph/drawio](https://github.com/jgraph/drawio/issues/1336)
- 202101: Outside the scope of the project.

- https://github.com/jmcklondonuk/drawio_enterprise_architect_integration /202403/js/inactive
  - This project imports XMI files from Sparx System Enterprise Architect into Draw.io
  - It can be added in Draw.io as a plug-in.
  - it parses UML elements that are present in the diagram, returns a structure with UML elements that can be easily represented as JSON, it traverses the data structure with UML elements and dynamically creates mxgraph vertices and edges with the default style
# discuss
- ## 

- ## 

- ## 

- ## http://draw.io 是最适合由Sonnet 生成的流程图、架构图格式。 比svg增加了可编辑，比mermaid、plantuml 漂亮。
- https://x.com/9hills/status/1901933558790488255
- 我还试了 excalidraw 和 tldraw，确实是 http://draw.io 画的稳定，但不够有创意，我还没找到有什么关键词能让其画的好看
  - 目前是靠人，http://draw.io 可以自由编辑。
- 比 mermaid 漂亮是的，但是语义对人类太不友好了，也不像 mermaid 可以直接在 github readme 渲染

- 是让sonnet直接调用drawio的mcp tool？

- ## [Draw.io: Open Source Online Diagramming | Hacker News _202308](https://news.ycombinator.com/item?id=37137448)
- > draw.io is not open source software. The complete source code required to build the app from scratch is not available. The Apache license allows you to deploy the project and make changes to the source code that is available on the site.
  - Everything needed to run it locally on your ownmachine or self host it is open source (Apache v2.0); 
  - its the integrations with various other services (Google Drive, Atlassian and the like) that are kept proprietary.
  - The file for converting the mermaid code to mxgaph xml is available only in minified version. the unminified version "mermaid2drawio.js" is missing.
- Draw.io has one of the most well-executed open source business models I've ever come across. 
  - They have a minimum core product available open-source (which I like because I have confidence I can make changes to SVG files I create years from now), but they keep all of their integration code proprietary (Google Drive, Jira/Confluence, etc) to keep enough of a moat from other companies stealing their SAAS.
- they took the bulk of the renderer behind closed doors a while ago. Behold(看，注视) https://github.com/jgraph/drawio/blob/dev/src/main/webapp/mxgraph/mxClient.js

- The fact that you cannot create an arbitrary filled polygon in drawio baffles me.
