---
title: "JAVA EXAMPLE CODES"
date: 2024-12-17
draft:  false
featured: false  
description: "JAVA CODES"
thumbnail: "/posts/Java/Images/JAVA.jpg"
featureImage: "/posts/Java/Images/JAVA.jpg" 
shareImage: "/posts/Java/Images/JAVA.jpg"
author: "Angel Vyas"
tags:
    - Java
categories:     
    - Java
---

</br>
</br>

<h2> Here, you can find some basic Java example codes to help you get started. These examples cover a variety of fundamental concepts and are great for beginners looking to practice and learn.</h2>


### 1-D
```java
class D1
{
public static void main(String[] args)
{
int month_days[];
month_days=new int[12];
month_days[0]=31;
month_days[1]=28;
month_days[2]=31;
month_days[3]=30;
month_days[4]=31;
month_days[5]=30;
month_days[6]=31;
month_days[7]=31;
month_days[8]=30;
month_days[9]=31;
month_days[10]=30;
month_days[11]=31;
System.out.println("january has:"+month_days[0]+"days");
}
}
```
### 2-D
```java
class TwoDArray
{

public static void main(String [] args)
{
int twoD[][]=new int[4][5];
int i,j,k=0;
for(i=0;i<4;i++)
for(j=0;j<5;j++)
{
twoD[i][j]=k;
k++;
}
for(i=0;i<4;i++)
{
for(j=0;j<5;j++)
{
System.out.print(twoD[i][j]+" ");
}
System.out.println( );
}
}
```
### 3-D
```java
class ThreeDArray
{
public static void main(String[] args)
{
int threeD[][][]=new int[3][4][5];
int i,j,k;
for(i=0;i<3;i++)
for(j=0;j<4;j++)
for(k=0;k<5;k++)
threeD[i][j][k]=i*j*k;
for(i=0;i<3;i++)
{
for(j=0;j<4;j++)
{
for(k=0;k<5;k++)
{
System.out.print(threeD[i][j][k]+" ");
}
System.out.println();

}
System.out.println();
}
}
}
```
### Abstract class
```java
abstract class Figure
{
double dim1,dim2;
Figure(double a,double b)
{
dim1=a;
dim2=b;
}

//area is now an abstract method
abstract double area();
}
class Rectangle extends Figure
{
Rectangle(double a,double b)
{
super(a,b);
}
//override area for rectangle
double area()
{
System.out.println("Inside Area for Rectangle:");
return dim1*dim2;
}
}
class Triangle extends Figure
{
Triangle(double a, double b)
{
super(a,b);
}
//override area for right triangle
double area()

{
System.out.println("Inside Area for Triangle");
return dim1*dim2/2;
}
}
class AbstractAreas
{
public static void main(String args[])
{
//Figure f=new Figure(10,10);//illegal now
Rectangle r=new Rectangle(9,5);
Triangle t=new Triangle(10,8);
Figure figref;//this is OK,no object is created
figref=r;
System.out.println("Area is:"+figref.area());
figref=t;
System.out.println("Area is"+figref.area());
}
}
```
### Adapter Class
```java
/*6. Write a Java program to illustrate adapter class. */
Import java.awt.*;
Import java.awt.event.*;
Import java.applet.*;
/*&lt;applet code=”AdapterDemo” width=500 height=500&gt;
&lt;/applet&gt;
*/
Public class AdapterDemo extends Applet
{
Public void init()
{
addMouseListener(new MyMouseAdapter(this));
addMouseMotionListener(new MyMouseMotionAdapter(this));
}
}

Class MyMouseAdapter extends MouseAdapter
{
AdapterDemo adapterDemo;
Public MyMouseAdapter(AdapterDemo adapterDemo)
{
this.adapterDemo=adapterDemo;
}
Public void mouseClicked(MouseEvent me)
{
adapterDemo.showStatus(“Mouse Clicked”);
}
}
Class MyMouseMotionAdapter extends MouseMotionAdapter
{
AdapterDemo adapterDemo;
Public MyMouseMotionAdapter(AdapterDemo adapterDemo)
{
this.adapterDemo=adapterDemo;
}
Public void mouseDragged(MouseEvent me)
{
adapterDemo.showStatus(“Mouse Dragged”);
}
}
```
### Classes and Objects in Java
```java
class Box
{
double w,h,d;
}
class BoxDemo
{
public static void main(String[] args)
{
Box mybox=new Box();
double volume;
mybox.w=10;
mybox.h=10;
mybox.d=10;

volume=mybox.h*mybox.d*mybox.w;
System.out.println("volume=:"+volume);
}

}
```
### Methods in Java
```java
class Box
{
double width,height,depth;
void volume()
{
System.out.println("volume is:");
System.out.println(width*height*depth);
}}
class BoxDemo3
{
public static void main(String[] args)
{
Box mybox1=new Box();
Box mybox2=new Box();
mybox1.width=10;
mybox1.height=20;
mybox1.depth=15;
mybox2.width=3;

mybox2.height=6;
mybox2.depth=9;
mybox1.volume();
mybox2.volume();

}
}
```

