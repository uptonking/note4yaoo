---
title: lib-fwk-reef-blog
tags: [blog, reef, state]
created: '2020-11-04T17:20:10.860Z'
modified: '2020-12-08T13:26:33.515Z'
---

# lib-fwk-reef-blog

# reef-blog

## [Why I wrote my own vanilla JS alternative to Vue and React_201807](https://gomakethings.com/why-i-wrote-my-own-vanilla-js-alternative-to-vue-and-react/)
- simplicity
  - I find React confusing. 
    - It has a lot of moving parts and custom methods.
  - I like Vue’s simplicity
    - create a template, attach some data, and render
    - but don’t like how it mixes JS into the DOM with custom `v-` attributes that do things like loop through items and run conditionals. 
    - I’d rather that stuff happen in my JavaScript.
- Both React and Vue are pretty large at around 30kb minified and gzipped, 
  - and lock you in with a maze of proprietary methods.
  - I don’t want to transpile my code. I don’t want to use weird custom DOM attributes.
  - I just want to write clean markup, simple JavaScript, and build cool stuff.
- Reef does less
  - Reef is an anti-framework. It does a lot less than the big guys like React and Vue.
  - It doesn’t have a Virtual DOM.
  - It doesn’t automagically update the UI when state changes.
  - It doesn’t provide a bunch of custom methods.
- Reef does just one thing: render UI.
- Couldn’t you just use some template strings and innerHTML? Sure. 
  - But Reef sanitizes your data before rendering to minimize the risk of XSS scripting attacks. 
  - It also only updates things that have changed instead clobbering the DOM and removing focus from your form fields.
- How Reef.js works
  - Reef.js is used to create templates, attach data to them, and then use that data to render them into the DOM. 
  - You can update the data (or state), and update the template in the DOM to match.





- [Why do people choose frameworks over vanilla JS?(podcast audio)_201909](https://vanillajspodcast.com/why-do-people-choose-frameworks-over-vanilla-js/)
  - reefjs, sveltejs, Vanilla JS Toolkit

# state-ui-blog

## [How I built my own vanilla JS alternative to Vue and React](https://gomakethings.com/how-i-built-my-own-vanilla-js-alternative-to-vue-and-react/)

## [Adding reactivity to state based components with vanilla JS_201809](https://gomakethings.com/adding-reactivity-to-state-based-components-with-vanilla-js/)

## [Components, state, and vanilla JavaScript](https://gomakethings.com/components-state-and-vanilla-javascript/)

## [How to create a vanilla JS web app._201705](https://gomakethings.com/who-should-drive-a-vanilla-js-web-app/)

- I was able to get the functionality recreated in about 15 minutes, 
  - and spent my extra 5 minutes bolting in some nice extras like keeping the list of names persistent after reloading the page using localStorage. 
  - My version is incredibly ugly — Domenic's version is a much better designed 
  - but it’s functional and works without any dependencies

- [Refactoring a vanilla JS app with state based UI_201901](https://gomakethings.com/refactoring-a-vanilla-js-app-with-state-based-ui/)

## [Why event delegation is a better way to listen for events in vanilla JS](https://gomakethings.com/why-event-delegation-is-a-better-way-to-listen-for-events-in-vanilla-js/)
