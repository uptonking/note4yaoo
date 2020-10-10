---
title: note-ux-design-material-api
tags: [api, material-design]
created: '2020-10-10T16:34:57.054Z'
modified: '2020-10-10T16:40:37.832Z'
---

# note-ux-design-material-api

## material-design-components-web

- ### components-catalog
- typography
- button
  - Icon, Disabled
- icon-button
- chips
  - Chips are compact elements that allow users to enter information, select a choice, filter content, or trigger an action.
  - 类似button group
- ripple
- layout-grid
- menu
- drawer
- tab-bar
- fab
- top-app-bar
  - Short, Fixed, Prominent, Dense
- text-field
- radio
- checkbox
- select
- switch
- slider
- card
- list
- image-list
- data-table
- dialog
- elevation
- linear-progress
- snackbar
- theme

- ### adapter结构
- addClass
- removeClass
- hasClass
- setStyle/Property/Attr
- addClassToLeadingIcon
- removeClassFromLeadingIcon
- eventTargetHasClass

 

- notifyClosed/Closing
- notifyOpened/Opening
- notifyNavigation
- notifyNavigationIconClicked
- notifyChange
- notifyInteraction
- notifyTrailingIconInteraction
- notifySelection
- notifyRemoval

 

- isOpened
- isRTL
- getAttribute
- getComputedStyleValue
- getRootBoundingClientRect
- getContentHeight
- getViewportScrollY
- getTopAppBarHeight
- getTotalActionItems
- hasLeadingIcon
- hasTrailingAction
- focusPrimaryAction
- setPrimaryActionAttr
- setTrailingActionAttr
- getChipListCount
- removeFocusFromChipAtIndex

 

- removeChipAtIndex
- selectChipAtIndex
- getIndexOfChipById
- focusChipPrimaryActionAtIndex
- announceMessage

 

- ### foundation结构
- adapter
- defaultAdapter
- animationFrame
- animationTimer
- isCollapsed

 

- handleClick
- handleTargetScroll
- handleWindowResize
- handleNavigationClick
- handleInteraction
- handleTrailingIconInteraction
- handleTransitionEnd

 

- isSelected
- setSelected
- setSelectedFromChipSet
- setAlwaysCollapsed
- getAlwaysCollapsed
- getDimensions
- getSelectedChipIds

 

- beginExit
- removeFocus
- select

 

- ### component结构
- on
- id
- selected
- shouldRemoveOnTrailingIconClick
- ripple
- chips
- selectedChipIds

 

- setScrollTarget
- beginExit
- focusPrimaryAction
- focusTrailingAction
- removeFocus
- setSelectedFromChipSet
- addChip

 

- MDCTopAppBar:nav
- MDCIconButtonToggle:change
- MDCChip:interaction
- MDCChip:selection
- MDCChip:removal
- MDCChip:trailingIconInteraction
- MDCChip:navigation
- MDCChip:interaction	
- MDCChip:selection
- MDCChip:removal
- MDCChip:navigation

 

- ### 使用material-design-web的示例项目
- https://github.com/lucka-me/mapler
  - Web app to make map as wallpaper
- https://github.com/gamesminer/Spotty-Vanilla
  - music streaming service，依赖vanilla js和firebase
- https://github.com/enbock/Time-Tracker
  - 基于react，但使用的是纯js `import * as mdc from 'material-components-web';`
- https://github.com/abraham/slides-today
  - Slides.today is a site dedicated to the presentations
  - 依赖 angular
- https://github.com/Growthfilev2/admin_panel
  - Admin Panel For Growthfile
- https://github.com/srinathh/reactmdcweb
- https://github.com/chrisromito/action_tracker
- https://github.com/nadsadin/nuppi_shoping
- https://github.com/ableron/ableron
- https://github.com/Cuke7/material_template
- https://github.com/jersoncarranza/sabroso
- https://github.com/squirrel-labs/GameLobby
- https://github.com/ThisNameWasTaken/disaster-ready  
- https://github.com/littleGabriel/music-chart
