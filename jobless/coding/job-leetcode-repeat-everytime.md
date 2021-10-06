---
title: job-leetcode-repeat-everytime
tags: [algorithms, coding, job, leetcode, repeat]
created: '2021-09-21T19:40:24.161Z'
modified: '2021-10-06T14:58:39.894Z'
---

# job-leetcode-repeat-everytime

# guide

# 斐波那契数
- 该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。
  - `F(0) = 0，F(1) = 1` 前2项
  - `F(n) = F(n - 1) + F(n - 2)`，其中 n > 1

```JS
/**
 * * 斐波那契数列 fibonacci
 * https://leetcode-cn.com/problems/fibonacci-number/
 */
function fibonacci(n) {
  // 处理 0、1
  if (n < 2) return n;

  // 记录前2个数
  let n1 = 0;
  let n2 = 1;

  let curr = 0;

  for (let i = 2; i < n + 1; i++) {
    curr = n1 + n2;
    n1 = n2;
    n2 = curr;
  }

  return curr;
}

/**
 * * 2次递归带来重复计算
 * https://blog.csdn.net/weixin_40170902/article/details/80835750
 */
function fibonacciRecursive(n) {

  // 处理 0、1；也是递归终止条件
  if (n < 2) return n;

  return fibonacciRecursive(n - 1) + fibonacciRecursive(n - 2);
}

/**
 * * 使用缓存优化fibonacci
 * - 优化的递归性能仍然不如循环
 * * cache中保存的是整个数列，但却缺前2项[,,1,2,3,5...]
 * https://segmentfault.com/a/1190000022973482
 */
function fibonacciRecursive(n, cache = []) {

  // 处理 0、1；递归终止条件
  if (n < 2) return n;

  if (cache[n]) return cache[n]

  cache[n] = fibonacciRecursive(n - 1, cache) + fibonacciRecursive(n - 2, cache);

  return cache[n];
}
```
