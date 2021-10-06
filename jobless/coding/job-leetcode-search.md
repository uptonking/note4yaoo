---
title: job-leetcode-search
tags: [algorithms, coding, job, leetcode, search]
created: '2021-10-05T09:04:20.790Z'
modified: '2021-10-06T14:46:44.158Z'
---

# job-leetcode-search

# guide

# 在排序数组中查找元素的第一个和最后一个位置

```JS
function searchRange(nums, target) {
  let mid;
  let low = 0;
  let high = nums.length - 1;

  while (low <= high) {
    mid = Math.floor((low + high) / 2);

    if (nums[mid] === target) {
      let start = mid;
      let end = mid;
      while (nums[start] === target)
        start--;
      while (nums[end] === target)
        end++;

      return [start + 1, end - 1];
    }

    if (nums[mid] > target) {
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return [-1, -1];
}
```
