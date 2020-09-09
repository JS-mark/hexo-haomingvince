---
title: 各种排序算法总结
date: 2020-09-08 16:48:53
tags: 
- 排序
- 算法
categories:
- 算法
---

## 各种排序算法总结

本文主要是为了总结各种算法的写法，复杂度，以及稳定性分析，主要是个人做个记录，如果有任何需要修改或优化的地方欢迎在评论区留言哦！

### 排序算法时间、空间、稳定性表

|   算法  |   最好  |  最坏   |  平均   |  空间   |  稳定性 |
| --- | --- | --- | --- | --- | :---: |
|  冒泡排序  |  O(n)   |   O(n<sup>2</sup>)  |  O(n<sup>2</sup>)   |  O(1)   | 稳定  |
|  选择排序  |  O(n<sup>2</sup>)  |   O(n<sup>2</sup>)  |  O(n<sup>2</sup>)   |  O(1)  | 不稳定 |
|  插入排序  |  O(n)   |   O(n<sup>2</sup>)  |  O(n<sup>2</sup>)   |  O(1)   | 稳定  |
|  快速排序  |  O(nlog n)   |  O(n<sup>2</sup>)   |  O(nlog n)   |  O(log n)-O(n)   | 不稳定 |
|  归并排序  |  O(nlog n)   |   O(nlog n)  |  O(nlog n)   |   O(n)  |  稳定   |
|  希尔排序  |  O(n^1.3)   |   O(n<sup>2</sup>)  |  O(nlog n)-O(n<sup>2</sup>)   |  O(1)   | 不稳定    |
|  计数排序  |  O(n+k)   |   O(n+k)  |   O(n+k)  |  O(n+k)   |  稳定   |
|  基数排序  |   O(nk)  |  O(nk)   |   O(nk)  |   O(n+k)  |  稳定   |
|  桶排序    |   O(n)  |   O(n)  |   O(n)  |  O(n+m)   |  稳定   |
|  堆排序    |  O(nlog n)   |   O(nlog n)  |  O(nlog n)   |   O(1)  |  不稳定   |

注：稳定性是指：假定在待排序的记录序列中，存在多个具有**相同的关键字**的记录，若经过排序，这些记录的**相对次序**保持不变，即在原序列中，ri=rj，且ri在rj之前，而在排序后的序列中，ri仍在rj之前，则称这种排序算法是稳定的；否则称为不稳定的。

## 冒泡排序 Bubble Sort

### 概述

作为本人踏入算法殿堂学习的第一个排序算法，冒泡排序可以算是经典算法之一了，它的基本思想是：***<u>两个数比较大小，较大的数下沉，较小的数冒起来</u>***。

### Python 算法实现

```Python
def bubble(array):
    for i in range(len(array)):
        for j in range(len(array)-i-1):
            if array[j] > array[j+1]:  #判断大小，大的排在后面
                array[j], array[j+1] = array[j+1], array[j]
    return array
```

### 复杂度

平均时间复杂度 O(n<sup>2</sup>)

## 选择排序 Selection Sort

### 概述

在长度为n的无序数组中，第一次遍历n-1个数，找到最小的数值与第一个元素交换；  
第二次遍历n-2个数，找到最小的数值与第二个元素交换；  
。。。  
第n-1次遍历，找到最小的数值与第n-1个元素交换，排序完成。

### Python 算法实现

```python
def selection(array):
    for i in range(len(array)):
        low = i
        for j in range(i+1, len(array)):
            if array[j] < array[low]:
                low = j
        array[i], array[low] = array[low], array[i]
    return array
```

### 复杂度

平均时间复杂度 O(n<sup>2</sup>)

## Reference

[排序算法总结 | 菜鸟教程](https://www.runoob.com/w3cnote/sort-algorithm-summary.html)

[排序算法的稳定性及其意义_u012501054的博客-CSDN博客](https://blog.csdn.net/u012501054/article/details/79342580)