---
title: lib-toolkit-layer-reactjs-popup
tags: [layer, lib, reactjs-popup]
created: '2022-05-08T13:32:01.841Z'
modified: '2022-05-08T13:32:31.029Z'
---

# lib-toolkit-layer-reactjs-popup

# guide
- features
  - consistent solution: Modal, Tooltip, Menu : All in one library
  - Function as children pattern to take control over your popup anywhere
  - typescript support
  - zero dependencies

- modal不依赖trigger，tooltip和menu依赖trigger
  - It's important to mention that the controlled popup works for modal only 
  - and I think it does not make sense to use a controlled popup for tooltip and menu because we need the trigger element to calculate popup position.
# reactjs-popup-not-yet
- [Position is not recalculated on content change](https://github.com/yjose/reactjs-popup/issues/145)

- If you place the component inside a scrollable container, open the tooltip and then scroll the container, the tooltip position is not updated.
  - [content with fixed position on scroll](https://github.com/yjose/reactjs-popup/issues/208)
  - Unfortunately, bug still occurs. Quick and dirty workaround would be quit tooltip on scrolling.
  - 问题复现，在官方Custom Modal示例中，当modal中的tooltip打开时滚动body，tooltip会滚动，但modal是fixed的

- On Popup Open, we set focus to the first focusable element.
  - https://github.com/yjose/reactjs-popup/issues/250
  - Yes, please add an optional prop to disable this 

- [Rendering not in body](https://github.com/yjose/reactjs-popup/issues/232)
# discuss
- [is it possible to place popup code in one place and trigger in another?](https://github.com/yjose/reactjs-popup/issues/182)
- change trigger={refToInput.current} by ref={refToInput} and you ref should have access to Native Components functions such us openPopup

# 
# docs
- Starting from v2 you can customize where the popup is rendered on the page!
  - By default a `div` with id `popup-root` is appended to the very end of the `body` tag and the popup content is rendered inside, 
  - but if an element with this id already exists, this will be used instead.
  - This can be helpful when you need your popup to render inside of React's root element.

- reactjs-popup is built to be a tooltip by default

- If you need to have more control over your component, we provide function as a child pattern to get access to `close` popup action.
- It's important to mention that the **controlled popup works for modal only** 
  - and I think it does not make sense to use a controlled popup for tooltip and menu because we need the trigger element to calculate popup position.

- Starting from v2 you need to add `nested` to Popup to make sure nested Modal/tooltips will work as expected
