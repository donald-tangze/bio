

XML或annotation parser  --> BeanDefinition 

> 只有 singleton，非延迟加载的bean的instantiation实例化和applicationContext是一起处理的，其他延迟加载的和protype只到生成BeanDefinition，下面步骤是第一次使用时发生进行初始化

-->   instantiation 实例化 所有的引用是null  

-->  initialization初始化            (加载包括这两步)

> 

![B221E14D-FCD2-48A1-A4EE-190C8072CE60](/Users/don2021/Pictures/Photos Library.photoslibrary/originals/B/B221E14D-FCD2-48A1-A4EE-190C8072CE60.jpeg)

![img](http://s0.lgstatic.com/i/image2/M01/8A/C6/CgoB5l14puyAAa1gAABPP0lufvQ678.png)

![image-20220206150731348](/Users/don2021/Library/Application Support/typora-user-images/image-20220206150731348.png)









![image-20220206152523105](/Users/don2021/Library/Application Support/typora-user-images/image-20220206152523105.png)

![image-20220206215820265](/Users/don2021/Library/Application Support/typora-user-images/image-20220206215820265.png)







<context  attribute1=""  attr2="">

​	<beans>

​		<bean attribute1=""  attr2="">   attributes

​			<element1>

​			<element2>



## Spring Data JPA VS Mybatis

Spring Dataf

JPA规范源自ORM框架的起源：Hibernate

解决问题：面向对象Object Oriented，和关系型数据库Relational DBS，之间的映射Mapping



JDBC  ->  JPA or Mybatis

 [TestJDBC.java](../计算机技术资料/3.0语言：Java/java/SSh书的代码/第五章/TestJDBC.java) 

[MyBatis还是JPA?](https://juejin.cn/post/6880696204297142280)

https://cloud.tencent.com/developer/article/1594337

中国用MyBatis比spring data多，前者更简单，容易入手，Mapper，直接写sql，在关联查询上比后者有优势，对于数据模型频繁变动的项目更适合

spring data是标准，未来趋势，国外使用较多。

他们都可以对接不同的数据库，H2,  Mysql, postgreq,  Oracle, 

Mybatis的原理， 都是动态代理，aop，将sql包装在jdbc sql connection, statement, executeQuery

Repository  模式，实际更复杂，基于spring boot的aop

