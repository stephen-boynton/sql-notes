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
