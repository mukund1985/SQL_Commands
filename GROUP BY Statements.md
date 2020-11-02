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

