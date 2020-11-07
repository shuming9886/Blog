---
title: 快速排序等排序算法的Python3实现
date: 2019-12-31 11:55:56
tags:
	- 算法
---



# 快速排序



原理思路：

分而治之的思想，通过递归解决问题。基本思想：把需要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的数据都要小，然后按此方法对这两部分数据分别进行快速排序，整个排序过程以递归进行，以此达到将整个数据变成有序序列。

设要排序的数组是A[0]……A[N-1]，首先选取一个数据作为关键数据（pivot），然后将所有比它小的数都放到它左边，所有比它大的数都放到它右边，这个过程称为一趟快速排序。需要注意的是，快速排序不是一种稳定的排序算法。

算法流程:

1.设置两个变量i、j，初始值分别为i=0，j=N-1；

2.以第一个数组元素作为关键数据，赋值给**key**，即key=A[0]；

3.从j开始向前搜索，即由右开始向前搜索（j--），找到第一个小于**key**的值A[j]，将A[j]和A[i]的值交换；

4.从i开始向后搜索，即由前开始向后搜索（i++），找到第一个大于**key**的A[i]，将A[i]和A[j]的值交换；

5.重复第3、4步，直到i=j； （3,4步中，没找到符合条件的值，即3中A[j]不小于**key**,4中A[i]不大于**key**的时候改变j、i的值，使得j=j-1，i=i+1，直至找到为止。另外，i==j这一过程一定正好是i+或j-完成的时候，此时令循环结束。）



快速排序的一次划分算法从两头交替搜索，直到low和high重合，因此其时间复杂度是O(n)；而整个快速排序算法的时间复杂度与划分的趟数有关。 

理想的情况是，每次划分所选择的中间数恰好将当前序列几乎等分，经过log<sub>2</sub>n趟划分，便可得到长度为1的子表。这样，整个算法的时间复杂度为O(nlog<sub>2</sub>n)。

最坏的情况是，每次所选的中间数是当前序列中的最大或最小元素，这使得每次划分所得的子表中一个为空表，另一子表的长度为原表的长度-1。这样，长度为n的数据表的快速排序需要经过n趟划分，使得整个排序算法的时间复杂度为O(n<sup>2</sup>)。

Python3代码：

```python
def quick_sort(data,left,right):
    if left > right:
        return;
    i = left;
    j = right;
    x = data[left];
    while i < j:
        while data[j] >= x and i < j:
            j -= 1;
        while data[i] <= x and i < j:
            i += 1;
        if i < j:
            temp = data[i];
            data[i] = data[j];
            data[j] = temp;
    data[left] = data[i];
    data[i] = x;
    quick_sort(data,left,i-1);
    quick_sort(data,i+1,right);

array = [2,3,5,7,1,4,6,15,5,2,7,9,10,15,9,17,12]
quick_sort(array,0,len(array)-1);

```

# 选择排序

选择排序（Selection sort）是一种简单直观的排序算法。它的工作原理是：第一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，然后再从剩余的未排序元素中寻找到最小（大）元素，然后放到已排序的序列的末尾。以此类推，直到全部待排序的数据元素的个数为零。选择排序是不稳定的排序方法。

```python
def selection_sort(arr):
    for i in range(len(arr)-1):
        # 将起始于元素设为最小元素
        min_index = i;
        # 第二层for表示最小元素和后面的元素逐个比较
        for j in range(i+1,len(arr)):
            if arr[j] < arr[min_index]:
                min_index = j
        arr[min_index], arr[i] = arr[i], arr[min_index];
    return arr

A = [11, 99, 33 , 69, 77, 88, 55, 11, 33, 36,39, 66, 44, 22]
selection_sort(A)
print(A)
```

# 冒泡排序

冒泡排序（Bubble Sort）算法的原理如下:

1. 比较相邻的元素。如果第一个比第二个大，就交换他们两个。 
2. 对每一对相邻元素做同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。 
3. 针对所有的元素重复以上的步骤，除了最后一个。 
4. 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

```python
def bubble_sort(arr):
    for i in range(len(arr)-1):
        for j in range(len(arr)-1-i):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr

```

# 插入排序

插入排序（Insertion-Sort）的算法描述是一种简单直观的排序算法。它的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。

把n个待排序的元素看成为一个有序表和一个无序表。开始时有序表中只包含1个元素，无序表中包含有n-1个元素，排序过程中每次从无序表中取出第一个元素，将它插入到有序表中的适当位置，使之成为新的有序表，重复n-1次可完成排序过程。

原理：

- 从第二个元素开始和前面的元素进行比较，如果前面的元素比当前元素大，则将前面元素 后移，当前元素依次往前，直到找到比它小或等于它的元素插入在其后面
- 然后选择第三个元素，重复上述操作，进行插入
- 依次选择到最后一个元素，插入后即完成所有排序 

```python
def bubble_sort(arr):
    for i in range(len(arr)-1):
        for j in range(len(arr)-1-i):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr

def insertion_sort(arr):
    # 第一层for循环表示循环插入的遍数
    for i in range(1,len(arr)):
        # 设置当前需要插入的元素
        current = arr[i]
        # 与当前元素比较的比较元素
        pre_index = i - 1
        while pre_index >= 0 and arr[pre_index] > current:
            # 当比较元素大于当前元素则把比较元素后移
            arr[pre_index+1] = arr[pre_index]
            # 往前选择下一个比较元素
            pre_index -= 1
        # 当比较元素小于当前元素，则将当前元素插入在其后
        arr[pre_index+1] = current
    return arr
```

# 归并排序

归并排序（MERGE-SORT）是建立在归并操作上的一种有效的排序算法,该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为二路[归并](https://baike.baidu.com/item/归并/253741)。归并排序是一种稳定的排序方法。

![1](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-algorithm.png)

```python
l = [1, 5, 8, 9, 2, 4, 12]

def merge(left, right):
    result = []
    i = j = 0
    while len(left) > i and len(right) > j:
        if left[i] > right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

def merge_sort(l):
    if len(l) <= 1:
        return l
    moddle = len(l)//2
    left = merge_sort(l[0: moddle])
    right = merge_sort(l[moddle: len(l)])
    print('left:', left, 'right:', right)
    return merge(left, right)

if __name__ == '__main__':
    a =  merge_sort(l)
    print(a)

```

