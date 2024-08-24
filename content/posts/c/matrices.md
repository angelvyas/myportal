---
title: 'Matrices in C'
date: 2024-24-05
draft:  false
featured: false  
description: "Matrices in C-language"
thumbnail: "/posts/c/images/matrix.png"
featureImage: "/posts/c/images/matrix.png" 
shareImage: "/posts/c/images/matrix.png"
author: "Angel Vyas"
tags:
    - C Language
    - Matrices
    

categories:     
    - C Language
---
</br>

## Matrices:
### *Matrix Multiplication*
```c
#include<stdio.h>
int main()
{   int m,n,p,q,a[10][10],b[10][10],c[10][10],k,i,j;
    printf("enter the rows and column value for matrix 1:\n");
    scanf("%d%d",&m,&n);
    printf("enter the rows and columns value for matrix 2:\n");
    scanf("%d%d",&p,&q);
    printf("enter the elements of matrix 1:\n");
    for(i=0;i<m;i++)
    {
        for(j=0;j<n;j++){
            scanf("%d",&a[i][j]);
        }
    }
    printf("matrix 1 is:\n");
    for(i=0;i<m;i++){
        for(j=0;j<n;j++){
            printf("%d\t",a[i][j]);
        
        }
        printf("\n");
    }
    printf("enter the elements of matrix 2:\n");
    for(i=0;i<p;i++)
    {
        for(j=0;j<q;j++){
            scanf("%d",&b[i][j]);
        }
    }
    printf("matrix 2 is:\n");
    for(i=0;i<p;i++){
        for(j=0;j<q;j++){
            printf("%d\t",b[i][j]);
        
        }
        printf("\n");
    }
    for(i=0;i<m;i++){
        for(j=0;j<q;j++){
            c[i][j]=0;
        }
    }

    for(i=0;i<m;i++){
        for(j=0;j<q;j++){
            for(k=0;k<n;k++){
                c[i][j]=c[i][j]+a[i][k]*b[k][j];

            }
        }
    }
    printf("\nmultiplication of the given two matrices is:\n");
    for(i=0;i<m;i++){
        for(j=0;j<q;j++){
            printf("%d\t",c[i][j]);
        }
        printf("\n");
    }

    return 0;

}
```
</br>

### *Transpose of a Matrix*
```c 
#include <stdio.h>
int main()
{
    int m, i, j, n, a[10][10];
    printf("enter the size of rows and columns of the matrix\n");
    scanf("%d%d", &m, &n);
    printf("enter the elements of the matrix\n");
    for (i = 0; i < m; i++)
    {
        for (j = 0; j < n; j++)
        {
            scanf("%d", &a[i][j]);
        }
    }
    printf("the given matrix is\n");
    for (i = 0; i < m; i++)
    {
        for (j = 0; j < n; j++)
        {
            printf("%d\t", a[i][j]);
        }
        printf("\n");
    }
    printf("the transpose of the given matrix is:\n");
    for (i = 0; i < m; i++)
    {
        for (j = 0; j < n; j++)
        {
            printf("%d\t", a[j][i]);
        }
        printf("\n");
    }
    return 0;
}
```
</br>


