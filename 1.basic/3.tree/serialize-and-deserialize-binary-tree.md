# 算法题 297. 二叉树的序列化与反序列化
[leetcode 地址](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

## 题目描述

序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

提示: 输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 LeetCode 序列化二叉树的格式。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

 

示例 1：
![图1](./images/serialize-and-deserialize-binary-tree1.jpg)


输入：root = [1,2,3,null,null,4,5]
输出：[1,2,3,null,null,4,5]
示例 2：

输入：root = []
输出：[]
示例 3：

输入：root = [1]
输出：[1]
示例 4：

输入：root = [1,2]
输出：[1,2]


提示：

树中结点数在范围 [0, 104] 内
-1000 <= Node.val <= 1000

### 思路
1. dfs，前序遍历
2. 序列化时，将当前节点值并入字符串，用‘，’隔开，null也是
3. 反序列化时，将字符串从'，'处隔开，数组的第一个值就是当前节点，第二个值是当前节点的左侧子节点，第三个值就是右侧
4. 递归即可


### 代码
```javascript

/**
 * Encodes a tree to a single string.
 *
 * @param {TreeNode} root
 * @return {string}
 */
var serialize = function (root) {
    let str = "";
    var dfs = function (root) {
        if (!root) {
            str += ",null";
            return;
        }
        str += `,${root.val}`;
        dfs(root.left);
        dfs(root.right);
    };
    dfs(root);
    return str.slice(1);
};

/**
 * Decodes your encoded data to tree.
 *
 * @param {string} data
 * @return {TreeNode}
 */
var deserialize = function (data) {
    let list = data.split(",");
    var dfs = function (str) {
        if (str[0] === "null") {
            str.shift();
            return null;
        }
        let node = new TreeNode(str[0]);
        str.shift();
        node.left = dfs(str);
        node.right = dfs(str);
        return node;
    };
    return dfs(list);
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n)
- 空间复杂度：O(h)