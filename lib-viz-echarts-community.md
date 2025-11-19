---
title: lib-viz-echarts-community
tags: [community, echarts]
created: 2023-02-05T19:07:25.787Z
modified: 2023-02-05T19:07:38.220Z
---

# lib-viz-echarts-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## [A love letter to Apache Echarts | Hacker News _202402](https://news.ycombinator.com/item?id=39369828)
- my current headache that I'm trying to solve with echarts is handling log scales with data that contains negative/zero values. Quite a few graph libraries that support log scaling don't support this, and I think it may have to do with some fundamental conflict between ui people who (imo reasonably) look at their data and say "my log scale Y axis ticks should be -1, -100, -10000, -1000000! Why is that so hard?" And some dev with a slightly puritanical bent thinks about log(0) and log(-100) and their eye starts twitching and in the end of the day the feature never gets added. I get it math nerds, I get it. But throw me a bone, will ya?
  - Matplotlib for python solves this with a SymLogScale, which is allows you to chart (-10 ^3, - 10^2, ..., 10^2, 10^3) in the way that you'd expect. It does this by being linear between two small limits (to avoid doing log(0) and upsetting the mathmos) and showing sign(x) * log(abs(x)) elsewhere.
  - You can probably do the transformation yourself directly on your data, and then do the inverse transformation relatively easily for your tool tips.
- If dealing with log(0) is an issue, a simple solution is to add 1/0.1/0.01.. to all values in the sample. Pick a fraction that is within the margin of error for your calculations. This is not supposed to be a blanket advice for everyone - use your judgement based on the use-case.

- Surprising to me that Vega and Vegalite don't get a lot more love
  - they simplify the act of transforming data into visualizations down to the essential association of dimensions to axes/color/etc visualization concerns.
- Visuals defined in JSON (so perfect for manipulation and generation) and also able to bake-in custom interactions within that is an awesome power.
  - I like the look of Observable Plot, but it doesn't do interaction like Vega/Vega-Lite. (They are working on some interaction though, and they have quite the team)

- I just moved out ant charts for echarts. Too many bugs IMHO in ant charts (ant.design however is great).

- ## Finally decided to switch to WebGL 2.0 in my ClayGL renderer._202302
- https://twitter.com/pissang1/status/1625815227836280832
  - Spent one day to finish and pass all test cases, much less time than I expected. 
  - Though still many features in WebGL 2.0 has not been used yet.
