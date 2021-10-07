---
title: job-leetcode-linked-list
tags: [algorithms, coding, job, leetcode, linked-list]
created: '2021-10-05T09:01:17.377Z'
modified: '2021-10-06T14:46:31.518Z'
---

# job-leetcode-linked-list
> 单向链表

# guide

```JS
// 单向链表节点定义
function ListNode(val, next) {
  this.val = val === undefined ? 0 : val;
  this.next = next === undefined ? null : next;
}
```

# 反转单向链表
> 给你单链表的头节点 head，请你反转链表，并返回反转后的链表。

```JS
/**
 * * 反转链表。
 * * 三指针法。
 * https://leetcode-cn.com/problems/reverse-linked-list/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/14
 */
function reverseList(head) {
  if (!head || !head.next) return head;
  let prev = null;
  let curr = head;
  let next;
  while (curr) {
    // 临时保存 curr后继节点
    next = curr.next;
    // 反转当前节点
    curr.next = prev;
    prev = curr;
    curr = next;
  }
  // 最后返回新链表的头结点
  head = prev;
  return head;
}
```

```JS
/**
 * * 递归实现，从头节点开始，递归反转它的每一个节点，直到 null
 */
function reverseList2(head) {
  if (!head || !head.next) return head;
  return reverse(null, head);
}
function reverse(prev, curr) {
  if (!curr) return prev;
  const nextNode = curr.next;
  curr.next = prev;
  return reverse(curr, nextNode);
}
```

# 反转链表 指定范围

```JS
/**
 * * 反转链表 II 反转从位置 left 到位置 right 的链表节点
 * https://leetcode-cn.com/problems/reverse-linked-list-ii/
 * https://xie.infoq.cn/article/f5db6e4a84aef1339e4582d40
 */
function reverseBetween(head, left, right) {
  let prev = null;
  let curr = head;
  // 将prev和head都移动m-1次，prev在m-1位置，head在m位置
  while (left > 1) {
    prev = curr;
    curr = curr.next;
    // 每次循环将m减1，控制移动次数
    left--;
    // 移动指针的同时，需要减少n的数量，完成移动后剩下的n次，即为反转链表的次数
    right--;
  }
  const prevListTail = prev; // prev即为链表反转后，前半段的尾指针
  const reversedListTail = curr; // curr即为链表反转后，反转部分的尾指针
  // 将链表反转n次
  while (right > 0) {
    // 反转链表节点的通用方法
    const next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
    // 每次循环将n减1，控制移动次数
    right--;
  }
  // 如果prevListTail不为空，即为链表中间的一段进行了反转，需要将前半段与反转后的链表头指针连接起来
  if (prevListTail) {
    // 链表反转后，prev的位置即为反转部分的头指针
    prevListTail.next = prev;
  } else {
    // 链表未空，表示链表从头开始反转，反转后的prev即为新链表的头，因此需要重新设置链表的头指针
    head = prev;
  }
  // 链表反转后，反转部分原来的头，变成了尾部，而curr已加移出了链表，成为了最后一段链表的头指针
  // 因此需要将反转部分的尾指针与最后一段的头指针连接起来，组成新链表
  reversedListTail.next = curr;
  return head;
}
```

# K个一组翻转链表

```JS
/**
 * * K个一组翻转链表
 * * 思路：按k的长度，先计算尾指针节点，然后依次反转多段链表
 * 如果节点总数不是k的整数倍，那么请将最后剩余的节点保持原有顺序。
 * https://leetcode-cn.com/problems/reverse-nodes-in-k-group/
 * https://leetcode-cn.com/problems/reverse-nodes-in-k-group/solution/jsshi-xian-by-huinuo-3/
 */
function reverseKGroup(head, k) {
  if (!head || !head.next) return head;
  // 哨兵
  const root = new ListNode(0);
  root.next = head;
  let prev = root;
  while (head) {
    let tail = prev;
    // 计算要反转范围的尾指针
    for (let i = 0; i < k; i++) {
      tail = tail.next;
      if (!tail) return root.next;
    }
    // 下一个子链起点
    const next = tail.next;
    [head, tail] = reverseListK(head, tail);
    prev.next = head;
    tail.next = next;
    prev = tail;
    head = tail.next;
  }
  return root.next;
}
// 反转链表的变体
function reverseListK(head, tail) {
  let prev = tail.next;
  let curr = head;
  let next;
  // 循环终止条件是 prev === tail，到尾部了
  while (prev !== tail) {
    next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
  }
  return [tail, head];
}
```

# 获取链表的中间节点

```JS
/**
 * * 求链表的中间结点
 * https://leetcode-cn.com/problems/middle-of-the-linked-list/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/15
 */
/**
 * * 双指针法
 * 快指针走两步，慢指针走一步，快指针走完，慢指针则为中间值
 * - 如果链表长度为奇数，则返回中间节点
 * - 如果链表长度为偶数，则有两个中间节点，这里返回第一个
 */
function middleNode(head) {
  // if (!head || !head.next) return head;
  let fast = head;
  let slow = head;
  while (fast && fast.next) {
    fast = fast.next.next;
    slow = slow.next;
  }
  return slow;
}
// 链表元素放到数组
function middleNode2(head) {
  if (!head || !head.next) return head;
  const arr = [];
  while (head) {
    arr.push(head);
    head = head.next;
  }
  return arr[Math.ceil((arr.length - 1) / 2)];
}
```

