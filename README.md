<h1 align="center">JavaDeveloperBrain:mortar_board:</h1>

<div align="center">

[comment]: <> ([![GitHub issues]&#40;https://img.shields.io/github/issues/Swayingleaves/JavaDeveloperBrain?style=for-the-badge&#41;]&#40;https://github.com/Swayingleaves/JavaDeveloperBrain/issues&#41;)
[![GitHub forks](https://img.shields.io/github/forks/Swayingleaves/JavaDeveloperBrain?style=for-the-badge)](https://github.com/Swayingleaves/JavaDeveloperBrain/network)
[![GitHub stars](https://img.shields.io/github/stars/Swayingleaves/JavaDeveloperBrain?style=for-the-badge)](https://github.com/Swayingleaves/JavaDeveloperBrain/stargazers)
![Java进阶](https://img.shields.io/badge/Java-%E8%BF%9B%E9%98%B6-brightgreen?style=for-the-badge)

</div>

<p align="center">Java工程师必备：包含计算机网络知识、JavaSE、JVM、Spring、Springboot、SpringCloud、Mybatis、多线程并发、netty、MySQL、MongoDB、Elasticsearch、Redis、HBASE、RabbitMQ、RocketMQ、Pulsar、Kafka、Zookeeper、Linux、设计模式、智力题、项目架构、分布式相关、算法、面试题</p>

---
<h3 align="center">不白嫖，来个star:star2::star2::star2:</h3>

# Features

- [x] 将目录里的xMind文件转为md文件 
- [ ] 将一些难以文字描述的东东画图
- [ ] 添加新知识点 :man_technologist:
- [ ] 添加新模块:收集面试题和解答他们:man_technologist:
- [ ] 优化知识点描述，现在有些知识点真的只是记下来了，但是没有整理导致别人看起来很乱不知所云 :man_technologist:



# 内容概览

[comment]: <> (<details><summary></summary>)
[comment]: <> (</details>)
## <a>Java-基础部分</a>
 - [基本类型](Java-基础/Java类型.md)
 - [包装类型](Java-基础/Java类型.md)
 - [关键字](Java-基础/Java关键字.md)
 - [Object](Java-基础/Object.md)
 - [String](Java-基础/String.md)
 - [数组](Java-基础/数组.md)
 - [继承](Java-基础/继承.md)
 - [反射](Java-基础/反射.md)
 - [异常](Java-基础/异常.md)
 - [泛型](Java-基础/泛型.md)
 - [容器](#)
   - [List](Java-基础/容器-collection.md#list)
     - [Vector](Java-基础/容器-collection.md#vector)
     - [LinkedList](Java-基础/容器-collection.md#linkedlist)
     - [ArrayList](Java-基础/容器-collection.md#arraylist)
     - [CopyOnWriteArrayList](Java-基础/容器-collection.md#copyonwritearraylist)
   - [Set](Java-基础/容器-collection.md#set)
     - [HashSet](Java-基础/容器-collection.md#hashset)
     - [LinkedHashSet](Java-基础/容器-collection.md#linkedhashset)
     - [TreeSet](Java-基础/容器-collection.md#treeset)
   - [queue](Java-基础/容器-collection.md#queue)
   - [Map](Java-基础/容器-map.md#map)
     - [HashMap](Java-基础/容器-map.md#hashmap)
     - [LinkedHashMap](Java-基础/容器-map.md#linkedhashmap)
     - [TreeMap](Java-基础/容器-map.md#treemap)
     - [ConcurrentHashMap](Java-基础/容器-map.md#concurrenthashmap)
     - [IdentityHashMap](Java-基础/容器-map.md#identityhashmap)
     - [WeakHashMap](Java-基础/容器-map.md#weakhashmap)
 - [Java-IO](Java-基础/JavaIO.md)
   - [文件io](Java-基础/JavaIO.md#文件io)
   - [网络io](Java-基础/JavaIO.md#网络io)
   - [NIO](Java-基础/JavaIO.md#nio)
 - [Java长期支持版本新特性](Java-基础/Java长期支持版本.md)

## <a>Java-JVM</a>

- [内存结构](Java-JVM/内存结构.md)
  - [程序计数器](Java-JVM/内存结构.md#程序计数器)
  - [Java虚拟机栈](Java-JVM/内存结构.md#java虚拟机栈)
  - [本地方法栈](Java-JVM/内存结构.md#本地方法栈)
  - [堆](Java-JVM/内存结构.md#堆)
  - [方法区](Java-JVM/内存结构.md#方法区)
  - [运行时常量池](Java-JVM/内存结构.md#运行时常量池)
  - [直接内存](Java-JVM/内存结构.md#直接内存)
- [垃圾回收](Java-JVM/垃圾回收.md)
  - [判断一个对象能否被回收](Java-JVM/垃圾回收.md#判断一个对象能否被回收)
    - [引用计数法](Java-JVM/垃圾回收.md#引用计数法)
    - [可达性算法](Java-JVM/垃圾回收.md#可达性算法)
  - [哪些可以作为是根节点](Java-JVM/垃圾回收.md#哪些可以作为是根节点)
  - [分代收集理论](Java-JVM/垃圾回收.md#分代收集理论)
  - [GC定义](Java-JVM/垃圾回收.md#gc定义)
    - [新生代收集（Minor GC/Young GC）](Java-JVM/垃圾回收.md#新生代收集minor-gcyoung-gc)
    - [老年代收集（Major GC/Old GC）](Java-JVM/垃圾回收.md#老年代收集major-gcold-gc)
    - [混合收集（Mixed GC）](Java-JVM/垃圾回收.md#混合收集mixed-gc)
    - [整堆收集（Full GC）](Java-JVM/垃圾回收.md#整堆收集full-gc)
  - [回收算法](Java-JVM/垃圾回收.md#回收算法)
    - [标记-清除](Java-JVM/垃圾回收.md#标记-清除)
    - [标记-复制](Java-JVM/垃圾回收.md#标记-复制)
    - [标记-整理](Java-JVM/垃圾回收.md#标记-整理)
  - [Hotspot算法实现细节](Java-JVM/垃圾回收.md#hotspot算法实现细节)
    - [根节点枚举GC Roots](Java-JVM/垃圾回收.md#根节点枚举gc-roots)
    - [安全点Safe Point](Java-JVM/垃圾回收.md#安全点safe-point)
    - [安全区域Safe Region](Java-JVM/垃圾回收.md#安全区域safe-region)
    - [记忆集Remembered Set与卡表Card Table](Java-JVM/垃圾回收.md#记忆集remembered-set与卡表card-table)
    - [写屏障Write Barrier](Java-JVM/垃圾回收.md#写屏障write-barrier)
  - [并发的可达性分析](Java-JVM/垃圾回收.md#并发的可达性分析)
    - [为什么需要并发标记](Java-JVM/垃圾回收.md#为什么需要并发标记)
    - [三色标记Tri-color Marking](Java-JVM/垃圾回收.md#三色标记tri-color-marking)
      - [什么是三色标记](Java-JVM/垃圾回收.md#什么是三色标记)
  - [垃圾回收器](Java-JVM/垃圾回收.md#垃圾回收器)
    - [Serial收集器](Java-JVM/垃圾回收.md#serial收集器)
    - [ParNew收集器](Java-JVM/垃圾回收.md#parnew收集器)
    - [ParallelScavenge收集器](Java-JVM/垃圾回收.md#parallelscavenge收集器)
    - [SerialOld收集器](Java-JVM/垃圾回收.md#serialold收集器)
    - [ParallelOld收集器](Java-JVM/垃圾回收.md#parallelold收集器)
    - [CMS收集器](Java-JVM/垃圾回收.md#cms收集器)
    - [G1收集器](Java-JVM/垃圾回收.md#g1收集器)
    - [ZGC收集器](Java-JVM/垃圾回收.md#zgc收集器)
- [内存分配与回收策略](Java-JVM/内存分配与回收策略.md)
  - [对象优先在 Eden 分配](Java-JVM/内存分配与回收策略.md#对象优先在-eden-分配)
  - [大对象直接进入老年代](Java-JVM/内存分配与回收策略.md#大对象直接进入老年代)
  - [长期存活的对象进入老年代](Java-JVM/内存分配与回收策略.md#长期存活的对象进入老年代)
  - [动态对象年龄判定](Java-JVM/内存分配与回收策略.md#动态对象年龄判定)
  - [空间分配担保](Java-JVM/内存分配与回收策略.md#空间分配担保)
- [类加载机制](Java-JVM/类加载机制.md)
  - [有哪些类加载器](Java-JVM/类加载机制.md#有哪些类加载器)
    - [1.引导类加载器 bootstrap classloader](Java-JVM/类加载机制.md#1引导类加载器-bootstrap-classloader)
    - [2.扩展类加载器 extensions classloader](Java-JVM/类加载机制.md#2扩展类加载器-extensions-classloader)
    - [3.应用程序类加载器 application classloader](Java-JVM/类加载机制.md#3应用程序类加载器-application-classloader)
    - [4.自定义类加载器 java.lang.classloder](Java-JVM/类加载机制.md#4自定义类加载器-javalangclassloder)
  - [生命周期](Java-JVM/类加载机制.md#生命周期)
    - [1. 加载](Java-JVM/类加载机制.md#1-加载)
    - [2. 验证](Java-JVM/类加载机制.md#2-验证)
    - [3. 准备](Java-JVM/类加载机制.md#3-准备)
    - [4. 解析](Java-JVM/类加载机制.md#4-解析)
    - [5. 初始化](Java-JVM/类加载机制.md#5-初始化)
  - [双亲委派模型](Java-JVM/类加载机制.md#双亲委派模型)
    - [怎么打破双亲委派模型？](Java-JVM/类加载机制.md#怎么打破双亲委派模型)
- [JVM调优](Java-JVM/JVM调优.md)
  - [原则](Java-JVM/JVM调优.md#原则)
  - [jvm调优](Java-JVM/JVM调优.md#jvm调优)
  - [JVM调优目标](Java-JVM/JVM调优.md#jvm调优目标)
  - [JVM调优的步骤](Java-JVM/JVM调优.md#jvm调优的步骤)
  - [JVM参数解析及调优](Java-JVM/JVM调优.md#jvm参数解析及调优)
- [Java即时编译](Java-JVM/Java即时编译.md)
  - [什么是](Java-JVM/Java即时编译.md#什么是)
  - [Java的执行过程](Java-JVM/Java即时编译.md#java的执行过程)
  - [1.JVM中的编译器](Java-JVM/Java即时编译.md#1jvm中的编译器)
    - [Client Compiler](Java-JVM/Java即时编译.md#client-compiler)
    - [Server Compiler](Java-JVM/Java即时编译.md#server-compiler)
  - [2.分层编译](Java-JVM/Java即时编译.md#2分层编译)
  - [3.即时编译的触发](Java-JVM/Java即时编译.md#3即时编译的触发)
  - [编译优化](Java-JVM/Java即时编译.md#编译优化)
    - [1. 中间表达形式（Intermediate Representation）](Java-JVM/Java即时编译.md#1-中间表达形式intermediate-representation)
    - [2.方法内联](Java-JVM/Java即时编译.md#2方法内联)
    - [3. 逃逸分析](Java-JVM/Java即时编译.md#3-逃逸分析)
      - [1、锁消除](Java-JVM/Java即时编译.md#1锁消除)
      - [2、栈上分配](Java-JVM/Java即时编译.md#2栈上分配)
      - [3、标量替换](Java-JVM/Java即时编译.md#3标量替换)
      - [4、部分逃逸分析](Java-JVM/Java即时编译.md#4部分逃逸分析)
    - [4. Loop Transformations](Java-JVM/Java即时编译.md#4-loop-transformations)
      - [1、循环展开](Java-JVM/Java即时编译.md#1循环展开)
      - [2、循环分离](Java-JVM/Java即时编译.md#2循环分离)
    - [5. 窥孔优化与寄存器分配](Java-JVM/Java即时编译.md#5-窥孔优化与寄存器分配)
 
## <a>Java-多线程</a>

- [线程](Java-多线程/线程.md)
  - [线程的生命状态](Java-多线程/线程.md#线程的生命状态)
    - [新建new](Java-多线程/线程.md#新建new)
    - [可运行runnable](Java-多线程/线程.md#可运行runnable)
    - [阻塞blocked](Java-多线程/线程.md#阻塞blocked)
    - [等待waiting](Java-多线程/线程.md#等待waiting)
    - [期限等待timed waiting](Java-多线程/线程.md#期限等待timed-waiting)
    - [死亡terminated](Java-多线程/线程.md#死亡terminated)
  - [使用线程](Java-多线程/线程.md#使用线程)
      * [继承Thread](Java-多线程/线程.md#继承thread)
      * [实现Runnable接口](Java-多线程/线程.md#实现runnable接口)
      * [实现Callable接口](Java-多线程/线程.md#实现callable接口)
      * [Callable如何返回值的](Java-多线程/线程.md#callable如何返回值的)
      * [FutureTask](Java-多线程/线程.md#futuretask)
  * [线程基本方法](Java-多线程/线程.md#线程基本方法)
      * [wait](Java-多线程/线程.md#wait)
      * [sleep](Java-多线程/线程.md#sleep)
      * [yield](Java-多线程/线程.md#yield)
      * [interrupt](Java-多线程/线程.md#interrupt)
      * [join](Java-多线程/线程.md#join)
      * [notify](Java-多线程/线程.md#notify)
      * [await() signal() signalAll()](Java-多线程/线程.md#await-signal-signalall)
  * [Java里怎么保证多个线程的互斥性](Java-多线程/线程.md#java里怎么保证多个线程的互斥性)
      * [什么是互斥](Java-多线程/线程.md#什么是互斥)
      * [衍生出来就是线程怎么同步的问题](Java-多线程/线程.md#衍生出来就是线程怎么同步的问题)
      * [什么是同步](Java-多线程/线程.md#什么是同步)
  * [线程和进程的区别](Java-多线程/线程.md#线程和进程的区别)
  * [怎么让多个线程有序执行](Java-多线程/线程.md#怎么让多个线程有序执行)
      * [join方法](Java-多线程/线程.md#join方法)
      * [线程池](Java-多线程/线程.md#线程池)
      * [lock-condition](Java-多线程/线程.md#lock-condition)
  * [Java线程和操作系统的线程区别](Java-多线程/线程.md#java线程和操作系统的线程区别)
      * [Java线程在操作系统上本质](Java-多线程/线程.md#java线程在操作系统上本质)
      * [操作系统中的进程（线程）状态](Java-多线程/线程.md#操作系统中的进程线程状态)
      * [操作系统中线程和Java线程状态的关系](Java-多线程/线程.md#操作系统中线程和java线程状态的关系)
- [volatile](Java-多线程/volatile.md)
- [Java对象头](Java-多线程/Java对象头.md)
- [锁机制](Java-多线程/锁机制.md)
- [线程池](Java-多线程/线程池.md)
- [CAS](Java-多线程/CAS.md)
- [AQS](Java-多线程/AQS.md)
- [ThreadLocal](Java-多线程/ThreadLocal.md)

## <a>计算机网络</a>

- [网络协议分层](计算机网络/网络协议分层.md)
- [TCP报文](计算机网络/TCP报文.md)
- [UDP报文](计算机网络/UDP报文.md)
- [IP报文](计算机网络/IP报文.md)  
- [TCP/IP](计算机网络/TCP_IP.md)
- [HTTP](计算机网络/HTTP.md)
- [cookie](计算机网络/cookie和session.md)
- [session](计算机网络/cookie和session.md)
- [JWT](计算机网络/JWT.md)
- [跨域](计算机网络/跨域.md)
- [网络攻击行为](计算机网络/网络攻击行为.md)
- [CDN](计算机网络/CDN.md)
- [HTTP面试题](计算机网络/HTTP面试题.md)

## <a>数据库</a>

### MySQL
- [MySQL](数据库/MySQL.md)
  - [架构](数据库/MySQL.md#架构)
  - [SQL优化](数据库/MySQL.md#sql优化)
  - [储存引擎](数据库/MySQL.md#储存引擎-1)
    - [InnoDB](数据库/MySQL.md#innodb)
    - [MyISAM](数据库/MySQL.md#myisam)
  - [索引](数据库/MySQL.md#索引)
  - [事务](数据库/MySQL.md#事务)
    - [ACID](数据库/MySQL.md#acid)
        - [原子性（Atomicity，或称不可分割性）](数据库/MySQL.md#原子性atomicity或称不可分割性)
        - [一致性（Consistency）](数据库/MySQL.md#一致性consistency)
        - [隔离性（Isolation）](数据库/MySQL.md#隔离性isolation)
          - [隔离级别](数据库/MySQL.md#隔离级别)
            - [读未提交：read uncommitted](数据库/MySQL.md#读未提交read-uncommitted)
            - [读已提交：read committed](数据库/MySQL.md#读已提交read-committed)
            - [可重复读：repeatable read](数据库/MySQL.md#可重复读repeatable-read)
        - [串行化：serializable](数据库/MySQL.md#串行化serializable)
        - [持久性（Durability）](数据库/MySQL.md#持久性durability)
  - [事务日志](数据库/MySQL.md#事务日志)
    - [redo log（重做日志）](数据库/MySQL.md#redo-log重做日志)
    - [undo log（回滚日志）](数据库/MySQL.md#undo-log回滚日志)
  - [二进制日志( binlog )](数据库/MySQL.md#二进制日志-binlog-)
  - [锁](数据库/MySQL.md#锁)
    - [行级锁](数据库/MySQL.md#行级锁)
    - [表级锁](数据库/MySQL.md#表级锁)
    - [页锁](数据库/MySQL.md#页锁)
  - [切分](数据库/MySQL.md#切分)
     - [水平切分](数据库/MySQL.md#水平切分)
     - [垂直切分](数据库/MySQL.md#垂直切分)
  - [复制](数据库/MySQL.md#复制)
    - [主从复制](数据库/MySQL.md#主从复制)
  - [中间件](数据库/MySQL.md#中间件)
    - [mycat](数据库/MySQL.md#mycat)
    - [ShardingSphere](数据库/MySQL.md#shardingsphere)
### MongoDB
- [MongoDB](数据库/MongoDB.md)
  - [特点](数据库/MongoDB.md#特点)
    - [关键组件](数据库/MongoDB.md#关键组件)
      - [_id](数据库/MongoDB.md#_id)
      - [集合](数据库/MongoDB.md#集合)
      - [游标](数据库/MongoDB.md#游标)
      - [数据库](数据库/MongoDB.md#数据库)
      - [文档](数据库/MongoDB.md#文档)
      - [字段](数据库/MongoDB.md#字段)
  - [MongoDB 复制（副本集）](数据库/MongoDB.md#mongodb-复制副本集)
    - [什么是](数据库/MongoDB.md#什么是)
    - [复制结构图](数据库/MongoDB.md#复制结构图)
    - [复制原理](数据库/MongoDB.md#复制原理)
  - [MongoDB 分片](数据库/MongoDB.md#mongodb-分片)
    - [什么是](数据库/MongoDB.md#什么是-1)
    - [分片集群结构](数据库/MongoDB.md#分片集群结构)
    - [三个主要组件](数据库/MongoDB.md#三个主要组件)
      - [Shard](数据库/MongoDB.md#shard)
      - [Config Server](数据库/MongoDB.md#config-server)
      - [Query Routers](数据库/MongoDB.md#query-routers)
### HBASE
- [HBASE](数据库/Hbase.md)
  - [什么是？](数据库/Hbase.md#什么是)
  - [列式存储](数据库/Hbase.md#列式存储)
    - [储存图](数据库/Hbase.md#储存图)
    - [Row Key](数据库/Hbase.md#row-key)
    - [列族ColumnFamily](数据库/Hbase.md#列族columnfamily)
    - [列](数据库/Hbase.md#列属于某一个列簇在-hbase-中可以进行动态的添加)
    - [Cell](数据库/Hbase.md#cell--是指具体的-value)
    - [TimeStamp](数据库/Hbase.md#timestamp-在这张图里面没有显示出来这个是指版本号用时间戳timestamp-来表示)
  - [架构](数据库/Hbase.md#架构)
    - [架构图](数据库/Hbase.md#架构图)
    - [Client](数据库/Hbase.md#client)
    - [Zookeeper](数据库/Hbase.md#zookeeper)
    - [HMaster](数据库/Hbase.md#hmaster)
    - [HRegionServer](数据库/Hbase.md#hregionserver)
  - [Region 寻址方式](数据库/Hbase.md#region-寻址方式)
  - [Hbase 的写逻辑](数据库/Hbase.md#hbase-的写逻辑)
### Elasticsearch
- [Elasticsearch](数据库/Elasticsearch.md)
  - [es的特点](数据库/Elasticsearch.md#es的特点)
  - [应用场景](数据库/Elasticsearch.md#应用场景)
  - [Elasticsearch基本概念](数据库/Elasticsearch.md#elasticsearch基本概念)
    - [索引(index)](数据库/Elasticsearch.md#索引index)
    - [类型(type)](数据库/Elasticsearch.md#类型type)
    - [文档(document)](数据库/Elasticsearch.md#文档document)
    - [映射(mapping)](数据库/Elasticsearch.md#映射mapping)
    - [倒排索引](数据库/Elasticsearch.md#倒排索引)
    - [集群](数据库/Elasticsearch.md#集群)
    - [插入数据流程](数据库/Elasticsearch.md#插入数据流程)
    -[查询数据流程](数据库/Elasticsearch.md#查询数据流程)
    -[es性能优化](数据库/Elasticsearch.md#es性能优化)
        * [加大filesystem cache大小](数据库/Elasticsearch.md#加大filesystem-cache大小)
        * [数据预热](数据库/Elasticsearch.md#数据预热)
        * [冷热分离](数据库/Elasticsearch.md#冷热分离)
        * [document设计](数据库/Elasticsearch.md#document设计)
        * [禁止直接分页](数据库/Elasticsearch.md#禁止直接分页)
    - [es的分词器有哪些](数据库/Elasticsearch.md#es的分词器有哪些)
    - [es为什么这么快](数据库/Elasticsearch.md#es为什么这么快)
## <a>消息队列</a>

- [为什么使用消息队列](消息队列/mq常见面试题.md#为什么要使用消息队列)
- [Redis](消息队列/Redis.md)
- [RabbitMQ](消息队列/RabbitMQ.md)
- [RocketMQ](消息队列/RocketMQ.md)
- [Kafka](消息队列/Kafka.md)
- [Zookeeper](消息队列/Zookeeper.md)
- [pulsar](消息队列/Pulsar.md)
- [常见面试题](消息队列/mq常见面试题.md)

## <a>Redis</a>

- [特点](Redis/redis.md#特点)
- [Redis为什么这么快](Redis/redis.md#Redis为什么这么快)
- [常见使用场景](Redis/redis.md#常见使用场景)
- [数据类型](Redis/redis.md#数据类型)
- [内存回收策略](Redis/redis.md#内存回收策略)
- [持久化方式](Redis/redis.md#持久化方式)
- [Redis中的事务](Redis/redis.md#redis-中的事务)
- [常问故障场景](Redis/redis.md#常问故障场景)
- [集群](Redis/redis.md#集群)

## <a>Spring</a>

- [Spring](Spring/Spring.md)
- [SpringMVC](Spring/SpringMVC.md)
- [SpringBoot](Spring/Springboot.md)

## <a>Springcloud</a>

- [SpringCloud](SpringCloud/springcloud.md#springcloud)
- [SpringCloudAlibaba](SpringCloud/springcloud.md#springcloudalibaba)

## <a>Linux</a>

- [文件和目录的操作](Linux/linux.md#文件和目录的操作)
- [查看文件](Linux/linux.md#查看文件)
- [管理用户](Linux/linux.md#管理用户)
- [进程管理](Linux/linux.md#进程管理)
- [打包和压缩文件](Linux/linux.md#打包和压缩文件)
- [grep+正则表达式](Linux/linux.md#grep)
- [Vi编辑器](Linux/linux.md#Vi编辑器)
- [权限管理](Linux/linux.md#权限管理)
- [网络管理](Linux/linux.md#网络管理)
- [cpu100%怎么排查](Linux/linux.md#cpu100怎么排查)
- [用户空间与内核空间](Linux/linux.md#用户空间与内核空间)
- [进程切换](Linux/linux.md#进程切换)
- [进程的阻塞](Linux/linux.md#进程的阻塞)
- [文件描述符fd](Linux/linux.md#文件描述符fd)
- [缓存 I/O](Linux/linux.md#缓存-io)
- [IO模型](Linux/linux.md#io模型)
- [select、poll、epoll](Linux/linux.md#selectpollepoll)

## <a>Mybatis</a>

- [什么是mybatis](Mybatis/mybatis.md)
- [JDBC执行六步骤](Mybatis/mybatis.md)
- [mybatis执行8步骤](Mybatis/mybatis.md)
- [MyBatis整体架构](Mybatis/mybatis.md)
- [mybatis缓存](Mybatis/mybatis.md)

## <a>Netty</a>

- [重要的组件](Netty/netty.md#重要的组件)
- [netty的使用示例](Netty/netty.md#netty的使用示例)
- [TCP粘包/拆包问题](Netty/netty.md#tcp粘包拆包问题)
- [解编码技术](Netty/netty.md#解编码技术)
- [高性能的原因](Netty/netty.md#高性能的原因)

## <a>分布式相关</a>

- [分布式锁](分布式相关/分布式锁.md)
- [分布式事务](分布式相关/分布式事务.md)
- [CAP理论](分布式相关/CAP.md)
- [BASE](分布式相关/BASE.md)
- [一致性算法](分布式相关/一致性算法.md)

## <a>容器技术</a>

- [docker](容器技术/docker.md)
- k8s

## <a>数据结构和算法</a>

- [排序算法](数据结构和算法/排序算法.md)
- 树相关
- BFS
- DFS
- 回溯算法
- 二分法
- 贪心算法
- 动态规划
- 分治思想
- [LRU](数据结构和算法/LFU.md)
- [LFU](数据结构和算法/LRU.md)
- [加减乘除](数据结构和算法/加减乘除.md)

## <a>设计模式</a>

- [工厂模式](设计模式/工厂模式.md)
- [单例模式](设计模式/单例模式.md)
- 建造者模式
- 原型模式
- 适配器模式
- [装饰器模式](设计模式/装饰者模式.md)
- 代理模式
- 外观模式
- 桥接模式
- 组合模式
- 享元模式
- [策略模式](设计模式/策略模式.md)
- 模板方法模式
- 观察者模式
- 迭代子模式
- 责任链模式
- 备忘录模式
- 状态模式
- 访问者模式
- 中介者模式
- 解释器模式

## <a>职业规划和学习习惯</a>

- [项目中遇到的问题](职业规划和学习习惯/职业规划和学习习惯.md#项目中遇到的问题)
- [职业规划](职业规划和学习习惯/职业规划和学习习惯.md#职业规划)
- [平时规则](职业规划和学习习惯/职业规划和学习习惯.md#平时规则)

## <a>场景设计</a>

- [有A、B两个大文件，每个文件几十G,而内存只有4G,其中A文件存放学号+姓名，而B文件存放学号+分数，要求生成文件C，存放姓名和分数。怎么实现?](场景设计/场景设计.md)
- [秒杀系统怎么设计](场景设计/场景设计.md#秒杀系统怎么设计)
- [唯一ID设计](场景设计/场景设计.md#唯一ID设计)
- [产品上线出问题怎么定位错误](场景设计/场景设计.md#产品上线出问题怎么定位错误)
- [大量并发查询用户商品信息，MySQL压力大查询慢，保证速度怎么优化方案](场景设计/场景设计.md#大量并发查询用户商品信息，MySQL压力大查询慢，保证速度怎么优化方案)
- [海量日志数据，提取出某日访问百度次数最多的那个IP。给定a、b两个文件，各存放50亿个url,每个url各 占64字节，内存限制是4G,让你找出a、b文件共同的url?](场景设计/场景设计.md)
- [一般内存不足而需要分析的数据又很大的问题都可以使用分治的思想，将数据hash(x)%1000分为小文件再分别加载小文件到内存中处理即可](场景设计/场景设计.md#一般内存不足而需要分析的数据又很大的问题都可以使用分治的思想将数据hashx1000分为小文件再分别加载小文件到内存中处理即可)
- [如何保证接口的幂等性](场景设计/场景设计.md#如何保证接口的幂等性)
- [什么是延迟双删](场景设计/场景设计.md#什么是延迟双删)
- [什么是SPI](场景设计/场景设计.md#什么是SPI)
- [什么是RPC？](场景设计/场景设计.md#什么是rpc)
- [gRPC](场景设计/场景设计.md#gRPC)
- [一个优秀的RPC框架需要考虑的问题](场景设计/场景设计.md#一个优秀的RPC框架需要考虑的问题)
- [什么是DDD](场景设计/场景设计.md#什么是ddd)
- [Java实现生产者消费者](场景设计/场景设计.md#java实现生产者消费者)
- [Java实现BlockQueue](场景设计/场景设计.md#java实现blockqueue)
- [解决哈希冲突的方法](场景设计/场景设计.md#解决哈希冲突的方法)
- [排行榜设计](场景设计/场景设计.md#排行榜设计)

## <a>智力题</a>

- [100只试管里有-只是有毒的，现在有10个小白鼠，如何最快速地判断出那只试管有毒](智力题/智力题.md)
- [共1000瓶药水，其中I瓶有毒药。已知小白鼠喝毒药一天内死若想在一天内找到毒药，最少需要几只小白鼠?](智力题/智力题.md)
- [只有两个无刻度的水桶，-个可以装6L水，-一个可以装5L水，如何在桶里装入3L的水](智力题/智力题.md)
- [25匹马，5个赛道， 每次只能同时有5匹马跑，最少比赛几次选出前三名?家里有两个孩子,一个是女孩，另一个也是女孩的概率是多少?](智力题/智力题.md)
- [烧一根不均匀的绳，从头烧到尾总共需要1个小时。现在有若干条材质相同的绳子，问如何用烧绳的方法来计时一个小时十五分钟呢?](智力题/智力题.md)
- [共12个一样的小球，其中只有一个重量与其它不一一样(未知轻重)，给你一个天平，找出那个不同重量的球?](智力题/智力题.md)
- [有10瓶药，每瓶有10粒药，其中有一瓶是变质的。好药每颗重1克，变质的药每颗比好药重0.1克。问怎样用天秤称一次找出变质的那瓶药？](智力题/智力题.md)
- [你有两个罐子，50个红色弹球，50个蓝色弹球，如何将这100个球放入到两个罐子，随机选出一个罐子取出的球为红球的概率最大?](智力题/智力题.md)
- [抢30是双人游戏，游戏规则是:第一个人喊"1"或"2"，第二个人要接着往下喊一个或两个数，然后再轮到第一个人。 两人轮流进行下去。最后喊30的人获胜。问喊数字的最佳策略。](智力题/智力题.md)
- [某人进行10次打靶，每次打靶可能的得分为0到10分，10次打靶共得90分的可能性有多少种](智力题/智力题.md)

## <a>项目架构</a>
- TODO
## <a>面试解答</a>

- [面试解答6月牛客](面试解答/面试解答2021-06.md)
- [面试解答7月牛客](面试解答/面试解答2021-07.md)
- [面试解答9月牛客](面试解答/面试解答2021-09.md)
- [面试解答10月牛客](面试解答/面试解答2021-10.md)

## <a>商城类问题</a>

- [秒杀](商城类问题/商城类问题.md#秒杀)
- [超卖](商城类问题/商城类问题.md#如何解决超卖问题)
- [订单延迟](商城类问题/商城类问题.md#订单延时取消怎么做)

## <a>python</a>

- [如何离线移植依赖包](Python/Python.md)

# 知识点梳理
点击查看：[知识点大图](img/Java.png)

# 免责声明
> **:bangbang:某些知识点、观点、图片是从各种优秀博主、作者、大佬们的文章里或文献里提取的，我只是搬运工，如果觉得有侵犯到您的权益，请联系我，我将根据您的要求修改（添加您的出处链接、删除、修改....），谢谢大佬！**


# 彩蛋

[md code]

[comment]: <> (如果你发现了这行字：快转行吧！！！Java不仅卷，学的东西真的T多了，呜呜呜呜~~~~)

# 最后

`remind` 不积跬步无以至千里

邓宁克鲁格效应

![](img/邓宁克鲁格效应.png)