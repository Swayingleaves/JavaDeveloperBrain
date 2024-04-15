* [Apache Seata](#apache-seata)
  * [Seata 是什么?](#seata-是什么)
  * [AT 模式](#at-模式)
    * [前提](#前提)
    * [整体机制](#整体机制)
    * [写隔离](#写隔离)
    * [读隔离](#读隔离)
    * [工作机制](#工作机制)
      * [一阶段](#一阶段)
      * [二阶段\-回滚](#二阶段-回滚)
      * [二阶段\-提交](#二阶段-提交)
  * [TCC 模式](#tcc-模式)
  * [Saga 模式](#saga-模式)
  * [XA 模式](#xa-模式)
* [链接](#链接)


# Apache Seata

## Seata 是什么?

Seata 是一款开源的分布式事务解决方案，致力于提供高性能和简单易用的分布式事务服务。Seata 将为用户提供了 AT、TCC、SAGA 和 XA
事务模式，为
用户打造一站式的分布式解决方案。

在 Seata 的架构中，一共有三个角色：

![seata架构.png](..%2Fimg%2F%E5%88%86%E5%B8%83%E5%BC%8F%E7%9B%B8%E5%85%B3%2Fseata%2Fseata%E6%9E%B6%E6%9E%84.png)

- TC (Transaction Coordinator) - 事务协调者：维护全局和分支事务的状态，驱动全局事务提交或回滚。
- TM (Transaction Manager) - 事务管理器：定义全局事务的范围，开始全局事务、提交或回滚全局事务。
- RM ( Resource Manager ) - 资源管理器：管理分支事务处理的资源( Resource )，与 TC 交谈以注册分支事务和报告分支事务的状态，并驱动分支事务提交或回滚。

其中，TC 为单独部署的 Server 服务端，TM 和 RM 为嵌入到应用中的 Client 客户端。

在 Seata 中，一个分布式事务的生命周期如下：

![seata生命周期.png](..%2Fimg%2F%E5%88%86%E5%B8%83%E5%BC%8F%E7%9B%B8%E5%85%B3%2Fseata%2Fseata%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.png)

- TM 请求 TC 开启一个全局事务。TC 会生成一个 XID 作为该全局事务的编号。
    - XID，会在微服务的调用链路中传播，保证将多个微服务的子事务关联在一起。
- RM 请求 TC 将本地事务注册为全局事务的分支事务，通过全局事务的 XID 进行关联。
- TM 请求 TC 告诉 XID 对应的全局事务是进行提交还是回滚。
- TC 驱动 RM 们将 XID 对应的自己的本地事务进行提交还是回滚。

## AT 模式

### 前提

基于支持本地 ACID 事务的关系型数据库。

Java 应用，通过 JDBC 访问数据库。

### 整体机制

两阶段提交协议的演变：

- 一阶段：业务数据和回滚日志记录在同一个本地事务中提交，释放本地锁和连接资源。

- 二阶段：
    - 提交异步化，非常快速地完成。
    - 回滚通过一阶段的回滚日志进行反向补偿。

### 写隔离

- 一阶段本地事务提交前，需要确保先拿到 全局锁 。
- 拿不到 全局锁 ，不能提交本地事务。
- 拿 全局锁 的尝试被限制在一定范围内，超出范围将放弃，并回滚本地事务，释放本地锁。

以一个示例来说明：

两个全局事务 tx1 和 tx2，分别对 a 表的 m 字段进行更新操作，m 的初始值 1000。

tx1 先开始，开启本地事务，拿到本地锁，更新操作 m = 1000 - 100 = 900。本地事务提交前，先拿到该记录的 全局锁 ，本地提交释放本地锁。
tx2 后开始，开启本地事务，拿到本地锁，更新操作 m = 900 - 100 = 800。本地事务提交前，尝试拿该记录的 全局锁 ，tx1 全局提交前，该记录的全局锁被
tx1 持有，tx2 需要重试等待 全局锁 。

![at模式事物举例1.png](..%2Fimg%2F%E5%88%86%E5%B8%83%E5%BC%8F%E7%9B%B8%E5%85%B3%2Fseata%2Fat%E6%A8%A1%E5%BC%8F%E4%BA%8B%E7%89%A9%E4%B8%BE%E4%BE%8B1.png)

tx1 二阶段全局提交，释放 全局锁 。tx2 拿到 全局锁 提交本地事务。

![at模式事物举例2.png](..%2Fimg%2F%E5%88%86%E5%B8%83%E5%BC%8F%E7%9B%B8%E5%85%B3%2Fseata%2Fat%E6%A8%A1%E5%BC%8F%E4%BA%8B%E7%89%A9%E4%B8%BE%E4%BE%8B2.png)

如果 tx1 的二阶段全局回滚，则 tx1 需要重新获取该数据的本地锁，进行反向补偿的更新操作，实现分支的回滚。

此时，如果 tx2 仍在等待该数据的 全局锁，同时持有本地锁，则 tx1 的分支回滚会失败。分支的回滚会一直重试，直到 tx2 的 全局锁
等锁超时，放弃 全局锁 并回滚本地事务释放本地锁，tx1 的分支回滚最终成功。

因为整个过程 全局锁 在 tx1 结束前一直是被 tx1 持有的，所以不会发生 脏写 的问题。

### 读隔离

在数据库本地事务隔离级别 读已提交（Read Committed） 或以上的基础上，Seata（AT 模式）的默认全局隔离级别是 读未提交（Read
Uncommitted） 。

如果应用在特定场景下，必需要求全局的 读已提交 ，目前 Seata 的方式是通过 SELECT FOR UPDATE 语句的代理。

![at模式事物举例3.png](..%2Fimg%2F%E5%88%86%E5%B8%83%E5%BC%8F%E7%9B%B8%E5%85%B3%2Fseata%2Fat%E6%A8%A1%E5%BC%8F%E4%BA%8B%E7%89%A9%E4%B8%BE%E4%BE%8B3.png)

SELECT FOR UPDATE 语句的执行会申请 全局锁 ，如果 全局锁 被其他事务持有，则释放本地锁（回滚 SELECT FOR UPDATE
语句的本地执行）并重试。这个过程中，查询是被 block 住的，直到 全局锁 拿到，即读取的相关数据是 已提交 的，才返回。

出于总体性能上的考虑，Seata 目前的方案并没有对所有 SELECT 语句都进行代理，仅针对 FOR UPDATE 的 SELECT 语句。

### 工作机制

以一个示例来说明整个 AT 分支的工作过程。

业务表：product

| Field | Type         | Key |
|-------|--------------|-----|
| id    | bigint(20)   | PRI 
| name  | varchar(100) |
| since | varchar(100) |

AT 分支事务的业务逻辑：

```sql
update product
set name = 'GTS'
where name = 'TXC';
```

#### 一阶段

过程：

- 解析 SQL：得到 SQL 的类型（UPDATE），表（product），条件（where name = 'TXC'）等相关的信息。
- 查询前镜像：根据解析得到的条件信息，生成查询语句，定位数据。

  ```sql
  select id, name, since
  from product
  where name = 'TXC';
  ```
  
  得到前镜像：
  
  | id | name | since |
  |----|------|-------|
  | 1  | TXC  | 2014  |

- 执行业务 SQL：更新这条记录的 name 为 'GTS'。
- 查询后镜像：根据前镜像的结果，通过 主键 定位数据。

  ```sql
  select id, name, since
  from product
  where id = 1;
  ```

  得到后镜像：
  
  | id | name | since |
  |----|------|-------|
  | 1  | GTS  | 2014  |

- 插入回滚日志：把前后镜像数据以及业务 SQL 相关的信息组成一条回滚日志记录，插入到 UNDO_LOG 表中。
  
  ```json
  
  
  {
    "branchId": 641789253,
    "undoItems": [
      {
        "afterImage": {
          "rows": [
            {
              "fields": [
                {
                  "name": "id",
                  "type": 4,
                  "value": 1
                },
                {
                  "name": "name",
                  "type": 12,
                  "value": "GTS"
                },
                {
                  "name": "since",
                  "type": 12,
                  "value": "2014"
                }
              ]
            }
          ],
          "tableName": "product"
        },
        "beforeImage": {
          "rows": [
            {
              "fields": [
                {
                  "name": "id",
                  "type": 4,
                  "value": 1
                },
                {
                  "name": "name",
                  "type": 12,
                  "value": "TXC"
                },
                {
                  "name": "since",
                  "type": 12,
                  "value": "2014"
                }
              ]
            }
          ],
          "tableName": "product"
        },
        "sqlType": "UPDATE"
      }
    ],
    "xid": "xid:xxx"
  }
  ```

- 提交前，向 TC 注册分支：申请 product 表中，主键值等于 1 的记录的 全局锁 。
- 本地事务提交：业务数据的更新和前面步骤中生成的 UNDO LOG 一并提交。
- 将本地事务提交的结果上报给 TC。

#### 二阶段-回滚

- 收到 TC 的分支回滚请求，开启一个本地事务，执行如下操作。
- 通过 XID 和 Branch ID 查找到相应的 UNDO LOG 记录。
- 数据校验：拿 UNDO LOG 中的后镜与当前数据进行比较，如果有不同，说明数据被当前全局事务之外的动作做了修改。这种情况，需要根据配置策略来做处理，详细的说明在另外的文档中介绍。
- 根据 UNDO LOG 中的前镜像和业务 SQL 的相关信息生成并执行回滚的语句：

  ```sql
  update product
  set name = 'TXC'
  where id = 1;
  ```

- 提交本地事务。并把本地事务的执行结果（即分支事务回滚的结果）上报给 TC。

#### 二阶段-提交

- 收到 TC 的分支提交请求，把请求放入一个异步任务的队列中，马上返回提交成功的结果给 TC。
- 异步任务阶段的分支提交请求将异步和批量地删除相应 UNDO LOG 记录。

## TCC 模式

## Saga 模式

## XA 模式

# 链接

- https://seata.apache.org/zh-cn/docs/overview/what-is-seata
- https://seata.apache.org/zh-cn/blog/seata-quick-start/