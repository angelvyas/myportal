---
title: "OS"
date: 2025-06-11
draft:  false
featured: false  
description: "os"
thumbnail: "/posts/docker/images/"
featureImage: "/posts/docker/images/"
shareImage: "/posts/docker/images/"
author: "Angel Vyas"
tags:
    - os
          
categories:     
    - general
    
---
### Banker's Algorithm
```c 
#include <stdio.h>

int main() {
    int n = 5; // Number of processes
    int m = 3; // Number of resource types
    int i, j, k;

    int alloc[5][3] = {
        { 0, 1, 0 }, // P0
        { 2, 0, 0 }, // P1
        { 3, 0, 2 }, // P2
        { 2, 1, 1 }, // P3
        { 0, 0, 2 }  // P4
    };

    int max[5][3] = {
        { 7, 5, 3 }, // P0
        { 3, 2, 2 }, // P1
        { 9, 0, 2 }, // P2
        { 2, 2, 2 }, // P3
        { 4, 3, 3 }  // P4
    };

    int avail[3] = { 3, 3, 2 }; // Available Resources

    int newRequest[5][3] = {0}, ProNo;

    printf("Banker's Algorithm\n");

    printf("For the new request: enter process number (0 to 4)\n");
    scanf("%d", &ProNo);

    printf("Enter the new request of process P%d in the order resources [A B C]\n", ProNo);
    scanf("%d", &newRequest[ProNo][0]);
    scanf("%d", &newRequest[ProNo][1]);
    scanf("%d", &newRequest[ProNo][2]);

    // Check if request is less than or equal to available
    if (newRequest[ProNo][0] > avail[0] || 
        newRequest[ProNo][1] > avail[1] || 
        newRequest[ProNo][2] > avail[2]) {
        printf("Request cannot be granted now as it exceeds available resources.\n");
        printf("Process must wait.\n");
        return 0;
    }

    // Pretend allocation
    avail[0] -= newRequest[ProNo][0];
    avail[1] -= newRequest[ProNo][1];
    avail[2] -= newRequest[ProNo][2];

    alloc[ProNo][0] += newRequest[ProNo][0];
    alloc[ProNo][1] += newRequest[ProNo][1];
    alloc[ProNo][2] += newRequest[ProNo][2];

    // Calculate need matrix
    int need[n][m];
    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {
            need[i][j] = max[i][j] - alloc[i][j];
        }
    }

    int f[n], ans[n], ind = 0;
    for (k = 0; k < n; k++) {
        f[k] = 0;
    }

    int flag;
    int y = 0;

    for (k = 0; k < 5; k++) {
        for (i = 0; i < n; i++) {
            if (f[i] == 0) {
                flag = 0;
                for (j = 0; j < m; j++) {
                    if (need[i][j] > avail[j]) {
                        flag = 1;
                        break;
                    }
                }
                if (flag == 0) {
                    ans[ind++] = i; // Safe sequence
                    for (y = 0; y < m; y++) {
                        avail[y] += alloc[i][y];
                    }
                    f[i] = 1;
                }
            }
        }
    }

    int safe = 1;
    for (i = 0; i < n; i++) {
        if (f[i] == 0) {
            safe = 0;
            break;
        }
    }

    if (safe == 0) {
        printf("Request cannot be granted now, as it may lead to Deadlock.\n");
        printf("There is no safe sequence.\n");
        printf("Your request is not granted to avoid Deadlock.\n");
        printf("Process has to wait.\n");
    } else {
        printf("Request can be granted, as a safe sequence is present.\n");
        printf("There will be no deadlock.\n");
        printf("Following is the SAFE Sequence:\n");
        for (i = 0; i < n - 1; i++)
            printf("P%d -> ", ans[i]);
        printf("P%d\n", ans[n - 1]);
    }

    return 0;
}

```
**OUTPUT**</br>
Banker's Algorithm</br>
For the new request: enter process number (0 to 4)</br>
1</br>
Enter the new request of process P1 in the order resources [A B C]</br>
1</br>
0</br>
2</br>
Request can be granted, as a safe sequence is present.</br>
There will be no deadlock.</br>
Following is the SAFE Sequence:</br>
P1 -> P3 -> P4 -> P0 -> P2</br>

