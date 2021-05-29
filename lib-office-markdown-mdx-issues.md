---
title: lib-office-markdown-mdx-issues
tags: [issues, markdown, mdx]
created: '2021-05-27T15:08:51.036Z'
modified: '2021-05-29T14:51:42.137Z'
---

# lib-office-markdown-mdx-issues

# pieces
- ## 

- ## 

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
