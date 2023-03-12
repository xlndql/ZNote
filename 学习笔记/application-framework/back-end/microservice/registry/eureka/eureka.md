# Eureka

## **Eureka 的作用**

1. 注册所有的服务信息，包括服务消费者和服务提供者
2. 拉取服务消费者所需服务的信息
3. 获取相应服务提供者的信息并做负载均衡
4. 形成服务消费者和服务提供者的远程调用

ps：Eureka 和服务之间会有心跳续约，每 30 秒 1 次，如果未获取到心跳，则将服务信息从注册中心移除。

## **搭建 Eureka 服务**

* 新建模块
* 引入 Eureka 依赖

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

* 编写启动类

Eureka 的启动类中一定要添加 @EnableEurekaServer 注解，开启 Eureka 的注册中心功能：

```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaApplication.class, args);
    }
}
```

* 编写配置文件

编写一个 application.yml 文件，内容如下：

```yaml
server:
  port: 10001
spring:
  application:
    name: eureka-server
eureka:
  client:
    service-url: 
      defaultZone: http://localhost:10001/eureka
```

* 启动服务

启动该模块，就可以在浏览器中访问 http://localhost:10001

## **服务注册**

* 引入依赖

在需要注册为 Eureka 服务的模块中导入依赖：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

* 添加配置文件

修改 application.yml 文件，添加服务名称，Eureka 地址：

```yaml
spring:
  application:
    name: serviceA
eureka:
  client:
    service-url:
      defaultZone: http://localhost:10001/eureka
```

* 启动多个 serviceA 服务只需要将每个服务的端口更改不冲突就可以在 Eureka 中注册获取到服务信息。

## **服务发现**

* 引入依赖（同上）
* 添加配置文件（同上，name 需要替换）
* 服务拉取和负载均衡

通过去 Eureka 中拉取 serviceA 服务的实例列表，并实现负载均衡，只需要添加一些注解即可。

在 RestTemplate 的 Bean 上添加一个 @LoadBalanced 的注解

将使用到的 RestTemplate 处 url 的ip和端口用服务名替代，即 serviceA

例如 http://localhost:8080/user/ 替换为 http://serviceA/user/
