set value when create payment return.

### 1.Direct Return  pacs.008 -> pacs.004

~~~
PaymentBizDelegate.createPaymentReturnFromExistingPayment()  line: 793
   -- PaymentUtils#convertInwardRemittanceToOutwardReturn()  line: 1103
~~~

  1.1. InternalSettlementMethod:  get from 008 additional_date key "internalSettlementDetails" 

```
+ a.inwardSettlement 
  keep unchanged

+ b.OutwardSettlement      remove old value, set new value: 
  + bank code = a.inwardSettlement bank code
  + settlement Date = current date
  + InternalSettlementDetailDTO.InternalSettlementMethod: 
  internalSettlementDetailDTO=inwardSettlement.InternalSettlementDetailDTO 
  eg: inward "NOSTRO" -> outward "NOSTRO"
      inward "VOSTRO" -> outward "VOSTRO"
      inward "SUNDRY" -> outward "SUNDRY"
      inward "SYSTEM_DETERMINED"/NULL -> outward "SYSTEM_DETERMINED"/NULL
     
```

### 2. Forward Return with receiving pacs.004

Similar with when create out pacs.008 from iw pacs.008, copy fields from iw pacs.008 additional_data

~~~
PaymentBizDelegate.createPaymentReturnFromExistingPayment()  line: 814
   -- PaymentUtils#convertInwardRemittanceToOutwardReturn()  line: 1103
~~~

  1.1. set ow 004 settlement day: get from iw 004 additional_date key: "computedValueDay" 

```
outPayment.setSettlementDay(MapUtils.getObject(iwPayment.getAdditionalData, "computedValueDay"))
```

  1.2. set  ow 004  settlementMethod: get from 004 additional_date key: "stpOutwardSettlementMethod" 

```
outPayment.setSettlementMethod(MapUtils.getObject(iwPayment.getAdditionalData, "stpOutwardSettlementMethod" ))
```

  1.3. copy to ow 004 internalSettlementDetails in addition_data from 004 additional_date key "internalSettlementDetails"

```
InternalSettlementDetails internal = MapUtils.getObject(iwPayment.getAdditionalData, "internalSettlementDetails"）；
outPayment.addAdditionalData("internalSettlementDetails", internal);
```

  1.4. set ow 004  charges, get from 004  additional_date key: "chargeInfo" 

```
-- PaymentUtils#convertInwardRemittanceToOutwardReturn()  line: 1029
outPayment.addCharge(MapUtils.getObject(iwPayment.getAdditionalData, "chargeInfo"))
```

  1.5. set ow 004  Charge Bearer: get from 004  additional_date key: "computedChargeBearer"

```
outPayment.setChargeBearer(MapUtils.getObject(iwPayment.getAdditionalData, "computedChargeBearer"))
```

  1.6. copy to ow 004 exchangeDetail in addition_data: get from 004 additional_date key: "computedExchangeDetail" 

```
-- PaymentUtils#convertInwardRemittanceToOutwardReturn()  line: 1010
out.putAdditionalData(PaymentAdditionalDataKey.EXCHANGE_DETAIL,
				MapUtils.getObject(in.getAdditionalData(), PaymentAdditionalDataKey.COMPUTED_EXCHANGE_DETAIL));
out.putAdditionalData(PaymentAdditionalDataKey.COMPUTED_EXCHANGE_DETAIL, null);
```

1.7. copy to ow  ow 004 originalChargeBearer in addition_data: get from 004  "chargeBearer " 

```
-- PaymentUtils#convertInwardRemittanceToOutwardReturn()  line: 1005
out.putAdditionalData(PaymentAdditionalDataKey.ORIGINAL_CHARGE_BEARER, in.getChargeBearer());
```

###  3.Completed Return without receiving 004

  1.1. InternalSettlementMethod:  get from 008 additional_date key "internalSettlementDetails" 

```
+ a.inwardSettlement 
	null
	
  (copy ow 008 message's outward settlement method
  * bank code  - unchanged
  * settlement - method unchanged
  * amount     - Returned instructed amount
  * value date - user input
  
+ b.OutwardSettlement      remove old value, set new value: 
  copy ow 008 message's inward settlement method
  * bank code  - unchanged
  * settlement - method unchanged
  * amount     - Returned settlement amount
  * value date - LocalDate.now()
```

Processor supplement amount and value date after user input and confirm before save database
