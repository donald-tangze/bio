# [SQL in a Nutshell](https://www.oreilly.com/library/view/sql-in-a/9781492088851/?_gl=1*em2e7y*_ga*MTMxMDkzODA0MS4xNjk3NDQxMDY2*_ga_092EL089CH*MTY5NzQ0NTk4Mi4yLjAuMTY5NzQ0NTk4Mi42MC4wLjA.)



## 1. Dataset Hierarchy

Catalogs (Instance) -> Schema( Database) -> Table (View) -> Column -> Data Type -> Constraint

## 2.Foundamental Concepts



#### 2.1.Category of syntax

* Identifiers   User- or System-supplied name for database objects, such as table, index, constraint...

* Literals        User- or System-supplied string or values that are not Identifiers   

  > include number, strings, dates, and boolean

* Operators

  > symbols specifying an action to be performed on one or more expressions, most often in DELETE, INSERT, SELECT, UPDATE statements.

   * Arithmetic operators     + - * / %
   * Assignment operators   =   :=
   * Bitwise operators           |  ^
   * Comparison operators    = <> >= <=
   * Logical                                 ALL AND ANY BETWEEN EXISTS  IN LIKE NOT OR SOME
   * Set                                        UNION [ALL]  INTERSECT   EXCEPT
   * Unary                            +   -  ~

* Reserved words and keywords

  > Words with special meaning to the database SQL parser.

#### 2.2.Data Type

* NUMBER         SMALLINT, BIGINT, INTEGER, NUMERIC(p, s), FLOAT, DOUBLE
* Boolean
* character, VARCHAR, TEXT,  
* Temporal           date/TIME/datetime/ TIMESTAMP
* Collection           Array
* JSON
* XML
* Geospatial type
* BINARY  十六进制存储 (BLOB, CLOB, NCLOB) 

#### 2.3.CONSTRAINT

* primary key   must be unique and not null; must not  be type of blob, array
* FORIGN KEY Constraint
* UNIQUE
* CHECK Constraint

## 3.DDL

##### 3.1. CREATE DATABASE

* CREATE SCHEMA

##### 3.3. CREATE TABLE

```sql
CREATE [{LOCAL TEMPORARY| GLOBAL TEMPORARY}] TABLE table_name
   (column_name datatype attributes [,...] ) |
   [column_name WITH OPTIONS options] |
   [LIKE  table_name] |
   
   [REF IS column_name
     {SYSTEM GENERATED | USER GENERATED | DERIVED} ]
   [CONSTRAINT constraint_type [constraint_name] [,...] ]
[OF type_name [UNDER super_table] [table_definition] ]
[ON COMMIT {PRESERVE ROWS | DELETE ROWS}
```

column_name  data_type + attribute( NOT NULL, DEFAULT expression, collate, refrence, CONSTRAINT)

* CREATE ROLE

  ```sql
  CREATE ROLE role_name [WITH ADMIN {CURRENT_USER | CURRENT_ROLE}]
  ```

##### 3.3. CREATE INDEX

```CREATE [UNIQUE] INDEX index_name ON table_name (column_name[, ..])```

Unique Indexes

Multi-column Indexes

type of indexes: B-tree Indexes;  Bitmap indexes;  Text Indexes



* CREATE VIEW
* ALTER commands

```
ALTER TABLE table_name
  [ADD [COLUMN] column_name datatype attributes]
| [ALTER [COLUMN] column_name SET DEFAULT default_value]
| [ALTER [COLUMN] column_name DROP DEFAULT]
| [ALTER [COLUMN] column_name ADD SCOPE table_name
| [ALTER [COLUMN] column_name DROP SCOPE {RESTRICT | CASCADE}]
| [DROP [COLUMN] column_name {RESTRICT | CASCADE}]
| [ADD table_constraint]
| [DROP CONSTRAINT table_constraint_name {RESTRICT | CASCADE}]
```

* DROP commands

## 4.Read data (select)

