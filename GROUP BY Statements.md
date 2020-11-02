The GROUP BY clause divides the rows returned from the SELECT statement into
groups. 

For each group, you can apply an aggregate function e.g., to calculate the sum
of items or count the number of items in the groups.

**Aggregate Function**

* SQL provided a variety of aggregate functions. 
* The main idea behind an aggregate function is to take multiple inputs and return a single output. 

* Most Common Aggregate Functions:
    * AVG() - returns average value
    * COUNT() - returns number of values
    * MAX() - returns maximum value
    * MIN() - returns minimum value
    * SUM() - returns the sum of all values

* Aggregate function calls happen only in the **SELECT** clause or the **HAVING** clause. 

* Example - 

```sql
SELECT MIN(replacement_cost) FROM film
```

```sql
SELECT MAX(replacement_cost) FROM film
```

```sql
SELECT MAX(replacement_cost), MIN(replacement_cost)  FROM film
```

```sql
SELECT COUNT (*)  FROM film
```

```sql
SELECT AVG (replacement_cost)  FROM film
```

```sql
SELECT ROUND (AVG (replacement_cost),2)   FROM film
```

```sql
SELECT SUM (replacement_cost)  FROM film
```


**GROUP BY Function**

* **GROUP BY** allows us to aggregate columns per some category. 

```sql
SELECT category_col, AGG(data_col)
FROM table
GROUP BY category_col
```

* The **GROUP BY** clause must appear right after a **FROM** or **WHERE** statement. 

```sql
SELECT category_col, AGG(data_col)
FROM table
WHERE category_col!='A'
GROUP BY category_col
```

* In the **SELECT** statement, columns must either have an aggregate function or be in the **GROUP BY** call. 

```sql
SELECT company, division, SUM(sales)
FROM finance_table
GROUP BY company,division
```

```sql
SELECT company,division,SUM(sales)
FROM finance_table
WHERE division IN ('marketing','transport')
GROUP BY company,division
```

* **WHERE** statements should not refer to the aggregation result,. 

```sql
SELECT company, SUM(sales)
FROM finance_table
GROUP BY company
ORDER BY SUM(sales)
LIMIT 5
```

* If you want to start results based on the aggregate, make sure to reference the entire function. 

*Examples - 

```sql
SELECT customer_id FROM payment
GROUP BY customer_id
ORDER BY customer_id
```

```sql
SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
```

```sql
SELECT customer_id, COUNT(amount) FROM payment
GROUP BY customer_id
ORDER BY COUNT(amount) DESC
```

```sql
SELECT customer_id,staff_id,SUM(amount) FROM payment
GROUP BY staff_id,customer_id
ORDER BY customer_id
```

We can do as same like below as well, so at the **SELECT** doesnt matter the position but while doing **GROUP BY** position matters. 

```sql
SELECT staff_id,customer_id,SUM(amount) FROM payment
GROUP BY staff_id,customer_id
ORDER BY staff_id,customer_id
```

```sql
SELECT staff_id,customer_id,SUM(amount) FROM payment
GROUP BY staff_id,customer_id
ORDER BY SUM(amount)
```

* Lets see the **GROUP BY** at date column. 

```sql
SELECT DATE(payment_date), SUM(amount) FROM payment
GROUP BY DATE(payment_date)
ORDER BY SUM(amount) DESC
```

**GROUP BY Excercise**

* We have two staff members, with Staff IDs 1 and 2. We want to give a bonus to the staff member that handled the most payments. (Most in terms of number of payments processed, not total dollor amount).
* How many paymwnts did each staff member handle and who gets the bonus? 

```sql
SELECT staff_id,COUNT(amount)
FROM payment
GROUP BY staff_id
```

* Corporate HQ is conducting a study on the relationship between replacement cost and a movie MPAA rating (e.g. G, PG, R, etc)
* What is the average replacement cost per MPAA rating?
    * Note - You may need to expand the AVG column to view correct results. 

```sql
SELECT rating, (AVG(replacement_cost),2)
FROM film
GROUP BY rating
```

* We are running a promotion to reward our top 5 customers with coupons.
* What are the customer ids of the top 5 customer by total spend? 

```sql
SELECT customer_id, SUM(amount)
FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5
```

**HAVING**

* The **HAVING** clause allows us to filter **after** an aggregation has already taken place. 

* Lets see some previous examples - 

```sql
SELECT company, SUM(sales)
FROM finance_table
GROUP BY company
```

* Lets convert this for **HAVING** type - 

```sql
SELECT company, SUM(sales)
FROM finance_table
WHERE comapny!= 'Google'
GROUP BY company
```
* We have already seen we can filter before executing the **GROUP BY**, but what if we want to filter based on **SUM(sales)?**

* We can not use **WHERE** to filter based off of aggregate results, because those happen **after** a **WHERE** is executed, So I can use **HAVING** clause. 

```sql
SELECT company, SUM(sales)
FROM finance_table
WHERE comapny!= 'Google'
GROUP BY company
HAVING SUM(sales) > 1000
```

* **HAVING** allows us to use the aggregate result as a filter along with a **GROUP BY**. 

FInaly it will be look like - 

```sql
SELECT company,SUM(sales)
FROM finance_table
GROUP BY company
HAVING SUM(sales) > 1000
```

* Examples - 

```sql 
SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
HAVING SUM(amount) > 200
```


```sql
SELECT store_id, COUNT(customer_id) FROM customer
GROUP BY store_id
HAVING COUNT(customer_id) > 300
```

**HAVING Excercise**

* We are launching a platinum service for our most loyal customers. We will assign platinum status to customers that have had 40 or more transaction payments. 
* What customer_ids are eligible for platinum status? 

```sql
SELECT customer_id, COUNT(*)
FROM payment
GROUP BY customer_id
HAVING COUNT(*) >= 40
```

* What are the customer ids of customers who have spent more than $100 in payment transactions with our staff_id member 2 ?

```sql
SELECT customer_id, SUM(amount)
FROM payment
WHERE staff_id = 2
GROUP BY customer_id
HAVING SUM(amount) > 100
```