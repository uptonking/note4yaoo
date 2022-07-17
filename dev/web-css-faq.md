---
title: web-css-faq
tags: [css, faq, web]
created: 2021-01-08T20:27:25.158Z
modified: 2021-01-08T20:28:00.955Z
---

# web-css-faq

# faq-not-yet

# faq-repeat
- [Removing unused CSS is expensive](https://twitter.com/mjackson/status/1422375213212131334)
# faq

 

## css selector的性能比较

- Sweating over the selectors used in modern browsers is futile; most selection methods are now so fast it's really not worth spending much time over. 
- excessive unused styles are likely to cost more, performance wise, than any selectors you chose so look to tidy up there second. 
  - 尽量不用高冗余的单个庞大的styles.css，只引入所需样式
- By choosing to measure performance through the loading, you are measuring plenty of much much bigger things than CSS, CSS Performance is only a small part of loading a page
- the efficiency order of selectors, from fastest to the slowest
  - id Selectors (#myId)
  - class Selectors (.myClassname)
  - tag Selectors (div, h1, p)
  - neighbour Selectors (h1+p)
  - children Selectors (ul>li）
  - descendant Selectors (li a)
  - star Selectors (*)
  - property Selectors (a[rel="external"])
  - pseudo class Selectors (a:hover, li:nth-child)
- I completely agree it is useless to optimize selectors upfront, but for completely different reasons. optimized for one browser only.
- It is practically impossible to predict the final performance impact of a given selector by just examining the selectors. In the engine, selectors are reordered, split, collected and compiled. To know the final performance of a given selectors, you would have to know in which bucket the selector was collected, how it is compiled, and finally what does the DOM tree looks like. All of that is very different between the various engines, making the whole process even less predictable.
- It's used to validate claims such as 'attribute selectors are slow' or 'pseudo selectors are slow'.
- the slowest selector type differed from browser to browser
- One thing we can be clear on is that using a **flat** hierarchy of class-based selectors
- It's unnecessary to worry about the type of selector used. selector engines work through selectors clearly differs. 
- Further more, the difference between fastest and slowest selectors isn't massive, even on a ludicrous DOM size like this.    
- ref
  - https://calendar.perfplanet.com/2011/css-selector-performance-has-changed-for-the-better/
  - https://ecss.io/appendix1.html (chrome34/firefox29/ie9/android4)
  - https://benfrain.com/css-performance-revisited-selectors-bloat-expensive-styles/

- ### [CSS Selector Performance has changed! (For the better)](https://calendar.perfplanet.com/2011/css-selector-performance-has-changed-for-the-better/)
  - My view is that authors should not need to worry about optimizing selectors (and from what I see, they generally don’t), that should be the job of the engine
  - Style sharing allows the browser to figure out that one element in the style tree has the same styles as something it has already figured out.
  - The browser matches styles from right to left, so the rightmost selector is really important. 
    - Rule hashes break a stylesheet into groups based on the rightmost selector. 
    - When the browser uses rule hashes, it doesn’t have to look through every single selector in the entire stylesheet, but a much smaller group of selectors that actually have a chance of matching. 
    - Another simple but very clever change that eliminates unnecessary work for every single HTML element on the page!
  - The ancestor filters are Probability filters which calculate the likelihood that a selector will match. 
    - For that reason, the ancestor filter can quickly eliminate rules when the element in question doesn’t have required matching ancestors. 
    - In this case, it tests for descendant and child selectors and matches based on class, id, and tag. 
    - Descendant selectors in particular were previously considered to be quite slow because the rendering engine needed to loop through each ancestor node to test for a match. 
    - The bloom filter to the rescue.
    - The bloom filter tests whether a CSS rule is a member of the set of rules which match the element you are currently testing.
    - The cool thing about the bloom filter is that false positives are possible, but false negatives are not. 
      - That means that if the bloom filter says a selector doesn’t match the current element, the browser can stop looking and move on the the next selector. 
      - On the other hand, if the bloom filter says the current selector matches, the browser can continue with normal matching methods to be 100% certain it is a match. 
      - Larger stylesheets will have more false positives
    - The ancestor filter makes matching descendant and child selectors very fast. It can also be used to scope otherwise slow selectors to a minimal subtree so the browser only rarely needs to handle less efficient selectors.
  - Fast path re-implements more general matching logic using a non-recursive, fully inlined loop. 
    - It is used to match selectors that have any combination of:
      - Descendant, child, and sub-selector combinators, and
      - tag, id, class, and attribute component selectors
    - Fast Path improved performance across such a large subset of combinators and selectors.
  - What is still slow?
    - direct and indirect adjacent combinators can still be slow, however, ancestor filters and rule hashes can lower the impact as those selectors will only rarely be matched. 
    - there is still a lot of room for webkit to optimize pseudo classes and elements, but regardless they are much faster than trying to do the same thing with JavaScript and DOM manipulations

- ### [JavaScript Selector Performance_201703](https://gomakethings.com/javascript-selector-performance/)
  - Specifically getElementById()` and `getElementsByClassName()` are more than twice as fast as `querySelector()` and `querySelectorAll()`.
  - So, that’s bad, right? I honestly don’t think it matters.
  - Yes `getElementById()` and `getElementsByClassName()` are faster. 
  - But the flexibility and consistency of `querySelector()` make the obvious muscle-memory choice for my projects.
  - And it’s not slow. It’s just not as fast.
  - getElementById() can run about 15 million operations a second, 
    - compared to just 7 million per second for querySelector() in the latest version of Chrome. 
    - But that also means that querySelector() runs 7,000 operations a millisecond. 
    - 虽然慢一点，但也足够快，性能的主要问题不在这里
