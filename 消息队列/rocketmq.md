
* [RocketMQ](#rocketmq)
    * [架构图](#架构图)
    * [组件](#组件)
    * [rocket的事务实现机制](#rocket的事务实现机制)


# RocketMQ
## 架构图
![](../img/消息队列/rocketmq/架构图.png)
## 组件
- `NameServer` 主要用作注册中心，用于管理 Topic 信息和路由信息的管理
- `Broker` 负责存储、消息 tag 过滤和转发。需将自身信息上报给注册中心 NameServer
- `Producer` 生产者
- `Consumer` 消费者
## rocket的事务实现机制