# 算法题 876. 链表的中间结点
[leetcode 地址](https://leetcode-cn.com/problems/middle-of-the-linked-list/)

## 题目描述

```
给定一个头结点为 head 的非空单链表，返回链表的中间结点。

如果有两个中间结点，则返回第二个中间结点。

 

示例 1：

输入：[1,2,3,4,5]
输出：此列表中的结点 3 (序列化形式：[3,4,5])
返回的结点值为 3 。 (测评系统对该结点序列化表述是 [3,4,5])。
注意，我们返回了一个 ListNode 类型的对象 ans，这样：
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, 以及 ans.next.next.next = NULL.
示例 2：

输入：[1,2,3,4,5,6]
输出：此列表中的结点 4 (序列化形式：[4,5,6])
由于该列表有两个中间结点，值分别为 3 和 4，我们返回第二个结点。

```

### 思路
1. 快慢指针，快指针每次走两步，慢指针每次走一步
2. 当快指针走到链表末尾，慢指针就在链表的中间节点

### 代码
```javascript
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var middleNode = function (head) {
    let slow = head;
    let fast = head;
    while (fast !== null&& fast.next!==null){
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n) 
- 空间复杂度：O(1) 