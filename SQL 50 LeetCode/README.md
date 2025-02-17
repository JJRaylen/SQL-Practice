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
[[570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT temp.name 
FROM 
    (SELECT m.id,m.name, count(*) as no_e
    FROM
    Employee m INNER JOIN Employee e
    ON m.id = e.managerID
    GROUP BY 1,2) as temp
WHERE no_e >=5;
```
[1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT A.user_id, 
       ROUND(IFNULL(AVG(action = 'confirmed'), 0), 2) AS confirmation_rate
FROM Signups AS A
LEFT JOIN Confirmations AS B ON A.user_id = B.user_id
GROUP BY A.user_id;
```
---
Basic Aggregate Functions
---
[620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT id, movie, description, rating
FROM Cinema
WHERE id%2 =1 AND description <> 'boring' 
ORDER BY rating DESC
```
[1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT  p.product_id, 
        IFNULL(ROUND(SUM(units*price)/SUM(units),2),0) AS average_price
FROM 
    Prices p LEFT JOIN UnitsSold u
    ON  p.product_id = u.product_id AND 
        (purchase_date BETWEEN start_date AND end_date)
group by p.product_id
```
[1075. Project Employees I](https://leetcode.com/problems/project-employees-i/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT  P.project_id, 
        round(AVG(E.experience_years),2) AS average_years
FROM
    Project p JOIN Employee e 
    ON p.employee_id = e.employee_id
GROUP BY 1
```
[1633. Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT contest_id,
ROUND(COUNT(DISTINCT user_id) * 100 / (SELECT COUNT(user_id) FROM Users), 2) as percentage
FROM Register
GROUP BY contest_id
ORDER BY percentage desc, contest_id
```
[1211. Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT  query_name, 
        ROUND(AVG(rating/position),2) as quality,
        ROUND(AVG(rating < 3),4)*100 as poor_query_percentage
FROM    Queries
GROUP BY query_name
```
[1193. Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT  SUBSTR(trans_date, 1, 7) AS month,
        country,
        count(*) as trans_count, 
        ifnull(sum(state = "approved"),0) as approved_count,
        SUM(amount) as trans_total_amount,
        sum(case
                when state ="approved" then amount
                else 0
            end) as approved_total_amount
FROM Transactions
GROUP BY 1, 2;
```
[1174. Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT  round(avg(order_date = customer_pref_delivery_date)*100,2) as immediate_percentage
FROM delivery
WHERE (customer_id, order_date) in (
    select customer_id, min(order_date)
    from delivery
    group by customer_id
    );
```
[550. Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
select round(count(distinct player_id)/(select count(distinct player_id) from Activity),2) as fraction
from Activity
where (player_id,DATE_SUB(event_date,INTERVAL 1 DAY))
in (select player_id, min(event_date) as first_login from Activity group by player_id )
```
---
SHORTING & GROUPING
---
[2356. Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT  teacher_id, count(distinct subject_id) AS cnt
FROM teacher
GROUP BY 1
```
[1141. User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT activity_date AS day, COUNT(DISTINCT user_id) AS active_users
FROM Activity
WHERE (activity_date > "2019-06-27" AND activity_date <= "2019-07-27")
GROUP BY 1;
```
[1070. Product Sales Analysis III]
```sql
select product_id, year as first_year, quantity, price
FROM Sales
WHERE (product_id, year) in (
    SELECT product_id, min(year)
    FROM Sales
    Group by product_id
);
```
[596. Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT class
FROM Courses
GROUP BY 1
HAVING COUNT(student)>4;
```
[1729. Find Followers Count](https://leetcode.com/problems/find-followers-count/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
select user_id, count(follower_id) as followers_count
from followers
group by 1
order by user_id asc;
```
[619. Biggest Single Number](https://leetcode.com/problems/biggest-single-number/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT case
                when count(num) = 1 then num
                else null
        end as num 
from MyNumbers
group by num
order by num desc
limit 1;
```
[1045. Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
select customer_id
from customer
group by 1
having count(distinct product_key) = (select count(product_key) from product)
```
---
ADVANCED JOIN
---
[1731. The Number of Employees Which Report to Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
select e1.employee_id,
        e1.name,
        count(e2.reports_to) as reports_count,
        round(avg(e2.age)) as average_age
from employees e1 join employees e2 on e1.employee_id = e2.reports_to
where e2.reports_to is not null
group by 1,2
order by 1;
```
[1789. Primary Department for Each Employee](https://leetcode.com/problems/primary-department-for-each-employee/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
Select employee_id, department_id
from employee
where primary_flag ='Y' or
employee_id in (select employee_id 
                        from employee
                        group by employee_id
                        having count(employee_id) =1)
```
[1789. Primary Department for Each Employee](https://leetcode.com/problems/triangle-judgement/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
select x,y,z,
case when x+y >z 
        and y+z>x and x+z >y then 'Yes'
        else 'No'
        end as triangle
from Triangle
```
[180. Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
# Write your MySQL query statement below
select distinct l1.Num As ConsecutiveNums
from Logs l1,
     logs l2,
     logs l3
where l1.id=l2.id-1 
and l2.id=l3.id-1
and l1.num=l2.num
and l2.num =l3.num
```
```sql
# Write your MySQL query statement below
select  distinct num as ConsecutiveNums
from (
    select id, num, lag(num) over (order by id) as previous,
    lead(num) over (order by id) as after
    from Logs
) as a
where previous = num and after = previous;
```
[1164. Product Price at a Given Date])(https://leetcode.com/problems/product-price-at-a-given-date/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
 SELECT DISTINCT
        product_id,
        FIRST_VALUE (new_price) OVER (
                                PARTITION BY
                                product_id
                                ORDER BY
                                change_date DESC
        ) AS price
        FROM
        Products
        WHERE
        change_date <= '2019-08-16'
```
[1204. Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
WITH cte as (SELECT turn, person_id, person_name, weight, sum(weight) OVER (order by turn) as cw
FROM Queue
ORDER BY turn)

SELECT DISTINCT FIRST_VALUE(person_name) OVER(
    ORDER BY cw DESC
) as person_name
FROM cte
WHERE cw <= 1000;
``
[1907. Count Salary Categories](https://leetcode.com/problems/count-salary-categories/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT 'Low Salary' AS category, 
       COUNT(if(income<20000,1,null)) AS accounts_count
FROM Accounts
UNION ALL
SELECT 'Average Salary', 
       COUNT(if(income>=20000 and income<=50000,1,null))
FROM Accounts
UNION ALL
SELECT 'High Salary', 
       COUNT(if(income>50000,1,null))
FROM Accounts;
```
---
SubQueries
---
[1978. Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company/submissions/1545293227/?envType=study-plan-v2&envId=top-sql-50)
```sql
select employee_id
from Employees
where salary <30000 and  manager_id is not null and manager_id not in (select distinct employee_id from employees)
order by employee_id;
```
[626. Exchange Seats](https://leetcode.com/problems/exchange-seats/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT id, 
    CASE
        WHEN id%2=0 THEN LAG(student) OVER (ORDER BY id)
        ELSE IFNULL(LEAD(student) OVER (ORDER BY id),student)
    END as student
FROM Seat
```
[1341. Movie Rating](https://leetcode.com/problems/movie-rating/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
(SELECT name AS results
FROM MovieRating JOIN Users USING(user_id)
GROUP BY name
ORDER BY COUNT(*) DESC, name
LIMIT 1)

UNION ALL

(SELECT title AS results
FROM MovieRating JOIN Movies USING(movie_id)
WHERE EXTRACT(YEAR_MONTH FROM created_at) = 202002
GROUP BY title
ORDER BY AVG(rating) DESC, title
LIMIT 1);
```
[1321. Restaurant Growth](https://leetcode.com/problems/restaurant-growth/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT DISTINCT t1.visited_on, 
                t2.amount, 
                t2.average_amount
FROM 
    (SELECT DISTINCT visited_on
     FROM customer
     WHERE visited_on >= (SELECT MIN(visited_on) FROM customer) + INTERVAL 6 DAY) t1
LEFT JOIN 
    (SELECT distinct visited_on, 
            SUM(amount) OVER (ORDER BY visited_on ASC RANGE BETWEEN INTERVAL 6 DAY PRECEDING AND CURRENT ROW) as amount,
            ROUND(sum(amount) OVER (ORDER BY visited_on ASC RANGE BETWEEN INTERVAL 6 DAY PRECEDING AND CURRENT ROW)/7,2) as average_amount
     FROM customer) t2
ON t1.visited_on = t2.visited_on
ORDER BY t1.visited_on ASC;
```
[602. Friend Requests II: Who Has the Most Friends](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT id, SUM(num) AS num
FROM (
    (SELECT requester_id AS id,
            COUNT(requester_id) AS num
     FROM RequestAccepted
     GROUP BY requester_id)
    UNION ALL
    (SELECT accepter_id AS id,
            COUNT(accepter_id) AS num
     FROM RequestAccepted
     GROUP BY accepter_id)
) AS combined
GROUP BY id
ORDER BY SUM(num) DESC
LIMIT 1;
```
[585. Investments in 2016](https://leetcode.com/problems/investments-in-2016/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT ROUND(SUM(tiv_2016), 2) AS tiv_2016
FROM (
    SELECT tiv_2016,
           COUNT(*) OVER(PARTITION BY tiv_2015) AS tiv_2015_count,
           COUNT(*) OVER(PARTITION BY lat, lon) AS city_count
    FROM Insurance
) AS InsuranceWithCounts
WHERE tiv_2015_count > 1
  AND city_count = 1;
```
[185. Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
WITH cte as
(SELECT t2.name as Department, t1.name as Employee, t1.salary as Salary
FROM Employee t1 LEFT JOIN Department t2
ON t1.departmentId = t2.id
ORDER BY Department, Salary)


SELECT Department, Employee,Salary
FROM
    (SELECT Department, Employee, Salary, 
            DENSE_RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS rnk
    FROM cte) as temp
WHERE rnk <=3;
```
---
Advanced String Function/Regex/Clause
---
[1667. Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT user_id, CONCAT(
    UPPER(LEFT(name, 1)), 
    LOWER(SUBSTRING(name, 2))
) AS name
FROM users
ORDER BY user_id;
```
[1527. Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT patient_id, patient_name, conditions
FROM Patients
WHERE conditions LIKE "DIAB1%" OR conditions LIKE "% DIAB1%";
```
[196. Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
delete p1 from person p1,person p2 
where p1.email=p2.email and p1.id>p2.id;
```
[176. Second Highest Salary](https://leetcode.com/problems/second-highest-salary/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT COALESCE(
           (SELECT salary
            FROM (
                SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) as rnk
                FROM Employee
            ) as temp
            WHERE rnk = 2
            LIMIT 1),
           NULL
       ) AS SecondHighestSalary;
```
[1484. Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT sell_date,
        count(DISTINCT(product)) as num_sold,
                GROUP_CONCAT(DISTINCT product ORDER BY  Product ASC SEPARATOR ",") as products
FROM Activities
GROUP BY sell_date
ORDER BY sell_date ASC
```
[1327. List the Products Ordered in a Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT p.product_name, sum(o.unit) as unit
FROM
Orders o LEFT JOIN Products p
ON o.product_id = p.product_id
WHERE DATE_FORMAT(order_date,"%Y%m") = 202002
GROUP BY product_name
having sum(o.unit)>=100;
```
[1517. Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT * 
FROM Users
WHERE mail REGEXP '^[A-Za-z][A_Za-z0-9_.-]*@leetcode.com$' AND mail LIKE '%@leetcode.com';
```