### Producer Consumer Problem
```c
#include<unistd.h> 
#include<stdio.h> 
#include<pthread.h> 
#include<semaphore.h> 
int buf[5],  f,   r;  //Circular queue 
sem_t  mutex,  full,  empty; 
void *produce(void *arg)
{ 
    int i; 
    for(i=0;i<10;i++) 
    { 
        sem_wait(&empty);//Wait of empty slot and decrement the empty   
        sem_wait(&mutex); //Wait if consumer is comsuming a item 
 
        printf("produced item is %d\n",i); 
        buf[(++r)%5]=i; 
        sleep(1); 
 
        sem_post(&mutex); // signal the consumer to consume the item mutex=0 
        sem_post(&full); // full will be increamented 
 
    } 
} 
void *consume(void *arg) 
{ 
        int item,i; 
        for(i=0;i<10;i++) 
        { 
                sem_wait(&full); //Wait for item  and decrement the full 
                sem_wait(&mutex); // Wait if producer s producing a item 
 
                item=buf[(++f)%5]; 
                printf("consumed item is %d\n",item); 
                sleep(1); 
 
                sem_post(&mutex); // signal the producer  to produce the item mutex=0 
                sem_post(&empty); // incrementing the empty variable 
        } 
} 
int main() 
{ 
    pthread_t tid1,tid2; 
    sem_init(&mutex,  0,  1); 
    sem_init(&full,  0,  0); 
    sem_init(&empty, 0,  5); 
    pthread_create(&tid1, NULL, produce, NULL); 
    pthread_create(&tid2,NULL, consume, NULL); 
     pthread_join(tid1,NULL); 
    pthread_join(tid2,NULL); 
 
    return 0; 
}
```
**OUTPUT**</br>
produced item is 0</br>
produced item is 1</br>
produced item is 2</br>
produced item is 3</br>
produced item is 4</br>
consumed item is 0</br>
consumed item is 1</br>
consumed item is 2</br>
^C

### Paging technique of memory management
```c
#include<stdio.h> 
int main() 
{ 
int ms, Fsize, NoFrames, NoProcess, RemFrames, i, j, x, y, pa, offset; 
int NoPages, PageTable[10]; 
printf("\nEnter the memory size -- "); 
scanf("%d", &ms); 
printf("\nEnter the Frame size -- "); 
scanf("%d", &Fsize); 
NoFrames = ms/Fsize; 
printf("\n The no. of Frames available in memory are -- %d ", NoFrames); 
    RemFrames = NoFrames; 
 
       printf("\n Enter no. of pages required : "); 
       scanf("%d", &NoPages); 
         
        if(NoPages >RemFrames) 
        { 
            printf("\n Memory is Full"); 
            return (0); 
        } 
        RemFrames = RemFrames - NoPages; 
        printf("\n ---Enter page table --- "); 
        for(j=0;j<NoPages;j++) 
            scanf("%d", &PageTable[j]); 
             
        printf("\n ---page table --- "); 
        printf(" \n| PNo || FNo |"); 
        for(j=0;j<NoPages;j++) 
            printf(" \n| %d || %d |",j,PageTable[j]); 
      
    int yes=1; 
    do 
    { 
    printf("\nEnter Logical Address to find Physical Address "); 
    printf("\nEnter page number and offset -- "); 
    scanf(" %d %d",&y, &offset); 
    if( y>=NoPages || offset>=Fsize) 
 { 
        printf("\n trap: Page Number or offset illegal"); 
   return(0); 
 } 
    else 
    { 
        pa = (PageTable[y]*Fsize) + offset; 
         
        printf("Fsize=%d,offset=%d\n,frame no=%d",Fsize,offset,PageTable[y]); 
        printf("\n The Physical Address is -- %d", pa); 
    } 
        printf("\nContinue : yes=1,no=0\n"); 
        scanf("%d",&yes); 
         
    }while(yes==1); 
     
    return 0; 
} 
```
**OUTPUT**</br>
Enter the memory size -- 32</br>
Enter the Frame size -- 4</br>
The no. of Frames available in memory are -- 8</br>
Enter no. of pages required : 4</br>
 ---Enter page table --- 5</br>
6</br>
1</br>
2</br>
 ---page table ---</br>
| PNo || FNo |</br>
| 0 || 5 |</br>
| 1 || 6 |</br>
| 2 || 1 |</br>
| 3 || 2 |</br>
Enter Logical Address to find Physical Address</br>
Enter page number and offset -- 0 0</br>
Fsize=4,offset=0</br>
,frame no=5</br>
 The Physical Address is -- 20</br>
Continue : yes=1,no=0</br>
1</br>
Enter Logical Address to find Physical Address</br>
Enter page number and offset -- 1 3</br>
Fsize=4,offset=3</br>
,frame no=6</br>
 The Physical Address is -- 27</br>
Continue : yes=1,no=0</br>
^C</br>


