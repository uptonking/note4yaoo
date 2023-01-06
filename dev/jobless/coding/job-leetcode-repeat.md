---
title: job-leetcode-repeat
tags: [algorithms, coding, job, leetcode, repeat]
created: 2021-10-05T09:05:19.429Z
modified: 2021-10-06T14:46:25.494Z
---

# job-leetcode-repeat

# guide
- 思路
  - 先暴力求解，在解决时间、空间复杂度过高的问题
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
