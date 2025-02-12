# SQL 50 - LeetCode
## Crack SQL Interview in 50 Qs
Solved assignment from [SQL 50 Study Plan](https://leetcode.com/studyplan/top-sql-50/) on LeetCode

---
### Select Assigment
---

[1757 - Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/)
```sql
SELECT product_id 
FROM Products
WHERE low_fats = "Y" AND recyclable ="Y";
```
[584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT name
FROM Customer
WHERE referee_id !=2 OR referee_id IS NULL;
```
[595. Big Countries](https://leetcode.com/problems/big-countries/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT name, population,area
FROM World
WHERE area >=3000000 
        OR population >= 25000000;
```
[1148. Article Views I](https://leetcode.com/problems/article-views-i/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT DISTINCT author_id as id
FROM Views
WHERE author_id = viewer_id
ORDER BY author_id;
```
[1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT tweet_id
FROM Tweets
WHERE length(content) > 15
```
---
### Basic Join
---
[1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT b.unique_id, a.name
FROM Employees a
LEFT JOIN EmployeeUNI b
ON b.id = a.id;
```
[1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT product_name, year, price
FROM Sales s
LEFT JOIN Product p
ON s.product_id = p.product_id;
```
[1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT  v.customer_id, count(*) as count_no_trans
FROM Visits v
LEFT JOIN Transactions t
ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
```
[197. Rising Temperature](https://leetcode.com/problems/rising-temperature/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT today.id
FROM Weather yesterday 
CROSS JOIN Weather today

WHERE DATEDIFF(today.recordDate,yesterday.recordDate) = 1
    AND today.temperature > yesterday.temperature;
```
[1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT e.machine_id, round(AVG(e.timestamp - s.timestamp),3) as processing_time
FROM
    (SELECT * FROM Activity WHERE activity_type = 'end') e
    LEFT JOIN
    (SELECT * FROM Activity WHERE activity_type = 'start') s
    ON e.machine_id = s.machine_id and e.process_id = s.process_id
GROUP BY e.machine_id
```
[577. Employee Bonus](https://leetcode.com/problems/employee-bonus/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT name, bonus
FROM
    Employee e LEFT JOIN Bonus b
    ON e.empId = b.empId
WHERE b.bonus <1000 or b.bonus IS NULL
```
[1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT s.student_id, s.student_name, su.subject_name, count(e.student_id) as attended_exams
FROM
    Students s
    CROSS JOIN Subjects su
    LEFT JOIN Examinations e
    ON s.student_id = e.student_id AND su.subject_name = e.subject_name
GROUP BY s.student_id, s.student_name, su.subject_name
ORDER BY s.student_id, su.subject_name
```
```sql
SELECT
    Students.student_id,
    Students.student_name,
    Subjects.subject_name,
    COUNT(Examinations.student_id) AS attended_exams
FROM Students
CROSS JOIN Subjects
LEFT JOIN Examinations ON (Subjects.subject_name = Examinations.subject_name AND Students.student_id = Examinations.student_id)
GROUP BY 1,2,3
ORDER BY Students.student_id ASC;
```
