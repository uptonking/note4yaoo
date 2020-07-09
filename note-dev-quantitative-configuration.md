---
tags: [dev, quantitative]
title: note-dev-quantitative-configuration
created: '2020-07-09T13:26:54.403Z'
modified: '2020-07-09T13:30:55.664Z'
---

# note-dev-quantitative-configuration

## frontend

- bootstrap 4的breakpoints

``` 
$font-size-base:  1rem !default; // Assumes the browser default, `16px`
$font-size-lg: $font-size-base * 1.25 !default;
$font-size-sm: $font-size-base * .875 !default;

$grid-breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px
) !default;
```
