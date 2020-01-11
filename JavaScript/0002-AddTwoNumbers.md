# Add Two Numbers（2.两数相加）

## 题目描述
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

### Example:
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## 思路分析
直接看输入及输出即可了解本题的意义，两个数组从左开始做求和运算，如果求和>10，需要向前进一位。需要考虑的有两点：
- 当两个链表的长度不同时，记得后续的求和忽略短的链表
- 最后一位的进位记得补上

## 代码
- 时间复杂度O(m + n)
- 空间复杂度O(m + n + 1) 最大

```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    const result = [];

    let last_add = 0;
    while(l1 && l2) {
        let num1 = l1.val;
        let num2 = l2.val;
        
        let sum = last_add + num1 + num2;
        last_add = Math.floor(sum / 10);
        result.push(sum % 10);
        
        l1 = l1.next;
        l2 = l2.next;
    }
    
    let l = l1 ? l1 : l2;
    while(l) {
        let sum = last_add + l.val;
        last_add = Math.floor(sum / 10);
        result.push(sum % 10);
        
        l = l.next;
    }
    if(last_add) {
        result.push(1);
    }
    
    return result;
};
```