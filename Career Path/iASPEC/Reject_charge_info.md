## Test Issue 20230418

### 1.Charge Administration

* 1.1.when charge type ="By Beneficiary Country", Country is must input field. Now country field is hidden, not be seen.

* 1.2.Remittance Type default value : "INTERMEDIARY", value: "outward" is not needed for current version.

* 1.3.In page "Charge Administration", Query Status default value: "Active"     Not Fixed

* 1.4.hide input field as below table  Not Fixed

  ![image-20230418121407625](C:\Users\donald\AppData\Roaming\Typora\typora-user-images\image-20230418121407625.png)

2.Reject Charge

* In app1, When default charge is set as USD dollar, remittance currency is HKD, if these two currency don't match, charge amount show "No items"

![image-20230418130107316](C:\Users\donald\AppData\Roaming\Typora\typora-user-images\image-20230418130107316.png)



## Test Issue 20230414

outward pacs.002测试改进点：
### 1.显示pop out box的charge Info

1.1.获取Reject Charge

* a.查询post调用doListChargeAdministration.action 
  Parameters:
  
  * remittanceType = "Intermediary"
  * chargeType="Reject Charge By Remitted Bank" 
  * Remitted Bank = instructedBankBIC
  
  Response:
  
  * First priority, check if there is currency = settlementCurrency. If existed, use this value
  * Second priority, check if there is currency = "HKD". If existed, use this value
  
* b.若a没找到，执行查询post调用doListChargeAdministration.action  
  Parameters:
  	a. chargeType="Reject Default" 

  Response:

  * First priority, check if there is currency = settlementCurrency. If existed, use this value
  * Second priority, check if there is currency = "HKD". If existed, use this value

* c.获取到Reject chargeInfo 之后，目前的reject charge的currency有三种情况

   * 1.与settlementCurrency相同，都是HKD

   * 2.与settlementCurrency相同，都不是HKD

   * 3.与settlementCurrency不同，settlementCurrency 不是HKD， 而Reject Charge是HKD

      理论上，三种情况下都查出来exchangeDetail，CurrencyExchangeAction的 retrieveCurrencyExchange方法。

      ```
      {
        "buySell": "BUY",
        "fromCurrency": "HKD",
        "toCurrency": "USD",
        "amount": 500
      }
      ```


1.2.显示Reject Charge

* 1.2.1.Reject charge  Currency与settlementCurrency相同，都是HKD

```
"chargeInfo":
{
    "amount": "100",      
    "currency": "HKD",   
    "chargeAgentBic": "SCBKHKHHXXX"  
},
"exchangeDetail":{ 
    "buyCurrency": "HKD",
    "buyAmount": 180,
    "sellCurrency": "HKD",
    "sellAmount": 180,         
    "valueDate": "2023-04-11",
    "exchangeRateForBuyVsSellCurrDisplay": "800",   
    "exchangeRateForBuyVsSellCurrCompute": 8.0,     
    "spotOrForwardExchangeIndicator": "S"
}
```

**Customer Charger Currency**: HKD  100  [chargeInfo.currency]   [chargeInfo.amount] 

**HKD Equivalent**:   

**Exchange Rate**:   

* 1.2.2.Reject charge  Currency与settlementCurrency相同，都不是HKD

```
"chargeInfo":
{
"amount": "22.5",      
"currency": "USD",   
"chargeAgentBic": "SCBKHKHHXXX"  
},
"exchangeDetail":{
    "buyCurrency": "USD",
    "buyAmount": 22.5,
    "sellCurrency": "HKD",
    "sellAmount": 180,         
    "valueDate": "2023-04-11",
    "exchangeRateForBuyVsSellCurrDisplay": "800",   
    "exchangeRateForBuyVsSellCurrCompute": 8.0,     
    "spotOrForwardExchangeIndicator": "S"
}
```

**Customer Charger Currency**:  USD   22.5    [chargeInfo.currency]   [chargeInfo.amount] 

**HKD Equivalent**:   180    [exchangeDetail.sellAmount]

**Exchange Rate**:     8.0     [exchangeDetail.exchangeRateForBuyVsSellCurrCompute]



