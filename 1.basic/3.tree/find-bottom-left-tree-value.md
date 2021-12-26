# 算法题 513. 找树左下角的值
[leetcode 地址](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)

## 题目描述

给定一个二叉树的 根节点 root，请找出该二叉树的 最底层 最左边 节点的值。

假设二叉树中至少有一个节点。

示例 1:
![图1](./images/find-bottom-left-tree-value1.jpg)


输入: root = [2,1,3]
输出: 1
示例 2:
![图2](./images/find-bottom-left-tree-value2.jpg)


输入: [1,2,3,4,null,5,6,null,null,7]
输出: 7

提示:

二叉树的节点个数的范围是 [1,104]
-231 <= Node.val <= 231 - 1 

### 思路
1. bfs
2. 找到最后一行的第一个元素


### 代码
```javascript

```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(n)