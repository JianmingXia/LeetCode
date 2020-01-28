# 买卖股票的最佳时机

## 题目描述
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。

### 示例
```
示例 1:

输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。

示例 2:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

## 思路分析
先找到当前的最低价格，然后依次遍历：
- 如果价格比当前低，后续遍历拿此价格作为进价
- 如果价格比当前高，可以考虑此次售出，计算出利润与之前的所得利润比较，得出更大值

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

```
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
  let max = 0;
  let minIndex = 0;
  for(let i = 1; i < prices.length; i++) {
    if(prices[i] < prices[minIndex]) {
      minIndex = i;
    } else if(prices[i] - prices[minIndex] > max) {
      max = prices[i] - prices[minIndex];
    }
  }

  return max;
};
```