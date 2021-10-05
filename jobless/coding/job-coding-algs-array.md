---
title: job-coding-algs-array
tags: [algorithms, array, coding, job, leetcode]
created: '2021-10-05T09:00:35.959Z'
modified: '2021-10-05T09:01:08.983Z'
---

# job-coding-algs-array

# guide

# 合并两个有序数组

```JS
/**
 * * 合并2个有序数组，原地合并；
 * - 因为有序，所以可以从后向前处理
 * https://leetcode-cn.com/problems/merge-sorted-array/
 */
function mergeTwoSortedArr(nums1, m, nums2, n) {

  let mm = m - 1;
  let nn = n - 1;

  let i = m + n - 1;

  while (nn >= 0) {

    // nums1太大了，已经处理完全部放右边了
    if (mm < 0) {
      nums1[i--] = nums2[nn--];
      continue;
    }

    nums1[i--] = nums1[mm] < nums2[nn] ? nums2[nn--] : nums1[mm--];
  }

}
```

```JS
/**
 * * 合并两个数组，数组可无序；
 * * 思路是归并排序的合并部分算法
 * - m和n表示元素个数
 */
function mergeTwoArr(nums1, m, nums2, n) {
  const temp = [];
  const resultLen = m + n;

  // 两边都还有数组
  while (m && n) {
    if (nums1[0] < nums2[0]) {
      temp.push(nums1.shift());
      m--;
    } else {
      temp.push(nums2.shift());
      n--;
    }
  }

  if (m > 0) {
    temp.push(...nums1.slice(0, m))
  }
  if (n > 0) {
    temp.push(...nums2.slice(0, n))
  }

  // oj系统不支持直接修改
  // nums1 = temp;
  for (let i = 0; i < resultLen; i++) {
    nums1[i] = temp[i]
  }

  return nums1
}
```

# 打乱数组 洗牌算法

> 设计算法来打乱一个没有重复元素的整数数组。

```JS
/**
 * * 洗牌算法。打乱数组。
 * - Fisher-Yates 洗牌算法，
 *   - 时间复杂度： O(n) 空间复杂度：O(n)
 *   * 基本思想就是从原始数组中随机取一个之前没取过的数字到新的数组中
 * - Knuth-Durstenfeld shuffle
 *   - 在Fisher 等人的基础上对算法进行了改进，在原始数组上对数字进行交互，省去了额外O(n)的空间
 * https://leetcode-cn.com/problems/shuffle-an-array/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/74
 * https://leetcode-cn.com/problems/shuffle-an-array/solution/jing-dian-xi-pai-suan-fa-fisher-yates-shufflesuan-/
 * https://segmentfault.com/a/1190000039246947
 * 浅拷贝数组，利用random()方法重制数组下标索引。
 * 可用来实现音乐随机播放。
 *
 */
const Solution = function(nums) {
  this.nums = nums;
};
Solution.prototype.reset = function() {
  return this.nums;
};

// Knuth-Durstenfeld Shuffle
// 将“删除”的数字移至数组末尾，即将每个被删除数字与最后一个未删除的数字进行交换。
Solution.prototype.shuffle = function() {
  // 每次拷贝数组
  const res = [...this.nums];
  const len = res.length;

  // * 从后往前，相当于每次随机取一个不重复的元素，放到数组末尾，尾部元素一直都是乱序的
  for (let i = len - 1; i >= 0; i--) {
    const randIndex = Math.floor(Math.random() * (i + 1));
    swap(res, randIndex, i);
  }

  return res;
};

// Fisher–Yates shuffle
function shuffle(arr) {
  let random;
  const newArr = [];

  // 重复直到所有元素都被删除。
  while (arr.length) {
    // 从第1个到剩余的未删除项（包含）之间选择一个随机数 k。
    random = Math.floor(Math.random() * arr.length);

    // 从剩余的元素中将第k个元素删除并取出，放到新数组中。
    newArr.push(arr[random]);

    // 从原数组中删除
    arr.splice(random, 1);
  }

  return newArr;
}

const swap = function(arr, i, j) {
  const temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
};
```
