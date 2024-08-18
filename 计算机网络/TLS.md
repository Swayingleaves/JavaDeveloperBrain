# TLS的建立流程
HTTPS协议其实就是HTTP over TSL，TSL(Transport Layer Security) 传输层安全协议是https协议的核心。

TSL可以理解为SSL (Secure Socket Layer)安全套接字层的后续版本。

TSL握手协议如下图所示

![TSL握手协议.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2FTSL%E6%8F%A1%E6%89%8B%E5%8D%8F%E8%AE%AE.png)

在建立TCP连接后，开始建立TLS连接。下面抓包分析TLS握手过程，抓包图片来源于传输层安全协议抓包分析之SSL/TLS (自己没抓到这么完整的包，只能搬运过来了，摔)

(1) client端发起握手请求，会向服务器发送一个ClientHello消息，该消息包括其所支持的SSL/TLS版本、Cipher Suite加密算法列表（告知服务器自己支持哪些加密算法）、sessionID、随机数等内容。

![ClientHello.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2FClientHello.png)

(2) 服务器收到请求后会向client端发送ServerHello消息，其中包括：

SSL/TLS版本；

session ID，因为是首次连接会新生成一个session id发给client；

Cipher Suite，sever端从Client Hello消息中的Cipher Suite加密算法列表中选择使用的加密算法；

Radmon 随机数。

![ServerHello.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2FServerHello.png)

(3) 经过ServerHello消息确定TLS协议版本和选择加密算法之后，就可以开始发送证书给client端了。证书中包含公钥、签名、证书机构等信息。

![cretificate.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2Fcretificate.png)

(4) 服务器向client发送ServerKeyExchange消息，消息中包含了服务器这边的EC Diffie-Hellman算法相关参数。此消息一般只在选择使用DHE 和DH_anon等加密算法组合时才会由服务器发出。

![ServerKeyExchange.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2FServerKeyExchange.png)

(5) server端发送ServerHelloDone消息，表明服务器端握手消息已经发送完成了。

![ServerHelloDone.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2FServerHelloDone.png)

(6) client端收到server发来的证书，会去验证证书，当认为证书可信之后，会向server发送ClientKeyExchange消息，消息中包含客户端这边的EC Diffie-Hellman算法相关参数，然后服务器和客户端都可根据接收到的对方参数和自身参数运算出Premaster secret，为生成会话密钥做准备。

![ClientKeyExchange.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2FClientKeyExchange.png)

(7) 此时client端和server端都可以根据之前通信内容计算出Master Secret（加密传输所使用的对称加密秘钥），client端通过发送此消息告知server端开始使用加密方式发送消息。

![ChangeCipherSpec.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2FChangeCipherSpec.png)

(8) 客户端使用之前握手过程中获得的服务器随机数、客户端随机数、Premaster secret计算生成会话密钥master secret，然后使用该会话密钥加密之前所有收发握手消息的Hash和MAC值，发送给服务器，以验证加密通信是否可用。服务器将使用相同的方法生成相同的会话密钥以解密此消息，校验其中的Hash和MAC值。

![finish.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2Ffinish.png)

(9) 服务器发送ChangeCipherSpec消息，通知客户端此消息以后服务器会以加密方式发送数据。

![ChangeCipherSpec2.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2FChangeCipherSpec2.png)

(10) sever端使用会话密钥加密（生成方式与客户端相同，使用握手过程中获得的服务器随机数、客户端随机数、Premaster secret计算生成）之前所有收发握手消息的Hash和MAC值，发送给客户端去校验。若客户端服务器都校验成功，握手阶段完成，双方将按照SSL记录协议的规范使用协商生成的会话密钥加密发送数据。

![finish2.png](..%2Fimg%2F%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%2Ftls%2Ffinish2.png)

# 参考文章
- https://www.cnblogs.com/snowater/p/7804889.html