```sql
SELECT [{ALL | DISTINCT}] select_item [AS alias] [,...]
FROM [ONLY | OUTER]
   {table_name  [[AS] alias] | view_name [[AS] alias]} [,...]
[ [join_type] JOIN join_condition ]

[WHERE search_condition] [ {AND | OR | NOT} search_condition [...] ]

[GROUP BY group_by_expression{group_by_columns | ROLLUP group_by_columns |
      CUBE group_by_columns | GROUPING SETS ( grouping_set_list ) |
      ( ) | grouping_set , grouping_set_list}
   [HAVING search_condition] ]
[ORDER BY {order_expression [ASC | DESC]} [,...] ]
```

##### 4.1.JOIN Clause  |  JOIN Subclause

```sql
FROM table [AS alias] {CROSS JOIN |
{ [NATURAL] [join_type] JOIN joined_table [AS alias]
   { ON join_condition1 [{AND|OR} join_condition2] [...] ] |
     USING (column1 [,...]) } }
[...]

/*
* JOIN TYPE
*    [CROSS] JOIN
*    [INNER] JOIN
*    [LEFT | RIGHT] [OUTER] JOIN
*    FULL [OUTER] JOIN
*/
```

##### 4.2. GROUP BY Clause

```
[GROUP BY group_by_expression {group_by_columns 
	| ROLLUP group_by_columns 
	| CUBE group_by_columns 
	| GROUPING SETS ( grouping_set_list ) 
	| ( ) | grouping_set , grouping_set_list}
   [HAVING search_condition] ]
   
   HAVEING Clause add search conditions on the result of the GROUP BY Clause
```

##### 4.3.ORDER BY Clause

```
ORDER BY {sort_expression [COLLATE collation_name]
   [ASC | DESC]} [,...]
```

##### 4.4. WHERE Clause

```
 { WHERE search_criteria | WHERE CURRENT OF cursor_name } 
```

* BETWEEN
* Filter
* LIKE
* IN
* NOT
* IS NULL  or IS NOT NULL
* EXISTS  SubQuery
* SOME | ANY

##### 4.5. Sub Query



## 5.DML(Insert, delete, update, commit)

| SQL command       | SQL class       | MySQL/ MariaDB | Oracle | PostgreSQL | SQL Server |
| ----------------- | --------------- | -------------- | ------ | ---------- | ---------- |
| COMMIT            | SQL-transaction | SWV            | SWV    | SWV        | SWV        |
| DELETE            | SQL-data        | SWV            | SWV    | SWV        | SWV        |
| INSERT            | SQL-data        | SWV            | SWV    | SWV        | SWV        |
| MERGE             | SQL-data        | NS             | SWV    | NS         | SWV        |
| RELEASE SAVEPOINT | SQL-transaction | S              | NS     | S          | NS         |
| RETURNING         | Non-standard    | NS/SWL         | SWV    | S          | NS         |
| ROLLBACK          | SQL-transaction | SWL            | SWV    | S          | SWV        |
| SAVEPOINT         | SQL-transaction | S              | S      | S          | SWL        |
| SET TRANSACTION   | SQL-transaction | SWV            | SWL    | SWV        | SWL        |
| START TRANSACTION | SQL-transaction | SWL            | NS     | SWV        | NS         |
| TRUNCATE TABLE    | SQL-data        | SWL            | SWV    | SWV        | SWL        |
| UPDATE            | SQL-data        | SWV            | SWV    | SWV        | SWV        |

* COMMIT

* DELETE

  ```sql
  DELETE FROM { table_name | ONLY (table_name) }
  [{ WHERE search_condition | WHERE CURRENT OF cursor_name }]
  ```

* INSERT

  ```sql
  INSERT INTO [ONLY] {table_name | view_name} [(column1 [,...] )]
  [OVERRIDE {SYSTEM | USER} VALUES]
  {DEFAULT VALUES | VALUES (value1 [,...]) | SELECT_statement }
  ```

* MERGE

* ROLLBACK

* TRUNCATE TABLE

* UPDATE

  ```sql
  UPDATE [ONLY] {table_name | view_name}
  SET {{column_name = { ARRAY [array_val [,...] ] | DEFAULT |
     NULL | scalar_expression},
        column_name = { ARRAY | DEFAULT |
     NULL | scalar_expression}
        [,...] }
      | ROW = row_expression }
  [ WHERE search_condition | WHERE CURRENT OF cursor_name ]
  ```

