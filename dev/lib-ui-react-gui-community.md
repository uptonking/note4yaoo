---
title: lib-ui-react-gui-community
tags: [community, react-gui]
created: 2021-07-12T05:41:00.288Z
modified: 2021-07-12T05:41:18.380Z
---

# lib-ui-react-gui-community

# discuss-stars

- ## What is react-gui?
- https://github.com/reactwg/react-18/discussions/71
- This is a personal experiment I moved to a FB repo to share with colleagues. 
  - There is no official relationship with React. 
  - We are experimenting with it in a few places at FB in a very limited way, and at this stage there are no current plans for a publicly supported release. 
  - Some ideas from it have been feeding back into React Native for Web and discussed with the React Native team, 
  - but it's too early to say whether this will become anything more.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## React GUI is an exploration of what React Native's APIs could look like if they were more modular, more composable, expanded beyond mobile touch interfaces, and modeled on web standards.
- https://twitter.com/ReactWeb/status/1442563831775956996
- This looks cool, but I think it’s worth noting it’d look messier with evt callbacks that:
  - are defined in the component, since the hook wraps them in both an object and the hook call
  - need to be memo’d. Yet another wrapper
  - are used alongside a ref callback. What is what?
- Headless UIs would benefit. Logic and styles can be separated.

- ## It looks like Facebook will release react-gui soon. 
- https://twitter.com/estejs/status/1414259301632385027
  - It looks like it's heavily inspired maybe slightly changed React Native for Web.
  - As I checked source code, it really looks like RNfW revamped for web only. So much goodness there.
- React Native for Web is React Native for web. react-gui seems to be React Native for Web for web only.
- react-gui seems to be less strict React Native for Web.
