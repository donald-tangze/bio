## XBFPS Status Diagram

AML Status                                         Pending   ->  Passed  ->   Failed

Ledger Tx Status (Balance Status)        UNPOSTED   ->    ON_HOLD      ->   Forwarded

Verification Status   skipped



# Remark

FPS Server IP of Leo: 10.3.80.132

* xb-fps:   10.3.80.132:8080/xb-payment/

* ICL:         10.3.80.132:8080/hkicl-simulator/toBank

FPS Server IP 2:   10.3.60.49:28080



## new features, add two channel:

###  1. Cross-board FPS

####  (1) Business Requirement

##### 1.1 *process pacs.008:  (xb-fps in - swift out)

 xb-fps pacs.008 in,  then swift  pacs.008 out

> 1. When Inward cross-border fps message sent out  from ECFPS,  XML raw message would be sent to payment Hub SMXA service through Web Service.
>
> 2. Then SMXA service save this remittance XML text into database table, parse XML into payment Object, pass Object through Redis Queue message into Payment Service, Processor service. Processor handler use existing handle event  to validate the same payment Object in inward process, 
> 3. manually or automatic create an outward transaction payment in outward process.

* Event: PAYMENT_PROCESSOR_IW_PAYMENT_RECEIVED 

  (reuse existing event)
  
  NotifyFpsReceivedHandler    notify fps that ppr that have received. 
  AdditionalData key: xbfps_id  +  OnHoldReprocess:  sendSupplementaryInfo
  suceess once, then skip.   
  // might be put in processingTools or outward handler 

> 1. adjust logic, skip below handlers: 
>
>    ```txt
>    Need to do incomingAMLResultMQHandler, if failed, similar to Swift 008
>             
>    //use channel flag, when messageChannel==xbfps, skip below inward handlers
>    incomingBankRelatedAccountsApiHandler;  (MUST)  
>    updateInwardBankPositionOBPUMQHandler;  (skip)       G/L A/C use same account number
>    settlementAndBalanceMQHandler;          (skip)
>                        
>    determineOwBankRelatedAccountApiHandler (skip)
>             
>    <ref bean="incomingHKDEquivalentAmountCalculationHandler" />   (Reserved)
>    <ref bean="intermediaryBankCheckSelfHandler" />     
>    <ref bean="incomingBankRelatedAccountsApiHandler" />
>    add method queryAccountByClearingSystem in adminClientImpl,clearingSystem + memberId  (PPRBankMasterDTO)
>    TACBTWTPXXX
>    DKGCHKHHXXX 
>    <ref bean="updateInwardBankPositionOBPUMQHandler" />
>    <ref bean="stpSwitchApiHandler" />
>    <ref bean="futureValueDateSelfHandler" />
>    incomingAMLResultMQHandle;  
>    <ref bean="sTPAndCutOffTimeApiHandler" />
>    <ref bean="holidaySettingExistApiHandler" />
>    <ref bean="adverseWeatherApiHandler" />
>    <ref bean="outgoingChannelSelfHandler" />
>    <ref bean="checkMessageFieldsValidSelfHandler" />
>    <ref bean="sTPAmountLimitMQHandler" />
>    <ref bean="settlementAmountLargerThanChargerMQHandler" />
>    chargeBearer changed
>    <ref bean="settlementAndBalanceMQHandler" />
>    chargeBearer changed
>    <ref bean="agentExceptionListApiHandler" />
>    <ref bean="sTPCurrencyScopeApiHandler" />
>    <ref bean="restrictedCountryScopeApiHandler" />
>    <ref bean="duplicatePaymentApiHandler" />
>    <ref bean="creditorAndDebtorSelfHandler" />
>    <ref bean="investigationCheckApiHandler" />
>    <ref bean="incomingAMLResultMQHandler" />
>    <ref bean="nextAgentInstructionExistSelfHandler" />
>    <ref bean="determineOwBankRelatedAccountApiHandler" />
>    <ref bean="determineHandlingStatusSelfHandler" />
>    /**
>    * 1. How to deduct charge amount? still deduct charge amount from transaction amount and currency.
>    * 2. Is charge amount calculation rule same with swift message?
>    */
>    ```

