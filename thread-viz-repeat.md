---
title: thread-viz-repeat
tags: [repeat, thread, viz]
created: '2021-10-24T14:01:56.584Z'
modified: '2021-10-24T14:02:18.073Z'
---

# thread-viz-repeat

# discuss

- ## 

- ## 

- ## 

- ## 

- ## I spent tons of time in the canvas API back in my @chartjs days. It was a lot of fun, but the most important thing I learned from that experience was that you'd have to pay me at least $1M / year to touch the canvas API directly again, let alone build charts/tables/grid with it.
- https://twitter.com/tannerlinsley/status/1533847458861547521
- I think canvas is difficult because you're essentially re-coding what the browser does for free with the DOM, but now you have to control it yourself in an HTML element with a fundamentally different rendering paradigm.
- When I worked on my game years ago, I had this same problem. 
  - I could put text on the screen, but I needed to manage the container and make sure the text was wrapped per word if it was too long for the container. 
  - Lots of foundational code we take for granted on the web.

- How do you visualize 10.000+ data points in browser without using canvas? Big data visualization as a usecase becoming more common than what people think.
  - At that point, might want to rethink the visualization. Data density only goes so far before you usually need binning/summarization to glean meaningful insights

- Do you mean that the API is poorly designed, or just that there is a lot of work to build everything on top of the limited abstractions?
  - The latter

- Tell me about it! Worked on a project with d3 a while back. I'm either committing to base my entire career on SVGs or I'm not touching the `<canvas/>` ever again Appreciate the guys who built visx at @AirbnbEng tho! Declarative programming eases the pain of building dynamic SVGs

- I spend a lot of time with @amcharts 5 based on canvas, and I'm so happy I only have to deal with the abstraction on top of it 🥲 It's been a long time since I had to interact directly.
- I think it takes a lot of extra work since it’s very low level but I actually really enjoyed working in it. It made me feel like a cool low-level systems engineer 

- ## I’ve noticed visualization tools love demoing maps. 
- https://twitter.com/bernhardsson/status/1452078179003346948
  - It’s always like “with three clicks, here are the top grossing gas stations in Philadelphia” or whatever. 
  - Vs in reality if you do data science/business intelligence, maps are maybe used 0.1% of the time?
- At my previous company, DataMarket, we put a lot of effort into choropleth maps, as we were working with wordwide and regional socio-economic data. They were used a lot. 
  - At @GRID_hq it’s about everyday work that “gravitates(被吸引到、转向) to spreadsheets”, and we don’t see a strong need.
  - To be clear, I agree with your main point: 99% of use-cases for BI and operational visualizations do not require maps.
- I’m sure there’s plenty of people who use map visualizations all the time. Like, if you work at the US Census Bureau, it’s great.
  - Maps are pretty useful in the real estate industry. Also logistics, retail, etc
- Yes we always laugh at it. Nobody needs maps except documentary producers. It's stupid.
- Also a serious GIS analyst just isn't going to use your BI tool, they're using something like ESRI
