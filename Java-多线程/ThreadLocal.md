

* [ThreadLocal](#threadlocal)
  * [原理](#原理)
    * [线程局部变量](#线程局部变量)
    * [只在当前线程拥有，绝对的线程安全](#只在当前线程拥有绝对的线程安全)
    * [一个线程内可以存在多个 ThreadLocal 对象，所以其实是 ThreadLocal 内部维护了一个 Map](#一个线程内可以存在多个-threadlocal-对象所以其实是-threadlocal-内部维护了一个-map)
  * [源码分析](#源码分析)
    * [get](#get)
    * [set](#set)
  * [使用场景](#使用场景)
  * [手动释放ThreadLocal遗留存储?你怎么去设计/实现？](#手动释放threadlocal遗留存储你怎么去设计实现)
  * [弱引用导致内存泄漏，那为什么key不设置为强引用](#弱引用导致内存泄漏那为什么key不设置为强引用)
  * [线程执行结束后会不会自动清空Entry的value](#线程执行结束后会不会自动清空entry的value)
  * [threadlocal如果不remove，出问题了怎么补救？](#threadlocal如果不remove出问题了怎么补救)
  * [FastThreadLocal](#fastthreadlocal)
* [参考文章：](#参考文章)

# ThreadLocal
## 原理
#### 线程局部变量
#### 只在当前线程拥有，绝对的线程安全
#### 一个线程内可以存在多个 ThreadLocal 对象，所以其实是 ThreadLocal 内部维护了一个 Map
ThreadLocalMap
- ThreadLocalMap 解决 hash 冲突的方式采用的是线性探测法，如果发生冲突会继续寻找下一个空的位置
- 内存泄漏
  - Entry为弱引用实际上 ThreadLocalMap 中使用的 key 为 ThreadLocal 的弱引用，弱引用的特点是，如果这个对象只存在弱引用，那么在下一次垃圾回收的时候必然会被清理掉。
  - 所以如果 ThreadLocal 没有被外部强引用的情况下，在垃圾回收的时候会被清理掉的，这样一来 ThreadLocalMap中使用这个 ThreadLocal 的 key 也会被清理掉。但是，value 是强引用，不会被清理，这样一来就会出现 key 为 null 的 value
  - 一定要remove

## 源码分析
### get
先获取当前线程，然后获取当前线程中的ThreadLocalMap，然后以当前的ThreadLocal为key，到ThreadLocalMap中获取value
```java
public T get() {
    Thread t = Thread.currentThread();
    ThreadLocalMap map = getMap(t);
    if (map != null) {
        ThreadLocalMap.Entry e = map.getEntry(this);
        if (e != null) {
            @SuppressWarnings("unchecked")
            T result = (T)e.value;
            return result;
        }
    }
    return setInitialValue();
}
```
通过取模获取数组下标，如果没有冲突直接返回数据，否则同样出现遍历的情况
```java
private Entry getEntry(ThreadLocal<?> key) {
    int i = key.threadLocalHashCode & (table.length - 1);
    Entry e = table[i];
    if (e != null && e.get() == key)
        return e;
    else
        return getEntryAfterMiss(key, i, e);
}
```
```java
private Entry getEntryAfterMiss(ThreadLocal<?> key, int i, Entry e) {
    Entry[] tab = table;
    int len = tab.length;

    while (e != null) {
        ThreadLocal<?> k = e.get();
        if (k == key)
            return e;
        if (k == null)
            expungeStaleEntry(i);
        else
            i = nextIndex(i, len);
        e = tab[i];
    }
    return null;
}
```
### set
首先获取当前线程，然后获取当前线程中存储的threadLocals变量，此变量其实就是ThreadLocalMap，最后看此ThreadLocalMap是否为空，为空就创建一个新的Map，不为空则以当前的ThreadLocal为key，存储当前value
```java
public void set(T value) {
    Thread t = Thread.currentThread();
    ThreadLocalMap map = getMap(t);
    if (map != null)
        map.set(this, value);
    else
        createMap(t, value);
}
```
ThreadLocalMap内部使用一个数组来保存数据，类似HashMap；每个ThreadLocal在初始化的时候会分配一个threadLocalHashCode，然后和数组的长度进行取模操作，所以就会出现hash冲突的情况，在HashMap中处理冲突是使用数组+链表的方式，而在ThreadLocalMap中，可以看到直接使用nextIndex，进行遍历操作，明显性能更差
```java
private void set(ThreadLocal<?> key, Object value) {

    // We don't use a fast path as with get() because it is at
    // least as common to use set() to create new entries as
    // it is to replace existing ones, in which case, a fast
    // path would fail more often than not.

    Entry[] tab = table;
    int len = tab.length;
    int i = key.threadLocalHashCode & (len-1);

    for (Entry e = tab[i];
         e != null;
         e = tab[i = nextIndex(i, len)]) {
        ThreadLocal<?> k = e.get();

        if (k == key) {
            e.value = value;
            return;
        }

        if (k == null) {
            replaceStaleEntry(key, value, i);
            return;
        }
    }

    tab[i] = new Entry(key, value);
    int sz = ++size;
    if (!cleanSomeSlots(i, sz) && sz >= threshold)
        rehash();
}
```

```java
void createMap(Thread t, T firstValue) {
    t.threadLocals = new ThreadLocalMap(this, firstValue);
}
```

## 使用场景
1. 线程间数据隔离，各线程的 ThreadLocal 互不影响
2. 方便同一个线程使用某一对象，避免不必要的参数传递
3. 全链路追踪中的 traceId 或者流程引擎中上下文的传递一般采用 ThreadLocal
4. Spring 事务管理器采用了 ThreadLocal
5. Spring MVC 的 RequestContextHolder 的实现使用了 ThreadLocal

举例：
- 每个线程维护了一个“序列号”
  ```java
  public class SerialNum {
    // The next serial number to be assigned
    private static int nextSerialNum = 0;
  
    private static ThreadLocal serialNum = new ThreadLocal() {
      protected synchronized Object initialValue() {
        return new Integer(nextSerialNum++);
      }
    };
  
    public static int get() {
      return ((Integer) (serialNum.get())).intValue();
    }
  }
  ```
- Session的管理
  ```java
  private static final ThreadLocal threadSession = new ThreadLocal();  
    
  public static Session getSession() throws InfrastructureException {  
      Session s = (Session) threadSession.get();  
      try {  
          if (s == null) {  
              s = getSessionFactory().openSession();  
              threadSession.set(s);  
          }  
      } catch (HibernateException ex) {  
          throw new InfrastructureException(ex);  
      }  
      return s;  
  }  
  
  ```
- SimpleDateFormat
```java
import java.text.DateFormat;
import java.text.SimpleDateFormat;
 
public class DateUtils {
    public static final ThreadLocal<DateFormat> threadLocal = new ThreadLocal<DateFormat>(){
        @Override
        protected DateFormat initialValue() {
            return new SimpleDateFormat("yyyy-MM-dd");
        }
    };
}

DateUtils.df.get().format(new Date());
```

## 手动释放ThreadLocal遗留存储?你怎么去设计/实现？
包装其父类remove方法为静态方法，如果是spring项目， 可以借助于bean的声明周期， 在拦截器的afterCompletion阶段进行调用。

## 弱引用导致内存泄漏，那为什么key不设置为强引用

如果key设置为强引用， 当threadLocal实例释放后， threadLocal=null， 但是threadLocal会有强引用指向threadLocalMap，threadLocalMap.Entry又强引用threadLocal， 这样会导致threadLocal不能正常被GC回收。

弱引用虽然会引起内存泄漏， 但是也有set、get、remove方法操作对null key进行擦除的补救措施， 方案上略胜一筹。

## 线程执行结束后会不会自动清空Entry的value
事实上，当currentThread执行结束后， threadLocalMap变得不可达从而被回收，Entry等也就都被回收了，但这个环境就要求不对Thread进行复用，但是我们项目中经常会复用线程来提高性能， 所以currentThread一般不会处于终止状态。

## threadlocal如果不remove，出问题了怎么补救？
threadLocal和thread是绑定的，生命周期相同，那么，kill掉这个线程可以释放ThreadLocalMap

## FastThreadLocal
1. ThreadLocalMap是存放在Thread下面的，ThreadLocal作为key，所以多个线程操作同一个ThreadLocal其实就是在每个线程的ThreadLocalMap中插入的一条记录，不存在任何冲突问题；
2. ThreadLocalMap在解决冲突时，通过遍历的方式，非常影响性能；
3. FastThreadLocal通过其他方式解决冲突的问题，达到性能的优化

Netty中分别提供了FastThreadLocal和FastThreadLocalThread两个类，FastThreadLocalThread继承于Thread，下面同样对常用的set和get方法来进行源码分析：
```java
public final void set(V value) {
    if (value != InternalThreadLocalMap.UNSET) {
        set(InternalThreadLocalMap.get(), value);
    } else {
        remove();
    }
}

public final void set(InternalThreadLocalMap threadLocalMap, V value) {
    if (value != InternalThreadLocalMap.UNSET) {
        if (threadLocalMap.setIndexedVariable(index, value)) {
            addToVariablesToRemove(threadLocalMap, this);
        }
    } else {
        remove(threadLocalMap);
    }
}

```
此处首先对value进行判定是否为InternalThreadLocalMap.UNSET，然后同样使用了一个InternalThreadLocalMap用来存放数据：
```java
public static InternalThreadLocalMap get() {
        Thread thread = Thread.currentThread();
        if (thread instanceof FastThreadLocalThread) {
            return fastGet((FastThreadLocalThread) thread);
        } else {
        return slowGet();
        }
}

private static InternalThreadLocalMap fastGet(FastThreadLocalThread thread) {
        InternalThreadLocalMap threadLocalMap = thread.threadLocalMap();
        if (threadLocalMap == null) {
            thread.setThreadLocalMap(threadLocalMap = new InternalThreadLocalMap());
        }
        return threadLocalMap;
}

```
可以发现InternalThreadLocalMap同样存放在FastThreadLocalThread中，不同在于，不是使用ThreadLocal对应的hash值取模获取位置，而是直接使用FastThreadLocal的index属性，index在实例化时被初始化：
```java
private final int index;

public FastThreadLocal() {
    index = InternalThreadLocalMap.nextVariableIndex();
}

```
再进入nextVariableIndex方法中：
```java
static final AtomicInteger nextIndex = new AtomicInteger();
 
public static int nextVariableIndex() {
    int index = nextIndex.getAndIncrement();
    if (index < 0) {
        nextIndex.decrementAndGet();
        throw new IllegalStateException("too many thread-local indexed variables");
    }
    return index;
}

```
在InternalThreadLocalMap中存在一个静态的nextIndex对象，用来生成数组下标，因为是静态的，所以每个FastThreadLocal生成的index是连续的，再看一下InternalThreadLocalMap中是如何setIndexedVariable的：
```java
public boolean setIndexedVariable(int index, Object value) {
    Object[] lookup = indexedVariables;
    if (index < lookup.length) {
        Object oldValue = lookup[index];
        lookup[index] = value;
        return oldValue == UNSET;
    } else {
        expandIndexedVariableTableAndSet(index, value);
        return true;
    }
}

```
indexedVariables是一个对象数组，用来存放value；直接使用index作为数组下标进行存放；如果index大于数组长度，进行扩容；get方法直接通过FastThreadLocal中的index进行快速读取：
```java
public final V get(InternalThreadLocalMap threadLocalMap) {
    Object v = threadLocalMap.indexedVariable(index);
    if (v != InternalThreadLocalMap.UNSET) {
        return (V) v;
    }

    return initialize(threadLocalMap);
}

public Object indexedVariable(int index) {
    Object[] lookup = indexedVariables;
    return index < lookup.length? lookup[index] : UNSET;
}

```
直接通过下标进行读取，速度非常快；但是这样会有一个问题，可能会造成空间的浪费；
# 参考文章：
- https://www.pdai.tech/md/java/thread/java-thread-x-threadlocal.html#java-%E5%BC%80%E5%8F%91%E6%89%8B%E5%86%8C%E4%B8%AD%E6%8E%A8%E8%8D%90%E7%9A%84-threadlocal
- https://www.cnblogs.com/javazhiyin/p/11834121.html
- https://juejin.cn/post/6844903966363353101