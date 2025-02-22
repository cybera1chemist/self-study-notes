# 3. Data Structure and Management in MySQL

## Module 1: Intro to MySQL

### Filtering Data

|  关键字  | Syntax | Explanation |
| ----- | ------ | --- |
| AND, OR, NOT | WHERE condition1 AND condition2;|  |
| IN | SELECT * FROM tb WHERE col IN (v1, v2);| col = v1 or v2 |
| BETWEEN | SELECT * FROM tb WHERE col BETWEEN v1 AND v2;| v can be number or date |
| LIKE | SELECT * FROM tb WHERE col LIKE pattern;||

#### Patterns that can be used by LIKE:
* %: 0, 1 or multiple characters
* \_: 1 single character

example: LIKE 'g__%';    \-\-begin with g, and len >= 3

### Joining Tables

#### Alias:

Temporary names. Can rename col, functions, tables...

`SELECT col1 AS col1_alias, col2, col3 AS col3_alias FROM tb;`

example: 

`SELECT CONCAT (f_name, " ", last_name) AS 'client_name' FROM client_details;`

`SELECT t.first_col FROM a_long_name_table AS t;`

#### Join:

| Join Type | Explanation|  |
| -----     | -----     | ---|
| INNER JOIN | Values in both left and right tables |`SELECT t1.col FROM t1 INNER JOIN t2 ON t1.col = t2.col;`|
|LEFT JOIN |values in both, or values in left|`SELECT t1.col1, t2.col2 FROM t1 LEFT JOIN t2 ON t1.col3 = t2.col4;`|
|RIGHT JOIN|opposite of LEFT JOIN|`SELECT t1.col1, t2.col2 FROM t1 RIGHT JOIN t2 ON t1.col3 = t2.col4;`|
|SELF JOIN|values in either table|`SELECT t1.col1, t2.col2 FROM table AS t1 INNER JOIN table AS t2 ON t1.col3 = t2.col4;`|

* Note: When using SELF JOIN, we should use key word INNER JOIN and AS to use 1 table as 2 tables （什么弱智语法...）

#### UNION:

Purpose: Combine multiple columns.

Syntax 1: by default, it returns distinct values

`SELECT col1, col2 FROM tb1 UNION SELECT col1, col2 FROM tb2;`

Requiremens:

1. There are 2 `SELECT` here, and we must select the same number of columns.
2. The related (unioned) columns must have the same data type.

Syntax 2: use `ALL` to returns duplicated values

`SELECT col1, col2 FROM tb1 UNION ALL SELECT col1, col2 FROM tb2;`


### Grouping Data

#### GROUP BY:

Syntax:
```
SELECT col1, col2 FROM tb GROUP BY col1, col2;
SELECT col1, col2 FROM tb WHERE condiion GROUP BY col1, col2;
-- if there's a WHERE, GROUP BY must be after WHERE
```

* Aggreate functions examples:

SUM, AVERAGE, MAX, MIN, COUNT

* Examples of using GROUP BY:

1. See what departments do we have:

`SELECT Department FROM orders GROUP BY Department;`

This is identical to:

`SELECT DISTINCT Department FROM orders;`

2. Compute each department's total orders number:

`SELECT Department, COUNT(Department) FROM orders GROUP BY Department;`


#### HAVING:

Syntax: (use it after GROUP BY)

```
SELECT c1, c2 FROM tb WHERE condition1
GROUP BY c1
HAVING condition2
```

Example: Filter the grouped rows.
`SELECT Department, SUM(orderTotal) FROM orders GROUP BY Department HAVING SUM(orderTotal) > 2275;`

* Difference from `WHERE`: we use where to filter the table first, then we select rows, then we group them. `HAVING` is used at last to filter the grouped table. （明明也用`WHERE`就行了……这到底谁发明的语言，发明者以为让编程语言 看着越像自然语言（英语）使用体验就会越好吗，《黑客与画家》里面说，如果设计师把用户都当傻子，就不可能设计出优雅的作品）
* If we don't use `GROUP BY` and use `HAVING` by itself, it will be very similar to `WHERE`.

## Module 2: Update databases and working with views

### Use `REPLACE` to Update and Insert Data

Syntax1: (very similar to `INSERT` command)
```
REPLACE INTO tb (c1, c2) VALUES (v1, v2);
```
Syntax2:
```
REPLACE INTO tb (c1, c2) SET col = value;
-- This will replace other columns' values with NULLs where col = value
```

How it works?
1. Check the primary keys (or `UNIQUE` keys)
2. If it can't find any matching key, it will add new data (just like `INSERT`)
3. Else, it will delete the matched key and replace it

Example: Replace an old employee with a new one
```
-- 已知老员工的ID是1
REPLACE INTO Employees(ID, name) VALUES (1, 'Mary');
```

### Constraints

#### 3 types of constraints:
|Constraint Type|Explanation|
| ---- |----|
|Key constraints|primary key|
|Domain constraints|data type or data range|
|Referential integrity constraints|the foreign key must exist in parent table|

#### Ways to constraint columns:

`not null`, `unique`, `check`, `cascade`

Example:

```
create table customers(CustomerID INT not null primary key,
    phoneNumber INT not null unique);
create table bookings(ID int not null primary key,
    NumOfGuests int not null CHECK(NumOfGuests<=8),
    CustomerID, 
    foreign key (CustomerID) References customers.CustomerID
    ON DELETE CASCADE ON UPDATE CASCADE);
```
`ON DELETE CASCADE` or `ON UPDATE CASCADE`: if a customer is deleted in customer table, then bookings table can't reference it, so the coresponding rows will be deleted/updated too

### Changing Table Structure

#### Use `ALTER TABLE` to modify constraints

|Command|Syntax|
|----|----|
|MODIFY|`ALTER TABLE tb MODIFY c1 int not null unique;`|
|ADD|`ALTER TABLE tb ADD COLUMN col int check(col>=5); -- can either add constraint or not`|
|DROP|`ALTER TABLE tb ADD COLUMN col;`|

#### Copying tables

Syntax1:
```
CREATE TABLE new_tb SELECT cols FROM old_tb;
```
Syntax2:
```
CREATE TABLE database1.new_tb SELECT cols FROM db2.old_tb;
```

### Sub-Queries

Definition: an inner query placed within an outer query

(child query and parent query)

Example:
```
SELECT cols FROM tb 
WHERE expression operator (SELECT col FROM tb WHERE condition);
```

* operators:

math operators: >, <, =, <=, >=...

other operators: ALL, ANY, SOME, EXISTS, NOT EXISTS

* Explanation:

`SELECT cols FROM tb WHERE something <= ALL (v1, v2, v3)`: true if something <= v1 and v2 and v3

`SELECT cols FROM tb WHERE something <= ANY (v1, v2, v3)`: true if something <= v1 or v2 or v3

`SELECT cols FROM tb WHERE EXISTS (sub-query)`: true if something <= v1 or v2 or v3

### Virtual Tables



## Module 3: Functions and MySQL stored procedures

## Module 4: Wrap up