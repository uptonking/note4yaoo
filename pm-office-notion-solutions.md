---
title: pm-office-notion-solutions
tags: [note-taking, notion, office]
created: 2022-11-25T10:08:57.343Z
modified: 2022-11-25T10:09:16.492Z
---

# pm-office-notion-solutions

# guide

# discuss
- ## 

- ## 

- ## 

- ## for notion staff_202207
- https://twitter.com/jitl/status/1550140132891791360
- March 2019:
  - total engineering team of 4
  - React Native to render a webview
- July 2022:
  - total engineering team of ~100
  - 3 iOS eng, 4 android eng
  - SwiftUI/Jetpack Compose renders home tab
  - Everything else is still a webview
- Web is the slowest option but the most cross platform. Native is the fastest option but the least cross platform. RN + react-native-web somewhere in the middle. Chose the right tradeoffs for your team, your users, your project, your market. 
- 
- 
- 
- 
- 


- ## Someone DM'd me to ask what tech we use in the Notion iOS/Android apps._202205
- https://twitter.com/jitl/status/1530326516013342723
  - They're hybrid native apps – idiomatic Kotlin/Swift + a webview running our web app.
  - We used React Native back in the day, but removed it by early 2020.
  - SQLite.
- Our strategy is to progressively nativeify more parts of our app as we grow the team.
  - 👉🏻 However, the editor will probably remain a webview for the foreseeable future, because of complexity tradeoff. 
  - Google Docs, Quip, Dropbox Paper, Coda - all use native shell, webview editor.

- It’s not so much SQLite that makes the desktop app fast — it’s more that the network makes web apps slow…
  - Just as a rough estimate, it takes about 15ms for light to travel from west coast to the east coast…
- It(react-native) added a ton of overhead to the app while providing no value in our hybrid app architecture. It made sense for bootstrapping when we had <5 engineers. 
- The editor has always been web on every platform. React Native drew two screens: (1) the webview, (2) the share sheet, shown when you share to Notion from a browser.
  - The advantage of React Native is allowing web developers to build phone app. If we already have webview for that, React Native does not add value.
- iOS & Android engineers chose Compose / SwiftUI for this and regretted it because not enough control over optimization. Yet another lesson to be conservative about tech adoption.