## 6.Security

#### 6.1. CONNECT

mysql -uroot -p'Abc123456!' < sakila-schema.sql

mysql -uroot -p'Abc123456!' < sakila-data.sql



##### 6.1.1. [create User](https://dev.mysql.com/doc/refman/8.0/en/create-user.html)



#### 6.2. CREATE TABLE

#### 6.3. GRANT 

```json
GRANT { {object privilege [,...] | role [,...]} }
[ON database_object_name]
[TO grantee [,...] ]
[WITH HIERARCHY OPTION] [WITH GRANT OPTION] [WITH ADMIN OPTION]
[FROM { CURRENT_USER | CURRENT_ROLE } ]
```

##### MySQL GRANT

```
GRANT [ 
		{ 
            ALL [PRIVILEGES] 
            | {SELECT | INSERT | UPDATE} [ (column_name[, ...]) ] 
            | DELETE | REFERENCES [ (column_name[, ...]) ] 
        } 
   		|
   		{
            [{ALTER | CREATE | DROP} [dml_option]] 
            | [EVENT] | [EXECUTE] |
            [FILE] | [INDEX] | [LOCK TABLES] | [PROCESS] | [RELOAD] |
            [REPLICATION {CLIENT | SLAVE}] | [SHOW DATABASES] | [SHOW VIEW] | 
            [SHUTDOWN] | [SUPER] | [TRIGGER] | [USAGE]
   		}[, ...]
		ON [ {TABLE | FUNCTION | PROCEDURE} ] 
			{ [database_name.]table_name | * | *.* | database_name.* }
		[PROXY ON user_name TO user_name[, ...]] 
		TO grantee_name [IDENTIFIED BY [PASSWORD] 'password'][, ...]
		[AS user_name 
   			[WITH ROLE {DEFAULT | NONE | ALL | ALL EXCEPT [role_name[, ...]] } ]
		[REQUIRE security_options]
		[WITH with_option[...]]
```



#### 6.4. REVOKE



![image-20231016191629334](C:\Users\donal\AppData\Roaming\Typora\typora-user-images\image-20231016191629334.png)

## 7.Built-in Function (Scalar Function)

#### 7.1.Variable function (date and time functions)

![image-20231016155001613](C:\Users\donal\AppData\Roaming\Typora\typora-user-images\image-20231016155001613.png)

#### 7.2. General-purpose functions

* CASE

  ```
  CASE WHEN expression1 THEN value1
       WHEN expression2 THEN value2
       ELSE default value
   END
  ```

* CAST

  

* NULLIF(expression,  defaultValue)

#### 7.3. Numeric functions

* ABS

* CEIL / CEILING  (nearest larger integer)

* FLOOR              (nearest smaller integer)

* Round()

* EXTRACT 日期  temporal expression   EXTRACT(*data_part* FROM *expression*)

  ```
  EXTRACT(data_part FROM expression)  
  DATEPART(data_part, expression)  (MS SQL Server)
  ```

  

* MOD

* POSITION

* POWER

* SQRT

* Trigonometric functions 三角函数

![image-20231016155149671](C:\Users\donal\AppData\Roaming\Typora\typora-user-images\image-20231016155149671.png)

#### 7.4 String functions

* Concatenation operator   CONCAT(string1, string2 ...)       ||
* **CONVERT**    
* LOWER / UPPDER
* OVERLAY
* SUBSTRING
* TRIM

![image-20231016155450810](C:\Users\donal\AppData\Roaming\Typora\typora-user-images\image-20231016155450810.png)

#### 7.5. Date function

##### 7.5.0. CAST()

```
CAST('2023-10-23 16:45:00' AS DATE)

CAST('134abc' AS signed integer)
```

##### 7.5.1. Str_to_date()

```
Str_to_date('23-10-2023', '%m-%d-%Y')
DATE_FORMAT()
```



##### 7.5.2. DATE_ADD()

