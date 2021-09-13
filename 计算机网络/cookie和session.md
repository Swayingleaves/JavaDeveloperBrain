
* [<a href="#">Cookie</a>](#cookie)
    * [<a href="#">Cookie是什么？</a>](#cookie是什么)
    * [<a href="#">创建cookie</a>](#创建cookie)
    * [<a href="#">cookie过期</a>](#cookie过期)
* [<a href="#">Session</a>](#session)
    * [<a href="#">session是什么</a>](#session是什么)
    * [<a href="#">session如何判断是否是同一会话</a>](#session如何判断是否是同一会话)
    * [<a href="#">session的缺点</a>](#session的缺点)
    * [<a href="#">禁用cookie后使用session</a>](#禁用cookie后使用session)


# [Cookie](#)
## [Cookie是什么？](#)
http协议里的cookie包含web cookie和浏览器cookie，他是服务器发送到web浏览器的一小块数据，服务器发送到浏览器的cookie，浏览器会进行存储，并与下一个请求一起发送到服务器，通常，他用于判断两个请求是否来自于同一个浏览器，例如用户保持登录状态
## [创建cookie](#)
当接受到客户端的HTTP请求后，服务器可以发送带有响应的set-cookie 标头，cookie通常由浏览器储存，然后cookie和http 请求头一同向服务器发出请求
## [cookie过期](#)
如果未指定到期时间，默认会话结束销毁，否则持久化到磁盘，到期删除
- expires
- max-age

# [Session](#)
## [session是什么](#)
客户端请求服务端，服务端会为这次请求开辟一块内存空间，这个对象便是Session对象，session弥补了HTTP无状态的特性，服务器可以利用session存储客户端在同一个会话期间的一些操作
## [session如何判断是否是同一会话](#)
- 开辟session空间后同时会生成sessionID，并通过响应头的set-cookie:  JSESSIONID=xxx命令 向客户端发送要求设置cookie的响应，客户端收到响应后，在本机客户端设置一个JSESSIONID=xxx的cookie的信息，改cookie的过期时间为浏览器会话结束
- 后面客户端的每次请求头都带上cookie（包含该sessionid）服务器通过读取请求头里的cookie信息获取到sessionid
## [session的缺点](#)
a服务器储存了session后，服务做了负载均衡，此次访问被转发到服务b，但是服务B没有储存a 的session，会导致session的失效
- 可以把token储存Redis
## [禁用cookie后使用session](#)
在URL后加上sessionid
