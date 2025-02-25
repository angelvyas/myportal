---
title: "DS - BST"
date: 2025-02-25
draft:  false
featured: false  
description: "DS - BST"
thumbnail: "/posts/data_structures/images/bst.png"
featureImage: "/posts/data_structures/images/bst.png" 
shareImage: "/posts/data_structures/images/bst.png"
author: "Angel Vyas"
tags:
    - Data Structures
          
categories:     
    - Data Structures
---

### **Binary Search Tree (BST) in Data Structures**
A Binary Search Tree (BST) is a special kind of binary tree where each node follows a specific ordering property:

- Left Subtree: Contains nodes with values less than the node’s value.
- Right Subtree: Contains nodes with values greater than the node’s value.
- Both left and right subtrees must also be binary search trees.


🔍 **Properties of BST**
1. Binary Tree Structure: Each node has at most two children.
2. Ordered: Left child < Parent < Right child
3. No Duplicate Values: Typically, BSTs don’t allow duplicate elements.
</br>
</br>

⚙️ **Operations on a BST**
|Operation	|Time Complexity	|Description|
| :-----|:-----|:-----|
|Search|	O(log n) (Balanced) / O(n) (Unbalanced)|	Find if an element exists.|
|Insert|	O(log n) (Balanced) / O(n) (Unbalanced)|	Add a new element.|
|Delete|	O(log n) (Balanced) / O(n) (Unbalanced)|	Remove an element.|
|Traversal|	O(n)|	Visit all nodes (In-order, Pre-order, Post-order).|


🔗 **Types of Traversal in BST**
1. `In-order (Left, Root, Right):` Returns elements in sorted order.
2. `Pre-order (Root, Left, Right):` Useful for copying the tree.
3. `Post-order (Left, Right, Root):` Useful for deleting the tree.

💻 **Implementation of a Binary Search Tree**
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
</br>

✅ **Advantages of a Binary Search Tree**
- Efficient searching, insertion, and deletion when the tree is balanced.
- Provides sorted data through in-order traversal.
- Can be extended to more advanced trees (e.g., AVL Tree, Red-Black Tree).

</br>

❌ **Disadvantages of BST**
- Performance degrades to O(n) if the tree becomes unbalanced (like a linked list).
- Requires self-balancing (AVL, Red-Black) for consistently good performance.

</br>

🔄 **Applications of BST**
- Searching and sorting operations
- Implementing associative arrays
- In-memory data structures like sets and maps
- Used in databases for indexing

