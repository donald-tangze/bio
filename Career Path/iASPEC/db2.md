# DB2 database

[IBM Cloud official websit](https://cloud.ibm.com/services/dashdb-for-transactions/crn%3Av1%3Abluemix%3Apublic%3Adashdb-for-transactions%3Aeu-gb%3Aa%2Ff03932b06dc1452896fa172443469bfa%3A44059dca-6de2-4039-8097-c7a1a420cf51%3A%3A?paneId=manage)



## 1. DB2 Installation 

### 1.1.Install docker with db2 database service

```shell
docker pull icr.io/db2_community/db2
```

[Link ](https://www.ibm.com/docs/en/db2/11.5?topic=system-macos)

htt ps://www.ibm.com/blog/announcement/ibm-db2-developer-community-edition/

https://www.idug.org/blogs/john-maenpaa1/2020/11/04/installing-db2-on-macos-using-docker

### 1.2.Install db2 on cloud through IBM Cloud

* apply lite(free) account and db2 resources in London and Dallas Cloud Region 

* [Resource Management](https://bs2ipcul0apon0jufi80lite.db2.cloud.ibm.com/crn%3Av1%3Abluemix%3Apublic%3Adashdb-for-transactions%3Aeu-gb%3Aa%2Ff03932b06dc1452896fa172443469bfa%3A44059dca-6de2-4039-8097-c7a1a420cf51%3A%3A/console/index.html#connection/overview)

```shell
db2cli validate -dsn dashdb -connect -user crj31643 -passwd cG6PjJy4NBnHf90b
#To start CLPPlus with a connection to a Db2 on Cloud database that uses the entries in the db2dsdriver.cfg file, run the following command:
#Linux environments:
#Example 1
clpplus -nw crj31643/cG6PjJy4NBnHf90b@dashdb

#Example 2
#Start CLPPlus with your user ID and the alias that you created in the db2dsdriver.cfg file and run the script in one step:
clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql
```



### 2. DB2 Training Course 

[Coursera](https://www.coursera.org/learn/introduction-to-relational-databases/lecture/fLjW2/db2)

### 3. Connect to DB2 on Cloud 

####  3.1.through Cli with SSL

* install IBM Data Server Driver Package (Mac OS) [Link](https://epwt-www.mybluemix.net/software/support/trial/cst/programwebsite.wss?siteId=853&h=null&tabId=)

  ​	Driver in Mac OS installation directory： /Applications/dsdriver/bin

* Use Tool clpplus: [Link](https://cloud.ibm.com/docs/Db2onCloud?topic=Db2onCloud-connect_ibm#clpplus ) 

![image-20230821114939184](https://p.ipic.vip/vkvtr2.png)

![image-20230821115244704](https://p.ipic.vip/pwjplx.png)



####  3.2.through Database Client: DBeaver









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