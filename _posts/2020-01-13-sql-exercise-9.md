---
layout: post
title: SQL Exercise 9
date: 2020-01-13 11:25 +0000
categories: ["Database"]
---
```sql
SELECT e.EMPLOYEE_ID,e.FIRST_NAME,e.LAST_NAME,e.JOB_ID,e.DEPARTMENT_ID,e.SALARY
from employees e
    join jobs j on (e.job_id = j.job_id)
where (j.job_title='Programmer' and e.salary > 6000) or (j.job_title='Accountant' and e.salary > 8000
```
