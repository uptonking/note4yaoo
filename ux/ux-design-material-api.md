---
title: ux-design-material-api
tags: [api, material-design]
created: 2020-10-10T16:34:57.054Z
modified: 2021-01-01T20:08:12.231Z
---

# ux-design-material-api

# material-design-components-web

- ## CompAdapter
- interface methods for host interactions
- 全是接口方法
- 可分类：样式读写、属性存取器、事件发布、组件其他行为

 

- ## CompFoundation
- host-agnostic/indirect logic
- 属性字段全部私有
- 暴露get/setXxx方法，而不暴露属性字段
- get/SetXxx方法大多通过调用adapter对象的方法实现

 

- ## Comp
- public api proxying to methods in foundation
- 构造函数中暴露this.root
- 有时会直接使用默认的MDCFoundation，而没有自己的f，如Modal
- 暴露属性存取器，存取器方法内会
  - 调用foundation的get/setXxx方法
  - 或直接读写dom属性，如this.nativeControl_.checked
- 暴露get/SetXxx方法，可以直接读写dom属性
- 暴露操作组件的方法，大多也会调用foundation对象中的方法
- adapter对象会在getDefaultFoundation()中创建
  - 样式读写通过this.root.classList.add/remove实现
  - 大多数操作都通过直接读写dom元素对象的属性实现

 

- ## components-catalog
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
  - Alert, Confirmation, Full-screen
  - Trapping focus correctly for a modal dialog requires a complex set of events and interaction patterns that we feel is best not duplicated within the logic of this component. 
- elevation
- linear-progress
- snackbar
- theme

- ## adapter结构 interface methods for host interactions
- addClass
- removeClass
- hasClass
- setStyle/Property/Attr
- addClassToLeadingIcon
- removeClassFromLeadingIcon
- eventTargetHasClass
- addBodyClass
- addClassForElementIndex
- addClassToElementAtIndex
- removeClassFromElementAtIndex
- addAttributeToElementAtIndex
- elementContainsClass
- elementHasClass

 

- isOpened
- isContentScrollable
- isFocusInsideList
- isRootFocused
- isRTL
- isSelectableItemAtIndex
- isAttachedToDOM
- isIndeterminate
- isChecked
- isFocused
- areButtonsStacked
- hasRadioAtIndex
- hasLeadingIcon
- hasNativeControl
- hasLabel
- hasOutline
- listItemAtIndexHasClass
- getAttribute
- setAttribute
- getComputedStyleValue
- getRootBoundingClientRect
- getContentHeight
- getViewportScrollY
- getTopAppBarHeight
- getTotalActionItems
- hasTrailingAction
- setPrimaryActionAttr
- setTrailingActionAttr
- getChipListCount
- getActionFromEvent
- getListItemCount
- getFocusedElementIndex
- getAttributeForElementIndex
- setAttributeForElementIndex
- setTabIndexForListItemChildren
- getPrimaryTextAtIndex
- getElementIndex
- getMenuItemCount
- getSelectedSiblingOfItemAtIndex
- setNativeControlDisabled
- setNativeControlChecked
- setNativeControlAttr
- getTabIndex
- setTrackStyleProperty
- setTrackMarkers
- setMarkerValue
- getOffsetLeft
- getOffsetWidth
- getContentOffsetLeft/Width
- getNativeInput
- getLabelWidth

 

- notifyClosed/Closing/Close
- notifyOpened/Opening/Open
- notifyNavigation
- notifyNavigationIconClicked
- notifyChange
- notifyInput
- notifyInteraction
- notifyInteracted
- notifyTrailingIconInteraction
- notifySelection
- notifySelected
- notifyRemoval
- notifyAction
- registerInteractionHandler
- deregisterInteractionHandler
- registerBodyInteractionHandler
- registerResizeHandler
- deregisterResizeHandler
- registerTextFieldInteractionHandler
- deregisterTextFieldInteractionHandler
- registerInputInteractionHandler

 

- removeAttribute
- removeFocusFromChipAtIndex
- removeNativeControlAttr
- removeChipAtIndex
- selectChipAtIndex
- getIndexOfChipById
- focusChipPrimaryActionAtIndex
- focusPrimaryAction
- announceMessage
- trapFocus
- releaseFocus
- restoreFocus
- saveFocus
- clickDefaultButton
- reverseButtons
- focusItemAtIndex
- focusListRoot
- closeSurface
- focusActiveNavigationItem
- forceLayout
- computeBoundingRect
- announce
  - Announces the snackbar's label text to screen reader users.
