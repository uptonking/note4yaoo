---
title: job-leetcode-repeat
tags: [algorithms, coding, job, leetcode, repeat]
created: '2021-10-05T09:05:19.429Z'
modified: '2021-10-06T14:46:25.494Z'
---

# job-leetcode-repeat

# guide
- to-do
# 最大子序和

```JS
/**
 * * 最大子序和(最大和的连续子数组)
 * * 思路：求和时，是正数就加上，否则重新开始
 * https://leetcode-cn.com/problems/maximum-subarray/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/94
 * - 动态规划（Dynamic Programming，DP）是一种将复杂问题分解成小问题求解的策略
 * - 分治算法要求各子问题是相互独立的，而动态规划各子问题是相互关联的。
 * - 使用动态规划求解问题时的步骤
 *  - 定义子问题
 *    - 动态规划是将整个数组归纳考虑，假设我们已经知道了以第 i-1 个数结尾的连续子数组的最大和 dp[i-1]，
 *    - 显然以第i个数结尾的连续子数组的最大和的可能取值要么为 dp[i-1]+nums[i]，要么就是 nums[i] 单独成一组，也就是 nums[i] ，在这两个数中我们取最大值
 *  - 实现需要反复执行解决的子子问题部分
 *    - dp[n] = Math.max(dp[n−1]+nums[n], nums[n])
 *  - 识别并求解出边界条件
 *    - dp[0]=nums[0]
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

# 买卖股票的最佳时机

```JS
/**
 * * 买卖股票的最佳时机。只简单买卖一次。
 * * 思路：贪心算法，取最左最小值，取最右最大值，那么得到的差值就是最大利润。
 * - 每次循环都计算最小价格和最大利润
 * https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/
 * https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/comments/1060657
 * - 给定一个数组 prices ，它的第i个元素prices[i] 表示一支给定股票第 i 天的价格。
 * - 你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。
 * - 设计一个算法来计算你所能获取的最大利润。
 * - 返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0
 */
function maxProfit(prices) {
  if (prices.length <= 1) return 0;

  let minPrice = prices[0];
  let maxProfit = 0;

  for (let i = 0; i < prices.length; i++) {
    // 今天的最大获利
    maxProfit = Math.max(maxProfit, prices[i] - minPrice);

    // 买入价格的最小值，下次使用
    minPrice = Math.min(minPrice, prices[i]);
  }

  return maxProfit;
}
```

# 最长递增子序列

```JS
/**
 * * 最长递增子序列
 * * 思路：第i个元素之前的最小上升子序列的长度无非就是max(dp[i],dp[j]+1),
 * https://leetcode-cn.com/problems/longest-increasing-subsequence/
 * - 给你一个整数数组 nums ，找到其中最长严格递增子序列的长度。
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
