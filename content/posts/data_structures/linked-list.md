---
title: "DS - Linked List"
date: 2024-09-10
draft:  false
featured: false  
description: "DS - Linked List - Data Structures"
thumbnail: "/posts/data_structures/images/linked-list.png"
featureImage: "/posts/data_structures/images/linked-list.png" 
shareImage: "/posts/data_structures/images/linked-list.png"
author: "Angel Vyas"
tags:
    - Data Structures
    - Linked List        
categories:     
    - Data Structures
---

A linked list is a fundamental data structure used in computer science to organize and store a collection of elements. Unlike arrays, linked lists do not require a contiguous block of memory and can efficiently handle dynamic memory allocation.

### Key Characteristics
- `Nodes`: A linked list is composed of nodes, where each node contains two main parts:
    - `Data`: The value or information stored in the node.
    - `Reference (or Link)`: A pointer or reference to the next node in the sequence.
- `Head`: The first node in the linked list. It provides the entry point to the list.
- `Tail`: The last node in the list, which typically points to null (or None in some languages) to indicate the end of the list.

### Types of Linked Lists
- `Singly Linked List`: Each node contains a single reference to the next node. Traversal is only possible in one direction (from head to tail).
> Operations: Insertion, deletion, and traversal are done by following the next references.

- `Doubly Linked List`: Each node contains two references: one to the next node and one to the previous node. This allows for bidirectional traversal.
> Operations: Insertion, deletion, and traversal can be done in both directions (forward and backward).

- `Circular Linked List`: The last node in the list points back to the first node, forming a circle. This can be singly or doubly linked.
> Operations: Traversal can continue indefinitely due to the circular nature of the list.

### Operations
- `Insertion`: Adding a node to the list (at the beginning, end, or a specific position).
- `Deletion`: Removing a node from the list (from the beginning, end, or a specific position).
- `Traversal`: Accessing each node in the list to process or display its data.
- `Search`: Finding a node with a specific value.


### Program
```c
#include <stdio.h>
#include <stdlib.h>
struct node
{
    int data;
    struct node *next;
};
struct node *head = NULL;
void insert(int value)
{
    struct node *nn = (struct node *)malloc(sizeof(struct node));
    nn->data = value;
    nn->next = NULL;
    if (head == NULL)

        head = nn;
    else
    {
        struct node *current = head;
        while (current->next != NULL)
        {
            current = current->next;
        }
        current->next = nn;  
    }
}
void delete(int value)
{
    if (head == NULL)
    {
        printf("empty list");
        return;
    }
    struct node *current = head;
    struct node *previous = NULL;
    while (current != NULL)
    {
        if (current->data == value)
        {
            if (previous == NULL)
                head = current->next;
            else
                previous->next = current->next;
            free(current);
            return;
        }
        previous = current;
        current = current->next;
    }
    printf("element not found");
}
void traverse()
{
    struct node *current = head;
    while (current != NULL)
    {
        printf("%d", current->data);
        current = current->next;
    }
}

void main()
{
    insert(10);
    printf("\ninserted successfully");
    insert(20);
    printf("\ninserted successfully");
    insert(30);
    printf("\ninserted successfully\n");
    traverse();
    delete (20);
    printf("\ndeleted successfully\n");
    traverse();
}
```