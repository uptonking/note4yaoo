---
title: web-ux5-form-checkbox-radio
tags: [components, ui, web]
created: 2021-08-29T16:05:34.092Z
modified: 2021-08-29T16:06:25.175Z
---

# web-ux5-form-checkbox-radio

# guide

- checkbox对使用css修改样式支持度很有限
  - 就算自己修改了checkbox的样式，也很难保证跨平台的一致性
  - 不如一开始就不使用浏览器native默认样式，完全自定义
# discuss
- ## [Why cannot change checkbox color whatever I do?](https://stackoverflow.com/questions/24322599)
- Checkboxes are not able to be styled. You would need a third party js plugin there are many available.
  - In fact, you can style checkboxes quite easily with a few lines of CSS. No need for third-party plugins...the real problem is cross-browser compatibility, but that's for everything.
- The same problem will arise when trying to style that little down arrow on a dropdown `select` element.
- It's not possible to style checkbox inputs (nor radios) in css.
  - But you can create a custom checkbox and add a hidden checkbox or something like that. Which is what most people do because it can easily be compatible across browsers.
