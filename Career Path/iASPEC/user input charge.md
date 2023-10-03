##  Task: user input charge 

#### 1.inward process

* save computed charge bearer, charge info, customized exchange info, settlement Method, value date in payment additional data. 

* Then manually create transaction can use these cached data.

```
Payment Additional Data Key:         value Class                Frontend use fields
COMPUTED_CHARGE_BEARER             : String                     charge bearer
CHARGE_INFO                        : ChargeInfoDTO              charges
EXCHANGE_DETAIL                    : CustomizedExchangeDetail   exchageDetail
STP_OUTWARD_SETTLEMENT_METHOD      : String                     settlementMethod
COMPULATED_VALUE_DATE
```

##### Responsibility of SettlementAmountLargerThanChargerMQHandler

move method code from ChargeAmountApiHandler here. 

* determineChargeAmountByAgentAndCountry
* calculateEquivalentChargeAmount

#### 2.  create transaction

##### (2.1) manually 

user click manually create transaction, payment service insert an outward payment record which copy fields value of inward payment. 

##### (2.2) stp create outward transaction



####  3.outward process

get charge info, exchange info from  payment additional data.

##### (1) Responsibility of ChargeAmountApiHandler: mainly be responsible for verify and transfer customized exchange info 

* verify customized exchange info in getCustomizedExchangeDetail(), Alert message when failed
* transfer customized exchange info into EXPU.ExchangeDetail
* verfiy if Charge Info DTO of SCBKHKHH  exist in Charges,  Alert message when failed

> if original Charge Bearer == Debt, then charges might don't need have SCBKHKHH, set charge Status = charged
>
> if original Charge Bearer != Debt, then charges must have SCBKHKHH, then set charge status = charged

issue  #172, 

##### (2) Responsibility of UpdateExchangePositionEXPUMQHandler

* prepare to send EXPU request: use ExchangeDetail of Step 1    

* create ledger record, use ExchangeDetail of Step 1

    Responsibility of UpdateExchangePositionEXPUMQHandler





#### 4.TEST

Inward Reference: 

HY8pgu9r75nfcCEe8vkVdYxjouVFevF0i0E

ALnRnVaha4efTl4fM7HKCU8WDifwlHblVqS
