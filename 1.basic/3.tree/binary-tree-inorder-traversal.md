# 算法题 94. 二叉树的中序遍历
[leetcode 地址](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

## 题目描述

示例 1：

![图1](./images/binary-tree-inorder-traversal1.jpg)

输入：root = [1,null,2,3]
输出：[1,3,2]
示例 2：

输入：root = []
输出：[]
示例 3：

输入：root = [1]
输出：[1]
示例 4：

![图2](./images/binary-tree-inorder-traversal2.jpg)


输入：root = [1,2]
输出：[2,1]
示例 5：

![图3](./images/binary-tree-inorder-traversal3.jpg)


输入：root = [1,null,2]
输出：[1,2]

提示：

树中节点数目在范围 [0, 100] 内
-100 <= Node.val <= 100

进阶: 递归算法很简单，你可以通过迭代算法完成吗？

### 思路
递归


### 代码
```javascript
var inorderTraversal = function (root) {
    return inorder(root, [])
};
var inorder = function (node, ans) {
    if (!node) return ans;
    ans = inorder(node.left, ans);
    ans.push(node.val)
    ans = inorder(node.right, ans);
    return ans
}
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(h)