HTTP协议
HTTP的特性
HTTP构建于TCP/IP协议之上，默认端口号是80
HTTP是无连接无状态的
HTTP报文
请求报文
HTTP 协议是以 ASCII 码传输，建立在 TCP/IP 协议之上的应用层规范。规范把 HTTP 请求分为三个部分：状态行、请求头、消息主体。类似于下面这样：

<method> <request-URL> <version>
<headers>

<entity-body>
HTTP定义了与服务器交互的不同方法，最基本的方法有4种，分别是GET，POST，PUT，DELETE。URL全称是资源描述符，我们可以这样认为：一个URL地址，它用于描述一个网络上的资源，而 HTTP 中的GET，POST，PUT，DELETE就对应着对这个资源的查，增，改，删4个操作（CRUD）。

GET用于信息获取，GET请求报文示例：
    GET /books/?sex=man&name=Professional HTTP/1.1
    Host: www.example.com
    User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
    Gecko/20050225 Firefox/1.0.1
    Connection: Keep-Alive
POST表示可能修改变服务器上的资源的请求。
    POST / HTTP/1.1
    Host: www.example.com
    User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
    Gecko/20050225 Firefox/1.0.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 40
    Connection: Keep-Alive

    sex=man&name=Professional  
举例，Chrome随便打开一个网页，就会看到HTTP报文，我们看到的被浏览器简化的及外国，我们点击view source即可查看原始报文：




响应报文
HTTP 响应与 HTTP 请求相似，HTTP响应也由3个部分构成，分别是：

状态行
响应头(Response Header)
响应正文
状态行由协议版本、数字形式的状态代码、及相应的状态描述，各元素之间以空格分隔。

常见的状态码有如下几种：

200 OK 客户端请求成功
301 Moved Permanently 请求永久重定向
302 Moved Temporarily 请求临时重定向
304 Not Modified 文件未修改，可以直接使用缓存的文件。
400 Bad Request 由于客户端请求有语法错误，不能被服务器所理解。
401 Unauthorized 请求未经授权。这个状态代码必须和WWW-Authenticate报头域一起使用
403 Forbidden 服务器收到请求，但是拒绝提供服务。服务器通常会在响应正文中给出不提供服务的原因
404 Not Found 请求的资源不存在，例如，输入了错误的URL
500 Internal Server Error 服务器发生不可预期的错误，导致无法完成客户端的请求。
503 Service Unavailable 服务器当前不能够处理客户端的请求，在一段时间之后，服务器可能会恢复正常。
下面是一个HTTP响应的例子：

HTTP/1.1 200 OK

Server:Apache Tomcat/5.0.12
Date:Mon,6Oct2003 13:23:42 GMT
Content-Length:112

<html>...
同样的可以在Chrome中查看原始报文和简化过的。



会话跟踪
什么是会话？客户端打开与服务器的连接发出请求到服务器响应客户端请求的全过程称之为会话。

什么是会话跟踪？。会话跟踪指的是对同一个用户对服务器的连续的请求和接受响应的监视。

为什么需要会话跟踪？浏览器与服务器之间的通信是通过HTTP协议进行通信的，而HTTP协议是”无状态”的协议，它不能保存客户的信息，即一次响应完成之后连接就断开了，下一次的请求需要重新连接，这样就需要判断是否是同一个用户，所以才有会话跟踪技术来实现这种要求。

会话跟踪常用的方法:

URL重写。URL(统一资源定位符)是Web上特定页面的地址，URL重写的技术就是在URL结尾添加一个附加数据以标识该会话,把会话ID通过URL的信息传递过去，以便在服务器端进行识别不同的用户。
隐藏表单域。将会话ID添加到HTML表单元素中提交到服务器，此表单元素并不在客户端显示
Cookie。Cookie是Web服务器发送给客户端的一小段信息，客户端请求时可以读取该信息发送到服务器端，进而进行用户的识别。对于客户端的每次请求，服务器都会将Cookie发送到客户端,在客户端可以进行保存,以便下次使用。客户端可以采用两种方式来保存这个Cookie对象，一种方式是保存在客户端内存中，称为临时Cookie，浏览器关闭后这个Cookie对象将消失。另外一种方式是保存在客户机的磁盘上，称为永久Cookie。以后客户端只要访问该网站，就会将这个Cookie再次发送到服务器上，前提是这个Cookie在有效期内，这样就实现了对客户的跟踪。Cookie是可以被禁止的。
Session。每一个用户都有一个不同的session，各个用户之间是不能共享的，是每个用户所独享的，在session中可以存放信息。在服务器端会创建一个session对象，产生一个sessionID来标识这个session对象，然后将这个sessionID放入到Cookie中发送到客户端，下一次访问时，sessionID会发送到服务器，在服务器端进行识别不同的用户。Session的实现依赖于Cookie，如果Cookie被禁用，那么session也将失效。（如果你熟悉requests，那么你肯定用到requests.session，和这里讲到的Session一致，常常用于需要登录才能采集的网站）
跨站攻击
CSRF（Cross-site request forgery，跨站请求伪造）

