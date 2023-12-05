<h1 align="center">JavaDeveloperBrain</h1>

<div align="center">

[comment]: <> ([![GitHub issues]&#40;https://img.shields.io/github/issues/Swayingleaves/JavaDeveloperBrain?style=for-the-badge&#41;]&#40;https://github.com/Swayingleaves/JavaDeveloperBrain/issues&#41;)
[![GitHub forks](https://img.shields.io/github/forks/Swayingleaves/JavaDeveloperBrain?style=for-the-badge)](https://github.com/Swayingleaves/JavaDeveloperBrain/network)
[![GitHub stars](https://img.shields.io/github/stars/Swayingleaves/JavaDeveloperBrain?style=for-the-badge)](https://github.com/Swayingleaves/JavaDeveloperBrain/stargazers)
![Java进阶](https://img.shields.io/badge/JAVA-%E5%9F%BA%E7%A1%80%2F%E8%BF%9B%E9%98%B6-green?style=for-the-badge)

</div>

<p align="center">[Java工程师必备+学习+知识点+面试]：包含计算机网络知识、JavaSE、JVM、Spring、Springboot、SpringCloud、Mybatis、多线程并发、netty、MySQL、MongoDB、Elasticsearch、Redis、HBASE、RabbitMQ、RocketMQ、Pulsar、Kafka、Zookeeper、Linux、设计模式、智力题、项目架构、分布式相关、算法、面试题</p>

---

<h3 align="center">:star2:<a href="TODO.md">TODO list</a>:star2:</h3>

# 内容概览[↓↓](#最后)

<table>
<thead>

</thead>
<tbody>
  <tr>
    <th ><b>Java</b></th>
    <td ><a href="#java-基础部分">基础部分</a></td>
    <td ><a href="#java-jvm">JVM</a></td>
    <td ><a href="#java-多线程">多线程</a></td>
    <td ></td>
  </tr>
  <tr>
    <th  rowspan="2"><b>计算机网络</b></th>
    <td ><a href="#计算机网络">网络协议分层</a></td>
    <td ><a href="#tcp报文">TCP</a></td>
    <td ><a href="#UDP报文">UDP</a></td>
    <td ><a href="#三次握手">三次握手</a></td>
    <td ><a href="#四次挥手">四次挥手</a></td>
  </tr>
  <tr>
    <td ><a href="#TCP怎么保障可靠传输">TCP怎么保障可靠传输</a></td>
    <td ><a href="#HTTPS">HTTPS</a></td>
    <td ><a href="#HTTP面试题">HTTP面试题</a></td>
    <td ></td>
    <td ></td>
  </tr>
  <tr>
    <th rowspan="2"><b>数据库</b></th>
    <td ><a href="#mysql">MySQL</a></td>
    <td ><a href="#mongodb">MongoDB</a></td>
    <td ><a href="#hbase">HBASE</a></td>
    <td ><a href="#nebula-graph">Nebula Graph</a></td>
    <td ><a href="#elasticsearch">Elasticsearch</a></td>
  </tr>
  <tr>
    <td ><a href="#redis-1">Redis</a></td>
    <td ><a href="#sql问题">SQL问题</a></td>
    <td ></td>
    <td ></td>
    <td ></td>
  </tr>
  <tr>
    <th rowspan="2"><b>消息队列</b></th>
    <td ><a href="#redis">Redis</a></td>
    <td ><a href="#rabbitmq">RabbitMQ</a></td>
    <td ><a href="#rocketmq">RocketMQ</a></td>
    <td ><a href="#kafka">Kafka</a></td>
    <td ><a href="#zookeeper">Zookeeper</a></td>
  </tr>
  <tr>
    <td ><a href="#pulsar">Pulsar</a></td>
    <td ></td>
    <td ></td>
    <td ></td>
    <td ></td>
  </tr>

  <tr>
    <th rowspan="2"><b>框架</b></th>
    <td ><a href="#spring">Spring</a></td>
    <td ><a href="#springmvc">SpringMVC</a></td>
    <td ><a href="#springboot">SpringBoot</a></td>
    <td ><a href="#springcloud">SpringCloud</a></td>
    <td ><a href="#springcloudalibaba">SpringCloudAlibaba</a></td>
  </tr>
 <tr>
    <td ><a href="#mybatis">Mybatis</a></td>
    <td ><a href="#netty">Netty</a></td>
    <td ></td>
    <td ></td>
    <td ></td>
  </tr>
  <tr>
    <th ><a href="#linux"><b>Linux</b></a></th>
    <td ><a href="#linux的进程线程文件描述符是什么">进程、线程、文件描述符</a></td>
    <td ><a href="#IO模型">IO模型</a></td>
    <td ><a href="#selectpollepoll">select、poll、epoll</a></td>
    <td ></td>
  </tr>
  <tr>
    <th ><a href="#分布式相关"><b>分布式相关</b></a></th>
    <td ><a href="#分布式锁">分布式锁</a></td>
    <td ><a href="#分布式事务">分布式事务</a></td>
    <td ><a href="#分布式唯一ID设计">分布式唯一ID设计</a></td>
    <td ><a href="#CAP理论">CAP理论</a></td>
    <td ><a href="#一致性算法">一致性算法</a></td>
  </tr>
  <tr>
    <th ><a href="#架构"><b>架构</b></a></th>
    <td ><a href="#系统设计">系统设计</a></td>
    <td ><a href="#计算和储存分离">计算和储存分离</a></td>
    <td ><a href="#DDD领域驱动设计">DDD领域驱动设计</a></td>
    <td ></td>
  </tr>
  <tr>
    <th ><a href="#容器技术"><b>容器技术</b></a></th>
    <td ><a href="#docker">Docker</a></td>
    <td ><a href="#kubernetes">Kubernetes</a></td>
    <td ></td>
    <td ></td>
  </tr>
  <tr>
    <th rowspan="2"><a href="#数据结构和算法"><b>数据结构和算法</b></a></th>
    <td ><a href="#排序算法">排序算法</a></td>
    <td ><a href="#树相关">树相关</a></td>
    <td ><a href="#BFS">BFS</a></td>
    <td ><a href="#DFS">DFS</a></td>
    <td ><a href="#回溯算法">回溯算法</a></td>
  </tr>
 <tr>
    <td ><a href="#二分法">二分法</a></td>
    <td ><a href="#贪心算法">贪心算法</a></td>
    <td ><a href="#动态规划">动态规划</a></td>
    <td ><a href="#分治思想">分治思想</a></td>
    <td ></td>
  </tr>
  <tr>
    <th ><a href="#设计模式"><b>设计模式</b></a></th>
    <td ></td>
    <td ></td>
    <td ></td>
    <td ></td>
  </tr>
  <tr>
    <th ><b>面试</b></th>
    <td ><a href="#职业规划和学习习惯">职业规划和学习习惯</a></td>
    <td ><a href="#场景设计">场景设计</a></td>
    <td ><a href="#智力题">智力题</a></td>
    <td ><a href="#面试解答">面试解答</a></td>
    <td ><a href="#商城类问题">商城类问题</a></td>
  </tr>
</tbody>
</table>

# 内容详情

## <a>Java-基础部分</a>[↑↑](#内容概览)

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
- 容器
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
- [Java虚拟线程](Java-基础/虚拟线程.md)

## <a>Java-JVM</a>[↑↑](#内容概览)

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

    * [方法区的回收](Java-JVM/垃圾回收.md#方法区的回收)
    * [finalize()](Java-JVM/垃圾回收.md#finalize)
    * [引用类型](Java-JVM/垃圾回收.md#引用类型)
        * [强引用](Java-JVM/垃圾回收.md#强引用)
        * [软引用](Java-JVM/垃圾回收.md#软引用)
        * [弱引用](Java-JVM/垃圾回收.md#弱引用)
        * [虚引用](Java-JVM/垃圾回收.md#虚引用)

    - [分代收集理论](Java-JVM/垃圾回收.md#分代收集理论)
    - [Java对象头](Java-JVM/Java对象头.md)
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
    - [2.分层编译](Java-JVM/Java即时编译.md#2分层编译)
    - [3.即时编译的触发](Java-JVM/Java即时编译.md#3即时编译的触发)
    - [编译优化](Java-JVM/Java即时编译.md#编译优化)
        - [1. 中间表达形式（Intermediate Representation）](Java-JVM/Java即时编译.md#1-中间表达形式intermediate-representation)
        - [2.方法内联](Java-JVM/Java即时编译.md#2方法内联)
        - [3. 逃逸分析](Java-JVM/Java即时编译.md#3-逃逸分析)
        - [4. Loop Transformations](Java-JVM/Java即时编译.md#4-loop-transformations)
        - [5. 窥孔优化与寄存器分配](Java-JVM/Java即时编译.md#5-窥孔优化与寄存器分配)

## <a>Java-多线程</a>[↑↑](#内容概览)

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
    * [机器内存模型](Java-多线程/volatile.md#机器内存模型)
        * [多核下的缓存一致性问题](Java-多线程/volatile.md#多核下的缓存一致性问题)
        * [指令重排](Java-多线程/volatile.md#指令重排)
    * [JMM](Java-多线程/volatile.md#jmm)
    * [作用](Java-多线程/volatile.md#作用)
        * [可见性](Java-多线程/volatile.md#可见性)
        * [禁止指令重排](Java-多线程/volatile.md#禁止指令重排)
    * [volatile解决可见性的代码](Java-多线程/volatile.md#volatile解决可见性的代码)
    * [验证volatile不具备原子性](Java-多线程/volatile.md#验证volatile不具备原子性)
- [Java对象头](Java-多线程/Java对象头.md)
- [锁机制](Java-多线程/锁机制.md)
    * [Synchronized](Java-多线程/锁机制.md#synchronized)
    * [Lock](Java-多线程/锁机制.md#lock)
        * [ReentrantLock](Java-多线程/锁机制.md#reentrantlock)
    * [锁优化](Java-多线程/锁机制.md#锁优化)
        * [自旋锁](Java-多线程/锁机制.md#自旋锁)
        * [循环](Java-多线程/锁机制.md#循环)
        * [锁消除](Java-多线程/锁机制.md#锁消除)
        * [锁粗化](Java-多线程/锁机制.md#锁粗化)
        * [锁升级](Java-多线程/锁机制.md#锁升级)
    * [死锁](Java-多线程/锁机制.md#死锁)
    * [synchronized锁和lock锁的区别](Java-多线程/锁机制.md#synchronized锁和lock锁的区别)
- [线程池](Java-多线程/线程池.md)
    * [创建线程池的方式](Java-多线程/线程池.md#创建线程池的方式)
        * [1、Executors](Java-多线程/线程池.md#1executors)
            * [newCachedThreadPool](Java-多线程/线程池.md#newcachedthreadpool)
            * [newFixedThreadPool](Java-多线程/线程池.md#newfixedthreadpool)
            * [newScheduledThreadPool](Java-多线程/线程池.md#newscheduledthreadpool)
            * [newSingleThreadExecutor](Java-多线程/线程池.md#newsinglethreadexecutor)
        * [2、ThreadPoolExecutor](Java-多线程/线程池.md#2threadpoolexecutor)
    * [ThreadPoolExecutor](Java-多线程/线程池.md#threadpoolexecutor-1)
        * [参数含义](Java-多线程/线程池.md#参数含义)
    * [ThreadPoolExecutor原理流程](Java-多线程/线程池.md#threadpoolexecutor原理流程)
    * [如何释放线程](Java-多线程/线程池.md#如何释放线程)
    * [如何设置线程数](Java-多线程/线程池.md#如何设置线程数)
- [CAS](Java-多线程/CAS.md)
    * [原理](Java-多线程/CAS.md#原理)
    * [参数](Java-多线程/CAS.md#参数)
    * [CAS的问题](Java-多线程/CAS.md#cas的问题)
- [AQS](Java-多线程/AQS.md)
    * [AQS（AbstractQueuedSynchronizer）](Java-多线程/AQS.md#aqsabstractqueuedsynchronizer)
        * [工作原理概要](Java-多线程/AQS.md#工作原理概要)
        * [同步队列模型](Java-多线程/AQS.md#同步队列模型)
    * [ReentrantLock](Java-多线程/AQS.md#reentrantlock)
        * [Sync (extends AbstractQueuedSynchronizer)](Java-多线程/AQS.md#sync-extends-abstractqueuedsynchronizer)
        * [NonfairSync (extends Sync) 非公平锁](Java-多线程/AQS.md#nonfairsync-extends-sync-非公平锁)
            * [lock](Java-多线程/AQS.md#lock)
            * [unlock](Java-多线程/AQS.md#unlock)
        * [FairSync (extends Sync) 公平锁](Java-多线程/AQS.md#fairsync-extends-sync-公平锁)
        * [Condition](Java-多线程/AQS.md#condition)
        * [同步工具类](Java-多线程/AQS.md#同步工具类)
            * [CountDownLatch](Java-多线程/AQS.md#countdownlatch)
            * [CyclicBarrier](Java-多线程/AQS.md#cyclicbarrier)
            * [Semaphore](Java-多线程/AQS.md#semaphore)
- [ThreadLocal](Java-多线程/ThreadLocal.md)
    * [原理](Java-多线程/ThreadLocal.md#原理)
    * [ThreadLocalMap](Java-多线程/ThreadLocal.md#threadlocalmap)
    * [源码分析](Java-多线程/ThreadLocal.md#源码分析)
        * [get](Java-多线程/ThreadLocal.md#get)
        * [set](Java-多线程/ThreadLocal.md#set)
    * [使用场景](Java-多线程/ThreadLocal.md#使用场景)
        * [每个线程维护了一个“序列号”](Java-多线程/ThreadLocal.md#每个线程维护了一个序列号)
        * [Session的管理](Java-多线程/ThreadLocal.md#session的管理)
        * [SimpleDateFormat](Java-多线程/ThreadLocal.md#simpledateformat)
    * [手动释放ThreadLocal遗留存储?你怎么去设计/实现？](Java-多线程/ThreadLocal.md#手动释放threadlocal遗留存储你怎么去设计实现)
    * [弱引用导致内存泄漏，那为什么key不设置为强引用](Java-多线程/ThreadLocal.md#弱引用导致内存泄漏那为什么key不设置为强引用)
    * [线程执行结束后会不会自动清空Entry的value](Java-多线程/ThreadLocal.md#线程执行结束后会不会自动清空entry的value)
    * [threadlocal如果不remove，出问题了怎么补救？](Java-多线程/ThreadLocal.md#threadlocal如果不remove出问题了怎么补救)
    * [FastThreadLocal](Java-多线程/ThreadLocal.md#fastthreadlocal)

## <a>计算机网络</a>[↑↑](#内容概览)

- [网络协议分层](计算机网络/网络协议分层.md)
    * [OSI 7层(基本只是拿来作比较)](计算机网络/网络协议分层.md#osi-7层基本只是拿来作比较)
    * [TCP/IP 5(4)层](计算机网络/网络协议分层.md#tcpip-54层)
        * [应用层](计算机网络/网络协议分层.md#应用层)
            * [常见的协议](计算机网络/网络协议分层.md#常见的协议)
                * [域名系统](计算机网络/网络协议分层.md#域名系统)
                * [文件传送协议](计算机网络/网络协议分层.md#文件传送协议)
                * [SMTP电子邮件协议](计算机网络/网络协议分层.md#smtp电子邮件协议)
                * [远程登录协议](计算机网络/网络协议分层.md#远程登录协议)
        * [传输层](计算机网络/网络协议分层.md#传输层)
            * [常见的协议](计算机网络/网络协议分层.md#常见的协议-1)
                * [TCP](计算机网络/网络协议分层.md#tcp)
                * [UDP](计算机网络/网络协议分层.md#udp)
        * [网络层](计算机网络/网络协议分层.md#网络层)
        * [数据链路层](计算机网络/网络协议分层.md#数据链路层)
            * [封装成帧](计算机网络/网络协议分层.md#封装成帧)
            * [透明传输](计算机网络/网络协议分层.md#透明传输)
            * [差错检测](计算机网络/网络协议分层.md#差错检测)
        * [物理层](计算机网络/网络协议分层.md#物理层)
- #### <a href="计算机网络/TCP报文.md">TCP报文</a>
- #### <a href="计算机网络/UDP报文.md">UDP报文</a>
- [IP报文](计算机网络/IP报文.md)
- [TCP/IP](计算机网络/TCP_IP.md)
    * [UDP 和 TCP 的特点](计算机网络/TCP_IP.md#udp-和-tcp-的特点)
        * [UDP](计算机网络/TCP_IP.md#udp)
        * [TCP](计算机网络/TCP_IP.md#tcp)

    * #### <a href="计算机网络/TCP_IP.md#三次握手">三次握手</a>
    * #### <a href="计算机网络/TCP_IP.md#四次挥手">四次挥手</a>
    * #### <a href="计算机网络/TCP_IP.md#tcp怎么保障可靠传输">TCP怎么保障可靠传输</a>
        * [数据合理分片和排序](计算机网络/TCP_IP.md#数据合理分片和排序)
        * [数据校验：校验和](计算机网络/TCP_IP.md#数据校验校验和)
        * [TCP 的接收端会丢弃重复的数据](计算机网络/TCP_IP.md#tcp-的接收端会丢弃重复的数据)
        * [超时重传](计算机网络/TCP_IP.md#超时重传)
        * [流量控制](计算机网络/TCP_IP.md#流量控制)
        * [拥塞控制](计算机网络/TCP_IP.md#拥塞控制)
        * [ARQ协议](计算机网络/TCP_IP.md#arq协议)
    * [如何实现可靠UDP传输](计算机网络/TCP_IP.md#如何实现可靠udp传输)
    * [HTTP长连接还是短连接？](计算机网络/TCP_IP.md#http长连接还是短连接)
- [HTTP](计算机网络/HTTP.md)
    * [特点](计算机网络/HTTP.md#特点)
    * [方法](计算机网络/HTTP.md#方法)
        * [get](计算机网络/HTTP.md#get)
        * [head](计算机网络/HTTP.md#head)
        * [post](计算机网络/HTTP.md#post)
        * [put](计算机网络/HTTP.md#put)
        * [patch](计算机网络/HTTP.md#patch)
        * [delete](计算机网络/HTTP.md#delete)
        * [options](计算机网络/HTTP.md#options)
        * [connect](计算机网络/HTTP.md#connect)
        * [trace](计算机网络/HTTP.md#trace)
    * [状态码](计算机网络/HTTP.md#状态码)
        * [1XX](计算机网络/HTTP.md#1xx)
        * [2XX](计算机网络/HTTP.md#2xx)
        * [3XX](计算机网络/HTTP.md#3xx)
        * [4XX](计算机网络/HTTP.md#4xx)
        * [5XX](计算机网络/HTTP.md#5xx)
    * #### <a href="计算机网络/HTTP.md#https">HTTPS</a>
        * [什么是HTTPS](计算机网络/HTTP.md#什么是https)
        * [端口](计算机网络/HTTP.md#端口)
        * [HTTPS解决的问题](计算机网络/HTTP.md#https解决的问题)
        * [HTTPS加密过程](计算机网络/HTTP.md#https加密过程)
    * [HTTPS的CA证书放了什么，公钥放在CA里吗？](计算机网络/HTTP.md#https的ca证书放了什么公钥放在ca里吗)
    * [CA证书是在客户端还是服务器](计算机网络/HTTP.md#ca证书是在客户端还是服务器)
    * [HTTP1.1和HTTP1.0的主要区别](计算机网络/HTTP.md#http11和http10的主要区别)
    * [HTTP2.0和HTTP1.x的区别](计算机网络/HTTP.md#http20和http1x的区别)
    * [HTTP的request和response格式](计算机网络/HTTP.md#http的request和response格式)
- [cookie](计算机网络/cookie和session.md)
- [session](计算机网络/cookie和session.md)
- [JWT](计算机网络/JWT.md)
    * [<a href="#">json web token</a>](计算机网络/JWT.md#json-web-token)
    * [<a href="#">格式</a>](计算机网络/JWT.md#格式)
    * [<a href="#">特点</a>](计算机网络/JWT.md#特点)
- [跨域](计算机网络/跨域.md)
    * [<a href="#">什么是跨域？</a>](计算机网络/跨域.md#什么是跨域)
    * [<a href="#">同源策略</a>](计算机网络/跨域.md#同源策略)
    * [<a href="#">解决方案</a>](计算机网络/跨域.md#解决方案)
        * [<a href="#">JSONP</a>](计算机网络/跨域.md#jsonp)
        * [<a href="#">CORS</a>](计算机网络/跨域.md#cors)
- [网络攻击行为](计算机网络/网络攻击行为.md)
    * [CSRF攻击](计算机网络/网络攻击行为.md#csrf攻击)
    * [XSS](计算机网络/网络攻击行为.md#xss)
    * [SQL注入](计算机网络/网络攻击行为.md#sql注入)
    * [DDOS](计算机网络/网络攻击行为.md#ddos)
    * [SYN Flood攻击](计算机网络/网络攻击行为.md#syn-flood攻击)
- [CDN](计算机网络/CDN.md)
    * [<a href="#">什么是CDN</a>](计算机网络/CDN.md#什么是cdn)
    * [<a href="#">好处</a>](计算机网络/CDN.md#好处)
- #### <a href="计算机网络/HTTP面试题.md">HTTP面试题</a>
    * [在浏览器中输入url地址显示主页的过程](计算机网络/HTTP面试题.md#在浏览器中输入url地址显示主页的过程)
    * [QPS和TPS的区别](计算机网络/HTTP面试题.md#qps和tps的区别)
    * [有哪些编码格式(GBK,UTF-8,ISO-)有没有想过为什么会有这么多的编码格式](计算机网络/HTTP面试题.md#有哪些编码格式gbkutf-8iso-有没有想过为什么会有这么多的编码格式)
    * [实现一个长URL转短URL](计算机网络/HTTP面试题.md#实现一个长url转短url)

## <a>数据库</a>[↑↑](#内容概览)

### MySQL[↑↑](#内容概览)

- [MySQL](数据库/MySQL.md)
    - [架构](数据库/MySQL.md#架构)
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
    - [SQL优化](数据库/MySQL.md#sql优化)
    - [MySQL与PostGreSQL的区别](数据库/MySQL.md#mysql与postgresql的区别)

### SQL问题

* [count(*)分页](数据库/count.md)

### MongoDB[↑↑](#内容概览)

* [MongoDB](数据库/MongoDB.md#mongodb)
* [特点](数据库/MongoDB.md#特点)
* [关键组件](数据库/MongoDB.md#关键组件)
    * [_id](#数据库/MongoDB.md_id)
    * [集合](数据库/MongoDB.md#集合)
    * [游标](数据库/MongoDB.md#游标)
    * [数据库](数据库/MongoDB.md#数据库)
    * [文档](数据库/MongoDB.md#文档)
    * [字段](数据库/MongoDB.md#字段)
* [单机mongo架构](数据库/MongoDB.md#单机mongo架构)
* [集群模式1-MongoDB 复制（副本集）Replica set(主从关系)](数据库/MongoDB.md#集群模式1-mongodb-复制副本集replica-set主从关系)
* [集群模式2-MongoDB 分片](数据库/MongoDB.md#集群模式2-mongodb-分片)
* [WiredTiger存储引擎](数据库/MongoDB.md#wiredtiger存储引擎)

### HBASE[↑↑](#内容概览)

* [HBASE](数据库/Hbase.md#hbase)
    * [什么是？](数据库/Hbase.md#什么是)
    * [列式存储](数据库/Hbase.md#列式存储)
    * [架构](数据库/Hbase.md#架构)
        * [架构图](数据库/Hbase.md#架构图)
* [HBase 架构组件](数据库/Hbase.md#hbase-架构组件)
    * [Regions](数据库/Hbase.md#regions)
    * [HBase Master](数据库/Hbase.md#hbase-master)
    * [Zookeeper](数据库/Hbase.md#zookeeper)
    * [HBase Meta Table](数据库/Hbase.md#hbase-meta-table)
    * [Region Server 组成](数据库/Hbase.md#region-server-组成)
    * [HBase 写数据步骤](数据库/Hbase.md#hbase-写数据步骤)
    * [HBase MemStore](数据库/Hbase.md#hbase-memstore)
    * [HBase Region Flush](数据库/Hbase.md#hbase-region-flush)
    * [HBase HFile](数据库/Hbase.md#hbase-hfile)
    * [HBase Read 合并](数据库/Hbase.md#hbase-read-合并)
    * [HBase Minor Compaction](数据库/Hbase.md#hbase-minor-compaction)
    * [HBase Major Compaction](数据库/Hbase.md#hbase-major-compaction)
    * [Region = Contiguous Keys](数据库/Hbase.md#region--contiguous-keys)
    * [Region 分裂](数据库/Hbase.md#region-分裂)
    * [Region 负载均衡](数据库/Hbase.md#region-负载均衡)
    * [HDFS 数据备份](数据库/Hbase.md#hdfs-数据备份)
    * [HBase 故障恢复](数据库/Hbase.md#hbase-故障恢复)
* [Apache HBase 架构的优缺点](数据库/Hbase.md#apache-hbase-架构的优缺点)
    * [优点](数据库/Hbase.md#优点)
    * [缺点](数据库/Hbase.md#缺点)

### Elasticsearch[↑↑](#内容概览)

* [Elasticsearch](数据库/Elasticsearch.md#elasticsearch)
    * [es的特点](数据库/Elasticsearch.md#es的特点)
    * [应用场景](数据库/Elasticsearch.md#应用场景)
* [Elasticsearch基本概念](数据库/Elasticsearch.md#elasticsearch基本概念)
    * [索引(index)](数据库/Elasticsearch.md#索引index)
    * [类型(type)](数据库/Elasticsearch.md#类型type)
    * [文档(document)](数据库/Elasticsearch.md#文档document)
    * [映射(mapping)](数据库/Elasticsearch.md#映射mapping)
    * [倒排索引](数据库/Elasticsearch.md#倒排索引)
* [集群](数据库/Elasticsearch.md#集群)
    * [基本概念](数据库/Elasticsearch.md#基本概念)
        * [节点(Node)](数据库/Elasticsearch.md#节点node)
        * [集群(Cluster)](数据库/Elasticsearch.md#集群cluster)
        * [分片索引(Shard)](数据库/Elasticsearch.md#分片索引shard)
        * [索引副本(Replica)](数据库/Elasticsearch.md#索引副本replica)
    * [集群简单原理](数据库/Elasticsearch.md#集群简单原理)
    * [插入数据流程](数据库/Elasticsearch.md#插入数据流程)
    * [查询数据流程](数据库/Elasticsearch.md#查询数据流程)
* [选举算法](数据库/Elasticsearch.md#选举算法)
* [es性能优化](数据库/Elasticsearch.md#es性能优化)
    * [加大filesystem cache大小](数据库/Elasticsearch.md#加大filesystem-cache大小)
    * [数据预热](数据库/Elasticsearch.md#数据预热)
    * [冷热分离](数据库/Elasticsearch.md#冷热分离)
    * [document设计](数据库/Elasticsearch.md#document设计)
    * [禁止直接分页](数据库/Elasticsearch.md#禁止直接分页)
* [es的分词器有哪些](数据库/Elasticsearch.md#es的分词器有哪些)
* [es为什么这么快](数据库/Elasticsearch.md#es为什么这么快)
* [es 的分页方案](数据库/Elasticsearch.md#es的分页方案)
* [es 的查询流程](数据库/Elasticsearch.md#es的查询流程)

### Nebula Graph[↑↑](#内容概览)

* [什么是Nebula Graph](数据库/Nebula.md#什么是nebula-graph)
    * [什么是图数据库](数据库/Nebula.md#什么是图数据库)
    * [Nebula Graph 的优势](数据库/Nebula.md#nebula-graph-的优势)
* [数据模型](数据库/Nebula.md#数据模型)
    * [数据模型](数据库/Nebula.md#数据模型-1)
        * [图空间（Space）](数据库/Nebula.md#图空间space)
        * [点（Vertex）](数据库/Nebula.md#点vertex)
        * [边（Edge）](数据库/Nebula.md#边edge)
        * [标签（Tag）](数据库/Nebula.md#标签tag)
        * [边类型（Edge type）](数据库/Nebula.md#边类型edge-type)
        * [属性（Properties）](数据库/Nebula.md#属性properties)
    * [有向属性图](数据库/Nebula.md#有向属性图)
* [路径](数据库/Nebula.md#路径)
    * [walk](数据库/Nebula.md#walk)
    * [trail](数据库/Nebula.md#trail)
    * [path](数据库/Nebula.md#path)
* [点 VID](数据库/Nebula.md#点-vid)
* [服务架构](数据库/Nebula.md#服务架构)
    * [架构总览](数据库/Nebula.md#架构总览)
    * [Meta 服务](数据库/Nebula.md#meta-服务-1)
    * [Graph服务](数据库/Nebula.md#graph服务)
    * [Storage服务](数据库/Nebula.md#storage服务)

## <a>消息队列</a>[↑↑](#内容概览)

### Redis[↑↑](#内容概览)

- [Redis](消息队列/Redis.md)

### RabbitMQ[↑↑](#内容概览)

- [RabbitMQ](消息队列/RabbitMQ.md)
    * [概念介绍](消息队列/RabbitMQ.md#概念介绍)
    * [架构图](消息队列/RabbitMQ.md#架构图)
    * [exchange类型](消息队列/RabbitMQ.md#exchange类型)
        * [Direct](消息队列/RabbitMQ.md#direct)
        * [Fanout](消息队列/RabbitMQ.md#fanout)
        * [Topic](消息队列/RabbitMQ.md#topic)
    * [RabbitMQ 消息持久化](消息队列/RabbitMQ.md#rabbitmq-消息持久化)
    * [集群](消息队列/RabbitMQ.md#集群)
    * [交换器无法根据自身类型和路由键找到符合条件队列时，会如何处理？](消息队列/RabbitMQ.md#交换器无法根据自身类型和路由键找到符合条件队列时会如何处理)
    * [RabbitMQ 的六种模式](消息队列/RabbitMQ.md#rabbitmq-的六种模式)
    * [死信队列应用场景](消息队列/RabbitMQ.md#死信队列应用场景)
    * [事务机制](消息队列/RabbitMQ.md#事务机制)
    * [Confirm模式](消息队列/RabbitMQ.md#confirm模式)
        * [producer端confirm模式的实现原理](消息队列/RabbitMQ.md#producer端confirm模式的实现原理)
        * [开启confirm模式的方法](消息队列/RabbitMQ.md#开启confirm模式的方法)
        * [编程模式](消息队列/RabbitMQ.md#编程模式)

### RocketMQ[↑↑](#内容概览)

- [RocketMQ](消息队列/RocketMQ.md#rocketmq)
    * [架构图](消息队列/RocketMQ.md#架构图)
    * [组件](消息队列/RocketMQ.md#组件)
        * [NameServer](消息队列/RocketMQ.md#nameserver)
        * [Broker](消息队列/RocketMQ.md#broker)
        * [Producer](消息队列/RocketMQ.md#producer)
        * [Consumer](消息队列/RocketMQ.md#consumer)
    * [消息特性](消息队列/RocketMQ.md#消息特性)
    * [消息功能](消息队列/RocketMQ.md#消息功能)
    * [rocket的事务实现机制](消息队列/RocketMQ.md#rocket的事务实现机制)
    * [Broker 集群部署架构](消息队列/RocketMQ.md#broker-集群部署架构)
        * [多 Master 模式](消息队列/RocketMQ.md#多-master-模式)
        * [多 Master 多 Salve - 异步复制 模式](消息队列/RocketMQ.md#多-master-多-salve---异步复制-模式)
        * [多 Master 多 Salve - 同步双写 模式](消息队列/RocketMQ.md#多-master-多-salve---同步双写-模式)
        * [Dledger 模式](消息队列/RocketMQ.md#dledger-模式)

### Kafka[↑↑](#内容概览)

- [Kafka](消息队列/Kafka.md)
    * [架构图](消息队列/Kafka.md#架构图)
    * [概念](消息队列/Kafka.md#概念)
        * [topic](消息队列/Kafka.md#topic)
        * [partition](消息队列/Kafka.md#partition)
        * [segment](消息队列/Kafka.md#segment)
        * [offset](消息队列/Kafka.md#offset)
        * [broker](消息队列/Kafka.md#broker)
        * [producer](消息队列/Kafka.md#producer)
        * [consumer](消息队列/Kafka.md#consumer)
    * [Kafka零拷贝](消息队列/Kafka.md#kafka零拷贝)
    * [常见问题](消息队列/Kafka.md#常见问题)
        * [kafka中zookeeper的作用](消息队列/Kafka.md#kafka中zookeeper的作用)
        * [kafka的consumer是拉模式还是推模式](消息队列/Kafka.md#kafka的consumer是拉模式还是推模式)
        * [kafka生产者丢消息情况](消息队列/Kafka.md#kafka生产者丢消息情况)
        * [kafka消费者丢消息情况](消息队列/Kafka.md#kafka消费者丢消息情况)
        * [Kafka如何保证高可用性](消息队列/Kafka.md#kafka如何保证高可用性)
        * [Kafka的消息保存在哪里？Kafka的消息是如何分区的？](消息队列/Kafka.md#kafka的消息保存在哪里kafka的消息是如何分区的)
        * [Kafka是如何处理流量峰值的？](消息队列/Kafka.md#kafka是如何处理流量峰值的)
        * [Kafka消息压缩方式](消息队列/Kafka.md#kafka消息压缩方式)
        * [Kafka的重平衡机制是什么？](消息队列/Kafka.md#kafka的重平衡机制是什么)
        * [Kafka中的生产者和消费者是什么？Kafka是如何确保数据的顺序性和一致性的？](消息队列/Kafka.md#kafka中的生产者和消费者是什么kafka是如何确保数据的顺序性和一致性的)
        * [kafka消费组怎么消费一个topic的数据](消息队列/Kafka.md#kafka消费组怎么消费一个topic的数据)
        * [Kafka有哪些优缺点？](消息队列/Kafka.md#kafka有哪些优缺点)
        * [Kafka的API是什么？如何使用Kafka API实现生产和消费？](消息队列/Kafka.md#kafka的api是什么如何使用kafka-api实现生产和消费)
        * [如何部署和扩展Kafka集群？](消息队列/Kafka.md#如何部署和扩展kafka集群)

### Zookeeper[↑↑](#内容概览)

- [Zookeeper](消息队列/Zookeeper.md)
    * [概念](消息队列/Zookeeper.md#概念)
    * [用zookeeper可以干嘛](消息队列/Zookeeper.md#用zookeeper可以干嘛)
    * [数据结构](消息队列/Zookeeper.md#数据结构)
        * [ZNode](消息队列/Zookeeper.md#znode)
    * [监听机制](消息队列/Zookeeper.md#监听机制)
    * [角色](消息队列/Zookeeper.md#角色)
        * [leader](消息队列/Zookeeper.md#leader)
        * [follower](消息队列/Zookeeper.md#follower)
        * [Observer](消息队列/Zookeeper.md#observer)
    * [Zookeeper Leader 选举原理](消息队列/Zookeeper.md#zookeeper-leader-选举原理)
    * [常见的问题](消息队列/Zookeeper.md#常见的问题)
        * [什么是Zookeeper？它的作用是什么？](消息队列/Zookeeper.md#什么是zookeeper它的作用是什么)
        * [Zookeeper是如何实现数据的一致性和可靠性的？](消息队列/Zookeeper.md#zookeeper是如何实现数据的一致性和可靠性的)
        * [Zookeeper中的watcher是什么？如何使用watcher机制实现分布式锁？](消息队列/Zookeeper.md#zookeeper中的watcher是什么如何使用watcher机制实现分布式锁)
        * [Zookeeper的性能瓶颈在哪里？如何优化Zookeeper的性能？](消息队列/Zookeeper.md#zookeeper的性能瓶颈在哪里如何优化zookeeper的性能)
        * [如何在Zookeeper集群中进行数据的备份和恢复？](消息队列/Zookeeper.md#如何在zookeeper集群中进行数据的备份和恢复)

### Pulsar[↑↑](#内容概览)

- [Pulsar](消息队列/Pulsar.md)
    * [pulsar的优势](消息队列/Pulsar.md#pulsar的优势)

* [Apache Pulsar 架构](消息队列/Pulsar.md#apache-pulsar-架构)
    * [Topic 与分区](消息队列/Pulsar.md#topic-与分区)
    * [物理分区与逻辑分区](消息队列/Pulsar.md#物理分区与逻辑分区)
* [消息存储原理与 ID 规则](消息队列/Pulsar.md#消息存储原理与-id-规则)
    * [消息 ID 生成规则](消息队列/Pulsar.md#消息-id-生成规则)
    * [分片机制详解：Legder 和 Entry](消息队列/Pulsar.md#分片机制详解legder-和-entry)
* [消息副本与存储机制](消息队列/Pulsar.md#消息副本与存储机制)
    * [消息元数据组成](消息队列/Pulsar.md#消息元数据组成)
    * [消息副本机制](消息队列/Pulsar.md#消息副本机制)
* [消息恢复机制](消息队列/Pulsar.md#消息恢复机制)
* [pulsar的消息模式](消息队列/Pulsar.md#pulsar的消息模式)
    * [独占模式（Exclusive）](消息队列/Pulsar.md#独占模式exclusive)
    * [灾备模式（Failover）](消息队列/Pulsar.md#灾备模式failover)
    * [共享模式（Shared）](消息队列/Pulsar.md#共享模式shared)
* [定时和延时消息](消息队列/Pulsar.md#定时和延时消息)
    * [相关概念](消息队列/Pulsar.md#相关概念)
    * [适用场景](消息队列/Pulsar.md#适用场景)
    * [使用方式](消息队列/Pulsar.md#使用方式)
    * [定时消息](消息队列/Pulsar.md#定时消息)
    * [延时消息](消息队列/Pulsar.md#延时消息)
    * [使用说明和限制](消息队列/Pulsar.md#使用说明和限制)
* [消息重试与死信机制](消息队列/Pulsar.md#消息重试与死信机制)
    * [自动重试](消息队列/Pulsar.md#自动重试)
    * [自定义参数设置](消息队列/Pulsar.md#自定义参数设置)
    * [重试规则](消息队列/Pulsar.md#重试规则)
    * [重试消息的消息属性](消息队列/Pulsar.md#重试消息的消息属性)
    * [重试消息的消息 ID 流转](消息队列/Pulsar.md#重试消息的消息-id-流转)
    * [主动重试](消息队列/Pulsar.md#主动重试)

- [常见面试题](消息队列/mq常见面试题.md)
    * [什么是消息队列](消息队列/mq常见面试题.md#什么是消息队列)
    * [为什么要使用消息队列](消息队列/mq常见面试题.md#为什么要使用消息队列)
    * [如何保证消息队列高可用](消息队列/mq常见面试题.md#如何保证消息队列高可用)
    * [如何保证消息队列不被重复消费（幂等性）](消息队列/mq常见面试题.md#如何保证消息队列不被重复消费幂等性)
    * [如何保证消息的可靠传输](消息队列/mq常见面试题.md#如何保证消息的可靠传输)
        * [生产者丢数据](消息队列/mq常见面试题.md#生产者丢数据)
        * [MQ丢数据](消息队列/mq常见面试题.md#mq丢数据)
        * [消费者丢数据](消息队列/mq常见面试题.md#消费者丢数据)
    * [如何保证消息的顺序性](消息队列/mq常见面试题.md#如何保证消息的顺序性)
    * [如何处理消息堆积](消息队列/mq常见面试题.md#如何处理消息堆积)
    * [mq 中的消息过期失效了](消息队列/mq常见面试题.md#mq-中的消息过期失效了)

## <a>Redis</a>[↑↑](#内容概览)

* [特点](Redis/Redis.md#特点)
* [Redis为什么这么快](Redis/Redis.md#redis为什么这么快)
* [常见使用场景](Redis/Redis.md#常见使用场景)
* [数据类型](Redis/Redis.md#数据类型)
    * [redisObject](Redis/Redis.md#redisobject)
    * [string](Redis/Redis.md#string)
    * [list](Redis/Redis.md#list)
    * [hash](Redis/Redis.md#hash)
    * [set](Redis/Redis.md#set)
    * [zset（sorted set）](Redis/Redis.md#zsetsorted-set)
    * [bitmap](Redis/Redis.md#bitmap)
    * [HyperLogLog](Redis/Redis.md#hyperloglog)
* [内存回收策略](Redis/Redis.md#内存回收策略)
* [持久化方式](Redis/Redis.md#持久化方式)
    * [RDB快照](Redis/Redis.md#rdb快照)
    * [AOF追加](Redis/Redis.md#aof追加)
* [Redis 中的事务](Redis/Redis.md#redis-中的事务)
* [常问故障场景](Redis/Redis.md#常问故障场景)
    * [缓存雪崩](Redis/Redis.md#缓存雪崩)
    * [缓存穿透](Redis/Redis.md#缓存穿透)
* [集群](Redis/Redis.md#集群)
    * [主从复制模式](Redis/Redis.md#主从复制模式)
    * [Sentinel（哨兵）模式](Redis/Redis.md#sentinel哨兵模式)
    * [Cluster 集群模式](Redis/Redis.md#cluster-集群模式)
* [Redis Cluster 节点通信原理：Gossip 算法](Redis/Redis.md#redis-cluster-节点通信原理gossip-算法)
    * [Gossip 简介](Redis/Redis.md#gossip-简介)
    * [节点状态和消息类型](Redis/Redis.md#节点状态和消息类型)
* [Redis cluster伸缩的原理](Redis/Redis.md#redis-cluster伸缩的原理)
* [redis索引](Redis/Redis.md#redis索引)

### <a>Redis常见面试题</a>[↑↑](#内容概览)

* [储存结构和使用场景](Redis/Redis常见面试题.md#储存结构和使用场景)
* [淘汰策略](Redis/Redis常见面试题.md#淘汰策略)

## <a>Spring</a>[↑↑](#内容概览)

- [Spring](Spring/Spring.md)
    * [架构图](Spring/Spring.md#架构图)
    * [模块](Spring/Spring.md#模块)
    * [IOC](Spring/Spring.md#ioc)
        * [IOC和DI的概念](Spring/Spring.md#ioc和di的概念)
        * [使用IOC的好处](Spring/Spring.md#使用ioc的好处)
        * [Spring IoC的初始化过程](Spring/Spring.md#spring-ioc的初始化过程)
        * [Spring bean的生命周期](Spring/Spring.md#spring-bean的生命周期)
        * [bean的作用域](Spring/Spring.md#bean的作用域)
        * [循环依赖问题](Spring/Spring.md#循环依赖问题)
    * [AOP](Spring/Spring.md#aop)
        * [AOP原理](Spring/Spring.md#aop原理)
        * [AOP术语](Spring/Spring.md#aop术语)
        * [Spring对AOP的支持](Spring/Spring.md#spring对aop的支持)
    * [怎么定义一个注解](Spring/Spring.md#怎么定义一个注解)
        * [引入依赖](Spring/Spring.md#引入依赖)
        * [定义注解](Spring/Spring.md#定义注解)
    * [事务](Spring/Spring.md#事务)
        * [Spring 支持两种方式的事务管理](Spring/Spring.md#spring-支持两种方式的事务管理)
        * [事务的传播性 Propagation](Spring/Spring.md#事务的传播性-propagation)
    * [spring使用的设计模式](Spring/Spring.md#spring使用的设计模式)
        * [简单工厂](Spring/Spring.md#简单工厂)
        * [工厂方法](Spring/Spring.md#工厂方法)
        * [单例模式](Spring/Spring.md#单例模式)
        * [适配器模式](Spring/Spring.md#适配器模式)
        * [装饰器模式](Spring/Spring.md#装饰器模式)
        * [代理模式](Spring/Spring.md#代理模式)
    * [spring中properties和yml的加载顺序](Spring/Spring.md#spring中properties和yml的加载顺序)
    * [使用@Autowired注解自动装配的过程是怎样的？](Spring/Spring.md#使用autowired注解自动装配的过程是怎样的)
    * [@Autowired和@Resource之间的区别](Spring/Spring.md#autowired和resource之间的区别)
    * [Spring中BeanFactory与FactoryBean的区别](Spring/Spring.md#spring中beanfactory与factorybean的区别)

### SpringMVC[↑↑](#内容概览)

- [SpringMVC](Spring/SpringMVC.md)
    * [流程](Spring/SpringMVC.md#流程)
    * [执行流程](Spring/SpringMVC.md#执行流程)

### SpringBoot[↑↑](#内容概览)

- [SpringBoot](Spring/SpringBoot.md)
    * [springboot启动流程](Spring/SpringBoot.md#springboot启动流程)
    * [怎么让Spring把Body变成一个对象](Spring/SpringBoot.md#怎么让spring把body变成一个对象)
    * [SpringBoot的starter实现原理是什么？](Spring/SpringBoot.md#springboot的starter实现原理是什么)

## <a>Springcloud</a>[↑↑](#内容概览)

* [服务注册与发现](SpringCloud/springcloud.md#服务注册与发现)
    * [eureka](SpringCloud/springcloud.md#eureka)
    * [consul](SpringCloud/springcloud.md#consul)
    * [ribbon](SpringCloud/springcloud.md#ribbon)
    * [loadbalancer](SpringCloud/springcloud.md#loadbalancer)
    * [feign](SpringCloud/springcloud.md#feign)
    * [openFeign](SpringCloud/springcloud.md#openfeign)
    * [hystrix](SpringCloud/springcloud.md#hystrix)
    * [resilience4j](SpringCloud/springcloud.md#resilience4j)
    * [zuul](SpringCloud/springcloud.md#zuul)
    * [zuul2](SpringCloud/springcloud.md#zuul2)
    * [getway](SpringCloud/springcloud.md#getway)
    * [springcloud config](SpringCloud/springcloud.md#springcloud-config)
    * [Nacos](SpringCloud/springcloud.md#nacos)

## <a>SpringcloudAlibaba</a>[↑↑](#内容概览)

* [SpringcloudAlibaba](SpringCloud/springcloud.md#springcloudalibaba)
    * [Nacos](SpringCloud/springcloud.md#nacos-1)
    * [Sentienl](SpringCloud/springcloud.md#sentienl)

## <a>Linux</a>[↑↑](#内容概览)

* [文件和目录的操作](Linux/linux.md#文件和目录的操作)
* [查看文件](Linux/linux.md#查看文件)
* [管理用户](Linux/linux.md#管理用户)
* [进程管理](Linux/linux.md#进程管理)
* [打包和压缩文件](Linux/linux.md#打包和压缩文件)
* [grep+正则表达式](Linux/linux.md#grep)
* [Vi编辑器](Linux/linux.md#Vi编辑器)
* [权限管理](Linux/linux.md#权限管理)
* [网络管理](Linux/linux.md#网络管理)
* [cpu100%怎么排查](Linux/linux.md#cpu100怎么排查)
* [用户空间与内核空间](Linux/linux.md#用户空间与内核空间)
* #### <a href="Linux/linux.md#linux-的进程线程文件描述符是什么">Linux的进程、线程、文件描述符是什么</a>
* [进程切换](Linux/linux.md#进程切换)
* [进程的阻塞](Linux/linux.md#进程的阻塞)
* [文件描述符fd](Linux/linux.md#文件描述符fd)
* [缓存 I/O](Linux/linux.md#缓存-io)
* #### <a href="Linux/linux.md#io模型">IO模型</a>
* #### <a href="Linux/linux.md#selectpollepoll">select、poll、epoll</a>
* [进程间8种通信方式详解](Linux/linux.md#进程间8种通信方式详解)
* [Linux物理内存和虚拟内存](Linux/linux.md#linux物理内存和虚拟内存)
* [页面置换算法](Linux/linux.md#页面置换算法)
* [进程调度算法](Linux/linux.md#进程调度算法)

## <a>Mybatis</a>[↑↑](#内容概览)

- [什么是mybatis](Mybatis/mybatis.md)
- [JDBC执行六步骤](Mybatis/mybatis.md)
- [mybatis执行8步骤](Mybatis/mybatis.md)
- [MyBatis整体架构](Mybatis/mybatis.md)
- [mybatis缓存](Mybatis/mybatis.md)

## <a>Netty</a>[↑↑](#内容概览)

* [重要的组件](Netty/netty.md#重要的组件)
    * [Channel](Netty/netty.md#channel)
    * [ChannelFuture](Netty/netty.md#channelfuture)
    * [EventLoop](Netty/netty.md#eventloop)
    * [ChannelHandler](Netty/netty.md#channelhandler)
    * [ChannelPipeline](Netty/netty.md#channelpipeline)
    * [TaskQueue](Netty/netty.md#taskqueue)
* [netty的使用示例](Netty/netty.md#netty的使用示例)
    * [服务端](Netty/netty.md#服务端)
    * [客户端](Netty/netty.md#客户端)
* [TCP粘包/拆包问题](Netty/netty.md#tcp粘包拆包问题)
    * [什么是粘包拆包](Netty/netty.md#什么是粘包拆包)
    * [发生的原因](Netty/netty.md#发生的原因)
    * [粘包解决策略](Netty/netty.md#粘包解决策略)
    * [netty粘包问题解决方案](Netty/netty.md#netty粘包问题解决方案)
* [解编码技术](Netty/netty.md#解编码技术)
    * [Java序列化的缺点](Netty/netty.md#java序列化的缺点)
    * [Google的protobuf](Netty/netty.md#google的protobuf)
    * [Facebook的Thrift](Netty/netty.md#facebook的thrift)
    * [JBoss的Marshalling](Netty/netty.md#jboss的marshalling)
    * [MessagePack](Netty/netty.md#messagepack)
* [高性能的原因](Netty/netty.md#高性能的原因)
    * [非阻塞io](Netty/netty.md#非阻塞io)
    * [零拷贝](Netty/netty.md#零拷贝)
    * [内存池](Netty/netty.md#内存池)
    * [高效的Reactor线程模型](Netty/netty.md#高效的reactor线程模型)
        * [Reactor 单线程模型](Netty/netty.md#reactor-单线程模型)
        * [Reactor 多线程模型](Netty/netty.md#reactor-多线程模型)
        * [（采用）主从 Reactor 多线程模型](Netty/netty.md#采用主从-reactor-多线程模型)
    * [无锁化串行设计](Netty/netty.md#无锁化串行设计)
    * [高性能的序列化框架](Netty/netty.md#高性能的序列化框架)
    * [灵活的TCP 参数配置能力](Netty/netty.md#灵活的tcp-参数配置能力)
* [netty相关问题](Netty/netty.md#netty相关问题)

## <a>分布式相关</a>[↑↑](#内容概览)

- #### <a href="分布式相关/分布式锁.md">分布式锁</a>
    * [基于数据库](分布式相关/分布式锁.md#基于数据库)
    * [Redis](分布式相关/分布式锁.md#redis)
    * [zookeeper](分布式相关/分布式锁.md#zookeeper)
- #### <a href="分布式相关/分布式事务.md">分布式事务</a>
- [分布式事务](分布式相关/分布式事务.md)
    * [两阶段提交](分布式相关/分布式事务.md#两阶段提交)
    * [TCC（Try-Confirm-Cancel）](分布式相关/分布式事务.md#tcctry-confirm-cancel)
    * [本地消息表](分布式相关/分布式事务.md#本地消息表)
    * [可靠消息最终一致性](分布式相关/分布式事务.md#可靠消息最终一致性)
    * [尽最大努力通知](分布式相关/分布式事务.md#尽最大努力通知)
- #### <a href="分布式相关/分布式ID.md#分布式唯一id设计">分布式唯一ID设计</a>
    * [UUID](分布式相关/分布式ID.md##uuid)
    * [多台MySQL服务器](分布式相关/分布式ID.md##多台mysql服务器)
    * [Twitter Snowflake](分布式相关/分布式ID.md##twitter-snowflake)
    * [百度UidGenerator算法](分布式相关/分布式ID.md##百度uidgenerator算法)
    * [美团Leaf算法](分布式相关/分布式ID.md##美团leaf算法)
- #### <a href="分布式相关/CAP.md">CAP理论</a>  
    * [一致性 Consistency](分布式相关/CAP.md#一致性-consistency)
    * [可用性 Availability](分布式相关/CAP.md#可用性-availability)
    * [分区容错性 Partition Tolerance](分布式相关/CAP.md#分区容错性-partition-tolerance)
    * [常见的注册中心](#常见的注册中心)
- [BASE](分布式相关/BASE.md)
    * [基本可以  Basically Available](分布式相关/BASE.md#基本可以--basically-available)
    * [软状态  Soft-state](分布式相关/BASE.md#软状态--soft-state)
    * [最终一致性  Eventually Consistent](分布式相关/BASE.md#最终一致性--eventually-consistent)
- #### <a href="分布式相关/一致性算法.md">一致性算法</a>
    * [Paxos](分布式相关/一致性算法.md#paxos)
    * [Raft](分布式相关/一致性算法.md#raft)

## <a>容器技术</a>[↑↑](#内容概览)

- #### <a href="容器技术/docker.md">Docker</a>
    * [Docker简介](容器技术/docker.md#docker简介)
    * [Docker常用命令](容器技术/docker.md#docker常用命令)
    * [Docker应用架构](容器技术/docker.md#docker应用架构)
    * [底层实现原理](容器技术/docker.md#底层实现原理)
- #### <a href="容器技术/k8s.md">Kubernetes</a>

## <a>数据结构和算法</a>[↑↑](#内容概览)

- #### <a href="数据结构和算法/排序算法.md">排序算法</a>
- #### <a href="">树相关</a>
- #### <a href="">BFS</a>
- #### <a href="">DFS</a>
- #### <a href="">回溯算法</a>
- #### <a href="">二分法</a>
- #### <a href="">贪心算法</a>
- #### <a href="">动态规划</a>
- #### <a href="">分治思想</a>
- [LRU](数据结构和算法/LRU.md)
- [LFU](数据结构和算法/LFU.md)
- [加减乘除](数据结构和算法/加减乘除.md)

## <a>设计模式</a>[↑↑](#内容概览)

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

## <a>职业规划和学习习惯</a>[↑↑](#内容概览)

- [项目中遇到的问题](职业规划和学习习惯/职业规划和学习习惯.md#项目中遇到的问题)
- [职业规划](职业规划和学习习惯/职业规划和学习习惯.md#职业规划)
- [平时规则](职业规划和学习习惯/职业规划和学习习惯.md#平时规则)

## <a>场景设计</a>[↑↑](#内容概览)

- [有A、B两个大文件，每个文件几十G,而内存只有4G,其中A文件存放学号+姓名，而B文件存放学号+分数，要求生成文件C，存放姓名和分数。怎么实现?](场景设计/场景设计.md)
- [秒杀系统怎么设计](场景设计/场景设计.md#秒杀系统怎么设计)
- [唯一ID设计](场景设计/场景设计.md#唯一ID设计)
- [产品上线出问题怎么定位错误](场景设计/场景设计.md#产品上线出问题怎么定位错误)
- [大量并发查询用户商品信息，MySQL压力大查询慢，保证速度怎么优化方案](场景设计/场景设计.md#大量并发查询用户商品信息，MySQL压力大查询慢，保证速度怎么优化方案)
- [海量日志数据，提取出某日访问百度次数最多的那个IP。给定a、b两个文件，各存放50亿个url,每个url各 占64字节，内存限制是4G,让你找出a、b文件共同的url?](场景设计/场景设计.md)
- [一般内存不足而需要分析的数据又很大的问题都可以使用分治的思想，将数据hash(x)%1000分为小文件再分别加载小文件到内存中处理即可](场景设计/场景设计.md#一般内存不足而需要分析的数据又很大的问题都可以使用分治的思想将数据hashx1000分为小文件再分别加载小文件到内存中处理即可)
- [如何保证接口的幂等性](场景设计/场景设计.md#如何保证接口的幂等性)
- [缓存和数据库不一致问题](场景设计/场景设计.md#缓存和数据库不一致问题)
- [什么是SPI](场景设计/场景设计.md#什么是SPI)
- [什么是RPC？](场景设计/场景设计.md#什么是rpc)
- [gRPC](场景设计/场景设计.md#gRPC)
- [一个优秀的RPC框架需要考虑的问题](场景设计/场景设计.md#一个优秀的RPC框架需要考虑的问题)
- [什么是DDD](场景设计/场景设计.md#什么是ddd)
- [Java实现生产者消费者](场景设计/场景设计.md#java实现生产者消费者)
- [Java实现BlockQueue](场景设计/场景设计.md#java实现blockqueue)
- [解决哈希冲突的方法](场景设计/场景设计.md#解决哈希冲突的方法)
- [排行榜设计](场景设计/场景设计.md#排行榜设计)

## <a>智力题</a>[↑↑](#内容概览)

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

## <a>架构</a>[↑↑](#内容概览)

- #### <a href="架构/系统设计.md">系统设计</a>
- #### <a href="架构/计算和储存分离.md">计算和储存分离</a>
- #### <a href="架构/DDD领域驱动设计.md">DDD领域驱动设计</a>

## <a>面试解答</a>[↑↑](#内容概览)

- [HR会问什么](面试解答/HR会问什么.md)
- [面试解答6月牛客](面试解答/面试解答2021-06.md)
- [面试解答7月牛客](面试解答/面试解答2021-07.md)
- [面试解答9月牛客](面试解答/面试解答2021-09.md)
- [面试解答10月牛客](面试解答/面试解答2021-10.md)

## <a>商城类问题</a>[↑↑](#内容概览)

- [秒杀](商城类问题/商城类问题.md#秒杀)
- [超卖](商城类问题/商城类问题.md#如何解决超卖问题)
- [订单延迟](商城类问题/商城类问题.md#订单延时取消怎么做)

# 免责声明[↑↑](#内容概览)

> **:bangbang:某些知识点、观点、图片是从各种优秀博主、作者、大佬们的文章里或文献里提取的，我只是搬运工，如果觉得有侵犯到您的权益，请联系我，我将根据您的要求修改（添加您的出处链接、删除、修改....），谢谢大佬！
**

# 最后[↑↑](#内容概览)

> 不积跬步无以至千里

## 微信交流

> 可以关注我的微信公众号，一些学习资料关注后可以分享给你


<img src="img%2F微信公共号二维码.png" align="center" width="50%" />