# 算法题 109. 有序链表转换二叉搜索树
[leetcode 地址](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/)

## 题目描述

```
给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:

给定的有序链表： [-10, -3, 0, 5, 9],

一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

### 思路
1. 因为是有序排列，因此找到链表的中点就能作为二叉树的根节点。
2. 搜索前半段链表的中点作为左侧子树根节点，右侧同理
3. 递归调用即可
4. 使用快慢指针，快指针每次走两步，慢指针每次走一步，当快指针在链表尾部时，慢指针就在中点

### 代码
```javascript

```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：
- 空间复杂度：