---
title: "Multithreading in Java"
date: 2024-11-17
draft:  false
featured: false  
description: "Multithreading in Java"
thumbnail: "/posts/Java/Images/thread.png"
featureImage: "/posts/Java/Images/thread.png" 
shareImage: "/posts/Java/Images/thread.png"
author: "Angel Vyas"
tags:
    - Java
categories:     
    - Java
---


`Multithreading` in Java is a powerful feature that allows concurrent execution of two or more threads within a program. A thread is a lightweight subprocess and the smallest unit of processing, and multithreading helps improve the performance and efficiency of applications, especially those requiring multiple simultaneous operations.

### Key Concepts of Multithreading in Java:
`Thread`: A thread is a separate path of execution in a program. Java supports threads through the java.lang.Thread class and the java.lang.Runnable interface.

`Concurrency`: Multithreading enables Java programs to perform multiple tasks simultaneously, making better use of CPU resources. This is particularly beneficial in applications that involve heavy computations or multiple independent operations.

### Lifecycle of a Thread:

`New`: The thread is created but not yet started.
`Runnable`: The thread is ready to run and waiting for CPU allocation.
`Running`: The thread is executing its task.
`Blocked/Waiting`: The thread is temporarily inactive, waiting for resources or other threads.
`Terminated`: The thread has completed its execution.

### Creating Threads 
Threads in Java can be created in two ways:
1. By `extending` the `Thread class`.
2. or by `implementing` the `Runnable Interface`.

```java
class Mythread extends Thread {
    public void run() {
        for (int i = 10; i >= 0; i--) {
            System.out.println("Thread #1:" + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
        System.out.println("Thread #1 is finished:");

    }

    public static void main(String args[]) throws InterruptedException {
        Mythread thread1 = new Mythread();
        Myrunnable runnable1 = new Myrunnable();
        Thread thread2 = new Thread(runnable1);// in this we're passing the object of our class Myrunnabe as the thread
                                               // will start running the object which is passed into it will also start
                                               // running, like a cart connected to a horse.
        thread1.start();
        thread1.join();// if we put the value of seconds then for 3seconds thread1 will run first.(CPU utilization)
        thread2.start();
        System.out.println(1 / 0);// there is an exception still the code is running because threads are
                                  // independent of each other main thread is different, thread1 is
                                  // different,thread2 is defferent.
    }
}

class Myrunnable implements Runnable {// when we are implementing any class it must override all methods otherwise the
                                      // class will be declared abstract, Runnable class has only run method.
    public void run() {

        for (int i = 0; i <= 10; i++) {
            System.out.println("Thread #2:" + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
        System.out.println("Thread #2 is finished:");

    }
}
```

</br>

#### Some important useful methods in Java
```java
class Main {
    public static void main(String[] args) throws InterruptedException {// this will throw the exception which might
                                                                        // occur when the thread is in sleep mode while
                                                                        // in for loop.
        System.out.println(Thread.activeCount());
        Thread.currentThread().setName("MAINNN");
        System.out.println(Thread.currentThread().getName());
        Thread.currentThread().setPriority(3);
        System.out.println(Thread.currentThread().getPriority());
        System.out.println(Thread.currentThread().isAlive());
        for (int i = 3; i >= 0; i--) {
            System.out.println(i);
            System.out.println();
            Thread.sleep(1000);
        }

        Mythread thread2 = new Mythread();
        thread2.setDaemon(true);
        System.out.println(thread2.isDaemon());
        thread2.start();// this start functions executes our run function without telling it to execute.
        System.out.println(thread2.isAlive());

    }
}

class Mythread extends Thread {
    public void run() {
        System.out.println("This thread is running");

    }
}
```
