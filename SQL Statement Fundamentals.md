# SQL Statement Fundamentals

* SELECT Statement
* SELECT DISTINCT
* COUNT
* SELECT WHERE
* ORDER BY
* LIMIT
* BETWEEN
* IN
* LIKE and ILIKE



#### Database

Create
```sql
create database dbname;
```
Drop
```sql
drop database dbname;
```

#### List All tables from schema - 

```sql
select * from information_schema.tables;
```

#### Selecting Multiple Columns from Table-

```sql
select first_name,last_name,email from customer
```

#### DISTINCT Function - 

* Sometimes a table contains a column that has duplicate values, and you may find yourself in a situation where you only want to list the unique/distinct values. 
* The __Distinct__ keyword can be used to return only the distinct values in a column.  The __Distinct__ keyword operates _on_ a column. 
* Calling __Distinct__ answer - What are the unique columns are there in the table.
* To Clarify which column __Distinct__ is being applied to, you can also use parenthesis for clarity:

```sql
SELECT DISTINCT column FROM table
```


#### COUNT Function - 

* The __COUNT__ function returns the number of input rows that match a specific condition of a query. 
* We can apply __COUNT__ on a spefic column or just pass __COUNT(*)__. 

```sql
SELECT COUNT(name) FROM table
```
```sql
SELECT COUNT(choice) FROM table
```
```sql
SELECT COUNT(*) FROM table
```

Above all statement return the same thing. 

* Because of this __COUNT__ by itself simply returns    back a count of the number of rows in a table. 
* **COUNT** is much more useful when combined with other commands, such as **DISTINCT**. 

```sql
SELECT COUNT(DISTINCT name) FROM table
```

* Example - 

```sql
SELECT COUNT(*) FROM payment;
```

```sql
SELECT COUNT(DISTINCT amount) FROM payment;
```

```sql
SELECT COUNT (payment_date) FROM payment
```

```sql
SELECT COUNT (DISTINCT payment_date) FROM payment
```

#### SELECT WHERE Function - 

* **SELECT** and **WHERE** are the most fundamental SQL statements and you will find yourself using them often. 
* The **WHERE** statement allows us to specify conditions on columns for the rows to be returned. 
* Basic Syntax example:- 

    *  **SELECT** column1,column2
    * **FROM** table
    * **WHERE** conditions;

* The **WHERE** clause appears immediately after the **FROM** clause of the **SELECT** statement. 
* The Conditions are used to filter the rows reutrned from the **SELECT** statement. 
* PostgreSQL prives a variety of standard operators to construct the conditions. 

We first have - 

* Comparison Operators - 
   * Compare a column value to something.
        * Is the price greater than $3.00?
        * Is the pet's name equal to "Sam"?
   * Logical Operators - 

     * Allow us to combine multiple comparison operatos - 
        * **AND**
        * **OR**
        * **NOT**   

* Examples -

```sql
SELECT name, choice FROM table WHERE name = 'David';
```  

```sql
SELECT name, choice FROM table WHERE name = 'David' AND choice='Red';
```  

```sql
SELECT * FROM customer
WHERE first_name = 'Jared';
``` 

```sql
SELECT titel FROM film
WHERE rental_rate >4 AND replacement_cost >= 19.99
AND rating='R'
```

```sql
SELECT phone FROM address
WHERE address = '259 Ipoh Drive'
```

#### ORDER BY Function - 

* You may have noticed PostgreSQL sometimes returns the same request query results in a different order. 
* You can use **ORDER BY** to sort rows based on a column value, in either ascending or descending order. 
* Use ASC to sort in ascending order. 
* Use DESC to sort in descending order. 
* If you leave it blank, **ORDER BY** uses ASC by default.


Basic Syntax for **ORDER BY** - 

```sql
SELECT column_1,column_2
FROM table
ORDER BY column_1 ASC/DESC
```

```sql
SELECT address_id FROM customer
ORDER BY address_id ASC
```

```sql
SELECT company,name,sales FROM table
ORDER BY company,sales
```

```sql
SELECT first_name,last_name FROM customer
ORDER BY store_id DESC,first_name ASC
```

**Note** - ORDER BY comes towards the ends of a query, since we want to do any selection and filtering first, before finally sorting. 


#### LIMIT Keyword - 

* The **LIMIT** command allows us to limit the number of rows returned for a query. 
* Useful for not wanting to return every single row in a table, but only view the top few rows to get an idea of the table layout.
* **LIMIT** also becomes useful in combination with **ORDER BY**
* **LIMIT** goest at the very end of a query request and is the last command to be executed. 

Its time to see some examples - 

``` sql
SELECT * FROM payment
WHERE amount != 0.00
ORDER BY payment_date ASC
LIMIT 5;
```

``` sql
SELECT customer_id FROM payment
ORDER BY payment_date ASC
LIMIT 10;
```

``` sql
SELECT title,length from FILM
ORDER BY length ASC
LIMIT 5
```

```sql
SELECT COUNT(title) FROM film
WHERE length <=50
```

#### BETWEEN Keyword - 

* The **BETWEEN** operator can be used to match a value against a range of values:- 
   * value **BETWEEN** low **AND** high 
   * value >= low **AND** value <= high

* You can also combine **BETWEEN** with the **NOT** logical operator:
   * value **NOT BETWEEN** low **AND** high

* The **NOT BETWEEN** operator is the same as:
   * value < low **OR** value > high
   * value **NOT BETWEEN** low **AND** high

* The **BETWEEN** operator is the same as:
   * value >= low **AND** value <= high
   * value **BETWEEN** low **AND** high

* The **BETWEEN** operator can also be used with dates. You need to format dates in the ISO 8601 standard format, which is YYYY-MM-DD. 
   * date **BETWEEN** '2007-01-01' **AND** '2007-02-01'

* When using **BETWEEN** operator with dates that also include timestamp information, pay careful attention to using **BETWEEN** versu <=,>= comparison operators, due to fact that a datetime starts at 0:00.


* Examples-

```sql
SELECT * FROM payment
WHERE amount BETWEEN 8 AND 9
```

```sql
SELECT COUNT (*) FROM payment
WHERE amount BETWEEN 8 AND 9
```

```sql
SELECT COUNT (*) FROM payment
WHERE amount NOT BETWEEN 8 AND 9
```

```sql
SELECT * FROM payment
WHERE payment_date BETWEEN '2007-02-01' AND '2007-02-15'
```

**Note**- Here while dealing with Date, need to take care timings 00:00 or 23:59. 


#### IN Keyword - 

* In certain cases you want to check for multiple possible value options, for example - if a user's name shows up **IN** a list of known names.

* We can use the **IN** operator to create a condition that checks to see if a value in included in a list of multiple options.

* The general syntax is:
   * value **IN** (option1, option2,...,option_n)


* Example:- 

```sql
SELECT color FROM table
WHERE color IN ('red','blue','green')
```

```sql
SELECT color FROM table
WHERE color NOT IN ('red','blue','green')
```

```sql
SELECT * FROM payment
WHERE amount IN (0.99,1.98,1.99)
```

```sql
SELECT COUNT (*) FROM payment
WHERE amount IN (0.99,1.98,1.99)
```

```sql
SELECT COUNT (*) FROM payment
WHERE amount NOT IN (0.99,1.98,1.99)
```

```sql
SELECT * FROM customer
WHERE first_name IN ('John','Jake','Julie')
```

```sql
SELECT * FROM customer
WHERE first_name NOT IN ('John','Jake','Julie')
```