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
    - Data Structures
    - Simple Queue
categories:     
    - Data Structures
---



A `simple queue` is a fundamental data structure that follows the First-In, First-Out `(FIFO)` principle. This means that the first element added to the queue will be the first one to be removed, just like people standing in line—whoever gets in first is served first.

### Key Operations in a Simple Queue:
- `Enqueue (Insertion)`: Adding an element to the back of the queue.
- `Dequeue (Removal)`: Removing an element from the front of the queue.
- `Peek (Front)`: Viewing the element at the front of the queue without removing it.
- `isEmpty`: Checking if the queue is empty.

**Example:**
Think of a line at a movie theater. The first person in line buys the ticket first, and as more people arrive, they join at the back of the line. When a person buys a ticket and leaves, the next person in line gets their turn.

### Visual Example:
>Initial queue: [1, 2, 3] (1 is at the front, 3 is at the back)</br>
>Enqueue(4): [1, 2, 3, 4]</br>
>Dequeue(): [2, 3, 4] (1 is removed)</br>
### Applications:
- `Task scheduling` (e.g., in operating systems)</br>
- `Breadth-First Search (BFS)` in graph traversal</br>
- `Managing resources` in simulations</br>

It’s a simple, efficient way to handle processes where order matters!
### Program:

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