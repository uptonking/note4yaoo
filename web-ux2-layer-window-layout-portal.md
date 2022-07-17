---
title: web-ux2-layer-window-layout-portal
tags: [components, portal, ui, window-layout]
created: 2021-01-13T17:13:36.979Z
modified: 2021-07-29T20:39:09.187Z
---

# web-ux2-layer-window-layout-portal

# guide

- iframe页面没有自己的历史记录，使用的是基座(父页面)的浏览历史
  - 当iframe页在内部进行跳转时，浏览器地址栏无变化，基座中加载的src资源也无变化
  - 当浏览器刷新时，无法停留在iframe内部跳转后的页面上，需要用户重新走一遍操作
# faq

## 如何将多个传统网站页面集成合并，组成一个portal门户目录，且冲突尽可能少

- 暂时没找到直接的方法，因为原本各网站的文字链接、资源url地址都会变化
- 可考虑重新开发

- ref
  - [Multiple web applications into one portal](https://stackoverflow.com/questions/8100098/multiple-web-applications-into-one-portal)
# iframe
- ## [iframe有什么好处，有什么坏处？](https://www.zhihu.com/question/20653055)
- 浏览器兼容性特别好
- iframe原本的用法在现在看来是不合时宜的，问题太多了但是它的其他功能却是不错的黑魔法，这里列举一些
  - 用来实现长连接，在websocket不可用的时候作为一种替代，最开始由google发明。Comet：基于 HTTP 长连接的“服务器推”技术
  - 跨域通信。JavaScript跨域总结与解决办法 ，类似的还有浏览器多页面通信，比如音乐播放器，用户如果打开了多个tab页，应该只有一个在播放
  - 历史记录管理，解决ajax化网站响应浏览器前进后退按钮的方案，在html5的history api不可用时作为一种替代。
  - 纯前端的utf8和gbk编码互转。
    - 比如在utf8页面需要生成一个gbk的encodeURIComponent字符串，可以通过页面加载一个gbk的iframe，
    - 然后主页面与子页面通信的方式实现转换，这样就不用在页面上插入一个非常巨大的编码映射表文件了
  - 用iframe实现无刷新文件上传，在FormData不可用时作为替代方案
  - 在移动端用于从网页调起客户端应用
  - 创建一个全新的独立的宿主环境。
    - iframe还可以用于创建新的宿主环境，用于隔离或者访问原始接口及对象，
    - 比如有些前端安全的防范会覆盖一些原生的方法防止恶意调用，那我们就能通过创建一个iframe，然后从iframe中取回原始对象和方法来破解这种防范。
- 可以用于单页面项目强制更新title
- 可以做委托提交，使页面不刷新、不跳转

- ## [为什么前端尽量少用iframe？](https://www.zhihu.com/question/23683645/answers/updated)
- 因为iframe等于打开一个新的网页，所有的JS/CSS全部加载一遍，内存会*2，无法释放，典型的内存泄露
  - 最近一个vue项目，一个组件用到了iframe，每次切换路由，会销毁这个组件，再重新加载，
    - 在火狐浏览器下，切换几十次内存占用暴增，最后浏览器崩溃，但是在谷歌浏览器下一切正常，
    - 通过各种方法最终定位到是iframe导致的内存泄漏，就是因为每次组件销毁但是iframe的内存在火狐下不会被释放，谷歌没有这种问题。
    - 解决方法是：把iframe提取到上一层组件，只加载一次，切换路由不会重新加载iframe，就一切正常了。
- 移动端对iframe不友好
  - 最近有个项目在移动端使用iframe，解决了安卓IOS又出问题，解决完ios安卓又出问题
- iframe是(几乎)不能访问外部数据的，js的作用域也会很奇怪
- iframe会阻塞主页面的Onload事件；
  - 动态创建iframe利用src来进行异步加载就可以避免上面的问题了
- iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。
- 当时是基于iframe实现布局方便考虑的，没成想这是一个巨大的坑，
  - 内容区域iframe高度自适应可把我们坑苦了，然后布局上出现各种怪异的问题
# discuss
- ## 50% of my job is reminding designers that they can't have tooltips on elements that aren't focusable. Stop it!
- https://twitter.com/devongovett/status/1430234270375636993
  - Usually it's random text (e.g. truncation), or icons. Disabled buttons are also a very common one.
- In the case of truncation, I imagine it’s similar to what Safari does natively? Is there a proper way to mimic that and retain accessibility?
  - That's the reason why I have an abstracted out Actionable utility in Arcade as well. Disabled buttons tooltips are not my favourite but we had a discussion
  - We're working on this instead: 添加一个添加的类似i的提示图标，鼠标不能聚焦到不可用button，但可以聚焦到不可用button旁边的i型icon
- I may regret asking this, but why can you not have a tooltip on a non-focusable element?
  - So that users that navigate using a keyboard can access it
  - Some users use a keyboard but not a screen reader, and the target needs to be focusable for them to access the tooltip.
# ref
- [iframe接班人-微前端框架qiankun在中后台系统实践](https://zhuanlan.zhihu.com/p/259209543)
