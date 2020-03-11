---
title: HashMap中的红黑树
tags:
  - 阅读源码
categories: 学习笔记
date: 2019-10-21 13:26:13
---

> 阅读java api源码，可以学到很多的设计模式，优秀的算法实现


# 前言
jdk8之前没有使用红黑树，出现哈希冲突采用哈希桶解决，当哈希冲突过多时会出现效率问题，jdk8采用红黑树，默认当哈希桶链表长度达到8时将链表转化成树，提高操作效率
<!-- more -->
# 红黑树
红黑树是什么？有什么优势？
## 什么是红黑树

摘自百科

> 红黑树（Red Black Tree） 是一种自平衡二叉查找树，是在计算机科学中用到的一种数据结构，典型的用途是实现关联数组。
它是在1972年由Rudolf Bayer发明的，当时被称为平衡二叉B树（symmetric binary B-trees）。后来，在1978年被 Leo J. Guibas 和 Robert Sedgewick 修改为如今的“红黑树”。
红黑树和AVL树类似，都是在进行插入和删除操作时通过特定操作保持二叉查找树的平衡，从而获得较高的查找性能。
它虽然是复杂的，但它的最坏情况运行时间也是非常良好的，并且在实践中是高效的： 它可以在O(log n)时间内做查找，插入和删除，这里的n 是树中元素的数目。

## 性质

红黑树不仅是二叉查找树，它还必须满足以下5个性质

- 节点非黑即红
- 根节点是黑色
- 每个叶节点（NIL节点，空节点）是黑色的
- 每个红色节点的两个子节点都是黑色(从每个叶子到根的所有路径上不能有两个连续的红色节点)
- 从任一节点到其每个叶子的所有路径都包含相同数目的黑色节点

相比于平衡二叉树(avl),红黑树追求的是 **相对平衡**

红黑树的效率相对较高，所以它被用来存储相关数据，基本的操作有增加/删除/查找，在这些操作之后可能会破坏红黑树的性质，所以需要相关操作来维护以让红黑树符合上面的性质要求。

## 左旋右旋

对红黑树进行插入，删除等操作后，会导致不满足红黑树的条件，所以需要进行调整

- 左旋

> 将x的右子树绕x逆时针旋转，使得x的右子树成为x的父亲，并修改相关引用。

- 右旋

> 是将x的左子树绕x顺时针旋转，使得x的左子树成为x的父亲，并修改相关的引用。