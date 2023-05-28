## Instant/Inward Return 004

1.intermediaryBankCheckSelfHandler

```
if (payment.getIsCreditorAsAgent() == TRUE) {
	getCreditorAsAgentBic == getInstructedAgentBic
}
else {
	getCreditorAgentBic ==  getInstructedAgentBic
}
```

1.1 matchOriginalTransactionApiHandler     

1. find original transaction by 
2. determine original message type, put it in additional Data,  Key:value 

2.SearchIwBankRelatedAccountsApiHandler*

settleMethod  + instructing BIC -> bankAccount

intermiediary  find bank account same with 008,009



3.updateInwardBankPositionOBPUMQHandler

>  bankAccount ->

4.CutOffTimeApiHandler

```
// replace swift cut off time by generic source Channel
```

5.outgoingChannelSelfHandler

currency  + instructed agent bic  

6.checkMessageFieldsValidSelfHandler        

```
payment.getMessageType()   -> getType()
```

7.sTPAmountLimitMQHandler 

```
SettlementAmount + SettlementAmountCurrency

getMessageType -> getType()    

original message type 009, original payment type == 009 skip
original message type 008, original payment type == 008 continue compare 
```

8.settlementAmountLargerThanChargerMQHandler

```
getMessageType -> getType()    
1.calculate charge amount 

```

9.settlementAndBalanceMQHandler*          

 ```
bankAccount
// rerun  little change from 008
SettlementEntry =  settlementServiceApi.listSettlementEntryPOST // todo interface update 
 ```

10.agentExceptionListApiHandler              
11.sTPCurrencyScopeApiHandler      

```
channel: swift chats fps
```

12.restrictedCountryScopeApiHandler       

>  no change



duplicatePaymentApiHandler              

```
return doesn't have debtorAccount, creditorAccount  
no change
```

creditorAndDebtorSelfHandler          

>  return doesn't have debtorAccount, creditorAccount  

investigationCheckApiHandler             

incomingAMLResultMQHandler            

nextAgentInstructionExistSelfHandler      

>  return doesn't have nextAgentInstruction

determineOwBankRelatedAccountApiHandler*  

>  instructedAgentBic -> OwBankRelatedAccount

determineHandlingStatusSelfHandler        



## Instant remittance return

handle some necessary fields when User create Return Transaction  including direct Return and Completed Return.

####  Direct Return  pacs008 -> pacs.004

~~~
PaymentBizDelegate.createPaymentReturnFromExistingPayment()  line: 793
   -- PaymentUtils#convertInwardRemittanceToOutwardReturn()  line: 1103
~~~

  1.1. Value day:    default current day.   Processor set value,  computer one more time in pre-create-transaction

  1.2. settlementMethod: opposite with 008 settlement method

  1.3. InternalSettlementMethod:  get from 008 additional_date key "InternalSettlementMethod " 

  1.4. charge, Processor set value,    computer one more time in pre-create-transaction

  1.5. Charge Bearer: default SHARE

  1.6. Exchange Info: null

```
+ a.inwardSettlement 
  keep unchanged

+ b.OutwardSettlement      remove old value, set new value: 
  + bank code = a.inwardSettlement bank code
  + settlement Date = current date
  + Nostro/Vostro Flag= opposite of inwardSettlement   
```

#### Completed remittance Return

Similar with when create out pacs.008 from iw pacs.008, copy fields from iw pacs.008 additional_data

~~~
PaymentBizDelegate.createPaymentReturnFromExistingPayment()  line: 814
   -- PaymentUtils#convertInwardRemittanceToOutwardReturn()  line: 1103
~~~

  1.1. Value day: get from 004  additional_date key: "computedValueDay" 

  1.2. settlementMethod: get from004  additional_date key: "stpOutwardSettlementMethod" 

  1.3. InternalSettlementMethod: get from 004 additional_date key "InternalSettlementMethod  

  1.4. charge fields, get from 004  additional_date key: "chargeInfo" 

  1.5. Charge Bearer: get from 004  additional_date key: "computedChargeBearer"

  1.6. Exchange Info: get from 004  additional_date key: "exchargeInfo" 

  1.7. copy additional_date key "original Charge Bearer" from 004  Charge Bearer



OW Transaction: PPSS2302221432

inward 004:  SW230222170448

outward 004:  PPSS2302221435



###  PAYMENT_PROCESSOR_IW_PAYMENT_RETURN_RECEIVED

  search values logic, save in add_data

\1. Mater Payment Id, from original ow payment Id

\2. then find iw payment id, get Instructing Agent BIC

\3. charge fields, calculate charge

\4. settlementMethod

MasterPaymentId: from original ow payment Id

