# 算法题 821. 字符的最短距离

[leetcode 地址](https://leetcode-cn.com/problems/shortest-distance-to-a-character)

## 题目描述

```
给定一个字符串 S 和一个字符 C。返回一个代表字符串 S 中每个字符到字符串 S 中的字符 C 的最短距离的数组。

示例 1:

输入: S = "loveleetcode", C = 'e'
输出: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]
说明:

- 字符串 S 的长度范围为 [1, 10000]。
- C 是一个单字符，且保证是字符串 S 里的字符。
- S 和 C 中的所有字母均为小写字母。

```

### 思路

第一次循环：找到s中所有c的下标。
第二次循环：循环对比s中每个字符，到所有c的下标的距离，取其中的最小值放入answer中

### 代码
/**
 * @param {string} s
 * @param {character} c
 * @return {number[]}
 */

var shortestToChar = function (s, c) {
    let indexs = []; // 存储所有c在s中的下标
    let answer = []; // 存储结果
    for (let i = 0; i < s.length; i++) { // 第一遍循环先找到所有c在s中的下标
        if (c === s[i]) {
            indexs.push(i)
        }
    }
    for (let i = 0; i < s.length; i++) { // 第二遍循环
        let distance = 0;
        if (c === s[i]) { // 如果当前位等于c，则将0放入answer
            answer.push(distance)
        } else {
            distance = Math.abs(i - indexs[0]);
            for (let j = 1; j < indexs.length; j++) {// 循环判断当前位和每一个c的距离，取最小值
                distance = Math.min(distance, Math.abs(i - indexs[j]));
            }
            answer.push(distance)
        }
    }
    return answer;
};
```
### 复杂度分析

- 时间复杂度：O(NM)，其中 N 为s的长度，M为s中c出现的次数。
- 空间复杂度：O(N+M)，其中 N 为s的长度，M为s中c出现的次数。