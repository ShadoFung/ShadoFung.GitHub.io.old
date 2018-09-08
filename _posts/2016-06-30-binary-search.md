---
layout: post
title: "二、二分查找"
date: 2016-06-24
excerpt: "二分查找也称折半查找（Binary Search），它是一种效率较高的查找方法。但是，折半查找要求线性表必须采用顺序存储结构，而且表中元素按关键字有序排列。"
tags: [算法, java]
comments: true
---
## 2.二分查找 ##
**说明：元素必须是有序的，如果是无序的则要先进行排序操作。**

**基本思想：**也称为是折半查找，属于有序查找算法。用给定值k先与中间结点的关键字比较，中间结点把线形表分成两个子表，若相等则查找成功；若不相等，再根据k与该中间结点关键字的比较结果确定下一步查找哪个子表，这样递归进行，直到查找到或查找结束发现表中没有这样的结点。

**复杂度分析：最坏情况下，关键词比较次数为log2(n+1)，且期望时间复杂度为O(log2n)；**

**注：折半查找的前提条件是需要有序表顺序存储，对于静态查找表，一次排序后不再变化，折半查找能得到不错的效率。但对于需要频繁执行插入或删除操作的数据集来说，维护有序的排序会带来不小的工作量，那就不建议使用。——《大话数据结构》**

**Java代码实现**
{% highlight java %}
//二分查找 版本1 循环
public int BinarySearch1(int a[], int value, int n) {
    int low, high, mid;
    low = 0;
    high = n-1;
    while(low<=high) {
        mid = (low+high)/2;
        if(a[mid]==value) {
            return mid;
		}
        if(a[mid]>value) {
            high = mid-1;
		}
        if(a[mid]<value) {
            low = mid+1;
		}
    }
    return -1;
}

//二分查找，递归版本
public int BinarySearch2(int a[], int value, int low, int high)
{
    int mid = low+(high-low)/2;
    if(a[mid]==value) {
        return mid;
	}
    if(a[mid]>value) {
        return BinarySearch2(a, value, low, mid-1);
	}
    if(a[mid]<value) {
        return BinarySearch2(a, value, mid+1, high);
	}
}
{% endhighlight %}