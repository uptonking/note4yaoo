---
title: lib-db-app-community-dev-xp
tags: [community, database, dev-xp]
created: 2023-10-26T22:03:59.661Z
modified: 2023-10-26T22:04:11.502Z
---

# lib-db-app-community-dev-xp

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 🦀☕️🔥 [Leveraging Rust in our Java database | Hacker News_202309](https://news.ycombinator.com/item?id=37557880)
- 
- 
- 

# discuss
- ## 

- ## 

- ## The story I hear repeatedly from database developers I look up to is that they weren't always database developers. 
- https://x.com/eatonphil/status/1806497245849649637
  - Almost always, they got their start in web development, and at some point started working for a database company on the database.

- ## I think `io_uring` allows reimagining how the database IO can be redesigned.
- https://twitter.com/sunbains/status/1764358289809371588
  - Use linked requests to avoid torn writes. Write to dblwr files and then to data files. Since you save a copy of the buffers to the kernel with the io_uring model, you can use fixed buffers and copy the page to the fixed buffers and be on your merry way.
  - I need to figure out if I can immediately add the page to the free list in the buffer pool after submitting the request. 
  - I think I should be able to but haven’t thought it through fully. If it works it will simplify the IO layer design considerably. Make it a single producer consumer problem.
  - I forgot to mention that you can link fsync() with your write requests too. The completion of fsync() is your only real guarantee. I would have to track which which pages were covered by the fsync() and not the track the individual writes AFAICT.

- Full stack atomic IOs would be my top choice for avoiding torn writes, but definitely worth looking deeply at how deeply integrating with the the io_uring model can be leveraged for databases
  - You can always disable the dblwr if your stack is capable only atomic writes.
- You can always disable the dblwr if your stack is capable only atomic writes.
  - Yes, I had worked on a project back in 2018 to improve time it took to create a spoof env using ZFS tech on Databases and the system still works with great performance, were able to reduce few hours to 5 mins using the tech… dbwlr was one of the findings in initials runs..

- ## 🔥🔥 [How to steal a developer's local database | Hacker News_201609](https://news.ycombinator.com/item?id=12406310)
- 
- 
- 

- ## 🔥 [Replacing Linux with a Database System | Hacker News_201807](https://news.ycombinator.com/item?id=17634424)
- 
- 
- 

- ## 🔥 [Scrumdog – a program to download Jira Issues to a local database | Hacker News_202207](https://news.ycombinator.com/item?id=32109461)
- 
- 
- 

- ## 🔥 [Download the Entire Wikimedia Database | Hacker News_200901](https://news.ycombinator.com/item?id=26370397)
- 
- 
- 

- ## 🔥 [Download the Entire Wikimedia Database | Hacker News_202103](https://news.ycombinator.com/item?id=26370397)
- 
- 
- 
