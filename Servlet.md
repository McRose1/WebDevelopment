# Servlet 
处理请求（POST）和发送响应（GET）的过程是由一种叫做 Servlet 的程序来完成的，并且 Servlet 是为了解决实现动态页面而衍生的东西。

Servlet 为创建基于 web 的应用程序提供了基于组件、独立于平台的方法，可以不受 CGI（Common Gateway Interface, 公共网关接口） 程序的性能限制。

Servlet 有权限访问所有的 Java API，包括访问企业级数据库的 JDBC API

## B/S：浏览器/服务器

## Tomcat 和 Servlet 的关系
Tomcat 是 Web 应用服务器，是一个 Servlet/JSP 容器。Tomcat 作为 Servlet 容器，负责处理客户请求，把请求送给 Servlet，并将 Servlet 的响应传送给客户。

而 Servlet 是一种运行在支持 Java 语言的服务器上的组件

1. Tomcat 接收 http 请求文本并解析，然后封装成 HttpServletRequest 类型的 request 对象，所有的 HTTP 头数据可以通过 request 对象调用对应的方法查询到
2. Tomcat 同时会将要响应的信息封装为 HttpServletResponse 类型的 response 对象，通过设置 response 的属性就可以控制要输出到浏览器的内容，然后将 response 交给 Tomcat，Tomcat 就会将其变成响应文本的格式发送给浏览器

Java Servlet API 是 Servlet 容器（Tomcat）和 Servlet 之间的接口，它定义了 Servlet 的各种方法，还定义了 Servlet 容器传送给 Servlet 的对象类。

其中最重要的就是 ServletRequest 和 ServletResponse

## 如何编写 Servlet
 1. 创建自己的 Servlet 继承 HttpServlet，重写 doGet 和 doPost 方法
 2. 在 web.xml 配置该 Servlet，为了让浏览器发出的请求知道到达哪个 Servlet，也就是让 Tomcat 将封装好的的 request 找到对应的 Servlet 让其使用
 
 注意：Web3.0开始用 @WebServlet("/search") 代替以前的 web.xml中的 servlet 的 <servlet-mapping> 元素中 servlet 的配置

## Servlet 的生命周期
服务器启动时或者第一次请求该servlet时，就会初始化一个 Servlet 对象，最后服务器关闭时，才会销毁这个 Servlet 对象，执行 destory() 方法

## Servlet 表单数据
### GET 方法
GET 方法向页面请求发送已编码的用户信息。页面和已编码的信息中间用？字符分隔：

http://www.test.com/hello?key1=value1&key2=value2

GET 方法是默认的从浏览器向 Web服务器传递信息的方法，它会产生一个很长的字符串，出现在浏览器的地址栏中。

如果要向服务器传递的是密码或其他的敏感信息，不要使用 GET 方法。

GET 方法有大小限制：请求字符串中最多只能有 1024 个字符。

### POST 方法
POST 方法打包信息的方式与 GET 方法基本相同，但是 POST 方法不是把信息作为 URL 中？字符后的文本字符串进行发送，而是把这些信息作为一个单独的消息。

消息以标准输出的形式传到后台程序，我们可以解析和使用这些标准输出。

- getParameter()：调用 request.getParameter() 方法来获取表单参数的值

### Servlet 读取 HTTP header 的方法















