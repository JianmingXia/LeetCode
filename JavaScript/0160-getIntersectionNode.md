# 相交链表

## 题目描述
编写一个程序，找到两个单链表相交的起始节点。

### 示例
```
示例 1：
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
 
示例 2：
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
 

示例 3：
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。
```

### 说明
- 如果两个链表没有交点，返回 null.
- 在返回结果后，两个链表仍须保持原有的结构。
- 可假定整个链表结构中没有循环。
- 程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。

## 思路分析
看到这题，第一想法是：如果是个双向链表就好了，直接遍历到两个链表的尾部，比较是否相等：
- 相等：记录当前节点，并同时向前遍历
- 不相等：返回记录的节点或空节点

不过前提是个单向链表，这个操作就不行了。不过有个前提，链表是没有环的，所以这里还有个方法来做。我们知道，如果两个节点是有公共节点的，那么链表的后几个元素应该是相等的。
这里我们假设单向链表的长度分别为 M 及 N，而公共链表长度为 C：
- 如果 C > 0，那么他们会在 M + N - C 处以及 N + M - C 处相遇
- 如果 C = 0，会在 M + N 处停止
上面其实就是解题思想，先同时遍历两个链表，如果一个链表遍历结束了，切换到另一个链表。

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
 * @param {ListNode} headA
 * @param {ListNode} headB
 * @return {ListNode}
 */
var getIntersectionNode = function(headA, headB) {
  let node1 = headA;
  let node2 = headB;

  while(node1 != node2) {
    node1 = node1 ? node1.next : headB;
    node2 = node2 ? node2.next : headA;
  }

  return node1;
};
```