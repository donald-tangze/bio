*Direct Return Instructed Amt, Settlement Amt.*

 SRCREF : PPSS2305130019  COMPCD : SCBK APPLID : PPR TXNTYPE : 1 OTHREF : TEST2305130010E                      
      DFLBCD :      DUEDATE : 00000000 CONTRYI :   ADJPDI : N ADJTXI : N ONLUPD : N                    
 DMBRCD ACCTCD  HBRCD  ORGDEPT SEQNO ORGDATE  TXNCD   DR/CR CUR/AMT  PARTICULARS                          
 28   2715669    28  PP   000051 20230515 CR HKD    129860.00  SCBKCNSZ                 OVERSEAS BR C/A    
 28   2404031    28  PP   000052 20230513 CR HKD    129810.00                      R & D PAYABLE-A    
 28   2715669    28  PP   000053 20230513 DR HKD    129810.00  SCBKCNSZ                 OVERSEAS BR C/A    
 28   2404031    28  PP   000054 20230513 DR HKD    129810.00                      R & D PAYABLE-A    
 28   4102021    28  PP   000055 20230513 CR HKD      150.00                      COMMISSON REC-REM   



 SRCREF : PPSS2305130028  COMPCD : SCBK APPLID : PPR TXNTYPE : 1 OTHREF : MAX-008-051302EI                     
      DFLBCD :      DUEDATE : 00000000 CONTRYI :   ADJPDI : N ADJTXI : N ONLUPD : N                    
 DMBRCD ACCTCD  HBRCD  ORGDEPT SEQNO ORGDATE  TXNCD   DR/CR CUR/AMT  PARTICULARS                          
 28   4102021    28  PP   000079 20230513 CR HKD      50.00                      COMMISSON REC-REM   
 28   1914661    28  PP   000080 20230513 DR CNY      42.25  SCBKCNSZ                 DUE FR OS BR-REM  





## 20230427

* in create transaction page, allow Debtor Agent to edit.  -- Completed
* SIT#76 check credit amount and debit amount of General Ledger Entry File are equal
  * here GENERAL_LEDGER((short) 10),





###  20230317 Tasks

* Update Host interface  (deadline Monday)

  * WMSG  and AMSG request added new field "Message channel (incoming)"

* split OBPU and settlement ledge record.

* cove payment test:  fields.

  

### 20230320

* set redsi hash data expired time and delete hash key value through spring-data-redis, Hash Data {uuid : {messageType : Swift MUR}}



### 20230321

* set redsi hash data expired time and delete hash key value through spring-data-redis, Hash Data {uuid : {messageType : Swift MUR}}



###  CERTIFICATION

Java  Certification

```
1. SSL CERT: Java  Certification
D:\donald\idea\common\ecph-commons\ecph-core-generic\src\main\java\com\iaspec\ecph\util\EcphSSLSocketFactory.java
IBM MQ connection Factory

2. UserCredentialsConnectionFactoryAdapter
Spring.jms.connection factory
there are user and password 


```



## Git merge

![image-20230224120723126](C:\Users\donald\AppData\Roaming\Typora\typora-user-images\image-20230224120723126.png)

```
payment-hub        .gitignore

/test/
/payment-processor/ecph-payment-processor-core/src/test/*
```

![image-20230224120954487](C:\Users\donald\AppData\Roaming\Typora\typora-user-images\image-20230224120954487.png)

 

Rui sen

![image-20230224151815549](D:\donald\document\admin_service.png)

![image-20230224145821474](C:\Users\donald\AppData\Roaming\Typora\typora-user-images\image-20230224145821474.png)

##  DEMO-20230213

### Charge for reject

* Debit instructing account(Vostro account)  and Credit SCB account should be present as a pair.
* Check Type, Account, status fields in Database should be correct.

###  Cove payment

* When Release to swift,  keep status of pacs.009.cov and pacs.008 are consistent and change into Submiting together
* Copy 008 internal settlement Method into Cove payment



Direct Return



Outward Return batch 2, add approval process Direct Return

###  Task 0206 Meeting

camt.056  cancellation

XML message generate. 

camx.



#### deployment and version management. 

release log:  include bugfix and enhancement. 



#### TASK 0116-0120

1. Implement the exception logic handling on incoming MT Query Message     Complete
2. adjustment of Host interface OBPU and STSU,                                                     Complete
3. XBFPS:  add a handler for EVENT: CheckInwardAMLResult4XbfpsHandler and Test     Complete
4. Add interface: NotifyFpsReceivedHandler, notify fps that ppr that have received cross border message. 
   Additional Data key: xbfps_id  +  OnHoldReprocess:  sendSupplementaryInfo          pending test
   only allowed to be executed successfully once, then skip.                             
5. supplement handler logic of Reject Message of pacs.002, Clarify Development requirement before test and execute Integration Test on Dev env                                                              Complete
6. supplement  handler logic of cancellation camt.056 and Investigation camt.029，Clarify Development requirement before test  and execute Integration Test on Dev env                 Complete

6. deploy app into SIT env and test MTn95/n96/n99 all saved, partly success and partly failed test passed.
7. check Authentication Key of BSPPBNK field:    , and check bank bic forbidden message type.(not allowed)

```
//Implement the exception logic handling on incoming MT Query Message

error log content:
ErrorException
Raw Message
new line
ErrorException
Raw Message
```



#### TASK 0117

pacs.009 不发outward remittance message.      status: pre-processing

(1) ow

(2) instructed bank = creditor bank

(3) settlement method = "INGA"     vostro account

####  TASK  11.15

JKS key: store encrypted password for security







####  TASK  11.01

24,25,28 DW

if it's  009.adv, then can acknowledge

if it's 009.cov, then can acknowledge

as long as not payee remittance, then allow to create transaction.

####  Task 10.28

1.Release to Swift AMSG

update status to "completed",  set result as "NOT_PASSED".

2.check swift status

PPSS2210250069        E = Syntax error detected by MERVA           Syntax error

PPSS2210260045        E = Syntax error detected by MERVA           Syntax error

SHUT_DOWN  status

### Task 10.27

summarize:

#### 1.concurrency: receive remittance and rerun-STP happen at the same time.

issue list: 468;  478; 484; 491;

#### 2. key conflict, lead to payment service failed to save processor results in database.

issue list:  429; 471; 479; 481; 492;

### 10.24

* After user approval requirement, would trigger an event: ACCEPT_PAYMENT to release Swift message to Host. Then what should do if release failed?  Answer is return status to EDITING

####  SHUT down status:

```
JMS  CachingConnectionFactory
- initConnection
- resetConnection
```

```
Redis jedisConnectionFactory
```

auto-delete job daily need to delete both  those pre-processing transaction and approval requirement record.



shutdown status = true, 

remove listener from topic.

#### 10.20 Task

* 1. bic

  * 1.1  getIbmBankCodeBy11bic
  * 1.2  getAccountByIbmBankCode

* 2. bic.substring(0,8) + XXX

  * 2.1 getIbmBankCodeBy11bic
  * 2.2  getAccountByIbmBankCode

* 3. for each  bic.substring(0,8) + [0,9]{3}    List<> retrieveIBMBankCodeListByBic

  * 3.1 getIbmBankCodeList   List<String>
  * 3.2 for each getAccountByIbmBankCode



if 11-digit, end-XXX,   Run 1 + 3

if 11-digit, not end-XXX, Run 1+2+3

if 8-digit, Run 2+3



* getIbmBankCodeListBybic.substring(0,8)   List<String>

* 1. bic         ibmcode + bic

  * 1.2  getAccountByIbmBankCode

* 2. bic.substring(0,8) + XXX    ibmcode + bic.substring(0,8) + XXX

  * 2.2  getAccountByIbmBankCode

* 3. for each  bic.substring(0,8) + [0,9]{3}    List<> retrieveIBMBankCodeListByBic

  * 3.2 for each getAccountByIbmBankCode

####  10.19 Task

issue #384

1.

Timer job, Check shutdownStatus value from properties or database every 5 seconds, verify if it's equal 1.

shutdownStatus == "1",  

1. HostMessageListener  connection with IBM MQ for host   =  stop.   

