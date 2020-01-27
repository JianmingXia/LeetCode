# 相同的树

## 题目描述
给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

### 示例
```
示例 1:

输入:       1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

输出: true

示例 2:

输入:      1          1
          /           \
         2             2

        [1,2],     [1,null,2]

输出: false

示例 3:

输入:       1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

输出: false
```

## 思路分析
根据示例，我的想法是直接中序遍历目标树，将树的节点内容存储到数组中。然后直接将数组转成字符串进行比较即可——性能有点超乎我的想象，超越了 94.61% 的用户。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
const inOrderTraversal = (tree, res) => {
  if(tree) {
    if(tree.left || tree.right) {
      res.push(tree.val);
      inOrderTraversal(tree.left, res);
      inOrderTraversal(tree.right, res);
    } else {
      res.push(tree.val);
    }
  } else {
    res.push(null);
  }
}

/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function(p, q) {
  const arr1 = [];
  inOrderTraversal(p, arr1);

  const arr2 = [];
  inOrderTraversal(q, arr2);

  return JSON.stringify(arr1) === JSON.stringify(arr2);
};
```