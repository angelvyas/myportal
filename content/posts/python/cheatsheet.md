### To add numbers.
```python
a=45
b=65
sum=(a+b)
print(sum)
```
**OUTPUT**

110

### To take an input from the user.
```python
name=input("name:")
age=int(input("age:"))
price=float(input("price:"))
print(name)
print(age)
print(price)
print("my name is",name, "and my age is",age, "and my price is",price)
```
**OUTPUT**

name:Arnav<br>
age:12<br>
price:45.23<br>
Arnav<br>
12
45.23
my name is Arnav and my age is 12 and my price is 45.23

### Variables
```python
#we use double quotes for string not for variables
#equal sign is called as assignment operator and convention is from right to left .
#string could be word, line or paragraph.
name="Anshika"
age="20"
value=34
value1="35"
price="56.99"
age1 = age
print("my name is:", name)
print(age1)
print(price)
#to print the datype of the given variable.
print(type(name)) 
print(type(price))
print(type(value))
print(type(value1))
```
**OUTPUT**

my name is: Anshika<br>
20<br>
56.99<br>
<class 'str'><br>
<class 'str'><br>
<class 'int'><br>
<class 'str'><br>

### Using Conditional Statements
```python
#if upper condition is stated true then we didn't check for the lower conditions.
color=input("color:")
if(color=="red"):#for checking equality we use doulbe equlaity operator.
    print("stop")
elif(color=="green"):
    print("go")
elif(color=="orange"):
    print("slow down")
else:
    print("under maintence go under your own risk")
```

**OUTPUT**

color:orange<br>
slow down

**we can skip elif and else if we want.**
```python
marks=int(input("marks:"))
if(marks >=90):
   print("detention")
elif(marks>=80 and marks<90):
   print("good")
elif(marks>=70 and marks<80):
   print("average")
elif(marks<70 and marks>=60):
   print("pass")
elif(marks<60):
   print("don't know what to do")
else:
   print("byee")
```
**OUTPUT**

marks:48<br>
don't know what to do

### Operators in Python
```python
#relational operator
a = 30
b = 40
print(a>b)
print(a>=b)
print(a<=b)
print(a<b)
print(a!=b)
print(a==b)

#assignment operator
a = 45
b=55
c=65
d=89
a+=10
print(a)#since now a has become a=a+10


#logical operators
print(not False)
print(not True)
print(True and False)
print(True or False)
print(True)
print(False)


a=50
b=20
print(not (a>b))

val1=True
val2=False
print(val1 and val2)
```

**OUTPUT**
False<br>
False<br>
True<br>
True<br>
True<br>
False<br>
55<br>
True<br>
False<br>
False<br>
True<br>
True<br>
False<br>
False<br>
False<br>

### Type Conversion
```python
#type conversion
a=50
b=60.23
print(a+b)#here python automatically considered a as 50.00 means as a float value, since float is superior then performed
#the operations.
#type casting- is done manually.
c="20"
d=60

c=int("20")#in this step we have done the casting //ly if want to change a value in float use c=float(value)
print(c+d)
print(type(c))

#can also convert integer to string value by casting.
d=23
d=str(23)
print(d)
print(type(d))
```
**OUTPUT**

110.22999999999999<br>
80<br>
<class 'int'><br>
23<br>
<class 'str'><br>

### Ternary
```python
food=input("food:")
eat="yes" if food =="chole bhature" or food == "jalebi" else "no"
print(eat)
#another way
#print("yes") if food == "jalebi" else print("no")
light=input("color:")
color=("stop","go")[light == "green"]#clever if which is single line ternary operator.
print(color)
```
**OUTPUT**

food:jalebi<br>
yes<br>
color:pink<br>
stop<br>

*Another Example*
```python
sal=float(input("salary:"))
tax=sal*(.1,.2)[sal>50000]
print(tax)
```
**OUTPUT**

salary:10000<br>
1000.0<br>

### Strings in Python
```python
p1= "angel"
p2="vyas"
print(p1+p2)#we can add two strings.
print(len(p1))#len functions is to find the length of the string, it includes spaces, works, special characters, etc.
str=p1+" "+p2
print(str)

#indexing
name="Angel Vyas"
print(name[3])
# name[3]=4
# print(name[3])#this means we can't manipulate the string elements, we can just access them.

#slicing-accessing parts of a string
#syntax:-str[starting_indx : ending_indx],ending indx is not included. For example:-
print(name[1 : 5])
print(name[2 : len(name)])
print(name[2 :])#if we do not write the ending_indx then python would understand we want to go to the end of the string.
print(name[ : 4])#if we do not write the starting_indx then python will understand we want to write from starting to the given ending_indx.
#using negative index:-
age="seventeen"
print(age[-3 : -8])#doubt
```
**OUTPUT**

angelvyas<br>
5<br>
angel vya<br>
e<br>
ngel<br>
gel Vyas<br>
gel Vyas<br>
Ange<br>


*STRING FUNCTIONS*
```python
str="my name is Angel Vyas."
print(str.endswith("yas."))
print(str.capitalize())#this will not cause any change in the original str.
print(str)#hence verified above statement.
#if we want to modify our original string:-
str=str.capitalize()
print(str)
print(str.replace("e", "o"))
print(str.replace("name", "self"))
print(str.find("a",))
print(str.find("angel"))
print(str.find("j"))#if we search for something which did not exist in your string then output will return -1.
print(str.count("angel"))#gives the count of the given word in the string you are searching for.
```
**OUTPUT**

True<br>
My name is angel vyas.<br>
my name is Angel Vyas.<br>
My name is angel vyas.<br>
My namo is angol vyas.<br>
My self is angel vyas.<br>
4<br>
11<br>
-1<br>
1<br>


### Nesting
```python
age=int(input("age:"))#if statement inside another if statement is called as nesting.
if(age>=18):
    if(age>=80):
        print("cannot drive")

    else:
        print("can drive")
else:
    print("cannot drive")
```
**OUTPUT**

age:12<br>
cannot drive



