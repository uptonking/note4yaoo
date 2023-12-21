---
title: web-events
tags: [events, web]
created: 2019-10-17T08:31:14.028Z
modified: 2021-04-23T17:10:52.920Z
---

# web-events

# guide

# editor-events
- beforeinput 这个事件会在 `<input>, <select> 或 <textarea> 或者 contenteditable` 的值即将被修改前触发，这样我们可以获取到输入框更新之前的值
  - [Should the HTML `<select>` element dispatch `beforeinput` events? - Stack Overflow](https://stackoverflow.com/questions/72688184/should-the-html-select-element-dispatch-beforeinput-events)
    - The beforeinput event isn't supposed to fire on `<select>`, just like it doesn't fire on non textual inputs
# faq
- click vs touch

- ## [Are browser events in JavaScript asynchronous? - Stack Overflow](https://stackoverflow.com/questions/15317924/are-browser-events-in-javascript-asynchronous)
- 
- [Asynchronous or Synchronous calling of event handlers in javascript - Stack Overflow](https://stackoverflow.com/questions/15924014/asynchronous-or-synchronous-calling-of-event-handlers-in-javascript)
- All event handlers are fired synchronously and in order of binding.
- Some event handlers are executed synchonously and others asynchronously. See DOM-Level-3-Events

- ## [onKeyPress Vs. onKeyUp and onKeyDown](https://stackoverflow.com/questions/3396754)
- Note: `keypress` event has been deprecated, you should look to use `beforeinput` or `keydown` instead.
- order
  - keydown > keypress > (textInput >) keyup
  - 类似的顺序参考: mousedown > mouseup > click
  - 注意不同浏览器实现可能有差异
- keypress强调输入文本字符，按键ctrl/shift/alt都不会触发此事件

- The `blur` event fires when an element has lost focus. 
  - The main difference between this event and `focusout` is that `focusout` bubbles while `blur` does not.

- The `focus` event fires when an element has received focus.
  -  The main difference between this event and `focusin` is that `focusin` bubbles while `focus` does not.

- ## 如何实现用2点触控two (simultaneous) touches事件模拟右键菜单，多点触控如何区分不同功能手势如放大缩小、
  - `UIEvent.detail`
    - The `MouseEvent` object passed into the event handler for click has its `detail` property set to the number of times the target was clicked. 
  - `TouchEvent.targetTouches`
    - return a `TouchList` listing all the `Touch` objects for touch points that are still in contact with the touch surface and whose `touchstart` event occurred inside the same target element as the current target element.
    - The `TouchList` interface represents a list of contact points on a touch surface. 
      - For example, if the user has three fingers on the touch surface (such as a screen or trackpad), the corresponding `TouchList` object would have one `Touch` object for each finger, for a total of three entries.
  - Note that the threshold for pinch and zoom movement detection is application specific (and device dependent).
- react中分别有onClick和onDoubleClick, 但将这两个事件同时写在一个div上时，点击只会触发单击事件，应该怎么实现在一个div中同时绑定单击与双击事件？
  - This is not a limitation of React, it is a limitation of the DOM's click and dblclick events
  - 不要同时绑定这两个事件，只绑定单击事件，在单击事件的监听方法中
    - 通过setTimeout()设置一个延时200ms,并通过一个标志位变量count记录当前点击次数，如果在200ms内，再次点击，count++
    - 当setTimeout中的延时函数执行时，判断count值，1是单击，2是双击，然后执行对应的逻辑
  - 同时绑定单击和双击事件，在绑定的单击事件中，setTimeout设置一个延迟，双击事件中，clearTimeout这个延迟，再执行对应的方法
  - 还可以使用lodash的debounce，区别是同时监听onClick和onDoubleClick
  - 还可以使用promise来推迟onClick的执行，这种方式也称作cancelablePromise
  - ref
    - https://medium.com/trabe/prevent-click-events-on-double-click-with-react-with-and-without-hooks-6bf3697abc40
    - https://api.jquery.com/dblclick/
    - https://stackoverflow.com/questions/5497073/how-to-differentiate-single-click-event-and-double-click-event
  - 示例

```js
  let count = 0;
  class App extends Component {
    onClick = () => {
      count += 1;
      setTimeout(() => {
        if (count === 1) {
          console.log('do single click ', count);
        } else if (count === 2) {
          console.log('do onDoubleClick: ', count);
        }
        count = 0;
      }, 300);
    }

    render() {
      return (...)
    }
  }
```

# summary
- ref
  - https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers
  - https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Event_handlers
  - https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent
- event.stopPropagation()
  - 阻止继续冒泡，不让事件向document传播，但默认事件仍然会执行
- event.preventDefault()
  - 阻止默认行为，如调用此方法时链接不会被打开，但会发生冒泡，会传播到上一层父元素
- return false
  - 会同时阻止事件冒泡和默认行为
  - react使用自己包装的SyntheticEvent，return false不会阻止事件传播(从v0.14起)

- 💡 oneventtype vs addEventListener
  - onclick事件在同一时间只能指向唯一对象
    - 若分别指定window.onresize=f1/f2/f3时，只会生效在最后一个指定的事件
    - 若同时使用onresize和addEventListener时，会交替执行，若事件相同则重复执行!!！
    - 若使用addEventListener重复定义相同的listener事件，只会执行一次
    - 通过onXxx绑定的事件方法，只能在目标阶段和冒泡阶段执行
    - 通过addEventListener绑定的事件方法，我们可以通过第三个参数控制在捕获(true)或冒泡(false)阶段执行(默认为false)
  - addEventListener给一个对象注册多个listener
  - addEventListener对任何DOM都是有效的，而onclick仅限于HTML
  - addEventListener可以控制listener的触发阶段（捕获/冒泡），对于多个相同的事件处理器，不会重复触发，不需要手动使用removeEventListener清除
  - 对于IE9之前，相对应的是attachEvent和detachEvent
  - addEventListener
    - 连续执行 addEventListener('click', cbFnRefVariable)时，只注册了一个cb
    - 连续执行 addEventListener('click', ()=>{})时，注册了多个cb
    - allows the registration of event listeners on the event target. 
    - If an EventListener is added to an EventTarget while it is processing an event, it will not be triggered by the current actions but may be triggered during a later stage of event flow, such as the bubbling phase.
    - If multiple identical EventListeners are registered on the same EventTarget with the same parameters, the duplicate instances are discarded. 
    - They do not cause the EventListener to be called twice and since they are discarded they do not need to be removed with the removeEventListener method.
  - Although the inline event registration model is ancient and reliable, it has one serious drawback. 
    - It requires you to write JavaScript behavior code in your XHTML structure layer, where it doesn't belong.
    - **avoid** writing inline javascript. It makes it harder to debug

- onkeydown vs onchange
  - onkeydown: 当按键按下时，先触发事件发生，然后处理完后才会把按键对应的按键值显示在文本框中。当用户按下键盘按键时触发。
    - onkeypress event handler has been deprecated. You may want to use onkeydown instead。当键盘按键被按下并释放一个键时发生。
    - onkeypress事件不是适用于所有按键(如： ALT, CTRL, SHIFT, ESC)
    - onkeypress与onkeydown一样，也是先处理事件，再显示文本
  - onchange：当对象或选中区的内容改变且失去焦点时触发
# guide
- Events can be created with the `Event` constructor
  - This constructor is supported in most modern browsers (with Internet Explorer being the exception)
- To add more data to the event object, the `CustomEvent` interface exists and the `detail` property can be used to pass custom data
- The older approach to creating events uses APIs inspired by Java
  - `const event = document.createEvent('Event'); `
- Elements can listen for events that haven't been created yet by eventName

- `EventTarget` is a DOM interface implemented by objects that can receive events and may have listeners for them.
  - `Element`, Document, and `Window` are the most common event targets, but other objects can be event targets, too. 
  - For example `XMLHttpRequest`, AudioNode, AudioContext, and others.
  - Many event targets (including elements, documents, and windows) also support setting event handlers via `onevent` properties and attributes
- `eventTarget.addEventListener(type, listener [, options])`
- `eventTarget.removeEventListener()`
- `eventTarget.dispatchEvent(event)`
  - Unlike "native" events, which are fired by the DOM and invoke event handlers asynchronously via the event loop, dispatchEvent() invokes event handlers synchronously. 
  - All applicable event handlers will execute and return before the code continues on after the call to dispatchEvent().
  - dispatchEvent() is the last step of the create-init-dispatch process, which is used for dispatching events into the implementation's event model. The event can be created using Event constructor.
# Web-API-GlobalEventHandlers
- `onchange`
  - ref
    - https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event
  - change events fire when user commits a value change to a form control
  - change event is fired for `<input>` ,  `<select>` , and `<textarea>` element when an alteration to the element's value is committed by user 
  - Unlike the input event, the change event is not necessarily fired for each alteration to an element's value
  - change event fires at a different moment Depending on the kind of element
  - For some elements, including `<input type="text">` , the change event doesn't fire until the control loses focus. 
    - onChange事件只有在文本框失去焦点的时候才能触发
  - onBlur event is fired when you have moved away from an object without necessarily having changed its value.
  - onChange event is only called when you have changed the value of the field and it loses focus.
  - React组件主要使用onChange合成事件，作为文本输入框(input)或文字输入区(textarea)触发文字输入时的事件，这个事件用起来很直觉，理应当是如此
  - onChange在浏览器上，只要在这个文本输入框上，有任何的键盘动作它都会触发，也就是如果你是使用了中文、日文、韩文输入法(IME)，不论是哪一种，拼音的、笔划的还是其他的，只要有按下一个键盘的动作，就会触发一次浏览器上这个元素的change事件   
  - React attaches listeners for Component.onChange to the DOM element.oninput event. 
    - https://github.com/facebook/react/issues/3964
- `oninput` 事件
  - input event fires when the value of an `<input>` ,  `<select>` , or `<textarea>` element has been changed
  - oninput event occurs when the text content of an element is changed through the user interface.
  - The event also applies to elements with contenteditable enabled, and to any element when designMode is turned on.
  - input event is fired every time the value of the element changes. 
    - This is unlike the change event, which only fires when the value is committed, such as by pressing the enter key, selecting a value from a list of options, and the like.
  - For `<input>` elements with type=checkbox or type=radio, the input event should fire whenever a user toggles the control
    - However, historically this has not always been the case. 
    - use the change event instead for elements of these types.
  - ref
    - https://blog.csdn.net/freshlover/article/details/39050609
    - https://www.geekjc.com/post/5bcb2c34e6f24c5a85df4bff
    - https://segmentfault.com/a/1190000020098620
- onchange vs oninput
  - onchange事件在内容改变（两次内容不能相等）且失去焦点时触发，js直接更改value值时不触发
    - onpropertychange属性可在某些情况下解决上面存在的问题，不用考虑是否失去焦点，不管js操作还是键盘鼠标手动操作，只要HTML元素属性发生改变即可立即捕获到。遗憾的是，onpropertychange为IE专属的
  - oninput只在value改变时触发，oninput要通过addEventListener()来注册，js直接更改value值时不触发
  - 用js动态地设置input的值，会发现oninput和onchange事件都没有自动触发，解决方案是自己实现双向绑定
- `onselect`
    - select event only fires after text inside an `<input type="text">` or `<textarea>` is selected.
- `onanimationstart`
    - called when an animationstart event is sent, indicating that a CSS animation has started playing.   
- `ontransitionstart`
    - called when a transitionstart event is sent, indicating that a CSS transition has started transitioning.
# drag
- HTML drag-and-drop uses `DOM event model` and `drag events` inherited from mouse events.
- ondrag/start/enter/over/exit/leave/end
- ondrop
- Making an element `draggable` requires adding the `draggable` attribute and the `ondragstart` global event handler
- Each drag event has a `dataTransfer` property that holds the event's data. 
  - This property (which is a DataTransfer object) also has methods to manage drag data. 
- The `dropEffect` property affects which cursor the browser displays while dragging
- If an element is to become a drop zone or `droppable` , the element must have both `ondragover` and `ondrop` event handler attributes.
- ref
    - https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API
    - https://developer.mozilla.org/en-US/docs/Web/API/DragEvent
    - https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations
- The HTML5 specification includes support for drag and drop operations.
    - This is supported by all modern desktop browsers, but not by mobile browsers running under Android and IOS
- JavaScript权威指南P462 例17-2 拖动文档元素的例子中提到
    - 注意 `将mousemove和mouseup处理程序注册为捕获阶段` 的事件处理程序
    - because the user may move the mouse faster than the document element can follow it
    - 如果这种情况发生，某些mousemove事件会发生在原始目标元素之外，没有捕获，这些事件将无法分派正确的处理程序
    - addEventListener方式其实对capture或者bubble都无影响，因为反正都是监听在document之上，不管鼠标多快，不管是不是超出目标元素的范围，mousemove事件都会发生，所以总会把目标元素移动到指定鼠标的位置
    - 这里的考虑是针对ie浏览器的elementToDrag.attachEvent()这种方式的事件绑定，因为它将mousemove事件直接绑定在了目标元素上，那么如果鼠标移动太快，而元素没有跟上，那么mousemove事件就不会再目标元素身上发生，就触发不了处理函数

- 元素无论自身有没有定位，offsetParent返回的是距离自己最近的有定位的祖先元素，若祖先没有定位，则返回body
- offset值指的是元素外边到祖先元素内边的距离
- event.pageX若有滚动条，要包括页面拉上面的部分，若无滚动条，则page与client一致
- event.offset获取鼠标在盒子内部的位置
- event.client获取鼠标在浏览器内部的位置
- event.screen获取鼠标在显示器屏幕的位置
- 拖拽步骤
  - 获取初始位置clientX/Y
  - 获取移动后的位置clentX/Y，计算偏移量=移动后clientX-初始clientX
  - 给盒子的left和top加偏移量
- FastClick实现原理 
  - 将所有touch与mouse事件绑定到document.body上
  - 当某个div触发touch事件，将会冒泡到document.body上
  - 针对不同类型的touch事件，触发document不同的mouse事件
  - 然后接下来就是document.body的事件委托了

- 计算位置坐标
  - Element.getBoundingClientRect() 
    - returns the size of an element and its position relative to the viewport.
    - The returned value is a DOMRect object,  with read-only left, top, right, bottom, x, y, width, and height properties
    - Properties other than width and height are relative to the top-left of the viewport.

- ref
  - [搞清clientHeight、offsetHeight、scrollHeight、offsetTop、scrollTop](https://www.cnblogs.com/itjeff/p/15715949.html)

- scrollLeft 、scrollTop 可读可写
  - 设置或获取位于对象最左/顶端和窗口中可见内容的最顶/左端之间的距离，即当前上滚或左滚的距离（针对父容器）
- scrollHeight、scrollWidth
  - 获取对象可滚动的总高度/宽度（针对父容器）
- offsetLeft、offsetTop
  - 获取当前对象与父元素之间的距离（不包含父元素的边框，父元素是position不为static）
  - 这两个属性只能用于元素设置了overflow的css样式中，否者这两个属性没有任何意义。且overflow的值不能为visible，但可以为hidden, auto, scroll的之中，但是hidden最常见
  - scrollLeft：是该元素的显示（可见）的内容与该元素实际的内容的距离
  - 一开始scrollLeft的值为0，你就看到了你的页面最左边的内容，而不显示超过浏览器的那部分。当你向右拖动滚动条时，scrollLeft的值在增大，你就看到了右边隐藏的内容，而看不到左边隐藏的部分。就会从scrollLeft的位置开始显示，而不显示0-scrollLeft的元素内容。即：该元素的显示位置与实际内容的位置的距离变大。元素会从scrollLeft的位置显示该元素的内容
- offsetWidth、 offsetHeight
  - 获取元素自身的宽度/高度（如果是标准盒模型width+padding+border；如果是IE盒模型 width）
- clientLeft、 clientTop
  - 效果和边框宽度相同，很少使用
- clientWidth、 clientHeight
  - 不含边框的元素自身的宽度/高度（如果是标准盒模型 width+padding；如果是IE盒模型 width-border）
- Firefox的event不支持offsetX属性，兼容方法

```js
function getOffsetX(event) {
  var evt = event || window.event;
  var srcObj = evt.target || evt.srcElement;
  if (evt.offsetX) {
    return evt.offsetX;
  } else {
    var rect = srcObj.getBoundingClientRect();
    var clientX = evt.clientX;
    return clientX - rect.left;
  }
```

# scrollHeight/Top
- scrollHeight
  - 获取元素内容的高度，包括overflow属性导致的不可见内容，在没有垂直滚动条的情况下，scrollHeight值与元素视图填充所有内容所需要的最小值clientHeight相同
  - 包括content、padding，不包括margin
  - 只有DOM元素才有，window/document没有
  - 判断元素是否滚动到底 
    - element.scrollHeight - element.scrollTop === element.clientHeight

- scrollTop
  - **可读写**，其他client? 和offset? 都只读
  - 设置或获取一个元素不可见部分的顶部距离盒子border-top的距离
  - 当一个元素的容器没有产生垂直方向的滚动条, 那它的scrollTop的值默认为0
  - 设置scrollTop的值小于0，scrollTop被设为0
  - scrollTop属性只有DOM元素才有，window/document没有

- scrollLeft
  - 可读写
  - 设置或获取位于元素左边界和目前可见内容的最左端之间的距离

- onscroll
  - 当元素的滚动条滚动时触发的事件
  - element.onscroll=function(){}，元素包括DOM元素、window、document
  - 滚动条一定要出现，而且滚动条是属于外层元素，触发的是外层元素的onscroll事件
- window.scroll()
  - 让window滚动条滚动到那个x, y坐标
- window.scrollTo()
  - 等于window.scroll()
- window.scrollBy()
  - 让window滚动条相对滚动x，y的距离

- window.scrollX、window.scrollY只读不写
  - read-only scrollY property of the Window interface returns the number of pixels that the document is currently scrolled vertically.

## clientHeight

- clientHeight
  - 返回元素内部的高度，单位像素，只读
  - 包含content和padding，**不包含滚动条**、border和margin
  - `clientHeight = content height + padding - scrollbarHeight`
  - 对于inline的元素这个属性一直是0
  - 在没有滚动条时，scrollHeight===clientHeight恒成立
  - 练习中，不管有没有滚动条，document.body的scrollWidth与clientWidth一直相等

- clientTop
  - border-top的高度，及上边框的粗细宽度
  - https://developer.mozilla.org/en-US/docs/Web/API/Element/clientTop
- clientLeft
  - 元素的左边框的宽度，以像素表示
  - 如果元素的文本方向是从右向左RTL，并且由于内容溢出导致左边出现了一个垂直滚动条，则该属性包括滚动条的宽度

## offsetHeight

- offsetHeight
  - 包含content、padding、滚动条、border，**不包括margin**
  - 标准盒模型采用，设置style的height即这里
  - 对于inline的元素这个属性一直是0

- offsetLeft
  - 当前元素相对于其offsetParent元素的左边的距离
- offsetTop
  - 当前元素相对于其offsetParent元素的顶部的距离，即子边框外侧到父边框的内侧的距离

## window

- window.innerHeight 
  - DOM视口的大小，包括滚动条
- window.outerHeight
  - 整个浏览器窗口的大小，还包括标题栏、工具栏、状态栏等

## limitations

- In iOS UIWebViews, scroll events are not fired while scrolling is taking place; 
  - they are only fired after the scrolling has completed. 
  - See Bootstrap issue #16202. Safari and WKWebViews are not affected by this bug.
# keyboard 
- ref
  - https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key/Key_Values
- `onkeydown`
  - onkeydown/onkeypress/onkeyup在处理复制、粘贴、拖拽、长按键（按住键盘不放）等细节上并不完善
- `onkeypress`
  - This feature is no longer recommended. 
  - It may have already been **removed** from the relevant web standards
  - Note that some implementations may fire keypress event if supported. 
  - The events will be fired repeatedly while the key is held down.
# focus
- focus vs selection
  - Focus (which element is receiving user input events) is not the same thing as selection (the currently highlighted part of the document). 
  - You can get the current selection using `window.getSelection()` .

- The `activeElement` read-only property of the `Document` and `ShadowRoot` interfaces returns the Element within the DOM or shadow DOM tree that currently has focus.
  - Often `activeElement` will return a `HTMLInputElement` or `HTMLTextAreaElement` object if it has the text selection at the time
  - Other times the focused element might be a `<select>` element (menu) or an `<input>` element, of type "button", "checkbox", or "radio".
  - Typically a user can press the tab key to move the focus around the page among focusable elements, and use the space bar to activate one (that is, to press a button or toggle a radio button). 
    - Which elements are focusable varies depending on the platform and the browser's current configuration. 
# mouse 
- mousedown vs click
  - click is fired after a full click action occurs:
    - that is, the mouse button is pressed and released while the pointer remains inside the same element. 
  - mousedown is fired the moment the button is initially pressed.
  - 如果在某个地方按下鼠标后移开鼠标在另外一个地方松开鼠标会触发onmousedown事件，但是onclick事件却不会被触发
- `onmousedown`
  - mousedown event fires when the user depresses the mouse button **按下时**
  - mousedown event is fired at an Element when a pointing device button is pressed while the pointer is inside the element.
  - onmousedown > onmousemove > onmouseup
- `onclick`
  - ref
    - https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onclick
    - https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event
  - The click event is raised when the user clicks on an element.
  - It fires **after** both the mousedown and mouseup events have fired, in that order.
  - When using the click event to trigger an action, also consider adding this same action to the `keydown` event, to allow the use of that same action by people who don't use a mouse or a touch screen.
  - `target.onclick = functionRef; `
    - functionRef is a function name or a function expression. 
    - functionRef receives a MouseEvent object as its sole argument. 
    - Within the function, `this` will be the element upon which the event was triggered.        
    - Only one onclick handler can be assigned to an object at a time. 
      - You may prefer to use `EventTarget.addEventListener()` method instead, since it's more flexible.
  - An element receives a click event when a pointing device button (such as a mouse's primary mouse button) is both pressed and released while the pointer is located *inside* the element.
  - If the button is pressed on one element and the pointer is moved outside the element before the button is released, the event is fired on the most specific ancestor element that contained *both* elements.
  - MouseEvent object passed into the event handler for click has its `detail` property set to the number of times the target was clicked. 
    - In other words, detail will be 2 for a double-click, 3 for triple-click, and so forth. 练习中，最大为3，继续点就变成1
    - This counter resets after a short interval without any clicks occurring; 
    - the specifics of how long that interval is may vary from browser to browser
- `ondblclick`
  - ref
    - https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/ondblclick
    - https://developer.mozilla.org/en-US/docs/Web/API/Element/dblclick_event
  - The dblclick event is raised when the user double clicks an element. 
  - It fires **after** two click events (and by extension, after two pairs of mousedown and mouseup events)..
  - `target.ondblclick = functionRef; `
  - Only one ondblclick handler can be assigned to an object at a time. 
    - You may prefer to use the EventTarget.addEventListener()
- double click vs click
  - You can use a timeout to check if there is an another click after the first click.
  - If you don't need to mix them, you can rely on click and dblclick and each will do the job just fine.
  - A problem arises when trying to mix them
    - a dblclick event will actually trigger a click event as well
    - so you need to determine whether a single click is a "stand-alone" single click, or part of a double click.
  - u *shouldn't* use both click and dblclick on one and the same element
  - It is **inadvisable** to bind handlers to both the click and dblclick events for the same element. 
    - The sequence of events triggered varies from browser to browser, with some receiving two click events before the dblclick and others only one. 
    - Double-click sensitivity (maximum time between clicks that is detected as a double click) can vary by operating system and browser, and is often user-configurable.
  - You can use the event's `detail` property to detect the number of clicks related to the event. This makes double clicks inside of click fairly easy to detect.
  - The problem remains of detecting single clicks and whether or not they're part of a double click. For that, we're back to using a timer and `setTimeout` .
  - The maximum delay required for two consecutive clicks to be interpreted as a double-click is not standardized
  - React组件可以通过抽象出高阶组件DoubleClick记录点击次数
- mouseover vs mouseenter
  - mouseout和mouseleave类似
  - mouseover支持事件冒泡，mouseenter不支持事件冒泡 
    - mouseover从子元素进入父元素的时候，会触发父元素的mouseover事件，而mouseenter并不会
# CompositionEvent
- ref
  - https://developer.mozilla.org/en-US/docs/Web/API/CompositionEvent
  - https://segmentfault.com/a/1190000008023476
- The DOM CompositionEvent represents events that occur due to the user indirectly entering text
- Those events would fire when you type non-latin characters like Japanese with IME input to "compose" a word with one or more than two letters
- 组合事件是由compositionStart，compositionUpdate和compositionEnd三个事件的组合，Start和End事件只执行一次，Update会执行多次
- CompositionEvent(组成事件)可以辅助开发者，它可以在可编辑的DOM元素上触发，主要是input与textarea上，所以可以用来辅助解决change事件的输入法问题
- 共有三个事件，分别为compositionstart、compositionupdate与compositionend  
  - 它们代表的是开始进行字的输入的开始、更新与结束
  - 也就是代表开始以输入法编辑器来组合键盘上的英文字符，选字或刷新字的组合，到最后输出字到真实DOM中的文本输入框中
  - 每个中文字在输入时，compositionstart与compositionend都只会会被触发一次，而compositionupdate则是有可能多次触发
- 可以利用CompositionEvent作为一个信号，如果正在使用IME输入中文时，change事件中的代码就先不要运行，**等到compositionend触发时，接着change事件才可以运行**其中的代码，运作的原理就是这样简单而已
- 在React应用中，如果是一个"Uncontrolled"(不受控制的)的input组件，它与网页上真实DOM中的input元素的事件行为无差异，也就是说，直接使用CompositionEvent的解决方式，就可以解决这个输入法的问题

- Chrome浏览器在2016年的版本53之后，更改了change与compositionend的触发顺序
# event要点

## 元素宽高

- window.outerWidth是整个浏览器窗口的大小，包括标题栏、状态栏、developer窗口
- window.innerWidth和innerHeight是DOM视口的大小，包括内容、滚动条、边框，不包括developer窗口的宽度
  - 会导致handsontable的滚动条显示不出来
- document.documentElement.clientWidth：不包括滚动条，但包括边框
- document.body.clientHeight：不包括整个文档的滚动条，也不包括 `<html>` 元素的边框，也不包括 `<body>` 的边框和滚动条
- `documentElement` 是文档根元素，就是 `<html>` 标签，body就是 `<body>` 标签了，这两种方式兼容性较好，可以一直兼容到IE6
- 所有DOM元素都有4个属性，只需要给它固定大小并设置 `overflow:scroll` 即可表现出来
  - clientHeight：内部可视区域大小，不包括滚动条，包括边框
  - offsetHeight：整个可视区域大小，包括滚动条和边框
  - scrollHeight：元素内容的高度，包括溢出部分
  - scrollTop：元素内容向上滚动了多少像素，如果没有滚动则为0 

## 位置坐标

- ref
  - https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/offsetX
  - https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/clientX
  - https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/pageX
  - https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/screenX
  - https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/x
  - https://developer.mozilla.org/en-US/docs/Web/API/Window/scrollX
- offsetX/Y: 指鼠标指针相对于触发事件元素的左上角的偏移
  - 在Chrome/Safari中指外边缘，即将该元素边框的宽度计算在内，firefox/ie则不包含边框值
- clientX/Y是相对于浏览器视口viewport左上角的距离，参照点会随滚动条滚动而移动
  - 不包含标题栏、状态栏
- pageX/Y是相对文档左上角的距离，不会随滚动条移动
  - 当可视窗口和文档重叠(即无滚动条)时，pageX和clientX相等
  - 当可视窗口viewport出现滚动条时，clientX小于pageX
- screenX/Y: 鼠标位置相对于显示屏幕左上角的距离
- layerX/Y: FF特有，当触发元素没有设置绝对定位或相对定位，则以页面为参考点，如果设置了，则以触发盒子的左上角为参考点（包含border）
- x和y: IE特有，由于IE坐标选择十分混乱，故尽量不要使用
  - MouseEvent.x property is an alias for the MouseEvent.clientX property.
- 下面未标注的是各浏览器都支持的
  - e.offsetX：鼠标相对于事件源的X方向的距离 
  - e.offsetY：鼠标相对于事件源的Y方向的距离 
  - e.clientX：距离浏览器可视区域X方向的距离
  - e.clientY：距离浏览器可视区域Y方向的距离
  - e.pageX：鼠标相对于文档X方向的距离( ie678 不支持)
  - e.pageY：鼠标相对于文档X方向的距离( ie678 不支持)
  - e.screenX：鼠标距离屏幕X方向的距离
  - e.screenY：鼠标距离屏幕Y方向的距离
# hitTesting 点击测试
- [Flutter事件机制](https://book.flutterchina.club/chapter8/hittest.html)
  - Flutter 事件处理流程主要分两步，为了聚焦核心流程，我们以用户触摸事件为例来说明
  - 命中测试：当手指按下时，触发 PointerDownEvent 事件，按照深度优先遍历当前渲染（render object）树，对每一个渲染对象进行“命中测试”（hit test），如果命中测试通过，则该渲染对象会被添加到一个 HitTestResult 列表当中。
  - 事件分发：命中测试完毕后，会遍历 HitTestResult 列表，调用每一个渲染对象的事件处理方法（handleEvent）来处理 PointerDownEvent 事件，该过程称为“事件分发”（event dispatch）。随后当手指移动时，便会分发 PointerMoveEvent 事件。
  - 事件清理：当手指抬（ PointerUpEvent ）起或事件取消时（PointerCancelEvent），会先对相应的事件进行分发，分发完毕后会清空 HitTestResult 列表。
  - 命中测试是在 PointerDownEvent 事件触发时进行的，一个完成的事件流是 down > move > up (cancel)。
  - 如果父子组件都监听了同一个事件，则子组件会比父组件先响应事件。这是因为命中测试过程是按照深度优先规则遍历的，所以子渲染对象会比父渲染对象先加入 HitTestResult 列表，又因为在事件分发时是从前到后遍历 HitTestResult 列表的，所以子组件比父组件会更先被调用 handleEvent 。

- [命中测试 | 功能例子 | SpreadJS JavaScript 学习指南](https://demo.grapecity.com.cn/spreadjs/SpreadJSTutorial/features/workbook/hit-testing/purejs)
# more-layout-position
- https://caniuse.com/mdn-api_window_visualviewport
# dev
- ## `new Event()` + `dispatchEvent()` synthetic event
- bubbles by default is false
- Unlike "native" events, which are fired by the browser and invoke event handlers asynchronously via the event loop,  `dispatchEvent()` invokes event handlers synchronously. 
  - All applicable event handlers are called and return before `dispatchEvent()` returns.
