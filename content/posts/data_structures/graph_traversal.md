---
title: "DS - Graph Traversal Algorithms"
date: 2025-02-25
draft:  false
featured: false  
description: "DS - Graph Traversal Algorithm"
thumbnail: "/posts/data_structures/images/bdfs.png"
featureImage: "/posts/data_structures/images/bdfs.png" 
shareImage: "/posts/data_structures/images/bdfs.png"
author: "Angel Vyas"
tags:
    - Data Structures
          
categories:     
    - Data Structures
---
In Data Structures (DS), BFS (Breadth-First Search) and DFS (Depth-First Search) are two fundamental graph traversal algorithms used to explore nodes in a graph or tree.

 ## Breadth-First Search (BFS)
BFS explores a graph level by level, starting from a selected node and visiting all its neighbors before moving on to their neighbors.

`How it works:`
1. Start from the initial node (source).</br>
2. Visit all directly connected nodes.</br>
3. Move to the next level and repeat until all nodes are visited.

`Data Structure Used:`
Uses a Queue (FIFO) to keep track of nodes to visit next.

`Use Cases:` 
1. Shortest path in unweighted graphs (e.g., GPS navigation).
2. Finding the closest friend in a social network.
3. Web crawlers.

### Program:
```c
#include <stdio.h>

// creating queue data structure using arrays
int queue[100];

// defining pointers of the queue to perform pop and push
int front = 0, back = 0;

// defining push operation on the queue
void push(int var)
{
    queue[back] = var;
    back++;
}

// defining pop operation on queue
void pop()
{
    queue[front] = 0;
    front++;
}

// creating a visited array to keep the track of visited nodes
int visited[7] = {0};

int main()
{
    // defining the number of total persons
    int N = 6;

    // adjacenty matrix representing graph
    int graph[6][6] = {{0, 1, 1, 0, 0, 0},
                       {1, 0, 1, 0, 0, 0},
                       {1, 1, 0, 1, 1, 0},
                       {0, 0, 1, 0, 0, 0},
                       {0, 0, 1, 0, 0, 1},
                       {0, 0, 0, 0, 1, 0}};

    // front == back stands for empty queue
    // until queue is not empty perfroming bfs

    // adding a starting node in the list
    push(1);
    visited[0] = 1; // marking 1st node as visited
    while (front != back)
    {
        int current = queue[front];

        // printing current element
        printf("%d ", current);

        // popping the front element from the queue
        pop();

        for (int i = 0; i < 6; i++)
        {
            // adding non-visited connected nodes of the current node to the queue
            if ((graph[current - 1][i] == 1) && (visited[i] == 0))
            {
                visited[i] = 1; // marking visisted
                push(i + 1);
            }
        }
    }
    return 0;
}
```
</br>
</br>

## Depth-First Search (DFS)
DFS explores a graph by going as deep as possible along each branch before backtracking.

`How it works:`

1. Start from the initial node (source).
2. Visit one neighbor and keep going deeper.
3. Backtrack when you hit a dead end and explore the next neighbor.


`Data Structure Used:`
Uses a Stack (LIFO), either explicitly or through recursion.

`Use Cases:`
1. Solving puzzles (like mazes or Sudoku).
2. Detecting cycles in a graph.
3. Topological sorting.

### Program:
```c
#include <stdio.h>

#define MAX_VERTICES 100

// Function to perform Depth-First Search (DFS) traversal
void DFS(int graph[MAX_VERTICES][MAX_VERTICES], int visited[MAX_VERTICES], int vertices, int start) {
    printf("%d ", start); // Print the current vertex
    visited[start] = 1;    // Mark the current vertex as visited

    // Visit all adjacent vertices
    for (int i = 0; i < vertices; i++) {
        if (graph[start][i] == 1 && !visited[i]) {
            DFS(graph, visited, vertices, i);
        }
    }
}

int main() {
    int vertices, edges;

    // Input the number of vertices
    printf("Enter the number of vertices: ");
    scanf("%d", &vertices);

    if (vertices <= 0 || vertices > MAX_VERTICES) {
        printf("Invalid number of vertices. Exiting...\n");
        return 1;
    }

    int graph[MAX_VERTICES][MAX_VERTICES] = {0}; // Initialize the adjacency matrix with zeros
    int visited[MAX_VERTICES] = {0};             // Initialize the visited array with zeros

    // Input the number of edges
    printf("Enter the number of edges: ");
    scanf("%d", &edges);

    if (edges < 0 || edges > vertices * (vertices - 1)) {
        printf("Invalid number of edges. Exiting...\n");
        return 1;
    }

    // Input edges and construct the adjacency matrix
    for (int i = 0; i < edges; i++) {
        int start, end;
        printf("Enter edge %d (start end): ", i + 1);
        scanf("%d %d", &start, &end);

        // Validate input vertices
        if (start < 0 || start >= vertices || end < 0 || end >= vertices) {
            printf("Invalid vertices. Try again.\n");
            i--;
            continue;
        }

        graph[start][end] = 1;
        // For undirected graph, uncomment the following line:
        // graph[end][start] = 1;
    }

    // Input the starting vertex for DFS traversal
    int startVertex;
    printf("Enter the starting vertex for DFS traversal: ");
    scanf("%d", &startVertex);

    if (startVertex < 0 || startVertex >= vertices) {
        printf("Invalid starting vertex. Exiting...\n");
        return 1;
    }

    printf("DFS Traversal Order: ");
    DFS(graph, visited, vertices, startVertex);

    return 0;
}
```