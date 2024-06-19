
# 什么是Hadoop？它解决了什么问题？
Hadoop是一个开源的分布式计算框架，设计用于存储和处理大规模数据集。它通过将数据分布在多个廉价计算节点上并行处理来解决传统单机系统无法处理的大数据问题。Hadoop的核心优势在于它的扩展性和容错性，可以处理数百TB甚至PB级的数据。

# Hadoop的核心组件是什么？简要描述它们的作用。
Hadoop的核心组件包括：

- HDFS (Hadoop Distributed File System)：主要用于文件的分布式存储，适合存储大规模数据集，具备高容错性和高吞吐量的特点。
- MapReduce：Hadoop的数据处理模型，通过分布式计算框架实现大规模数据集的并行处理。
- YARN (Yet Another Resource Negotiator)：资源管理和调度系统，负责集群资源的管理和任务调度。

# 什么是HDFS（Hadoop分布式文件系统）？它的特点是什么？
HDFS是Hadoop的分布式文件系统，设计用于大规模数据存储和高吞吐量的文件访问。它的主要特点有：

- 高可扩展性：能水平扩展以处理大量数据。
- 高容错性：通过数据块副本机制确保数据的可靠性。
- 高吞吐量：优化了大数据量传输，使得读写操作高效。

# 解释MapReduce的工作原理
MapReduce是Hadoop的核心计算框架，分为两个主要阶段：

- Map阶段：输入数据被分割为小片段，由多个Mapper进行并行处理，每个Mapper生成中间键值对。
- Reduce阶段：将中间结果按键合并，由Reducer进行处理，生成最终结果。

# Mapper和Reducer的作用是什么？它们之间的交互是怎样的？
- Mapper：处理输入数据片段，将其转换为中间的键值对。
- Reducer：处理来自Mapper的键值对，将具有相同键的所有值汇总并生成最终输出。
- 交互：Mapper的输出被分发给Reducer，并在此过程中进行排序和分组，然后Reducer对其进行处理。

# 什么是Combiner？它的作用是什么？
Combiner是一种优化器，介于Mapper和Reducer之间，用于在Mapper本地进行部分汇总，减少数据传输量，提高MapReduce任务效率。

# YARN是什么？它与经典MapReduce相比有什么优势？
YARN是Hadoop的资源管理框架，负责集群资源管理和任务调度。与经典MapReduce相比，YARN的优势在于：

- 更好的资源利用：支持不同类型的计算任务，增强资源调度和管理的灵活性。
- 改进的扩展性：更易扩展到更多节点。
- 多功能性：允许在同一集群上运行多种计算框架。

# 为什么Hadoop 2版本引入了YARN？
Hadoop 2版本引入了YARN，以解决Hadoop 1.x版本中MapReduce的缺陷。YARN解决了以下问题：
- 降低资源管理复杂度：YARN将资源管理与计算框架解耦，使得资源管理更加灵活。
- 提升性能：YARN支持动态资源分配，可以动态调整计算资源的使用。
- 提升容错性：YARN支持容错性，可以自动恢复丢失的节点。
- 提升扩展性：YARN支持多种计算框架，可以轻松集成其他计算框架。
- 降低学习成本：YARN的API与MapReduce API相似，使得用户可以快速适应新的计算框架。
- 降低维护成本：YARN可以自动管理资源，减少运维成本。
- 降低开发成本：YARN可以支持多种计算框架，使得开发人员可以快速适应新的计算框架。
- 降低成本：YARN可以支持多种计算框架，使得成本降低。
- 降低风险：YARN可以支持多种计算框架，使得风险降低。

# 什么是Apache Hive？它的作用是什么？
Apache Hive是一个开源的数据仓库工具，用于查询和分析存储在Hadoop上的数据。它提供了SQL接口，使得用户可以像操作本地数据库一样操作Hadoop上的数据。

# Apache Spark和Hadoop的关系是什么？
Apache Spark是一个快且通用的集群计算系统，能够与Hadoop生态系统集成，特别是可以与HDFS等存储系统配合使用。Spark相比于传统MapReduce，提供了更高效率的数据处理和更丰富的API，支持批处理、流处理和机器学习等多种任务。

# 什么是Apache HBase？它与HDFS有什么区别？
Apache HBase是一个分布式的NoSQL数据库，基于Hadoop生态系统，用于实时读写访问超大规模数据集，类似于Google的Bigtable。与HDFS不同，HBase支持快速的读写操作和随机访问，而HDFS主要用于批处理和大数据分析。

# 如何对Hadoop作业进行性能优化？

- 数据本地化：确保计算发生在数据所在的地方，减少数据传输。
- 合理设置Mapper和Reducer数量：根据输入数据量和任务需求进行调优。
- 调优Mapper和Reducer的内存和CPU配置：确保资源使用最经济高效。
- 使用Combiner：减少数据传输量，提高效率。
- 调优HDFS配置：通过优化块大小和副本数量提高I/O性能。

# 什么是数据本地性？为什么它对Hadoop作业执行效率很重要？
数据本地性指任务在数据存储的节点上运行，从而减少数据传输量，提高作业效率。在Hadoop中，计算节点和数据存储节点往往是同一组物理节点，因此按照数据本地性原则，可以减少网络I/O，提高性能。

# 如何避免数据倾斜的问题？

- 合理设计键分区：确保数据均匀分布到各个Reducer。
- 使用Combiner：在Mapper端进行部分聚合，减少数据倾斜。
- 分批处理：对于超级节点的数据，分多批次进行处理。
- 调优分区策略：通过自定义分区函数来防止数据集中到少数Reducer上。

