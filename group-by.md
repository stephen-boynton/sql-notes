# GROUP BY Statements

## MIN MAX AVG SUM - Aggregate Functions

```sql

SELECT AVG(amount) FROM payment;

SELECT ROUND(AVG(amount), 2) FROM payment;

SELECT MIN(amount) FROM payment;

SELECT SUM(amount) FROM payment;

```

COUNT is an aggregate function. These combine data into a single result.

## GROUP BY

``` sql

SELECT column_1, aggregate_function(column_2)
FROM table_name
GROUP BY column_1;

SELECT customer_id
FROM payment
GROUP BY customer_id;

SELECT customer_id, SUM(amount)
FROM payment
GROUP BY customer_id;

SELECT customer_id, SUM(amount)
FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC;

SELECT staff_id COUNT(payment_id)
FROM payment_date
GROUP BY staff_id;

SELECT rating, COUNT(rating) FROM film
GROUP BY rating;

SELECT rental_duration, COUNT(rental_duration)
FROM film
GROUP BY rental_duration;

SELECT rating, AVG(rental_rate)
FROM film
GROUP BY rating;

SELECT customer_id, SUM(amount)
FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5;

```
The GROUP BY is one of the most useful tools for SQL. The GROUP BY clause divides the rows returned from the SELECT statement into groups.

For each group, you can apply an aggregate function:

* calc the sum of items
* count the number of items in the group

## HAVING

``` sql
SELECT column_1, aggregate_function(column_2)
FROM table_name
GROUP BY column_1
HAVING condition;

SELECT customer_id, SUM(amount)
FROM payment_date
GROUP BY customer_id;
HAVING SUM(amount) > 200;

SELECT store_id, COUNT(customer_id)
FROM customer
GROUP BY store_id;
HAVING COUNT(customer_id) > 300;

SELECT rating, AVG(rental_rate)
FROM film
WHERE rating IN ('R', 'G', 'PG');
GROUP BY rating
HAVING AVG(rental_rate) < 3;

```
Kind of like WHERE, but with a GROUP BY statement. The HAVING clase sets the condition for group rows created by the GROUP BY clause after the GROUP BY clause applies while the WHERE clause sets the condition for individual rows before GROUP BY clause applies. This is the main difference between HAVING and WHERE clauses.

HAVING does the filtering *after* the GROUP BY statement.
