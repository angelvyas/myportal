---
title: "EXTERNAL - SEM 3"
date: 2024-12-16
draft:  false
featured: false  
description: "EXTERNAL - SEM 3"
thumbnail: "/posts/data_structures/images/z"
featureImage: "/posts/data_structures/images/" 
shareImage: "/posts/data_structures/images/"
author: "Angel Vyas"
tags:
    - Data Structures
    -        
categories:     
    - Data Structures
---

### MERGE SORT:
```c
#include <stdio.h>
#define max 8
int arr[max]; // we have defined array globally.
void mergesort(int low, int high);
void merge(int low, int mid, int high);
void main()
{
    int i, j;
    printf("enter the elements\n");
    for (i = 0; i < 8; i++)
    {
        scanf("%d", &arr[i]);
    }
    mergesort(0, 7);
    printf("Sorted list is as follows:\n");
    for (i = 0; i <= 7; i++)
        printf("%d\n", arr[i]);
}

void mergesort(int low, int high)
{
    if (low != high)
    {
        int mid;
        mid = (low + high) / 2;
        mergesort(low, mid);
        mergesort(mid + 1, high);
        merge(low, mid, high);
    }
}

void merge(int low, int mid, int high)
{
    int temp[max];
    int i = low;
    int k = low;
    int j = mid + 1;
    while ((i <= mid) && (j <= high))
    {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
            temp[k++] = arr[j++];
    }
    while (i <= mid)
        temp[k++] = arr[i++];
    while (j <= high)
        temp[k++] = arr[j++];
    for (i = low; i <= high; i++)
    {
        arr[i] = temp[i];
    }
}
```
### HEAP SORT:
```c
#include <stdio.h>
void maxheapify(int a[], int, int);
void maxheap(int a[], int beg, int end)
{
    int i;
    for (i = end / 2; i >= beg; i--)
    {
        maxheapify(a, i, end);
    }
}

void maxheapify(int a[], int f, int size)
{
    int max = f;
    int l = f * 2, r = f * 2 + 1, t;

    if (l <= size && a[l] > a[max])
        max = l;
    if (r <= size && a[r] > a[max])
        max = r;
    if (f != max)
    {
        t = a[f];
        a[f] = a[max];
        a[max] = t;
        maxheapify(a, max, size);
    }
}

void heapsort(int a[], int size)
{
    int i, t;
    for (i = size; i >= 2; i--)
    {
        t = a[1];
        a[1] = a[i];
        a[i] = t;
        maxheapify(a, 1, i - 1);
    }
}

int main()
{
    int a[10], i;
    printf("Enter array elements:\n");
    for (i = 1; i < 10; i++)
    {
        scanf("%d", &a[i]);
    }

    maxheap(a, 1, 9);
    heapsort(a, 9);
    printf("Sorted array:\n");
    for (i = 1; i < 10; i++)
    {
        printf("%d", a[i]);
        printf("\n");
    }
}
```
### QUICK SORT:
```c
#include <stdio.h>
#define max 8
int arr[max];
void quicksort(int low, int high);
int partition(int low, int high);
int main()
{
    int i;
    printf("Enter the elements:\n");
    for (i = 1; i <= max; i++)
        scanf("%d", &arr[i]);
    quicksort(1, 8);
    printf("Sorted list is as follows:\n");
    for (i = 1; i <= max; i++)
        printf("%d\n", arr[i]);
}

void quicksort(int low, int high)
{
    if (low < high)
    {
        int pi = partition(low, high);
        quicksort(low, pi - 1);
        quicksort(pi + 1, high);
    }
}

int partition(int low, int high)
{
    int pivot = arr[high];
    int i = low - 1, j, temp;
    for (j = low; j <= high - 1; j++)
    {
        if (arr[j] < pivot)
        {
            i++;
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    return (i + 1);
}
```

