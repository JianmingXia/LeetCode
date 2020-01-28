# 最小栈

## 题目描述
设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) -- 将元素 x 推入栈中。
pop() -- 删除栈顶的元素。
top() -- 获取栈顶元素。
getMin() -- 检索栈中的最小元素。

### 示例
```
示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```

## 思路分析
这里其实只需要实现一个小型的栈即可，但是题目中有个要求需要注意：常数时间内检索到最小元素的栈。
所以这里我增加了一个栈，用于辅助记录最小元素。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * initialize your data structure here.
 */
var MinStack = function() {
  this.len = 0;
  this.sourceNums = [];
  this.minNums = [];
};

/** 
 * @param {number} x
 * @return {void}
 */
MinStack.prototype.push = function(x) {
  this.sourceNums.push(x);
  if(this.len === 0) {
    this.minNums.push(x);
  } else {
    this.minNums.push(this.minNums[this.len - 1] > x ? x : this.minNums[this.len - 1]);
  }

  this.len++;
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function() {
  this.len--;
  
  this.sourceNums.length = this.len; 
  this.minNums.length = this.len; 
};

/**
 * @return {number}
 */
MinStack.prototype.top = function() {
  return this.sourceNums[this.len - 1];
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function() {
  return this.minNums[this.len - 1];
};
```