* Event: PRE_CHECK_CREATE_TRANSACTION    (only applicable for manual create)

  ~~~xml
  <ref bean="determineValueDateApiHandler" />
  <ref bean="updateOrCheckSettlementMethodHandler" />
  ~~~

* Event: PRE_CHECK_OW_PAYMENT                   (only applicable for  manual create)

  ~~~xml
  <ref bean="validCharacterSelfHandler" />
  <ref bean="hostSystemReadinessMQHandler" />
  <ref bean="outgoingHKDEquivalentAmountCalculationHandler" />
  <ref bean="updateOrCheckSettlementMethodHandler" />
  <ref bean="checkChargeAmountApiHandler" />
  <ref bean="codeWordApiHandler" />
  ~~~

* Event: PAYMENT_PROCESSOR_OW_PAYMENT_CREATED

  (reuse existing event)

  ~~~xml
  // Also for incoming xb-fps message, outgoing swift message, need to do same logic with transaction
  <ref bean="hostSystemReadinessMQHandler" />
  <ref bean="outgoingHKDEquivalentAmountCalculationHandler" />   Y
  <ref bean="validCharacterSelfHandler" />             Y
  <ref bean="determineValueDateApiHandler" />          Y
  <ref bean="updateOrCheckSettlementMethodHandler" />  Change, inward settlementMethod would be null? {same account, date, method(clearing house:ICL)}
  <ref bean="checkChargeAmountApiHandler" />           Change rule same with swift, deduct 
  <ref bean="checkOwBankRelatedAccountApiHandler" />    Y
  <ref bean="updateOutwardBankPositionOBPUMQHandler" /> Y
  <ref bean="updateExchangePositionEXPUMQHandler" />    Y
  <ref bean="effectReqStatusSTSUMQHandler" />           Change<!-- bankReference as MSGKEY -->
  <ref bean="camt054NeededApiHandler" />                Y
  <ref bean="codeWordApiHandler" />                     Y
  <ref bean="determineOwHandlingStatusSelfHandler" />   Y
  ~~~

* PAYMENT_PROCESSOR_OW_PAYMENT_SUBMIT_TO_SWIFT

  (reuse existing event)
  
  

#####  1.2 process pacs.004 (xb-fps in - swift out)

xb-fps pacs.004 in,  then pacs.004 out, same with 1.1 pacs.008

After receiving pacs.004, processor handler, then set status to  Outstanding_for_review

* iw-received         Event Type: PAYMENT_PROCESSOR_IW_PAYMENT_RETURN_RECEIVED     
  * match xb-fps pacs.008 message

* create outward pacs.004 of swift, based on original swift pacs.008 message
  * manually create outward pacs.004 message





##### 1.3 process pacs.008  (swift in - xb-fps out)     Test

swift  pacs.008 in,  then xb-fps pacs.008 out

* Event: PAYMENT_PROCESSOR_IW_PAYMENT_RECEIVED 

  (reuse existing event)

* Event: PRE_CHECK_CREATE_TRANSACTION    (only applicable for  manual create)

  ~~~
  <ref bean="determineValueDateApiHandler" />
  <ref bean="updateOrCheckSettlementMethodHandler" />
  ~~~

* Event: PRE_CHECK_OW_PAYMENT                   (only applicable for  manual create)

  ~~~xml
  <ref bean="validCharacterSelfHandler" />
  <ref bean="hostSystemReadinessMQHandler" />
  <ref bean="outgoingHKDEquivalentAmountCalculationHandler" />
  <ref bean="updateOrCheckSettlementMethodHandler" />
  <ref bean="checkChargeAmountApiHandler" />
  <ref bean="codeWordApiHandler" />
  ~~~

