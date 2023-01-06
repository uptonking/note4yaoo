---
title: job-leetcode-string-repeat
tags: [leetcode, repeat, string]
created: 2021-10-08T19:43:08.951Z
modified: 2021-10-08T19:43:27.831Z
---

# job-leetcode-string-repeat

# 查找字符串数组中的最长公共前缀 LCP

```JS
/**
 * * 查找字符串数组中的最长公共前缀。
 * * 思路：选一个字符串作为基准，用子串匹配后面每个字符串是否都有公共部分，有就退出循环，没有就继续查找
 * https://leetcode-cn.com/problems/longest-common-prefix/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/19
 */
function longestCommonPrefix(strs) {
  if (!strs.length) return '';
  if (strs.length === 1) return strs[0];

  // 👀️计算出长度最短的字符串,作为基准，
  // 也可以简单取第1个字符串作为基准
  const minLenStr = strs.find(
    (i) => i.length === Math.min(...strs.map((i) => i.length)),
  );

  // 从第1个字符开始往后逐次比较，最长公共子串就保存在这里
  let ret = '';
  for (let i = 0; i < minLenStr.length; i++) {
    const curr = minLenStr.slice(0, i + 1);
    if (
      strs.every((item) => item.slice(0, i + 1) === curr)
    ) {
      ret = curr;
    }
  }
  return ret;
}

function longestCommonPrefix2(strs) {
  if (strs === null || strs.length === 0) return '';
  let ret = strs[0];
  for (let i = 1; i < strs.length; i++) {
    let j = 0;
    for (; j < ret.length && j < strs[i].length; j++) {
      if (ret.charAt(j) !== strs[i].charAt(j)) break;
    }
    ret = ret.substring(0, j);
    if (ret === '') return '';
  }
  return ret;
}
```

# 无重复字符的最长子串
- 给定一个字符串 s ，请你找出其中不含有重复字符的最长子串的长度。

```JS
/**
 * * 无重复字符的最长子串。
 * * 思路：使用一个数组来维护滑动窗口，遍历字符串，判断字符是否在滑动窗口数组里
 * https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/21
 * 时间复杂度：O(n2)， 其中 arr.indexOf() 时间复杂度为 O(n) ，arr.splice(0, index+1) 的时间复杂度也为 O(n)
 * 
 */
function lengthOfLongestSubstring(s) {
  // 当前处理的无重复子串的字符
  const arr = [];
  // 最长子串的长度
  let max = 0;
  for (let i = 0; i < s.length; i++) {

    const index = arr.indexOf(s[i]);
    if (index > -1) {
      // 👀️ 如果是重复字符，则删除重复部分的闭区间
      arr.splice(0, index + 1);
    }

    // 将无重复的字符加入数组；刚删除了，也可以再加一次
    arr.push(s[i]);
    max = Math.max(arr.length, max);
  }
  return max;
}
```

# 验证回文串
- 回文字符串 是正着读和倒过来读一样的字符串

```JS
/**
 * * 验证回文串
 * * 思路：头部和尾部夹逼比较
 * https://leetcode-cn.com/problems/valid-palindrome/
 */
// 最简单的回文字符串验证，考虑所有字符
function isPalindrome(s) {
  if (typeof s !== 'string') return false;
  return s.split('').reverse().join('') === s;
}

function isPalindrome(s) {
  if (typeof s !== 'string') return false;
  // 只处理字母和数字，忽略大小写，去掉其他字符
  s = s.replace(/[^0-9a-zA-Z]/g, '').toLocaleLowerCase();

  let i = 0;
  let j = s.length - 1;
  while (i < j) {

    if (s[i] !== s[j]) return false;
    i++;
    j--;
  }
  return true;
}
```

# 回文子串的数量