### Inner Class
```java
class Outer
{
int outer_x=100;
void test()
{
Inner inner=new Inner();
inner.display();
}
class Inner
{
void display()
{
System.out.println("display:outer_x="+outer_x);
}
}
}
class InnerClass
{
public static void main(String[] args)
{
Outer outer =new Outer();
outer.test();
}

}
```
### MultiLevel Inheritance
```java
class A
{
    int a;
    void showA()
    {
        System.out.println("a:"+a);
    }
}
class B extends A
{
    int b;
    void showB()
    {
        System.out.println("b:"+b);
    }
}
class C extends B
{
    int c;
    void showC()
    {
        System.out.println("c:"+c);
    }
}
class MultiLvlInheritance
{
    public static void main(String args[])
    {
        A ob = new A();
        ob.a = 10;
        ob.showA();
        C ob1 = new C();
        ob1.a= 12;
        ob1.b = 15;
        ob1.c = 18;
        ob1.showA();
        ob1.showB();
        ob1.showC();
    }
}
```

### Overriding
```java
class A
{

int i,j;
A(int a,int b)
{
i=a;
j=b;
}
void show()
{
System.out.println("i and j:"+i+""+j);
}
}
class B extends A
{
int k;
B(int a,int b,int c)
{
super(a,b);
k=c;
}
void show()
{
super.show();
System.out.println("k:"+k);
}

}
class Override
{
public static void main(String[] args)
{
B subob=new B(1,2,3);
subob.show();
}
}
```
### Overload
```java
class OverLoad
{
void test()
    {System.out.println("No parameters");
    }
void test(int a)
{
    System.out.println("a="+a);
}
void test(int a , int b)
{
    System.out.println("a and b:"+a+" & "+b);
}
double test(double a)
{
    System.out.println("double a :"+a);
    return a*a;
}
}
class OverLoadDemo
{
    public static void main(String args[])
    {
        OverLoad ob = new OverLoad();
        double result;
        ob.test();
        ob.test(10);
        ob.test(10,20);
        result= ob.test(123.4);
        System.out.println("Result of ob.test(123.4:)"+result);
    }
}
```
### Call By Reference
```java
class Test
{
    int a,b;
    Test(int i, int j)
    {
        a=i;
        b=j;
    }
    void meth(Test o)
    {o.a*=2;
     o.b/=2;
    }
}
class CallByRef
{
        public static void main(String args[])
        {
            Test ob = new Test(15,20);
            System.out.println("ob.a and ob.b before call:"+ob.a+" "+ob.b);
            ob.meth(ob);
            System.out.println("ob.a and ob.b after call:"+ob.a+" "+ob.b);
        }

}
```
### Return an Object
```java
class Test
{
 int a;
 Test(int i)
 {
    a=i;
 }
 Test incrByten()
 {
    Test temp = new Test(a+10);
    return temp;
 }
}
class RetrOb
{
    public static void main(String args[])
    {
        Test ob1 = new Test(2);
        Test ob2;
        ob2 = ob1.incrByten();
        System.out.println("ob1.a:"+ob1.a);
        System.out.println("ob2.a:"+ob2.a);
        ob2 = ob2.incrByten();
        System.out.println("ob2.a after second increment:"+ob2.a);
    }
}
```
### Reccursion
```java
class factorial{
    int fact(int n)
    {
        if(n==1)
        return 1;
        
        else
        return (fact(n-1)*n);
    }
    public static void main(String args[]){
        factorial f=new factorial();
        System.out.println("factorial of 3 is:"+f.fact(3));
        System.out.println("factorial of 10 is:"+f.fact(10));
    }
}
```

