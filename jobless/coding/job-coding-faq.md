---
title: job-coding-faq
tags: [coding, engineering, job, 手撕代码]
created: '2021-09-21T19:50:09.680Z'
modified: '2021-10-10T08:52:32.419Z'
---

# job-coding-faq

# guide

- 手撕代码的问题处理
  - 分析、抽象目标
  - 设计 api、测试用例 和 workflow
  - 设计各个api的input-args, output-return
# to-do
- 判断DOM标签的合法性
  - 判断标签的闭合可以使用栈，跟判断有效的括号思路类似。
# 实现算术运算的加法
- 按位与 & 同1才1
- 按位或 | 有1则1
- 按位异或 ^ 不同则1 

- 简单实现
  - 按位异或 是不进位的加法
  - a + b = (a ^ b) + ((a & b) << 1
  - 通过迭代的方式模拟加法

```JS
function sum(a, b) {
  if (a == 0) return b;
  if (b == 0) return a;

  let newA = a ^ b;
  let newB = (a & b) << 1;

  return sum(newA, newB);
}
```

# 替换日期格式 yyyy-MM-dd > MM-dd-yy

```JS
var reg = /(\d{2})\.(\d{2})\/(\d{4})/
var data = '10.24/2017'
data = data.replace(reg, '$3-$1-$2')
console.log(data) //2017-10-24
```

# 统计HTML标签中出现次数最多的标签
- elements = element.getElementsByTagName(tagName)
  - returns a live HTMLCollection of elements with the given tag name.

```JS
const tags = document.getElementsByTagName('*');
let map = new Map();
let maxStr = '';
let max = 0;
// 只是使用下标来获取，没有使用数组的方法，所以不需要将类数组转为数组
for (let i = 0; i < tags.length; i++) {
  let value = map.get(tags[i].tagName);

  if (value) {
    map.set(tags[i].tagName, ++value);
  } else {
    map.set(tags[i].tagName, 1);
  }

  if (value > max) {
    maxStr = tags[i].tagName;
    max = value;
  }
}
```

# 统计HTML标签中以b开头的标签数量

```JS
// 获取当前文档中的所有标签。
const tags = document.getElementsByTagName('*');
// 注意要先将类数组转换成数组
const value = [...tags].filter((item) => item.tagName.startsWith('B'));

// ------ 递归实现 -----

const $prefixBElements = [];

function dfs($el) {
  if ($el.tagName.startsWith('B')) {
    $prefixBElements.push($el);
  }
  for (const $child of $el.children) {
    dfs($child);
  }
}
dfs(document.documentElement);

console.log($prefixBElements);
```
