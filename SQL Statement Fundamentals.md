# SQL Statement Fundamentals

<u>#### Database</u>
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

#### Select Distinct - 

Sometimes a table contains a column that has duplicate values, and you may find yourself in a situation where you only want to list the unique/distinct values. The __Distinct__ keyword can be used to return only the distinct values in a column.  The __Distinct__ keyword operates _on_ a column. 
Calling __Distinct__ answer - What are the unique columns are there in the table.

To Clarify which column __Distinct__ is being applied to, you can also use parenthesis for clarity:

```sql
SELECT DISTINCT column FROM table
```


#### Count Function - 

* The __COUNT__ function returns the number of input rows that match a specific condition of a query. 
We can apply __COUNT__ on a spefic column or just pass __COUNT(*)__. 

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

**Count Example**

```sql
SELECT COUNT(*) FROM payment;
```
