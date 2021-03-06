# m组n个元素排序

> 有M个数组，每个数组含有N个元素，N个元素是从小到大有序的。要求你将这N*M个元素，从小到大排序到另外一个数组里。

## 多路归并

使用M个指针分别指向M个数组的起始元素。

此时的这M个元素分别是M个数组里最小的元素，再寻找出这M个元素的最小元素就可以放到我们的目标数组里。

## 遍历

1. **寻找出这M个元素的最小元素的时间复杂度：**

   O(M）

2. **多路归并的总体时间复杂度：**

   每次O(M）总共M * N个元素，总体时间复杂度O(N * M * M)。

3. **多路归并的总体空间复杂度**

   O(M)



## 小顶堆

1. **寻找出这M个元素的最小元素的时间复杂度：**

   建堆O(N) 

   主要是向下调整，向下调整的时间复杂度为O(h)=O(log M) 

   向上调整O(mlogm)

2. **多路归并的总体时间复杂度：**

   O(N * M * log M)

3. **多路归并的总体空间复杂度**

   O(M)