### BST:
```c
#include <stdio.h>
#include <stdlib.h>

struct BinaryTreeNode
{
    int key;
    struct BinaryTreeNode *left, *right;
};

struct BinaryTreeNode *newNodeCreate(int value)
{
    struct BinaryTreeNode *temp = (struct BinaryTreeNode *)malloc(
        sizeof(struct BinaryTreeNode));
    temp->key = value;
    temp->left = temp->right = NULL;
    return temp;
}

struct BinaryTreeNode *
insertNode(struct BinaryTreeNode *node, int value)
{
    if (node == NULL)
    {
        return newNodeCreate(value);
    }
    if (value < node->key)
    {
        node->left = insertNode(node->left, value);
    }
    else if (value > node->key)
    {
        node->right = insertNode(node->right, value);
    }
    return node;
}

void postOrder(struct BinaryTreeNode *root)
{
    if (root != NULL)
    {
        postOrder(root->left);
        postOrder(root->right);
        printf(" %d ", root->key);
    }
}
void inOrder(struct BinaryTreeNode *root)
{
    if (root != NULL)
    {
        inOrder(root->left);
        printf(" %d ", root->key);
        inOrder(root->right);
    }
}

void preOrder(struct BinaryTreeNode *root)
{
    if (root != NULL)
    {
        printf(" %d ", root->key);
        preOrder(root->left);
        preOrder(root->right);
    }
}
int main()
{
    struct BinaryTreeNode *root = NULL;

    root = insertNode(root, 50);
    insertNode(root, 30);
    insertNode(root, 20);
    insertNode(root, 40);
    insertNode(root, 70);
    insertNode(root, 60);
    insertNode(root, 80);
    postOrder(root);
    printf("\n");

    preOrder(root);
    printf("\n");

    inOrder(root);
    printf("\n");
    return 0;
}
```
### QUEUE USING ARRAY:
```c
#include <stdio.h>//simpleq
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
    int ch, d;
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

### QUEUE USING LINKED LIST:
```c
#include <stdio.h>//q using linked list
#include <stdlib.h>

struct node
{
	struct node *next;
	int data;
};

struct node *f, *r;

void enqueue()
{
	int a;
	printf("\nEnter the data value\n");
	scanf("%d", &a);

	struct node *nn = (struct node *)malloc(sizeof(struct node));
	nn->data = a;
	nn->next = NULL;

	if (r == NULL)
	{
		f = nn;
		r = nn;
	}

	else
	{

		r->next = nn;
		r = nn;
	}
}

void display()
{
	struct node *temp;
	temp = f;
	printf("\nThe Queue list is as:");

	while (temp->next != NULL)
	{
		printf("\n%d", temp->data);
		temp = temp->next;
	}

	printf("\n%d", temp->data);
}

void dequeue()
{
	if (f != NULL)
		f = f->next;
}

void main()
{

	while (1)
	{
		int ch;

		printf("\nMENU\n");
		printf("1.enqueue\n");
		printf("2.display\n");
		printf("3.dequeue\n");
		printf("4.exit\n");
		printf("Enter choice:\n");
		scanf("%d", &ch);

		switch (ch)
		{

		case 1:
			enqueue();
			break;
		case 2:
			display();
			break;
		case 3:
			dequeue();
			break;
		case 4:
			exit(0);

		default:
			printf("Invalid\n");
		}
	}
}
```
### STACK:
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
### CIRCULAR QUEUE:
```c
#include <stdio.h>//circularq
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

### SINGLY LINKED LIST:
```c
#include <stdio.h>//linked list
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
    else
    {
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
}
void traverse()
{
    struct node *current = head;
    while (current != NULL)
    {
        printf("%d\t", current->data);
        current = current->next;
    }
}

void main()
{

    while (1)
    {
        int ch;

        printf("\nMENU\n");
        printf("1.insert\n");
        printf("2.delete\n");
        printf("3.traverse\n");
        printf("4.exit\n");
        printf("Enter choice:\n");
        scanf("%d", &ch);

        switch (ch)
        {

        case 1:
            int d;
            printf("enter the data value to be inserted");
            scanf("%d", &d);
            insert(d);
            break;
        case 2:
            int a;
            printf("enter the data value to be deleted");
            scanf("%d", &a);
            delete (a);
            break;

        case 3:
            traverse();
            break;
        case 4:
            exit(0);

        default:
            printf("Invalid\n");
        }
    }
}
```

### DOUBLY LINKED LIST:
```c
#include <stdio.h>//doubly linked list
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

