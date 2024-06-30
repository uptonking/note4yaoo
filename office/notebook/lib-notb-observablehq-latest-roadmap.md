---
title: lib-notb-observablehq-latest-roadmap
tags: [observablehq, roadmap]
created: 2021-05-14T14:42:02.774Z
modified: 2024-06-30T03:22:22.924Z
---

# lib-notb-observablehq-latest-roadmap

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Notebooks for generating and publishing versioned datasets
- https://talk.observablehq.com/t/notebooks-for-generating-and-publishing-versioned-datasets/5091
- You can build something along those lines on top of Serverless Cells
- This recent Github project might also be useful to you: [GitHub OCTO | Flat Data](https://octo.github.com/projects/flat-data)

- ## Serverless Cells
- https://talk.observablehq.com/t/serverless-cells/4491
  - https://github.com/endpointservices/serverlesscells
- Add yet-another-cors-proxy using serverless cells. 
  - Very simple implementation because the proxy is also a web environment so you are just forwarding the arguments of a fetch call to execute remotely “as is”.
  - [CORS Proxy fetchp](https://observablehq.com/@tomlarkworthy/fetchp)
  - A drop in replacement for fetch that uses a proxy to get around CORS and can optionally mixin secrets into URL parameters and Basic Auth.
- I think open source the backend would be a great next step!
  - You can write a notebook to be your API client to deploy something to some cloud service, then another to be a dashboard to monitor it in real-time, testing, etc. 

- [Serverless Cells](https://observablehq.com/@endpointservices/serverless-cells)
  - https://github.com/endpointservices/serverlesscells
