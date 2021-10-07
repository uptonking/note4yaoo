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

# 搜索旋转排序数组

```JS
/**
 * * 搜索旋转排序数组
 * * 思路：二分查找
 * - 首先判断那边是有序数组 还是在无序数组那边，
 * https://leetcode-cn.com/problems/search-in-rotated-sorted-array/
 * https://juejin.cn/post/6986639440441507871
 * - 在下标k旋转使数组变为 [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]
 * - 给你 旋转后 的数组 nums 和一个整数 target ，如果 nums 中存在这个目标值 target ，则返回它的下标，否则返回 -1 。
 *
 */
function search(nums, target) {
  let l = 0;
  let r = nums.length - 1;

  while (l <= r) {
    // 求取中间的值
    const mid = Math.floor(l + (r - l) / 2);

    if (nums[l] < nums[mid]) {
      // 如果左边的是有序数列
      // 如果在有序数列中，则缩小范围到左边的数组中
      if (nums[l] <= target && target <= nums[mid]) {
        r = mid;
      } else {
        l = mid + 1;
      }
    } else if (nums[l] > nums[mid]) {
      // 如果右边的有序数列，则还是在左边找，
      // 因为是旋转后的升序数组，所以如果arr[l] <= target || target <= arr[mid]，则有还是在左边数组中
      if (nums[l] <= target || target <= nums[mid]) {
        r = mid;
      } else {
        l = mid + 1;
      }
    } else {
      // 如果遇到了 arr[l]===arr[mid]，有2中情况，第一个遇到了相同的值例如 [3,3,3,5],第二种情况找到了答案
      // 找到了答案
      if (nums[l] === target) {
        return l;
      } else {
        // 过滤掉重复值 继续下一轮循环
        l++;
      }
    }
  }

  return -1;
}
```
