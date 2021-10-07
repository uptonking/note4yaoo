---
title: job-leetcode-search-base
tags: [algorithms, coding, job, leetcode, search]
created: '2021-10-05T10:10:13.503Z'
modified: '2021-10-06T14:46:53.654Z'
---

# job-leetcode-search-base

# guide

# 二分查找
- 时间复杂度 O(logn)
- 空间复杂度 O(1)

- 二分查找局限性
  - 数组必须有序
  - 针对的对象是数组结构，因为是通过下标来随机访问元素
  - 数组太小不合适，直接使用顺序查找即可
  - 数组太长不合适，数组要求连续的内存空间，数组太长不利于存储

```JS
function binarySearch(nums, target) {

  if (!nums || nums.length < 1) return -1;

  let low = 0;
  let high = nums.length;
  let mid;

  // 包含只有1个元素的情况
  while (low <= high) {
    mid = Math.floor((low + high) / 2);

    if (target === nums[mid]) return mid;

    if (target > nums[mid]) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return -1;
}

function binarySearchRecursive(nums, target, low, high) {
  if (!nums || nums.length < 1) return -1;

  if (low === undefined) low = 0;
  if (high === undefined) high = nums.length - 1;

  // 只有1个元素时，也要执行后面
  if (low > high) return -1;

  const mid = Math.floor((low + high) / 2);

  if (target === nums[mid]) return mid;

  if (target > nums[mid]) {
    return binarySearchRecursive(nums, target, mid + 1, high);
  } else {
    return binarySearchRecursive(nums, target, low, mid - 1);
  }

}
```

- ref
  - https://leetcode-cn.com/problems/binary-search/
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/83
