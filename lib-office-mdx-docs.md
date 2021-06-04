---
title: lib-office-mdx-docs
tags: [docs, lib, mdx]
created: '2021-06-04T16:49:14.136Z'
modified: '2021-06-04T16:49:32.208Z'
---

# lib-office-mdx-docs

# guide

# intro
- MDX is an authorable format that lets you seamlessly write JSX in your Markdown documents.
  - You can import components, such as interactive charts, and embed them within your content

- MDX syntax can be boiled down to being JSX in Markdown. 
  - It’s a superset of Markdown syntax that also supports importing, exporting, and JSX.

- Traditionally, Markdown is used to generate HTML. 
  - **Markdown is good for content**.

- Recently, more and more developers have started using JSX to generate HTML markup. 
  - JSX is typically combined with a frontend framework like React or Vue. 
  - These frameworks add support for components
  - **JSX is good for components**.
  - It makes repeating things more clear and allows for separation of concerns. 

- MDX fully supports JSX syntax. 
  - Any line that start with the `<` character starts a JSX block.

- MDX supports two more features: imports and exports.

- import can be used to import components, data, and documents.
- You can import components, such as your own or from rebass
- You can also import data that you want to display, like `.json` files
- You can embed MDX documents in other documents. 
  - This is also known as transclusion. 
  - You can achieve this by importing an .mdx (or .md) file
  - `import Contributing from './docs/contributing.mdx'; `

- export can be used to export data and components.
- you can export metadata like which layout to use or the authors of a document. 
  - It’s a mechanism for an imported MDX file to communicate with the thing that imports it.
- This is similar to what frontmatter allows in Markdown, but instead of supporting only data in something like YAML, MDX lets you use richer JavaScript structures.

- If you need to define a variable in your MDX document, you can use an export to do so. 
  - Not only do exports emit data, they instantiate data you can reference in JSX blocks

- In addition to rendering components inline, you can also pass in `components` to be used instead of the default HTML elements that Markdown compiles to. 
  - This allows you to use your existing components and even CSS-in-JS like styled-components.
- If you’re using an app layout that wraps your application, you can use the `MDXProvider` to only pass your components in one place
  - This allows you to remove duplicated component passing and importing. 
- The `MDXProvider` has a special `wrapper` key that you can use in the component mapping. 
  - With your wrapper component you can set the layout of your document, inject styling, or even manipulate the children passed to the component.
- Sometimes from an MDX file you might want to override the wrapper. 
  - This is especially useful when you want to override layout for a single entry point at the page level. 
  - To achieve this you can use the ES default export and it will wrap your MDX document instead of the wrapper passed to MDXProvider.

- MDXProvider uses React Context to provide the component mapping internally to MDX when it renders.
# Writing a plugin
- Now let’s consider an example where you want to pass all headings through the title module to ensure consistent capitalization. 
  -  We can use `unist-util-visit` to visit all headings and change the text nodes with `title(text)`.
# API
- MDX (the library), at its core, transforms MDX (the syntax) to JSX. 
  - It receives an MDX string and outputs a JSX string. 
  - It does this by parsing the MDX document to a syntax tree and then generates a JSX document from that tree. 
  - The JSX document is typically evaluated later through something like Babel or webpack. 
  - You can extend MDX by passing plugins that change the tree to customize how the JSX string is created.

- By default, MDX is asynchronous because plugins can be asynchronous themselves! 
  - This means that plugins can request data, read from the file system. Anything! 
  - You should use the async API, unless you have very good reasons to use the sync API.

- If you’re using the MDX library directly, you might want to process an MDX string synchronously. 
  - It’s important to note that if you have any async plugins, they will be ignored.

- If you want to extract data from a MDX file, you can access the compiler directly
# runtime
- A React component that evaluates MDX
  - warning: this is not the preferred way to use MDX since it introduces a substantial amount of overhead and dramatically increases bundle sizes. 
  - It must not be used with user input that isn’t sandboxed.

```typescript
import React from 'react'
import MDX from '@mdx-js/runtime'

// Custom components:
const components = {
  h1: props => <h1 style={{color: 'tomato'}} {...props} />,
  Demo: () => <p>This is a demo component</p>
}

// Data available in MDX:
const scope = {
  somethingInScope: 1
}

// The MDX:
const children = `
# Hello, world!

{1 + somethingInScope}

<Demo />

<div>Here is the scope variable: {some}</div>
`

<MDX components={components} scope={scope} children={children} />
```

# ast
- MDX, the library, uses two syntax trees. 
  - The first, MDXAST, represents markdown with embedded JSX, and is a superset of mdast. 
  - The second, MDXHAST, represent HTML with embedded JSX, and is a superset of hast.

- The majority of the MDXAST specification is defined by mdast.
- The new node types in v2-next.9 renames the types `export, import, jsx`into 
  - `mdxjsEsm, mdxJsxFlowElement`

- The majority of the MDXHAST specification is defined by hast. 
  - MDXHAST includes all nodes defined by MDXAST, except for Comment, as it’s defined by hast already.
- MDXAST defines the following additional node types:
  - `jsx, import, export, inlineCode`
# components
- The MDX core library accepts a string and exports a JSX string that represents a component (via code generation). 
  - It uses a custom pragma which customizes the rendering of elements in Markdown and JSX.
- layoutProps is created based on your exports and then passed to the wrapper. 
- Because MDXProvider uses React Context directly, it is affected by the same caveats.
  - It is therefore important that you do not declare your components mapping inline in the JSX. 
  - Doing so will trigger a rerender of your entire MDX page with every render cycle. 
  - Not only is this bad for performance, but it can cause unwanted side affects
# plugins
- MDX uses remark and rehype internally.
-  the core of MDX is mostly plugins itself! 
   -  We first use remark-mdx to add MDX syntax support 
   -  and then use a rehype plugin to transpile it to JSX. 
   -  The final result is JSX that can be used in React/Preact/Vue/etc.

- The flow of MDX consists of the following six steps:
  1. Parse: MDX text => MDAST
  2. Transpile: MDAST => MDXAST (remark-mdx)
  3. Transform: remark plugins applied to AST
  4. Transpile: MDXAST => MDXHAST
  5. Transform: rehype plugins applied to AST
  6. Generate: MDXHAST => JSX text

- MDX allows you to hook into this flow at step 3 and 5, where you can use remark and rehype plugins (respectively) to benefit from their ecosystems.
- Creating a plugin for MDX is mostly the same as creating a plugin for remark or rehype
# Transform Content
- With MDX you can interact with or manipulate raw MDX content. 
- Since MDX is a part of the unified ecosystem, there are many utilities you can use to work with MDX.
- The remark-mdx library is a parsing extension to enhance the Markdown AST to understand MDX (resulting in MDXAST)
