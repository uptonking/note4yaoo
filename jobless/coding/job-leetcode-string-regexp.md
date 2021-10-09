---
title: job-leetcode-string-regexp
tags: [algorithms, coding, job, leetcode, regexp, string]
created: '2021-10-05T09:04:48.742Z'
modified: '2021-10-06T14:47:19.962Z'
---

# job-leetcode-string-regexp

# guide
- 字典序就是字母的顺序，a b c d ... z，题目要求最小字典序就是尽量让字母按照顺序出现，比如abc字典序小于acb
# 字符串相加

```js
/**
 * * 字符串相加。
 * * 思路：双指针 + 进位处理。
 * 给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和并同样以字符串形式返回。
 * https://leetcode-cn.com/problems/add-strings/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/32
 * https://juejin.cn/post/6985884324025499661
 * 从 num1 ，num2 的尾部开始计算，模拟人工加法，保存到 tmp 中；
 * 计算 tmp 的个位数，并添加到 result 的头部，这里的 result 是 string 类型，不是 number 类型；
 * 两个字符相减会变成number类型。
 */
function addStrings(num1, num2) {
  // 使用两个指针分别指向数字字符串的末尾位置。
  let i = num1.length - 1;
  let j = num2.length - 1;
  // 变量carry记录进位。
  let carry = 0;
  let ret = '';

  while (i >= 0 || j >= 0) {
    const n1 = i >= 0 ? num1[i] : 0;
    const n2 = j >= 0 ? num2[j] : 0;

    // 进位当当前两个数的和
    const sum = Number(n1) + Number(n2) + carry;

    // 获取一个当前位
    ret = (sum % 10) + ret;

    // 获取进位
    carry = Math.floor(sum / 10);
    i--;
    j--;
  }

  if (carry === 1) ret = carry + ret;
  return ret;
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

# 翻转字符串里的单词

```JS
/**
 * * 翻转字符串里的单词(无空格字符构成一个单词)。
 * 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
 * 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 * 示例： "the sky is blue"  -->  "blue is sky the"
 * https://leetcode-cn.com/problems/reverse-words-in-a-string/
 */
function reverseWords(s) {
  // return s.match(/[\w!,]+/g).reverse().join(" ");
  return s.trim().replace(/\s+/g, ' ').split(' ').reverse().join(' ');
}
```

# 最小覆盖子串

```JS
/**
 * * 最小覆盖子串
 * * 思路：先找出所有的包含T的子串。找出长度最小的
 * https://leetcode-cn.com/problems/minimum-window-substring/
 * https://github.com/sl1673495/leetcode-javascript/issues/43
 * https://leetcode-cn.com/problems/minimum-window-substring/solution/zui-xiao-fu-gai-zi-chuan-jshua-dong-chuang-kou-shu/
 * https://leetcode-cn.com/problems/minimum-window-substring/solution/76-zui-xiao-fu-gai-zi-chuan-js-by-6xiaodi/
 * 返回 s 中涵盖 t 所有字符的最小子串
 */
function minWindow(s, t) {
  // 先制定目标 根据t字符串统计出每个字符应该出现的个数
  const targetMap = makeCountMap(t);

  const sl = s.length;
  const tl = t.length;
  let left = 0; // 左边界
  let right = -1; // 右边界
  const countMap = {}; // 当前窗口子串中 每个字符出现的次数
  let min = ""; // 当前计算出的最小子串

  // 循环终止条件是两者有一者超出边界
  while (left <= sl - tl && right <= sl) {
    // 和 targetMap 对比出现次数 确定是否满足条件
    let isValid = true;
    Object.keys(targetMap).forEach((key) => {
      const targetCount = targetMap[key];
      const count = countMap[key];
      if (!count || count < targetCount) {
        isValid = false;
      }
    });

    if (isValid) {
      // 如果满足 记录当前的子串 并且左边界右移
      const currentValidLength = right - left + 1;
      if (currentValidLength < min.length || min === "") {
        min = s.substring(left, right + 1);
      }
      // 也要把map里对应的项去掉
      countMap[s[left]]--;
      left++;
    } else {
      // 否则右边界右移
      addCountToMap(countMap, s[right + 1]);
      right++;
    }
  }

  return min;
}

function addCountToMap(map, str) {
  if (!map[str]) {
    map[str] = 1
  } else {
    map[str]++
  }
}

function makeCountMap(strs) {
  const map = {}
  for (let i = 0; i < strs.length; i++) {
    const letter = strs[i]
    addCountToMap(map, letter)
  }
  return map
}

// console.log(minWindow("aa", "a"))

function minWindow2(s, t) {
  let left = 0;
  let right = 0;

  // 需要的子串及字符个数
  const need = new Map();

  for (const c of t) {
    need.set(c, need.has(c) ? need.get(c) + 1 : 1);
  }

  let needTypeCount = need.size; // 需求中不同字符总个数
  let minSub = '';
  while (right < s.length) {
    const current = s[right];
    if (need.has(current)) {
      // 需要对应字符个数减1
      need.set(current, need.get(current) - 1);
      if (need.get(current) === 0) {
        needTypeCount--;
      }
    }

    // 完全满足t字符串的子串了，尝试尽可能减小子串的长度
    while (needTypeCount === 0) {
      const mewMinSub = s.substring(left, right + 1); // 左闭右开

      // 找到最小子串
      // 优化：minSub最开始是空字符串无需逻辑判断，到下一轮再比较长度
      if (!minSub || mewMinSub.length < minSub.length) {
        minSub = mewMinSub;
      }

      const currentLight = s[left];
      // 移动左指针对应字符在需求列表中，对应字符需求数加1（子串减少一个目标字符，就有一个需求量的增加）
      if (need.has(currentLight)) {
        need.set(currentLight, need.get(currentLight) + 1);
        if (need.get(currentLight) === 1) {
          needTypeCount++;
        }
      }
      left++;
    }

    right++;
  }
  return minSub;
}
```
