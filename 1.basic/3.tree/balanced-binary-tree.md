# 算法题 110. 平衡二叉树
[leetcode 地址](https://leetcode-cn.com/problems/balanced-binary-tree/)

## 题目描述
给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1 。

示例 1：
[!图1](./images/balanced-binary-tree1.jpg)

输入：root = [3,9,20,null,null,15,7]
输出：true
示例 2：
[!图2](./images/balanced-binary-tree2.jpg)


输入：root = [1,2,2,3,3,null,null,4,4]
输出：false
示例 3：

输入：root = []
输出：true


提示：

树中的节点数在范围 [0, 5000] 内
-104 <= Node.val <= 104

### 思路
1. 先写一个方法计算每个节点的高度
2. 递归判断每个节点的左右子节点的高度差


### 代码
```javascript
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isBalanced = function (root) {
    if (!root) return true;
    if (Math.abs(dfs(root.left) - dfs(root.right)) > 1) return false;
    return isBalanced(root.left) && isBalanced(root.right);
};

var dfs = function (node) {
    if (!node) return 0;
    return Math.max(dfs(node.left), dfs(node.right)) + 1;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n²)
- 空间复杂度：O(n)