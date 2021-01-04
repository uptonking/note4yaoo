---
title: web-css-inherited-properties
tags: [css, web]
created: '2020-07-29T05:41:39.595Z'
modified: '2020-12-21T07:45:31.968Z'
---

# web-css-inherited-properties

# guide

- [css 2.1 Appendix F. Full property table](https://www.w3.org/TR/CSS21/propidx.html)

# inheritance

- In CSS, inheritance controls what happens when no value is specified for a property on an element.
- CSS properties can be categorized in two types:
  - inherited properties, which by default are set to the computed value of the parent element
  - non-inherited properties, which by default are set to initial value of the property
- The `inherit` keyword allows authors to explicitly specify inheritance. 
  - It works on both inherited and non-inherited properties.
  - `revert` keyword revert property to the user agent's default unless a user stylesheet exists

# non-inherited

- display

- box-sizing: content-box
- width: auto
- height: auto

- border-style
- border-color
- border-width

- background
- background-color

# inherited

azimuth
border-collapse
border-spacing
caption-side
color
cursor
direction
elevation
empty-cells
font-family
font-size
font-style
font-variant
font-weight
font
letter-spacing
line-height
list-style-image
list-style-position
list-style-type
list-style
orphans
pitch-range
pitch
quotes
richness
speak-header
speak-numeral
speak-punctuation
speak
speech-rate
stress
text-align
text-indent
text-transform
visibility
voice-family
volume
white-space
widows
word-break
word-spacing
word-wrap
