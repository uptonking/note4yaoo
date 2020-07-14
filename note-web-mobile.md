---
title: note-web-mobile
tags: [mobile, web]
created: '2020-06-21T08:14:11.535Z'
modified: '2020-07-14T10:35:56.201Z'
---

# note-web-mobile

## features-for-mobile

- 手机端的事件特点
  - touch事件
  - 没有hover
- 移动端要少用
  - 少用滚动条，占据空间且不美观
  - 少用resize事件，拖动手势比点击复杂
- 导航菜单项较多时，竖向放置更友好
- 移动端浏览器，向上滑时会隐藏上面的url地址栏和下面的导航菜单，来增大显示空间

## faq

- 移动设备上的web网页是有300ms延迟的，往往会造成按钮点击延迟甚至是点击失效
  - 这是由于区分单机事件和双击屏幕缩放的历史原因造成的
  - fastclick可以解决在手机上点击事件的300ms延迟
  - zepto的touch模块，tap事件也是为了解决在click的延迟问题
  - 触摸屏的相应顺序为touchstart-->touchmove-->touchend-->click，也可以通过绑定ontouchstart事件，加快事件的响应，解决300ms的延迟问题
- fixed定位缺陷
  - ios下fixed元素容易定位出错，软键盘弹出时，影响fixed元素定位
  - android下fixed表现要比iOS更好，软键盘弹出时，不会影响fixed元素定位
  - 解决方案： 可用iScroll插件解决这个问题

## pieces

- 一些情况下对非可点击元素（label，span）监听click事件，ios下不会触发，css增加 `cursor：pointer` 就搞定了
- 防止手机中网页放大和缩小

``` html
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=0" />
```

- 设置Web应用是否以全屏模式运行

``` 
<meta name="apple-mobile-web-app-capable"content="yes">

```

- 禁止复制、选中文本

``` 
user-select: none;
```

- 手机页面通常在第一次加载后会进行缓存，然后每次刷新会使用缓存而不是去重新向服务器发送请求。如果不希望使用缓存可以设置no-cache

``` 
<meta http-equiv="Cache-Control"content="no-cache"/>
```

- ios设置input按钮样式会被默认样式覆盖

``` css
input,
textarea {
  border: 0;
  -webkit-appearance: none;
}
```