* Event:  **OUTWARD_XBFPS_TRANSACTION_CREATED**, instead of PAYMENT_PROCESSOR_OW_PAYMENT_CREATED    batch 1+ batch 2  -->  NEW event

  inward change little，outward batch 1 change a lot.

  ```
  // Question:
  // How to determine which outward channel a incoming message should send?  swift or xb-fps (tbc) inward handler set field destinationChannel (or user input in create )
  ```

  ~~~xml
  // Also for incoming xb-fps message, outgoing swift message, need do same logic with transaction
  <ref bean="hostSystemReadinessMQHandler" />
  <ref bean="outgoingHKDEquivalentAmountCalculationHandler" />   Reserve
  <ref bean="validCharacterSelfHandler" />              Reserve
  <ref bean="determineValueDateApiHandler" />           Reserve
  <ref bean="updateOrCheckSettlementMethodHandler" />   Change, outward settlementMethod would be null? no
  <ref bean="checkChargeAmountApiHandler" />            Reserve  according to bic code. Master file
  <ref bean="checkOwBankRelatedAccountApiHandler" />    Reserve
  <ref bean="updateOutwardBankPositionOBPUMQHandler" /> Reserve
  <ref bean="updateExchangePositionEXPUMQHandler" />    Reserve
  <ref bean="effectReqStatusSTSUMQHandler" />           Change
  <ref bean="camt054NeededApiHandler" />                SKIP
  <ref bean="codeWordApiHandler" />                     SKIP
  <ref bean="determineOwHandlingStatusSelfHandler" />   Reserve
  ~~~

* **Event: OUTWARD_XBFPS_TRANSACTION_BATCH2** instead of PAYMENT_PROCESSOR_OW_PAYMENT_SUBMIT_TO_SWIFT

  outward batch 2 change a lot. create a new event for PAYMENT_PROCESSOR_OW_XB_PAYMENT_CREATED

~~~xml
<ref bean="hostSystemReadinessMQHandler" /> Delete
<ref bean="writeMsg2HostWMSGMQHandler" />   Replace
<ref bean="submitAMLCheckMQHandler" />      Delete
<ref bean="outgoingAMLResultMQHandler" />   Replace 
<ref bean="vostroBalanceQOBDMQHandler" />   Delete
<ref bean="checkApprovalStatusSelfHandler" />  Reserve 
<ref bean="release2SwiftAMSGMQHandler" />      Replace
<ref bean="swiftAckStatusQSTSMQHandler"/>      Delete
~~~

* interface1: /xbCreditTransfer     

  > equivalent to writeMsg2HostWMSGMQHandler
  >
  > response: 
  >
  > 1.status = "success"  or  != "success";  2.paymentId
  >
  > save raw message cross border fps in database.  

* interface2: /reprocessXbPaymentTransaction    Reprocess the cross-border payment transaction 

  ```
  repostOnHoldXbPaymentPOST
  ```

  > * query AML result:  equivalent to  CheckAMLResultMQHandler
  >
  >   request: paymentId (162) + option1
  >
  >   response:  amlStatus(enum) + status
  >
  > * release to  host: equivalent to release2SwiftAMSGMQHandler
  >
  >   request: paymentId (162) + option2
  >
  >   response:  status = "success"  or  != "success";  

* interface 3: /deleteTx    delete outstanding outward transaction to xb-fps

  > equivalent to resetReqStatusSTSUMQHandler
  >
  > request:
  >
  > response: 

* Query Status: QUERY_SUBMISSION_STATUS

  interface: /retrieveXbPayment

##### 1.4 *process pacs.004   (swift in - xb-fps out)  

swift pacs.004 in,  then xb-fps pacs.004 out.  inverse of point 1.1

* xb-fps 



swift pacs.008 send to fps successully  1.3

Task: edit outward pacs.008

  (Alpha) contact Public Bank click return after receiving SCB's xb-fps pacs.008 , send pacs.004 back  from Public Bank's fps    1.2

​                                        



#### (3) Test Result

##### Compare fps in - swift out with swift in - swift out

1.for inward cross border remittance, Transaction Reference, OSN Number and Finnet Session Number are absent

2.Considering cross border FPS remittance have done settlement, please kindly confirm if it is right that inward processor handlers won't do  below processes:

(inward) Check if settlement done or balance sufficient; 

(inward) Check if AML hit;   

(inward) Update bank position for settlement;

(outward) Update incoming request status

3.For cross border FPS remittance settled by HKICL clearing system, would you provide what are related bank account and Ledger account  for saving and generating ledger record files?

