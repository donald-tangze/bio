

Tianjin Airline & Capital Airline Booking system and official site    2011.07-2015.03

1.devlope code of modules including ticket management, pricing, integration with bank and 3rd-platform payment api.

2.test, integrate, ensure new feature to production evironment in regular basis timely.

3.the system designed by Strust2, Spring, Hibernate, make use of  JAVA, JSP, Servlet,  JQuery, Oracle etc.



Alibaba Health   Senior Software Engineer    2015.3 - 2017.8

1.Develop 

3.It make use of Microservices, Maven, RDMS, MySQL, Jenkins, MQ



System Engineer    Huawei Consumer Knowledge Base System    2017.10-2021.10

1. The high availability distributed system cover all huawei consumer product's document knowledge, provide web, mobile access for ordinay customer, sales and repair stores all over globe. Conduct partial design, develop core code, create and popularize java code, db table, interface standard inside develop group,  optimize performance.

2. Assign tasks, organise codeReview, resolve problem, monitor and maintain online system, manage team‘s process throughout different stages of agile and sprint.

3. It make use of Spring Boot, Spring Cloud(Eureka), MongoDB, Redis, MQ, MySQL.



• Practical experience with Spring, Spring Boot, Dubbo, RESTful API, TDD, MyBatis
• Good understanding of Microservices.
• Hands-on experience with Open Shift
• Commercial experience with CVS, Git, Maven, RDMS, SQL, Code Review, Jenkins

− Environnement technique : HTML, Java J2EE + Spring, Wicket, Javascript, AJAX, JSON, Tomcat, SVN, Scrum

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