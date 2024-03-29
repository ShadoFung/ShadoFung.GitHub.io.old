---
layout: post
title: "六、分块查找"
date: 2016-07-25
excerpt: "分块查找是折半查找和顺序查找的一种改进方法，分块查找由于只要求索引表是有序的，对块内节点没有排序要求，因此特别适合于节点动态变化的情况。"
tags: [算法, java]
comments: true
---
## 分块查找 ##
分块查找又称索引顺序查找，它是顺序查找的一种改进方法。 
 
**算法思想：**将n个数据元素"按块有序"划分为m块（m ≤ n）。每一块中的结点不必有序，但块与块之间必须"按块有序"；即第1块中任一元素的关键字都必须小于第2块中任一元素的关键字；而第2块中任一元素又都必须小于第3块中的任一元素，……

**算法流程：**  
step1 先选取各块中的最大关键字构成一个索引表；  
step2 查找分两个部分：先对索引表进行二分查找或顺序查找，以确定待查记录在哪一块中；然后，在已确定的块中用顺序法进行查找。  