2. PaymentProcessorMessageRouter listener with Redis for other components  =  stop. 

   

   #346

   

   issue#149     fix

   issue#362     fix

###  10.17 Task

code review:   handling status,  pre-requisity:   received    



### 10.15 Task

Avoid  Outstanding ->  PENDING_STP

##### 1. adverse weather Handler,

* failed:   suspended   ->  pending_stp          stop
* succeed:  

#####  2. payeebank   verify criteria:  

* for pacs.008, see if creditor is SCBK
* for pacs.009, see if creditor as agent is SCBK

For payee bank remittance,  set status as Outstanding_for_review

#### 1014 Task

save swift status into payment custom5. 

handler result is "not_passed",  set handling_status to complete.

####  1013Task

* QSTS  Return negatively activated, modify outward payment handling status to editing.

  

1. verify show charge info and exchange info

   

2. auto-retry  10 times.  set AML check

   > if manual try, set 

3. modify charge,  instructing agent 11 digit



handling error,   error code , error description  into custom5

<STATUS>|<Error Code>|<Error Descriptions>|<Error Code>|<Error Descriptions>

Example, if Exception encountered:

EXCEPTION_PENDING|AMSG-9903|Host Unexpected System Error

Example, if ALL Exception issue has been resolved

EXCEPTION_CLEAR|AMSG-9903|Host Unexpected System Error

null

1.009  (creditor bic = scbkhkhh)  --> outstanding for review  +  payee bank  normal 

2.009  (creditor bic != scbkhkhh)  -->  intermediary, continue 

