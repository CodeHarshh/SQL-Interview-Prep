# SQL-Interview-Prep

Here's the README file format with each question followed by its query:

````markdown
# SQL Queries for Worker and Bonus Tables

This document contains SQL queries based on various scenarios related to the `Worker` and `Bonus` tables.

## Table Definitions

### Worker Table
```sql
CREATE TABLE worker (
    worker_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    first_name CHAR(25),
    last_name CHAR(25),
    salary INT(15),
    joining_date DATE,
    department CHAR(25)
);

INSERT INTO worker (first_name, last_name, salary, joining_date, department) VALUES
('John', 'Doe', 50000, '2021-05-01', 'HR'),
('Jane', 'Smith', 60000, '2020-03-15', 'Finance'),
('Michael', 'Johnson', 55000, '2022-01-20', 'IT'),
('Emily', 'Davis', 70000, '2019-07-10', 'Marketing'),
('Chris', 'Brown', 45000, '2023-04-25', 'HR'),
('Sarah', 'Wilson', 50000, '2021-11-30', 'Finance'),
('David', 'Clark', 48000, '2022-08-05', 'IT'),
('Anna', 'Taylor', 75000, '2018-12-01', 'Marketing'),
('James', 'Anderson', 52000, '2020-09-15', 'HR'),
('Laura', 'Moore', 68000, '2019-10-20', 'Finance');

````

### Bonus Table

```sql
CREATE TABLE bonus (
    worker_ref_id INT,
    bonus_amount INT,
    bonus_date DATE,
    FOREIGN KEY (worker_ref_id) REFERENCES worker(worker_id) ON DELETE CASCADE
);

INSERT INTO bonus (worker_ref_id, bonus_amount, bonus_date) VALUES
(1, 5000, '2022-12-25'),
(2, 7000, '2022-11-30'),
(3, 6000, '2023-01-15'),
(4, 8000, '2022-10-20'),
(5, 4000, '2023-03-01'),
(6, 4500, '2022-07-10'),
(7, 5000, '2023-02-14'),
(8, 8500, '2022-05-30'),
(9, 5200, '2023-04-05'),
(10, 7500, '2022-09-15');
```

## Queries


```sql
-- Q-1. Write an SQL query to fetch “FIRST_NAME” from Worker table using the alias name as <WORKER_NAME>.
select first_name as WORKER_NAME from worker;
```
```sql
-- Q-2. Write an SQL query to fetch “FIRST_NAME” from Worker table in upper case.
select upper(first_name) as FIRST_NAME from worker ;
```
```sql
-- Q-3. Write an SQL query to fetch unique values of DEPARTMENT from Worker table.
select distinct department as DISTINCT_VALUE from worker;
```
```sql
-- Q-4. Write an SQL query to print the first three characters of  FIRST_NAME from Worker table.
select substring(first_name,1,3) from worker;
```
```sql
-- Q-5. Write an SQL query to find the position of the alphabet (‘h’) in the first name column Michael from Worker table.
select instr (first_name,'h') as position from worker where first_name='Michael';
```
```sql
-- Q-6. Write an SQL query to print the FIRST_NAME from Worker table after removing white spaces from the right side.
-- RTRIM KEY word
select RTRIM(first_name)  from worker;
```
```sql
-- Q-7. Write an SQL query to print the DEPARTMENT from Worker table after removing white spaces from the left side.
select LTRIM(DEPARTMENT) as LTRIM  from worker;
```

```sql
-- Q-8. Write an SQL query that fetches the unique values of DEPARTMENT from Worker table and prints its length.
select distinct department, LENGTH(department) from worker;
```
```sql
-- Q-9. Write an SQL query to print the FIRST_NAME from Worker table after replacing ‘a’ with ‘A’.
select replace(first_name,'a','A') from worker;
```
```sql
-- Q-10. Write an SQL query to print the FIRST_NAME and LAST_NAME from Worker table into a single column COMPLETE_NAME.
-- A space char should separate them.
select concat (first_name ,' ', last_name) from worker;
```
```sql
-- Q-11. Write an SQL query to print all Worker details from the Worker table order by FIRST_NAME Ascending.
select * from worker order by first_name Asc;
```
```sql
-- Q-12. Write an SQL query to print all Worker details from the Worker table order by 
-- FIRST_NAME Ascending and DEPARTMENT Descending.
select * from worker order by first_name asc , department desc;
```
```sql
-- Q-13. Write an SQL query to print details for Workers with the first name as Michael and Chris from Worker table.
select * from worker where first_name='Michael' or  first_name='Chris';
-- or 
select * from worker where first_name in('Michael','Chris');
```
```sql
-- Q-14. Write an SQL query to print details of workers excluding first names, “Vipul” and “Satish” from Worker table.
 select * from worker where first_name not in('Michael','Chris');
