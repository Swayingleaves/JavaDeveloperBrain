
* [Redis](#redis)
  * [Redis实现mq主要是依赖数据结构list](#redis实现mq主要是依赖数据结构list)
  * [不足](#不足)


# Redis
## Redis实现mq主要是依赖数据结构list
lpush：从队列左边插入数据； rpop：从队列右边取出数据
## 不足
- `消息持久化` redis是内存数据库，虽然有aof和rdb两种机制进行持久化，但这只是辅助手段，这两种手段都是不可靠的。当redis服务器宕机时一定会丢失一部分数据，这对于很多业务都是没法接受的
- `热key性能问题` 不论是用codis还是twemproxy这种集群方案，对某个队列的读写请求最终都会落到同一台redis实例上，并且无法通过扩容来解决问题。如果对某个list的并发读写非常高，就产生了无法解决的热key，严重可能导致系统崩溃
- `没有确认机制`
  每当执行rpop消费一条数据，那条消息就被从list中永久删除了。如果消费者消费失败，这条消息也没法找回了。你可能说消费者可以在失败时把这条消息重新投递到进队列，但这太理想了，极端一点万一消费者进程直接崩了呢，比如被kill -9，panic，coredump…
- `不支持多订阅者`
  一条消息只能被一个消费者消费，rpop之后就没了。如果队列中存储的是应用的日志，对于同一条消息，监控系统需要消费它来进行可能的报警，BI系统需要消费它来绘制报表，链路追踪需要消费它来绘制调用关系……这种场景redis list就没办法支持了
- `不支持二次消费`
  一条消息rpop之后就没了。如果消费者程序运行到一半发现代码有bug，修复之后想从头再消费一次就不行了