3.009  (creditor  isn't bic code)    -->   intermediary + outstanding for review     normal 

previous three rules are all apply to pacs.009cov. 



4.009 adv  (whatever creditor bic is)   --  all terminate, outstanding for review



UAT #issue 25,188.  test data can pass into ui



####  10-10 Task

when batch 1 passed all handlers, update outward transaction status to pre_processing

#### 10-08 Task

Fix issues

* issue#292  ready for deployment
* issue#285  #289    
* #282   charge
*  246 exchangeInfo = null
* 94   settlement account





* input settlement merge, test

#####  topic: outward transaction message type: 008  cove

* UAT#266

need to check  authenticated key named "SWFTAUTH" by swfit address (instructed agent bic code) in BSPPRWF custom config table.  

user input cove as settlement, 



* UAT#270   

Responsibility  of BankRelatedAccountHandler:   cove settlement method,  check  after  user input reimbursement agent as instructing reimbursement agent,

####  Task1007:

* check vostro account balance: use inward transaction Vostro bank account

* settlement Status: 
  * SettlementAndbalanceMQHandler passed, set to settled
  * BankRelatedAccountHandler  failed,  set to undetermined
* acknowledge function
* Determine outward Charge Bearer, Settlement Method



Task1005:

SIT issue:   #29 yaml  remittance update



user input charge bearer

user input charge info

####  Task1003:

SIT issue:   #29 yaml  remittance update

UAT issue: 

* check if save processing day in database   -- Yes



#### Task1001:

~~issue 199 duplicate with 219~~

> Test, 引申未解决，228

issue 217 duplicate with 145 and 222  BankRelatedAccountHandler 

> Test, alerted message

~~issue 219 CreditorAndDebtorHandler  add check on underlying customer credit info of pacs.009.cov~~

~~issue 221, add a new UpdateReqStatusHandler~~

~~issue 222, For pacs.008 [COVE], Debit a Nostro Account in inward settlement need manual handle.  BankRelatedAccountHandler~~ 

> test: 引申问题，DetermineHandlingStatus, npe and  QOBD insufficient balance

~~UAT issue 223  stop STP when encounter with  Related Business Application Header~~

~~<u>UAT   issue 224  CreditorAndDebtorHandler  add all fields of Postal address</u>~~

> Test, 未解决228 fix if-else order

SIT issue:   #29 yaml  remittance update

UAT issue 

####  TASK, set  processingDate of inward remittance as today by inward status

inward status                     custom2    format:  YYYY/MM/DD

suspended                          null                  processor

other status                        today

user  create  transaction  today               payment service

#### Task 0928: 

Settlement, outward need a verification handler,  when user input inward and outward settlement account and settlement method, verify if these account and method are valid.

####  Task: 0927 SIT issue #29

####  BankRelatedAccountHandler

Nostro/Vostro  Account query

* get IBM Bank Code
* get specified account by IBM Bank Code, currency, nostro/vostro flag and account type 
* read file from disk into database,  now the same swift BIC code has two IBM Bank code(8 bit/ 9 bit)
* for pacs.008, stop when debit a nostro account in inward process  
* for pacs.009 or pacs.009.cov, stop when credit a vostro account in outward process

#### DetermineOwSettleMethodHandler

for pacs.009 or pacs.009.cov, stop when credit a vostro account in outward process

vostro have higher priority than nostro account.

#### Task: 0926

Business Application Header, related  != null, must stop STP

#### Task: 0923

##### issue#113 Settlement method "COVE"

> cover, instructed agent be reimbursed by third-party.  priority sequence:
>
> Third Reimbursement Agent
>
> Instructed Reimbursement Agent
>
> Instructing Reimbursement Agent

##### issue#145  Additional STP validation of pacs.009 & pacs.009.cov

settlement Method

CreditorAndDebitorInfoSelfHandler



280，281



####  Part1: pacs.008 

keep same with our code implement



#### Part2: pacs.008[COVE] + pacs.009.cov

when pacs.008 has COV settlement method, check if  settlement method = INDA and NOSTRO account exist in DB by reimbursement agent bic.

* if settlement Method = "INDA", set result = NOT_PASSED and handling_status = "outstanding for review"
* if settlement Method = "INGA" and don't exist NOSTRO account, set result = NOT_PASSED and handling_status = "outstanding for review"
* if settlement Method = "INGA" and exist NOSTRO account, check if statement received, 
  * if inward passed all handlers, then begin new outward transaction process as usual
  * if don't passed handlers, set result = NOT_PASSED

Responsibility of inward BankRelatedAccountHandler.

#### Part3: pacs.009/ pacs.009.COV

##### inward process

do settlement as usual.   Responsibility of inward BankRelatedAccountHandler and SettlementAndBalanceHandler

##### outward process

find if next instructed  agent's NOSTRO account exist,

* if exist, set ow settlement Method = "INDA" and continue outward transaction process,  outward message type keep same as inward message;
* if don't exist, set result = NOT_PASSED, and handling_status = "outstanding for review", won't create outward transaction

Responsibility of inward DetermineOutwardMethodHandler





 #### issue#121 Debtor Id

#### issue, add version to verify isCurrentHandlerPassed

add a new redis key:   {paymentId + handlerName + version : passed}

```
when update version, need redo, except below only one
<ref bean="effectReqStatusSTSUMQHandler" />  

```



####  0923: user input charge

ChargeAmountApiHandler

shareBearer = "CRDT" & "SHAR", chargeInfo exist SCBKHKHH, don't do charge deduct and exchange compute.

get chargeAdditionData, and save in exchangeInfo for EXPU interface

### 0920 Task: user input Settlement --- issue#76

```java
InternalSettlementDetailDTO 
        private InternalSettlementMethod settlementMethod;   // INDA or INGA
        private LocalDate settlementDate;
        private String bankCode; // bank code in IBM format
        private String accountType; // single character account type
        private String currency;
        private BigDecimal amount;
        private String sundryReference;
```

![inputSettlement](C:\Users\donald\Desktop\ecph_sit\inputSettlement.jpg)

##### 1. inward process

* put [system queried] instructing Bank Related Account info into payment additional data. include IBMBankCode, account No, currency etc.        Resoponsibility of inward BankRelatedAccountHandler

  ```json
  [system queried] instructing Bank Related Account info
  BSPPACT=
  {recordType=1, 
  bankCodeInIBMFormat=SCBKGBLD, 
  currency=GBP, 
  bankIndicator=N, 
  accountType=A, 
  accountNo=62-82-01403-6, 
  accountID=6282014036, 
  lastActiveDate=60939100800000, 
  accountStatus=N}
  ```

* put [system queried] instructed agent account info into payment additional data.   Resoponsibility of DetermineOwSettleMethodApiHandler

##### 2. outward process

verify if there is key = INTERNAL_SETTLEMENT_DETAILS exist in additional data. Now we have two pieces of  data to choose.   (INTERNAL_SETTLEMENT_DETAILS and SYSTEM_QUERY_RESULT)

Resoponsibility of **UpdateBankPositionOBPUMQHandler**

* If yes, use input account firstly,  key = INTERNAL_SETTLEMENT_DETAILS.
* If no, use system query result firstly,  SYSTEM_QUERY_RESULT   that's bank related account from database,  that is to say,  additional data of step.1.



##### 3. Effected area and code 

* OBPU,  when generateRequest, movenmentDetails has arguments:

  Bank Code in IBM Format, 

  Nostro / Vostro Bank Indicator, 

  Bank A/C Type Indicator, 

  Currency,  

  account Type



* ledger record: General Ledger Record;  DebitorCreditorLedgerRecord

  Bank Code in IBM Format, 

  account No

  nostroVostroBankIndicator

#### Task:  19/09/2022

UpdateBankPositionOBPUMQHandler:  when in inward process, might execute once every day.

```
    protected String constructJobKey(PaymentDTO payment) {
        return getName() + payment.getId() + LocalDate.now();
    }
```



futureValueDayHandler： even this handler does not passed, other handler might continue executing

```
    protected boolean terminate(String eventType, PaymentDTO payment, Map<String, Object> options) {
        return false;
    }
    
    status is TransactionHandlingStatus.SUSPENDED
```



X:  Foreign exchange



<AppHdr>>

<Document>

BankToCustomerDebitCreditNotificationDTO  <BkToCstmrDbtCdtNtfctn>  [1..1]

* NotificationDTO     <Ntfctn> [1..*]
    * NotificationEntryDTO  <Ntry> [1..*]
      * EntryDetail <NtryDtls>  [0..*]
        * NotificationEntryTransactionDetailDTO  <TxDtls> [0..*]
        * Batch <Btch>



<AppHdr>>

<Document>

* <FIToFICstmrCdtTrf>
  * <CdtTrfTxInf>
    *  <RmtInf>

FIToFICustomerCreditTransferDTO  <CdtTrfTxInf>

* StructuredRemittanceInfoDTO  <RmtInf>
  * TaxRecordDTO [0..*]
  * ChargeDTO  [0..*]





 \1. EXRQ 
    pls provide the tranasction amount, instead of setting the amount field to zero
\2. OBPU
    Set the application code to PPR/PP

\3. WMSG/AMSG/STSU and EXRQ 
    add the optional field to identify the related reference 

 WMSG/AMSG:  additionalData: incomingMQReference

STSU and EXRQ:  bankReference

\4. EXPU
    incorrect exchange reference information shown on MQ 
    **PPRPP328IR20220818170521SWIFT  g0fDf5gIKyE59Nul**    



\1. Call OBPU, some invalid character in message . some field information (TXNREF / TXNREF2 VERNO) missing

theireReference set wrong value, and theirReference versionNo missing 
![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA2kAAACaCAYAAAAzZgCMAAAgAElEQVR4nO2d0bWlKgyGLWXKoIQpg8dbjo+nDEuYMizFN+/D2SpgEiAgqPtnrW/dO8cdEwhCoojDMAwrjV2HZVmHZV4Ha9bBbNh1mObPsWUdJltZbvHl7LgO83Kc0xC2Touvc/u7ncrtHE2d+k3c+TbMUc/wN6+u31P6mWP/PP3KuMeNWQdrz3Ilfh9n2u+jUz9LnG90+oXLqS0AUPbrYVgHM3761tRG36vHwUF5vX+BHAAtsJYYj6wTF1DjnHM9h2OBK0vNvSp9rvxn3Jud64oaN7fzWoE9ZhDOkaOvRE7bLu8dl7gDVm7QkWvwUjmqQZxj4cS2BwqMPst1void22Q7j3XaRTt5v71+T+lnezvnBKQ12oUZIDj/7f1lOYJgaaIA3422Xw+DLknT6vuacTDzen+9HACdkcae2BioGe9iY93GNgaN9hhTrLKO27mkGEGrr5adYrvYN49L3AEb6Shc5UrlIo3F3blkO1dhcpA7eXP10E7eb6/fU/oZ214RtO2y331i9LEDlvm9Y7XfETJI0gCPtl8Pgy5JK72O3joOaq/3t8sB0B2rT9JUqw0EfTvbOPL5TUqSxWISkietvpp2Cu3y7nFJ21E4x5bK5QTPEZkNciKO2Ml2JmX9VJP32+v3lH42tH+SFpNLfhRvkKQBnkc8SbPvHwe11/vb5QDojhXGAiv3W9VNKUnfh3DsLRnHY4lKib6adkrt8u5xSdtRWgbPzLHULJfsGJKdzERaUj/N5P32+j2ln3m+yBxwVe3C2f455r4TI547OBeSNBCi7deerGYpT4a+14+D2uv97XIA3IBYopXyrqytqM/9zT6nW2UyIY2BFfRVs1Nql9ePS9wBe3Q88aXx8HipXNBg0guDqUEC+TvHTm4DCfIiUdavKEl7af2e0s823Lsqy/y7xjp2gVUN2lwb52MQEZMvgyQNyGj69TAol/Io9L1+HNRe72+XA6AD+yZBxgnUpbHHOv14WYdpjGxKVKqPuZ6iYw+lO2Vs1eortDO5XV4/Lgkdj52kjBD4lcoxzBO/DrVo8mZgHaKsn2byfnv9ntLPXKidE6WLtyhoc+p22hBkSFzfLbUFAB9y+/Uw6JO0XH2vHwe11/vb5QBojc2PCYZh9a7rndl/slZNn13JsUmztDL6rm+JvhI7c9rl9eNSgmNG+9mmM7hDQE6apXIZE2mtyXueD8KLjF2DnFm/nknaXev3lH52am9zfhTODchF7yJ+/OMum3AHNiRpoCY5/XoYypK0HH2vHwftqrve3y4HQGssP05I/dIN7k/jWWV93DtkuZtc5C4jz9VXZGdOu9i3j0tCI3HB7LIIWW0Fua1TW6fjU5Nelcmb6Cju0jdpy86c+nVL0m5cv6f0MxZzfiJgg9+ULn+SvsmEJA1cQkK/HobyJC1V3+vHQe31/nY5AG6AG7yLcajTd92Yghs/tfrYMYaLsRhSrzetvlp2Rtvl9eMSd8A6Rk8Ho018FFsg53ZoaYIuuhNgZVn3zohl7MypX4uNQ55Wv6f0sxhSsFcatO225gyCzPkR/IAcxCRmqJikRfS9fhzUXu9vlwPgJkQ/1UH1WyOPn0X6mPEsafliYLdN+V2uvlp2prTL68clpXMukws7DTWpZXY0MhOO2enotZTOzPqpXrJ8e/2e0s8SqLGRgCXksv0n/A5JGshFSpBqJ2msPvv+cVB7vb9dDoA7wI11sZu72u9scfrYZZUhkTE59f01rb5adqa2y7vHJe6AvUnwLHWolMCa+03MTs4eZf1yPsZqY7a/pX5P6WcJxJK03HbRvpQrnR9JGsjlFknaF4yDl72E/3A5AO4Al4wl9+vMID+mLwVWX8p4Wqivip1X+OF+45IxZjXyb7gDWuNK5SinCcf2zsAECuydjoidu1x4XFm/5C+bcxflS+v3lH6WWn/uTltuu7DLsIJ+EU0oDZI0oCdpuXnFJC0anLx0HNRe72+XA+AOcDdfYv1W+ySN1BckV4YhdqMo+dUOrb5Kdub44ZHjklnHeVm3MlH6f+EO2BsFz45zpDXB4cvc4guYnJ2GfhG0Zv1OHcwKgfS31O/m/Wwc+V3u3JeEJf9ltYtjyyL4naqDNxgGOtxjyW0GXou6Xw+6JK3GdfTKcXDQX+9vlwOgG8bZVIIYC9wg//S9R6N4J03Ql5rwiYmFSb9pq9VXxc5MPwzD88YlM67zciRpyzxyT9S4k9h7Bc+S493G3H7j/pvsBDaQIRDlcus3nB8Bz7P/4uIcu0v8xvo9pJ9NkbaU/Kf1e+jDpC16jX9uFoV/wfso6ddJ7x1M9fS9ehwkbE3eAvztcgBcjQ2u16BvLjN/cykc08LrndyGX6Ev+z0yYuzKebKn1VdkZ4EfnjYuhUkaryfWaXMnqVK5hclajXwHwIxEcDoTdzcYx7gy85TQEXLr9+EUaGx1SujQr6zfQ/qZuMZa8kOp3y3jd85/hvg9YzOSNFDSrzVJWul19NpxcKufzbzev0QOgEux/Lg0jQkJDXO9az4hxOlL3mXQiQHC3+YsMdTqK7Kz0A8PG5fs9JukLcusWe74VMxnOVdvOyKol529vX4PoKRub/c7eC6tr9kifQ+5Hppf72+XA+BCvFcFCuVb6Hsrxe3yoHFJv3EIAAAAAAAAAIAOdDcAAAAAAAAAAMBBdwMAAAAAAAAAABx0NwAAAAAAAAAAwEF3AwAAAAAAAAAAHHQ3AAAAAAAAAADAQXcDAAAAAAAAAAAcdDcAAAAAAAAAAMBBdwMAAAAAAAAAABx0NwAAAAAAAAAAwEF3AwAAAAAAAAAAHHQ3AAAAAAAAAADAQXcDAAAAAAAAAAAcdDcAAAAAAF0xN7AB9QMAAIfYD8w6jNM6LIvDvA5jbMBTyhm7DvPsy83TOhhBxo5nmRQ5yuZ5PrDdnQMAAKAUzbwyDGvTeayXnRMxd06jrFNtZ2Bz7nxr7DrMm4027fe59Rsn364T033858rb8beuSW3aOK57QhzJ9Zd5Xgd7kT4A4kgHzTEgUrCDpFJuJAZTF8vYqZWLnSdVDgAAwD1Rzw9PmceUdprxHIyGwTAVZHaZb805eI4laVfVb2GStNb+4+oZ1anV9xA5rR9i/YVLDGtdDwDQCAf3zjf7dxLcTmlryVnnYrDH3907Z9zgaO06mOACSpHj9OPiAgCAF2D180rTeay1nU4AHAa74tOqAju588QSitOTlFhwX1I/p91G+xtXnLhDP/tgnbaZ57PNNfU9Qk7rB6G/uHacfF/regCAhTtg5Qto2gaGsZLc8Hsng5Jx73BQxzl2OeriYuwa7XFx5egCAABwP1Tzim0/j7W0cz8nd+Nz4o/XmKdT51v3nPP0m3hICVaN+u1JGpPk3KWfeQlCqq1afU+RU/ph6w9kO7v9lWjn2nErAD7MgVin5RIgrZyIMzBnDZw2TZc3oBskaQAA8HqEeeVW89gFdsaSmNjxkvplzbcmeCeoUpImHdcmaa372WZnyrt5pfqeIqf1g5SEpdhTcj0AIMMciHVa7pGzVk7kyiQtnCSQpAEAwPspCNqazmNX2Gll+ze56kFp6XybmKSV1K9lkqb233bOnCSlQN9T5FR+SOi3V960AECG+qM0cJrzC7x7B9TKxbC6x8YpE83pDgmSNAAAeD82EgDfZB67ys4tEA7f+XHfc6pi53A+t3q+TU3SCupXPUm7wH9b0qBNorP0PUWugh/Yc9mjLyUnxQnXAwBxqD9yF4l1Xoacj4tlHyy1chGk9eMu7guz+4UsyRjiblTupAEAAOBxsPNK53msmZ3u75bfbendADg3SYnWr8Z8a9KTNG393I0itq3sp8nfGKK3/9xkl/oEEbn9e+u47kFxpPju30d3bpKmvd4B8KH+SAympxd4B2JNtFZOInVQtv4gxQ5UDqQdSNIAAODdSPNKz3mstZ3GT2S2QDT2XShN/arMt7ntqKifuKX6nBkXXOS/6GcCKFtbx3UPiiO9p6tB3/C+nTYnJmna6x2AE9Qfrd8hvW1enTsNp4tEKyewD0axuxF29T7i6A5WpB7LXHS5kwYAAIBHIc4rtuM81thO9htbmclItH620nybGfyq6mf8VTnWBp8BSA3UL/Sfm6SFH+Zmt3/X6nuKXOH1ty+P/eg+fVcvw/fa6x2AM9Qf3YHQHQys/zv2DkiuHMN+cWYMiqT8kvHCLpI0AAB4LdF55Sbz2NV2uvPjdswGSY2tYedQcb416Ularfrt2MiN34b+i/Y9S9SxdVz3tDjSrOQ3+ebJ6TcJSVdp3AqAD/VH5yLZL/RwcB2IgVcrRyA9fs6B2jxE3KkHSRoAALySpHnlBvPY5XZa/game97YxhQpdladb01iklapfiGpu15e7b9oguKcuzg+e4pcxetvMPQnK6r4HYAsmAPuzkixu0C2gpyLu0ShdIclaoJIWs/twtUFAADAI8iZV3rOYy3sjG1qkPIdqlQ7q863Ji1Jq1E/6bxSsN7Sf5IdVBLTOq57Sxy5tXfSt/kq6APggDkQvWNk6YtIK7fhdvQaL1xSgzWSNAAA+B5y55Ve81grO5PlmCA4x84eSVpp/bTnbeW/6He7mCSmdVz3ijgyMyHERiEgA2PMauTfMAfcTmeJ49xFpJUbhjV7zXcKU+75Ei5IAAAAD8Hmzytd5rGGdiYnG1QQrK0fRe58WylJUz1Jc+pNPilp2c+sLMfVr3Vc9/g40mRsz48EDeRg1nFe1q1Mlv2tcJL9kfPkX+ixj0Gq5JzBdx793ZVCEhsgf9vUwA6+0QAAANyegnml6TzW2E5vaZaVballZ8w/p7bcbHXPa/0kjdOnrh9ng6M39m5dk34myMUS2aZxXWu5Gv3zc3ycHJ9zMWTt6wF8DWZc5+VI0pZ55J6oSSeyx8WwLIlb2yvl2K1yCSyji9p+P/ubLwmTBgAAgPujnleGtek81trOYQi2HN/mz3DurNmeFLH51gQ2cRBBtKZ+XtBNxRNhQtTRf5ScJ8sthayo725yaj8I/Uz63m716wF8DWGSxj+FjZ3IEp13jr8YmStXI0kLCb8fkoRBkgYAAG+gNIhqNY+1tnOD2nJcCkyflKRp6sfqm9M3jWjpP+9Dy0HsE5NrEde1lquVpM3zbxvGbvAjSQMF2Ok3SVuWWbnc0cN8HtvmGqKVy8R7tNy/8QEAALyFp8wtSjvfviwrt37d4onSOCvXf63jupvHkQC0Rr1xCAAAAAAAAACAHnQ3AAAAAAAAAADAQXcDAAAAAAAAAAAcdDcAAAAAAAAAAMBBdwMAAAAAAAAAABx0NwAAAAAAAAAAwEF3AwAAAAAAAAAAHHQ3AAAAAAAAAADAQXcDAAAAAAAAAAAcdDcAAAAAAAAAAMBBdwMAAAAAAAAAABx0NwAAAAAAAAAAwEF3AwAAAAAAAAAAHHQ3AAAAAADgQswNbED93g/8AKrS3QAAAABAwK7DPNNM4zoYLjC6Su4udn4wH/llOZgnwc4Nsw7j5Mst8zqMF+nrYecU6FuWiA9L7Axsdv1oE2SMXYd5s9Gm/T63fuPE97V5/q3nXfznytvxt66xNrXj2car+2e2H2yfcWIwtJ1UPbd+Eu2Hn3N68ubsK9Jm4tzR/hn2G6FNUnXem+4GAAAAAAKWDizCgKilHBlgtrZzWIeRCbo2LNem5kgISH22rr7WdpoxCEJD/TMdQKvtjJxHlDPn4DkWTF5Vv4VJ0lr7j6tnTGfr/qnyQ4dxQmpHyk47pfln9+/sJ2mSzyXfR/vnck7SYr/P6W/3o7sBAAAAgIA9Aglrfu8YG3O+g32agEvlFl/Ojk7wIQVfHewcnWPuE5lo0P3Refo7FZhq9bW20wkSwzYTn1YV2MmdRwzyDfGEKSWY1NbPabfROv3MJVKfJv77YJ22meezzaSMPR+7rH+W9rNW44Rj5zwR7WM+7Ua0fXKSNp3P6Y6bWxvG/Lf1i4nrn4RceJzTF33SeEu6GwAAAAAIWCExGvxA0NSUowJI59jpaVprO4ffO+QnGwf/zrlUB0p22gI64q68Sl9jO40TpFH9aQ/+iePa+lF2jfYIjmPn3IJnKcGqUb89ScsMWFv3M/E6U7DbyVxjmvqp/WBlW2qPE1J/iLUX6RsXJknLaSeqDiVPvHL03Z/uBgAAAAACVg5O2GCwVC4SXEp3upvYKeEE/GGQuwVtXAAWC2hz9bW2MxakqYK4xPp55zZykra9t7Y/YaqUpEnHtUla635WI1j3sIo+Hamf2g8xW7bjlcaJrS2jCRdhe1TGym2Q0k61/Y4kDQAAAGiFjQQnXDBcKlc7Sattp4QQXE7M3zdSlqLl6GtuZ8R/mqA1qX6hn3L9lpikldSvZZKm9t92ztyESsJGrjGN37V+iNlSeZy49Emajf8OSVoJ3Q0AAAAABOyNkrSUY3dI0jg7pXOZ8wYWycG81C4d7NwShPBdKPc9pyp2Dudz7wHrVUlaQf2qJ2kX+C85QchAlZgn+F3lB3vItBgnvGW1qfXfdE3+3047JFokadfS3QAAAABAwMrBCbtsqlQuDHZs4gYErewUYO+eCwHgXrf5CKJTgyXN3fpL7XR/t/zueucmBrlJSrR+hnj6c2GSpq2f+97Svi355G+Y0dt/brJLbamftC2+OdjbRRG0R/2u8YNtP054uybOCf6253pTbZGSUCNJK6G7AQAAAICAFYITKbAtlWNgg8TWdnJIMkQycdrAYsgMljQ2trDT+AE09cSj2M4PpB1XJmnK+olbnM+ZTxcv8l/KNuyirfb8++zv3OX4I9cP9vhNy3GC2kmUrdemy0l0qOWpm09L3qFM7p9c3Qv03Z/uBgAAAAAC1r8DbO06jMEd69iTLZUcQdK7Qq3sZNgDnYSnfd425+P5HCnJgqivo53st6Eyk5Fo/QJb97+ba5M0Vf2M/5TJ2iB4TwiCr/afG6iHH4RO+hyCXb0PGCdfv8p+ne0Hp21ajxPek0XXTsP0xSn4d9COSNKuprsBAAAAgICVJ+7ok60COfv5m3UCMXapXGs7CfZgmAtm3ETADYat/7vUJC2qr5OdblKwHbNBMG1r2DkIG2SY65K0WvWj+mBKInOl/6J9z+bX0W2vlKWuqf1a5QfrH+8xTlDf6LPB8dmp/5b4jEECtP9daFMsdyyhuwEAAACAgHUCoelgtJGgpIKcdf6e8n5KUzsDvM0KuKDJnJdmUb+N7cyXrK+HnU57SolTbBOFFDvFgPCqJK1S/UJSN9e42n/RQN05d867hVXrV+IHR67HOOH1X8vYGSRpW9tZx2fWaSskaVfR3QAAAABAwKbd1a4ux91d5oKS1nY6uEuuYoGruyOddjfJHH2t7Ywl0ykbsaTamfT+lIvk48QkrUb9pPMmbQLRwH+SHSk3EVjbheA9p35qP9h+40SOnZPzt8mp51bvySJJu57uBgAAAAAC9iZJ2hC5G9/azg9uYJnzDhkbBEfsydXX2s5kOSYJzbGzR5JWWj/teVv5LxpkM8ldjOSkqnb9QjuZekfRykUQk7Tl9903t03cHR23NpX8gCSNxRizGvk3/Y0EAAAAeOx9krSi76TVtjOwJzWwcYPRUx2GxEQ0N5BqaGdyskG1t7Z+FLnJRKUkTfUkzam3+JS4RT+zspz2SSH7EXpl/dR+sDr7r0rSuOR1T5jCRMwcSyFHJGk6zDrOy7qViW+/3oYCAAAAEvZGSdpwBHtscNnKTuO/T+Lu2hfC1WEJNhsQP8Kr1dfYTm/JmpVtqWVnzD9UPxqG4LzWT9I4fer6cTY4emPv1jXpZ4Kc9pMU++Yl1DWmrJ/aD9rrXSk3jvy7de4mJ9ymLvN81hk+Qeb6t9dOSNJcG+flSNKWeeSeqN3AWAAAAIDF3itJu8sdcnbrb4JTPax/PGWrcq2+1nYOgxPkO3Kz+7dZTu6y7aQwkSTNrKfNNUiIfqGpn5c4zOe2PCVEHf1HyXmyVABuhd9vbWLq1k/lh8bjRGgjxUy0p5uIhYmm12ahPYn9mvL9tyZpfH1vYCwAAADAYtsGNdF3egxzN7+xnaVJhfcExQm4uE0AuiRpCjs3qI/3bgFp9WQk0k9i/UiE6Re59WP1zYnfuWrsP2OJb3otv99Oi123lEzKJjGa+mX7ofE4EfuA+ekp4AfxswVuXwrtSezX35ykDcNqp98kbVlmLHcEAAAAAIX5LOfqbcdFdmYvU3wYufXzlvA9wH/DQ+r3hH72BBu/CWwcAgAAAAAAAACPorsBAAAAAAAAAAAOuhsAAAAAAAAAAOCguwEAAAAAAAAAAA66GwAAAAAAAAAA4KC7AQAAAAAAAAAADrobAAAAAAAAAADgoLsBAAAAAAAAAAAOuhsAAAAAAAAAAOCguwEAAAAAAAAAAA66GwAAAAAAAAAA4KC7AQAAAAAAAAAADrobAAAAAAAAAADgoLsBIBtzAxsAAAAAAAAAF9HdAB9j12Ge12FZDuZpHUxM1qzDOPlyy7wOYySh0errYecU6FuWdZjGiM7G7bIxzb/yc4KuEjtb1s+OZ5nL+wsA4HtoNA5u4zN7XhP5jdbOD8auw7zNYTatXaj5L2kcpWxdPnULddtj3joxrYNl6mfG4zfUcTsdx11ba/ghp13G6aiPZdprco87+qcx4iObOefH6pvQL2LtlxqHtPaDa5fLJPSxErni6xZyHeluwMHIdPINKzTwLMhxk4BWX2s7zXieXMLORE5Sjdtlxwb2xgZ3pZ1P8XtxewIA3k/DcXD6HJOC0pn7jdbOj2wYzMaStHD+O8HNfxpZG/k9M5/teqgkzTln2JYlftC0izsXcfPyZpP9/Ns6waulbAx/xySqqWw2RuMGG7HLxv3Wyw+T9HuhT2vlWo8vXyHXjK7K6QvKvYPi3nHjLv594Jn9uwnugGRr6Wttp9OBws4SuxvZtF0ctsF6dvRLdzpVdnaon7XrYIz/tyv7CwDge2g5DpYEpdp5jHqaFQ2CHDvmiRh/zWdcpmStH7xac/zOmGNlBJmkbb/fsH5yyQbq4VguzN9FflC2i3fDkJmXwyTN08UlOkJ/yWVvy0jcEEsKc+KQ1n7Y9Vm/j3nXCGGvVq71+PINcu3oqjzo0CPdGO6ditNxKzfk1qm5u1/Z+hrbKd6hG4SBqkO7bGyde7THAMb+Xmtnx/qxcszgWFsfAOBl2LbjoDooVepzx7otmJWSl42SpzP7U4ecZeVWHstz5+k90GPs1/pB2y7hqg4pcXT9G3uaVuspWtjHxCWKkf6TE4e09oOoz/BJsVaueZz1drmmdFOcATdhDM7dEqYRU+/KpOprbWcsSeOOd2uX7Tef824DJTeQau28ld+tQleJPgDAq2g9DpYGpdnjrvm852TO55eStOSlbyFWeQPMymM5Zw81D6fchNP6Qdsue+IixBVUkib664J5LJaAuTrJts2MQ1r7IaZPe93WHicgp4ztqtJNcQbCIBDrtKpHltpB5wo7rWw/N0j0apdwsordadLaeSu/W+WFfMHkBgB4Hq3HQW1QWm3cNWlJmvZJhfrJjk1L0k6vHoRJT+LY3utJ2mh43WSS5upkAt2ay/Zj58y9eV0ahzR9kiboa33dQk4RR1anm+IMLNNQRribYs4vKCcHwpy+TnbuyzZmf80suwShY7ucJjFJRmvnzfze/G4vAOA9dBgHVcFezXHXpCVp3jLJjPE1+iSGwwpJGtUmoZ2fYD11TtAG3dp2cZM0LsHgkjTSZ0KbFGGP+p3sSGjfrDikgx+i+pg+rJJrPb68Xa45XZTmwd6t4BrZOpsyzEdjpw7Y1e/eldrp/m5Zh2mUX2Lu1i6MXnZg0drZ2e/7C7vuhay4i3jFHUgAwMPoMA5WTdIS9Ennj43P4WYX0a3ZKdtTsYced+MQOwrv+wx+kpYzrlfZwCW1XQY/SYvN15aQD5+mxZ5o1bgmsjdcyY1DOvghJdmiElGVXOvx5e1yzemiNAPpYt2Ozc6uTe6djSltPXKyvp52Oud3BwT3yVr3drH+AL79nb3rpbWzp99t4ANHX7V+DQD4HjqMg0VJWo1xN3P8o3aGTHlfSZ2kMaR+JodLckKKPoWQ2y5DkKQNciJA2h/4LSVp0MLGDZuPZmbeZY5LT99a+6FLktZqfHm7XHO6KE1H3B3J+heju/zP7dg5jRzbjamXney3OGZiMO3ULtxLmOzLl1o7e/rdrt5HJFMH5Vr9DADwMmz7cVAVlBbok86fOm56Kxfc+S+sA2V7ri8WfpynkgP3iVLOjnClyUFWuzi+4Xzq2mQZm12/XzmHaTd7yI5DOvihaZIW+Pjy8eXtcs3pojQN7kVV6sJxL46wMVMbOaqvk51u59mO2SBpszdol5Rljdw3RrLsvInfKf+kBAWl+gAAL6LDOFi63LF43DX5SZorGz65sDHbU7FCImb5JY/esj+bPh/USA6S28XxDfV+4uaHWJIWruq57F0dpu6xNsuOQzr4oddyxybjy9vlmtNFaRxvU4yEC0f6bUrHTtLXw04rDIaGmTR6tMtm50wnHuSL3Fo7b+D3kNQXxWvpAwC8hA7jYGmSVjru1ljuLSVNl2wcMvDb6rO7CTLnKfJDQbtQSVpoezRJc+t38UoQKbAm7Yv4j+sXrf3Qa+OQJuPL2+Wa00VppHM7A2HqnaiUp1i2gr7WdiZvRRuct3W7sMsxQ4J6aO3s6XfxXMKkVVMfAOA9tB4Hc4LSGvqk35Xcoebmv+IddzPrR43/7se0Y37P9UNpu3ArWuyQlqRdtmFIQBj/JG+9r4xDWvmh1xb8rceXt8q1pZviSKdOHLyjg7GVnZCrr7WdyXJBJ2rdLt4ORxFq2NnL7xzJyXQlfQCA99B6HNR+LLh03KXOf0WSpl5SHrPf0vMYmTzY+Jhf/NHmzHYhkzSnvebxXkla2N6xpWfaOKS1H2LJFtd/tXKtx5e3y1XEGLMa+TfXKNZhjwso+WViZvlBkhMU+lrbGVlG8A4AABGdSURBVOtE3CDQtF2Mf/fGMFADodbOLn4XEAf5C/QBAN5D63EwtvkCF4QXjbsupk6Sxt4cs4edWU/TNjkmKOOCYK692G+ZFvpB2y5ckubWOyUZaZakDf7cmrrzZG4c0toPUrJlnL6bsyxTkms9vrxdrgpmHedl3cpE9ulhHS6/wDIM9tbvcheYITqnu6yAvJtGOUCrr7Gd3hI5K9vSq12kXZNSOrzKztZ+F/rt/tIpVf/a+gAAr6TpOGiFgM7KCZTWTm+8C3Rw4+A48u/uuptnUXZ6u7VN53Mbuw5TUAc2STP0Bl77uYQgXlz2qPSDtl3YJM05Jvkwpb612ROoWdZZFIc09sOebAV939twROhLuXIl1y3krlnqaMZ1Xo4kbZlH7onaBcqVBnsDhMSpwax/PGVrdK2+1nZ6nciRm92/zZGXaC9ul9S7DewgqmyXln6ntmb2fj/Tg3VRfwEAfA+23Tg4DOegPJxXZi4A1+gz55f0SYK5IZz7KFg7iTrG9MW+k8bNc2LS4pyTahuNH7TtIiVp4Vxlhb7aMkkL7Yr1Z20c0tIPMTnu26tauR7jy+vlyvu1l6Txei6+wLQXooSl5C0xCcz82t0uSZrCzn0AmWgdsQ8pt2iX5N1vDP1Sa0m7tPK7NHlPI+8DJGkAgFRajYMbp29eOWNaVX1Gl6SJSdZMrC6h6jgyumciALO8rnnin5rEkpbYZ1py/aBtFylJGwY/CbCS/xsmaalb/teIQ1r5gUy25k8sIdivlVNft5C7sm/b6TdJW5b5Ccsda2E+j4B723GRnerlcS9vl1b185bs9G4rAMA7aTwOPmFeqbE0/O5LyzV1xJJ5+CGb1nHW2+UKeNbGIQAAAAAAAADw9XQ3AAAAAAAAAADAQXcDAAAAAAAAAAAcdDcAAAAAAAAAAMBBdwMAAAAAAAAAABx0NwAAAAAAAAAAwEF3AwAA4OtBQUFBQUGpWXrPa6CY7gYAAMDXg4KCgoKCUrP0ntdAMd0NAACArwcFBQUFBaVm6T2vgWK6GwAAAF8PCgoKCgpKzdJ7XgPFdDcAAAC+HhQUFBQUlJql97wGiuluAAAAfD0oKCgoKCg1S+95DRTT3QAAAPh6UFDuUpbl37r8/KzLz7/epnx1gR9QSkvveQ0U090AAB6KuYEN4C3+Q0G5S1n++7Muw7Au/yE56Fla+GFZ4OM3l97zGigm9gOzDuO0DsviMK/DGAtwWst9MHYd5o/cZBNknlK/xnLGrsM8+3LztA7movbU6uth5xToW5Z1mMaIzi9ol6fYeVP/UWX5+2dd/nxICNSW5d+6/Pf3N7Dbicuq5f79/Nrmyv35uy7/Fl7m57+zTIKcVl/LcvjrL3385+/hz5/D5mX55/ua4+8Poy/83V/105dl+bcufz7+J9p1+e9vxE667vu5G/bPXf7fz6dOw6kNa5ZSO0/nEvxQZOe/n9++E16Df/9L1vVr3x+yPxfbF+1jR19z7fXkGHv2a8a7/n5kHcy1pNXXsgzD8DvnzfPv3EPNU3b6HJ/XwTp/3+UCpmkdbGJMDkqJBCbzcg5o9sDG3kTuIxsGX9Ek7Sn1ayw3EkGsi63cnlp9re00YxBsh/pnJtB/ebs8xc6b+y8sy/ITJCP/iZPxEdQxMMGpWm67y8/xwwQtjeValuWvbI933Ancoz5gfOGdjyQ/wF9+/pb5fWAS1Mb9c5cNk5GLkrQSO8nzRfygtvPff8G4Evozrc+c+kHF6y/ex2hbPTlmvNyvmZ8gSYvpIs6n1deyDMOwDlNkXnWPuzceJ2H+EudMUBHh4B5kzH7W7AYflMObyhniDnckeHpU/VrLWediddrPfUK5MHdjmuprbacTqIf9Kvb09tXt8hQ77++/sOxB2h5EycHTETD88e78eoEElTgo5Lyg5r8jiPSeWHDB+s/Puvzz70zH5Er0tSxe0hQmVGEg+F/YBv8Ofv7b6+T+ndX334/zu5/gaU5eohYLKo8leD++zTuxJLtF//xHPNG6OElT1o893wXBvZdIhv0z42kjmdTUtPPfz+ddPIbdt0KSxj0JFpO0X99515Kb5IfXrFJfyzIMg59sneY4Z67ikrTRroMxH2wQc89I1K6FO2CFAMRx3jz2lXPvjs/TbyeSAq6n1a+53KdNKRm3rU/HW+trbOd+TmG5AHn85e3yFDsf4L+weMHwn0jg7AZNVKC7BQrB3V6t3Lp+7shTMu6d+pygdJdjgp3K+moXb3nan3PSeDwZ+UsGfN5v/x1JmqhzT9KIBM4NyCNPYQ+Zn6hezXtSrfun1yf+fBLdrS0uSNJKriP5fHVvPMT61d5Hk/tdfGy6oux9MEw0wydwhK+jSZqUaIX9TKmvZTluUM6f/0703DdNQpJmiHnTibWp+Q/UgjmwOY5r/D3QCLLo1nKD+ayjNc6/E5K0p9SveXtKOG0bXrSt9bW2Mxbkc8ff3i5PsfMB/vMm9uB9FC4o2X+/P3VjltwwCZBWTipecqAK5NN1leirXQ47/h7+cgPBv59jP22SNP88aW2assROlaQ17p/7+1KfJ1rSE6QapfZ1lLPU8fSOp1Nv3g4mSUvod+5vvHaNJCE5dornEXQefZOvhypJ287LJWmZ+lqWY76ZjtUf1pmPps+xba5LTtK08x/IhDkQcw631Ke13InEJO0p9evenkzbhudtra+5nVa2f5MLg/nXt8tT7Ly//7yJPQiWYne4o8E6s+RKKycVJGl/D/99guy9bn9/0hKhWklaRtukblShStI698/Lk7SK11HOhiHiu1vUU53YEz8mGTnb9iufmqTl2inWWUiI3b7J+aQoSeOe3GXqa1m8JG1LqvbY2B7/3p+o2fT5Tz3HgwwiDW+JY+EGHbtzWstFbE/ZUOPW9btDe7pYJiBtra+Tnfu67tl/N2lfKvel7fIUO2/uP29iD4ICKbgS7yxTGyf8RzxdyJCLlVggyMpFAsTa+moXL0lz/n9dncDyZ2mapHm/ib1ntOmMbVCTmaTdoX9emaTVvo6S/bDfuPnjvwO3/53Wdbw3Kcgx11GYIKUkaVo7yXNFbjp4SRNzYys3SZN0avW1LF6S5v2/M/fZQZmkOb9J2k0dKKD+yAUn1nnpfT6ClN05reUitmcnaXer3x3a04F9b6e1vl52ur9bfrdtdwP100D2Le3yFDvv7b99UmcCH/ZOLff7xd1U488RLO6Jn04uVpLfa3E3m9gD2fx3cFL1XV3C94jcJY/bUsd1TVxSWDNJS0x+U5Mvb4MMd8v//+j63KF/9kjStNdRih9iyZH4tMmza/jddl/YHOOs80hkonYU2EnaEFuu6SZNsXGUS9LcjUN+/hPf69Tqa1mOm4Kf+cZd8jg5f9cmadwqFFAL6o9bcDIf60xPG3Q4zjklB63kJNul3z2lfndoz5R2ba2vp53GD/S3QJ38Zsg3tctT7Lyv//ZJnbmry74XQQVPp40Tzu+1aeWkkhoMk7vDKb53dvUytjxbfvynDPuSRz8pu2OSVm2J3fBHeNLbr3+2SdJq2in7IZqsxJbvkZ8L+CO+I0bZH03CCu08/T7yVDhMcKm+r9qCv7K+lmVP0rYkal/yGCRlSNLuCvVHewQvxnFe6IhTcNJajiIlOHxK/e7QnsFvxe3UW+nraGf4rS0v0P/idnmKnTf23z6pM3eX+U0S/EDHW0bkBgvsEso8OakcAXwkuQg/HjvEA6ISfS3KKUkLA+GfIICXkqbWSVrORhXLv+BzAfKW/3fon9cmaRXtTPRDdCOh5OSJStSopI65cRTTU2gnbTOf0J2SJsLuaJLGjUvUUkilvpbllKSFNyptMDe6cxuStDtA/dFNdObDmWEQwj7BaSUXs5373VPqd4f2HJzgdGZ28Gmtr5OdbpC+330Kgn77he3yFDtv7r994k9Z1sh9CNldtsS95E4tJ8uQ44r37knmEzFfXk46aumrXcIkbV3pJPKWSVqFQNILdLmnLZ36Z7PljqV2Jvoh/WPP53N519n+dPc/WSZzqXUNO9lzZe48Gj59y34nzf1+HLu7Y56+luWcpA30zUIkaXeF+qNZT0uCqOVAJwe2lovYnpKk3bp+N2hPb1MF7net9fWw0x4y0rtL3kD1De3yFDvv7791TVimRCz3IZcuEcuWwkBLK0cVf9MB/Q6Lye9PVdJXs1DJF/VkpHmSFlsiVvGbXORyrzv0z1ZJWoGdOX7QJj/+R+GFhMv1n9AXWyVpqZsDkUlTuFOuZndH5luMWn0tC5l8UUsbtUkaNg65mkjDp9zVth3lpN+lbMF/9/r1bE93aVhs57rW+lrbGdsEg/teyNvb5Sl2PsB//gQfg9lBLOUdFDfIUMp5v3FtLtwCP+87TeX6ahYu+Vr+/Uv6HfmbBlvw5yxnjRV2qW7H/nn63ZVb8JdcR5plxdrt66PfSTvqkZVocbKFbV6y+c3pswGaJI3rn0p9LQuZfA3DOhhDz1NZSZoz/2EL/qtgDkQfYVo6eGktJ3UaKUl7Sv16tacbWOa8a9NKX2s7k+WCYP3t7fIUOx/gP2/ST4EKFtjvG+VtRhKT24+7CVPNID8aRF4TbJeU5K3TMz8YLJ4rlqRFloTmbBiSUqIf/W3cP4/f6ZO0MMkmf1N6HWX6IXdXxHw7j/GlKElT2unb9C96o+FUv/ApoWOHLkmjn+Rp9bUsbJLGzlXOjcxYkqZ9taEFYRJ6tZwSY8xq5N/EHMbcIeaCl9ZyJxKTtKfUr0t72vyAu7W+1nbG+h/3JObt7fIUOx/gvzAY8TZn8LarPweb3HKc/TgXPCvl1jUIXColTNLSvCv01SzJmz4kLGurkaQt/+LtlZpYphRxKV2H/unblp+kcRu/kL8ttDPXDymbaJByqXakJovJG5TobwLkfGKDTZrcJIywN5qkMTc7tPpaFnJpozgfJyZpRjvvX42TA3DzdlU5vZ3jfPSJidcnnGRf6jP5gQv78ddOcsY4WD9Jc4/1tvMRck5Hncegbc0F7anV19hOb8malW35pnZ5ip0P8F9qQMMGtPuSK38r+9hHajVy4fsrbEKZ8BRiP9++6cK5/rX1XVH6Jmk/fjt4uy0KejI/TM3b6357i3kK2rB//trk9osfL0lL6S+npcexRFBp57rq/BBbYvlbh3ATDHepcLCxCfNOmmhDyjJOhZ3k+XOWgUofuiZ8Ie5eSWy0UqqvZamTpFl/zhqduS93B+erCXdwTt3QRCtXYOe8OH1tHrknailO24ye/X9Ht7hvIWfW08v9JDPxOPYJ9Wssx25RTmA76mtt5zA4wboj5/W9mbn78uJ2eYqdD/Bf8lOB6Fb8W6AVBAnRjSPS5dLfneOCoYHf5pradEGpr2UpSdLo71YRhEHi38jvhW/P5X6j6mQn6b8UfQ36Z2p7ionDf0n21atfuh9Ife7Hxf8IbRP2Gff3+zWo6A+MjNbOdVU82ZOSptCf3LjEXkvyx6xz9LUsVZI0jnki4urOhHOvZpVOjlyBnV6SxuuLncgSSdAcf0mwmZwpSNKeUL/GckXBc0N9re3c8O4gZQxWb22Xp9j5AP+l7FK3rvI7Gv4TDScoip0zU65Kkhby97/0gDlRX8uSn6QdgWfdJO3Ppy0jPs/4NtphO2fnn7QnHa36Z4UkbV2Dp0AJ/UpTP40fPH3utv8h7GYxf+nfZ35QPnnjFq2dkZ1Jz/XikybvfMnj0p/fNmF2kNXqa1nyk7T5mAvJJG1eh2mkV7ncBXfDL9tATomdtvF/Vi539DCfR525hrSW0/KU+r29PVujtFNajvfN7fIUO2/ov5rl+OBwXmCglcst/lK0PsHLt5eSDQ1K/Xf3/unpVCyhzbGz1sYSmiW/PZYJ32Fp8jeV/nN0Jx6yccig3jgEAABAM1BQWpWa30ZD0Rf4AeXq0nteA8V0NwAAAL4eFJRWpea30VD0BX5Aubr0ntdAMd0NAACArwcFBQUFBaVm6T2vgWK6GwAAAF8PCgoKCgpKzdJ7XgPFdDcAAAC+HhQUFBQUlJql97wGyvgfzZYyHx7iIt8AAAAASUVORK5CYII=)
![img](data:image/png;base64,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)

\2. Invalid layout of EXPU

![img](data:image/png;base64,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)



\3. AMSG/QSTS  ==> transaction reference is missing 

\4. EXRQ , amount fields are always zerro 

\5. AMKR , MUR number missing 







Handler Task:

1.检查已经跑完

seq job status validation result  behavior                                          exmaple                                        

 1      done        passed                  rerun                                               STPSwitchAndCutOffTimeApiHandler 

 2      done        not passed           pass:not-rerun, notpass:rerun     settlementAndBalanceHandler,Camt054NeededApiHandler

 3      done        not passed           pass:not-rerun, notpass: not-rerun





如果passed， 不需要rerun, eg: Camt054NeededApiHandler

如果not_passed, 需要rerun,  

3.IW  retry settlementAndBalanceHandler  定时任务重试10次之后标记为outstanding



2.terminate

current handler failed, terminate handlerChain.





### Handler rerunable & terminate

#### Please help to add approval for the following handlers / failed reason.

- currency checking (restricted currency / no such currency)
- STP limit checking (STP limit exceeded)
- debtor/creditor info checking (debtor name too short, debtor addressing meaningless/too short, debtor/creditor ac/name missing)
- settlement amount less than charge and not full paid
- possible duplication
- AML true hit
- query received
- "instruction for next agent" exists

iw process, add AB 

- holiday 

  test fail

- 20a.sh   address 

- add iw handler, not passed, outstanding  when no holiday record found or today is holiday

  

  

payment.approvalStatus = PENDING_ACCEPTANCE,     payment.approvalRequirement = "AB"

UserAcceptanceApprovalService.createApprovalItem(PaymentDTO payment)

![sit_schedule](C:\Users\donald\Desktop\ecph_sit\sit_schedule.jpg)



1. 009  cover

2. 004 准备多久 
3. 触发iw的return， outward的004



ow status diagram

ow的handler all passed之后，把ow的状态改成completed，把iw的状态从pending_transaction 改成 completed



####  20220830

1. save General Ledger Entry File  into DB

	* bank position
	* cash positiona

1. General Ledger Entry File 

####  20220908

In addition according to the UAT Stage Plan PPT the user should start next Monday 12/9 for the testing of "Outstanding Remittance (Amend & Approval).
          Derek had requested to have a preview/pre-test by him tomorrow and Friday first, please ensure that this would be available and if not do let him know beforehand so as to alert the users in time before Derek's preview/pre-test.

#### 20220914 Create Approval Record

Code is implemented according to below logic. Please kindly know. 

1. For all handlers in outward process, terminate when current handler  failed. 
2. Check Approval Handler:  change payment's handling status according to  payment's approval status. If payment's approval status is  pending_acceptance and pending_approval, then payment's handling status  is pending_acceptance and pending_approval. Only if payment's approval  status is approved, then payment's handling status is submitting; 
3. when payment's approval is pending_acceptance or pending_approval,  create approval record in db.



#### 20220915&1003   pacs.009

1. add third validation result: Not Applicable, code adjustment as belows.  please kindly review. 

   A. do adjustment when handling status verify and control flow as belows: 

   1. AbstractValidationAndToolsExecutionServiceImpl ->  GenericValidationRule. validate() 
   2. PaymentValidationRule -> isCurrentHandlerPassed()  
   
   3. determineHandlingStatusSelfHandler 
   4. checkApprovalStatusSelfHandler 

   5. swiftAckStatusQSTSMQHandler 
   
      
   

B. return not applicable result when message is not pacs.008 in below handlers 


​		1.CreditorAndDebtorInfoHandler 

​		2.ChargeAmountApiHandler

​		3.settlementAmountLargerThanChargerMQHandler

​		4.STPAmountLimit

​		5.Adverse weather check, only apply to pacs.008, Other pacs.009, 009COV message need to do as well

​    	6.Code Word handler	



​	

```
        <ref bean="incomingHKDEquivalentAmountCalculationHandler" />
        <ref bean="intermediaryBankCheckSelfHandler" />

        <ref bean="incomingBankRelatedAccountsApiHandler" />
        <ref bean="incomingUpdateBankPositionOBPUMQHandler" />

        <ref bean="stpSwitchApiHandler" />
        <ref bean="futureValueDateSelfHandler" />
        <ref bean="sTPAndCutOffTimeApiHandler" />
        <ref bean="holidaySettingExistApiHandler" />
        <ref bean="adverseWeatherApiHandler" />

        <ref bean="outgoingChannelSelfHandler" />
        <ref bean="sTPAmountLimitMQHandler" />
        <ref bean="settlementAmountLargerThanChargerMQHandler" />
        <ref bean="settlementAndBalanceMQHandler" />
        <ref bean="agentExceptionListApiHandler" />
        <ref bean="sTPCurrencyScopeApiHandler" />
        <ref bean="creditorCountryScopeApiHandler" />
        <ref bean="duplicatePaymentApiHandler" />
        <ref bean="creditorAndDebtorSelfHandler" />
        <ref bean="investigationCheckApiHandler" />
        <ref bean="incomingAMLResultMQHandler" />
        <ref bean="nextAgentInstructionExistSelfHandler" />
        <ref bean="determineOwSettlementMethod" />
        <ref bean="determineHandlingStatusSelfHandler" />
```





#### Task

1. the address lines total sum is more than 30 characters. 不包含符号
2. add new sql for custom_config  for category: ow.charge.amount.  exist 12 us dollar

user Remarks

ssf



#### 0915 Task: Requirement

1. Add event type  : querySubmissionStatus

   trigger:

   status:

> batch 2 approval

2. event type: ACCEPT_PAYMENT







* 

#### ~~0922 Task, delete outward transaction~~

rename getName() when expuHandler,  obpuHandler, are in delete process

terminate()   return value

##### OBPU:  reverse flow,  delete effected osn and obpu, expu

obpu;  Ledger record in db

input  fields:   bankCode, accountType, NostroVostroFlag, settlementDate 
