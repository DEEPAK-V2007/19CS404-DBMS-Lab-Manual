# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**

![alt text](image.png)

```
SELECT PatientID,
       COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY PatientID;
```

**Output:**

![alt text](image-1.png)

**Question 2**

![alt text](image-2.png)

```
SELECT InsuranceCompany,
       COUNT(*) AS TotalExpiredPatients
FROM Insurance
WHERE ValidityPeriod < DATE('now')
GROUP BY InsuranceCompany;
```

**Output:**

![alt text](image-3.png)

**Question 3**

![alt text](image-4.png)

```
SELECT DoctorID,
       strftime('%H:%M', AppointmentDateTime) AS TimeSlot,
       COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID, TimeSlot
HAVING COUNT(*) = (
    SELECT MAX(cnt)
    FROM (
        SELECT COUNT(*) AS cnt
        FROM Appointments a2
        WHERE a2.DoctorID = Appointments.DoctorID
        GROUP BY strftime('%H:%M', a2.AppointmentDateTime)
    )
)
ORDER BY TotalAppointments DESC;
```

**Output:**

![alt text](image-5.png)

**Question 4**

![alt text](image-6.png)

```
SELECT COUNT(*) AS 'COUNT'
FROM customer
WHERE city = 'Noida';
```

**Output:**

![alt text](image-7.png)

**Question 5**

![alt text](image-8.png)

```
SELECT AVG(income) AS avg_income
FROM employee
WHERE name LIKE 'A%';
```

**Output:**

![alt text](image-9.png)

**Question 6**

![alt text](image-10.png)

```
SELECT MAX(purch_amt) AS MAXIMUM
FROM orders;
```

**Output:**

![alt text](image-11.png)

**Question 7**

![alt text](image-12.png)

```
SELECT COUNT(DISTINCT salesman_id) AS COUNT
FROM orders;
```

**Output:**

![alt text](image-13.png)

**Question 8**

![alt text](image-14.png)

```
SELECT (age / 5) * 5 AS age_group,
       MIN(salary) AS "MIN(salary)"
FROM customer1
GROUP BY (age / 5) * 5
HAVING MIN(salary) < 2000;
```

**Output:**

![alt text](image-15.png)

**Question 9**

![alt text](image-16.png)

```
SELECT age, SUM(income) AS "SUM(income)"
FROM employee
GROUP BY age
HAVING SUM(income) > 1000000;
```

**Output:**

![alt text](image-17.png)

**Question 10**

![alt text](image-18.png)

```
SELECT address,
       AVG(salary) AS "AVG(salary)"
FROM customer1
GROUP BY address
HAVING AVG(salary) > 5000;
```

**Output:**

![alt text](image-19.png)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
