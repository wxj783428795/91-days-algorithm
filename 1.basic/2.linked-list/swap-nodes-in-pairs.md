# 算法题 24. 两两交换链表中的节点
[leetcode 地址](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

## 题目描述

```
给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

示例 1：

输入：head = [1,2,3,4]
输出：[2,1,4,3]
示例 2：

输入：head = []
输出：[]
示例 3：

输入：head = [1]
输出：[1]


提示：

链表中节点的数目在范围 [0, 100] 内
0 <= Node.val <= 100

```

### 思路
1. 两两交换节点，会形成闭环，所以要保存下下个节点作为当前节点的下个节点。
2. 也要保存当前节点的前一个节点，用于下两个节点与上两个节点之间的连接。
3. 要判断边界情况，比如链表长度为0和1的时候，直接返回head就行。


### 代码
```javascript
var swapPairs = function (head) {
    let curr = head;
    if (!head || !head.next)
        return head;
    let answer = head.next;
    let prev = null;
    while (curr) {
        let next = curr.next;
        if (!next) {
            prev.next = curr;
            return answer
        }
        let nextnext = next.next;
        next.next = curr;
        curr.next = nextnext;
        if (prev) {
            prev.next = next;
        }
        prev = curr;
        curr = curr.next;
    }
    return answer
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(1)