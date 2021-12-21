# 算法题 2021-12-18  61. 旋转链表
[leetcode 地址](https://leetcode-cn.com/problems/rotate-list/)

## 题目描述

```
给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

示例 1:

输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
示例 2:

输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
```

### 思路
1. 找到链表的tail，以及长度
2. 将tail的next指向head，形成环。
3. 在长度-k处断开链表即可


### 代码
```javascript
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var rotateRight = function (head, k) {
    if (!head) return head;
    let length = 1;
    let next = head;
    while (next.next) {
        length++;
        next = next.next;
    }
    //这时的next是链表的最后一个元素
    let move = k % length;
    if (!move) return head;
    //将tail的next指向head，形成环
    next.next = head;
    //然后再第length-move处断开环
    let step = length - move;
    let newTail = head;
    while (--step > 0) {
        newTail = newTail.next
    }
    let answer = newTail.next;
    newTail.next = null
    return answer
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n) n为链表长度
- 空间复杂度：O(1)