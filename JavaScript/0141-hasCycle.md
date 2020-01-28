# 环形链表

## 题目描述
给定一个链表，判断链表中是否有环。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

### 示例
```
示例 1：
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。

示例 2：
输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。

示例 3：
输入：head = [1], pos = -1
输出：false
解释：链表中没有环。
```

## 思路分析
这一题本来是很简单的题，但是示例倒是给我弄迷糊了。
重新理解题目后，我们就明白了，使用快慢指针判断是否有环即可。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

```
const getFastPos = (root) => {
  if(root && root.next && root.next.next) {
    return root.next.next;
  } else {
    return null;
  }
}

/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function(head) {
  let slow = head;
  let fast = getFastPos(head);

  while(slow && fast) {
    if(slow === fast) {
      return true;
    } else {
      slow = slow.next;
      fast = getFastPos(fast);
    }
  }  

  return false;
};
```