# 你有使用Hadoop处理过哪些大数据问题？可以具体描述一下你的经验吗？
在实际工作中，我使用Hadoop处理过例如日志分析、用户行为分析、数据ETL（提取、转换、加载）等大数据问题。具体经验包括：

- 日志分析：通过MapReduce程序解析和归档海量服务器日志，提取有用信息如错误日志和访问日志。
- 用户行为分析：使用Hive和Pig从社交网络数据中提取用户行为模式，生成报告供商业决策使用。
- 数据ETL：将异构数据源的数据导入HDFS，进行清洗、转换并存储，为后续的数据分析做好准备。

# 你如何处理处理Hadoop集群中的故障？这个过程中遇到过什么挑战？

处理Hadoop集群中的故障包括以下几个步骤：

- 监控和报警：通过使用Ganglia、Nagios等工具进行实时监控，设置告警机制及时发现故障。
- 日志分析：深入分析Hadoop的各类日志（HDFS、YARN、MapReduce）找到故障原因。
- 节点恢复和替换：对失效节点进行修复或替换，重新启动相关服务。
- 数据恢复：使用HDFS的副本机制恢复丢失的数据块，确保数据完整性。
- 遇到的挑战包括硬件故障导致的数据丢失、紧急情况下快速排查问题的压力以及协调多个组件之间的兼容性和稳定性。

## Hadoop面试题（一）

### 1、集群的最主要瓶颈
&emsp; 磁盘IO

### 2、Hadoop运行模式
&emsp; 单机版、伪分布式模式、完全分布式模式

### 3、Hadoop生态圈的组件并做简要描述
&emsp; 1）Zookeeper：是一个开源的分布式应用程序协调服务,基于zookeeper可以实现同步服务，配置维护，命名服务。  
&emsp; 2）Flume：一个高可用的，高可靠的，分布式的海量日志采集、聚合和传输的系统。   
&emsp; 3）Hbase：是一个分布式的、面向列的开源数据库, 利用Hadoop HDFS作为其存储系统。   
&emsp; 4）Hive：基于Hadoop的一个数据仓库工具，可以将结构化的数据档映射为一张数据库表，并提供简单的sql 查询功能，可以将sql语句转换为MapReduce任务进行运行。   
&emsp; 5）Sqoop：将一个关系型数据库中的数据导进到Hadoop的 HDFS中，也可以将HDFS的数据导进到关系型数据库中。

### 4、解释“hadoop”和“hadoop 生态系统”两个概念
&emsp; Hadoop是指Hadoop框架本身；hadoop生态系统，不仅包含hadoop，还包括保证hadoop框架正常高效运行其他框架，比如zookeeper、Flume、Hbase、Hive、Sqoop等辅助框架。

### 5、请列出正常工作的Hadoop集群中Hadoop都分别需要启动哪些进程，它们的作用分别是什么?
&emsp; 1）NameNode：它是hadoop中的主服务器，管理文件系统名称空间和对集群中存储的文件的访问，保存有metadate。  
&emsp; 2）SecondaryNameNode：它不是namenode的冗余守护进程，而是提供周期检查点和清理任务。帮助NN合并editslog，减少NN启动时间。  
&emsp; 3）DataNode：它负责管理连接到节点的存储（一个集群中可以有多个节点）。每个存储数据的节点运行一个datanode守护进程。  
&emsp; 4）ResourceManager（JobTracker）：JobTracker负责调度DataNode上的工作。每个DataNode有一个TaskTracker，它们执行实际工作。  
&emsp; 5）NodeManager：（TaskTracker）执行任务。  
&emsp; 6）DFSZKFailoverController：高可用时它负责监控NN的状态，并及时的把状态信息写入ZK。它通过一个独立线程周期性的调用NN上的一个特定接口来获取NN的健康状态。FC也有选择谁作为Active NN的权利，因为最多只有两个节点，目前选择策略还比较简单（先到先得，轮换）。  
&emsp; 7）JournalNode：高可用情况下存放namenode的editlog文件。  


## Hadoop面试题总结（二）——HDFS

### 1、 HDFS 中的 block 默认保存几份？
&emsp; 默认保存3份

### 2、HDFS 默认 BlockSize 是多大？
&emsp; 默认64MB

### 3、负责HDFS数据存储的是哪一部分？
&emsp; DataNode负责数据存储

### 4、SecondaryNameNode的目的是什么？
&emsp; 他的目的使帮助NameNode合并编辑日志，减少NameNode 启动时间

### 5、文件大小设置，增大有什么影响？
&emsp; HDFS中的文件在物理上是分块存储（block），块的大小可以通过配置参数( dfs.blocksize)来规定，默认大小在hadoop2.x版本中是128M，老版本中是64M。  
&emsp; **思考：为什么块的大小不能设置的太小，也不能设置的太大？**  
&emsp; &emsp; HDFS的块比磁盘的块大，其目的是为了最小化寻址开销。如果块设置得足够大，从磁盘传输数据的时间会明显大于定位这个块开始位置所需的时间。
因而，**传输一个由多个块组成的文件的时间取决于磁盘传输速率**。  
&emsp; 如果寻址时间约为10ms，而传输速率为100MB/s，为了使寻址时间仅占传输时间的1%，我们要将块大小设置约为100MB。默认的块大小128MB。  
&emsp; 块的大小：10ms×100×100M/s = 100M，如图  
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/HDFS%E5%9D%97.png"/>  
&emsp; 增加文件块大小，需要增加磁盘的传输速率。