```
DATE_ADD(date1,  INTERVAL numberic DAY)
EXTRACT(INTERVAL FROM expression)  
DATEPART(INTERVAL, expression)  (MS SQL Server)
```

Interval name:   DAY,  YEAR, MONTH, HOUR, MINUTE, SECOND

equivalent to   DATEADD (MS Server) ;   add_months(Oracle) 

##### 7.5.3. Current date/time

CURRENT_DATE        CURRENT_TIME()               CURRENT_TIMESTAMP()

##### 7.5.4. DateDiff

return the number of full days between two dates.



#### 7.6. Collection functions



#### 7.6. Platform-Specific  extensions

##### 7.6.1.MYSQL

* DATE_FORMAT(date, format)      sample: DATE_FORMAT('2023-10-14', '%m-%d-%Y')

* TIME_FORMAT(time, format)

* HEX()

* IF(exp1, exp2, exp3)

* TIMESTAMP(exp1[, exp2])         sample: TIMESTAMP('2023-10-14', "09:30:00")

* STR_TO_DATE(str, format)         sample: STR_TO_DATE('2023-10-14', '%Y-%m-%d')

  > reverse to DATE_FORMAT(date, format) 

##### 7.6.2.ORACLE

* NEW_TIME(date, time_zone1, time_zone2)

* NEXT_DAY(date, string)

##### 7.6.3.PostgreSQL

* FORMAT(string, replace1[, replace2])
* TO_CHAR(expression, format)     convert expression to formatted string
* TO_DATE(string, format)      sample:  TO_FORMAT('2023-10-14', 'MM-DD-YY HH24-MI-SS')
* TO_TIMESTAMP(string, format)
* TO_NUMBER(string, format)

##### 7.6.5.SQL Server

* GETDATE()

## 8.Aggregate and Window functions

#### 8.1. Aggregate functions

* MAX/Min(expression)
* SUM(expression)
* AVG(expression)
* COUNT(*)
* having clause:  filter result set after grouping  

#### 8.2. Window functions, aka, Analytic functions

**window function is equivalent to Group_Clauses.  They both divided selected result sets into different set/collections by criteria. Here, in window function, criteria might be a expression, time range**

**Then are used together with aggregate  functions: Max, Min, avg, sum**



```sql
FUNCTION_NAME(expr) [filter_clause] OVER window_clause
filter_clause ::= FILTER ( WHERE boolean_expression )
window_clause ::= window_name | (window_specification)
window_specification ::= [partitioning] [ordering] [framing]
partitioning ::= PARTITION BY value[, value...] 
   [COLLATE collation_name]
ordering ::= ORDER [SIBLINGS] BY rule[, rule...]
rule ::= {value | position | alias} [ASC | DESC] 
   [NULLS {FIRST | LAST}]
framing ::= {ROWS | RANGE | GROUPS} {start | between} [exclusion]
start ::= {UNBOUNDED PRECEDING | unsigned-integer PRECEDING | 
   CURRENT ROW}
between ::= BETWEEN bound1 AND bound2
bound1 ::= bound
bound2 ::= bound
bound ::= {start | UNBOUNDED FOLLOWING | unsigned-integer FOLLOWING}
exclusion ::= {EXCLUDE CURRENT ROW | EXCLUDE GROUP | EXCLUDE TIES | 
   EXCLUDE NO OTHERS}
```

select param1, sum(param2) over *window_clause*   from *table_name*

window_clause ::   [*partitioning*] [*ordering*] [*framing*]

*partitioning* ::  partition by value

*ordering* :: order by rule

*framing* :: {ROWS | RANGE | GROUPS} {*start* | *between* }

*start*  ::  UNBOUNDED PRECEDING  |  CURRENT ROW  

*between*  ::  BETWEEN *bound1* AND *bound2*

*bound*  ::  { start }

```sql
# Example

SELECT 
    DISTINCT visited_on, 
    SUM(amount) OVER(ORDER BY visited_on RANGE BETWEEN INTERVAL 6 DAY PRECEDING AND CURRENT ROW) amount, 
    MIN(visited_on) OVER() 1st_date 
    FROM Customer
```

#### 8.3. Comparison between Group Clause and Window functions

