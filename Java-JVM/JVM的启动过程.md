
* [JVM的启动过程](#jvm的启动过程)
    * [1、JVM的装入环境和配置](#1jvm的装入环境和配置)
    * [2、装载JVM](#2装载jvm)
    * [3、初始化JVM，获得本地调用接口](#3初始化jvm获得本地调用接口)
    * [4、运行Java程序](#4运行java程序)


# JVM的启动过程
## 1、JVM的装入环境和配置

在学习这个之前，我们需要了解一件事情，就是JDK和JRE的区别。

JDK是面向开发人员使用的SDK，它提供了Java的开发环境和运行环境，JDK中包含了JRE。

JRE是Java的运行环境，是面向所有Java程序的使用者，包括开发者。

JRE = 运行环境 = JVM。

如果安装了JDK，会发现电脑中有两套JRE，一套位于/Java/jre.../下，一套位于/Java/jdk.../jre下。那么问题来了，一台机器上有两套以上JRE，谁来决定运行那一套呢？这个任务就落到java.exe身上，java.exe的任务就是找到合适的JRE来运行java程序。

java.exe按照以下的顺序来选择JRE：

1、自己目录下有没有JRE

2、父目录下有没有JRE

3、查询注册表： HKEY_LOCAL_MACHINE\SOFTWARE\JavaSoft\Java Runtime Environment\"当前JRE版本号"\JavaHome

这几步的主要核心是为了找到JVM的绝对路径。


jvm.cfg的路径为：JRE路径\lib\"CPU架构"\jvm.fig

jvm.cfg的内容大致如下：


-client KNOWN
-server KNOWN
-hotspot ALIASED_TO -client
-classic WARN
-native ERROR
-green ERROR

KNOWN 表示存在 、IGNORE 表示不存在 、ALIASED_TO 表示给别的JVM去一个别名
WARN 表示不存在时找一个替代 、ERROR 表示不存在抛出异常

## 2、装载JVM
通过第一步找到JVM的路径后，Java.exe通过LoadJavaVM来装入JVM文件。
LoadLibrary装载JVM动态连接库，然后把JVM中的到处函数JNI_CreateJavaVM和JNI_GetDefaultJavaVMIntArgs 挂接到InvocationFunction 变量的CreateJavaVM和GetDafaultJavaVMInitArgs 函数指针变量上。JVM的装载工作完成。

## 3、初始化JVM，获得本地调用接口

调用InvocationFunction -> CreateJavaVM也就是JVM中JNI_CreateJavaVM方法获得JNIEnv结构的实例。

## 4、运行Java程序

JVM运行Java程序的方式有两种：jar包 与 Class

运行jar 的时候，Java.exe调用GetMainClassName函数，该函数先获得JNIEnv实例然后调用JarFileJNIEnv类中getManifest()，从其返回的Manifest对象中取getAttrebutes("Main-Class")的值，即jar 包中文件：META-INF/MANIFEST.MF指定的Main-Class的主类名作为运行的主类。之后main函数会调用Java.c中LoadClass方法装载该主类（使用JNIEnv实例的FindClass）。

运行Class的时候，main函数直接调用Java.c中的LoadClass方法装载该类。