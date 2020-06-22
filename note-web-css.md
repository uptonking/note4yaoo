---
favorited: true
tags: [style, web]
title: note-web-css
created: '2019-12-17T04:23:15.125Z'
modified: '2020-06-22T09:16:47.489Z'
---

# note-web-css

## summary
- Ordering CSS Properties by type/group/importance
  - positioning & layout: position, float, overflow,clear, display
  - box model: width, height, margin, padding
  - visual: color, background, border, box-shadow
  - text: font-size/family, text-align, text-transform
  - misc: z-index,cursor

## faq
- css selector的性能比较
    - Sweating over the selectors used in modern browsers is futile; most selection methods are now so fast it's really not worth spending much time over. 
    - excessive unused styles are likely to cost more, performance wise, than any selectors you chose so look to tidy up there second. 
      - 尽量不用高冗余的单个庞大的styles.css，只引入所需样式
    - By choosing to measure performance through the loading, you are measuring plenty of much much bigger things than CSS, CSS Performance is only a small part of loading a page
    - the efficiency order of selectors, from fastest to the slowest
      - id Selectors (#myid)
      - class Selectors (.myclassname)
      - tag Selectors (div,h1,p)
      - neighbour Selectors (h1+p)
      - children Selectors (ul>li）
      - descendant Selectors (li a)
      - star Selectors (*)
      - property Selectors (a[rel="external"])
      - pseudo class Selectors (a:hover,li:nth-child)
    - I completely agree it is useless to optimize selectors upfront, but for completely different reasons. optimized for one browser only.
    - It is practically impossible to predict the final performance impact of a given selector by just examining the selectors. In the engine, selectors are reordered, split, collected and compiled. To know the final performance of a given selectors, you would have to know in which bucket the selector was collected, how it is compiled, and finally what does the DOM tree looks like. All of that is very different between the various engines, making the whole process even less predictable.
    - It's used to validate claims such as 'attribute selectors are slow' or 'pseudo selectors are slow'.
  - the slowest selector type differed from browser to browser
  - One thing we can be clear on is that using a **flat** hierarchy of class-based selectors
  - It's unnecessary to worry about the type of selector used. selector engines work through selectors clearly differs.Further more, the difference between fastest and slowest selectors isn't massive, even on a ludicrous DOM size like this.    
  - ref
      - https://calendar.perfplanet.com/2011/css-selector-performance-has-changed-for-the-better/
      - https://ecss.io/appendix1.html (chrome34/firefox29/ie9/android4)
      - https://benfrain.com/css-performance-revisited-selectors-bloat-expensive-styles/