### Passing object as a Parameter
```java
class Test {
    int a, b;

    Test(int i, int j) {
        a = i;
        b = j;

    }

    Boolean equals(Test o) {
        if (o.a == a && o.b == b) {
            return true;
        } else {
            return false;
        }
    }
}

class Passob {
    public static void main(String[] args) {
        Test ob1 = new Test(100, 22);
        Test ob2 = new Test(100, 22);
        Test ob3 = new Test(-1, -1);
        System.out.println("ob1==ob2" + ob1.equals(ob2));
        System.out.println("ob1==ob3" + ob1.equals(ob3));
    }
}
```

### Multiple Inheritance Using Interface
```java
interface I {
    void meth();
}

class A {
    void meth1() {
        System.out.println("defined in class A");
    }

}

class B extends A implements I {
    public void meth() {
        System.out.println("defined in class B");
    }
}

class MultiInheritance {
    public static void main(String[] args) {
        B ob = new B();
        ob.meth();
        ob.meth1();
    }
}
```


### Single Level Inheritance
```java
class A
{
int i,j;
void showij()
{
System.out.println("i and j:"+i+" "+j);
}
}
//create a subclass by extending class A
class B extends A
{
int k;

void showk()
{
System.out.println("k:"+k);
}
void sum()
{
System.out.println("i+j+k:"+(i+j+k));
}
}
class SimpleInheritance
{
public static void main(String args[])
{
A superob=new A();
B subob=new B();
//The superclass may be used by itself
superob.i=10;
superob.j=20;
System.out.println("Contents of superob:");
superob.showij();
System.out.println();
/*The subclass has access to all public members of its
superclass*/
subob.i=7;

subob.j=8;
subob.k=9;
System.out.println("Contents of subob:");
subob.showij();
subob.showk();
System.out.println("Sum of i,j&k in subob");
subob.sum();
}
}
```

### Static Keyword
```java
class StaticDemo
{
static int a=10;

static int b;
static void meth(int x)
{
System.out.println("x="+x);
System.out.println("a="+a);
System.out.println("b="+b);
}
static
{
System.out.println("static block initialized");
b=a*4;
}
public static void main(String[] args)
{
meth(20);
}
}
```

### String class 
```java
class stringTest {
    public static void main(String[] args) {
        String s = "welcome to java programming";
        System.out.println(s);
        System.out.println("string length=" + s.length());
        System.out.println("character at 3rd position=" + s.charAt(3));
        System.out.println(s.substring(3));
        System.out.println("substring=" + s.substring(2, 5));
        String s1 = "java";
        String s2 = "programming";
        System.out.println("concatenated string=" + s1.concat(s2));
        String s4 = "learn code learn";
        System.out.println("Index of Learn" + s4.indexOf("Learn"));
        System.out.println("Index of a=" + s4.indexOf('a', 3));
        Boolean out = "java".equals("java");
        System.out.println("checking equality" + out);
        out = "Java".equalsIgnoreCase("java");
        System.out.println("checking equality" + out);
        int out1 = s1.compareTo(s2);
        System.out.println("the difference between ASCII values is" + out1);
        String word1 = "JAVA PROGRAMMING";
        System.out.println("changing to lower case" + word1.toLowerCase());
        String word2 = "java programming";
        System.out.println("changing to upper case:" + word2.toUpperCase());
        String str1 = "frogramming";
        System.out.println("original string" + str1);
        String str2 = "frogramming".replace('f', 'p');
        System.out.println("replaced f with p" + str2);

    }
}
```

