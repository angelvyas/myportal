---
title: 'Basics of C'
date: 2024-08-24
draft:  false
featured: false  
description: "Basics of C-language"
thumbnail: "/posts/c/images/cc.png"
featureImage: "/posts/c/images/cc.png" 
shareImage: "/posts/c/images/cc.png"
author: "Angel Vyas"
tags:
    - C Language
    - Basics of C
    
categories:     
    - C Language
---

C is a powerful, general-purpose programming language that provides control over system resources and efficient execution. This post will cover some essential concepts in C that every programmer should understand: Control Strings, Global Variables, Strings, Switch Statements, Ternary Operators, Unformatted Input/Output, Bitwise Operators, and Algebraic Operations.

### Control String

Control strings are used in functions like `printf` and `scanf` to format input and output. They consist of placeholders like %d for integers, %f for floating-point numbers, and %s for strings. Here's a simple example:

```c
#include<stdio.h>
int main()
{
    int x = -23;
    float y = 2.34;
    char z[] = "angelvyas";
    long p = 2222222222;
    unsigned w = 3.4;

    printf("the value of x is %d", x);
    printf("\n the vlaue of y is %f", y);
    printf("\n the value of char is %c", z[4]);
    printf("\b the value of p is %ld", p);
    printf ("\t the value of w is %u", w);
    return 0;
}
```

### Global Variables

Global variables are declared outside of any function and can be accessed by any function in the program. They retain their value throughout the program's execution. Use global variables sparingly, as they can make debugging difficult if overused.

```c
#include <stdio.h>
#define x 20

int main()
{
    printf("hi the value of x is- %d", x);
    return 0;
}
```
</br>



### *To print a value*
```c
#include <stdio.h>
int main()
{
    int i=1;
    while(i<=10)
    {
        printf("%d \n", i);
        i++;
    }
    return 0;
}
```
</br>

### *String initialisation and printing*
```c
#include <stdio.h>
#include <string.h>
int main()
{
    //char name[7][6]={"mango","banana", "apple", "orange", "pineapple", "dragonfruit", "litchi"};
    //printf("%c",name[2][3]);

    char a[2]="ai";
    printf("%s",a[0]);
    return 0;
}
```
</br>

### *Switch Statement*
```c
#include <stdio.h>
int main()
{
    int a, b;
    char c,d;
    printf("enter the value for operators:\n");
    scanf("%d%d", &a, &b);

    scanf("%c", &c);
    printf("give the operator:\n");
    scanf("%c", &c);

    switch (c)
    {
    case '+':
        d = a + b;
        printf("answer is %d", d);
        break;
    case '*':
        d = a * b;
        printf("answer is %d", d);
        break;

    default:
        printf("no");
    }
    return 0;
}
```
</br>

### *Turnery Operator*
```c
#include <stdio.h>

int main()
{
    int a = 20;
    int b = (a < 8) ? 0 : 1;//after question mark it is if area anf after colon it is else area
    printf("the value of b is %d", b);
    return 0;

}
```
</br>

### *Unformattedinputoutput*
```c
#include <stdio.h>

int main()
{
    // getc: It reads a single character from a given input stream
    printf("Print the one char: ");
    printf("%c",getc(stdin));

    // The difference between getc() and getchar() is 
    // getc() can read from any input stream, 
    // but getchar() reads a single input character from standard input.
    //  So getchar() is equivalent to getc(stdin).
    printf("\n Example of getchar \n");
    printf("%c", getchar());
    return 0;
}
```
</br>

### *Bitwise Operator*
```c
#include <stdio.h>
int main()
{
    int a=4;
    int b=5;
    printf("the value of bitwise and %d", a&b);
    printf("the value of bitwise or %d", a|b);
    printf("the value of bitwise not %d", ~a);
    return 0;
    

} 
```
</br>

### *Scientific Notation Datatype*
```c
#include<stdio.h>
int main(){/*scientific notation datatype*/
    double a=56.23;
    char y='a';
    
    printf("%e %d",a,y);
    return 0;
}
```
</br>

## Algebraic Operations
```c
#include <stdio.h>
int main()
{   int a,b;
    printf("enter the number:");
    scanf("%d%d", &a,&b);
    printf("addition is: %d",a+b);
    printf("subtraction is:%d", a-b);
    printf("mutiplication is:%d", a * b);
    printf("modulas is:%d", a % b);
     0;
}
```
</br>

### *To take input operator and operands then perform the operation.*
```c
#include <stdio.h>
#include <math.h>
int main()
{
    int a, b;
    char c;
    printf("enter the numbers:");
    scanf("%d%d", &a, &b);
    scanf("%c", &c);
    printf("enter the operator:");
    scanf("%c", &c);
    if (c == '+')
    {
        printf("anwer:%d", a + b);
    }
    else if (c == '-')
    {
        printf("answer:%d", a - b);
    }
    else if (c == '*')
    {
        printf("answer:%d", a * b);
    }
    else
    {
        printf("answer:%d", a / b);
    }
    return 0;
}
```
</br>