window function can support a virtual, moving window surrounding a row within  a partition

## 9. PL / SQL

| SQL command      | SQL class    | MySQL/ MariaDB  | Oracle          | PostgreSQL      | SQL Server      |
| ---------------- | ------------ | --------------- | --------------- | --------------- | --------------- |
| ALTER AGGREGATE  | Non-standard | NS              | NS              | SWV             | NS              |
| ALTER FUNCTION   | Non-standard | SWV             | SWV             | SWV             | SWV             |
| ALTER METHOD     | SQL-schema   | NS              | NS              | NS              | NS              |
| ALTER PROCEDURE  | SQL-schema   | SWV             | SWV             | SWV             | SWV             |
| ALTER TRIGGER    | Non-standard | NS              | SWV             | SWV             | SWV             |
| CALL             | SQL-schema   | [ON ALL SERVER] | SWV             | [ON ALL SERVER] | SWL             |
| CLOSE            | SQL-data     | [ON ALL SERVER] | [ON ALL SERVER] | [ON ALL SERVER] | SWV             |
| CREATE AGGREGATE | Non-standard | SWV             | SWV             | SWV             | SWV             |
| CREATE CAST      | SQL-schema   | NS              | NS              | SWV             | NS              |
| CREATE FUNCTION  | SQL-schema   | SWV             | SWV             | SWV             | SWV             |
| CREATE METHOD    | SQL-schema   | NS              | NS              | NS              | NS              |
| CREATE PROCEDURE | SQL-schema   | SWV             | SWV             | SWV             | SWV             |
| CREATE TRIGGER   | SQL-schema   | SWL             | SWV             | SWV             | SWL             |
| DECLARE CURSOR   | SQL-data     | SWL             | SWL             | SWL             | SWL             |
| DROP AGGREGATE   | Non-standard | [ON ALL SERVER] | [ON ALL SERVER] | [ON ALL SERVER] | [ON ALL SERVER] |
| DROP CAST        | SQL-schema   | NS              | NS              | [ON ALL SERVER] | NS              |
| DROP FUNCTION    | SQL-schema   | [ON ALL SERVER] | [ON ALL SERVER] | [ON ALL SERVER] | [ON ALL SERVER] |
| DROP PROCEDURE   | SQL-schema   | [ON ALL SERVER] | [ON ALL SERVER] | [ON ALL SERVER] | [ON ALL SERVER] |
| DROP TRIGGER     | SQL-schema   | [ON ALL SERVER] | [ON ALL SERVER] | [ON ALL SERVER] | [ON ALL SERVER] |
| FETCH            | SQL-data     | SWL             | SWL             | SWV             | SWV             |
| OPEN             | SQL-data     | [ON ALL SERVER] | SWV             | [ON ALL SERVER] | SWV             |
| RETURN           | SQL-schema   | SWL             | [ON ALL SERVER] | SWV             | SWV             |

#### 9.1.procedure/ function

```sql
CREATE {PROCEDURE | FUNCTION} object_name
   ( [{[IN | OUT | INOUT] [parameter_name] data_type
   [DEFAULT parameter_default] [AS LOCATOR] [RESULT]}[, ...]] )
[RETURNS data_type [AS LOCATOR] | returns_table_type]
[CAST FROM data_type [AS LOCATOR]]]
[LANGUAGE {ADA | C | COBOL | FORTRAN | M | MUMPS | PASCAL | PLI | SQL}]
[PARAMETER STYLE {SQL | GENERAL}]
[SPECIFIC specific_name]
[DETERMINISTIC | NOT DETERMINISTIC]
[NO SQL | CONTAINS SQL | READS SQL DATA | MODIFIES SQL DATA]
[RETURN NULL ON NULL INPUT | CALL ON NULL INPUT]
[DYNAMIC RESULT SETS int]
[STATIC DISPATCH] code_block

returns_table_type ::= TABLE [(column_name1 data_type1, 
   column_name2 data_type2[, ...)] | ONLY PASS THROUGH
```



#### 9.2. Cursor

