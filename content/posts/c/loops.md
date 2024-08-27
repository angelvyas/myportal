---
title: 'Loops in C-language'
date: 2024-08-24
draft:  false
featured: false  
description: "Loops in C-language"
thumbnail: "/posts/c/images/loops.jpg"
featureImage: "/posts/c/images/loops.jpg" 
shareImage: "/posts/c/images/loops.jpg"
author: "Angel Vyas"
tags:
    - C Language
categories:     
    - C Language
---
</br>

Loops in C language are used to repeatedly execute a block of code based on certain conditions. They are fundamental for tasks such as iterating over arrays, processing data, and performing repetitive operations.

## Loops
```c
#include <stdio.h>
#include <string.h>

void main()
{
    // loop means - to execute the statement while the condition satisfied
    // for and while are two method mainly used for loops(do while is also there)

    // condition gives output in the form of 1 = True 0 = False

    int i = 0; // assignment
    while(i <= 10) // condition 
    {
        printf("Hi this is the example of loop %d \n", i);
        i = i + 1; // increment
    }

    while(1) // condition 
    {
        printf("Hi this is the example of loop %d \n", i);
        i = i + 1; // increment
        
        if (i <= 10){
            continue;
        }else{
            break;
        }

    }

    
    // looping using for loop
    for(int i = 0; i <= 10; i = i + 1)
    {
        printf("Hi all - %d \n", i);
    }

}
```
</br>

## Example Questions-
### *Pyramids*
1<br>
22<br>
333<br>
4444<br>

```c
#include <stdio.h>
int main()
{
    int n,i,j;
    printf("enter the value for n\n");
    scanf("%d", &n);
    for (i = 1; i <= n; i++)
    {
        for (j = 1; j <= i; j++)
        {
            printf("%d", i);
        }
        printf("\n");
    }
    return 0;
}
```

</br>
1<br>
12<br>
123<br>
1234<br>

```c
#include <stdio.h>
int main()
{
    int n,i,j;
    printf("enter the value for n");
    scanf("%d", &n);
    for (i = 1; i <= n; i++)
    {
        for (j = 1; j <= i; j++)
        {
            printf("%d", j);
        }
        printf("\n");
    }
    return 0;
}
```
</br>

### *Fibonnaci Series*
```c
#include <stdio.h>
int main()
{
    int n,i;
    printf("enter the value of n:\n");
    scanf("%d", &n);
    int t1=0,t2=1,t3=t1+t2;
    printf("%d\n%d", t1,t2);
    for(i=3;i<=n;++i){
        printf("\n%d", t3);
        t1=t2;
        t2=t3;
        t3=t1+t2;
    }
    return 0;

}
```
</br>

### *Geometric Series*
```c
#include <stdio.h>
int main()
{
    int x, n, count, sum, i;
    printf("enter the value for x and n:\n");
    scanf("%d%d",&x,&n);
    i = 1;
    count = 1;
    sum = 1;
    while (i <= n)
    {
        count = count * x;
        sum = sum + count;
        i++;
    }
    printf("sum is %d", sum);
    return 0;
}
```
</br>


### *Factorial*
```c
#include<stdio.h>
void main()
{   int fact(int a);
    int n,z;
    printf("enter the number:");
    scanf("%d",&n);
    z=fact(n);
    printf("the factorial of the given number is:%d",z);
}
int fact(int a)
{   int i,c=1,res;
    for(i=1;i<=a;i++)
    {
        res=i * c;
        c=res;

    }
    return c;

} 
```
</br>

### **Using Reccursion-**
```c
#include <stdio.h>
int fact(int a);
void main()
{
    int num, res;
    printf("enter the number:");
    scanf("%d", &num);
    res = fact(num);
    printf("result is %d", res);
}
int fact(int n)
{
    if (n == 1)
    {
        return 1;
    }
    else
    {
        
        return (n * fact(n - 1));
    }
}
```
</br>

## *GCD*
```c
#include<stdio.h>
int main()
{
    int a,b,c,temp;
    int gcd(int m,int n);
    printf("enter the values for a and b.\n");
    scanf("%d%d",&a,&b);
    if(a<b){
        temp=a;
        a=b;
        b=temp;

    }
    c=gcd(a,b);
    printf("gcd of given two numbers is:%d",c);
    return 0;
}
int gcd(int m,int n){
    int rem;
    rem=m%n;
    while(rem!=0){
        m=n;
        n=rem;
        rem=m%n;

    }
    return n;
}
```
</br>

### **Using Reccursion-**
```c
#include <stdio.h>
int gcd(int m, int n);
void main()
{
    int x, y, z;
    printf("enter two numbers \n");
    scanf("%d%d", &x, &y);
    z = gcd(x, y);
    printf("gcd of two number is %d", z);
}
int gcd(int m, int n)
{
    if (n != 0)
    {
        return gcd(n, m % n);
    }
    else
    {
        return m;
    }
}
```
</br>





