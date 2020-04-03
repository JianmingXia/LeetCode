# 两两交换链表中的节点

## 题目描述
给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

### 示例
```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

## 思路分析
这里用了递归的方式来求解，下面的题解也很清楚了，这里不多数了

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var swapPairs = function(head) {
  // 无节点或只有单个节点
  if(!head || !head.next) {
    return head;
  }

  let firstNode = head;
  let secondNode = head.next;

  // 第一个节点会被转成第二个，是后续节点的父节点
  firstNode.next = swapPairs(secondNode.next);
  // 第二个节点会被转成第一个
  secondNode.next = firstNode;

  return secondNode;
};
```