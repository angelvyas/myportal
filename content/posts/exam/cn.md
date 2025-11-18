---
title: 'practise'
date: 2025-11-18
draft:  false
featured: false  
description: "networks"
thumbnail: "/posts/exam/images/smile.png"
featureImage: "/posts/exam/images/smile.png" 
shareImage: "/posts/exam/images/smile.png"
author: "Angel Vyas"
tags:
    - general
categories:     
    - general
---

### GBN
```c
#include <stdio.h>

int main() {
    int total, win, lost, i, j;

    printf("Total frames: ");
    scanf("%d", &total);

    printf("Window size: ");
    scanf("%d", &win);

    printf("Enter lost frame number: ");
    scanf("%d", &lost);

    for(i = 1; i <= total; i += win) {

        printf("\nSending frames: ");
        for(j = i; j < i + win && j <= total; j++)
            printf("%d ", j);

        for(j = i; j < i + win && j <= total; j++) {

            if(j == lost) {
                printf("\nFrame %d lost! Resending window...\n", j);

                // resend from lost frame
                for(j = lost; j < i + win && j <= total; j++)
                    printf("Resent frame %d -> ACK\n", j);

                break; // stop checking further ACKs
            }
            else {
                printf("\nACK for frame %d", j);
            }
        }
    }

    printf("\n\nAll frames delivered!\n");
    return 0;
}
```

### CLASSFUL IP
```c
#include <stdio.h>

int main() {
    int a, b, c, d;   // to store 4 octets

    printf("Enter IP address (format: a.b.c.d): ");
    scanf("%d.%d.%d.%d", &a, &b, &c, &d);

    if(a >= 0 && a <= 127)
        printf("Class A\nDefault Mask: 255.0.0.0\n");
    else if(a >= 128 && a <= 191)
        printf("Class B\nDefault Mask: 255.255.0.0\n");
    else if(a >= 192 && a <= 223)
        printf("Class C\nDefault Mask: 255.255.255.0\n");
    else if(a >= 224 && a <= 239)
        printf("Class D (Multicast)\n");
    else if(a >= 240 && a <= 255)
        printf("Class E (Research)\n");
    else
        printf("Invalid IP address!\n");

    return 0;
}
```
### CLASSLESS
```c
#include <stdio.h>

int main() {
    int a, b, c, d;

    printf("Enter IP address (format: a.b.c.d): ");
    scanf("%d.%d.%d.%d", &a, &b, &c, &d);

    if (a >= 0 && a <= 127)
        printf("Class A\n");
    else if (a >= 128 && a <= 191)
        printf("Class B\n");
    else if (a >= 192 && a <= 223)
        printf("Class C\n");
    else if (a >= 224 && a <= 239)
        printf("Class D (Multicast)\n");
    else if (a >= 240 && a <= 255)
        printf("Class E (Experimental)\n");
    else
        printf("Invalid IP\n");

    return 0;
}
```
### DJIKSTRA'S ALGO
```c
#include <stdio.h>
#define INF 9999
#define V 5    // number of vertices

int main() {
    int graph[V][V] = {
        {0,  10, 0,  30, 100},
        {10, 0,  50, 0,  0},
        {0,  50, 0,  20, 10},
        {30, 0,  20, 0,  60},
        {100,0,  10, 60, 0}
    };

    int dist[V], visited[V];
    int i, j, count, u, v;

    // initialize
    for(i = 0; i < V; i++) {
        dist[i] = INF;
        visited[i] = 0;
    }

    int start = 0;  // starting node
    dist[start] = 0;

    for(count = 0; count < V-1; count++) {

        // find minimum distance unvisited node
        int min = INF;
        for(i = 0; i < V; i++)
            if(!visited[i] && dist[i] < min) {
                min = dist[i];
                u = i;
            }

        visited[u] = 1;

        // relax adjacent vertices
        for(v = 0; v < V; v++)
            if(graph[u][v] && !visited[v] &&
               dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
    }

    // print results
    printf("Shortest distances from node %d:\n", start);
    for(i = 0; i < V; i++)
        printf("To %d = %d\n", i, dist[i]);

    return 0;
}
```

### ENCRYPTION / DECRYPTION
```c
#include <stdio.h>

void encrypt(char *msg, int key) {
    for (int i = 0; msg[i] != '\0'; i++) {
        msg[i] = msg[i] + key;   // shift forward
    }
}

void decrypt(char *msg, int key) {
    for (int i = 0; msg[i] != '\0'; i++) {
        msg[i] = msg[i] - key;   // shift backward
    }
}

int main() {
    char message[100];
    int key;

    printf("Enter message: ");
    fgets(message, sizeof(message), stdin);

    printf("Enter key (number): ");
    scanf("%d", &key);

    encrypt(message, key);
    printf("Encrypted: %s\n", message);

    decrypt(message, key);
    printf("Decrypted: %s\n", message);

    return 0;
}
```

### link state routing
```c
#include <stdio.h>
#define INF 999

int main() {
    int n, source;
    int cost[10][10], dist[10], visited[10];
    int i, j, minDist, nextNode;

    printf("Enter number of routers: ");
    scanf("%d", &n);

    printf("Enter cost adjacency matrix (use 999 for no direct link):\n");
    for(i = 0; i < n; i++)
        for(j = 0; j < n; j++)
            scanf("%d", &cost[i][j]);

    printf("Enter source router (0 to %d): ", n - 1);
    scanf("%d", &source);

    // Initialization
    for(i = 0; i < n; i++) {
        dist[i] = cost[source][i];
        visited[i] = 0;
    }

    dist[source] = 0;
    visited[source] = 1;

    // Dijkstra / Link State Computation
    for(i = 1; i < n; i++) {
        minDist = INF;

        for(j = 0; j < n; j++)
            if(!visited[j] && dist[j] < minDist) {
                minDist = dist[j];
                nextNode = j;
            }

        visited[nextNode] = 1;

        for(j = 0; j < n; j++)
            if(!visited[j] && (minDist + cost[nextNode][j] < dist[j]))
                dist[j] = minDist + cost[nextNode][j];
    }

    // Output Result
    printf("\nShortest distance from router %d to others:\n", source);
    for(i = 0; i < n; i++)
        printf("Router %d -> %d = %d\n", source, i, dist[i]);

    return 0;
}
```