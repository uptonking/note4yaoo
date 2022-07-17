---
title: job-leetcode-dp
tags: [job, leetcode, 动态规划]
created: 2021-10-08T18:41:09.962Z
modified: 2021-10-08T18:41:34.540Z
---

# job-leetcode-dp

# guide

- 要点
  - 子序列不一定是连续的，子串才必须是连续的。

- 动态规划（Dynamic Programming，DP）是一种将复杂问题分解成小问题求解的策略
  - 分治算法要求各子问题是相互独立的，而动态规划各子问题是相互关联的。
- 使用动态规划求解问题时的步骤
  - 定义子问题，划分阶段
  - 选择状态
  - 确定决策并写出状态转移方程，实现需要反复执行解决的子子问题部分
  - 写出规划方程（包括边界条件）
# 最大子序和

```JS
/**
 * * 最大子序和，找到一个具有最大和的连续子数组，返回最大和
 * * 思路：求和时，是正数就加上，否则重新开始
 * https://leetcode-cn.com/problems/maximum-subarray/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/94

 */
function maxSubArray(nums) {
  let sum = nums[0];
  let max = nums[0];

  for (let i = 1; i < nums.length; i++) {
    if (sum > 0) {
      // 如果之前的的和大于0，那么可以继续累加
      sum += nums[i];
    } else {
      // 若是sum为负，则加正数或负数都只是小，不如重新的开始
      sum = nums[i];
    }

    max = Math.max(max, sum);
  }

  return max;
}
```

# 最长递增子序列

```JS
/**
 * * 最长递增子序列 / 最长上升子序列
 * * 思路：贪心 + 二分查找，类似 扑克排序法
 * https://leetcode-cn.com/problems/longest-increasing-subsequence/
 * https://blog.csdn.net/weixin_37780776/article/details/119898537
 * https://leetcode-cn.com/problems/longest-increasing-subsequence/solution/ti-jie-zui-chang-di-zeng-zi-xu-lie-dong-flpfr/
 * - 给你一个整数数组 nums ，找到其中最长严格递增子序列的长度。
 */

function lengthOfLIS(nums) {
  const size = nums.length;
  if (size <= 1) return size;

  // 存放递增序列的辅助数组，因为递增有序，所以可以二分查找
  const sub = [nums[0]];

  for (let i = 1; i < size; i++) {
    if (nums[i] > sub[sub.length - 1]) {
      // 若当前元素大于辅助数组末尾元素，那就是满足条件的递增序列，可直接加进去
      sub.push(nums[i]);
    } else {

      // 如果当前值已存在于辅助数组，没必要搜索了；加了判断反而降低了性能，不如让二分搜索能替换相等的值
      // if (!sub.includes(nums[i])) {

      // 若当前元素比辅助数组末尾元素小
      // 那就在sub辅助数组中找到大于或等于num[i]的第一个元素的的位置，用nums[i]覆盖这个位置
      const firstGTEIndex = getFirstGTE(sub, 0, sub.length - 1, nums[i]);

      // 因为nums[i] <= sub原位置值，所以赋值以后仍然是递增的
      sub[firstGTEIndex] = nums[i];
      // }
    }
  }

  return sub.length;
}

/**
 * 👀️ 这里不能完全照抄二分查找，因为不是找准确值，而是找第一个大于或等于target的元素
 * 标准二分模版在查找结束时，low或high有1个是不准确的
 */
/** 在arr数组的索引范围low-high内，找到大于或等于target的第一个元素的位置 */
function getFirstGTE(arr, low, high, target) {
  let mid;
  while (low <= high) {
    mid = Math.floor((low + high) / 2);

    if (target === arr[mid]) return mid;

    if (target < arr[mid]) {
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  if (arr[mid] >= target) return mid;

  // ？ if arr[mid+1] < target
  return mid + 1;
}
```

```JS
/**
 * * 典型的动态规划
 * * 思路：第i个元素之前的最小上升子序列的长度无非就是max(dp[i],dp[j]+1)
 */
function lengthOfLIS(nums) {
  const dp = new Array(nums.length).fill(1);

  for (let i = 1; i < nums.length; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[i] > nums[j]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
  }

  return Math.max(...dp);
}
```

# 最长连续递增序列

