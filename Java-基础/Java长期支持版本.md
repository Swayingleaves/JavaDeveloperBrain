* [Java8](#java8)
  * [Lambda表达式](#lambda表达式)
  * [函数式接口](#函数式接口)
  * [默认方法](#默认方法)
  * [方法引用](#方法引用)
  * [Stream API](#stream-api)
    * [Collections](#collections)
  * [Optional](#optional)
  * [Date Time API](#date-time-api)
  * [重复注解](#重复注解)
  * [Base64](#base64)
  * [JVM的新特性](#jvm的新特性)
* [Java11](#java11)
  * [增加了一系列好用的字符串处理方法](#增加了一系列好用的字符串处理方法)
  * [用于 Lambda 参数的局部变量语法](#用于-lambda-参数的局部变量语法)
  * [标准化HTTP Client](#标准化http-client)
  * [单个命令编译运行源代码](#单个命令编译运行源代码)
  * [ZGC](#zgc)
# Java8
## Lambda表达式
```java
语法格式:
(parameters) -> expression 或 (parameters) -> { statements;}
代码示例：
Arrays.asList("jay","Eason",""SHE).foreach((s) -> System.out.print(s));
```
允许把函数作为一个方法的参数（函数作为参数传递到方法中）
## 函数式接口
- @FunctionalInterface
```java
@FunctionalInterface
public interface Runnable{
    public abstract void run();
}
```
- 只有一个函数
## 默认方法
默认方法就是一个在接口里面有了一个实现的方法。它允许将新方法添加到接口，但不强制实现了该接口的类必须实现新的方法。
```java
public interface ISingerService{
    //默认方法
  default void sing(){
     System.out.printLn("唱歌");
  }
  void writeSong();
}

public class JaySingerServiceImpl implements ISingerService{
    @Override
    public void writeSong(){
      System.out.printLn("写了一首七里香");
    }
}
```
## 方法引用 
可以直接引用已有Java类或对象（实例）的方法或构造器。
```java
//利用函数式接口Consumer的accept方法实现打印,Lambda表达式如下
Consumer<String> consumer = x -> System.out.printLn(x);
consumer.accept("jay");
//引用PrintStream类（也就是System.out的类型）的printLn方法，这就是方法引用
consumer = System.out::println;
consumer.accept("sss");
```
## Stream API 
### Collections
- filter 筛选
- map流映射
- reduce 将流中的元素组合起来
- collect 返回集合
- sorted 排序
- flatMap 流转换
- limit返回指定流个数
- distinct去除重复元素
## Optional
用来解决NullPointerException。Optional代替if...else解决空指针问题，使代码更加简洁。
## Date Time API
LocalDate /LocalDateTime
## 重复注解
重复注解，即一个注解可以在一个类、属性或者方法上同时使用多次；用@Repeatable定义重复注解

```java
import java.lang.annotation.Repeatable;

@Repeatable(ScheduleTimes.class)
public @interface ScheduleTime{
    String value();
}

public @interface ScheduleTimes{
  ScheduleTimes[] value();
}

public class ScheduleTimeTask{
    
    @ScheduleTime("10")
    @ScheduleTime("12")
    public void doSomething(){};
}
```
## Base64
Java 8把Base64编码的支持加入到官方库中~
- `String encoded = Base64.getEncoder().encodeToString(str.getBytes( StandardCharsets.UTF_8));`
- `String decoded = new String(Base64.getDecoder().decode(encoded), StandardCharsets.UTF_8);`
## JVM的新特性
使用元空间Metaspace代替持久代（PermGen space），JVM参数使用-XX:MetaSpaceSize和-XX:MaxMetaspaceSize设置大小。
# Java11
## 增加了一系列好用的字符串处理方法
- isBlank() 判空。
- strip() 去除首尾空格
- stripLeading() 去除字符串首部空格
- stripTrailing() 去除字符串尾部空格
- lines() 分割获取字符串流。
- repeat() 复制字符串
## 用于 Lambda 参数的局部变量语法
```java
var map = new HashMap<String,Object>();
map.put("aaa","aaa");
map.forEach((k,v)->{
    System.out.println(k+":"+v);    
})
```
## 标准化HTTP Client
Java 9 引入Http Client API,Java 10对它更新，Java 11 对它进行标准化。这几个版本后，Http Client几乎被完全重写，支持HTTP/1.1和HTTP/2 ，也支持 websockets。
## 单个命令编译运行源代码
- Java 11之前
  - // 编译 `javac Jay.java`
  - // 运行 `java Jay`
- Java 11之后 `java Jay.java`
## ZGC
可伸缩低延迟垃圾收集器
- GC 停顿时间不超过 10ms
- 既能处理几百 MB 的小堆，也能处理几个 TB 的大堆
- 应用吞吐能力不会下降超过 15%（与 G1 回收算法相比）
- 方便在此基础上引入新的 GC 特性和利用 colord
- 针以及 Load barriers 优化奠定基础
- 当前只支持 Linux/x64 位平台

# Java17

## 封闭类和接口（Sealed Classes and Interfaces, JEP 409）：

引入封闭类和接口，允许开发者限制哪些类可以扩展或实现它们。这有助于设计更可预测的类层次结构。

语法示例：
```java

public sealed class Shape permits Circle, Square { }
```

## 模式匹配 for switch (Pattern Matching for switch, Preview, JEP 406)：

扩展 switch 语句，以支持基于模式匹配的分支操作，这使得 switch 更加灵活和强大。

语法示例：
```java
switch (obj) {
  case Integer i -> System.out.println("Integer: " + i);
  case String s -> System.out.println("String: " + s);
  default -> System.out.println("Other: " + obj);
}
```
## 强度减少（Strong Encapsulation, JEP 403）：

更严格地限制模块化系统中的反射访问，使默认情况下不能通过反射访问模块的内部 API。
## 外部函数和内存 API (Foreign Function & Memory API, Incubator, JEP 412)：

引入新的 API，使 Java 程序能够安全、高效地调用非 Java 代码（如 C 函数），并操作非堆内存。
## 增强的伪随机数生成器（Enhanced Pseudo-Random Number Generators, JEP 356）：

增加了一组新的接口和实现，以提高伪随机数生成的灵活性和可扩展性。
## 弃用和移除：

永久删除 Applets，并移除 RMI Activation，这些旧的功能已经不再使用。

# Java21

## 结构化并发（Structured Concurrency, JEP 428）：

通过将多个任务作为单个结构化单元来管理，以简化多线程编程，增强可读性和可维护性。
## 模式匹配 for switch (Pattern Matching for switch, JEP 441)：

这是对 Java 17 中引入的模式匹配 switch 的正式化，在 Java 21 中已经成为标准功能。
## 记录模式（Record Patterns, JEP 440）：

扩展了模式匹配功能，使其能够匹配 Record 类型，方便解构和处理 Record 类的字段。
## 虚拟线程（Virtual Threads, JEP 444）：

引入了虚拟线程的概念，极大地简化了并发编程，使得创建和管理大量线程变得更加轻量级。
## String 模式匹配和增强（String Templates, JEP 430）：

新增了字符串模板功能，简化了字符串插值操作。
## 外部函数和内存 API (Foreign Function & Memory API, JEP 442)：

这项功能在 Java 17 中作为孵化器引入，而在 Java 21 中则被进一步增强和正式化。
## 垃圾收集器改进：

在垃圾收集器方面，特别是 ZGC 和 G1 等垃圾收集器，做了大量优化以提升性能和稳定性。
## 向量 API (Vector API, JEP 438)：

进一步改进和稳定，允许开发者利用向量化硬件加速批量计算任务