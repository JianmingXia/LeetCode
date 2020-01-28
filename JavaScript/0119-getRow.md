# 杨辉三角 II

## 题目描述
给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。

在杨辉三角中，每个数是它左上方和右上方的数的和。

### 示例
```
输入: 3
输出: [1,3,3,1]
```

### 说明
你可以优化你的算法到 O(k) 空间复杂度吗？

## 思路分析
这题跟上一题是类似的，只不过上一题需要输出所有行，这题输出指定行即可——输出指定行就有一个小要求，尽可能的节省空间，这里我用了一个辅助数据，用于保存上一次计算的结果，勉强够用了。

## 代码
- 时间复杂度O(n²)
- 空间复杂度O(n)

```
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
  let res = [];
  for(let i = 0; i <= rowIndex; i++) {
    const newRes = [];
    for(let j = 0; j <= i; j++) {
      if(j === 0 || j === i) {
        newRes.push(1);
      } else {
        newRes.push(res[j - 1] + res[j]);
      }
    }

    res = newRes;
  }  

  return res;
};
```