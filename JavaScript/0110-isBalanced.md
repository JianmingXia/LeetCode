# 平衡二叉树

## 题目描述
给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

### 示例
```
示例 1:

给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
返回 true 。

示例 2:

给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。
```

## 思路分析
### 思路1
这里用到了之前做的题——二叉树的最大深度，判断当前节点是否是平衡二叉树：
- 如果不是，则不是平衡二叉树
- 如果是，则判断左子树 与 右子树是否是平衡二叉树
这里需要注意一下，从根节点依次往下判断，重复获取深度，这里有点浪费

### 思路2
上面也说过，思路1从顶向下遍历过程中，存在重复获取树的高度情况，所以现在改变思路，从底向上判断，并且复用之前得到的子树深度。当然这里也进行了优化，如果节点已判断为非平衡二叉树，提前止损，后续遍历早点结束。

NOTE：代码中最开始我补了一个初始化：res.flag = true，在最初提交的时候，有一个用例测试不通过，后面百思不得其解，因为在本地测试是 OK 的。后面想到可能是测试用例执行的时候被污染了，尝试添加了初始化部分，果然已通过。

## 代码
- 时间复杂度O(n²)
- 空间复杂度O(n)

### 思路1
```
const maxDepth = (root) => {
  if(!root) {
    return 0;
  }

  const leftDepth = maxDepth(root.left);
  const rightDepth = maxDepth(root.right);

  return 1 + (leftDepth > rightDepth ? leftDepth : rightDepth);
};

/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isBalanced = function(root) {
  if(!root) {
    return true;
  }

  return Math.abs(maxDepth(root.left) - maxDepth(root.right)) < 2 && isBalanced(root.left) && isBalanced(root.right);
};
```

### 思路2
```
const depth = (root) => {
  if(!res.flag || !root) {
    return 0;
  }

  const leftDepth = depth(root.left) + 1;
  const rightDepth = depth(root.right) + 1;

  if(Math.abs(leftDepth - rightDepth) > 1) {
    res.flag = false;
  }

  return Math.max(leftDepth, rightDepth);
};

/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
const res = {flag: true};

var isBalanced = function(root) {
  res.flag = true;
  depth(root);

  return res.flag;
};
```