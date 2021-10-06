---
title: job-leetcode-string-regexp
tags: [algorithms, coding, job, leetcode, regexp, string]
created: '2021-10-05T09:04:48.742Z'
modified: '2021-10-06T14:47:19.962Z'
---

# job-leetcode-string-regexp

# guide

- to-do
  - 最长回文子串
    - https://leetcode-cn.com/problems/longest-palindromic-substring/
# 查找字符串数组中的最长公共前缀 LCP

```JS
/**
 * * 查找字符串数组中的最长公共前缀。
 * https://leetcode-cn.com/problems/longest-common-prefix/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/19
 * - 用数组中的第一个字符串作为基准
 * - 匹配后面每个字符串是否都有公共部分，有就退出循环，没有就继续查找
 */

function longestCommonPrefix(strs) {
  if (!strs.length) return '';
  if (strs.length === 1) return strs[0];

  // 取最短的字符串作为基准，也可以简单取第1个字符串作为基准
  const minLenStr = strs.find(
    (i) => i.length === Math.min(...strs.map((i) => i.length)),
  );

  // 从第1个字符开始往后逐次比较
  let ret = '';
  for (let i = 0; i < minLenStr.length; i++) {
    if (
      strs.every((item) => item.slice(0, i + 1) === minLenStr.slice(0, i + 1))
    ) {
      ret = minLenStr.slice(0, i + 1);
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

# 验证回文串
- 回文字符串 是正着读和倒过来读一样的字符串

```JS
/**
 * * 验证回文串
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

# 计算字符串中有多少个回文子串

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

# 第一个只出现一次的字符

```JS
/**
 * * 第一个只出现一次的字符
 * https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/50
 * 使用 map 两次遍历即可：
 * 遍历字符串，将每个字符的值与出现次数记录到map中
 * 再次遍历 map.keys() ，获取 map 中每个字符出现的次数，判断是否仅仅只有 1 次，返回第一个仅出现一次的字符
 */

function firstUniqChar(s) {
  if (!s) return ' ';

  const map = {};

  for (let i = 0, len = s.length; i < len; i++) {
    // 出现1次的就是1，再次出现就会变0
    map[s[i]] = map[s[i]] === undefined ? 1 : 0;
  }

  for (const item in map) {
    if (map[item] === 1) {
      return item;
    }
  }

  return ' ';
}
```

# 无重复字符的最长子串

```JS
/**
 * * 无重复字符的最长子串。
 * https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/21
 * 快慢指针维护一个滑动窗口，如果滑动窗口里面有快指针fastp所指向的元素（记录这重复元素在滑动窗口的索引tmp），
 * 那么滑动窗口要缩小，即慢指针slowp要移动到tmp的后一个元素。
 */

/**
 * 使用一个数组来维护滑动窗口，遍历字符串，判断字符是否在滑动窗口数组里
 * 时间复杂度：O(n2)， 其中 arr.indexOf() 时间复杂度为 O(n) ，arr.splice(0, index+1) 的时间复杂度也为 O(n)
 */
function lengthOfLongestSubstring(s) {
  const arr = [];
  let max = 0;
  for (let i = 0; i < s.length; i++) {
    const index = arr.indexOf(s[i]);
    if (index !== -1) {
      arr.splice(0, index + 1);
    }
    arr.push(s.charAt(i));
    max = Math.max(arr.length, max);
  }
  return max;
}
```

# 翻转字符串里的单词

```JS
/**
 * * 翻转字符串里的单词(无空格字符构成一个单词)。
 * 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
 * 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 * https://leetcode-cn.com/problems/reverse-words-in-a-string/
 */

function reverseWords(s) {
  // return s.match(/[\w!,]+/g).reverse().join(" ");
  return s.trim().replace(/\s+/g, ' ').split(' ').reverse().join(' ');
}
```

# 字符串相加

```js
/**
 * * 字符串相加。
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/32
 * 从 num1 ，num2 的尾部开始计算，模拟人工加法，保存到 tmp 中；
 * 计算 tmp 的个位数，并添加到 result 的头部，这里的 result 是 string 类型，不是 number 类型；
 */
function addStrings(num1, num2) {
  let i = num1.length - 1;
  let j = num2.length - 1;
  let move = 0;
  let result = '';

  let n1;
  let n2;

  while (i >= 0 || j >= 0) {
    n1 = i >= 0 ? num1[i] : 0;
    n2 = j >= 0 ? num2[j] : 0;
    const tmp = Number(n1) + Number(n2) + move;
    move = tmp >= 10 ? 1 : 0;
    result = (tmp % 10) + result;
    i--;
    j--;
  }
  return move ? move + result : result;
}
```

# 字符串转换整数 (atoi)

```JS
/**
 * * 字符串转换整数 (atoi)
 * https://leetcode-cn.com/problems/string-to-integer-atoi/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/132
 * 如果第一个字符不能转换为数字，parseInt会返回 NaN。
 */

function myAtoi(s) {
  // parseInt
  const number = parseInt(s, 10);

  // 判断 parseInt 的结果是否为 NaN，是则返回 0
  if (isNaN(number)) return 0;

  if (number < Math.pow(-2, 31) || number > Math.pow(2, 31) - 1) {
    // 超出
    return number < Math.pow(-2, 31) ? Math.pow(-2, 31) : Math.pow(2, 31) - 1;
  }

  return number;
}
```
