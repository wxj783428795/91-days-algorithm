# 算法题 347. 前 K 个高频元素
[leetcode 地址](https://leetcode-cn.com/problems/top-k-frequent-elements/)

## 题目描述

```
给你一个整数数组 nums 和一个整数 k ，请你返回其中出现频率前 k 高的元素。你可以按 任意顺序 返回答案。

 

示例 1:

输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
示例 2:

输入: nums = [1], k = 1
输出: [1]
 

提示：

1 <= nums.length <= 105
k 的取值范围是 [1, 数组中不相同的元素的个数]
题目数据保证答案唯一，换句话说，数组中前 k 个高频元素的集合是唯一的
 

进阶：你所设计算法的时间复杂度 必须 优于 O(n log n) ，其中 n 是数组大小。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/top-k-frequent-elements
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

### 思路
1. 用一个map记录key和出现的次数
2. 桶排序

### 代码
```javascript
var topKFrequent = function (nums, k) {
    let map = {};
    for (let num of nums) {
        if (map[num] === undefined) {
            map[num] = 1;
        } else {
            map[num] += 1;
        }
    }
    let arr = [];
    Object.entries(map).map((item) => {
        if (arr[item[1]] === undefined) {
            arr[item[1]] = [item[0]];
        } else {
            arr[item[1]].push(item[0]);
        }
    });
    let ans = [];
    for (let i = arr.length - 1; i >= 0 && ans.length < k; i--) {
        arr[i] && ans.push(...arr[i]);
    }
    return ans;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n) 排序的复杂度
- 空间复杂度：O(n) 