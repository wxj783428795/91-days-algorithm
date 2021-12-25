# 算法题 100. 相同的树
[leetcode 地址](https://leetcode-cn.com/problems/same-tree/)

## 题目描述

给你两棵二叉树的根节点 p 和 q ，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

 

示例 1：

![图1](./images/same-tree1.jpg)


输入：p = [1,2,3], q = [1,2,3]
输出：true

示例 2：

![图2](./images/same-tree2.jpg)


输入：p = [1,2], q = [1,null,2]
输出：false

示例 3：

![图3](./images/same-tree3.jpg)


输入：p = [1,2,1], q = [1,1,2]
输出：false
 

提示：

两棵树上的节点数目都在范围 [0, 100] 内
-104 <= Node.val <= 104

 

### 思路
1. dfs
2. 如果两个节点同时为空，则返回true
3. 如果两个节点只有一个为空，则返回false，树肯定不相等
4. 如果两个节点值不同则返回false
5. 递归判断节点的左右子节点


### 代码
```javascript
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function (p, q) {
    if (!p && !q) {
        return true;
    }
    if (!p || !q) {
        return false;
    }
    if (p.val !== q.val) {
        return false;
    }
    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right)
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(h)