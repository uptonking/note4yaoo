---
tags: [dev/mobile]
title: note-dev-mobile
created: '2019-06-09T05:37:46.916Z'
modified: '2020-06-22T09:10:01.467Z'
---

# note-dev-mobile
- 跨平台可选技术栈
  - react-native
  - flutter
  - hbuilder/apicloud
  - 考虑跨平台是否需要一致的ui与功能，如ios刘海屏、支付功能
  - 考虑同时维护多套移动端代码的成本，后台业务逻辑可通用

## features
- 跨平台一致的ui体验
- 动画支持
- 调用摄像头扫码

## react-native
- 优点
  - 跨平台
  - 大公司支持
  - 开发迭代快速，更快快速，h5更新有时可绕过审核
- 缺点
  - 引入react-native会增加打包体积，并且react-native的大小由facebook控制
  - 动画在低配设备上效果不佳
  - 进入app的react-native部分时，加载时间较长
  - react-native功能滞后于原生平台提供的新功能
  - 有时不会向后兼容，比如PropType被弃用
  - 定位问题需要时间判断是在react-native还是native
  - 代码容易产生多个分支，增加冲突解决与维护工作
  - 修复问题需要考虑3个技术栈

- 使用体验总结
  - aribnb
      - [20180620](https://medium.com/airbnb-engineering/react-native-at-airbnb-f95aa460be1c)
      - https://juejin.im/post/5b2a5368f265da595c0cf6d5
  - udacity
      - [20180703](https://engineering.udacity.com/react-native-a-retrospective-from-the-mobile-engineering-team-at-udacity-89975d6a8102)
      - https://juejin.im/post/5b421b606fb9a04fd15ff802

## android
- 开发因素
  - android设备过于碎片化，不同尺寸不同分辨率的设备ui体验很难一致
## ios
