## SQL EXERCISE SET

AUTHOR
Jaymar Budduan

## ==================================================

## OVERVIEW
This file contains 13 SQL exercises covering filtering, joins, grouping, updates, and data transformation using SQLite.

## ==================================================

## TABLES USED
customers
sales
inventory
new_customers
promo_signups

## ==================================================

## EXERCISE 1
CREATE TABLE promo_signups (
customer_id INTEGER,
customer_name TEXT,
email TEXT,
region TEXT
);

INSERT INTO promo_signups (customer_id, customer_name, email, region)
SELECT customer_id, customer_name, email, region
FROM new_customers
WHERE region = 'NCR';

SELECT * FROM promo_signups;

## ==================================================

## EXERCISE 2
SELECT customer_name, product_name, total_amount, category
FROM sales
WHERE region = 'Visayas'
AND total_amount < 5000
AND category IN ('Accessories', 'Peripherals');

## ==================================================

## EXERCISE 3
SELECT *
FROM sales
WHERE sale_date BETWEEN '2025-04-01' AND '2025-06-30'
ORDER BY sale_date DESC;

## ==================================================

## EXERCISE 4
SELECT first_name, last_name, email, city
FROM customers
WHERE city NOT IN ('Manila', 'Makati', 'Pasig');

## ==================================================

## EXERCISE 5
SELECT item_name
FROM inventory
WHERE item_name LIKE '%Cloud';

## ==================================================

## EXERCISE 6
SELECT first_name, last_name, total_spent
FROM customers
ORDER BY total_spent ASC, first_name ASC
LIMIT 5;

## ==================================================

## EXERCISE 7
SELECT category, COUNT(*) AS num_sales, AVG(total_amount) AS avg_sale_amount
FROM sales
GROUP BY category
ORDER BY avg_sale_amount DESC;

## ==================================================

## EXERCISE 8
SELECT region, SUM(total_amount) AS total_revenue
FROM sales
WHERE category = 'Electronics'
GROUP BY region
HAVING SUM(total_amount) > 100000;

## ==================================================

## EXERCISE 9
SELECT c.first_name, c.last_name, COUNT(s.sale_id) AS total_sales
FROM customers c
LEFT JOIN sales s
ON s.customer_name = c.first_name || ' ' || c.last_name
GROUP BY c.first_name, c.last_name;

## ==================================================

## EXERCISE 10
SELECT item_name, quantity_on_hand,
CASE
WHEN quantity_on_hand = 0 THEN 'Out of Stock'
WHEN quantity_on_hand BETWEEN 1 AND 10 THEN 'Low Stock'
ELSE 'In Stock'
END AS stock_status
FROM inventory;

## ==================================================

##EXERCISE 11
SELECT item_name,
COALESCE(unit_cost, 0) AS unit_cost,
COALESCE(unit_cost, 0) * quantity_on_hand AS inventory_value
FROM inventory;

## ==================================================

## EXERCISE 12
SELECT *
FROM inventory
WHERE unit_cost >= 10000;

UPDATE inventory
SET unit_cost = unit_cost * 1.10
WHERE unit_cost >= 10000;

SELECT *
FROM inventory
WHERE unit_cost >= 10000;

## ==================================================

## EXERCISE 13
ALTER TABLE customers
ADD COLUMN membership_tier TEXT DEFAULT 'Standard';

SELECT first_name, last_name, membership_tier
FROM customers;
