---
title: 'Important Questions of C-language'
date: 2024-08-24
draft:  false
featured: false  
description: "Important Questions of C-language"
thumbnail: "/posts/c/images/c-language.png"
featureImage: "/posts/c/images/c-language.png" 
shareImage: "/posts/c/images/c-language.png"
author: "Angel Vyas"
tags:
    - C Language
categories:     
    - C Language
---

    

### To find average of two numbers.
```c
#include <stdio.h>
int main()
{
    float a;
    float b;
    printf("give the values for a and b:\n");
    scanf("%f%f", &a,&b);
    float c=(a+b)/2;
    printf("the average of two numbers is %f\n", c);
    return 0;
}
```
</br>

### To find the binary equivalent of a number.
```c
#include <stdio.h>//LEARN!!!
int main()
{
    int n,r;
    printf("enter the values for n:");
    scanf("%d", &n);
    int binary=0,rem,count=1;
    while(n>0&&n<255){
        rem=n%2;
        binary=binary+(count*rem);
        n=n/2;
        count=count*10;
    }
    printf("the binary equivalent is %d", binary);
    return 0;
}
```
</br>

### **Using Reccursion**

```c
#include <stdio.h>
int main()
{
    unsigned i, r;
    printf("ENTER THE NUMBER:");
    scanf("%d", &i);
    //using for loop:
    // if (i < 255 && i > 0) 
    // {
    //     for (; i > 0; i = i / 2)
    //     {
    //         printf("%d", i % 2);
    //     }
    // }
    // else
    // {
    //     printf("given number is not in range");
    // }

    if (i < 255 && i > 0)
    {

        while (1)
        {
            r = i % 2;
            printf("%d", r);

            if (i / 2 == 0)
            {
                break;
            }
            else
            {
                i = i / 2;
            }
        }
    }
    else
    {
        printf("given number is not in range");
    }
}
```
</br>

### Checking whether the number is prime or not.
```c
#include <stdio.h>
int main()
{   int a,i,flag;
float b;
    printf("enter the number:\n");
    scanf("%d", &a);
    for(i=2;i<a;i++){

        if(a%i==0){
            flag=1;
            break;
            
        }}
        if(flag==0){
            printf("prime number");
        }
        else{
            printf("not prime");
        }

    
    
    return 0;
}
```
</br>

### Using Conditional Statements
```c
#include <stdio.h>
#include <string.h>

void main()
{
    int i = 0;

    if (i > 10){
        printf("value is greater then 10");
    }
    else if( i > 5 ){
        printf("value is greater then 5");
    }else if(i > 1){
        printf("value is less then 10 and 5");
    }else{
        printf("jdfjsldjflsd");
    }

    i = 1;
    switch (i)
    {
    case 1:
        printf("hi this is 1");
        break;
    case 2:
        printf("hi this is 2");
    default:
        printf("mujhe nahi pata");
    }


    // checking the condition with logical operators
    // [and &&] - [OR ||] [not !]
    i = 6;

    if (i > 4 && i < 8){
        printf(" i in the range of 4 to 6 \n ");
    }

    if (i > 4 || i < 10 ){
        printf(" i in the range of 4 and 6 \n");
    }

    if (!0){
        printf(" this is true conditions");
    }


    // printf("hi");
}
```
</br>

### To find the greatest of all of the given values.
```c
#include <stdio.h>
int main()
{
    float a, b, c;
    printf("enter the values:\n");
    scanf("%f%f%f", &a, &b, &c);
    if (a > b && a > c)
    {
        printf("the greatest of all is %f", a);
    }
    else if (b > a && b > c)
    {
        printf("the greatest of all is %f", b);
    }
    else
    {
        printf("greatest of all is %f", c);
    }
    return 0;
}
```
</br>

### To print the min and max from the list.
```c
#include <stdio.h>
int main()
{
    int a[10], n, i, max = 0,min=a[0];
    printf("\nenter the size of the list");
    scanf("%d", &n);
    printf("enter the elements of the list");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }
    printf("\nthe given list is");
    for (i = 0; i < n; i++)
    {
        printf("%d", a[i]);
        printf("\n");
    }
    for (i = 0; i < n; i++)
    {
        if (a[i] > max)
        {
            max = a[i];
        }
        if (a[i] < min)
        {   
            min = a[i];
        }
        
    }
    printf("\nmax is %d",max);
    printf("\nmin is %d",min);

    return 0;
}
```
</br>

