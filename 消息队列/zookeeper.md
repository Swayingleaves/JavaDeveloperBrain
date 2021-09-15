
* [Zookeeper](#zookeeper)
    * [概念](#概念)
    * [数据结构](#数据结构)
    * [角色](#角色)
        * [leader](#leader)
        * [follower](#follower)
        * [Observer](#observer)
    * [zab协议](#zab协议)
        * [Zxid](#zxid)
        * [模式](#模式)
        * [4阶段](#4阶段)
            * [选举阶段](#选举阶段)
            * [发现阶段](#发现阶段)
            * [同步阶段](#同步阶段)
            * [广播阶段](#广播阶段)


# Zookeeper
## 概念
- Zookeeper 是一个分布式协调服务，可用于服务发现，分布式锁，分布式领导选举，配置管理等。
- Zookeeper 提供了一个类似于 Linux 文件系统的树形结构（可认为是轻量级的内存文件系统，但 只适合存少量信息，完全不适合存储大量文件或者大文件），同时提供了对于每个节点的监控与通知机制。
## 数据结构
zookkeeper 提供的名称空间非常类似于标准文件系统，key-value 的形式存储。名称 key 由斜线 / 分割的一系列路径元素，zookeeper 名称空间中的每个节点都是由一个路径标识
## 角色
### leader

- 一个 Zookeeper 集群同一时间只会有一个实际工作的 Leader，它会发起并维护与各 Follwer及 Observer 间的心跳。
- 所有的写操作必须要通过 Leader 完成再由 Leader 将写操作广播给其它服务器。只要有超过半数节点（不包括 observeer 节点）写入成功，该写请求就会被提交（类 2PC 协议）。

### follower
- 一个 Zookeeper 集群可能同时存在多个 Follower，它会响应 Leader 的心跳，
- Follower 可直接处理并返回客户端的读请求，同时会将写请求转发给 Leader 处理，
- 并且负责在 Leader 处理写请求时对请求进行投票。

### Observer
- 角色与 Follower 类似，但是无投票权。Zookeeper 需保证高可用和强一致性，为了支持更多的客 户端，需要增加更多 Server；Server 增多，投票阶段延迟增大，影响性能；引入 Observer，
- Observer 不参与投票； Observers 接受客户端的连接，并将写请求转发给 leader 节点； 加入更多 Observer 节点，提高伸缩性，同时不影响吞吐率。
## zab协议
### Zxid

Zxid 是一个 64 位的数字其中低 32 位是一个简单的单调递增的计数器，针对客户端每 一个事务请求，计数器加 1；而高 32 位则代表 Leader 周期 epoch 的编号，每个当选产生一个新 的 Leader 服务器，就会从这个 Leader 服务器上取出其本地日志中最大事务的 ZXID，并从中读取epoch 值，然后加 1，以此作为新的 epoch，并将低 32 位从 0 开始计数
- epoch 可以理解为当前集群所处的年代或者周期，每个 leader 就像皇帝，都有自己的年号，所以每次改朝换代，leader 变更之后，都会在前一个年代的基础上加 1。这样就算旧的 leader 崩溃恢复之后，也没有人听他的了，因为 follower 只听从当前年代的 leader 的命令。

### 模式
- 恢复模式(选主) 当服务启动或者在领导者崩溃后，Zab 就进入了恢复模式，当领导者被选举出来，且大多数 Server 完成了和 leader 的状态同步以后，恢复模式就结束了
- 广播模式(同步)

### 4阶段
#### 选举阶段 
节点在一开始都处于选举阶段，只要有一个节点得到超半数 节点的票数，它就可以当选准 leader。只有到达 广播阶段（broadcast） 准 leader 才会成 为真正的 leader。这一阶段的目的是就是为了选出一个准 leader，然后进入下一个阶段
#### 发现阶段
在这个阶段，followers 跟准 leader 进行通信，同步 followers 最近接收的事务提议。这个一阶段的主要目的是发现当前大多数节点接收的最新提议，并且 准 leader 生成新的 epoch，让 followers 接受，更新它们的 accepted Epoch 一个 follower 只会连接一个 leader，如果有一个节点 f 认为另一个 follower p 是 leader，f 在尝试连接 p 时会被拒绝，f 被拒绝之后，就会进入重新选举阶段。
#### 同步阶段
同步阶段主要是利用 leader 前一阶段获得的最新提议历史，同步集群中所有的副本。只有当 大多数节点都同步完成，准 leader 才会成为真正的 leader。follower 只会接收 zxid 比自己的 lastZxid 大的提议。
#### 广播阶段
到了这个阶段，Zookeeper 集群才能正式对外提供事务服务，并且 leader 可以进行消息广播。同时如果有新的节点加入，还需要对新节点进行同步