### Super Keyword(to access super class constructor.)
```java
class SuperTest

{
int a;
char c;
float f;
SuperTest(int a,char c,float f)
{
this.a=a;
this.c=c;
this.f=f;
}
void print()
{
System.out.println("a="+a+""+"c="+c+""+"f="+f);
}
}
class SubTest extends SuperTest
{
SubTest()
{
Super(12,'N',12.3f);
public static void main(String[] args)
{
SubTest st=new SubTest();
st.print();

}
}
}
```
### Super keyword another program
```java
class A
{
int i;
}
//create a subclass by extending class A
class B extends A
{
int i;//this i hides the i in A
B(int a,int b)
{
super.i=a;//i in A
i=b;//i in B

}
void show()
{
System.out.println("i in superclass:"+super.i);
System.out.println("i in subclass:"+i);
}
}
class UseSuper
{
public static void main(String args[])
{
B subob=new B(1,2);
subob.show();
}
}
```
### This Keyword
```java 
class This
{
int a=12;
void meth(int a)
{
System.out.println(a);
System.out.println(this.a);
}
public static void main(String[] args)
{
This td=new This();
td.meth(10);
System.out.println(td.a);
}}
```

### Typecasting
```java
class TypeCasting
{
public static void main(String[] args)
{
int i=257;

byte b;
double d=323.123;
System.out.println("int to byte conversion");
b=(byte)i;
System.out.println("i and b are:"+i+" "+b);
System.out.println("double to int conversion");
i=(int)d;
System.out.println("i and d are:"+i+" "+d);
System.out.println("double to byte conversion");
b=(byte)d;
System.out.println("b and d are:"+b+" "+d);
}
}
```
### Abstract Class
```java
abstract class Figure
{
double dim1,dim2;
Figure(double a,double b)
{
dim1=a;
dim2=b;
}

//area is now an abstract method
abstract double area();
}
class Rectangle extends Figure
{
Rectangle(double a,double b)
{
super(a,b);
}
//override area for rectangle
double area()
{
System.out.println("Inside Area for Rectangle:");
return dim1*dim2;
}
}
class Triangle extends Figure
{
Triangle(double a, double b)
{
super(a,b);
}
//override area for right triangle
double area()

{
System.out.println("Inside Area for Triangle");
return dim1*dim2/2;
}
}
class AbstractAreas
{
public static void main(String args[])
{
//Figure f=new Figure(10,10);//illegal now
Rectangle r=new Rectangle(9,5);
Triangle t=new Triangle(10,8);
Figure figref;//this is OK,no object is created
figref=r;
System.out.println("Area is:"+figref.area());
figref=t;
System.out.println("Area is"+figref.area());
}
}
```

## LAB CYCLE:
### Traffic light
```java
/*10. Write a Java program that simulates a traffic light. The program lets the user select one of three
lights: red, yellow, or green with radio buttons. On selecting a button, an appropriate message with
“Stop” or “Ready” or “Go” should appear above the buttons in selected color. Initially, there is no
message shown.*/
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
class TrafficLight1 extends JFrame implements ActionListener
{
String msg=" " ;
private JLabel label;
private JTextField display;
private JRadioButton r1,r2,r3;
private ButtonGroup bg;
private Container c;
public TrafficLight1()
{
setLayout(new FlowLayout());
c=getContentPane();
label=new JLabel(" Traffic Light");
display =new JTextField(10);
r1=new JRadioButton("RED");
r2=new JRadioButton("GREEN");
r3=new JRadioButton("YELLOW");
bg=new ButtonGroup();
c.add(label);
c.add(r1);
c.add(r2);
c.add(r3);
c.add(display);
bg.add(r1);
bg.add(r2);
bg.add(r3);
r1.addActionListener(this);
r2.addActionListener(this);
r3.addActionListener(this);
setSize(400,400);
setVisible(true);
c.setBackground(Color.pink);
}
public void actionPerformed(ActionEvent ie)
{
msg=ie.getActionCommand();
if (msg.equals("RED"))
{
c.setBackground(Color.RED);
display.setText(msg+ " :TURN ON");
}
else if (msg.equals("GREEN"))
{
c.setBackground(Color.GREEN);
display.setText(msg+ " :TURN ON");
}
else if (msg.equals("YELLOW"))
{
c.setBackground(Color.YELLOW);
display.setText(msg+ " :TURN ON");
}
}
public static void main(String args[])
{
TrafficLight1 light=new TrafficLight1();
light.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
}

```

