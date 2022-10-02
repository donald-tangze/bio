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



## google-hibernate-generic

https://github.com/vincentruan/hibernate-generic-dao

https://code.google.com/archive/p/hibernate-generic-dao/





## IBM MQ 

https://github.com/ibm-messaging/mq-jms-spring

https://developer.ibm.com/tutorials/mq-jms-application-development-with-spring-boot/



### [Redis shell](https://redis.io/commands/hgetall/)

```
redis-cli -u redis://user:pass@host:port

HGETALL key
```

