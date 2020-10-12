---
title: note-ux-design-material-api
tags: [api, material-design]
created: '2020-10-10T16:34:57.054Z'
modified: '2020-10-10T16:40:37.832Z'
---

# note-ux-design-material-api

## materialcomponents for react

- https://github.com/material-components/material-components-web-react
  - 常用props
    - className,id,label,selected
  - 常用state
    - classList,leadingIconClassList,value
  - 实现的简单组件示例，如Fab
  - 在componentDidMount中创建MDCFoundation实例，并调用 `this.foundation.init();`
  - 在componentWillUnmount中调用 `this.foundation.destroy();`
  - adapter存取器方法的属性中很多setState
  - 一般都有根据props计算拼接再classes的方法
  - 组件暴露的handleChange等事件处理方法，大多都调用foundation中的方法
  - 函数ref可作为普通属性向下多级传递
  - foundation也可以放到state的属性中，参考Menu、select
    - [fix(text-field): put foundation on state and do render input unless foundation is present ](https://github.com/material-components/material-components-web-react/pull/353)
    - Well the inner components of a component will be initialized first. 
    - In this case, text field initializes before it considers itself "mounted". 
    - So the innerComp's componentDidMount is called before text field's componentDidMount. relies on the foundation existing, which only happens after the text field's componentDidMount.
    - So by adding foundation to state, we can guarantee that the will always have a foundation.
    - foundation is moved to state so that Text Field's componentDidMount will trigger a re-render through setState after initializing the foundation

``` JS
// 将复杂组件拆分成可组合的小组件
return (
  <div className={classes} {...otherProps}>
      {children}
    </div>
);
```

- https://github.com/prateekbh/preact-material-components
  - `abstract class MaterialComponent extends React.Component`
    - 实例属性: MDComponent,mdcProps,mdcNotifyProps,classText,control,ripple
    - 实例方法: render返回VNode,react生命周期，setControlRef,buildClassName,materialDom
  - 实现简单组件如Button/Checkbox/Fab时，只需实现materialDom方法，预定义组件的dom结构
  - 在componentDidMount中创建MDC组件实例，并注册事件监听器
  - 在componentWillUnmount中移除监听器，再调用MDC组件实例的destroy方法
  - 使用此方法创建react组件的优缺点
    - 工作量较小，因为直接使用了MDC组件的class
    - react组件的api完全自己定义，受MDC组件api变化的影响较小
    - foundation/adapter的架构从长远看更适合与其他前端框架集成

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

 

- ### 使用material-design-web的示例项目
- https://github.com/lucka-me/mapler
  - Web app to make map as wallpaper
  - 入口组件下只有4个二级组件，个别组件实现代码较长
  - 多次手动调用 `this.comp.init(parentNode)` 来挂载组件到parentNode下
  - 子组件通过 `this.parent.append(Element)` 挂载
  - 封装了创建html元素的方法 `document.createElement(tag)` ，未拼接html结构字符串
- https://github.com/gamesminer/Spotty-Vanilla
  - music streaming service，依赖vanilla js和firebase
  - 顶层组件或二级组件手动调用mount方法，mount方法中会调用mountChildren来初始化子组件，而mountChildren方法中又会调用下层子组件的mount方法，会自动初始化整棵dom树
  - mount方法中会动态创建子组件内容 `this.mountPoint.innerHTML = 'domstring'`
  - 通过ejs-loader将import导入的.html模板文件转换成js函数，来创建对应的html字符串

``` JS
// Use the "interpolate" delimiter to create a compiled template.
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'
```

- https://github.com/enbock/Time-Tracker
  - 基于react，但使用的是纯js `import * as mdc from 'material-components-web';`
  - 在componentDidMount中创建MDCTopAppBar对象，并添加 `listen('MDCTopAppBar:nav',handleEvent)`
  - `new mdc.topAppBar.MDCTopAppBar(ReactDOM.findDOMNode(this))`
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
  - 手动创建MDCDrawer等组件，并添加监听器
  - 通过 `document.createElement('div')` 动态创建元素，然后再创建MDCSnackbar组件实例
- https://github.com/ThisNameWasTaken/disaster-ready  
- https://github.com/littleGabriel/music-chart
