* [springcloud](#springcloud)
    * [服务注册与发现](#服务注册与发现)
        * [eureka](#eureka)
        * [consul](#consul)
    * [服务负载与调用](#服务负载与调用)
        * [ribbon](#ribbon)
        * [loadbalancer](#loadbalancer)
    * [服务负载与调用](#服务负载与调用-1)
        * [feign](#feign)
        * [openFeign](#openfeign)
    * [服务熔断与降级](#服务熔断与降级)
        * [hystrix](#hystrix)
        * [resilience4j](#resilience4j)
    * [服务网关](#服务网关)
        * [zuul](#zuul)
        * [zuul2](#zuul2)
        * [getway](#getway)
    * [服务分布式配置](#服务分布式配置)
        * [springcloud config](#springcloud-config)
        * [Nacos](#nacos)
* [springcloudAlibaba](#springcloudalibaba)
    * [Nacos](#nacos-1)
        * [服务注册中心](#服务注册中心)
        * [服务配置](#服务配置)
        * [服务总线](#服务总线)
    * [sentienl](#sentienl)
# springcloud
Spring Cloud是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、智能路由、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。

Spring Cloud并没有重复制造轮子，它只是将各家公司开发的比较成熟、经得起实际考验的服务框架组合起来，通过Spring Boot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包。
## 服务注册与发现
### eureka
服务治理组件，包括服务端的注册中心和客户端的服务发现机制；
### consul
基于Hashicorp Consul的服务治理组件。
## 服务负载与均衡
### ribbon
负载均衡的服务调用组件，具有多种负载均衡调用策略；
### loadbalancer
## 服务负载与调用
### feign
基于Ribbon和Hystrix的声明式服务调用组件；
### openFeign
基于Ribbon和Hystrix的声明式服务调用组件，可以动态创建基于Spring MVC注解的接口实现用于服务调用，在Spring Cloud 2.0中已经取代Feign成为了一等公民。
## 服务熔断与降级
### hystrix
服务容错组件，实现了断路器模式，为依赖服务的出错和延迟提供了容错能力；
### resilience4j
## 服务网关
### zuul
API网关组件，对请求提供路由及过滤功能。
### zuul2
### getway
API网关组件，对请求提供路由及过滤功能。
## 服务分布式配置
### springcloud config
集中配置管理工具，分布式系统中统一的外部配置管理，默认使用Git来存储配置，可以支持客户端配置的刷新及加密、解密操作。
### Nacos
## 总线
### Spring Cloud Bus
用于传播集群状态变化的消息总线，使用轻量级消息代理链接分布式系统中的节点，可以用来动态刷新集群中的服务配置。
# springcloudAlibaba
## Nacos
### 服务注册中心
### 服务配置
### 服务总线
## sentienl