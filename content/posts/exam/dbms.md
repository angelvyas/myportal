---
title: "..."
date: 2025-06-15
draft:  false
featured: false  
description: ""
thumbnail: "/posts/docker/images/"
featureImage: "/posts/docker/images/"
shareImage: "/posts/docker/images/"
author: "Angel Vyas"
tags:
    - dbms
          
categories:     
    - general
    
---

### plsql to update salary of employee 20% manager, 15% salesman and 10% for others.
declare</br>
job emp.job%type;</br>
esal emp.sal%type;</br>
eno emp.eit%type;</br>
inc number(7,2);</br>
begin</br>
eno:=: eid;</br>
select job into ejob from emp where eid=eno;</br>
if ejob='Manager' then</br>
inc:=0.2;</br>
update emp set salary =salary+salary * inc where eid=eno;</br>
dbms_output.put_line('Manager sal is updated');</br>
else if</br>
inc:=0.15;</br>
update emp set salary=salary+salary * inc where eid=eno;</br>
dbms_output.put_line('others sal is updated);</br>
end if;</br>
end;</br>

### Write a Procedure for Fibonacci series 
create or replace procedure fib(n number) as   </br>
a number:=0; </br>
b number:=1; </br>
c number; </br>
i number; </br>
begin </br>
dbms_output.put_line(a); </br>
dbms_output.put_line(b); </br>
for i in 3..n loop </br>
c:=a+b; </br>
a:=b; </br>
b:=c; </br>
dbms_output.put_line(c); </br>
end loop; </br>
end; </br>
Procedure created. </br>
declare </br>
n number(10); </br>
begin </br>
n:=:n; </br>
fib(n); </br>
end; </br>
input: 5 </br>
</br>
output:  </br>
0 </br>
1 </br>
1 </br>
2 </br>
3 </br>
 </br>
Statement processed.</br>

### Update sal using sal
create or replace procedure empupdate(eno emp.empno%type, inc number)as</br> 
  begin </br>
  update emp set sal=sal+inc where empno=eno;</br>
commit; </br>
  dbms_output.put_line('update successfully'); </br>
  end; </br>
declare </br>
eno emp.empno%type; </br>
inc number; </br>
begin </br>
eno:=:eno; </br>
inc:=:inc; </br>
empupdate(eno,inc); </br>
end; </br>
select * from emp; </br>


### Swapping of two numbers
  t number; </br>
   begin </br>
   t:=a; </br>
   a:=b; </br>
  b:=t; </br>
  end; </br>
 </br>
declare </br>
 a number:=:a; </br>
 b number:=:b; </br>
 begin </br>
 dbms_output.put_line('before swapping'||a||','||b); </br>
swap(a,b); </br>
 dbms_output.put_line('after swapping'||a||','||b);</br> 
end; </br>

### Function to find max of two numbers
DECLARE  </br>
   a number;  </br>
   b number;  </br>
   c number;  </br>
FUNCTION findMax(x IN number, y IN number)   </br>
RETURN number  </br>
IS  </br>
    z number;  </br>
BEGIN  </br>
   IF x > y THEN  </br>
      z:= x;  </br>
   ELSE  </br>
      Z:= y;  </br>
   END IF;   </br>
   RETURN z;  </br>
END;  </br>
BEGIN  </br>
   a:=:a;  </br>
   b:=:b;  </br>
    c := findMax(a, b);  </br>
   dbms_output.put_line(' Maximum of two nums is: ' || c);  </br>
END;</br>

### Function for total sal payable to emps
CREATE OR REPLACE FUNCTION get_total_sal  </br>
RETURN NUMBER </br>
IS </br>
    totalsal NUMBER := 0; </br>
BEGIN </br>
    SELECT SUM(sal) INTO totalsal </br>
    FROM emp; </br>
RETURN totalsal; </br>
END; </br>
declare </br>
 sal NUMBER := 0; </br>
BEGIN </br>
 sal := get_total_sal (); </br>
    DBMS_OUTPUT.PUT_LINE('Sal: ' || sal); </br>
END; </br>
Sal: 35740</br> 

### Trigger that dosent allow salary to be updated if commission is null
create or replace trigger "empupdatesal" before </br>
   update of sal on emp </br>
    for each row </br>
   begin </br>
   if :old.commission is null then </br>
   raise_application_error(-20100,'commission is null, sal cannot be updated'); </br>
   end if;</br> 
   end; </br>

### Trigger that does not allow duplicates
CREATE OR REPLACE TRIGGER  "DEPT_T1"  </br>
BEFORE </br>
insert on "DEPT" </br>
for each row </br>
declare </br>
a number; </br>
begin </br>
if(:new.deptno is Null) then </br>
   raise_application_error(-20001,'error::deptno cannot be null'); </br>
   else </br>
   select count(*) into a from dept where deptno=:new.deptno; </br>
   if(a=1) then </br>
  raise_application_error(-20002,'error:: cannot have duplicate deptno'); </br>
  end if; </br>
  end if; </br>
end; </br>

### Cursor program to print emp number, name, etc
DECLARE </br>
   cursor c is select empno, ename, deptno, sal from emp ; </br>
    i emp.empno%type; </br>
    j emp.ename%type; </br>
    k emp.deptno%type; </br>
   l emp.sal%type;</br>
    BEGIN </br>
   open c; </br>
    dbms_output.put_line('Empno, name, deptno, salary of employees are:= '); </br>
   loop </br>
   fetch c into i, j, k, l; </br>
   exit when c%notfound; </br>
   dbms_output.put_line(i||' '||j||' '||k||' '||l); </br>
   end loop; </br>
   close c; </br>
  END; </br>

  ### Procedure for factorial
  create or replace procedure factorial(n in number, fact out number) as</br>
  i int :=1;</br>
  begin</br>
  fact:=1;</br>
  while i<=n loop</br>
  fact :=fact*i;</br>
  i:=i+1;</br>
  end loop;</br>
  end;</br>
  declare</br>
  n int;</br>
  fact int;</br>
  begin</br>
  n:=:n;</br>
  factorial(n,fact);</br>
  dbms_output.put_line('Factorial is:'||fact);</br>
  end;</br>




