---
title: lib-editor-quill-community-server-async
tags: [comment, quill, server]
created: 2024-04-15T15:50:36.128Z
modified: 2024-04-15T15:51:05.131Z
---

# lib-editor-quill-community-server-async

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-lazy
- ## 

- ## 

- ## [Question: Lazy load & append to end of existing delta content _201812](https://github.com/quilljs/quill/issues/2417)
- I think you want something like:

```JS
const delta = new Delta().retain(existingContentLength).concat(nextDeltaChunk);
quill.updateContents(delta);
```

- We've actually started exploring alternative solutions, while just dealing with the slow load. A new version may be coming out soon, and perhaps this will resolve it.

- ## ⚡️💥 [Initial rendering of long document performance _201604](https://github.com/quilljs/quill/issues/627)
- The rendering is a problem if you give editor.setContents directly an array of operations. The following fiddle will demonstrate the speed of the setContents for large operations (500 operations takes around 3 seconds and 1000 operations take around 10 seconds).
  - 💡 The solution to this is compose the deltas into one either on the client side before applying or server side before storing. The following fiddle demonstrates the performance with composed operations which takes 20 milliseconds to set.
  - https://jsfiddle.net/battuashwik/hf047xo7/

- I took at look at the specific ops that are performing slowly. I've confirmed that the output from editor.getContents() is in fact 1 single insert operation that is 93K characters long. So it's not an issue of too many operations. And so in this case I don't think that compose() would help
  - It is not exactly a single operation as new line is treated as a new operation and i see the problem in your case. Just updated the fiddle to demonstrate your exact case which takes around 600 ms which is a lot.
  - https://jsfiddle.net/battuashwik/1gds5ym9/
  - To verify this you can print the result from editor.getContents and check the ops array. You will see a series of operations rather than one.

- 💡 One alternative solution i can think of is doing lazy loading of operations. I updated the second fiddle https://jsfiddle.net/battuashwik/hf047xo7 to demonstrate that. 
  - This way atleast the browser will not freeze and hence better UI experience. 
  - You can also implement batching of operations instead of using setTimeout on every operation. Unfortunately to get the right number for batching you need to run some tests to figure out what is the exact threshold that updateContents starts to perform slow.
  - 这种方法可能的问题
    - 随着op分批执行文章内容会显示动态更新，~~一开始看到的内容陈旧、样式陈旧~~, (浏览器刷新很快应该感知不到)
    - 拆分op的粒度错误，比如只看到一半的表格
  - 可结合 懒加载、先compose再apply

- I did find a nifty trick to speed the heck out of Firefox though. Basically you just unmount the quill node, set your contents, then mount it again. This makes no difference in chrome, but in Firefox it speeds it up by over 40x! The same 20 minute task on the slow firefox machine now takes 15 seconds
# discuss
- ## 

- ## 

- ## 

- ## [[How to] drop embed (or html) inside quill editor from external source _201907](https://github.com/quilljs/quill/issues/2668)
- According to developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API#Define_the_drag's_data we just need to set to 'text/html' instead of 'text' or 'html' and it works fine!
