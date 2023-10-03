camt.056, camt.029:  

1.SUBMIT_OUTWARD_INVESTIGATION               investigation  -> processor
2.PAYMENT_PROCESS_PAYMENT_RESULT         processor      -> investigation 

MTn92/95/96/99:           

1.SUBMIT_OUTWARD_SWIFT_MT_MESSAGE       investigation  -> processor
2.PAYMENT_PROCESS_PAYMENT_RESULT           processor      -> investigation 



DB Table

table                                       entity                                   DTO                                           XML Message DTO

ECPH_INVE_DTL_TBL           InvestigationCase             InvestigationCaseDTO           FIToFIPaymentCancellationRequestDTO (CAMT.056)

​                                                                                                                                               ResolutionOfInvestigationDTO (CAMT.029) 



ECPH_MT_INVE_DTL_TBL    MTInvestigation               MTInvestigationDTO              MtN95DTO

​                                                                                                                                               MtN96DTO

​                                                                                                                                               MtN99DTO

ECPH_PAYMENT_TBL           Payment                            PaymentDTO                          FIToFICustomerCreditTransferDTO (pacs.008)

​                                                                                                                                              FinancialInstitutionCreditTransferDTO (pacs.009)

​                                                                                                                                              PaymentReturnDTO (pacs.004) 

​                                                                                                                                              FIToFIPaymentStatusReportDTO (pacs.002)   

ECPH_STTL_DTL_TBL          SettlementEntry

#### DB server

pprdbsd1   10.10.203.181

root / password

