# 算法题 26. 删除有序数组中的重复项
[leetcode 地址](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

## 题目描述

```
给你一个有序数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

 

说明:

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以「引用」方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
 
示例 1：

输入：nums = [1,1,2]
输出：2, nums = [1,2]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
示例 2：

输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
 

提示：

0 <= nums.length <= 3 * 104
-104 <= nums[i] <= 104
nums 已按升序排列

```

### 思路
1. 双指针，由于是排序数组，所以相同的数字肯定是连续的，所以一次遍历就能解决问题
2. 慢指针先不动，快指针每次前进1
3. 当快慢指针数字相同时，快指针前进1，慢指针不动
4. 当快慢指针数字不同时，把快指针的值赋值给慢指针的下一位，然后快慢指针都前进1
5. 重复3和4直到快指针到数组末尾。

### 代码
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function (nums) {
    let i = 0;
    let j = 1;
    while (j < nums.length) {
        if (nums[i] === nums[j]) {
            j++
        } else {
            nums[i + 1] = nums[j];
            i++;
            j++;
        }
    }
    return i + 1
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n) 
- 空间复杂度：O(1) 