## 2023.10.27 

#### 1. Definition:  Key-Value storage(键值数据库); Nosql storage; 

### 2.Usage Scenario:

Message Broker; message Queue, similar to Rabbit MQ and Kafka

### 3.[Redis document](https://redis.io/docs/data-types/)

client: RedisInsight, including tutorial

#### 3.1.[Redis Value datatype](https://redis.io/docs/data-types/)

* hashes 

  > are record types structured as collections of *field-value pairs*.  
  >
  > We can use hashes to *represent basic objects* and to store *groupings of counters*, among other things.

* String

  > Redis strings store sequences of bytes, including *text, serialized objects, and binary arrays*. 
  >
  > They're often used for *caching*, but they support additional functionality that lets you implement *counters* and perform *bitwise operations*, too.

* List

  >  Redis lists are linked lists of string values. Redis lists are frequently used to:
  >
  > * Implement *stacks* and *queues*.
  >
  > * Build *queue management* for background worker systems.

* Set

  > A Redis set is an unordered collection of unique strings (members). You can use Redis sets to efficiently:
  >
  > - Track unique items (e.g., track all unique IP addresses accessing a given blog post).
  > - Represent relations (e.g., the set of all users with a given role).
  > - Perform common *set operations* such as intersection, unions, and differences.

* Sorted Set

  > A Redis sorted set is a collection of unique strings (members) ordered by an associated score. When more than one string has the same score, the strings are ordered lexicographically. Some use cases for sorted sets include:
  >
  > - Leaderboards. For example, you can use sorted sets to easily maintain ordered lists of the highest scores in a massive online game.
  > - *Rate limiters*. In particular, you can use a sorted set to build a sliding-window rate limiter to prevent excessive API requests.