### 6、hadoop的块大小，从哪个版本开始是128M
&emsp; Hadoop1.x都是64M，hadoop2.x开始都是128M。

### 7、HDFS的存储机制（☆☆☆☆☆）
&emsp; HDFS存储机制，包括HDFS的**写入数据过程**和**读取数据过程**两部分  
&emsp; **HDFS写数据过程**
<p align="center">
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/HDFS%E5%86%99%E6%95%B0%E6%8D%AE%E6%B5%81%E7%A8%8B.png"/>  
<p align="center">
</p>
</p>  

&emsp; 1）客户端通过Distributed FileSystem模块向NameNode请求上传文件，NameNode检查目标文件是否已存在，父目录是否存在。  
&emsp; 2）NameNode返回是否可以上传。  
&emsp; 3）客户端请求第一个 block上传到哪几个datanode服务器上。  
&emsp; 4）NameNode返回3个datanode节点，分别为dn1、dn2、dn3。  
&emsp; 5）客户端通过FSDataOutputStream模块请求dn1上传数据，dn1收到请求会继续调用dn2，然后dn2调用dn3，将这个通信管道建立完成。  
&emsp; 6）dn1、dn2、dn3逐级应答客户端。  
&emsp; 7）客户端开始往dn1上传第一个block（先从磁盘读取数据放到一个本地内存缓存），以packet为单位，dn1收到一个packet就会传给dn2，dn2传给dn3；
dn1每传一个packet会放入一个应答队列等待应答。  
&emsp; 8）当一个block传输完成之后，客户端再次请求NameNode上传第二个block的服务器。（重复执行3-7步）。

&emsp; **HDFS读数据过程**
<p align="center">
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/HDFS%E8%AF%BB%E6%95%B0%E6%8D%AE%E6%B5%81%E7%A8%8B.png"/>  
<p align="center">
</p>
</p>  

&emsp; 1）客户端通过Distributed FileSystem向NameNode请求下载文件，NameNode通过查询元数据，找到文件块所在的DataNode地址。  
&emsp; 2）挑选一台DataNode（就近原则，然后随机）服务器，请求读取数据。  
&emsp; 3）DataNode开始传输数据给客户端（从磁盘里面读取数据输入流，以packet为单位来做校验）。  
&emsp; 4）客户端以packet为单位接收，先在本地缓存，然后写入目标文件。

### 8、secondary namenode工作机制（☆☆☆☆☆）
<p align="center">
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/secondary%20namenode%E5%B7%A5%E4%BD%9C%E6%9C%BA%E5%88%B6.png"/>  
<p align="center">
</p>
</p>  

**1）第一阶段：NameNode启动**  
&emsp; （1）第一次启动NameNode格式化后，创建fsimage和edits文件。如果不是第一次启动，直接加载编辑日志和镜像文件到内存。   
&emsp; （2）客户端对元数据进行增删改的请求。   
&emsp; （3）NameNode记录操作日志，更新滚动日志。   
&emsp; （4）NameNode在内存中对数据进行增删改查。  
**2）第二阶段：Secondary NameNode工作**  
&emsp; （1）Secondary NameNode询问NameNode是否需要checkpoint。直接带回NameNode是否检查结果。  
&emsp; （2）Secondary NameNode请求执行checkpoint。  
&emsp; （3）NameNode滚动正在写的edits日志。  
&emsp; （4）将滚动前的编辑日志和镜像文件拷贝到Secondary NameNode。  
&emsp; （5）Secondary NameNode加载编辑日志和镜像文件到内存，并合并。  
&emsp; （6）生成新的镜像文件fsimage.chkpoint。  
&emsp; （7）拷贝fsimage.chkpoint到NameNode。  
&emsp; （8）NameNode将fsimage.chkpoint重新命名成fsimage。

### 9、NameNode与SecondaryNameNode 的区别与联系？（☆☆☆☆☆）
**机制流程看第7题**  
1）区别  
&emsp; （1）NameNode负责管理整个文件系统的元数据，以及每一个路径（文件）所对应的数据块信息。  
&emsp; （2）SecondaryNameNode主要用于定期合并命名空间镜像和命名空间镜像的编辑日志。  
2）联系：  
&emsp; （1）SecondaryNameNode中保存了一份和namenode一致的镜像文件（fsimage）和编辑日志（edits）。  
&emsp; （2）在主namenode发生故障时（假设没有及时备份数据），可以从SecondaryNameNode恢复数据。

### 10、HDFS组成架构（☆☆☆☆☆）
<p align="center">
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/HDFS%E7%BB%84%E6%88%90%E6%9E%B6%E6%9E%84.png"/>  
<p align="center">
</p>
</p>  

