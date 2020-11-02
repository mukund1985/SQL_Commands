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

