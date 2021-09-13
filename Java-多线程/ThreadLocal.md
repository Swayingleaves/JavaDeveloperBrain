
* [ThreadLocal](#threadlocal)
  * [原理](#原理)
    * [线程局部变量](#线程局部变量)
    * [只在当前线程拥有，绝对的线程安全](#只在当前线程拥有绝对的线程安全)
    * [一个线程内可以存在多个 ThreadLocal 对象，所以其实是 ThreadLocal 内部维护了一个 Map](#一个线程内可以存在多个-threadlocal-对象所以其实是-threadlocal-内部维护了一个-map)
  * [使用场景](#使用场景)


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

参考文章：
- https://www.pdai.tech/md/java/thread/java-thread-x-threadlocal.html#java-%E5%BC%80%E5%8F%91%E6%89%8B%E5%86%8C%E4%B8%AD%E6%8E%A8%E8%8D%90%E7%9A%84-threadlocal