# Two Sum（1.两数之和）

## 题目描述
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

### Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## 思路分析
根据target，找到求和等于target的两位下标。根据javascript对象的特性，当对象属性未被设置时为undefined。在下标递增的情况下，以数组中值为属性，判断对象中的属性是否存在，如果为undefined，则需要继续查找，并在当前对象中设置属性；当map[find_num]不为undefined时，即满足条件。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    const length = nums.length;
    
    const map = {};
    for(let i = 0; i < length; i++) {
        const find_num = target - nums[i];
        
        if(typeof map[find_num] !== "undefined") {
            return [map[find_num], i];
        }
        map[nums[i]] = i;
    }
    
    return [];
};
```