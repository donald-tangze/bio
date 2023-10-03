##  pacs.008 Cove payment 

#### Scenario 1: one intermediary  **Reimbursement**  agent

SCBKUS6LXXX   ->  SCBKHKHHXXX  ->                                                            -> SCBKGB2XXXX   

​                                                                      | ->  SCBKCNBSSHA  

```
pacs.008              DebtorAgent        SCBKHKHHXXX   
                      CreditorAgent      SCBKGB2XXXX
                      reimbursement agent 1   SCBKCNBSSHA

pacs.009 cove         DebtorAsAgent      SCBKHKHHXXX  
                      DebtorAgent        SCBKCNBSSHA   
                      CreditorAgent      SCBKCNBSSHA
                      CreditorAsAgent    SCBKGB2XXXX 
                      Underlying Debtor          SCBKUS6LXXX        
                      Underlying Creditor        SCBKGB2XXXX   
```



#### Scenario 2: two intermediary  **Reimbursement**  agent (Case p.9.2.1)

SCBKUS6LXXX   ->  SCBKHKHHXXX  ->                                                            -> SCBKGB2XXXX   

​                                                            | ->  SCBKCNBSSHA   -> IRVTUS3NXXX

```
inward pacs.008              
                      Debtor
                      DebtorAgent        SCBKUS6LXXX          
                      Previous instructng agent
                      instructing agent  SCBKUS6LXXX
                      instructed agent   SCBKHKHHXXX  
                      intermediary agent 
                      CreditorAgent      SCBKGB2XXXX
                      creditor
                      
                     
outward pacs.008 (COVE)
                      Debtor                                    (same with iw 008's)
                      DebtorAgent        SCBKUS6LXXX            (same with iw 008's)
                      Previous instructng agent   SCBKUS6LXXX
                      instructing agent  SCBKHKHHXXX
                      instructed agent   SCBKGB2XXXX     
                      intermediary agent 
                      CreditorAgent      SCBKGB2XXXX            (same with iw 008's) 
                      creditor                                  (same with iw 008's)
                      -------
                      reimbursement agent 1   SCBKCNBSSHA  (user input)
                      reimbursement agent 2   IRVTUS3NXXX
                      
                     
pacs.009 cove         DebtorAsAgent      SCBKHKHHXXX     (pacs.008's instructing agent)
                      DebtorAgent        SCBKCNBSSHA     (pacs.008's reimbursement agent 1)
                      instructing agent  SCBKHKHHXXX     (pacs.008's instructing agent)
                      instructed agent   SCBKCNBSSHA     (pacs.008's reimbursement agent 1)
                      intermediary agent                                                     (pacs.008's reimbursement agent 2)
                      CreditorAgent      IRVTUS3NXXX     (pacs.008's reimbursement agent 2)  (pacs.008's reimbursement agent 3)
                      CreditorAsAgent    SCBKGB2XXXX     (pacs.008's instructed agent)
                      ----
```

​                            

#### Scenario 3: three intermediary  **Reimbursement**  agent

SCBKUS6LXXX   ->  SCBKHKHHXXX  ->                                                                                   -> SCBKGB2XXXX   

​                                                          |->  SCBKCNBSSHA -> IRVTUS3NXXX  ->  SCBKUS33XXX



```
pacs.008              DebtorAgent        SCBKHKHHXXX   
                      CreditorAgent      SCBKGB2XXXX
                      reimbursement agent 1   SCBKCNBSSHA
                      reimbursement agent 2   IRVTUS3NXXX
                      reimbursement agent 3   SCBKUS33XXX
                      
pacs.009 cove         DebtorAsAgent      SCBKHKHHXXX  
                      DebtorAgent        SCBKCNBSSHA   
                      CreditorAgent      SCBKUS33XXX
                      CreditorAsAgent    SCBKGB2XXXX     
                      IntermediaryAgent  IRVTUS3NXXX
```

##  pacs.009  adv payment 

####  Inward handler

> pacs.009 adv   --- MainStream
>
> pacs.009 (core)

#### create ow transaction user input:   

* 1.INGA/INDA:     pacs.009 adv ->  pacs.009 (core)       

use same payment service interface with  pacs.009 (core) -> pacs.009 (core)

​    TEST?

​    008 cove -> 008 cove    [N]

​    008 core -> 008 cove    [Y]

* 2.COVE:    pacs.009 adv ->  pacs.009 (adv)   + pacs.009 (core)              

  use same payment service interface with  pacs.009 (core) -> pacs.009 (core)

This process of pacs.009(ADV) is different from pacs.008(COVE), because pacs.009(ADV) need normal pacs.009 while  pacs.008(COVE) need pacs.009(COVE). Here need confirm logic flow.



* **3.pacs.009 -> pacs.009  adv** 

```
SCBKCNBSSHA  ->  SCBKHKHHXXX                              ->   IRVTUS3NXXX
                          ->  SCBKUS6LXXX   ->  SCBKUS33XXX                             
```

issue:

1. internal settlement method:  outward settlementMethod is null

   ![image-20230308191105379](C:\Users\donald\AppData\Roaming\Typora\typora-user-images\image-20230308191105379.png)

