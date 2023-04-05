---
title: lib-xplat-react-native-blog
tags: [blog, react-native]
created: 2021-09-11T16:39:27.862Z
modified: 2021-09-11T16:39:49.984Z
---

# lib-xplat-react-native-blog

# guide

# [shopify: Migrating our Largest Mobile App to React Native_202212](https://shopify.engineering/migrating-our-largest-mobile-app-to-react-native)

- Build and Migrate, All at Once
  - we decided to gradually start adopting React Native in the app instead of doing a full rewrite.
  - Any change to the design system had to be done three times—once in native Android, once in native iOS, and once in React Native
  - we first needed to make sure that all the engineers on our team knew how to write React Native code.
  - Identifying and Prioritizing What to Migrate 
  - we decided that we should go all-in and prioritize high-impact screens first, like the root screens of the app.
- Benefits of the Move
  - Reducing Implementation Differences Between iOS and Android
  - More Hands Make Lighter Work
  - Simpler Code
- A Few Bumps in the Road
  - FlashList - A performant variant of FlatList
  - React Native Skia - High Performance 2D Graphics in React Native
  - React Native Performance - A Performance monitoring framework
- Native Routes
- Deeplink Support
- Safe Area
# [Twitter's div Soup and Uglyfied CSS, Explained](https://giuseppegurgone.com/twitter-html/)
- Twitter web is a complex application built with React Native for Web 
- React Native provides a small number of cross platform primitives that are the building blocks for your application. 
  - View, Text, Image, Touchable, Button
- To ensure reliable interactions like touch or gestures and to provide a higher degree of compatibility, React Native for Web reimplements some web primitives making sure that semantics and accessibility are preserved if not enhanced.
- Because of this some of the primitives compile to `div`, hence the div soup that is visible when inspecting twitter.com
  - Most of this code compiles to divs with appropriate, though sometimes redundant, accessibility attributes
  - The accessibility tree produced by our code snippet looks correct
  - The framework author has put in a lot of effort into producing advanced yet accessible components that give us better cross platform primitives.
-  “What’s wrong with native elements?” “Why not use web platform primitives that come with semantics and built-in behavior?”.
- Why reimplement a button when the web platform provides one?
  - The short answer is that the button element doesn’t support flexbox children 
  - and on touch devices the implementation of the web platform button is not good enough to match the behavior of correspondent mobile native versions.
- Why would you output a div with a paragraph role when you can use a p element instead?
  - The “paragraph” role isn’t mapped to a `<p>` tag because it’s an HTML conformance error to include block-level children within the element; 
  - in React Native for Web both Text and View support block-level children.
- Looking at the final HTML produced by React Native for Web, it is impossible not to notice the abundant amount of hashed CSS class names that goes with every element.
  - The classes prefixed with `css-` are for CSS rules that define base styles for the View, Text, Image and TextInput primitives.
  - Imagine those as User Agent styles but for the React Native primitives.
  - The other type of class name is the one prefixed with `r-`. These are for styles authored by the consumers of the framework
- React Native for Web implements the React Native StyleSheet API and produces atomic CSS class names that are resolved deterministically in application order.
  - Styles are authored in JavaScript using the `StyleSheet.create` API which accepts an object of name-rule pairs. 
  - Developers can then reference rules by name using the dictionary returned by` StyleSheet.create`.
- How can devs make sense of all of this?
  - Even knowing all the implementation details mentioned above, the disconnect between source code and output can make it hard to use the browser developer tools to debug an application built with React Native for Web.
  - React Developer Tools have first-class support for React Native and come with a panel to inspect primitives and edit styles.

- conclusion
  - While not being a good choice for every kind of website, React Native for Web is a framework that can help developers build better cross platform applications.
  - The not-so human readable source code of twitter.com is the output of a framework that provides new, cross platform primitives which overcome the limitations of similar web platform primitives.
