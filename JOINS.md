**JOINS**

* **JOINS** will allow us to combine information from multiple tables!

* A SQL join is a Structured Query Language (SQL) instruction to combine data from two sets of data (i.e. two tables). 

* The main reason for the different **JOIN** types is to decide how to deal with information only present in one of joined tables.

* Different Kinds of **JOINS** - 

   * INNER JOINS
   * OUTER JOINS
   * FULL JOINS
   * UNIONS

* Imagine you’re running a store and would like to record information about your customers and their orders. By using a relational database, you can save this information as two tables that represent two distinct entities: **customers** and **orders**.

* Let’s say we want to find all orders placed by a particular customer. We can do this by joining the customers and orders tables together using the relationship established by the customer_id key:

```sql
SELECT order_date,order_amount
FROM customers
JOIN orders
   ON customers.customer_id = orders.customer_id
WHERE customer_id = 3
```

* Here, we’re joining the two tables using the join keyword, and specifying what key to use when joining the tables in the on customers.customer_id = orders.customer_id line following the join statement. 

**AS Statement (Alias) **

* Before we learn about **JOINS**, Lets see **AS** which allows us to create an **alias** for a column or result. 

* Example - 

```sql
SELECT column AS new_name
FROM table;

SELECT SUM(Column) AS new_name
FROM table;

SELECT amount AS rental_price
FROM payment;

SELECT SUM(amount) AS net_revenue
FROM payment;

```

* The AS operator gets executed at the very end of a query, meaning that we can not use the **ALIAS** inside a **WHERE** operator. 

* Example - 

```sql
SELECT COUNT(amount) AS num_transactions
FROM payment

SELECT COUNT(*) AS num_transactions
FROM payment

SELECT customer_id,SUM(amount) AS total_spent
FROM payment
GROUP BY customer_id

SELECT customer_id, amount AS new_name
FROM payment
WHERE amount > 2
```

**INNER JOIN**

* There are sevral types of **JOINs**, now here we will discuss about **INNER JOIN**. 

* Lets imagine a simple example - 

    * Our Company is holding a conference for people in the movie rental industry. 
    * We will have people register online beforehand and then login the day of the conference. 
    * After the conference we will have two tables - 
        * Registrations
        * Logins

    * The respective id columns indicate what order they registered or logged in on site. 

    * For the sake of simplicity, we will assume the names are unique. 

    * So **INNER JOIN** will result with the set of records that match in both tables.

    ```sql
    SELECT * FROM TableA
    INNER JOIN TableB
    ON TableA.col_match = TableB.col_match

    SELECT * FROM Registrations
    INNER JOIN Logins
    ON Registrations.name = Logins.name

    SELECT reg_id,Logins.name,log_id
    FROM Registration
    INNER JOIN Logins
    ON Registrations.name = Logins.name
    ```
* Remember that table order wont matter in an **INNER JOIN**. 

* Also If you see just **JOIN** without the **INNER**, PostgreSQL will treat it as an **INNER JOIN**

```sql
SELECT payment_id,payment.customer_id,first_name
FROM payment
INNER JOIN customer
ON payment.customer_id = customer.customer_id
```


**OUTER JOIN**

* These type of **JOIN** will allow to specify how to deal with values only present in one of the tables being joined.

* Some Examples - 
    * FULL OUTER JOIN
    * LEFT OUTER JOIN
    * RIGHT OUTER JOIN 


**FULL OUTER JOIN** 

```sql
SELECT * FROM TableA
FULL OUTER JOIN TableB
ON Table.col_match = TableB.col_match
```

```sql
SELECT * FROM TableB
FULL OUTER JOIN TableA
ON Table.col_match = TableB.col_match
```

* Keeping the above example of **INNER JOIN**

```sql
SELECT * FROM Registrations
FULL OUTER JOIN Logins
ON Registrations.name = Logins.name
```

* **FULL OUTER JOIN with WHERE** (Get rows unique to either table(rows not found in both tables)

```sql
SELECT * FROM TableA
FULL OUTER JOIN TableB
ON TableA.col_match = TableB.col_match
WHERE TableA.id IS null OR
TableB.id IS null
```

* Examples - 

```sql
SELECT * FROM customer
FULL OUTER JOIN payment
ON customer.customer_id = payment.customer_id
WHERE customer.customer_id IS null
OR payment.payment_id IS null
```


**LEFT OUTER JOIN** 

* A **LEFT OUTER JOIN** results in the set of records that are in the left table, if there is no match with the right table, the results are null. 

* We can add **WHERE** statement to modify a **LEFT OUTER JOIN**. 

* So what is **LEFT OUTER JOIN** actually looks like - 

```sql 
SELECT * FROM TableA
LEFT OUTER JOIN TableB
ON TableA.col_match = TableB.col_match
```

Are same as - 

```sql 
SELECT * FROM TableA
LEFT JOIN TableB
ON TableA.col_match = TableB.col_match
```

 **LEFT OUTER JOIN** With **WHERE** (Get rows unique to left table) - 

* What if we only wanted entries unique to Table A? Those rows found in Table A and **not** found in Table B. 

The way we do that - 

```sql
SELECT * FROM TableA
LEFT OUTER JOIN TableB
ON TableA.col_match = TableB.col_match
WHERE TableB.id IS null
```

```sql
SELECT film.film_id,title,inventory_id,store_id
FROM film
LEFT JOIN inventory ON
inventory.film_id = film.film_id
WHERE inventory.film_id IS null
```

**RIGHT JOIN** 

* A **RIGHT JOIN** is essentially the same as a **LEFT JOIN**, except the tables are switched.

* This would be the same as switching the table order in a **LEFT OUTER JOIN**.

```sql
SELECT * FROM TableA
RIGHT OUTER JOIN TableB
ON TableA.col_match = TableB.col_match
```

