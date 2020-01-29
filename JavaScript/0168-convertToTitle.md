# Excel表列名称

## 题目描述
给定一个正整数，返回它在 Excel 表中相对应的列名称。

例如，

    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...

### 示例
```
示例 1:

输入: 1
输出: "A"

示例 2:

输入: 28
输出: "AB"

示例 3:

输入: 701
输出: "ZY"
```

## 思路分析
无须多言，一个普通的进制处理问题。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
const chars = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'];

/**
 * @param {number} n
 * @return {string}
 */
var convertToTitle = function(n) {
  let res = '';
  while(n) {
    const remainder = (n - 1) % 26;
    res = chars[remainder] + res;

    n = parseInt((n - 1) / 26);
  }

  return res;
};
```