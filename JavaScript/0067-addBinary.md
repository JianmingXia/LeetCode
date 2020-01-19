# 二进制求和

## 题目描述
给定两个二进制字符串，返回他们的和（用二进制表示）。

输入为非空字符串且只包含数字 1 和 0。

### 示例
```
示例 1:

输入: a = "11", b = "1"
输出: "100"

示例 2:

输入: a = "1010", b = "1011"
输出: "10101"
```

## 思路分析
这题跟 66 题差不多：
- 只不过 66 是 +1，这里是两个数相加
- 二进制的处理与十进制类似

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
const getReverseArray = (str) => {
  return str.split("").reverse();
}

/**
 * @param {string} a
 * @param {string} b
 * @return {string}
 */
var addBinary = function(a, b) {
  const arr1 = getReverseArray(a);
  const arr2 = getReverseArray(b);

  const len = arr1.length > arr2.length ? arr1.length : arr2.length;
  // 进位 flag
  let flag = 0;
  let res = [];
  for(let i = 0; i < len; i++) {
    const num = Number(arr1[i] ? arr1[i] : 0) + Number(arr2[i] ? arr2[i] : 0) + flag;

    res.push(num % 2);
    flag = num > 1 ? 1 : 0;
  }

  if(flag) {
    res.push(flag);
  }

  return res.reverse().join("");
};
```