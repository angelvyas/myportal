---
title: "DS - Stack"
date: 2024-09-10
draft:  false
featured: false  
description: "DS - Stack"
thumbnail: "/posts/data_structures/images/stack.png"
featureImage: "/posts/data_structures/images/stack.png" 
shareImage: "/posts/data_structures/images/stack.png"
author: "Angel Vyas"
tags:
    - Data Structures
    - Stack        
categories:     
    - Data Structures
---

A stack is a fundamental data structure in computer science that operates on a Last In, First Out (LIFO) principle. This means that the last element added to the stack is the first one to be removed. You can think of a stack like a stack of plates: you add new plates to the top and remove them from the top as well.

### Key Operations
- `Push`: Add an element to the top of the stack.
- `Pop`: Remove the element from the top of the stack.
- `Peek (or Top)`: Retrieve the element at the top of the stack without removing it.
- `IsEmpty`: Check if the stack is empty.


### Characteristics
- `LIFO Order`: The most recently added element is the first one to be removed.
- `Dynamic Size`: In many implementations, a stack can grow or shrink as needed, depending on the underlying data structure (such as an array or linked list).


### Program
```c
#include <stdio.h>

#include <stdlib.h>

#define SIZE 4

int top = -1, inp_array[SIZE];
void push();
void pop();
void show();

int main()
{
    int choice;

    while (1)
    {
        printf("\nPerform operations on the stack:");
        printf("\n1.Push the element\n2.Pop the element\n3.Show\n4.End");
        printf("\n\nEnter the choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
        case 1:
            push();
            break;
        case 2:
            pop();
            break;
        case 3:
            show();
            break;
        case 4:
            exit(0);

        default:
            printf("\nInvalid choice!!");
        }
    }
}

void push()
{
    int x;

    if (top == SIZE - 1)
    {
        printf("\nOverflow!!");
    }
    else
    {
        printf("\nEnter the element to be added onto the stack: ");
        scanf("%d", &x);
        top = top + 1;
        inp_array[top] = x;
    }
}

void pop()
{
    if (top == -1)
    {
        printf("\nUnderflow!!");
    }
    else
    {
        printf("\nPopped element: %d", inp_array[top]);
        top = top - 1;
    }
}

void show()
{
    if (top == -1)
    {
        printf("\nUnderflow!!");
    }
    else
    {
        printf("\nElements present in the stack: \n");
        for (int i = top; i >= 0; --i)
            printf("%d\n", inp_array[i]);
    }
}
```