### To print the multiplication table of a given number.
```c
#include <stdio.h>
int main()
{
    int i,j,count;
    printf("enter the number and the number of rows:");
    scanf("%d%d", &i, &j);
    for(count=1;count<=j;count++){
        printf(" \n%d * %d = %d", i, count, i * count);
    }
    return 0;
}
```
</br>

### To find the palindrome of a given value.
```c
#include <stdio.h>
int main()
{   unsigned n;
    printf("enter the value");
    scanf("%d", &n);
    int rem,num;
    int rev=0;
    num=n;
    while(num!=0){
        rem=num%10;
        rev=rev * 10+rem;
        num=num/10;
    }
    printf("reverse is %d", rev);
    if(rev==n){
        printf("\npalindrome");

    }
    else{
        printf("not palindrome\n");
    }
    return 0;
}
```
</br>

### To check whether the given number is prime or not.
```c
#include <stdio.h>
int main()
{
    int i, count;
    printf("enter the number:");
    scanf("%d", &i);
    int flag = 0;
    for (count = 2; count < i; count++)
    {
        if (i % count == 0){
            flag = 1;
            break;
        }
    }

    if(flag == 0){
        printf("Provided number is a prime number");
    }else{
        printf("Provided number is not a prime number");
    }

    return 0;
}
```
</br>

### To find the roots of a quadratic equation.
```c
#include <stdio.h>
#include <math.h>
int main()
{
    double a, b, c, r1, r2;
    printf("enter the values for a,b,c:");
    scanf("%lf%lf%lf", &a, &b, &c);
    double d = b * b - 4 * a * c;
    if (d > 0)
    {
        r1 = (-b + sqrt(d)) / (2 * a);
        r2 = (-b - sqrt(d)) / (2 * a);
        printf("r1=%lf r2=%lf", r1, r2);
    }
    else if (d == 0)
    {

        printf("roots are %lf", b / (2 * a));
    }
    else
    {
        printf("imaginary roots");
    }
}
```
</br>

### Range of a value.
```c
#include<stdio.h>
int main()
{
    int x = 21500000000; //it is out of the range that's why it will print any garbage value
    printf("the value of x is %d", x);
    return 0;
}
```
</br>

### To find the reverse of a given number.
```c
#include <stdio.h>
int main()
{
    int i, j, k;
    printf("ENTER THE NUMBER:");
    scanf("%d", &i);
    int n = 10;
    printf("%d", i % 10);
    j = i / 10;
    printf("%d", j % 10);
    k = i / 100;
    printf("%d", k);

    return 0;
}
```
</br>

### To calculate simple of compound interest.
```c
#include <stdio.h>
int main()
{
    float p, r, t, f;
    printf("ENTER THE VALUES FOR P,R,T:");
    scanf("%f%f%f", &p, &r, &t);
    float s = (p * r * t) / 100;
    float d = 1 + r / 100;
   
   
    int count;
    float rem;
    for (count = 1; count < t; count++)
    {
        d *= d;
    }
    printf("\n SIMPLE INTEREST:%f", s);
    printf("\n COMPOUND INTEREST:%f", p * d);
    return 0;
}
```
</br>

### Using sizeof function.
```c
#include <stdio.h>
int main(){
    int a;
    float b;
    double c;
    char d;
    printf("\n the size of integer is %ld", sizeof(a));
    printf("\n the size of float is %ld", sizeof(b));
    printf("\n the size of double is %ld", sizeof(c));
    printf("\n the size of character is %ld", sizeof(d));
    return 0;

}
```
</br>

### To find the sum of the digits of a number.
```c
#include <stdio.h>
int main()
{   unsigned n;
int rem,sum=0;
    printf("enter the number:");
    scanf("%u", &n);
    while(n!=0){
        rem=n%10;
        sum=sum+rem;
        n=n/10;
    }
    printf("the sum is:%d\n",sum);
    return 0;
}
```