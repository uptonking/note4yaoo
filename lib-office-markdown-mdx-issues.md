---
title: lib-office-markdown-mdx-issues
tags: [issues, markdown, mdx]
created: '2021-05-27T15:08:51.036Z'
modified: '2021-05-29T14:51:42.137Z'
---

# lib-office-markdown-mdx-issues

# pieces
- ## 

- ## How should markdown be saved and rendered?
- https://dev.to/michael/how-should-markdown-be-saved-and-rendered-51f
- All the responses here are right, and I definitely would stress @mortoray 's point
  - There's a general rule for for asset transformation: **always keep the original**
  - I like to think of the HTML as a function of the markdown. 
  - Every time the markdown changes, run the function to output HTML. 
  - Within the main function are a series of other functions to handle each subtask and return the latest state of the HTML. 
  - I think the functional approach makes the process easy to modify and reason with.
- Storing as markdown keeps a lot of flexibility for later. 
  - In particular it lets you alter the design. 
  - HTML is overly structured and too strict to be design-change friendly. 
  - Many simple design changes would require altering the HTML, not just the CSS. 
  - IF you keep the markdown, the true source, it's easy enough to render new HTML.

- [How would you store Markdown?](https://www.reddit.com/r/Database/comments/iwvjse/how_would_you_store_markdown/)
- It's just text, store it in a text field.

- [What is the best way to store a field that supports markdown in my database when I need to render both HTML and “simple text” views?](https://stackoverflow.com/questions/17250972)
- Decide like this:
  - Store the original data (text with markdown).
  - Generate the derived data (HTML and plaintext) on the fly.
  - Measure the performance:
    - If it's acceptable, you're done, woohoo!
    - If not, cache the derived data.
- Caching can be done in many ways... 
  - you can generate the derived data immediately, and store it in the database, 
  - or you can initially store NULLs and do the generation lazily (when and if it's needed). 
  - You can even cache it outside the database.
  - But whatever you do, make sure the cache is never "stale" - i.e. when the original data changes, the derived data in the cache must be re-generated
  - One way to do that is via triggers.
- just store the data as HTML in the database and then process it to turn it into plain text. In my opinion there are some downsides to that:
  - You will likely need application code to strip the HTML and extract the plain text.
  - Processing the HTML blob can be slow.
  - HTML parsers don't always work well/they can be complex. 
- I would propose what most email providers do:
  - Store a rich text/HTML version and a plain text version. Two fields in the database.
  - As is the use case with email providers, the users might want those two fields to have different content.
  - You can write a UI function that lets the user enter in HTML and then transforms it via the application into a plain text version. This gives the user a nice starting point and they can massage/edit the plain text version before saving to the database.
  - 可参考gmail，可以切换标准视图 和 简单视图，注意是邮件网站自身变简单了，邮件内容还是很花哨但很慢、简单了一点
- Always store the source, in your case it is markdown.
  - You may need it for various purpose, e.g. the same input can be edited, audit trail, debugging etc etc.
- Also store the formats that are frequently used.
  - No overhead for processor/ram if the same format is frequently requested, you are trading it with the disk storage which is cheap comparing to the formars.
- Use on demand conversion/rendering for less frequent used formats.
  - Occasional overhead


- ## Need to fetch markdown from remote source via getInitialProps NextJs
- https://github.com/mdx-js/mdx/issues/789
- Fetching remote Markdown is something that an application I am working on needed to do as well. 
  - Using `@mdx/runtime` as the example posted by @millette is the same approach we ended up using 
  - and it has been effective for **returning compiled JSX to react** for render to the page.

```JSX
import Link from 'next/link'
import MDX from '@mdx-js/runtime'
import { MDXProvider } from '@mdx-js/react'

const FrontPage = ({ MDXContent }) => (
  <MDXProvider>
    <div>
      <p>Hello <Link href="/p2"><a>Earth</a></Link></p>
      <MDX>{MDXContent}</MDX>
    </div>
  </MDXProvider>
)

FrontPage.getInitialProps = async ({ req }) => {
  // console.log('FrontPage.getInitialProps') // , a, b, c)
  const res = await fetch('http://localhost:3000/c1.txt')
  const c = await res.text()
  // console.log('CCC', c)
  // return { MDXContent: '### more stuff' }
  return { MDXContent: c }
}

export default FrontPage
```

- ## How to use mdx dynamically?
- https://spectrum.chat/mdx/general/how-to-use-mdx-dynamically~29843751-310d-4a2b-aad2-41680b300640
  - I'm fetching MDX content as strings from an API and rendering them inside a React site/app. 
  - I was able to achieve this with @mdx-js /runtime, which exposes exactly the API I'm looking for.
  - but warning: this is not the preferred way to use MDX since it introduces a substantial amount of overhead and dramatically increases bundle sizes. It should also not be used with user input that isn’t sandboxed.
- TL; DR: There isn't a quick and easy way to do either on the client side.
  - Serverside rendering or prerendering through webpack will get better results.
  - This is due to both a full markdown parser (remark), part of a JavaScript parser (babel/buble) being included in the bundle.
  - Both are needed, and neither is currently provided natively by a browser.
  - Easiest approach to minimizing the size would be to use a bundler that supports tree-shaking (like webpack or rollup) to cut back on unused files included.
- MDX can include both JSX/React elements and plain ol' HTML elements.
  - Unsandboxed user entered content can lead to issues like cross site scripting
- https://github.com/probablyup/markdown-to-jsx
  - The most lightweight, customizable React markdown component.
  - All this clocks in at around 5 kB gzipped, which is a fraction of the size of most other React markdown components.
  - markdown-to-jsx uses a heavily-modified fork of simple-markdown as its parsing engine 
