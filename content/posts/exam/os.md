---
title: "..."
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
### Banker's Algorithmsssss
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

</br>

### FCFS Scheduling Algorithm
```c
#include<stdio.h> 
int main() 
{ 
int processes[] = { 1, 2, 3}; 
int n =3;
   int  bt[] = {10, 5, 8}; 
     
    int wt[n], tat[n], total_wt = 0, total_tat = 0; 
     
    wt[0] = 0; 
    
    // calculating waiting time 
    for (int  i = 1; i < n ; i++ ) 
        wt[i] =  bt[i-1] + wt[i-1] ; 
    
   // calculating turnaround time 
   for (int  i = 0; i < n ; i++) 
        tat[i] = bt[i] + wt[i]; 
         
    //Display processes along with all details 
    printf("Processes   Burst time   Waiting time   Turn around time\n"); 
    
    // Calculate total waiting time and total turn  
    // around time 
    for (int  i=0; i<n; i++) 
    { 
        total_wt = total_wt + wt[i]; 
        total_tat = total_tat + tat[i]; 
        printf("   %d ",(i+1)); 
        printf("       %d ", bt[i] ); 
        printf("       %d",wt[i] ); 
        printf("       %d\n",tat[i] ); 
    } 
    int s=(float)total_wt / (float)n; 
    int t=(float)total_tat / (float)n; 
    printf("Average waiting time = %d",s); 
    printf("\n"); 
    printf("Average turn around time = %d ",t); 
  
    return 0; 
} 
```
</br>

**OUTPUT**</br>
RUN 1: </br>
Processes     Burst time     Waiting time     Turn around time</br>
1                  10          0                    10 </br>
                                                                              
2                  5           10                   15            </br>
 
3                  8           15                   23</br>                      
Average waiting time = 8                                      </br>                                                     
Average turn around time = 16  </br>

</br>
</br>

### SJF Scheduling Algorithm
```c
#include <stdio.h>
#define MAX 15

struct process {
    int pid;
    int bt;
    int wt;
    int tt;
};

int main() {
    struct process proc[MAX], temp;
    int n, i, j;
    int total_wt = 0, total_tt = 0;
    float avg_wt, avg_tt;

    printf("Enter number of processes (max 15): ");
    scanf("%d", &n);

    printf("Enter Process ID and Burst Time:\n");
    for (i = 0; i < n; i++) {
        scanf("%d %d", &proc[i].pid, &proc[i].bt);
    }

    // Sort processes by burst time using bubble sort
    for (i = 0; i < n - 1; i++) {
        for (j = 0; j < n - i - 1; j++) {
            if (proc[j].bt > proc[j + 1].bt) {
                temp = proc[j];
                proc[j] = proc[j + 1];
                proc[j + 1] = temp;
            }
        }
    }

    // Calculate waiting time and turnaround time
    for (i = 0; i < n; i++) {
        if (i == 0) {
            proc[i].wt = 0;
        } else {
            proc[i].wt = proc[i - 1].wt + proc[i - 1].bt;
        }

        proc[i].tt = proc[i].wt + proc[i].bt;
        total_wt += proc[i].wt;
        total_tt += proc[i].tt;
    }

    avg_wt = (float)total_wt / n;
    avg_tt = (float)total_tt / n;

    printf("\nProcess ID  Burst Time  Waiting Time  Turnaround Time\n");
    for (i = 0; i < n; i++) {
        printf("%9d  %10d  %13d  %16d\n", proc[i].pid, proc[i].bt, proc[i].wt, proc[i].tt);
    }

    printf("\nAverage Waiting Time = %.2f\n", avg_wt);
    printf("Average Turnaround Time = %.2f\n", avg_tt);

    return 0;
}

```
</br>

**OUTPUT** </br>
Enter number of processes (max 15): 4</br>
Enter Process ID and Burst Time:</br>
2 4 5</br>
3 5 6</br>
1 7 8</br>
</br>
Process ID  Burst Time  Waiting Time  Turnaround Time</br>
        5           3              0                 3</br>
        2           4              3                 7</br>
        5           6              7                13</br>
        1           7             13                20</br>

Average Waiting Time = 5.75</br>
Average Turnaround Time = 10.75</br>

### RR (Round Robin) Scheduling Algorithm

