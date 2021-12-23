# 算法题 146. LRU 缓存机制
[leetcode 地址](https://leetcode-cn.com/problems/lru-cache/)

## 题目描述

```
运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制 。
实现 LRUCache 类：

LRUCache(int capacity) 以正整数作为容量 capacity 初始化 LRU 缓存
int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
void put(int key, int value) 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字-值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。
 

进阶：你是否可以在 O(1) 时间复杂度内完成这两种操作？


示例：

输入
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
输出
[null, null, null, 1, null, -1, null, -1, 3, 4]

解释
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // 缓存是 {1=1}
lRUCache.put(2, 2); // 缓存是 {1=1, 2=2}
lRUCache.get(1);    // 返回 1
lRUCache.put(3, 3); // 该操作会使得关键字 2 作废，缓存是 {1=1, 3=3}
lRUCache.get(2);    // 返回 -1 (未找到)
lRUCache.put(4, 4); // 该操作会使得关键字 1 作废，缓存是 {4=4, 3=3}
lRUCache.get(1);    // 返回 -1 (未找到)
lRUCache.get(3);    // 返回 3
lRUCache.get(4);    // 返回 4

提示：

1 <= capacity <= 3000
0 <= key <= 10000
0 <= value <= 105
最多调用 2 * 105 次 get 和 put

```

### 思路
1. 使用双向链表，每次put或get时，都将节点放置于链表head处。
2. 使用map保存链表中的节点。空间换取时间，可以做到O(1)时间去到链表的值。


### 代码
```javascript
/**
 * @param {number} capacity
 */
var LRUCache = function (capacity) {
    this.maxSize = capacity;
    this.size = 0;
    this.head = null;
    this.tail = null;
    this.map = new Map();
};

/** 
 * @param {number} key
 * @return {number}
 */
LRUCache.prototype.get = function (key) {
    let node = this.map.get(key);
    if (node) {
        if (this.head === node) { } else if (this.tail === node) {
            let prev = node.prev;
            prev.next = null;
            this.head.prev = node;
            node.next = this.head;
            this.head = node;
            this.tail = prev;
        } else {
            let prev = node.prev;
            let next = node.next;
            prev.next = next;
            next.prev = prev;
            this.head.prev = node;
            node.next = this.head;
            node.prev = null;
            this.head = node;
        }
        return node.val
    } else {
        return -1
    }
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LRUCache.prototype.put = function (key, value) {
    //先看链表中存不存在这个key;
    if (this.map.get(key)) {
        //如果存在，则更新这个节点
        let node = this.map.get(key);
        node.val = value;
        //将节点放到链表头部
        if (this.head) {
            if (this.head === node) { } else if (this.tail === node) {
                let prev = node.prev;
                prev.next = null;
                this.head.prev = node;
                node.next = this.head;
                node.prev = null;
                this.head = node;
                this.tail = prev;
            } else {
                let prev = node.prev;
                let next = node.next;
                prev.next = next;
                next.prev = prev;
                this.head.prev = node;
                node.next = this.head;
                node.prev = null;
                this.head = node;
            }
        } else {
            this.head = node;
            this.tail = node;
        }
    } else {
        //如果不存在，则创建新节点
        let node = new DoubleLinkedNode(key, value);
        //在map中存储新节点
        this.map.set(key, node)
        //将节点放到链表头部
        if (this.head) {
            this.head.prev = node;
            node.next = this.head;
            this.head = node;
        } else {
            this.head = node;
            this.tail = node;
        }
        //链表长度+1；
        this.size = this.size + 1;
        //判断是否超出容量
        if (this.size > this.maxSize) {
            //如果超出，则将尾节点移除
            //在map中移除尾节点
            this.map.delete(this.tail.key)
            //将链表尾节点往前移一位
            let prev = this.tail.prev;
            prev.next = null;
            this.tail.prev = null;
            this.tail = prev;
            this.size--
        }
    }
};

function DoubleLinkedNode(key, value) {
    this.key = key;
    this.val = value;
    this.prev = null;
    this.next = null;
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * var obj = new LRUCache(capacity)
 * var param_1 = obj.get(key)
 * obj.put(key,value)
 */
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：均为O(1)
- 空间复杂度：O(N)，n为capacity