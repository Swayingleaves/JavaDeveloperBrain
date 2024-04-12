
* [final](#final)
  * [不可变的原因](#不可变的原因)
* [储存数据](#储存数据)
* [string pool](#string-pool)
  * [new String("abc")会创建几个对象](#new-stringabc会创建几个对象)
  * [intern()](#intern)
  * [str1 + " a nice day"](#str1---a-nice-day)
  * ["a" + "b" + "c"](#a--b--c)
* [StringBuilder](#stringbuilder)
* [StringBuffer](#stringbuffer)

# final
## 不可变的原因
在Java中，String类型被设计成final的主要原因是为了保证字符串的不可变性。这意味着一旦一个字符串被创建，它的值就不能再被改变。这种不可变性带来了很多好处，例如：

- 线程安全：由于字符串是不可变的，所以在多线程环境下，不需要担心并发访问的问题。

- 缓存哈希值：由于字符串的哈希值是不可变的，所以可以在哈希表等数据结构中缓存字符串的哈希值，提高性能。

- 安全性：不可变的字符串可以防止在处理字符串时，因为修改字符串而导致的潜在安全问题，例如SQL注入攻击。

- 简化代码：由于字符串是不可变的，所以在编写代码时，不需要担心字符串值被改变的情况，这使得代码更加简单和可读。

此外，String类型作为Java中最常用的类型之一，设计成final还可以提高字符串的性能，因为编译器可以对字符串的操作进行一些优化，例如重复使用相同的字符串对象、避免创建新的字符串对象等。
# 储存数据
- Java8内部使用char数组储存数据
  - `private final char value[];`
- Java9后使用byte数组同时使用coder来标识使用哪种编码
  - `private final byte[] value;`
  - `private final byte coder;`
# string pool
### new String("abc")会创建几个对象
- 使用这种方式一共会创建两个字符串对象（前提是 String Pool 中还没有 "abc" 字符串对象）。
- "abc" 属于字符串字面量，因此编译时期会在 String Pool 中创建一个字符串对象，指向这个 "abc" 字符串字面量；
- 而使用 new 的方式会在堆中创建一个字符串对象。
### intern()
字符串常量池（String Pool）保存着所有字符串字面量（literal strings），这些字面量在编译时期就确定。不仅如此，还可以使用 String 的 intern() 方法在运行过程中将字符串添加到 String Pool 中。当一个字符串调用 intern() 方法时，如果 String Pool 中已经存在一个字符串和该字符串值相等（使用 equals() 方法 进行确定），那么就会返回 String Pool 中字符串的引用；否则，就会在 String Pool 中添加一个新的字符串，并返回这个新字符串的引用。
```
下面示例中，s1 和 s2 采用 new String() 的方式新建了两个不同字符串，而 s3 和 s4 是通过 s1.intern() 方法取得一
个字符串引用。intern() 首先把 s1 引用的字符串放到 String Pool 中，然后返回这个字符串引用。因此 s3 和 s4 引用
的是同一个字符串。
String s1 = new String("aaa"); 
String s2 = new String("aaa"); 
System.out.println(s1 == s2); // false
 
String s3 = s1.intern(); 
String s4 = s1.intern(); 
System.out.println(s3 == s4); // true

如果是采用 "bbb" 这种字面量的形式创建字符串，会自动地将字符串放入 String Pool 中。
String s5 = "bbb"; 
String s6 = "bbb"; 
System.out.println(s5 == s6); // true
```
### str1 + " a nice day"
- 编译为 new StringBuilder().append(str1).append(" a nice day");
- 但是如果str1被final修饰，此变量会在初始化时加载到常量池，所以会直接变为str1的值"value"+"a nice day"
### "a" + "b" + "c"
编译优化不会创建对象
# StringBuilder
- 可变 byte数组没有被final修饰
- 线程不安全
- 速度快
# StringBuffer
- 可变 byte数组没有被final修饰
- 线程安全
  - 方法被synchronized修饰
- 速度慢

大量字符串操作使用他们
  - 操作少量的数据: 适用 String
  - 单线程操作字符串缓冲区下操作大量数据: 适用 StringBuilder
  - 多线程操作字符串缓冲区下操作大量数据: 适用 StringBuffer

# String 的hashcode()方法
String也是遵守equals的标准的，也就是 s.equals(s1)为true，则s.hashCode()==s1.hashCode()也为true。此处并不关注eqauls方法，而是讲解 hashCode()方法，String.hashCode()有点意思，而且在面试中也可能被问到。先来看一下代码：
```java
public int hashCode() {
        int h = hash;
        if (h == 0 && value.length > 0) {
            char val[] = value;
            for (int i = 0; i < value.length; i++) {
                h = 31 * h + val[i];
            }
            hash = h;
        }
        return h;
    }
```
## 为什么要选31作为乘数呢？
从网上的资料来看，一般有如下两个原因：

- 31是一个不大不小的质数，是作为 hashCode 乘子的优选质数之一。另外一些相近的质数，比如37、41、43等等，也都是不错的选择。那么为啥偏偏选中了31呢？请看第二个原因。
- 31可以被 JVM 优化，31 * i = (i << 5) - i。

# 参考文章
- https://mp.weixin.qq.com/s?__biz=MzI2OTQ4OTQ1NQ==&mid=2247483956&idx=1&sn=1c19164967621fa5449a7830d006c8f9&scene=19#wechat_redirect