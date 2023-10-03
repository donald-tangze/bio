### 0920 Task: user input Settlement --- issue#76

```java
settlement acount includes: settlementMethod, settlementDate, currency, [IBMBankCode, Account A/C,  account type]

InternalSettlementDetailDTO 
        private InternalSettlementMethod settlementMethod;   // INDA or INGA
        private LocalDate settlementDate;
		private String currency;
        private String bankCode; // bank code in IBM format
        private String accountType; // single character account type
        private BigDecimal amount;
        private String sundryReference;

     
[system queried] instructing Bank Related Account info
BSPPACT=
{recordType=1, 
bankCodeInIBMFormat=SCBKGBLD, 
currency=GBP, 
bankIndicator=N,         // N means INDA
accountType=A, 
accountNo=62-82-01403-6, 
accountID=6282014036, 
lastActiveDate=60939100800000, 
accountStatus=N}
```

![inputSettlement](C:\Users\donald\Desktop\ecph_sit\inputSettlement.jpg)

##### 1. Inward process

* put  [system queried instructing Bank Related Account]  into payment additional data.  Key: "internalSettlementDetails"

  > Resoponsibility of inward BankRelatedAccountHandler

* put [system queried instructed agent Bank Related Account]  into payment additional data.  Key:  "internalSettlementDetails"     

  > Resoponsibility of DetermineOwSettleMethodApiHandler

* put [inward movement]  into payment additional data.  Key:  "inwardBankMovementDetail"

  > [Resoponsibility of UpdateInwardBankPositionHandler]

##### 2. User modify data 

After user modify data, would send data to backend for outward process.  Data key:   "internalSettlementDetails", which include inward Settlement Detail and outward Settlement detail. 



##### 3. Outward process

###### (1) Verify User Input Settlement 

 when user input inward and outward settlement account and settlement method, verify if these account and method are valid. Key: "**internalSettlementDetails**"

Resoponsibility of **CheckInputSettlementMethodHandler**,  a new verification handler in outward  process

precheck and Settlement.

Verfication Rule:

1. They are all might be null.

2. If not null, need to exist in database really. The account no, nostro/vostro flag, bank code, currency can find records in BSPPACT config table.

3. Agent and input bank code might have no connection, don't check

4. use user input bank code, settlementDate, settlement Method OBPU.

   

###### (2) handle OBPU

Resoponsibility of **UpdateBankPositionOBPUMQHandler**

verify if there is key = INTERNAL_SETTLEMENT_DETAILS exist in additional data. 

For outward bank account movement, we have two pieces of  data to choose now .   (INTERNAL_SETTLEMENT_DETAILS and  SYSTEM_QUERY_RESULT [BSPPACT] )

* If yes, use input account firstly,  key = "INTERNAL_SETTLEMENT_DETAILS"
* If no, use system query result firstly,  SYSTEM_QUERY_RESULT  that iss bank related account from database,  that is to say,  Key= "BSPPACT"

For inward bank account movement, we have two pieces of  data to choose now.

* If yes, use input account firstly,  key = "INTERNAL_SETTLEMENT_DETAILS"
* If no, use system query result firstly,  SYSTEM_QUERY_RESULT  that iss bank related account from database,  that is to say,  Key= "inwardBankMovementDetail"



Whatever, generate movementDetail, fields can not be null.





###  Test

local test

inward:  HY8pgu9r75nfcCEe8vkVdYxjouVFevF0i0E

inward id :   21327 

outward:   21489

##### 3. Effected area and code 

* OBPU MQ interface,  when generateRequest, movenmentDetails has arguments:

  Bank Code in IBM Format, 

  Nostro / Vostro Bank Indicator, 

  Bank A/C Type Indicator, 

  Currency,  

  account Type



* save ledger record: General Ledger Record;  DebitorCreditorLedgerRecord

  Bank Code in IBM Format, 

  account No

  nostroVostroBankIndicator

[
  {
    "name": "Check if Host System is readable",
    "result": "PASSED",
    "validationDatetime": "2022-10-18T13:14:26.381",
    "code": "0000",
    "outward": false
  },

cat	= 'BSPPACT' AND KE2 = 'EUR'   ICBCUS33XXX
