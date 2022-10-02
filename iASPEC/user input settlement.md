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

user modify data 

##### 2. outward process

###### (1) Verify User Input Settlement 

CheckInputSettlementMethodHandler, precheck and 

Settlement, outward need a verification handler,  when user input inward and outward settlement account and settlement method, verify if these account and method are valid.



Question:  

1. Agent and input bank code has connection, if need to check?  no

2. Which bank code, settlementDate, settlement Method OBPU should use, ?  use user input

   

###### (2) handle OBPU

Resoponsibility of **UpdateBankPositionOBPUMQHandler**



verify if there is key = INTERNAL_SETTLEMENT_DETAILS exist in additional data. Now we have two pieces of  data to choose.   (INTERNAL_SETTLEMENT_DETAILS and  [BSPPACT]  SYSTEM_QUERY_RESULT)

* If yes, use input account firstly,  key = INTERNAL_SETTLEMENT_DETAILS.
* If no, use system query result firstly,  SYSTEM_QUERY_RESULT   that's bank related account from database,  that is to say,  additional data of step.1.



Only if (directionType = outward) {

​	user input internal Settlement exit

​    create MovementDetail

​     

}

generate OBPU

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
  
  