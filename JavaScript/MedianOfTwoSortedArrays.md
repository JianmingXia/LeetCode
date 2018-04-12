# Median of Two Sorted Arrays（4.两个排序数组的中位数）

## 题目描述
There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

### Example 1:
```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

### Example 2:
```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

## 思路分析
已知两个有序数组，求得两个排序数组的中位数，第一反应，直接做了个简单的归并排序，变成一个有序数组，再直接求中位数即可。
这个方法简单粗暴，但是空间复杂度上有点浪费，还有更优的解，有时间再做更新。

## 代码
- 时间复杂度O(n)
- 空间复杂度O(n)

```
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
const getArrayMediam = function(arr) {
    const length = arr.length;
    if(length % 2 === 1) {
        return arr[(length - 1) / 2];
    } else {
        return (arr[length / 2] + arr[length / 2 - 1]) / 2;
    }
};

var findMedianSortedArrays = function(nums1, nums2) {
    if(nums1.length === 0) {
        return getArrayMediam(nums2);
    }
    if(nums2.length === 0) {
        return getArrayMediam(nums1);
    }
    
    const new_arr = [];
    let index_a = 0;
    let index_b = 0;
    while(true) {
        if(index_a >= nums1.length && index_b >= nums2.length) {
            break;
        } else if(index_a >= nums1.length) {
            new_arr.push(nums2[index_b++]);
        } else if(index_b >= nums2.length) {
            new_arr.push(nums1[index_a++]);
        } else {
            if(nums1[index_a] > nums2[index_b]) {
                new_arr.push(nums2[index_b++]);
            } else {
                new_arr.push(nums1[index_a++]);
            }
        }
    }
    
    return getArrayMediam(new_arr);
};
```