---
title: "DS - Sorting Techniques"
date: 2025-02-25
draft:  false
featured: false  
description: "DS - Sorting Techniques"
thumbnail: "/posts/data_structures/images/sorting.png"
featureImage: "/posts/data_structures/images/sorting.png" 
shareImage: "/posts/data_structures/images/sorting.png"
author: "Angel Vyas"
tags:
    - Data Structures
          
categories:     
    - Data Structures
---

### **Merge Sort in Data Structures**

Merge Sort is a popular Divide and Conquer algorithm used to sort arrays or lists efficiently. It works by recursively dividing the array into smaller halves, sorting them, and then merging the sorted halves back together.

⚙️ **How Merge Sort Works**</br>
`Divide:` Split the array into two halves until each sub-array has only one element.</br>
`Conquer:` Recursively sort each half.</br>
`Merge:` Combine the sorted halves into a single sorted array.</br>
</br>

🏷️ **Time and Space Complexity**
| Case           |Time Complexity|Space Complexity| Stable |
| :---------------- | :------: | ----: | ----:|
| Best        |   O(n log n)  |O(n) |Yes|
| Average           |  O(n log n)  |O(n) |Yes|
| Worst   | O(n log n)   | O(n) |Yes|

n = number of elements in the array</br>
Merge Sort is stable, meaning it maintains the relative order of equal elements.

#### Program:
```c
#include <stdio.h>
#define max 8
int arr[max]; // we have defined array globally.
void mergesort(int low, int high);
void merge(int low, int mid, int high);
void main()
{
    int i, j;
    printf("enter the elements\n");
    for (i = 0; i < 8; i++)
    {
        scanf("%d", &arr[i]);
    }
    mergesort(0, 7);
    printf("Sorted list is as follows:\n");
    for (i = 0; i <= 7; i++)
        printf("%d\n", arr[i]);
}

void mergesort(int low, int high)
{
    if (low != high)
    {
        int mid;
        mid = (low + high) / 2;
        mergesort(low, mid);
        mergesort(mid + 1, high);
        merge(low, mid, high);
    }
}

void merge(int low, int mid, int high)
{
    int temp[max];
    int i = low;
    int k = low;
    int j = mid + 1;
    while ((i <= mid) && (j <= high))
    {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
            temp[k++] = arr[j++];
    }
    while (i <= mid)
        temp[k++] = arr[i++];
    while (j <= high)
        temp[k++] = arr[j++];
    for (i = low; i <= high; i++)
    {
        arr[i] = temp[i];
    }
}
```