- activateIndicator
- deactivateIndicator
- focus
- shakeLabel
- floatLabel
- activateLineRipple
- deactivateLineRipple
- setLineRippleTransformOrigin
- notchOutline
- closeOutline

 

- ## foundation结构 host-agnostic/indirect logic
- adapter
- defaultAdapter
- animationFrame
- animationTimer
- isCollapsed
- shouldFloat
- shouldShake
- 还有很多以存取器形式定义的属性
  - get nativeControl_()

 

- opened
- closed
- isOpen
- isOpening
- isClosing
- isSelected
- isActive
- getValue
- setValue
- setSelected
- setSelectedFromChipSet
- setAlwaysCollapsed
- getAlwaysCollapsed
- getDimensions
- getSelectedChipIds
- getSelectedIndex
- setSelectedIndex
- setUseActivatedClass
- setWrapFocus
- setVerticalOrientation
- setSingleSelection
- setHasTypeahead
- setDefaultFocusState
- setEnabled
- setDisabled
- setChecked
- setDeterminate
- getTimeoutMs
- setTimeoutMs
- setFocusOnActivate
- setValid
- isValid
- isDisabled
- setDisabled
- setHelperTextContent

 

- handleClick
- handleChange
- handleInput
- handleKeydown
- handleTargetScroll
- handleWindowResize
- handleNavigationClick
- handleScrimClick
- handleInteraction
- handleTrailingIconInteraction
- handleTransitionEnd
- handleFocusIn
- handleFocusOut
- handleItemAction
- handleMenuSurfaceOpened
- handleTransitionEnd
- handleAnimationEnd
- handleActionButtonClick
- handleActionIconClick
- handleTextFieldInteraction

 

- open
- close
- beginExit
- removeFocus
- select
- layout
- focusNextElement
- focusFirstElement
- typeaheadMatchItem
- clearTypeaheadBuffer
- setProgress
- setupTrackMarker
- activate
- deactivate
- activateFocus
- deactivateFocus
- computeDimensions
- autoCompleteFocus

 

- ## component结构 public api proxying to methods in foundation
- foundation
- root
- getDefaultFoundation
- emit
- listen
- unlisten
- on
- id
- open
- close
- quickOpen
- isOpen
- active
- focusOnActivate
- items
- selected
- shouldRemoveOnTrailingIconClick
- ripple
- chips
- selectedChipIds
- escapeKeyAction
- scrimClickAction
- autoStackButtons
- vertical
- listElements
- wrapFocus
- typeaheadInProgress
- hasTypeahead
- singleSelection
- selectedIndex
- determinate
- indeterminate
- progress
- checked
- disabled
- value
- min/max/step
- timeoutMs
- closeOnEscape
- labelText
- actionButtonText
- useNativeValidation
- valid
- helperTextContent
- ripple
- leadingIconAriaLabel
- trailingIconContent
- prefixText
- suffixText
- 私有属性
  - this.nativeControl_
    - checkbox,radio,switch

 

- getOptionByIndex
- getPrimaryTextAtIndex
- setScrollTarget
- setSelectedFromChipSet
- setEnabled
- setAnchorCorner
- setAnchorMargin
- setAnchorElement
- setAbsolutePosition
- setFixedPosition
- setSelectedIndex
- setIsHoisted
- setDefaultFocusState
- setEnabled

 

- open
- close
- focus
- layout
- beginExit
- focusPrimaryAction
- focusTrailingAction
- addChip
- trapFocus
- removeFocus
- getPrimaryText
- initializeListType
- typeaheadMatchItem
- stepUp/Down
- activate
- deactivate
- computeIndicatorClientRect
- computeDimensions

 

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
- MDCDialog:opening
- MDCDialog:opened
- MDCDialog:closing
- MDCDialog:closed
- MDCList:action
  - Indicates that a list item with the specified index has been activated.
- MDCMenu:selected
- MDCDrawer:opened
- MDCDrawer:closed
- MDCSlider:input
- MDCSlider:change
- MDCSnackbar:opening/opened
- MDCTab:interacted	

 
