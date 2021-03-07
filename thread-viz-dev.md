---
title: thread-viz-dev
tags: [dev, thread, viz]
created: '2021-02-28T08:06:00.007Z'
modified: '2021-02-28T08:06:19.703Z'
---

# thread-viz-dev

# pieces

- ## 

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
