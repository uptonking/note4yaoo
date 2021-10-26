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
- 反转从位置 left 到位置 right 的链表节点，返回反转后的链表 

```JS
/**
 * * 反转链表 II；反转从位置 left 到位置 right 的链表节点
 * https://leetcode-cn.com/problems/reverse-linked-list-ii/
 * https://xie.infoq.cn/article/f5db6e4a84aef1339e4582d40
 */
function reverseBetween(head, left, right) {
  let prev = null;
  let curr = head;

  // 将curr移动到left位置，即找到待反转部分的头结点
  while (left > 1) {
    prev = curr;
    curr = curr.next;
    left--;
    right--;
  }

  const prevListTail = prev; // prev即为链表反转后，前半段的尾指针
  const reversedListTail = curr; // curr即为链表反转后，反转部分的尾指针

  // 将链表反转left-right次；注意前面right已经减过了，right这里开始时就是要反转的节点数量
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
    prevListTail.next = prev;
  } else {
    // 链表未空，表示链表从头开始反转，反转后的prev即为新链表的头，因此需要重新设置链表的头指针
    head = prev;
  }

  // 链表反转后，反转部分原来的头，变成了尾部，而curr已经移出了链表，成为了最后一段链表的头指针
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

# 环形链表：判断一个单链表是否有环

```JS
/**
 * * 判断一个单链表是否有环。
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

  // 若相遇，则说明有环，会退出循环
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

# 环形链表 开环形链表相交的起点

```JS
/**
 * * 寻找环形链表相交的起点
 * * 思路：公式推导 从头节点到入环点的距离D  = (慢指针)从首次相遇点到入环点的距离S2
 * D+n(S1+S2)+S1=2(D+S1)  -->  (n−1)S1+nS2=D  -->  D=S2
 * https://leetcode-cn.com/problems/linked-list-cycle-ii/
 * https://leetcode-cn.com/problems/linked-list-cycle-ii/solution/141ti-de-kuo-zhan-ru-guo-lian-biao-you-huan-ru-he-/
 */
function detectCycle(head) {
  // 如果链表为空，或者链表只有一个元素且无环，则返回null
  if (!head || !head.next) return null;

  let slow = head;
  let fast = head;
  while (fast) {
    if (fast.next == null) { // fast.next走出链表了，说明无环
      return null;
    }
    slow = slow.next; // 慢指针走一步
    fast = fast.next.next; // 慢指针走一步
    if (slow == fast) { // 首次相遇
      fast = head; // 让快指针回到头节点
      while (true) { // 开启循环，让快慢指针相遇
        if (slow == fast) { // 相遇，在入环处
          return slow;
        }
        slow = slow.next;
        fast = fast.next; // 快慢指针都走一步
      }
    }
  }
  return null;
};
```

# 判断一个链表是否为回文链表

```JS
/**
 * * 判断该链表是否为回文链表
 * https://leetcode-cn.com/problems/palindrome-linked-list/
 * https://leetcode-cn.com/problems/palindrome-linked-list-lcci/solution/js-jie-fa-by-cranky-roentgen-3/
 */
/**
 * * 思路1: 比较 正序构造字符串 和 倒序构造的字符串是否相等
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
 * * 思路2:链表转数组，数组转字符串，比较字符串
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

# 链表中倒数第k个节点

```JS
/**
 * * 链表中倒数第k个节点
 * * 思路： 快慢双指针，让快指针先走k步，然后两个指针一起移动，
 * * 当快指针到最后一个节点处，慢指针指针就在倒数第K个节点
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

# 删除链表倒数第n个结点

```JS
/**
 * * 删除链表倒数第n个结点。
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
  // 👀️ 在单链表中删除节点
  slow.next = slow.next.next;
  return head;
}
```

# 相交链表

```JS
/**
 * * 找到两个单链表相交的起始节点。注意相交节点之后的节点序列共享。
 * * 思路1，标记法。先访问并标记完一条，然后检查另一条。
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
