---
title: "Arrays in C"
date: 2024-08-24
draft:  false
featured: false  
description: "C Language - Arrays in C Language"
thumbnail: "/posts/c/images/array.png"
featureImage: "/posts/c/images/array.png" 
shareImage: "/posts/c/images/array.png"
author: "Angel Vyas"
tags:
    - C Language
    - Arrays
    - Examples
categories:     
    - C Language
---

An array is a data structure used in programming to store a collection of elements, typically of the same type, in a fixed-size sequence.


### *Initialisation of Array*

```c
#include <stdio.h>
int main()
{
    // it's not important to give size during initialisation.
    // eg: float y[]={1.2,2,3.32};
    
    int g[5];
    int i;

    printf("\n enter the elements of array");
    for (i = 0; i < 5; i++)
    {
        scanf("%d", &g[i]);
    }
    printf("values of array are \n");
    for (i = 0; i < 5; i++)
    {
        printf("\n value of g[%d]=%d", i, g[i]);
    }
    return 0;
}
```
</br>

### *To read an Array from keyboard*

```c
#include <stdio.h>
int main()
{

    int a[3][3];
    for (int i = 0;i<3;i++){
        for(int j = 0;j<3;j++){
            printf("Enter the value of matrix [%d][%d]: ", i,j);
            scanf("%d", &a[i][j]);
        }
    }


 
// print value read by keyboard
for (int i = 0;i<3;i++){
    for(int j = 0;j<3;j++){
        printf("\n print the value of matrix [%d][%d]: %d", i,j, a[i][j]);
    }
}

return 0;
}
```
</br>

### *Example of char array with initialization*

```c  
#include<stdio.h>
int main(){
char city[][10] = {"Jaipur","Jhodpur","Jaisalmer"};

for (int i = 0;i<3;i++){
    for(int j = 0;j<3;j++){
        printf("\n print the value of matrix [%d][%d]: %s", i,j, city[i][j]);
    }
}
return 0;
}
```
</br>

### *to print the characters of an Array*
```c
#include<stdio.h>
void main{
char angel[] = "angelvyas";
printf("the value of char is %c", angel[6]);
 printf("the value of x is %d", x);
}
```
</br>

### *Sum of Arrays*
```c
#include <stdio.h>
int main()
{
    int a[10], n, i, sum = 0;
    printf("\nenter the size of an array");

    scanf("%d", &n);
    printf("enter the elements of the array");

    for (i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }
    printf("\nthe given array is");
    for (i = 0; i < n; i++)
    {
        printf("%d", a[i]);
        printf("\n");
    }
    printf("\nthe sum of elements of the given array is");
    for (i = 0; i < n; i++)
    {
        sum = sum + a[i];
    }
    printf("%d", sum);
    return 0;
}
```
</br>

### *2D Array:*

```c
#include <stdio.h>

int main(){
    int a[4][5];
    int i,j;
    printf("enter the value for array: \n");
    for(i=0;i<4;i++){
        for(j=0;j<5;j++)
        scanf("%d", &a[i][j]);
    }
    printf("\nthe value of array is");
    for(i=0;i<4;i++){
        for(j=0;j<5;j++){
        printf("value of a[%d][%d]=%d", i,j,a[i][j]);
    }
    return 0;
    }
}
```
</br>

