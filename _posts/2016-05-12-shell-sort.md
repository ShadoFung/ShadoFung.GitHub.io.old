---
layout: post
title: "二、希尔排序"
date: 2016-05-04
excerpt: "希尔排序(Shell's Sort)是插入排序的一种又称“缩小增量排序”（Diminishing Increment Sort），是直接插入排序算法的一种更高效的改进版本。希尔排序是非稳定排序算法。该方法因D.L.Shell于1959年提出而得名。"
tags: [算法, java]
comments: true
---
## 希尔排序(Shell Sort) ##
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
{% endhighlight %}