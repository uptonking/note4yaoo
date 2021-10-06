---
title: job-leetcode-repeat
tags: [algorithms, coding, job, leetcode, repeat]
created: '2021-10-05T09:05:19.429Z'
modified: '2021-10-06T14:46:25.494Z'
---

# job-leetcode-repeat

# guide
- to-do
  - [买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)
# 最大子序和

```JS
/**
 * * 最大子序和(最大和的连续子数组)
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
      // 否则的话之前是负数，加正数或负数都只小，不如从新的开始
      sum = nums[i];
    }

    max = Math.max(max, sum);
  }

  return max;
}
```
