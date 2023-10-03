## Report and txt interface

Report generation and txt import and export. Use apache poi framework , jxls.

* 1.generate excel, txt file, stored in server hard disk. 
  * query list from db
  * use [free marker](https://freemarker.apache.org/docs/pgui_datamodel_basics.html) module to transfer object list to column and row in the excel

* 2.Then user can download, file transfer based on http protocol. content-type=multipart



### Fixed Length   

> derived from ancient tool JAR to conduct transfer between Fixed format txt and Object

batch fixed length data stored in txt file txt file. 

single fixed length data as request and response between host and ppr 

## System Monitoring

* server availability, **curl**  http 8080 to query server status, verify if response status is 200

* server  hardware: cpu, file disk, memory monitoring, shell script:  **vmstat**; **df**;
* server virtual memory;  Old space 
* integration with other system. Database db2;  jms mq; redis;

### Database backup; server restart, stop;



#### ibm db2 command

* db2 backup 

  ~~~sql
  db2 backup
  ~~~

* import csv file into db2

~~~sql
db2 "IMPORT from STP_cus_config.csv OF DEL insert into ECPH_CUS_CFG_TBL (CAT,ke1, ke2, ke3, ke4,ke5,ke6,status,val)"; 
~~~

* export csv file from db2, [export bash command](https://www.ibm.com/docs/en/db2/10.5?topic=commands-export)

```shell
db2 export to result4.csv of del modified by nochardel SELECT ke1, ke2, ke3 FROM ECPH_CUS_CFG_TBL limit 10; 

db2 "delete FROM ECPH_CUS_CFG_TBL where cat like 'ow.charge.amount'";

db2 "export to result5.csv of del modified by chardel''  SELECT CAT,ke1, ke2, ke3, ke4,ke5,ke6,status,val FROM ECPH_CUS_CFG_TBL where CAT LIKE 'STP.%' or cat like 'ow.%'";

db2 "export to result6.csv of del modified by chardel''  SELECT CAT,ke1, ke2, ke3, ke4,ke5,ke6,status,val FROM ECPH_CUS_CFG_TBL";

scp root@10.3.60.47:/root/donald/STP_cus_config.csv db2inst1@10.3.60.43:/home/db2inst1
```

### IBM MQ 

Script, Queue Manager

https://github.com/ibm-messaging/mq-jms-spring

https://developer.ibm.com/tutorials/mq-jms-application-development-with-spring-boot/

https://www.ibm.com/docs/en/ibm-mq/9.0?topic=mq-about

https://www.ibm.com/docs/en/ibm-mq/9.0?topic=queues-define-qlocal

runmqc:  firstly open script, then input and execute mq command.

### Redis

* Standalone

* Sentinel 哨兵 与server是不同线程
* Cluster

#### Client 

Jedis,  Lettuce

cache, messaging queue(based on Spring Integration, which is implementation of  [Enterprise Integration Pattern theory](https://www.enterpriseintegrationpatterns.com/)),

Topic, channel, Adapter

###  Security

**Spring-vault** ;   **trust-store**

encrypted Properties Loader, load systemeric and unsystemric property



### [Script](https://tldp.org/LDP/abs/html/index.html)

Shell script,  Operation-menu script    tar type install

**menu-operation.sh**

* shell job

* shell send email    mailx  command

  [define variable array](https://blog.csdn.net/qq_34160841/article/details/115431244)  

> 读取数组元素值的一般格式是：
>
> ${数组名[下标]}
>
> 例如： valuen=${array_name[n]}
>
> 使用 @ 符号可以获取数组中的所有元素，例如：
>
> echo ${array_name[@]}

### Spring Framework

JMS     connect with IBM MQ



JPA - hibernate    connect with DB2

google-hibernate-generic

https://github.com/vincentruan/hibernate-generic-dao

https://code.google.com/archive/p/hibernate-generic-dao/

### JNDI

Service namespace 

### Swagger

1. step 1,  define interface in YAML.
2. step 2, use Codegen tool to generate code: api, DTO, client  class. 
3. write logic implementation of restful api. Usually, bizDelegate to invoke service and dao to access database and other injected bean service.



###  