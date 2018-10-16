---
layout: post
title: java的排序算法
date: 2018-10-12 10:00:00 +0300
description: 数组常用的几种排序方式
img: preview.png # Add image post (optional)
tags: [java] # add tag
---

# 1.概述
  排序算法分为内部排序和外部排序，内部排序把数据记录放在内存中进行排序，
而外部排序因排序的数据量大，内存不能一次容纳全部的排序记录，所以在排序过程中需要访问外存。
![](https://user-gold-cdn.xitu.io/2018/9/10/165c15fba21994d3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

## 冒泡排序
冒泡排序（Bubble Sort）是一种简单的排序算法。它重复访问要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。
访问数列的工作是重复地进行直到没有再需要交换的数据，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢“浮”到数列的顶端，像水中的气泡从水底浮到水面。
{% highlight java linenos %}
public class SortFunction
{
    public static int[] fun1 (int[] array){
        for(int i=0; i<array.length-1; i++){
            for(int j=0; j<array.length-1-i; j++){
                if(array[j] > array[j+1]){
                    //将值较大的存到临时变量中
                    int temp = array[j];
                    //把值较小的赋给前一个位置
                    array[j] = array[j+1];
                    //把值较大的赋给后一个位置，实现每次比较后，都把大的值往后移
                    array[j+1] = temp;
                }
            }
        }
        return array;
    }
    
    public static void main(String[] args)
    {
        int[] array = {5,4,7,9,10,2};
        int[] nums = fun1(array);
        for (int i : nums)
        {
            System.out.print(i+" ");
        }
    }
}
{% endhighlight %}
输出结果：
{% highlight cmd %}
2 4 5 7 9 10 
{% endhighlight %}

## 2.二分法排序





