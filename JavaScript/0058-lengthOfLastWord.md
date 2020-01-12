# 最后一个单词的长度

## 题目描述
给定一个仅包含大小写字母和空格 ' ' 的字符串，返回其最后一个单词的长度。

如果不存在最后一个单词，请返回 0 。

说明：一个单词是指由字母组成，但不包含任何空格的字符串。

### 示例
```
示例:

输入: "Hello World"
输出: 5
```

## 思路分析
这题其实是个非常简单的题目，但是由于审题原因，这里错了好几次——题目的关键字是“返回其最后一个单词的长度”。所以我们找到最后一个单词，计算长度即可，其它的都是花里胡哨的。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

### 复杂思路
```
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
  if (s.length === 0) {
    return 0;
  }

  const reverseArr = s.split("").reverse();

  let index = 0;
  for (; index < reverseArr.length; index++) {
    if (reverseArr[index] === " ") {
      continue;
    } else {
      break;
    }
  }

  if(index === reverseArr.length) {
    return 0;
  }
  const lastBlankPos = reverseArr.indexOf(" ", index);
  if (lastBlankPos < 0) {
    return s.length - index;
  } else {
    return lastBlankPos - index;
  }
};
```

### 简易思路
```
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
  return s
    .trim()
    .split(" ")
    .pop().length;
};
```