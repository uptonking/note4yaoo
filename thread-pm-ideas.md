---
title: thread-pm-ideas
tags: [ideas, thread]
created: '2021-01-17T17:13:54.678Z'
modified: '2021-01-17T17:14:34.313Z'
---

# thread-pm-ideas

# repeat

# ideas

- ## 

- ## Floating field labels are bad for accessibility! Don’t use them just because Google does.
- https://twitter.com/devongovett/status/1364577800116711424

- ## Quick tip: don't use a datepicker on date of birth fields. That's dumb.
- https://twitter.com/brad_frost/status/1362771518137249794
- Working with localization, I would say that it’s not dumb at all. 
  - Lots of people fill out in wrong order since they have different format for the date.
- Why do date pickers for birth dates always start on the most granular level (days)?  
  - Why not show a grid of years (easy to scroll) > select month > select day? 🤔 
  - Date pickers are a super powerful UI component, but are rarely implemented correctly

- ## How we built a profile card generator for Storybook
- https://storybook.js.org/blog/generative-image-service/
- No dev blog is complete without custom auto-generated social images

- ## If you are wanting to reference a tweet on a page, don't embed, just use a simple image + alt text + link.
- https://twitter.com/TheRealNooshu/status/1350578919389470721
- Just a note that https://tweetcyborg.com converts a tweet to a simple image for you. 
  - No idea if this is the best service to do it, but it works
- What about inlining a copy of the tweet, with minimum styles, like I did here for example?
  - I’m using this plugin for @eleven_ty , if it can be an inspiration
- I've found exactly the same thing. 
  - Twitter's embedding is very inefficient. 
  - I'm still trying to find something which will turn it into an image + alt text + link automagically. 
