---
title: thread-viz-dev
tags: [dev, thread, viz]
created: 2021-02-28T08:06:00.007Z
modified: 2021-02-28T08:06:19.703Z
---

# thread-viz-dev

# pieces

- ## 

- ## Creating a React Library for Consistent Data Visualization
- https://shopify.engineering/react-library-consistent-data-visualization
  - Introducing the PolarisVizProvider

- ## I know the customer is always right, but not when they ask for an option to support log scales on bar charts. No!
- https://twitter.com/mistercrunch/status/1431103110022242307
  - [Graph tip - Don't use a log scale on a bar graph!](https://www.graphpad.com/support/faq/graph-tip-dont-use-a-log-scale-on-a-bar-graph/)
- Disagree. You can lose long tails without log on the y

- ## Chartability is a methodology for ensuring that data visualizations, systems, and interfaces are accessible.
- https://observablehq.com/@frankelavsky/chartability

- ## With 0.5M+ downloads/month, Dash is the new standard for AI & data science apps. 
- https://twitter.com/plotlygraphs/status/1411395563711389696
  - Dash apps go where Tableau and PowerBI cannot... NLP, object detection, predictive analytics, and more. 
  - 给出了三维散点图的例子

- ## CSS utility classes meet Custom Properties to style HTML elements as charts.
- https://twitter.com/smashingmag/status/1374266140990566400
  - https://github.com/ChartsCSS/charts.css

- https://twitter.com/shadeed9/status/1374271549709168641
- Is using tables for charts mandatory when having graphs? I’ve been using lists for my own system and always wondered if that was okay.
  - Depends on your datas, in fact. If your list  is repeating headers, a table would probably be a better choice.
  - However as long as the accessibility tree exposes everything, you're safe. 
  - I started some charts using definition list, but their supports is embarassing

- ## If PDFs are where data goes to die, where does data go to *live*?
- https://twitter.com/chris_whong/status/1372990040113053702
- I hate myself for saying this, but... Excel.
- Anywhere with an open data license, a decent API, and an explanation of fields and collection methods. 
  - Any format people can read and use easily. http://data.ny.gov, http://humdata.org, http://datacatalog.worldbank.org etc: data needs eyeballs and motives to live
- AirTable and APIs
- https://github.com/simonw/datasette
  - a tool for exploring and publishing data. 
  - It helps people take data of any shape or size and publish that as an interactive, explorable website and accompanying API.

- ## Observable Collaboration is a huge leap forward for thinking with data, together. And it’s a new architecture for Observable, taking us into the future.
- https://twitter.com/mbostock/status/1370134788279922689
  - Our new front-end has a Redux-inspired state system, which with Next.js’ server-side props and TypeScript have dramatically improved our dev velocity.
  - We also have a new multiplayer editor and client-server architecture  building on CodeMirror 6
  - The challenges here are deep. But in remote-first times, it brings me so much joy to be “in the notebook” with others.
- I've set up an example for collaborative editing in CodeMirror 6. With a very cute interactive [demo](https://codemirror.net/6/examples/collab/)

- ## here's a UX question I'm thinking over: Does a log scale work better than a linear one for profiling tools (given that most commits are usually small)
- https://twitter.com/brian_d_vaughn/status/1368219961383063552
  - With a log scale would people be surprised to find out that the 18ms commit was only 18ms compared to the much taller (yellow) 224ms commit? With a linear scale, would they be frustrated that an 18ms commit was impossible to find without individually stepping through each commit?
  - Is there a third approach I haven't considered? (I bet there's lots of research here that I'm unaware of.)
- I’d say linear is more true to the data
  - it will however lead to missing some less severe peaks. Difficult tradeoff. 
  - I think log will work but you’d have to make it clear to prevent people from comparing height in absolute terms. 
  - Other option is hiding the extremes (switchable)
- the dots represent the number of articles per interval. we wanted to keep the scale the same across charts & keep it meaningful (🔵 = 1 article). whenever there are more than 15, it adds a hat to keep it from overwhelming the chart
- Log scale works when the differences between individual varies in degrees of magnitude such. Example. 2, 20, 200, 2000, 20000. Differ in an exponential fashion. 10^1, 10^2, 10^3
- The graph is too small to make a meaningful comparison anyways so definitely go with log here (I’m guessing this is an overview and you can drill down further). Alternatively you could try (not saying it’s a good idea) to use log for the bar height and linear for the bar color
