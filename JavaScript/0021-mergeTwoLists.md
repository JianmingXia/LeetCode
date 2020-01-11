# 合并两个有序链表

## 题目描述
将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

### 示例
```
示例：
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

## 思路分析
这题的思路其实也很简单：
直接判断是否链表为空：
- 有：返回另一个链表
- 无：进行合并
  - 依次比较进行合并，直到某一个链表为空。这里注意一下初始化链表就行。
  - 将另一个不为空的链表直接链到之前合并的尾部

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

function newNode(val) {
  return {
    val,
    next: null
  }
}

function pushRes(latestNode, node) {
  if (typeof latestNode.val === "undefined") {
    latestNode.val = node.val;

    return latestNode;
  } else {
    latestNode.next = node;

    return node;
  }
}

/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {
  if (!l1) {
    return l2;
  }
  if (!l2) {
    return l1;
  }

  let res = newNode();
  let current;
  let latestNode = res;
  while (l1 && l2) {
    if (l1.val < l2.val) {
      current = newNode(l1.val)
      latestNode = pushRes(latestNode, current);
      l1 = l1.next;
    } else {
      current = newNode(l2.val)
      latestNode = pushRes(latestNode, current);
      l2 = l2.next;
    }
  }

  latestNode.next = l1 ? l1 : l2;

  return res;
};
```