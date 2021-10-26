---
title: job-leetcode-linked-list-sort
tags: [leetcode, linked-list, repeat]
created: '2021-10-08T19:42:43.443Z'
modified: '2021-10-08T19:49:54.670Z'
---

# job-leetcode-linked-list-sort

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
```

```JS
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

# 合并K个升序链表

```JS
/**
 * * 合并K个升序链表
 * * 思路: 归并的思想，先拆分到只有1个或2个链表，再两两合并。
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

# 排序链表

```js
/**
 * * 链表排序
 * * 类似数组归并排序，先找链表中间节点，然后拆分链表为左右，最后递归合并相邻2个有序链表
 * https://leetcode-cn.com/problems/sort-list/
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/79
 * 给你链表的头结点 head ，请将其按 升序 排列并返回排序后的链表 。
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

# 删除排序链表中的重复元素

```JS
/**
 * * 删除排序链表中的重复元素，最终链表可包含重复元素中的一个
 * https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/
 * 给你这个链表的头节点 head ，请你删除所有重复的元素，使每个元素 只出现一次 。
 */
function deleteDuplicates(head) {
  if (!head || !head.next) return head;

  head.next = deleteDuplicates(head.next);

  if (head.val === head.next.val) head.next = head.next.next;

  return head;
}

function deleteDuplicates(head) {
  if (!head || !head.next) return head;

  let curr = head;

  while (curr && curr.next) {
    if (curr.val === curr.next.val) {
      curr.next = curr.next.next;
    } else {
      curr = curr.next;
    }
  }

  return head;
}
```

```JS
/**
 * * 删除排序链表中的重复元素，且最终链表不包含该元素
 * * 思路主要思路还是双指针，
 * - prev指针上一个元素，head指针遍历每个元素，当prev和head指向的元素值不同时，两者同时向后移动，
 * - 当prev和head指向的元素值相同时，此时说明出现重复元素，那么prev指针不动，head指针继续向后搜索直到找到不同的元素，
 * - 然后修改指针指向，将重复元素段移除。
 * https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/comments/
 */
function deleteDuplicates(head) {
  if (!head || !head.next) return head;

  let linkHead = head;
  let prev = head;
  head.prev = null;
  let flag = false;

  while (head.next) {
    head.next.prev = head;
    head = head.next;

    if (head.val === prev.val) {
      if (!flag) {
        flag = true; // 打开开关，开始寻找下一个值不同的元素
      }
    } else {
      if (flag) {
        // 找到不同值的元素，修改指针
        if (!prev.prev) {
          // 如果重复的是列表头元素
          linkHead = head;
          head.prev = null;
        } else {
          // 如果重复的元素位于列表中间
          prev.prev.next = head;
          head.prev = prev.prev;
        }
        flag = false; // 关闭开关，继续寻找相同的元素
      }
      prev = head;
    }
  }

  if (flag) {
    // 如果重复元素段在链表尾部
    if (!prev.prev) {
      linkHead = null;
    } else {
      prev.prev.next = null;
    }
  }

  return linkHead;
}
```

# 重排链表

```JS
/**
 * * 重排链表
 * https://leetcode-cn.com/problems/reorder-list/
 * https://juejin.cn/post/7002949115776598023
 */
function reorderList(head) {
  const list = []; // 使用数组存储链表
  let node = head; // 使用node遍历链表

  // 遍历链表，将每个元素依次存入数组
  while (node) {
    list.push(node);
    node = node.next;
  }

  const newList = []; // 使用新数组，存储新排序的链表节点
  let i = 0; // 使用i指针从头往后遍历list
  let j = list.length - 1; // 使用j指针从后往前遍历list

  // 左右指针不断向中间移动，知道相遇
  while (i <= j) {
    // 将i、j指向的元素，依次存入newList
    newList.push(list[i++], list[j--]);
  }

  let newNode = newList[0]; // 缓存新链表的头节点

  // newList的每个元素，就是新链表的每个节点
  for (let i = 1; i < newList.length; i++) {
    // 将每个节点连接到链表
    newNode.next = newList[i];
    // 将新链表节点向后移动一位，待连接下一个节点
    newNode = newNode.next;
  }
  // 将尾节点的next置为null，避免链表出现环
  newNode.next = null;

  // head也是新链表的头结点
  return head;
}
```

# 两数相加

```JS
/**
 * * 两数相加。
 * 给定两个用链表表示的整数，每个节点包含一个数位。
 * 这些数位是反向存放的。并用链表形式返回结果。
 * https://github.com/sisterAn/JavaScript-Algorithms/issues/114
 */
function addTwoNumbers(l1, l2) {
  // 用carry存储每次的进位
  let carry = 0;
  // 作为占位的空节点，最后会丢掉
  const root = new ListNode(0);

  let curr = root;

  while (l1 || l2) {
    let sum = 0;
    if (l1) {
      sum += l1.val;
      l1 = l1.next;
    }

    if (l2) {
      sum += l2.val;
      l2 = l2.next;
    }

    sum += carry;
    carry = Math.floor(sum / 10);

    curr.next = new ListNode(sum % 10);
    curr = curr.next;
  }

  if (carry === 1) {
    curr.next = new ListNode(carry);
    curr = curr.next;
  }

  return root.next;
}
```
