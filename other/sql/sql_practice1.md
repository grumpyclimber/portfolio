### 1. What is the total amount each customer spent at the restaurant?
```sql
SELECT
  customer_id, SUM(price) AS total_sales
FROM
  dannys_diner.sales t1 
JOIN dannys_diner.menu t2 ON t2.product_id = t1.product_id
GROUP BY customer_id
ORDER BY customer_id

```
| customer_id | total_sales |
| ----------- | ----------- |
| A           | 76          |
| B           | 74          |
| C           | 36          |


### 2. How many days has each customer visited the restaurant?

```sql
SELECT
  customer_id, COUNT(DISTINCT(order_date)) AS days_count
FROM
  dannys_diner.sales 
GROUP BY customer_id
```
| customer_id | days_count |
| ----------- | ---------- |
| A           | 4          |
| B           | 6          |
| C           | 2          |

### 3. What was the first item(s) from the menu purchased by each customer?

```sql
WITH sales_by_date AS (
  SELECT
    t1.customer_id,
    t1.order_date,
    t1.product_id,
    t2.product_name,
    RANK() OVER (
      PARTITION BY t1.customer_id
      ORDER BY
        t1.order_date
    ) AS row_number
  FROM
    dannys_diner.sales t1
    JOIN dannys_diner.menu t2 ON t2.product_id = t1.product_id
  ORDER BY
    row_number
)
SELECT DISTINCT 
  customer_id,
  product_name
FROM
  sales_by_date
WHERE
  row_number = 1
ORDER BY
  customer_id
```
| customer_id | product_name |
| ----------- | ------------ |
| A           | curry        |
| A           | sushi        |
| B           | curry        |
| C           | ramen        |

This is the first example where we see how quickly things can get a touch more complicated. 
The dataset contains only dates of the order, so in the above example we can see that customer A ordered both curry and sushi at the same time,
therefore we should include both. 


### 4. What is the most purchased item on the menu and how many times was it purchased by all customers?


```sql
SELECT
  menu.product_name,
  COUNT(*) AS item_sales
FROM
  dannys_diner.sales
  JOIN dannys_diner.menu ON menu.product_id = sales.product_id
GROUP BY
  sales.product_id,
  menu.product_name
ORDER BY
  item_sales DESC
LIMIT 1
```
| product_name| item_sales   |
| ----------- | ------------ |
| ramen       | 8            |

### 5. Which item(s) was the most popular for each customer?

```sql
WITH temp_a AS (
  SELECT
    t1.customer_id,
    t2.product_name,
    COUNT(t1.*) AS quantity,
    RANK() OVER (
      PARTITION BY t1.customer_id
      ORDER BY
        COUNT(t1.*)
    ) AS item_rank
  FROM
    dannys_diner.sales t1
    INNER JOIN dannys_diner.menu t2 ON t2.product_id = t1.product_id
  GROUP BY
    t1.customer_id,
    t2.product_name
)
SELECT
  customer_id,
  quantity,
  product_name
FROM
  temp_a
WHERE
  item_rank = 1
```
| customer_id | quantity | product_name |
| ----------- | -------- | ------------ |
| A           | 1        | sushi        |
| B           | 2        | sushi        |
| B           | 2        | curry        |
| B           | 2        | ramen        |
| C           | 3        | ramen        |

### 6. Which item was purchased first by the customer after they became a member and what date was it? (including the date they joined)
```sql
WITH sales_table AS (
  SELECT
    sales.customer_id,
    order_date,
    product_name,
    RANK() OVER(
      PARTITION BY sales.customer_id
      ORDER BY
        sales.order_date
    ) AS orders_rank
  FROM
    dannys_diner.sales
    INNER JOIN dannys_diner.menu ON menu.product_id = sales.product_id
    INNER JOIN dannys_diner.members ON members.customer_id = sales.customer_id
  WHERE
    sales.order_date >= members.join_date
  ORDER BY
    customer_id,
    order_date
)
SELECT
  customer_id,
  order_date,
  product_name
FROM
  sales_table
WHERE
  orders_rank = 1
```
| customer_id | order_date | product_name |
| ----------- | ---------- | ------------ |
| A           | 2021-01-07 | curry        |
| B           | 2021-01-11 | sushi        |

### 7. Which menu item(s) was purchased just before the customer became a member and when?
```sql
WITH sales_table AS (
  SELECT
    sales.customer_id,
    order_date,
    product_name,
    RANK() OVER(
      PARTITION BY sales.customer_id
      ORDER BY
        sales.order_date DESC
    ) AS orders_rank
  FROM
    dannys_diner.sales
    INNER JOIN dannys_diner.menu ON menu.product_id = sales.product_id
    INNER JOIN dannys_diner.members ON members.customer_id = sales.customer_id
  WHERE
    sales.order_date < members.join_date::DATE
  ORDER BY
    customer_id,
    order_date
)
SELECT
  customer_id,
  order_date,
  product_name
FROM
  sales_table
WHERE
  orders_rank = 1
```
| customer_id | order_date | product_name |
| ----------- | --------   | ------------ |
| A           | 2021-01-01 | sushi        |
| A           | 2021-01-01 | curry        |
| B           | 2021-01-04 | sushi        |

### 8. What is the number of unique menu items and total amount spent for each member before they became a member?
```sql
SELECT
  t1.customer_id,
  COUNT(DISTINCT t1.product_id),
  SUM(t2.price) AS total_purchase
FROM
  dannys_diner.sales t1
  JOIN dannys_diner.menu t2 ON t2.product_id = t1.product_id
  JOIN dannys_diner.members t3 ON t3.customer_id = t1.customer_id
WHERE
  t1.order_date < t3.join_date::DATE
GROUP BY
  t1.customer_id
```
| customer_id | count | total_purchase |
| ----------- | ----- | -------------- |
| A           | 2     | 25             |
| B           | 2     | 40             |

