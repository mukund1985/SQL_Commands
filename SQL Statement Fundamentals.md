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

**Example**

```sql
SELECT COUNT(*) FROM payment;
```

```sql
SELECT COUNT(DISTINCT amount) FROM payment;
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

* Basic Syntax for **ORDER BY** - 

```sql
      SELECT column_1,column_2
      FROM table
      ORDER BY column_1 ASC/DESC
```

```sql

      SELECT address_id FROM customer
      ORDER BY address_id ASC
```

**Note** - ORDER BY comes towards the ends of a query, since we want to do any selection and filtering first, before finally sorting. 

