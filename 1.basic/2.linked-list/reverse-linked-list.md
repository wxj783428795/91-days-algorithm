# 算法题 206. 反转链表
[leetcode 地址](https://leetcode-cn.com/problems/reverse-linked-list/)

## 题目描述

给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。
 

示例 1：

![图1](./images/reverse-linked0list1.jpg)

输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]

示例 2：

![图2](./images/reverse-linked-list2.jpg)


输入：head = [1,2]
输出：[2,1]

示例 3：

输入：head = []
输出：[]
 

提示：

链表中节点的数目范围是 [0, 5000]
-5000 <= Node.val <= 5000
 

进阶：链表可以选用迭代或递归方式完成反转。你能否用两种方法解决这道题？

### 思路
1. 遍历，保存上一个节点。
2. 将当前节点的下一个节点指向上次循环保存的上一个节点


### 代码
```javascript
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function (head) {
    if (!head || !head.next) return head;
    let prev = null;
    let curr = head;
    while (curr) {
        let next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(1)