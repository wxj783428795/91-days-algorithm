# 算法题 989. 数组形式的整数加法

[leetcode 地址](https://leetcode-cn.com/problems/add-to-array-form-of-integer/)

## 题目描述

```
对于非负整数 X 而言，X 的数组形式是每位数字按从左到右的顺序形成的数组。例如，如果 X = 1231，那么其数组形式为 [1,2,3,1]。

给定非负整数 X 的数组形式 A，返回整数 X+K 的数组形式。

 

示例 1：

输入：A = [1,2,0,0], K = 34
输出：[1,2,3,4]
解释：1200 + 34 = 1234
示例 2：

输入：A = [2,7,4], K = 181
输出：[4,5,5]
解释：274 + 181 = 455
示例 3：

输入：A = [2,1,5], K = 806
输出：[1,0,2,1]
解释：215 + 806 = 1021
示例 4：

输入：A = [9,9,9,9,9,9,9,9,9,9], K = 1
输出：[1,0,0,0,0,0,0,0,0,0,0]
解释：9999999999 + 1 = 10000000000
 

提示：

1 <= A.length <= 10000
0 <= A[i] <= 9
0 <= K <= 10000
如果 A.length > 1，那么 A[0] != 0
```

### 思路

将K的每位与A的每位相加，如果大于10，则下一次相加要进位。

### 代码
```javascript
/**
 * @param {number[]} num
 * @param {number} k
 * @return {number[]}
 */
var addToArrayForm = function (num, k) {

    let answer = []; 
    let carry = 0; // 进位
    for (let i = 1; i <= num.length || k >= 1; i++) {
        let num1 = num.length - i >= 0 ? num[num.length - i] : 0;
        let num2 = k % 10;
        let sum = num1 + num2 + carry; //每位的和记得加上上一位的进位
        if (sum >= 10) { 
            answer.unshift(sum % 10);
            carry = Math.floor(sum / 10)
        } else {
            answer.unshift(sum)
            carry = 0
        }
        k = Math.floor(k / 10)
    }
    if (carry !== 0) { // 出循环后，如果最后进位不为0，则将进位添加到数组首位
        answer.unshift(carry)
    }
    return answer;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(N)，其中 N 为 num 和 k 中较长的长度。
- 空间复杂度：O(N)，其中 N 为 answer 的长度。