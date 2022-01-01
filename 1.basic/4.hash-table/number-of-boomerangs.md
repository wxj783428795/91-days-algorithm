# 算法题 447. 回旋镖的数量
[leetcode 地址](https://leetcode-cn.com/problems/number-of-boomerangs/)

## 题目描述

```
给定平面上 n 对 互不相同 的点 points ，其中 points[i] = [xi, yi] 。回旋镖 是由点 (i, j, k) 表示的元组 ，其中 i 和 j 之间的距离和 i 和 k 之间的欧式距离相等（需要考虑元组的顺序）。

返回平面上所有回旋镖的数量。

 
示例 1：

输入：points = [[0,0],[1,0],[2,0]]
输出：2
解释：两个回旋镖为 [[1,0],[0,0],[2,0]] 和 [[1,0],[2,0],[0,0]]
示例 2：

输入：points = [[1,1],[2,2],[3,3]]
输出：2
示例 3：

输入：points = [[1,1]]
输出：0
 

提示：

n == points.length
1 <= n <= 500
points[i].length == 2
-104 <= xi, yi <= 104
所有点都 互不相同

```

### 思路
1. 双层循环，内层循环计算每个点与外层点的距离，并用哈希表保存，距离以及距离相同的点的个数
2. 总的次数为 个数*（个数-1），累加即可。

### 代码
```javascript
var numberOfBoomerangs = function (points) {
    let ans = 0;
    for (let p1 of points) {
        let map = {};
        for (let p2 of points) {
            let dis = getDistance(p1, p2);
            if (map[dis] === undefined) {
                map[dis] = 1;
            } else {
                map[dis] += 1
            }
        }
        Object.entries(map).forEach(([k, v]) => {
            ans += v * (v - 1)
        })
    }
    return ans
};

var getDistance = (p1, p2) => {
    return Math.pow(p1[0] - p2[0], 2) + Math.pow(p1[1] - p2[1],2);
}
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n²) 
- 空间复杂度：O(n) 