[db2常用操作命令](https://cloud.tencent.com/developer/article/1414071)

````shell
7、 连接到数据库 　
su db2inst1
#db2 connect to [dbname] user [username] using [password]
db2 connect to ecph3 user ecph using PaymentHub12345
db2 list tables for user


db2 truncate table ecph_payment_tbl immediate


## zip压缩文件包
zip -q -r html.zip /home/html
unzip -P password  路径/文件.zip  -d  ./service
cp -r   路径/文件   目标路径
## 输出最后10行内容，同时监视文件的改变，只要文件有一变化就显示出来。
tail -f  -n 100 filename
## 执行脚本文件
db2 -tvf scripts.sql

BIC            BankCodeIBMFormat     account
AGRIHKHXXXX      BSUIHKHHA 
                 SPDBCNSH             CURRENCY = CNY, bankIndicator= N
                 IRVTUSNYC
                 GIBAGBLD
                 GIBASKBB
                 HSBCHKHH
````





## Hibernate and Spring data

Manning <Java persistence in Hibernate and JPA> 2nd version

persistence in
Java, we’re normally talking about mapping and storing object instances in a database
using SQL.

## Different Types of SQL JOINs

Here are the different types of the JOINs in SQL:

- `(INNER) JOIN`: Returns records that have matching values in both tables
- `LEFT (OUTER) JOIN`: Returns all records from the left table, and the matched records from the right table
- `RIGHT (OUTER) JOIN`: Returns all records from the right table, and the matched records from the left table
- `FULL (OUTER) JOIN`: Returns all records when there is a match in either left or right table

![SQL INNER JOIN](https://www.w3schools.com/sql/img_innerjoin.gif) ![SQL LEFT JOIN](https://www.w3schools.com/sql/img_leftjoin.gif) 



![SQL RIGHT JOIN](https://www.w3schools.com/sql/img_rightjoin.gif) ![SQL FULL OUTER JOIN](https://www.w3schools.com/sql/img_fulljoin.gif)





## The SQL UNION Operator

The `UNION` operator is used to combine the result-set of two or more `SELECT` statements.

- Every `SELECT` statement within `UNION` must have the same number of columns
- The columns must also have similar data types
- The columns in every `SELECT` statement must also be in the same order



## The SQL CASE Expression

The `CASE` expression goes through conditions and returns a value when the first condition is met (like an if-then-else statement). So, once a condition is true, it will stop reading and return the result. If no conditions are true, it returns the value in the `ELSE` clause.

If there is no `ELSE` part and no conditions are true, it returns NULL.

## CASE Syntax

CASE
  WHEN *condition1* THEN *result1*
  WHEN *condition2* THEN *result2*
  WHEN *conditionN* THEN *resultN*
  ELSE *result*
END;

## SQL Constraints

SQL constraints are used to specify rules for the data in a table.

Constraints are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.

Constraints can be column level or table level. Column level constraints apply to a column, and table level constraints apply to the whole table.

The following constraints are commonly used in SQL:

- `NOT NULL` - Ensures that a column cannot have a NULL value
- `UNIQUE` - Ensures that all values in a column are different
- `PRIMARY KEY` - A combination of a `NOT NULL` and `UNIQUE`. Uniquely identifies each row in a table
- `FOREIGN KEY` - Prevents actions that would destroy links between tables
- `CHECK` - Ensures that the values in a column satisfies a specific condition
- `DEFAULT` - Sets a default value for a column if no value is specified
- `CREATE INDEX` - Used to create and retrieve data from the database very quickly

## SQL Data Types

Each column in a database table is required to have a name and a data type.

An SQL developer must decide what type of data that will be stored inside each column when creating a table. The data type is a guideline for SQL to understand what type of data is expected inside of each column, and it also identifies how SQL will interact with the stored data.

https://www.w3schools.com/sql/sql_datatypes.asp

## MySQL Data Types (Version 8.0)

In MySQL there are three main data types: string, numeric, and date and time.

### String Data Types

| Data type                   | Description                                                  |
| :-------------------------- | :----------------------------------------------------------- |
| CHAR(size)                  | A FIXED length string (can contain letters, numbers, and special characters). The *size* parameter specifies the column length in characters - can be from 0 to 255. Default is 1 |
| VARCHAR(size)               | A VARIABLE length string (can contain letters, numbers, and special characters). The *size* parameter specifies the maximum string length in characters - can be from 0 to 65535 |
| BINARY(size)                | Equal to CHAR(), but stores binary byte strings. The *size* parameter specifies the column length in bytes. Default is 1 |
| VARBINARY(size)             | Equal to VARCHAR(), but stores binary byte strings. The *size* parameter specifies the maximum column length in bytes. |
| TINYBLOB                    | For BLOBs (Binary Large Objects). Max length: 255 bytes      |
| TINYTEXT                    | Holds a string with a maximum length of 255 characters       |
| TEXT(size)                  | Holds a string with a maximum length of 65,535 bytes         |
| BLOB(size)                  | For BLOBs (Binary Large Objects). Holds up to 65,535 bytes of data |
| MEDIUMTEXT                  | Holds a string with a maximum length of 16,777,215 characters |
| MEDIUMBLOB                  | For BLOBs (Binary Large Objects). Holds up to 16,777,215 bytes of data |
| LONGTEXT                    | Holds a string with a maximum length of 4,294,967,295 characters |
| LONGBLOB                    | For BLOBs (Binary Large Objects). Holds up to 4,294,967,295 bytes of data |
| ENUM(val1, val2, val3, ...) | A string object that can have only one value, chosen from a list of possible values. You can list up to 65535 values in an ENUM list. If a value is inserted that is not in the list, a blank value will be inserted. The values are sorted in the order you enter them |
| SET(val1, val2, val3, ...)  | A string object that can have 0 or more values, chosen from a list of possible values. You can list up to 64 values in a SET list |

### Numeric Data Types

| Data type                     | Description                                                  |
| :---------------------------- | :----------------------------------------------------------- |
| BIT(*size*)                   | A bit-value type. The number of bits per value is specified in *size*. The *size* parameter can hold a value from 1 to 64. The default value for *size* is 1. |
| TINYINT(*size*)               | A very small integer. Signed range is from -128 to 127. Unsigned range is from 0 to 255. The *size* parameter specifies the maximum display width (which is 255) |
| BOOL                          | Zero is considered as false, nonzero values are considered as true. |
| BOOLEAN                       | Equal to BOOL                                                |
| SMALLINT(*size*)              | A small integer. Signed range is from -32768 to 32767. Unsigned range is from 0 to 65535. The *size* parameter specifies the maximum display width (which is 255) |
| MEDIUMINT(*size*)             | A medium integer. Signed range is from -8388608 to 8388607. Unsigned range is from 0 to 16777215. The *size* parameter specifies the maximum display width (which is 255) |
| INT(*size*)                   | A medium integer. Signed range is from -2147483648 to 2147483647. Unsigned range is from 0 to 4294967295. The *size* parameter specifies the maximum display width (which is 255) |
| INTEGER(*size*)               | Equal to INT(size)                                           |
| BIGINT(*size*)                | A large integer. Signed range is from -9223372036854775808 to 9223372036854775807. Unsigned range is from 0 to 18446744073709551615. The *size* parameter specifies the maximum display width (which is 255) |
| FLOAT(*size*, *d*)            | A floating point number. The total number of digits is specified in *size*. The number of digits after the decimal point is specified in the *d* parameter. This syntax is deprecated in MySQL 8.0.17, and it will be removed in future MySQL versions |
| FLOAT(*p*)                    | A floating point number. MySQL uses the *p* value to determine whether to use FLOAT or DOUBLE for the resulting data type. If *p* is from 0 to 24, the data type becomes FLOAT(). If *p* is from 25 to 53, the data type becomes DOUBLE() |
| DOUBLE(*size*, *d*)           | A normal-size floating point number. The total number of digits is specified in *size*. The number of digits after the decimal point is specified in the *d* parameter |
| DOUBLE PRECISION(*size*, *d*) |                                                              |
| DECIMAL(*size*, *d*)          | An exact fixed-point number. The total number of digits is specified in *size*. The number of digits after the decimal point is specified in the *d* parameter. The maximum number for *size* is 65. The maximum number for *d* is 30. The default value for *size* is 10. The default value for *d* is 0. |
| DEC(*size*, *d*)              | Equal to DECIMAL(size,d)                                     |

**Note:** All the numeric data types may have an extra option: UNSIGNED or ZEROFILL. If you add the UNSIGNED option, MySQL disallows negative values for the column. If you add the ZEROFILL option, MySQL automatically also adds the UNSIGNED attribute to the column.

### Date and Time Data Types

| Data type        | Description                                                  |
| :--------------- | :----------------------------------------------------------- |
| DATE             | A date. Format: YYYY-MM-DD. The supported range is from '1000-01-01' to '9999-12-31' |
| DATETIME(*fsp*)  | A date and time combination. Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1000-01-01 00:00:00' to '9999-12-31 23:59:59'. Adding DEFAULT and ON UPDATE in the column definition to get automatic initialization and updating to the current date and time |
| TIMESTAMP(*fsp*) | A timestamp. TIMESTAMP values are stored as the number of seconds since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1970-01-01 00:00:01' UTC to '2038-01-09 03:14:07' UTC. Automatic initialization and updating to the current date and time can be specified using DEFAULT CURRENT_TIMESTAMP and ON UPDATE CURRENT_TIMESTAMP in the column definition |
| TIME(*fsp*)      | A time. Format: hh:mm:ss. The supported range is from '-838:59:59' to '838:59:59' |
| YEAR             | A year in four-digit format. Values allowed in four-digit format: 1901 to 2155, and 0000. MySQL 8.0 does not support year in two-digit format. |

# [DB2](https://www.ibm.com/docs/en/db2-for-zos/12?topic=columns-data-types)

- **[String data types](https://www.ibm.com/docs/en/SSEPEK_12.0.0/intro/src/tpc/db2z_stringdatatypes.html)**
  Db2 supports several types of string data: character strings, graphic strings, and binary strings.
- **[Numeric data types](https://www.ibm.com/docs/en/SSEPEK_12.0.0/intro/src/tpc/db2z_numericdatatypes.html)**
  Db2 supports several types of numeric data types, each of which has its own characteristics.
- **[Date, time, and timestamp data types](https://www.ibm.com/docs/en/SSEPEK_12.0.0/intro/src/tpc/db2z_datetimetimestamp.html)**
  Although storing dates and times as numeric values is possible, using datetime data types is recommended. The datetime data types are DATE, TIME, and TIMESTAMP.
- **[XML data type](https://www.ibm.com/docs/en/SSEPEK_12.0.0/intro/src/tpc/db2z_xmldatatype.html)**
  The XML data type is used to define columns of a table that store XML values. This pureXML® data type provides the ability to store well-formed XML documents in a database.
- **[Large object data types](https://www.ibm.com/docs/en/SSEPEK_12.0.0/intro/src/tpc/db2z_largeobjectdatatypes.html)**
  You can use large object data types to store audio, video, images, and other files that are larger than 32 KB.
- **[ROWID data type](https://www.ibm.com/docs/en/SSEPEK_12.0.0/intro/src/tpc/db2z_rowiddatatype.html)**
  You use the ROWID data type to uniquely identify rows in a Db2 subsystem.
- **[Distinct types](https://www.ibm.com/docs/en/SSEPEK_12.0.0/intro/src/tpc/db2z_distincttypes.html)**
  A distinct type is a user-defined data type that is based on existing built-in Db2 data types.



摘要:db2- 隨手筆記

-- 若*號後面要加上別的欄位，則Table 需要別名 ------
select A.*,DATE(colname) from tablename A



-- 去除空白格 ------
Strip(xxx)
LTRIM()、RTRIM() => 從 CHAR、VARCHAR、GRAPHIC 或者 VARGRAPHIC中去掉左側或右側的空格


-- 大小寫轉換 ------
LCASE()、LOWER() => 返回定長、變長字符串的小寫形式
UCASE()、UPPER() => 返回定長、變長字符串的大寫形式


-- DataType Convert ------
int(xxx) result：轉換成整數型態
char(xxx) result：轉換成字元型態


-- string treatment ------
strip(xxx) result：相當於 MS SQL 的 Trim


-- null判斷 ------
column is not null
column is null


-- 相當 MS SQL的 IsNull Function ------
COALESCE(PROD_CAT,'')
COALESCE(PROD_CAT,0)


-- 相當 MS SQL的 charindex Function ------
locate('E','ABCDEF') => 5


-- Year、Month、Day function ----
select * from TB where year(REC_DT)=2010 and month(REC_DT)=11 and day(REC_DT)=25 and hour(REC_DT)=14 and minute(REC_DT)=25 and second(REC_DT)=32 with ur;


-- ms sql substring => db2 substr ----
select substr(ColumnName,StartIndex,length) from relation_info with ur;
ps:StartIndex：從1開始


-- 撈前10筆資料 ----
Select * from TableName fetch first 10 rows only with ur;


-- 列出資料庫內所有 Procedures、Tables、Views、Functions ----
select * from SYSCAT.procedures order by procschema with ur;
select * from SYSCAT.tables order by tabschema with ur;
select * from SYSCAT.views order by viewschema with ur;
select * from SYSCAT.functions order by funcschema with ur;



## JSON Libraries

jackson2, gson, fastJson

关于jackson和gson的比较文章有很多，stackoverflow上自行搜索，下面仅推荐几篇blog：

jackson vs gson
JSON in Java
the ultimate json library json-simple vs gson vs jackson vs json

在功能特性支持、稳定性、可扩展性、易用性以及社区活跃度上 jackson 和 gson 差不多，入门教程可以分别参考baeldung jackson系列 以及 baeldung gson系列。但是jackson有更多现成的类库兼容支持例如jackson-datatype-commons-lang3，以及更丰富的输出数据格式支持例如jackson-dataformat-yaml，而且spring框架默认使用jackson，因此最终我选择使用jackson

深度对比Jackson和Fastjson，最终我还是选择了...
https://blog.51cto.com/u_13260163/3062053