4.When Update incoming request status, transaction reference is must parameters,  what would it be for cross border remittance?

#####  Compare swift  in - fps out with swift in - swift out

where to save XML raw message, need request smxa save remittance service.

#####  Compare Chats in - swift out with swift in - swift out

Payment-hub integrate with Host for swift message according to MQ written in PPR Interface Specification, then whether this specification would apply to Chats message?  When payment-hub integrate with Host for Chats message, to what extent current interface request parameters and response parameters would change?  Currently we expect only preliminary conclusion for designing and implementing.

###  2. CHATS

2023

###  3. Selection of Outgoing Channel

refer to Functional Requirement Spec 2.1.1  Selection of Outgoing Channel

cross border fps: HKD/RMB

CHATS: HKD/RMB/EUR/USD

SWIFT: HKD/RMB/EUR/USD/JPY/AUD......15+

\-     Instructed Bank registered with FPS

> Master bank files

\-     Internal Priority – such as the cost of the selected channel

  

 Attached is stress test result. At that time,  we  get a minimum concurrent volume: around 150-200 remittance            per hour under current circumstance. in one server



### 4.TODO

#### 1.Priority High: Conversion between ICL member Id and Swift BIC code



#### 2. XML Raw Message

Send transfer request message to xbfps server, xbfps replied xb fps XML text.  processor need to save in DB <ECPH_REMIT_INST_TBL>

messageId: MSG20221223143345245

swiftOSN:  225251

#### 3.XbfpsClientImpl.xbPaymentReturn

supplement request fields:  including all fields user input in UI

charges, etc



#### 4.when received swift return pacs.004 message, match swift pacs.008 transaction. Verify if this pacs.004 is valid. Confirm Match rule



#### 5. when received xbfps return pacs.004 message, match xbfps pacs.008 transaction. Verify if this pacs.004 is valid. What's Match rule? 

in ID    -   Return ID       Settlement_Amount

22825  -  22830  

22817  -  22829                       4500

22818  -  22838                       4600
22880  -  22895                       6300

22903  -  22904                       7800

22879  -  

22902  -  



in id   -    outward ID

22868  -  22869                       2399

22880  -                                    6300



## **FRN20221229PAYX02PM100806** 

PPSS2212290253

inward 22996          reject 



```txt

1.create outward pacs.008
PaymentBizDelegate.createTransactionFromExistingPayment
paymentItemService.createPayment   ->
paymentDAO.save

2.confirm outward pacs.008
operateRemittanceAction.confirm  -> 
xbPaymentBizDelegate.submitCustomerCreditTransfer   -> 
xbPaymentService.submitCustomerCreditTransfer  ->

paymentApiController.submitCustomerCreditTransferPOST  ->
paymentBizDelegate.submitCustomerCreditTransfer   ->
paymentItemService.updatePayment   ->
paymentDAO.save

3.create outward return pacs.004

PaymentBizDelegate.createPaymentReturnFromExistingPayment
paymentItemService.createPayment   ->
paymentDAO.save

4.confirm outward return pacs.004
operateRemittanceAction.confirm  -> 
xbPaymentBizDelegate.submitCustomerCreditTransfer   -> 
xbPaymentService.submitCustomerCreditTransfer  ->
paymentApiController.submitPaymentReturnPOST  ->

paymentBizDelegate.submitPaymentReturn   ->
  paymentItemService.updatePayment   ->
  paymetnProcesslientImpl.processPayment
  paymentItemService.submitPaymentReturn   ->

```



issue 11: when confirm outward return message from existing inward remittance, add PRE_CHECK_OW_PAYMENT logic in Console.// ZhangPeng

```
@POST
@Path("/preCheckOutwardTransaction")
public InternalMessageResult preCheckOutwardTransactionPOST(InternalMessage request);


PRE_CHECK_OW_PAYMENT
PRE_CHECK_OW_RETURN
```

issue 12: when create outward return message from existing inward remittance, add PRE_CHECK_CREATE_TRANSACTION   logic in Payment and Processor.// Donald

```
PRE_CHECK_CREATE_TRANSACTION
```



"ecph.stp.cut-off-time.xbfps"