架构主要由四个部分组成，分别为**HDFS Client、NameNode、DataNode和Secondary NameNode**。下面我们分别介绍这四个组成部分。  
1）Client：就是客户端。       
&emsp; （1）文件切分。文件上传HDFS的时候，Client将文件切分成一个一个的Block，然后进行存储；         
&emsp; （2）与NameNode交互，获取文件的位置信息；  
&emsp; （3）与DataNode交互，读取或者写入数据；      
&emsp; （4）Client提供一些命令来管理HDFS，比如启动或者关闭HDFS；  
&emsp; （5）Client可以通过一些命令来访问HDFS；  
2）NameNode：就是Master，它是一个主管、管理者。  
&emsp; （1）管理HDFS的名称空间；  
&emsp; （2）管理数据块（Block）映射信息；  
&emsp; （3）配置副本策略；  
&emsp; （4）处理客户端读写请求。  
3）DataNode：就是Slave。NameNode下达命令，DataNode执行实际的操作。  
&emsp; （1）存储实际的数据块；  
&emsp; （2）执行数据块的读/写操作。  
4）Secondary NameNode：并非NameNode的热备。当NameNode挂掉的时候，它并不能马上替换NameNode并提供服务。  
&emsp; （1）辅助NameNode，分担其工作量；  
&emsp; （2）定期合并Fsimage和Edits，并推送给NameNode；  
&emsp; （3）在紧急情况下，可辅助恢复NameNode。

### 11、HAnamenode 是如何工作的? （☆☆☆☆☆）
<p align="center">
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/HAnamenode%E5%B7%A5%E4%BD%9C%E6%9C%BA%E5%88%B6.png"/>  
<p align="center">
</p>
</p>  

ZKFailoverController主要职责  
&emsp; 1）健康监测：周期性的向它监控的NN发送健康探测命令，从而来确定某个NameNode是否处于健康状态，如果机器宕机，心跳失败，那么zkfc就会标记它处于一个不健康的状态。  
&emsp; 2）会话管理：如果NN是健康的，zkfc就会在zookeeper中保持一个打开的会话，如果NameNode同时还是Active状态的，那么zkfc还会在Zookeeper中占有一个类型为短暂类型的znode，当这个NN挂掉时，这个znode将会被删除，然后备用的NN，将会得到这把锁，升级为主NN，同时标记状态为Active。  
&emsp; 3）当宕机的NN新启动时，它会再次注册zookeper，发现已经有znode锁了，便会自动变为Standby状态，如此往复循环，保证高可靠，需要注意，目前仅仅支持最多配置2个NN。  
&emsp; 4）master选举：如上所述，通过在zookeeper中维持一个短暂类型的znode，来实现抢占式的锁机制，从而判断那个NameNode为Active状态

## Hadoop面试题总结（三）——MapReduce

### 1、谈谈Hadoop序列化和反序列化及自定义bean对象实现序列化?
1）序列化和反序列化  
&emsp; （1）序列化就是把内存中的对象，转换成字节序列（或其他数据传输协议）以便于存储（持久化）和网络传输。   
&emsp; （2）反序列化就是将收到字节序列（或其他数据传输协议）或者是硬盘的持久化数据，转换成内存中的对象。  
&emsp; （3）Java的序列化是一个重量级序列化框架（Serializable），一个对象被序列化后，会附带很多额外的信息（各种校验信息，header，继承体系等），不便于在网络中高效传输。所以，hadoop自己开发了一套序列化机制（Writable），精简、高效。  
2）自定义bean对象要想序列化传输步骤及注意事项：  
&emsp; （1）必须实现Writable接口  
&emsp; （2）反序列化时，需要反射调用空参构造函数，所以必须有空参构造  
&emsp; （3）重写序列化方法  
&emsp; （4）重写反序列化方法  
&emsp; （5）注意反序列化的顺序和序列化的顺序完全一致  
&emsp; （6）要想把结果显示在文件中，需要重写toString()，且用"\t"分开，方便后续用  
&emsp; （7）如果需要将自定义的bean放在key中传输，则还需要实现comparable接口，因为mapreduce框中的shuffle过程一定会对key进行排序

### 2、FileInputFormat切片机制（☆☆☆☆☆）
job提交流程源码详解  
&emsp; waitForCompletion()  
&emsp; submit();  
&emsp; // 1、建立连接  
&emsp; &emsp; connect();   
&emsp; &emsp; &emsp; // 1）创建提交job的代理  
&emsp; &emsp; &emsp; new Cluster(getConfiguration());  
&emsp; &emsp; &emsp; &emsp; // （1）判断是本地yarn还是远程  
&emsp; &emsp; &emsp; &emsp; initialize(jobTrackAddr, conf);  
&emsp; // 2、提交job  
&emsp; submitter.submitJobInternal(Job.this, cluster)  
&emsp; &emsp; // 1）创建给集群提交数据的Stag路径  
&emsp; &emsp; Path jobStagingArea = JobSubmissionFiles.getStagingDir(cluster, conf);  
&emsp; &emsp; // 2）获取jobid ，并创建job路径  
&emsp; &emsp; JobID jobId = submitClient.getNewJobID();  
&emsp; &emsp; // 3）拷贝jar包到集群  
&emsp; &emsp; copyAndConfigureFiles(job, submitJobDir);  
&emsp; &emsp; rUploader.uploadFiles(job, jobSubmitDir);  
&emsp; &emsp; // 4）计算切片，生成切片规划文件  
&emsp; &emsp; writeSplits(job, submitJobDir);  
&emsp; &emsp; maps = writeNewSplits(job, jobSubmitDir);  
&emsp; &emsp; input.getSplits(job);  
&emsp; &emsp; // 5）向Stag路径写xml配置文件  
&emsp; &emsp; writeConf(conf, submitJobFile);  
&emsp; &emsp; conf.writeXml(out);  
&emsp; &emsp; // 6）提交job,返回提交状态  
&emsp; &emsp; status = submitClient.submitJob(jobId, submitJobDir.toString(), job.getCredentials());