### 9. If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
```sql
WITH temp_a AS(
  SELECT
    t1.customer_id,
    t1.product_id,
    t2.product_name,
    t2.price * 20 AS points
  FROM
    dannys_diner.sales t1
    JOIN dannys_diner.menu t2 ON t2.product_id = t1.product_id
  WHERE
    t1.product_id = 1
  UNION ALL
  SELECT
    t1.customer_id,
    t1.product_id,
    t2.product_name,
    t2.price * 10 AS points
  FROM
    dannys_diner.sales t1
    JOIN dannys_diner.menu t2 ON t2.product_id = t1.product_id
  WHERE
    t1.product_id != 1
)
SELECT
  customer_id,
  SUM(points) AS points
FROM
  temp_a
GROUP BY
  customer_id
ORDER BY
  points DESC
```

| customer_id | points |
| ----------- | ------ |
| B           | 940    |
| A           | 860    |
| C           | 360    |

### 10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?
```sql
SELECT
  sales.customer_id,
  SUM(
    CASE
      WHEN sales.order_date BETWEEN members.join_date :: DATE
      AND (members.join_date :: DATE + 6) THEN 20 * menu.price
      WHEN menu.product_name != 'sushi' THEN 10 * menu.price
      WHEN menu.product_name = 'sushi' THEN 20 * menu.price
    END
  ) AS points
FROM
  dannys_diner.sales
  INNER JOIN dannys_diner.menu ON sales.product_id = menu.product_id
  INNER JOIN dannys_diner.members ON sales.customer_id = members.customer_id
WHERE
  sales.order_date <= '2021-01-31' :: DATE
GROUP BY
  sales.customer_id
ORDER BY
  points
```
| customer_id | points  |
| ----------- | ------  |
| B           | 820     |
| A           | 1370    |




### 11. Danny and his team can use to quickly derive insights without needing to join the underlying tables using SQL Recreate the following table output using the available data.
```sql
SELECT
  sales.customer_id,
  order_date,
  product_name,
  price,
  CASE
    WHEN sales.order_date >= members.join_date THEN 'Y'
    ELSE 'N'
  END AS member
FROM
  dannys_diner.sales FULL
  OUTER JOIN dannys_diner.menu ON menu.product_id = sales.product_id FULL
  OUTER JOIN dannys_diner.members ON members.customer_id = sales.customer_id
ORDER BY
  customer_id,
  order_date
```
| customer_id | order_date | product_name | price | member |
| ----------- | ---------- | ------------ | ----- | ------ |
| A           | 2021-01-01 | sushi        | 10    | N      |
| A           | 2021-01-01 | curry        | 15    | N      |
| A           | 2021-01-07 | curry        | 15    | Y      |
| A           | 2021-01-10 | ramen        | 12    | Y      |
| A           | 2021-01-11 | ramen        | 12    | Y      |
| A           | 2021-01-11 | ramen        | 12    | Y      |
| B           | 2021-01-01 | curry        | 15    | N      |
| B           | 2021-01-02 | curry        | 15    | N      |
| B           | 2021-01-04 | sushi        | 10    | N      |
| B           | 2021-01-11 | sushi        | 10    | Y      |
| B           | 2021-01-16 | ramen        | 12    | Y      |
| B           | 2021-02-01 | ramen        | 12    | Y      |
| C           | 2021-01-01 | ramen        | 12    | N      |
| C           | 2021-01-01 | ramen        | 12    | N      |
| C           | 2021-01-07 | ramen        | 12    | N      |


### 12. Danny also requires further information about the ranking of customer products, but he purposely does not need the ranking for non-member purchases so he expects null ranking values for the records when customers are not yet part of the loyalty program.
```sql
WITH temp_a AS (
  SELECT
    sales.customer_id,
    order_date,
    product_name,
    price,
    CASE
      WHEN sales.order_date >= members.join_date THEN 'Y'
      ELSE 'N'
    END AS member
  FROM
    dannys_diner.sales FULL
    OUTER JOIN dannys_diner.menu ON menu.product_id = sales.product_id FULL
    OUTER JOIN dannys_diner.members ON members.customer_id = sales.customer_id
  ORDER BY
    customer_id,
    order_date
)
SELECT
  *,
  CASE
    WHEN member = 'Y' THEN RANK() OVER(
      PARTITION BY customer_id,
      member
      ORDER BY
        order_date
    )
  END
FROM
  temp_a

```

|customer_id|order_date              |product_name|price|member|case|
|-----------|------------------------|------------|-----|------|----|
|A          |2021-01-01|sushi       |10   |N     |    |
|A          |2021-01-01|curry       |15   |N     |    |
|A          |2021-01-07|curry       |15   |Y     |1   |
|A          |2021-01-10|ramen       |12   |Y     |2   |
|A          |2021-01-11|ramen       |12   |Y     |3   |
|A          |2021-01-11|ramen       |12   |Y     |3   |
|B          |2021-01-01|curry       |15   |N     |    |
|B          |2021-01-02|curry       |15   |N     |    |
|B          |2021-01-04|sushi       |10   |N     |    |
|B          |2021-01-11|sushi       |10   |Y     |1   |
|B          |2021-01-16|ramen       |12   |Y     |2   |
|B          |2021-02-01|ramen       |12   |Y     |3   |
|C          |2021-01-01|ramen       |12   |N     |    |
|C          |2021-01-01|ramen       |12   |N     |    |
|C          |2021-01-07|ramen       |12   |N     |    |
