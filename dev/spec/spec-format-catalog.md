---
title: spec-format-catalog
tags: [catalog, format, spec]
created: 2019-12-02T10:25:27.789Z
modified: 2020-10-15T13:42:23.746Z
---

# spec-format-catalog

> specifications about file formats

# guide

# popular-file-formats

- csf (Component Story Format)
  - title, component, parameters, decrators
- [Storybook for everyone: CSF vs MDX](https://dev.to/lauracarballo/storybook-for-everyone-csf-vs-mdx-88b)
  - Both CSF and MDX provide a great way of building component libraries. 
  - I recently ran a twitter poll on prefered method when writing stories and nearly 70% of the people (80 votes aprox.) voted on using CSF, which is understandable as it is still the standard and recommended way. 
  - But, MDX is still a very convenient way of writing stories in those cases where CSF seems a bit of a barrier for non technical users or our component needs precise and well structured documentation.
- [What are your thoughts on the MDX format for @storybookjs](https://twitter.com/lcarb14/status/1379913918445801473)
  - I'm currently preferring MDX as it provides both Stories and Docs with a single file.
# tabular
- https://github.com/brimdata/zed
  - [Zed Formats](https://zed.brimdata.io/docs/formats)
  - The Zed data model defines a new and easy way to manage, store, and process data utilizing an emerging concept called super-structured data. 
  - The data model specification defines the high-level model that is realized in a family of interoperable serialization formats, providing a unified approach to row, columnar, and human-readable formats.
# JSON-stat
- docs
  - https://json-stat.org/
  - https://github.com/jsonstat/toolkit
  - https://json-stat.org/samples/oecd.json

- Until the introduction of JSON-stat, the main statistical standards for data and metadata exchange were XML-based: they were usually complicated and verbose.
- JSON-stat is a simple lightweight JSON dissemination format best suited for data visualization, mobile apps or open data initiatives, that has been designed for all kinds of disseminators(传播者).
  - JSON-stat also proposes an HTML microdata schema to enrich HTML tables and put the JSON-stat vocabulary in the browser.

- The JSON-stat format is a simple lightweight JSON format for data dissemination. 
  - It is based in a cube model that arises from the evidence that the **most common form of data dissemination is the tabular form**.
- HTML microdata allows machine-readable data to be embedded in HTML documents in the form of nested groups of name-value pairs. 
  - JSON-stat proposes a vocabulary in microdata format to enrich HTML tables.
- If you have to process JSON-stat responses, you are not on your own. 
  - There are solutions available in several programming languages: JavaScript, Java, R, Python, Julia, PHP. 
  - And many end user tools to browse, filter, validate and convert JSON-stat.
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
