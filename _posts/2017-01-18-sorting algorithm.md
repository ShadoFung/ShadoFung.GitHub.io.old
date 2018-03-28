---
layout: post
title: "八大排序"
date: 2017-01-18
excerpt: "八大常用排序算法"
tags: [算法]
comments: true
---
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/sorting.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/sorting.png"></a>
</figure>

## 一、插入排序 ##
#### 1.基本思想 ####
在要排序的一组数中，假定前n-1个数已经排好序，现在将第n个数插到前面的有序数列中，使得这n个数也是排好顺序的。如此反复循环，直到全部排好顺序。
#### 2.过程 ####
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/insertion_sort_1.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/insertion_sort_1.png"></a>
	<figcaption>插入排序</figcaption>
</figure>
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/insertion_sort_2.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/insertion_sort_2.png"></a>
	<figcaption>相同的场景</figcaption>
</figure>
#### 3.平均时间复杂度 O(n²) ####
#### 4.Java代码实现 ####
{% highlight java %}
public static void  insert_sort(int array[],int lenth){

   int temp;

   for(int i=0;i<lenth-1;i++){
       for(int j=i+1;j>0;j--){
           if(array[j] < array[j-1]){
               temp = array[j-1];
               array[j-1] = array[j];
               array[j] = temp;
           }else{         //不需要交换
               break;
           }
       }
   }
}
{% endhighlight %}

## 二、希尔排序 ##
#### 1.前言 ####
数据序列1： 13-17-20-42-28 利用插入排序，13-17-20-28-42. Number of swap:1;
数据序列2： 13-17-20-42-14 利用插入排序，13-14-17-20-42. Number of swap:3;
如果数据序列基本有序，使用插入排序会更加高效。
#### 2.基本思想 ####
在要排序的一组数中，根据某一增量分为若干子序列，并对子序列分别进行插入排序。
然后逐渐将增量减小,并重复上述过程。直至增量为1,此时数据序列基本有序,最后进行插入排序。
#### 3.过程 ####
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/shell_sort_1.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/shell_sort_1.png"></a>
	<figcaption>希尔排序</figcaption>
</figure>
#### 4.平均时间复杂度 O(n^1.3) ####
#### 5.Java代码实现 ####
{% highlight java %}
public static void shell_sort(int array[],int lenth){

   int temp = 0;
   int incre = lenth;

   while(true){
       incre = incre/2;

       for(int k = 0;k<incre;k++){    //根据增量分为若干子序列

           for(int i=k+incre;i<lenth;i+=incre){

               for(int j=i;j>k;j-=incre){
                   if(array[j]<array[j-incre]){
                       temp = array[j-incre];
                       array[j-incre] = array[j];
                       array[j] = temp;
                   }else{
                       break;
                   }
               }
           }
       }

       if(incre == 1){
           break;
       }
   }
}
{% enhighlight %}

## 三、选择排序 ##
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

## 四、堆排序(HeapSort) ##
#### 1.基本思想 ####
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/heap_sort_1.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/heap_sort_1.png"></a>
	<figcaption>堆排序</figcaption>
</figure>
## 五、冒泡排序 ##
## 六、快速排序 ##
## 七、归并排序 ##
## 八、基数排序 ##