# 盛最多水的容器

## 题目描述
给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

### 示例
```
输入：[1,8,6,2,5,4,8,3,7]
输出：49
```

### 说明
你不能倾斜容器，且 n 的值至少为 2。

## 思路分析
面积如何计算不必多说，这里只提及如何向内收缩：首先在每一个状态下，无论长板或短板收窄 1 格，都会导致水槽底边宽度 −1。所以：
- 若向内移动短板：水槽的短板可能变大，因此水槽面积可能增大
- 若向内移动长板：水槽的短板不变或变小，下个水槽的面积一定小于当前水槽面积

## 代码
- 时间复杂度O(n)
- 空间复杂度O(1)

```
/**
 * @param {number[]} heights
 * @return {number}
 */
var maxArea = function(heights) {
  let start = 0;
  let end = heights.length - 1;

  let res = 0;
  while(start < end) {
    res = Math.max(res, (end - start) * Math.min(heights[start], heights[end]));

    if(heights[end] < heights[start]) {
      end--;
    } else {
      start++;
    }
  }

  return res;
};
```