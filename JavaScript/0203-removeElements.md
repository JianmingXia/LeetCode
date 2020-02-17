# 移除链表元素

## 题目描述
删除链表中等于给定值 val 的所有节点。

### 示例
```
示例:

输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
```

## 思路分析
移除链表指定元素关键点是将符合条件的元素跳过，即：当前节点的上个节点 => 当前节点的下个节点。这里需要考虑一下边界值，当节点的第一个值符合条件需要跳过时，因为链表的设计原理，没有这样的节点，所以我们伪造了这样的节点。

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
 * @param {number} val
 * @return {ListNode}
 */
var removeElements = function(head, val) {
  let res = {next: head};
  
  let node = res;
  while(node.next) {
    if(node.next.val === val) {
      node.next = node.next.next;
    } else {
      node = node.next;
    }
  }

  return res.next;
};
```