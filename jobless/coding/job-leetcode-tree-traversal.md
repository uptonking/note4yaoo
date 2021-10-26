---
title: job-leetcode-tree-traversal
tags: [coding, job, leetcode, traversal, tree]
created: '2021-10-05T10:07:02.318Z'
modified: '2021-10-06T14:54:33.247Z'
---

# job-leetcode-tree-traversal

# guide

- 二叉树遍历小结
  - 二叉树的前中后序深度优先遍历都基于stack，访问元素都使用 `stack.pop()`，只有后序遍历将访问结果`unshift`插入结果数组的第一个
  - 二叉树的层序遍历基于queue，访问元素使用 `queue.shift()`

```JS
// 二叉树的节点定义
function TreeNode(val, left, right) {
  this.val = val === undefined ? 0 : val;
  this.left = left === undefined ? null : left;
  this.right = right === undefined ? null : right;
}
```

```JS
// 二叉树遍历模版
function orderTraversal(root) {
  if (!root) return [];

  const ret = [];

  return ret;
}
// 用于基于循环实现的深度优先遍历
// const stack = [];
// let curr = root;
```

# 根据前序遍历和中序遍历生成二叉树

```JS
/**
 * * 根据前序遍历和中序遍历生成二叉树。
 * * 思路：根据pre-o确定根节点，在in-o遍历中找到该节点，然后递归左右子树。
 * 假设树中没有重复的元素。
 * https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/
 */
export function buildTree(preorder, inorder) {
  if (preorder.length !== inorder.length || inorder.length === 0) {
    // * 这里返回的是null，会作为空的left/right，不可以返回[]
    return null;
  }

  // root和i代表的是同一个节点，当前根节点对象和索引
  const root = new TreeNode(preorder[0]);
  const i = inorder.indexOf(preorder[0]);

  // 递归处理子数组时要去掉i节点，左子树
  root.left = buildTree(preorder.slice(1, i + 1), inorder.slice(0, i));

  // * 根左右、左根右；右这部分的索引是相同的
  root.right = buildTree(preorder.slice(i + 1), inorder.slice(i + 1));

  return root;
}
```

# 根据后序遍历和中序遍历生成二叉树

```JS
/**
 * * 根据后序遍历和中序遍历生成二叉树。
 * * 注意参数顺序。
 * https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
 */
export function buildTree(inorder, postorder) {
  if (postorder.length !== inorder.length || inorder.length === 0) {
    return null;
  }

  const root = new TreeNode(postorder[postorder.length - 1]);
  const i = inorder.indexOf(postorder[postorder.length - 1]);

  // * 左根右、左右根；左这部分的索引是相同的
  root.left = buildTree(inorder.slice(0, i), postorder.slice(0, i));

  root.right = buildTree(inorder.slice(i + 1), postorder.slice(i, -1));

  return root;
}
```

# 前序遍历

```JS
function preorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  function preTree(node) {
    if (node) {
      ret.push(node.val);

      pretree(node.left);
      pretree(node.right);
    }
  }

  preTree(root);

  return ret;
}
```

```JS
function preorderTraversal(root) {
  if (!root) return [];
  const ret = [];
  const stack = [root];
  let curr = root;

  while (stack.length) {
    curr = stack.pop();
    ret.push(curr.val);

    curr.right && stack.push(curr.right);
    curr.left && stack.push(curr.left);
  }

  return ret;
}
```

- ref
  - https://leetcode-cn.com/problems/binary-tree-preorder-traversal/
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/37
# 中序遍历

```JS
function inorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  function inTree(node) {
    if (node) {
      inTree(node.left);

      ret.push(node.val);

      inTree(node.right);
    }
  }

  inTree(root);

  return ret;
}
```

```JS
function inorderTraversal(root) {
  if (!root) return [];

  const ret = [];

  const stack = [];
  let curr = root;

  while (stack.length || curr) {
    while (curr) {
      stack.push(curr);
      curr = curr.left;
    }

    curr = stack.pop();
    ret.push(curr.val);

    curr = curr.right;
  }

  return ret;
}
```

- ref
  - https://leetcode-cn.com/problems/binary-tree-inorder-traversal/
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/38
# 后序遍历

```JS
function postorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  function postTree(node) {
    if (node) {
      postTree(node.left);
      postTree(node.right);

      ret.push(node.val)
    }
  }

  postTree(root);

  return ret;
}
```

```JS
function postorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  const stack = [root];
  let curr = root;

  while (stack.length) {

    curr = stack.pop();

    ret.unshift(curr.val);

    curr.left && stack.push(curr.left);
    curr.right && stack.push(curr.right);
  }

  return ret;
}
```

