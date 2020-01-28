# 杨辉三角

## 题目描述
给定一个非负整数 numRows，生成杨辉三角的前 numRows 行。

在杨辉三角中，每个数是它左上方和右上方的数的和。

### 示例
```
输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## 思路分析
这题还是比较简单的，输出杨辉三角即可。

## 代码
- 时间复杂度O(n²)
- 空间复杂度O(n²)

```
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
  let res = [];
  for(let i = 0; i < numRows; i++) {
    const row = [1];
    for(let j = 1; j <= i; j++) {
      if(j == i) {
        row.push(1);
      } else {
        row.push(res[i - 1][j - 1] + res[i - 1][j]);
      }
    }

    res.push(row);
  }  

  return res;
};
```