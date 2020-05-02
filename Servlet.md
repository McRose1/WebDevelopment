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

`http://www.test.com/hello?key1=value1&key2=value2`

GET 方法是默认的从浏览器向 Web服务器传递信息的方法，它会产生一个很长的字符串，出现在浏览器的地址栏中。

如果要向服务器传递的是密码或其他的敏感信息，不要使用 GET 方法。

GET 方法有大小限制：请求字符串中最多只能有 1024 个字符。

### POST 方法
POST 方法打包信息的方式与 GET 方法基本相同，但是 POST 方法不是把信息作为 URL 中？字符后的文本字符串进行发送，而是把这些信息作为一个单独的消息。

消息以标准输出的形式传到后台程序，我们可以解析和使用这些标准输出。

- getParameter()：调用 request.getParameter() 方法来获取表单参数的值

### Servlet 读取 HTTP request header 的方法
通过 HttpServletRequest 对象：

| 方法 | 描述 |
| ----------- | ----------- |
| Cookie[] getCookies() | 返回一个数组，包含客户端发送该请求的所有的 Cookie 对象 |
| Enumeration getAttributeNames() | 返回一个枚举，包含提供给该请求可用的属性名称 |
| Enumeration getHeaderNames() | 返回一个枚举，包含在该请求中包含的所有的头名 |
| Enumeration getParameterNames() | 返回一个 String 对象的枚举，包含在该请求中包含的参数的名称 |
| HttpSession getSession() | 返回与该请求关联的当前 session 会话，或者如果请求没有 session 会话，则创建一个 |
| HttpSession getSession(boolean create) | 返回与该请求关联的当前 HttpSession，或者如果没有当前会话，且创建是真的，则返回一个新的 session 会话 |
| Locale getLocale() | 基于 Accept-Language 头，返回客户端接受内容的首选的区域设置 |
| Object getAttribute(String name) | 以对象形式返回已命名属性的值，如果没有给定名称的属性存在，则返回 null |
| ServletInputStream getInputStream() | 使用 ServletInputStream，以二进制数据形式检索请求的主体 |
| String getAuthType() | 返回用于保护 Servlet 的身份验证方案的名称，例如，"BASIC" 或 "SSL"，如果JSP没有受到保护则返回 null |
| String getCharacterEncoding() | 返回请求主体中使用的字符编码的名称 |
| String getContentType() | 返回请求主体的 MIME 类型，如果不知道类型则返回 null | 
| String getContextPath() | 返回指示请求上下文的请求 URI 部分 |
| String getHeader(String name) | 以字符串形式返回指定的请求头的值 |
| String getMethod() | 返回请求的 HTTP 方法的名称，例如，GET、POST 或 PUT |
| String getParameter(String name) | 以字符串形式返回请求参数的值，或者如果参数不存在则返回 null |
| String getPathInfo() | 当请求发出时，返回与客户端发送的 URL 相关的任何额外的路径信息 | 
| String getProtocol() | 返回请求协议的名称和版本 | 
| String getQueryString() | 返回包含在路径后的请求 URL 中的查询字符串 |
| String getRemoteAddr() | 返回发送请求的客户端的互联网协议（IP）地址 |
| String getRemoteHost() | 返回发送请求的客户端的完全限定名称 |
| String getRemoteUser() | 如果用户已通过身份验证，则返回发出请求的登录用户，或者如果用户未通过身份验证，则返回 null | 
| String getRequestURI() | 从协议名称直到 HTTP 请求的第一行的查询字符串中，返回该请求的 URL 的一部分 |
| String getRequestedSessionId() | 返回由客户端指定的 session 会话 ID | 
| String getServletPath() | 返回调用 JSP 的请求的 URL 的一部分 | 
| String[] getParameterValues(String name) | 返回一个字符串对象的数组，包含所有给定的请求参数的值，如果参数不存在则返回 null |
| boolean isSecure() | 返回一个布尔值，指示请求是否使用安全通道，如 HTTPS | 
| int getContentLength() | 以字节为单位返回请求主体的长度，并提供输入流，或者如果长度未知则返回 -1 | 
| int getIntHeader(String name) | 返回指定的请求头的值为一个 int 值 |
| int getServerPort() | 返回接收到这个请求的端口号 | 
| int getParameterMap() | 将参数封装成 Map 类型 | 

