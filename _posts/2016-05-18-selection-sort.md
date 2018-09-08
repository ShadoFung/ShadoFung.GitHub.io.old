---
layout: post
title: "三、选择排序"
date: 2016-05-18
excerpt: "选择排序（Selection sort）是一种简单直观的排序算法。它的工作原理是每一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，直到全部待排序的数据元素排完。 选择排序是不稳定的排序方法。"
tags: [算法, java]
comments: true
---
## 选择排序(Selction Sort) ##
#### 1.基本思想 ####
在长度为N的无序数组中，第一次遍历n-1个数，找到最小的数值与第一个元素交换；  
第二次遍历n-2个数，找到最小的数值与第二个元素交换；  
。。。  
第n-1次遍历，找到最小的数值与第n-1个元素交换，排序完成。
#### 2.过程 ####
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/selection_sort_1.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/selection_sort_1.png"></a>
	<figcaption>选择排序</figcaption>
</figure>
#### 3.平均时间复杂度 O(n²) ####
#### 4.Java代码实现 ####
{% highlight java %}
public static void select_sort(int array[],int lenth){

   for(int i=0;i<lenth-1;i++){

       int minIndex = i;
       for(int j=i+1;j<lenth;j++){
          if(array[j]<array[minIndex]){
              minIndex = j;
          }
       }
       if(minIndex != i){
           int temp = array[i];
           array[i] = array[minIndex];
           array[minIndex] = temp;
       }
   }
}
{% endhighlight %}