* 1.2.3.Settlement Currency不是HKD, Charge Currency 是HKD

  ```
  "databaseChargeInfo":
  {
      "amount": "180",      
      "currency": "HKD",   
      "chargeAgentBic": "SCBKHKHHXXX"  
  },
  "chargeInfo":
  {
      "amount": "22.5",      
      "currency": "USD",   
      "chargeAgentBic": "SCBKHKHHXXX"  
  },
  "exchangeDetail":{
      "buyCurrency": "USD",
      "buyAmount": 22.5,
      "sellCurrency": "HKD",
      "sellAmount": 180,         
      "valueDate": "2023-04-11",
      "exchangeRateForBuyVsSellCurrDisplay": "800",   
      "exchangeRateForBuyVsSellCurrCompute": 8.0,     
      "spotOrForwardExchangeIndicator": "S"
  }
  ```

  **Customer Charger Currency**:  USD     22.5    [chargeInfo.currency]   [chargeInfo.chargeAgentBic] 
  
  **HKD Equivalent**: 180    [exchangeDetail.sellAmount]
  
  **Exchange Rate**:    8.0    [exchangeDetail.exchangeRateForBuyVsSellCurrCompute]
  
  

1.3.用户手动输入值

* 用户可在**HKD Equivalent**手动输入新值，每次输入后，用户需要点击check button调用货币汇率兑换接口，将港币转换成汇款单中的货币。这里输入后可以将chargeInfo 和ExchangeDetail 清空，要求用户点check button。

* 港币转港币也需要调用一次。参考TransactionDetail页面的js，在payment-console，CurrencyExchangeAction的 retrieveCurrencyExchange方法

  ```json
  {
    "buySell": "BUY",
    "fromCurrency": "HKD",
    "toCurrency": "USD",
    "amount": 500
  }
  ```


### 2.**Reject** 的pop out box 点击confirm前js校验

confirm前check:

* Reject Reason Code不能为空

* charge Info不能为空, Charge Amount可以为0

* 如果settlementCurrency != charge amount Currency, exchange Detail 不能为空，提示“Current HKD Equivalent is not checked!”

### 3.Refer to pacs.002 payment detail UI screen

3.1.字段Additional Information 使用2个输入框，每个输入框一行。

3.2.Add one input column "proprietary",  

3.3.Remove Payment Status的Payment Progress 输入框



## Reject Charge Details

1. When user reject pacs.002, pop out an input box, add a Reject charge column in this box. Show value using default value from charge type: "Rejecte Charge By Remitting Bank", if there is no value, leave it blank. User could change default value to positive number. Here the charge column are same with that of payment detail page.

* chargeAgentBic default value is "SCBKHKHHXXX", don't need to input。 
* currency and amount value are default value from charge management table. query by type: "Rejecte Charge By Remitting Bank", if there is no value, leave it blank. 

![Reject_Charge](C:\Users\donald\Desktop\Reject_Charge.png)



2. After user confirm pop out box,  add reject charge into paymentDTO.additional Data, instead of paymentDTO.charges. Saving format sample are like below.  

{key: value} is {PaymentAdditionalDataKey.CHARGE_INFO :  com.iaspec.ecph.payment.dto.ChargeInfoDTO}

{PaymentAdditionalDataKey.EXCHANGE_DETAIL:  com.iaspec.ecph.paymentprocessor.dto.EXPUUpdateExchangeMovementOfTreasurySystemDTO.ExchangeDetail}

```
"chargeInfo":
{
"amount": "30",      ---- Customer Charge Amt
"currency": "HKD",   ---- Customer Charge Currency
"chargeAgentBic": "SCBKHKHHXXX"  ---- 固定值
},
"exchangeDetail":{
    "buyCurrency": "USD",
    "buyAmount": 22.5,
    "sellCurrency": "HKD",
    "sellAmount": 180,         --- HKD Equivalent
    "valueDate": "2023-04-11",
    "exchangeRateForBuyVsSellCurrDisplay": "800",   
    "exchangeRateForBuyVsSellCurrCompute": 8.0,     ---- Exchange Rate
    "spotOrForwardExchangeIndicator": "S"
}
```

3. In pacs.002 detail page, show same reject charge info. And disable user input, that is to say. charge info are only for view, not for editing.

   ![image-20230412143931851](C:\Users\donald\AppData\Roaming\Typora\typora-user-images\image-20230412143931851.png)

   

