# 对称二叉树

## 题目描述
给定一个二叉树，检查它是否是镜像对称的。

### 示例
```
例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3
```

### 说明
如果你可以运用递归和迭代两种方法解决这个问题，会很加分。

## 思路分析
### 思路1
这个与上一题有点像，上题使用了中序遍历，这题应用前序和后序遍历，刚刚可以解决这个问题。

### 思路2
采用递归的方式，判断左树与右树是否是对称，一直递归下去。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

### 思路1
```
const preOrderTraversal = (tree, res) => {
  if(tree) {
    if(tree.left || tree.right) {
      res.push(tree.val);
      preOrderTraversal(tree.left, res);
      preOrderTraversal(tree.right, res);
    } else {
      res.push(tree.val);
    }
  } else {
    res.push(null);
  }
}

const postOrderTraversal = (tree, res) => {
  if(tree) {
    if(tree.left || tree.right) {
      postOrderTraversal(tree.left, res);
      postOrderTraversal(tree.right, res);
      res.push(tree.val);
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
 * @param {TreeNode} root
 * @return {boolean}
 */
var isSymmetric = function(root) {
  const arr1 = [];
  preOrderTraversal(root, arr1);

  const arr2 = [];
  postOrderTraversal(root, arr2);

  arr1.reverse();
  
  return JSON.stringify(arr1) === JSON.stringify(arr2);
};
```

### 思路2

```
const isMirror = (tree1, tree2) => {
  if(!tree1 && !tree2) {
    return true;
  } else if (tree1 && tree2) {
    return tree1.val === tree2.val && isMirror(tree1.left, tree2.right) && isMirror(tree1.right, tree2.left);
  } else {
    return false;
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
 * @param {TreeNode} root
 * @return {boolean}
 */
var isSymmetric = function(root) {
  if(!root) {
    return true;
  }
  
  return isMirror(root.left, root.right);
};
```