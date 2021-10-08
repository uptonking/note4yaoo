---
title: job-leetcode-sort
tags: [algorithms, coding, job, leetcode, sort]
created: '2021-10-05T09:04:03.081Z'
modified: '2021-10-06T14:47:06.903Z'
---

# job-leetcode-sort

# guide

# 数组中的第K个最大元素

```JS
/**
 * * 数组中的第K个最大元素。
 * * 思路：先从最后非叶子节点从后往前构建大顶堆，然后将堆顶交换到未排序末尾，重复交换 k 次
 * https://leetcode-cn.com/problems/kth-largest-element-in-an-array/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/62
 */
function findKthLargest(nums, k) {
  const len = nums.length;
  if (len === 1) return nums[0];

  // 整个数组，从最后一个非叶子节点从后往前构建大顶堆，使数组整体有序
  for (let i = Math.floor(len / 2 - 1); i >= 0; i--) {
    heapifyMax(nums, i, len);
  }

  // 👀️ 处理到第k个数就可以结束了
  for (let j = len - 1; j >= len - k; j--) {
    swap(nums, 0, j);
    heapifyMax(nums, 0, j);
  }

  return nums[len - k];
}
```

# 前K个高频元素

```JS
/**
 * * 前K个高频元素。给定一个非空的整数数组，返回其中出现频率前k高的元素。
 * * 思路：使用Map存储值和频率，然后对频率构建大顶堆，虽然比较的是频率，但需要根据key获取频率
 * https://leetcode-cn.com/problems/top-k-frequent-elements/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/61
 * 遍历一遍数组统计每个元素的频率，并将元素值（key）与出现的频率（value）保存到 map 中
 */
function topKFrequent(nums, k) {
  // let map ={};// 不要用对象字面量，若扩展到任意类型的元素频率统计，需要区分 1和 '1'
  const map = new Map();

  nums.forEach((num) => {
    if (map.has(num)) {
      map.set(num, map.get(num) + 1);
    } else {
      map.set(num, 1);
    }
  });
  const mapSize = map.size;
  const mapKeys = [...map.keys()];

  if (mapSize <= k) return mapKeys;

  for (let i = Math.floor(mapSize / 2 - 1); i >= 0; i--) {
    heapifyMax(mapKeys, i, mapSize, map);
  }

  for (let j = mapSize - 1; j >= mapSize - k; j--) {
    swap(mapKeys, 0, j);
    heapifyMax(mapKeys, 0, j, map);
  }

  return mapKeys.slice(-k).reverse();
}

function heapifyMax(nums, i, heapSize, map) {
  for (let j = 2 * i + 1; j < heapSize; j = 2 * j + 1) {
    if (j + 1 < heapSize) {
      if (!map && nums[j] < nums[j + 1]) {
        j++;
      }

      if (map && map.get(nums[j]) < map.get(nums[j + 1])) {
        j++;
      }
    }

    if (
      (!map && nums[i] < nums[j]) ||
      (map && map.get(nums[i]) < map.get(nums[j]))
    ) {
      swap(nums, i, j);
      i = j;
    } else {
      break;
    }
  }
}
```

# 最小的k个数

```JS
/**
 * * 最小的k个数；
 * * 思路：堆排序，维护一个K大小的小顶堆。
 * https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/59
 *
 * 动态数组可能会插入或删除元素，难道我们每次求 Top k 问题的时候都需要对数组进行重新排序吗？
 */
function getLeastNumbers(arr, k) {
  if (k === 0) return [];
  const len = arr.length;
  if (len <= 1) return arr;

  for (let i = Math.floor(len / 2 - 1); i >= 0; i--) {
    heapifyMin(arr, i, len);
  }

  for (let j = len - 1; j >= len - k; j--) {
    swap(arr, 0, j);
    heapifyMin(arr, 0, j);
  }

  console.log(arr);

  return arr.slice(-k).reverse();
}

function heapifyMin(arr, i, heapSize) {
  for (let j = 2 * i + 1; j < heapSize; j = 2 * j + 1) {
    if (j + 1 < heapSize && arr[j] > arr[j + 1]) {
      j++;
    }

    if (arr[i] > arr[j]) {
      swap(arr, i, j);
      i = j;
    } else {
      break;
    }
  }
}
```
