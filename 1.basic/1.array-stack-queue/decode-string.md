# 算法题 394. 字符串解码
[leetcode 地址](https://leetcode-cn.com/problems/decode-string/)

## 题目描述

```
给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。



示例 1：

输入：s = "3[a]2[bc]"
输出："aaabcbc"
示例 2：

输入：s = "3[a2[c]]"
输出："accaccacc"
示例 3：

输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
示例 4：

输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"
通过次数131,369提交次数

```

### 思路

1. 循环遍历字符串，将字符从头开始压栈，如果遇到']'，则开始出栈，直到'['。将括号之间的字符串标记为需要重复的字符串。
2. 继续出栈，直到字符不为数字为止，这期间出栈的数字记为需要重复的次数。
3. 循环创建重复字符串，并压入栈中
4. 进入下一轮循环。

### 代码
```javascript
/**
 * @param {string} s
 * @return {string}
 */
var decodeString = function (s) {
    let stack = [];
    for (let i = 0; i < s.length; i++) {
        if (s[i] === ']') {
            let str = ''
            let count = ''
            while (stack.length && stack[stack.length - 1] != '[') {
                str = stack.pop() + str;
            }
            stack.pop();
            while (stack.length && Number.isInteger(+stack[stack.length - 1])) {
                count = stack.pop() + count;
            }
            for (let j = 0; j < +count; j++) {
                stack.push(str)
            }
        } else {
            stack.push(s[i])
        }
    }
    return stack.join('')
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(N)
- 空间复杂度：O(N)