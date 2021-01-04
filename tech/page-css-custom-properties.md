---
title: page-css-custom-properties
tags: [css]
created: '2020-10-31T19:48:24.822Z'
modified: '2020-10-31T19:50:54.156Z'
---

# page-css-custom-properties

# [Why we prefer CSS Custom Properties to SASS variables](https://codyhouse.co/blog/post/css-custom-properties-vs-sass-variables)

1. Creating and applying color themes 
- Note that in the dark theme we need to go through each property where the color variables were used, and update them with a new variable
- While building our framework, we came up with a different approach based on CSS variables
- The important point is that we don't need to create new color variables for our second (dark) theme
- you can nest color themes

2. Controlling the type scale 
- we decided to incorporate the whole scale formula into the custom-style/_typography.scss file
- It gives you the possibility to control the whole typography system by editing only two variables

3. Controlling the spacing scale 
4. Editing vertical rhythm on a component level #
- One way to take advantage of this feature is injecting custom properties into other custom properties, thus creating 'controls' that can be edited on a component level

5. Abstracting components behaviour 
6. What's the catch?
7. Can I use CSS variables with a preprocessor? 
8. Conclusion 

- In this article, we've gone through a few examples that demonstrate what's the advantage of using CSS custom properties over SASS variables. 
- We've focused on how they enable you to create 'controls' that speed up the way you modify components, or set rules that affect typography and spacing
