###  2022.03.24

Redis的实操中的，cluster集群部署，client客户端是表象。 

内核是

* 1.数据库的数据结构，链表linkedlist, String, sortSet,

  > 每种数据结构的具体实现，例如 List 在底层是一个链表，在 List 中查找元素时就会比较慢，而 Hash 和 Set 底层都是哈希表实现的，所以定位元素的速度非常快，而 Sorted Set 是把哈希表和跳表结合起来使用，查找元素和遍历元素都比较快。

* 2.集群部署，分布式系统典型问题，高性能，高可靠，集群复制，故障监测，master选举

> Redis 之所以可以实现高可靠、高性能，和它的持久化机制、主从复制机制、哨兵、故障自动恢复、切片集群等密不可分。
>
> Redis 提供了两种持久化方式：RDB 和 AOF，分别对应数据快照和实时的命令持久化
>
> 采用多个副本。我们需要 Redis 可以实时保持多个副本的同步，也就是我们说的主从复制。
>
> 实现主从自动切换，就需要能够保证高可用的组件：哨兵
>
> **切片集群**：Redis Cluster、Twemproxy、Codis 这些集群解决方案
>
> 既然是多个节点存储数据，而且还要在节点不足时能够增加新的节点扩容集群，这也对应着切片集群的核心问题：**数据路由和数据迁移**。

常见互联网使用场景，抢购，页面uv，缓存；

> Redis 在用作缓存时，有很多典型的问题，比如说数据库和 Redis 缓存的数据一致性问题、缓存穿透问题、缓存雪崩问题。这些问题会涉及到缓存策略、缓存如何设置过期时间、应用与缓存如何配合

内存数据库

![图片](https://static001.geekbang.org/resource/image/0e/3c/0e7b8c42d1daf631b19c7164ac4bdf3c.jpg)

2022.07.31

Spring-integration-redis

#### Redis Queue Inbound Channel Adapter

Attributes:

Queue: The name of the Redis list on which the queue-based 'pop' operation is performed to get Redis messages.

https://docs.spring.io/spring-integration/reference/html/redis.html#redis

| component                                                    | Function                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| XML                                                          | Non-invasive pattern, loosely coupled, separation of concern, isolatte business code and spring messaging code。 declarative configuration, you can “connect” your domain-specific code to the messaging infrastructure provided by Spring Integration. |
| Message                                                      | Header + payload                                             |
| channel                                                      | Pipe. either point-to-point (单点消费)or  publish-subscribe(多点消费) semantics. |
|                                                              |                                                              |
| Endpoint:                                                    | filter   onnect application code to the messaging framework and to do so in a non-invasive manner. |
| Transformer                                                  |                                                              |
| adapter                                                      |                                                              |
| Router                                                       |                                                              |
| Splitter                                                     |                                                              |
| Service Activator                                            | a generic endpoint for connecting a service instance to the messaging system. The input message channel must be configured, and, if the service method to be invoked is capable of returning a value, an output message Channel may also be provided. |
| Channel Adapter                                              | an endpoint that connects a message channel to some other system or transport. Channel adapters may be either inbound or outbound.    the channel adapter does some mapping between the message and whatever object or resource is received from or sent to the other system (file, HTTP Request, JMS message, and others). |
| [Messaging Gateways](https://docs.spring.io/spring-integration/reference/html/messaging-endpoints.html#gateway) | A gateway hides the messaging API provided by Spring Integration. It lets your application’s business logic be unaware of the Spring Integration API. By using a generic Gateway, your code interacts with only a simple interface. |

![handler endpoint](https://tva1.sinaimg.cn/large/e6c9d24egy1h4qicbyhzej20gy05dq34.jpg)

**Figure 4. Service Activator**

![source endpoint](https://docs.spring.io/spring-integration/reference/html/images/source-endpoint.jpg)

Figure 5. An inbound channel adapter endpoint connects a source system to a `MessageChannel`.



