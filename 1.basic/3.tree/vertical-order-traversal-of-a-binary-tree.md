# 算法题 987. 二叉树的垂序遍历
[leetcode 地址](https://leetcode-cn.com/problems/vertical-order-traversal-of-a-binary-tree/)

## 题目描述

给你二叉树的根结点 root ，请你设计算法计算二叉树的 垂序遍历 序列。

对位于 (row, col) 的每个结点而言，其左右子结点分别位于 (row + 1, col - 1) 和 (row + 1, col + 1) 。树的根结点位于 (0, 0) 。

二叉树的 垂序遍历 从最左边的列开始直到最右边的列结束，按列索引每一列上的所有结点，形成一个按出现位置从上到下排序的有序列表。如果同行同列上有多个结点，则按结点的值从小到大进行排序。

返回二叉树的 垂序遍历 序列。
示例 1：

![图1](./images/vertical-order-traversal-of-a-binary-tree1.jpg)

输入：root = [3,9,20,null,null,15,7]
输出：[[9],[3,15],[20],[7]]
解释：
列 -1 ：只有结点 9 在此列中。
列  0 ：只有结点 3 和 15 在此列中，按从上到下顺序。
列  1 ：只有结点 20 在此列中。
列  2 ：只有结点 7 在此列中。
示例 2：

![图2](./images/vertical-order-traversal-of-a-binary-tree2.jpg)


输入：root = [1,2,3,4,5,6,7]
输出：[[4],[2],[1,5,6],[3],[7]]
解释：
列 -2 ：只有结点 4 在此列中。
列 -1 ：只有结点 2 在此列中。
列  0 ：结点 1 、5 和 6 都在此列中。
          1 在上面，所以它出现在前面。
          5 和 6 位置都是 (2, 0) ，所以按值从小到大排序，5 在 6 的前面。
列  1 ：只有结点 3 在此列中。
列  2 ：只有结点 7 在此列中。
示例 3：

![图3](./images/vertical-order-traversal-of-a-binary-tree3.jpg)


输入：root = [1,2,3,4,6,5,7]
输出：[[4],[2],[1,5,6],[3],[7]]
解释：
这个示例实际上与示例 2 完全相同，只是结点 5 和 6 在树中的位置发生了交换。
因为 5 和 6 的位置仍然相同，所以答案保持不变，仍然按值从小到大排序。
 

提示：

树中结点数目总数在范围 [1, 1000] 内
0 <= Node.val <= 1000


### 思路
1. 前序遍历，以列号为key，将同一col的节点以`[[row,val]]`的形式，保存在散列表中
2. 遍历散列表的值，以key从小到大排序。
3. 排好序后的结果，即为从左到右的垂序遍历结果。
4. 但是还要解决，同一列中，同一行的元素要从小到大排序的问题，因此需要再一次排序


### 代码
```javascript
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var verticalTraversal = function (root) {
    let obj = {};
    let preOrder = function (node, row, col) {
        if (!node) return;
        if (obj[col]) {
            obj[col].push([row, node.val]);
        } else {
            obj[col] = [[row, node.val]];
        }
        preOrder(node.left, row + 1, col - 1);
        preOrder(node.right, row + 1, col + 1);
    }
    preOrder(root, 0, 0);//前序遍历，以列号为key，将同一col的节点以`[[row,val]]`的形式，保存在散列表中

    return Object.keys(obj).sort((a, b) => parseInt(a) - parseInt(b))//将列号从小到大排序
            .map(key => obj[key])
            .map(item=>{//如果同一列中有多个节点，接着排序
                if(item.length>0){
                    item = item.sort((a, b) => {//如果行号不同，则按行号从小到大排序
                        if (a[0] > b[0]) {
                            return 1
                        } else if (a[0] < b[0]) {
                            return -1
                        } else {//如果行号相同，则按照val从小到大排序
                            return a[1] - b[1]
                        }
                    })
                }
                return item
            })
            .map(item => item.map(item => item[1]))
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(nlogn) 排序的复杂度
- 空间复杂度：O(n) 