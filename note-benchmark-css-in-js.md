---
title: note-benchmark-css-in-js
tags: [benchmark, css-in-js]
created: '2020-08-08T11:39:35.407Z'
modified: '2020-08-08T11:39:55.792Z'
---

# note-benchmark-css-in-js

## benchmarking

- css-in-js benchmarks app online /202008
  - https://github.com/necolas/react-native-web/tree/master/packages/benchmarks
  - https://necolas.github.io/react-native-web/benchmarks/
  - These benchmarks are approximations of extreme cases that libraries may encounter. 
  - Their purpose is to provide an early-warning signal for performance regressions. 
  - Each test report includes the mean(平均值) and standard deviation(标准差) of the timings, and approximations of the time spent in scripting (S) and layout (L).
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

## comparison

- [styled-components-vs-emotion](https://github.com/jsjoeio/styled-components-vs-emotion)
  - /20191025
  - emotion is ready for React Concurrent mode and it has a smaller bundle size

## ref

- MicheleBertoli/css-in-js /201809
  - https://github.com/MicheleBertoli/css-in-js
  - React: CSS in JS techniques comparison
  - only list supported features of libs
