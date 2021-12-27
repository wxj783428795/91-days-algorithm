# 算法题 108. 将有序数组转换为二叉搜索树
[leetcode 地址](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

## 题目描述

给你一个整数数组 nums ，其中元素已经按 升序 排列，请你将其转换为一棵 高度平衡 二叉搜索树。

高度平衡 二叉树是一棵满足「每个节点的左右两个子树的高度差的绝对值不超过 1 」的二叉树。


示例 1：
![图1](./images/convert-sorted-array-to-binary-search-tree1.jpg)

输入：nums = [-10,-3,0,5,9]
输出：[0,-3,9,-10,null,5]
解释：[0,-10,5,null,-3,null,9] 也将被视为正确答案：
![图2](./images/convert-sorted-array-to-binary-search-tree2.jpg)


示例 2：
![图3](./images/convert-sorted-array-to-binary-search-tree3.jpg)

输入：nums = [1,3]
输出：[3,1]
解释：[1,3] 和 [3,1] 都是高度平衡二叉搜索树。


提示：

1 <= nums.length <= 104
-104 <= nums[i] <= 104
nums 按 严格递增 顺序排列

### 思路
1. 找到数组的中间的元素作为树的根节点。
2. 把数组从中间一分为二，左边的数组是树的左子树，右边为右子树
3. 递归之


### 代码
```javascript
/**
 * @param {number[]} nums
 * @return {TreeNode}
 */
var sortedArrayToBST = function (nums) {
    if(!nums.length) return null;
    if (nums.length === 1) return new TreeNode(nums[0]);
    let middle = Math.floor(nums.length / 2);
    let node = new TreeNode(nums[middle]);
    node.left = sortedArrayToBST(nums.slice(0, middle));
    node.right = sortedArrayToBST(nums.slice(middle + 1));
    return node;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(h)