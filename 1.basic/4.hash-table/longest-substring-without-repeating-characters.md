# 算法题 3. 无重复字符的最长子串
[leetcode 地址](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

## 题目描述

```
给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串 的长度。


示例 1:

输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
示例 4:

输入: s = ""
输出: 0
 

提示：

0 <= s.length <= 5 * 104
s 由英文字母、数字、符号和空格组成
通过次数1,404,538提交次数3,664,827

```

### 思路
1. 遍历字符串，记录无重复字串的左侧下标。
2. 当前字符在目前子串中时，将左侧下标更新。
3. 当前字符不在目前子串中时，更新最大长度。

### 代码
```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function (s) {
    if (!s.length) return 0;
    let max = 0;
    let left = 0;
    let str = ''
    for (let i = 0; i < s.length; i++) {
        if (str.includes(s[i])) {
            left += s.slice(left, i).indexOf(s[i]) + 1
            continue;
        }
        str = s.slice(left, i + 1);
        max = Math.max(max, str.length);
    }
    return max;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(n) 