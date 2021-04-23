---
title: web-ux-ui-shell
tags: [components, ui, ui-shell]
created: '2020-12-28T10:06:47.657Z'
modified: '2021-04-23T15:42:07.105Z'
---

# web-ux-ui-shell

# Overview

- ## [UI shell carbon-v9](https://v9.carbondesignsystem.com/experimental/ui-shell/usage)
- The UI shell is the top level in a product's UI. 
  - The UI shell consists of the primary header and footer, as well as header panels that are used for navigation and global UI services.
- The shell is divided into 3 distinct "zones" which establish purpose and level of control.
  - The global zone holds the IBM global platform switcher, 
    - which allows the user to quickly navigate between different IBM platforms. 
    - This zone cannot be altered by the platform or product owner.
  - The platform zone contains platform-level elements, which could include functions like search, docs, support, profile, and notifications. 
    - Platform owners can also choose to include custom top-nav text links in this zone.
  - The local zone is controlled at the product level. 
    - It contains the product-level side nav as well as the main content area.
- The UI shell is designed to be configurable. 
  - A product/platform can choose which shell components and configurations to use.
- The header spans the full width of the viewport and is the topmost element in the UI. 
  - Header elements are persistent within a product.
  - Header responsive behavior
- These are vertical panels that are anchored in the header and invoked by controls on the right side of the header. 
  - The profile and notifications panels are examples of this element. 
  - Header panels are always treated as floating panels.
- Side-nav panels
  - These panels contain product-level navigation and can be either fixed-width or flexible

- ## [UI shell carbon-v10](https://www.carbondesignsystem.com/components/UI-shell-header/usage)
- A shell is a collection of components shared by all products within a platform. 
  - It provides a common set of interaction patterns that persist between and across products.
- The UI shell is made up of three components—the header, the left panel, and the right panel.
  - All three can be used independently, but the components were designed to work together.
- The UI shell header is the foundation for navigating and orienting your user to the UI.

- The left panel contains secondary navigation and is positioned below the header and fixed to the left. 
  - Both links and sub-menus can be used in the side-nav and may be mixed together.
- Use the left panel if there are more than five secondary navigation items, 
  - or if you expect a user to switch between secondary items frequently. 
- Sub-menus are denoted with a chevron(V型符号/标志) and expand when clicked, pushing the other items down in the panel. 
  - To collapse the sub-menu, the user must again click the menu header in the left panel.
- The left panel does not support three tiers of navigation. 
  - If you have additional content to display beneath a sub-menu, use tabs within the page.

- The right panel is invoked by icons on the right side of the header, and remains anchored to that icon. 
  - Right panels have a consistent width, span the full height of the viewport, and are flush to the right edge of the viewport.
- Right panels always float over page content, 
  - and always remain anchored to their associated icon. 
  - You can have multiple right panels, but only one can be expanded at any time.
- To dismiss the panel, a user must select an item, or click or tap the header icon.
- There is no selected state for right panel items. 
  - Even if a user is currently within one of the panel items, the item remains unselected.
