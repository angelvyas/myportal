---
title: "Circular Queue"
date: 2024-09-05
draft:  false
featured: false  
description: "Circular Queue - Data Structures"
thumbnail: "/posts/data_structures/images/cirq.jpg"
featureImage: "/posts/data_structures/images/cirq.jpg" 
shareImage: "/posts/data_structures/images/cirq.jpg"
author: "Angel Vyas"
tags:
    - Data Structures
    - Circular Queue
    
    
categories:     
    - Data Structures
---



A circular queue is a data structure that operates on a First-In, First-Out (FIFO) basis but with a circular arrangement. Unlike a linear queue, where elements are added at the rear and removed from the front, a circular queue connects the last position back to the first, forming a circle. This allows for efficient use of space by reusing empty positions once elements are dequeued.

### Key Points:
- `Fixed Size`: The queue has a predefined capacity.
- `Circular Structure`: When the rear reaches the end, it wraps around to the beginning if space is available.
- `Efficient Space Utilization`: It avoids wasting memory by utilizing free space once items are removed.


### Key Operations:

- `Enqueue`: Add an element to the rear.
- `Dequeue`: Remove an element from the front.
- `isFull`: Check if the queue is full.
- `isEmpty`: Check if the queue is empty.


**Example**

For a queue of size 5:


>Initially: [ , , , , ]<br/>
>After Enqueue(1), Enqueue(2): [1, 2, , , ]<br/>
>After Dequeue(): [ , 2, , , ]<br/>
>Enqueue(3), Enqueue(4), Enqueue(5): [ , 2, 3, 4, 5]<br/>
>Enqueue(6) wraps around: [6, 2, 3, 4, 5]<br/>


### Applications

Memory buffers, task scheduling, and network data handling where efficient use of limited space is important.

### Program

```c
#include <stdio.h>
#include <stdlib.h>
#define max 6
int queue[max];
int front = -1;
int rear = -1;
void enqueue(int element)
{
    if (front == -1 && rear == -1)
    {
        front = 0;
        rear = 0;
        queue[rear] = element;
    }
    else if ((rear + 1) % max == front)
    {
        printf("Queue is full");
    }
    else
    {
        rear = (rear + 1) % max;
        queue[rear] = element;
    }
}
int dequeue()
{
    if ((front == -1) && (rear == -1))
    {
        printf("\nQueue is empty");
    }
    else if (front == rear)
    {
        printf("\nThe dequeued element is %d", queue[front]);
        front = -1;
        rear = -1;
    }
    else
    {
        printf("\nThe dequeued element is %d", queue[front]);
        front = (front + 1) % max;
    }
}
void display()
{
    if (front == -1 && rear == -1)
    {
        printf("Queue is empty\n");
    }
    else
    {
        printf("Elements in the queue are: ");
        int i = front;
        while (1)
        {
            printf("%d ", queue[i]);
            if (i == rear)
            {
                break;
            }
            i = (i + 1) % max;
        }
        printf("\n");
    }
}

void main()
{
    int ch, x;

    while (1)
    {
        printf("\n1.Enqueue");
        printf("\n2.Dequeue");
        printf("\n3.Display");
        printf("\n4.Exit");
        printf("\nEnter your choice:");
        scanf("%d", &ch);
        switch (ch)
        {
        case 1:
            printf("Enter the data:\n");
            scanf("%d", &x);
            enqueue(x);
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
            printf("Invalid Operator");
        }
    }
}
```