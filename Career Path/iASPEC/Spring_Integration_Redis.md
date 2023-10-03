

### [Redis shell](https://redis.io/commands/hgetall/)

```shell
redis-cli -u redis://user:pass@host:port
redis-cli -u redis://:foobared@10.3.60.47:6379

redis-cli -h 10.3.60.47 -p 6379 -a foobared

hash list queue
HGETALL key 
hget key field

// redis 监控
info [-operation]
operation: memory, cpu, 
```

Redis 的使用包含[spring-data-redis](https://docs.spring.io/spring-data/data-redis/docs/current/reference/html/) and spring-integration-redis. 前者是作为内存数据库，后者是作为消息队列，

问题：

1. 前者使用数据结构是String 和Hash,  消息队列使用的是redis数据结构List
2. 前者保存数据时，没有设置过期时间。也没有删除数据。 redisTemplate.expire(key,  expired Timeout)
3. redis数据储存使用容量100MB, 是否能根据数据类型来判断使用容量。
4. settlement ，scenario of CAMT.054: processor (api)-> settlement(write redis) -> SMXA(write redis) -> processor(read redis)
5. 微服务监控   快速定位是哪个链条环节出错。   通过日志ELK(elastic search + logstash + kibana)
6. 查看与redis存在连接的服务，比如settlement是否存在redis 连接
7. inject RedisTemplate, similar with HashOperations





```
payment reference:PPSS2303183804 

swift reference: 
wmsgMurLinkKey=6357cc8b-0588-4735-ad53-eea992d916c4,
MESSAGE_REFERENCE=M000202303181245450000003703

settlement did invoke processor through redis interface.
processor没有收到 settlement发的message.

redis has only one mur.



2023-03-18 00:45:45.589 [settlementMsgRouterExecutor-4] [SystemLogger] DEBUG -  () PaymentProcessorClientImpl.submitPaymentSettlementResult#start - settlement=[SettlementEntryDTO[acctId=2880002219, acctOwner=BOSHCNSHXXX, acctServicer=SCBKHKHHXXX, acctServicerReference=PPSS2303183804, additionalData={incomingMessageKey=SW230318004407, wmsgMurLinkKey=6357cc8b-0588-4735-ad53-eea992d916c4, paymentVersion=0, MESSAGE_REFERENCE=M000202303181245450000003703}, clientReqId=1679064150852890, clientSysId=SWIFT, clientUsrId=SWIFT, createUser=PPR, creationDatetime=2023-03-18T00:45:43.263, creditDebitIndicator=CREDIT, endToEndId=E230301113902, entryType=DEBIT_CREDIT_NOTIFICATION, instructedAmount=1234, instructedAmountCurrency=USD, instructionId=PPSS2303183804, isOutward=true, lastUpdateDatetime=2023-03-18T00:45:43.263, lastUpdateUser=PPR, matchedPaymentOrCharge=true, settlementAmount=1211.5, settlementAmountCurrency=USD, settlementDate=2023-03-20, status=REPLIED, uetr=9d66ef3f-997b-4328-80f4-001884719056]], eventType=[PAYMENT_PROCESSOR_SUBMITED_CREDIT_DEBIT_NOTIFICATION_TO_SWIFT]

// case 2
Root Cause: payment-processor-2023-03-18-1.log:2023-03-18 00:06:06.690 [fromSettlementMsgRouterExecutor-3] [SystemLogger] ERROR -  () Error when excuting the Redis Job: (outward) Write Swift msg of settlement to Host, current job status: RUNNING


PPSS2303182994
settlement did invoke processor through redis interface.
processor没有收到 settlement发的message.
redis has only one mur.
wmsgMurLinkKey=9577402f-cd4a-4558-b789-e9ef39f73e65
MESSAGE_REFERENCE=M000202303181205180000002893

2023-03-18 00:05:19.067 [settlementMsgRouterExecutor-2] [SystemLogger] DEBUG -  () PaymentProcessorClientImpl.submitPaymentSettlementResult#start - settlement=[SettlementEntryDTO[acctId=2880002219, acctOwner=BOSHCNSHXXX, acctServicer=SCBKHKHHXXX, acctServicerReference=PPSS2303182994, additionalData={incomingMessageKey=SW230318000331, wmsgMurLinkKey=9577402f-cd4a-4558-b789-e9ef39f73e65, paymentVersion=0, MESSAGE_REFERENCE=M000202303181205180000002893}, clientReqId=1679064150852015, clientSysId=SWIFT, clientUsrId=SWIFT, createUser=PPR, creationDatetime=2023-03-18T00:05:18.831, creditDebitIndicator=CREDIT, endToEndId=E230301113902, entryType=DEBIT_CREDIT_NOTIFICATION, instructedAmount=1234, instructedAmountCurrency=USD, instructionId=PPSS2303182994, isOutward=true, lastUpdateDatetime=2023-03-18T00:05:18.831, lastUpdateUser=PPR, matchedPaymentOrCharge=true, settlementAmount=1211.5, settlementAmountCurrency=USD, settlementDate=2023-03-20, status=REPLIED, uetr=9d66ef3f-997b-4328-80f4-000445163217]], eventType=[PAYMENT_PROCESSOR_SUBMITED_CREDIT_DEBIT_NOTIFICATION_TO_SWIFT]


2023-03-18 00:06:06.466 [fromSettlementMsgRouterExecutor-3] [SystemLogger] DEBUG -  () PaymentProcessorMessageRouter.handleMessage#start - eventType=[PAYMENT_PROCESSOR_SUBMITED_CREDIT_DEBIT_NOTIFICATION_TO_SWIFT], message=[InternalMessage[businessService=null, clientReqId=20791a84-152f-4f8a-a7b5-dbbc10b2449d, clientSysId=null, clientUsrId=null, data={"acctId":"2880002219","acctServicer":"SCBKHKHHXXX","acctOwner":"BOSHCNSHXXX","acctServicerReference":"PPSS2303182994","settlementAmount":1211.5,"settlementAmountCurrency":"USD","settlementDate":"2023-03-20","creditDebitIndicator":"CREDIT","instructionId":"PPSS2303182994","endToEndId":"E230301113902","uetr":"9d66ef3f-997b-4328-80f4-000445163217","instructedAmount":1234,"instructedAmountCurrency":"USD","matchedPaymentOrCharge":true,"status":"REPLIED","entryType":"DEBIT_CREDIT_NOTIFICATION","isOutward":true,"clientReqId":"1679064150852015","clientUsrId":"SWIFT","clientSysId":"SWIFT","createUser":"PPR","creationDatetime":"2023-03-18T00:05:18.831","lastUpdateUser":"PPR","lastUpdateDatetime":"2023-03-18T00:05:18.831","additionalData":{"incomingMessageKey":"SW230318000331","wmsgMurLinkKey":"9577402f-cd4a-4558-b789-e9ef39f73e65","paymentVersion":0,"MESSAGE_REFERENCE":"M000202303181205180000002893"}}, eventType=PAYMENT_PROCESSOR_SUBMITED_CREDIT_DEBIT_NOTIFICATION_TO_SWIFT, msgType=camt.054.001.08, options=null]]


payment-processor-2023-03-18-1.log:2023-03-18 00:06:06.542 [fromSettlementMsgRouterExecutor-3] [SystemLogger] DEBUG -  () PaymentProcessorBizDelegate.processSettlement#start - settlementNotice=[SettlementEntryDTO[accId=2880002219, acctOwner=BOSHCNSHXXX, acctServicer=SCBKHKHHXXX, acctServicerReference=PPSS2303182994, additionalData={incomingMessageKey=SW230318000331, wmsgMurLinkKey=9577402f-cd4a-4558-b789-e9ef39f73e65, paymentVersion=0, MESSAGE_REFERENCE=M000202303181205180000002893}, clientReqId=1679064150852015, clientSysId=SWIFT, clientUsrId=SWIFT, createUser=PPR, creationDatetime=2023-03-18T00:05:18.831, creditDebitIndicator=CREDIT, endToEndId=E230301113902, entryType=DEBIT_CREDIT_NOTIFICATION, instructedAmount=1234, instructedAmountCurrency=USD, instructionId=PPSS2303182994, isOutward=true, lastUpdateDatetime=2023-03-18T00:05:18.831, lastUpdateUser=PPR, matchedPaymentOrCharge=true, settlementAmount=1211.5, settlementAmountCurrency=USD, settlementDate=2023-03-20, status=REPLIED, uetr=9d66ef3f-997b-4328-80f4-000445163217]]


```



## Spring intergration

1.是Channel 进行绑定，还是Queue进行绑定？

 是Queue决定绑定关系

queue是有缓存的特有的组件，如redis。  

2.发出sendmessage，用

```xml
	<int:outbound-channel-adapter


	<!-- gateway service. This means that the RedisChannelGateway bean could be injected into other beans -->
	<int:gateway id="eventChannelGateway"
                service-interface="org.toptal.queue.RedisChannelGateway"
                error-channel="errorChannel" default-request-channel="eventChannel">
       <int:method  name="" />
       <int:default-header name="topic" value="queue"/>
	</int:gateway>

	<int:object-to-json-transformer input-channel="eventChannel"
                                   output-channel="eventChannelJson"/>
```



3.接受receive message，用

```xml
    <int-redis:queue-inbound-channel-adapter id="event-inbound-channel-adapter"
                                                channel="eventChannelJson" queue="my-event-queue"
                                                serializer="serializer" auto-startup="true"
                                                connection-factory="redisConnectionFactory"/>


    <int-redis:queue-inbound-gateway queue="" connection-factory="redisConnectionFactory" serializer="genericJackson2JsonRedisSerializer" request-channel="" reply-channel="" />



    <int:service-activator ref="bizDelegate" method="submitOutwardMessage" input-channel="submit-out-swift-mx" output-channel="submit-out-swift-mx-result" />
    <!-- activator，指定具体的处理类和方法 defines which service and method should be used to process the event. -->


    <int:json-to-object-transformer input-channel="eventChannelJson"  output-channel="eventChannel" type="com.toptal.integration.spring.model.PostPublishedEvent"/>                               
    <!-- json-to-object-transformer needs a type attribute in order to transform JSON to objects, set above to type="com.toptal.integration.spring.model.PostPublishedEvent" -->
```

messaging  common set up设置

```xml
    <int:router input-channel="inChannel" expression="payload.paymentType">
        <int:mapping value="CASH" channel="cashPaymentChannel"/>
        <int:mapping value="CREDIT" channel="authorizePaymentChannel"/>
        <int:mapping value="DEBIT" channel="authorizePaymentChannel"/>
    </int:router>
    <！-- consume messages from a message channel and forward each consumed message to one or more different message channels depending on a set of conditions.
         As of Spring Integration 2.0, we offer an alternative that lets you use SpEL to implement simple computations that previously required a custom POJO router.
          Routers and the Spring Expression Language (SpEL)-->			

    
    <int:chain
```

4.adapter和gateway 的区别？

Channel adapters are one such mechanism used for one-way integration (send or receive).  只能单向，有inboud-adapter和outboud-adapter

And gateways are used for request/reply scenarios (inbound or outbound).  可以双向，作为bean service 注入





activator，指定具体的处理类和方法



```
/**
 *  if all validateRules results are passed, then update VerificationStatus to matched, vice versa update to unmatched
 *  handle status according to validation result list
 *  状态模式， 处理eventType
 * @param payment
 * @param options
 */
// todo update logic.  ow
private void determineVerificationStatus(PaymentDTO payment, Map<String, Object> options) {
```



target endpoint
Figure 6. An outbound channel adapter endpoint connects a MessageChannel to a target system.





channel    -   redis queue



get from **Queue** :payment-processor-processPayment-queue  **EventType**: PAYMENT_PROCESSOR_IW_PAYMENT_RECEIVED  
  ^
  ^
paymentClient.submitPaymentProcessingResult     

**EventType**: PAYMENT_PROCESS_PAYMENT_RESULT     **Queue** payment-processPayment-queue



给 payment发了redis queue msg，没有收到payment service 发的  **EventType**: PAYMENT_PROCESSOR_OW_PAYMENT_CREATED      的queue msg




