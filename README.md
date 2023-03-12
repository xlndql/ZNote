
obsidian的具体搭建过程前往[[obsidian配置过程记录]]

---
# 我的编程学习之路

> 为了让自己在大学中有目的有效率的学习编程并成为一名软件工程师，我决定写这一份学习清单兼笔记来记录自己的学习过程。
> 虽然现在已经大二寒假了，自己也完成了一些小的目标，但是由于之前一年的时间没有进行系统的学习记录和总结，所以会经常感觉到自己的学习漫无目的，成效很低，今天看到了这样一份github上大佬的学习过程[John Washam的编程学习清单](https://github.com/jwasham/coding-interview-university/blob/main/translations/README-cn.md)，所以我下定决心要做这一份学习清单，希望自己能够一直坚持下去吧！
><p align="right">2023.1.8</p>
## 前言

我的学习清单大部分参照了 [Road 2 Coding](https://www.r2coding.com/#/README) 和 [鱼皮-编程学习路线](https://luxian.yupi.icu/#/roadmap/Java%E5%AD%A6%E4%B9%A0%E8%B7%AF%E7%BA%BF) 。

## 路线汇总

### 思维导图

![[编程学习路线图.png]]
### 具体内容

- 学习笔记
	- 应用框架
		- 后端
			- Spring家族
			- 构建管理工具
				- Maven
				- Gradle
			- 接口管理
				- Swagger 接口文档
				* Postman 接口测试
			- 服务器软件
			- 中间件
			- 数据库
				- ORM层框架
					- MyBatis
					- Mybatis-plus
					- Hibernate
					- JPA
				- 连接池
					- Druid
					- HikariCP
					- C3P0
				- 分库分表
				  * MyCat
				  * Sharding-JDBC
				  * Sharding-Sphere
			- 搜索引擎
			- 分布式/微服务
				- Spring Cloud
				* Spring Cloud Alibaba
				* [服务发现/注册](./registry/register.md)
				* 网关
				  * Zuul
				  * Gateway
				* [服务调用（负载均衡）](./load-balance/load-balance.md)
				* 熔断/降级
				  * Hystrix
				* 配置中心
				  * Config
				  * Apollo
				  * Nacos
				* 认证和鉴权
				  * Shiro
				  * Spring Security
				    * 用户认证
				    * 权限管理
				  * OAuth2
				  * SSO
				* 分布式事务
				  * JTA接口
				  * 2pC、3PC
				  * XA模式
				  * TCC模式
				  * SAGA模式
				  * LCN模式
				* 任务调度
				  * Quartz
				  * Elastic-Job
				* 链路追踪与监控
				  * Zipkin
				  * Sleuth
				  * Skywalking
				* 日志分析与监控
				  * ELK
			- 虚拟化/容器化
				- 容器技术
					- docker
				- 容器编排技术
					- Kubernetes
					- Swarm
		- 前端
			- 基础套件
			- 模板框架
			- 组件化框架
- 刷题笔记
- 项目笔记
- 日常笔记
- 其它笔记