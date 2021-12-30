* [分布式唯一ID设计](#分布式唯一id设计)
  * [UUID](#uuid)
  * [多台MySQL服务器](#多台mysql服务器)
  * [Twitter Snowflake](#twitter-snowflake)
  * [百度UidGenerator算法](#百度uidgenerator算法)
  * [美团Leaf算法](#美团leaf算法)
    * [Leaf-segment数据库方案 号段模式](#leaf-segment数据库方案-号段模式)
    * [Leaf-snowflake方案](#leaf-snowflake方案)


## 分布式唯一ID设计
### UUID
缺点很明显，太长且无序
### 多台MySQL服务器
- 既然MySQL可以产生自增ID，那么用多台MySQL服务器，能否组成一个高性能的分布式发号器呢？ 显然可以。
- 假设用8台MySQL服务器协同工作，第一台MySQL初始值是1，每次自增8，第二台MySQL初始值是2，每次自增8，依次类推。前面用一个 round-robin load balancer 挡着，每来一个请求，由 round-robin balancer 随机地将请求发给8台MySQL中的任意一个，然后返回一个ID
- 这个方法跟单台数据库比，缺点是ID是不是严格递增的，只是粗略递增的。不过这个问题不大，我们的目标是粗略有序，不需要严格递增。
### Twitter Snowflake
核心思想是：采用bigint（64bit）作为id生成类型，并将所占的64bit 划分成多段。
- ①1位标识：由于long基本类型在Java中是带符号的，最高位是符号位，正数是0，负数是1，所以id一般是正数，最高位是0。
- ②41位时间截(毫秒级）：需要注意的是，41位时间截不是存储当前时间的时间截，而是存储时间截的差值（当前时间截 - 开始时间截）得到的值，这里的开始时间截，一般是指我们的id生成器开始使用的时间截，由我们的程序来指定。41位的毫秒时间截，可以使用69年（即T =（1L << 41）/（1000 60 60 24 365）= 69）。
- ③10位的数据机器位：包括5位数据中心标识Id（datacenterId）、5位机器标识Id(workerId)，最多可以部署1024个节点（即1 << 10 = 1024）。超过这个数量，生成的ID就有可能会冲突。
- ④12位序列：毫秒内的计数，12位的计数顺序号支持每个节点每毫秒（同一机器，同一时间截）产生4096个ID序号（即1 << 12 = 4096）。
  PS：全部结构标识（1+41+10+12=64）加起来刚好64位，刚好凑成一个Long型。
### 百度UidGenerator算法
uid-generator使用的就是snowflake，只是在生产机器id，也叫做workId时有所不同。

uid-generator中的workId是由uid-generator自动生成的，并且考虑到了应用部署在docker上的情况，在uid-generator中用户可以自己去定义workId的生成策略，默认提供的策略是：应用启动时由数据库分配。说的简单一点就是：应用在启动时会往数据库表(uid-generator需要新增一个WORKER_NODE表)中去插入一条数据，数据插入成功后返回的该数据对应的自增唯一id就是该机器的workId，而数据由host，port组成。

对于uid-generator中的workId，占用了22个bit位，时间占用了28个bit位，序列化占用了13个bit位，需要注意的是，和原始的snowflake不太一样，时间的单位是秒，而不是毫秒，workId也不一样，同一个应用每重启一次就会消费一个workId。
### 美团Leaf算法
#### Leaf-segment数据库方案 号段模式
- 分段获取
- 即当号段消费到某个点时就异步的把下一个号段加载到内存中
#### Leaf-snowflake方案
Leaf中的snowflake模式和原始snowflake算法的不同点，也主要在workId的生成，Leaf中workId是基于ZooKeeper的顺序Id来生成的，每个应用在使用Leaf-snowflake时，在启动时都会都在Zookeeper中生成一个顺序Id，相当于一台机器对应一个顺序节点，也就是一个workId。
