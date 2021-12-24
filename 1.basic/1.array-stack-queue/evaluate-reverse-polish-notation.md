# 算法题 150. 逆波兰表达式求值
[leetcode 地址](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/)

## 题目描述

```
根据 逆波兰表示法，求表达式的值。

有效的算符包括 +、-、*、/ 。每个运算对象可以是整数，也可以是另一个逆波兰表达式。

说明：

整数除法只保留整数部分。
给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

示例 1：

输入：tokens = ["2","1","+","3","*"]
输出：9
解释：该算式转化为常见的中缀算术表达式为：((2 + 1) * 3) = 9
示例 2：

输入：tokens = ["4","13","5","/","+"]
输出：6
解释：该算式转化为常见的中缀算术表达式为：(4 + (13 / 5)) = 6
示例 3：

输入：tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
输出：22
解释：
该算式转化为常见的中缀算术表达式为：
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22

提示：

1 <= tokens.length <= 104
tokens[i] 要么是一个算符（"+"、"-"、"*" 或 "/"），要么是一个在范围 [-200, 200] 内的整数

```

### 思路
1. 遍历数组，如果是数字就存入栈中
2. 如果是符号，则从栈顶弹出两个元素进行计算
3. 注意除法只保留正数，正数时用floor，负数时用ceil


### 代码
```javascript
/**
 * @param {string[]} tokens
 * @return {number}
 */
var evalRPN = function (tokens) {
    let stack = [];
    for (let i = 0; i < tokens.length; i++) {
        if (isNumber(tokens[i])) {
            stack.push(tokens[i])
        } else {
            let calc;
            let num1 = Number(stack.pop())
            let num2 = Number(stack.pop())
            switch (tokens[i]) {
                case '+':
                    calc = num2 + num1;
                    break;
                case '-':
                    calc = num2 - num1;
                    break;
                case '*':
                    calc = num2 * num1;
                    break;
                case '/':
                    calc = num2 / num1 >= 0 ? Math.floor(num2 / num1) : Math.ceil(num2 / num1);
                    break;
            }
            stack.push(calc)
        }
    }
    return stack[0]
};
var isNumber = (char) => Number.isInteger(Number(char));
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(n)