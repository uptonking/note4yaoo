---
title: job-fe-css-layout
tags: [css, job, layout]
created: 2021-09-23T15:46:13.688Z
modified: 2021-10-10T09:17:17.328Z
---

# job-fe-css-layout

# guide

# 多栏布局

## 2栏：左侧定宽，右侧自适应

- 💡️ 方法1: 左列设置 float，右列使用 overflow:hidden/display:flex 创建 BFC
- 原理：利用 BFC 不会与 float box 重叠
- 虽然 BFC 不会与 float box 重叠，但实测这句话对于绝对定位元素并不成立
- 设置 display:inline-block/table-cell 时需要显式声明 width，不能算自适应

```HTML
<style>
  .container {
    height: 400px;
  }

  .left {
    float: left;
    width: 200px;
    height: 100%;
    border: orange 2px solid;
  }

  .right {
    overflow: hidden;
    height: 100%;
    border: tomato 2px solid;
  }
</style>

<body>
  <div class="container">
    <div class="left"></div>
    <div class="right"></div>
  </div>
</body>
```

- 💡️ 方法2: 左列 float/positon:absolute，右列保持块级元素，使用 margin-left 向右偏移
- 原理：利用块级元素会自动填充行内可用空间

```HTML
<style>
  .container {
    /* position: relative; */
    height: 400px;
  }

  .left {
    /* position: absolute; */
    float: left;
    width: 200px;
    height: 100%;
    border: orange 2px solid;
  }

  .right {
    margin-left: 200px;
    height: 100%;
    border: tomato 2px solid;
  }
</style>
```

- 💡️ 方法3：flex 布局，左列 flex：0 0 width，右列 flex：1 (= 1 1 0%)

```HTML
<style>
  .container {
    display: flex;
    height: 400px;
  }

  .left {
    flex: 0 0 200px;
    height: 100%;
    border: orange 2px solid;
  }

  .right {
    flex: 1;
    height: 100%;
    border: tomato 2px solid;
  }
</style>
```

- 💡️ 方法4: 左右列同时 float，右列以 calc(100%-xxx) 作为宽度

```HTML
<style>
  .container {
    height: 400px;
  }

  .left {
    float: left;
    width: 200px;
    height: 100%;
    border: orange 2px solid;
  }

  .right {
    float: left;
    width: calc(100% - 208px);
    height: 100%;
    border: tomato 2px solid;
  }
</style>
```

## 2栏：左侧适应内容，右侧自适应

- 💡️ 方法1: 左侧 float，右侧 overflow:hidden/display:flex 
- 原理：适应内容依赖于 float box 的包裹性，右侧创建 BFC

```CSS
.container {
  height: 400px;
}

.left {
  float: left;
  height: 100%;
  border: orange 2px solid;
}

.right {
  overflow: hidden;
  height: 100%;
  border: tomato 2px solid;
```

- 💡️ 方法2: flex布局：左侧可以不设置（默认值 flex: 0 1 auto），右侧设置 flex:1 (1 1 0%)

```CSS
.container {
  display: flex;
  height: 400px;
}

.left {
  height: 100%;
  border: orange 2px solid;
}

.right {
  flex: 1;
  height: 100%;
  border: tomato 2px solid;
```

- 💡️方法3: grid布局：左侧设置 auto，右侧 1fr

```CSS
.container {
  display: grid;
  grid-template-columns: auto 1fr;
  grid-template-rows: 400px;
  width: 100%;
}

.left {
  border: orange 2px solid;
}

.right {
  border: tomato 2px solid;
}
```

## 3栏：左右定宽，中间自适应

### 圣杯布局

- 圣杯布局指一种经典的布局(整体上中下，中又分为左中右)，三栏布局出现在它的中间段
- 圣杯布局缺陷
  - 留给center部分的最小宽度不能小于left部分的宽度，否则左右列会掉到下一行
  - 任意一列内容高度拉长时，其他两列的背景并不会自动填充

```HTML
<div class="header"></div>
<div class="container">
  <div class="center"></div>
  <div class="left"></div>
  <div class="right"></div>
</div>
<div class="footer"></div>
```

