---
title: spec-format-mdx
tags: [format, markdown, mdx, spec]
created: '2021-06-04T16:50:05.110Z'
modified: '2021-06-04T16:50:25.889Z'
---

# spec-format-mdx

# guide

# spec-docs

## [mdx syntax](https://github.com/micromark/mdx-state-machine)

- MDX is the combination of Markdown with JSX.
- Markdown is great
  - easy to read
  - most stuff is relatively simple to write
  - It’s loose and ambiguous: it may not work but u won't get an error
  - Markdown is good for content.
- html has drawbacks
  - HTML in Markdown is naive, how it’s parsed sometimes doesn’t make sense
  - HTML is unsafe by default, so it’s sometimes (partially) unsupported
  - HTML and Markdown don’t mix well, resulting in confusing rules such as blank lines or markdown="1" attributes
  - HTML is coupled with browsers, Markdown is useful for other things too
  - Traditionally, Markdown is used to generate HTML, writing markup in Markdown
- JSX is great
  - familiar syntax (like XML)
  - agnostic to semantics and intended for compilers (can have any domain-specific meaning)
  - strict and unambiguous 
  - JSX is good for components.
  - more and more developers have started using JSX to generate HTML markup.
- Why MDX?
  - MDX is not tied to HTML or JavaScript

- Block
  - A block of MDX is an element or expression that is both the first thing on its opening line, and the last thing on its closing line.
  - Expressions can also be blocks
- Span
  - A span of MDX is an element or expression that is not a block: it’s either not the first thing, or the last thing, or both
- Content
  - block element can contain further Markdown blocks, whereas an MDX span element can contain further Markdown spans.
  - Spans cannot contain blocks
  - Blocks will create paragraphs
  - MDX expressions can contain arbitrary data
- Closing MDX
  - MDX elements and expressions must be closed, and what closes them must be in an expected place
  - “closing” tag cannot be put in a different paragraph/block
  - 在`}`之后注意不要写圆点，如`}.`
- Attributes
  - Attribute expressions: `<Component {attribute expression} />`
  - Boolean attributes: `<Component boolean another />`
  - initialized attributes `<Component key="value" other="more" />`
  - Attribute values can also use single quotes
- Names
  - Element names are optional, which is a feature called “fragments” `<>Fragment block</>`
  - The syntax of the name of an element allows dashes `<c-d />`
  - Names can be prefixed with a namespace using a colon or dot `<svg:rect />` `<org.acme.example />`
- Keys
  - Similar to names, keys of attributes also follow the same syntax, dashes allowed
  - namespaces can also be used
  - Methods don’t work for keys
- Whitespace
  - Whitespace is mostly optional, except between two identifiers (such as the name and a key, or between two keys)

### Deviations from Markdown

- MDX adds constructs to Markdown but also prohibits certain normal Markdown constructs.
- HTML
  - Whether block or inline, HTML in Markdown is not supported.
  - Character data, processing instructions, declarations, and comments are not supported at all. 
  - Instead of HTML elements, use JSX elements.
- Indented code
  - Indentation to create code blocks is not supported. 
  - Instead, use fenced code blocks.
- Autolinks
  - Autolinks are not supported. 
  - Instead, use links or references.`[]()`
- Errors
  - Whereas all Markdown is valid, incorrect MDX will crash.

### Deviations from JSX

- MDX removes certain constructs from JSX, because JSX is typically mixed with JavaScript whereas MDX is usable without it.
- Comments
  - JavaScript comments in JSX are not supported.
- Element or fragment attribute values
  - JSX elements or JSX fragments as attribute values are not supported.
- U+003E GREATER THAN (`>`) and U+007D RIGHT CURLY BRACE (`}`) are fine
- Expressions
  - JSX allows valid JavaScript inside expressions. 
  - We support anything in braces.
  - Because JSX parses JavaScript, but we don’t parse JavaScript
  - Brace counting in expressions，表达式中引号内的{}半个花括号也会计数，要求偶数

### Common MDX gotchas

- Markdown first looks for blocks (such as a heading) and only later looks for spans (such as emphasis) in those blocks.
  - This becomes a problem typically in the two cases listed below. 
  - However, as MDX has parse errors, parsing will crash, and an error will be presented.
- Blank lines in JSX spans
- U+003E GREATER THAN (`>`) seen as block quote

## [mdx parser](https://github.com/micromark/mdx-state-machine)

- The MDX state machine is used to tokenize MDX blocks and MDX spans. 
  - Blocks (also known as flow) make up the structure of the document (such as headings), 
  - whereas spans (also known as text or inline) make up the intra-paragraph parts of the flow (such as emphasis).
  - The initial state varies based on whether flow or text is parsed, and is respectively either Before MDX block state or Before MDX span state.
  - The final state is switched to by the MDX adapter, which right before completion will switch to either After MDX block state or After MDX span state.
- The MDX adapter handles tokens from the MDX state machine, which has further effects, such as validating whether they are conforming and figuring out when parsing is done.
  - Adapters are defined to handle a token either when a token enters right before it’s pushed to the stack, or when a token exits right after it’s popped off the stack
- The purpose of the `mdx-state-machine` is to tokenize.
  - The states of the MDX state machine have certain effects, such as that they create tokens in the stack and consume characters. 
  - The stack is used by adapters.
- The purpose of the adapter is to handle the results of the tokenizer.
  - The MDX adapter handles tokens, which has further effects, such as validating whether they are conforming and figuring out when parsing is done.
- To parse MDX is to feed the input character to the state of the state machine, and when not settled, repeat this step.
- How MDX is handled is intentionally undefined and left up to the host parser. 
  - When to feed an EOF is similarly undefined.
  - Host parsers must not support indented code and autolinks, as those conflict with MDX.
