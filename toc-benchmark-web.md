---
tags: [benchmark, toc]
title: toc-benchmark-web
created: '2019-12-22T12:19:22.028Z'
modified: '2020-06-16T02:56:17.442Z'
---

# toc-benchmark-web

## style-perf

- tests
  - https://github.com/necolas/react-native-web/tree/master/packages/benchmarks
  - https://necolas.github.io/react-native-web/benchmarks/
- Mount deep tree (50)
  - 13.12ms, css-modules 
  - 15.70ms, styled-components@^5.0.0   
  - 18.79ms, emotion@^10.0.27  
  - 22.78ms, react-jss@^10.0.4  
  - 30.01ms, inline-styles 
- Update dynamic styles (100)
  - 07.48ms, inline-styles 
  - 14.70ms, react-jss@^10.0.4
  - 22.44ms, emotion@^10.0.27  
  - css-modules 

## css-in-js

- https://github.com/MicheleBertoli/css-in-js
  - /201809

## table-perf
