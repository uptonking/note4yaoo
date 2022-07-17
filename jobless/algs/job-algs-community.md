---
title: job-algs-community
tags: [algorithms, community, job]
created: 2021-09-25T08:09:55.885Z
modified: 2021-09-25T08:10:17.911Z
---

# job-algs-community

# discuss

## 

## 

## 

## 

## [What are the time complexities of preorder, inorder, postorder, and level order binary tree traversals with both recursive and iterative algorithms?](https://www.quora.com/What-are-the-time-complexities-of-preorder-inorder-postorder-and-level-order-binary-tree-traversals-with-both-recursive-and-iterative-algorithms)

- For all of these traversals - whether done recursively or iteratively - you’ll have to visit every node in the binary tree. 
  - That means that you’ll get a runtime complexity of  O(n)  - where n is the number of nodes in the binary tree.

- In an average case however, if you are considering a balanced/close-to-balanced tree, the time complexity is always O(n) as you HAVE to visit each node where as space complexity changes to O(log n).
- In worst case, considering your parsed tree is a skewed tree, then, both time and space complexities whether it is implemented recursively or iteratively is O(n).

- Time complexities are exactly the same.
  - Only the order in which you visit the nodes will vary.
  - And the ordering is helpful in different applications.
  - And the ordering is helpful in different applications.

- In all cases, you are visiting every node of the tree. 
  - The only difference is the overhead spent at each node. 
  - **The order in which the nodes are visited does not affect the time complexity**. 
  - But, that overhead is a constant and so all methods are O(n) in time. 
  - If a poor algorithm or data structure is used, some traversal methods may be O(n*ln(n)). 
  - Some may also be O(ln(n)) in space, but that depends on both the algorithms and exact data structures involved.

- [二叉树四种遍历方式的速度差异](https://blog.csdn.net/na_beginning/article/details/62219224)
- 在规模小的二叉树上没有太大差异，
  - 对于大的二叉树，递归遍历都快于非递归遍历，但是每次运行的结果都有差异，一般来讲中序遍历是执行比较快的，后序遍历和层次遍历最慢

## [How to "draw" a Binary Tree to the console](https://stackoverflow.com/questions/801740)

- Look at the output of `pstree` command in Linux. It does not produce the output in the exact form that you want, but IMHO it's more readable that way.
- https://github.com/kyliau/print-binary-tree

## [Time complexity using N way Merge](https://stackoverflow.com/questions/10420397)

- Note that the base-4 log of a number is exactly half the base-2 log of a number; 
  - thus, you're only introducing a constant-factor speedup. 
  - Except you're not, because you introduce a similar constant-factor SLOWDOWN in the cost of the actual merging (2-way merge needs 1 comparison per item, 4-way may need up to 3). 
  - So while there may be fewer passes, the passes are each more costly.
  - So you've complicated the code a fair bit, and the benefits are in question.

- It sounds reasonable but is not, because in this case you have to do at least 5 comparions to sort each 4 elements. 
  - This way you have 5*N*log4(N) comparisons and this is greater than N*log2(N) by factor 5*log(2)/log(4)

## [What is `Array.prototype.sort()` time complexity?](https://stackoverflow.com/questions/57763205)

- Since V8 v7.0 and Chrome 70 Timsort algorithm is used.
  - Which, for smaller arrays, has a time complexity of O(n) and space complexity of 0(1). 
  - And for larger arrays, it has a time complexity of O(nlog(n)) and space complexity of O(n).
- The older version of V8 uses Quick Sort, and it has a check for small arrays (up to 10 elements). 
  - So for smaller arrays, the time complexity is O(n^2), and space complexity is O(1).
  - For larger arrays, time complexity is O(nlog(n)) (average case), and space complexity is O(log(n))

- Chrome, as of version 70, uses a hybrid of merge sort and insertion sort called Timsort.
- Firefox uses merge sort.

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
