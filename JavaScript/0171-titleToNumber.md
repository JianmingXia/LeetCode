# Excel表列序号

## 题目描述
给定一个Excel表格中的列名称，返回其相应的列序号。

例如，

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...

### 示例
```
示例 1:

输入: "A"
输出: 1

示例 2:

输入: "AB"
输出: 28

示例 3:

输入: "ZY"
输出: 701
```

## 思路分析
与前面的一样，无须多言，一个普通的进制处理问题。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * @param {string} s
 * @return {number}
 */
var titleToNumber = function(s) {
  const chars = s.split('');
  const baseNum = 'A'.charCodeAt();

  let res = 0;
  for(let i = 0; i < s.length; i++) {
    res = res * 26 + chars[i].charCodeAt() - baseNum + 1;
  }

  return res;
};
```