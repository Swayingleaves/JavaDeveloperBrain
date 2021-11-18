
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
- 可以缓存hash值
  - 因为 String 的 hash 值经常被使用，例如 String 用做 HashMap 的 key。不可变的特性可以使得 hash 值也不可变， 因此只需要进行一次计算
  - 理解final关键字的作用
- String Pool 的需要
  - 如果一个 String 对象已经被创建过了，那么就会从 String Pool 中取得引用。只有 String 是不可变的，才可能使用String Pool。
- 安全性
- 线程安全
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
String s2 = new String("aaa"); System.out.println(s1 == s2); // false 
String s3 = s1.intern(); 
String s4 = s1.intern(); System.out.println(s3 == s4); // true
如果是采用 "bbb" 这种字面量的形式创建字符串，会自动地将字符串放入 String Pool 中。
String s5 = "bbb"; 
String s6 = "bbb"; System.out.println(s5 == s6); // true
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
- 大量字符串操作使用他们
  - 操作少量的数据: 适用 String
  - 单线程操作字符串缓冲区下操作大量数据: 适用 StringBuilder
  - 多线程操作字符串缓冲区下操作大量数据: 适用 StringBuffer