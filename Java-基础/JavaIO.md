* [文件io](#文件io)
  * [磁盘操作](#磁盘操作)
  * [字节流](#字节流)
  * [字符流](#字符流)
* [序列化](#序列化)
  * [什么是序列化](#什么是序列化)
  * [序列化的实现](#序列化的实现)
  * [案例](#案例)
  * [transient](#transient)
* [网络io](#网络io)
  * [InetAddress](#inetaddress)
  * [URL](#url)
  * [socket](#socket)
  * [特点](#特点)
* [NIO](#nio)
  * [什么是NIO](#什么是nio)
  * [流与块](#流与块)
  * [通道 Channel](#通道-channel)
  * [缓冲区Buffer](#缓冲区buffer)
  * [选择器 Selector](#选择器-selector)
    * [选择器](#选择器)
      * [什么是选择器](#什么是选择器)
    * [流程](#流程)
  * [NIO的bug](#nio的bug)
# 文件io
## 磁盘操作
```java
public static void listAllFiles(File dir){
    if(dir == null || !dir.exists()){
        return;
    }
    if (dir.isFile()){
        System.out.println(dir.getName());
        return;
    }
    for (File file : dir.listFiles()) {
        listAllFiles(file);
    }
}
```
## 字节流
可以处理任意类型的数据
```java
public static void copyFile(String src, String dist) throws IOException {
    FileInputStream in = new FileInputStream(src);
    FileOutputStream out = new FileOutputStream(dist);

    byte[] buffer = new byte[20 * 1024];
    int cnt;
    //read()最多读取buffer.length个字节
    //返回的是实际读取的个数
    //返回-1的时候表示读到eof，即文件尾
    while ((cnt = in.read(buffer, 0, buffer.length)) != -1) {
        out.write(buffer, 0, cnt);
    }
    in.close();
    out.close();
}
```
- inputStream
  - FileInputStream
- outputStream
  - FileOutputStream
## 字符流
- 只能处理字符类型的数据
```java
public static void readFileContent(String filePath) throws IOException {
    FileReader fileReader = new FileReader(filePath);
    BufferedReader bufferedReader = new BufferedReader(fileReader);
    String line;
    while ((line = bufferedReader.readLine()) != null) {
        System.out.println(line);
    }
    //装饰者模式使得BufferedReader 组合了一个Reader对象
    //在调用BufferedReader的close()方法时会去调用Reader的close()方法
    //因此只要一个close()即可
    bufferedReader.close();
}
```

- 编码与解码
  - 编码就是把字符转换为字节，而解码是把字节重新组合成字符。
- Reader
- InputStreamReader
实现从字节流解码成字符流
- Writer
- InputStreamWriter
实现字符流编码成为字节流

# 序列化
## 什么是序列化
- 序列化就是一种用来处理对象流的机制，将对象的内容进行流化。可以对流化后的对象进行读写操作，可以将流化后的对象传输于网络之间。序列化是为了解决在对象流读写操作时所引发的问题
- 方便存储和传输
- 序列化：`ObjectOutputStream.writeObject()`
- 反序列化：`ObjectInputStream.readObject()`
## 序列化的实现
将需要被序列化的类实现Serialize接口
## 案例
```java
private static class A implements Serializable{
    private int x;
    private String y;

    public A(int x, String y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public String toString() {
        return "A{" +
                "x=" + x +
                ", y='" + y + '\'' +
                '}';
    }
}

public static void main(String[] args) throws IOException, ClassNotFoundException {
    A a1= new A(123,"abc");
    String objectFile = "a1";

    ObjectOutputStream objectOutputStream = new ObjectOutputStream(new FileOutputStream(objectFile));
    objectOutputStream.writeObject(a1);
    objectOutputStream.close();

    ObjectInputStream objectInputStream = new ObjectInputStream(new FileInputStream(objectFile));
    A a2 = (A) objectInputStream.readObject();
    objectInputStream.close();
    System.out.println(a2);
}
```
```text
输出:
A{x=123, y='abc'}
```
## transient
- transient 关键字可以使一些属性不会被序列化
- ArrayList 中存储数据的数组 elementData 是用 transient 修饰的，因为这个数组是动态扩展的，并不是所有的空间都被使用，因此就不需要所有的内容都被序列化。通过重写序列化和反序列化方法，使得可以只序列化数组中有内容的那部分数据。
  - `private transient Object[] elementData;`

# 网络io
## InetAddress
用于表示网络上的硬件资源，即 IP 地址；
- InetAddress.getByName(String host);
- InetAddress.getByAddress(byte[] address);
## URL
案例
```java
public static void main(String[] args) throws IOException {
    URL url = new URL("http://www.baidu.com");
    //字节流
    InputStream is = url.openStream();
    //字符流
    InputStreamReader isr = new InputStreamReader(is, StandardCharsets.UTF_8);
    //提供缓存功能
    BufferedReader br = new BufferedReader(isr);
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
    br.close();
}
```
## socket
```java
public class IOServer {
    public static void main(String[] args) throws Exception {
        ServerSocket serverSocket = new ServerSocket(8000);
        //接收新线程
        new Thread(() -> {
            while (true) {
                try {
                    //1-阻塞方法获取新连接
                    Socket socket = serverSocket.accept();
                    //2-每一个新连接都创建一个线程，负责读取数据
                    new Thread(() -> {
                        try {
                            int len;
                            byte[] data = new byte[1024];
                            InputStream inputStream = socket.getInputStream();
                            //3-按字节流方式读取数据
                            while ((len = inputStream.read(data)) != -1) {
                                System.out.println(new String(data, 0, len));
                            }
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                    }).start();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }).start();
    }
}
```
![](../img/io/socket示意图.png)
## 特点
同步阻塞，一个线程只能处理一个请求，如果要处理多个请求需要开启多个线程

# NIO
## 什么是NIO
新的输入/输出 (NIO) 库是在 JDK 1.4 中引入的，弥补了原来的 I/O 的不足，提供了高速的、面向块的 I/O
## 流与块
I/O 与 NIO 最重要的区别是数据打包和传输的方式，I/O 以流的方式处理数据，而 NIO 以块的方式处理数据。
## 通道 Channel
- 是对原 I/O 包中的流的模拟，可以通过它读取和写入数据
- 特点
  - 通道与流的不同之处在于，流只能在一个方向上移动(一个流必须是 InputStream 或者 OutputStream 的子类)，而通道是双向的，可以用于读、写或者同时用于读写。
- 类型
  - FileChannel：从文件中读写数据；
  - DatagramChannel：通过 UDP 读写网络中数据；
  - SocketChannel：通过 TCP 读写网络中数据；
  - ServerSocketChannel：可以监听新进来的 TCP 连接，对每一个新进来的连接都会创建一个 SocketChannel。
## 缓冲区Buffer
- 发送给一个通道的所有数据都必须首先放到缓冲区中，同样地，从通道中读取的任何数据都要先读到缓冲区中。也就是说，不会直接对通道进行读写数据，而是要先经过缓冲区。
- 缓冲区实质上是一个数组，但它不仅仅是一个数组。缓冲区提供了对数据的结构化访问，而且还可以跟踪系统的读/写进程。
- 类型
  - ByteBuffer
  - CharBuffer
  - ShortBuffer
  - IntBuffer
  - LongBuffer
  - FloatBuffer
  - DoubleBuffer
- 缓冲区状态变量
  - capacity：最大容量；
  - position：当前已经读写的字节数；
    - 下一个要被读取或者写入的元素的索引
  - limit：还可以读写的字节数。
    - 缓冲区中第一个不能被读或者写的位置
- 状态变量的改变过程
  1. 新建一个大小为 8 个字节的缓冲区，此时 position 为 0，而 limit = capacity = 8。capacity 变量不会改变
     ![](../img/io/nio状态变量改变过程1.png)
  2. 从输入通道中读取 5 个字节数据写入缓冲区中，此时 position 为 5，limit 保持不变。
     ![](../img/io/nio状态变量改变过程2.png)
  3. 在将缓冲区的数据写到输出通道之前，需要先调用 flip() 方法，这个方法将 limit 设置为当前 position，并将position 设置为 0。
     ![](../img/io/nio状态变量改变过程3.png)
  4. 从缓冲区中取 4 个字节到输出缓冲中，此时 position 设为 4。
     ![](../img/io/nio状态变量改变过程4.png)
  5. 最后需要调用 clear() 方法来清空缓冲区，此时 position 和 limit 都被设置为最初位置。
     ![](../img/io/nio状态变量改变过程5.png)
- 文件 NIO 实例
```java
public static void fastCopy(String src, String dist) throws IOException {
    //获取源文件的输入字节流
    FileInputStream fin = new FileInputStream(src);
    //获取输入字节流的文件通道
    FileChannel fcin = fin.getChannel();
    //获取目标文件的输出字节流
    FileOutputStream fout = new FileOutputStream(dist);
    //获取输出字节流的文件通道
    FileChannel fcout = fout.getChannel();
    //为缓冲区分配1024字节
    ByteBuffer buffer = ByteBuffer.allocateDirect(1024);
    while (true) {
        //从输入通道中读取数据到缓冲区
        int r = fcin.read(buffer);
        //read()返回 -1 表示EOF
        if (r == -1) {
            break;
        }
        //切换读写
        buffer.flip();
        //把缓冲区的内容写入输出文件中
        fcout.write(buffer);
        //清空缓冲区
        buffer.clear();
    }
}
```
## 选择器 Selector
### 选择器
#### 什么是选择器
![](../img/io/nio选择器.png)
- NIO 常常被叫做非阻塞 IO，主要是因为 NIO 在网络通信中的非阻塞特性被广泛使用。
- NIO 实现了 IO 多路复用中的 Reactor 模型，一个线程 Thread 使用一个选择器 Selector 通过轮询的方式去监听多个通道 Channel 上的事件，从而让一个线程就可以处理多个事件。
- 通过配置监听的通道 Channel 为非阻塞，那么当 Channel 上的 IO 事件还未到达时，就不会进入阻塞状态一直等待，而是继续轮询其它 Channel，找到 IO 事件已经到达的 Channel 执行。
- 因为创建和切换线程的开销很大，因此使用一个线程来处理多个事件而不是一个线程处理一个事件，对于 IO 密集型的应用具有很好地性能。
- 应该注意的是，只有套接字 Channel 才能配置为非阻塞，而 FileChannel 不能，因为 FileChannel 配置非阻塞也没有意义。
### 流程
- 创建选择器
`Selector selector = Selector.open();`
- 将通道注册到选择器上
  ```
  ServerSocketChannel ssChannel = ServerSocketChannel.open();
  ssChannel.configureBlocking(false);
  ssChannel.register(selector, SelectionKey.OP_ACCEPT);
  ```
  - 事件
    - `SelectionKey.OP_CONNECT`
    - `SelectionKey.OP_ACCEPT`
    - `SelectionKey.OP_READ`
    - `SelectionKey.OP_WRITE`
- 监听事件
  `int num = selector.select();`
  - 它会一直阻塞直到有至少一个事件到达。
- 获取到达的事件
```java
Set<SelectionKey> keys = selector.selectedKets();
Iterator<SelectionKey> keyIterator = keys.iterator();
while(keyIterator.hasNext()){
    SelectionKey key = keyIterator.next();
    if(key.isAcceptable()){
        //....
    } else if (key.isReadable()){
        //....    
    }
    keyIterator.remove();
}
``` 
- 事件循环
  因为一次 select() 调用不能处理完所有的事件，并且服务器端有可能需要一直监听事件，因此服务器端处理事件的代码一般会放在一个死循环内。
```java
while(true){
    int num = selector.select();
    Set<SelectionKey> keys = selector.selectedKets();
    Iterator<SelectionKey> keyIterator = keys.iterator();
    while(keyIterator.hasNext()){
        SelectionKey key = keyIterator.next();
        if(key.isAcceptable()){
            //....
        } else if (key.isReadable()){
            //....    
        }
        keyIterator.remove();
    }    
}
```
- nio示例
```java
public class NIOServer {
    public static void main(String[] args) throws IOException {
        Selector selector = Selector.open();
        ServerSocketChannel ssChannel = ServerSocketChannel.open();
        ssChannel.configureBlocking(false);
        ssChannel.register(selector, SelectionKey.OP_ACCEPT);

        ServerSocket serverSocket = ssChannel.socket();
        InetSocketAddress address = new InetSocketAddress("127.0.0.1", 8888);
        serverSocket.bind(address);

        while (true) {
            selector.select();
            Set<SelectionKey> keys = selector.selectedKeys();
            Iterator<SelectionKey> keyIterator = keys.iterator();

            while (keyIterator.hasNext()) {
                SelectionKey key = keyIterator.next();

                if (key.isAcceptable()) {
                    ServerSocketChannel ssChannel1 = (ServerSocketChannel) key.channel();
                    //服务器会为每个新连接创建一个SocketChannel
                    SocketChannel sChannel = ssChannel1.accept();
                    sChannel.configureBlocking(false);

                    //这个新连接主要用于从客服端读取数据
                    sChannel.register(selector, SelectionKey.OP_READ);
                } else if (key.isReadable()) {
                    SocketChannel sChannel = (SocketChannel) key.channel();
                    System.out.println(readDataFromSocketChannel(sChannel));
                    sChannel.close();
                }
                keyIterator.remove();
            }
        }
    }

    private static String readDataFromSocketChannel(SocketChannel sChannel) throws IOException {
        ByteBuffer buffer = ByteBuffer.allocate(1024);
        StringBuilder data = new StringBuilder();
        while (true) {
            buffer.clear();
            int n = sChannel.read(buffer);
            if (n == -1) {
                break;
            }
            buffer.flip();
            int limit = buffer.limit();
            char[] dst = new char[limit];
            for (int i = 0; i < limit; i++) {
                dst[i] = (char) buffer.get(i);
            }
            data.append(dst);
            buffer.clear();
        }
        return data.toString();
    }
}
```
```java
public static class NIOClient{
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("127.0.0.1",8888);
        OutputStream out = socket.getOutputStream();
        String s = "hello world";
        out.write(s.getBytes(StandardCharsets.UTF_8));
        out.close();
    }
}
```
## NIO的bug
JDK NIO的BUG，例如臭名昭著的epoll bug，它会导致Selector空轮询，最终导致CPU 100%。官方声称在JDK1.6版本的update18修复了该问题，但是直到JDK1.7版本该问题仍旧存在，只不过该BUG发生概率降低了一些而已，它并没有被根本解决

**Selector BUG出现的原因**

因为poll和epoll对于突然中断的连接socket会对返回的eventSet事件集合置为EPOLLHUP或者EPOLLERR，eventSet事件集合发生了变化，这就导致Selector会被唤醒，唤醒后遍历，若Selector的轮询结果为空，也没有wakeup或新消息处理，则发生空轮询，CPU使用率100%，

**Netty的解决办法**
- 对Selector的select操作周期进行统计，每完成一次空的select操作进行一次计数，
- 若在某个周期内连续发生N次空轮询，则触发了epoll死循环bug。
- 重建Selector，判断是否是其他线程发起的重建请求，若不是则将原SocketChannel从旧的Selector上去除注册，重新注册到新的Selector上，并将原来的Selector关闭。