✅ **Why Use Merge Sort?**
1. Efficient for large datasets.</br>
2. Stable sorting (preserves equal elements' order).</br>
3. Preferred for sorting linked lists because it doesn’t require random access.
</br>
</br>


### **Heap Sort in Data Structures**
Heap Sort is a comparison-based sorting algorithm that uses a binary heap data structure. It works by first building a max heap from the input data and then repeatedly removing the largest element from the heap and placing it at the end of the array.

🔍 **Key Concepts**</br>
`Binary Heap:` A complete binary tree where each parent node is greater than or equal to its child nodes (in the case of a max heap).</br>
`Max Heap:` The largest element is always at the root.</br>
`Min Heap:` The smallest element is always at the root (used for finding the minimum, but not typically used in heap sort).</br>

⚙️ **How Heap Sort Works**
1. Build a Max Heap from the unsorted array.
2. Swap the root (maximum value) with the last element.
3. Heapify the root of the reduced heap to maintain the max heap property.
4. Repeat steps 2–3 until the array is sorted.

🏷️ **Time and Space Complexity**

| Case           |Time Complexity|Space Complexity| Stable |
| :---------------- | :------: | ----: | ----:|
| Best        |   O(n log n)  |O(1) |No|
| Average           |  O(n log n)  |O(1) |No|
| Worst   | O(n log n)   | O(1) |No|

### Program:
```c 
#include <stdio.h>
void maxheapify(int a[], int, int);
void maxheap(int a[], int beg, int end)
{
    int i;
    for (i = end / 2; i >= beg; i--)
    {
        maxheapify(a, i, end);
    }
}

void maxheapify(int a[], int f, int size)
{
    int max = f;
    int l = f * 2, r = f * 2 + 1, t;

    if (l <= size && a[l] > a[max])
        max = l;
    if (r <= size && a[r] > a[max])
        max = r;
    if (f != max)
    {
        t = a[f];
        a[f] = a[max];
        a[max] = t;
        maxheapify(a, max, size);
    }
}

void heapsort(int a[], int size)
{
    int i, t;
    for (i = size; i >= 2; i--)
    {
        t = a[1];
        a[1] = a[i];
        a[i] = t;
        maxheapify(a, 1, i - 1);
    }
}

int main()
{
    int a[10], i;
    printf("Enter array elements:\n");
    for (i = 1; i < 10; i++)
    {
        scanf("%d", &a[i]);
    }

    maxheap(a, 1, 9);
    heapsort(a, 9);
    printf("Sorted array:\n");
    for (i = 1; i < 10; i++)
    {
        printf("%d", a[i]);
        printf("\n");
    }
}
```

✅ **Advantages of Heap Sort**</br>
- Time-efficient: Always runs in O(n log n) time.</br>
- In-place: Requires only a constant amount O(1) of additional memory.</br>
- No recursion: Unlike merge sort, it doesn't use additional stacks for recursion.</br>

❌ **Disadvantages**</br>
- Not stable: Equal elements might not maintain their original order.</br>
- Cache performance: Poorer than other algorithms like quicksort due to non-sequential memory access.</br>

</br>

### **Quick Sort in Data Structures**
Quick Sort is a highly efficient Divide and Conquer sorting algorithm. It works by selecting a pivot element from the array and partitioning the other elements into two sub-arrays:

- Elements less than the pivot
- Elements greater than the pivot
The process is recursively applied to the sub-arrays until the entire array is sorted.

🔍 **Key Concepts**</br>
`Pivot Selection:` You can choose the first element, last element, middle element, or even a random element as the pivot.</br>
`Partitioning:` Rearranges the elements so that elements smaller than the pivot are on the left and greater ones are on the right.</br>
`Recursion:` The same process is applied recursively to the left and right sub-arrays.
</br>
</br>

⚙️ **How Quick Sort Works**
1. Choose a pivot element.
2. Rearrange the elements so that all elements less than the pivot are on the left, and those greater are on the right.
3. Recursively apply the same logic to the left and right sub-arrays.

</br>

🏷️ **Time and Space Complexity**

| Case           |Time Complexity|Space Complexity| Stable |
| :---------------- | :------: | ----: | ----:|
| Best        |   O(n log n)  |O(log n) |No|
| Average           |  O(n log n)  |O(log n) |No|
| Worst   | O(n²)   | O(log n) |No|

n = number of elements in the array</br>
Not stable (equal elements may not maintain their original order)

### Program:
```c
#include <stdio.h>
#define max 8
int arr[max];
void quicksort(int low, int high);
int partition(int low, int high);
int main()
{
    int i;
    printf("Enter the elements:\n");
    for (i = 1; i <= max; i++)
        scanf("%d", &arr[i]);
    quicksort(1, 8);
    printf("Sorted list is as follows:\n");
    for (i = 1; i <= max; i++)
        printf("%d\n", arr[i]);
}

void quicksort(int low, int high)
{
    if (low < high)
    {
        int pi = partition(low, high);
        quicksort(low, pi - 1);
        quicksort(pi + 1, high);
    }
}

int partition(int low, int high)
{
    int pivot = arr[high];
    int i = low - 1, j, temp;
    for (j = low; j <= high - 1; j++)
    {
        if (arr[j] < pivot)
        {
            i++;
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    return (i + 1);
}
```
✅ **Advantages of Quick Sort**
- Efficient for large datasets.
- Requires less memory than merge sort (in-place sorting).
- Generally faster than other O(n log n) algorithms in practice.
</br>

❌ **Disadvantages**
- Not stable (equal elements may lose their relative order).
- Worst-case time complexity is O(n²) (rare but possible if the pivot is poorly chosen, like already sorted arrays).