# 合并两个有序链表

```JS
/**
 * * 合并两个有序链表。
 * * 思路：递归合并
 * 将两个升序链表合并为一个新的 升序 链表并返回。
 * https://leetcode-cn.com/problems/merge-two-sorted-lists/
 */
function mergeTwoLists(l1, l2) {
  if (!l1) return l2;
  if (!l2) return l1;
  if (l1.val <= l2.val) {
    l1.next = mergeTwoLists(l1.next, l2);
    return l1;
  } else {
    l2.next = mergeTwoLists(l2.next, l1);
    return l2;
  }
}
function mergeTwoLists2(l1, l2) {
  const preHead = new ListNode(-1);
  let cur = preHead;
  while (l1 && l2) {
    if (l1.val < l2.val) {
      cur.next = l1;
      l1 = l1.next;
    } else {
      cur.next = l2;
      l2 = l2.next;
    }
    cur = cur.next;
  }
  cur.next = l1 || l2;
  return preHead.next;
}
```

# 链表排序

```js
/**
 * * 链表排序
 * * 类似数组归并排序，先找链表中间节点，然后递归合并
 * https://leetcode-cn.com/problems/sort-list/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/79
 */
const sortList = function(head) {
  return mergeSortRec(head);
};
// 类似归并排序
// 若分裂后的两个链表长度不为1，则继续分裂，直到分裂后的链表长度都为 1，
// 然后合并小链表
function mergeSortRec(head) {
  if (!head || !head.next) return head;
  // 获取中间节点
  const middle = middleNode2(head);
  // 分裂成两个链表
  const temp = middle.next;
  middle.next = null;
  let left = head;
  let right = temp;
  // 继续分裂（递归分裂）
  left = mergeSortRec(left);
  right = mergeSortRec(right);
  // 合并两个有序链表
  return mergeTwoLists(left, right);
}
// ⚠️️ 与上面获取中间节点的方法不同
function middleNode2(head) {
  // if (!head || !head.next) return head;
  let fast = head;
  let slow = head;
  // 可以走到倒数第一个节点
  while (fast && fast.next && fast.next.next) {
    fast = fast.next.next;
    slow = slow.next;
  }
  return slow;
}
```

# 合并K个升序链表

```JS
/**
 * * 合并K个升序链表
 * * 思路: 两两合并。 采用分治法，简单来说就是不停的对半划分
 * 给你一个链表数组，每个链表都已经按升序排列。返回合并后的链表。
 * https://leetcode-cn.com/problems/merge-k-sorted-lists/
 * https://juejin.cn/post/6844903844971806727
 */
function mergeKLists(lists) {
  let len = lists.length;
  if (len === 0) return null;
  if (len === 1) return lists[0];
  while (len > 1) {
    const k = Math.floor((len + 1) / 2);
    for (let i = 0; i < Math.floor(len / 2); i++) {
      lists[i] = mergeTwoLists(lists[i], lists[i + k]);
    }
    len = k;
  }
  return lists[0];
}
```

# 判断一个单链表是否有环

```JS
/**
 * * 判断一个单链表是否有环。环形链表
 * 为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。
 * 如果 pos 是 -1，则在该链表中没有环。
 * https://leetcode-cn.com/problems/linked-list-cycle/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/13
 */
/**
 * * 双指针法。
 * 快指针一次走两步，慢指针一次走一步，
 * 如果单链表中存在环，则快慢指针终会指向同一个节点，否则直到快指针指向 null 时，快慢指针都不可能相遇
 */
function hasCycle(head) {
  if (!head || !head.next) return false;
  let fast = head.next.next;
  let slow = head.next;
  // 若相遇，则说明有环，会推出循环
  while (fast !== slow) {
    // fast已经走完了一圈，没发现有环
    if (!fast || !fast.next) return false;
    fast = fast.next.next;
    slow = slow.next;
  }
  return true;
}
// 标记法：给每个已遍历过的节点加标志位，遍历链表，当出现下一个节点已被标志时，则证明单链表有环
function hasCycle2(head) {
  while (head) {
    if (head.flag) return true;
    head.flag = true;
    head = head.next;
  }
  return false;
}
function hasCycleS3(head) {
  try {
    JSON.stringify(head);
    return false;
  } catch (err) {
    return true;
  }
}
```

# 环形链表 开始入环的第一个节点

