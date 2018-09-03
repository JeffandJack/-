# 图解HTTP笔记
## WWW三项构建技术
1. HTML（HyperText Markup Lanaguage,超文本标记语言）。把SGML（Standard Generalized Markup Lanaguage,标记通用标记语言）作为页面的文本标记语言。
2. HTTP（HyperText Transfer Protocol,超文本传输协议）。作为文档传输协议。
3. URL（Uniform Resource Locator,统一资源定位符）。指定文档所在的地址。

## HTTP版本

## URI和URL
URI用字符串标识某一互联网资源，而URL表示资源的地点（互联网上所处的位置）。可见URL是URI的子集。
### URL
URL(Uniform Resource Locator,统一资源定位符)
### URI
URI(UUniform Resource Identifier,统一资源标识符)，就是由某个协议方案（指访问资源所使用的协议类型名称）表示的资源的定位标识符。
- Uniform 规定统一的格式可方便处理多种不同类型的资源，而不用根据上下文环境来识别资源指定的访问方式。另外，加入新增的协议方案（如http:或ftp:）也更容易
- Resource 资源的定义是“可标识的任何东西”。不仅是文档文件，图像或服务（例如当天的天气预报）等能够区别于其他类型的，全都可作为资源。另外，资源不仅可以是单一的，也可以是多数的集合体。
- Identifier 表示可标识的对象。也称为标识符。

## HTTP方法Method
|方法|说明|支持的HTTP协议版本|
|:---|:---|:---|
|GET|获取资源|1.0、1.1|
|POST|传输实体主体|1.0、1.1|
|PUT|传输文件|1.0、1.1|
|HEAD|获得报文首部|1.0、1.1|
|DELETE|删除文件|1.0、1.1|
|OPTION|询问支持的方法|1.1|
|TRACE|追踪路径|1.1|
|CONNECT|要求用隧道协议连接代理|1.1|
|LINK|建立和资源之间的联系|1.0|
|UNLINK|断开连接关系|1.0|

**注:LINK和UNLINK已被HTTP/1.1废弃，不再支持**

## HTTP是无状态协议
HTTP协议自身不对请求和响应之间的通信状态进行保存，即无状态（stateless）协议。但是可以引入Cookie技术管理状态。

## 持久连接
问题：HTTP协议的初始版本中，每进行一次HTTP通信就要断开一次TCP连接，当HTML文档中包含多种其他的资源时，每次的请求都会造成无谓的TCP连接建立和断开，增加通信量的开销。
解决办法：只要任意一段没有明确提出断开连接，则保持TCP连接状态，即HTTP Persistent Connections也称为HTTP keep-alive或HTTP connection reuse。
好处：
1. 减轻服务器端的负载。减少了TCP连接的重复建立和断开所造成的额外开销
2. 提高Web页面的显示速度。减少开销的时间可以使HTTP请求和响应能够更早地结束
**注：在HTTP/1.1中，所有的连接默认都是持久连接，但在HTTP/1.0内并未标准化**

## 管线化
持久化连接使得多数请求以管线化（pipelining）方式发送成为可能。以前发送请求后需要等待并收到响应后，才能发送下一个请求。
线化技术出现后，不用等待响应应亦可直接发送下一个请求，这样就能够做到同时并行发送多个请求。

## 使用Cookie的状态管理
Cookie技术通过在请求和响应的报文中写入Cookie信息来控制客户端的状态。
1. Cookie会根据从服务器端发送的响应报文内的Set-Cookie的首部字段信息，通知客户端保存Cookie。当下次客户端再往该服务器发送请求时，
客户端会自动在请求报文中加入Cookie值后发送出去。
2. 服务器端发现客户端发送过来的Cookie后，会去检查究竟是从哪一个客户端发来的连接请求，然后对比服务器上的记录，最后得到之前的状态信息。

## 术语说明
- HyperText 借助多文档之间相互关联形成的超文本
- WWW(World Wide Web,万维网)
借助多文档之间相互关联形成的超文本，连成可互相参阅的万维网。
- HTTP(HyperText Transfer Protocol,超文本传输协议) 文档传输协议
- HTML(HyperText Markup Lanaguage,超文本标记语言) 页面的文本标记语言
- MAC()
- CGI(Common Gateway Interface，通用网关接口)
- REST(Representational State Transfer,表征状态转移)
- SSL(Secure Sockets Layer,安全套接层)
- TLS(Transport Layer Security,传输层安全)