### 3、在一个运行的Hadoop 任务中，什么是InputSplit？（☆☆☆☆☆）
FileInputFormat源码解析(input.getSplits(job))  
（1）找到你数据存储的目录。  
（2）开始遍历处理（规划切片）目录下的每一个文件。  
（3）遍历第一个文件ss.txt。  
&emsp; a）获取文件大小fs.sizeOf(ss.txt);。  
&emsp; b）计算切片大小computeSliteSize(Math.max(minSize,Math.min(maxSize,blocksize)))=blocksize=128M。  
&emsp; c）**默认情况下，切片大小=blocksize**。  
&emsp; d）开始切，形成第1个切片：ss.txt—0:128M 第2个切片ss.txt—128:256M 第3个切片ss.txt—256M:300M（每次切片时，都要判断切完剩下的部分是否大于块的1.1倍，**不大于1.1倍就划分一块切片**）。   
&emsp; e）将切片信息写到一个切片规划文件中。  
&emsp; f）整个切片的核心过程在getSplit()方法中完成。  
&emsp; g）数据切片只是在逻辑上对输入数据进行分片，并不会再磁盘上将其切分成分片进行存储。InputSplit只记录了分片的元数据信息，比如起始位置、长度以及所在的节点列表等。  
&emsp; h）注意：block是HDFS上物理上存储的存储的数据，切片是对数据逻辑上的划分。  
（4）**提交切片规划文件到yarn上，yarn上的MrAppMaster就可以根据切片规划文件计算开启maptask个数**。

### 4、如何判定一个job的map和reduce的数量?
1）map数量  
&emsp; splitSize=max{minSize,min{maxSize,blockSize}}  
&emsp; map数量由处理的数据分成的block数量决定default_num = total_size / split_size;  
2）reduce数量  
&emsp; reduce的数量job.setNumReduceTasks(x);x 为reduce的数量。不设置的话默认为 1。

### 5、 Maptask的个数由什么决定？
&emsp; 一个job的map阶段MapTask并行度（个数），由客户端提交job时的切片个数决定。

### 6、MapTask和ReduceTask工作机制（☆☆☆☆☆）（也可回答MapReduce工作原理）
**MapTask工作机制**
<p align="center">
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/MR-Pics/MapTask%E5%B7%A5%E4%BD%9C%E6%9C%BA%E5%88%B6.png"/>  
<p align="center">
</p>
</p>  

（1）Read阶段：Map Task通过用户编写的RecordReader，从输入InputSplit中解析出一个个key/value。  
（2）Map阶段：该节点主要是将解析出的key/value交给用户编写map()函数处理，并产生一系列新的key/value。  
（3）Collect收集阶段：在用户编写map()函数中，当数据处理完成后，一般会调用OutputCollector.collect()输出结果。在该函数内部，它会将生成的key/value分区（调用Partitioner），并写入一个环形内存缓冲区中。  
（4）Spill阶段：即“溢写”，当环形缓冲区满后，MapReduce会将数据写到本地磁盘上，生成一个临时文件。需要注意的是，将数据写入本地磁盘之前，先要对数据进行一次本地排序，并在必要时对数据进行合并、压缩等操作。  
（5）Combine阶段：当所有数据处理完成后，MapTask对所有临时文件进行一次合并，以确保最终只会生成一个数据文件。

**ReduceTask工作机制**
<p align="center">
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/MR-Pics/ReduceTask%E5%B7%A5%E4%BD%9C%E6%9C%BA%E5%88%B6.png"/>  
<p align="center">
</p>
</p>  

（1）Copy阶段：ReduceTask从各个MapTask上远程拷贝一片数据，并针对某一片数据，如果其大小超过一定阈值，则写到磁盘上，否则直接放到内存中。  
（2）Merge阶段：在远程拷贝数据的同时，ReduceTask启动了两个后台线程对内存和磁盘上的文件进行合并，以防止内存使用过多或磁盘上文件过多。  
（3）Sort阶段：按照MapReduce语义，用户编写reduce()函数输入数据是按key进行聚集的一组数据。为了将key相同的数据聚在一起，Hadoop采用了基于排序的策略。 由于各个MapTask已经实现对自己的处理结果进行了局部排序，因此，ReduceTask只需对所有数据进行一次归并排序即可。  
（4）Reduce阶段：reduce()函数将计算结果写到HDFS上。

### 7、描述mapReduce有几种排序及排序发生的阶段（☆☆☆☆☆）
1）排序的分类：  
&emsp; （1）部分排序：  
&emsp; &emsp; MapReduce根据输入记录的键对数据集排序。保证输出的每个文件内部排序。  
&emsp; （2）全排序：  
&emsp; &emsp; 如何用Hadoop产生一个全局排序的文件？最简单的方法是使用一个分区。但该方法在处理大型文件时效率极低，因为一台机器必须处理所有输出文件，从而完全丧失了MapReduce所提供的并行架构。  
&emsp; &emsp; 替代方案：首先创建一系列排好序的文件；其次，串联这些文件；最后，生成一个全局排序的文件。主要思路是使用一个分区来描述输出的全局排序。例如：可以为待分析文件创建3个分区，在第一分区中，记录的单词首字母a-g，第二分区记录单词首字母h-n, 第三分区记录单词首字母o-z。  
&emsp; （3）辅助排序：（GroupingComparator分组）  
&emsp; &emsp; Mapreduce框架在记录到达reducer之前按键对记录排序，但键所对应的值并没有被排序。甚至在不同的执行轮次中，这些值的排序也不固定，因为它们来自不同的map任务且这些map任务在不同轮次中完成时间各不相同。一般来说，大多数MapReduce程序会避免让reduce函数依赖于值的排序。但是，有时也需要通过特定的方法对键进行排序和分组等以实现对值的排序。  
&emsp; （4）二次排序：  
&emsp; &emsp; 在自定义排序过程中，如果compareTo中的判断条件为两个即为二次排序。  
2）自定义排序WritableComparable  
&emsp; bean对象实现WritableComparable接口重写compareTo方法，就可以实现排序  
&emsp; &emsp; @Override  
&emsp; &emsp; public int compareTo(FlowBean o) {  
&emsp; &emsp; &emsp; // 倒序排列，从大到小  
&emsp; &emsp; &emsp; return this.sumFlow > o.getSumFlow() ? -1 : 1;  
&emsp; &emsp; }  
3）排序发生的阶段：  
&emsp; （1）一个是在map side发生在spill后partition前。  
&emsp; （2）一个是在reduce side发生在copy后 reduce前。

