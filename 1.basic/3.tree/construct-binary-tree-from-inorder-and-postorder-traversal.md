# 算法题 106. 从中序与后序遍历序列构造二叉树
[leetcode 地址](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

## 题目描述

```
根据一棵树的中序遍历与后序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出

中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7

```

### 思路
1. 后序遍历，是`左右根`，因此后序遍历的最后一个节点肯定是这个树的根节点。
2. 中序遍历，是`左根右`, 因此，在后序遍历中找到根节点后，在中序遍历中找到根节点的索引，在这个节点之前的节点，都是树的左子树节点；之后的都是树的右子树节点。
3. 递归即可。当中序遍历或后续遍历数组为空时，返回null。
4. 每次递归，前序和中序数组都会少一个元素，就是本次递归的那个元素。


### 代码
```javascript
/**
 * @param {number[]} inorder
 * @param {number[]} postorder
 * @return {TreeNode}
 */
var buildTree = function (inorder, postorder) {
    if (!inorder.length) return null;
    let val = postorder[postorder.length - 1];
    let i = inorder.indexOf(val);
    let node = new TreeNode(val);
    node.left = buildTree(inorder.slice(0, i), postorder.slice(0, i))
    node.right = buildTree(inorder.slice(i + 1), postorder.slice(i, postorder.length - 1))
    return node;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(h)