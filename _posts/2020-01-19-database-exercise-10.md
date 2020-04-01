---
layout: post
title: Database Exercise 10
date: 2020-01-15 09:12 +0000
categories: ["Database"]
publish: true
toc: true
---
# 1 
## a
``` sql
alter table employee 
drop constraint employee_sssn_fk;
alter table employee 
add constraint employee_sssn_fk 
foreign key (superssn)
references employee(ssn) on delete set null;
```
`on delete restrict`  
`on delete cascade`

## b
```sql
DELETE FROM EMPLOYEE 
WHERE Lname = 'Borg'
```
Delete Mr. Borg managers and his employees

## c
 Imo, cascade is better, after deleting parent, the child will not be appeared => Easy to see

# 2
This simply duplicates the existed table to a new table.
```
CREATE employee_backup
AS SELECT * FROM employee;
```
This will copy all rows from a table to a table. Two table have been created and have the same structure.
```
SELECT * INTO employee_backup
FROM employee;
```
# 3 
## a
```sql
create view MyView(Dname, fname, lname, salary)
as 
select D.Dname, E.fname, E.lname, E.salary
from department D
    join employee E on (D.Mgrssn = E.ssn);
```
Before run above code, ensure that the view is not created before. If not this error will be appeared:
![](/assets/img/2020-01-19-23-35-38.png)
To fix above problem, drop the view `DROP VIEW MyView;`

## b
```sql
create view view_b(fname, lname, mfname, mlname, salary, dno)
as
select E.fname, E.lname, EE.fname, EE.lname, E.salary, E.dno
from employee E
    join department D on (D.Dnumber = E.Dno)
    join employee EE on (E.superssn = EE.ssn)
where D.Dname = 'Research';
```
## c
Muốn hiển thị cột `Pname`, `Dname` thì phải thêm chúng ở `select` và `group by`
```
create view view_c(ProductName, DepName, TotalEmp, TotalHours)
as
select p.pname, d.dname, count(essn), sum(w.hours)
from works_on W
    join project P on (P.Pnumber = W.Pno)
    join department D on (P.Dnum = D.Dnumber)
group by p.pname, d.dname;
```
## d
Use `having` to choose the tuple that have the column `count(essn)` > 1
```sql
create view view_(ProductName, DepName, TotalEmp, TotalHours)
as
select p.pname, d.dname, count(essn), sum(w.hours)
from works_on W
    join project P on (P.Pnumber = W.Pno)
    join department D on (P.Dnum = D.Dnumber)
group by p.pname, d.dname
having count(essn) > 1;
```
# 4
## Schema
![](/assets/img/2020-01-20-00-55-22.png)
## The View
```sql
CREATE VIEW DEPT_SUMMARY (D, C, Total_s, Average_s) 
AS SELECT Dno, COUNT (*), SUM (Salary), AVG (Salary) 
FROM EMPLOYEE GROUP BY Dno;
```
View DEPT_SUMMARY shows a list of different departments which all employees are working in, each listed department have total emps, sum of their salary, and average salary.  
## Questions:
```sql
a) 
SELECT *
FROM DEPT_SUMMARY;

b) 
SELECT D, C
FROM  DEPT_SUMMARY
WHERE TOTAL_S > 100000;

c) 
SELECT D, AVERAGE_S
FROM  DEPT_SUMMARY
WHERE C > (SELECT C FROM DEPT_SUMMARY WHERE D=4);

d) 
UPDATE DEPT_SUMMARY
SET  D=3
WHERE D=4;

e) 
DELETE FROM DEPT_SUMMARY
WHERE C>4;
```  
## Answer: 
    a. Displays the same as DEPT_SUMMARY
    b. For each department has total salary > 100000. Displays department number and total emps
    c. For each department has total employee > total employee of department #4. Displays department number and average salary.

    Can not update or delete when the view use GROUP BY
    
    d. In DEPT_SUMMARY, change department 4 to department 3
    e. Delete all departments which have total emp > 4