### Table
```java
/*12. Suppose that a table named Table.txt is stored in a text file. The first line in the file is the
header, and the remaining lines correspond to rows in the table. The elements are separated by
commas. Write a java program to display the table using Labels in Grid Layout.*/
import java.io.*;
import java.util.*;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.event.*;
class A extends JFrame 
{
public A() 
{
setSize(400,400);
setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
GridLayout g=new GridLayout(0,3);
setLayout(g);
try 
{
FileInputStream fin = new FileInputStream("D:/java/emp.txt");
Scanner sc = new Scanner(fin).useDelimiter(",");
String[] arrayList;
String a;
while (sc.hasNextLine()) 
{
a=sc.nextLine();
arrayList=a.split(",");
for (String i:arrayList) 
{
add(new JLabel(i));
}
}
} 
catch (Exception ex) 
{
}
setDefaultLookAndFeelDecorated(true);
pack();
setVisible(true);
}
}
public class Tb2 
{
public static void main(String[] args) 
{
A a = new A();
}
}


```

### PC Fixed

```java
/*2. Correct implementation of Producer-Consumer*/
class Q {
int n;
boolean available = false;
synchronized int get() {
while(available==false)
try {
wait();
} catch(InterruptedException e) {
System.out.println("InterruptedException caught");
}
System.out.println("Got: " + n);
available = false;
notify();
return n;
}
synchronized void put(int n) {
while(available==true)
try {
wait();
} catch(InterruptedException e) {
System.out.println("InterruptedException caught");
}
this.n = n;
available = true;
System.out.println("Put: " + n);
notify();
}
}
class Producer implements Runnable {
Q q;
Producer(Q q) {
this.q = q;
new Thread(this, "Producer").start();
}
public void run() {
int i = 0;
while(true) {
q.put(i++);
}
}
}
class Consumer implements Runnable {
Q q;
Consumer(Q q) {
this.q = q;
new Thread(this, "Consumer").start();
}
public void run() {
while(true) {
q.get();
}
}
}
class PCFixed1 {
public static void main(String args[]) {
Q q = new Q();
new Producer(q);
new Consumer(q);
System.out.println("Press Control-C to stop.");
}
}
```

### multi thread application
```java
    /*1. Write a java Program that implements a multi-thread application that has three threads. First
thread generates random integer every 1 second and if the value is even, second thread computes the
square of the number and prints. If the value is odd, the third thread will print the value of cube of the
number.*/
 import java.util.Random;
class Square extends Thread
{
int x;
Square(int n)
 	{
 		x = n;
 	}
 	public void run()
 	{
 		int sqr = x * x;
 System.out.println("Square of " + x + " = " + sqr );
 	}
}
class Cube extends Thread
{
 	int x;
 	Cube(int n)
 	{
 		x = n;
 	}
 	public void run()
 	{
 		int cub = x * x * x;
 System.out.println("Cube of " + x + " = " + cub );
}
}
class Number extends Thread
{
public void run()
 	{
 Random random = new Random();
 for(int i =0; i<10; i++)
 		{
 int randomInteger = random.nextInt(100);
 System.out.println("Random Integer generated : " + randomInteger);
if(randomInteger%2==0)
{
Square s = new Square(randomInteger);
 			s.start();
		}
		else
		{	
			Cube c = new Cube(randomInteger);
 				c.start();
 			}
try 
{
 Thread.sleep(1000);
 			} 
catch (InterruptedException ex) 
{
System.out.println(ex);
}
 		}
 	}
}
public class MultipleThreads 
{
public static void main(String args[])
 	{
 Number n = new Number();
 		n.start();
 	}
}

```
### Mouse Events
```java
/*Write a Java program to handle mouse events.*/
import java.awt.*;
import java.awt.event.*;
import java.applet.*;
/*<applet code="MouseEvents" width=100 height=100>
</applet>
*/
public class MouseEvents extends Applet implements 
MouseListener,MouseMotionListener{
String msg=" ";
int mouseX=0,mouseY=0;
public void init(){
addMouseListener(this);
addMouseMotionListener(this);
}
public void mouseClicked(MouseEvent me){
mouseX=0;
mouseY=10;
msg="Mouseclicked";
repaint();
}
public void mouseEntered(MouseEvent me){
mouseX=0;
mouseY=10;
msg="Mouseentered";
repaint();
}
public void mouseExited(MouseEvent me){
mouseX=0;
mouseY=10;
msg="Mouseexited";
repaint();
}
public void mousePressed(MouseEvent me){
mouseX=me.getX();
mouseY=me.getY();
msg="down";
repaint();
}
public void mouseReleased(MouseEvent me){
mouseX=me.getX();
mouseY=me.getY();
msg="up";
repaint();
}
public void mouseDragged(MouseEvent me){
mouseX=me.getX();
mouseY=me.getY();
msg="*";
showStatus("dragging mouse at"+mouseX+","+mouseY);
repaint();
}
public void mouseMoved(MouseEvent me){
showStatus("movingmouse at"+me.getX()+","+me.getY());
}
public void paint(Graphics g){
g.drawString(msg,mouseX,mouseY);
}
}


```

