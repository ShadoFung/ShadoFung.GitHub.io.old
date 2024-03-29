---
layout: post
title: "七大查找算法汇总"
date: 2016-08-08
excerpt: "查找是在大量的信息中寻找一个特定的信息元素，在计算机应用中，查找是常用的基本运算，例如编译程序中符号表的查找。"
tags: [算法, java]
comments: true
---
1.顺序查找  
2.二分查找  
3.插值查找  
4.斐波那契查找  
5.树表查找  
6.分块查找  
7.哈希查找

查找是在大量的信息中寻找一个特定的信息元素，在计算机应用中，查找是常用的基本运算，例如编译程序中符号表的查找。本文简单概括性的介绍了常见的七种查找算法，说是七种，其实二分查找、插值查找以及斐波那契查找都可以归为一类——插值查找。插值查找和斐波那契查找是在二分查找的基础上的优化查找算法。  
**查找定义：**根据给定的某个值，在查找表中确定一个其关键字等于给定值的数据元素（或记录）。  
**查找算法分类：**  
（1）静态查找和动态查找；  
	注：静态或者动态都是针对查找表而言的。动态表指查找表中有删除和插入操作的表。  
（2）无序查找和有序查找。  
	无序查找：被查找数列有序无序均可；  
	有序查找：被查找数列必须为有序数列。  
**平均查找长度（Average Search Length，ASL）：**需和指定key进行比较的关键字的个数的期望值，称为查找算法在查找成功时的平均查找长度。  
对于含有n个数据元素的查找表，查找成功的平均查找长度为：ASL = Pi*Ci的和。  
Pi：查找表中第i个数据元素的概率。  
Ci：找到第i个数据元素时已经比较过的次数。  