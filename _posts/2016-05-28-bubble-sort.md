---
layout: post
title: "五、冒泡排序"
date: 2016-05-28
excerpt: "冒泡排序（Bubble Sort），是一种计算机科学领域的较简单的排序算法。这个算法的名字由来是因为越大的元素会经由交换慢慢“浮”到数列的顶端（升序或降序排列），就如同碳酸饮料中二氧化碳的气泡最终会上浮到顶端一样，故名“冒泡排序”。"
tags: [算法, java]
comments: true
---
## 冒泡排序(Bubble Sort) ##
#### 1.基本思想 ####
两个数比较大小，较大的数下沉，较小的数冒起来。
#### 2.过程 ####
1. 比较相邻的两个数据，如果第二个数小，就交换位置。
2. 从后向前两两比较，一直到比较最前两个数据。最终最小数被交换到起始的位置，这样第一个最小数的位置就排好了。
3. 继续重复上述过程，依次将第2.3...n-1个最小数排好位置。
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/bubble_sort_1.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/bubble_sort_1.png"></a>
	<figcaption>冒泡排序</figcaption>
</figure>
#### 3.平均时间复杂度 O(n²) ####
#### 4.Java代码实现 ####
{% highlight java %}
public static void BubbleSort(int [] arr){

     int temp;//临时变量
     for(int i=0; i<arr.length-1; i++){   //表示趟数，一共arr.length-1次。
         for(int j=arr.length-1; j>i; j--){

             if(arr[j] < arr[j-1]){
                 temp = arr[j];
                 arr[j] = arr[j-1];
                 arr[j-1] = temp;
             }
         }
     }
}
{% endhighlight %}
#### 5.优化 ####
1. **针对问题：**  
数据的顺序排好之后，冒泡算法仍然会继续进行下一轮的比较，直到arr.length-1次，后面的比较没有意义的。
2. **方案：**  
设置标志位flag，如果发生了交换flag设置为true；如果没有交换就设置为false。  
这样当一轮比较结束后如果flag仍为false，即：这一轮没有发生交换，说明数据的顺序已经排好，没有必要继续进行下去。  
{% highlight java %}
public static void BubbleSort1(int [] arr){

   int temp;//临时变量
   boolean flag;//是否交换的标志
   for(int i=0; i<arr.length-1; i++){   //表示趟数，一共arr.length-1次。

       flag = false;
       for(int j=arr.length-1; j>i; j--){

           if(arr[j] < arr[j-1]){
               temp = arr[j];
               arr[j] = arr[j-1];
               arr[j-1] = temp;
               flag = true;
           }
       }
       if(!flag) break;
   }
}
{% endhighlight %}