---
title: lib-ui-spectrum-latest-roadmap
tags: [adobe-spectrum, roadmap]
created: 2021-04-12T16:24:57.306Z
modified: 2021-05-05T07:48:16.100Z
---

# lib-ui-spectrum-latest-roadmap

# guide

# roadmap
- https://react-spectrum.adobe.com/Support.html
- https://github.com/adobe/react-spectrum/projects
# breaking-changes

# release-notes

- ## React Aria's date and time picking components are coming along! 
- https://twitter.com/devongovett/status/1433833680187772931
  - All fully internationalized – i.e. non-Gregorian calendars, localized formatting, non-Latin numeral support, time zone support, etc. It's going to be pretty comprehensive!
- Some details: 
  - we're building a custom date and time manipulation library from scratch to support all of these i18n requirements since no existing library supports this. 
  - Doesn't rely on the JS Date object at all.
  - Despite this, it's 3x smaller than date-fns and tree shakeable too!
- This library will be **completely separate from React Aria/React Stately**, so it should be useful outside the context of React apps as well.
  - One day we hope to replace the internals with Temporal to make it even smaller once browsers support it.
- Keyboard control is one of the main features. 
  - We're following browser/native conventions with focusable segments for the year/month/day etc. 
  - Can type or use arrow keys to increment/decrement. 
  - Format follows locale. 
  - Unconstrained text entry is too hard to parse in all locales
- I'm assuming date and time pickers can be combined into a date-time-picker
  - Yeah the naming is still in flux, but DateField, DatePicker, and DateRangePicker also support times. There's a `granularity` prop to control that (e.g. day/hours/minutes/seconds).
# changelog
- [Standard card Component](https://github.com/adobe/react-spectrum/issues/2080)

- ref
  - [This chronological list](https://spectrum.adobe.com/page/whats-new/) shows all of the items that have been added or updated in the design system.
  - [releases](https://react-spectrum.adobe.com/releases/index.html)