### 8、描述mapReduce中shuffle阶段的工作流程，如何优化shuffle阶段（☆☆☆☆☆）
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/MR-Pics/mapReduce%E4%B8%ADshuffle%E9%98%B6%E6%AE%B5%E7%9A%84%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B.png"/>  

分区，排序，溢写，拷贝到对应reduce机器上，增加combiner，压缩溢写的文件。

### 9、描述mapReduce中combiner的作用是什么，一般使用情景，哪些情况不需要，及和reduce的区别？
1）Combiner的意义就是对每一个maptask的输出进行局部汇总，以减小网络传输量。  
2）Combiner能够应用的前提是不能影响最终的业务逻辑，而且，Combiner的输出kv应该跟reducer的输入kv类型要对应起来。  
3）Combiner和reducer的区别在于运行的位置。  
&emsp; Combiner是在每一个maptask所在的节点运行；  
&emsp; Reducer是接收全局所有Mapper的输出结果。

<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/MR-Pics/mapReduce%E4%B8%ADcombiner%E4%BD%9C%E7%94%A8.png"/>

### 10、如果没有定义partitioner，那数据在被送达reducer前是如何被分区的？
&emsp; 如果没有自定义的 partitioning，则默认的 partition 算法，即根据每一条数据的 key 的 hashcode 值摸运算（%）reduce 的数量，得到的数字就是“分区号“。

### 11、MapReduce 出现单点负载多大，怎么负载平衡？ （☆☆☆☆☆）
&emsp; 通过Partitioner实现

### 12、MapReduce 怎么实现 TopN？ （☆☆☆☆☆）
&emsp; 可以自定义groupingcomparator，对结果进行最大值排序，然后再reduce输出时，控制只输出前n个数。就达到了topn输出的目的。

### 13、Hadoop的缓存机制（Distributedcache）（☆☆☆☆☆）
&emsp; 分布式缓存一个最重要的应用就是在进行join操作的时候，如果一个表很大，另一个表很小，我们就可以将这个小表进行广播处理，即每个计算节点上都存一份，然后进行map端的连接操作，经过我的实验验证，这种情况下处理效率大大高于一般的reduce端join，广播处理就运用到了分布式缓存的技术。  
&emsp; DistributedCache将拷贝缓存的文件到Slave节点在任何Job在节点上执行之前，文件在每个Job中只会被拷贝一次，缓存的归档文件会被在Slave节点中解压缩。将本地文件复制到HDFS中去，接着Client会通过addCacheFile() 和addCacheArchive()方法告诉DistributedCache在HDFS中的位置。当文件存放到文地时，JobClient同样获得DistributedCache来创建符号链接，其形式为文件的URI加fragment标识。当用户需要获得缓存中所有有效文件的列表时，JobConf 的方法 getLocalCacheFiles() 和getLocalArchives()都返回一个指向本地文件路径对象数组。

### 14、如何使用mapReduce实现两个表的join?（☆☆☆☆☆）
&emsp; 1）reduce side join : 在map阶段，map函数同时读取两个文件File1和File2，为了区分两种来源的key/value数据对，对每条数据打一个标签（tag）,比如：tag=0 表示来自文件File1，tag=2 表示来自文件File2。  
&emsp; 2）map side join : Map side join 是针对以下场景进行的优化：两个待连接表中，有一个表非常大，而另一个表非常小，以至于小表可以直接存放到内存中。这样，我们可以将小表复制多份，让每个map task 内存中存在一份（比如存放到hash table 中），然后只扫描大表：对于大表中的每一条记录key/value，在hash table 中查找是否有相同的key 的记录，如果有，则连接后输出即可。

### 15、什么样的计算不能用mr来提速？
&emsp; 1）数据量很小。  
&emsp; 2）繁杂的小文件。  
&emsp; 3）索引是更好的存取机制的时候。  
&emsp; 4）事务处理。  
&emsp; 5）只有一台机器的时候。

### 16、ETL是哪三个单词的缩写
&emsp; Extraction-Transformation-Loading的缩写，中文名称为数据提取、转换和加载。  

## Hadoop面试题（四）——YARN

### 1、简述hadoop1与hadoop2 的架构异同
&emsp; 1）加入了yarn解决了资源调度的问题。  
&emsp; 2）加入了对zookeeper的支持实现比较可靠的高可用。