* Stream

  > A Redis stream is a data structure that acts like an append-only log but also implements several operations to overcome some of the limits of a typical append-only log.
  >
  > Examples of Redis stream use cases include:
  >
  > - Event sourcing (e.g., tracking user actions, clicks, etc.)
  > - Sensor monitoring (e.g., readings from devices in the field)
  > - Notifications (e.g., storing a record of each user's notifications in a separate stream)

* Redis geospatial

  > Redis geospatial indexes let you store coordinates and search for them. This data structure is useful for finding nearby points within a given radius or bounding box.

### 4.[Redis data type Command](https://redis.io/commands/)

#### 4.1.hashes 

- [`HSET`](https://redis.io/commands/hset) sets the value of one or more fields on a hash.
- [`HGET`](https://redis.io/commands/hget) returns the value at a given field.   (HGETALL)
- [`HMGET`](https://redis.io/commands/hmget) returns the values at one or more given fields.
- [`HINCRBY`](https://redis.io/commands/hincrby) increments the value at a given field by the integer provided.

#### 4.2.String

- [`SET`](https://redis.io/commands/set) stores a string value.
- [`SETNX`](https://redis.io/commands/setnx) stores a string value only if the key doesn't already exist. Useful for implementing locks.
- [`GET`](https://redis.io/commands/get) retrieves a string value.
- [`MGET`](https://redis.io/commands/mget) retrieves multiple string values in a single operation.
- [`INCRBY`](https://redis.io/commands/incrby) atomically increments (and decrements when passing a negative number) counters stored at a given key.
- Another command exists for floating point counters: [`INCRBYFLOAT`](https://redis.io/commands/incrbyfloat).

####  4.3.List

- [`LPUSH`](https://redis.io/commands/lpush) adds a new element to the head of a list; [`RPUSH`](https://redis.io/commands/rpush) adds to the tail.
- [`LPOP`](https://redis.io/commands/lpop) removes and returns an element from the head of a list; [`RPOP`](https://redis.io/commands/rpop) does the same but from the tails of a list.
- [`LLEN`](https://redis.io/commands/llen) returns the length of a list.
- [`LMOVE`](https://redis.io/commands/lmove) atomically moves elements from one list to another.
- [`LTRIM`](https://redis.io/commands/ltrim) reduces a list to the specified range of elements.

#### 4.4.Set

- [`ZADD`](https://redis.io/commands/zadd) adds a new member and associated score to a sorted set. If the member already exists, the score is updated.
- [`ZRANGE`](https://redis.io/commands/zrange) returns members of a sorted set, sorted within a given range.
- [`ZRANK`](https://redis.io/commands/zrank) returns the rank of the provided member, assuming the sorted is in ascending order.
- [`ZREVRANK`](https://redis.io/commands/zrevrank) returns the rank of the provided member, assuming the sorted set is in descending order.

#### 4.5.Sorted Set





#### 4.6. Stream

- [`XADD`](https://redis.io/commands/xadd) adds a new entry to a stream.

- [`XREAD`](https://redis.io/commands/xread) reads one or more entries, starting at a given position and moving forward in time.

- [`XRANGE`](https://redis.io/commands/xrange) returns a range of entries between two supplied entry IDs.

- [`XLEN`](https://redis.io/commands/xlen) returns the length of a stream.

  

#### 4.7. Geospatial

- [`GEOADD`](https://redis.io/commands/geoadd) adds a location to a given geospatial index (note that longitude comes before latitude with this command).
- [`GEOSEARCH`](https://redis.io/commands/geosearch) returns locations with a given radius or a bounding box.



![Redis学习路径](https://static001.geekbang.org/resource/image/0e/3c/0e7b8c42d1daf631b19c7164ac4bdf3c.jpg?wh=2250*1363)

### 5. [主从同步](https://time.geekbang.org/column/article/272852?utm_campaign=geektime_search&utm_content=geektime_search&utm_medium=geektime_search&utm_source=geektime_search&utm_term=geektime_search)

命令：主-从-从

```sh
# 实例 2 就变成了实例 1 的从库
replicaof 172.16.19.3 6379

# 从库给主库发送 psync 命令，表示要进行数据同步
psync <主库的 runID>  <复制进度 offset>

# 响应表示第一次复制采用的全量复制，也就是说，主库会把当前所有的数据都复制给从库。
FULLRESYNC 

# 命令，生成 RDB 文件
bgsave 

# 第三个阶段，主库会把第二阶段执行过程中新收到的写命令，再发送给从库
repl backlog 
repl buffer
```

### 6. 哨兵：主从切换，主节点故障下线，选举新的从节点



## 2022.03.24

Redis实操中的，cluster集群部署，client客户端是表象。 

内核是

* 1.数据库的数据结构，链表linkedlist, String, sortSet,

> 每种数据结构的具体实现，例如 List 在底层是一个链表，在 List 中查找元素时就会比较慢，而 Hash 和 Set 底层都是哈希表实现的，所以定位元素的速度非常快，而 Sorted Set 是把哈希表和跳表结合起来使用，查找元素和遍历元素都比较快。

* 2.集群部署，分布式系统典型问题，高性能，高可靠，集群复制，故障监测，master选举

> Redis 之所以可以实现高可靠、高性能，和它的持久化机制、主从复制机制、哨兵、故障自动恢复、切片集群等密不可分。

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

![图片](https://tva1.sinaimg.cn/large/e6c9d24egy1h4qixi0a5cj21dj0u0gow.jpg)



##  2022.07.31 Spring-integration-redis

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
| [Service Activator(https://docs.spring.io/spring-integration/reference/html/overview.html#pojo-invocation) | a generic endpoint for connecting a service instance to the messaging system. The input message channel must be configured, and, if the service method to be invoked is capable of returning a value, an output message Channel may also be provided. |
| [Channel Adapter](https://docs.spring.io/spring-integration/reference/html/redis.html#redis-inbound-channel-adapter) | an endpoint that connects a message channel to some other system or transport. Channel adapters may be either inbound or outbound.    the channel adapter does some mapping between the message and whatever object or resource is received from or sent to the other system (file, HTTP Request, JMS message, and others). |
| [Messaging Gateways](https://docs.spring.io/spring-integration/reference/html/messaging-endpoints.html#gateway) | A gateway hides the messaging API provided by Spring Integration. It lets your application’s business logic be unaware of the Spring Integration API. By using a generic Gateway, your code interacts with only a simple interface. |

![handler endpoint](https://tva1.sinaimg.cn/large/e6c9d24egy1h4qicbyhzej20gy05dq34.jpg)

**Figure 4. Service Activator**

![source endpoint](https://docs.spring.io/spring-integration/reference/html/images/source-endpoint.jpg)

Figure 5. An inbound channel adapter endpoint connects a source system to a `MessageChannel`.



![target endpoint](https://docs.spring.io/spring-integration/reference/html/images/target-endpoint.jpg)

Figure 6. An outbound channel adapter endpoint connects a `MessageChannel` to a target system.	
