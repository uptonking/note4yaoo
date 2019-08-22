---
tags: [web]
title: note-web-dom
created: '2019-08-01T16:03:46.398Z'
modified: '2019-08-16T10:31:33.999Z'
---

# note-web-dom

## element

- select vs dropdown
    - select各浏览器都有实现，dropdown需要自己实现
    - select各浏览器实现的样式不统一，难以跨平台体验一致
    - select可用于form
- html全局属性可用于任何 HTML 元素
	- accesskey	规定激活元素的快捷键。
	- `class`	规定元素的一个或多个类名（引用样式表中的类）。
	- contenteditable	规定元素内容是否可编辑。
	- contextmenu	规定元素的上下文菜单，上下文菜单在用户点击元素时显示。
	- `data-*`	用于存储页面或应用程序的私有定制数据。
	- dir		规定元素中内容的文本方向。
	- `draggable`	规定元素是否可拖动。
	- `dropzone`	规定在拖动被拖动数据时是否进行复制、移动或链接。
	- `hidden`	规定元素仍未或不再相关，浏览器不应显示已规定 hidden 属性的元素。
	- `id`	规定元素的唯一 id。
	- lang	规定元素内容的语言。
	- spellcheck	规定是否对元素进行拼写和语法检查。
	- `style`	规定元素的行内 CSS 样式。
	- `tabindex`	规定元素的 tab 键次序。
		- tabindex 属性规定元素的 tab 键控制次序（当 tab 键用于导航时）
		- 以下元素支持 tabindex 属性：<a>, <area>, <button>, <input>, <object>, <select> 以及 <textarea>。
	- title	规定有关元素的额外信息。
	- translate	规定是否应该翻译元素内容。
- `<dl><dt><dd>` 定义带缩进的列表
	- dt是title
	- dd是带缩进的内容
- dom中的表单元素，表单用于采集用户输入，主要3种input、textarea、select
	- `<form>`
		- fieldset, legend
	- `<input>`
		- label：为input 元素定义标记，使用for属性和input元素的id进行绑定
		- 属性：type, checked, disabled, accept
		- 可选type
			- text
			- password
			- file
			- checkbox	
			- radio
			- submit
			- button			
			- reset
			- image：定义图像形式的提交按钮
			- hidden：定义隐藏的输入字段
		- html5新增type
			- email
			- url
			- number：min, max
			- range
			- date
			- time
			-datetime
			- month
			- week
			- search
			- tel
			- color
	- `<textarea>`
	- `<select>`
		- `<option>`



## window height

- html高度问题
    - window.innerWidth包括scrollBar
    - innerHeight是DOM视口的大小，包括内容、边框以及滚动条  
        - 会导致handsontable的滚动条显示不出来  
    - outerHeight是整个浏览器窗口的大小，包括窗口标题、工具栏、状态栏等。
    - document.documentElement.clientWidth不包括scrollBar

```
document.documentElement.clientHeight：不包括整个文档的滚动条，但包括<html>元素的边框
document.body.clientHeight：不包括整个文档的滚动条，也不包括<html>元素的边框，也不包括<body>的边框和滚动条
其中documentElement是文档根元素，就是<html>标签，body就是<body>标签了，这两种方式兼容性较好，可以一直兼容到IE6
```

- 滚动高度
    - clientHeight: 内部可视区域大小
    - offsetHeight：整个可视区域大小，包括border和scrollbar在内
    - scrollHeight：元素内容的高度，包括溢出部分
    - scrollTop：元素内容向上滚动了多少像素，如果没有滚动则为0   
    - `所有DOM元素都有上述4个属性，只需要给它固定大小并设置overflow:scroll即可表现出来`  

- dom位置
    - Event对象属性
          - clientX：相对于可视区域的x坐标。  
          - clientY：相对于可视区域的y坐标。   
          - screenX：相对于用户屏幕的x坐标。  
          - screenY：相对于用户屏幕的y坐标。  
          
    - IE特有属性
          - offsetX：鼠标相对于目标事件的父元素的内边界在x坐标的位置  
          - offsetY：鼠标相对于目标事件的父元素的内边界在y坐标的位置  
          - x：设置或获取鼠标指针位置相对于父文档的y坐标。同clientX  
          - y：设置或获取鼠标指针位置相对于父文档的y坐标。同clientY  


## dev-log

- 渐进式图片  
JPEG、GIF和PNG这三种图像格式都提供了一种功能，让图像能够更快地显示。图像可以以一种特殊方式存储，显示时先大概显示图像的草图，当文件全部下载后再填充细


