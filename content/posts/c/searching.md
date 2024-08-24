---
title: 'Searching in C'
date: 2024-24-05
draft:  false
featured: false  
description: "Searching in C-language"
thumbnail: "/posts/c/images/search.jpg"
featureImage: "/posts/c/images/search.jpg" 
shareImage: "/posts/c/images/search.jpg"
author: "Angel Vyas"
tags:
    - C Language
    - Searching
categories:     
    - C Language
---
</br>

Searching in C language refers to the process of finding a specific element or value within a data structure, typically an array. Searching algorithms help determine whether an element exists in the data structure and, if so, its position. 
## Searching:
### *L-Search*
```c
#include<stdio.h>
int lsearch(int b[],int n,int key);
void main()
{
    int a[20],num,k,loc,i;
    printf("\nEnter the number of elements in the list:");
    scanf("%d",&num);
    printf("Enter the elements of the list:\n");
    for(i=0;i<num;i++)
    scanf("%d",&a[i]);
    printf("Enter the key you are searching for:\n");
    scanf("%d",&k);
    loc = lsearch(a,num,k);
    if(loc!=-1)
    printf("successful search %d is found at %d\n",k,loc+1);
    else{
        printf("unsuccessful search\n");
    }

}
int lsearch(int b[],int n,int key)
{
    int i;
    for(i=0;i<n;i++)
    {
        if(b[i]==key)
        return i;
    }
    return -1;
}

```
</br>

### *B-Search*
```c
#include <stdio.h>
int bsearch(int a[], int n, int key);
void main()
{
    int a[20], n, i, k, pos = -1;
    printf("Enter the number of elements in the given array:\n");
    scanf("%d", &n);
    printf("Enter the elements of an array:\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }
    printf("Enter the key you are searching for:\n");
    scanf("%d", &k);
    pos = bsearch(a, n, k);
    if (pos != -1)
    {
        printf("the key %d is found at %d", k, pos + 1);
    }
    else
        printf("the key is not found\n");
}
int bsearch(int a[], int n, int key)
{
    int first = 0, last = n - 1, middle;
    while (first <= last)
    {
        middle = (first + last) / 2;
        if (key < a[middle])
            last = middle - 1;
        else if (key > a[middle])
            first = middle + 1;
        else
            return middle;
    }
}
```
</br>


