# 算法题 Delete Sublist to Make Sum Divisible By K
[binarysearch 地址](https://binarysearch.com/problems/Delete-Sublist-to-Make-Sum-Divisible-By-K)

## 题目描述

```
You are given a list of positive integers nums and a positive integer k. Return the length of the shortest sublist (can be empty sublist ) you can delete such that the resulting list's sum is divisible by k. You cannot delete the entire list. If it's not possible, return -1.

Constraints

1 ≤ n ≤ 100,000 where n is the length of nums
Example 1
Input
nums = [1, 8, 6, 4, 5]
k = 7
Output
2
Explanation
We can remove the sublist [6, 4] to get [1, 8, 5] which sums to 14 and is divisible by 7.
```

### 思路
1. 前缀和+同余定理
2. 哈希表储存前缀和
3. 还没完全理解，先CV，回头慢慢消化

### 代码
```javascript
var floorMod = function (a, b) {
    return ((a % b) + b) % b;
};
class Solution {

    solve(nums, k) {
        let map = new Map()
        map.set(0, -1);
        let sum = nums.reduce((p, c) => p + c, 0);
        let target = sum % k;
        let currSum = 0;
        let res = nums.length;
        for (let i = 0; i < nums.length; i++) {
            currSum = (currSum + nums[i]) % k;
            map.set(currSum, i);
            let prev = floorMod(currSum - target, k)
            if (map.has(prev)) {
                res = Math.min(res, i - map.get(prev))
            }
        }
        return res === nums.length ? -1 : res;
    }
}
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(k) 