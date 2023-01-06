---
title: job-leetcode-number-math
tags: [job, leetcode, math, numeric]
created: 2021-10-08T18:03:56.082Z
modified: 2021-10-08T18:04:24.850Z
---

# job-leetcode-number-math

# guide

# 用 Rand7() 实现 Rand10()

```JS
/**
 * * 用 Rand7() 实现 Rand10()： k进制诸位生成 + 拒绝采样
 * * 思路是先构造一个randN，这个N必须是10的整数倍，然后randN % 10就可以得到了rand10.
 * * 思路：rand7 -> rand49 -> rand40 -> rand10
 * 已有方法rand7()可生成1到7范围内的均匀随机整数，试写一个方法 rand10 生成 1 到 10 范围内的均匀随机整数。
 * https://leetcode-cn.com/problems/implement-rand10-using-rand7/
 * https://juejin.cn/post/6844904055022583822
 * https://blog.csdn.net/fuxuemingzhu/article/details/81809478
 * https://leetcode-cn.com/problems/implement-rand10-using-rand7/comments/85710
 * rand7() 等概率地产生 1,2,3,4,5,6,7.
 * rand7() - 1 等概率地产生 [0,6].
 * (rand7() - 1) *7 等概率地产生0, 7, 14, 21, 28, 35, 42
 * (rand7() - 1) * 7 + (rand7() - 1) 等概率地产生 [0, 48] 这 49 个数字
 * 如果步骤 4 的结果大于等于 40，那么就重复步骤 4，直到产生的数小于 40
 * 把步骤 5 的结果 mod 10 再加 1， 就会等概率的随机生成 [1, 10]
 */
function rand10() {
  while (true) {
    // 把等概率产生数的空间扩大，使得该空间大于要产生新的数的范围。
    // 找到最接近这个空间的一个值k，使得k%新数==0，k是这个要新生成数的倍数。
    // 对于本例子来讲，就是把等概率产生数的空间扩大至0-48
    const num = (rand7() - 1) * 7 + rand7() - 1;

    // 为什么不直接num = (rand7()-1)*8;
    // 那么得到的随机数只能是[0,8,16,24,32,40,48]

    // 然后取最接近48且为10的倍数的一个值k，这个值是40
    // 每次产生一个新值，若该值小于40，那么对该值mod10
    // 也就是说新空间中的0，10，20，30代表10；1，11，21，31代表1；2，12，22，32代表2；以此类推。
    if (num < 40) {
      return (num % 10) + 1;
    }
  }
}

function rand7() {}
```

# 两个有序数组的中位数

```JS
/***
 * * 找出这两个有序数组的中位数
 * * 思路：先排序，再求中间位置的值
 *
 * https://leetcode-cn.com/problems/median-of-two-sorted-arrays/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/162
 * https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/4-xun-zhao-liang-ge-zheng-xu-shu-zu-de-zhong-we-40/
 */
function findMedianSortedArrays(nums1, nums2) {
  if (!nums1.length && !nums2.length)
    return null;

  // 如果数组1为空
  if (!nums1.length) {
    // 若此时数组2仅一个值，那么该值为中位数
    if (nums2.length === 1) return nums2[0];

    /**
     * 否则比较数组2，取中位数
     * 比较单个数组采用二分法
     */
    const half = Math.floor(nums2.length / 2);
    return findMedianSortedArrays(nums2.slice(0, half), nums2.slice(half));
  }

  // 如果数组2为空，同理
  if (!nums2.length) {
    if (nums1.length === 1) nums1[0];

    const half = Math.floor(nums1.length / 2);
    return findMedianSortedArrays(nums1.slice(0, half), nums1.slice(half));
  }

  // 如果两个数组都只剩1个数，取两者中间值
  if (nums1.length === 1 && nums2.length === 1) {
    return nums1[0] === nums2[0] ? nums1[0] : (nums1[0] + nums2[0]) / 2;
  }

  // 比较两个数组的最小值，丢弃最小值
  nums1[0] < nums2[0] ? nums1.shift() : nums2.shift();

  // 这里注意边界值，丢弃最小值后有的数组可能为空
  if (!nums1.length) {
    // 强制丢掉最大值
    nums2.pop();
    return findMedianSortedArrays(nums1, nums2);
  }
  if (!nums2.length) {
    nums1.pop();
    return findMedianSortedArrays(nums1, nums2);
  }

  // 比较两个数组的最大值，丢弃最大值
  nums1[nums1.length - 1] > nums2[nums2.length - 1] ? nums1.pop() : nums2.pop();

  // 重复该操作
  return findMedianSortedArrays(nums1, nums2);
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
 * * 投票法：从第一个数开始count=1，遇到相同的就加1，遇到不同的就减1，减到0就重新换个数开始计数，总能找到最多的那个
 * 假设数组是非空的，并且给定的数组总是存在多数元素，如aabbaa
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

# 整数数组所有可能的子集

```JS
/**
 * * 整数数组所有可能的子集
 * * 思路：dfs，遇到这三种类型（子集，排列，组合） 立马想到使用回溯
 * * 回溯模板
 * - 在外面定义一个结果集 ret
 * - 在外面在定义一个结果集的下一层结果集route
 * - 回溯（这里呢 要确定状态参数，题目给定的nums，和存放最终结果的res 当然在列，还要补上用来锚定回溯定位点的 start锚点）
 * https://leetcode-cn.com/problems/subsets/
 * https://leetcode-cn.com/problems/subsets/solution/js-hui-su-by-liberhome-ngy7/
 * 给你一个整数数组 nums ，数组中的元素 互不相同 。返回该数组所有可能的子集（幂集）。
 * 解集 不能 包含重复的子集。你可以按 任意顺序 返回解集。
 */

function subsets(nums) {
  const ret = [];
  const route = [];

  function backtrack(nums, start, route) {
    // 先把上一轮的一维结果存入最终二维结果集
    ret.push(route.slice(0));

    // 从start锚点向后循环依次把nums[i]加入一维结果集
    for (let i = start; i < nums.length; i++) {
      route.push(nums[i]);

      // 更新锚点和一维结果集，递归回溯
      backtrack(nums, i + 1, route);

      // 最后撤销本轮接入一维结果集的结果 探索未曾出现的可能
      route.pop();
    }
  }

  backtrack(nums, 0, route);

  return ret;
}
```
