
* [Zookeeper](#zookeeper)
* [概念](#概念)
* [用zookeeper可以干嘛](#用zookeeper可以干嘛)
* [数据结构](#数据结构)
    * [ZNode](#znode)
        * [ZNode的类型](#znode的类型)
        * [ZNode的状态信息](#znode的状态信息)
* [监听机制](#监听机制)
    * [Watcher注册监听器实例：基于Zookeeper实现简易版配置中心](#watcher注册监听器实例基于zookeeper实现简易版配置中心)
* [角色](#角色)
    * [leader](#leader)
    * [follower](#follower)
    * [Observer](#observer)
* [Zookeeper Leader 选举原理](#zookeeper-leader-选举原理)
    * [1、服务器启动时的 leader 选举](#1服务器启动时的-leader-选举)
    * [2、运行过程中的 leader 选举](#2运行过程中的-leader-选举)
* [参考文章](#参考文章)


# Zookeeper
# 概念
- Zookeeper 是一个分布式协调服务，可用于服务发现，分布式锁，分布式领导选举，配置管理等。
- Zookeeper 提供了一个类似于 Linux 文件系统的树形结构（可认为是轻量级的内存文件系统，但 只适合存少量信息，完全不适合存储大量文件或者大文件），同时提供了对于每个节点的监控与通知机制。

# 用zookeeper可以干嘛
- 统一命令服务  域名和Ip的映射关系用zk储存，nginx也可以
- 统一配置管理，分布式环境下的配置文件同步，将配置文件写入一个znode，其他节点监听这个节点
- 统一集群管理，分布式环境下各个节点的状态同步，将节点状态写入一个znode，其他节点监听这个节点
# 数据结构
zookeeper 提供的名称空间非常类似于标准文件系统，key-value 的形式存储。名称 key 由斜线 / 分割的一系列路径元素，zookeeper 名称空间中的每个节点都是由一个路径标识

## ZNode
ZooKeeper数据模型ZNode 在ZooKeeper中，数据信息被保存在一个个数据节点上，这些节点被称为ZNode。ZNode 是Zookeeper 中最小数据单位，在 ZNode 下面又可以再挂 ZNode，这样一层层下去就形成了一个层次化命名空间 ZNode 树，我们称为 ZNode Tree，它采用了类似文件系统的层级树状结构进行管理
- 可以储存少量数据（1MB）
### ZNode的类型
Zookeeper 节点类型可以分为三大类：
- 持久性节点（Persistent）
- 临时性节点（Ephemeral）-e
- 顺序性节点（Sequential）-s -es

在开发中在创建节点的时候通过组合可以生成以下四种节点类型：持久节点、持久顺序节点(-s)、临时节点、临时顺序节点(-es)。不同类型的节点则会有不同的生命周期：

**持久节点**：是Zookeeper中最常见的一种节点类型，所谓持久节点，就是指节点被创建后会一直存在服务器，直到删除操作主动清除
- create /node
- 默认类型

**持久顺序节点**：就是有顺序的持久节点，节点特性和持久节点是一样的，只是额外特性表现在顺序上。顺序特性实质是在创建节点的时候，会在节点名后面加上一个数字后缀，来表示其顺序。
- create -s /node


**临时节点**：就是会被自动清理掉的节点，它的生命周期和客户端会话绑在一起，客户端会话结束，节点会被删除掉。与持久性节点不同的是，临时节点不能创建子节点。
- create -e /node

**临时顺序节点**：就是有顺序的临时节点，和持久顺序节点相同，在其创建的时候会在名字后面加上数字后缀。
- create -es /node
### ZNode的状态信息
整个 ZNode 节点内容包括两部分：节点数据内容和节点状态信息。数据内容是空，其他的属于状态信息。这些节点的状态信息分别的含义如下所示：

```html
cZxid 就是 Create ZXID，表示节点被创建时的事务ID。
ctime 就是 Create Time，表示节点创建时间。
mZxid 就是 Modified ZXID，表示节点最后一次被修改时的事务ID。
mtime 就是 Modified Time，表示节点最后一次被修改的时间。
pZxid 表示该节点的子节点列表最后一次被修改时的事务 ID。只有子节点列表变更才会更新 pZxid，子节点内容变更不会更新。
cversion 表示子节点的版本号。
dataVersion 表示内容版本号。
aclVersion 标识acl版本
ephemeralOwner 表示创建该临时节点时的会话 sessionID，如果是持久性节点那么值为 0
dataLength 表示数据长度。
numChildren 表示直系子节点数。
```

#  监听机制
Zookeeper使用Watcher机制实现分布式数据的发布/订阅功能

一个典型的发布/订阅模型系统定义了一种 一对多的订阅关系，能够让多个订阅者同时监听某一个主题对象，当这个主题对象自身状态变化时，会通知所有订阅者，使它们能够做出相应的处理。

在 ZooKeeper 中，引入了 Watcher 机制来实现这种分布式的通知功能。ZooKeeper 允许客户端向服务端注册一个 Watcher 监听，当服务端的一些指定事件触发了这个 Watcher，那么Zk就会向指定客户端发送一个事件通知来实现分布式的通知功能。

整个Watcher注册与通知过程如图所示。

![](../img/消息队列/zookeeper/监听机制.png)

- Client向ZK注册监听器。监听某个目录 可以监听下面的子节点， 也可以监听下面的数据。
- 客户端在向Zookeeper服务器注册的同时，会将Watcher对象存储在客户端的WatcherManager当中。用来对各种监听器进行管理。
- 当Zookeeper服务器触发Watcher事件后，会向客户端发送通知。如果监听的目录中的数据或节点发生了改变，ZK就会发送一个通知到Client。这里的流程是把Watcher对象发送到WatchManager里，则之前存储的watcher对象里面的内容就会被更新。更新之后，Client就会从WatchManager中再次获取到watcher对象，然后调用接收到通知之后的执行逻辑，比如是要把变化后的监听数据拿回来还是去做其他事情

## Watcher注册监听器实例：基于Zookeeper实现简易版配置中心
创建一个Web项目，将数据库连接信息交给Zookeeper配置中心管理，即：当项目Web项目启动时，从Zookeeper进行MySQL配置参数的拉取 

要求项目通过数据库连接池访问MySQL（连接池可以自由选择熟悉的） 

当Zookeeper配置信息变化后Web项目自动感知，正确释放之前连接池，创建新的连接池

第一步：创建web工程，客户端连接ZK集群
```java
public class ZkServlet extends HttpServlet {

    ZkClient zkClient = null;
    Connection conn = null;
    DataSource dataSource = null;

    /*
     * init: servlet对象创建的，调用此方法完成初始化操作
     * */
    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        // 客户端连接ZK集群
        new ZkClient("linux121:2181, linux122:2181, linux123:2181");

        // 判断节点是否存在，不存在创建节点并赋值
        boolean exists = zkClient.exists("/mysql_configuration");
        if (!exists) {
            zkClient.createEphemeral("/mysql_configuration", "{'driverClassName':'com.mysql.jdbc.Driver', 'url':'jdbc:mysql://linux123:3306/zookeeper?characterEncoding=UTF-8', 'username':'root', 'password':'123'}");
        }
        // 设置自定义的序列化类型
        zkClient.setZkSerializer(new ZkStrSerializer());
    }
}
```
这里将Mysql的配置信息组织成Map的格式存储在ZK结群的某一节点上，方便后续客户端的读取和使用。

第二步：从ZK集群上拉取Mysql配置文件信息，并注册监听器

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    // 初始化zk的监听器
    registerListener();

    // 客户端从节点上读取数据
    String data = (String) zkClient.readData("/mysql_configuration");
    // 利用JSON将读取下的数据格式转为Map类型，方便后续创建数据库连接池对象
    Map<String, String> map = JSON.parseObject(data, new TypeReference<Map<String, String>>(){});
    System.out.println("MysqlConfiguration: " + map);
    try {
        // 根据拉取的Mysql配置信息获取数据库连接
        conn = getDruidConnection(map);
        // 根据连接池查询数据库数据
        queryMysqlData(conn);
        // 向前端返回Mysql的配置信息
        resp.getWriter().write(map.toString());

        // 休眠10s后向zookeeper中写入新的配置文件
        Thread.sleep(10000);
        // 休眠10s后，更新该节点的数据，观察监听器的功能
        zkClient.writeData("/mysql_configuration", "{'driverClassName':'com.mysql.jdbc.Driver', 'url':'jdbc:mysql://linux123:3306/zookeeper?characterEncoding=UTF-8', 'username':'root', 'password':'12345678'}");

        // 测试结束，关闭资源
        conn.close();

    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
各自定义函数如下所示：
```java
// 注册监听器
public void registerListener(final HttpServletResponse resp)
{
    // 注册监听器，节点数据改变的类型，接收通知后的处理逻辑定义
    zkClient.subscribeDataChanges("/mysql_configuration", new IZkDataListener() {

        // path: 是监听的数据路径
        // data: 改变之后的新的数据
        public void handleDataChange(String path, Object data) throws Exception {
            // 定义接收通知之后的处理逻辑
            // 首先释放原先的连接池
            conn.close();

            // 根据新的配置信息，创建新的连接池
            // 获取新的配置信息
            Map<String, String> newMysqlConf = getMysqlConf((String) data);
            System.out.println("New Mysql Configuration: " + newMysqlConf);

            // 创建新的连接池连接数据
            conn = getDruidConnection(newMysqlConf);

            // 根据新连接查询数据
            queryMysqlData(conn);
            resp.getWriter().write("New Mysql Configuration: " + newMysqlConf);
        }

        // 处理数据的删除 -> 节点删除
        public void handleDataDeleted(String path) throws Exception {
            System.out.println(path + " is deleted!!");
        }
    });
}

public Map<String, String> getMysqlConf(String data)
{
    // 将字符串的data数据转换为Map类型
    Map<String, String> map = JSON.parseObject((String) data, new TypeReference<Map<String, String>>(){});
    return map;
}

// 通过连接池获取jdbc连接对象
public Connection getDruidConnection(Map map) throws Exception {
    dataSource = DruidDataSourceFactory.createDataSource(map);
    conn = dataSource.getConnection();
    return conn;
}

// 查询表中的数据并打印
public void queryMysqlData(Connection conn) throws SQLException {
    Statement statement = conn.createStatement();

    String sql = "select * from homework";
    ResultSet resultSet = statement.executeQuery(sql);
    while(resultSet.next())
    {
        System.out.println(resultSet.getInt("id"));
        System.out.println(resultSet.getString("name"));
        System.out.println(resultSet.getString("addr"));
    }
}
```
利用`subscribeDataChanges`函数来实现对节点数据变化的监听。这里要注意的就是`handleDataChange(String path, Object data)`方法里的data参数是改变之后的新的数据内容。因此通过代码的实际使用也可以重新理解最开始介绍的Watcher机制的过程。如果监听的目录中的数据或节点发生了改变，ZK就会发送一个通知到Client。就是把Watcher对象发送到WatchManager里，则之前存储的watcher对象里面的内容就会被更新。而Client从WatchManager中再次获取到watcher对象，此时的watcher对象的内容就是被更新后的数据信息（也就是参数data数据）
# 角色
## leader

- 一个 Zookeeper 集群同一时间只会有一个实际工作的 Leader，它会发起并维护与各 Follwer及 Observer 间的心跳。
- 所有的写操作必须要通过 Leader 完成再由 Leader 将写操作广播给其它服务器。只要有超过半数节点（不包括 observeer 节点）写入成功，该写请求就会被提交（类 2PC 协议）。

## follower
- 一个 Zookeeper 集群可能同时存在多个 Follower，它会响应 Leader 的心跳，
- Follower 可直接处理并返回客户端的读请求，同时会将写请求转发给 Leader 处理，
- 并且负责在 Leader 处理写请求时对请求进行投票。

## Observer
- 角色与 Follower 类似，但是无投票权。Zookeeper 需保证高可用和强一致性，为了支持更多的客 户端，需要增加更多 Server；Server 增多，投票阶段延迟增大，影响性能；引入 Observer，
- Observer 不参与投票； Observers 接受客户端的连接，并将写请求转发给 leader 节点； 加入更多 Observer 节点，提高伸缩性，同时不影响吞吐率。

# Zookeeper Leader 选举原理

zookeeper 的 leader 选举存在两个阶段，一个是服务器启动时 leader 选举，另一个是运行过程中 leader 服务器宕机。在分析选举原理前，先介绍几个重要的参数。

- 服务器 ID(myid)：编号越大在选举算法中权重越大
- 事务 ID(zxid)：值越大说明数据越新，权重越大
- 逻辑时钟(epoch-logicalclock)：同一轮投票过程中的逻辑时钟值是相同的，每投完一次值会增加

选举状态：

- LOOKING: 竞选状态
- FOLLOWING: 随从状态，同步 leader 状态，参与投票
- OBSERVING: 观察状态，同步 leader 状态，不参与投票
- LEADING: 领导者状态
## 1、服务器启动时的 leader 选举
每个节点启动的时候都 LOOKING 观望状态，接下来就开始进行选举主流程。这里选取三台机器组成的集群为例。第一台服务器 server1启动时，无法进行 leader 选举，当第二台服务器 server2 启动时，两台机器可以相互通信，进入 leader 选举过程。
1. 每台 server 发出一个投票，由于是初始情况，server1 和 server2 都将自己作为 leader 服务器进行投票，每次投票包含所推举的服务器myid、zxid、epoch，使用（myid，zxid）表示，此时 server1 投票为（1,0），server2 投票为（2,0），然后将各自投票发送给集群中其他机器。
2. 接收来自各个服务器的投票。集群中的每个服务器收到投票后，首先判断该投票的有效性，如检查是否是本轮投票（epoch）、是否来自 LOOKING 状态的服务器。
3. 分别处理投票。针对每一次投票，服务器都需要将其他服务器的投票和自己的投票进行对比，对比规则如下：
   1. 优先比较 epoch
   2. 检查 zxid，zxid 比较大的服务器优先作为 leader
   3. 如果 zxid 相同，那么就比较 myid，myid 较大的服务器作为 leader 服务器
4. 统计投票。每次投票后，服务器统计投票信息，判断是都有过半机器接收到相同的投票信息。server1、server2 都统计出集群中有两台机器接受了（2,0）的投票信息，此时已经选出了 server2 为 leader 节点。
5. 改变服务器状态。一旦确定了 leader，每个服务器响应更新自己的状态，如果是 follower，那么就变更为 FOLLOWING，如果是 Leader，变更为 LEADING。此时 server3继续启动，直接加入变更自己为 FOLLOWING。

![](../img/消息队列/zookeeper/选取流程.png)
## 2、运行过程中的 leader 选举
当集群中 leader 服务器出现宕机或者不可用情况时，整个集群无法对外提供服务，进入新一轮的 leader 选举。

1. 变更状态。leader 挂后，其他非 Oberver服务器将自身服务器状态变更为 LOOKING。
2. 每个 server 发出一个投票。在运行期间，每个服务器上 zxid 可能不同。
3. 处理投票。规则同启动过程。
4. 统计投票。与启动过程相同。
5. 改变服务器状态。与启动过程相同。

# 常见的问题
## 什么是Zookeeper？它的作用是什么？
Zookeeper是一个开源的分布式协调服务，用于管理大型分布式系统中的配置信息、命名服务、分布式锁、分布式队列和领导者选举等功能。

Zookeeper主要用于协调和管理分布式系统中的各种资源和服务，它提供了一个高可用的、可靠的、高性能的集中式服务，用于解决分布式系统中的一致性问题。它可以让分布式应用程序中的各个节点通过同步的方式访问共享数据，从而保证了数据的一致性和可靠性。

Zookeeper的主要作用包括：

1. 配置管理：Zookeeper可以用于集中管理分布式应用程序的配置信息，这样可以方便地对配置进行修改和更新。
2. 命名服务：Zookeeper可以用于注册和查找分布式系统中的各种服务和节点，例如分布式数据库、Web服务器、消息队列等。
3. 分布式锁：Zookeeper可以用于实现分布式锁，保证分布式系统中的各个节点能够按照一定的顺序访问共享资源，从而避免竞争和冲突。
4. 分布式队列：Zookeeper可以用于实现分布式队列，用于处理分布式系统中的消息传递和任务调度。
5. 领导者选举：Zookeeper可以用于实现领导者选举，确保在分布式系统中只有一个节点成为领导者，从而保证系统的稳定性和可靠性。

## Zookeeper是如何实现数据的一致性和可靠性的？
Zookeeper是如何实现数据的一致性和可靠性的呢？主要有以下几个方面：

- 事务日志：Zookeeper会将每一次写操作记录在本地的事务日志中，以保证数据的可靠性。如果一台服务器崩溃或者网络发生故障，Zookeeper可以通过回放事务日志来恢复数据的一致性。
- 临时节点：Zookeeper中的临时节点只有在创建它的客户端连接断开时才会被删除，这样可以确保分布式系统中的各个节点能够及时发现其他节点的故障情况，从而实现数据的一致性。
- 选择合适的数据模型：Zookeeper的数据模型非常简单，仅仅是一个层级结构的命名空间，但是却可以通过这种简单的模型来实现复杂的分布式应用程序。例如，可以通过Zookeeper的数据模型来实现分布式锁、领导者选举等功能。
- Watcher机制：Zookeeper的Watcher机制可以让客户端在节点的状态发生变化时得到通知，从而及时更新数据，保证数据的一致性。
- 集群节点的角色：Zookeeper集群中的每个节点都有特定的角色，例如Leader节点、Follower节点等。Leader节点负责处理所有的更新操作，而Follower节点则负责复制Leader节点的数据。这样可以保证数据的可靠性和一致性。

## Zookeeper中的watcher是什么？如何使用watcher机制实现分布式锁？
Zookeeper中的Watcher是一种事件通知机制，用于实现分布式应用程序中的数据监听和触发机制。Watcher机制允许客户端在节点状态发生变化时得到通知，从而可以及时更新数据，保证数据的一致性。

在Zookeeper中，客户端可以在对某个Znode节点进行操作时注册一个Watcher，当该节点的状态发生变化时，Zookeeper会向客户端发送一个事件通知，客户端可以在收到通知后进行相应的处理。

利用Watcher机制，可以实现分布式锁。实现步骤如下：

1. 在Zookeeper上创建一个Znode节点，作为锁的节点。
2. 客户端需要获取锁时，先在锁节点下创建一个临时有序节点，并获取该节点的名称。
3. 客户端检查是否自己创建的节点是当前锁节点下的最小序号节点，如果是，则获得了锁。
4. 如果不是，客户端就监听它前面的节点，等待它的前一个节点被删除（即前一个客户端释放了锁）。
5. 当前客户端收到Watcher通知后，重复步骤3和4，直到获取到锁。
6. 客户端释放锁时，删除自己创建的节点即可。

通过上述步骤，客户端就可以利用Zookeeper的Watcher机制实现分布式锁。这种方式不仅能够确保锁的可靠性，还能够避免因为网络等问题导致的死锁问题，具有很好的可靠性和性能表现。

## Zookeeper的性能瓶颈在哪里？如何优化Zookeeper的性能？
Zookeeper的性能瓶颈主要有以下几个方面：

1. 磁盘IO：Zookeeper需要频繁地进行磁盘IO操作，包括写入和读取数据。当集群规模增大时，磁盘IO会成为性能瓶颈。
2. 网络IO：Zookeeper集群中的各个节点需要频繁地进行通信，包括同步数据和处理请求等操作。网络IO的延迟和带宽瓶颈也会影响Zookeeper的性能。
3. CPU：Zookeeper需要进行复杂的计算和协调工作，包括选举Leader节点、同步数据等操作，这些操作会占用大量的CPU资源。

针对上述性能瓶颈，可以采取以下几种方式来优化Zookeeper的性能：

1. 增加硬件资源：可以增加磁盘、网络和CPU等硬件资源，以提高Zookeeper的性能。
2. 分离磁盘：可以将Zookeeper的数据和事务日志存储在不同的磁盘上，以减少磁盘IO的竞争和延迟。
3. 使用SSD：可以使用SSD代替传统的机械硬盘，以提高磁盘IO的性能。
4. 调整Zookeeper的参数：可以根据具体的场景和需求调整Zookeeper的参数，包括tickTime、syncLimit、initLimit、maxClientCnxns等。
5. 使用集群缓存：可以使用集群缓存技术，如Memcached或Redis等，将Zookeeper中的热点数据存储在内存中，以减少磁盘IO的压力。
6. 使用异步请求：可以使用异步请求的方式来减少网络IO的延迟，提高请求的吞吐量。

## 如何在Zookeeper集群中进行数据的备份和恢复？
在Zookeeper集群中进行数据备份和恢复是非常重要的，因为Zookeeper存储的数据对于整个分布式应用都非常关键。一旦出现数据丢失或损坏，可能会导致应用无法正常运行。因此，备份和恢复是Zookeeper管理和运维的重要组成部分。

以下是在Zookeeper集群中进行数据备份和恢复的一般步骤：

1. 数据备份
Zookeeper的数据备份通常使用快照（snapshot）机制。快照是Zookeeper数据的一个镜像，可以在恢复数据时使用。通过执行如下命令可以进行快照备份：
```bash
bin/zkCli.sh -server server1:2181 get / -d > snapshot.out

```
其中，server1:2181是Zookeeper集群中的任意一个节点的地址。/表示需要备份的节点路径，-d选项表示以递归方式备份该节点下的所有子节点。

快照备份的缺点是它只能备份数据到快照生成时的状态，不能备份在快照生成后的新数据。因此，为了实现更全面的备份，可以结合使用事务日志（transaction log）进行备份。

事务日志包含了Zookeeper集群中的所有数据更新，因此可以使用它来恢复数据。事务日志备份的命令如下：
```bash
cp -r /var/lib/zookeeper/data/version-2/ /path/to/backup/
```
其中，/var/lib/zookeeper/data/version-2/是Zookeeper数据目录，/path/to/backup/是备份目录。
2. 数据恢复
   恢复数据的过程是将备份的数据替换掉当前的数据。首先需要将所有节点停止，然后将备份数据拷贝到Zookeeper数据目录中，并重启所有节点。

在使用快照进行数据恢复时，可以使用load命令将快照文件导入到Zookeeper中：
```bash
bin/zkCli.sh -server server1:2181 load /path/to/snapshot.out
```
在使用事务日志进行数据恢复时，只需将备份的数据替换掉当前的数据即可。

需要注意的是，如果Zookeeper集群正在运行，不能直接覆盖数据目录中的数据，否则可能会导致数据丢失。因此，在进行数据恢复时，最好将集群中的所有节点都停止，然后再进行恢复操作。此外，需要确保备份的数据与当前集群的版本兼容。如果备份的数据与当前版本不兼容，可能需要先将集群升级到备份数据的版本，然后再进行恢复。
# 参考文章
- https://zhuanlan.zhihu.com/p/363323489
- https://www.runoob.com/w3cnote/zookeeper-leader.html
- https://chat.openai.com/