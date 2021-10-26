---
title: job-leetcode-problems
tags: [algorithms, coding, job, leetcode]
created: '2021-10-06T19:59:34.467Z'
modified: '2021-10-06T19:59:58.846Z'
---

# job-leetcode-problems

# guide

# 螺旋矩阵

```JS
/**
 * * 螺旋矩阵
 * * 思路1：逐个遍历，在边界先确定方向，再根据方向修改索引，遍历下一个
 * * 思路2：先遍历外圈，再递归遍历内圈
 * https://leetcode-cn.com/problems/spiral-matrix/
 * https://leetcode-cn.com/problems/spiral-matrix/solution/jsshi-xian-luo-xuan-ju-zhen-by-adorable-deg/
 * m行n列的矩阵 matrix ，请按照 顺时针螺旋顺序，返回矩阵中的所有元素。
 * m == matrix.length; n == matrix[i].length
 */
function spiralOrder(matrix) {
  const m = matrix.length;
  const n = matrix[0].length;

  let i = 0;
  let j = 0;

  const ret = [];

  // 0-右，1-下，2-左，3-上
  let direction = 0;

  for (let curr = 0; curr < m * n; curr++) {
    ret.push(matrix[i][j]);
    // console.log('curr, ', i, j, matrix[i][j]);

    matrix[i][j] = true;

    // 若正在向右，且到底边界 或 右方下一个已访问过了，则改方向
    if (direction === 0 && (j === n - 1 || matrix[i][j + 1] === true)) {
      direction = 1;
    }
    if (direction === 1 && (i === m - 1 || matrix[i + 1][j] === true)) {
      direction = 2;
    }
    if (direction === 2 && (j === 0 || matrix[i][j - 1] === true)) {
      direction = 3;
    }
    if (direction === 3 && (i === 0 || matrix[i - 1][j] === true)) {
      direction = 0;
    }

    if (direction === 0) j++;
    if (direction === 1) i++;
    if (direction === 2) j--;
    if (direction === 3) i--;
  }

  return ret;
}

// 按圈递归处理
function spiralOrderRecursive(matrix) {
  const recursive = (arr, result) => {
    for (let i = 0, len = arr.length; i < len; i++) {
      if (!arr[i].length) return result;

      if (i === 0) {
        // 第一行的元素正序插入
        result = result.concat(arr[i]);
      } else if (i === len - 1) {
        // 倒数第一行的元素倒序插入
        result = result.concat(arr[i].reverse());
      } else {
        // 其他取每行的最后一个，即最右边的值
        result.push(arr[i].pop());
      }
    }

    // 移除第一行和最后一行
    arr.shift();
    arr.pop();

    // 访问并移除每行左边第1个值
    for (let i = arr.length - 1; i >= 0; i--) {
      if (arr[i].length) {
        // shift 删除第一个元素并返回删除的值
        result.push(arr[i].shift());
      } else {
        return result;
      }
    }

    // 如果数组还有，就递归处理
    if (arr.length) {
      return recursive(arr, result);
    } else {
      return result;
    }
  };

  return recursive(matrix, []);
}
```

# 缺失的第一个正数

```JS
/**
 * * 缺失的第一个正数
 * * 理想情况下，索引i的位置的最小正数是 i+1
 * * 思路：将值大小在数组长度范围内的这些值交换到正确位置，最后遍历数组，nums[i]!==i+1的就是缺失的
 * 未排序的整数数组，请你找出其中没有出现的最小的正整数。
 * https://leetcode-cn.com/problems/first-missing-positive/
 * https://mingtiao.top/2020/06/27/Leetcode-41-%E7%BC%BA%E5%A4%B1%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E6%AD%A3%E6%95%B0/
 * * 空间复杂度O(1)，不能用额外存储，只能置换
 *
 */
function firstMissingPositive(nums) {
  const len = nums.length;

  // 逐个循环，将值大小在[1,len]范围内的nums[i]元素值放到正确的位置，即 1,2,3...
  for (let i = 0; i < len; i++) {
    // 如果索引i的位置方的不是 i+1，
    while (nums[i] !== i + 1) {
      // 不为正确的数字

      // 若nums[i]不在1 ~len范围内，
      if (nums[i] <= 0 || nums[i] > len) break;
      // num[nums[i] - 1]位置上已经放置了正确的数字，不必再交换
      if (nums[i] === nums[nums[i] - 1]) break;

      // 若nums[i]的值在长度范围内，则进行交换，使nums[i]放置到正确位置即 nums[i]-1
      const temp = nums[nums[i] - 1];
      nums[nums[i] - 1] = nums[i];
      nums[i] = temp;
    }
  }

  for (let i = 0; i < len; i++) {
    if (nums[i] !== i + 1) return i + 1;
  }

  return len + 1;
}
```

