# 反转链表

## 题目描述
反转一个单链表。

### 示例
```
示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

### 说明
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

## 思路分析
### 思路 1
因为当前节点反转后，会指向上个节点，所以这个用了两个辅助节点：原链表的上个节点、原链表的下个节点。通过两个辅助节点，迭代完成反转。

### 思路 2
采用递归的方式有点绕：比如节点是 1 2 3 4 5 null
- 前面一直递归，直到结点 4 时开始进行反转：5 4 null
- 然后回到 节点 3（此时节点 3 的 next 也是 4）：5 4 3 null
- 依次到节点 2、1，从而完成反转

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

### 思路1
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
var reverseList = function(head) {
  let lastNode = null;
  while(head) {
    // 暂存下个节点
    let next = head.next;

    // 反转当前节点
    head.next = lastNode;
    lastNode = head;
    head = next;
  }

  return lastNode;
};
```

### 思路2
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
var reverseList = function(head) {
  if(!head || !head.next) {
    return head;
  }

  let newHead = reverseList(head.next);

  head.next.next = head;
  head.next = null;

  return newHead;
};
```
