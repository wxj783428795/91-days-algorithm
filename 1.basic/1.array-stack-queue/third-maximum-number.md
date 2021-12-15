# 算法题 414. 第三大的数

[leetcode 地址](https://leetcode-cn.com/problems/third-maximum-number/)

## 题目描述

```
给你一个非空数组，返回此数组中 第三大的数 。如果不存在，则返回数组中最大的数。

示例 1：

输入：[3, 2, 1]
输出：1
解释：第三大的数是 1 。
示例 2：

输入：[1, 2]
输出：2
解释：第三大的数不存在, 所以返回最大的数 2 。
示例 3：

输入：[2, 2, 3, 1]
输出：1
解释：注意，要求返回第三大的数，是指在所有不同数字中排第三大的数。
此例中存在两个值为 2 的数，它们都排第二。在所有不同数字中排第三大的数为 1 。

提示：

1 <= nums.length <= 104
-231 <= nums[i] <= 231 - 1

进阶：你能设计一个时间复杂度 O(n) 的解决方案吗？

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/third-maximum-number
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

### 思路

1. 将数组转换为set，去除重复值
2. 再转换为数组，并从大到小排序
3. 如果数组长度<3,则返回数组的第一个元素（即最大值）,否则返回数组的第三个元素

### 代码
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var thirdMax = function (nums) {
    let arr = Array.from(new Set(nums)).sort((a, b) => b - a)
    return arr.length < 3 ? arr[0] : arr[2]
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**

- 时间复杂度：O(nlogn)，其中 n 是数组 nums 的长度。排序需要 O(nlogn) 的时间。
- 空间复杂度：O(logn)，排序需要的栈空间为 O(logn)。
