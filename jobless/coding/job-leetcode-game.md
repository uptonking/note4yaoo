---
title: job-leetcode-game
tags: [game, job, leetcode]
created: 2021-10-08T10:50:06.814Z
modified: 2021-10-08T10:50:26.290Z
---

# job-leetcode-game

# guide

# 爬楼梯

```JS
/**
 * * 爬楼梯
 * * 规律：第 n 层的走法数量是第 n-1 层和第 n-2 层走法数量之和。
 * * 与Fibonacci不同的是，fib是0、1、1、2，这里是1，2，3
 * 每次你可以爬1或2个台阶。你有多少种不同的方法可以爬到n个台阶的楼顶呢？
 * https://leetcode-cn.com/problems/climbing-stairs/
 * https://segmentfault.com/a/1190000040464134
 * https://www.cnblogs.com/echolun/p/14707269.html
 * https://blog.csdn.net/qq_30216191/article/details/81712018
 */

/**
 * * 解法1: 循环累加
 */
function climbStairs(n) {
  if (n <= 2) return n;

  // 第n级台阶的爬法
  let ret = 0;
  // n1 表示前 2 项，n2 表示前 1 项
  let n1 = 1;
  let n2 = 2;

  for (let i = 3; i < n + 1; i++) {
    // 前两项值固定，因此从第 3 项开始循环
    ret = n1 + n2;
    n1 = n2;
    n2 = ret;
  }

  return ret;
}
/**
 * * 解法2: 递归
 * 就是斐波那契函数的形式，oj会提示超出时间限制
 */
function climbStairs(n) {
  if (n <= 2) return n;

  return climbStairs(n - 1) + climbStairs(n - 2);
}

/***
 * * 扩展：每次可以走 1 步、2 步、3 步
 */
function climbStairs(n) {
  if (n <= 2) return n;
  if (n === 3) return 4;

  return climbStairs(n - 1) + climbStairs(n - 2) + climbStairs(n - 3);
}
```

# 岛屿数量

```JS
/**
 * * 岛屿数量
 * * 思路：深度优先，标0法
 * * 若元素等于1，岛屿数量 count++，与其同时用 dfs 算法访问周围的其他点，进行同样的操作；
 * * 且将访问过且等于 1 的点标记为零。
 * https://leetcode-cn.com/problems/number-of-islands/
 * 给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。
 */
function numIslands(grid) {
  // 存放岛屿数量
  let count = 0;
  if (grid.length === 0) return count;
  for (let i = 0; i < grid.length; i++) {
    for (let j = 0; j < grid[0].length; j++) {
      if (grid[i][j] === '1') {
        dfsSearch(grid, i, j);
        count++;
      }
    }
  }
  return count;
}

function dfsSearch(grid, i, j) {
  if (i < 0 || j < 0 || i >= grid.length || j >= grid[0].length) return;

  if (grid[i][j] === '1') {
    grid[i][j] = '0';
    dfsSearch(grid, i + 1, j); // 搜索右边
    dfsSearch(grid, i - 1, j); // 搜索左边
    dfsSearch(grid, i, j + 1); // 搜索下边
    dfsSearch(grid, i, j - 1); // 搜索上边
  }
}
```

# 接雨水

```JS
/**
 * * 接雨水
 * * 思路1：暴力法，找出下雨后水能达到的最高位置
 * * 思路2：左右双指针向中间直到相遇，
 * 在某个位置i处,它能存的水，取决于它左右两边的最大值中较小的一个
 * 当遍历到 left，只要 right 对应柱子高度大于 left 左边所有柱子高度，则其收集雨水量一定是由 leftMax 决定。
 * https://leetcode-cn.com/problems/trapping-rain-water/
 * https://leetcode-cn.com/problems/trapping-rain-water/solution/javascriptjie-fa-tong-su-yi-dong-42jie-y-pjc5/
 * https://leetcode-cn.com/problems/trapping-rain-water/solution/yu-shui-shou-ji-javascript-by-jtangming/
 * 给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。
 */
function trap(height) {
  let ret = 0;

  let left = 0;
  let right = height.length - 1;
  let leftMax = 0;
  let rightMax = 0;
  while (left < right) {
    if (height[left] < height[right]) {
      // 若左边比右边矮，则左边能存多少水由左边决定

      leftMax = Math.max(height[left], leftMax);
      ret += leftMax - height[left];
      left++;
    } else {
      // 若左边比右边高，则右边能存多少水由右边决定
      rightMax = Math.max(height[right], rightMax);
      ret += rightMax - height[right];
      right--;
    }
  }
  return ret;
}

// 暴力法，超出时间限制
function trap(height) {
  let ret = 0;

  for (let i = 0; i < height.length; i++) {
    let maxLeft = 0;
    let maxRight = 0;
    // 以当前curr 这个位置为基准，找出左边的边界的最大值
    for (let j = i; j >= 0; j--) {
      maxLeft = Math.max(maxLeft, height[j]);
    }

    // 找出右边边界的最大值
    for (let j = i; j < height.length; j++) {
      maxRight = Math.max(maxRight, height[j]);
    }

    ret += Math.min(maxLeft, maxRight) - height[i];
  }

  return ret;
}
```