* *DECLARE*, 

  ```
  DECLARE cursor_name [{SENSITIVE | INSENSITIVE | ASENSITIVE}]
  [[NO] SCROLL] CURSOR [{WITH | WITHOUT} HOLD]
     [{WITH | WITHOUT} RETURN]
  FOR select_statement
  [FOR {READ ONLY | UPDATE [OF column[, ...]]}]
  ```

* *OPEN*

* *FETCH*

  ```
  FETCH [ { NEXT | PRIOR | FIRST | LAST |
    { ABSOLUTE | RELATIVE  int } }
    FROM ] cursor_name
  [INTO variable1 [, ...] ]
  ```

* *CLOSE*

```
DECLARE employee_cursor CURSOR FOR
   SELECT au_lname, au_fname
   FROM pubs.dbo.authors
   WHERE lname LIKE 'K%'
OPEN employee_cursor
FETCH NEXT FROM employee_cursor
BEGIN
  FETCH NEXT FROM employee_cursor
END
CLOSE employee_cursor
```



#### 9.3. RETURN Statement

#### 9.4. SET Statement

#### 9.5. CALL Statement

```
CALL procedure_name([parameter[, ...]])
```

#### 9.6. Platform-Specific  extensions

##### 9.6.1. ORACLE

IF..ELSE        LOOP 

##### 9.6.2. IBM DB2

```
SELECT COUNT(*)
INTO cnt_CUST4_CF
from *table*
```

https://stackoverflow.com/questions/41225730/how-to-assign-value-in-stored-procedure-variable-when-executing-it

#####  9.6.3. [MySQL Stored Procedure]( https://dev.mysql.com/doc/refman/8.0/en/sql-compound-statements.html)

```
-- Declare variable to store output value from the stored procedure
DECLARE @storeParameter2_Value INT
EXEC SP_LIST_COLUMN_1 
    @Parameter1 = 1, 
    @Parameter2 = @storeParameter2_Value OUTPUT
-- Show the value of @Paramter2
SELECT @storeParameter2_Value AS [List of Paramter2]
```

https://medium.com/@yuvrendergill21/sql-stored-procedures-variables-parameters-outputs-62c653ebe0a0





Hi Clara

This is Donald Tang. My primary role in the last ten years has been Backend Developer, with around 20 percentage of the time being frontend related.

I prefer a Backend developer role with part frontend development responsibility.

Thank you, Clara!

Best Regards

Donald Tang





[Leetcode Test](https://leetcode.com/problems/average-selling-price/?envType=study-plan-v2&envId=top-sql-50)

Test 1251

```sql
# step 1
select p.product_id, p.price, u.units 
from prices p
left join UnitsSold u
on
    p.product_id = u.product_id
    and p.start_date <= u.purchase_date
    and p.end_date >= u.purchase_date

| product_id | price | units |
| ---------- | ----- | ----- |
| 1          | 5     | 100   |
| 1          | 20    | 15    |
| 2          | 15    | 200   |
| 2          | 30    | 30    |

# step 2
select 
    p.product_id as product_id, 
    round(sum(p.price*u.units)/sum(u.units), 2) as average_price  
from prices p
left join UnitsSold u
on
    p.product_id = u.product_id
    and p.start_date <= u.purchase_date
    and p.end_date >= u.purchase_date
group by 
    p.product_id;
Output: 
+------------+---------------+
| product_id | average_price |
+------------+---------------+
| 1          | 6.96          |
| 2          | 16.96         |
+------------+---------------+





# Write your MySQL query statement below
select  
        Students.student_id,
        Students.student_name , 
        Subjects.subject_name
from  Students
CROSS JOIN Subjects 

left join Examinations
on 
    Examinations.student_id = Students.student_id 
    and Examinations.subject_name  = Subjects.subject_name 
    
***************************************************************
select  
        Students.student_id,
        Students.student_name , 
        Subjects.subject_name,
        count(Examinations.student_id) as attended_exams

from  Students
CROSS JOIN Subjects 

left join Examinations
on 
    Examinations.student_id = Students.student_id 
    and Examinations.subject_name  = Subjects.subject_name 

group by Students.student_id, Subjects.subject_name
order by Students.student_id, Subjects.subject_name
```

