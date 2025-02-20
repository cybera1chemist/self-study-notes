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

## Module 3: Functions and MySQL stored procedures

## Module 4: Wrap up