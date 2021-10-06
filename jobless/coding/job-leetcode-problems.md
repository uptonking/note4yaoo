---
title: job-leetcode-problems
tags: [algorithms, coding, job, leetcode]
created: '2021-10-06T19:59:34.467Z'
modified: '2021-10-06T19:59:58.846Z'
---

# job-leetcode-problems

# guide

# 两个有序数组的中位数

```JS
/***
 * * 找出这两个有序数组的中位数
 * * 思路：先排序，再求中间位置的值
 * * 扩展：合并2个有序数组，可利用优化的归并排序
 * https://leetcode-cn.com/problems/median-of-two-sorted-arrays/
 * 
 */
function findMedianSortedArrays(nums1, nums2) {

  const nums = nums1.concat(nums2);

  nums.sort((a, b) => a - b);

  const len = nums.length;

  return len % 2 === 0 ? (nums[len / 2 - 1] + nums[len / 2]) / 2 : nums[(len - 1) / 2];

}
```

# 多数元素 / 众数
- 找出其中所有出现超过 ⌊ n/3; n/2 ⌋ 次的元素
- 试设计时间复杂度为 O(n)、空间复杂度为 O(1)的算法

- 摩尔投票算法
  - 每次从序列中选择两个不同的数字抵消掉，最后剩下的一个数字或几个相同的数字，就是出现次数大于总数一半的那个
  - 摩尔投票法，该算法用于1/2情况
  - 出现次数大于n/2的最多只有1个元素
- 改进投票算法
  - 出现次数大于该数组长度1/3的值最多只有2个

```JS
/**
 * * 找出其中所有出现超过 ⌊ n/2 ⌋ 次的元素
 * 假设数组是非空的，并且给定的数组总是存在多数元素，如aabbaa
 * * 投票法：从第一个数开始count=1，遇到相同的就加1，遇到不同的就减1，减到0就重新换个数开始计数，总能找到最多的那个
 */

function majorityElement(nums) {
  let count = 0;

  let candidate;

  for (let i = 0; i < nums.length; i++) {
    if (count === 0) candidate = nums[i];

    candidate === nums[i] ? count++ : count--;
  }

  return candidate;
}

// 排序后多数元素一定会覆盖 n/2 位置。因此排序后直接返回该位置元素即可。
var majorityElement = function(nums) {
  nums.sort((a, b) => a - b);

  return nums[Math.floor(nums.length / 2)];
};
```

```JS
/**
 * * 找出其中所有出现超过 ⌊ n/3⌋ 次的元素
 * * 投票法：出现次数大于该数组长度1/3的值最多只有2个
 * https://leetcode-cn.com/problems/majority-element-ii/solution/qiu-zhong-shu-javascript-by-bruceyuj/
 * https://leetcode-cn.com/problems/majority-element-ii/comments/591551
 */
function majorityElement3(nums) {
  const len = nums.length;
  const ret = [];

  let n1 = null;
  let n2 = null;
  let cnt1 = 0;
  let cnt2 = 0;

  for (let i = 0; i < len; i++) {
    if (n1 === nums[i]) {
      cnt1++;
    } else if (n2 === nums[i]) {
      cnt2++;
    } else if (cnt1 === 0) {
      n1 = nums[i];
      cnt1++;
    } else if (cnt2 === 0) {
      n2 = nums[i];
      cnt2++;
    } else {
      cnt1--;
      cnt2--;
    }
  }

  cnt1 = 0;
  cnt2 = 0;

  for (let i = 0; i < len; i++) {
    if (n1 === nums[i]) {
      cnt1++;
    } else if (n2 === nums[i]) {
      cnt2++;
    }
  }

  if (cnt1 > (len / 3) >>> 0) {
    ret.push(n1);
  }
  if (cnt2 > (len / 3) >>> 0) {
    ret.push(n2);
  }

  return ret;
}
```
