# 删除排序链表中的重复元素

## 题目描述
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

### 示例
```
示例 1:

输入: 1->1->2
输出: 1->2

示例 2:

输入: 1->1->2->3->3
输出: 1->2->3
```

## 思路分析
这题是应用之前的“指针”姿势来操作，有关键的两个指针，分别：
- head：这个是记录链表的头，到时需要返回的
- node：记录当前处理的位置

处理逻辑是这样的，判断 node 的值是否与 node->next 相等：
- 如果相等，则将 node->next = node->next->next
- 如果不相等，node = node->next，继续迭代

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

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
var deleteDuplicates = function(head) {
  if(!head) {
    return head;
  }

  let node = head;
  while(node.next) {
    if(node.val == node.next.val) {
      node.next = node.next.next;
    } else {
      node = node.next;
    }
  }

  return head;
};
```