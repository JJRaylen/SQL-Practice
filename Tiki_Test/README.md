[CLICK HERE TO VIEW SOURCE TEST](https://drive.google.com/file/d/12Bx1KVPYar_acGFR6DAkS16sNEB-AFmA/view?usp=sharing)
---
Test from **TIKI Marketplace Data Analyst Test**
This test assesses candidate ability to solve business problems using deductive, inductive,
and quantitative reasoning and also candidate's SQL skills. The test contains 3 parts: SQL,
Logical & Problem Solving and Case Study.

This one focus on solving SQL question.
---
Question 1:
---
- Given three following columns in table X:
#### Table X

| Seller_ID | Category    | Sales_Milion_VND |
|-----------|------------|----------------------|
| 1         | Book       | 258                  |
| 2         | Electronics| 299                  |
| 3         | Electronics| 123                  |
| 4         | Book       | 272                  |
| 5         | FMCG       | 485                  |
| 6         | Book       | 187                  |
| 7         | FMCG       | 349                  |
| 8         | FMCG       | 61                   |
| 9         | Electronics| 321                  |
| 10        | FMCG       | 20                   |

a. Write a SQL query to find the best seller by each category.
#### Solution:
```sql
SELECT Seller ID, Category, Sales_Milion_VND
FROM
    (SELECT Seller_ID, 
            Category, 
            Sales_Milion_VND, 
            DENSE_RANK() OVER (PARTITION BY Category ORDER BY Sales_Milion_VND DESC) as rnk
    FROM X) AS TEMP
WHERE rnk =1;
```
b. Given three following columns in table Y:
#### Table Y
| Award_Year | Award            | Seller_ID |
|------------|------------------|-----------|
| 2017       | Best Seller      | 9         |
| 2018       | Best Seller      | 5         |
| 2017       | Best Operations  | 5         |
| 2018       | Best Quality     | 10        |
| 2018       | Best Operations  | 6         |
| 2017       | Best Seller      | 4         |
| 2017       | Best Operations  | 5         |
| 2017       | Best Quality     | 7         |
| 2017       | Best Quality     | 10        |

Write a SQL query to find of 3 best sellers in (a), how many award did they received in
2017.
#### Solution:
```sql
SELECT   Seller_ID,
         Category, 
         COUNT(CASE WHEN Award_Year = 2017 then 1 else null END) as Award_in_2017)
FROM Y
JOIN 
    (SELECT Seller_ID, Category, Sales_Milion_VND
    FROM
        (SELECT Seller_ID, 
                Category, 
                Sales_Milion_VND, 
                DENSE_RANK() OVER (PARTITION BY Category ORDER BY Sales_Milion_VND DESC) as rnk
        FROM X) AS TEMP
    WHERE rnk =1;) as part_a
ON Y.Seller_ID = part_a.Seller_ID
GROUP BY 1,2
```
---
Question 2:
---
You have one sample dataset attached to this test:
- product_history.csv: records of product’s status & stock changes from May – October
2018.
#### Dimension Definitions

| Dimension     | Definition                                    |
|--------------|----------------------------------------------|
| Date         | Log Date                                     |
| Product ID   | Unique ID for each product                  |
| Product Status | Status of a product:                      |
|              | - **ON**: Available for Sales               |
|              | - **OFF**: Unavailable for Sales            |
| Stock        | Total stock of a product at a specific log date |

a. Write a SQL query to find the number of product that were available for sales at the
end of each month.
#### Solution
```sql
```

b. Average stock is calculated as: Total stock in a month/ total date in a month. Write a
SQL query to find Product ID with the most “average stock” by month.
#### Solution
```sql
```




