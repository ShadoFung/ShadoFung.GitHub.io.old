---
layout: post
title: "七、归并排序"
date: 2016-06-12
excerpt: "归并排序（MERGE-SORT）是建立在归并操作上的一种有效的排序算法,该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为二路归并。"
tags: [算法, java]
comments: true
---
## 归并排序(Merge Sort) ##
#### 1.基本思想 ####
归并排序是建立在归并操作上的一种有效的排序算法。该算法是采用分治法的一个非常典型的应用。  
首先考虑下如何将2个有序数列合并。这个非常简单，只要从比较2个数列的第一个数，谁小就先取谁，取了后就在对应数列中删除这个数。然后再进行比较，如果有数列为空，那直接将另一个数列的数据依次取出即可。
{% highlight java %}
//将有序数组a[]和b[]合并到c[]中
void MemeryArray(int a[], int n, int b[], int m, int c[])
{
 int i, j, k;

 i = j = k = 0;
 while (i < n && j < m)
 {
     if (a[i] < b[j])
         c[k++] = a[i++];
     else
         c[k++] = b[j++]; 
 }

 while (i < n)
     c[k++] = a[i++];

 while (j < m)
     c[k++] = b[j++];
}
{% endhighlight %}
解决了上面的合并有序数列问题，再来看归并排序，其的基本思路就是将数组分成2组A，B，如果这2组组内的数据都是有序的，那么就可以很方便的将这2组数据进行排序。如何让这2组组内数据有序了？  
可以将A，B组各自再分成2组。依次类推，当分出来的小组只有1个数据时，可以认为这个小组组内已经达到了有序，然后再合并相邻的2个小组就可以了。这样通过**先递归的分解数列，再合并数列**就完成了归并排序。
#### 2.过程 ####
<figure>
	<a href="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/merge_sort_1.png"><img src="https://raw.githubusercontent.com/ShadoFung/ShadoFung.GitHub.io/master/_posts/images/sorting_algorithm/merge_sort_1.png"></a>
	<figcaption>归并排序</figcaption>
</figure>
#### 3.平均时间复杂度 O(n㏒n) ####
归并排序的效率是比较高的，设数列长为n，将数列分开成小数列一共要㏒n步，每步都是一个合并有序数列的过程，时间复杂度可以记为O(n)，故一共为O(n㏒n)。
#### 4.Java代码实现 ####
{% highlight java %}
public static void merge_sort(int a[],int first,int last,int temp[]){

  if(first < last){
      int middle = (first + last)/2;
      merge_sort(a,first,middle,temp);//左半部分排好序
      merge_sort(a,middle+1,last,temp);//右半部分排好序
      mergeArray(a,first,middle,last,temp); //合并左右部分
  }
}
//合并 ：将两个序列a[first-middle],a[middle+1-end]合并
public static void mergeArray(int a[],int first,int middle,int end,int temp[]){     
  int i = first;
  int m = middle;
  int j = middle+1;
  int n = end;
  int k = 0; 
  while(i<=m && j<=n){
      if(a[i] <= a[j]){
          temp[k] = a[i];
          k++;
          i++;
      }else{
          temp[k] = a[j];
          k++;
          j++;
      }
  }     
  while(i<=m){
      temp[k] = a[i];
      k++;
      i++;
  }     
  while(j<=n){
      temp[k] = a[j];
      k++;
      j++; 
  }

  for(int ii=0;ii<k;ii++){
      a[first + ii] = temp[ii];
  }
}
{% endhighlight %}