```JS
/**
 * * 寻找环形链表相交的起点
 * https://leetcode-cn.com/problems/linked-list-cycle-ii/
 */
function detectCycle(head) {
  // 如果链表为空，或者链表只有一个元素且无环，此时指针无法行动，则返回null
  if (!head || !head.next) return null;
  // 创建快慢指针
  let slow = head;
  let fast = head;
  while (fast && fast.next) {
    // 慢指针走一步，快指针走两步
    slow = slow.next;
    fast = fast.next.next;
    // 如果两个指针的指向相同，则表示已经查找到环。
    // 但两个指针相遇的节点不一定是环的连接点，而是在环的某个位置
    if (slow === fast) {
      break;
    }
  }
  // 前面的退出循环条件有两个，一个是没有找到环，一个是找到了环
  // 通过快慢指针是否相同，判断是否找到环，如果没有，则返回null
  if (slow !== fast) return null;
  // 如果有环，而且快指针的速度是慢指针的两倍。
  // 因此如果创建两个指针，从链表起始点和快慢指针相遇节点分别出发。
  // 两者相遇的节点必然是环的连接点。
  let startNode = head;
  let meetNode = fast;
  // 遍历链表，查找连接点，如果两个指针相等，则表示找到连接点。
  while (startNode !== meetNode) {
    startNode = startNode.next;
    meetNode = meetNode.next;
  }
  return meetNode;
}
```

# 判断一个链表是否为回文链表

```JS
/**
 * * 判断该链表是否为回文链表
 * https://leetcode-cn.com/problems/palindrome-linked-list/
 * https://leetcode-cn.com/problems/palindrome-linked-list-lcci/solution/js-jie-fa-by-cranky-roentgen-3/
 */
/**
 * * 比较回文字符串
 */
function isPalindrome(head) {
  let str1 = '';
  let str2 = '';
  while (head) {
    str1 = str1 + head.val;
    str2 = head.val + str2;
    head = head.next;
  }
  return str1 === str2;
}
/**
 * * 思路1：先反转链表，再判断是否相同
 * * 思路2:链表转数组，数组转字符串，比较回文字符串
 */
function isPalindrome(head) {
  /** 新链表的头节点 */
  let list2;
  let curr = head;
  let next;
  // 反转链表变体，原链表不变
  while (curr) {
    // 每次都创建一个新节点，然后将已有链表作为next，node就变为了头节点
    const node = new ListNode(curr.val);
    node.next = list2;
    list2 = node;
    curr = curr.next;
  }
  let curr1 = head;
  let curr2 = list2;
  while (curr1 && curr2) {
    if (curr1.val !== curr2.val) return false;
    curr1 = curr1.next;
    curr2 = curr2.next;
  }
  // 两个都遍历完了
  if (!curr1 && !curr2) return true;
  // 两个中有1个没遍历完
  return false;
}
```

# 删除链表倒数第 n 个结点。

```JS
/**
 * * 删除链表倒数第 n 个结点。
 * 要求在删除了指定节点后，需要返回的是链表的头结点。所以返回的是head。
 * * 双指针法
 * 快指针先走n个节点，然后快慢指针一起，知道快指针走到null,这时慢指针指向n-1
 * https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/16
 */
function removeNthFromEnd(head, n) {
  let fast = head;
  let slow = head;
  while (--n) {
    fast = fast.next;
  }
  // 若快指针走到最后一个节点了，说明倒数第n个就是头结点
  if (!fast.next) {
    // 删除头结点
    return head.next;
  }
  fast = fast.next;
  // 快指针走到最后一个非空节点
  while (fast && fast.next) {
    fast = fast.next;
    slow = slow.next;
  }
  slow.next = slow.next.next;
  return head;
}
```

# 链表中倒数第k个节点

```JS
/**
 * * 链表中倒数第k个节点
 * * 思路： 快慢双指针，让第一个先走k步，然后两个指针一起移动，
 * * 当第一个指针到最后一个节点处，第二个指针就在倒数第K个节点
 */
function getKthFromEnd(head, k) {
  let fast = head;
  let slow = head;
  while (k !== 0) {
    fast = fast.next;
    k--;
  }
  while (fast !== null) {
    fast = fast.next;
    slow = slow.next;
  }
  return slow;
}
```

# 相交链表

```JS
/**
 * * 找到两个单链表相交的起始节点。注意相交节点之后的节点序列共享。
 * * 思路1，标记法，或者用新数组存放已访问过的节点。先访问并标记完一条，然后检查另一条。
 * https://leetcode-cn.com/problems/intersection-of-two-linked-lists/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/17
 * 思路2，链表转数组。
 */
function getIntersectionNode(headA, headB) {
  while (headA) {
    headA.visited = true;
    headA = headA.next;
  }
  while (headB) {
    if (headB.visited) return headB;
    headB = headB.next;
  }
  return null;
}
```

```JS
// 不能过值相等而判断相交节点，因为存在两条链表都相同的情况
// 可直接比较引用
function getIntersectionNode2(headA, headB) {
  if (!headA || !headB) return null;
  const arr1 = listToArray(headA);
  const arr2 = listToArray(headB);
  let retNode = null;
  retNode = arr1.find((node) => arr2.includes(node));
  return retNode;
}
/** 
 * * 链表转数组 
 */
function listToArray(head, isValOnly) {
  const arr = [];
  while (head) {
    if (isValOnly) {
      arr.push(head.val);
    } else {
      arr.push(head);
    }
    head = head.next;
  }
  return arr;
}
```

# 重排链表

```JS

```
