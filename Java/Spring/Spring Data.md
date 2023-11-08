## 1.书籍

[<Java Persistence with Spring Data and Hibernate -2023>](https://www.manning.com/books/java-persistence-with-spring-data-and-hibernate)

[<Java Persistence with Hibernate - 2nd Version -2015 >](https://www.manning.com/books/java-persistence-with-hibernate-second-edition )

[<Java Persistence with Hibernate - 2008>]( https://www.manning.com/books/java-persistence-with-hibernate) 

[<Hibernate in Action - 2004> ](https://www.manning.com/books/hibernate-in-action)





![CH05_F04_Tudose2](C:\Users\donal\Downloads\CH05_F04_Tudose2.png)

Domain model



## 2.Spring Data JPA VS Mybatis

Spring Data

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



| Framework        | Characteristics                                              |
| :--------------- | :----------------------------------------------------------- |
| JPA              | Uses the general JPA API and requires a persistence provider. We can switch between persistence providers from the configuration.Requires explicit management of the `EntityManagerFactory`, `EntityManager`, and transactions.The configuration and the amount of code to be written is similar to the native Hibernate native approach.We can switch to the JPA approach by constructing an `EntityManagerFactory` from a native Hibernate configuration. |
| Native Hibernate | Uses the native Hibernate API. You are locked into using this chosen framework.Builds its configuration starting with the default Hibernate configuration files (hibernate.cfg.xml or hibernate.properties).Requires explicit management of the `SessionFactory`, `Session`, and transactions.The configuration and the amount of code to be written are similar to the JPA approach.We can switch to the native Hibernate native approach by unwrapping a `Session-Factory` from an `EntityManagerFactory` or a `Session` from an `EntityManager`. |
| Spring Data JPA  | Needs additional Spring Data dependencies in the project.The configuration will also take care of the creation of beans needed for the project, including the transaction manager.The repository interface only needs to be declared, and Spring Data will create an implementation for it as a proxy class with generated methods that interact with the database.The necessary repository is injected and not explicitly created by the programmer.This approach requires the least amount of code to be written, as the configuration takes care of most of the burden. |



### Introducing Spring Data

Spring Data is a family of projects belonging to the Spring framework whose purpose is to simplify access to both relational and NoSQL databases:

Spring Data Commons—Spring Data Commons, part of the umbrella Spring Data project, provides a metadata model for persisting Java classes and technology-neutral repository interfaces.

Spring Data JPA—Spring Data JPA deals with the implementation of JPA-based repositories. It provides improved support for JPA-based data access layers by reducing the boilerplate code and creating implementations for the repository interfaces.

Spring Data JDBC—Spring Data JDBC deals with the implementation of JDBC-based repositories. It provides improved support for JDBC-based data access layers. It does not offer a series of JPA capabilities, such as caching or lazy loading, resulting in a simpler and limited ORM.



### Introducing Hibernate
Object/relational mapping (ORM) is a programming technique for making the connection between the incompatible worlds of object-oriented systems and relational databases. Hibernate is an ambitious project that aims to provide a complete solution to the problem of managing persistent data in Java. Today, Hibernate is not only an ORM service but also a collection of data management tools extending well beyond ORM.

The Hibernate project suite includes the following:

Hibernate ORM—Hibernate ORM consists of a core, a base service for persistence with SQL databases, and a native proprietary API. Hibernate ORM is the foundation for several of the other projects in the suite, and it’s the oldest Hibernate project. You can use Hibernate ORM on its own, independent of any framework or any particular runtime environment with all JDKs. As long as a data source is accessible, you can configure it for Hibernate, and it works.

Hibernate EntityManager—This is Hibernate’s implementation of the standard Jakarta Persistence API. It’s an optional module you can stack on top of Hibernate ORM. Hibernate’s native features are a superset of the JPA persistence features in every respect.

Hibernate Validator—Hibernate provides the reference implementation of the Bean Validation (JSR 303) specification. Independent of other Hibernate projects, it provides declarative validation for domain model (or any other) classes.