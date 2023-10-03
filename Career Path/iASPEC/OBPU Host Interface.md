[TOC]

## 1.Outward OBPU For Swift, Chats, XbFPS

IS_CREDIT=False

### 1.1.prepare Movement Details

* 1.1.1.get internal settlement detail
  * STP
  * Manually create:   get from [getCustomizedOutwardSettlementDetail]

```
for Outward transaction, internal settlement detail
Object object = MapUtils.getObject(payment.getAdditionalData(), INTERNAL_SETTLEMENT_DETAILS);
```

* 1.1.2.convert internal settlement detail to Movement Detail

# 1.2. OBPU handler

## 1.2.1.channel = Swift

* 1.settlementMethod=COVE
  * find related bank account of reimbursement agent
* 2.settlementMethod=INDA/INGA
  * find related bank account of instructed agent
* 3.判断 related agent的地域特征

  * 3.1.outport bank
    * Credit
  * 3.2.overseas branch
    * Debit
  * 3.3.local bank
    * Debit

## 1.2.2.channel = Chats

## 1.2.3.channel = XBFPS



# 2.Inward OBPU For Swift, Chats, XbFPS

### 2.1.prepare Movement Details

* 1.1.1.get internal settlement detail

```
for Outward transaction, internal settlement detail
Object object = MapUtils.getObject(payment.getAdditionalData(), INTERNAL_SETTLEMENT_DETAILS);
```

* 1.1.2.convert internal settlement detail to Movement Detail

## 2.2.1.channel = Swift

* 1.settlementMethod=COVE
  * find related bank account of reimbursement agent
* 2.settlementMethod=INDA/INGA
  * find related bank account of instructed agent
* 3.判断 related agent的地域特征   ---  Debit
  * 3.1.outport bank
  * 3.2.overseas branch
  * 3.3.local bank

## 2.2.2.channel = Chats

## 2.2.3.channel = XBFPS



## OBPU handler

user input in UI

|          | valueDay>current                                       | CPFG | key                                    | value  | user input                          |
| -------- | ------------------------------------------------------ | ---- | -------------------------------------- | ------ | ----------------------------------- |
| iw       | Y                                                      | C    | inwardBankMovementDetail --            | obpu   | ignore                              |
|          | excecute each every day, until value day = current day |      | ~~inwardGeneralLedgeRecord   (no)~~    |        |                                     |
|          |                                                        |      | inwardDebitLedgeRecord (Cash Debit)    | ledger | ignore                              |
|          |                                                        |      | ~~fixedInwardLedgeRecord   (no)~~      |        |                                     |
| iw(T)    | N                                                      | B    | inwardBankMovementDetail               | obpu   | ignore                              |
|          | save movement detail in additionnal data               |      | inwardGeneralLedgeRecord               |        | ignore                              |
|          |                                                        |      | inwardDebitLedgeRecord                 |        | ignore                              |
|          |                                                        |      | fixedInwardLedgeRecord                 |        | ignore                              |
| ow       | Y                                                      | C    | outwardBankMovementDetail              | obpu   | choose from user input and movement |
|          |                                                        |      | outwardGeneralLedgeRecord              |        |                                     |
|          |                                                        |      | outwardDebitLedgeRecord                |        |                                     |
|          |                                                        |      | fixedOutwardLedgeRecord                |        |                                     |
| ow       | N                                                      | B    | outwardBankMovementDetail              |        | choose from user input and movement |
|          |                                                        |      | outwardGeneralLedgeRecord   ( yes)     |        |                                     |
|          |                                                        |      | outwardDebitLedgeRecord  (bank Credit) |        |                                     |
|          |                                                        |      | fixedInwardLedgeRecord         (yes)   |        |                                     |
| ow-iw(T) |                                                        | B    | inwardBankMovementDetail (UPDATE)      |        | choose from user input and movement |
|          |                                                        |      | inwardGeneralLedgeRecord   ( yes)      |        |                                     |
|          |                                                        |      | inwardDebitLedgeRecord  (bank Debit)   |        |                                     |
|          |                                                        |      | fixedInwardLedgeRecord        (yes)    |        |                                     |



movenmentDetail key fields: account NO

ledger record key fields:

## bank relation account handler:

if (settlementMethod != INDA, INGA)

  pass directly



if (inward) {

  agentBic = instructing agent bic

  if (settlementMethod == INGA)

​    nostro = true      // N

​    flag = Credit Flag  +

  else if (settlementMethod == INDA)

​    nostro = false  // V

​    flag =  Debit Flag  

} else if (outward) {

  agentBic = instructed agent bic

  if (settlementMethod == INDA)

​    nostro = true  // N

  else if (settlementMethod == INGA)

​    nostro = false  // V

}



ibmBankCode = get_ibm_bank_code(agentBic)



if (ibmBankCode is blank)

  // failed (bank relation not found)



account = do_enquire(ibmBankCode, nostro, settlementCcy) // 

if (account == null)

  // failed (Nostro/Vostro account not found



## update bank position handler:







Debit / Credit Flag

* iw
  * INGA        Debit Flag       (intermediary bank account in instructing bank)            Nostro
  * INDA        Debit Flag       (instructing  bank account in intermediary bank)           Vostro

* ow
  * INGA       Credit Flag       (instructed bank account in intermediary bank)            Vostro
  * INDA       Credit Flag       (intermediary bank account in instructed bank)            Nostro

Nostro / Vostro Bank Indicator

```java
if (paymentDTO.getSettlementMethod() == INGA){
    noVostroFlag = "V";
    debitCreditFlag = CREDIT_FLAG.getValue();
}
else if (paymentDTO.getSettlementMethod() == INDA){
    noVostroFlag =  "N";
    debitCreditFlag = DEBIT_FLAG.getValue();
}

 /*switch (directionType) {
            case INCOMING : {
                switch (paymentDTO.getSettlementMethod()){
                    case INGA:
                        nostroVostroFlag = "N";
                        debitCreditFlag = CREDIT_FLAG.getValue();
                        break;
                    case INDA:
                        nostroVostroFlag =  "V";
                        debitCreditFlag = DEBIT_FLAG.getValue();
                        break;
                }
            }
            break;
            case OUTGOING:{
                switch (paymentDTO.getSettlementMethod()){
                    case INGA:
                        nostroVostroFlag = "V";
                        debitCreditFlag = CREDIT_FLAG.getValue();
                        break;
                    case INDA:
                        nostroVostroFlag =  "N";
                        debitCreditFlag = DEBIT_FLAG.getValue();
                        break;
                }
            }
        }*/
```

