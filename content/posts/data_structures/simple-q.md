---
title: "DS - Simple Queue"
date: 2024-08-26
draft:  false
featured: false  
description: "Simple Queue - Data Structure"
thumbnail: "/posts/data_structures/images/simpleq.png"
featureImage: "/posts/data_structures/images/simpleq.png" 
shareImage: "/posts/data_structures/images/simpleq.png"
author: "Angel Vyas"
tags:
    - Data Structure
categories:     
    - Data Structure
---

```c
#include <stdio.h>
#include <stdlib.h>
#define n 5
int a[n];
int f = -1;
int r = -1;
void enqueue(int e)
{
    if (r == n - 1)
    {
        printf("Q is full\n");
    }
    else
    {
        if (f == -1 && r == -1)
        {
            f = 0;
            r = 0;
        }
        else
        {
            r++;
        }
        a[r] = e;
    printf("inserted successfully\n");

    }
}

void dequeue()
{
    if (f == -1 && r == -1)
    {
        printf("Q is empty\n");
    }
    else
    {
        if (f == r)
        {
            f = -1;
            r = -1;
        }
        else
        {
            f++;
        }
    }
}

void display()
{
    if (f == -1 && r == -1)
    {
        printf("queue is empty\n");
    }
    else
    {
        printf("Queue:\n");
        for (int i = f; i <= r; i++)
        {
            printf("%d\t", a[i]);
        }
        printf("\n");
    }
}

int main()
{
    int ch, d, c;
    while (1)
    {
        printf("1. enqueue operation\n");
        printf("2. dequeue operation\n");
        printf("3. Display queue\n");
        printf("4. exit\n");
        printf("enter your choice\n");
        scanf("%d", &ch);
        switch (ch)
        {
        case 1:
            printf("enter the data\n");
            scanf("%d", &d);
            enqueue(d);
            break;
        case 2:
            dequeue();
            break;

        case 3:
            display();
            break;

        case 4:
            exit(0);
            break;

        default:
            printf("invalid operation\n");
        }
    }
}

```