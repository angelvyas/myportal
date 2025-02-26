---
title: "JAVA - Super and This Keyword"
date: 2024-11-17
draft:  false
featured: false  
description: "Fundamentals of Java"
thumbnail: "/posts/Java/Images/JAVA.png"
featureImage: "/posts/Java/Images/JAVA.png" 
shareImage: "/posts/Java/Images/JAVA.png"
author: "Angel Vyas"
tags:
    - Java
categories:     
    - Java
---


## *Super and This keywords of Java*
### **Super Keyword**:
`Definition`: super is a reference to the immediate parent class of the current object. It is mainly used in the context of inheritance.
</br>

`Usage`:
1. Call the parent class's constructor: super() can be used to call the constructor of the parent class. This is often used to initialize inherited fields.
2.Access parent class methods: If a method in the subclass overrides a method in the parent class, super can be used to call the parent class’s version of the method.
3. Access parent class fields: super can be used to access fields in the parent class if they are hidden by fields in the subclass.

```java
//super keyword is used to access the super class constructor.
class Rectangle {
    int length;
    int breadth;
    int x = 10;

    Rectangle(int length, int breadth) {
        this.length = length;
        this.breadth = breadth;

    }

}

class Cuboid extends Rectangle {
    int height;
    int x = 20;

    Cuboid(int l, int b, int h) {
        super(l, b);
        height = h;
    }

    void display() {
        System.out.println(super.x);
        System.out.println(x);
        System.out.println(this.x);

    }

    public static void main(String args[]) {
        Cuboid c1 = new Cuboid(10, 20, 30);
        c1.display();

    }
}
```
</br>

### **This Keyword**:

`Definition`: this is a reference to the current object whose method or constructor is being called.
</br>

`Usage`:
1. Access instance variables: When a parameter or local variable has the same name as an instance variable, this is used to distinguish between them.
2. Call another constructor in the same class: this() can be used to invoke another constructor within the same class.
3. Pass the current object as a parameter: You can pass this as an argument to another method.

```java
class Reactangle {
    int length;
    int breadth;

    Reactangle(int length, int breadth) {
        this.length = length;// if we will take the name of parameter variables same as our class variables
        // then there will be a problem since if we write length=length, it means we're
        // assigning the value to itself only and no value is assigned to our class
        // variable to avoid this we use this keyword which indicates to the class
        // variable while comparing it with parameterized variable.(this keyword is used to avoid the name conflict.)
        this.breadth = breadth;

    }

    void display() {
        System.out.println("length:" + this.length);
        System.out.println("breadth:" + this.breadth);
    }

    public static void main(String[] args) {
        Reactangle r1 = new Reactangle(2, 5);
        Reactangle r2 = new Reactangle(3, 4);
        r1.display();
        r2.display();
    }
}
```

#### `Key Differences`:
1. this refers to the current object, whereas super refers to the immediate parent class.
2. this() is used to call a constructor in the same class, while super() calls the constructor of the parent class.
3. this can only be used in non-static methods or constructors, while super can also be used similarly in instance methods or constructors.