```CSS
.header {
  height: 20px;
  background-color: rgb(102, 113, 195);
}

.footer {
  height: 20px;
  background-color: rgb(176, 101, 194);
}

.container {
  overflow: hidden;
  padding: 0 100px 0 200px;
}

.container .center {
  float: left;
  width: 100%;
  height: 200px;
  background-color: rgb(223, 143, 143);
}

.container .left {
  float: left;
  width: 200px;
  margin-left: -100%;
  position: relative;
  left: -200px;
  height: 200px;
  background-color: rgb(102, 195, 177);
}

.container .right {
  float: left;
  width: 100px;
  margin-left: -100px;
  position: relative;
  right: -100px;
  height: 200px;
  background-color: rgb(146, 195, 102);
```

### 双飞翼布局

- 在圣杯布局基础上进一步优化，解决了圣杯布局错乱问题，实现了内容与布局的分离；任何一栏都可以是最高栏，不会出问题，header 与 footer 不变

```HTML
<div class="container">
  <div class="center">
    <div class="inner"></div>
  </div>
  <div class="left"></div>
  <div class="right"></div>
</div>
```

```CSS
.container {
  overflow: hidden;
  /* 可以设置2*左列宽度+右列宽度为容器最小宽度保证显示效果 */
  min-width: 500px;
}

.container .center {
  float: left;
  width: 100%;
  height: 200px;
  background-color: yellowgreen;
}

.container .center .inner {
  margin: 0 100px 0 200px;
}

.container .left {
  float: left;
  width: 200px;
  margin-left: -100%;
  height: 200px;
  background-color: orange;
}

.container .right {
  float: left;
  width: 100px;
  margin-left: -100px;
  height: 200px;
  background-color: royalblue;
```

### 绝对定位布局

- 左右列使用绝对定位，左列设置 left top，右列设置 right top（不设置 top:0 时，绝对定位元素不能与其他元素 margin 重叠，无法形成一行），中间列不设置 width，只设置 margin-left 和 margin-right

```CSS
.container {
  position: relative;
}

.container .center {
  margin-right: 200px;
  margin-left: 100px;
  height: 200px;
  background-color: rgb(223, 143, 143);
}

.container .left {
  position: absolute;
  width: 100px;
  height: 200px;
  left: 0;
  top: 0;
  background-color: rgb(102, 195, 177);
}

.container .right {
  position: absolute;
  width: 200px;
  height: 200px;
  right: 0;
  top: 0;
  background-color: rgb(146, 195, 102);
}
```

### 💡️ flex

- 目前三栏布局最常见的一种实现方式：
  - 左右列的 flex-shrink 需要设置为 0 才能保证左右列不被中间列压缩；
  - 如果要构建圣杯布局时，center 也无需使用 overflow
- center: flex:1; order:2; 
- left: flex: 0 0 200px; order:1; 
- right: flex:0 0 100px; order:3; 

```CSS
.container {
  display: flex;
  min-width: 500px;
}

.container .center {
  flex: 1;
  order: 2;
  height: 200px;
  background-color: yellowgreen;
}

.container .left {
  flex: 0 0 200px;
  order: 1;
  height: 200px;
  background-color: orange;
}

.container .right {
  flex: 0 0 100px;
  order: 3;
  height: 200px;
  background-color: royalblue;
```

### grid

- 最简单的实现方式，
  - 通过 grid-template-columns:200px 1fr 100px; 
  - 自动分配中间列，通过 grid-template-rows: 200px; 
  - 统一设定高度，但此时的 center div 需要放在中间

```CSS
.container {
  display: grid;
  grid-template-columns: 200px 1fr 100px;
  grid-template-rows: 200px;
  min-width: 500px;
}

.container .center {
  background-color: yellowgreen;
}

.container .left {
  background-color: orange;
}

.container .right {
  background-color: royalblue;
}
```

## 3栏：左侧定宽，中右均分

- flex 实现：左列 flex: 0 0 width 中右列 flex: 1
- grid 实现：grid-template-columns: width 1fr 1fr
- 三列 float：中右列使用 calc 计算宽度，但实际使用中宽度计算不准确很可能导致元素溢出到下一行

```CSS
.container div {
  height: 200px;
}

.left {
  float: left;
  width: 200px;
  background-color: orange;
}

.center {
  float: left;
  width: calc(0.5 * (100% - 200px));
  background-color: gray;
}

.right {
  float: left;
  width: calc(0.5 * (100% - 200px));
  background-color: tomato;
}
```
