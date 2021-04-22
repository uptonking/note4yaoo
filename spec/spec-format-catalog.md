---
title: spec-format-catalog
tags: [catalog, format, spec]
created: '2019-12-02T10:25:27.789Z'
modified: '2020-10-15T13:42:23.746Z'
---

# spec-format-catalog

- specifications about file format  

# popular-file-formats

- csf (Component Story Format)
  - title, component, parameters, decrators
- [Storybook for everyone: CSF vs MDX](https://dev.to/lauracarballo/storybook-for-everyone-csf-vs-mdx-88b)
  - Both CSF and MDX provide a great way of building component libraries. 
  - I recently ran a twitter poll on prefered method when writing stories and nearly 70% of the people (80 votes aprox.) voted on using CSF, which is understandable as it is still the standard and recommended way. 
  - But, MDX is still a very convenient way of writing stories in those cases where CSF seems a bit of a barrier for non technical users or our component needs precise and well structured documentation.
- [What are your thoughts on the MDX format for @storybookjs](https://twitter.com/lcarb14/status/1379913918445801473)
  - I'm currently preferring MDX as it provides both Stories and Docs with a single file.

# graphics

- SVG(SCALABLE VECTOR GRAPHICS)
  - SVG is a markup language for describing two-dimensional graphics applications and images, and a set of related graphics script interfaces. 
  - [SVG Working Group Charter](https://www.w3.org/Graphics/SVG/2014/new-charter)
  - [SVG Roadmap](https://www.w3.org/Graphics/SVG/WG/wiki/Roadmap)

# ref

- [Understand how structured data works](https://developers.google.com/search/docs/guides/intro-structured-data)
  - Structured data is a standardized format for providing information about a page and classifying the page content
  - Most Search structured data uses schema.org vocabulary, but you should rely on the documentation on developers.google.com as definitive for Google Search behavior
  - [JSON-LD](http://json-ld.org/)
    - A JavaScript notation embedded in a `<script>` tag in the page head or body. 
    - Google can read JSON-LD data when it is dynamically injected into the page's contents
  - [RDFa](https://rdfa.info/)
    - An HTML5 extension that supports linked data by introducing HTML tag attributes that correspond to the user-visible content that you want to describe for search engines. 
    - RDFa is commonly used in both the head and body sections of the HTML page.
  - [Microdata](https://www.w3.org/TR/microdata/)
    - An open-community HTML specification used to nest structured data within HTML content. 
    - It is typically used in the page body, but can be used in the head.
