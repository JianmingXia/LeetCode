# Detect Capital（检测大写字母）

## 题目描述
Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:
- All letters in this word are capitals, like "USA".
- All letters in this word are not capitals, like "leetcode".
- Only the first letter in this word is capital if it has more than one letter, like "Google".
Otherwise, we define that this word doesn't use capitals in a right way.
### Example 1:
```
Input: "USA"
Output: True
```

### Example 2:
```
Input: "FlaG"
Output: False
```

Note: The input will be a non-empty word consisting of uppercase and lowercase latin letters.

## 思路分析
检测大写字母，只有三种情况符合要求
- 全部大写
- 全部小写
- 第一位大写，其它为小写

## 代码
### 正则解决
```
var detectCapitalUse = function (word) {
    return /^([A-Z]+|[a-z]+|[A-Z][a-z]+)$/.test(word);
};
```

### 硬编码
```
// TODO
```