# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**

![alt text](image.png)

```
select medication_id as medic, medication_name,dosage from Medications 
where dosage = (select min(dosage) from Medications);
```

**Output:**

![alt text](image-1.png)

**Question 2**

![alt text](image-2.png)

```
select name,city from customer
where city in(select city from customer where id=3 or id=7);
```

**Output:**

![alt text](image-3.png)

**Question 3**

![alt text](image-4.png)

```
SELECT commission
FROM salesman
WHERE salesman_id IN (
    SELECT salesman_id
    FROM customer
    WHERE city = 'Paris'
);
```

**Output:**

![alt text](image-5.png)

**Question 4**

![alt text](image-6.png)

```
select ord_no,purch_amt,ord_date,customer_id,salesman_id from orders where salesman_id in (select salesman_id from salesman where city='London')
```

**Output:**

![alt text](image-7.png)

**Question 5**

![alt text](image-8.png)

```
select medication_id as medic,medication_name,dosage from Medications where dosage=(select max(dosage) from Medications);
```

**Output:**

![alt text](image-9.png)

**Question 6**

![alt text](image-10.png)

```
select ID,NAME,AGE,ADDRESS,SALARY from CUSTOMERS where AGE<30;
```

**Output:**

![alt text](image-11.png)

**Question 7**

![alt text](image-12.png)

```
select * from customer where city not in(select city from customer where id=(select max(id) from customer))
```

**Output:**

![alt text](image-13.png)

**Question 8**

![alt text](image-14.png)

```
SELECT salesman_id, name
FROM salesman
WHERE salesman_id IN (
    SELECT salesman_id
    FROM customer
    GROUP BY salesman_id
    HAVING COUNT(customer_id) > 1
);
```

**Output:**

![alt text](image-15.png)

**Question 9**

![alt text](image-16.png)

```
select * from Employee where age <(select avg(age) from Employee where income>250000)
```

**Output:**

![alt text](image-17.png)

**Question 10**

![alt text](image-18.png)

```
select grade, COUNT(*) from customer where grade>(select avg(grade) from customer where city='New York') group by grade;
```

**Output:**

![alt text](image-19.png)


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