### Servlet 设置 HTTP response header 的方法
通过 HttpServletRequest 对象：

| 方法 | 描述 |
| ----------- | ----------- |
| String encodeRedirectURL(String url) | 为 sendRedirect 方法中使用的指定的 URL 进行编码，或者如果编码不是必需的，则返回 URL 未改变 |
| String encodeURL(String url) | 对包含 session 会话 ID 的指定 URL 进行编码，或者如果编码不是必需的，则返回 URL 未改变 |
| boolean containsHeader(String name) | 返回一个布尔值，指示是否已经设置已命名的响应报头 |
| boolean isCommitted() | 返回一个布尔值，指示响应是否已经提交 |
| void addCookie(Cookie cookie) | 把指定的 cookie 添加到响应 |
| void addDateHeader(String name, long date) | 添加一个带有给定的名称和日期值的响应报头 |
| void addHeader(String name, String value) | 基于 Accept-Language 头，返回客户端接受内容的首选的区域设置 |
| Object getAttribute(String name) | 添加一个带有给定的名称和值的响应报头 |
| void addIntHeader(String name, int value) | 添加一个带有给定的名称和整数值的响应报头 |
| void flushBuffer() | 强制任何在缓冲区中的内容被写入到客户端 |
| void reset() | 清除缓冲区中存在的任何数据，包括状态码和头 |
| void resetBuffer() | 清除响应中基础缓冲区的内容，不清除状态码和头 | 
| void sendError(int sc) | 使用指定的状态码发送错误响应到客户端，并清除缓冲区 |
| void sendError(int sc, String msg) | 使用指定的状态发送错误响应到客户端 |
| void sendRedirect(String location) | 使用指定的重定向位置 URL 发送临时重定向响应到客户端 |
| void setBufferSize(int size) | 为响应主体设置首选的缓冲区大小 |
| void setCharacterEncoding(String charset) | 设置被发送到客户端的响应的字符编码（MIME 字符集）例如，UTF-8 | 
| void setContentLength(int len) | 设置在 HTTP Servlet 响应中的内容主体的长度，该方法设置 HTTP Content-Length 头 | 
| void setContentType(String type) | 如果响应还未被提交，设置被发送到客户端的响应的内容类型 |
| void setDateHeader(String name, long date) | 设置一个带有给定的名称和日期值的响应报头 |
| void setHeader(String name, String value) | 设置一个带有给定的名称和值的响应报头 |
| void setIntHeader(String name, int value) | 设置一个带有给定的名称和整数值的响应报头 | 
| void setLocale(Locale loc) | 如果响应还未被提交，设置响应的区域 |
| void setStatus(int sc)| 为该响应设置状态码 |

## Servlet 数据库访问
进行数据库插入操作的时候使用 PreparedStatement 更好：
- 可以写动态参数化的查询；
- 比 Statement 更快；
- 可以防止 SQL 注入式攻击
```Java
//编写预处理 SQL 语句
String sql= "INSERT INTO websites1 VALUES(?,?,?,?,?)";

//实例化 PreparedStatement
PreparedStatement ps = conn.prepareStatement(sql);

//传入参数，这里的参数来自于一个带有表单的jsp文件，很容易实现
ps.setString(1, request.getParameter("id"));
ps.setString(2, request.getParameter("name"));
ps.setString(3, request.getParameter("url"));
ps.setString(4, request.getParameter("alexa"));
ps.setString(5, request.getParameter("country"));

//执行数据库更新操作，不需要SQL语句
ps.executeUpdate();
sql = "SELECT id, name, url FROM websites1";
ps = conn.prepareStatement(sql);

//获取查询结果
ResultSet rs = ps.executeQuery();
```










































