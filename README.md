# SQL EXERCISE SET

AUTHOR
Jaymar Budduan

# OVERVIEW
This file contains 13 SQL exercises covering filtering, joins, grouping, updates, and data transformation using SQLite.

# TABLES USED
- customers
- sales
- inventory
- new_customers
- promo_signups

## EXERCISE 1
 CREATE TABLE promo_signups (<br>
 customer_id INTEGER,<br>
 customer_name TEXT,<br>
 email TEXT,<br>
 region TEXT<br>
 );

INSERT INTO promo_signups (customer_id, customer_name, email, region)<br>
SELECT customer_id, customer_name, email, region<br>
FROM new_customers<br>
WHERE region = 'NCR';<br>

SELECT * FROM promo_signups;


## EXERCISE 2
SELECT customer_name, product_name, total_amount, category<br>
FROM sales<br>
WHERE region = 'Visayas'<br>
AND total_amount < 5000<br>
AND category IN ('Accessories', 'Peripherals');


## EXERCISE 3
SELECT *<br>
FROM sales<br>
WHERE sale_date BETWEEN '2025-04-01' AND '2025-06-30'<br>
ORDER BY sale_date DESC;


## EXERCISE 4
SELECT first_name, last_name, email, city<br>
FROM customers<br>
WHERE city NOT IN ('Manila', 'Makati', 'Pasig');


## EXERCISE 5
SELECT item_name<br>
FROM inventory<br>
WHERE item_name LIKE '%Cloud';


## EXERCISE 6
SELECT first_name, last_name, total_spent<br>
FROM customers<br>
ORDER BY total_spent ASC, first_name ASC<br>
LIMIT 5;


## EXERCISE 7
SELECT category, COUNT(*) AS num_sales, AVG(total_amount) AS avg_sale_amount<br>
FROM sales<br>
GROUP BY category<br>
ORDER BY avg_sale_amount DESC;


## EXERCISE 8
SELECT region, SUM(total_amount) AS total_revenue<br>
FROM sales<br>
WHERE category = 'Electronics'<br>
GROUP BY region<br>
HAVING SUM(total_amount) > 100000;


## EXERCISE 9
SELECT c.first_name, c.last_name, COUNT(s.sale_id) AS total_sales<br>
FROM customers c<br>
LEFT JOIN sales s<br>
ON s.customer_name = c.first_name || ' ' || c.last_name<br>
GROUP BY c.first_name, c.last_name;


## EXERCISE 10
SELECT item_name, quantity_on_hand,<br>
CASE<br>
WHEN quantity_on_hand = 0 THEN 'Out of Stock'<br>
WHEN quantity_on_hand BETWEEN 1 AND 10 THEN 'Low Stock'<br>
ELSE 'In Stock'<br>
END AS stock_status<br>
FROM inventory;

## EXERCISE 11
SELECT item_name,<br>
COALESCE(unit_cost, 0) AS unit_cost,<br>
COALESCE(unit_cost, 0) * quantity_on_hand AS inventory_value<br>
FROM inventory;

## EXERCISE 12
SELECT *<br>
FROM inventory<br>
WHERE unit_cost >= 10000;<br>
<br>
UPDATE inventory<br>
SET unit_cost = unit_cost * 1.10<br>
WHERE unit_cost >= 10000;<br>
<br>
SELECT *<br>
FROM inventory<br>
WHERE unit_cost >= 10000;

## EXERCISE 13
ALTER TABLE customers<br>
ADD COLUMN membership_tier TEXT DEFAULT 'Standard';<br>
<br>
SELECT first_name, last_name, membership_tier<br>
FROM customers;