### Segmentation technique of Memory Management
```c
#include<stdio.h> 
int main() 
{ 
    int i, y, PhyAddre, offset; 
    int NoSeg, SegmentTable[10][10]; 
 
    printf("\nEnter number segments -- "); 
    scanf("%d", &NoSeg); 
    printf("\nEnter the Segmentation Table data: Base value & Limit Value\n -- "); 
    for(i=0;i<NoSeg;i++) 
    scanf("%d%d", &SegmentTable[i][0],&SegmentTable[i][1]); 
 
    printf("\n----Enter the Segmentation Table data---\n"); 
    printf("Segment NO || Base || Limit || \n"); 
    for(i=0;i<NoSeg;i++) 
    printf("||   %d    ||  %d  ||  %d   || \n",i,SegmentTable[i][0],SegmentTable[i][1]); 
 
     int yes=1; 
     
do 
    { 
    printf("\nEnter Logical Address to find Physical Address "); 
    printf("\nEnter segment number and offset\n "); 
    scanf(" %d %d",&y, &offset); 
     
    if(offset>SegmentTable[y][1]) 
    { 
        printf("Trap : Addressing Error\n");  
    } 
    else 
    { 
    PhyAddre=SegmentTable[y][0]+offset; 
    printf("\n The Physical Address is -- %d", PhyAddre); 
    printf("\nContinue : yes=1,no=0\n"); 
        scanf("%d",&yes); 
    } 
    }while(yes==1); 
     
    return 0; 
} 
```
**OUTPUT**</br>
Enter number of segments -- 5 </br>
 Enter the Segmentation Table data: Base value & Limit Value </br>
 --  </br>
219  600 </br>
2300  14</br>
90  100 </br>
1327  580 </br>
1952  96 </br>
 ----Enter the Segmentation Table data---</br> 
Segment NO || Base || Limit ||  </br>
||   0    ||  219  ||  600   ||  </br>
||   1    ||  2300  ||  14   ||  </br>
||   2    ||  90  ||  100   ||  </br>
||   3    ||  1327  ||  580   ||  </br>
||   4    ||  1952  ||  96   ||  </br>
 Enter Logical Address to find Physical Address  </br>
Enter segment number and offset </br>
 0 430 </br>
 The Physical Address is -- 649</br> 
Continue : yes=1,no=0 </br>
1    </br>
 Enter Logical Address to find Physical Address  </br>
Enter segment number and offset </br>
 1 10 </br>
 The Physical Address is -- 2310 </br>
Continue : yes=1,no=0 </br>
1 </br>
Enter Logical Address to find Physical Address</br>  
Enter segment number and offset </br>
 2 500 </br>
Trap : Addressing Error</br> 
 Continue : yes=1,no=0</br>
^C

### Page Replacement Policies (FCFS)
```c
#include<stdio.h> 
int main() 
{ 
    int i,j,n,a[50],frame[10],no,k,avail,count=0; 
    printf("\n ENTER THE NUMBER OF PAGES:\n"); 
    scanf("%d",&n); 
    printf("\n ENTER THE PAGE NUMBER :\n"); 
    for(i=1;i<=n;i++) 
        scanf("%d",&a[i]); 
         
    printf("\n ENTER THE NUMBER OF FRAMES :"); 
        scanf("%d",&no); 
         
    for(i=0;i<no;i++) 
        frame[i]= -1; 
    j=0; 
    printf("\tref string\t page frames\n"); 
     
    for(i=1;i<=n;i++) 
    { 
        printf("%d\t\t",a[i]); 
        avail=0; 
        for(k=0;k<no;k++) 
            if(frame[k]==a[i]) 
                avail=1; 
            if (avail==0) 
            { 
                frame[j]=a[i]; 
                j=(j+1)%no; 
                count++; 
                for(k=0;k<no;k++) 
                    printf("%d\t",frame[k]); 
            } 
        printf("\n"); 
    } 
    printf("Page Fault Is %d",count); 
    return 0; 
} 
```
**OUTPUT**</br>
ENTER THE NUMBER OF PAGES:  20 </br>
ENTER THE PAGE NUMBER :       7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1 7 0 1</br> 
ENTER THE NUMBER OF FRAMES :3 </br>
      ref string       page frames </br>
7               7       -1      -1 </br>
0               7       0       -1 </br>
1               7       0       1 </br>
2               2       0       1 </br>
0 </br>
3               2       3       1</br> 
0               2       3       0 </br>
4               4       3       0 </br>
2               4       2       0 </br>
3               4       2       3 </br>
0               0       2       3 </br>
3 </br>
2 
1               0       1       3</br> 
2               0       1       2 </br>
0 </br>
1 </br>
7               7       1       2</br> 
0               7       0       2</br> 
1               7       0       1 </br>
Page Fault Is 15</br>


