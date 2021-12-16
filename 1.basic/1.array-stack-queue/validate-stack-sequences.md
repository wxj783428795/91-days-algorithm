# 算法题 946. 验证栈序列
[leetcode 地址](https://leetcode-cn.com/problems/validate-stack-sequences/)

## 题目描述

```
给定 pushed 和 popped 两个序列，每个序列中的 值都不重复，只有当它们可能是在最初空栈上进行的推入 push 和弹出 pop 操作序列的结果时，返回 true；否则，返回 false 。


示例 1：

输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
示例 2：

输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。
 

提示：

1 <= pushed.length <= 1000
0 <= pushed[i] <= 1000
pushed 的所有元素 互不相同
popped.length == pushed.length
popped 是 pushed 的一个排列

```

### 思路

1. 用一个临时的stack存储数据
2. 从0开始遍历pushed数组，和popped数组。
3. 当stack为空，或stack的最后一个元素不为当前popped元素时，将当前pushed元素压栈
4. 当stack不为空，并且stack最后一个元素等于当前popped元素时，当stack最后一个元素弹出
5. 循环直到遍历完当前数组，或不满足以上两个条件时，说明栈序列不对，则跳出循环
6. 最后判断stack是否为空，为空说明栈序列正确



### 代码
```javascript
/**
 * @param {number[]} pushed
 * @param {number[]} popped
 * @return {boolean}
 */
var validateStackSequences = function (pushed, popped) {
    let stack = [];
    let i = 0, j = 0;
    while (i < pushed.length || j < popped.length) {
        if ((stack.length === 0 || stack[stack.length - 1] !== popped[j]) && i < pushed.length) {
            stack.push(pushed[i])
            i++
        } else if (stack.length !== 0 && stack[stack.length - 1] === popped[j]) {
            stack.pop()
            j++
        } else {
            break;
        }
        console.log(stack)
    }
    return !stack.length

};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(N) N为pushed和popped的长度的和
- 空间复杂度：O(N) N为pushed或popped的长度