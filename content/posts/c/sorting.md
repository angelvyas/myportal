---
title: 'Sorting'
date: 2024-08-24
draft:  false
featured: false  
description: "Sorting in C-language"
thumbnail: "/posts/c/images/sorting.png"
featureImage: "/posts/c/images/sorting.png" 
shareImage: "/posts/c/images/sorting.png"
author: "Angel Vyas"
tags:
    - C Language
    - Sorting
    - Examples
    - bubble Sort
    - Insertion Sort 
    - Selection Sort
categories:     
    - C Language
---

Sorting in C language refers to arranging the elements of an array in a specific order, typically in ascending or descending order.

## Sorting:
### *Bubble Sort*
```c
#include <stdio.h>
int main()
{
    int i, j, k, temp, n, a[20];

    printf("enter the number of elements in the array:\n");
    scanf("%d", &n);
    printf("\nenter the elements of the array:");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }
    for (i = 1; i < n; i++)
    {
        for (j = 0; j < n - 1; j++)
        {
            if (a[j] > a[j + 1])
            {
                temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }

        printf("pass %d\n", i);

        for (k = 0; k < n; k++)
        {
            printf("%d", a[k]);
        }
            printf("\n");

    }}
```
</br>

### *Insertion Sort*
```c
 #include <stdio.h>
int main()
{
    int i, j, n, temp, a[30];
    printf("enter the number of elements in the array:\n");
    scanf("%d", &n);
    printf("\nenter the elements of the array");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }

    for (i = 1; i < n; i++)
    {
        
        j = i;
      while ((a[j-1]>a[j]) && (j >= 0))
        {   
            
            temp=a[j];
            a[j]=a[j-1];
            a[j-1]=temp;
            j--;
        }
    
        
    }
    printf("sorted list is\n");

    for (i = 0; i < n; i++)
    {
        printf("%d\n", a[i]);
    }

    return 0;
}

```
</br>

### *Selection Sort*
```c
#include <stdio.h>

void swap(int *xp, int *yp)
{
    int temp = *xp;
    *xp = *yp;
    *yp = temp;
}

void selection(int a[], int n)
{
    int i, j, min;
    for (i = 0; i < n; i++)
    {
        min = j;
        printf("a[%d]:%d\n", i, a[i] );
        for (j = i + 1; j < n; j++)
        {
            printf("a[%d]:%d ", j, a[j] );
            if (a[j] < a[i])
            {
                swap(&a[i], &a[j]);
            }
        }printf("\n");
    }
}
void www(int a[], int size)
{
    int i;
    for (i = 0; i < size; i++)
    {
        printf("%d\n", a[i]);
    }
    printf("\n");
}

int main()
{
    int a[] = {5,6,4,3,2};
    int n = 5;
    selection(a, n);
    printf("sorted array:\n");
    www(a, n);
    return 0;
}
```
</br>


