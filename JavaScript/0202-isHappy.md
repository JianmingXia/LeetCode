# 快乐数

## 题目描述
编写一个算法来判断一个数是不是“快乐数”。

一个“快乐数”定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是无限循环但始终变不到 1。如果可以变为 1，那么这个数就是快乐数。

### 示例
```
示例: 

输入: 19
输出: true
解释: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

## 思路分析
> 反正快乐就完事了= =!
其实思路很简单：
- 如果平方和返回 1，则是快乐数
- 如果平方和不为 1，判断该数之前是否出现过：
  - 如果未出现，继续迭代
  - 如果出现过，那表示已出现相同情况（平方和作为一个纯函数，后续的返回会保持一致），则不是快乐数

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
const getSumOfSquare = (num) => {
  let res = 0;

  while(num) {
    res += Math.pow(num % 10, 2);

    num = parseInt(num / 10);
  }

  return res;
}

/**
 * @param {number} n
 * @return {boolean}
 */
var isHappy = function(n) {
  const repeatNums = [n];

  while(true) {
    const sumOfSquare = getSumOfSquare(repeatNums[repeatNums.length - 1]);

    if(sumOfSquare === 1) {
      return true;
    } else if(repeatNums.indexOf(sumOfSquare) >= 0) {
      return false;
    } else {
      repeatNums.push(sumOfSquare);
    }
  }
};
```