* We will see below topics - 
 
   * Timestamps and EXTRACT
   * Math Functions
   * String Functions
   * Sub-query
   * Sulf-Join

* Displaying Current Time Information - 
    * We will see some commands that report back time and date information. 
    * These will be more useful when creating our own tables and databases, rather than when querying a database. 
    * As in PostgreSQL can hold date and time information: 
         * **TIME** - Contains only time. 
         * **DATE** - Contains only date. 
         * **TIMESTAMP** - Contains date and time. 
         * **TIMESTAMPTZ** - Contains date,time and timezone. 

    * Careful considerations should be made when designing a table and database and choosing a time data type. 
    * Depending on the situation you may or may not need the full level of **TIMESTAMPZ**. 
    * Remember, you can always remove historical information, but you cant add it!. 
    
    * Lets explore functions and operations related to these specific data types:- 
         * TIMEZONE
         * NOW
         * TIMEOFDAY
         * CURRENT_TIME
         * CURRENT_DATE


* Extracting Current Time Information -     
    * Lets explore extracting information from a time based data type using:- 
         * EXTRACT()
         * AGE()
         * TO_CHAR()

    * EXTRACT()
        * Allows you to "extract" or obtain a sub-component of a date value - 
            * YEAR
            * MONTH
            * DAY
            * WEEK
            * QUARTER
       
        * Allows you to "extract" or obtain a sub-component of a date value
            * EXTRACT(YEAR FROM date_col)

    * AGE()
        * Calculates and returns the current age given a timestamp
        * Usage: 
            * AGE(date_col)
        * Returns
            * 13 Years 1 mon 5 days 01:34:13.003423

    * TO_CHAR()
        * General function to convert date types to text
        * Useful for timestamp formatting
        * Usage 
            * TO_CHAR(date_col,'mm-dd-yyyy')


**Examples** 

```sql
SELECT EXTRACT(YEAR FROM payment_date) AS Year
FROM payment
```

```sql
SELECT EXTRACT(MONTH FROM payment_date) AS Pay_Month
FROM payment
```

```sql
SELECT EXTRACT(QUARTER FROM payment_date) AS Pay_Month
FROM payment
```

```sql
SELECT AGE(payment_date) AS Age
FROM payment
```

```sql
SELECT TO_CHAR(payment_date, 'MONTH-YYYY')
FROM payment
```

```sql
SELECT TO_CHAR(payment_date, 'MM-dd-YYYY')
FROM payment
```


**Excercise** 

1. During Whcih months did payment occur? 

    * Format your answer to return back the full month name. 

```sql
DISTINCT(TO_CHAR(payment_date,'MONTH'))
FROM payment
```


2. How many payments occurred on a Monday? 
  
```sql
SELECT COUNT(*)
FROM payment
WHERE EXTRACT(dow FROM payment_date) = 1
```


**Mathemetical Functions and Operators** 

* Lets explore some mathemetical operations we can perform with SQL!. 

 ```sql
 SELECT ROUND (rental_rate/replacement_cost,4)*100 AS Percent_Cost
FROM film
 ```

```sql
 SELECT 0.1 * replacement_cost AS Deopsit
 FROM film
 ```

 **String Functions and Operators** 

 * PostgreSQL also provides a variety of string functions and operators that allow us to edit, combine, and alter text data columns. 

 ```sql
 SELECT upper(first_name) || ' ' || upper(last_name) AS full_name
FROM customer
```

```sql
SELECT LOWER(LEFT(first_name,1)) || LOWER(last_name) || '@gmail.com' AS custom_email
FROM customer
```

 **SubQuery** 

 * A sub query allows you to construct complex queries, essentially performing a query on the results of another query. 

 * The syntax is straightforward and involves two SELECT statements. 

 * Lets imagine a table consisting of student names and their test scores - 
   
    * Standard Query - 
       
         ```sql
         SELECT student,grade
         FROM test_scores
         ```

    * Standard Query to return average grade - 
        
        ```sql
        SELECT AVG(grade)
        FROM test_scores
        ```

* How can we get a list of students who scored better than the average grade? 
    
    ```sql
    SELECT AVG(grade) FROM test_scores
    ```

     * It looks like we need two steps, first get the average grade, then compare the rest of the table against it. 

     ```sql
     SELECT AVG(grade) FROM test_scores
     ```
    
    * This is where a subquery can help us get the result in a "Single" query request. 

    ```sql
    SELECT student,grade
    FROM test_scores
    WHERE grade > (SELECT AVG(grade) FROM test_scores)
    ```

    OR 

     ```sql
    SELECT student,grade
    FROM test_scores
    WHERE grade > (70)
    ```
 
* The subquery is performed first since it is inside the parenthesis. 

* We can also use the **IN** operator in conjunction with a subquery to check against multiple results returned. 


    