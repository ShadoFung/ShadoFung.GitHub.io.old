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
- 数据序列1： 13-17-20-42-28 利用插入排序，13-17-20-28-42. Number of swap:1;
- 数据序列2： 13-17-20-42-14 利用插入排序，13-14-17-20-42. Number of swap:3;
- 如果数据序列基本有序，使用插入排序会更加高效。
#### 2.基本思想 ####
- 在要排序的一组数中，根据某一增量分为若干子序列，并对子序列分别进行插入排序。
- 然后逐渐将增量减小,并重复上述过程。直至增量为1,此时数据序列基本有序,最后进行插入排序。
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

## 三、选择排序 ##
#### 1.基本思想 ####
- 在长度为N的无序数组中，第一次遍历n-1个数，找到最小的数值与第一个元素交换；
- 第二次遍历n-2个数，找到最小的数值与第二个元素交换；
- 。。。
- 第n-1次遍历，找到最小的数值与第n-1个元素交换，排序完成。
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
#### ①图示： （88,85,83,73,72,60,57,48,42,6） ####
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/heap_sort_2.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/heap_sort_2.png"></a>
	<figcaption>HeapSort</figcaption>
</figure>
#### 2.平均时间复杂度：O(n㏒n) ####
由于每次重新恢复堆的时间复杂度为O(n㏒n)，共n - 1次重新恢复堆操作，再加上前面建立堆时n / 2次向下调整，每次调整时间复杂度也为O(n㏒n)。二次操作时间相加还是O(n㏒n)。
#### 3.Java代码实现 ####
{% highlight java %}
//构建最小堆
public static void MakeMinHeap(int a[], int n){
 for(int i=(n-1)/2 ; i>=0 ; i--){
     MinHeapFixdown(a,i,n);
 }
}
//从i节点开始调整,n为节点总数 从0开始计算 i节点的子节点为 2*i+1, 2*i+2  
public static void MinHeapFixdown(int a[],int i,int n){

   int j = 2*i+1; //子节点
   int temp = 0;

   while(j<n){
       //在左右子节点中寻找最小的
       if(j+1<n && a[j+1]<a[j]){   
           j++;
       }

       if(a[i] <= a[j])
           break;

       //较大节点下移
       temp = a[i];
       a[i] = a[j];
       a[j] = temp;

       i = j;
       j = 2*i+1;
   }
}
public static void MinHeap_Sort(int a[],int n){
  int temp = 0;
  MakeMinHeap(a,n);

  for(int i=n-1;i>0;i--){
      temp = a[0];
      a[0] = a[i];
      a[i] = temp; 
      MinHeapFixdown(a,0,i);
  }     
}
{% endhighlight %}
## 五、冒泡排序(BubbleSort) ##
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
- 数据的顺序排好之后，冒泡算法仍然会继续进行下一轮的比较，直到arr.length-1次，后面的比较没有意义的。
2. **方案：**
- 设置标志位flag，如果发生了交换flag设置为true；如果没有交换就设置为false。
- 这样当一轮比较结束后如果flag仍为false，即：这一轮没有发生交换，说明数据的顺序已经排好，没有必要继续进行下去。
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
## 六、快速排序 ##
## 七、归并排序 ##
## 八、基数排序 ##