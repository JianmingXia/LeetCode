# 删除链表的倒数第N个节点

## 题目描述
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

### 示例
```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5
```

### 说明
给定的 n 保证是有效的。

### 进阶
你能尝试使用一趟扫描实现吗？

## 思路分析
简单的实现方式是：
- 第一次遍历，获取链表长度
- 第二次遍历，移除第 len - n + 1 节点即可

题目中有个进阶要求：尝试使用一次扫描。这里有个思路：
- 第一个节点先向前走 n + 1次
- 第二个节点准备向前走
- 一、二节点一起走，直至第一个节点到末尾
- 二节点执行移除操作

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
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function(head, n) {
  let helpNode = {
    next: head
  };

  let firstNode = helpNode;
  for(let i = 0; i <= n; i++) {
    firstNode = firstNode.next;
  }
  
  let secondNode = helpNode;
  while(firstNode) {
    firstNode = firstNode.next;
    secondNode = secondNode.next;
  }

  secondNode.next = secondNode.next.next;

  return helpNode.next;
};
```