```JS
/**
 * * 最长连续递增序列
 * * 思路：贪心算法，若 nums[i] < nums[i+1]，那就+1，否则重新计数1
 * https://leetcode-cn.com/problems/longest-continuous-increasing-subsequence/
 * - 给定一个未经排序的整数数组，找到最长且连续递增的子序列，并返回该序列的长度。
 * 时间复杂度：O(n),空间复杂度：O(1)
 */
function findLengthOfLCIS(nums) {
  const len = nums.length;
  if (len <= 1) return len;

  // 连续子序列最小也是1
  let ret = 1;
  let count = 1;

  for (let i = 0; i < len - 1; i++) {
    if (nums[i] < nums[i + 1]) {
      // 如果下个元素是递增的，+1
      count++;
    } else {
      // 如果非递增，重新计数 1
      count = 1;
    }

    // 检查更新连续子序列的最大长度
    if (count > ret) ret = count;
  }

  return ret;
}
```

- ref
  - [674. 最长连续递增序列 题解cpp](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0674.%E6%9C%80%E9%95%BF%E8%BF%9E%E7%BB%AD%E9%80%92%E5%A2%9E%E5%BA%8F%E5%88%97.md)
# 最长公共子序列

```JS
/**
 * * 最长公共子序列
 * https://leetcode-cn.com/problems/longest-common-subsequence/
 * - 给定两个字符串 text1 和 text2，返回这两个字符串的最长 公共子序列 的长度
 * - 一个字符串的 子序列 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。
 *
 */
function longestCommonSubsequence(text1, text2) {
  // base case 一个字符串和自身没有子序列 dp[0][j] = dp[i][0] = 0
  const dp = Array.from(Array(text1.length + 1), () =>
    Array(text2.length + 1).fill(0),
  );

  for (let i = 1; i <= text1.length; i++) {
    for (let j = 1; j <= text2.length; j++) {
      if (text1[i - 1] === text2[j - 1]) {

        dp[i][j] = dp[i - 1][j - 1] + 1;
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }

  return dp[text1.length][text2.length];
}
```

# 最长重复子数组

```JS
/**
 * * 最长重复子数组
 * - 返回两个数组中公共的、长度最长的子数组的长度。
 * https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/
 * https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/solution/718-zui-chang-zhong-fu-zi-shu-zu-jsdong-tai-gui-hu/
 * - 子序列默认不连续，子数组默认连续
 */

function findLength(nums1, nums2) {
  const [m, n] = [nums1.length, nums2.length];

  // dp数组初始化，都初始化为0
  const dp = new Array(m + 1).fill(0).map((x) => new Array(n + 1).fill(0));

  // 初始化最大长度为0
  let ret = 0;
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      // 遇到A[i - 1] === B[j - 1]，则更新dp数组
      if (nums1[i - 1] === nums2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + 1;
      }
      // 更新res
      ret = dp[i][j] > ret ? dp[i][j] : ret;
    }
  }

  // 遍历完成，返回res
  return ret;
}
```

```js
/**
 * * 基于循环比较实现，优点是内存消耗非常少
 * https://juejin.cn/post/6845166890822680583
 */
function findLength(nums1, nums2) {
  let result = 0;
  let lastResult = 0;
  let lastIndexI = 0;
  let lastIndexJ = 0;

  // 以其中一个数组的遍历作为主循环
  for (let i = 0, j = 0; i < nums1.length;) {
    // 开始逐段比较，如果相同就继续
    if (nums1[i] === nums2[j]) {
      result++;
      i++;
      j++;
      if (lastResult < result) {
        lastResult = result;
      }
    } else {
      // 如果失败，重置内循环的计数器j到lastIndexJ
      i = lastIndexI;
      lastIndexJ++;
      j = lastIndexJ;
      result = 0;
    }

    if (j >= nums2.length || nums2.length - lastIndexJ <= lastResult) {
      // 如果内循环的计数器j到头了，那么就记录结果，重置主循环的计数器i到lastIndexI

      lastIndexI++;
      i = lastIndexI;

      if (nums1.length - i <= lastResult) {
        // 优化思路时，当发现已有当长度少于之前的结果，就停止或开始下一段的比较
        break;
      }
      j = 0;
      lastIndexJ = 0;
      result = 0;
    }
  }

  return lastResult;
}
```
