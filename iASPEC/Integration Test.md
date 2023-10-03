## 1. Request from SWIFT INTERFACE TESTING

测MQ: SWSG. IBM MQ listener

## 2. Request to HOST INTERFACE TESTING

 Receive & Sending of Message from HOST or Other System through MQ

2.1 **Receive of Message from HOST**

synchronize and save data from HOST

2.2 **Sending of Message to HOST**

PPZZ

通过api触发，调用Handler，去send  message through queue to Host, 

STSU

WMSG

AMLC

AMLR

AMSG

QSTS

2.3 **Sending of Message to FRX**

EXRQ

EXPU

2.4 **Sending of Message to SLS System**

OBPU

QOBD

2.5 **Receive of Message from BIF System**





## 4. FUNCTIONAL TESTING – As Intermediary Bank



Task:

### 1. database data

* custom config table: ECPH_CUS_CFG_TBL

* ECPH_PAYMENT_TBL

* ECPH_ADVERSE_WEATHER_HIST_TBL

* ECPH_INVE_DTL_TBL

  script.sql 放在qnap 目录

### 2. api interface

### 3. MQ interface





1.测试与IBM MQ的连通性，先用mock数据测，判断是否能建立连接connection，没有timeout

再用一个个MQ真实测

2.用json数据 + eventType 测handler， 根据validationResults + paymentDTO, 判断是否handler逻辑处理完成

3.端到端集成测试，从swift发出报文 -> HOST -> payment hub( processor ) -> rtmg -> [payment -> processor handler]{1...} -> invoke IBM MQ to HOST 

* today's task:   set different tools for different event Type,  将event type 串联起来
* Redis Internal Msg
*  Queue: <code>payment-processor-processPayment-queue</code>   -> processor  ->  Queue: <code>payment-processPayment-queue</code> 
*  （eventType:  PAYMENT_PROCESSOR_IW_PAYMENT_RECEIVED ->  PAYMENT_PROCESS_PAYMENT_RESULT  -> PAYMENT_PROCESSOR_OW_PAYMENT_CREATED

## Processing Tool Map

| event Type                                        | processing Tools                    | Action Type                  |
| ------------------------------------------------- | ----------------------------------- | ---------------------------- |
| PAYMENT_PROCESSOR_IW_PAYMENT_RECEIVED             | invoke payment [CREATE_OW_PAYMENT]  | CREATE_OW_PAYMENT            |
| RERUN_STP                                         | invoke payment [CREATE_OW_PAYMENT]  | CREATE_OW_PAYMENT            |
| PAYMENT_CREATE_OW_RETURN (payment.getType=RETURN) | no tool so far, manual process      | CREATE_OW_PAYMENT            |
|                                                   |                                     |                              |
| PAYMENT_PROCESSOR_OW_PAYMENT_CREATED              | invoke payment: batch1 -> batch2    | SUBMIT_to_SWITFT             |
| PAYMENT_PROCESSOR_OW_PAYMENT_SUBMIT_TO_SWIFT      | processUpdPaymentProcessingTools    | Process_update               |
|                                                   |                                     |                              |
| PAYMENT_PROCESSOR_OW_RETURN_CONFIRMED             | no tool, waiting for rerun          |                              |
| PAYMENT_PROCESSOR_OW_RETURN_SUBMIT_TO_SWIFT       | no tool, save updated payment in db |                              |
|                                                   |                                     |                              |
| PAYMENT_PROCESSOR_OUTWARD_CANCELLATION_RECEIVED   | no tool                             |                              |
| PAYMENT_PROCESSOR_OUTWARD_CANCELLATION_APPROVED   | no tool,                            | SUBMIT_PAYMENT_STATUS_REPORT |



settlementAmount

original number                                                                        78675

Level 1                         50 HKD                   6.25                       78668.75

Level 2                        100 HKD                   12.5                      78662.50

Level 3                        180 HKD                   22.5                      78652.50

Level 4                        220 HKD                    27.5        			  78647.50

Level 5                        270 HKD                    33.75        			78641.25



####  ftp server:

root / iaspec  @fps-test.fps.dev:22

/data/www/html/payment-hub/.scb/



####  app  server:

App 1

10.10.203.182  :  pprapsd1     

root / password

10.10.203.183  :  pprapsd2     

root / password

tomcat目录：/opt/iaspec/payment-hub

上传文件目录：/opt/iaspec/payment-hub or ~  



####  work station in 13/F SCB

scb / 1234abCD    ~~Password1@~~

admin    http://10.10.203.182:8080/payment-console

Super account: super   password: Ppr2022

Test account: test1, test2, test3, test4    password: Ppr2022

#### DB server

pprdbsd1   10.10.203.181

root / password

[db2常用操作命令](https://cloud.tencent.com/developer/article/1414071)

````shell
7、 连接到数据库 　
su db2inst1
#db2 connect to [dbname] user [username] using [password]
db2 connect to ecph user ecph using PaymentHub12345
db2 list tables for user

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



1.status update

outstanding_for_return_reject    true hit AMLR 001 return code

outstanding_for_review    other not passed  

all passed     pending_transaction