# 复原 IP 地址

```JS
/**
 * * 复原 IP 地址
 * https://leetcode-cn.com/problems/restore-ip-addresses/
 * https://juejin.cn/post/6844904148509409293
 * 给定一个只包含数字的字符串，用以表示一个 IP 地址，返回所有可能从 s 获得的 有效 IP 地址
 */
function restoreIpAddresses(s) {
  //  判断最大边界
  if (s.length > 12) return [];
  // 保存所有符合条件的IP地址
  const ret = [];

  // 分四步递归处理ip分段
  const search = (cur, sub) => {
    // 边界条件，数组长度等于4且组合起来与之前的字符串相等
    if (cur.length === 4 && cur.join('') === s) {
      //  过滤 001 010等情况
      if (cur[3].length > 1 && cur[3][0] === 0) {
        return false;
      }
      ret.push(cur.join('.'));
    } else {
      // 正常的处理过程，最多循环三次
      for (let i = 0, len = Math.min(3, sub.length), tmp; i < len; i++) {
        tmp = sub.substr(0, i + 1);
        //  过滤 001 010等情况
        if (tmp.length > 1 && tmp[0] == 0) {
          return false;
        }

        if (tmp < 256) {
          // 如果当前的数小于 256 说明在 255 范围内，接着递归调用(把不是范围内的排出掉)
          search(cur.concat([tmp]), sub.substr(i + 1));
        }
      }
    }
  };

  search([], s);
  return ret;
}
```

# 比较版本号

```JS
/**
 * * 比较版本号
 * * 思路1: 单指针，使用split分割成数组
 * * 思路2: 双指针，不使用数组，用双指针去指向当前版本号所在的位置，自己分割字符
 * https://leetcode-cn.com/problems/compare-version-numbers/
 * https://leetcode-cn.com/problems/compare-version-numbers/solution/bi-jiao-ban-ben-hao-dan-zhi-zhen-shuang-zhi-zhen-j/
 * 版本号由一个或多个修订号组成，各修订号由一个 '.' 连接
 * 每个修订号由 多位数字 组成，可能包含 前导零 。
 * 比较修订号时，只需比较 忽略任何前导零后的整数值
 */
function compareVersion(version1, version2) {
  const arr1 = version1.split('.');
  const arr2 = version2.split('.');

  let pointer = 0;

  // 先比较完相同长度的部分
  while (pointer < arr1.length && pointer < arr2.length) {
    // 💡️ 字符串相减，会先转换成数值再相减；如 '3'-'02' 得到-1
    const res = arr1[pointer] - arr2[pointer];
    if (res === 0) {
      pointer++;
    } else {
      return res > 0 ? 1 : -1;
    }
  }

  // 上面比完若未结束返回，到这里应该相同长度的部分是相等的

  // 若arr1仍有小版本号
  while (pointer < arr1.length) {
    if (Number(arr1[pointer]) > 0) {
      // 第1个大
      return 1;
    } else {
      pointer++;
    }
  }

  // 若arr2仍有小版本号
  while (pointer < arr2.length) {
    if (Number(arr2[pointer]) > 0) {
      // 第1个小
      return -1;
    } else {
      pointer++;
    }
  }

  // 版本号完全相同
  return 0;
}

/**
 * * 双指针法，将字符分割的部分自己实现
 */
function compareVersion(version1, version2) {
  let p1 = 0;
  let p2 = 0;

  /** 寻找当前区间的版本号 */
  const findDigit = (str, start) => {
    let i = start;
    while (str[i] !== '.' && i < str.length) {
      i++;
    }
    return i;
  };

  while (p1 < version1.length && p2 < version2.length) {
    const nextA = findDigit(version1, p1);
    const nextB = findDigit(version2, p2);
    const numA = Number(version1.substr(p1, nextA - p1));
    const numB = Number(version2.substr(p2, nextB - p2));
    if (numA !== numB) {
      return numA > numB ? 1 : -1;
    }
    p1 = nextA + 1;
    p2 = nextB + 1;
  }
  // 若arrayA仍有小版本号
  while (p1 < version1.length) {
    const nextA = findDigit(version1, p1);
    const numA = Number(version1.substr(p1, nextA - p1));
    if (numA > 0) {
      return 1;
    }
    p1 = nextA + 1;
  }
  // 若arrayB仍有小版本号
  while (p2 < version2.length) {
    const nextB = findDigit(version2, p2);
    const numB = Number(version2.substr(p2, nextB - p2));
    if (numB > 0) {
      return -1;
    }
    p2 = nextB + 1;
  }
  // 版本号完全相同
  return 0;
}
```
