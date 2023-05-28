配置变动统计

1.MTInvestigation.hbm.xml          investigation service

2.cron-expression.properties       admin service

3.confirm if sql change.     no

 

修改payment-console的redis.xml

## 1. Queries and Investigation

### MTn95/n96/n99     (Queries) / (Answer to Queries)  / (Free Format Message)

> Include MT195/196/199,  MT295/296/299,  they are different message under Category 1xx, 2xx respectively.

SW230412A02741

Invalid message fields  (G00004)

ServiceException: failed to invoke API    (G00009)

ServiceException: invoked API and message failed to be saved     (G00009)

IOException:  failed to read file (G00015)

###  1.2 pacs.002    Reject

**SW230112143940**

```text
//create outward pacs.002   status report

OperateRemittanceAction.requestReject
XbPaymentBizDelegate.requestReject
MakerCheckerServiceImpl.createMakerRequest

<payment>
PaymentAdminBizDelegate.updateTransactionStatus
MessageAdapterClientImpl.submitSwiftMXMessage
redisMessageDispatcher.submitSwiftMXMessage

<smxa>
SMXABizDelegate.submitOutwardMessage
messageConversionService.convertToMessage
```

### 1.3 CAMT.056 / CAMT.029   Cancellation

CAMT.056 / CAMT.029     (Payment Cancellation)   (Resolution of Investigation)





##  2.Integration Test

### 1. Scheduler job scan directory regularly, read MT message from TXT file. 

Trigger 

###  2. Transfer incoming MT message to SMTA

```
queue="${redis.sync-list.receive-in-swift-mt}"
```

no Handler

###  3. Send out Outward Query Message

Processor generate QueryDTO, invoke SMTA interface to get Raw Message, and write it to Host.

```
queue="${redis.sync-list.submit-out-swift-mt}"
```

three Handlers

###  4.CheckInwardMTMessageHandler

PaymentDTO

MT103, MT202           verify

others                          not applicable