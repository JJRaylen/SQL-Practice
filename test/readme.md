SQL ENTRANCE TEST – TELESALES GENESYS ANALYST


Scenario: Telesales Performance Analysis
You're a data analyst for a company with a telesales team. You have the following tables:
•	SalesReps: 
o	RepID (INT, PRIMARY KEY), 
o	Name (VARCHAR), 
o	HireDate (DATE), 
o	Team (VARCHAR)
•	Customers: 
o	CustomerID (INT, PRIMARY KEY), 
o	Name (VARCHAR), 
o	City (VARCHAR), 
o	SignUpDate (DATE)
•	Calls: 
o	CallID (INT, PRIMARY KEY), 
o	RepID (INT, FOREIGN KEY referencing SalesReps), 
o	CustomerID (INT, FOREIGN KEY referencing Customers), 
o	CallDate (DATE), 
o	CallDurationMinutes (INT), 
o	CallOutcome (VARCHAR) (e.g., "Sale", "No Sale", "Follow Up")
•	Sales: 
o	SaleID (INT, PRIMARY KEY), 
o	CallID (INT, FOREIGN KEY referencing Calls), 
o	SaleDate (DATE), 
o	SaleAmount (DECIMAL)


Question 1: What is the average call duration for each sales rep?
SELECT S.REPID
	,AVG(C.CALLDURATIONMINUTES) AS AVG_DURATION
FROM SALESREPS S
JOIN CALLS C ON S.REPID = C.REPID
GROUP BY S.REPID
Question 2: List the top 5 sales reps with the highest total sales amount.
SELECT SR.REPID
	,SUM(S.SALEAMOUNT) AS SUM_SALEAMOUNT
FROM SALESREPS SR
	JOIN CALLS C ON S.REPID = C.REPID
	JOIN SALES S ON C.CALLID = S.CALLID
GROUP BY SR.REPID
ORDER BY SUM_SALEAMOUNT DESC LIMIT 5
Question 3: For each sales rep, calculate the average sale amount for successful calls (calls that resulted in a sale).
SELECT SR.NAME
	,AVG(S.SALEAMOUNT) AS AVGSALEAMOUNT
FROM SALES S
	JOIN CALLS C ON S.CALLID = C.CALLID
	JOIN SALESREPS SR ON C.REPID = SR.REPID
WHERE C.CALLOUTCOME = ‘SALES’
GROUP BY SR.NAME

Question 4: What is the purpose of the below query? and what is the order in which the query is executed?
SELECT sr.Name AS SalesRepName
	,c.Name AS CustomerName
	,COUNT(DISTINCT ca.CallID) AS TotalCalls
	,SUM(s.Amount) AS TotalSalesAmount
	,AVG(DATEDIFF(s.SaleDate, ca.CallDate)) AS AvgTimeToSale
FROM SalesReps sr
	INNER JOIN Calls ca ON sr.RepID = ca.RepID
	INNER JOIN Customers c ON ca.CustomerID = c.CustomerID
	LEFT JOIN Sales s ON ca.CallID = s.CallID
WHERE sr.Team = 'Team A'
	AND c.City = 'New York'
	AND ca.CallDate BETWEEN '2023-01-01'
		AND '2023-12-31'
GROUP BY sr.RepID
	,sr.Name
	,c.CustomerID
	,c.Name
ORDER BY TotalSalesAmount DESC;
Answer: 
-	Purpose: to analyze the sales performance of 'Team A' employees in 'New York' in 2023. More specifically, it wants to understand the relationship between salespeople, customers, call volume, sales, and average time to close a deal.
-	Order: from & join -> where -> group by -> having -> select -> order by

Sample Data:
SalesReps:
RepID	Name	HireDate	Team
1	John Smith	2022-01-15	Team A
2	Jane Doe	2022-03-20	Team A
3	David Lee	2023-05-10	Team B
4	Sarah Jones	2023-07-01	Team B

Customers:
CustomerID	Name	City	SignUpDate
1	Alice Brown	New York	2024-01-05
2	Bob Williams	Los Angeles	2024-02-10
3	Carol Davis	New York	2024-03-15
4	Dave Garcia	Chicago	2024-04-20

Calls:
CallID	RepID	CustomerID	CallDate	CallDurationMinutes	CallOutcome
1	1	1	2024-05-01	10	Sale
2	1	2	2024-05-05	5	No Sale
3	2	3	2024-05-10	15	Sale
4	3	4	2024-05-15	20	Sale
5	1	1	2024-05-20	8	Follow Up
6	2	2	2024-05-25	12	No Sale
7	4	3	2024-05-30	7	Sale

Sales:
SaleID	CallID	SaleDate	SaleAmount
1	1	2024-05-01	100
2	3	2024-05-10	200
3	4	2024-05-15	150
4	7	2024-05-30	250