### Keyboards Events
```java
/*5. Write a Java program to handle keyboard events.*/
import java.awt.*;
import java.awt.event.*;
import java.applet.*;
/*<applet code="SimpleKey" width=300 height=100>
</applet> */
public class SimpleKey extends Applet implements KeyListener{
String msg=" ";
int X=10,Y=20;
public void init(){
addKeyListener(this);
}
public void keyPressed(KeyEvent ke){
showStatus("key down");
}
public void keyReleased(KeyEvent ke){
showStatus("Key up");
} 
public void keyTyped(KeyEvent ke){
msg+=ke.getKeyChar();
repaint();
}
public void paint(Graphics g){
g.drawString(msg,X,Y);
} }

```

### Integer Division
```java
/*9. Write a Java program that creates a user interface to perform integer divisions. The user enters
two numbers in the text fields, Num1 and Num2. The division of Num1 and Num 2 is displayed in the
Result field when the Divide button is clicked. If Num1 or Num2 were not an integer, the program
would throw a Number Format Exception. If Num2 were Zero, the program would throw an
Arithmetic Exception. Display the exception in a message dialog box.*/
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
public class Division extends JFrame
implements ActionListener
{
Container c;
JButton btn;
JLabel lbl1,lbl2,lbl3;
JTextField tf1,tf2,tf3;
JPanel p;
Division()
{
super("Exception Handler");
c=getContentPane();
c.setBackground(Color.red);
btn=new JButton("DIVIDE");
btn.addActionListener(this);
tf1=new JTextField(30);
tf2=new JTextField(30);
tf3=new JTextField(30);
lbl1=new JLabel("NUM 1");
lbl2=new JLabel("NUM 2");
lbl3=new JLabel("RESULT");
p=new JPanel();
p.setLayout(new GridLayout(3,2));
p.add(lbl1); p.add(tf1);
p.add(lbl2); p.add(tf2);
p.add(lbl3); p.add(tf3);
c.add(new JLabel("Division"),"North");
c.add(p,"Center");
c.add(btn,"South");
}
public void actionPerformed(ActionEvent e)
{
if(e.getSource()==btn)
{
try 
{
int a=Integer.parseInt(tf1.getText());
int b=Integer.parseInt(tf2.getText());
int c=a/b;
tf3.setText(""+c);
}
catch(NumberFormatException ex)
{
tf3.setText("--");
JOptionPane.showMessageDialog(this,"Only Integer Division");
}
catch(ArithmeticException ex)
{
tf3.setText("--");
JOptionPane.showMessageDialog(this,"Division by zero");
}
catch(Exception ex)
{
tf3.setText("--");
JOptionPane.showMessageDialog(this,"Other Err "+ex.getMessage());
}
}
}
public static void main(String args[])
{
Division b=new Division();
b.setSize(300,300);
b.setVisible(true);
}
}
```

