---
title: job-algs-community
tags: [algorithms, community, job]
created: '2021-09-25T08:09:55.885Z'
modified: '2021-09-25T08:10:17.911Z'
---

# job-algs-community

# discuss

## 

## 

## 

## 

## [Javascript swap array elements](https://stackoverflow.com/questions/872310)

- 使用临时变量，思路简单清晰，语言无关

```JS
// You only need one temporary variable. 
var b = list[y];
list[y] = list[x];
list[x] = b;

// a = [b, b = a][0]; // 先创建数组字面量
```

- 解构赋值

```JS
// destructuring assignment

[arr[0], arr[1]] = [arr[1], arr[0]];
```

- `splice(start, deleteCount, item1, item2, itemN)` 从索引为start的位置开始，删除deleteCount个元素，再插入剩余参数中itemN个元素
  - 会直接修改原数组
  - returns an array containing the deleted elements or empty array

```JS
var A = [1, 2, 3, 4, 5, 6, 7, 8, 9],
  x = 0,
  y = 1;
A[x] = A.splice(y, 1, A[x])[0];
alert(A); // alerts "2,1,3,4,5,6,7,8,9"
```

- `slice(start, end)` 截取连续元素
  - 不会修改原数组
  - returns a new array containing the extracted elements.

```JS
// slice交换的思路是 提取拼接多段元素 i1, i2
arr.slice(0, i1).concat(arr[i2], arr.slice(i1 + 1, i2), arr[i1], arr.slice(i2 + 1))

// 交换第一个和最后一个
[a.pop(), ...a.slice(1), a.shift()]
```
