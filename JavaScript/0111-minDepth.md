# 二叉树的最小深度

## 题目描述
给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

说明: 叶子节点是指没有子节点的节点。

### 示例
```
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回它的最小深度  2.
```

## 思路分析
这里和之前的最大深度有点类似，不过刚开始我也犯了错，直接用之前最大深度的思想调整了一下解决，提交之后发生了错误，[1, 2] 深度为 2，但是我的结果是 1。
重新审视了题目，题目中有个说明：最近叶子节点。重新调整了代码：
- 左右子树的深度都有：取浅一点
- 左右子树只有一个有深度，则取有深度的
- 如果都没深度，取 0 即可

这里 2 3 做了一个小优化

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var minDepth = function(root) {
  if(!root) {
    return 0;
  }

  const leftDepth = minDepth(root.left);
  const rightDepth = minDepth(root.right);

  // 左右子树都有深度，则取较短的
  // 否则取有深度的那个，此时当前节点不算叶子节点
  if(leftDepth && rightDepth) {
    return  1 + Math.min(leftDepth, rightDepth);
  } else {
    return  1 + leftDepth + rightDepth;
  }
};
```