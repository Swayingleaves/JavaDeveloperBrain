
* [equals](#equals)
* [hashcode](#hashcode)
* [toString](#tostring)
* [clone](#clone)
* [wait](#wait)
* [notify](#notify)
* [finalize](#finalize)
* [重写了equals后为什么要重写hashcode，如果不重写，会有什么影响](#重写了equals后为什么要重写hashcode如果不重写会有什么影响)

# equals
- 对于基本类型，== 判断两个值是否相等，基本类型没有 equals() 方法。
- 对于引用类型，== 判断两个变量是否引用同一个对象（即是否指向同一个内存地址），而 equals() 判断引用的对象是否等价(默认情况下，Object 类中的 equals() 方法与 == 相同，但许多类重写了这个方法，需要判断重写后的方法返回的内容来判断是否相同来判断对象是否相等)。
# hashcode
- hashCode() 返回散列值，而 equals() 是用来判断两个对象是否等价。等价的两个对象散列值一定相同，但是散列值相同的两个对象不一定等价。
- 在覆盖 equals() 方法时应当总是覆盖 hashCode() 方法，保证等价的两个对象散列值也相等。
  - 重写equals的一般步骤 
    - 检查两个对象是否为同一个对象，如果是，则返回true。 
    - 检查传入的对象是否为空，如果是，则返回false。 
    - 检查传入的对象是否与当前对象属于同一类，如果不是，则返回false。 
    - 将传入的对象转换成当前对象的类型。 
    - 比较两个对象的属性是否相等，如果都相等，则返回true，否则返回false。
- hashCode方法实际上必须要完成的一件事情就是，为该equals方法认定为相同的对象返回相同的哈希值
# toString
- 一般生成对象字符串
# clone
- 浅拷贝
- 引用一个对象，拷贝基本数据类型的值，引用类型只拷贝引用
- 深拷贝
- 引用不同对象，拷贝基本数据类型的值，引用类型创建新对象
# wait
- 挂起线程
# notify
- 唤醒线程
# finalize
- GC时调用，回收资源

# 重写了equals后为什么要重写hashcode，如果不重写，会有什么影响
- 每个覆盖了equals方法的类中，必须覆盖hashCode。如果不这么做，就违背了hashCode的通用约定。进而导致该类无法结合所以与散列的集合一起正常运作，这里指的是HashMap、HashSet、HashTable、ConcurrentHashMap。
  - hashcode源码注释中的大致意思是：当我们将equals方法重写后有必要将hashCode方法也重写，这样做才能保证不违背hashCode方法中“相同对象必须有相同哈希值”的约定
- 比如hashmap里的put操作就会判断key的hashcode是否相等，如果出现重写了equals但未重写hashcode，则可能出现这种情况：hashMap.put("k","v1")，hashMap.put("k":"v2")，而不是使用v2替换v1的值，这样我们的HashMap就乱套了