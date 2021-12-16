# 算法题 41. 缺失的第一个正数
[leetcode 地址](https://leetcode-cn.com/problems/first-missing-positive/)

## 题目描述

```
给你一个未排序的整数数组 nums ，请你找出其中没有出现的最小的正整数。

请你实现时间复杂度为 O(n) 并且只使用常数级别额外空间的解决方案。
 

示例 1：

输入：nums = [1,2,0]
输出：3
示例 2：

输入：nums = [3,4,-1,1]
输出：2
示例 3：

输入：nums = [7,8,9,11,12]
输出：1
 

提示：

1 <= nums.length <= 5 * 105
-231 <= nums[i] <= 231 - 1

```

### 思路

- 首先要明白，缺失的正整数，肯定在1 ~ n+1之间,n为数组长度
- 遍历数组，将数组按照1-n的位置排序。如果元素的值x在1-n之间，则将其和第x-1个元素互换位置。新的第x-1个元素有可能页在1-n之间，因此也需要互换位置。
- 再次遍历数组，此时没有缺失的正数元素，应该比他的下标大1，如果不满足这个条件，则这个下标+1就是缺失的正整数。
- 如果遍历数组结束后，都满足比下标大1，则缺失的正整数就是数组长度+1.


### 代码
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var firstMissingPositive = function (nums) {
    for (let i = 0; i < nums.length; i++) {
        while (nums[i] >= 1 && nums[i] <= nums.length && nums[i] !== nums[nums[i] - 1]) {
            let temp = nums[nums[i] - 1];
            nums[nums[i] - 1] = nums[i];
            nums[i] = temp;
        }
    }
    console.log(nums)
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] - 1 !== i) {
            return i + 1
        }
    }
    return nums.length + 1
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(1)