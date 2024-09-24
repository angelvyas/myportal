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
</br>
</br>
</br>


### Singly Linked List:
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

void main(){



    while(1)
{
	int ch;

	printf("\nMENU\n");
	printf("1.insert\n");
	printf("2.delete\n");
	printf("3.traverse\n");
	printf("4.exit\n");
	printf("Enter choice:\n");
	scanf("%d", &ch);

switch(ch)
{

	case 1:
    int d;
    printf("enter the data value to be inserted");
    scanf("%d",&d);
    insert(d);
		break;
	case 2:
    int a;
    printf("enter the data value to be deleted");
    scanf("%d",&a);
    delete(a);
		break;

	case 3:traverse();
		break;
	case 4:exit(0);

	default: printf("Invalid\n");
}
}
}
```
</br>
</br>
</br>

### Queue Using Linked List:
```c 
#include <stdio.h>
#include <stdlib.h>

struct node
{
	struct node *next;
	int data;
};

struct node *f,*r;

void enqueue()
{
	int a;
	printf("\nEnter the data value\n");
	scanf("%d",&a);

	struct node *nn=(struct node *)malloc(sizeof(struct node));
	nn->data=a;
	nn->next=NULL;

	if(r==NULL)
	{
		f=nn;
		r=nn;
	}

	else {

		r->next=nn;
		r=nn;

	     }
}

void display()
{
	struct node *temp;
	temp=f;
	printf("\nThe Queue list is as:");

	while(temp->next!=NULL)
	{
		printf("\n%d",temp->data);
		temp=temp->next;
	}

	printf("\n%d",temp->data);
}

void dequeue()
{
	if(f!=NULL)
	f=f->next;
}

void main()
{

while(1)
{
	int ch;

	printf("\nMENU\n");
	printf("1.enqueue\n");
	printf("2.display\n");
	printf("3.dequeue\n");
	printf("4.exit\n");
	printf("Enter choice:\n");
	scanf("%d", &ch);

switch(ch)
{

	case 1:enqueue();
		break;
	case 2:display();
		break;
	case 3:dequeue();
		break;
	case 4:exit(0);

	default: printf("Invalid\n");
}
}
}
```
</br>
</br>
</br>


### Doubly Linked List:

```c
#include <stdio.h>
#include <stdlib.h>
struct node
{
    struct node *prev;
    struct node *next;

    int data;
};
struct node *head;
void insertion_beginning();
void insertion_last();
void deletion_beginning();
void deletion_last();
void display();
void main()
{
    int choice = 0;
    while (choice != 6)
    {
        printf("\nChoose one option from the following list ...\n");
        printf("\n1.Insert in begining\n2.Insert at last\n3.Delete from Beginning\n4.Delete from last\n5.Show\n6.Exit\n");
        printf("\nEnter your choice?\n");
        scanf("\n%d", &choice);
        switch (choice)
        {
        case 1:
            insertion_beginning();
            break;
        case 2:
            insertion_last();
            break;
        case 3:
            deletion_beginning();
            break;
        case 4:
            deletion_last();
            break;
        case 5:
            display();
            break;
        case 6:
            exit(0);
            break;
        default:
            printf("Please enter valid choice..");
        }
    }
}
void insertion_beginning()
{
    struct node *ptr;
    int item;
    ptr = (struct node *)malloc(sizeof(struct node));
    printf("\nEnter Item value");
    scanf("%d", &item);

    if (head == NULL)
    {
        ptr->next = NULL;
        ptr->prev = NULL;
        ptr->data = item;
        head = ptr;
    }
    else
    {
        ptr->data = item;
        ptr->prev = NULL;
        ptr->next = head;
        head->prev = ptr;
        head = ptr;
    }
    printf("\nNode inserted\n");
}

void insertion_last()
{
    struct node *ptr, *temp;
    int item;
    ptr = (struct node *)malloc(sizeof(struct node));
    printf("\nEnter value");
    scanf("%d", &item);
    ptr->data = item;
    if (head == NULL)
    {
        ptr->next = NULL;
        ptr->prev = NULL;
        head = ptr;
    }
    else
    {
        temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = ptr;
        ptr->prev = temp;
        ptr->next = NULL;
    }

    printf("\nnode inserted\n");
}

void deletion_beginning()
{
    struct node *ptr;
    if (head == NULL)
    {
        printf("\n UNDERFLOW");
    }
    else if (head->next == NULL)
    {
        head = NULL;
        free(head);
        printf("\nnode deleted\n");
    }
    else
    {
        ptr = head;
        head = head->next;
        head->prev = NULL;
        free(ptr);
        printf("\nnode deleted\n");
    }
}
void deletion_last()
{
    struct node *ptr;
    if (head == NULL)
    {
        printf("\n UNDERFLOW");
    }
    else if (head->next == NULL)
    {
        head = NULL;
        free(head);
        printf("\nnode deleted\n");
    }
    else
    {
        ptr = head;
        if (ptr->next != NULL)
        {
            ptr = ptr->next;
        }
        ptr->prev->next = NULL;
        free(ptr);
        printf("\nnode deleted\n");
    }
}
void display()
{
    struct node *ptr;
    printf("\n printing values...\n");
    ptr = head;
    while (ptr != NULL)
    {
        printf("%d\n", ptr->data);
        ptr = ptr->next;
    }
}
```