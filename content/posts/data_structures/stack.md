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


### **Programs:**

#### Implementation of Stack.
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

#### Stack using Linked List:

```c
#include <stdio.h>
#include <stdlib.h>

// Define the structure of a node in the linked list
struct Node {
    int data;
    struct Node* next;
};

// Function to create a new node
struct Node* newNode(int data) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->next = NULL;
    return node;
}

// Function to check if the stack is empty
int isEmpty(struct Node* top) {
    return top == NULL;
}

// Function to push an element onto the stack
void push(struct Node** top, int data) {
    struct Node* node = newNode(data);
    node->next = *top;
    *top = node;
    printf("%d pushed to stack\n", data);
}

// Function to pop an element from the stack
int pop(struct Node** top) {
    if (isEmpty(*top)) {
        printf("Stack underflow\n");
        return -1;
    }
struct Node* temp = *top;
    int popped = temp->data;
    *top = (*top)->next;
    free(temp);
    return popped;
}

// Function to peek the top element of the stack
int peek(struct Node* top) {
    if (isEmpty(top)) {
        printf("Stack is empty\n");
        return -1;
    }
    return top->data;
}

// Function to display the stack
void display(struct Node* top) {
    if (isEmpty(top)) {
        printf("Stack is empty\n");
        return;
    }
    struct Node* temp = top;
    printf("Stack elements: ");
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}
int main() {
    struct Node* stack = NULL;  // Initialize the stack to NULL (empty stack)

    // Testing stack operations
    push(&stack, 10);
    push(&stack, 20);
    push(&stack, 30);
    display(stack);  // Expected output: 30 20 10

    printf("Popped: %d\n", pop(&stack));  // Expected output: 30
    display(stack);  // Expected output: 20 10

    printf("Top element: %d\n", peek(stack));  // Expected output: 20

    pop(&stack);  // Popping 20
    pop(&stack);  // Popping 10
    pop(&stack);  // Stack underflow

    return 0;
}
```