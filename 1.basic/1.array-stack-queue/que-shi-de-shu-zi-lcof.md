# 算法题 剑指 Offer 53 - II. 0～n-1中缺失的数字
[leetcode 地址](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

## 题目描述

```
一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

示例 1:

输入: [0,1,3]
输出: 2

示例 2:

输入: [0,1,2,3,4,5,6,7,9]
输出: 8

限制：

1 <= 数组长度 <= 10000

```

### 思路1
1. 遍历数组，用当前元素减去前一个，如果差不为1，就返回**当前元素-1**
2. 特殊情况1，数组第一个元素不为0，说明缺失的数字就是0
3. 特殊情况2，遍历完整个数组也没发现差不为1的情况，说明缺失的是最后**数组最后一个元素+1**

### 代码1
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function (nums) {
    if (nums[0] !== 0) {
        return 0
    }

    for (let i = 1; i < nums.length; i++) {
        if (nums[i] - nums[i - 1] !== 1) {
            return nums[i] - 1
        }
    }
    return nums[nums.length - 1] + 1
};
```
### 复杂度分析1
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n) n为nums的长度
- 空间复杂度：O(1) 没有用到额外空间


### 思路2
1. 排序数组中的搜索问题，用二分法
2. 将数组一分为二，i和j，分别为数组的两端。如果中间的元素（m=（i+j）/2），下标和元素值相等，则说明左侧数组没有缺失元素，缺失的元素在右侧。将i更新为m+1，继续遍历。
3. 跳出循环后，答案即为i

### 代码1
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function (nums) {
    let i = 0, j = nums.length - 1;
    while (i <= j) {
        let m = Math.floor((i + j) / 2);
        if (nums[m] === m) {//数字和下标能对应，说明缺失的数字在右侧
            i = m + 1
        } else {// 说明缺失的数字在左侧
            j = m - 1
        }
    }
    return i;
};
```

### 复杂度分析2
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(logN) N为nums长度，二分法的时间复杂度就是O(logN)
- 空间复杂度：O(1) 没有用到额外空间