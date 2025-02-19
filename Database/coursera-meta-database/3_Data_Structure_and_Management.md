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

#### UNION:



## Module 2: Update databases and working with views

## Module 3: Functions and MySQL stored procedures

## Module 4: Wrap up