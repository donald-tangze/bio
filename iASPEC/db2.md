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