```JS
/**
 * * 计算字符串中有多少个回文子串。
 * https://leetcode-cn.com/problems/palindromic-substrings/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/107
 * 具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被视作不同的子串。
 * 暴力法
 */
function countSubstrings(s) {
  let count = 0;
  for (let i = 0; i < s.length; i++) {
    for (let j = i; j < s.length; j++) {
      if (isPalindrome(s.substring(i, j + 1))) {
        count++;
      }
    }
  }
  return count;
}

// 中心扩展法
const countSubstrings2 = function(s) {
  const len = s.length;
  let res = 0;
  for (let i = 0; i < 2 * len - 1; i++) {
    let l = i / 2;
    let r = i / 2 + (i % 2);
    while (l >= 0 && r < len && s.charAt(l) == s.charAt(r)) {
      l--;
      r++;
      res++;
    }
  }
  return res;
};

// 动态规划
const countSubstrings3 = function(s) {
  const len = s.length;
  let count = 0;
  const dp = new Array(len);
  for (let j = 0; j < len; j++) {
    for (let i = 0; i <= j; i++) {
      if (s[i] === s[j] && (j - i <= 1 || dp[i + 1])) {
        dp[i] = true;
        count++;
      } else {
        dp[i] = false;
      }
    }
  }
  return count;
};
```

# 最长回文子串

```JS
/**
 * * 最长回文子串
 * * 思路: 中心扩展法的核心就是通过找到回文中心，然后以该中心向左右两边扩展来查找。
 * https://leetcode-cn.com/problems/longest-palindromic-substring/
 * https://juejin.cn/post/6844903902865784846
 * https://writings.sh/post/algorithm-longest-palindromic-substring
 * https://leetcode-cn.com/problems/longest-palindromic-substring/solution/javascriptdui-zhong-xin-kuo-zhan-fa-de-li-jie-by-l/
 */
function longestPalindrome(s) {
  if (!s) return '';
  if (s.length === 1) return s;
  if (s.length === 2) return s[0] === s[1] ? s : s[1];

  let maxStr = '';
  const len = s.length;

  for (let i = 0; i < len; i++) {
    let even = ''; // 定义偶数中心回文
    let odd = ''; // 定义奇数中心回文

    if (s[i] === s[i + 1]) {
      // 若是偶数中心回文，比较中心的前一项和后一项
      const evenIndex = center(s, i - 1, i + 2);
      even = s.slice(evenIndex.left, evenIndex.right);
    }

    // 若是奇数中心回文,
    const oddIndex = center(s, i - 1, i + 1);
    odd = s.slice(oddIndex.left, oddIndex.right);

    // 比较奇、偶，选择最长的
    const longer = even.length > odd.length ? even : odd;
    maxStr = maxStr.length > longer.length ? maxStr : longer;
  }

  return maxStr;
}

// 中心扩展
function center(s, left, right) {
  const len = s.length;
  while (left >= 0 && right < len && s[left] === s[right]) {
    left--;
    right++;
  }
  return { left: left + 1, right: right };
}
```

```JS
// 动态规划
function longestPalindromeDp(s) {
  if (s.length === 1) return s;

  // 创建二阶数组存储从j到i是否是回文数组，0为不回文，1为回文
  const arr = new Array(s.length).fill([]);

  // 存储最长回文子串的起始位置
  let begin = 0;
  // 存储最长子串的长度
  let max = 0;

  for (let i = 0; i < s.length; i++) {
    let j = 0;
    while (j <= i) {
      // 如果 i-j <= 1 时，说明i位置和j位置要么是重合的，要么是相邻的，即为最后一次查找
      // 否则继续查询[j + 1]到[i - 1]是否为回文
      if (s[j] === s[i] && (i - j <= 1 || arr[j + 1][i - 1])) {
        // 如果符合上述条件，说明j到i是回文
        arr[j][i] = 1;

        if (i - j + 1 > max) {
          // 如果当前子串大于存储的子串长度，则替换之
          begin = j;
          // 注意+1，比如从3到5的长度为3 = 5 - 3 + 1
          max = i - j + 1;
        }
      }

      j++;
    }
  }
  return s.substr(begin, max);
}
```
