---
Test 01 What is AVG Call Duratuon for each saless rep?
---
```sql
SELECT  sr.RepID,
        AVG(c.CallDurationMinutes) as AVG_Duration
FROM SalesReps sr
JOIN Calls c ON sr.RepID = c.RepID
GROUP BY sr.RepID
ORDER BY sr.RepID;
```

---
Test 02:List the top 5 sales reps with the highest total sales amount.
---
```sql
SELECT  SR.REPID,
	    SUM(S.SALEAMOUNT) AS SUM_SALEAMOUNT,
        DENSE_RANK() OVER (ORDER BY SUM(S.SALEAMOUNT) DESC) AS RNK
FROM SALESREPS SR
	JOIN CALLS C ON S.REPID = C.REPID
	JOIN SALES S ON C.CALLID = S.CALLID
GROUP BY SR.REPID
HAVING RNK <= 5
	    SUM(S.SALEAMOUNT) AS SUM_SALEAMOUNT,
ORDER BY SUM(S.SALEAMOUNT) DESC;
```
---
Question 3: For each sales rep, calculate the average sale amount for successful calls (calls that resulted in a sale
---
```sql
SELECT SR.RepID,SR.NAME
	,AVG(S.SALEAMOUNT) AS AVGSALEAMOUNT
FROM SALES S
	JOIN CALLS C ON S.CALLID = C.CALLID
	JOIN SALESREPS SR ON C.REPID = SR.REPID
WHERE C.CALLOUTCOME = ‘SALES’
GROUP BY 1,2;
```
---
Question 4 What is the purpose of below query? what is the order in which the query is excuted?
---
```sql
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
```

-- A1: To analyze the sale perfomance of Team A's employess in Newyork in 2023. This query also show the relationship between salespeople, customers, calls volume, sales and AVG time of

-- A2:Process: From & Join >> WHERE >> GROUP BY >> HAVING >> SELECT >> ORDER BY
