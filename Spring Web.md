那么现在需要哪些组件来完成一个请求的对应和执行呢？

1.需要有一个地方（例如 Map）去维护从 HTTP path/method 到具体执行方法的映射；

2.当一个请求来临时，根据请求的关键信息来获取对应的需要执行的方法；

3.根据方法定义解析出调用方法的参数值，然后通过反射调用方法，获取返回结果。



首先，解析 HTTP 请求。对于 Spring 而言，它本身并不提供通信层的支持，它是依赖于 Tomcat、Jetty 等容器来完成通信层的支持，例如当我们引入 Spring Boot 时，我们就间接依赖了 Tomcat。依赖关系图如下：

![img](https://static001.geekbang.org/resource/image/45/44/456dc47793b0f99c9c2d193027f0ed44.png)

```java

//org.springframework.boot.autoconfigure.web.servlet.ServletWebServerFactoryConfiguration

class ServletWebServerFactoryConfiguration {

   @Configuration(proxyBeanMethods = false)
   @ConditionalOnClass({ Servlet.class, Tomcat.class, UpgradeProtocol.class })
   @ConditionalOnMissingBean(value = ServletWebServerFactory.class, search = SearchStrategy.CURRENT)
   public static class EmbeddedTomcat {
      @Bean
      public TomcatServletWebServerFactory tomcatServletWebServerFactory(
         //省略非关键代码
         return factory;
      }

   }
   
@Configuration(proxyBeanMethods = false)
@ConditionalOnClass({ Servlet.class, Server.class, Loader.class, WebAppContext.class })
@ConditionalOnMissingBean(value = ServletWebServerFactory.class, search = SearchStrategy.CURRENT)
public static class EmbeddedJetty {
   @Bean
   public JettyServletWebServerFactory JettyServletWebServerFactory(
         ObjectProvider<JettyServerCustomizer> serverCustomizers) {
       //省略非关键代码
      return factory;
   }
}

//省略其他容器配置
}


```