```c
#include <stdio.h>
#define MAX 15

struct process {
    int pid;
    int bt;
    int wt;
    int tt;
    int rem_bt;
};

int main() {
    struct process proc[MAX];
    int n, i, quantum, t = 0;
    int total_wt = 0, total_tt = 0;
    float avg_wt, avg_tt;
    int done;

    printf("Enter number of processes (max 15): ");
    scanf("%d", &n);

    printf("Enter Process ID and Burst Time:\n");
    for (i = 0; i < n; i++) {
        scanf("%d %d", &proc[i].pid, &proc[i].bt);
        proc[i].rem_bt = proc[i].bt;
        proc[i].wt = 0;  // Initialize waiting time to 0
    }

    printf("Enter Time Quantum: ");
    scanf("%d", &quantum);

    printf("\nOrder of Process Execution:\n");

    // Round Robin Scheduling
    do {
        done = 1;
        for (i = 0; i < n; i++) {
            if (proc[i].rem_bt > 0) {
                done = 0;
                printf("P%d ", proc[i].pid);

                if (proc[i].rem_bt > quantum) {
                    t += quantum;
                    proc[i].rem_bt -= quantum;
                } else {
                    t += proc[i].rem_bt;
                    proc[i].wt = t - proc[i].bt;
                    proc[i].rem_bt = 0;
                }
            }
        }
    } while (!done);

    // Calculate turnaround time and totals
    for (i = 0; i < n; i++) {
        proc[i].tt = proc[i].wt + proc[i].bt;
        total_wt += proc[i].wt;
        total_tt += proc[i].tt;
    }

    avg_wt = (float)total_wt / n;
    avg_tt = (float)total_tt / n;

    // Print results
    printf("\n\n|  PID  |  BT  |  WT  |  TAT |\n");
    printf("-------------------------------\n");
    for (i = 0; i < n; i++) {
        printf("|  %3d  | %3d  | %3d  | %3d  |\n", proc[i].pid, proc[i].bt, proc[i].wt, proc[i].tt);
    }

    printf("\nAverage Waiting Time: %.2f\n", avg_wt);
    printf("Average Turnaround Time: %.2f\n", avg_tt);

    return 0;
}

```
</br>

**OUTPUT**</br>
Enter number of processes (max 15): 3</br>
Enter Process ID and Burst Time:</br>
1 10</br>
2 5</br>
3 8</br>
Enter Time Quantum: 2</br>
</br>
Order of Process Execution:</br>
P1 P2 P3 P1 P2 P3 P1 P2 P3 P1 P3 P1</br>
</br>
|  PID  |  BT  |  WT  |  TAT |</br>
-------------------------------</br>
|    1  |  10  |  13  |  23  |</br>
|    2  |   5  |  10  |  15  |</br>
|    3  |   8  |  13  |  21  |</br>
</br>
Average Waiting Time: 12.00</br>
Average Turnaround Time: 19.67</br>
 </br>
 </br>

### Priority Scheduling Algorithm
```c
#include <stdio.h>
#define MAX 15

struct process {
    int pid;
    int priority;
    int bt;
    int wt;
    int tt;
};

int main() {
    struct process proc[MAX], temp;
    int n, i, j;
    int total_wt = 0, total_tt = 0;
    float avg_wt, avg_tt;

    printf("Enter number of processes (max 15): ");
    scanf("%d", &n);

    printf("Enter Process ID, Burst Time, and Priority for each process:\n");
    for (i = 0; i < n; i++) {
        scanf("%d %d %d", &proc[i].pid, &proc[i].bt, &proc[i].priority);
    }

    // Sort by priority (lower number = higher priority)
    for (i = 0; i < n - 1; i++) {
        for (j = 0; j < n - i - 1; j++) {
            if (proc[j].priority > proc[j + 1].priority) {
                temp = proc[j];
                proc[j] = proc[j + 1];
                proc[j + 1] = temp;
            }
        }
    }

    // Calculate waiting time and turnaround time
    proc[0].wt = 0;
    proc[0].tt = proc[0].bt;
    total_tt = proc[0].tt;

    for (i = 1; i < n; i++) {
        proc[i].wt = proc[i - 1].wt + proc[i - 1].bt;
        proc[i].tt = proc[i].wt + proc[i].bt;
        total_wt += proc[i].wt;
        total_tt += proc[i].tt;
    }

    avg_wt = (float)total_wt / n;
    avg_tt = (float)total_tt / n;

    // Output the table
    printf("\n| Process ID | Priority | Burst Time | Waiting Time | Turnaround Time |\n");
    printf("-----------------------------------------------------------------------\n");

    for (i = 0; i < n; i++) {
        printf("|     %3d    |   %3d    |    %3d     |     %3d      |      %3d       |\n",
               proc[i].pid, proc[i].priority, proc[i].bt, proc[i].wt, proc[i].tt);
    }

    printf("\nAverage Waiting Time = %.2f\n", avg_wt);
    printf("Average Turnaround Time = %.2f\n", avg_tt);

    return 0;
}

```
</br>

