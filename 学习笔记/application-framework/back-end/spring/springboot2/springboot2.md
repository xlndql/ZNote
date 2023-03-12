# Spring Boot 2

## 目录

* 常用注解
* 资源整合
* 高级特性
* 本地热部署
* RestTemplate


## RestTemplate

RestTemplate 简化了发起 HTTP 请求以及处理相应的过程，并且支持 REST。

**使用**

在 SpringBoot 项目的启动类中加入：

```java
@Bean
public RestTemplate restTemplate() {
  return new RestTemplate();
}
```

然后在 Controller 层中引入：

```java
@Autowired
private RestTemplate restTemplate;
```

然后就可以在方法中发起 HTTP 请求了