### Files
```java
/*14. Write a Java program to list all the files in a directory including the files present in all its
subdirectories.Note:the directory what I have taken is event handling try with your own directories*/
import java.io.*;
class DirList1
{
public static void main(String args[])
{
String dname="/event handling";
File myDir=new File(dname);
if(myDir.isDirectory())
{
File arr[]=myDir.listFiles();
RecursivePrint(arr, 0); 
}
}
static void RecursivePrint(File[] arr, int level) 
{ 
for (File f : arr) 
{ 
// tabs for internal levels 
for (int i = 0; i < level; i++) 
System.out.print("\t"); 
if(f.isFile()) 
System.out.println(f.getName()+"is a file"); 
else if(f.isDirectory()) 
{ 
System.out.println(f.getName()+"is a directory"); 
// recursion for sub-directories 
RecursivePrint(f.listFiles(), level + 1); 
}
} 
} 
}

```

### Factorial
```java
/*8. Develop an applet in Java that receives an integer in one text field, and computes its factorial
Value and returns it in another text field, when the button named “Compute” is clicked.*/
import java.awt.*;
import java.awt.event.*;
import java.applet.*;
/* <applet code="Compute1" width=300 height=300>
</applet>
*/
public class Compute1 extends Applet implements
ActionListener
{
Button btn,cbtn;
Label lb1,lb2;
TextField tf1,tf2;
public void init()
{
btn=new Button("Compute");
cbtn=new Button("Clear");
btn.addActionListener(this);
cbtn.addActionListener(this);
tf1=new TextField(30);
tf2=new TextField(30);
lb1=new Label("Number");
lb2=new Label("Result");
setLayout(new GridLayout(3,2));
add(lb1);
add(tf1);
add(lb2);
add(tf2);
add(btn);
add(cbtn);
}
public void actionPerformed(ActionEvent ae)
{
if(ae.getSource()==btn)
{
int a=Integer.parseInt(tf1.getText());
int fact=1;
for(int i=1;i<=a;i++)
{
fact=fact*i;
}
tf2.setText(""+fact);
}
else
{
tf1.setText("");
tf2.setText("");
}
}
}
```

