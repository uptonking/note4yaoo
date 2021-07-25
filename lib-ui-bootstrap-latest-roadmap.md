---
title: lib-ui-bootstrap-latest-roadmap
tags: [bootstrap, lib, roadmap]
created: '2020-10-19T09:02:57.994Z'
modified: '2020-12-08T13:33:25.985Z'
---

# lib-ui-bootstrap-latest-roadmap

# roadmap

- We’ll likely add css grid support in with v5.1
# changelog
- ref
  - https://blog.getbootstrap.com/archive/
  - https://github.com/twbs/bootstrap/tags
  - https://v5.getbootstrap.com/docs/5.0/migration/

- v5.0.0-alpha1__20200617
  - New look and feel
  - jQuery and JavaScript: Bootstrap no longer depends on jQuery
  - Data attributes for all JavaScript plugins are now namespaced: use `data-bs-toggle` instead of `data-toggle`.
  - All plugins can now accept a CSS selector as the first argument. 
  - Upgraded from Popper v1.x to Popper v2.x.
  - CSS custom properties: dropped support for Internet Explorer
  - Updated forms
  - Utilities API
  - Enhanced grid system
  - Improved customizing docs
  - Coming soon: RTL, offcanvas, and more

- v4.0.0__20180119
  - Moved from Less to Sass.
  - Improved grid system to better target mobile devices.
  - Opt-in flexbox support is here
  - Dropped wells, thumbnails, and panels for cards. 
  - Consolidated all our HTML resets into a new module, Reboot. 
  - Brand new customization options by moving all options into Sass variables.
  - Dropped IE8 support and moved to rem and em units. 
  - Rewrote all our JavaScript plugins in ES6.
  - Improved auto-placement of tooltips and popovers thanks to Tether lib

- v3.4.0__20181214
  - Added a `.row-no-gutters` class
  - Resolved an XSS issue in Alert, Carousel, Collapse, Dropdown, Modal, and Tab components
  - Switched to BrowserStack for tests.
  - Replaced ZeroClipboard with clipboard.js
- v3.3.7__20160725
  - Added support for jQuery 3.
  - Removed unsupported vendor prefixes for @viewport.
- v3.0.0__20130820
  - New design and an optional theme! With v3, we've gone flat.
  - Mobile first and always responsive! 
  - Better box model by default. Everything gets box-sizing: border-box
  - With four tiers of grid classes—phones, tablets, desktops, and large desktops
  - Rewritten JavaScript plugins. All events are now namespaced, no-conflict stuff works way better, and more.
  - New Glyphicons icon font! 
  - Added some components! New to the mix are panels and list groups
  - Removed some components! accordion, typeahead, submenus

- v2.0.0__20120201
  - Essentially an entire rewrite of the library—docs, CSS, and JavaScript. 
  - Adds optional responsive CSS for nearly all components.
  - Updated grid system, now only 12 columns instead of 16
  - Responsive CSS is compiled separately, as bootstrap-responsive.css
  - New plugins: Collapse Carousel Typeahead

- v1.3.0__20130718
  - Javascript plugins for modals, alerts, dropdowns, scrollspy, tabs, tooltips, and popovers that work with jQuery and Ender
  - Inline labels for marking inline content with key visual flags
  - Media thumbnails
  - Breadcrumbs
- v1.0.0__20110819
  - Initial release of Bootstrap! 
  - Includes only CSS and docs (JavaScript plugins not added until v1.3)
