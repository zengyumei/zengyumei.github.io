---
layout: post
title:  经典排序算法的学习
summary: "经典排序算法的学习"
date:   2019-2-14 20:15:18 +0700
categories: 算法
tags: '算法'
author: 曾宇媚
comment: true
---

## 排序
最近再次重温了以下六种经典的排序算法，并整理出来和大家一起分享。算法都是基于javascript。


### 一、插入排序

> 原理：通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。

1. 步骤：
* 从第一个元素开始，该元素可以认为已经被排序；
* 取出下一个元素，在已经排序的元素序列中从后向前扫描；
* 如果该元素（已排序）大于新元素，将该元素移到下一位置；
* 重复步骤3，直到找到已排序的元素小于或者等于新元素的位置，并将新元素插入到该位置；
* 重复上面的操作，直到排序完成。

2. 实现

```
function insertionSort(arr) {
    var len = arr.length;
    var preIndex, current;
    for (var i=1; i<len; i++) {
        preIndex = i - 1;
        current = arr[i];
        while (preIndex >= 0 && arr[preIndex] > current) {
            arr[preIndex + 1] = arr[preIndex];
            preIndex--;
        }
        arr[preIndex + 1] = current;
    }
    return arr;

```


### 二、选择排序

> 原理：首先在待排序列中找到最小/大的元素，并存放到已排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小/大的元素，然后放到已排序序列的末尾。

1. 步骤：
* 在待排序列中找到最小/大的元素，并存放到已排序序列的起始位置；
* 再从剩余未排序元素中继续寻找最小/大的元素，然后放到已排序序列的末尾；
* 重复上面的操作，直到排序完成。

2. 实现

```
function selectionSort(arr) {
    var len = arr.length;
    var minIndex, temp;
    for (var i=0; i<len-1; i++) {
        minIndex = i;
        for (var j=i+1; j<len; j++) {
            if (arr[j] < arr[minIndex]) {     // 寻找最小值
                minIndex = j;                 // 保存最小值的索引
            }
        }
        temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
    return arr;
} 
```


### 三、冒泡排序

> 原理：冒泡排序的原理很简单，它重复地走过要排序的数列，一次比较相邻的两个元素，如果它们的顺序错误就把它们交换过来。

1. 步骤：
* 从待排序列第一位开始比较相邻的两个元素，如果前面的比后面的大，就进行交换；
* 对相邻的每一对元素作同样的工作，一直到结尾的最后一对，这时最后一个元素就是整个待排序列的最大值；
* 重复上面的操作，直到排序完成。

2. 实现

```
function bubbleSort(arr) {
    var len = arr.length;
    for (var i=0; i<len-1; i++) {
        for (var j = 0; j<len-1; j++) {
            if (arr[j] > arr[j+1]) {   // 相邻两元素比较
                var temp = arr[j+1];   // 前者比后者大，交换顺序
                arr[j+1] = arr[j];
                arr[j] = temp;
            }
        }
    }
    return arr;
}
```


### 四、快速排序

> 原理：通过一趟排序将待排记录分隔成独立的两部分，其中一部分记录的关键字均比另一部分的关键字小，则可分别对这两部分记录继续进行排序，以达到整个序列有序。

1. 步骤：
* 从待排序列中挑出一个元素作为基准数；
* 分区：重新排序数列，所有比基准值小的元素放在基准左边，所有比基准值大的元素放在基准的右边；
* 再对左右区间重复第二步，直到各区间只有一个数。

2. 实现

```
function quickSort(arr){
	var len = arr.length;
    if (len <= 1) {
        return arr;
    }
    var left = [], right=[];
    var index = Math.floor(len/2);
    var num = arr.splice(index,1);
    for (var i=0; i<len; i++) {
        if (arr[i]<num) {
            left.push(arr[i]);
        }else{
            right.push(arr[i]);
        }
    }
    return quickSort(left).concat(num,quickSort(right))
}
```


### 五、归并排序

> 原理：将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。

1. 步骤：
* 把长度为n的输入序列分成两个长度为n/2的子序列；
* 对这两个子序列分别采用归并排序；
* 将两个排序好的子序列合并成一个最终的排序序列。

2. 实现

```
function mergeSort(arr) {  // 采用自上而下的递归方法
    var len = arr.length;
    if (len < 2) {
        return arr;
    }
    var middle = Math.floor(len/2),
        left = arr.slice(0, middle),
        right = arr.slice(middle);
    return merge(mergeSort(left), mergeSort(right));
}
 
function merge(left, right) {
    var result = [];
 
    while (left.length>0 && right.length>0) {
        if (left[0] <= right[0]) {
            result.push(left.shift());
        } else {
            result.push(right.shift());
        }
    }
 
    while (left.length)
        result.push(left.shift());
 
    while (right.length)
        result.push(right.shift());
 
    return result;
}
```


### 六、堆排序

> 原理：采用二叉堆的数据结构来实现的。二叉堆是一个近似完全二叉树，子结点的键值或索引总是小于（或者大于）它的父节点。

1. 步骤：
* 将初始待排序列构建成一个大顶堆，此堆为初始的无序区；
* 将堆顶元素R[1]与最后一个元素R[n]交换，此时得到新的无序区(R1,R2,……Rn-1)和新的有序区(Rn)；
* 由于交换后新的堆顶R[1]可能违反堆的性质，因此需要对当前无序区(R1,R2,……Rn-1)调整为新堆；
* 然后再次将R[1]与无序区最后一个元素交换，得到新的无序区(R1,R2….Rn-2)和新的有序区(Rn-1,Rn)；
* 不断重复此过程直到有序区的元素个数为n-1，排序完成。

2. 实现

```
// 建立大顶堆
function buildMaxHeap(arr) {   
    len = arr.length;
    for (var i = Math.floor(len/2); i >= 0; i--) {
        adjustHeap(arr, i);
    }
}

// 堆调整
function adjustHeap(arr, i) {     
    var left = 2 * i + 1,
        right = 2 * i + 2,
        largest = i;
 
    if (left < len && arr[left] > arr[largest]) {
        largest = left;
    }
 
    if (right < len && arr[right] > arr[largest]) {
        largest = right;
    }
 
    if (largest != i) {
        swap(arr, i, largest);
        adjustHeap(arr, largest);
    }
}

//交换顺序
function swap(arr, i, j) {
    var temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

//堆排序
function heapSort(arr) {
    buildMaxHeap(arr);
 
    for (var i = arr.length - 1; i > 0; i--) {
        swap(arr, 0, i);
        len--;
        adjustHeap(arr, 0);
    }
    return arr;
}
```

## 小结

### 算法复杂度

下面是以上六种经典排序算法的复杂度比较：
<img style="width: 600px;text-align:center；" src="/images/posts/Sort.jpg">

### 应用场景

* 当数据量较小的时候，可以选用插入排序或者简单选择排序；
* 当数据基本有序的时候，可以选用直接插入、冒泡或快速排序；
* 当数据规模较大，可以采用归并排序、堆排序或者快速排序。



[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