### Calculator
```java
/*7. Write a Java program that works as a simple calculator. Use a grid layout to arrange buttons for
the digits and for the +, -,*, % operations. Add a text field to display the result. Handle any possible
exceptions like divided by zero.*/
/* <applet code="Math1" width=500 height=500>
</applet>
*/
import java.awt.*;
import java.awt.event.*;
import java.applet.*;
public class Math1 extends Applet implements ActionListener
{ Button 
b1,b2,b3,b4,b5,b6,b7,b8,b9,b0,clear,add,minus,mul,div,clc,equal;
TextField tf;
String msg="",op="-";
int b,a,count;
public void init()
{
b1=new Button("1");
b2=new Button("2");
b3=new Button("3");
b4=new Button("4");
b5=new Button("5");
b6=new Button("6");
b7=new Button("7");
b8=new Button("8");
b9=new Button("9");
b0=new Button("0");
clear=new Button("C");
add=new Button("+");
minus=new Button("-");
mul=new Button("*");
div=new Button("/");
equal=new Button("=");
b1.addActionListener(this);
b2.addActionListener(this);
b3.addActionListener(this);
b4.addActionListener(this);
b5.addActionListener(this);
b6.addActionListener(this);
b7.addActionListener(this);
b8.addActionListener(this);
b9.addActionListener(this);
b0.addActionListener(this);
add.addActionListener(this);
minus.addActionListener(this);
mul.addActionListener(this);
div.addActionListener(this);
clear.addActionListener(this);
equal.addActionListener(this);
tf=new TextField(30);
setLayout(new GridLayout(5,5));
add(tf);
add(clear);
add(equal);
add(div);
add(b0);
add(b1);
add(b2);
add(b3);
add(add);
add(b4);
add(b5);
add(b6);
add(minus);
add(b7);
add(b8);
add(b9);
add(mul);
}
public void actionPerformed(ActionEvent ae)
{ switch(ae.getActionCommand())
{ case "1": msg=msg+"1";
tf.setText(msg);
break;
case "2": msg=msg+"2";
tf.setText(msg);
break;
case "3": msg=msg+"3";
tf.setText(msg);
break;
case "4": msg=msg+"4";
tf.setText(msg);
break;
case "5": msg=msg+"5";
tf.setText(msg);
break;
case "6": msg=msg+"6";
tf.setText(msg);
break;
case "7": msg=msg+"7";
tf.setText(msg);
break;
case "8": msg=msg+"8";
tf.setText(msg);
break;
case "9": msg=msg+"9";
tf.setText(msg);
break;
case "0": msg=msg+"0";
tf.setText(msg);
break;
case "+": if(count==0)
{ b=Integer.parseInt(tf.getText());
op="+";
tf.setText("");
msg="";
count++;
}
else
{ a=Integer.parseInt(tf.getText());
Math2(b,a,op);
op="+";
tf.setText("");
msg="";
}
break;
case "-": if(count==0)
{
b=Integer.parseInt(tf.getText());
op="-";
tf.setText("");
msg="";
count++;
}
else
{
a=Integer.parseInt(tf.getText());
Math2(b,a,op);
op="-";
tf.setText("");
msg="";
}
break;
case "*": if(count==0)
{
b=Integer.parseInt(tf.getText());
op="*";
tf.setText("");
msg="";
count++;
}
else
{
a=Integer.parseInt(tf.getText());
Math2(b,a,op);
op="*";
tf.setText("");
msg="";
}
break;
case "/": if(count==0)
{
b=Integer.parseInt(tf.getText());
op="/";
tf.setText("");
msg="";
count++;
}
else
{
a=Integer.parseInt(tf.getText());
Math2(b,a,op);
op="/";
tf.setText("");
}
msg="";
break;
case "C": tf.setText("");
b=0;
msg="";
count=0;
break;
case "=": a=Integer.parseInt(tf.getText());
Math2(b,a,op);
tf.setText(""+b);
count=0;
msg="";
break;
}
}
public void Math2(int b1,int a1,String op1)
{
switch(op1)
{
case "+": b=b1+a1;
break;
case "-": b=b1-a1;
break;
case "*": b=b1*a1;
break;
case "/": b=b1/a1;
break;
}
}
}


```

### Double Linked List
```java
public class ddl
{
class node
{
int data;
node prev;
node next;
public node(int data)
{
this.data=data;
}
}
node head,tail=null;
public void addNode(int data)
{
node newNode= new node(data);
if(head==null)
{
head=tail=newNode;
head.prev=null;
tail.next=null;
}
else
{
tail.next=newNode;
newNode.prev=tail;
tail=newNode;
tail.next=null;
}
}
public void displayF()
{
node current=head;
if(head==null)
{
System.out.println("List is empty");
return;
}
System.out.println("nodes of ddl FORWARD:");
while(current!=null)
{
System.out.print(current.data+" ");
current=current.next;
}
System.out.println();
}
public void displayB()
{
node current=tail;
if(tail==null)
{
System.out.println("List is empty");
return;
}
System.out.println("nodes of ddl BACKWARD:");
while(current!=null)
{
System.out.print(current.data+" ");
current=current.prev;
}
System.out.println();
}
public void deletenode(int key)
{ 
node temp = head, prev = null; 
if (temp != null && temp.data == key)
{
head = temp.next;
return;
} 
while (temp != null && temp.data != key)
{
prev = temp;
temp = temp.next;
} 
if (temp == null)
return;
prev.next = temp.next;
}
public static void main(String args[])
{
ddl d = new ddl();
d.addNode(1);
d.addNode(2);
d.addNode(3);
d.addNode(4);
d.addNode(5);
d.displayF();
d.displayB();
d.deletenode(2);
System.out.println("after deletion");
d.displayF();
}
}
```