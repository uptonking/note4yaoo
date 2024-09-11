---
title: lib-editor-codemirror-community-device-ios-android
tags: [codemirror, community, compatibility, ios]
favorited: true
created: 2024-08-11T06:41:17.954Z
modified: 2024-08-11T06:42:01.565Z
---

# lib-editor-codemirror-community-device-ios-android

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-ios
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 📱 [What is the purpose of settimeout of 10ms in updateForFocusChange? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/what-is-the-purpose-of-settimeout-of-10ms-in-updateforfocuschange/8369)
  - codemirror’s blur happens after a 10ms timeout, making it the last event, occurring after my event
- There are several types of interactions that will cause the editor to lose and then immediately regain focus (people implementing buttons that steal focus on mousedown but then immediately move it back to the editor, our own kludge for dealing with Android inappropriately closing the virtual keyboard in some situations). This timeout tries to isolate code tracking focus state from that kind of phantom(幽灵；幻觉) focus changes.
  - If you want to directly track DOM focus state, I’d recommend using a DOM event observer rather than an update listener. Those get the raw DOM events.
