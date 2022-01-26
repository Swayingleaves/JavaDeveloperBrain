
* [CAP理论](#cap理论)
  * [一致性 Consistency](#一致性-consistency)
  * [可用性 Availability](#可用性-availability)
  * [分区容错性 Partition Tolerance](#分区容错性-partition-tolerance)
  * [常见的注册中心](#常见的注册中心)

# CAP理论
图
![](../img/分布式相关/cap.png)

CAP 定理（CAP theorem）指出对于一个分布式系统来说，当设计读写操作时，只能能同时满足以下三点中的两个
- CAP 理论中分区容错性 P 是一定要满足的，在此基础上，只能满足可用性 A 或者一致性 C

### 一致性 Consistency

Consistency，一致性的意思。

一致性就是说，我们读写数据必须是一摸一样的。

比如一条数据，分别存在两个服务器中，server1和server2。

我们此时将数据a通过server1修改为数据b。此时如果我们访问server1访问的应该是b。

当我们访问server2的时候，如果返回的还是未修改的a，那么则不符合一致性，如果返回的是b，则符合数据的一致性。
### 可用性 Availability
Availability，可用性的意思。

这个比较好理解，就是说，只要我对服务器，发送请求，服务器必须对我进行相应，保证服务器一直是可用的
### 分区容错性 Partition Tolerance
Partition tolerance，分区容错的意思。

一般来说，分布式系统是分布在多个位置的。比如我们的一台服务器在北京，一台在上海。可能由于天气等原因的影响。造成了两条服务器直接不能互相通信，数据不能进行同步。这就是分区容错。我们认为，分区容错是不可避免的。也就是说 P 是必然存在的。

网络时区造成的分区情况

## 常见的注册中心
| |Nacos|Eureka|Consul|CoreDNS|Zookeeper|
|---|---|---|---|---|---|
|一致性协议|	CP+AP|	AP|	CP|	— |	CP|
|健康检查|	TCP/HTTP/MYSQL/Client Beat|	Client Beat|	TCP/HTTP/gRPC/Cmd|	—	|Keep Alive|
|负载均衡策略|	权重/metadata|/Selector|	Ribbon|	Fabio|	RoundRobin|	— |
|雪崩保护|	|有	|有	|无	|无	|无|
|自动注销实例|	|支持	|支持	|支持	|不支持	|支持|
|访问协议|	HTTP/DNS|	HTTP|	HTTP/DNS|	DNS	|TCP|
|监听支持|	支持|	支持|	支持	|不支持|	支持|
|多数据中心|	支持|	支持	|支持	|不支持|不支持|
|跨注册中心同步|	支持|	不支持|	支持|	不支持|	不支持|
|SpringCloud集成|	支持|	支持|	支持|	不支持|	支持|
|Dubbo集成|	支持|	不支持|	支持|	不支持|	支持|
|K8S集成|	支持|	不支持|	支持|	支持|	不支持|