```
```sql
-- Q-15. Write an SQL query to print details of Workers with DEPARTMENT name as “Admin*”.
select * from worker where department like 'Mark%';
```
```sql
-- Q-16. Write an SQL query to print details of the Workers whose FIRST_NAME contains ‘a’.
select * from worker where first_name like '%a%';
```
```sql
-- Q-17. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘a’.
select * from worker where first_name like '%a';
```
```sql
-- Q-18. Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘s’ and contains five alphabets.
select * from worker where first_name like '%s' and length(first_name)=5;
```

```sql
-- Q-19. Write an SQL query to print details of the Workers whose SALARY lies between 100000 
--and 500000.```
select * from worker where SALARY between 60000 and 70000;
```
```sql
-- Q-20. Write an SQL query to print details of the Workers who have joined in Feb’2014.
select * from worker where joining_date='2019-07-10';
```
```sql
-- Q-21. Write an SQL query to fetch the count of employees working in the department 'HR'.
select department, count(first_name) from worker where department='hr';
```
```sql
-- Q-22. Write an SQL query to fetch worker full names with salaries >= 50000 and <= 100000.
select concat(first_name,' ',last_name),salary from worker where  SALARY >= 50000 and  salary<=100000;
```
```sql
-- Q-23. Write an SQL query to fetch the no. of workers for each department in the descending order.
select department,count(department) as no_of_worker  from worker group by department order by no_of_worker desc;
```
```sql
-- Q-24. Write an SQL query to retrieve the details of workers who have received a bonus. 
-- Use the worker table to display the worker details, and the bonus table to check for workers
--  who have a corresponding bonus entry.
select * from worker INNER JOIN  bonus on worker_id=worker_ref_id;
```
```sql
-- Q-25. Write an SQL query to fetch the count of workers (more than 1) in each department where workers have received a bonus.
select department,count(first_name) from worker INNER JOIN bonus 
 on worker_id=worker_ref_id  group by department HAVING COUNT(worker_id) > 1;;
```
```sql
-- Q-26. Write an SQL query to show only odd rows from a table.
select * from worker where (worker_id % 2 != 0);
```
```sql
-- Q-27. Write an SQL query to show only even rows from a table. 
select * from worker where (worker_id % 2 = 0);
```
```sql
-- Q-28. Write an SQL query to clone a new table from another table.
create table worker_clone like worker;
INSERT into  worker_clone select * from worker;
select * from worker_clone;
```
```sql
-- Q-29. Write an SQL query to fetch intersecting records of two tables.
 SELECT w.worker_id, w.first_name, w.last_name, w.salary, w.department, b.bonus_amount, 
b.bonus_date FROM worker w INNER JOIN bonus b ON w.worker_id = b.worker_ref_id;
```
```sql
-- Q-30. Write an SQL query to show records from one table that another table does not have.
-- MINUS
Select worker.* from worker left join worker_clone using(worker_id) WHERE worker_clone.worker_id is NULL;
```
```sql
-- Q-31. Write an SQL query to show the current date and time.
-- DUAL
select curdate();
-- or
select now();
```
```sql
-- Q-32. Write an SQL query to show the top n (say 5) records of a table order by descending salary.
SELECT * FROM worker ORDER BY salary DESC limit 5 ;
```
```sql
 -- Q-33. Write an SQL query to determine the nth (say n=5) highest salary from a table.
SELECT salary FROM worker ORDER BY salary DESC limit 5 ;
```
```sql
 -- Q-34. Write an SQL query to determine the 5th highest salary without using LIMIT keyword.
SELECT DISTINCT salary FROM worker ORDER BY salary DESC LIMIT 1 OFFSET 4;
 ```
```sql
-- Q-35. Write an SQL query to fetch the list of employees with the same salary.
select *  from  worker  w1 , worker w2  where w1.salary=w2.salary and 
w1.worker_id!= w2.worker_id ;
```
```sql
-- Q-36. Write an SQL query to show the second highest salary from a table using sub-query.
select max(salary) from worker where salary not in (select max(salary) from worker);
```
```sql
-- Q-37. Write an SQL query to show one row twice in results from a table.
select * from worker UNION ALL select * from worker ORDER BY worker_id;
```
```sql
-- Q-38. Write an SQL query to list worker_id who does not get bonus.
select worker_id from worker where worker_id not in (select worker_ref_id from bonus);

```
```sql
-- Q-39. Write an SQL query to fetch the first 50% records from a table.
select * from worker where worker_id<= (select floor (count(worker_id)/2) from worker) ;
```
```sql
-- Q-40. Write an SQL query to fetch the departments that have less than 3 people in it.
select department, count(department) from worker group by department having count(department)<3;
```sql
```
```sql
-- Q-41. Write an SQL query to show all departments along with the number of people in there.
select department, count(department) from worker group by department ;
```
```sql
-- Q-42. Write an SQL query to show the last record from a table.
select * from worker where worker_id=(select max(worker_id) from worker);
```
```sql
-- Q-43. Write an SQL query to fetch the first row of a table.
select * from worker where worker_id=(select min(worker_id) from worker);
```
```sql
-- Q-44. Write an SQL query to fetch the last five records from a table.
(select * from worker order by worker_id desc limit 5) order by worker_id;
```
```sql
-- Q-45. Write an SQL query to print the name of employees having the highest salary in each department.
select department,first_name,salary from worker where salary=(select max(salary) from worker);
```
```sql
-- Q-46. Write an SQL query to fetch departments along with the total salaries paid for each of them.
select department , sum(salary) as depSal from worker group by department order by depSal desc;
```
```sql
-- Q-47. Write an SQL query to fetch the names of workers who earn the highest salary.
select first_name, salary from worker where salary = (select max(Salary) from worker); 
```
```sql
-- Q-48. Write an SQL query to calculate the total bonus amount given to workers in each department.
select department ,sum(bonus_amount) from worker INNER JOIN bonus on worker_id=worker_ref_id group by department;
```
```sql
-- Q-49. Find the total salary and bonus combined for each worker:
select worker_id,concat(first_name,' ',last_name) as worker_name,(salary+bonus_amount) as Total_earning
from worker left join bonus on worker_id=worker_ref_id;
```
```sql
--Q. 50 Calculate the average bonus amount for each department:
SELECT w.department, AVG(b.bonus_amount) AS Avg_Bonus FROM worker w INNER JOIN bonus b ON 
w.worker_id = b.worker_ref_id GROUP BY w.department;
```

