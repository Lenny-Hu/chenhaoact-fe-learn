#HTTP1基础

#什么是http?
HTTP 是基于 **TCP/IP 协议的应用层协议**。它不涉及数据包（packet）传输，主要规定了客户端和服务器之间的通信格式。


##客户端是如何取得服务端的这些资源的？它们之间的通信是怎样的？

侧重讲讲三个过程：

**
1.TCP 连接： 浏览器与服务器三次握手，建立 TCP 连接
2.客户端请求： 建立 TCP 连接后，客户端就会向服务器发送一个 HTTP 请求信息（比如请求 HTML 资源，我们暂且就把这个称为“ HTML 请求”）
3.服务器响应： 服务器接收到请求后进行处理并发回一个 HTTP 响应信息
**

当然，接下来还有浏览器解析渲染的过程~巴拉巴拉~我们才能最终看到页面~~

参考：
[从输入URL到页面加载完的过程中都发生了什么事情](http://blog.aijc.net/server/2015/11/03/%E4%BB%8E%E8%BE%93%E5%85%A5URL%E5%88%B0%E9%A1%B5%E9%9D%A2%E5%8A%A0%E8%BD%BD%E5%AE%8C%E7%9A%84%E8%BF%87%E7%A8%8B%E4%B8%AD%E9%83%BD%E5%8F%91%E7%94%9F%E4%BA%86%E4%BB%80%E4%B9%88%E4%BA%8B%E6%83%85)

[从输入URL 到页面加载完成的过程中都发生了什么事情？ - FEX](http://fex.baidu.com/blog/2014/05/what-happen/)


#HTTP2
## 一 简介
HTTP 2.0 的出现，相比于 HTTP 1.x，**大幅提升了 web 性能**。在**与 HTTP/1.1 完全语义兼容**的基础上，进一步**减少了网络延迟**。而对于前端开发人员来说，一定程度上**减少了在前端方面的优化工作**。

例如：
同时请求 379 张图片，http1.1用14.7s，http2用1.61s，提升了超过10倍。

## 二 Http2优化与提升性能的方法
**多路复用** (Multiplexing)
允许同时通过单一的 HTTP/2 连接发起多重的请求-响应消息。

**二进制分帧 **
在不改动 HTTP/1.x 的语义、方法、状态码等的情况下, HTTP/2在 应用层(HTTP/2)和传输层(TCP or UDP)之间增加一个二进制分帧层，将所有传输的信息分割为更小的消息和帧（frame）,并对它们采用二进制格式的编码。以突破 HTTP1.1 的性能限制，改进传输性能，实现低延迟和高吞吐量


**在过去， HTTP 性能优化的关键并不在于高带宽，而是低延迟**。**HTTP/2** 通过让所有数据流共用同一个连接，可以更有效地使用 TCP 连接，**让高带宽也能真正的服务于 HTTP 的性能提升**。


**首部压缩（Header Compression） 
**HTTP/1.1并不支持 HTTP 首部压缩，为此 SPDY 和 HTTP/2 应运而生， SPDY 使用的是通用的DEFLATE 算法，而 **HTTP/2 则使用了专门为首部压缩而设计的 [HPACK 算法](http://http2.github.io/http2-spec/compression.html)**。

**服务端推送（Server Push）**
服务端推送是一种在**客户端请求之前发送数据的机制**。在 HTTP/2，服务器可对客户端的一个请求发送多个响应。Server Push 让 HTTP1.x 时代使用内嵌资源的优化手段变得没有意义；如果一个请求是由你的主页发起的，**服务器很可能会响应主页内容、logo 以及样式表，因为它知道客户端会用到这些东西**。这相当于在**一个 HTML 文档内集合了所有的资源**，不过与之相比，**服务器推送还有一个很大的优势：可以缓存！**也让在遵循同源的情况下，不同页面之间可以共享缓存资源成为可能。

参考自：
[知乎-HTTP/2.0 相比1.0有哪些重大改进？以及它的的大致内容是什么？](https://www.zhihu.com/question/34074946)


相关资源：
HTTP 协议入门 （阮一峰）
http://www.ruanyifeng.com/blog/2016/08/http.html

[Gitbook 《HTTP2 讲解》
](https://ye11ow.gitbooks.io/http2-explained/content/)

前端开发与 HTTP/2 的羁绊——安利篇
https://aotu.io/notes/2016/03/17/http2-char/

















