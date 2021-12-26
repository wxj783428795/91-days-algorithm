# 算法题 105. 从前序与中序遍历序列构造二叉树
[leetcode 地址](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

## 题目描述

给定一棵树的前序遍历 preorder 与中序遍历  inorder。请构造二叉树并返回其根节点。

示例 1:

![图1](./images/construct-binary-tree-from-preorder-and-inorder-traversal1.jpg)

Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
示例 2:

Input: preorder = [-1], inorder = [-1]
Output: [-1]

提示:

1 <= preorder.length <= 3000
inorder.length == preorder.length
-3000 <= preorder[i], inorder[i] <= 3000
preorder 和 inorder 均无重复元素
inorder 均出现在 preorder
preorder 保证为二叉树的前序遍历序列
inorder 保证为二叉树的中序遍历序列

### 思路
1. 前序遍历，是`根左右`，因此前序遍历的第一个节点肯定是这个树的根节点。
2. 中序遍历，是`左根右`, 因此，在前序遍历中找到根节点后，在中序遍历中找到根节点的索引，在这个节点之前的节点，都是树的左子树节点；之后的都是树的右子树节点。
3. 递归即可。当前序遍历或后续遍历数组为空时，返回null。
4. 每次递归，前序和中序数组都会少一个元素，就是本次递归的那个元素。


### 代码
```javascript
/**
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function (preorder, inorder) {
    if (!preorder.length) return null
    let rootVal = preorder[0];
    let i = inorder.indexOf(rootVal);
    let node = new TreeNode(rootVal, buildTree(preorder.slice(1, i + 1), inorder.slice(0, i)), buildTree(preorder.slice(i + 1), inorder.slice(i + 1)))
    return node;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(h)