---
title: 'Pointers in C-language'
date: 2024-08-24
draft:  false
featured: false  
description: "Pointers in C-languge"
thumbnail: "/posts/c/images/pointers.png"
featureImage: "/posts/c/images/pointers.png" 
shareImage: "/posts/c/images/pointers.png"
author: "Angel Vyas"
tags:
    - C Language
categories:     
    - C Language
---

## Pointers
### *Basics*
```c
#include<stdio.h>
int main()
{
    int a=10;
    printf("Address of P: %p \n", *a);

    int *p;

    p=&a;

    *p = 30;

    printf("Address of P: %p \n", p);
    printf("Value of P: %d \n", a);
    printf("%d", *(&a));


}
```
### *to read the elements and display*
```c
#include<stdio.h>
void rnp(int*p,int n);
int main()
{
    int num,a[15];
    printf("\n enter the number of elements:");
    scanf("%d",&num);
    rnp(a,num);

}
void rnp(int*p,int n)
{
    int i,sum=0;
    int*q=p;
    for(i=1;i<=n;i++)
    {
        printf("\nenter the %d elements of an array",i);
        scanf("%d",p);
        p++;
    }
    printf("\nelements are:");

        for(i=1;i<=n;i++)
        {
            sum=sum+*q;
            printf("%5d",*q);
            q++;
        }
        printf("\nsum of elements of an array is %d",sum);
    }

```
</br>

### *to display elements in reverse order*
```c
#include <stdio.h>
void display(int *p, int n);
int main()
{
    int a[10], num, i;
    printf("\nenter the number of elements:");
    scanf("%d", &num);
    printf("\nenter the elements:");
    for (i = 0; i < num; i++)
        scanf("%d", &a[i]);
    display(a, num);
}
void display(int *p, int n)
{
    int i;
    printf("\n elements in the array are:");
    for(i=0;i<n;i++)
    {
        printf("%5d", *p);
        p++;

    }
    p--;//it will take null character automatically at the end of the list whether you try to prevent it ,it will must take the garbage value.

    printf("\neleemnts in the reverse order are:");
    for(i=0;i<n;i++)
    {
        printf("%5d", *p);
        p--;
    
    }
}
```