**OUTPUT**</br>
 
 
Enter number of processes (max 15): 3</br>
Enter Process ID, Burst Time, and Priority for each process:</br>
1 10 2</br>
2 5 1</br>
3 8 3</br>
</br>
| Process ID | Priority | Burst Time | Waiting Time | Turnaround Time |</br>
-----------------------------------------------------------------------</br>
|       2    |     1    |      5     |       0      |        5       |</br>
|       1    |     2    |     10     |       5      |       15       |</br>
|       3    |     3    |      8     |      15      |       23       |</br>
</br>
Average Waiting Time = 6.67</br>
Average Turnaround Time = 14.33</br>
 </br>
 </br>

 **Programs to implement following system calls of UNIX operating system: fork, exec, getpid, exit, wait, close, stat, opendir, readdir ,closedir and lseek**  

####  Write a C program to read from  file  and write  to another file.
```c
#include<stdio.h> 
#include<stdlib.h> 
#include<unistd.h> 
#include<fcntl.h> 
#define BUFF_SIZE 1000 
int main(void) 
{ 
int n,fd1,fd2; 
char buff[BUFF_SIZE]; 
//open the file for reading 
fd1 = open("testfile.txt",O_RDWR,0644); 
//read the data from file 
n=read(fd1,buff,BUFF_SIZE); 
// creating a new file using open. 
fd2=open("fileforcopy.txt", O_CREAT | O_RDWR, 0777); 
//writting data to file (fd) 
if( write(fd2, buff, n) == n)
printf("file copying is successful. and the data is:\n"); 
//Write to display (1 is standard fd for output device) 
write(1, buff, n); 
//closing the files 
int close(int fd1); 
int close(int fd2); 
return 0; 
} 
```
</br>

**INPUT & OUTPUT**</br>
testfile.txt file copied to fileforcopy.txt  </br>
file copying is successful. and the data is: hello mgit</br>
</br>
</br>


####  Program using lseek() system call that reads 10 characters from file “seeking” and print on screen. Skip next 5 characters and again read 10 characters and write on screen. 
```c
#include <stdio.h>      // for perror()
#include <unistd.h>     // for read(), write()
#include <fcntl.h>      // for open()
#include <sys/types.h>  // for types like mode_t
#include <sys/stat.h>   // for file permissions

int main() {
    int f;
    char buff[10];

    // Open the file 'seeking' in read-write mode
    f = open("seeking", O_RDWR);
    if (f < 0) {
        perror("Error opening file");
        return 1;
    }

    // Read first 10 bytes and write to stdout
    read(f, buff, 10);
    write(1, buff, 10);

    // Read next 10 bytes and write to stdout
    read(f, buff, 10);
    write(1, buff, 10);

    close(f);
    return 0;
}
 
```
**how to execute**</br>
>echo -n "1234567890abcdefghijxxxxxxxxxx" > seeking</br>
nano file_seek.c</br>
then paste code here</br>
compile:gcc file_seek.c -o file_seek</br>
run:./file_seek</br>

</br>

**OUTPUT**</br>
1234567890abcdefghij

</br>
</br>


#### Write a C program to print file status information using stat function.
```c
#include<stdio.h> 
#include <sys/types.h> 
#include <sys/stat.h> 
#include <dirent.h> 
#include<unistd.h> 
struct stat statbuf; 
char dirpath[256]; 
int main(int argc, char *argv[]) 
{ 
// getcwd is to get the name of the current working directory if found 
getcwd(dirpath,256); 
DIR *dir = opendir(dirpath); 
struct dirent *dp; 
for (dp=readdir(dir); dp != NULL ;  dp=readdir(dir)) 
{ 
stat(dp->d_name, &statbuf); 
printf("the file name is %s \n", dp->d_name); 
printf("dir = %d\n", S_ISDIR(statbuf.st_mode)); 
printf("file size is %ld in bytes \n", statbuf.st_size); 
printf("last modified time is %ld in seconds \n", statbuf.st_mtime); 
printf("last access time is %ld in seconds \n", statbuf.st_atime); 
printf("The device containing the file is %ld\n", statbuf.st_dev); 
printf("File serial number is %ld\n\n", statbuf.st_ino); 
} 
} 
```
</br>

