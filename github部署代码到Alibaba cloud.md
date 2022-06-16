[toc]

土办法是： 本地打包，然后手动上传包到cloud server, 每次修改需要重新打包上传，费时费力

CD:continuous deployment持续部署

### 1.Github Actions(to-do)



### 2.manually pull, build, run 

```git pull```

#### [连接alibaba cloud server到github](https://www.cxyzjd.com/article/niaoer2010/95629123)

账号： root  密码：BJtz2019

* 阿里云ECS的SERVER_SSH_KEY生成

  [Generating a new SSH key](https://docs.github.com/cn/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

  ```shell
  //通过Xshell登录进服务器，执行ssh-keygen命令：
  ssh-keygen -t ed25519 -C "donald.tangze@outlook.com"
  ```



####  2.build jar package 

在project目录下

```
mvn clean package
```

##### [在aliyun server上安装mvn](https://developer.aliyun.com/article/663332)

https://blog.51cto.com/u_15504393/5043147

wget下载maven tar.gz包，解压安装，设置maven环境变量/etc/profile，设置settings的mirror

vim /etc/profile 编辑环境变量文件

source /etc/profile

```
# set maven environment
export MAVEN_HOME=/app/maven/apache-maven-3.8.5
export PATH=${PATH}:${MAVEN_HOME}/bin 
```



####  3.run jar包

在project目录下，mvn clean package

在target目录下： java -jar api-0.0.1-SNAPSHOT.jar

#### 4.create a containerized Spring Boot application using Docker

- Clone and run a Spring Boot application with Maven
- [Create a new Dockerfile which contains instructions required to build a Java image](https://docs.docker.com/language/java/build-images/#create-a-dockerfile-for-java)

> 

- Run the newly built image as a container
- Set up a local development environment to connect a database to the container
- Use Docker Compose to run the Spring Boot application
- Configure a CI/CD pipeline for your application using GitHub Actions
- Deploy your application to the cloud

https://github.com/spotify/dockerfile-maven

https://spring.io/guides/topicals/spring-boot-docker/



### [Spring MVC Framework and REST](https://www.genuitec.com/spring-frameworkrestcontroller-vs-controller/#:~:text=Spring%20MVC%20Framework%20and%20REST&text=While%20the%20traditional%20MVC%20controller,HTTP%20response%20as%20JSON%2FXML.)

 While the traditional MVC controller relies on the View technology, the RESTful web service controller simply returns the object and the object data is written directly to the HTTP response as JSON/XML. 



JSP (JavaServer Page) put under /WEB-INF, build your application as an excutable JAR file, no way to satisfy directory /WEB-INF.

That's to say JSP is usually packaged WAR filE. Tomcat is servlet container, make use of war

if you're building an excutable Jar file, MVC view template can only choose from FreeMarker, Thymeleaf, Mustache etc.



#### JDBC & Spring Data JPA (RDB)

jdbcTemplate好处是省略很多公式代码，connection, preparedStament, resultSet, close resultSet, close statement, close connect

spring data jpa: domain-specific language(DSL)

> readOrder ByDeliveryZipAndPlacedAtBetween()s
>
> 