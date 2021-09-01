# CAS(Compare-and-Swap)
## 原理
- 实际上是使用了unsafe的CAS操作
- 用期望值去与内存地址的值判断是否相等，相等则用更新值替换，否则CAS等待
## 参数
compareAndSwapInt
- this 对象
- Offset 内存地址
- expect 旧的期望值
- update 新的值
## ABA问题
### 什么是ABA
如果一个变量初次读取的时候是 A 值，它的值被改成了 B，后来又被改回为 A
### 怎么解决
控制变量值的版本来保证 CAS 的正确性