- ref
  - https://leetcode-cn.com/problems/binary-tree-postorder-traversal/
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/40
# 层序遍历

```JS
/**
 * * 基于队列实现，返回一维数组
 */
function levelorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  const queue = [root];
  let curr = root;

  while (queue.length) {
    curr = queue.shift();

    ret.push(curr.val);

    curr.left && queue.push(curr.left);
    curr.right && queue.push(curr.right);
  }

  return ret;
}
```

```JS
/**
 * * 递归实现，返回每层的节点值，返回的是二维数组
 */
function levelorderTraversal(root) {
  if (!root) return [];
  const ret = [];

  function levelTree(node, depth) {
    if (node) {
      ret[depth] = ret[depth] || [];
      ret[depth].push(node.val);

      // ! 注意这里不能是++depth
      // levelTree(node.left, ++depth);
      levelTree(node.left, depth + 1);
      levelTree(node.right, depth + 1);
    }
  }

  levelTree(root, 0);

  return ret;
}
```

```JS
/**
 * *  基于队列实现，返回每层的节点值，返回的是二维数组
 */
function getNodesByLevelOrder(root) {
  if (!root) return [];
  const ret = [];

  const queue = [root];
  let curr = root;

  while (queue.length) {
    const levelVals = [];
    const levelSize = queue.length;

    // 每次处理完上一层的元素，然后就加入了下一层的元素
    for (let i = 0; i < levelSize; i++) {
      curr = queue.shift();
      levelVals.push(curr.val);

      curr.left && queue.push(curr.left);
      curr.right && queue.push(curr.right);
    }

    ret.push(levelVals);
    // ret.unshift(level);
  }

  return ret;
}
```

- ref
  - https://leetcode-cn.com/problems/binary-tree-level-order-traversal/
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/47
  - https://github.com/sisterAn/JavaScript-Algorithms/issues/46
# 二叉树的锯齿形层序遍历

```JS
/**
 * * 二叉树的锯齿形层序遍历，
 * * 思路：与基于循环或递归相同，奇数索引的元素是倒序的，要在上一个偶数层unshift
 * https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/
 */
function zigzagLevelOrder(root) {
  if (!root || root.length === 0) return [];

  const ret = [];

  const level = (node, depth) => {
    if (!node) return;

    ret[depth] = ret[depth] || [];

    // 当前层值的访问顺序，第depth层，偶数层正序，奇数层倒序
    depth % 2 === 0 ? ret[depth].push(node.val) : ret[depth].unshift(node.val);

    level(node.left, depth + 1);
    level(node.right, depth + 1);
  };

  level(root, 0);

  return ret;
}

function zigzagLevelOrder2(root) {
  if (!root || root.length === 0) return [];

  const ret = [];

  const queue = [root];
  let curr = root;

  let depth = -1;

  while (queue.length) {
    const levelArr = [];
    const levelSize = queue.length;

    depth++;

    for (let i = 0; i < levelSize; i++) {
      curr = queue.shift();

      depth % 2 === 0 ? levelArr.push(curr.val) : levelArr.unshift(curr.val);

      curr.left && queue.push(curr.left);
      curr.right && queue.push(curr.right);
    }

    ret.push(levelArr);
  }

  return ret;
}
```

# 二叉树的右视图

```JS
/**
 * * 二叉树的右视图
 * * 思路：层序遍历，每层只取最右边1个
 * 想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。
 * https://leetcode-cn.com/problems/binary-tree-right-side-view/
 * https://github.com/Chocolate1999/leetcode-javascript/issues/51
 */
function rightSideView(root) {
  if (!root) return [];

  const ret = [];
  const queue = [root];
  let curr = root;

  while (queue.length) {
    const levelArr = [];
    const levelSize = queue.length;

    for (let i = 0; i < levelSize; i++) {
      curr = queue.shift();
      if (i === levelSize - 1) {
        ret.push(curr.val);
      }

      curr.left && queue.push(curr.left);
      curr.right && queue.push(curr.right);
    }
  }

  return ret;
}

function rightSideView(root) {
  if (!root) return [];

  const ret = [];

  const level = (node, depth) => {
    if (!node) return;

    // 每层只保存最右边的元素
    if (ret.length === depth) ret.push(node.val);

    // 因为每层保存一个，所以先递归处理右子树
    level(node.right, depth + 1);
    level(node.left, depth + 1);
  };

  level(root, 0);

  return ret;
}
```
