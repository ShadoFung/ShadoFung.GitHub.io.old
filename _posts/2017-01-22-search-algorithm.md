---
layout: post
title: "七大查找算法"
date: 2017-01-22
excerpt: "七大常用查找算法"
tags: [算法, java]
comments: true
---
1. 顺序查找
2. 二分查找
3. 插值查找
4. 斐波那契查找
5. 树表查找
6. 分块查找
7. 哈希查找
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
## 1.顺序查找 ##
**说明：顺序查找适合于存储结构为顺序存储或链接存储的线性表。**

**基本思想：**顺序查找也称为线形查找，属于无序查找算法。从数据结构线形表的一端开始，顺序扫描，依次将扫描到的结点关键字与给定值k相比较，若相等则表示查找成功；若扫描结束仍没有找到关键字等于k的结点，表示查找失败。  

**复杂度分析：**查找成功时的平均查找长度为：（假设每个数据元素的概率相等） ASL = 1/n(1+2+3+…+n) = (n+1)/2 ;  

当查找不成功时，需要n+1次比较，时间复杂度为O(n);  
所以，顺序查找的时间复杂度为O(n)。
**Java代码实现**
{% highlight java %}
//顺序查找
public int SequenceSearch(int a[], int value, int n) {
    int i;
    for(i=0; i<n; i++) {
        if(a[i]==value) {
            return i;
		}
	}
    return -1;
}
{% endhighlight %}
## 2.二分查找 ##
**说明：元素必须是有序的，如果是无序的则要先进行排序操作。**

**基本思想：**也称为是折半查找，属于有序查找算法。用给定值k先与中间结点的关键字比较，中间结点把线形表分成两个子表，若相等则查找成功；若不相等，再根据k与该中间结点关键字的比较结果确定下一步查找哪个子表，这样递归进行，直到查找到或查找结束发现表中没有这样的结点。

复杂度分析：最坏情况下，关键词比较次数为log2(n+1)，且期望时间复杂度为O(log2n)；

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
## 3.插值查找 ##
在介绍插值查找之前，首先考虑一个新问题，为什么上述算法一定要是折半，而不是折四分之一或者折更多呢？  

打个比方，在英文字典里面查“apple”，你下意识翻开字典是翻前面的书页还是后面的书页呢？如果再让你查“zoo”，你又怎么查？很显然，这里你绝对不会是从中间开始查起，而是有一定目的的往前或往后翻。  
同样的，比如要在取值范围1 ~ 10000 之间 100 个元素从小到大均匀分布的数组中查找5， 我们自然会考虑从数组下标较小的开始查找。  
经过以上分析，折半查找这种查找方式，不是自适应的（也就是说是傻瓜式的）。二分查找中查找点计算如下：  
mid=(low+high)/2, 即mid=low+1/2*(high-low);  
通过类比，我们可以将查找的点改进为如下：  
mid=low+(key-a[low])/(a[high]-a[low])*(high-low)，  
也就是将上述的比例参数1/2改进为自适应的，根据关键字在整个有序表中所处的位置，让mid值的变化更靠近关键字key，这样也就间接地减少了比较次数。 
 
**基本思想：**基于二分查找算法，将查找点的选择改进为自适应选择，可以提高查找效率。当然，差值查找也属于有序查找。  

**注：对于表长较大，而关键字分布又比较均匀的查找表来说，插值查找算法的平均性能比折半查找要好的多。反之，数组中如果分布非常不均匀，那么插值查找未必是很合适的选择。**  

**复杂度分析：查找成功或者失败的时间复杂度均为O(log2(log2n))。**

**Java代码实现**
{% highlight java %}
//插值查找
public int InsertionSearch(int a[], int value, int low, int high) {
    int mid = low+(value-a[low])/(a[high]-a[low])*(high-low);
    if(a[mid]==value) {
        return mid;
	}
    if(a[mid]>value) {
        return InsertionSearch(a, value, low, mid-1);
	}
    if(a[mid]<value) {
        return InsertionSearch(a, value, mid+1, high);
	}
}
{% endhighlight %}
## 4.斐波那契查找 ##
在介绍斐波那契查找算法之前，我们先介绍一下很它紧密相连并且大家都熟知的一个概念——黄金分割。

黄金比例又称黄金分割，是指事物各部分间一定的数学比例关系，即将整体一分为二，较大部分与较小部分之比等于整体与较大部分之比，其比值约为1:0.618或1.618:1。

0.618被公认为最具有审美意义的比例数字，这个数值的作用不仅仅体现在诸如绘画、雕塑、音乐、建筑等艺术领域，而且在管理、工程设计等方面也有着不可忽视的作用。因此被称为黄金分割。

大家记不记得斐波那契数列：1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89…….（从第三个数开始，后边每一个数都是前两个数的和）。然后我们会发现，随着斐波那契数列的递增，前后两个数的比值会越来越接近0.618，利用这个特性，我们就可以将黄金比例运用到查找技术中。
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/search_algorithm/fibonacci_search_1.jpg"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/search_algorithm/fibonacci_search_1.jpg"></a>
	<figcaption>相同的场景</figcaption>
</figure>