CSRF(XSRF) 顾名思义，是伪造请求，冒充用户在站内的正常操作。

例如，一论坛网站的发贴是通过 GET 请求访问，点击发贴之后 JS 把发贴内容拼接成目标 URL 并访问：

http://example.com/bbs/create_post.php?title=标题&content=内容
那么，我们只需要在论坛中发一帖，包含一链接：

http://example.com/bbs/create_post.php?title=我是脑残&content=哈哈
只要有用户点击了这个链接，那么他们的帐户就会在不知情的情况下发布了这一帖子。可能这只是个恶作剧，但是既然发贴的请求可以伪造，那么删帖、转帐、改密码、发邮件全都可以伪造。

如何防范 CSRF 攻击？可以注意以下几点：

关键操作只接受POST请求

验证码。CSRF攻击的过程，往往是在用户不知情的情况下构造网络请求。所以如果使用验证码，那么每次操作都需要用户进行互动，从而简单有效的防御了CSRF攻击。但是如果你在一个网站作出任何举动都要输入验证码会严重影响用户体验，所以验证码一般只出现在特殊操作里面，或者在注册时候使用。

检测 Referer。常见的互联网页面与页面之间是存在联系的，比如你在www.baidu.com应该是找不到通往www.google.com的链接的，再比如你在论坛留言，那么不管你留言后重定向到哪里去了，之前的那个网址一定会包含留言的输入框，这个之前的网址就会保留在新页面头文件的 Referer 中。通过检查Referer的值，我们就可以判断这个请求是合法的还是非法的，但是问题出在服务器不是任何时候都能接受到Referer的值，所以 Referer Check 一般用于监控 CSRF 攻击的发生，而不用来抵御攻击。

Token。目前主流的做法是使用 Token 抵御 CSRF 攻击。Token 使用原则：Token 要足够随机————只有这样才算不可预测；Token 是一次性的，即每次请求成功后要更新Token————这样可以增加攻击难度，增加预测难度；Token 要注意保密性————敏感操作使用 post，防止 Token 出现在 URL 中。注意：过滤用户输入的内容不能阻挡 csrf，我们需要做的是过滤请求的来源。

XSS（Cross Site Scripting，跨站脚本攻击）XSS 全称“跨站脚本”，是注入攻击的一种。其特点是不对服务器端造成任何伤害，而是通过一些正常的站内交互途径，例如发布评论，提交含有 JavaScript 的内容文本。这时服务器端如果没有过滤或转义掉这些脚本，作为内容发布到了页面上，其他用户访问这个页面的时候就会运行这些脚本。运行预期之外的脚本带来的后果有很多中，可能只是简单的恶作剧——一个关不掉的窗口：

while (true) {
    alert("你关不掉我~");
}
看到上面说的这些，你是不是非常熟悉，这和我们每天做的反爬虫很相似嘛。验证码、Referer、Token，每一点都需要注意，更细的我们以后再说。

实践
打开知乎首页，下拉，会出现一个叫session_token的参数，去探索，这个token带边什么意思，有什么作用，爬虫会需要它吗？

[HTTP协议](https://zhangslob.github.io/docs/network/HTTP/)



HTTP有哪些请求方法?#
GET
POST
HEAD
PUT
DELETE
PATCH
OPTIONS
HTTP常见的状态码有哪些?#
200 302 301 400 403 404 500 502 503

GET和POST的区别?#
GET用于获取数据
GET一般不发请求数据,参数通过URL Query
GET参数直接暴露在地址栏中
GET可以被保存,收藏
GET响应可以被缓存
GET是幂等的,POST是非幂等的
GET要注意URL长度限制 URL长度限制为4K/主要验证数据的准确性,包括分页
POST注意点 业务破坏性 是否进行清理 重复提交 服务端验证

Cookie和Session的区别?#
Cookie在客户端,可以被篡改
Session在服务段,不能被篡改
Token和Session的区别?#
Token是算法计算出来的,验证时通过算法计算进行验证
session实时维护在服务端
HTTP和HTTPS的区别?#
HTTPS= HTTP+SSL

安全
是否需要握手
是否免费
性能

[Python自动化测试面试题-接口篇](https://www.cnblogs.com/superhin/p/12616452.html)