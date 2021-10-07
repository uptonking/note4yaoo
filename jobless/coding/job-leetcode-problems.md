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

# 下一个排列

```JS
/**
 * * 下一个排列
 * * 思路：从后向前找到nums[i]大于nums[i-1]的时候，重排nums[i-1]之后的所有数字；找不到则从小到大重新排序。
 * https://leetcode-cn.com/problems/next-permutation/
 * https://leetcode-cn.com/problems/next-permutation/solution/javascript-mo-ni-by-leoren/
 * - 实现获取 下一个排列 的函数，算法需要将给定数字序列重新排，组合出下一个更大的整数。
 * - 如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）
 */
function nextPermutation(nums) {
  let flag = 0;

  for (let i = nums.length - 1; i >= 0; i--) {
    // 如果当前值i大于前一个值i-1，则进行操作
    if (nums[i] > nums[i - 1]) {
      // 选取i及其后面最小的一个值，和前一个值i-1进行交换
      let tmp = nums[i - 1];
      let min = i;
      for (let j = i + 1; j < nums.length; j++) {
        if (nums[j] > tmp && nums[min] > nums[j]) min = j;
      }
      nums[i - 1] = nums[min];
      nums[min] = tmp;

      // 将i及其后面的值进行排序
      for (let j = i; j < nums.length; j++) {
        min = j;
        for (let k = j + 1; k < nums.length; k++) {
          min = nums[min] < nums[k] ? min : k;
        }
        tmp = nums[j];
        nums[j] = nums[min];
        nums[min] = tmp;
      }
      flag = 1;
      break;
    }
  }

  // 如果所有值逆序排，则从小到大排列
  if (!flag) {
    for (let i = 0; i < (nums.length + 1) >> 1; i++) {
      const tmp = nums[i];
      nums[i] = nums[nums.length - 1 - i];
      nums[nums.length - 1 - i] = tmp;
    }
  }
  return nums;
}
```

# 全排列问题

```JS
/**
 * * 全排列问题
 * 给定一个 没有重复 数字的序列，返回其所有可能的全排列。
 * https://leetcode-cn.com/problems/permutations/
 * https://leetcode-cn.com/problems/permutations/
 * 全排列，首先将每个元素排到第一位。剩余元素再重复第一步操作，依次处理各个元素。
 * 对于移动的元素，在递归操作之前，和之后该如何操作。
 */

// swap
const permute = function(nums) {
  const len = nums.length;
  if (len === 0) return [
    []
  ];
  const res = [];
  const perm = function(arr, p, q, res) {
    if (p === q) {
      res.push([...arr]);
    }
    for (let i = p; i < q; i++) {
      swap(arr, i, p);
      perm(arr, p + 1, q, res);
      swap(arr, i, p);
    }
  };
  const swap = function(arr, left, right) {
    const temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;
  };
  perm(nums, 0, len, res);
  return res;
};
```

# 计算平方根 sqrt

```JS
/**
 * * 给你一个非负整数 x ，计算并返回 x 的 算术平方根 。
 * https://leetcode-cn.com/problems/sqrtx/
 */
function mySqrt(x) {
  if (x === 1) return 1;
  let min = 0;
  let max = x;

  while (max - min > 1) {
    let m = Math.floor((max + min) / 2);

    x / m < m ? (max = m) : (min = m);
  }

  return min;
}
```