### 2、为什么会产生 yarn,它解决了什么问题，有什么优势？
&emsp; 1）Yarn最主要的功能就是解决运行的用户程序与yarn框架完全解耦。  
&emsp; 2）Yarn上可以运行各种类型的分布式运算程序（mapreduce只是其中的一种），比如mapreduce、storm程序，spark程序……

### 3、HDFS的数据压缩算法?（☆☆☆☆☆）
&emsp; Hadoop中常用的压缩算法有**bzip2、gzip、lzo、snappy**，其中lzo、snappy需要操作系统安装native库才可以支持。  
&emsp; 数据可以压缩的位置如下所示。
<p align="center">
<img src="https://github.com/Dr11ft/BigDataGuide/blob/master/Pics/Hadoop%E9%9D%A2%E8%AF%95%E9%A2%98Pics/YARN-Pics/MapReduce%E6%95%B0%E6%8D%AE%E5%8E%8B%E7%BC%A9.png"/>  
<p align="center">
</p>
</p>  

&emsp; **企业开发用的比较多的是snappy**。

### 4、Hadoop的调度器总结（☆☆☆☆☆）
（1）默认的调度器FIFO  
&emsp; Hadoop中默认的调度器，它先按照作业的优先级高低，再按照到达时间的先后选择被执行的作业。  
（2）计算能力调度器Capacity Scheduler  
&emsp; 支持多个队列，每个队列可配置一定的资源量，每个队列采用FIFO调度策略，为了防止同一个用户的作业独占队列中的资源，该调度器会对同一用户提交的作业所占资源量进行限定。调度时，首先按以下策略选择一个合适队列：计算每个队列中正在运行的任务数与其应该分得的计算资源之间的比值，选择一个该比值最小的队列；然后按以下策略选择该队列中一个作业：按照作业优先级和提交时间顺序选择，同时考虑用户资源量限制和内存限制。   
（3）公平调度器Fair Scheduler  
&emsp; 同计算能力调度器类似，支持多队列多用户，每个队列中的资源量可以配置，同一队列中的作业公平共享队列中所有资源。实际上，Hadoop的调度器远不止以上三种，最近，出现了很多针对新型应用的Hadoop调度器。

### 5、MapReduce 2.0 容错性（☆☆☆☆☆）
1）MRAppMaster容错性  
&emsp; 一旦运行失败，由YARN的ResourceManager负责重新启动，最多重启次数可由用户设置，默认是2次。一旦超过最高重启次数，则作业运行失败。   
2）Map Task/Reduce  
&emsp; Task Task周期性向MRAppMaster汇报心跳；一旦Task挂掉，则MRAppMaster将为之重新申请资源，并运行之。最多重新运行次数可由用户设置，默认4次。

### 6、mapreduce推测执行算法及原理（☆☆☆☆☆）
1）作业完成时间取决于最慢的任务完成时间  
&emsp; 一个作业由若干个Map 任务和Reduce 任务构成。因硬件老化、软件Bug 等，某些任务可能运行非常慢。  
&emsp; 典型案例：系统中有99%的Map任务都完成了，只有少数几个Map老是进度很慢，完不成，怎么办？  
2）推测执行机制  
&emsp; 发现拖后腿的任务，比如某个任务运行速度远慢于任务平均速度。为拖后腿任务启动一个备份任务，同时运行。谁先运行完，则采用谁的结果。  
3）不能启用推测执行机制情况  
&emsp; （1）任务间存在严重的负载倾斜；  
&emsp; （2）特殊任务，比如任务向数据库中写数据。  
4）算法原理  
&emsp; 假设某一时刻，任务T的执行进度为progress，则可通过一定的算法推测出该任务的最终完成时刻estimateEndTime。另一方面，如果此刻为该任务启动一个备份任务，则可推断出它可能的完成时刻estimateEndTime`,于是可得出以下几个公式：  
&emsp; &emsp; estimateEndTime=estimatedRunTime+taskStartTime  
&emsp; &emsp; estimatedRunTime=(currentTimestamp-taskStartTime)/progress  
&emsp; &emsp; estimateEndTime`= currentTimestamp+averageRunTime  
&emsp; 其中，currentTimestamp为当前时刻；taskStartTime为该任务的启动时刻；averageRunTime为已经成功运行完成的任务的平均运行时间。这样，MRv2总是选择（estimateEndTime- estimateEndTime·）差值最大的任务，并为之启动备份任务。为了防止大量任务同时启动备份任务造成的资源浪费，MRv2为每个作业设置了同时启动的备份任务数目上限。  
&emsp; 推测执行机制实际上采用了经典的算法优化方法：以空间换时间，它同时启动多个相同任务处理相同的数据，并让这些任务竞争以缩短数据处理时间。显然，这种方法需要占用更多的计算资源。在集群资源紧缺的情况下，应合理使用该机制，争取在多用少量资源的情况下，减少作业的计算时间。  

## Hadoop面试题总结（五）——优化问题

### 1、MapReduce跑得慢的原因？（**☆☆☆☆☆**）
Mapreduce 程序效率的瓶颈在于两点：  
1）计算机性能  
&emsp; CPU、内存、磁盘健康、网络  
2）I/O 操作优化  
&emsp; （1）数据倾斜  
&emsp; （2）map和reduce数设置不合理  
&emsp; （3）reduce等待过久  
&emsp; （4）小文件过多   
&emsp; （5）大量的不可分块的超大文件   
&emsp; （6）spill次数过多  
&emsp; （7）merge次数过多等

