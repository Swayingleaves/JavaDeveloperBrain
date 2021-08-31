# 原则
- 大多数的Java应用不需要进行JVM优化；
- 大多数导致GC问题的原因是代码层面的问题导致的（代码层面）；
- 上线之前，应先考虑将机器的JVM参数设置到最优；
- 减少创建对象的数量（代码层面）；
- 减少使用全局变量和大对象（代码层面）；
- 优先架构调优和代码调优，JVM优化是不得已的手段（代码、架构层面）；
- 分析GC情况优化代码比优化JVM参数更好（代码层面）；
# jvm调优
### JVM调优目标
- 延迟：GC低停顿和GC低频率；
- 低内存占用；
- 高吞吐量;
### 举例
- Heap 内存使用率 <= 70%;
- Old generation内存使用率<= 70%;
- avgpause <= 1秒;
- Full gc 次数0 或 avg pause interval >= 24小时 ;
### JVM调优的步骤
1. 分析GC日志及dump文件，判断是否需要优化，确定瓶颈问题点；
2. 确定JVM调优量化目标；
3. 确定JVM调优参数（根据历史JVM参数来调整）；
4. 依次调优内存、延迟、吞吐量等指标；
5. 对比观察调优前后的差异；
6. 不断的分析和调整，直到找到合适的JVM参数配置；
7. 找到最合适的参数，将这些参数应用到所有服务器，并进行后续跟踪。
### JVM参数解析及调优
- -Xmx4g –Xms4g –Xmn1200m –Xss512k -XX:NewRatio=4 -XX:SurvivorRatio=8 -XX:PermSize=100m -XX:MaxPermSize=256m -XX:MaxTenuringThreshold=15
- XX:+PrintGCDetails
  - -Xlog
- -Xmx4g：堆内存最大值为4GB。
- -Xms4g：初始化堆内存大小为4GB。
  - 初始化堆内存大小，默认为物理内存的1/64(小于1GB)。
- -Xmn1200m：设置年轻代大小为1200MB。增大年轻代后，将会减小年老代大小。此值对系统性能影响较大，Sun官方推荐配置为整个堆的3/8。
- -Xss512k：设置每个线程的堆栈大小。JDK5.0以后每个线程堆栈大小为1MB，以前每个线程堆栈大小为256K。应根据应用线程所需内存大小进行调整。在相同物理内存下，减小这个值能生成更多的线程。但是操作系统对一个进程内的线程数还是有限制的，不能无限生成，经验值在3000~5000左右。
- -XX:NewRatio=4：设置年轻代（包括Eden和两个Survivor区）与年老代的比值（除去持久代）。设置为4，则年轻代与年老代所占比值为1：4，年轻代占整个堆栈的1/5
- -XX:SurvivorRatio=8：设置年轻代中Eden区与Survivor区的大小比值。设置为8，则两个Survivor区与一个Eden区的比值为2:8，一个Survivor区占整个年轻代的1/10
- -XX:PermSize=100m：初始化永久代大小为100MB。
- -XX:MaxPermSize=256m：设置持久代大小为256MB。
- -XX:MaxTenuringThreshold=15：设置垃圾最大年龄。如果设置为0的话，则年轻代对象不经过Survivor区，直接进入年老代。对于年老代比较多的应用，可以提高效率。如果将此值设置为一个较大值，则年轻代对象会在Survivor区进行多次复制，这样可以增加对象再年轻代的存活时间，增加在年轻代即被回收的概论。
- -XX:MaxDirectMemorySize=1G：直接内存。报java.lang.OutOfMemoryError: Direct buffer memory异常可以上调这个值。
- -XX:+DisableExplicitGC：禁止运行期显式地调用System.gc()来触发fulll GC。
- -XX:ConcGCThreads=4：CMS垃圾回收器并行线程线，推荐值为CPU核心数。
- -XX:ParallelGCThreads=8：新生代并行收集器的线程数。
- 内存优化示例
  - java heap：参数-Xms和-Xmx，建议扩大至3-4倍FullGC后的老年代空间占用。
  - 永久代：-XX:PermSize和-XX:MaxPermSize，建议扩大至1.2-1.5倍FullGc后的永久带空间占用。
  - 新生代：-Xmn，建议扩大至1-1.5倍FullGC之后的老年代空间占用。
  - 老年代：2-3倍FullGC后的老年代空间占用。
- 延迟优化示例
  - 应用程序可接受的平均停滞时间: 此时间与测量的Minor
  - GC持续时间进行比较。可接受的Minor GC频率：Minor
  - GC的频率与可容忍的值进行比较。
  - 可接受的最大停顿时间:最大停顿时间与最差情况下FullGC的持续时间进行比较。
  - 可接受的最大停顿发生的频率：基本就是FullGC的频率。
  - 新生代空间越大，Minor GC的GC时间越长，频率越低。如果想减少其持续时长，就需要减少其空间大小。如果想减小其频率，就需要加大其空间大小。