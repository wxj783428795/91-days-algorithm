# 算法题 30. 串联所有单词的子串
[leetcode 地址](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/)

## 题目描述

```
给定一个字符串 s 和一些 长度相同 的单词 words 。找出 s 中恰好可以由 words 中所有单词串联形成的子串的起始位置。

注意子串要与 words 中的单词完全匹配，中间不能有其他字符 ，但不需要考虑 words 中单词串联的顺序。

 

示例 1：

输入：s = "barfoothefoobarman", words = ["foo","bar"]
输出：[0,9]
解释：
从索引 0 和 9 开始的子串分别是 "barfoo" 和 "foobar" 。
输出的顺序不重要, [9,0] 也是有效答案。
示例 2：

输入：s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
输出：[]
示例 3：

输入：s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
输出：[6,9,12]
 

提示：

1 <= s.length <= 104
s 由小写英文字母组成
1 <= words.length <= 5000
1 <= words[i].length <= 30
words[i] 由小写英文字母组成

```

### 思路
1. 将words中单词和出现的次数以key和value存入一个map中。
2. 遍历s，截取words中所有字符的总长度的子字符串。
3. 遍历子字符串，去除子字符串中的单词，判断其在不在第一个map中，如果在，就将单词和出现次数存入第二个map中。如果不在，则直接跳过，进入下一次循环。
4. 比较map1和map2的key，value是否相同，如果相同，则记录当前下标。

### 代码
```javascript
/**
 * @param {string} s
 * @param {string[]} words
 * @return {number[]}
 */
var findSubstring = function (s, words) {
    //遍历words，将单词和出现的次数存入map中
    let map1 = {};
    let ans = []
    for (let word of words) {
        if (map1[word] === undefined) {
            map1[word] = 1;
        } else {
            map1[word] += 1;
        }
    }
    let length = words.join('').length;
    for (let i = 0; i < s.length - length + 1; i++) {
        let subStr = s.slice(i, i + length);
        let map2 = {};
        let subStrWords = [];
        for (let j = 0; j < words.length; j++) {
            let subStrWord = subStr.slice(j * words[0].length, (j + 1) * words[0].length);
            if (map1[subStrWord] === undefined) {
                break;
            } else {
                subStrWords.push(subStrWord);
                if (map2[subStrWord] === undefined) {
                    map2[subStrWord] = 1;
                } else {
                    map2[subStrWord] += 1;
                }
            }
        }
        if (subStrWords.length === words.length) {
            let flag = true;
            for (let k = 0; k < subStrWords.length; k++) {
                if (map1[subStrWords[k]] !== map2[subStrWords[k]]) {
                    flag = false;
                    break;
                }
            }
            if (flag) {
                ans.push(i)
            }
        }
    }
    return ans;
};
```
### 复杂度分析
**复杂度分析不是很会，不一定对，如果有错，请指正。**
- 时间复杂度：O(n*m) n为s的长度，m为words数组的长度
- 空间复杂度：O(m) 