**OUTPUT**</br>
the file name is fileone.txt</br> 
dir = 0 </br>
file size is 31 in bytes </br>
last modified time is 1581656490 in seconds </br>
last access time is 1581656969 in seconds </br>
The device containing the file is 2053 </br>
File serial number is 2099241 </br>
the file name is filestatus.c </br>
dir = 0 </br>
file size is 772 in bytes </br>
last modified time is 1581146159 in seconds </br>
last access time is 1581920990 in seconds </br>
The device containing the file is 2053 </br>
File serial number is 2099181 </br>
...(and so on)</br>
</br>
</br>

**how to execute:**
>nano dirinfo.c</br>
then paste the code</br>
>compile: gcc dirinfo.c -o dirinfo</br>
>run: ./dirinfo</br>
</br>
</br>

#### Program for opendir(), readdir() and closedir system calls
```c
#include <stdio.h>
#include <stdlib.h>     // for exit()
#include <dirent.h>     // for DIR, struct dirent

int main(int argc, char *argv[]) {
    char buff[100];
    DIR *dirp;
    struct dirent *dptr;

    printf("\nEnter Directory Name: ");
    scanf("%s", buff);

    dirp = opendir(buff);
    if (dirp == NULL) {
        printf("The given directory does not exist.\n");
        exit(1);
    }

    printf("\nFiles in the directory:\n");
    while ((dptr = readdir(dirp)) != NULL) {
        printf("%s\n", dptr->d_name);
    }

    closedir(dirp);
    return 0;
}
 ```

 **how to execute:**</br>
 >nano read_dir.c</br>
then paste the code</br>
compile: gcc read_dir.c -o read_dir</br>
run: ./read_dir</br>
</br>

**OUTPUT**</br>
Enter Directory Name: .</br>
</br>
Files in the directory:</br>
.</br>
..</br>
read_dir</br>
read_dir.c</br>
some_other_file.txt</br>

 </br>
 </br>

 ####  C Program for fork() and  getpid()  system call
 ```c
 #include <stdio.h>
#include <unistd.h>
#include <stdlib.h> // for exit()

int main() {
    int pid, pid1, pid2;

    pid = fork();  // create a new process

    if (pid == -1) {
        printf("ERROR IN PROCESS CREATION\n");
        exit(1);
    }

    if (pid != 0) {
        pid1 = getpid();
        printf("\nThe parent process ID is %d\n", pid1);
    } else {
        pid2 = getpid();
        printf("\nThe child process ID is %d\n", pid2);
    }

    return 0;
}
 
```
</br>
</br>

**OUTPUT**</br>
The parent process ID is 58936</br>

The child process ID is 58937</br>

**how to execute:**</br>
>save the code: nano fork_demo.c</br>
>compile:gcc fork_demo.c -o fork_demo</br>
>run:./fork_demo</br>
</br>
</br>

####  program to execute another C program using exec system call.
first create hello.c
```c
#include <stdio.h>

int main() {
    printf("Hello! I am the child program.\n");
    return 0;
}
```
then exec_demo.c
```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/wait.h>  // Required for wait()

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        perror("Fork failed");
        exit(1);
    }

    if (pid == 0) {
        // Child process
        printf("Child process about to run hello...\n");
        execl("./hello", "hello", NULL);  // Run the other C program

        // If exec fails
        perror("execl failed");
        exit(1);
    } else {
        // Parent process
        printf("Parent process waiting for child...\n");
        wait(NULL);
        printf("Child process completed.\n");
    }

    return 0;
}
```
**how to execute**</br>
>compile both files: gcc hello.c -o hello</br>
>gcc exec_demo.c -o exec_demo</br>
>to run:./exec_demo</br>
</br>


**OUTPUT**</br>
Parent process waiting for child...</br>
Child process about to run hello...</br>
Hello! I am the child program.</br>
Child process completed.</br>