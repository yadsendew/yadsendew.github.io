---
layout: post
title: Database Exercise 10
date: 2020-01-15 09:12 +0000
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

## b
```sql
DELETE FROM EMPLOYEE 
WHERE Lname = 'Borg'
```


## c
 Imo, cascade is better, after deleting parent, the child will not be appeared => Easy to see

# 2
```
CREATE employee_backup
AS SELECT * FROM employee;
How about this?
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
