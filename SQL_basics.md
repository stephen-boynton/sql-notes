# Syntax Basics

## SELECT statement

`SELECT column1, column2, ... FROM table_name`

Comma between columns or `*` for all! But it's not good practice to use `*`, because it could be ridiculous. In small tables, it's not really an issue. You should be as specific as possible, because it could slow the response from the server. So don't be lazy.

You can technically write everything in either case, but good practice is capitalize.

Here are some examples:

``` sql
SELECT first_name, last_name FROM actor;
SELECT first_name, last_name FROM customer;
```

### SELECT DISTINCT

``` sql
SELECT DISTINCT column_1, column_2 FROM table_name
SELECT DISTINCT release_year FROM film;
SELECT DISTINCT rental_rate FROM film;
```

This removes all copies and only returns unique information. Such as you have two titles worth 4.99, then it would only return 4.99 once.

### SELECT WHERE

``` sql
SELECT column_1, column_2 ... column_n FROM table_name WHERE conditions;

SELECT last_name, first_name
FROM customer
WHERE first_name = 'Jamie';

SELECT last_name, first_name
FROM customer
WHERE first_name = 'Jamie' AND last_name = 'Rice';

SELECT customer_id, amount, payment_date
FROM payment_date
WHERE amount <= 1 OR amount >= 8;

```

One of the most important combinations for search queries! Search rows for conditions.

WHERE comes after the FROM clause. Operators are normal but you use OR or AND instead of || or &&.

It doesn't matter what order you put the columns selection are in, that's what order it will be returned in.

## COUNT Function

``` sql
SELECT COUNT(*) FROM table;

SELECT COUNT(column) FROM table;

SELECT COUNT(*) FROM payment;

SELECT COUNT(DISTINCT amount) FROM payment_date;
```

The COUNT function returns the number of input rows that match a specific condition of a query.

The `COUNT(*)` function returns the number of rows returned by Select Clause. PostGre scans sequentially.

## LIMIT statement

``` sql

SELECT * FROM customer
LIMIT 5;

```

LIMIT allows you to limit the number of rows you get back after a query, usually goes at the end of a query.

ORDER BY is a good use case. Good to take a quick peek at what the data looks like in the table.

## ORDER BY statement

```sql
SELECT column_1, column_2
FROM table_name
ORDER BY column_1 ASC/DESC;

SELECT first_name, last_name
FROM customer
ORDER BY first_name ASC;

SELECT last_name, first_name
FROM customer
ORDER BY last_name DESC;

SELECT last_name, first_name
FROM customer
ORDER BY last_name ASC,
first_name DESC;
```

ORDER BY allows you to return things in a specific order, duh. ASC = ascending order and DESC = descending order. You choose one, not both. Never both. You can order by multiple columns. ASC is the default.
