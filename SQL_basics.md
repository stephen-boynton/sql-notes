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

PostgreSQL allows you ORDER BY a column you didn't even select:

```sql
SELECT first_name
FROM customer
ORDER BY last_name ASC;
```

Other SQL databases may not allow you to do this, but it's pretty cool you can do it in PostgreSQL. Best practice is to select the column you will be sorting by because not everywhere will let you.

## BETWEEN Statements

```sql

SELECT customer_id, amount
FROM payment
WHERE amount BETWEEN 8 AND 9;

SELECT customer_id, amount
FROM payment
WHERE amount NOT BETWEEN 8 AND 9;

SELECT payment_date
FROM payment
WHERE payment_date BETWEEN '2007-02-07' AND '2007-02-15';

```

We use the BETWEEN operator to match a value against a range of values. Easier way to do between to values (>= and <=).

Also you can use NOT BETWEEN, the opposite.

## IN statement

``` sql

SELECT customer_id, rental_id, return_date
FROM rental_id
WHERE customer_id IN (1,2)
ORDER BY return_date DESC;

SELECT customer_id, rental_id, return_date
FROM rental_id
WHERE customer_id NOT IN (1,2)
ORDER BY return_date DESC;

SELECT customer_id, rental_id, return_date
FROM rental_id
WHERE customer_id IN (1,13,10)
ORDER BY return_date DESC;

```

IN with WHERE to check if value matches any value in list of value.

IN will return faster than using a whole bunch of = and OR/AND statements.

Can also use NOT IN.

## LIKE Statement

```sql
SELECT first_name, last_name
FROM customer
WHERE first_name LIKE 'Jen%';

SELECT first_name, last_name
FROM customer
WHERE first_name LIKE '%y';

SELECT first_name, last_name
FROM customer
WHERE first_name LIKE '%er%';

SELECT first_name, last_name
FROM customer
WHERE first_name LIKE '_her%';

SELECT first_name, last_name
FROM customer
WHERE first_name NOT LIKE 'Jen%';

SELECT first_name, last_name
FROM customer
WHERE first_name ILIKE 'jEnN%';

```

Uses pattern matching. The % pattern says find me values that are like 'Jen' and anything after. You can also use wildcard and the `_` for matching a single character. There is also NOT LIKE.

PostgreSQL provides case insensitive version of LIKE -- ILIKE.
