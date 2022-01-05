# 算法题 974. 和可被 K 整除的子数组
[leetcode 地址](https://leetcode-cn.com/problems/subarray-sums-divisible-by-k/)

## 题目描述

```
给定一个整数数组 A，返回其中元素之和可被 K 整除的（连续、非空）子数组的数目。


示例：

输入：A = [4,5,0,-2,-3,1], K = 5
输出：7
解释：
有 7 个子数组满足其元素之和可被 K = 5 整除：
[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]


提示：

1 <= A.length <= 30000
-10000 <= A[i] <= 10000
2 <= K <= 10000

```

### 思路
1. 前缀和：用一个散列表，保存数组每一位的前缀和
2. 同余定理：因为子数组要满足被K整除，子数组的和可以用前缀和的差求出。由同余定理可得，如果两个前缀和对K取的模相同，则差一定能被K整除。
3. 因此再用一个散列表保存，每个前缀和对K取模，以及该模出现的次数。

### 代码
```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var subarraysDivByK = function (nums, k) {
    let sumMap = { 0: nums[0] };
    for (let i = 1; i < nums.length; i++) {
        sumMap[i] = nums[i] + sumMap[i - 1];
    }
    let modMap = { 0: 1 };
    let res = 0;
    for (let i = 0; i < nums.length; i++) {
        let mod = ((sumMap[i] % k) + k) % k;
        if (modMap[mod] !== undefined) {
            res += modMap[mod];
            modMap[mod] += 1;
        } else {
            modMap[mod] = 1;
        }
    }
    return res;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n) 排序的复杂度
- 空间复杂度：O(n) 