### 2、MapReduce优化方法（☆☆☆☆☆）
1）数据输入  
&emsp; （1）合并小文件：在执行mr任务前将小文件进行合并，大量的小文件会产生大量的map任务，增大map任务装载次数，而任务的装载比较耗时，从而导致mr运行较慢。   
&emsp; （2）采用ConbinFileInputFormat来作为输入，解决输入端大量小文件场景。  
2）map阶段  
&emsp; （1）减少spill次数：通过调整io.sort.mb及sort.spill.percent参数值，增大触发spill的内存上限，减少spill次数，从而减少磁盘 IO。   
&emsp; （2）减少merge次数：通过调整io.sort.factor参数，增大merge的文件数目，减少merge的次数，从而缩短mr处理时间。    
&emsp; （3）在 map 之后先进行combine处理，减少I/O。  
3）reduce阶段  
&emsp; （1）合理设置map和reduce数：两个都不能设置太少，也不能设置太多。太少，会导致task等待，延长处理时间；太多，会导致 map、reduce任务间竞争资源，造成处理超时等错误。   
&emsp; （2）设置map、reduce共存：调整slowstart.completedmaps参数，使map运行到一定程度后，reduce也开始运行，减少reduce的等待时间。  
&emsp; （3）规避使用reduce，因为Reduce在用于连接数据集的时候将会产生大量的网络消耗。  
&emsp; （4）合理设置reduce端的buffer，默认情况下，数据达到一个阈值的时候，buffer中的数据就会写入磁盘，然后reduce会从磁盘中获得所有的数据。也就是说，buffer和reduce是没有直接关联的，中间多个一个写磁盘->读磁盘的过程，既然有这个弊端，那么就可以通过参数来配置，使得buffer中的一部分数据可以直接输送到reduce，从而减少IO开销：mapred.job.reduce.input.buffer.percent，默认为0.0。当值大于0的时候，会保留指定比例的内存读buffer中的数据直接拿给reduce使用。这样一来，设置buffer需要内存，读取数据需要内存，reduce计算也要内存，所以要根据作业的运行情况进行调整。  
4）IO传输  
&emsp; （1）采用数据压缩的方式，减少网络IO的的时间。安装Snappy和LZOP压缩编码器。  
&emsp; （2）使用SequenceFile二进制文件  
5）数据倾斜问题  
&emsp; （1）数据倾斜现象
&emsp; &emsp; 数据频率倾斜——某一个区域的数据量要远远大于其他区域。  
&emsp; &emsp; 数据大小倾斜——部分记录的大小远远大于平均值。  
&emsp; （2）如何收集倾斜数据  
&emsp; &emsp; 在reduce方法中加入记录map输出键的详细情况的功能。
```java
public static final String MAX_VALUES = "skew.maxvalues";
private int maxValueThreshold;

@Override
public void configure(JobConf job) {
     maxValueThreshold = job.getInt(MAX_VALUES, 100);
}

@Override
public void reduce(Text key, Iterator<Text> values,
                     OutputCollector<Text, Text> output,
                     Reporter reporter) throws IOException {
     int i = 0;
     while (values.hasNext()) {
         values.next();
         i++;
     }
     if (++i > maxValueThreshold) {
         log.info("Received " + i + " values for key " + key);
     }
}
```
&emsp; （3）减少数据倾斜的方法  
&emsp; &emsp; 方法1：抽样和范围分区  
&emsp; &emsp; &emsp; 可以通过对原始数据进行抽样得到的结果集来预设分区边界值。  
&emsp; &emsp; 方法2：自定义分区   
&emsp; &emsp; &emsp; 另一个抽样和范围分区的替代方案是基于输出键的背景知识进行自定义分区。例如，如果map输出键的单词来源于一本书。其中大部分必然是省略词（stopword）。那么就可以将自定义分区将这部分省略词发送给固定的一部分reduce实例。而将其他的都发送给剩余的reduce实例。  
&emsp; &emsp; 方法3：Combine  
&emsp; &emsp; &emsp; 使用Combine可以大量地减小数据频率倾斜和数据大小倾斜。在可能的情况下，combine的目的就是聚合并精简数据。

### 3、HDFS小文件优化方法（☆☆☆☆☆）
1）HDFS小文件弊端：  
&emsp; HDFS上每个文件都要在namenode上建立一个索引，这个索引的大小约为150byte，这样当小文件比较多的时候，就会产生很多的索引文件，一方面会大量占用namenode的内存空间，另一方面就是索引文件过大是的索引速度变慢。   
2）解决的方式：   
&emsp; （1）Hadoop本身提供了一些文件压缩的方案。
&emsp; （2）从系统层面改变现有HDFS存在的问题，其实主要还是小文件的合并，然后建立比较快速的索引。  
3）Hadoop自带小文件解决方案  
&emsp; （1）Hadoop Archive：  
&emsp; &emsp; 是一个高效地将小文件放入HDFS块中的文件存档工具，它能够将多个小文件打包成一个HAR文件，这样在减少namenode内存使用的同时。   
&emsp; （2）Sequence file：  
&emsp; &emsp; sequence file由一系列的二进制key/value组成，如果为key小文件名，value为文件内容，则可以将大批小文件合并成一个大文件。   
&emsp; （3）CombineFileInputFormat：  
&emsp; &emsp; CombineFileInputFormat是一种新的inputformat，用于将多个文件合并成一个单独的split，另外，它会考虑数据的存储位置。  



# 链接
- https://github.com/MoRan1607/BigDataGuide