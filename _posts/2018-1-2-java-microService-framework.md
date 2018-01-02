---
categories: architecture
tags: [java] 	
---
# Spring Cloud
based on spring boot
![micro-service](/assets/img/micro-service-spring-cloud.png)
## Spring Cloud Netflix
### config server(配置服务器)
```java
// java code ,use @EnableConfigServer;add info in bootstrap.properties
@EnableConfigServer 
@SpringBootApplication 
public  class Application { 
public static void main(String[] args)  { 
new  SpringApplicationBuilder(Application.class).web(true).run(args); 
} 
} 

```
### service discovery（服务发现）
#### Eureka
```java
// java code ,use @EnableEurekaServer; add info in application.properties
@EnableEurekaServer 
@SpringBootApplication 
public  class Application { 
public static void main(String[] args)  { 
new  SpringApplicationBuilder(Application.class).web(true).run(args); 
} 
} 
```
### Hystrix(断路器) 
#### Hystrix
### monitor(监控)
### router(路由)
#### Zuul
```java
//java code, use @EnableZuulProxy ; add info in application.properties
@EnableZuulProxy 
@SpringCloudApplication 
public class  Application { 
public static void main(String[] args)  { 
new  SpringApplicationBuilder(Application.class).web(true).run(args); 
} 
}
```
### load balancing(负载均衡)
#### Ribbon
```java
// java code ,use @EnableDiscoveryClient,@LoadBalanced
@SpringBootApplication 
@EnableDiscoveryClient 
public  class RibbonApplication { 
@Bean 
@LoadBalanced 
RestTemplate restTemplate() { 
return new RestTemplate(); 
} 
public static void main(String[] args)  { 
SpringApplication.run(RibbonApplication.class， args); 
} 
}
```