```
### 1.doesn't exist intermediary agent    payemnt create transaction
iw pacs.009           Debtor
                      DebtorAgent        
                      instructing agent  SCBKUS6LXXX
                      instructed agent   SCBKHKHHXXX  
                      CreditorAgent      SCBKGB2XXXX
                      Creditor  

  ++ ow pacs.009  adv      
                      Debtor                COPY
                      DebtorAgent           COPY default same as iw DebtorAgent   
                      Prev-instng-agent     SCBKUS6LXXX
                      instructing agent     SCBKHKHHXXX  
                      instructed Agent      SCBKGB2XXXX
                      creditor agent        SCBKGB2XXXX / (empty) -> same as instructed Agent
                      Creditor              COPY
                    ---manual change--
                      reimbursement agent 1   SCBKCNBSSHA   (user input)
                      reimbursement agent 2   SCBKCNBSSHA   (user input)

  ++ ow pacs.009 core     processor create through interface



### 2.exist intermediary agent  (Use Case p.9.1.2.b)
iw pacs.009           Debtor
                      DebtorAgent    
                      Prev_instg_agent
                      instructing agent     SCBKUS6LXXX
                      instructed agent      SCBKHKHHXXX  
                      intermediary agent    
                      creditor Agent        SCBKGB2XXXX
                      creditor

ow pacs.009  adv      
                      Debtor                                (iw 009's Debtor) 
                      DebtorAgent                           (iw 009's instructed agent ) 
                      Prev_instg_agent      SCBKUS6LXXX
                      instructing agent     SCBKHKHHXXX     (iw 009's instructed agent ) 
                      instructed Agent      SCBKGB2XXXX     (iw 009's creditor agent )
                      intermediary agent
                      creditor agent                        (iw 009's creditor agent )
                      creditor              SCBKGB2XXXX     (iw 009's Creditor) 
                      
                      reimbursement agent 1   SCBKCNBSSHA   (user input)
                      reimbursement agent 2   SCBKCNBSSHA   (user input)
                      
ow pacs.009 core          
                      Debtor                                (009 adv's Debtor)
                      DebtorAgent                           (009 adv's instructing agent)
                      Prev_instg_agent       
                      instructing agent     SCBKHKHHXXX     (009 adv's instructing agent)
                      instructed Agent      SCBKCNBSSHA     (009 adv's reimbursement agent 1)
                      intermediary agent                                                      (009 adv's reimbursement agent 2)
                      creditor agent        SCBKGB2XXXX     (009 adv's reimbursement agent 2) (009 adv's reimbursement agent 3)
                      creditor              copy            (009 adv's instructed agent)
```

## 流程图

```java
// create pacs.008
PaymentBizDelegate.createTransactionFromExistingPayment()  line: 450
   -- paymentItemService.retrievePayment()
   -- paymentItemService.createPayment()
   -- paymentProcessorClient.preCheckCreateTransactionPayment

[Payment Console UI]  User input
    
// submit (confirm) pacs.008    
[Payment Servcie] 
PaymentApiController.submitCustomerCreditTransfer
   -- convert(request -> paymentDTO)
PaymentBizDelegate.submitCustomerCreditTransfer()
   -- paymentService.validateCustomerCreditTransfer(payment, options);
      -- 在validate之后再赋值
   -- paymentProcessorClient.preCheckPayment() (first click confirm trigger)
   -- paymentItemService.updatePayment(payment)
   -- paymentProcessorClient.processPayment(payment, PAYMENT_PROCESSOR_OW_PAYMENT_CREATED, options);

[Processor]
   -- validation handlers
   -- SubmitToPaymentForSwiftSubmissionProcessingTool
   -- PaymentClientImpl.submitPaymentProcessingResult
    
[Payment Servcie]
PaymentMessageRouter.handleMessage
  paymentBizDelegate.handlePaymentProcessingResult
   -- paymentItemService.updatePayment(payment);
   // batch 1 -> batch 2
   -- paymentService.submitPayment(payment);
      -- create paymentInstruction
      // generate Raw Message
      -- maClient.submitSwiftMXMessage(paymentInstruction...);
      -- paymentProcessorClient.processPayment(payment, PAYMENT_PROCESSOR_OW_PAYMENT_SUBMIT_TO_SWIFT, null);

[SMXA Servcie]
  SMXABizDelegate.submitOutwardMessage()
      -- 
      
      
      
// create pacs.009   
PaymentBizDelegate.createTransactionFromExistingPayment()  line: 450
      -- paymentItemService.retrievePayment()
      -- paymentItemService.createPayment()
      -- paymentProcessorClient.preCheckCreateTransactionPayment
      
[Payment Console UI]  User input
    
      
// submit (confirm) pacs.009   
[Payment Servcie] 
PaymentApiController.submitFICreditTransfer()
   -- convert(FICreditTransferRequest -> PaymentDTO)
      
PaymentBizDelegate.submitFICreditTransfer()
   -- paymentService.validateFICreditTransfer(payment, options);
      --  -- 在validate之后再赋值
   -- paymentProcessorClient.preCheckPayment() (first click confirm trigger)
   -- paymentItemService.updatePayment(payment)
   -- paymentProcessorClient.processPayment(payment, PAYMENT_PROCESSOR_OW_PAYMENT_CREATED, options);

[Processor - batch 1]
   -- validation handlers
   -- SubmitToPaymentForSwiftSubmissionProcessingTool
   -- PaymentClientImpl.submitPaymentProcessingResult
    
[Payment Servcie]
PaymentMessageRouter.handleMessage
  paymentBizDelegate.handlePaymentProcessingResult
   -- paymentItemService.updatePayment(payment);
   // batch 1 -> batch 2
   -- paymentService.submitPaymentToSwift(payment);
      -- create paymentInstruction
      // generate Raw Message
      -- maClient.submitSwiftMXMessage(paymentInstruction...);
      -- paymentProcessorClient.processPayment(payment, PAYMENT_PROCESSOR_OW_PAYMENT_SUBMIT_TO_SWIFT, null);

[SMXA Servcie]
  SMXABizDelegate.submitOutwardMessage()
      -- 
```





## Issue:

Current Underlying Customer Creditor Transfer info are null  in pacs.009 cove.   Payment Service's Responsibility

            <UndrlygCstmrCdtTrf>
                <InstdAmt/>
            </UndrlygCstmrCdtTrf>