# x 的平方根

## 题目描述
实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

### 示例
```
示例 1:

输入: 4
输出: 2

示例 2:

输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
```


## 思路分析
其实单纯的依次迭代也是可以实现的，但是这里用了一个巧方法——二分法，避免无效试错。

## 代码
- 时间复杂度O(log n)
- 空间复杂度O(1)

```
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function(x) {
  let low = 0;
  let high = x;
  let mid = Math.ceil((low + high) / 2);

  while(mid <= high) {
    if(mid * mid === x) {
      return mid;
    } else if(mid * mid > x) {
      high = mid - 1;
    } else {
      low = mid + 1;
    }

    mid = Math.ceil((low + high) / 2)
  }

  return high;
};
```