---
title: 数据结构基础知识
date: 2019-06-12 15:38:58
categories:
- data
tags:
- backend
---
数组的特点：
1. 同等大小元素组成的连续的内存区域，索引是连续的整数。
2. O(1)访问任意数组的元素
3. O(1)增加或移除最末尾的元素
4. O(n)增加或移除任意位置的元素

链表的特点：
1. O(1)从第一个开始插入或移除元素
2. 对于双端链表，O(1)从最后开始插入或移除元素
3. O(n)的时间找到任意的元素
4. 元素没有必要是连续的
5. 用双端链表插入和移除的时间复杂度是O(1)

## 二叉树
1. 深度优先 - 优先遍历子树，然后再遍历相邻的兄弟节点。(traverse one subtree before exploring a sibling tree)
2. 广度优先 - 按照树的层级，逐级进行遍历。(travserse one level before processing to next level)



