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
  - Alert, Confirmation, Full-screen
  - Trapping focus correctly for a modal dialog requires a complex set of events and interaction patterns that we feel is best not duplicated within the logic of this component. 
- elevation
- linear-progress
- snackbar
- theme

- ### adapter结构 methods for host interactions
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

 

- ### foundation结构 host-agnostic/indirect logic
- adapter
- defaultAdapter
- animationFrame
- animationTimer
- isCollapsed
- shouldFloat
- shouldShake

 

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

 

- ### component结构 public api proxying to methods in foundation
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

 
